---
category: general
date: 2026-08-04
description: إضافة مستطيل إلى ملف PDF باستخدام C#. تعلم كيفية رسم شكل في PDF باستخدام
  C# مع Aspose.Pdf في مثال واضح ومتكامل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: ar
lastmod: 2026-08-04
og_description: إضافة مستطيل إلى PDF باستخدام C#. يوضح هذا الدرس كيفية رسم شكل في
  PDF باستخدام C# بسرعة وموثوقية.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: إضافة مستطيل إلى PDF باستخدام C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: إضافة مستطيل إلى ملف PDF باستخدام C# – دليل خطوة بخطوة
url: /ar/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة مستطيل إلى PDF باستخدام C# – دليل خطوة بخطوة

إذا كنت بحاجة إلى **إضافة مستطيل إلى ملفات PDF** من تطبيق C#، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستشاهد مثالًا كاملاً قابلاً للتنفيذ يرسم شكلًا في PDF باستخدام مكتبة Aspose.Pdf، وستفهم لماذا كل سطر من الشيفرة مهم.

رسم الأشكال في ملفات PDF هو طلب شائع لمولدات التقارير، قوالب الفواتير، والعلامات التجارية المخصصة للمستندات. بنهاية هذا الشرح يمكنك إدراج أي تعليقات توضيحية مستطيلة، تغيير حجمها أو لونها أو موضعها، وحفظ المستند المعدل دون فقدان المحتوى الموجود.

**ما ستتعلمه**

* كيفية تحميل ملف PDF موجود باستخدام Aspose.Pdf.
* كيفية تعريف حدود المستطيل وإنشاء شكل مستطيل.
* كيفية إضافة المستطيل إلى مجموعة الفقرات في الصفحة.
* كيفية حفظ ملف PDF المحدث والتحقق من النتيجة.
* تنويعات لعدة صفحات، الشفافية، وأنماط الخطوط المخصصة.

**المتطلبات المسبقة**

* .NET 6.0 أو أحدث (تعمل الشيفرة أيضًا مع .NET Framework 4.7+).
* Visual Studio 2022 أو أي بيئة تطوير C#.
* إشارة NuGet إلى `Aspose.Pdf` (نسخة تجريبية مجانية أو نسخة مرخصة).
* ملف PDF إدخال باسم `input.pdf` موجود في مجلد يمكنك التحكم فيه.

---

## كيفية رسم شكل في PDF C# – إعداد المشروع

1. **إنشاء مشروع وحدة تحكم جديد**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **إضافة حزمة Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **وضع `input.pdf`** في دليل المشروع (أو أي مجلد ستشير إليه لاحقًا).

المشروع الآن جاهز لتجميع الشيفرة التي ستقوم **بإضافة مستطيل إلى PDF**.

---

## الخطوة 1: تحميل مستند PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*فئة `Document` تقوم بتحليل الملف وتوفر مجموعة `Pages`. التحميل هو العملية الأولى المطلوبة قبل أي رسم.*

---

## الخطوة 2: اختيار الصفحة المستهدفة

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*إذا كنت بحاجة إلى إضافة المستطيل إلى صفحة مختلفة، استبدل الفهرس برقم الصفحة المطلوب. المكتبة تُطلق استثناءً عندما يكون الفهرس خارج النطاق، لذا تأكد من أن PDF يحتوي على عدد كافٍ من الصفحات.*

---

## الخطوة 3: تعريف حدود المستطيل

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*نظام الإحداثيات يستخدم النقاط (1 pt = 1/72 inch). المثال ينشئ مستطيل بعرض 250 pt وارتفاع 100 pt بالقرب من أعلى الصفحة. عدّل القيم لتناسب تخطيطك.*

---

## الخطوة 4: إنشاء شكل المستطيل

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*فئة `Rectangle` ترث من `GraphicalObject`. ضبط `FillColor` و`Border` اختياري، لكنه يوضح كيفية التحكم في المظهر عندما تتعلم **كيفية رسم شكل في PDF C#** بخلاف الخط الخارجي البسيط.*

---

## الخطوة 5: إضافة المستطيل إلى الصفحة

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*الفقرات هي الحاوية لأي كائن قابل للرسم. بإدراج الشكل في `Paragraphs`، تقوم Aspose.Pdf برسمه عند حفظ المستند.*

---

## الخطوة 6: حفظ PDF المعدل

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*الحفظ ينشئ ملفًا جديدًا بحيث يبقى `input.pdf` الأصلي دون تغيير. يمكنك استبدال الملف المصدر بتمرير نفس المسار، لكن الاحتفاظ بنسخة احتياطية يُعد ممارسةً جيدةً.*

---

## الشيفرة الكاملة (قابلة للتنفيذ)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**الناتج المتوقع** – افتح `output.pdf` في أي عارض PDF. يجب أن ترى مستطيلًا مملوءًا باللون الأزرق بالقرب من الزاوية العليا اليمنى للصفحة الأولى، محاطًا بحدود رمادية داكنة.

---

## كيفية رسم شكل في PDF C# على صفحات متعددة

إذا كنت بحاجة إلى **إضافة مستطيل إلى PDF** على كل صفحة، يمكنك تكرار مجموعة `Pages`:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*هذا النمط يعيد استخدام نفس الحدود على كل صفحة. عدّل الإحداثيات حسب الصفحة إذا كنت تحتاج إلى مواضع مختلفة.*

---

## المشكلات الشائعة ونصائح أفضل الممارسات

| المشكلة | السبب | الحل |
|---------|-------|------|
| يظهر المستطيل خارج الصفحة | الإحداثيات تُقاس من الزاوية السفلية اليسرى؛ استخدام نظام إحداثيات موجه للأعلى قد يسبب ارتباكًا. | تذكر أن محور Y ينمو للأعلى. استخدم قيمًا تناسب حجم الصفحة (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| الشكل غير مرئي | شفافية التعبئة مضبوطة على `0` أو عرض الحد على `0`. | تأكد أن `FillOpacity` أكبر من `0` وأن `Border.Width` لا يقل عن `0.5`. |
| حفظ يسبب استثناء `AccessDeniedException` | ملف الإخراج مفتوح في برنامج آخر. | أغلق أي عارضات قبل تشغيل الشيفرة، أو احفظ إلى مسار مختلف. |
| المستطيل يتداخل مع المحتوى الموجود | لم يتم ضبط التحكم في الطبقات. | استخدم خاصية `ZIndex` (القيم الأعلى تُرسم فوق) إذا كنت بحاجة للتحكم في الطبقات. |

---

## توسيع المستطيل – التدرجات، الدوران، والشفافية

تدعم Aspose.Pdf الرسومات المتقدمة. لإنشاء مستطيل مدوَّر مع تدرج خطي:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*نفس نمط الشيفرة يوضح **كيفية رسم شكل في PDF C#** مع تأثيرات بصرية أغنى.*

---

## التحقق من النتيجة برمجيًا

يمكنك التأكد من إضافة المستطيل بفحص عدد الفقرات في الصفحة:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

إذا زاد العدد بمقدار واحد بعد الإدراج، فإن العملية نجحت.

---

## الخلاصة

أنت الآن تعرف كيف **تضيف مستطيل إلى PDF** باستخدام C#. غطى الدليل تحميل المستند، تعريف الحدود، إنشاء شكل المستطيل، إدراجه في صفحة، وحفظ النتيجة. كما رأيت كيفية التعامل مع صفحات متعددة، تجنب الأخطاء الشائعة، وتطبيق تنسيقات متقدمة.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **كيفية رسم شكل في PDF C#** للدوائر، المضلعات، أو المسارات الحرة، وتعلم دمج الأشكال مع النصوص والصور لإنشاء تقارير PDF متكاملة.

برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}