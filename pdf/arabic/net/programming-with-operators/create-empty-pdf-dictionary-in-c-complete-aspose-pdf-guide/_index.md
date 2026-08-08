---
category: general
date: 2026-07-26
description: إنشاء قاموس PDF فارغ باستخدام Aspose.Pdf في C#. تعلم خطوة بخطوة كيفية
  إضافة حالة رسومية إلى قاموس ExtGState للتلاعب بملفات PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty pdf dictionary
- Aspose.Pdf
- ExtGState dictionary
- CosPdfDictionary
- PDF graphics state
- C# PDF manipulation
language: ar
lastmod: 2026-07-26
og_description: إنشاء قاموس PDF فارغ باستخدام Aspose.Pdf للغة C#. اتبع هذا الدليل
  العملي لتعديل حالات الرسومات في ملفات PDF الخاصة بك.
og_image_alt: Diagram showing how to create empty PDF dictionary with Aspose.Pdf in
  C#
og_title: إنشاء قاموس PDF فارغ في C# – دليل Aspose.Pdf الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: Create empty PDF dictionary with Aspose.Pdf in C#. Learn step‑by‑step
    how to add a graphics state to ExtGState dictionary for PDF manipulation.
  headline: Create Empty PDF Dictionary in C# – Complete Aspose.Pdf Guide
  type: TechArticle
tags:
- Aspose
- PDF
- C#
- GraphicsState
title: إنشاء قاموس PDF فارغ في C# – دليل Aspose.Pdf الكامل
url: /ar/net/programming-with-operators/create-empty-pdf-dictionary-in-c-complete-aspose-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء قاموس PDF فارغ في C# – دليل Aspose.Pdf الكامل

هل تساءلت يومًا كيف **create empty PDF dictionary** عند تعديل حالة رسومات PDF؟ لست وحدك — يواجه العديد من المطورين هذه المشكلة عند محاولة ضبط الشفافية أو أوضاع الدمج برمجيًا. في هذا الدرس سنستعرض حلاً عمليًا باستخدام Aspose.Pdf لـ C#، موضحين بالضبط كيفية إدخال حالة رسومات جديدة في قاموس *ExtGState* لملف PDF موجود.

سنتناول كل ما تحتاجه: تحميل ملف PDF، الوصول إلى قاموس الموارد الخاص به، بناء **CosPdfDictionary** جديد، وأخيرًا حفظ التغييرات. في النهاية ستحصل على نمط قابل لإعادة الاستخدام لأي تعديلات على *PDF graphics state* قد تحتاجها.

---

## ما ستتعلمه

- كيفية إنشاء كائنات **create empty PDF dictionary** باستخدام API منخفض المستوى لـ Aspose.Pdf.  
- دور **ExtGState dictionary** في التحكم في شفافية الخط/الملء وأوضاع الدمج.  
- نصائح عملية لتعامل مع ملفات PDF باستخدام C#، بما في ذلك معالجة الحالات الحدية عندما يكون القاموس مفقودًا.  
- عينة شفرة كاملة قابلة للتنفيذ يمكنك نسخها ولصقها في مشروعك.  

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+).  
- نسخة مرخصة من **Aspose.Pdf for .NET** (الإصدار التجريبي المجاني يعمل للاختبار).  
- إلمام أساسي بـ C# ومفاهيم PDF مثل الموارد وحالات الرسومات.  

إذا كان أي من ذلك غير مألوف لك، لا تقلق — يمكنك تثبيت Aspose.Pdf عبر NuGet (`Install-Package Aspose.Pdf`) والبقية مجرد C# عادي.

---

## الخطوة 1 – تحميل مستند PDF

أولًا، تحتاج إلى كائن `Document` يمثل الملف الذي تريد تحريره. تغليفه داخل كتلة `using` يضمن التخلص السليم.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;   // for low‑level PDF objects
using Aspose.Pdf.Text;        // if you need to add text later

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

*لماذا هذا مهم*: فتح الملف يمنحك الوصول إلى كائنات COS الداخلية (Canonical Object Structure)، حيث توجد **CosPdfDictionary**. بدون كائن المستند، لا يمكنك الوصول إلى قواميس الموارد التي تحتوي على مدخلات **ExtGState**.

---

## الخطوة 2 – الوصول إلى قاموس موارد الصفحة الأولى

صفحات PDF تخزن مواردها (الخطوط، الصور، حالات الرسومات، إلخ) في قاموس مخصص. سنختار الصفحة الأولى للبساطة، لكن نفس المنطق ينطبق على أي فهرس صفحة.

```csharp
// Step 2: Access the first page and its resource dictionary
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

*نصيحة احترافية*: إذا كان ملف PDF يحتوي على صفحات متعددة بمجموعات موارد مختلفة، كرّر هذا الجزء لكل صفحة تحتاج إلى تعديلها. فئة `DictionaryEditor` هي غلاف مريح يتيح لك التعامل مع قاموس COS كـ .NET `Dictionary<string, object>`.

---

## الخطوة 3 – استرجاع أو تهيئة قاموس ExtGState

قاموس **ExtGState** يحتوي على كائنات حالة رسومات مسماة (`GS0`, `GS1`, …). بعض ملفات PDF تحتويه بالفعل؛ البعض الآخر لا. سنسترجعه بأمان، وننشئ واحدًا فارغًا جديدًا إذا لزم الأمر.

```csharp
// Step 3: Get the existing ExtGState dictionary (or create it if missing)
CosPdfDictionary extGState;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGState = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and attach it to the resources
    extGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor.Add("ExtGState", extGState);
}
```

*لماذا نفعل ذلك*: محاولة إضافة حالة رسومات إلى **ExtGState dictionary** غير موجود سيؤدي إلى استثناء. هذا الفحص الوقائي يجعل الكود قويًا لأي ملف PDF مدخل.

---

## الخطوة 4 – بناء حالة رسومات جديدة باستخدام CosPdfDictionary

الآن يأتي جوهر الدرس: **إنشاء قاموس PDF فارغ** يحدد حالة رسومات مخصصة. سنحدد شفافية الخط (`CA`)، شفافية التعبئة (`ca`)، ووضع الدمج (`BM`). يمكنك إضافة المزيد من المدخلات لاحقًا — هذه مجرد مجموعة ابتدائية.

```csharp
// Step 4: Create a new graphics state dictionary with desired parameters
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the parameters we want
KeyValuePair<string, ICosPdfPrimitive>[] parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),        // Fill opacity (semi‑transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))      // Blend mode
};

// Populate the dictionary
foreach (var p in parameters)
{
    newGraphicsState.Add(p);
}
```

*شرح*:  
- `CA` و `ca` هما مفاتيح PDF قياسية تتحكم في شفافية الخط والملء على التوالي.  
- `BM` يحدد وضع الدمج؛ “Normal” هو الافتراضي لكن يمكنك استخدام “Multiply”، “Screen”، إلخ، حسب احتياجات التصميم.  
- باستخدام `CosPdfDictionary.CreateEmptyDictionary`، نحن **create empty PDF dictionary** كائنات نملأها لاحقًا بأزواج المفتاح/القيمة.

---

## الخطوة 5 – إدراج حالة الرسومات الجديدة في ExtGState

مع جاهزية حالة الرسومات، نضيفها ببساطة إلى **ExtGState dictionary** تحت اسم فريد (مثلاً `GS0`). إذا كنت تخطط لإضافة حالات متعددة، فقط زد اللاحقة.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary
extGState.Add("GS0", newGraphicsState);
```

*نصيحة*: قبل الإضافة، قد ترغب في التحقق مما إذا كان `GS0` موجودًا بالفعل لتجنب الكتابة فوقه. شرط سريع `if (!extGState.ContainsKey("GS0"))` ينجز المهمة.

---

## الخطوة 6 – حفظ ملف PDF المعدل

جميع التغييرات موجودة في الذاكرة حتى تقوم بحفظها. اختر مسار الإخراج المناسب لسير عملك.

```csharp
// Step 6: Save the modified PDF
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*النتيجة*: افتح `output.pdf` في أي عارض PDF، ثم افحص موارد الصفحة (مثلاً باستخدام أداة فحص PDF). سترى مدخلاً جديدًا تحت **ExtGState** يسمى `GS0` مع المعلمات التي حددناها.

---

## مثال كامل يعمل

بجمع كل شيء معًا، إليك البرنامج الكامل جاهز للنسخ واللصق:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Access first page resources
    Page firstPage = pdfDocument.Pages[1];
    DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

    // Ensure ExtGState dictionary exists
    CosPdfDictionary extGState;
    if (resourceEditor.ContainsKey("ExtGState"))
        extGState = resourceEditor["ExtGState"].ToCosPdfDictionary();
    else
    {
        extGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        resourceEditor.Add("ExtGState", extGState);
    }

    // Build new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };
    foreach (var p in parameters) newGraphicsState.Add(p);

    // Insert into ExtGState
    if (!extGState.ContainsKey("GS0"))
        extGState.Add("GS0", newGraphicsState);

    // Save result
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**الناتج المتوقع**: سيظهر `output.pdf` بنفس مظهر الملف الأصلي، لكن أي محتوى يشير لاحقًا إلى `GS0` (مثلاً عبر عامل `gs` في تدفق المحتوى) سيتبنى الشفافية ووضع الدمج المحددين. إذا لم يكن لديك مثل هذا المرجع بعد، يمكنك إضافته يدويًا أو عبر واجهات برمجة التطبيقات عالية المستوى لـ Aspose.

---

## الأسئلة المتكررة والحالات الحدية

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كان ملف PDF يحتوي بالفعل على مدخل `ExtGState` باسم `GS0`؟* | تحقق من `extGState.ContainsKey("GS0")` قبل الإضافة. إذا كان موجودًا، إما أن تكتب فوقه عمدًا (`extGState["GS0"] = newGraphicsState`) أو تختار اسمًا جديدًا مثل `GS1`. |
| *هل يمكنني إضافة المزيد من المعلمات، مثل عرض الخط (`LW`) أو نمط الشرط (`D`)?* | بالطبع. فقط قم بتمديد مصفوفة `parameters` بإضافة مدخلات `KeyValuePair<string, ICosPdfPrimitive>` إضافية. |
| *هل هذا النهج متوافق مع ملفات PDF المشفرة؟* | نعم، طالما أنك تزود كلمة المرور الصحيحة عند إنشاء كائن `Document` (`new Document(path, password)`). |
| *هل أحتاج إلى إغلاق المستند يدويًا؟* | عبارة `using` تعتني بالتخلص من الكائن، مما يضمن أيضًا تفريغ أي تغييرات معلقة. |
| *كيف يختلف هذا عن استخدام الفئة عالية المستوى `Graphics`؟* | واجهة برمجة التطبيقات عالية المستوى تُجرد القواميس الداخلية، وهو أمر ممتاز للمهام البسيطة. ومع ذلك، عندما تحتاج إلى تحكم دقيق في حالات الرسومات — مثل أوضاع الدمج المخصصة — يجب عليك العمل مع **CosPdfDictionary** منخفض المستوى، أي كائنات **create empty PDF dictionary** مباشرة. |

---

## الخلاصة

لقد أظهرنا للتو كيفية **create empty PDF dictionary** كائنات باستخدام Aspose.Pdf، وإدخال حالة رسومات مخصصة في **ExtGState dictionary**، وحفظ الملف المعدل — كل ذلك بلغة C# نظيفة ومألوفة. يتيح هذا النمط تحكمًا دقيقًا في الشفافية، أوضاع الدمج، وأي معلمات أخرى لحالة الرسومات معرفة في مواصفات PDF.

من هنا قد ترغب في:

- تطبيق حالة الرسومات الجديدة على محتوى الصفحة الحالي باستخدام عامل `gs`.  
- بناء مكتبة من حالات الرسومات القابلة لإعادة الاستخدام للعلامة التجارية أو العلامات المائية.  
- 

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات إضافية في الـ API واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء خطوط متقطعة في ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [إنشاء وتعبئة المستطيلات في ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}