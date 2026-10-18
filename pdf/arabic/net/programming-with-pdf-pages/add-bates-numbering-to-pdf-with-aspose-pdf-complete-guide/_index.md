---
category: general
date: 2026-06-30
description: إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose.PDF في C#. تعلّم كيفية
  ترقيم صفحات PDF، وتعيين بادئة مخصصة، وإنشاء مستند ترقيم بايتس موثوق.
draft: false
keywords:
- add bates numbering
- how to add bates
- number pdf pages
- how to number pdf
- bates numbering document
language: ar
og_description: إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose.PDF. يوضح هذا الدليل
  كيفية ترقيم صفحات PDF وإنشاء مستند ترقيم بايتس بلغة C#.
og_title: إضافة ترقيم بيتس إلى PDF – دليل Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  headline: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  name: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  steps:
  - name: Customizing Appearance (Optional)
    text: 'If you need a different font, size, or placement, you can tweak the `BatesNumbering`
      properties:'
  - name: Expected Output
    text: Open `bates_numbered.pdf` in any PDF viewer. You’ll see a label like **CASE‑1000**
      on the first page, **CASE‑1001** on the second, and so on. The numbers appear
      in the bottom‑left corner by default (or wherever you set `XIndent`/`YIndent`).
  - name: 1. What if the PDF is huge (hundreds of MB)?
    text: 'Aspose.PDF streams pages to disk by default, so memory consumption stays
      low. However, you can explicitly enable **compression**:'
  - name: 2. Need a different numbering format (e.g., suffix instead of prefix)?
    text: 'Set the `Suffix` property:'
  - name: 3. How to restart numbering for a new section?
    text: Call `bates.StartNumber = 1;` before processing the next batch, or create
      a second `BatesNumbering` instance.
  - name: 4. The PDF already contains watermarks—will the numbers overlap?
    text: 'Adjust `XIndent` and `YIndent` to move the numbers away from existing elements.
      You can also change the `Position` enum (`BatesNumberingPosition.TopRight`,
      etc.):'
  - name: 5. Does this work with encrypted PDFs?
    text: 'If the source PDF is password‑protected, open it like this:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF processing
- Bates numbering
title: إضافة ترقيم بيتس إلى ملفات PDF باستخدام Aspose.PDF – دليل شامل
url: /ar/net/programming-with-pdf-pages/add-bates-numbering-to-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم Bates إلى PDF باستخدام Aspose.PDF – دليل كامل

هل احتجت يوماً إلى **إضافة ترقيم bates** إلى ملف PDF لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—ففرق القانونية، المدققون، وحتى المطورون غالبًا ما يسألون *كيفية إضافة bates* لتتبع مجموعات المستندات الكبيرة. في هذا الدرس سنستعرض حلاً كاملاً وجاهزًا للتنفيذ يرقم صفحات PDF، يضيف بادئة مخصصة، ويحفظ **مستند ترقيم bates** جديد. لا إطالة، فقط الكود الذي يمكنك نسخه ولصقه اليوم.

سنغطي كل شيء من إعداد Aspose.PDF، اختيار رقم البداية، التعامل مع الحالات الخاصة مثل الملفات الضخمة، وحتى تعديل التنسيق إذا احتجت إلى شيء غير الإعداد الافتراضي. في النهاية ستتمكن من **رقم صفحات pdf** تلقائيًا، وستفهم لماذا هذا النهج قوي وسهل الصيانة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

- .NET 6.0 أو أحدث (المثال يستخدم .NET 6 لكنه يعمل مع .NET Core 3.1+)
- ترخيص Aspose.PDF for .NET (التقييم المجاني يكفي للاختبار)
- ملف PDF تريد معالجته (مسمى `source.pdf` في المثال)
- Visual Studio 2022 أو أي محرر C# تفضله

هذا كل شيء—لا حزم NuGet إضافية بخلاف Aspose.PDF.

## الخطوة 1: تثبيت Aspose.PDF for .NET

افتح الطرفية أو وحدة تحكم مدير الحزم وشغّل:

```bash
dotnet add package Aspose.PDF
```

أو، داخل Visual Studio:

```
Tools → NuGet Package Manager → Manage NuGet Packages for Solution…
Search “Aspose.PDF” and click Install.
```

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة آلاف الصفحات، فعّل **وضع توفير الذاكرة في Aspose.PDF** عن طريق ضبط `PdfConversion.SaveOptions.UseObjectPooling = true;` لاحقًا.

## الخطوة 2: إنشاء هيكل تطبيق Console بسيط

لننشئ تطبيق console بسيط حتى تتمكن من تشغيل الكود فورًا:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in the next steps.
        }
    }
}
```

احفظ الملف باسم `Program.cs`. هذا الهيكل يمنحنا مكانًا نظيفًا لإضافة منطق **ترقيم bates**.

## الخطوة 3: فتح مستند PDF المصدر

العملية الأولى الفعلية هي فتح ملف PDF الذي تريد وضع الطوابع عليه. سنستخدم كتلة `using` حتى يتم تحرير مقبض الملف تلقائيًا:

```csharp
// Step 3: Open the source PDF document
using (var doc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // Subsequent steps go here.
}
```

> **لماذا نستخدم كتلة `using`؟** لأنها تضمن إغلاق تدفق الملف الأساسي، مما يمنع مشاكل قفل الملف عندما تحاول لاحقًا استبدال نفس الملف.

## الخطوة 4: إعداد واجهة BatesNumbering

توفر Aspose.PDF واجهة مريحة تسمى `BatesNumbering`. إنها تخفي التعامل منخفض المستوى صفحة بصفحة وتتيح لك التركيز على الترقيم نفسه.

```csharp
// Step 4: Create a Bates numbering facade
var bates = new BatesNumbering
{
    // Step 4a: Choose the starting number
    StartNumber = 1000,

    // Step 4b: Add an optional prefix (e.g., CASE-)
    Prefix = "CASE-"
    
    // You can also set a suffix, font size, or position if needed.
};
```

### تخصيص المظهر (اختياري)

إذا كنت بحاجة إلى خط مختلف، حجم مختلف، أو موضع مختلف، يمكنك تعديل خصائص `BatesNumbering`:

```csharp
bates.FontSize = 10;               // Smaller than the default 12
bates.TextColor = Color.Black;    // Ensure high contrast
bates.XIndent = 20;               // Move number 20 points from the left edge
bates.YIndent = 30;               // Move number 30 points from the bottom edge
```

هذه الإعدادات مفيدة عندما يتداخل الموضع الافتراضي مع المحتوى الموجود.

## الخطوة 5: تطبيق ترقيم Bates على المستند

الآن نقوم فعليًا بوضع الأرقام على كل صفحة:

```csharp
// Step 5: Apply the Bates numbering to the document
bates.AddBatesNumbering(doc);
```

خلف الكواليس، تقوم Aspose.PDF بالتكرار على كل صفحة، وتدرج السلسلة المنسقة (مثل `CASE-1000`, `CASE-1001`, …)، وتراعي أي خيارات تخطيط قمت بتحديدها مسبقًا.

## الخطوة 6: حفظ ملف PDF المرقم حديثًا

أخيرًا، اكتب النتيجة إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد—سنحتفظ بالاثنين للسلامة:

```csharp
// Step 6: Save the newly numbered PDF
doc.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering applied successfully!");
```

تشغيل البرنامج يجب أن ينتج ملفًا باسم `bates_numbered.pdf` مع كل صفحة معنونة بوضوح.

### النتيجة المتوقعة

افتح `bates_numbered.pdf` في أي عارض PDF. سترى تسمية مثل **CASE‑1000** على الصفحة الأولى، **CASE‑1001** على الصفحة الثانية، وهكذا. تظهر الأرقام في الزاوية السفلية اليسرى افتراضيًا (أو في أي موضع حددته بـ `XIndent`/`YIndent`).

## مثال عملي كامل

بدمج جميع الأجزاء معًا، إليك الكود الكامل الذي يمكنك نسخه ولصقه:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            const string sourcePath = "YOUR_DIRECTORY/source.pdf";
            const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";

            // Open the source PDF
            using (var doc = new Document(sourcePath))
            {
                // Configure Bates numbering
                var bates = new BatesNumbering
                {
                    StartNumber = 1000,
                    Prefix = "CASE-",
                    // Optional customizations:
                    // FontSize = 10,
                    // TextColor = Color.Black,
                    // XIndent = 20,
                    // YIndent = 30
                };

                // Apply numbering
                bates.AddBatesNumbering(doc);

                // Save the result
                doc.Save(outputPath);
                Console.WriteLine($"Bates numbering added. Saved to: {outputPath}");
            }
        }
    }
}
```

شغّل `dotnet run` من مجلد المشروع، وسترى رسالة في وحدة التحكم تؤكد نجاح العملية.

## حالات خاصة وأسئلة شائعة

### 1. ماذا لو كان ملف PDF ضخمًا (مئات الميجابايت)؟

تقوم Aspose.PDF بتدفق الصفحات إلى القرص افتراضيًا، لذا يبقى استهلاك الذاكرة منخفضًا. ومع ذلك، يمكنك تمكين **الضغط** صراحةً:

```csharp
doc.Compress();
```

### 2. هل تحتاج إلى تنسيق ترقيم مختلف (مثلاً لاحقة بدلًا من بادئة)؟

عيّن خاصية `Suffix`:

```csharp
bates.Suffix = "-2026";
```

يمكنك الجمع بينهما:

```csharp
bates.Prefix = "CASE-";
bates.Suffix = "-2026";
```

النتيجة: `CASE-1000-2026`.

### 3. كيف تعيد بدء الترقيم لقسم جديد؟

استدعِ `bates.StartNumber = 1;` قبل معالجة الدفعة التالية، أو أنشئ نسخة ثانية من `BatesNumbering`.

### 4. إذا كان PDF يحتوي بالفعل على علامات مائية—هل سيتداخل الترقيم؟

عدّل `XIndent` و `YIndent` لإبعاد الأرقام عن العناصر الموجودة. يمكنك أيضًا تغيير تعداد `Position` (`BatesNumberingPosition.TopRight`، إلخ):

```csharp
bates.Position = BatesNumberingPosition.TopRight;
```

### 5. هل يعمل هذا مع ملفات PDF مشفرة؟

إذا كان PDF المصدر محميًا بكلمة مرور، افتحه هكذا:

```csharp
var doc = new Document(sourcePath, new LoadOptions { Password = "yourPassword" });
```

بقية سير العمل تبقى دون تغيير.

## نصائح لتطبيقات جاهزة للإنتاج

- **الترخيص مبكرًا**: أدرج `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` في بداية `Main` لتجنب علامة التقييم.
- **المعالجة المتوازية**: للعمليات الدفعة على العديد من الملفات، غلف منطق كل ملف داخل حلقة `Parallel.ForEach`—مع مراعاة حدود الإدخال/الإخراج.
- **التسجيل**: استخدم `Ser

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إضافة طوابع ترقيم الصفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET | العلامات المائية والخلفيات](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [كيفية إضافة وتخصيص أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET | دليل معالجة المستندات](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [كيفية إضافة طابع نصي إلى PDF باستخدام Aspose.PDF .NET: دليل شامل](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}