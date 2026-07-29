---
category: general
date: 2026-07-03
description: تعلم كيفية إضافة علامة مائية إلى PDF باستخدام Aspose.PDF وإضافة طبقة
  نصية مخصصة إلى PDF في بضع أسطر فقط من كود C#.
draft: false
keywords:
- how to add watermark pdf
- add text overlay pdf
- how to use aspose pdf
- add custom text pdf
language: ar
og_description: كيفية إضافة علامة مائية إلى ملف PDF باستخدام Aspose.PDF في C#. دليل
  خطوة بخطوة يوضح كيفية إضافة نص مخصص كطبقة فوق PDF.
og_title: كيفية إضافة علامة مائية إلى PDF – دليل Aspose السريع
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add watermark PDF using Aspose.PDF and add custom text
    PDF overlay in just a few lines of C# code.
  headline: How to Add Watermark PDF – Add Text Overlay PDF with Aspose
  type: TechArticle
- description: Learn how to add watermark PDF using Aspose.PDF and add custom text
    PDF overlay in just a few lines of C# code.
  name: How to Add Watermark PDF – Add Text Overlay PDF with Aspose
  steps:
  - name: 4‑a. Add to the First Page Only (quick demo)
    text: '```csharp // Add the stamp to the first page pdfDocument.Pages[1].AddStamp(textStamp);
      ```'
  - name: 4‑b. Add to Every Page (real‑world watermark)
    text: '```csharp // Uncomment the following block to watermark every page /* foreach
      (Page page in pdfDocument.Pages) { page.AddStamp(textStamp); } */ ```'
  - name: Expected Output
    text: Open `stamp.pdf` in any PDF viewer. You should see the semi‑transparent
      text **“Auto‑fit”** slanted at a 45° angle, centered within a 400 × 200‑point
      rectangle. The rest of the page content remains untouched.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: كيفية إضافة علامة مائية إلى ملف PDF – إضافة نص فوق PDF باستخدام Aspose
url: /ar/net/programming-with-stamps-and-watermarks/how-to-add-watermark-pdf-add-text-overlay-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة علامة مائية إلى PDF – إضافة نص تغطية إلى PDF باستخدام Aspose

هل تساءلت يومًا **كيفية إضافة علامة مائية إلى ملفات PDF** دون البحث عن محرر ضخم؟ لست وحدك. في العديد من المشاريع—مثل توليد التقارير تلقائيًا أو معالجة الفواتير على دفعات—يمكن أن تجعل العلامة المائية الدقيقة أو تغطية النص المخصصة الفرق بين منتج احترافي ومجموعة فوضوية من الصفحات.

الخبر السار؟ مع **Aspose.PDF for .NET** يمكنك إضافة علامة مائية إلى أي PDF ببضع أسطر فقط. في هذا الدرس سنستعرض الشيفرة الدقيقة التي تحتاجها، نشرح لماذا كل إعداد مهم، ونظهر لك أيضًا كيفية **add text overlay PDF** و **add custom text PDF** لتطبيق لمسات العلامة التجارية الدقيقة.

---

## ما ستبنيه

بنهاية هذا الدليل ستحصل على تطبيق كونسول صغير يقوم بـ:

1. تحميل ملف PDF موجود (`input.pdf`).
2. إنشاء طابع نصي يتكيف تلقائيًا مع نص العلامة المائية.
3. وضع الطابع على الصفحة الأولى (أو على كل الصفحات إذا رغبت).
4. حفظ النتيجة كـ `stamp.pdf`.

بدون أدوات خارجية، بدون نقرات يدوية في واجهة المستخدم—فقط شفرة C# صافية يمكنك إدراجها في أي مشروع .NET 6+.

---

## المتطلبات المسبقة

- **Aspose.PDF for .NET** (حزمة NuGet `Aspose.Pdf`). النسخة التجريبية المجانية تكفي للاختبار.
- .NET 6 SDK أو أحدث مثبت.
- ملف PDF تجريبي (`input.pdf`) موجود في مجلد يمكنك الإشارة إليه.
- معرفة أساسية بـ C# و Visual Studio (أو أي بيئة تطوير تفضلها).

> **نصيحة محترف:** إذا كنت تستهدف .NET Framework بدلاً من .NET Core، فإن الشيفرة نفسها تعمل؛ فقط عدل ملف المشروع وفقًا لذلك.

---

## الخطوة 1: إعداد المشروع وتثبيت Aspose.PDF

أولاً، أنشئ مشروع كونسول:

```bash
dotnet new console -n PdfWatermarkDemo
cd PdfWatermarkDemo
dotnet add package Aspose.Pdf
```

> **لماذا هذا مهم:** إضافة حزمة NuGet يجلب كل منطق تحليل PDF منخفض المستوى، لذا لا تحتاج إلى إعادة اختراع العجلة.

---

## الخطوة 2: تحميل وثيقة PDF المصدر

فتح ملف PDF سهل مثل استدعاء مُنشئ `Document`. ضعها داخل كتلة `using` حتى يتم تحرير مقبض الملف تلقائيًا.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the source PDF document
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // The rest of the steps go here...
        }
    }
}
```

> **ما الذي يحدث؟** فئة `Document` تحلل الملف وتبني تمثيلًا في الذاكرة للصفحات، الخطوط، والموارد. هذا هو الأساس لأي تعديل لاحق.

---

## الخطوة 3: إنشاء طابع نصي مع تمكين الضبط التلقائي

*الطابع* في Aspose هو كائن قابل لإعادة الاستخدام يمكن أن يحتوي على نص، صور، أو حتى صفحات PDF. للعلامة المائية نستخدم `TextStamp` مع `AutoAdjustFontSizeToFitStampRectangle = true`. هذا يضمن أن النص يتوسع ليتناسب مع المستطيل الذي تحدده.

```csharp
// Step 3: Create a text stamp (watermark) with auto‑fit enabled
var textStamp = new TextStamp("Auto‑fit")
{
    // Auto‑adjust the font size so the text always fits the rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Define the rectangle size (in points; 1 point = 1/72 inch)
    Width = 400,
    Height = 200,
    // Optional: rotate the watermark for a classic diagonal look
    Rotate = RotationAngle.FromDegrees(45),
    // Optional: set opacity (0 = fully transparent, 1 = opaque)
    Opacity = 0.3,
    // Optional: choose a font and color that matches your brand
    TextState = new TextState
    {
        FontSize = 72,               // initial size; will be auto‑adjusted
        Font = FontRepository.FindFont("Arial"),
        FontStyle = FontStyles.Bold,
        ForegroundColor = Color.FromRgb(200, 200, 200) // light gray
    }
};
```

> **لماذا الضبط التلقائي؟** إذا غيرت لاحقًا نص العلامة المائية (مثلاً من “Draft” إلى “Confidential”) سيستوعب المستطيل نفسه الطول الجديد دون الحاجة لتعديل يدوي. هذه هي ميزة **add custom text pdf**.

---

## الخطوة 4: وضع الطابع على الصفحة (الصفحات) المطلوبة

يمكنك إضافة الطابع إلى صفحة واحدة أو حلقة عبر جميع الصفحات. هنا نوضح كلا النهجين.

### 4‑a. إضافة إلى الصفحة الأولى فقط (عرض سريع)

```csharp
// Add the stamp to the first page
pdfDocument.Pages[1].AddStamp(textStamp);
```

### 4‑b. إضافة إلى كل الصفحات (علامة مائية واقعية)

```csharp
// Uncomment the following block to watermark every page
/*
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(textStamp);
}
*/
```

> **ملاحظة تصميمية:** الإضافة إلى كل الصفحات هي السيناريو النموذجي لـ **add text overlay pdf** للعلامة التجارية المؤسسية. الحلقة خفيفة—Aspose يتولى الجزء الثقيل تحت الغطاء.

---

## الخطوة 5: حفظ ملف PDF المعدل

أخيرًا، احفظ التغييرات. يمكنك استبدال الملف الأصلي أو كتابة ملف جديد.

```csharp
// Step 5: Save the modified PDF with the stamp applied
pdfDocument.Save("YOUR_DIRECTORY/stamp.pdf");
Console.WriteLine("Watermark applied successfully! Check YOUR_DIRECTORY/stamp.pdf");
```

تشغيل البرنامج الآن ينتج ملف `stamp.pdf` حيث تظهر كلمة “Auto‑fit” مائلة عبر الصفحة الأولى (أو جميع الصفحات إذا فعلت الحلقة).

---

## مثال كامل يعمل

نجمع كل شيء معًا، إليك الشيفرة الكاملة الجاهزة للتنفيذ:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Create a text stamp with auto‑fit enabled
            var textStamp = new TextStamp("Auto‑fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                Width = 400,
                Height = 200,
                Rotate = RotationAngle.FromDegrees(45),
                Opacity = 0.3,
                TextState = new TextState
                {
                    FontSize = 72,
                    Font = FontRepository.FindFont("Arial"),
                    FontStyle = FontStyles.Bold,
                    ForegroundColor = Color.FromRgb(200, 200, 200)
                }
            };

            // Add the watermark to the first page (or loop for all pages)
            pdfDocument.Pages[1].AddStamp(textStamp);
            // foreach (Page page in pdfDocument.Pages) { page.AddStamp(textStamp); }

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/stamp.pdf");
            Console.WriteLine("Watermark applied successfully!");
        }
    }
}
```

### النتيجة المتوقعة

افتح `stamp.pdf` في أي عارض PDF. يجب أن ترى النص شبه الشفاف **“Auto‑fit”** مائل بزاوية 45°، مركزيًا داخل مستطيل 400 × 200 نقطة. يبقى باقي محتوى الصفحة دون تغيير.

---

## إضافة نص مخصص أكثر – ما وراء العلامة المائية البسيطة

إذا كنت بحاجة إلى **add custom text PDF** يتجاوز العلامة المائية العامة، ما عليك سوى تغيير معامل منشئ `TextStamp`:

```csharp
var customStamp = new TextStamp("Confidential – For Internal Use Only")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    Width = 500,
    Height = 250,
    Rotate = RotationAngle.FromDegrees(30),
    Opacity = 0.2,
    TextState = new TextState
    {
        FontSize = 60,
        Font = FontRepository.FindFont("Times New Roman"),
        FontStyle = FontStyles.Italic,
        ForegroundColor = Color.FromRgb(255, 0, 0) // bright red for emphasis
    }
};
```

ثم أضف `customStamp` إلى الصفحات المطلوبة كما فعلت من قبل. هذه المرونة هي السبب في اختيار الكثير من المطورين لـ Aspose عند **how to use Aspose PDF** في خطوط الإنتاج.

---

## المشكلات الشائعة والنصائح

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **العلامة المائية تظهر خلف المحتوى الموجود** | بشكل افتراضي Aspose يضيف الطوابع **أعلى** محتوى الصفحة، لكن بعض ملفات PDF لديها طبقات تحجبها. | اضبط `StampAlignment` إلى `StampAlignment.Center` *وتأكد* من أن `Opacity` منخفض بما يكفي لتظهر من خلاله. |
| **النص مقطوع** | المستطيل (`Width`/`Height`) صغير جدًا بالنسبة لحجم الخط المختار. | فعّل `AutoAdjustFontSizeToFitStampRectangle` (مفعل بالفعل) أو زد أبعاد المستطيل. |
| **بطء الأداء على ملفات PDF الكبيرة** | حلقة عبر آلاف الصفحات تضيف عبئًا. | أنشئ كائن `TextStamp` واحد وأعد استخدامه؛ تجنّب إنشاء نسخة جديدة داخل الحلقة. |
| **الخط غير موجود** | الخط المحدد غير مثبت على الخادم. | استخدم `FontRepository.FindFont("Arial")` الذي يلجأ إلى خط مدمج، أو دمج ملف TTF مخصص باستخدام `FontRepository` |

## ماذا تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Add and Align Text Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}