---
category: general
date: 2026-03-24
description: كيفية إضافة ختم إلى ملف PDF باستخدام Aspose.Pdf في C#. تعلم كيفية وضع
  ختم PDF وإضافة ختم نصي PDF مع التحجيم التلقائي في بضع خطوات سهلة.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: ar
og_description: كيف تضيف ختمًا إلى ملف PDF باستخدام C#؟ يوضح لك هذا الدليل كيفية وضع
  ختم PDF وإضافة ختم نصي PDF مع ضبط حجم الخط تلقائيًا باستخدام Aspose.Pdf.
og_title: كيفية إضافة ختم إلى PDF باستخدام Aspose.Pdf – دليل سريع
tags:
- pdf
- csharp
- aspose
- stamping
title: كيفية إضافة ختم إلى PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة ختم إلى PDF باستخدام Aspose.Pdf – دليل خطوة‑بخطوة

**كيفية إضافة ختم** إلى ملف PDF هو احتياج شائع عندما تريد وضع علامة تجارية أو توثيق أو ببساطة إضافة ملاحظة إلى المستند. هل تساءلت يوماً عن أسهل طريقة لوضع ختم PDF دون التعامل مع الرسومات منخفضة المستوى؟ في هذا الدرس سنستعرض حلاً كاملاً جاهزاً للتنفيذ يُظهر **كيفية إضافة ختم** ويشرح *لماذا* كل سطر مهم.

ستتعلم كيفية **وضع ختم PDF** على أي صفحة، وكيفية **إضافة ختم نصي PDF** يتقلص تلقائيًا ليتناسب مع مستطيله، وما هي الأخطاء التي يجب تجنبها عندما يكون النص طويلًا جدًا. في النهاية ستحصل على ملف C# واحد يمكنك إدراجه في مشروعك والبدء في ختم ملفات PDF فورًا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا).
* حزمة NuGet الخاصة بـ Aspose.Pdf for .NET (`Aspose.Pdf`) مُثبتة.
* ملف PDF باسم `input.pdf` في مجلد يمكنك الإشارة إليه (أي ملف PDF بسيط من صفحة واحدة يكفي).

لا حاجة لأي إعدادات إضافية—Aspose.Pdf يتولى كل الأعمال الثقيلة.

## الخطوة 1: إعداد المشروع وتحميل ملف PDF المصدر

أول شيء نحتاجه هو كائن `Document` يمثل ملف PDF الذي نريد إضافة ملاحظة إليه. فكر به كقماش فارغ سنرسم عليه الختم لاحقًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **لماذا هذا مهم:** `Document` هو نقطة الدخول لأي تعديل على PDF في Aspose.Pdf. باستخدام نمط `using` نضمن تحرير مقبض الملف، مما يمنع مشاكل قفل الملف عندما تحاول حفظ PDF المعدل لاحقًا.

## الخطوة 2: إنشاء ختم نصي مع ضبط حجم الخط تلقائيًا

الآن نقوم بإنشاء `TextStamp`. الخاصية التي تجعل هذا المثال مميزًا هي العلم `AutoAdjustFontSizeToFitStampRectangle`—هذا يخبر Aspose بتقليص النص حتى يتناسب داخل المستطيل الذي نحدده.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى شعار أو صورة بدلاً من النص، استخدم `ImageStamp`—منطق الضبط التلقائي موجود أيضًا لتكبير/تصغير الصورة.

## الخطوة 3: اختيار مكان **وضع ختم PDF** – الصفحة الأولى، الصفحة الأخيرة، أو فهرس مخصص

Aspose.Pdf يخزن الصفحات في مجموعة تبدأ من 1 (`pdfDocument.Pages[1]` هي الصفحة الأولى). يمكنك **وضع ختم PDF** على أي صفحة بتغيير الفهرس.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **لماذا هذا مرن:** لأن مجموعة `Pages` قابلة للتعديل، يمكنك المرور على جميع الصفحات وإضافة نفس الختم إلى كلٍ منها، أو استهداف صفحة معينة بناءً على منطق العمل (مثلاً، صفحة الغلاف فقط).

## الخطوة 4: حفظ المستند المعدل

بعد إضافة الختم، تحتاج إلى كتابة التغييرات إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد—الأمر متروك لك.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

عند فتح `output-stamped.pdf` ستلاحظ مستطيل رمادي فاتح على الصفحة الأولى يحتوي على النص “Long text that must fit”. إذا كان النص أطول، سيقوم Aspose تلقائيًا بتقليصه حتى يتناسب تمامًا داخل المستطيل 300 × 100 pt.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console (`Program.cs`). يتضمن جميع الأجزاء التي ناقشناها، بالإضافة إلى أداة مساعدة صغيرة للتحقق من ظهور الختم.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

* يفتح PDF مع صندوق رمادي شبه شفاف على الصفحة الأولى.
* داخل الصندوق يتناسب النص المقدم تمامًا، حتى لو استبدلته بجملة أطول.
* لا تحتاج إلى حسابات يدوية لحجم الخط—Aspose يقوم بكل العمل الشاق.

## المشكلات الشائعة عند **وضع ختم PDF**

| العرض | السبب المحتمل | الحل |
|---------|--------------|-----|
| النص مقطوع | `AutoAdjustFontSizeToFitStampRectangle` **معطل** أو المستطيل صغير جدًا. | فعّل العلم وزد `Width`/`Height` أو قلل طول النص. |
| الختم غير مركّز | `HorizontalAlignment`/`VerticalAlignment` الافتراضيان `Left`/`Top`. | اضبط `HorizontalAlignment = HorizontalAlignment.Center` و `VerticalAlignment = VerticalAlignment.Center`. |
| الختم غير مرئي في بعض المشاهدات | شفافية الخلفية مضبوطة على 0 أو لون الختم يطابق خلفية الصفحة. | استخدم `Background.Color` متباين أو اضبط `Opacity` > 0.3. |
| تداخل عدة خُتم | إضافة خُتم داخل حلقة دون تعديل الإحداثيات. | استخدم `textStamp.XIndent` و `textStamp.YIndent` لإزاحة كل ختم. |

معالجة هذه القضايا مبكرًا توفر عليك الكثير من وقت التصحيح لاحقًا.

## توسيع المثال: إضافة ختم صورة

إذا كنت بحاجة إلى **إضافة ختم نصي PDF** *وأيضًا* صورة (مثل شعار الشركة)، يمكنك دمج الاثنين:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

الآن تظهر الصفحة كل من الختم النصي الديناميكي وختم الصورة الثابت جنبًا إلى جنب.

## اختبار التنفيذ الخاص بك

1. شغّل تطبيق الـ console.
2. افتح `output-stamped.pdf` في Adobe Reader أو Edge أو أي عارض PDF.
3. تأكد من وجود مستطيل الختم وأن النص مرئي بالكامل.
4. غيّر النص إلى عبارة أطول، أعد التشغيل، وتأكد من أن الخط يتقلص تلقائيًا.

إذا لاحظت أي شيء غير صحيح، راجع أبعاد المستطيل وإعداد `AutoAdjustFontSizePrecision`.

## الخلاصة

أنت الآن تعرف **كيفية إضافة ختم** إلى PDF باستخدام Aspose.Pdf، وكيفية **وضع ختم PDF** على صفحة محددة، وكيفية **إضافة ختم نصي PDF** يتadjust حجم الخط تلقائيًا. المثال الكامل القابل للتنفيذ أعلاه يزيل التخمين ويمنحك أساسًا قويًا لسيناريوهات الختم المتقدمة—مثل معالجة دفعات من الملفات أو إضافة علامات مائية شرطية.

هل أنت مستعد للخطوة التالية؟ جرّب ختم كل صفحة داخل حلقة، جرب خطوطًا مختلفة، أو اجمع بين الختم النصي والصوري لإنشاء ختم احترافي. السماء هي الحد، ومع Aspose.Pdf لديك محرك موثوق تحت الغطاء.

إذا واجهت أي صعوبات، اترك تعليقًا أو راجع وثائق Aspose.Pdf لمزيد من خيارات التخصيص. طباعة خُتم سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}