---
category: general
date: 2026-04-06
description: أضف مستطيلًا إلى ملف PDF بسرعة باستخدام C#. تعلم كيفية رسم مستطيل على
  PDF، تحميل مستند PDF باستخدام C#، واستخدام Aspose PDF لرسم المستطيل في هذا الدليل
  خطوة بخطوة.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- draw shape in pdf
- load pdf document c#
- aspose pdf draw rectangle
language: ar
og_description: أضف مستطيلًا إلى PDF على الفور. يوضح هذا الدليل كيفية رسم مستطيل على
  PDF، وتحميل مستند PDF باستخدام C#، واستخدام Aspose PDF لرسم المستطيل مع أمثلة شفرة
  واضحة.
og_title: إضافة مستطيل إلى PDF باستخدام C# – دليل Aspose PDF الكامل
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: إضافة مستطيل إلى PDF باستخدام C# – دليل Aspose PDF الكامل
url: /ar/net/images-graphics/add-rectangle-to-pdf-with-c-full-aspose-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة مستطيل إلى PDF – دليل Aspose PDF الكامل

هل احتجت يوماً إلى **إضافة مستطيل إلى PDF** لكنك لم تكن متأكدًا من أي استدعاء API ينجز المهمة؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عند أتمتة التقارير أو تمييز أقسام في مستند. في هذا الدليل سنستعرض الخطوات الدقيقة لـ **رسم مستطيل على PDF** باستخدام Aspose.PDF لـ .NET، وسترى مثالًا كاملاً قابلاً للتنفيذ يمكنك إدراجه في مشروعك الخاص.

سنغطي أيضًا كيفية **load PDF document C#**، والتحقق من أن الشكل يتناسب مع الصفحة، ومناقشة بعض المشكلات الشائعة عندما تحاول **draw shape in PDF**. في النهاية ستحصل على برنامج يعمل يضيف مستطيلًا أصفرًا ساطعًا إلى الصفحة الأولى من أي PDF تشير إليه.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- حزمة NuGet لـ Aspose.PDF for .NET (الإصدار 23.11 أو أحدث)
- ملف PDF تجريبي (`input.pdf`) موجود في مجلد يمكنك الإشارة إليه
- Visual Studio أو VS Code أو أي بيئة تطوير C# تفضلها

لا توجد ملفات تكوين إضافية، ولا COM interop، فقط بضع جمل `using` وبعض الأسطر المنطقية.

## الخطوة 1: تحميل مستند PDF C# – تجهيز الملف

أول شيء يجب عليك القيام به هو فتح ملف PDF الموجود حتى يكون لديك ما يمكنك الرسم عليه. تجعل Aspose.PDF ذلك بسطر واحد.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color

// Step 1: Load the PDF document
var inputPath = @"C:\MyPdfs\input.pdf";
using var pdfDocument = new Document(inputPath);
```

**لماذا هذا مهم:**  
`Document` يمثل ملف PDF بالكامل. من خلال وضعه داخل كتلة `using` نضمن تحرير مقبض الملف فور الانتهاء، مما يمنع مشاكل قفل الملف على Windows. إذا نسيت `using`، قد ترى رسالة “cannot access the file because it is being used by another process” لاحقًا عند محاولة الحفظ.

## الخطوة 2: الوصول إلى الصفحة المستهدفة والتحقق من الحدود – رسم الشكل في PDF بأمان

قبل أن تلصق مستطيلًا على الصفحة، تحتاج إلى كائن الصفحة ويجب عليك التأكد من أن المستطيل يتناسب داخل أبعاد الصفحة. هذا يمنع استثناءات وقت التشغيل ويحافظ على مظهر PDF مرتبًا.

```csharp
// Step 2: Get the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define rectangle bounds: lower‑left X/Y and upper‑right X/Y
var rectangleBounds = new Rectangle(50, 700, 200, 800);

// Verify the rectangle is inside the page limits
bool fits = rectangleBounds.LLX >= 0 &&
            rectangleBounds.URX <= firstPage.PageInfo.Width &&
            rectangleBounds.LLY >= 0 &&
            rectangleBounds.URY <= firstPage.PageInfo.Height;

if (!fits)
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

**شرح:**  
منشئ `Rectangle` يتوقع أربعة أرقام: X الأسفل‑اليسار، Y الأسفل‑اليسار، X الأعلى‑اليمين، Y الأعلى‑اليمين. تُقاس هذه القيم بالنقاط (1 pt ≈ 1/72 in). خطوة التحقق هي شبكة أمان صغيرة—مفيدة خاصةً عندما تحسب الإحداثيات بشكل ديناميكي (مثلاً بناءً على حجم الصورة أو طول النص).

## الخطوة 3: إضافة مستطيل إلى PDF – جوهر “Add Rectangle to PDF”

الآن الجزء الممتع: إدراج الشكل فعليًا. توفر Aspose.PDF فئة `RectangleShape` التي يمكنك وضعها في مجموعة `Paragraphs` الخاصة بالصفحة.

```csharp
// Step 3: Add a yellow rectangle shape
var rectangleShape = new RectangleShape(rectangleBounds)
{
    FillColor = Color.Yellow,
    Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black) // Optional: thin black border
};

firstPage.Paragraphs.Add(rectangleShape);
```

**لماذا نستخدم `RectangleShape`؟**  
إنه رسم متجه، لذا يتوسع المستطيل بسلاسة على أي جهاز. إضافته إلى `Paragraphs` يعني أنه يتصرف كأي عنصر محتوى آخر—موقعه بالنسبة للصفحة، وليس بالنسبة للنص الموجود. إذا كنت بحاجة إلى تعبئة شفافة، ما عليك سوى تعيين `FillColor = Color.Transparent`.

> **نصيحة احترافية:** غيّر `FillColor` إلى `Color.FromArgb(128, 255, 255, 0)` للحصول على أصفر شبه شفاف يسمح للنص الموجود خلفه بالظهور.

## الخطوة 4: حفظ PDF المحدث – إكمال دورة “Add Rectangle to PDF”

بمجرد وضع الشكل، تقوم ببساطة بحفظ المستند إلى ملف جديد (أو استبدال الأصلي إذا كنت تفضل ذلك).

```csharp
// Step 4: Save the updated PDF
var outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

هذا كل شيء! افتح `output.pdf` وسترى مستطيلًا أصفرًا ساطعًا يجلس بإحكام بين الإحداثيات التي حددتها.

## مثال كامل يعمل – جميع الخطوات في ملف واحد

فيما يلي البرنامج الكامل المستقل الذي يمكنك تجميعه وتشغيله كما هو. يتضمن معالجة الأخطاء وتعليقات تشرح كل سطر.

```csharp
// ---------------------------------------------------------------
// AddRectangleToPdf.cs
// Demonstrates how to add rectangle to PDF using Aspose.PDF for .NET
// ---------------------------------------------------------------
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddRectangleToPdf
{
    static void Main()
    {
        // ----- 1. Load the PDF document -----
        string inputPath = @"C:\MyPdfs\input.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        using var pdfDoc = new Document(inputPath);

        // ----- 2. Access first page and define rectangle bounds -----
        Page page = pdfDoc.Pages[1];
        var rect = new Rectangle(50, 700, 200, 800);

        // Verify rectangle fits the page
        bool fits = rect.LLX >= 0 && rect.URX <= page.PageInfo.Width &&
                    rect.LLY >= 0 && rect.URY <= page.PageInfo.Height;
        if (!fits)
        {
            Console.WriteLine("Rectangle exceeds page dimensions. Adjust coordinates.");
            return;
        }

        // ----- 3. Create and add rectangle shape -----
        var shape = new RectangleShape(rect)
        {
            FillColor = Color.Yellow,
            Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black)
        };
        page.Paragraphs.Add(shape);

        // ----- 4. Save the modified PDF -----
        string outputPath = @"C:\MyPdfs\output.pdf";
        pdfDoc.Save(outputPath);
        Console.WriteLine($"Rectangle added successfully. Saved to {outputPath}");
    }
}
```

**النتيجة المتوقعة:**  
عند فتح `output.pdf`، ستظهر الصفحة الأولى مستطيلًا أصفرًا يبدأ زاويه السفلية‑اليسرى عند (50 pt, 700 pt) وينتهي الزاوية العليا‑اليمنى عند (200 pt, 800 pt). سيكون للمستطيل حد أسود رفيع، مما يجعله واضحًا على معظم الخلفيات.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى رسم المستطيل على صفحة مختلفة؟

ما عليك سوى تغيير `pdfDoc.Pages[1]` إلى رقم الصفحة المطلوبة (`pdfDoc.Pages[3]` للصفحة الثالثة). تذكر أن Aspose يستخدم الفهرسة بدءًا من 1، وليس من 0.

### هل يمكنني رسم مستطيلات متعددة داخل حلقة؟

بالطبع. ضع منطق إنشاء المستطيل داخل حلقة `foreach` على مجموعة من الإحداثيات. فقط احرص على الأداء؛ إضافة آلاف الأشكال قد يزيد حجم الملف بشكل ملحوظ.

### كيف يختلف هذا عن استخدام `Graphics` أو `System.Drawing`؟

`System.Drawing` يعمل مع الصور النقطية؛ يتم دمج الناتج في صورة bitmap، والتي قد تصبح غير واضحة عند التكبير. `RectangleShape` يعتمد على المتجهات، مما يعني أنه يبقى واضحًا عند أي مستوى تكبير—مثالي لـ PDFs الاحترافية.

### ماذا لو كان PDF محميًا بكلمة مرور؟

حمّل المستند باستخدام كائن `PdfLoadOptions` الذي يتضمن كلمة المرور:

```csharp
var loadOpts = new PdfLoadOptions { Password = "mySecret" };
using var pdfDoc = new Document(inputPath, loadOpts);
```

ثم تابع كالمعتاد. سيُضاف المستطيل بمجرد فك تشفير المستند في الذاكرة.

## مرجع بصري

![مثال إضافة مستطيل إلى PDF يظهر الشكل الأصفر في الصفحة الأولى](/images/add-rectangle-to-pdf-example.png)

*نص بديل: “مثال إضافة مستطيل إلى PDF مع مستطيل أصفر في الصفحة الأولى”*

## ملخص وخطوات مستقبلية

لقد غطينا للتو كيفية **add rectangle to PDF** باستخدام Aspose.PDF لـ .NET، من تحميل المستند إلى حفظ الملف المعدل. النقاط الرئيسية:

1. تحميل PDF (`load pdf document c#`) مع التخلص المناسب.
2. تحديد حدود المستطيل والتحقق من أنها تناسب الصفحة.
3. استخدم `RectangleShape` لـ **draw rectangle on pdf** (أو أي **draw shape in pdf** أخرى قد تحتاجها).
4. احفظ النتيجة واستمتع بمستطيل حاد كمتجه.

هل أنت مستعد للمزيد؟ جرّب استبدال `RectangleShape` بـ `EllipseShape` أو `PolygonShape` لإنشاء تمييزات مخصصة. أو استكشف قدرات استخراج النص في Aspose لتحديد مواضع الأشكال ديناميكيًا بناءً على مواقع الكلمات المفتاحية. المكتبة غنية بما يكفي لتتيح لك بناء أدوات تعليقات توضيحية كاملة دون مغادرة C#.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه—سأكون سعيدًا بالمساعدة. ولا تنسَ إعطاء نجمة لحزمة Aspose.PDF على NuGet إذا وجدتها مفيدة. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}