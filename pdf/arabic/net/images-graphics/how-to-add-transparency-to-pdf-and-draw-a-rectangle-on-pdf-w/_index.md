---
category: general
date: 2026-09-12
description: تعلم كيفية إضافة الشفافية إلى ملف PDF، ورسم مستطيل على ملف PDF، وحفظ
  ملف PDF بالشفافية باستخدام Aspose.PDF في C# – دليل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: ar
lastmod: 2026-09-12
og_description: أضف الشفافية إلى ملف PDF، وارسم مستطيلًا على ملف PDF، واحفظ ملف PDF
  بالشفافية باستخدام Aspose.PDF في C#. اتبع هذا الدرس الكامل.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: إضافة الشفافية إلى ملف PDF ورسم مستطيل على PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: كيفية إضافة الشفافية إلى PDF ورسم مستطيل على PDF باستخدام Aspose.PDF
url: /ar/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة الشفافية إلى PDF ورسم مستطيل على PDF باستخدام Aspose.PDF

إذا كنت بحاجة إلى **إضافة شفافية إلى PDF**، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك في C#. ستتعلم أيضًا كيفية **رسم مستطيل على PDF** وأخيرًا **حفظ PDF مع الشفافية** بحيث يمكن إعادة استخدام النتيجة في التقارير، الفواتير، أو أي سير عمل لأتمتة المستندات.

في هذا البرنامج التعليمي ستقوم بـ:

* تحميل مستند PDF موجود.
* إنشاء حالة رسومية مخصصة تحدد شفافية الخط والملء.
* تطبيق تلك الحالة الرسومية على القماش (canvas) ورسم مستطيل.
* حفظ الملف المعدل مع الحفاظ على إعدادات الشفافية.

لا توجد أدوات خارجية مطلوبة بخلاف مكتبة Aspose.PDF for .NET، ويتم شرح كل سطر من الشيفرة لتفهم *لماذا* كل خطوة مهمة.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+).
* نسخة مرخصة أو تجريبية من **Aspose.PDF for .NET**. قم بتثبيتها عبر NuGet:

```bash
dotnet add package Aspose.Pdf
```

* ملف PDF إدخال (`input.pdf`) موجود في مجلد يمكنك الإشارة إليه من مشروعك.

## الخطوة 1: تحميل مستند PDF

العملية الأولى هي فتح الملف المصدر. استخدام جملة `using` يضمن التخلص من المستند بشكل صحيح، مما يمنع مشاكل قفل الملف لاحقًا عند محاولة الحفظ.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*لماذا هذا مهم*: تحميل المستند يمنحك الوصول إلى مجموعة الصفحات، قواميس الموارد، وكائنات القماش المطلوبة للرسم.

## الخطوة 2: الوصول إلى قاموس موارد الصفحة الأولى

كل صفحة PDF لديها **قاموس موارد** يخزن كائنات مثل الخطوط، الصور، والحالات الرسومية. لإدخال إعداد شفافية جديد نحتاج إلى تعديل مدخل `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*لماذا هذا مهم*: يتيح لنا `DictionaryEditor` قراءة وتعديل كائنات PDF منخفضة المستوى دون كسر بنية المستند.

## الخطوة 3: إنشاء حالة رسومية مخصصة بقيم الشفافية

الحالة الرسومية (`ExtGState`) تتحكم في كيفية عرض عمليات الرسم. نحدد معاملين للشفافية:

* **CA** – شفافية الخط (حدود الأشكال).
* **ca** – شفافية الملء (داخل الأشكال).

نقوم أيضًا بتعيين وضع المزج (`BM`) إلى “Normal”، وهو أكثر عمليات التركيب شيوعًا.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*لماذا هذا مهم*: بإضافة `GS0` إلى قاموس `ExtGState` ننشئ مرجعًا قابلًا لإعادة الاستخدام يمكن للقماش تفعيله قبل الرسم. شفافية الملء `0.5` تجعل المستطيل شبه شفاف، محققًا هدف **إضافة شفافية إلى PDF**.

## الخطوة 4: تطبيق الحالة الرسومية ورسم مستطيل

الآن نخبر قماش الصفحة باستخدام الحالة الرسومية التي أنشأناها، ثم نرسم مستطيلًا. الإحداثيات تتبع نظام إحداثيات PDF (الأصل في الزاوية السفلية اليسرى).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*لماذا هذا مهم*: `SetGraphicsState("GS0")` يبدل سياق الرسم إلى إعدادات الشفافية المعرفة مسبقًا. طريقة `Rectangle` تحدد الشكل، و`Stroke` ترسم الحد بالشفافية المحددة. إذا أردت مستطيلًا مملوءًا، استبدل `Stroke()` بـ `FillAndStroke()`.

## الخطوة 5: حفظ PDF المعدل مع الحفاظ على الشفافية

أخيرًا، نكتب المستند مرة أخرى إلى القرص. يحتوي ملف الإخراج على الحالة الرسومية الجديدة، المستطيل المرسوم، ومعلومات الشفافية.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*لماذا هذا مهم*: حفظ المستند ينهى جميع التغييرات. يمكن فتح الملف الناتج في أي عارض PDF، وسيظهر المستطيل بشفافية ملء 50 ٪.

### النتيجة المتوقعة

عند فتح `output_with_extgstate.pdf` يجب أن ترى مستطيلًا حدوده غير شفافة تمامًا وداخله شبه شفاف، مما يسمح برؤية محتوى الصفحة الأساسي من خلاله.

## حالات خاصة ونصائح عملية

| الحالة | التعديل الموصى به |
|-----------|------------------------|
| **صفحات متعددة** | كرّر الحلقة على `pdfDocument.Pages` وطبق الخطوات 2‑4 لكل صفحة مستهدفة. |
| **قيم شفافية مختلفة** | غيّر قيم `CosPdfNumber` لـ `CA` (الخط) و `ca` (الملء) إلى أي رقم بين `0` (شفاف بالكامل) و `1` (معتم بالكامل). |
| **وضعيات مزج مخصصة** | استبدل `"Normal"` بـ `"Multiply"` أو `"Screen"` أو أي وضع مزج PDF‑قياسي يدعمه عارضك. |
| **مستطيل مملوء** | استدعِ `canvas.FillAndStroke()` بدلاً من `canvas.Stroke()` لتطبيق كل من الملء والحد. |
| **إعادة استخدام نفس الحالة الرسومية** | يمكنك استدعاء `canvas.SetGraphicsState("GS0")` قبل رسم أي عدد من الأشكال على نفس الصفحة. |

**نصيحة احترافية:** دائمًا افحص قاموس الموارد بعد إضافة `ExtGState` جديد. إذا لم يكن القاموس موجودًا، أنشئه أولًا:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## مثال كامل قابل للتنفيذ

فيما يلي برنامج مستقل يمكنك نسخه إلى تطبيق Console وتشغيله فورًا (استبدل `YOUR_DIRECTORY` بمسار فعلي).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

تشغيل البرنامج ينتج `output_with_extgstate.pdf`، الذي يوضح **إضافة شفافية إلى PDF**، **رسم مستطيل على PDF**، و**حفظ PDF مع الشفافية** كلها في تدفق واحد.

## الخلاصة

أنت الآن تعرف كيفية **إضافة شفافية إلى PDF**، **رسم مستطيل على PDF**، و**حفظ PDF مع الشفافية** باستخدام Aspose.PDF for .NET. تدور العملية حول إنشاء `ExtGState` مخصص، تطبيقه على القماش، وحفظ التغييرات. باستخدام هذه اللبنات يمكنك توسيع التقنية إلى أشكال أخرى، صفحات متعددة، أو قيم شفافية ديناميكية.

**الخطوات التالية**

* استكشف بدائل رسم أخرى مثل `canvas.Ellipse`، `canvas.Path`، أو `canvas.TextFragment` مع إعادة استخدام نفس الحالة الرسومية.
* اجمع بين الشفافية وطبقات الصور لإنشاء علامات مائية (`canvas.Image` + `ExtGState` مخصص).
* راجع وثائق Aspose.PDF حول **معلمات الحالة الرسومية** للحصول على تأثيرات تركيبية متقدمة.

برمجة سعيدة، واستمتع بالمرونة البصرية التي توفرها الشفافية في سير عمل PDF الخاص بك!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}