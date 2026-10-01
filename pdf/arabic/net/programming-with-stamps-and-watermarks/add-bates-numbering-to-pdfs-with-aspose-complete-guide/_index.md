---
category: general
date: 2026-04-25
description: أضف ترقيم باتس إلى ملفات PDF بسرعة باستخدام Aspose.Pdf. تعلّم كيفية إضافة
  أرقام الصفحات إلى PDF، وضبط حجم الخط تلقائيًا، وإضافة علامة مائية نصية في C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: ar
og_description: أضف ترقيم باتس إلى ملفات PDF باستخدام Aspose.Pdf. يوضح هذا الدليل
  كيفية إضافة أرقام الصفحات إلى PDF، وضبط حجم الخط تلقائيًا، وإضافة علامة مائية نصية
  في مثال واحد قابل للتنفيذ.
og_title: إضافة ترقيم بايتس إلى ملفات PDF – دليل Aspose.C# الكامل
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: إضافة ترقيم بيتس إلى ملفات PDF باستخدام Aspose – دليل كامل
url: /ar/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم Bates إلى ملفات PDF باستخدام Aspose – دليل كامل

هل احتجت يومًا إلى **إضافة ترقيم Bates** إلى ملف PDF لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—ففرق القانونية، المدققون، والمطورون يواجهون هذه المشكلة يوميًا. الخبر السار؟ باستخدام Aspose.Pdf for .NET يمكنك وضع طابع ترقيم Bates، وضبط حجم الخط تلقائيًا، وحتى التعامل مع الطابع كعلامة مائية نصية خفيفة—كل ذلك في بضع أسطر من C#.

في هذا الدرس سنستعرض الخطوات الدقيقة لـ **إضافة أرقام الصفحات إلى PDF**، ونضبط الخط بحيث لا يتجاوز الحد، ونجيب على سؤال “كيفية إضافة Bates” مرة واحدة وإلى الأبد. في النهاية ستحصل على تطبيق console جاهز للتشغيل ينتج ملف PDF مرقم بشكل احترافي، وسترى كيف يمكن توسيعه إلى حل علامة مائية كامل.

## Prerequisites

قبل أن نبدأ، تأكد من وجود ما يلي:

* **Aspose.Pdf for .NET** (أحدث حزمة NuGet حتى أبريل 2026).  
* .NET 6.0 SDK أو أحدث – تعمل الواجهة البرمجية بنفس الطريقة على .NET Framework، لكن .NET 6 يمنحك أفضل أداء.  
* ملف PDF تجريبي اسمه `input.pdf` موجود في مجلد يمكنك الإشارة إليه (مثال: `C:\Docs\`).  

لا يلزم أي تكوين إضافي؛ المكتبة مستقلة تمامًا.

---

## الخطوة 1 – تحميل مستند PDF المصدر

أول شيء نفعله هو فتح الملف الذي نريد ترقيمه. تمثل فئة `Document` الخاصة بـ Aspose كامل ملف PDF، وتحميله بسيط كتمرير المسار إلى المُنشئ.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*لماذا هذا مهم*: تحميل المستند يمنحك الوصول إلى مجموعة `Pages`، وهي المكان الذي سنرفق فيه طابع Bates لاحقًا. إذا لم يتم العثور على الملف، تقوم Aspose بإلقاء استثناء `FileNotFoundException` واضح، لذا ستعرف بالضبط ما الخطأ.

---

## الخطوة 2 – إنشاء طابع نصي لأرقام Bates

الآن نقوم بإنشاء العنصر البصري الذي سيظهر على كل صفحة. تسمح لك فئة `TextStamp` بإدراج أي سلسلة نصية، وسنستخدم العنصر النائب `{page}-{total}` لتسمح لـ Aspose باستبدال هذه الرموز تلقائيًا.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*نقاط رئيسية*:

* **auto adjust font size** – ضبط `AutoAdjustFontSizeToFitStampRectangle` إلى `true` يضمن أن النص لا يخرج أبداً من المستطيل، وهو مثالي لأرقام الصفحات ذات الطول المتغير.  
* **add text watermark** – بخفض قيمة `Opacity` نحول رقم Bates إلى علامة مائية خفيفة، مما يلبي متطلب “add text watermark” دون خطوة منفصلة.  
* **how to add bates** – الرموز `{page}` و `{total}` هي السر؛ تقوم Aspose باستبدالهما أثناء التشغيل، لذا لا تحتاج إلى حساب أي شيء بنفسك.

---

## الخطوة 3 – تطبيق الطابع على كل صفحة

خطأ شائع هو وضع الطابع فقط على الصفحة الأولى. لتحقيق **إضافة أرقام الصفحات إلى PDF** فعليًا، نحتاج إلى التكرار عبر مجموعة `Pages` بالكامل.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

لماذا النسخ؟ تقوم طريقة `AddStamp` داخليًا بإنشاء نسخة، لكن استخدام نسخة جديدة صراحةً في كل تكرار يتجنب الآثار الجانبية غير المقصودة إذا قمت بتعديل خصائص الطابع لاحقًا (مثل تغيير اللون لصفحات معينة).

---

## الخطوة 4 – حفظ ملف PDF المحدث

مع وجود الطوابع، حفظ التغييرات سهل. يمكنك استبدال الملف الأصلي أو الكتابة إلى موقع جديد—هنا سنحفظ ملفًا جديدًا باسم `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

إذا فتحت `output.pdf` ستلاحظ أن كل صفحة تحمل التسمية “Bates: 1‑10”، “Bates: 2‑10”، … في أسفل اليمين، مع شفافية خفيفة تعمل كـ **add text watermark**.

---

## مثال كامل يعمل

بجمع كل ذلك، إليك برنامج console واحد متكامل يمكنك نسخه ولصقه في Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**النتيجة المتوقعة**: افتح `output.pdf` في أي عارض؛ كل صفحة تظهر سطرًا مثل “Bates: 3‑12” في الزاوية السفلية اليمنى، بحجم مناسب للمستطيل ومُظهر بشفافية 40 ٪. هذا يلبي كلًا من متطلبات التتبع القانوني واحتياج العلامة المائية البصرية.

---

## الاختلافات الشائعة والحالات الحدية

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|-----|
| **موضع مختلف** | ضبط `HorizontalAlignment` / `VerticalAlignment` أو تعيين `XIndent`/`YIndent` | بعض الشركات تفضل الموضع أعلى اليسار أو في الوسط. |
| **بادئة مخصصة** | استبدال `"Bates: "` بـ `"Doc‑ID: "` أو أي سلسلة | قد تستخدم نظام تسمية مختلف. |
| **طوابع متعددة** | إنشاء `TextStamp` ثاني (مثلاً لإشعار السرية) وإضافته بعد الأول | دمج **add bates numbering** مع متطلبات **add text watermark** الأخرى سهل. |
| **عدد صفحات كبير** | زيادة حجم الخط الأولي (مثلاً `14`) – سيقوم الضبط التلقائي بتصغيره عند الحاجة | عند وجود أكثر من 999 صفحة يصبح النص أطول؛ الضبط التلقائي يمنع القطع. |
| **ملفات PDF مشفرة** | استدعاء `pdfDocument.Decrypt("password")` قبل وضع الطابع | لا يمكنك تعديل ملف مؤمن بدون كلمة المرور. |

---

## نصائح احترافية ومخاطر

* **نصيحة احترافية:** اضبط `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` إذا لاحظت أن النص يلتصق بحافة الصفحة.  
* **احذر من:** المستطيلات الصغيرة جدًا (الحجم الافتراضي 100 × 30 pt). إذا كنت بحاجة إلى مساحة أكبر، اضبط `batesStamp.Width` و `batesStamp.Height` يدويًا.  
* **ملاحظة أداء:** وضع الطوابع على آلاف الصفحات قد يستغرق بضع ثوانٍ، لكن Aspose يبث الصفحات بكفاءة—لا حاجة لتحميل المستند بالكامل في الذاكرة.  

---

## الخلاصة

لقد عرضنا للتو كيفية **add bates numbering** إلى ملف PDF باستخدام Aspose.Pdf، مع **add page numbers pdf** في الوقت نفسه، وتمكين **auto adjust font size**، وإنشاء **add text watermark** في تدفق موحد. المثال الكامل القابل للتنفيذ أعلاه يمنحك أساسًا قويًا يمكنك تكييفه مع أي سير عمل للوثائق القانونية أو نظام تقارير داخلي.

هل أنت مستعد للخطوة التالية؟ جرّب دمج هذا النهج مع API دمج PDF الخاص بـ Aspose لمعالجة عدة ملفات دفعة واحدة، أو استكشف فئة `TextFragment` للحصول على علامات مائية أغنى (ملونة، مائلة، أو متعددة الأسطر). الاحتمالات لا حصر لها، والكود الذي لديك الآن هو أساس موثوق.

إذا وجدت هذا الدليل مفيدًا، لا تتردد في ترك تعليق، أو وضع نجمة على المستودع، أو مشاركة تنويعاتك الخاصة. ترميز سعيد، ولتكن ملفات PDF دائمًا مرقمة بدقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}