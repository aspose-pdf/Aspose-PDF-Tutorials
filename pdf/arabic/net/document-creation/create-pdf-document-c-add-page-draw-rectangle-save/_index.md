---
category: general
date: 2026-02-14
description: 'إنشاء مستند PDF باستخدام C# بسرعة: إضافة صفحة إلى PDF، رسم شكل مستطيل،
  وحفظ PDF إلى ملف باستخدام Aspose.Pdf في بضع أسطر من الشيفرة.'
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: ar
og_description: إنشاء مستند PDF باستخدام C# في دقائق. تعلم كيفية إضافة صفحة إلى PDF،
  ورسم مستطيل، وإضافة شكل إلى PDF، وحفظ PDF إلى ملف مع أمثلة شفرة واضحة.
og_title: إنشاء مستند PDF باستخدام C# – دليل خطوة بخطوة
tags:
- Aspose.Pdf
- C#
- PDF generation
title: إنشاء مستند PDF C# – إضافة صفحة، رسم مستطيل وحفظ
url: /ar/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF C# – إضافة صفحة، رسم مستطيل وحفظه

هل احتجت يوماً إلى **create PDF document C#** من الصفر وتساءلت من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون نفس الصعوبة عندما يتعاملون لأول مرة مع إنشاء ملفات PDF برمجياً. الخبر السار؟ ببضع أسطر من كود Aspose.Pdf يمكنك إضافة صفحة إلى PDF، رسم مستطيل، و**save PDF to file** دون عناء.

في هذا الدرس سنستعرض كل ما تحتاجه: تهيئة ملف PDF، إدراج صفحة جديدة، رسم شكل مستطيل، وأخيراً حفظ الملف على القرص. في النهاية ستحصل على تطبيق كونسول يعمل وينتج مستطيل بحدود زرقاء داخل صفحة PDF جديدة.

## ما الذي ستحتاجه

- **.NET 6 أو أحدث** (العينة تستخدم top‑level statements، لكن أي نسخة حديثة من .NET تعمل)
- حزمة NuGet **Aspose.Pdf for .NET**  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- مجلد لديك صلاحية كتابة فيه – سيحفظ الدرس الملف في `YOUR_DIRECTORY/shapes.pdf`.

لا إعدادات إضافية، لا XML، مجرد C# عادي.

## إنشاء مستند PDF C# – نظرة عامة

الخطوة الأولى هي إنشاء كائن `Document`. فكر فيه كقماش فارغ؛ كل ما تضيفه لاحقاً—صفحات، نصوص، أشكال—يُرفق بهذا الكائن الواحد.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **لماذا `using var`؟**  
> فئة `Document` تُطبق `IDisposable`. وضعها داخل جملة `using` يضمن تحرير جميع الموارد غير المُدارة (مقابض الملفات، المخازن الأصلية) فور الانتهاء، وهذا مهم خصوصاً في الخدمات طويلة التشغيل.

## إضافة صفحة إلى PDF

ملف PDF بدون صفحات يشبه كتاباً بلا صفحات—غير مفيد. إضافة صفحة هي استدعاء طريقة واحد، وتُعيد لك كائن `Page` يمكنك التلاعب به لاحقاً.

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **نصيحة:** الصفحة المضافة حديثاً تتبنى الحجم الافتراضي (A4) تلقائياً. إذا كنت تحتاج حجمًا مخصصًا، يمكنك ضبط `pdfPage.PageInfo.Width` و `Height` قبل إضافة أي محتوى.

## كيفية رسم مستطيل

الآن للجزء الممتع: رسم مستطيل. تستخدم Aspose.Pdf الفئة `RectangleShape`، التي تتوقع كائن `Rectangle` (x, y, width, height) يحدد الحدود. تبدأ الإحداثيات من الزاوية السفلية اليسرى للصفحة.

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **حالة حافة:** إذا كان `x + width` يتجاوز عرض الصفحة أو `y + height` يتجاوز ارتفاع الصفحة، تُطلق Aspose استثناء `ArgumentException`. تأكد دائمًا من أبعادك، خاصةً عند إنشاء ملفات PDF لأحجام صفحات مختلفة.

## إضافة الشكل إلى PDF

بعد إعداد الحدود، ننشئ الشكل، نُعطيه حدًا أزرق، ونضيفه إلى مجموعة الفقرات في الصفحة.

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **لماذا نضيفه إلى `Paragraphs`؟**  
> في Aspose.Pdf، تُعامل العناصر البصرية مثل الأشكال كـ “فقرات” لأنها تشغل مساحة مستطيلة على الصفحة. هذا التصميم يحافظ على تناسق محرك التخطيط بين النص والرسومات.

## حفظ PDF إلى ملف

الخطوة الأخيرة هي حفظ المستند. قدم مسارًا كاملاً، وتتعامل Aspose مع كل التفاصيل—الضغط، تدفقات الكائنات، وجداول المراجع المتقاطعة—تلقائيًا.

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **نصيحة احترافية:** استخدم `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")` إذا أردت وضع الملف بجوار الملف التنفيذي، أو أنشئ المجلد مسبقًا بـ `Directory.CreateDirectory` لتجنب استثناء `DirectoryNotFoundException`.

### النتيجة المتوقعة

افتح `shapes.pdf` بأي عارض PDF. يجب أن ترى صفحة واحدة بحجم A4 تحتوي على **مستطيل بحدود زرقاء** موضعه 50 نقطة من الحافة اليسرى والسفلية، بأبعاد 200 × 150 نقطة. لا نص، فقط الشكل—مثالي كعلامات مائية أو حقول نماذج أو عناصر نائبة بصرية.

![PDF document with a blue rectangle created using create pdf document c#](https://example.com/images/pdf-rectangle.png "PDF document with a blue rectangle created using create pdf document c#")

*Alt text:* *PDF document with a blue rectangle created using create pdf document c#.*

## مثال كامل يعمل

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. يُجمع كتطبيق كونسول (`dotnet new console`) ويعمل دون أي إعدادات إضافية بخلاف حزمة NuGet.

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

شغّل البرنامج، افتح الملف المُولد، وسترى الشكل بالضبط حيث عرّفته.

## أسئلة شائعة ومشكلات محتملة

- **س:** *ماذا لو أردت مستطيلًا مملوءًا؟*  
  **ج:** ألغِ التعليق عن سطر `FillColor` في مُهيئ `RectangleShape`. تدعم Aspose الألوان الصلبة، التدرجات، وحتى ملء الصور.

- **س:** *هل يمكنني رسم عدة أشكال على نفس الصفحة؟*  
  **ج:** بالتأكيد. فقط أنشئ كائنات `RectangleShape`، `Ellipse` أو `Polygon` إضافية وأضف كل واحدة إلى `pdfPage.Paragraphs`.

- **س:** *هل نظام الإحداثيات دائمًا من الزاوية السفلية اليسرى؟*  
  **ج:** نعم، تتبع Aspose مواصفات PDF حيث الأصل (0,0) يكون في الزاوية السفلية اليسرى. إذا كنت تفضّل الأصل من الزاوية العليا اليسرى، سيتعين عليك حساب `y = pageHeight - desiredY`.

- **س:** *ماذا يحدث إذا لم يكن المجلد الهدف موجودًا؟*  
  **ج:** سيُطلق `pdfDocument.Save` استثناء `DirectoryNotFoundException`. أنشئ المجلد مسبقًا باستخدام `Directory.CreateDirectory`.

## الخطوات التالية

الآن بعد أن عرفت **كيفية إضافة صفحة إلى PDF**، **كيفية رسم مستطيل**، **كيفية إضافة شكل إلى PDF**، و**كيفية حفظ PDF إلى ملف**، يمكنك توسيع هذا الأساس:

- إدراج نصوص، صور، أو جداول بجانب الأشكال.  
- استخدام `Graphics` للرسم الحر (خطوط، أقواس، مسارات مخصصة).  
- استكشاف تشفير PDF أو التوقيعات الرقمية إذا كانت الأمان مهمًا.  

كل من هذه المواضيع يبني مباشرةً على الكود الذي تناولناه، لذا اشعر بالثقة في التجربة.

---

**الخلاصة:** لقد تعلمت الآن سير العمل الكامل لـ **create PDF document C#** باستخدام Aspose.Pdf—التهيئة، إضافة صفحة، رسم شكل مستطيل، وحفظ الملف. هذه خطوة أساسية لإنشاء فواتير، تقارير، شهادات، أو أي مستند آلي تحتاجه في الوقت الفعلي. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}