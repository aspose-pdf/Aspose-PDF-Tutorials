---
category: general
date: 2026-02-28
description: إنشاء مستند PDF باستخدام C# مع ترقيم بيتس. تعلم كيفية إضافة ترقيم بيتس
  إلى PDF، وتعيين البوادئ، وتوليد أرقام PDF متسلسلة في دليل واحد.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: ar
og_description: إنشاء مستند PDF باستخدام C# مع ترقيم بيتس. يوضح هذا الدرس كيفية إضافة
  ترقيم بيتس إلى PDF، وتعيين بادئات مخصصة، وإنتاج أرقام PDF متسلسلة.
og_title: إنشاء مستند PDF باستخدام C# – إضافة ترقيم بايتس
tags:
- Aspose.PDF
- C#
- PDF automation
title: إنشاء مستند PDF بلغة C# – دليل إضافة ترقيم بيتس
url: /ar/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF باستخدام C# – دليل إضافة ترقيم Bates

هل تساءلت يومًا كيف **إنشاء مستند PDF C#** يحمل معرفًا فريدًا على كل صفحة؟ هذه مشكلة شائعة عندما تحتاج إلى تتبع الملفات القانونية، أو ملفات المحكمة، أو أي مجموعة من ملفات PDF يجب أن تكون قابلة للبحث عبر رقم. الخبر السار؟ مع Aspose.PDF يمكنك إضافة أرقام Bates ببضع أسطر من الشيفرة—دون الحاجة إلى تعديل يدوي.

في هذا الدليل سنستعرض العملية بالكامل: تحميل ملف PDF موجود، تكوين **add bates numbering pdf**، تطبيق الأرقام، وأخيرًا حفظ النتيجة. بنهاية القراءة ستكون قادرًا على **add document identification numbers** وحتى **add sequential PDF numbers** تلقائيًا، كل ذلك من خلال C#.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (تعمل الواجهة البرمجية أيضًا مع .NET Framework 4.5+)
- نسخة مرخصة من **Aspose.PDF for .NET** (الإصدار التجريبي المجاني يكفي للاختبار)
- ملف PDF إدخال تريد ترقيمه (سنسميه `input.pdf`)
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.PDF.

![إنشاء مستند PDF باستخدام C# مع ترقيم Bates](https://example.com/image.png "مثال إنشاء مستند PDF باستخدام C#")

## الخطوة 1: تحميل مستند PDF المصدر

قبل أن تتمكن من **add bates numbering pdf**، تحتاج إلى كائن `Document` يمثل الملف على القرص.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*لماذا هذا مهم*: فئة `Document` هي نقطة الدخول لكل عملية في Aspose.PDF. فهي تج abstracts نظام الملفات، بحيث يمكنك التعامل مع الصفحات، التعليقات، والبيانات الوصفية دون الحاجة إلى التعامل مع البايتات الخام.

> **نصيحة احترافية:** إذا كنت تعالج العديد من الملفات داخل حلقة، أعد استخدام نفس كائن `Document` فقط عندما يكون المصدر متطابقًا؛ وإلا، أنشئ كائنًا جديدًا لكل ملف لتجنب تسرب الذاكرة.

## الخطوة 2: تعريف خيارات ترقيم Bates

هنا يصبح جزء **how to add bates** ملموسًا. تقوم بتكوين كائن `BatesNumberingOptions` لتخبر Aspose ما هو البادئة التي يجب استخدامها، من أين يبدأ، وحجم الخط المطلوب.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*لماذا هذا مهم*: تسمح لك الخاصية `Prefix` بإدراج معرف القضية (مثال: “ABC-”). الخاصية `Start` أساسية عندما تقوم **adding sequential PDF numbers** عبر مستندات متعددة—فقط استمر في زيادة القيمة. و`FontSize` يضمن أن الأرقام لا تعيق المحتوى الموجود.

## الخطوة 3: تطبيق ترقيم Bates على المستند بالكامل

الآن نقوم فعليًا بطباعة الأرقام على كل صفحة. تقوم فئة `BatesNumbering` بكل العمل الشاق.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*لماذا هذا مهم*: في الخلفية، تقوم Aspose بزيارة كل صفحة، تحسب الرقم المناسب (Prefix + (Start + pageIndex))، وترسمه في الزاوية السفلية‑اليمنى افتراضيًا. يمكنك تعديل الموضع لاحقًا، لكن الإعداد الافتراضي يناسب معظم المستندات القانونية.

> **سؤال شائع:** *ماذا لو احتجت ترقيم مجموعة فرعية فقط من الصفحات؟*  
> استخدم التحميل الزائد `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` لتحديد النطاق.

## الخطوة 4: حفظ PDF مع تطبيق أرقام Bates

الخطوة الأخيرة هي كتابة المستند المعدل إلى القرص.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*لماذا هذا مهم*: طريقة `Save` تحافظ على تنسيق الملف الأصلي، لذا ستحصل على PDF قياسي يمكن لأي عارض فتحه—مُرفق بـ **add document identification numbers** على كل صفحة.

## مثال كامل يعمل

نجمع كل ما سبق في برنامج مستقل يمكنك لصقه في تطبيق Console جديد وتشغيله فورًا.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**النتيجة المتوقعة:** افتح `output.pdf` بأي عارض؛ سترى “ABC‑1000”، “ABC‑1001”، … مطبوعة في الزاوية السفلية‑اليمنى لكل صفحة. الأرقام نص قابل للتحديد، لذا يمكن البحث عنها ونسخها—تمامًا ما تتوقعه من تنفيذ **add sequential PDF numbers** صحيح.

## الحالات الخاصة والبدائل

### تحديد موضع مخصص

إذا تصادمت الزاوية الافتراضية مع تذييلات موجودة، يمكنك تعديل الموضع:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### صيغ أرقام مختلفة

هل تريد أرقامًا مملوءة بالأصفار (مثال: 001000)؟ استخدم `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### معالجة ملفات متعددة دفعة واحدة

عند معالجة العديد من ملفات PDF، حافظ على عداد مستمر:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### التعامل مع ملفات PDF محمية بكلمة مرور

إذا كان ملف PDF المصدر مشفرًا، مرّر كلمة المرور عند إنشاء كائن `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## الأسئلة المتكررة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني استخدام مكتبة مختلفة؟** | نعم، مكتبات مثل iTextSharp أو PdfSharp تدعم أيضًا إدراج نص على مستوى الصفحة، لكن Aspose.PDF يوفر أبسط واجهة برمجية لترقيم Bates. |
| **هل يؤثر ذلك على حجم الملف؟** | إضافة بضع بايتات من النص لكل صفحة لا تكاد تُذكر؛ عادةً يزداد حجم الناتج بأقل من 1 KB لكل صفحة. |
| **هل الترميز قابل للبحث؟** | بالتأكيد. Aspose يكتب الأرقام ككائنات نصية، ليست كصور، لذا يتم فهرستها بواسطة قارئات PDF. |
| **ماذا لو أردت خطًا مختلفًا؟** | عيّن `batesOptions.Font` إلى كائن `Font` (مثال: `FontRepository.FindFont("Arial")`). |

## الخلاصة

لقد استعرضنا كيفية **create PDF document C#** وإضافة **add bates numbering pdf** فورًا باستخدام Aspose.PDF. العملية بسيطة، موثوقة، وقابلة للبرمجة بالكامل—مثالية للمكاتب القانونية، الجهات الحكومية، أو أي مؤسسة تحتاج إلى **add document identification numbers** و **add sequential PDF numbers** على دفعات كبيرة من الملفات.

استخدم هذه الأساسيات وجرب: جرّب بادئات مختلفة لأقسام مختلفة، ربط الترميزات عبر ملفات متعددة، أو دمج رموز QR بجانب أرقام Bates لزيادة التتبع. السماء هي الحد عندما تكون لديك سير عمل أساسي مضبوط.

إذا وجدت هذا الدليل مفيدًا، شاركه، اترك تعليقًا، أو استكشف أدلّتنا الأخرى حول معالجة PDF باستخدام C#. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}