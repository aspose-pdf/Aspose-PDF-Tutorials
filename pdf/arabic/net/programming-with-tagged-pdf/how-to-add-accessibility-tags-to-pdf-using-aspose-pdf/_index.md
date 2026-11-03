---
category: general
date: 2026-10-23
description: أضف وسوم إمكانية الوصول إلى ملفات PDF باستخدام Aspose.PDF لـ .NET. اتبع
  دليلًا كاملاً خطوة بخطوة يغطي إمكانية وصول Aspose.Pdf، ووسم PDF باستخدام C#، وأفضل
  الممارسات لـ PDF/UA.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add accessibility tags to pdf
- Aspose.Pdf accessibility
- C# PDF tagging
- tagged PDF creation
- PDF accessibility best practices
- PDF document structure
language: ar
lastmod: 2026-10-23
og_description: إضافة علامات الوصول إلى PDF باستخدام Aspose.PDF لـ .NET. يوضح لك هذا
  البرنامج التعليمي كيفية إنشاء PDF مع علامات يتوافق مع معايير PDF/UA.
og_image_alt: Screenshot of a PDF page with a highlighted accessibility tag overlay
og_title: إضافة وسوم الوصول إلى ملفات PDF باستخدام Aspose.PDF – دليل كامل بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Add accessibility tags to PDF using Aspose.PDF for .NET. Follow a complete,
    step‑by‑step guide that covers Aspose.Pdf accessibility, C# PDF tagging, and PDF/UA
    best practices.
  headline: How to add accessibility tags to PDF using Aspose.PDF
  type: TechArticle
- description: Add accessibility tags to PDF using Aspose.PDF for .NET. Follow a complete,
    step‑by‑step guide that covers Aspose.Pdf accessibility, C# PDF tagging, and PDF/UA
    best practices.
  name: How to add accessibility tags to PDF using Aspose.PDF
  steps:
  - name: Prepare your development environment
    text: '1. Install the Aspose.PDF NuGet package:'
  - name: Load the source PDF
    text: The first operation opens the existing PDF that you want to tag.
  - name: Create a tagged content element (C# PDF tagging)
    text: A tagged content element describes the logical role of the text (e.g., paragraph,
      heading). Here we create a paragraph tag.
  - name: Define the tag’s location on the page
    text: Accessibility tags also need a geometric location so that the visual layout
      matches the logical structure.
  - name: Add the tag to the first page (tagged PDF creation)
    text: Now attach the tag to a specific page. In this example we use the first
      page, but you can iterate over `pdfDocument.Pages` for multi‑page documents.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The saved file now contains
      the accessibility tag.
  - name: Verify the accessibility tags
    text: You can confirm that the tag was added by opening the PDF in a viewer that
      supports structure inspection (e.g., Adobe Acrobat Pro > Tools > Accessibility
      > Read Order). The paragraph should appear in the logical structure tree.
  type: HowTo
tags:
- PDF
- C#
- Accessibility
title: كيفية إضافة وسوم الوصول إلى ملفات PDF باستخدام Aspose.PDF
url: /ar/net/programming-with-tagged-pdf/how-to-add-accessibility-tags-to-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة وسوم إمكانية الوصول إلى PDF باستخدام Aspose.PDF

إذا كنت بحاجة إلى **إضافة وسوم إمكانية الوصول إلى ملفات PDF**، يوضح لك هذا الدليل حلاً كاملاً باستخدام Aspose.PDF لـ .NET. سواءً كنت تُعد مستندات قانونية أو كتبًا إلكترونية أو تقارير يجب أن تتوافق مع معيار PDF/UA، ستتعلم كيفية إنشاء PDF مُوسوم يمكن لقارئات الشاشة تفسيره.

يغطي الدرس إعداد التطوير المطلوب، وإنشاء عنصر محتوى مُوسوم، وتحديد موقع الوسم على الصفحة، وحفظ المستند النهائي. لا توجد مراجع خارجية مطلوبة؛ كل مقطع شفرة جاهز للنسخ والتنفيذ.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- رخصة Aspose.PDF لـ .NET سارية (أو مفتاح تقييم مؤقت)
- Visual Studio 2022 أو أي محرر C# تفضله
- ملف PDF مصدر موجود على القرص (المثال يستخدم `source.pdf`)

تضمن هذه المتطلبات المسبقة تشغيل الكود دون أي إعدادات إضافية.

## إضافة وسوم إمكانية الوصول إلى PDF – دليل خطوة بخطوة

الأقسام التالية تُرشدك عبر كل عملية مطلوبة **لإضافة وسوم إمكانية الوصول إلى PDF**. كل خطوة تتضمن كتلة شفرة كاملة، شرحًا لأهمية الخطوة، ونصائح عملية مستمدة من مشاريع واقعية.

### إعداد بيئة التطوير الخاصة بك

1. ثبت حزمة Aspose.PDF NuGet:

```bash
dotnet add package Aspose.PDF
```

2. أنشئ مشروعًا جديدًا من نوع console (أو أضف الشفرة إلى مشروع موجود):

```bash
dotnet new console -n PdfTagger
cd PdfTagger
```

> **نصيحة احترافية:** استخدم العلامة `-n` للحفاظ على اسم مجلد المشروع متسقًا مع هدف الشفرة؛ يساعد ذلك عندما تبحث عن المشروع لاحقًا.

### تحميل ملف PDF المصدر

العملية الأولى تفتح ملف PDF الموجود الذي تريد وسمه.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Load the PDF document
var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");
```

**لماذا هذا مهم:** فتح المستند يُنشئ تمثيلًا في الذاكرة يتيح لك تعديل الصفحات، التعليقات التوضيحية، والوسوم. بدون تحميل الملف، لا يمكنك إرفاق أي معلومات إمكانية وصول.

### إنشاء عنصر محتوى مُوسوم (وسم PDF في C#)

عنصر المحتوى المُوسوم يصف الدور المنطقي للنص (مثل الفقرة أو العنوان). هنا نقوم بإنشاء وسم فقرة.

```csharp
// Step 2: Create a tagged content element
var paragraphTag = new TaggedContent
{
    Role = TaggedRoles.Paragraph, // defines the logical role
    Text = "Hello, tagged world!" // visible text that screen readers will announce
};
```

**لماذا هذا مهم:** تعداد `TaggedRoles` يطابق مباشرةً أدوار PDF/UA. استخدام الدور الصحيح أمر أساسي لأفضل ممارسات إمكانية وصول PDF لأنه يُخبر تقنيات المساعدة كيفية تفسير المحتوى.

### تحديد موقع الوسم على الصفحة

تحتاج وسوم إمكانية الوصول أيضًا إلى موقع هندسي بحيث يتطابق التخطيط البصري مع الهيكل المنطقي.

```csharp
// Step 3: Define the location on the page (in points)
// Rectangle(left, bottom, right, top)
var tagLocation = new Rectangle(100, 500, 400, 550);
```

**لماذا هذا مهم:** المستطيل يحدد مكان ظهور الفقرة على الصفحة. إذا لم يتطابق الموقع مع النص البصري، قد تنقل قارئات الشاشة معلومات غير صحيحة، مما يخالف أفضل ممارسات إمكانية وصول PDF.

### إضافة الوسم إلى الصفحة الأولى (إنشاء PDF مُوسوم)

الآن قم بإرفاق الوسم إلى صفحة محددة. في هذا المثال نستخدم الصفحة الأولى، لكن يمكنك التكرار عبر `pdfDocument.Pages` للمستندات متعددة الصفحات.

```csharp
// Step 4: Access the first page
var firstPage = pdfDocument.Pages[1];

// Step 5: Add the tagged content to the page at the specified position
firstPage.AddTag(paragraphTag, tagLocation);
```

> **احذر:** `Pages` يبدأ من 1 في Aspose.PDF. محاولة استخدام الفهرس 0 ستؤدي إلى رمي استثناء `ArgumentOutOfRangeException`.

### حفظ ملف PDF المعدل

أخيرًا، احفظ المستند المحدث إلى القرص. الملف المحفوظ الآن يحتوي على وسم إمكانية الوصول.

```csharp
// Step 6: Save the modified PDF with the new tag
pdfDocument.Save(@"YOUR_DIRECTORY\tagged_out.pdf");
```

**لماذا هذا مهم:** الحفظ يُثبت معلومات الوسم في تدفق بنية PDF (`/StructTreeRoot`). يمكن التحقق من الملف الناتج باستخدام أدوات فحص PDF/UA مثل PAC (PDF Accessibility Checker).

### التحقق من وسوم إمكانية الوصول

يمكنك التأكد من إضافة الوسم بفتح ملف PDF في عارض يدعم فحص البنية (مثل Adobe Acrobat Pro > Tools > Accessibility > Read Order). يجب أن تظهر الفقرة في شجرة البنية المنطقية.

بدلاً من ذلك، استخدم API الخاص بـ Aspose.PDF لقراءة الوسم مرة أخرى:

```csharp
var savedDoc = new Document(@"YOUR_DIRECTORY\tagged_out.pdf");
var savedPage = savedDoc.Pages[1];
var tags = savedPage.Tags; // collection of TaggedContent objects

foreach (var tag in tags)
{
    Console.WriteLine($"Role: {tag.Role}, Text: {tag.Text}");
}
```

**الناتج المتوقع:**

```
Role: Paragraph, Text: Hello, tagged world!
```

إذا كان الناتج يطابق الشفرة أعلاه، فقد تم إضافة وسم إمكانية الوصول بنجاح.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يدمج كل خطوة. انسخ الشفرة إلى `Program.cs` وشغّل `dotnet run`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

namespace PdfTagger
{
    class Program
    {
        static void Main()
        {
            // Load the source PDF
            var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

            // Create a paragraph tag
            var paragraphTag = new TaggedContent
            {
                Role = TaggedRoles.Paragraph,
                Text = "Hello, tagged world!"
            };

            // Define where the tag should appear
            var tagLocation = new Rectangle(100, 500, 400, 550);

            // Attach the tag to the first page
            var firstPage = pdfDocument.Pages[1];
            firstPage.AddTag(paragraphTag, tagLocation);

            // Save the tagged PDF
            var outputPath = @"YOUR_DIRECTORY\tagged_out.pdf";
            pdfDocument.Save(outputPath);

            // Verify the tag was added
            var savedDoc = new Document(outputPath);
            var savedPage = savedDoc.Pages[1];
            foreach (var tag in savedPage.Tags)
            {
                Console.WriteLine($"Role: {tag.Role}, Text: {tag.Text}");
            }

            Console.WriteLine("Accessibility tag added successfully.");
        }
    }
}
```

تشغيل البرنامج ينتج ملف `tagged_out.pdf`، وهو PDF يحتوي الآن على وسم فقرة. ستقرأ قارئات الشاشة مثل NVDA أو JAWS “Hello, tagged world!” عندما تصادف تلك المنطقة.

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية تعديل الشفرة | السبب |
|-----------|----------------------|--------|
| **صفحات متعددة** | التكرار عبر `pdfDocument.Pages` وتطبيق الوسوم على كل صفحة حسب الحاجة. | يضمن كل |

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [إنشاء ملفات PDF مُوسومة باستخدام Aspose.PDF لـ .NET: دليل كامل لتعزيز إمكانية الوصول وبنية المستند](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [إنشاء وإدارة ملفات PDF مُوسومة باستخدام Aspose.PDF لـ .NET: تعزيز إمكانية الوصول وتحسين محركات البحث](/pdf/english/net/advanced-features/create-manage-tagged-pdfs-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: تعزيز إمكانية وصول PDF عبر الوسم](/pdf/english/net/advanced-features/aspose-pdf-net-accessible-tagging-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}