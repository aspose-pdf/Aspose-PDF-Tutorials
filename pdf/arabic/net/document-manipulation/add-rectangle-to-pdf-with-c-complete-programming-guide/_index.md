---
category: general
date: 2026-06-05
description: أضف مستطيلًا إلى PDF باستخدام Aspose.Pdf في C#. تعلم كيفية تحميل PDF
  موجود، تعديل صفحة PDF، وإدراج شكل في PDF خلال دقائق.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: ar
og_description: أضف مستطيلًا إلى PDF بسرعة. يوضح هذا البرنامج التعليمي كيفية تحميل
  PDF موجود، تعديل صفحة PDF، ورسم مستطيل على PDF باستخدام Aspose.Pdf.
og_title: إضافة مستطيل إلى ملف PDF باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: إضافة مستطيل إلى PDF باستخدام C# – دليل برمجي كامل
url: /ar/net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة مستطيل إلى PDF باستخدام C# – دليل برمجة شامل

هل احتجت يوماً إلى **add rectangle to pdf** لكن لم تكن متأكدًا من أي استدعاء API تستخدم؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحاولون تعديل PDF برمجيًا للمرة الأولى. الخبر السار؟ ببضع أسطر من C# ومكتبة Aspose.Pdf القوية، يمكنك رسم مستطيل على أي صفحة من مستند موجود في لحظات.

في هذا الدليل سنستعرض تحميل PDF موجود، اختيار الصفحة الصحيحة، تعريف مستطيل مناسب، وأخيرًا إدراج الشكل في PDF. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET. وأيضًا سنتطرق إلى تفاصيل **draw rectangle on pdf** التي قد لم تفكر فيها.

## ما ستحصل عليه

- حل واضح خطوة بخطوة يعمل مباشرةً دون الحاجة لتعديلات.
- فهم كيفية **load existing pdf** بأمان.
- نصائح لـ **edit pdf page** دون إتلاف المستند.
- استراتيجيات لـ **insert shape into pdf** تتجاوز المستطيلات فقط.
- كود C# جاهز للتنفيذ يمكنك نسخه ولصقه فورًا.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.6+).
- حزمة NuGet Aspose.Pdf لـ .NET (`Install-Package Aspose.Pdf`).
- إلمام أساسي بصياغة C# (لا تحتاج إلى معرفة عميقة بـ PDF).

إذا كان لديك ذلك، هيا نبدأ.

![مثال على إضافة مستطيل إلى PDF](add-rectangle-to-pdf.png "لقطة شاشة تُظهر مستطيلًا مضافًا إلى صفحة PDF – add rectangle to pdf")

## إضافة مستطيل إلى PDF – نظرة عامة خطوة بخطوة

فيما يلي المثال الكامل القابل للتنفيذ والذي يتبع الترتيب الدقيق الذي سنناقشه:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

الآن لنفكك كل سطر لتفهم **why** ما نقوم به، وليس فقط **what**.

## تحميل مستند PDF موجود

### لماذا التحميل مهم

قبل أن تتمكن من الرسم، يجب أن يكون PDF في الذاكرة. يقوم مُنشئ `Document` بقراءة الملف، وتحليل هيكله الداخلي، ويعطيك نموذج كائنات للعمل معه. إذا كان الملف مقفلًا أو معطوبًا، ستطلق Aspose استثناءً وصفيًا—حتى تعرف بالضبط ما الخطأ.

### الكود

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- استبدل `YOUR_DIRECTORY` بالمسار المطلق أو النسبي لملف المصدر الخاص بك.
- يمكن أن يكون المسار URL إذا فعلت التحميل عن بُعد في Aspose (سيناريو متقدم).
- **نصيحة:** ضع هذا داخل كتلة `try/catch` للتعامل مع `FileNotFoundException` أو `PdfException` بسلاسة.

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## اختيار وتحضير الصفحة

### لماذا اختيار الصفحة أمر حاسم

ملفات PDF موجهة بالصفحات؛ كل صفحة لها نظام إحداثيات خاص بها. تستخدم Aspose فهرسًا **مبنيًا على 1**، مما يسبب ارتباكًا للمطورين القادمين من مجموعات مبنية على 0. اختيار الصفحة الخاطئة إما يطلق استثناء `ArgumentOutOfRangeException` أو يغيّر صفحة غير مقصودة.

### الكود

```csharp
Page page = doc.Pages[1]; // First page
```

إذا كنت بحاجة للعمل على الصفحة 3، ببساطة غير الفهرس إلى `3`. للسيناريوهات الديناميكية، يمكنك التكرار:

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## تعريف ورسم المستطيل على PDF

### فهم إحداثيات المستطيل

المستطيل في Aspose.Pdf يُعرّف بزاويته السفلية اليسرى (`xLL`, `yLL`) والعلوية اليمنى (`xUR`, `yUR`). يبدأ نظام الإحداثيات من **الزاوية السفلية اليسرى** للصفحة، مع زيادة X إلى اليمين وY إلى الأعلى. هذا عكس العديد من أطر واجهة المستخدم، لذا راقب المحاور.

- `0,0` هي الزاوية السفلية اليسرى للصفحة.
- العرض = `xUR - xLL`؛ الارتفاع = `yUR - yLL`.

إذا قمت بطريق الخطأ بتحديد مستطيل أكبر من الصفحة، سيطلق `AddRectangle` استثناءً. لتجنب ذلك، يمكنك الاستعلام عن حجم الصفحة:

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

ثم قيد مستطيلك:

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### كود لإضافة الشكل

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- `AddRectangle` يرسم تلقائيًا حدًا أسودًا رفيعًا.
- هل تريد مستطيلًا مملوءًا؟ استخدم `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });`.
- هل تحتاج إلى سمك خط مختلف؟ اضبط `rect.LineWidth = 2;` قبل الإضافة.

#### حالة خاصة: مستطيلات متعددة

إذا استدعيت `AddRectangle` بشكل متكرر، كل استدعاء يضيف شكلًا آخر. لتجنب التداخل، أزح المستطيلات اللاحقة:

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## حفظ PDF المعدل

### لماذا الحفظ هو الخطوة النهائية

جميع التعديلات تبقى في الذاكرة حتى تقوم بحفظها. `Document.Save` يكتب المحتوى الجديد إلى القرص (أو إلى تدفق). يمكن استبدال الملف الأصلي، لكن الاحتفاظ بنسخة احتياطية (`output.pdf`) أكثر أمانًا.

### الكود

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- يمكنك أيضًا حفظه إلى `MemoryStream` إذا كنت بحاجة لإرسال PDF عبر HTTP:

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## مثال كامل يعمل (جاهز للنسخ واللصق)

بجمع كل شيء معًا، إليك البرنامج النهائي الذي يمكنك تشغيله الآن:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**الناتج المتوقع:** افتح `output.pdf` وسترى مستطيلًا بحد أزرق مثبتًا في الزاوية السفلية اليسرى للصفحة الأولى، بحجم يصل إلى 500 × 700 نقطة (أو أصغر إذا كانت الصفحة صغيرة).

## أسئلة شائعة ونصائح احترافية

- **هل يمكنني إضافة المستطيل إلى كل صفحة تلقائيًا؟**  
  نعم—قم بالتكرار عبر `doc.Pages` وكرر استدعاء `AddRectangle` لكل كائن `Page`.

- **ماذا لو احتجت لرسم دائرة أو مضلع؟**  
  توفر Aspose طرق `AddCircle` و `AddPolygon` و `AddPolyline`. نفس منطق المستطيل ينطبق على الصناديق المحيطة.

- **هل هناك طريقة لتحديد موقع المستطيل بالنسبة لمركز الصفحة؟**  
  احسب إحداثيات المركز:  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **هل هناك مخاوف أداء مع ملفات PDF الكبيرة؟**  
  تقوم Aspose بتحميل الصفحات بشكل كسول، ولكن إذا كنت تعالج آلاف الصفحات، فكر في استخدام `PdfExtractor` للعمل على أجزاء أو بث الملف لتقليل استهلاك الذاكرة.

## الخلاصة

أنت الآن تعرف **how to add rectangle

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند PDF باستخدام Aspose.PDF – إضافة صفحة، شكل وحفظ](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [كيفية إضافة طوابع صفحات في PDFs باستخدام Aspose.PDF لـ .NET: دليل شامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [إضافة صور وأرقام صفحات إلى PDFs باستخدام Aspose.PDF لـ .NET: دليل شامل](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}