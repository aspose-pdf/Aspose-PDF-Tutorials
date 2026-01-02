---
category: general
date: 2026-01-02
description: أضف أرقام الصفحات إلى ملف PDF بسرعة باستخدام Aspose.Pdf في C#. تعلم كيفية
  إضافة ترقيم باتس، نص التذييل، علامة مائية مخصصة، وتكرار الصفحات في ملف PDF في سكريبت
  واحد.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: ar
og_description: أضف أرقام الصفحات إلى ملف PDF فورًا باستخدام Aspose.Pdf. يغطي هذا
  الدليل أيضًا إضافة ترقيم بايتس، نص التذييل، علامة مائية مخصصة، وتكرار الصفحات في
  ملف PDF.
og_title: إضافة أرقام الصفحات إلى PDF باستخدام C# – دورة برمجة شاملة
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: إضافة أرقام الصفحات إلى PDF باستخدام C# – دليل كامل خطوة بخطوة
url: /ar/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة أرقام الصفحات إلى PDF باستخدام C# – دليل برمجة كامل

هل احتجت يوماً إلى **add page numbers pdf** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—المطورون يسألون باستمرار كيف يمكنهم وضع أرقام، تذييلات، أو حتى معرف بنمط Bates على كل صفحة من ملف PDF.  

في هذا الدرس ستشاهد مثالًا جاهزًا للتنفيذ بلغة C# يقوم **بتكرار صفحات PDF**، يضيف تذييلًا برقم الصفحة، و(إذا رغبت) يضيف علامة مائية مخصصة. سنوضح لك أيضًا كيفية تحويل العلامة إلى رقم Bates، وهو مجرد طريقة فاخرة لقول “إضافة ترقيم Bates” للوثائق القانونية أو الجنائية. في النهاية، ستحصل على طريقة واحدة قابلة لإعادة الاستخدام تتعامل مع كل هذه المهام دون عناء.

## نظرة عامة على إضافة أرقام الصفحات إلى PDF

قبل الغوص في الشيفرة، دعنا نوضح ما يعنيه فعليًا “add page numbers pdf” في عالم Aspose.Pdf. المكتبة تتعامل مع أي قطعة نصية تضعها على الصفحة كـ **TextStamp**. بإنشاء طابع واحد يحتوي على عنصر نائب للصفحة (`{page}`) وتطبيقه على كل صفحة، ستحصل تلقائيًا على ترقيم متسلسل. يمكن لنفس الطابع أن يحمل نصًا إضافيًا، لذا يمكنك **إضافة نص تذييل** مثل “Confidential” أو معرف خاص بالقضية.

> **لماذا نستخدم طابعًا بدلاً من تعديل تدفق محتوى PDF؟**  
> الطوابع هي كائنات عالية المستوى تحترم هوامش الصفحة، الدوران، والرسومات الموجودة. كما أنها أسهل بكثير في الصيانة—فقط غيّر بعض الخصائص وأعد تشغيل السكريبت.

## تكرار صفحات PDF لتطبيق الطوابع

الخطوة العملية الأولى هي فتح ملف PDF المصدر والتجول عبر صفحاته. هذا هو نمط **loop through pdf pages** الكلاسيكي الذي تستخدمه معظم أمثلة Aspose.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **نصيحة احترافية:** إذا كان ملف PDF كبيرًا (مئات الصفحات)، فكر في معالجته على دفعات لتقليل استهلاك الذاكرة. Aspose.Pdf يبث الصفحات بشكل كسول، لذا فإن الحلقة نفسها فعّالة بالفعل.

## إضافة ترقيم Bates ونص التذييل

الآن بعد أن يمكننا المرور على كل صفحة، لننشئ **TextStamp** قابلًا لإعادة الاستخدام يحمل كلًا من رقم الصفحة والنص الاختياري للتذييل. عنصر `{page}` يتم استبداله تلقائيًا برقم الصفحة الحالي.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### لماذا يعمل هذا

* **`Bates-{page}`** – Aspose يستبدل `{page}` برقم الصفحة الفعلي، فيمنحك رقم Bates كلاسيكي تلقائيًا.  
* **`Confidential`** – هذا هو جزء **add footer text**. يمكنك استبداله بأي سلسلة، حتى سحب البيانات من قاعدة بيانات.  
* **التنسيق** – باستخدام `TextState` يمكنك تعديل اللون، الشفافية، وحتى الدوران دون لمس تدفقات محتوى PDF الداخلية.

إذا كنت تحتاج فقط إلى أرقام عادية، احذف البادئة “Bates‑” والنص الإضافي:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## إضافة علامة مائية مخصصة (اختياري)

أحيانًا تريد أكثر من تذييل—تحتاج إلى شعار شبه شفاف أو طبقة “DRAFT” تغطي الصفحة بالكامل. هنا يأتي دور **add custom watermark**. يمكن إعادة استخدام نفس فئة `TextStamp`، فقط غيّر محاذاتها وشفافيتها.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **ملاحظة:** الترتيب مهم. إضافة العلامة المائية أولاً يضمن بقاء أرقام الصفحات قابلة للقراءة فوق النص شبه الشفاف.

## حفظ PDF والتحقق من النتائج

بعد وضع الطوابع، الخطوة الأخيرة هي كتابة التغييرات إلى القرص. استدعاء `Save` الذي وضعناه سابقًا يقوم بالعمل الشاق، لكن دعنا نضيف مقتطف تحقق سريع يفتح الملف الجديد ويطبع عدد الصفحات التي تمت معالجتها.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

عند تشغيل البرنامج بالكامل، يجب أن ترى ملف PDF حيث تنتهي كل صفحة بشيء مثل **“Bates‑3 – Confidential”** (أو مجرد “3” إذا استخدمت الطابع البسيط) وإذا فعلت العلامة المائية، ستظهر كلمة “DRAFT” الخفيفة في منتصف الصفحة.

### النتيجة المتوقعة

| الصفحة | التذييل (مثال) |
|------|------------------|
| 1    | Bates‑1 – Confidential |
| 2    | Bates‑2 – Confidential |
| …    | … |
| N    | Bates‑N – Confidential |

إذا فتحت الملف في عارض، ستجد الأرقام على بعد 20 نقطة من الهوامش اليسرى والسفلية، متطابقة مع معايير الوثائق القانونية المعتادة.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

احفظه باسم `AddPageNumbers.cs`، استعد حزمة Aspose.Pdf عبر NuGet (`Install-Package Aspose.Pdf`)، ثم شغّله. ستحصل على ملف **add page numbers pdf** يوضح أيضًا **add bates numbering**، **add footer text**، **add custom watermark**، ونمط **loop through pdf pages** الكلاسيكي—كل ذلك في سكريبت واحد منظم.

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## الخلاصة

غطينا كل ما تحتاجه لتطبيق **add page numbers pdf** باستخدام Aspose.Pdf في C#. من تكرار كل صفحة، إلى وضع أرقام Bates، إضافة نص تذييل مخصص، وحتى وضع علامة مائية شبه شفافة، الشيفرة مختصرة بما يكفي لتدمجها في أي مشروع موجود.  

بعد ذلك، قد ترغب في استكشاف سيناريوهات أكثر تقدمًا—مثل سحب نص التذييل من قاعدة بيانات، تطبيق خطوط مختلفة لكل قسم، أو إنشاء ملف PDF فهرس منفصل يسرد جميع أرقام Bates. كل هذه الإضافات تبنى على الأفكار الأساسية التي عرضناها هنا، لذا أنت في موقع ممتاز لتوسيع الحل مع نمو متطلباتك.  

جرّبه، عدّل التنسيق، وأخبرنا في التعليقات كيف كانت تجربتك. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}