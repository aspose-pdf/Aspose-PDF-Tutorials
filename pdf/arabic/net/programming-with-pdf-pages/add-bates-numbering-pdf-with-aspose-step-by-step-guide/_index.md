---
category: general
date: 2026-08-08
description: إضافة ترقيم باتس إلى ملف PDF باستخدام Aspose.Pdf في C#. يوضح هذا الدليل
  أيضًا كيفية إضافة صفحة فارغة إلى ملف PDF وإنشاء ملف PDF برمجيًا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: ar
lastmod: 2026-08-08
og_description: إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose.Pdf في C#. تعلم كيفية
  إضافة صفحة فارغة إلى PDF، وإنشاء PDF برمجيًا، وحفظ المستند النهائي في دقائق.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: إضافة ترقيم بايتس لملف PDF باستخدام Aspose – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: إضافة ترقيم بيتس لملف PDF باستخدام Aspose – دليل خطوة بخطوة
url: /ar/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم بايتس إلى PDF باستخدام Aspose – دليل خطوة بخطوة

إضافة ترقيم بايتس إلى PDF باستخدام Aspose.Pdf أمر بسيط بمجرد أن تفهم الخطوات الأساسية. إذا كنت بحاجة أيضًا إلى إضافة صفحة فارغة إلى PDF أو إنشاء PDF برمجيًا، يغطي هذا الدليل كل ما تحتاجه.

في هذا الدرس سوف:

* تنشئ مستند PDF جديد من الصفر.  
* تضيف صفحة فارغة إلى PDF ستستضيف أرقام بايتس.  
* تُكوّن كائن ترقيم بايتس مع بادئة مخصصة.  
* تحفظ الـ PDF بحيث تظهر الأرقام في الملف المُنشأ.  

بنهاية الدرس ستحصل على تطبيق وحدة تحكم C# كامل الوظائف ينتج PDF يحتوي على أرقام بايتس مثل **CASE‑1000**, **CASE‑1001**, … – وهو مطلب شائع في سير عمل القضايا القانونية واكتشاف الأدلة الإلكترونية.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.8).  
* Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#.  
* ترخيص صالح لـ Aspose.Pdf for .NET (أو مفتاح تقييم مجاني).  
* إلمام أساسي بصياغة C#.

> **نصيحة احترافية:** إذا شغلت الكود بدون ترخيص، سيضيف Aspose علامة مائية صغيرة إلى ملف PDF الناتج.

## الخطوة 1: إعداد المشروع واستيراد Aspose.Pdf

أنشئ مشروع وحدة تحكم جديد وأضف حزمة Aspose.Pdf عبر NuGet:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

التوجيهات `using` المطلوبة للمثال هي:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

هذه المساحات الاسمية تمنحك الوصول إلى الفئات `Document` و `Page` و `BatesNumberingArtifact` المستخدمة لاحقًا.

## الخطوة 2: إضافة صفحة فارغة إلى PDF

يجب ربط رقم بايتس بصفحة، لذا نقوم أولاً بإنشاء صفحة فارغة ستستقبل كائن الترميز.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

فئة `Document` تمثل ملف PDF بالكامل، بينما تقوم `Pages.Add()` بإدراج صفحة جديدة فارغة في نهاية مجموعة صفحات المستند. وبما أن المستند يبدأ فارغًا، فإن هذا الاستدعاء ينشئ أيضًا الصفحة الأولى.

## الخطوة 3: تكوين كائن ترقيم بايتس

الآن نحدد شكل أرقام بايتس. تسمح لك `BatesNumberingArtifact` بتعيين رقم البداية، البادئة، اللاحقة، وخيارات التنسيق.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**لماذا هذا مهم:**  
تعيين `StartNumber` إلى **1000** يتماشى مع عادات تسمية ملفات القضايا القانونية. تضمن `Prefix` ظهور كل رقم كـ **CASE‑1000**, **CASE‑1001**, … مما يسهل البحث والترتيب.

## الخطوة 4: إرفاق الكائن بالصفحة

يجب إضافة الكائن إلى مجموعة `Artifacts` الخاصة بالصفحة حتى يقوم Aspose برسمه على كل صفحة عند الحفظ.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

عند حفظ المستند، يكرر Aspose الكائن تلقائيًا على جميع الصفحات، مع زيادة الرقم لكل صفحة لاحقة.

## الخطوة 5: (اختياري) إضافة صفحات إضافية

إذا كنت بحاجة إلى مزيد من الصفحات، ما عليك سوى تكرار `pdfDocument.Pages.Add()`. سيظهر كائن ترقيم بايتس الذي أرفقته في الخطوة السابقة تلقائيًا على كل صفحة جديدة.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## الخطوة 6: حفظ PDF – إنشاء PDF برمجيًا

أخيرًا، احفظ المستند على القرص. هذه هي النقطة التي يتم فيها رسم أرقام بايتس على الصفحات.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**النتيجة المتوقعة:**  
افتح *BatesNumberedDocument.pdf* وسترى ملف PDF مكوّن من ثلاث صفحات. كل صفحة تعرض رقم بايتس في الزاوية السفلية اليمنى:

* الصفحة 1 → **CASE‑1000**  
* الصفحة 2 → **CASE‑1001**  
* الصفحة 3 → **CASE‑1002**

يتم زيادة الأرقام تلقائيًا لأن الكائن مرفق بمجموعة الصفحات.

## مثال كامل قابل للتنفيذ

بجمع كل ما سبق، إليك برنامج وحدة تحكم كامل يمكنك نسخه ولصقه وتشغيله:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. بعد التنفيذ، ابحث عن الملف على سطح المكتب وتأكد من أرقام بايتس.

![مثال على إضافة ترقيم بايتس إلى PDF](/images/bates-numbering.png "مثال على إضافة ترقيم بايتس إلى PDF")

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى خط أو موضع مختلف؟

تُظهر `BatesNumberingArtifact` خصائص مثل `FontSize`، `FontColor`، `HorizontalAlignment`، و `VerticalAlignment`. على سبيل المثال:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### كيف يمكن استبعاد صفحة معينة من الترقيم؟

أنشئ كائن `BatesNumberingArtifact` منفصل للصفحات التي تريد ترقيمها وأضفه فقط إلى تلك الصفحات. الصفحات التي لا يحتويها كائن سيبقى ترقيمها غير موجود.

### هل يعمل هذا مع ملفات PDF موجودة؟

نعم. بدلاً من `new Document()`, حمّل ملفًا موجودًا:

```csharp
Document pdfDocument = new Document("input.pdf");
```

ثم أرفق الكائن بالصفحات المطلوبة واحفظ المستند.

## الخلاصة

أنت الآن تعرف **كيفية إضافة ترقيم بايتس إلى PDF** باستخدام Aspose.Pdf، **كيفية إضافة صفحة فارغة إلى PDF**، و**كيفية إنشاء PDF برمجيًا** في حل C# نظيف وقابل لإعادة الاستخدام. يعمل النهج مع أي عدد من الصفحات، بادئات مخصصة، وخيارات تنسيق، مما يمنحك سيطرة كاملة على المستند النهائي.

الخطوات التالية التي قد تستكشفها:

* استخدم **create pdf as

## ماذا ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إضافة وتخصيص أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET | دليل معالجة المستندات](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [كيفية إضافة صفحة فارغة في نهاية ملف PDF باستخدام Aspose.PDF لـ .NET | دليل خطوة بخطوة](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [إنشاء مستند PDF باستخدام Aspose.PDF – إضافة صفحة، شكل وحفظ](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}