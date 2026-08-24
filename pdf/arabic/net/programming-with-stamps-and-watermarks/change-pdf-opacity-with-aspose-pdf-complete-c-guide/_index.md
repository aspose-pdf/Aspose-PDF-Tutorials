---
category: general
date: 2026-02-12
description: تعلم كيفية تغيير شفافية PDF باستخدام Aspose.PDF، حفظ PDF المعدل، ضبط
  شفافية التعبئة، وتعديل موارد PDF في دليل C# واحد.
draft: false
keywords:
- change pdf opacity
- save modified pdf
- set fill opacity
- edit pdf resources
language: ar
og_description: غيّر شفافية PDF فورًا، احفظ PDF المعدل، وحرّر موارد PDF باستخدام Aspose.PDF
  في C#. الكود الكامل والشرح.
og_title: تغيير شفافية PDF باستخدام Aspose.PDF – دليل C# الكامل
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: تغيير شفافية PDF باستخدام Aspose.PDF – دليل C# الكامل
url: /ar/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تغيير شفافية PDF – دليل عملي بلغة C#

هل احتجت يوماً إلى **تغيير شفافية PDF** لكنك لم تكن متأكدًا من أي استدعاء API تستخدم؟ لست وحدك؛ مواصفات PDF تخفي تعديلات حالة الرسومات خلف عدد قليل من القواميس التي نادراً ما يتعامل معها المطورون.  

في هذا الدليل سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح لك كيفية **تغيير شفافية PDF**، **حفظ PDF المعدل**، **تعيين شفافية التعبئة**، و**تحرير موارد PDF** باستخدام Aspose.PDF for .NET. في النهاية ستحصل على ملف واحد يمكنك إدراجه في أي مشروع والبدء في تعديل الشفافية فورًا.

## ما ستتعلمه

- فتح ملف PDF موجود والوصول إلى قاموس موارد الصفحة الأولى.  
- **تحرير موارد PDF** لإدخال إدخال ExtGState مخصص.  
- **تعيين شفافية التعبئة** (وشفافية الحد) مع وضعية دمج.  
- **حفظ PDF المعدل** مع الحفاظ على التخطيط الأصلي.  

بدون أدوات خارجية، بدون كتابة صريحة لصيغة PDF—فقط كود C# نظيف وتوضيحات واضحة. معرفة أساسية بـ C# وVisual Studio كافية؛ حزمة Aspose.PDF NuGet هي الاعتماد الوحيد.

![change pdf opacity example](change-pdf-opacity.png "change pdf opacity example")

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6+ (أو .NET Framework 4.7.2+) | يدعم Aspose.PDF كلاهما؛ الإصدارات الأحدث توفر أداءً أفضل. |
| Aspose.PDF for .NET (NuGet) | يوفر الفئات `Document`، `CosPdfDictionary`، وغيرها التي سنستخدمها. |
| ملف PDF إدخال (`input.pdf`) | الملف الذي تريد تعديله؛ احفظه في مجلد معروف. |

> **نصيحة احترافية:** إذا لم يكن لديك ملف PDF تجريبي، أنشئ ملفًا من صفحة واحدة باستخدام أي أداة إنشاء PDF—ستتعامل معه Aspose.PDF بسهولة.

---

## الخطوة 1: فتح PDF والوصول إلى موارده

الخطوة الأولى هي فتح ملف PDF المصدر والحصول على قاموس موارد الصفحة التي تريد تعديلها. في معظم الحالات تكون الصفحة 1.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.DataEditor;
using Aspose.Pdf.Cos;

class PdfOpacityDemo
{
    static void Main()
    {
        // Step 1 – Load the PDF you want to edit
        var inputPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(inputPath);

        // Grab the first page (Aspose pages are 1‑based)
        var firstPage = pdfDocument.Pages[1];

        // Create a helper that lets us edit the page’s resource dictionary
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**لماذا يهم ذلك:**  
فتح المستند يمنحنا نموذج كائن حي. يحتوي قاموس `Resources` على كل شيء من الخطوط إلى حالات الرسومات. من خلال تغليفه بـ `DictionaryEditor` نحصل على طريقة مريحة لقراءة أو إنشاء إدخالات مثل `ExtGState`.

---

## الخطوة 2: تحديد (أو إنشاء) قاموس ExtGState

`ExtGState` هو المفتاح في PDF الذي يخزن كائنات حالة الرسومات، مثل الشفافية. إذا كان PDF يحتوي بالفعل على إدخال `ExtGState` سنعيد استخدامه؛ وإلا سننشئ قاموسًا جديدًا.

```csharp
        // Step 2 – Retrieve the existing ExtGState dictionary, or create a new one
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            // No ExtGState yet – create one and add it to the resources
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }
```

**لماذا يهم ذلك:**  
إذا حاولت إضافة حالة رسومات دون وجود حاوية `ExtGState`، سيتجاهل PDF ذلك. يضمن هذا الجزء وجود الحاوية، مما يجعل خطوة **تحرير موارد PDF** لاحقًا آمنة.

---

## الخطوة 3: بناء حالة رسومات مخصصة – تعيين شفافية التعبئة

الآن نحدد قيم الشفافية الفعلية. تستخدم مواصفات PDF مفتاحين: `ca` لشفافية التعبئة و`CA` لشفافية الحد. سنحدد أيضًا وضعية دمج (`BM`) حتى تتصرف الأجزاء الشفافة كما هو متوقع.

```csharp
        // Step 3 – Create a new graphics state with desired opacity and blend mode
        var customGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        // Stroke opacity (CA) – fully opaque (1.0)
        customGraphicsState.Add("CA", new CosPdfNumber(1));

        // Fill opacity (ca) – 50 % transparent
        customGraphicsState.Add("ca", new CosPdfNumber(0.5));

        // Blend mode – Normal is the most common; you can try Multiply, Screen, etc.
        customGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**لماذا يهم ذلك:**  
مفتاح **تعيين شفافية التعبئة** (`ca`) يتحكم مباشرةً في كيفية عرض أي شكل مملوء (نص، صور، مسارات). بزوجه مع وضعية دمج تتجنب حدوث تشوهات بصرية غير متوقعة عند عرض PDF على منصات مختلفة.

---

## الخطوة 4: حقن حالة الرسومات في ExtGState

نضيف الآن حالة الرسومات التي أنشأناها إلى قاموس `ExtGState` تحت اسم فريد، مثل `GS0`. يمكن أن يكون الاسم أي شيء تريده، طالما لا يتصادم مع الإدخالات الموجودة.

```csharp
        // Step 4 – Add the graphics state to the ExtGState dictionary
        // Choose a key that isn’t already used; “GS0” is a safe default.
        extGStateDict.Add("GS0", customGraphicsState);
```

**لماذا يهم ذلك:**  
بمجرد وجود الإدخال، يمكن لأي تدفق محتوى الإشارة إلى `GS0` لتطبيق إعدادات الشفافية. هذه هي الطريقة الأساسية التي نُـ **نغير بها شفافية PDF** دون تعديل المحتوى المرئي مباشرة.

---

## الخطوة 5: تطبيق حالة الرسومات على محتوى الصفحة (اختياري)

إذا أردت أن يستخدم كل كائن في الصفحة الشفافية الجديدة، يمكنك إضافة أمر في بداية تدفق محتوى الصفحة. هذه الخطوة اختيارية—إذا كنت تحتاج الحالة فقط للاستخدام لاحقًا، يمكنك التوقف بعد الخطوة 4.

```csharp
        // Optional – prepend the graphics state to the page’s content stream
        // This makes the whole page render with the new fill opacity.
        var content = firstPage.Contents[1];
        var opacityCommand = "/GS0 gs\n"; // “gs” applies the graphics state
        content.Stream = new CosPdfStream(pdfDocument);
        content.Stream.Add(new CosPdfString(opacityCommand));
        content.Stream.Add(content.Stream);
```

**لماذا يهم ذلك:**  
بدون حقن عامل `gs`، تظل حالة الرسومات موجودة في PDF لكنها غير مستخدمة. يوضح المقتطف أعلاه طريقة سريعة **لتغيير شفافية PDF** للصفحة بأكملها. للاستخدام الانتقائي يمكنك تعديل كائنات النص أو الصورة الفردية بدلاً من ذلك.

---

## الخطوة 6: حفظ PDF المعدل

أخيرًا، نقوم بتثبيت التغييرات. طريقة `Save` تكتب ملفًا جديدًا، تاركة الأصلي دون تعديل—تمامًا ما تحتاجه عندما تريد **حفظ PDF معدل** بأمان.

```csharp
        // Step 6 – Persist the changes to a new file
        var outputPath = @"YOUR_DIRECTORY\output.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF opacity changed and saved to: {outputPath}");
    }
}
```

تشغيل البرنامج ينتج `output.pdf` حيث تظهر تعبئة كل شكل في الصفحة 1 بنسبة شفافية 50 %. افتحه في Adobe Reader أو أي عارض PDF وسترى التأثير الشفاف.

---

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو كان PDF يحتوي بالفعل على `ExtGState` باسم “GS0”؟

إذا حدث تعارض في المفاتيح، سيطرح Aspose استثناءً. النهج الآمن هو توليد اسم فريد:

```csharp
string uniqueKey = "GS" + Guid.NewGuid().ToString("N");
extGStateDict.Add(uniqueKey, customGraphicsState);
```

### هل يمكنني تعيين قيم شفافية مختلفة لعدة صفحات؟

بالطبع. قم بالتكرار عبر `pdfDocument.Pages` وكرر الخطوات 2‑4 لكل موارد صفحات. تذكر أن تعطي كل صفحة اسم حالة رسومات خاص بها أو أعد استخدام نفس الاسم إذا كانت الشفافية متطابقة في جميع الصفحات.

### هل يعمل هذا مع PDF/A أو ملفات PDF المشفرة؟

بالنسبة لـ PDF/A، تعمل التقنية نفسها، لكن بعض المدققين قد يُشيرون إلى استخدام وضعيات دمج معينة. يجب فتح ملفات PDF المشفرة باستخدام كلمة المرور الصحيحة (`new Document(path, password)`)، وبعد ذلك تتصرف تغييرات الشفافية بنفس الطريقة.

### كيف أغير **شفافية الحد** بدلاً من تعبئة؟

قم بتعديل قيمة `CA` بدلاً من (أو بالإضافة إلى) `ca`. على سبيل المثال، `customGraphicsState.Add("CA", new CosPdfNumber(0.3));` يجعل الخطوط شفافة بنسبة 30 % بينما تبقى التعبئة غير شفافة.

---

## الخلاصة

غطينا كل ما تحتاجه لت **تغيير شفافية PDF** باستخدام Aspose.PDF: فتح المستند، **تحرير موارد PDF**، إنشاء حالة رسومات مخصصة، **تعيين شفافية التعبئة**، وأخيرًا **حفظ PDF معدل**. المقتطف الكامل أعلاه جاهز للنسخ‑اللصق، التجميع، والتنفيذ—بدون خطوات مخفية، بدون سكريبتات خارجية.

بعد ذلك، قد ترغب في استكشاف تعديلات حالة رسومات أكثر تقدمًا مثل **تعيين شفافية الحد**، **ضبط سمك الخط**، أو حتى **تطبيق صور قناع ناعم**. كل ذلك على بُعد بضعة إدخالات في القاموس، بفضل مرونة مواصفات PDF وواجهة Aspose.NET.

هل لديك حالة استخدام مختلفة—ربما تحتاج إلى **تحرير موارد PDF** لإضافة علامة مائية أو تغيير لون؟ النمط يبقى نفسه: حدد أو أنشئ القاموس المناسب، أضف أزواج المفتاح/القيمة، ثم احفظ. برمجة سعيدة، واستمتع بالتحكم الجديد في مظهر ملفات PDF!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}