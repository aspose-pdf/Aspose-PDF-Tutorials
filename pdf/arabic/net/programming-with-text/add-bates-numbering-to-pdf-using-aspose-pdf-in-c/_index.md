---
category: general
date: 2026-09-27
description: إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose.PDF في C#. تعلم كيفية تحميل
  مستند PDF، وضبط خيارات ترقيم بايتس، وحفظ الملف المحدث.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: ar
lastmod: 2026-09-27
og_description: إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose.PDF في C#. يوضح هذا
  الدليل كيفية تحميل مستند PDF، وتكوين ترقيم بايتس، وحفظ النتيجة.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: إضافة ترقيم باتس إلى PDF باستخدام Aspose.PDF – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: إضافة ترقيم باتس إلى ملف PDF باستخدام Aspose.PDF في C#
url: /ar/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم بايتس إلى PDF باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **إضافة ترقيم بايتس** إلى ملف PDF، يوضح لك هذا الدليل حلاً كاملاً وجاهزًا للتنفيذ. ستتعرف على كيفية **تحميل مستند PDF**، وتكوين خيارات ترقيم بايتس، وكتابة الملف المرقم مرة أخرى إلى القرص—كل ذلك باستخدام Aspose.PDF لـ .NET.

تطبيق أرقام بايتس شائع في الأعمال القانونية، وإنفاذ القانون، وسير العمل الأرشيفي. بنهاية هذا الشرح يمكنك تضمين معرف تسلسلي على كل صفحة، وتخصيص البادئة، والبدء بالعد من أي رقم تختاره.

## ما ستتعلمه

* كيفية **تحميل محتوى مستند PDF** إلى كائن `Aspose.Pdf.Document`.  
* الخطوات الدقيقة **لإضافة ترقيم بايتس** باستخدام `BatesNumberingOptions`.  
* كيفية حفظ الملف المعدل مع الحفاظ على التخطيط الأصلي والجودة.  

لا تحتاج إلى أدوات خارجية—فقط حزمة Aspose.PDF NuGet وبيئة تطوير .NET (Visual Studio، VS Code، أو Rider).  

---

## الخطوة 1: تثبيت Aspose.PDF لـ .NET

افتح مجلد المشروع في الطرفية وقم بتشغيل:

```bash
dotnet add package Aspose.PDF
```

تتضمن الحزمة مساحة الاسم `Aspose.Pdf`، التي توفر جميع الفئات المستخدمة في هذا الشرح. بعد التثبيت، أعد تحميل المشروع حتى يلتقط IDE المرجع الجديد.

## الخطوة 2: تحميل مستند PDF

تحميل الملف المصدر هو العملية الأولى لأن محرك ترقيم بايتس يعمل على كائن `Document` موجود.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**لماذا هذا مهم:** فئة `Document` تحلل بنية PDF، وتمنحك الوصول إلى الصفحات، والتعليقات التوضيحية، والبيانات الوصفية. بدون تحميل الملف أولاً، لا يمكنك تطبيق أي ترقيم.

## الخطوة 3: تكوين خيارات ترقيم بايتس

أنشئ كائن `BatesNumberingOptions` وحدد البادئة المطلوبة، ورقم البداية، ومعلمات التنسيق الاختيارية.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**لماذا هذا مهم:** `BatesNumberingOptions` تخبر Aspose.PDF كيفية إنشاء التسمية لكل صفحة. تساعدك `Prefix` على تجميع القضايا المرتبطة، بينما يتيح لك `StartNumber` متابعة تسلسل من دفعة سابقة.

## الخطوة 4: حفظ PDF مع تطبيق ترقيم بايتس

مرّر كائن الخيارات إلى طريقة `Save`. تقوم Aspose.PDF بكتابة الأرقام مباشرة على كل صفحة.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**لماذا هذا مهم:** التحميل الزائد `Save(string, BatesNumberingOptions)` يجمع خطوة التصيير مع عملية الترقيم، مما يضمن أن يحتوي ملف الإخراج على المعرفات المرئية.

## مثال كامل – كل شيء معًا

فيما يلي برنامج واحد مستقل يمكنك نسخه، لصقه، وتشغيله. يوضح **كيفية إضافة ترقيم بايتس** من البداية إلى النهاية.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج ينتج `output.pdf` حيث تعرض كل صفحة تسمية مشابهة لـ:

```
CASE01-1
CASE01-2
CASE01-3
...
```

تظهر الأرقام في التذييل بشكل افتراضي، ولكن يمكنك نقلها بتعديل خاصية `Margin` في `BatesNumberingOptions`.

## الحالات الخاصة والاختلافات الشائعة

| الحالة | ما الذي يجب تعديله |
|-----------|----------------|
| **بادئة مختلفة لكل دفعة** | غيّر `Prefix` قبل استدعاء `Save`. يمكنك تكرار العملية على مستندات متعددة ببادئات مميزة. |
| **متابعة الترقيم من ملف سابق** | عيّن `StartNumber` إلى آخر رقم مستخدم + 1. |
| **وضع الأرقام في الترويسة** | استخدم `batesOptions.Margin = new Margin(20, 0, 0, 0);` (هامش أعلى) أو خصّص `batesOptions.Position`. |
| **خط أو لون مخصص** | عيّن خصائص `Font`، `FontSize`، و`Color` كما هو موضح في القسم المعلق. |
| **ملفات PDF الكبيرة (1000+ صفحة)** | العملية فعّالة في الذاكرة؛ ومع ذلك قد ترغب في تمكين `doc.OptimizeResources()` قبل الحفظ لتقليل حجم الملف. |

**نصيحة احترافية:** إذا كان سير العمل الخاص بك يتطلب مخططات ترقيم مختلفة لكل مستند، غلف المنطق في طريقة مساعدة:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## الخلاصة

أنت الآن تعرف **كيفية إضافة ترقيم بايتس** إلى أي ملف PDF باستخدام Aspose.PDF في C#. غطّى الشرح تحميل مستند PDF، تكوين خيارات الترقيم، وحفظ الملف النهائي—كل ذلك في برنامج واحد قابل للتنفيذ.  

من هنا يمكنك استكشاف مواضيع ذات صلة مثل **إضافة علامات مائية**، **دمج ملفات PDF متعددة**، أو **استخراج النص** باستخدام Aspose.PDF. جرّب خطوطًا، ألوانًا، ومواقع مختلفة لتتناسب مع معايير تنسيق مؤسستك.

هل أنت مستعد لأتمتة سير عمل المستندات القانونية؟ أضف الشيفرة إلى خط أنابيب البناء الخاص بك، شغّلها على دفعات من الملفات، ودع Aspose.PDF يتولى العمل الشاق. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند PDF C# – إضافة ترقيم بايتس](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [إضافة ترقيم بايتس PDF – دليل خطوة بخطوة لترقيم صفحات PDF](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [دورة Aspose PDF – إدراج صفحة فارغة وتحديث ترقيم بايتس](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}