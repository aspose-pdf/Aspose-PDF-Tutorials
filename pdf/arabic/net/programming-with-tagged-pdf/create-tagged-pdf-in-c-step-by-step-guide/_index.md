---
category: general
date: 2026-03-06
description: إنشاء ملف PDF مع علامات باستخدام Aspose.Pdf في C#. تعلم كيفية إضافة صورة
  إلى PDF، وتحديد موضع الشكل، ووضع علامات على PDF لتحسين إمكانية الوصول.
draft: false
keywords:
- create tagged pdf
- add image to pdf
- set figure position
- how to tag pdf
- how to add image
language: ar
og_description: إنشاء ملف PDF مع علامات باستخدام Aspose.Pdf. يوضح هذا الدليل كيفية
  إضافة صورة إلى PDF، وتحديد موضع الشكل، ووضع علامات على PDF لتحسين إمكانية الوصول.
og_title: إنشاء PDF مع علامات في C# – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF Accessibility
title: إنشاء ملف PDF معلم في C# – دليل خطوة بخطوة
url: /ar/net/programming-with-tagged-pdf/create-tagged-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF مع علامات في C# – دليل كامل

هل احتجت يوماً إلى **إنشاء PDF مع علامات** في C# لكن لم تعرف من أين تبدأ؟ لست وحدك؛ فإمكانية الوصول أصبحت ضرورية في هذه الأيام، وPDF مع علامات هو العمود الفقري للوثيقة المتوافقة. في هذا الدليل سنستعرض مثالاً عملياً يضيف **صورة إلى PDF**، يحدد موضع الشكل، ويظهر **كيفية وضع علامات على PDF** باستخدام Aspose.Pdf. في النهاية ستحصل على PDF مع علامات جاهز لتوزيعه على أي شخص.

سنغطي كل شيء من تحميل ملف موجود إلى حفظ النتيجة النهائية، لذا لن تحتاج للبحث عن “كيفية إضافة صورة” في مكان آخر. لا إطالة—حل واضح وقابل للتنفيذ يعمل مع Aspose.Pdf 23.8 (الأحدث وقت كتابة هذا الدليل). افتح بيئة التطوير الخاصة بك، ولنبدأ.

---

## ما ستحتاجه

- **Aspose.Pdf for .NET** (حزمة NuGet `Aspose.Pdf`).  
- .NET 6+ (أو .NET Framework 4.7.2+).  
- ملف PDF إدخال يحتوي بالفعل على بنية منطقية (أي أنه مُعلَّم مسبقاً) – إذا لم يكن كذلك، يمكنك تفعيل العلامات عبر `pdfDocument.TaggedContent = true`.  
- ملف صورة (`image.png`) تريد تضمينه.  

هذا كل ما تحتاجه. لا مكتبات إضافية، ولا ملفات إعدادات غامضة.

---

## الخطوة 1: تحميل مستند PDF الموجود (إنشاء قاعدة PDF مع علامات)

أول ما نقوم به هو فتح PDF الذي نريد تحسينه. تحميل الملف يمنحنا الوصول إلى بنيته المنطقية، وهو أمر أساسي لتدفقات **إنشاء PDF مع علامات**.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.LogicalStructure;

// Load the source PDF – make sure the path points to a real file.
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Verify that the document has a tag tree; if not, enable it.
if (!pdfDocument.TaggedContent.IsTagged)
{
    pdfDocument.TaggedContent.IsTagged = true;
    Console.WriteLine("Tagging enabled on the document.");
}
```

*لماذا هذا مهم:* بدون شجرة علامات، لن ينقل PDF المعلومات الهيكلية إلى قارئات الشاشة. تمكين العلامات يضمن أن أي عناصر جديدة نضيفها (مثل الشكل) ترث التسلسل الهرمي الصحيح.

---

## الخطوة 2: الوصول إلى جذر البنية المنطقية (كيفية وضع علامات على PDF)

الآن نتعمق في البنية المنطقية للـ PDF. العنصر الجذري هو الحاوية لجميع العلامات—فكر فيه كخريطة محتويات المستند.

```csharp
// Grab the root of the logical structure.
var logicalRoot = pdfDocument.TaggedContent.RootElement;

// Optional: print existing children count for debugging.
Console.WriteLine($"Root has {logicalRoot.ChildElements.Count} child elements.");
```

*شرح:* `logicalRoot` يتيح لنا إلحاق علامات جديدة مثل `<Figure>` أو `<Table>`. هذا هو جوهر **كيفية وضع علامات على PDF** برمجياً.

---

## الخطوة 3: إنشاء علامة Figure وتحديد موضعها (تحديد موضع الشكل)

علامة *Figure* تجمع المحتوى البصري مع تسمية اختيارية. سننشئ واحدة، نحدد موضعها، ونرفقها بالجذر.

```csharp
// Create a new Figure element.
var figureTag = logicalRoot.CreateFigureElement();

// Define where the figure appears on the page.
figureTag.Position = new Position
{
    // X/Y are measured from the bottom‑left corner (points).
    X = 100,   // 100 points from the left edge
    Y = 150,   // 150 points from the bottom edge
    Width = 300,
    Height = 200
};

// Append the Figure to the logical structure.
logicalRoot.AppendChild(figureTag);

Console.WriteLine("Figure tag created and positioned.");
```

*لماذا نحدد موضعاً:* خطوة **تحديد موضع الشكل** تحدد أين سيظهر العنصر البصري على الصفحة. إذا تخطيت ذلك، قد يظهر الشكل في موقع غير متوقع أو يكون غير مرئي لتقنيات المساعدة.

---

## الخطوة 4: إضافة تمثيل بصري – إدراج صورة (إضافة صورة إلى PDF)

مع وجود العلامة، نحتاج إلى صورة فعلية. هذه هي الخطوة التي تجيب على **إضافة صورة إلى PDF**.

```csharp
// Grab the first page (pages are 1‑based in Aspose.Pdf).
var firstPage = pdfDocument.Pages[1];

// Create an Image object that points to the file stream.
var image = new Image
{
    ImageStream = File.OpenRead("YOUR_DIRECTORY/image.png"),
    // The rectangle defines the same area we set for the Figure.
    Rect = new Rectangle(100, 150, 400, 350) // X, Y, Width, Height
};

// Add the image to the page's paragraph collection.
firstPage.Paragraphs.Add(image);

Console.WriteLine("Image added to the first page.");
```

*نقطة أساسية:* يجب أن تتطابق إحداثيات المستطيل مع `figureTag.Position` التي حددناها سابقاً؛ وإلا سيتعارض الشكل مع محتواه البصري، مما يفسد إمكانية الوصول.

---

## الخطوة 5: حفظ PDF المحدث (إنهاء إنشاء PDF مع علامات)

أخيراً، نقوم بحفظ التغييرات في ملف جديد. الحفاظ على الأصل دون تعديل يُعد ممارسة جيدة.

```csharp
// Save the modified document.
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

Console.WriteLine("Tagged PDF saved as output.pdf");
```

في هذه المرحلة لديك ملف **إنشاء PDF مع علامات** يحتوي على صورة موضوعة بشكل صحيح داخل علامة `<Figure>`. افتح `output.pdf` في Adobe Acrobat وتفقد لوحة *Tags* – يجب أن ترى عقدة `Figure` تحت الجذر.

---

## مثال كامل وجاهز للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console. جميع الخطوات مرتبة بالترتيب الصحيح.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.LogicalStructure;

namespace TaggedPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF.
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (!pdfDocument.TaggedContent.IsTagged)
            {
                pdfDocument.TaggedContent.IsTagged = true;
                Console.WriteLine("Tagging enabled.");
            }

            // 2️⃣ Access the logical structure root.
            var logicalRoot = pdfDocument.TaggedContent.RootElement;

            // 3️⃣ Create a Figure tag and set its position.
            var figureTag = logicalRoot.CreateFigureElement();
            figureTag.Position = new Position
            {
                X = 100,
                Y = 150,
                Width = 300,
                Height = 200
            };
            logicalRoot.AppendChild(figureTag);
            Console.WriteLine("Figure tag added.");

            // 4️⃣ Add the image to the first page.
            var firstPage = pdfDocument.Pages[1];
            var image = new Image
            {
                ImageStream = File.OpenRead("YOUR_DIRECTORY/image.png"),
                Rect = new Rectangle(100, 150, 400, 350)
            };
            firstPage.Paragraphs.Add(image);
            Console.WriteLine("Image inserted.");

            // 5️⃣ Save the result.
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("PDF saved – tagging complete.");
        }
    }
}
```

### النتيجة المتوقعة

- يفتح `output.pdf` مع عرض الصورة عند النقاط (100, 150) وبحجم 300 × 200 نقطة.  
- تُظهر لوحة *Tags* عنصر `Figure` يحيط بالصورة.  
- أدوات قارئ الشاشة تُعلن “Figure” قبل وصف الصورة، مما يفي بمعايير إمكانية الوصول الأساسية.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو لم يكن PDF المصدر مُعلَّمًا مسبقًا؟

يتيح لك Aspose.Pdf تفعيل العلامات عبر ضبط `pdfDocument.TaggedContent.IsTagged = true;`. ستُنشئ المكتبة شجرة علامات افتراضية، وبعد ذلك يمكنك إضافة علامات مخصصة كما هو موضح.

### هل يمكنني إضافة تسمية توضيحية إلى الشكل؟

نعم. بعد إنشاء `figureTag`، يمكنك إرفاق `Paragraph` يحتوي على `TextFragment` وتعيين `Tag` الخاص به إلى `Caption`. مثال:

```csharp
var caption = new Paragraph(new TextFragment("Figure 1: Sample diagram"));
caption.Tag = figureTag.CreateCaptionElement();
logicalRoot.AppendChild(caption);
```

### كيف أضع الشكل في صفحة مختلفة؟

استبدل `var firstPage = pdfDocument.Pages[1];` بالفهرس المطلوب للصفحة، مثل `pdfDocument.Pages[3]`. تذكر تعديل إحداثيات `Position` إذا كان حجم الصفحة مختلفًا.

### ماذا لو احتجت إلى وضع علامات على عدة صور؟

أنشئ `Figure` جديد لكل صورة، أعط كل منها `Position` فريدة، وأضف كائن `Image` المناسب إلى الصفحة المعنية. يمكن تنفيذ ذلك عبر حلقة تمر على مجموعة من الصور.

### هل يعمل هذا مع توافق PDF/A؟

يدعم Aspose.Pdf معايير PDF/A‑1b و PDF/A‑2b و PDF/A‑3b. عند إنشاء مستند PDF/A، تأكد من ضبط وضع التوافق قبل الحفظ:

```csharp
pdfDocument.Convert(ConvertFormat.PdfA1b);
```

منطق العلامات يبقى كما هو.

---

## نصائح احترافية ومخاطر محتملة

- **نصيحة احترافية:** استخدم دائمًا مسارات مطلقة أو `Path.Combine` لتجنب أخطاء “الملف غير موجود” أثناء التشغيل.  
- **احذر من:** إحداثيات غير متطابقة بين علامة `Figure` ومستطيل `Image`—تقنيات المساعدة تعتمد على هذا التوافق.  
- **ملاحظة أداء:** إذا كنت تعالج عدة صفحات، احزم تدفق الصورة داخل كتلة `using` لتحرير الموارد بسرعة.  
- **تحقق من الإصدار:** الـ API المعروض يعمل مع Aspose.Pdf 23.8+. الإصدارات القديمة قد تحمل أسماء فئات مختلفة (مثل `LogicalStructureElement` بدلاً من `FigureElement`).

---

## الخلاصة

لقد أنشأنا **PDF مع علامات** من البداية إلى النهاية، وعرضنا **إضافة صورة إلى PDF**، وأظهرنا **كيفية تحديد موضع الشكل** بينما أجبنا على **كيفية وضع علامات على PDF** و**كيفية إضافة صورة** في مثال موحد. الكود جاهز للتنفيذ، والشروحات تغطي “السبب” وراء كل خطوة، والآن لديك أساس قوي لبناء ملفات PDF قابلة للوصول في C#.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة جداول باستخدام علامات `<Table>`، أو دمج طبقة توافق PDF/A‑2b لأغراض الأرشفة. النمط نفسه—التحميل، الوصول إلى البنية المنطقية، إنشاء علامة، إرفاق محتوى بصري، الحفظ—ينطبق على معظم مهام إمكانية الوصول في PDF.

إذا واجهت أي صعوبة أو لديك حالة استخدام غير مغطاة هنا، اترك تعليقًا أدناه. نتمنى لك تجربة وضع علامات ممتعة، واستمتع بإنشاء PDFs يمكن للجميع قراءتها!

![مخطط يوضح PDF مع علامة Figure وصورة – يوضح كيفية إنشاء PDF مع علامات](placeholder-image.png "مثال إنشاء PDF مع علامات")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}