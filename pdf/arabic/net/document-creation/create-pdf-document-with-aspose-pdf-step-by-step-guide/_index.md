---
category: general
date: 2026-01-15
description: إنشاء مستند PDF باستخدام Aspose.Pdf في C#. تعلم كيفية إضافة صفحة إلى
  PDF وتعيين لون تعبئة المستطيل مع معالجة الأشكال خارج الحدود.
draft: false
keywords:
- create pdf document
- add page to pdf
- set rectangle fill color
language: ar
og_description: إنشاء مستند PDF في C# باستخدام Aspose.Pdf. يوضح هذا الدليل كيفية إضافة
  صفحة إلى PDF، وتعيين لون تعبئة المستطيل، والتحقق من الحدود.
og_title: إنشاء مستند PDF باستخدام Aspose.Pdf – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF Generation
title: إنشاء مستند PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة

هل احتجت يومًا إلى **إنشاء مستند PDF** برمجيًا ولم تكن متأكدًا من أين تبدأ؟ لست وحدك — يواجه العديد من المطورين نفس الصعوبة عندما يتعاملون لأول مرة مع أتمتة PDF. في هذا الدليل سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح لك كيفية **إضافة صفحة إلى PDF**، رسم مستطيل، و**تعيين لون تعبئة المستطيل** مع السماح لـ Aspose.Pdf بالتحقق من حدود الشكل.

سنتناول كل شيء بدءًا من تهيئة المستند وحتى معالجة الاستثناء الحتمي `ArgumentException` الذي يحدث عندما يتجاوز الشكل حدود الصفحة. في النهاية ستحصل على مقتطف جاهز للنسخ واللصق وفهم واضح لأهمية كل سطر.

![مثال على إنشاء مستند PDF](/images/create-pdf-document.png "لقطة شاشة لمستند PDF تم إنشاؤه يظهر شكل مستطيل")

---

## ما يغطيه هذا الدليل

- المتطلبات المسبقة وحزم NuGet المطلوبة  
- كيفية **إنشاء مستند PDF** باستخدام Aspose.Pdf  
- إضافة صفحة جديدة باستخدام **add page to pdf**  
- رسم مستطيل و**تعيين لون تعبئة المستطيل**  
- تمكين `VerifyBoundary` لاكتشاف الأشكال خارج الحدود  
- معالجة الأخطاء بشكل صحيح والنتائج المتوقعة  

بدون حشو، فقط الجوانب العملية التي يمكنك إدراجها في مشروع حقيقي اليوم.

---

## المتطلبات المسبقة

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 أو أحدث | يدعم Aspose.Pdf معيار .NET Standard 2.0+، لذا فإن أوقات التشغيل الحديثة تمنحك أفضل أداء. |
| Visual Studio 2022 (or any C# IDE) | يجعل تصحيح الأخطاء وإدارة حزم NuGet سهلًا دون عناء. |
| Aspose.Pdf for .NET NuGet package | يوفر الفئات `Document` و `Page` و `RectangleShape` وغيرها التي سنستخدمها. |
| Basic C# knowledge | ليس من الضروري أن تكون خبيرًا، لكن الإلمام بالفئات ومعالجة الاستثناءات يساعد. |

ثبت المكتبة باستخدام:

```bash
dotnet add package Aspose.Pdf
```

---

## الخطوة 1 – تهيئة مستند PDF

أول شيء تقوم به عند **إنشاء مستند PDF** هو إنشاء كائن من الفئة `Document`. فكر فيه كدفتر فارغ ستضيف إليه لاحقًا صفحات، نصوص، صور، وأشكال.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Graphics;
using System.Drawing;   // For Color

// Create a new PDF document – this is your canvas.
Document pdfDocument = new Document();
```

*لماذا هذا مهم*: كائن `Document` يملك هيكل الملف بالكامل. بدون هذا الكائن لا مكان لإرفاق الصفحات أو الرسومات، وأي استدعاءات API لاحقة ستؤدي إلى استثناء `NullReferenceException`.

---

## الخطوة 2 – **إضافة صفحة إلى PDF** وتحديد حجمها

الآن بعد أن لدينا مستندًا، نحتاج إلى صفحة واحدة على الأقل. إضافة صفحة هي سطر واحد، لكننا سنلتقط أبعاد الصفحة لأننا سنحتاجها لاحقًا عندما ننشئ مستطيلًا خارج الحدود عن قصد.

```csharp
// Add a new page to the document.
Page pdfPage = pdfDocument.Pages.Add();

// Store page dimensions for later calculations.
float pageWidth  = pdfPage.PageInfo.Width;
float pageHeight = pdfPage.PageInfo.Height;
```

*نصيحة احترافية*: إذا احتجت إلى حجم صفحة مخصص (مثلاً A5 أو تنسيق قانوني)، عدل `pdfPage.PageInfo.Width` و `Height` **قبل** بدء الرسم.

---

## الخطوة 3 – **تعيين لون تعبئة المستطيل** ووضعه خارج الحدود

هنا يصبح الدليل أكثر إثارة. سننشئ `RectangleShape` أكبر عمدًا من الصفحة، ثم نفعّل `VerifyBoundary` لكي يطرح Aspose.Pdf استثناءً إذا لم يتناسب الشكل.

```csharp
// Define a rectangle that is 10 units wider and taller than the page.
Rectangle outOfBoundsRect = new Rectangle(
    pageWidth + 10,   // X‑coordinate (right edge)
    pageHeight + 10,  // Y‑coordinate (top edge)
    100,               // Width of the rectangle
    100);              // Height of the rectangle

// Create the rectangle shape with a light gray fill and black stroke.
RectangleShape rectangleShape = new RectangleShape(outOfBoundsRect)
{
    StrokeColor = Color.Black,
    FillColor   = Color.LightGray,
    VerifyBoundary = true   // Enables boundary validation.
};
```

*لماذا نضبط `FillColor`*: خاصية `FillColor` تحدد لون داخل الشكل. استخدام `Color.LightGray` يجعل المستطيل يبرز على صفحة بيضاء، وهو مفيد بشكل خاص عند تصحيح مشاكل التخطيط.

---

## الخطوة 4 – إضافة الشكل إلى مجموعة الفقرات في الصفحة

يتعامل Aspose.Pdf مع معظم الكائنات القابلة للرسم كـ “فقرات”. إضافة المستطيل إلى مجموعة `Paragraphs` في الصفحة يخبر المحرك برسمه عند حفظ الـ PDF.

```csharp
// Insert the rectangle into the page.
pdfPage.Paragraphs.Add(rectangleShape);
```

*خطأ شائع*: نسيان هذه الخطوة ينتج عنه شكل معرف تمامًا لكنه لا يظهر أبدًا في الـ PDF النهائي. تأكد دائمًا من إضافة الكائن إلى حاوية (`Paragraphs`، `Tables`، إلخ).

---

## الخطوة 5 – حفظ المستند ومعالجة الاستثناء المتوقع

عند استدعاء `Save`، يتحقق Aspose.Pdf من المستطيل لأننا فعلنا `VerifyBoundary`. بما أن المستطيل يتجاوز حجم الصفحة، يُطرح استثناء `ArgumentException`. دعنا نلتقطه بلطف ونسجل التفاصيل.

```csharp
try
{
    // Attempt to save – this will trigger boundary validation.
    pdfDocument.Save("shape_out.pdf");
    Console.WriteLine("PDF saved successfully. Check shape_out.pdf.");
}
catch (ArgumentException ex)
{
    Console.WriteLine("Caught ArgumentException: The shape exceeds page bounds.");
    Console.WriteLine($"Error details: {ex.Message}");
}
```

**الناتج المتوقع**:

```
Caught ArgumentException: The shape exceeds page bounds.
Error details: The rectangle shape is out of page bounds.
```

إذا علقّت `VerifyBoundary = true` أو صغرت المستطيل ليتناسب، سيتم حفظ الـ PDF بشكل طبيعي وسترى المستطيل الرمادي الفاتح في الزاوية السفلية اليمنى للصفحة.

---

## مثال كامل يعمل

انسخ المقتطف الكامل أدناه إلى مشروع كونسول جديد وشغّله. يوضح كل خطوة في مكان واحد، مما يسهل تجربة أحجام، ألوان، أو اتجاهات صفحة مختلفة.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Graphics;
using System;
using System.Drawing;   // For Color

class Program
{
    static void Main()
    {
        // Step 1: Initialize the PDF document.
        Document pdfDocument = new Document();

        // Step 2: Add a page and capture its dimensions.
        Page pdfPage = pdfDocument.Pages.Add();
        float pageWidth  = pdfPage.PageInfo.Width;
        float pageHeight = pdfPage.PageInfo.Height;

        // Step 3: Define an out‑of‑bounds rectangle and set its fill color.
        Rectangle outOfBoundsRect = new Rectangle(
            pageWidth + 10,   // X coordinate (beyond right edge)
            pageHeight + 10,  // Y coordinate (beyond top edge)
            100,               // Width
            100);              // Height

        RectangleShape rectangleShape = new RectangleShape(outOfBoundsRect)
        {
            StrokeColor = Color.Black,
            FillColor   = Color.LightGray,
            VerifyBoundary = true   // Enables validation.
        };

        // Step 4: Add the rectangle to the page.
        pdfPage.Paragraphs.Add(rectangleShape);

        // Step 5: Save and handle the expected exception.
        try
        {
            pdfDocument.Save("shape_out.pdf");
            Console.WriteLine("PDF saved successfully.");
        }
        catch (ArgumentException ex)
        {
            Console.WriteLine("Caught ArgumentException: The shape exceeds page bounds.");
            Console.WriteLine($"Details: {ex.Message}");
        }
    }
}
```

شغّله، وسترى رسالة الكونسول التي تؤكد أن المستطيل كان خارج الحدود. عدّل أبعاد `outOfBoundsRect` أو اضبط `VerifyBoundary = false` لإنشاء ملف PDF عادي.

---

## أسئلة شائعة وحالات حافة

**ماذا لو أردت أن يبقى المستطيل داخل الصفحة؟**  
قلل إحداثيات X و Y لتكون أقل من `pageWidth` و `pageHeight`. على سبيل المثال، استخدم `pageWidth - 120` و `pageHeight - 120` لتضعه بالقرب من الزاوية السفلية اليمنى.

**هل يمكنني تغيير لون التعبئة ديناميكيًا؟**  
بالطبع. استبدل `Color.LightGray` بأي قيمة من `System.Drawing.Color`، أو حتى أنشئ لونًا مخصصًا عبر `Color.FromArgb(alpha, red, green, blue)`.

**هل يعمل `VerifyBoundary` مع أشكال أخرى؟**  
نعم. ينطبق على `Ellipse` و `Polygon` و `TextFragment` وأي كائن يطبق `IShape`. تفعيلها طريقة ممتازة لاكتشاف أخطاء التخطيط مبكرًا.

**ماذا عن المستندات متعددة الصفحات؟**  
يمكنك تكرار خطوة “إضافة صفحة” لكل صفحة تحتاجها. تذكر الإشارة إلى كائن `Page` الصحيح عند وضع الأشكال؛ كل صفحة لها نظام إحداثياتها الخاص.

---

## الخلاصة

لقد **أنشأنا مستند PDF** من الصفر باستخدام Aspose.Pdf، **أضفنا صفحة إلى PDF**، وأظهرنا كيفية **تعيين لون تعبئة المستطيل** مع الاستفادة من `VerifyBoundary` لفرض قواعد التخطيط. المثال الكامل جاهز للنسخ واللصق، والآن تفهم *سبب* كل استدعاء API.

من هنا قد ترغب في:
- تجربة أشكال مختلفة (إهليلج، مضلع).  
- إضافة نص باستخدام `TextFragment` وتنسيقه بالخطوط.  
- تصدير PDF إلى تدفق ذاكرة لاستخدامه في واجهات برمجة التطبيقات على الويب.  

الإمكانات لا حصر لها، والنمط الذي اتبعناه — تهيئة، إضافة صفحة، رسم، تحقق، حفظ — سيساعدك في أي مهمة أتمتة PDF.  

هل لديك أسئلة أخرى؟ اترك تعليقًا، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}