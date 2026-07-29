---
category: general
date: 2026-07-03
description: دروس ترقيم بايتس توضح كيفية إضافة ترقيم بايتس لملفات PDF باستخدام Aspose.PDF.
  يتضمن إعداد بادئة رقم بايتس ومثالًا كاملاً على ترقيم بايتس.
draft: false
keywords:
- bates numbering tutorial
- add bates numbering pdf
- bates numbering example
- prefix bates number
language: ar
og_description: دورة تعليمية حول ترقيم بايتس تُرشدك إلى إضافة ترقيم بايتس لملفات PDF،
  وتعيين بادئة لرقم بايتس، وتقديم مثال عملي كامل.
og_title: 'دليل ترقيم بيتس: إضافة أرقام إلى ملف PDF باستخدام Aspose'
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  headline: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  type: TechArticle
- description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  name: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  steps:
  - name: What if I need to reset the counter for each section?
    text: You can call `pdfDocument.BatesNumbering.Reset()` before processing a new
      range of pages. Combine it with a loop over `pdfDocument.Pages` and set `Start`
      again for each section.
  - name: How do I apply different prefixes to different page ranges?
    text: 'Create multiple `BatesNumbering` objects—one per range—by cloning the document
      or by using the `Add` method (available in newer Aspose versions). Here’s a
      quick sketch:'
  - name: Does the library support Unicode prefixes?
    text: Absolutely. Pass any Unicode string (e.g., `"案件‑"`). Aspose.PDF handles
      right‑to‑left scripts and special symbols without extra configuration.
  - name: What about PDF security—will Bates numbering break encryption?
    text: If the source PDF is encrypted, you must provide the password before accessing
      `BatesNumbering`. The numbering process respects the original encryption settings—your
      output will stay encrypted unless you explicitly change it.
  type: HowTo
tags:
- Aspose.PDF
- PDF processing
- Bates numbering
title: 'دليل ترقيم بيتس: إضافة أرقام إلى PDF باستخدام Aspose'
url: /ar/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-numbers-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل ترقيم باتس – إضافة أرقام باتس إلى ملفات PDF باستخدام Aspose

هل احتجت يومًا إلى **دليل ترقيم باتس** لأنك اضطررت لتوسيم آلاف الصفحات لأغراض التقاضي؟ لست وحدك. في العديد من سير عمل القانونية والامتثال، طريقة موثوقة لـ *إضافة ترقيم باتس إلى ملفات PDF* هي مطلب لا يمكن التفاوض عليه. لحسن الحظ، تجعل Aspose.PDF العملية بأكملها سهلة للغاية، وفي هذا الدليل سنستعرض مثالًا كاملًا لـ **ترقيم باتس** يمكنك إدراجه مباشرةً في مشروعك.

> **ما ستحصل عليه:** مقطع شفرة قابل للتنفيذ يحدد رقم البداية، يطبق **بادئة رقم باتس**، ويحفظ النتيجة—كل ذلك في أقل من 30 سطرًا من C#.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (تعمل الواجهة البرمجية بنفس الطريقة على .NET Framework 4.6+)
- ترخيص صالح لـ Aspose.PDF for .NET (أو يمكنك استخدام وضع التقييم المجاني)
- ملف PDF إدخال يُدعى `input.pdf` موجود في مجلد تتحكم به
- Visual Studio 2022 أو أي محرر يدعم مشاريع C#

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf`.

## الخطوة 1: تثبيت Aspose.PDF for .NET

افتح الطرفية (أو وحدة تحكم مدير الحزم) وشغّل:

```bash
dotnet add package Aspose.Pdf
```

أو، إذا كنت تفضّل الواجهة الرسومية، انقر بزر الماوس الأيمن على **Dependencies → Manage NuGet Packages**، ابحث عن *Aspose.Pdf*، وانقر **Install**. سيقوم ذلك بتنزيل أحدث نسخة مستقرة (اعتبارًا من يوليو 2026، الإصدار 23.12).

## الخطوة 2: فتح مستند PDF المصدر

السطر الأول في أي سير عمل **إضافة ترقيم باتس إلى PDF** هو تحميل الملف الذي تريد وضع العلامة عليه. سنغلف العملية داخل كتلة `using` حتى يتم تحرير المستند تلقائيًا.

```csharp
using Aspose.Pdf;

// Step 2: Load the PDF you want to number
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here...
}
```

> **نصيحة احترافية:** إذا كان ملف PDF الخاص بك موجودًا في سحابة، يمكنك تمرير `Stream` بدلاً من مسار الملف—Aspose.PDF يتعامل مع كليهما بسلاسة.

## الخطوة 3: تعيين رقم البداية والبادئة

الآن يأتي جوهر **مثال ترقيم باتس**: إخبار Aspose من أين يبدأ وما النص الذي يجب أن يسبق كل رقم. خاصية `BatesNumbering` تكشف عن كل من `Start` و `Prefix`.

```csharp
    // Step 3a: Define where the numbering begins
    pdfDocument.BatesNumbering.Start = 1000;   // you can start anywhere

    // Step 3b: Add a custom prefix – this is the prefix bates number you asked for
    pdfDocument.BatesNumbering.Prefix = "ABC-";
```

لماذا نحتاج إلى البادئة؟ في العديد من القضايا القانونية تُحدد البادئة ملف القضية أو القسم أو دفعة الإنتاج. باستخدام `"ABC-"` كقالب، يمكنك تغييره إلى `"CASE42-"` أو أي سلسلة تناسب نمط التسمية الخاص بك.

## الخطوة 4: اختيار موضع ظهور الأرقام (اختياري)

الافتراضي في Aspose هو وضع الرقم في الزاوية السفلية اليمنى، لكن يمكنك تحريكه إلى أي مكان بتعديل خاصية `Location`. هذه الخطوة ليست إلزامية لعملية **إضافة ترقيم باتس إلى PDF** الأساسية، لكنها مفيدة لمعرفة.

```csharp
    // Optional: Move the number to the top‑left corner
    pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);
```

خاصية `Location` تأخذ إحداثيات X و Y مقاسة بالنقاط (1 pt ≈ 1/72 in). عدّلها حسب حاجة تخطيط صفحتك.

## الخطوة 5: حفظ ملف PDF المحدث

أخيرًا، احفظ التغييرات. طريقة `Save` على `BatesNumbering` تكتب ملفًا جديدًا مع الحفاظ على الأصل دون تعديل.

```csharp
    // Step 5: Write the output file with numbering applied
    pdfDocument.BatesNumbering.Save("YOUR_DIRECTORY/output.pdf");
}
```

عند فتح `output.pdf`، سيظهر على كل صفحة شيء مثل `ABC-1000`، `ABC-1001`، … حتى آخر صفحة.

## مثال عملي كامل

بجمع كل ما سبق، إليك **مثال ترقيم باتس** يمكنك نسخه ولصقه في طريقة `Main` لتطبيق console:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path configuration – adjust to your environment
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        // Load the PDF
        using (var pdfDocument = new Document(inputPath))
        {
            // Set start number and prefix
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "ABC-";

            // (Optional) Change location – comment out if default is fine
            // pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);

            // Save the numbered PDF
            pdfDocument.BatesNumbering.Save(outputPath);
        }

        Console.WriteLine($"Bates numbering applied! Check: {outputPath}");
    }
}
```

**الناتج المتوقع** (في وحدة التحكم):

```
Bates numbering applied! Check: YOUR_DIRECTORY\output.pdf
```

افتح ملف PDF المُولد وسترى أرقامًا متسلسلة مسبوقة بـ `ABC-` بدءًا من `1000`.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت لإعادة ضبط العداد لكل قسم؟

يمكنك استدعاء `pdfDocument.BatesNumbering.Reset()` قبل معالجة نطاق جديد من الصفحات. اجمع ذلك مع حلقة عبر `pdfDocument.Pages` واضبط `Start` مرة أخرى لكل قسم.

### كيف أطبق بادئات مختلفة على نطاقات صفحات مختلفة؟

أنشئ عدة كائنات `BatesNumbering`—واحد لكل نطاق—عن طريق استنساخ المستند أو باستخدام طريقة `Add` (متوفرة في إصدارات Aspose الأحدث). إليك مخطط سريع:

```csharp
// Number first 10 pages with "PRE‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "PRE-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(1, 10));

// Number the rest with "POST‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "POST-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(11, pdfDocument.Pages.Count));
```

### هل تدعم المكتبة بادئات Unicode؟

بالتأكيد. مرّر أي سلسلة Unicode (مثلاً، `"案件‑"`). Aspose.PDF يتعامل مع النصوص من اليمين إلى اليسار والرموز الخاصة دون إعداد إضافي.

### ماذا عن أمان PDF—هل سيؤدي ترقيم باتس إلى كسر التشفير؟

إذا كان ملف PDF المصدر مشفرًا، يجب توفير كلمة المرور قبل الوصول إلى `BatesNumbering`. عملية الترميز تحترم إعدادات التشفير الأصلية—ستظل النتيجة مشفرة ما لم تقم بتغيير ذلك صراحة.

```csharp
pdfDocument.Encrypt(new DocumentEncryption("ownerPwd", "userPwd"));
```

## نصائح وممارسات أفضل

- **معالجة دفعات:** غلف الروتين بالكامل داخل حلقة `foreach` لمعالجة العشرات من الملفات تلقائيًا.
- **التسجيل:** سجّل رقم البداية، البادئة، ومسار الإخراج في ملف سجل؛ هذا يسهل تتبع التدقيق للفرق القانونية.
- **الأداء:** بالنسبة لملفات PDF الضخمة (500 صفحة فأكثر)، فكر في تمكين **تحسين الذاكرة** عبر `pdfDocument.OptimizeMemory = true;`.
- **الاختبار:** احتفظ دائمًا بنسخة من ملف PDF الأصلي؛ ترقيم باتس لا يمكن عكسه بعد الحفظ.

## الخلاصة

في هذا **دليل ترقيم باتس** غطينا كل ما تحتاجه **لإضافة ترقيم باتس إلى ملفات PDF** باستخدام Aspose.PDF:

1. تثبيت المكتبة.
2. تحميل المستند المصدر.
3. تعيين رقم البداية و **بادئة رقم باتس**.
4. (اختياري) تعديل الموضع.
5. حفظ النتيجة.

الآن لديك **مثال ترقيم باتس** قوي يمكنك تكييفه مع أي سير عمل قانوني أو أرشيفي أو امتثالي. هل تريد التعمق أكثر؟ جرّب دمج أرقام باتس مع العلامات المائية، أو أنشئ ملف CSV يربط كل صفحة بمعرّفها. لا حدود للابتكار، وAspose توفر لك الأدوات للوصول إلى ذلك.

---

*هل أنت مستعد لنشر هذا في الإنتاج؟ اترك تعليقًا إذا واجهت أي مشاكل، وتمنياتنا لك بالبرمجة السعيدة!*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aspose Pdf Net Floatingbox Page Numbering](/pdf/german/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}