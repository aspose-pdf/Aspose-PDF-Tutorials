---
category: general
date: 2026-09-27
description: كيفية إضافة نص إلى ملف PDF باستخدام Aspose.PDF وتحديد موضع النص في صفحات
  PDF. اتبع هذا الدليل خطوة بخطوة لإدراج النص في صفحة PDF بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add text pdf
- position text in pdf
- insert text pdf page
- aspose pdf add text
- access specific pdf page
language: ar
lastmod: 2026-09-27
og_description: كيفية إضافة نص إلى ملف PDF باستخدام Aspose.PDF. تعلم كيفية وضع النص
  في PDF، إدراج نص في صفحة PDF، والوصول إلى صفحة PDF محددة مع أمثلة شفرة واضحة.
og_image_alt: Screenshot showing how to add text PDF with Aspose.PDF in C#
og_title: كيفية إضافة نص إلى PDF باستخدام Aspose.PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to add text PDF using Aspose.PDF and position text in PDF pages.
    Follow this step‑by‑step guide to insert text PDF page efficiently.
  headline: How to add text PDF with Aspose.PDF in C#
  type: TechArticle
- description: How to add text PDF using Aspose.PDF and position text in PDF pages.
    Follow this step‑by‑step guide to insert text PDF page efficiently.
  name: How to add text PDF with Aspose.PDF in C#
  steps:
  - name: Load the PDF document
    text: '```csharp // Step 1: Load the PDF document var document = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf");
      ```'
  - name: Access the specific PDF page
    text: '```csharp // Step 2: Access the second page (index starts at 1) var page
      = document.Pages[1]; ```'
  - name: Position text in PDF
    text: '```csharp // Step 3: Create a tagged content element positioned at (100,
      200) on the page var taggedContent = new Aspose.Pdf.TaggedContent(page) { X
      = 100, Y = 200 }; ```'
  - name: Insert text PDF page
    text: '```csharp // Step 4: Add a text fragment to the tagged content taggedContent.Add(new
      Aspose.Pdf.Text.TextFragment("Important")); ```'
  - name: Save the modified PDF
    text: '```csharp // Step 5: Save the modified PDF document.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Expected output
    text: 'When you open `output.pdf`:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: كيفية إضافة نص إلى ملف PDF باستخدام Aspose.PDF في C#
url: /ar/net/programming-with-text/how-to-add-text-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة نص إلى PDF باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **كيفية إضافة نص إلى PDF** بطريقة برمجية، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.PDF لـ .NET. ستتعلم كيفية وضع النص في PDF، وإدراج نص في صفحة PDF، والوصول إلى صفحة PDF محددة دون مغادرة بيئة التطوير المتكاملة الخاصة بك.

يغطي الدرس كل شيء بدءًا من تثبيت المكتبة وحتى حفظ المستند النهائي، بحيث يمكنك نسخ الشيفرة وتشغيلها فورًا. لا توجد مراجع خارجية مطلوبة—فقط الخطوات أدناه.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 (أو أحدث) مثبت.
* Visual Studio 2022 أو أي بيئة تطوير متكاملة تدعم C#.
* حزمة NuGet الخاصة بـ Aspose.PDF for .NET (`Aspose.Pdf`) مضافة إلى مشروعك.
* ملف PDF مصدر (`input.pdf`) موجود في دليل معروف.

هذه المتطلبات تضمن أن الشيفرة تُترجم وأن معالجة PDF تعمل كما هو متوقع.

## كيفية إضافة نص إلى PDF باستخدام Aspose.PDF

الأقسام التالية تقسم العملية إلى خطوات منفصلة وسهلة المتابعة. كل خطوة تشرح **لماذا** هي مهمة، وليس فقط **ماذا** تكتب.

### الخطوة 1: تحميل مستند PDF

```csharp
// Step 1: Load the PDF document
var document = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf");
```

**لماذا هذا مهم:** تحميل المستند ينشئ تمثيلًا في الذاكرة يمكن لـ Aspose.PDF تعديلّه. بدون هذا الكائن لا يمكنك الوصول إلى الصفحات أو إضافة محتوى.

### الخطوة 2: الوصول إلى صفحة PDF المحددة

```csharp
// Step 2: Access the second page (index starts at 1)
var page = document.Pages[1];
```

**لماذا هذا مهم:** صفحات PDF تُعدّ من 1 في Aspose.PDF، لذا `Pages[1]` تُعيد الصفحة الثانية. استخدام الفهرس الصحيح ضروري عندما تحتاج إلى **الوصول إلى صفحة PDF محددة** للتعديل.

### الخطوة 3: وضع النص في PDF

```csharp
// Step 3: Create a tagged content element positioned at (100, 200) on the page
var taggedContent = new Aspose.Pdf.TaggedContent(page) { X = 100, Y = 200 };
```

**لماذا هذا مهم:** خاصيتي `X` و `Y` تحددان الزاوية السفلية اليسرى للنص بالنقاط (1 pt ≈ 1/72 in). تعديل هذه القيم يتيح لك **وضع النص في PDF** بدقة في المكان الذي تريد.

### الخطوة 4: إدراج نص في صفحة PDF

```csharp
// Step 4: Add a text fragment to the tagged content
taggedContent.Add(new Aspose.Pdf.Text.TextFragment("Important"));
```

**لماذا هذا مهم:** `TextFragment` يمثل سلسلة من الأحرف. إضافته إلى عنصر `TaggedContent` في الواقع **يدرج نصًا في صفحة PDF** عند الإحداثيات المحددة في الخطوة السابقة.

### الخطوة 5: حفظ ملف PDF المعدل

```csharp
// Step 5: Save the modified PDF
document.Save("YOUR_DIRECTORY/output.pdf");
```

**لماذا هذا مهم:** حفظ التغييرات يكتب ملف PDF الجديد إلى القرص. الآن يحتوي ملف الإخراج على كلمة “Important” في الصفحة الثانية بالموقع المحدد بالضبط.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في تطبيق كونسول. يتضمن جميع توجيهات `using` الضرورية وتعليقات لتوضيح الفكرة.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace PdfTextAdder
{
    class Program
    {
        static void Main()
        {
            // Load the existing PDF
            var document = new Document("YOUR_DIRECTORY/input.pdf");

            // Access the second page (index starts at 1)
            var page = document.Pages[1];

            // Create a tagged content element at (100, 200)
            var taggedContent = new TaggedContent(page) { X = 100, Y = 200 };

            // Add the text fragment "Important"
            taggedContent.Add(new TextFragment("Important"));

            // Save the result
            document.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("Text added successfully. Check output.pdf.");
        }
    }
}
```

### النتيجة المتوقعة

عند فتح `output.pdf`:

* تحتوي الصفحة الثانية على كلمة **Important** موضوعة على بعد 100 pt من الحافة اليسرى و200 pt من الحافة السفلية.
* جميع الصفحات الأخرى تبقى دون تغيير.

إذا وضعت الإحداثيات خارج حدود الصفحة، سيتم قص النص. عدّل `X` و `Y` وفقًا لذلك.

## الاختلافات الشائعة وحالات الحافة

| الحالة | طريقة المعالجة |
|-----------|---------------|
| **رقم صفحة مختلف** | غيّر `document.Pages[1]` إلى الفهرس القائم على 1 المطلوب. |
| **عدة مقاطع نصية** | استدعِ `taggedContent.Add(new TextFragment("First"));` ثم أضف استدعاءات `Add` إضافية. |
| **تغيير نمط الخط** | أنشئ `TextFragment`، عيّن `TextState.Font` و `TextState.FontSize`، ثم أضفه إلى `taggedContent`. |
| **نص مائل** | عيّن `taggedContent.Rotation = 90;` قبل إضافة المقطع. |
| **ملفات PDF كبيرة** | حمّل المستند باستخدام `Document.LoadOptions` لتفعيل البث الفعال للذاكرة. |

تتيح لك هذه الاختلافات توسيع نمط **aspose pdf add text** الأساسي لتلبية متطلبات أكثر تعقيدًا.

## نصائح احترافية

* **نظام الإحداثيات:** يستخدم PDF أصلًا في الزاوية السفلية اليسرى. إذا كنت معتادًا على إحداثيات الزاوية العلوية اليسرى (مثل HTML)، اطرح قيمة Y من ارتفاع الصفحة.
* **الأداء:** أعد استخدام كائن `Document` واحد عند معالجة العديد من الصفحات لتجنب عمليات I/O المتكررة.
* **الأمان:** اعمل دائمًا على نسخة من ملف PDF الأصلي للحفاظ على الملف المصدر.

## الخلاصة

أنت الآن تعرف **كيفية إضافة نص إلى PDF** باستخدام Aspose.PDF، وكيفية **وضع النص في PDF**، وكيفية **إدراج نص في صفحة PDF**، وكيفية **الوصول إلى صفحة PDF محددة**. باتباع الخطوات أعلاه يمكنك تضمين أي سلسلة نصية في أي موقع داخل مستند PDF برمجيًا.

هل أنت مستعد لاستكشاف المزيد؟ جرّب إضافة صور، أو رسم أشكال، أو إنشاء جداول باستخدام Aspose.PDF. كل من هذه المواضيع يبني على نفس المبادئ التي أتقنتها الآن.

---

![مثال على كيفية إضافة نص إلى PDF](image.png)


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إضافة ختم نصي إلى PDF باستخدام Aspose.PDF .NET: دليل شامل](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [كيفية تدوير النص في ملفات PDF باستخدام Aspose.PDF for .NET: دليل خطوة بخطوة](/pdf/english/net/text-operations/rotate-text-aspose-pdf-net-guide/)
- [إضافة، تعديل، واستخراج النص باستخدام Aspose.PDF for .NET](/pdf/english/net/programming-with-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}