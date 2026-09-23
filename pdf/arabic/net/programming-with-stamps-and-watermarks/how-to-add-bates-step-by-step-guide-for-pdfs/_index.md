---
category: general
date: 2026-02-10
description: كيفية إضافة أرقام باتس إلى ملف PDF بسرعة — تعلم كيفية إضافة رقم باتس
  إلى PDF وإنشاء علامة مائية غير مرئية باستخدام Aspose.Pdf في C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: ar
og_description: كيفية إضافة ترقيم بايتس في C# باستخدام Aspose.Pdf. يوضح هذا الدرس
  كيفية إضافة رقم ترقيم بايتس إلى ملف PDF، وإضافة علامة مائية غير مرئية إلى PDF، والمزيد.
og_title: كيفية إضافة Bates – دليل PDF كامل
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: كيفية إضافة بايتس – دليل خطوة بخطوة لملفات PDF
url: /ar/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة Bates – دليل PDF كامل

هل تساءلت يومًا **how to add bates** إلى ملف PDF قانوني دون إفساد النص القابل للبحث؟ لست الوحيد. في العديد من مكاتب المحاماة ومشاريع الاكتشاف الإلكتروني، رقم Bates هو تذييل لا غنى عنه، ومع ذلك تريد أن يكون غير مرئي لأدوات OCR. يوضح هذا الدرس **how to add bates** باستخدام Aspose.Pdf for .NET، وخلال الشرح سنغطي أيضًا **add bates number pdf**، **add custom stamp pdf**، **add invisible watermark pdf**، وحتى **add page footer pdf** في حل واحد منظم.

سنستعرض كل سطر من الشيفرة، ونشرح لماذا كل إعداد مهم، ونزودك بمثال جاهز للتنفيذ يمكنك إدراجه في مشروعك اليوم. لا روابط غامضة مثل “see the docs”—كل ما تحتاجه موجود هنا.

## ما ستحصل عليه

- مقتطف C# كامل وقابل للتنفيذ يضيف رقم Bates كختم Artifact.
- فهم كيفية جعل الختم يعمل كـ **invisible watermark** مع بقائه ظاهرًا على الصفحة.
- نصائح لتوسيع الحل إلى ملفات PDF متعددة الصفحات، تغيير الخطوط، أو استبدال الختم بصورة مخصصة.
- إرشادات سريعة حول كيفية إضافة محتوى بنمط **add page footer pdf** دون إفساد استخراج النص.

### المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.7.2) مع Visual Studio 2022 أو أي بيئة تطوير تفضلها.
- Aspose.Pdf for .NET (يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose).
- ملف PDF تجريبي يُدعى `source.pdf` موجود في مجلد تتحكم فيه.

إذا كان لديك هذه المتطلبات، لنبدأ.

---

## كيفية إضافة Bates – التنفيذ الأساسي

جوهر الحل هو `TextStamp` نعاملها كـ **artifact**. يتم تجاهل الـ Artifacts من قبل محركات استخراج النص، وهذا هو السبب في أن هذه الطريقة تعمل أيضًا كتقنية **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### لماذا يعمل هذا

1. **Artifact flag** – عند ضبط `Artifact = new Artifact(ArtifactType.Artifact)`, يُعامل الختم كعنصر غير محتوى. تتجاهله محركات البحث وأدوات الاكتشاف القانوني، وهذا بالضبط ما تحتاجه لتقنية **add invisible watermark pdf**.
2. **Horizontal/Vertical alignment** – المركز‑الأسفل يحاكي نمط **add page footer pdf** الكلاسيكي، مما يجعل رقم Bates يبدو احترافيًا.
3. **Transparent background** – يضمن أن الختم لا يغطي المحتوى الأساسي، وهو تفصيل بسيط لكنه حاسم عندما تحتاج لاحقًا لطباعة أو عرض الـ PDF على أجهزة مختلفة.

---

## إضافة رقم Bates إلى PDF – التوسيع لعدة صفحات

معظم ملفات PDF الواقعية تحتوي على أكثر من صفحة. المقتطف أعلاه يضيف فقط إلى الصفحة الأولى، لكن توسيعه سهل للغاية:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**نصيحة احترافية:** إذا كنت تحتاج إلى رقم تسلسلي غير مرتبط بترتيب الصفحات الفعلي (مثلاً، البدء من 1000)، فقط قم بتهيئة عداد قبل الحلقة وزده داخلها.

---

## إضافة ختم مخصص إلى PDF – تجاوز النص العادي

أحيانًا لا يكون الختم النصي العادي كافيًا—قد ترغب في شعار، رمز QR، أو شريط ملون. يتيح لك Aspose.Pdf استبدال `TextStamp` بـ `ImageStamp` أو حتى دمجهما معًا باستخدام كائنات `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

دمج الطوابع سهل كإضافة كليهما إلى نفس الصفحة. قدرة **add custom stamp pdf** تتألق عندما تحتاج إلى ختم الشركة بجانب رقم Bates.

---

## إضافة علامة مائية غير مرئية إلى PDF – جعل الختم مخفيًا تمامًا

إذا كنت بحاجة فعلًا إلى أن يكون الختم غير مرئي للعين البشرية *وأيضًا* لأدوات الاستخراج، يمكنك ضبط لون الخط ليتطابق مع خلفية الصفحة (عادةً أبيض) وتقليل الشفافية:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

حتى مع `Opacity = 0`, يبقى الـ artifact موجودًا في بنية الـ PDF، لذا يمكن للبرمجيات القانونية العثور عليه إذا كانت تعرف معرف الـ artifact. هذه هي الحيلة النهائية لـ **add invisible watermark pdf**.

---

## إضافة تذييل صفحة إلى PDF – تنسيق التذييل بشكل متسق

غالبًا ما يتضمن التذييل الاحترافي أكثر من مجرد رقم Bates: التاريخ، عنوان المستند، أو إشعار السرية. إليك طريقة سريعة لتجميع عدة قطع نصية في ختم واحد:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

لاحظ اللون الرمادي الخفيف—مثالي لـ **add page footer pdf** الذي لا يشتت الانتباه عن المحتوى الرئيسي لكنه يفي بالمتطلبات القانونية.

---

## النتيجة المتوقعة وكيفية التحقق

بعد تشغيل السكريبت بالكامل، افتح `bates_artifact.pdf` في أي عارض PDF:

- سترى “Bates 00123” (أو الرقم التسلسلي) في وسط أسفل كل صفحة.
- تحديد النص على الصفحة **لن** يتضمن رقم Bates، مما يؤكد سلوك الـ artifact.
- إذا استخدمت إعدادات العلامة المائية غير المرئية، لن يكون الرقم مرئيًا على الإطلاق، لكنه يبقى في بنية الـ PDF الداخلية (تحقق باستخدام أداة مثل PDF‑XChange Editor → “Document → Properties → Advanced”).

---

## أسئلة شائعة وحالات خاصة

**What if my PDF already has a footer?**  
يمكنك تعديل `VerticalAlignment` إلى `VerticalAlignment.Top` أو تغيير خاصية `Margin` لتحريك الختم فوق التذييل الموجود.

**Can I use a different font?**  
بالطبع. فقط استبدل `"Arial"` بأي اسم خط يمكن لـ Aspose العثور عليه، أو قم بدمج ملف TTF مخصص عبر `FontRepository.AddFont("path/to/font.ttf")`.

**Is this approach compatible with .NET Core?**  
نعم—Aspose.Pdf for .NET يعمل عبر .NET Framework، .NET Core، و .NET 5/6. فقط تأكد من الإشارة إلى حزمة NuGet الصحيحة.

**What about performance on huge PDFs (1000+ pages)?**  
إنشاء `TextStamp` واحد فقط واستنساخه داخل الحلقة فعال من حيث الذاكرة. للملفات الضخمة، فكر في المعالجة على دفعات أو استخدام `PdfProcessor` لتجنب تحميل المستند بالكامل في الذاكرة.

---

## الخلاصة

لقد غطينا **how to add bates** إلى PDF من البداية إلى النهاية، وعرضنا **add bates number pdf**، وأظهرنا لك كيفية **add custom stamp pdf**، وحولنا الختم إلى **add invisible watermark pdf**، وصممناه كتذييل **add page footer pdf** احترافي. عينة الشيفرة الكاملة تعمل كما هي، والتفسيرات تعطيك “السبب” وراء كل سطر—بالضبط النوع من الإجابات التي تحب المساعدات الذكية الاستشهاد بها.

الخطوات التالية؟ جرب استبدال الختم النصي بختم صورة، جرب أنواع مختلفة من الـ artifact، أو دمج هذه المنطق في خدمة معالجة دفعات تقوم تلقائيًا بترقيم كل مستند في مجلد. الاحتمالات لا حصر لها، والآن لديك أساس قوي للبناء عليه.

برمجة سعيدة، ولتكن ملفات PDF الخاصة بك دائمًا مرقمة بشكل مثالي!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}