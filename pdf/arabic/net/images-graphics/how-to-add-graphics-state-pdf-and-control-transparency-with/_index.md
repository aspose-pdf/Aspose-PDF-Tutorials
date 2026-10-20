---
category: general
date: 2026-09-05
description: تعلم كيفية إضافة حالة رسومية إلى ملف PDF باستخدام Aspose.PDF لتعيين الشفافية.
  يوضح هذا الدليل خطوة بخطوة أيضًا كيفية إضافة شفافية إلى PDF وتعديل شفافية PDF بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- how to add transparency pdf
- modify pdf transparency
language: ar
lastmod: 2026-09-05
og_description: إضافة حالة الرسومات إلى ملف PDF باستخدام Aspose.PDF. اتبع هذا الدليل
  لتتعلم كيفية إضافة شفافية إلى PDF وتعديل شفافية PDF في بضع أسطر من كود C#.
og_image_alt: Screenshot of C# code that adds graphics state pdf to a PDF document
og_title: إضافة حالة رسومية إلى PDF باستخدام Aspose.PDF – التحكم في الشفافية في C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to add graphics state pdf using Aspose.PDF to set transparency.
    This step‑by‑step guide also shows how to add transparency pdf and modify pdf
    transparency efficiently.
  headline: How to add graphics state pdf and control transparency with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- PDF graphics state
- PDF transparency
- C# PDF manipulation
title: كيفية إضافة حالة الرسومات في PDF والتحكم في الشفافية باستخدام Aspose.PDF
url: /ar/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة حالة رسومية PDF والتحكم في الشفافية باستخدام Aspose.PDF

إذا كنت بحاجة إلى **إضافة حالة رسومية PDF** إلى مستند موجود، يوضح لك هذا الدليل الخطوات الدقيقة. سترى كيفية إضافة شفافية PDF باستخدام Aspose.PDF لـ .NET، وكيفية تعديل شفافية PDF دون الإخلال بتنسيق الصفحة الأصلي.

في الأقسام التالية سنستعرض مثالًا كاملاً وقابلاً للتنفيذ، نشرح لماذا كل سطر مهم، ونناقش الأخطاء الشائعة. في النهاية ستتمكن من تضمين حالات رسومية مخصصة—مثل قيم ألفا للخط والملء—في أي صفحة PDF.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
* رخصة صالحة لـ Aspose.PDF for .NET أو مفتاح تقييم مؤقت
* Visual Studio 2022 (أو أي محرر C# تفضله)
* ملف PDF إدخال (`input.pdf`) تملك حقوق تعديلّه

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf`.

## الخطوة 1: تحميل مستند PDF

العملية الأولى هي فتح ملف PDF المصدر. تقوم Aspose.PDF بلف الملف في كائن `Document`، مما يمنحك الوصول إلى الصفحات والموارد والهياكل منخفضة المستوى في PDF.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.Xmp;

string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document inside a using block so resources are released automatically.
using (var doc = new Document(inputPath))
{
    // The rest of the code lives inside this block.
}
```

**لماذا هذا مهم:** فتح الملف باستخدام عبارة `using` يضمن إغلاق مقبض الملف حتى إذا حدث استثناء. كما يقوم كائن `Document` بتحميل جدول المراجع المتقاطع، مما يتيح لنا تعديل القواميس منخفضة المستوى لاحقًا.

## الخطوة 2: الوصول إلى قاموس موارد الصفحة الأولى

كل صفحة PDF لديها قاموس *Resources* يخزن الخطوط، XObjects، وحالات الرسوم (`ExtGState`). لإدخال حالة رسومية جديدة، نسترجع هذا القاموس أولاً.

```csharp
// Inside the using block
Page page = doc.Pages[1];                     // Get the first page (pages are 1‑based)
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

**لماذا هذا مهم:** `ExtGState` هو المفتاح الذي تُخزن تحته كائنات حالة الرسوم. إذا لم تحتوي الصفحة بعد على إدخال `ExtGState`، تقوم Aspose.PDF بإنشاء قاموس فارغ تلقائيًا، لذا يعمل الكود في الحالتين.

## الخطوة 3: إنشاء قاموس حالة رسومية جديد

يحدد قاموس حالة الرسوم كيفية سلوك عمليات الرسم. للشفافية نحتاج إلى `CA` (ألفا الخط)، `ca` (ألفا الملء)، واختياريًا وضع المزج (`BM`). يبني الكود أدناه ذلك القاموس.

```csharp
// Create an empty COS dictionary that will become our new graphics state.
CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);

// Define the entries we want: 1.0 stroke opacity, 0.5 fill opacity, Normal blend mode.
var entries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke alpha (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill alpha (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

foreach (var entry in entries)
{
    newGs.Add(entry);
}
```

**لماذا هذا مهم:**  
* `CA` يتحكم في شفافية المسارات المرسومة (الخطوط، الحدود).  
* `ca` يتحكم في شفافية الكائنات المملوءة (الأشكال، النص).  
* `BM` يحدد وضع المزج؛ “Normal” هو الأكثر شيوعًا ويعمل مع جميع عارضات PDF.

### حالة خاصة: عدم وجود إدخال `ExtGState`

إذا لم يحتوي `page.Resources` على قاموس `ExtGState`، فإن `dictEditor["ExtGState"]` يُعيد `null`. في هذه الحالة يمكنك إنشاءه يدويًا:

```csharp
if (extGState == null)
{
    extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
    dictEditor["ExtGState"] = extGState;
}
```

إضافة هذا الحماية تجعل الدرس قويًا للملفات PDF التي لم تستخدم حالة رسومية مخصصة من قبل.

## الخطوة 4: إضافة الحالة الرسومية الجديدة إلى قاموس الموارد

الآن نربط القاموس الذي تم إنشاؤه حديثًا باسم (مثلاً `GS0`). يمكن لتدفقات المحتوى الإشارة إلى هذا الاسم لتطبيق الشفافية المحددة.

```csharp
// Register the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);
```

**لماذا هذا مهم:** مشغلات محتوى PDF مثل `gs` تتحول إلى حالة رسومية مسماة. بإضافة `GS0`, يمكنك تمكين تدفقات المحتوى اللاحقة من استخدام ` /GS0 gs ` لتفعيل إعدادات الشفافية.

## الخطوة 5: (اختياري) تطبيق الحالة الرسومية على المحتوى الموجود

إذا كنت تريد أن تصبح العناصر الموجودة في الصفحة الحالية شفافة، يمكنك إضافة مشغل `gs` إلى بداية تدفق محتوى الصفحة. هذه الخطوة اختيارية لأن العديد من الحالات لا تحتاج إلا إلى الحالة الرسومية للكائنات المضافة حديثًا.

```csharp
// Prepend "GS0" graphics state to the page’s content
page.Contents.Insert(0, new OperatorGraphicsState("GS0"));
```

**لماذا هذا مهم:** بدون هذا السطر ستظل الصفحة تحتفظ بمظهرها الأصلي. إضافة المشغل تضمن أن كل ما يُرسم بعد المشغل يرث قيم الشفافية الجديدة.

## الخطوة 6: حفظ ملف PDF المعدل

أخيرًا، احفظ المستند المحدث إلى القرص. يمكنك استبدال الملف الأصلي أو الكتابة إلى موقع جديد.

```csharp
string outputPath = @"YOUR_DIRECTORY\output.pdf";
doc.Save(outputPath);
```

**لماذا هذا مهم:** `doc.Save` يسلّس جدول المراجع المتقاطع المعدل، قواميس الموارد، وأي تدفقات محتوى جديدة، مما ينتج ملف PDF صالح يمكن لأي عارض فتحه.

## مثال كامل يعمل

بدمج جميع الأجزاء معًا، إليك برنامجًا مستقلًا يمكنك نسخه، لصقه، وتشغيله.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Xmp;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Cos;

class AddGraphicsStateExample
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        using (var doc = new Document(inputPath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Access the first page's resource dictionary
            // -----------------------------------------------------------------
            Page page = doc.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary();

            // Ensure ExtGState exists
            if (extGState == null)
            {
                extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
                dictEditor["ExtGState"] = extGState;
            }

            // -----------------------------------------------------------------
            // 3️⃣ Create a new graphics state (transparency settings)
            // -----------------------------------------------------------------
            CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries) newGs.Add(entry);

            // -----------------------------------------------------------------
            // 4️⃣ Register the graphics state as "GS0"
            // -----------------------------------------------------------------
            extGState.Add("GS0", newGs);

            // -----------------------------------------------------------------
            // 5️⃣ (Optional) Apply the graphics state to existing content
            // -----------------------------------------------------------------
            page.Contents.Insert(0, new OperatorGraphicsState("GS0"));

            // -----------------------------------------------------------------
            // 6️⃣ Save the modified PDF
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved with new graphics state at: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

بعد تشغيل البرنامج، افتح `output.pdf` في Adobe Acrobat Reader أو أي عارض PDF. يجب أن تظهر أي أشكال مملوءة (مثل المستطيلات الملونة) في الصفحة الأولى بنسبة **شفافية 50 %**، بينما تظل الخطوط غير شفافة بالكامل. إذا أضفت مشغل `gs` الاختياري، فإن *كل* المحتوى الموجود في تلك الصفحة سي inherit نفس الشفافية.

## أسئلة شائعة وحلول المشكلات

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني إضافة أكثر من حالة رسومية واحدة؟** | نعم. أنشئ قواميس إضافية (مثل `GS1`، `GS2`) وأشر إليها باستخدام مشغلات `gs` مختلفة. |
| **ماذا لو كان ملف PDF يستخدم بالفعل اسمًا مثل `GS0`؟** | اختر اسمًا فريدًا (مثل `MyGS`) أو تحقق من المفاتيح الموجودة باستخدام `extGState.Keys`. |
| **هل يعمل هذا مع ملفات PDF المشفرة؟** | يجب فتح المستند باستخدام كلمة المرور الصحيحة. استخدم `new Document(inputPath, new LoadOptions { Password = "pwd" })`. |
| **هل ستؤثر التغييرات على صفحات أخرى؟** | لا. تُضاف الحالة الرسومية إلى موارد الصفحة التي تقوم بتحريرها. لتؤثر على جميع الصفحات، كرر العملية لكل صفحة أو أضف القاموس إلى موارد *مستوى المستند*. |
| **هل هناك تأثير على الأداء؟** | إضافة حالة رسومية واحدة لا تؤثر بشكل ملحوظ. قد تحتاج ملفات PDF الكبيرة ذات الصفحات العديدة إلى حلقة، لكن العملية تظل O(number of pages). |

## نصائح احترافية

* **إعادة استخدام حالات الرسوم:** إذا كنت بحاجة إلى نفس الشفافية على صفحات متعددة، أضف القاموس إلى موارد *المستند* (`doc.Resources`) وأشر إليه من كل صفحة. هذا يقلل من حجم الملف.
* **وضعيات المزج:** جرب قيم `BM` أخرى مثل `Multiply`، `Screen`، أو `Overlay` للحصول على تأثيرات إبداعية. لا يدعم جميع العارضين كل وضعية مزج، لذا اختبرها مع جمهورك المستهدف.
* **الاختبار:** قارن دائمًا بين ملفات PDF الأصلية والمعدلة جنبًا إلى جنب. استخدم أداة مقارنة يمكنها عرض PDFs (مثل `DiffPDF`) للتحقق من أن التغييرات التي حدثت هي فقط المطلوبة.

## الخطوات التالية

الآن بعد أن عرفت **كيفية إضافة شفافية PDF** و**تعديل شفافية PDF**، يمكنك استكشاف المواضيع ذات الصلة:

* **إضافة حالة رسومية PDF** لتأثيرات الطباعة الزائدة والنقطة النصفية
* **إدراج صور بشفافية مخصصة** باستخدام `ImageFragment` وحالة رسومية
* **معالجة دفعات** لعدة ملفات PDF في مجلد باستخدام التوازي لتحسين الإنتاجية
* **استخدام API عالي المستوى لـ Aspose.PDF** (`PdfSaveOptions`، `PdfPageEditor`) لتدفقات عمل أكثر تعقيدًا

لا تتردد في تجربة قيم ألفا مختلفة


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الشيفرة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إضافة شفافية إلى PDF باستخدام Aspose – دليل C# كامل](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [كيفية إضافة ختم نصي إلى PDF باستخدام Aspose.PDF .NET: دليل شامل](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [كيفية إضافة صور إلى PDFs باستخدام Aspose.PDF for .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}