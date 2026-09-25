---
category: general
date: 2026-03-24
description: إضافة ترقيم باتس لملف PDF باستخدام Aspose.Pdf في C#. تعلم كيفية إضافة
  صفحة جديدة إلى PDF، تطبيق ترقيم باتس، وتحديث ترقيم باتس بكفاءة.
draft: false
keywords:
- add bates numbering pdf
- add new page pdf
- apply bates number
- create pdf aspose
- update bates numbering
language: ar
og_description: أضف ترقيم باتس إلى ملف PDF بسرعة. يوضح هذا الدليل كيفية إضافة صفحة
  جديدة إلى PDF، وتطبيق رقم باتس، وتحديث ترقيم باتس باستخدام Aspose.Pdf.
og_title: إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose – دليل شامل
url: /ar/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم بايتس PDF باستخدام Aspose – دليل كامل

هل احتجت يومًا إلى **add bates numbering pdf** للملفات لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—ففرق القانونية، المدققون، وأي شخص يتعامل مع حزم مستندات ضخمة يواجه هذه المشكلة بانتظام. الخبر السار؟ باستخدام Aspose.Pdf لـ .NET يمكنك إنجاز ذلك ببضع أسطر فقط، وستتعلم أيضًا كيفية **add new page pdf**، **apply bates number**، و**update bates numbering** لاحقًا.

في هذا الدرس سنستعرض سيناريو واقعي: لديك ملف PDF مصدر، تريد إدراج ختم بايتس على صفحة جديدة، وربما تحتاج إلى إعادة ترقيم المستند بالكامل لاحقًا. بنهاية الدرس ستكون قادرًا على **create pdf aspose** حلول جاهزة للإنتاج، وستفهم لماذا كل خطوة مهمة.

## ما ستحققه

- تحميل ملف PDF موجود باستخدام Aspose.Pdf.
- **Add new page pdf** لاستضافة ختم بايتس.
- **Apply bates number** باستخدام `TextStamp`.
- (اختياري) **Update bates numbering** عبر جميع الصفحات.
- مثال كامل بلغة C# يمكنك إدراجه في أي مشروع .NET.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).
- حزمة NuGet الخاصة بـ Aspose.Pdf لـ .NET (`Install-Package Aspose.Pdf`).
- ملف PDF مصدر (`source.pdf`) موجود في مجلد معروف.

لا تحتاج إلى إعدادات معقدة—فقط المكتبة وملف PDF لتجربته.

![إضافة مثال ترقيم بايتس PDF](https://example.com/placeholder.png "مخطط يوضح إضافة ترقيم بايتس إلى صفحة PDF")

## الخطوة 1 – تحميل ملف PDF المصدر (الأساس)

قبل أن تتمكن من **add bates numbering pdf**، تحتاج إلى كائن مستند للعمل معه. فكر في `Document` كالقماش؛ بدونها لا شيء لتضع عليه الختم.

```csharp
using Aspose.Pdf;

// Load the existing PDF – replace the path with your actual file location
using var pdfDocument = new Document(@"C:\MyPdfs\source.pdf");

// Verify the document was loaded (optional but handy for debugging)
Console.WriteLine($"Document loaded: {pdfDocument.Pages.Count} pages found.");
```

*لماذا هذا مهم:* تحميل الملف يمنحك الوصول إلى مجموعة الصفحات، البيانات الوصفية، وإعدادات الأمان. إذا كان الملف تالفًا، سيُطلق Aspose استثناءً توضيحيًا، مما يحفظك من فشل صامت لاحقًا.

## الخطوة 2 – **Add new page pdf** لختم بايتس

لماذا نضع الختم على صفحة جديدة تمامًا؟ العديد من سير عمل القانونية تتطلب ظهور رقم بايتس على صفحة عنوان منفصلة، مع الحفاظ على المحتوى الأصلي دون تعديل. إضافة صفحة هي سطر واحد مع Aspose.

```csharp
// Create a fresh page at the end of the document
var newPage = pdfDocument.Pages.Add();

// Quick sanity check – print the new total page count
Console.WriteLine($"New page added. Total pages: {pdfDocument.Pages.Count}");
```

*نصيحة محترف:* إذا كنت تحتاج الختم على كل صفحة بدلاً من ذلك، يمكنك تخطي إضافة صفحة جديدة والتكرار عبر `pdfDocument.Pages`. هنا نضيف **add new page pdf** لتوضيح نمط “صفحة الغلاف” الأكثر شيوعًا.

## الخطوة 3 – **Apply bates number** باستخدام TextStamp

قلب العملية هو `TextStamp`. يتيح لك تحديد موضع النص بدقة، وضبط الهوامش، وتنسيق المظهر.

```csharp
// Create a TextStamp that holds the Bates number
var batesStamp = new TextStamp("Bates: 001")
{
    // Align the stamp to the bottom‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    
    // Margin values are in points (1 point = 1/72 inch)
    Margin = new Margin(0, 0, 20, 20) // left, bottom, right, top
};

// Attach the stamp to the newly created page
newPage.AddStamp(batesStamp);
```

*لماذا اخترنا هذه الإعدادات:* وضعية أسفل‑اليمين تعكس ما تتوقعه معظم المحاكم من ترقيم بايتس. الهوامش بمقدار 20 نقطة تحافظ على النص بعيدًا عن حافة الصفحة، متجنبةً قص الطباعة. يمكنك استبدال `"Bates: 001"` بمتغير إذا كنت تحتاج أرقامًا متسلسلة.

## الخطوة 4 – حفظ ملف PDF المحدث

الحفظ بسيط، لكن قد ترغب في الحفاظ على الملف الأصلي. لنكتب إلى موقع جديد.

```csharp
string outputPath = @"C:\MyPdfs\output_with_bates.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved with Bates stamp at: {outputPath}");
```

في هذه المرحلة تكون قد نجحت في **add bates numbering pdf** إلى مستند، كما قمت بـ **add new page pdf** لاستضافته. افتح الملف في أي عارض—سترى الختم مثبتًا في الزاوية السفلية اليمنى من الصفحة الأخيرة.

## الخطوة 5 – (اختياري) **Update bates numbering** عبر جميع الصفحات

ماذا لو قررت لاحقًا إدراج المزيد من الختمات على صفحات أخرى؟ يوفر Aspose طريقة مساعدة تقوم تلقائيًا بزيادة الرقم على كل صفحة، مما يوفر عليك تعديل السلاسل يدويًا.

```csharp
// This will renumber all pages using the same stamp format
pdfDocument.Pages.UpdateBatesNumbering();
pdfDocument.Save(@"C:\MyPdfs\output_renumbered.pdf");
Console.WriteLine("All pages have been renumbered.");
```

*متى تستخدم هذا:* مثالي للدفعات الكبيرة حيث تحتاج كل صفحة إلى معرف فريد. الطريقة تحافظ على خصائص `TextStamp` الأصلية، لذا يبقى المحاذاة والهوامش متسقة.

## مثال كامل يعمل – من البداية إلى النهاية

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console. يتضمن جميع الخطوات، معالجة الأخطاء، وتعليقات توضيحية.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path to the source PDF – adjust as needed
        const string sourcePath = @"C:\MyPdfs\source.pdf";
        const string resultPath = @"C:\MyPdfs\output_with_bates.pdf";

        try
        {
            // 1️⃣ Load the existing PDF
            using var pdfDocument = new Document(sourcePath);
            Console.WriteLine($"Loaded PDF with {pdfDocument.Pages.Count} pages.");

            // 2️⃣ Add a new blank page for the Bates stamp
            var newPage = pdfDocument.Pages.Add();
            Console.WriteLine($"Added new page. Total pages now: {pdfDocument.Pages.Count}");

            // 3️⃣ Create and configure the Bates TextStamp
            var batesStamp = new TextStamp("Bates: 001")
            {
                HorizontalAlignment = HorizontalAlignment.Right,
                VerticalAlignment   = VerticalAlignment.Bottom,
                Margin = new Margin(0, 0, 20, 20) // left, bottom, right, top
            };

            // 4️⃣ Place the stamp on the newly added page
            newPage.AddStamp(batesStamp);
            Console.WriteLine("Bates stamp applied to the new page.");

            // 5️⃣ Save the modified PDF
            pdfDocument.Save(resultPath);
            Console.WriteLine($"PDF saved successfully at {resultPath}");

            // Optional: Renumber all pages if you add more stamps later
            // pdfDocument.Pages.UpdateBatesNumbering();
            // pdfDocument.Save(@"C:\MyPdfs\output_renumbered.pdf");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**النتيجة المتوقعة:** فتح `output_with_bates.pdf` يظهر المحتوى الأصلي دون تغيير، صفحة أخيرة جديدة، والنص “Bates: 001” مثبتًا في الزاوية السفلية اليمنى. إذا ألغيت التعليق عن سطر `UpdateBatesNumbering`، ستحصل كل صفحة على رقم متسلسل خاص بها.

## أسئلة شائعة وحالات خاصة

- **هل يمكنني تغيير الخط أو اللون؟**  
  بالتأكيد. `TextStamp` يرث من `Stamp`، لذا يمكنك ضبط `Font`، `FontSize`، `Color`، إلخ. مثال: `batesStamp.Font = FontRepository.FindFont("Arial"); batesStamp.FontSize = 12; batesStamp.TextColor = Color.Red;`.

- **ماذا لو كان ملف PDF محميًا بكلمة مرور؟**  
  حمّله مع كلمة المرور: `new Document(sourcePath, new LoadOptions { Password = "mySecret" })`.

- **هل يجب إغلاق كائن `Document`؟**  
  استخدام جملة `using` (كما هو موضح) يغلقه تلقائيًا، محررًا مقبض الملف.

- **هل تُقاس الهوامش بالنقاط أم بالبكسل؟**  
  بالنقاط. النقطة الواحدة تساوي 1/72 من البوصة، وهي الوحدة القياسية في PDF.

- **هل يمكن وضع الختم على الصفحة الأولى بدلًا من صفحة جديدة؟**  
  نعم—استبدل `newPage` بـ `pdfDocument.Pages[1]` (الصفحات تبدأ من 1).

## الخلاصة

أصبح لديك الآن وصفة واضحة من البداية إلى النهاية لـ **add bates numbering pdf** باستخدام Aspose.Pdf، بما في ذلك كيفية **add new page pdf**، **apply bates number**، و**update bates numbering** عندما يتوسع المستند. الكود جاهز للإدراج في أي مشروع C#، والشروحات ستساعدك على تكييفه مع تخطيطات مخصصة، خطوط مختلفة، أو معالجة دفعات.

### ما الخطوة التالية؟

- تعمق أكثر في **create pdf aspose** بإضافة صور، جداول، أو توقيعات رقمية.  
- أتمتة معالجة الدفعات: تكرار عبر مجلد من ملفات PDF وختم كل منها.  
- استكشف ميزات التوافق مع PDF/A في Aspose إذا كنت تحتاج مستندات قابلة للأرشفة.

جرّبه، عدّل المحاذاة، جرب نصوص ختم مختلفة، ودع المكتبة تتولى الجزء الصعب. إذا واجهت أي صعوبات، منتديات مجتمع Aspose مكان رائع لطرح الأسئلة—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}