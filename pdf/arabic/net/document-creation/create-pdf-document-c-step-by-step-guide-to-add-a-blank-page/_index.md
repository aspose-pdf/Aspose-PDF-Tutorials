---
category: general
date: 2026-04-10
description: إنشاء مستند PDF باستخدام C# بسرعة. تعلم كيفية إضافة صفحة فارغة إلى PDF،
  ورسم مستطيل في PDF، وإضافة شكل مستطيل وإدراجه في PDF بكود واضح.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- add rectangle shape
- add rectangle to pdf
language: ar
og_description: إنشاء مستند PDF باستخدام C# في دقائق. يوضح هذا الدليل كيفية إضافة
  صفحة PDF فارغة، ورسم مستطيل في PDF، وإضافة شكل مستطيل باستخدام كود سهل.
og_title: إنشاء مستند PDF باستخدام C# – دليل كامل
tags:
- C#
- PDF
- Aspose.PDF
- Document Generation
title: إنشاء مستند PDF بلغة C# – دليل خطوة بخطوة لإضافة صفحة فارغة ورسم مستطيل
url: /ar/net/document-creation/create-pdf-document-c-step-by-step-guide-to-add-a-blank-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF C# – دليل شامل

هل احتجت يوماً إلى **create PDF document C#** لميزة تقارير ولكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في كثير من المشاريع العائق الأول هو الحصول على PDF صفحة فارغة نظيفة ثم رسم رسومات بسيطة مثل المستطيل.

في هذا الدرس سنحل هذه المشكلة فورًا: ستتعرف على كيفية إضافة صفحة PDF فارغة، ورسم مستطيل PDF، وأخيرًا إضافة شكل المستطيل إلى الملف—كل ذلك بضع أسطر من C#. في النهاية ستحصل على ملف `shapes.pdf` جاهز للاستخدام يمكنك فتحه في أي عارض.

## ما ستتعلمه

- كيفية تهيئة مستند PDF باستخدام Aspose.PDF for .NET.  
- الخطوات الدقيقة **add blank page pdf** وتحديد موقع مستطيل داخلها.  
- لماذا يعتبر الصف `Rectangle` الاختيار المناسب لرسم الأشكال.  
- الأخطاء الشائعة مثل عدم تطابق حجم الصفحة وكيفية تجنبها.  

بدون أدوات خارجية، بدون سحر—فقط كود C# نقي يمكنك نسخه ولصقه في تطبيق Console.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+).  
- حزمة NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`).  
- فهم أساسي لصياغة C# (المتغيرات، عبارات `using`، إلخ).  

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فإن مدير حزم NuGet يجعل تثبيت Aspose.PDF بنقرة واحدة.

## الخطوة 1: تهيئة مستند PDF

إنشاء PDF يبدأ بكائن `Document`. فكر فيه كقماش سيحمل كل صفحة، صورة أو شكل تضيفه لاحقًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Initialise a new PDF document – this is the core of create pdf document c#
var pdfDocument = new Document();
```

يمنحك الصف `Document` إمكانية الوصول إلى مجموعة `Pages`، وهي المكان الذي سنضيف فيه لاحقًا **add blank page pdf**.

## الخطوة 2: إضافة صفحة فارغة إلى المستند

PDF بدون صفحات هو في الأساس فارغ. إضافة صفحة بسيطة كاستدعاء `pdfDocument.Pages.Add()`. الصفحة الجديدة ترث الحجم الافتراضي (A4) ما لم تحدد غير ذلك.

```csharp
// Add a fresh, blank page – this satisfies the add blank page pdf requirement
Page page = pdfDocument.Pages.Add();
```

> **لماذا هذا مهم:** إضافة الصفحة أولاً يضمن أن أي أوامر رسم لاحقة لديها سطح للعرض عليه. تخطي هذه الخطوة سيسبب خطأً أثناء التشغيل عندما تحاول رسم مستطيل.

## الخطوة 3: تعريف حدود المستطيل

الآن سنقوم **draw rectangle pdf** بإنشاء كائن `Rectangle`. المُنشئ يأخذ إحداثيات X/Y السفلية اليسرى متبوعة بالعرض والارتفاع. في مثالنا نريد مستطيلًا يناسب الصفحة بشكل جميل، مع ترك هامش صغير.

```csharp
// Rectangle coordinates: (0,0) is the lower‑left corner of the page
// Width = 500, Height = 700 – fits comfortably on an A4 page
var rectangle = new Rectangle(0, 0, 500, 700);
```

إذا كنت بحاجة إلى حجم مختلف، فقط عدّل قيم العرض/الارتفاع. أصل المستطيل (0,0) يتطابق مع الزاوية السفلية اليسرى للصفحة، وهو مصدر شائع للارتباك للمبتدئين.

## الخطوة 4: إضافة شكل المستطيل إلى الصفحة

مع كائن المستطيل جاهز، يمكننا **add rectangle shape** إلى الصفحة. طريقة `AddRectangle` ترسم الحدود باستخدام حالة الرسومات الحالية (الافتراضي هو خط أسود رفيع).

```csharp
// Add the rectangle shape – this completes the add rectangle to pdf step
page.AddRectangle(rectangle);
```

يمكنك تخصيص المظهر بتعديل كائن `Graphics` قبل استدعاء `AddRectangle`، مثل ضبط `LineWidth` أو `Color`. للحصول على تعبئة صلبة يمكنك استخدام `page.AddAnnotation(new SquareAnnotation(...))`، لكن ذلك خارج نطاق هذا الدليل البسيط.

## الخطوة 5: حفظ ملف PDF

أخيرًا، احفظ المستند على القرص. اختر مجلدًا لديك صلاحية كتابة فيه، ومنح الملف اسمًا معبرًا مثل `shapes.pdf`.

```csharp
// Save the PDF – you’ll find shapes.pdf in the specified directory
pdfDocument.Save(@"C:\Temp\shapes.pdf");
```

> **ملاحظة:** عبارة `using` في المقتطف الأصلي ليست ضرورية هنا لأن `Document` يطبق `IDisposable`. ومع ذلك، تغليفها بـ `using` عادة جيدة لتنظيف الموارد، خاصة في التطبيقات الأكبر.

## مثال كامل يعمل

نجمع كل ما سبق في برنامج Console مستقل يمكنك تشغيله فورًا:

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
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add a blank page to the document
                Page page = pdfDocument.Pages.Add();

                // Step 3: Define a rectangle that fits inside the page bounds (0,0 to 500,700)
                var rectangle = new Rectangle(0, 0, 500, 700);

                // Step 4: Add the rectangle shape to the page
                page.AddRectangle(rectangle);

                // Step 5: Save the PDF file
                string outputPath = @"C:\Temp\shapes.pdf";
                pdfDocument.Save(outputPath);

                Console.WriteLine($"PDF created successfully at {outputPath}");
            }
        }
    }
}
```

**الناتج المتوقع:** بعد تشغيل البرنامج، افتح `C:\Temp\shapes.pdf`. سترى صفحة واحدة بها مستطيل بخط أسود محيط يقع في الزاوية السفلية اليسرى، بحجم 500 × 700 نقطة بالضبط.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني تغيير حجم الصفحة قبل إضافة المستطيل؟* | نعم. أنشئ `Page` بأبعاد مخصصة: `var page = pdfDocument.Pages.Add(); page.PageInfo.Width = 600; page.PageInfo.Height = 800;` |
| *ماذا إذا احتجت إلى مستطيل مملوء؟* | استخدم كائن `Graphics`: `page.Canvas.Rectangle(rectangle, Color.Blue, Color.LightBlue);` |
| *هل Aspose.PDF مجاني؟* | يقدم **نسخة تجريبية مجانية** مع جميع الوظائف؛ يتطلب ترخيص تجاري للاستخدام في الإنتاج. |
| *كيف أضيف مستطيلات متعددة؟* | ببساطة كرّر الخطوتين 3‑4 مع كائنات `Rectangle` مختلفة أو عدّل الإحداثيات. |

## الخطوات التالية

الآن بعد أن عرفت كيف **create pdf document c#**، **add blank page pdf**، و**draw rectangle pdf**، قد ترغب في استكشاف:

- إضافة نص داخل المستطيل (`TextFragment`, `page.Paragraphs.Add`).  
- إدراج صور (`page.Resources.Images.Add`) لبناء تقارير أغنى.  
- تصدير PDF إلى صيغ أخرى مثل PNG أو DOCX باستخدام واجهات التحويل في Aspose.  

جميع هذه المواضيع تتفرع طبيعيًا من أساس **add rectangle to pdf** الذي بنيناه هنا.

---

*برمجة سعيدة!* إذا واجهت أي صعوبات، لا تتردد بترك تعليق أدناه. وتذكر—بمجرد إتقان الأساسيات، يصبح إنشاء PDFs معقدة أمرًا سهلًا.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}