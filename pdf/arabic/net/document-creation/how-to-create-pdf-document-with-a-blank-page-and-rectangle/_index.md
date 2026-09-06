---
category: general
date: 2026-09-05
description: إنشاء مستند PDF في C# بإضافة صفحة فارغة، ورسم مستطيل، وحفظ ملف PDF. اتبع
  مثال Aspose.PDF خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: ar
lastmod: 2026-09-05
og_description: إنشاء مستند PDF في C# عن طريق إضافة صفحة فارغة، ورسم مستطيل، وحفظ
  ملف PDF. اتبع هذا المثال الكامل باستخدام Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: إنشاء مستند PDF بصفحة فارغة ومستطيل – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: كيفية إنشاء مستند PDF بصفحة فارغة ومستطيل
url: /ar/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مستند PDF بصفحة فارغة ومستطيل

إذا كنت بحاجة إلى **إنشاء مستند PDF** برمجيًا، يوضح هذا الدليل حلاً كاملاً بلغة C#. ستتعلم كيفية إضافة صفحة فارغة، ورسم مستطيل على تلك الصفحة، وأخيرًا حفظ ملف PDF. يستخدم المثال مكتبة Aspose.PDF، التي تعمل مع .NET 6+ و .NET Framework 4.5+.

إضافة صفحة فارغة ورسم أشكال هي متطلبات شائعة للفواتير، الشهادات، أو التقارير المخصصة. بنهاية هذا الدرس ستحصل على مشروع قابل للتنفيذ ينتج ملف PDF يحتوي على مستطيل واحد موضعه (100، 100) بحجم 200 × 200 نقطة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Visual Studio 2022 (أو أي بيئة تطوير C#)
* .NET 6 SDK أو .NET Framework 4.5+
* حزمة Aspose.PDF for .NET عبر NuGet  
  ```bash
  dotnet add package Aspose.PDF
  ```
* صلاحية كتابة في دليل الإخراج

لا توجد إعدادات إضافية مطلوبة؛ الكود يعمل مباشرةً دون تعديل.

## إنشاء مستند PDF – نظرة عامة

تتكون العملية بالكامل من أربع خطوات منطقية:

1. **Instantiate** كائن `Document` – يمثل ملف PDF.
2. **Add a blank page** – توفر الصفحة مساحة للرسم.
3. **Draw a rectangle** – كائن `Path` يحدد الشكل.
4. **Save the PDF file** – يحفظ المستند على القرص.

كل خطوة معزولة في قسمها الخاص حتى يمكنك إعادة استخدامها أو استبدالها حسب الحاجة.

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="لقطة شاشة تُظهر مستند PDF مع مستطيل مرسوم على صفحة فارغة"}

## إضافة صفحة فارغة pdf

يجب أن يحتوي ملف PDF على صفحة واحدة على الأقل قبل أن يتم وضع أي رسومات. طريقة `Pages.Add()` تنشئ صفحة فارغة بأبعاد افتراضية (A4). إذا كنت تحتاج إلى حجم مختلف، مرّر معامل `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*لماذا هذه الخطوة مهمة* – كائن الصفحة يحتوي على مجموعات للنصوص، الصور، والرسومات المتجهية. بدون صفحة، أي محاولة لإضافة مستطيل ستؤدي إلى استثناء.

### حالة حافة: حجم صفحة مخصص

إذا كان التصميم يتطلب صفحة بحجم 6 × 9 بوصة، استبدل الاستدعاء الافتراضي بـ:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## رسم مستطيل pdf

رسم المستطيل هو مجرد إنشاء شكل `Rectangle` وتغليفه داخل `Path`. استدعاء `ValidateBounds()` يضمن أن الشكل يظل داخل حدود الصفحة، مما يمنع القطع.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*لماذا هذه الخطوة مهمة* – كائن `Path` هو العنصر المتجهي الأساسي المستخدم في Aspose.PDF. من خلال التحقق من الحدود تتجنب الأخطاء أثناء التشغيل عندما يتجاوز المستطيل حدود الصفحة.

### نصيحة احترافية: تنسيق المستطيل

يمكنك تغيير لون الحد وعرض الخط:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

هذا ينتج حدودًا حمراء بسُمك نقطتين.

## حفظ ملف pdf

حفظ المستند ينهى عملية إنشاء الملف على القرص. طريقة `Save` تقبل مسار ملف أو تدفق. توفير مسار مطلق يجعل الموقع واضحًا، وهو مفيد لسيناريوهات الأتمتة.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*لماذا هذه الخطوة مهمة* – الحفظ هو النقطة الوحيدة التي يتحول فيها التمثيل في الذاكرة إلى ملف فعلي. إذا كنت بحاجة لإرجاع PDF من واجهة برمجة تطبيقات ويب، استبدل مسار الملف بـ `MemoryStream`.

### حالة حافة: الكتابة فوق ملفات موجودة

Aspose.PDF يكتب فوق ملف موجود بشكل افتراضي. لحماية المخرجات السابقة، تحقق من وجود الملف أولًا:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## كيفية إضافة مستطيل – أفضل الممارسات

* **حافظ على الإحداثيات داخل هوامش الصفحة** – استخدم `ValidateBounds()` أو احسب الهوامش يدويًا.
* **أعد استخدام كائنات `GraphInfo`** عند رسم أشكال متعددة؛ هذا يقلل من تخصيص الذاكرة.
* **قم بتحرير كائن `Document`** (كما هو موضح باستخدام `using var`) لتحرير الموارد الأصلية بسرعة.
* **اختبر بإعدادات DPI مختلفة** إذا قمت لاحقًا بدمج صور نقطية؛ الأشكال المتجهية مثل المستطيلات تبقى واضحة بأي دقة.

## مثال عملي كامل

فيما يلي البرنامج الكامل الذي يمكنك نسخه إلى تطبيق كونسول. يُجمع دون تعديل وينتج `output.pdf` في مجلد المشروع.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج ينشئ ملف PDF بصفحة واحدة. عند فتح `output.pdf` ستظهر صفحة بيضاء فارغة مع مستطيل أحمر موضعه 100 نقطة من الحافة اليسرى والسفلية، بحجم 200 × 200 نقطة.

## الخلاصة

أنت الآن تعرف كيف **تنشئ مستند PDF**، **تضيف صفحة فارغة pdf**، **ترسم مستطيل pdf**، و**تحفظ ملف pdf** باستخدام Aspose.PDF في C#. يغطي المثال استدعاءات API الأساسية، يوضح سبب ضرورة كل استدعاء، ويقدم نصائح لتغييرات شائعة مثل أحجام الصفحات المخصصة أو تنسيق المستطيل.

بعد ذلك، استكشف مواضيع ذات صلة مثل **إضافة نص**، **دمج صور**، أو **إنشاء تقارير متعددة الصفحات**. النمط نفسه—إنشاء كائن `Document`، تعديل الصفحات، إضافة محتوى متجهي أو نقطي، ثم `Save`—ينطبق على جميع هذه السيناريوهات. لا تتردد في تجربة أشكال، ألوان، وتخطيطات صفحات مختلفة لتتناسب مع احتياجات مشروعك.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند PDF C# – إضافة صفحة، رسم مستطيل وحفظ](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [إنشاء مستند PDF باستخدام Aspose.PDF – دليل خطوة بخطوة](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [إنشاء مستند PDF باستخدام Aspose – إضافة صفحة، مربع نص، ونموذج](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}