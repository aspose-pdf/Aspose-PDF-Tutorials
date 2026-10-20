---
category: general
date: 2026-09-15
description: كيفية تغيير الشفافية في ملف PDF باستخدام Aspose.Pdf لـ .NET وتعلم كيفية
  إضافة الشفافية عند حفظ ملفات PDF المعدلة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change opacity
- how to add transparency
- save modified pdf
language: ar
lastmod: 2026-09-15
og_description: كيفية تغيير الشفافية في ملف PDF باستخدام Aspose.Pdf لـ .NET، بما في
  ذلك كيفية إضافة الشفافية وحفظ ملفات PDF المعدلة في دقائق.
og_image_alt: Screenshot showing a PDF page before and after opacity changes
og_title: كيفية تغيير الشفافية في ملف PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: How to change opacity in a PDF using Aspose.Pdf for .NET and learn
    how to add transparency while you save modified PDF files.
  headline: How to change opacity in a PDF with Aspose.Pdf for .NET
  type: TechArticle
tags:
- Aspose.Pdf
- .NET
- PDF manipulation
title: كيفية تغيير الشفافية في ملف PDF باستخدام Aspose.Pdf لـ .NET
url: /ar/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير الشفافية في ملف PDF باستخدام Aspose.Pdf لـ .NET

إذا كنت بحاجة إلى **how to change opacity** للكائنات داخل ملف PDF، يوضح لك هذا الدليل الخطوات الدقيقة باستخدام Aspose.Pdf لـ .NET. سترى أيضًا **how to add transparency** إلى حالات الرسومات وتتعلم الطريقة الصحيحة لـ **save modified PDF** دون فقدان الجودة.

تغيير الشفافية هو طلب شائع عندما تريد وضع علامات مائية فوق بعضها، إنشاء خلفيات باهتة، أو بناء تأثيرات شبيهة بواجهة المستخدم داخل مستند. يعمل مثال الشيفرة أدناه مع أي ملف PDF يمكن لـ Aspose.Pdf فتحه، ويشرح الدليل كل سطر لتفهم *لماذا* هو مهم.

## ما ستتعلمه

- تحميل مستند PDF باستخدام Aspose.Pdf.
- تحرير قاموس موارد الصفحة لإنشاء حالة رسومات جديدة.
- تحديد شفافية الخط (`CA`)، شفافية التعبئة (`ca`)، ووضع المزج (`BM`).
- إدراج حالة الرسومات في القاموس `ExtGState`.
- **Save modified PDF** ملفات تحافظ على إعدادات الشفافية الجديدة.
- معالجة الحالات الخاصة مثل عدم وجود إدخالات `ExtGState` أو المستندات متعددة الصفحات.

### المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6.0 أو أحدث | يوفر بيئة تشغيل كود C#. |
| Aspose.Pdf for .NET (حزمة NuGet `Aspose.Pdf`) | يوفر واجهة برمجة تطبيقات معالجة PDF المستخدمة في المثال. |
| معرفة أساسية بـ C# | مطلوب لفهم الصياغة وبنية المشروع. |
| ملف PDF إدخال (`input.pdf`) | الملف الذي ستقوم بتعديله. |

> **نصيحة احترافية:** قم بتثبيت الحزمة باستخدام `dotnet add package Aspose.Pdf` قبل البدء.

## الخطوة 1: تحميل مستند PDF

العملية الأولى هي فتح الملف المصدر. استخدام كتلة `using` يضمن أن المستند يتم تحريره بشكل صحيح، مما يمنع قفل الملفات على نظام Windows.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

> **Why this matters:** فتح المستند ينشئ تمثيلًا في الذاكرة يمكنك تحريره. يضمن بيان `using` تحرير الموارد، وهو أمر أساسي عندما تقوم لاحقًا **save modified PDF** إلى نفس المجلد.

## الخطوة 2: الحصول على الصفحة الأولى وقاموس مواردها

إعدادات الشفافية تعيش في قاموس موارد الصفحة. نركز على الصفحة الأولى للتبسيط، لكن نفس المنطق ينطبق على أي فهرس صفحة.

```csharp
// Step 2: Retrieve the first page and its resources
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

> **Why this matters:** يحتوي `Resources` على كائنات مثل الخطوط، الصور، وقاموس `ExtGState` حيث تُخزن حالات الرسومات. تعديل هذا القاموس هو الطريقة الوحيدة لتأثير الشفافية على أوامر الرسم التي تشير إلى الحالة.

## الخطوة 3: التأكد من وجود قاموس ExtGState

إذا كان ملف PDF يحتوي بالفعل على إدخال `ExtGState`، يمكننا إعادة استخدامه. وإلا يجب إنشاء قاموس جديد لتجنب `KeyNotFoundException`.

```csharp
// Step 3: Get or create the ExtGState dictionary
Aspose.Pdf.CosCosPdfDictionary extGStateDict;

if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and attach it
    extGStateDict = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

> **Why this matters:** ملفات PDF مرنة؛ بعض الملفات لا تعرف `ExtGState` أبدًا. إنشاء واحد يضمن أن معلمات الشفافية اللاحقة لها مكان لتخزينها.

## الخطوة 4: بناء حالة رسومات جديدة بقيم الشفافية

حالة الرسومات (`GS`) تحتفظ بمعلمات العرض. المفاتيح `CA` (شفافية الخط) و `ca` (شفافية التعبئة) تقبل قيمًا من `0` (شفاف تمامًا) إلى `1` (معتم تمامًا). المفتاح `BM` يحدد وضع المزج؛ `"Normal"` هو الاختيار الأكثر شيوعًا.

```csharp
// Step 4: Create a graphics state dictionary and set opacity parameters
var graphicsState = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA", new Aspose.Pdf.CosPdfNumber(1.0)),   // stroke opacity (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca", new Aspose.Pdf.CosPdfNumber(0.5)), // fill opacity (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM", new Aspose.Pdf.CosPdfName("Normal")) // blend mode
};

foreach (var p in parameters)
{
    graphicsState.Add(p);
}
```

> **Why this matters:** ضبط `ca` إلى `0.5` يخبر مُعرض PDF برسم الأشكال المملوءة بنصف شفافية. عدّل القيم الرقمية لتتناسب مع متطلبات التصميم الخاصة بك. إدخال `BM` اختياري لكنه يوضح كيف يندمج المحتوى الشفاف مع الكائنات الأساسية.

## الخطوة 5: تسجيل حالة الرسومات الجديدة في قاموس ExtGState

كل حالة رسومات يجب أن يكون لها اسم فريد (مثل `"GS0"`). يمكنك إعادة استخدام اسم إذا كنت تنوي الكتابة فوق حالة موجودة، لكن استخدام معرف جديد يجنب التأثيرات الجانبية غير المقصودة.

```csharp
// Step 5: Add the graphics state to ExtGState with a unique name
extGStateDict.Add("GS0", graphicsState);
```

> **Why this matters:** بمجرد تخزين الحالة، يمكنك الإشارة إليها من تدفقات محتوى الصفحة باستخدام المشغل `/GS0`. هذه هي الآلية التي تضيف **how to add transparency** إلى أوامر الرسم فعليًا.

## الخطوة 6: حفظ ملف PDF المعدل

بعد تحديث قاموس الموارد، اكتب التغييرات مرة أخرى إلى القرص. يمكنك إما استبدال الملف الأصلي أو إنشاء ملف جديد؛ المثال ينشئ `output.pdf` للحفاظ على المصدر سليمًا.

```csharp
// Step 6: Save the modified PDF
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Why this matters:** طريقة `Save` تسلسل الكائنات في الذاكرة، بما فيها حالة الرسومات الجديدة، إلى ملف PDF صالح. هذه هي الخطوة النهائية في **how to change opacity** و **save modified PDF** المستندات.

## مثال كامل قابل للتنفيذ

جمع كل الأجزاء معًا يمنحك برنامجًا مستقلاً يمكنك نسخه إلى تطبيق كونسول.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Collections;

class Program
{
    static void Main()
    {
        // Path to the source PDF
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";

        // Load the document
        using var pdfDocument = new Document(pdfPath);

        // Work with the first page
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState exists
        CosCosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create a new graphics state with opacity settings
        var graphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
        };
        foreach (var p in parameters)
            graphicsState.Add(p);

        // Add the state to ExtGState under the name "GS0"
        extGStateDict.Add("GS0", graphicsState);

        // Save the result
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        Console.WriteLine("Opacity changed and PDF saved successfully.");
    }
}
```

### النتيجة المتوقعة

افتح `output.pdf` في أي عارض PDF. أي محتوى يشير لاحقًا إلى حالة الرسومات `GS0` (على سبيل المثال، مستطيل مرسوم بـ `/GS0 gs`) سيظهر بـ **شفافية تعبئة 50 %** بينما يبقى الخط معتمًا بالكامل. إذا أضفت مثل هذه أوامر الرسم عبر API `Page.Contents.Add` في Aspose.Pdf، ستلاحظ تأثير الشفافية فورًا.

## معالجة صفحات متعددة وحالات رسومات متعددة

- **صفحات متعددة:** كرّر الحلقة عبر `pdfDocument.Pages` وكرر الخطوات 2‑5 لكل صفحة تريد تعديلها. تذكّر استخدام أسماء حالة مميزة (`GS1`, `GS2`, …) إذا احتاجت الصفحات مستويات شفافية مختلفة.
- **إعادة استخدام حالة موجودة:** إذا كان PDF يحتوي بالفعل على حالة باسم `"GS0"` وتريد فقط تعديل شفافيته، استرجعها بـ `extGStateDict["GS0"]` بدلاً من إنشاء إدخال جديد.
- **نصيحة أداء:** إضافة العديد من حالات الرسومات قد يزيد حجم الملف. دمج إعدادات الشفافية المتطابقة في حالة واحدة وإحالتها من صفحات متعددة.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|-------|-------|-----|
| `KeyNotFoundException` على `"ExtGState"` | ملف PDF يفتقر إلى القاموس. | إنشاء واحد كما هو موضح في الخطوة 3. |
| الشفافية غير مرئية | تدفق المحتوى لا يشير إلى الحالة الجديدة. | إدراج `/GS0 gs` قبل أوامر الرسم أو استخدام API `Graphics` في Aspose.Pdf مع معامل `GraphicsState`. |
| ملف PDF الناتج فاسد | محاولة حفظ إلى مجلد للقراءة فقط. | تأكد من أن مسار الوجهة قابل للكتابة وليس هو نفسه الملف المفتوح. |
| قيم الشفافية > 1 أو < 0 | تمرير النسب المئوية بدلًا من الكسور عن طريق الخطأ. | استخدم أرقامًا بين `0.0` و `1.0`. |

## الخطوات التالية

الآن بعد أن عرفت **how to change opacity** و **how to add transparency**، يمكنك استكشاف المواضيع ذات الصلة:

- **how to add transparency** للصور باستخدام كائنات `Image` وخاصية `Transparency`.
- دمج ملفات PDF متعددة مع الحفاظ على حالات الرسومات.
- استخدام خيارات **save modified PDF** مثل `PdfSaveOptions` لضغط أو تشفير النتيجة.

جرّب قيم `ca` و `CA` مختلفة، وضعيات المزج مثل `"Multiply"` أو `"Screen"`، ولاحظ كيف تؤثر على المخرجات البصرية. التقنيات التي تم تغطيتها هنا تشكل أساسًا قويًا لتنسيق PDF المتقدم في

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية إضافة علامة مائية صورة دوارة إلى ملفات PDF باستخدام Aspose.PDF لـ .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [كيفية إضافة طوابع صفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل كامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [كيفية إضافة طوابع أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET | العلامات المائية والخلفيات](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}