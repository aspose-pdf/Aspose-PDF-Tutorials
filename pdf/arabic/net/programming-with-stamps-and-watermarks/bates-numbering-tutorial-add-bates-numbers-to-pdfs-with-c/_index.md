---
category: general
date: 2026-02-25
description: دليل ترقيم بايتس – تعلم كيفية إضافة أرقام الصفحات إلى ملف PDF وتطبيق
  ترقيم بايتس مخصص باستخدام Aspose.Pdf في C#. دليل خطوة بخطوة مع الكود الكامل.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: ar
og_description: يُظهر لك درس الترقيم باتس كيفية إضافة أرقام الصفحات إلى PDF والترقيم
  المخصص باتس في C#. كود كامل، شروحات، ونصائح.
og_title: دليل ترقيم بايتس – إضافة أرقام بايتس إلى ملفات PDF باستخدام C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'دليل ترقيم بايتس: إضافة أرقام بايتس إلى ملفات PDF باستخدام C#'
url: /ar/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل ترقيم Bates – إضافة أرقام Bates إلى ملفات PDF بلغة C#

هل تساءلت يومًا كيف تضيف أرقام صفحات إلى PDF مع تضمين رقم Bates بأسلوب قانوني؟ لست وحدك. في هذا **bates numbering tutorial** سنستعرض كل ما تحتاج معرفته لوضع ختم على كل صفحة من PDF ببادئة مخصصة، أصفار بادئة، وتحديد موضع دقيق — باستخدام Aspose.Pdf for .NET.

الخبر السار؟ الأمر بسيط إلى حد ما بمجرد أن تستوعب المفاهيم الأساسية. بنهاية هذا الدليل ستحصل على برنامج قابل للتنفيذ يأخذ *input.pdf* ويولد *bates_out.pdf* مع تسمية أنيقة بنمط “ABC‑01000” على كل صفحة. هيا نبدأ.

## ما ستحتاجه

- **Aspose.Pdf for .NET** (الإصدار 23.10 أو أحدث). المكتبة تجارية، لكن النسخة التجريبية المجانية تكفي للتعلم.
- .NET 6+ SDK (أي نسخة حديثة ستفي بالغرض).
- بيئة تطوير C# أساسية — Visual Studio أو VS Code أو Rider.
- ملف PDF إدخال للتجربة (أي مستند متعدد الصفحات سيوضح التأثير).

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Pdf، ويمكن تشغيل الكود على Windows أو Linux أو macOS دون تعديل.

## الخطوة 1: تحميل مستند PDF المصدر (bates numbering tutorial – initialization)

أولاً نقوم بإنشاء كائن `Document` يمثل ملف PDF الذي نريد تعديله. فكر فيه كتحميل لوحة فارغة يمكنك الرسم عليها.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Why this matters:** بدون تحميل الملف، لا شيء لتضيف إليه تعليقات. فحص الصحة يمنع فشل صامت لاحقًا عندما تحاول إضافة القطع إلى مجموعة صفحات غير موجودة.

## الخطوة 2: تعريف قطعة ترقيم Bates (how to add bates)

تخبر *BatesNumberingArtifact* Aspose أين وكيف ترسم المعرف. يمكنك التحكم في البادئة، رقم البداية، عدد الأصفار، حجم الخط، وإحداثيات X/Y الدقيقة.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Why this matters:** خاصية `LeadingZeros` تضمن أن كل تسمية لها نفس الطول، وهو أمر حاسم في المستندات القانونية حيث يهم المحاذاة. عدّل `X` و `Y` لنقل الختم إلى الزاوية العليا‑اليمنى، السفلى‑اليسرى، أو أي موضع يطلبه سير العمل.

## الخطوة 3: إرفاق القطعة إلى كل صفحة (add page numbers pdf)

الآن نقوم بالتكرار عبر كل صفحة وإرفاق نفس القطعة. هنا يتم تحقيق متطلب *add page numbers pdf* — كل صفحة تحصل على تسمية متسلسلة تلقائيًا.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Why this matters:** بإضافة القطعة إلى مجموعة `Artifacts` بدلاً من رسم النص يدويًا، نترك Aspose يدير منطق الترقيم، الأصفار البادئة، وعملية العرض. هذا يقلل الأخطاء ويجعل الكود مختصرًا.

## الخطوة 4: حفظ ملف PDF المعدل (add bates numbering)

أخيرًا، نحفظ التغييرات في ملف جديد. من الجيد كتابة النتائج إلى اسم ملف مختلف للحفاظ على الأصل دون تعديل.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Why this matters:** طريقة `Save` تكتب ملف PDF بالكامل، وتدمج القطع كجزء من تدفق محتوى الصفحة. يمكن فتح الملف الناتج في أي عارض PDF وسيظهر أرقام Bates بالضبط كما تم تحديدها.

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه والصقه في مشروع تطبيق Console، استبدل مسارات العناصر النائبة، واضغط **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### النتيجة المتوقعة

افتح *bates_out.pdf* في Adobe Reader أو Foxit أو أي عارض. يجب أن ترى تسمية مثل **ABC‑01000** على الصفحة الأولى، **ABC‑01001** على الثانية، وهكذا، موضوعة على بعد 50 نقطة من الحافة اليسرى و30 نقطة من الأسفل. الأرقام محاذاة إلى اليمين بسبب الأصفار البادئة، مما يمنح المستند مظهرًا نظيفًا واحترافيًا.

## التغييرات الشائعة وحالات الحافة

| السيناريو | كيفية التعديل |
|----------|---------------|
| **بادئة مختلفة** | غيّر `Prefix = "XYZ"` في تعريف القطعة. |
| **ابدأ برقم مخصص** | عيّن `Start = 5000` (أو أي عدد صحيح). |
| **ضع الرقم في الزاوية العليا‑اليمنى** | استخدم `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **غيّر حجم الخط للوثائق الكبيرة** | عدّل `FontSize = 12` (أو أي حجم). |
| **أضف مستطيل خلفية** | أنشئ `RectangleArtifact` وأضفه قبل `BatesNumberingArtifact`. |
| **تجاوز صفحات معينة** | داخل حلقة `foreach`، أضف `if (page.Number % 2 == 0) continue;` لتجاوز الصفحات الزوجية. |

**Pro tip:** اختبر دائمًا باستخدام PDF قصير أولاً. يكون التحقق من الموضع أسرع قبل تشغيل السكريبت على ملف حالة مكون من 200 صفحة.

## الأسئلة المتكررة

- **هل يعمل هذا مع ملفات PDF المشفرة؟**  
  يمكن لـ Aspose.Pdf فتح الملفات المحمية بكلمة مرور إذا قدمت كلمة المرور عبر `Document(string, string)`. ستظل قطعة Bates تُطبق بعد فك التشفير.

- **هل يمكنني إضافة أرقام Bates وأرقام صفحات عادية معًا؟**  
  نعم. أضف `PageNumberArtifact` بجانب `BatesNumberingArtifact`. كل قطعة تحتفظ بالعداد الخاص بها.

- **ماذا لو كان ملف PDF يحتوي على أحجام صفحات مختلفة؟**  
  قيم `Position` هي نقاط مطلقة. للمستندات ذات الأحجام المختلطة، احسب الموضع لكل صفحة داخل الحلقة باستخدام `page.PageInfo.Width` و `page.PageInfo.Height`.

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن أتقنت **bates numbering tutorial**، قد ترغب في استكشاف:

- **إضافة علامات مائية** – نهج القطعة المشابه باستخدام `TextArtifact`.
- **دمج ملفات PDF متعددة** – استخدم `Document.AppendDocument`.
- **استخراج النص لفهرسة البحث** – فئة `TextAbsorber`.
- **أتمتة المعالجة الدفعية** – تكرار عبر مجلد من ملفات PDF وتطبيق نفس القطعة.

جميع هذه المواضيع تبني على نفس المفاهيم التي تعلمتها للتو، لذا أنت في موقع جيد لتوسيع مجموعة أدوات أتمتة PDF الخاصة بك.

*برمجة سعيدة! إذا واجهت أي صعوبات أو كان لديك أفكار لتخصيص إضافي، لا تتردد في ترك تعليق أدناه. عالم معالجة PDF واسع، ولكن مع **bates numbering tutorial** قوي تحت حزامك، أنت بالفعل متقدم على المنحنى.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}