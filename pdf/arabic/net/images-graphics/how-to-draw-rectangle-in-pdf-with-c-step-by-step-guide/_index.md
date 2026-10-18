---
category: general
date: 2026-03-27
description: تعلم كيفية رسم مستطيل في PDF باستخدام Aspose.Pdf للغة C#. أضف مستطيلًا
  إلى PDF، أضف شكلًا إلى PDF وارسم الشكل على PDF مع أمثلة شفرة واضحة.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: ar
og_description: اتقن كيفية رسم مستطيل في PDF باستخدام Aspose.Pdf. يوضح لك هذا الدليل
  كيفية إضافة مستطيل إلى PDF، إضافة شكل إلى PDF، ورسم الشكل على PDF خطوة بخطوة.
og_title: كيفية رسم مستطيل في PDF باستخدام C# – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: كيفية رسم مستطيل في PDF باستخدام C# – دليل خطوة بخطوة
url: /ar/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية رسم مستطيل في PDF باستخدام C# – دليل خطوة بخطوة

هل تساءلت يومًا **كيفية رسم مستطيل** في PDF دون الحاجة إلى التعامل مع صsyntax منخفض المستوى؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تصور صندوق حدود، أو منطقة تمييز، أو عنصر زخرفي بسيط داخل مستند مُولد. الخبر السار؟ مع Aspose.Pdf for .NET العملية سهلة للغاية.

في هذا الدرس سنستعرض كل ما تحتاجه **لإضافة مستطيل إلى PDF**، **لإضافة شكل إلى PDF**، وفي النهاية **لرسم مستطيل في PDF** باستخدام C# نظيف ومتقن. في النهاية ستحصل على برنامج قابل للتنفيذ ينتج ملف PDF يحتوي على مستطيل واضح—بدون الحاجة إلى أدوات خارجية.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)
- حزمة NuGet الخاصة بـ Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- بيئة تطوير C# أساسية (Visual Studio، VS Code، Rider، إلخ)

لا توجد مكتبات أخرى مطلوبة؛ كل شيء آخر يتم التعامل معه بواسطة Aspose.Pdf نفسه.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولاً، أنشئ تطبيقًا جديدًا من نوع console وقم باستيراد مساحة الأسماء Aspose.Pdf.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**لماذا هذا مهم:** استيراد `Aspose.Pdf.Drawing` يمنحك الوصول إلى فئة الشكل `Rectangle` التي سنستخدمها **لرسم شكل على PDF**. الحفاظ على نقطة الدخول مرتبة يجعل الخطوات اللاحقة أسهل في المتابعة.

## الخطوة 2: إنشاء مستند PDF جديد وإضافة صفحة

PDF بدون صفحات لا معنى له، لذا نبدأ بإنشاء كائن المستند وإضافة صفحة واحدة.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**شرح:** تمثل فئة `Document` الملف بأكمله، بينما تُعيد `Pages.Add()` كائن `Page` جديد حيث سنقوم لاحقًا **بإضافة مستطيل إلى PDF**. حجم A4 الافتراضي يناسب معظم الحالات، لكن يمكنك تمرير العرض/الارتفاع إذا احتجت إلى لوحة رسم مخصصة.

## الخطوة 3: تعريف شكل المستطيل

الآن يأتي جوهر **كيفية رسم مستطيل**—تحديد موقعه وأبعاده.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**لماذا نضبط هذه الخصائص:**  
- `BorderColor` و `BorderWidth` يتحكمان في الحد الخارجي، مما يجعل المستطيل مرئيًا.  
- `FillColor` يضيف خلفية خفيفة، مفيدة عندما تريد تمييز منطقة ما.  
- المُنشئ `(x, y, width, height)` يسمح لك **برسم مستطيل في PDF** بدقة في المكان الذي تحتاجه.

## الخطوة 4: إضافة المستطيل إلى الصفحة

مع جاهزية الشكل، الآن **نضيف الشكل إلى PDF** عن طريق ربطه بمجموعة `Annotations` الخاصة بالصفحة. تقوم Aspose.Pdf بالتحقق من الحدود تلقائيًا، لذا لا تحتاج للقلق بشأن التجاوز.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**ما يحدث خلف الكواليس:** مجموعة `Annotations` تتعامل مع المستطيل كرسمة متجهية. عند عرض الـ PDF، تقوم المكتبة بترجمة إحداثياتنا إلى تدفق محتوى الـ PDF.

## الخطوة 5: حفظ المستند

أخيرًا، اكتب ملف الـ PDF إلى القرص لتتمكن من فتحه بأي عارض.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**النتيجة:** عند فتح `RectangleDemo.pdf` ستظهر مستطيل رمادي فاتح مع حد أسود موضعه 100 نقطة من اليسار و500 نقطة من أسفل الصفحة. هذه هي الحل الكامل لـ **كيفية رسم مستطيل** في PDF باستخدام C#.

## مثال كامل يعمل

بجمع كل الأجزاء معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**المخرجات المتوقعة:** ملف باسم `RectangleDemo.pdf` يحتوي على صفحة واحدة بها مستطيل رمادي فاتح مركزي محاط بحد أسود. يمكنك فتحه باستخدام Adobe Reader أو Chrome أو أي عارض PDF آخر.

## الاختلافات الشائعة وحالات الحافة

### 1. رسم عدة مستطيلات

إذا احتجت إلى **إضافة مستطيل إلى PDF** أكثر من مرة، ما عليك سوى إنشاء كائنات `Rectangle` إضافية وإضافتها كلًّا إلى `page.Annotations`. يمكن تنفيذ ذلك عبر حلقة تمر على مجموعة من الإحداثيات بسهولة.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. استخدام وحدات قياس مختلفة

تعمل Aspose.Pdf بالنقاط (1 pt = 1/72 inch). إذا كنت تفضل المليمترات، قم بتحويلها أولًا:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. إضافة مستطيل كحقل نموذج

عندما تحتاج إلى مستطيل تفاعلي (مثل منطقة قابلة للنقر)، استخدم `LinkAnnotation` بدلاً من `Rectangle` العادي. الشيفرة مشابهة لكنها تضيف URL أو إجراء JavaScript.

### 4. مخاوف التوافق

إصدار Aspose.Pdf 23.9 (الصادر في أوائل 2026) يدعم بالكامل الـ APIs المعروضة أعلاه. قد تتطلب الإصدارات القديمة استخدام `page.AddAnnotation(rectangleShape)` بدلاً من `page.Annotations.Add`. تحقق دائمًا من ملاحظات الإصدار إذا واجهت أخطاء تجميع.

## نصائح احترافية ومخاطر

- **نصيحة احترافية:** اضبط `FillColor = Color.Transparent` إذا كنت تحتاج فقط إلى الحد. هذا يقلل من حجم الملف قليلًا.  
- **احذر من:** استخدام إحداثيات تتجاوز أبعاد الصفحة. تقوم Aspose.Pdf بقطع الشكل بصمت، مما قد يسبب ارتباكًا أثناء التصحيح.  
- **ملاحظة الأداء:** إضافة آلاف المستطيلات لا مشكلة، لكن إذا كنت تولد تقارير ضخمة ففكر في تجميع الأشكال في كائن `Graphics` واحد لتقليل الحمل.

## مرجع بصري

فيما يلي لقطة سريعة للـ PDF المُولد (المستطيل مبرز بالرمادي الفاتح). النص البديل يتضمن الكلمة المفتاحية الأساسية لتحسين SEO.

![كيفية رسم مستطيل في PDF مثال](https://example.com/images/rectangle-demo.png "كيفية رسم مستطيل في PDF مثال")

## الخلاصة

غطينا **كيفية رسم مستطيل** في PDF باستخدام Aspose.Pdf للغة C#. من خلال إنشاء `Document`، إضافة `Page`، تعريف شكل `Rectangle`، وأخيرًا **إضافة الشكل إلى PDF**، يمكنك توليد رسومات متجهية ببضع أسطر فقط. سواء كنت تحتاج إلى **إضافة مستطيل إلى PDF** للتمييز، أو لتصحيح تخطيط، أو لتراكب واجهة مستخدم، فإن النهج يتوسع بسهولة.

بعد ذلك، يمكنك استكشاف **رسم أشكال على PDF** بخلاف المستطيلات—مثل الدوائر، الخطوط المتعددة، أو حتى مسارات SVG مخصصة. أو الغوص في رسم النصوص، إدراج الصور، ومعالجة نماذج PDF لبناء تقارير متكاملة. مكتبة Aspose.Pdf تقدم API غني، ومع الأساسيات التي غطيناها الآن أنت جاهز للتجربة.

برمجة سعيدة، ولتظهر ملفات PDF دائمًا كما تتخيل!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}