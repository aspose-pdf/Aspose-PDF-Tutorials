---
category: general
date: 2026-07-20
description: إضافة مستطيل إلى PDF باستخدام Aspose.Pdf في C#. تعلم كيفية تحميل ملف
  PDF موجود، إنشاء مستطيل ملون، وحفظ PDF المعدل في بضع خطوات سهلة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle PDF
- load existing pdf
- save modified pdf
- how to add shape pdf
- create colored rectangle
language: ar
lastmod: 2026-07-20
og_description: أضف مستطيلًا إلى PDF بسرعة. يوضح هذا الدليل كيفية تحميل PDF موجود،
  وإنشاء شكل مستطيل ملون، وحفظ PDF المعدل باستخدام Aspose.Pdf.
og_image_alt: Screenshot showing a green rectangle added to a PDF page – add rectangle
  PDF example
og_title: إضافة مستطيل إلى PDF باستخدام Aspose.Pdf – دليل C# السريع
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Add rectangle PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, create colored rectangle, and save modified PDF in a few easy steps.
  headline: Add rectangle PDF with Aspose.Pdf – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: إضافة مستطيل إلى PDF باستخدام Aspose.Pdf – دليل C# الكامل
url: /ar/net/programming-with-operators/add-rectangle-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة مستطيل PDF – دليل C# كامل

هل تساءلت يومًا **how to add rectangle PDF** دون الحاجة للعبث بتدفقات PDF منخفضة المستوى؟ لست وحدك. يحتاج العديد من المطورين إلى **load existing PDF**، ورسم شكل، ثم **save modified PDF** — كل ذلك بطريقة نظيفة وقابلة للتكرار. في هذا الدرس سنستعرض ذلك تمامًا، باستخدام مكتبة Aspose.Pdf القوية لـ .NET.

سنغطي كل شيء بدءًا من جلب مستند فارغ من القرص، والتحقق من أن الشكل يناسب الصفحة، ورسم مستطيل أخضر، وأخيرًا حفظ التغييرات. في النهاية ستحصل على مثال جاهز للتنفيذ يمكنك إدراجه في أي مشروع C#. هيا نبدأ.

## Prerequisites

قبل أن نبدأ، تأكد من وجود ما يلي:

- **.NET 6.0** (أو أي نسخة حديثة من .NET) مثبتة.
- حزمة NuGet **Aspose.Pdf for .NET** (`Install-Package Aspose.Pdf`).
- ملف PDF للعمل معه – سنفترض أن `Blank.pdf` موجود في `YOUR_DIRECTORY`.
- فهم أساسي لصياغة C# (لا حاجة لأي شيء معقد).

> **Pro tip:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن *Aspose.Pdf* وقم بتثبيت أحدث إصدار ثابت.

## Step 1: Load an Existing PDF

الخطوة الأولى هي جلب ملف PDF إلى الذاكرة. تتولى فئة `Document` في Aspose.Pdf هذا في سطر واحد.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color

// Load the source PDF (replace the path with your actual location)
Document pdfDocument = new Document("YOUR_DIRECTORY/Blank.pdf");
```

**Why this matters:** تحميل الملف يمنحك الوصول إلى مجموعة الصفحات، والبيانات الوصفية، وخيارات العرض. إذا لم يكن الملف موجودًا، سيُطلق Aspose استثناء `FileNotFoundException`، لذا تحقق من المسار مرة أخرى.

## Step 2: Grab the Target Page

معظم سيناريوهات إضافة الأشكال تركز على صفحة واحدة – عادةً الأولى. يمكنك استرجاعها عبر الفهرس (Aspose يستخدم الفهرسة بدءًا من 1).

```csharp
// Access the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];
```

> **Note:** محاولة الوصول إلى رقم صفحة غير موجود ستؤدي إلى استثناء `ArgumentOutOfRangeException`. تأكد دائمًا من أن المستند يحتوي على عدد كافٍ من الصفحات قبل الفهرسة.

## Step 3: Define the Rectangle Geometry

المستطيل في مصطلحات PDF هو مجرد بنية `Rectangle` بأربع إحداثيات: `llx, lly, urx, ury` (الزاوية السفلية اليسرى، والزاوية العليا اليمنى). لننشئ مستطيلًا أكبر من صفحة A4 النموذجية لتوضيح فحص الحدود.

```csharp
// Rectangle larger than most pages (units are points; 72 points = 1 inch)
Rectangle shapeRect = new Rectangle(0, 0, 1200, 1200);
```

إذا أردت مستطيلًا يناسب الصفحة بشكل جيد، استخدم أبعادًا مثل `200, 200, 400, 400`. تُقاس الإحداثيات من الزاوية السفلية اليسرى للصفحة.

## Step 4: Validate the Shape Against Page Bounds

إضافة شكل يتجاوز حدود الصفحة قد يفسد التخطيط. توفر Aspose الدالة `IsShapeInsideBounds` لجعل هذا الأمر سهلًا.

```csharp
if (firstPage.IsShapeInsideBounds(shapeRect))
{
    // Shape fits – we can safely add it
}
else
{
    Console.WriteLine("Shape exceeds page boundaries – not added.");
}
```

**Why check?** بعض عارضات PDF تقص المحتوى الزائد بصمت، بينما قد يعرضه البعض الآخر بطريقة غريبة. التحقق يضمن أن يكون الناتج متوقعًا.

## Step 5: Add a Colored Rectangle to the Page

الجزء الممتع الآن: إنشاء **colored rectangle** وربطه بمجموعة الفقرات في الصفحة. سنستخدم تعبئة خضراء للوضوح.

```csharp
if (firstPage.IsShapeInsideBounds(shapeRect))
{
    // Create the rectangle fragment with a green fill
    RectangleFragment rectFragment = new RectangleFragment(shapeRect)
    {
        FillColor = Color.Green,      // Fill the shape with green
        Border = new BorderInfo(BorderSide.All, 1) // Optional thin border
    };

    // Add the rectangle to the page
    firstPage.Paragraphs.Add(rectFragment);
}
```

**Explanation:**  
- `RectangleFragment` هو كائن خفيف الوزن يمثل الشكل.  
- `FillColor` يحدد لون التعبئة الداخلي؛ يمكنك استخدام أي `System.Drawing.Color`.  
- إضافته إلى `Paragraphs` يضمن أن الشكل يحترم تدفق محتوى الصفحة.

### Edge Cases & Variations

- **ألوان مختلفة:** استبدل `Color.Green` بـ `Color.FromArgb(255, 0, 0)` للحصول على اللون الأحمر، أو أي قيمة ARGB أخرى.  
- **الشفافية:** استخدم `rectFragment.FillColor = Color.FromArgb(128, 0, 255, 0)` للحصول على شفافية 50 %.  
- **زوايا مستديرة:** لا تدعم Aspose المستطيلات المستديرة مباشرة، لكن يمكنك وضع `EllipseFragment` فوقها لمحاكاة التأثير.  
- **أشكال متعددة:** ببساطة كرّر كتلة الإنشاء مع إحداثيات جديدة وأضف كل fragment إلى `firstPage.Paragraphs`.

## Step 6: Save the Modified PDF

أخيرًا، اكتب التغييرات إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد – سنختار الأخير للحفاظ على المصدر دون تعديل.

```csharp
// Save the updated document
pdfDocument.Save("YOUR_DIRECTORY/ShapeValidated.pdf");
Console.WriteLine("PDF saved successfully with the green rectangle.");
```

**Why a separate file?** الحفاظ على الأصل يتيح لك تشغيل السكريبت عدة مرات دون تراكم التغييرات، وهو أمر مفيد أثناء الاختبار.

## Full Working Example

بتجميع كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing;   // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/Blank.pdf");

        // 2️⃣ Get the first page
        Page firstPage = pdfDocument.Pages[1];

        // 3️⃣ Define a rectangle (change dimensions as needed)
        Rectangle shapeRect = new Rectangle(0, 0, 1200, 1200);

        // 4️⃣ Verify bounds
        if (firstPage.IsShapeInsideBounds(shapeRect))
        {
            // 5️⃣ Create and add a green rectangle
            RectangleFragment rectFragment = new RectangleFragment(shapeRect)
            {
                FillColor = Color.Green,
                Border = new BorderInfo(BorderSide.All, 1)
            };
            firstPage.Paragraphs.Add(rectFragment);
        }
        else
        {
            Console.WriteLine("Shape exceeds page boundaries – not added.");
        }

        // 6️⃣ Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/ShapeValidated.pdf");
        Console.WriteLine("PDF saved successfully with the green rectangle.");
    }
}
```

**Expected output:** بعد التشغيل، افتح `ShapeValidated.pdf`. يجب أن ترى مستطيلًا أخضر صلبًا مثبتًا في الزاوية السفلية اليسرى، يغطي المنطقة المحددة بالإحداثيات. إذا كان المستطيل كبيرًا جدًا، ستظهر رسالة التحذير في وحدة التحكم بدلاً من ذلك.

## Common Questions & Troubleshooting

- **“لماذا يظهر المستطيل غير مركزي؟”**  
  إحداثيات PDF تبدأ من الزاوية السفلية اليسرى، وليس العلوية اليسرى. عدّل `llx` و `lly` لتحريك الشكل للأعلى أو اليمين.

- **“هل يمكنني إضافة المستطيل إلى طبقة محددة؟”**  
  نعم. استخدم `pdfDocument.Pages[1].Resources.Layers.Add` لإنشاء طبقة، ثم عيّن `rectFragment.Layer = yourLayer`.

- **“ملف PDF محمي بكلمة مرور—هل يمكنني إضافة شكل؟”**  
  حمّله باستخدام `new Document(path, password)` ثم تابع الخطوات نفسها. تذكر إعادة تطبيق إعدادات الأمان قبل الحفظ إذا لزم الأمر.

- **“ماذا لو أردت إضافة مستطيل إلى كل صفحة؟”**  
  قم بعمل حلقة عبر `pdfDocument.Pages` وكرر الخطوات 3‑5 لكل كائن `Page`.

## Conclusion

أصبحت الآن تمتلك فهماً قوياً **how to add rectangle PDF** باستخدام Aspose.Pdf في C#. من **loading an existing PDF**، **validating shape bounds**، **creating a colored rectangle**، إلى **saving the modified PDF**، كل خطوة موضحة مع شروحات وكود يمكنك نسخه مباشرة إلى مشروعك.

بعد ذلك، قد ترغب في استكشاف إضافة أشكال أخرى (`EllipseFragment`, `PolygonFragment`)، دمج الصور، أو حتى إنشاء ملفات PDF من الصفر. جميع هذه المواضيع ترتبط بالكلمات المفتاحية الثانوية **load existing pdf**, **save modified pdf**, **how to add shape pdf**, و **create colored rectangle**، لذا أنت الآن في موقع ممتاز لتوسيع مجموعة أدواتك في معالجة PDF.

هل جربت تعديلًا مختلفًا؟ شارك تجربتك في التعليقات، أو اطرح أي أسئلة ما زالت عالقة. Happy coding!

## What Should You Learn Next?

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند PDF باستخدام Aspose.PDF – إضافة صفحة، شكل وحفظ](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [إنشاء مستطيل مملوء Aspose Pdf Net](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج وصفحات](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}