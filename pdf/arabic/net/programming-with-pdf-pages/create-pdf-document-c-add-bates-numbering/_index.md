---
category: general
date: 2026-03-03
description: إنشاء مستند PDF بلغة C# مع ترقيم بايتس – تعلّم كيفية إضافة بايتس، إضافة
  أرقام صفحات متسلسلة، وتوليد بايتس في بضع خطوات فقط.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: ar
og_description: إنشاء مستند PDF باستخدام C# مع ترقيم بيتس. يوضح هذا الدليل كيفية إضافة
  بيتس، إضافة أرقام صفحات متسلسلة، وتوليد بيتس بسرعة.
og_title: إنشاء مستند PDF بلغة C# – إضافة ترقيم بيتس
tags:
- C#
- PDF
- Bates numbering
title: إنشاء مستند PDF باستخدام C# – إضافة ترقيم بيتس
url: /ar/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF C# – إضافة ترقيم Bates

هل احتجت يومًا إلى **create PDF document C#** ثم وضع علامة على كل صفحة بمعرف فريد لأغراض قانونية أو أرشيفية؟ لست وحدك—فالمكاتب القانونية والمحاكم وحتى الشركات الكبيرة تسأل باستمرار: “كيف يمكنني إضافة أرقام Bates إلى ملفات PDF تلقائيًا؟” الخبر السار هو أنه ببضع أسطر من الشيفرة يمكنك إنشاء PDF، وتوزيع أرقام Bates على كل صفحة، وحفظ النتيجة دون الحاجة لفتح أي محرر.

في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية يوضح **how to add Bates**، وكيفية **add sequential page numbers**، وحتى **generate Bates** باستخدام بادئات مخصصة. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- **.NET 6+** (الكود يعمل أيضًا على .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – مكتبة تجارية توفر API نظيفة لمعالجة PDF. نسخة التقييم المجانية تكفي للاختبار.
- فهم أساسي للغة C# (من المحتمل أنك مرتاح بالفعل مع عبارات `using` والكائنات).

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf`. إذا لم تقم بتثبيتها بعد، نفّذ:

```bash
dotnet add package Aspose.Pdf
```

> **نصيحة احترافية:** حافظ على تحديث نسخة Aspose الخاصة بك؛ الإصدار الأخير 23.x يضيف تحسينات أداء للوثائق الكبيرة.

## الخطوة 1: فتح (أو إنشاء) مستند PDF المصدر

أولاً نحتاج إلى ملف PDF للعمل معه. في العديد من السيناريوهات الواقعية لديك بالفعل ملف إدخال—مثل عقد ممسوح ضوئيًا. لأغراض المثال سنفتح ملفًا موجودًا يُدعى `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **لماذا هذا مهم:** فتح المستند داخل كتلة `using` يضمن تحرير مقبض الملف بسرعة، مما يتجنب مشاكل قفل الملف عندما تحاول لاحقًا استبدال نفس الملف.

## الخطوة 2: تعريف خيارات ترقيم Bates

أرقام Bates تتكون من **prefix** (غالبًا معرف القضية) و **starting number**. يمكنك أيضًا التحكم في عدد الأرقام، موضعها على الصفحة، ونمط الخط. هنا سنستخدم الكلمة الثانوية **add bates numbering pdf** عن طريق تكوين كائن `BatesNumberingOptions`.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **كيفية إضافة bates:** من خلال تعديل `Prefix` و `Start` تتحكم في السلسلة الدقيقة التي ستظهر على كل صفحة. خاصية `NumberOfDigits` تضمن عرضًا ثابتًا، وهو مفيد للملفات القانونية.

## الخطوة 3: تطبيق ترقيم Bates على كل صفحة

الآن يأتي الجزء الأساسي—إضافة الأرقام. طريقة `AddBatesNumbering` تتنقل عبر كل صفحة، ترسم النص، وتلتزم بالخيارات التي حددناها.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

في الخلفية، تقوم Aspose برسم النص كعنصر *content*، مما يعني أن الأرقام تصبح جزءًا من PDF ولا يمكن إخفاؤها في عارض. هذا بالضبط ما تحتاجه عندما تريد **add sequential page numbers** غير قابلة للتغيير.

### حالات حافة وتنوعات

- **Multiple prefixes:** إذا كنت تحتاج إلى بادئات مختلفة لكل قسم، أنشئ كائنات `BatesNumberingOptions` منفصلة واستدعِ `AddBatesNumbering` على نطاق صفحات (`pdfDocument.Pages[1..5]`).
- **Zero‑padding control:** احذف `NumberOfDigits` للحصول على رقم بطول متغير، أو اضبطه على قيمة أعلى للحصول على أصفار بادئة.
- **Custom positioning:** استخدم `Margin` لإزاحة الرقم عن الحافة، أو غيّر `HorizontalAlignment` إلى `Center` للحصول على نمط تذييل.

## الخطوة 4: حفظ ملف PDF المعدل

أخيرًا، اكتب المستند المحدث إلى القرص. يمكنك استبدال الأصلي أو إنشاء ملف جديد تمامًا.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

بعد تنفيذ هذا السطر، يحتوي `output.pdf` على المحتوى الأصلي بالإضافة إلى علامة Bates مرئية على كل صفحة—تمامًا ما تتوقعه عندما **how to generate bates** لملف قضية.

## مثال كامل قابل للتنفيذ

بجمع كل ذلك معًا، إليك المقتطف الكامل الذي يمكنك نسخه ولصقه في تطبيق كونسول:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### النتيجة المتوقعة

افتح `output.pdf` في أي عارض (Adobe Reader، Edge، إلخ). سترى كل صفحة مختومة بشيء مثل **CASE-001000**، **CASE-001001**، … حتى آخر صفحة. الأرقام تتوضع بإحكام في أسفل اليمين، مطابقةً للخيارات التي حددناها.

## أسئلة شائعة وحلول المشكلات

- **“ماذا لو كان ملف PDF محميًا بكلمة مرور؟”**  
  حمّله باستخدام كلمة المرور: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **“هل يمكنني إضافة أرقام Bates إلى PDF تم إنشاؤه حديثًا؟”**  
  بالتأكيد. فقط أنشئ المستند أولًا (`var doc = new Document();`) ثم اتبع الخطوات 2‑4 قبل الحفظ.

- **“هل الخط دائمًا مضمّن؟”**  
  تقوم Aspose تلقائيًا بضم الخط إذا لم يكن موجودًا بالفعل في PDF. إذا كنت تحتاج إلى عائلة خط محددة، اضبط `options.Font` وفقًا لذلك.

- **“ماذا عن الأداء على ملفات مكوّنة من 10,000 صفحة؟”**  
  المكتبة تبث الصفحات، لذا يبقى استهلاك الذاكرة معتدلًا. ومع ذلك، قد ترغب في زيادة `PdfSaveOptions.CompressionMode` للحصول على إدخال/إخراج أسرع.

## نصائح احترافية للاستخدام في الإنتاج

1. **معالجة دفعات:** غلف المنطق السابق داخل حلقة تت iterates على مجلد من ملفات PDF. استخدم `Directory.GetFiles("*.pdf")` وعالج كل ملف على حدة.
2. **التسجيل (Logging):** سجّل أول وآخر رقم Bates في ملف سجل—يساعد المدققين على التحقق من استمرارية الترقيم.
3. **معالجة الأخطاء:** احطِ الكتلة بالكامل بـ `try/catch` واظهر رسالة واضحة إذا كان ملف PDF المصدر مفقودًا أو معطوبًا.
4. **مرونة الصفر‑padding:** إذا كنت تحتاج إلى عدد أرقام ديناميكي بناءً على إجمالي الصفحات، احسب `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## الخلاصة

لقد أظهرنا للتو كيفية **create PDF document C#** وإضافة **Bates numbering** بسلاسة—مغطيين كل شيء من التحميل الأولي إلى الحفظ النهائي. المثال القصير يوضح **how to add bates**، **add sequential page numbers**، و **how to generate bates** باستخدام بادئات مخصصة وصفر‑padding. مع بعض التعديلات يمكنك تكييف هذا النمط للوظائف الدفعة، تخطيطات مختلفة، أو حتى دمجه في واجهة ويب API تُعيد PDF مرقّم حديثًا عند الطلب.

هل أنت مستعد للخطوة التالية؟ جرّب دمج هذا مع ميزة **watermark** من Aspose، أو أنشئ فهرسًا ملخصًا يسرد كل رقم Bates جنبًا إلى جنب مع وصف مختصر لمحتوى الصفحة. الاحتمالات لا حصر لها، والشيفرة التي لديك الآن تشكل أساسًا قويًا لأي سير عمل لأتمتة المستندات.

برمجة سعيدة، ولتكن ملفات PDF دائمًا مرقّمة بدقة! 

![لقطة شاشة لعارض PDF يظهر إنشاء مستند pdf c# مع تطبيق أرقام Bates](image-placeholder.png "إنشاء مستند pdf c# مع أرقام Bates")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}