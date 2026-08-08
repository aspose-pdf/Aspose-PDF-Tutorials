---
category: general
date: 2026-07-20
description: كيفية إضافة ترقيم باتس إلى ملف PDF باستخدام Aspose.Pdf. تعلم كيفية إضافة
  أرقام باتس إلى PDF وإضافة ختم إلى كل صفحة بسرعة وموثوقية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: ar
lastmod: 2026-07-20
og_description: كيفية إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose.Pdf. يوضح لك هذا
  الدليل كيفية إضافة أرقام بايتس إلى PDF وختم كل صفحة ببضع أسطر فقط من C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: كيفية إضافة ترقيم بايتس في ملفات PDF – دليل Aspose.Pdf الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: كيفية إضافة ترقيم بيتس في ملفات PDF باستخدام Aspose – دليل خطوة بخطوة
url: /ar/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة ترقيم Bates في PDF باستخدام Aspose – دليل خطوة بخطوة

هل تساءلت يومًا **كيف تضيف ترقيم bates** إلى مستند قانوني دون قضاء ساعات في واجهة المستخدم الرسومية؟ لست الوحيد. في العديد من مكاتب المحاماة، والوكالات الحكومية، وحتى الشركات الكبيرة، يُعد ختم كل صفحة بمعرف فريد مهمة يومية—ومع ذلك يمكن لسطر واحد من C# أن يجعل الأمر سهلًا للغاية.

في هذا الدرس سنستعرض مثالًا كاملًا قابلًا للتنفيذ يوضح لك بالضبط **كيف تضيف ترقيم bates** باستخدام مكتبة Aspose.Pdf. في النهاية ستعرف أيضًا كيفية **إضافة أرقام bates إلى ملفات pdf** و**إضافة ختم إلى كل صفحة** ببضع أسطر من الشيفرة فقط. لا سحر، فقط منطق واضح ونصائح عملية.

## ما ستتعلمه

- تحميل ملف PDF موجود باستخدام Aspose.Pdf.
- إنشاء كائن `BatesNumberingStamp` وتخصيص مظهره.
- التكرار عبر كل صفحة و**إضافة ختم إلى كل صفحة** تلقائيًا.
- حفظ النتيجة كملف PDF جديد يحمل رقم Bates احترافي على كل ورقة.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الشيفرة تعمل أيضًا على .NET Framework 4.7+).
- ترخيص صالح لـ Aspose.Pdf for .NET (أو مفتاح تقييم مؤقت).
- ملف PDF أصلي تريد ترقيمه (سنسميه `Original.pdf`).

إذا كنت تستوفي هذه العناصر الثلاثة، فأنت جاهز للبدء.

---

## Step 1: Set Up Your Project and Install Aspose.Pdf

أولاً، أنشئ مشروع console جديد (أو أضف الشيفرة إلى مشروع موجود). ثم احصل على حزمة NuGet:

```bash
dotnet add package Aspose.Pdf
```

> **نصيحة احترافية:** إذا كنت تعمل على شبكة مؤسسية، تأكد من أن مصدر NuGet الخاص بك مُعد للوصول إلى `https://www.nuget.org`.

## Step 2: Load the Source PDF Document

تحميل ملف PDF بسيط كما لو كنت تشير إلى Aspose بمسار الملف. فئة `Document` تمثل الملف بأكمله.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

لماذا نسجل عدد الصفحات؟ لأن ترقيم Bates يجب أن يكون تسلسليًا عبر *جميع* الصفحات، ومن الجيد التحقق من أنك لم تقم بتحميل ملف مختلف عن طريق الخطأ.

## Step 3: Create a Bates Numbering Stamp

قلب العملية هو `BatesNumberingStamp`. يتيح لك تحديد البادئة، الفاصل، عدد أصفار الأرقام، وحتى ما إذا كان يجب اعتبار الختم كـ *artifact* (أي غير مرئي لأدوات استخراج النص).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**لماذا هذه الإعدادات؟**  
- `StartingNumber = 1000` يحاكي سجل قانوني نموذجي يحتوي بالفعل على تراكم.  
- `NumberOfDigits = 5` يضمن أن أرقامًا مثل `01000`، `01001`، إلخ، تظهر بشكل منسق.  
- `Artifact = true` ضروري عندما يتم تمرير PDF إلى خطوط OCR أو e‑discovery؛ الأرقام تبقى مرئية للبشر لكن تُهمل من قبل محركات البحث النصية.

## Step 4: Add the Stamp to Every Page

الآن نقوم بالتكرار على `document.Pages` وتطبيق نفس الختم على كل صفحة. Aspose يزيد الرقم تلقائيًا لك.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **سؤال شائع:** *هل يمكنني التحكم في موضع الختم؟*  
> بالتأكيد. `BatesNumberingStamp` يرث من `Stamp`، لذا يمكنك ضبط خصائص مثل `HorizontalAlignment`، `VerticalAlignment`، `XIndent`، و`YIndent` قبل الحلقة. للتبسيط سنبقى على الزاوية السفلية‑اليمنى الافتراضية.

## Step 5: Save the Modified PDF

أخيرًا، احفظ التغييرات. يمكنك استبدال الملف الأصلي أو الكتابة إلى موقع جديد—هنا سنحتفظ بنسختين.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

عند فتح `BatesNumbered.pdf`، ستظهر كل صفحة بختم مشابه لـ:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

حيث `00123` هو إجمالي عدد الصفحات، والبادئة `ABC-` ثابتة.

---

## Full Working Example

انسخ الكتلة الكاملة أدناه إلى ملف `Program.cs` جديد وشغّله. عدّل مسارات الملفات لتتناسب مع بيئتك.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**المخرجات المتوقعة في وحدة التحكم:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

افتح الملف المحفوظ وسترى الأرقام المتسلسلة على كل صفحة—بالضبط ما تتوقعه عندما **تضيف أرقام bates إلى pdf**.

---

## Advanced Tweaks (Optional)

| الهدف | كيفية تحقيقه |
|------|-------------------|
| **تغيير لون الختم** | ضع `batesStamp.Color = Color.FromRgb(255, 0, 0);` قبل الحلقة. |
| **وضع الختم في الرأس** | عدّل خصائص `HorizontalAlignment` و`VerticalAlignment` كما هو موضح في الشيفرة المعلقة. |
| **تخطي صفحات معينة** | أضف شرط `if (page.Number % 2 == 0) continue;` داخل حلقة `foreach`. |
| **استخدام خط مخصص** | عيّن `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **جعل الختم مرئيًا لـ OCR** | ضع `Artifact = false`. |

## Frequently Asked Questions

**س: هل يعمل هذا مع ملفات PDF محمية بكلمة مرور؟**  
ج: نعم. حمّل المستند باستخدام كائن `PdfLoadOptions` الذي يزود كلمة المرور، ثم تابع كما هو موضح.

**س: ماذا لو احتجت إلى بادئات مختلفة لكل حالة؟**  
ج: أنشئ عدة كائنات `BatesNumberingStamp`، واضبط لكل منها `Prefix` الخاص، وطبقها فقط على نطاقات الصفحات المناسبة.

**س: هل المكتبة مجانية؟**  
ج: Aspose.Pdf يقدم تجربة مجانية لمدة 30 يومًا. للاستخدام الإنتاجي ستحتاج إلى ترخيص، لكن واجهة البرمجة (API) تبقى هي نفسها.

## Conclusion

لقد غطينا للتو **كيفية إضافة ترقيم bates** إلى أي PDF باستخدام Aspose.Pdf، وأظهرنا كيفية **إضافة أرقام bates إلى pdf** بطريقة نظيفة وقابلة للتكرار، وأوضحنا أبسط طريقة **لإضافة ختم إلى كل صفحة** باستخدام حلقة واحدة. الشيفرة مكتوبة بالكامل، تعمل في ثوانٍ، ويمكن دمجها في خطوط معالجة مستندات أكبر دون تعديل.

هل أنت مستعد للتحدي التالي؟ جرّب إنشاء صفحة غلاف تُظهر نطاق Bates، أو أدمج رمز QR بجانب كل ختم. الاحتمالات لا حصر لها، والنمط نفسه الذي تعلمته اليوم سيفيدك أينما احتجت إلى أتمتة بيانات PDF الوصفية.

إذا وجدت هذا الدليل مفيدًا، شاركه، اترك تعليقًا، أو استكشف دروسنا الأخرى حول دمج PDF، إضافة العلامات المائية، والتوقيعات الرقمية. ترميز سعيد!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إضافة طوابع صفحات في ملفات PDF باستخدام Aspose.PDF for .NET: دليل كامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [كيفية إضافة طوابع أرقام صفحات في ملفات PDF باستخدام Aspose.PDF for .NET | العلامات المائية والخلفيات](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [كيفية إضافة وتخصيص أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF for .NET | دليل معالجة المستندات](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}