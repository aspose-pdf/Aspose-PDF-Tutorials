---
category: general
date: 2026-10-10
description: تعلم كيفية إضافة مستطيل إلى ملف PDF، ورسم شكل على ملف PDF، وحفظ ملف PDF
  المعدل باستخدام Aspose.PDF. يتضمن دليلًا خطوة بخطوة للوصول إلى صفحة PDF معينة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: ar
lastmod: 2026-10-10
og_description: إضافة مستطيل إلى PDF باستخدام Aspose.PDF في C#. يوضح هذا الدليل كيفية
  رسم شكل على PDF، والوصول إلى صفحة PDF محددة، وحفظ PDF المعدل.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: إضافة مستطيل إلى ملف PDF باستخدام Aspose.PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: كيفية إضافة مستطيل إلى PDF باستخدام Aspose.PDF في C#
url: /ar/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة مستطيل إلى PDF باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **إضافة مستطيل إلى PDF** برمجيًا، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستتعلم **رسم شكل على PDF**، استهداف صفحة معينة، و **حفظ PDF المعدل** دون أخطاء.

التعامل مع مستندات PDF هو مطلب شائع للتقارير، الفوترة، أو تعليقات المستندات. بنهاية هذا الدرس يمكنك بثقة **إضافة شكل إلى PDF**، معالجة أخطاء الخروج عن الحدود، ودمج الحل في أي مشروع .NET.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير C#)  
* رخصة Aspose.PDF for .NET أو مفتاح تقييم مجاني – تعمل الواجهة البرمجية بنفس الطريقة في كلا الوضعين  
* ملف PDF اسمه `input.pdf` موجود في مجلد يمكنك الإشارة إليه من الكود الخاص بك  

هذه العناصر هي الاعتمادات الخارجية الوحيدة للمثال.

## الخطوة 1: تثبيت حزمة Aspose.PDF عبر NuGet

مكتبة Aspose.PDF توفر الفئات `Document`، `Rectangle`، وغيرها من فئات الرسم التي تحتاجها.

```bash
dotnet add package Aspose.PDF
```

تشغيل هذا الأمر يضيف أحدث نسخة مستقرة من Aspose.PDF إلى مشروعك، مما يجعل فئات PDF متاحة للترجمة.

## الخطوة 2: تحميل مستند PDF

العملية الأولى هي تحميل ملف المصدر. هذا ينشئ تمثيلًا في الذاكرة يمكنك تعديلّه.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*لماذا هذا مهم*: تحميل المستند يمنحك الوصول إلى مجموعة الصفحات الخاصة به، وهو ما يلزم **الوصول إلى صفحة PDF محددة** لاحقًا.

## الخطوة 3: الوصول إلى الصفحة الثانية (فهرس يبدأ من الصفر)

صفحات PDF مفهرسة بدءًا من `0`. لوضع مستطيل على الصفحة الثانية، استرجع الصفحة ذات الفهرس `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

إذا كان المستند يحتوي على أقل من صفحتين، سيتم إلقاء استثناء `ArgumentOutOfRangeException`، مما ينبهك إلى ضرورة وجود شرط حماية في كود الإنتاج.

## الخطوة 4: إنشاء شكل المستطيل

حدد موضع المستطيل وحجمه باستخدام بنية `Rectangle`، ثم غلفه في كائن رسم Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*لماذا هذا مهم*: خصائص `BorderInfo` و `FillColor` تتيح لك **رسم شكل على PDF** بخط واضح وتعبئة اختيارية، مما يجعل المستطيل بارزًا للقراء.

## الخطوة 5: إضافة المستطيل إلى مجموعة الفقرات الخاصة بالصفحة

Aspose.PDF يتعامل مع كائنات الرسم كعناصر فقرة. إضافة المستطيل إلى مجموعة `Paragraphs` الخاصة بالصفحة تعرضه على الصفحة.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

في هذه المرحلة يحتوي مستند PDF في الذاكرة على الشكل الجديد، لكن الملف على القرص لا يتغير حتى تقوم بحفظه.

## الخطوة 6: حفظ PDF المعدل ومعالجة أخطاء الخروج عن الحدود

استدعاء `Save` يكتب المستند المحدث إلى ملف جديد. إذا تجاوز المستطيل أبعاد الصفحة، تقوم Aspose بإلقاء استثناء `PdfException`. التقاط هذا الاستثناء يتيح لك الإبلاغ عن المشكلة بشكل نظيف.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*لماذا هذا مهم*: كتلة `try/catch` تضمن أن تطبيقك **يحفظ PDF المعدل** بأمان، ورسالة الخطأ تساعدك على تعديل إحداثيات المستطيل إذا لزم الأمر.

## مثال كامل يعمل

بجمع جميع الخطوات معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
PDF saved successfully with rectangle added.
```

وينشئ ملف `output.pdf` الذي يظهر المحتوى الأصلي بالإضافة إلى مستطيل أزرق في الإحداثيات المحددة على الصفحة الثانية.

إذا كان المستطيل أكبر من الصفحة، سترى:

```
Shape out of bounds: The shape exceeds page margins.
```

## أسئلة شائعة وحالات حافة

### ماذا لو كان PDF يحتوي على صفحة واحدة؟

محاولة الوصول إلى `pdfDocument.Pages[1]` تُلقي استثناء `ArgumentOutOfRangeException`. احمِ نفسك من ذلك بالتحقق من `pdfDocument.Pages.Count` قبل الفهرسة.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### كيف يمكن إضافة مستطيلات متعددة على صفحات مختلفة؟

كرر الخطوات 2‑4 لكل صفحة مستهدفة، مع تعديل إحداثيات المستطيل حسب الحاجة. يمكنك وضع المنطق داخل حلقة تتكرر على `pdfDocument.Pages`.

### هل يمكنني استخدام أشكال أخرى مثل الدوائر أو المضلعات؟

نعم. Aspose.PDF توفر فئات `Ellipse`، `Polygon`، و `Polyline` التي تتبع نفس النمط كـ `Rectangle`. استبدل استدعاء `new Aspose.Pdf.Drawing.Rectangle` بالفئة الشكلية المطلوبة.

### هل تدعم المكتبة ملفات PDF ذات الصفحات المدورة؟

Aspose.PDF تحترم تلقائيًا دوران الصفحة عند رسم الأشكال. تُفسّر إحداثيات المستطيل في نظام إحداثيات الصفحة الأصلي، لذا لا يلزم أي تحويل إضافي.

## اعتبارات الأداء

* **استخدام الذاكرة** – تحميل PDF كبير (مئات الميجابايت) يستهلك ذاكرة بنسبتها. إذا كنت بحاجة لتعديل صفحة واحدة فقط، فكر في استخدام `PdfFileInfo` لاستخراج تلك الصفحة، تعديلها، ثم دمجها مرة أخرى.  
* **المعالجة الدفعية** – عند إضافة أشكال إلى العديد من المستندات، أعد استخدام كائن `License` واحد لتجنب عبء التحقق المتكرر من الترخيص.

## الخطوات التالية

الآن بعد أن يمكنك **إضافة مستطيل إلى PDF**، استكشف هذه المواضيع ذات الصلة:

* **draw shape on PDF** – تعلم كيفية وضع نصوص، صور، وعلامات مائية فوق PDF  
* **add shape to PDF** – دمج أشكال متعددة في طبقة تعليقات توضيحية واحدة  
* **save modified PDF** – استخدم التدفقات (`MemoryStream`) لإرجاع ملفات PDF مباشرةً من واجهات برمجة الويب  
* **access specific PDF page** – تنفيذ استخراج نطاق الصفحات لتقارير مخصصة  

جرّب ألوانًا مختلفة، أنماط خطوط، ومستويات شفافية لتتناسب مع إرشادات علامتك التجارية.

---

*برمجة سعيدة! إذا ساعدك هذا الدرس في **إضافة مستطيل إلى PDF**، فكر في مشاركته مع زملائك أو المساهمة بتحسينات للمجتمع.*

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إضافة شكل إلى PDF باستخدام Aspose.PDF في C# – دليل خطوة بخطوة](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [كيفية إضافة كائن خط في PDF باستخدام Aspose.PDF for .NET: دليل خطوة بخطوة](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [كيفية إنشاء PDF في C# – إضافة صفحة، رسم مستطيل وحفظ](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}