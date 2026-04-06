---
category: general
date: 2026-04-06
description: إنشاء PDF من JPG بسرعة وتعلم كيفية قص الصورة في PDF، إضافة صفحة PDF جديدة،
  وتحويل JPG إلى PDF مع القص باستخدام C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: ar
og_description: إنشاء PDF من JPG وقص الصورة في PDF باستخدام C#. تعلم كيفية إضافة صفحة
  PDF جديدة وتحويل JPG إلى PDF مع القص.
og_title: إنشاء PDF من JPG في C# – دليل خطوة بخطوة
tags:
- Aspose.Pdf
- C#
- PDF generation
title: إنشاء PDF من JPG في C# – دليل كامل مع القص وإضافة صفحات جديدة
url: /ar/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF من JPG في C# – دليل كامل مع القص وإضافة صفحات جديدة

هل احتجت يوماً إلى **إنشاء PDF من JPG** لكن لم تكن متأكدًا من كيفية الاحتفاظ بالجزء الذي تريده فقط؟ لست وحدك. في العديد من التطبيقات—مثل الفواتير، الإيصالات، أو كتب الصور—يجب على المطورين تحويل صورة إلى PDF مع التخلص من الحواف غير المرغوب فيها.  

في هذا الدرس سنستعرض حلاً كاملاً جاهزًا للتنفيذ **ينشئ PDF من JPG**، يوضح لك كيفية **قص الصورة داخل PDF**، ويظهر **كيفية إضافة صفحة PDF جديدة** عندما تحتاج إلى أكثر من صورة واحدة. في النهاية ستعرف أيضًا كيفية **تحويل JPG إلى PDF مع القص** و**إدراج صورة في PDF C#** باستخدام مكتبة Aspose.Pdf.

## ما ستتعلمه

- إعداد Aspose.Pdf في مشروع .NET (بدون إعدادات معقدة).  
- تحميل ملف JPEG، تحديد المنطقة التي تريد الاحتفاظ بها، وقصها أثناء إدراجها في صفحة PDF.  
- إضافة صفحات إضافية إلى نفس المستند، مما يتيح لك بناء ملفات PDF متعددة الصفحات من عدة صور.  
- حفظ الملف النهائي والتحقق من الناتج.  

**المتطلبات المسبقة:** .NET 6+ (أو .NET Framework 4.6+)، Visual Studio 2022 أو أي محرر تفضله، وإشارة NuGet إلى `Aspose.Pdf`. لا تحتاج إلى أي خدمات خارجية أخرى.

![Create PDF from JPG example](image.jpg){: .align-center alt="مثال على إنشاء PDF من JPG يُظهر صورة مقصوصة موضوعة على صفحة PDF"}

---

## الخطوة 1: تثبيت Aspose.Pdf وتحضير مشروعك

أولاً، أضف حزمة Aspose.Pdf. افتح الطرفية في مجلد الحل الخاص بك وشغّل الأمر:

```bash
dotnet add package Aspose.Pdf
```

هذا السطر الواحد يجلب كل ما تحتاجه: الفئات `Document`، `Rectangle`، و`Page` التي سنستخدمها لاحقًا. في تجربتي، طريقة NuGet هي الأنظف للبقاء محدثًا دون العبث بملفات DLL.

> **نصيحة احترافية:** إذا كنت تستهدف .NET Framework، استخدم حزمة `Aspose.Pdf.NET` بدلاً منها؛ واجهة البرمجة (API) هي نفسها.

---

## الخطوة 2: تحميل JPEG وتحديد حجم الصفحة

نحتاج إلى لوحة قماشية تتطابق مع الأبعاد التي نريدها لصفحة PDF النهائية. الشيفرة أدناه تنشئ `Document` جديد وتفتح الصورة المصدر كـ stream.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

لماذا نستخدم مستطيل؟ في Aspose.Pdf يمثل `Rectangle` كلًا من أبعاد الصفحة ومنطقة الصورة التي تريد عرضها. بفصل *الصفحة* عن *منطقة القص* تحصل على تحكم دقيق في ما سيظهر في PDF.

---

## الخطوة 3: اختيار منطقة القص (الربع العلوي الأيسر)

لنفترض أنك تحتاج فقط إلى الربع العلوي الأيسر من الصورة. نحسب تلك المنطقة نسبةً إلى حجم الصفحة:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

منشئ `Rectangle` يأخذ قيم **X/Y السفلية اليسرى** و**X/Y العليا اليمنى**. بإضافة نصف الارتفاع إلى `LLY` نرفع أسفل منطقة القص، مما يتخلص من النصف السفلي من الصورة. عدّل هذه الحسابات إذا كنت تحتاج جزءًا مختلفًا.

> **لماذا القص قبل الإضافة؟**  
> القص على جانب PDF يتجنب إنشاء bitmap مؤقت على القرص، مما يوفر كلًا من I/O والذاكرة. Aspose يتولى الحسابات لك، والنتيجة PDF نظيفة وصديقة للمتجهات.

---

## الخطوة 4: إضافة صفحة جديدة وإدراج الصورة المقصوصة

الآن نضع الصورة فعليًا على صفحة PDF. هنا يبرز مفتاح **كيفية إضافة صفحة PDF جديدة**.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` يأخذ ثلاثة معطيات:

1. **Stream** – الـ JPEG المصدر.  
2. **Page rectangle** – يحدد حجم الصفحة (متغير `pageBounds`).  
3. **Crop rectangle** – يخبر Aspose أي جزء من الصورة يجب عرضه.

إذا احتجت صفحات إضافية، كرّر نمط `Add` + `AddImage` مع `imageStream` جديد في كل مرة. هذا يفي بمتطلب **كيفية إضافة صفحة PDF جديدة** مع الحفاظ على نظافة الشيفرة.

---

## الخطوة 5: حفظ PDF والتحقق من النتيجة

الخطوة الأخيرة سطر واحد فقط، لكن لا تستهين بها—الحفظ إلى المسار الصحيح يضمن إمكانية فتح الملف بأي عارض PDF.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

عند فتح `cropped_image.pdf`، يجب أن ترى صفحة واحدة تحتوي فقط على الربع العلوي الأيسر من JPEG الأصلي، مركزة تمامًا داخل صفحة بحجم 600 × 800.

---

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق console. يترجم كما هو، بشرط أن تكون قد ثبتت Aspose.Pdf ووضعّت JPEG في الموقع المحدد.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### النتيجة المتوقعة

- **الملف:** `cropped_image.pdf` (≈ 30 KB).  
- **المحتوى:** صفحة واحدة، 600 × 800 نقطة، تُظهر الربع العلوي الأيسر من `photo.jpg`.  
- **السلوك:** لا تشويه؛ الصورة تحتفظ بدقتها الأصلية داخل حدود القص.

---

## الأسئلة المتكررة وحالات الحافة

### ماذا لو أردت الاحتفاظ بالصورة كاملة، وليس ربعًا فقط؟

ما عليك سوى ضبط `cropArea` لتساوي `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### هل يمكنني استخدام حجم صفحة مختلف (مثل A4)؟

بالطبع. استبدل قيم `pageBounds` بأبعاد صفحة A4 بالنقاط (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

يمكن أن يبقى مستطيل القص كما هو أو يُعاد حسابه ليتناسب مع نسبة الأبعاد الجديدة.

### كيف أضيف عدة صور، كل واحدة في صفحتها الخاصة؟

استخدم حلقة تمر على مجموعة من مسارات الملفات:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### ماذا عن الشفافية أو صور PNG؟

Aspose.Pdf يتعامل مع PNG بنفس طريقة JPEG. إذا كان المصدر يحتوي على قناة ألفا، سيحافظ PDF عليها، بشرط أن نسخة PDF تدعم الشفافية (الإعداد الافتراضي يدعم ذلك).

### هل يعمل هذا على .NET Core على Linux؟

نعم. Aspose.Pdf متعدد المنصات؛ فقط تأكد من أن `imageStream` يشير إلى مسار ملف صالح على نظام التشغيل الهدف. لا تُستخدم أي واجهات Windows‑only.

---

## نصائح وممارسات أفضل

- **إدارة الذاكرة:** احرص دائمًا على وضع الـ streams داخل جمل `using` (كما هو موضح) لتجنب حجز الملفات.  
- **الأداء:** إذا كنت تعالج عشرات الصور، فكر في إعادة استخدام كائن `Document` واحد واستدعاء `pdfDocument.Pages.Add()` لكل صورة.  
- **معالجة الأخطاء:** غلف الروتين بالكامل بكتلة `try/catch` وسجّل `PdfException` لتسهيل استكشاف الأخطاء.  
- **ضبط الجودة:** يتيح لك Aspose.Pdf ضبط دقة الصورة عبر `ImageFragment`. للماسحات عالية الدقة، اضبط `ImageFragment.Resolution = 300;`.  
- **الأمان:** إذا كان PDF سيُشارك خارجيًا، يمكنك إضافة تشفير باستخدام `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

---

## الخلاصة

لقد غطينا الآن كيفية **إنشاء PDF من JPG** في C#، **قص الصورة داخل PDF**، و**إضافة صفحة PDF جديدة** لبناء مستندات متعددة الصفحات. النمط نفسه يتيح لك **تحويل JPG إلى PDF مع القص** و**إدراج صورة في PDF C#** لأي سيناريو—من الإيصالات البسيطة إلى كتب الصور المعقدة.  

جرّبه: غيّر منطق القص، جرب صفحات A4، أو ربط عدة صور معًا. مكتبة Aspose.Pdf تجعل هذه المهام سهلة، والشيفرة أعلاه تُعد مرجعًا قويًا يمكنك لصقه في أي مشروع.

---

### ما التالي؟

- **إضافة تعليقات نصية** إلى PDF (مثل عناوين تحت كل صورة).  
- **إنشاء جدول محتويات** تلقائيًا لملفات PDF متعددة الصفحات.  
- **دمج ملفات PDF متعددة** باستخدام `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

كل من هذه المواضيع يبني على الأساسيات التي تعلمتها الآن، لذا أنت في موقع جيد لاستكشافها.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}