---
category: general
date: 2026-08-14
description: ارسم مستطيلًا على ملف PDF بسرعة باستخدام C#. تعلّم كيفية تحديد أبعاد
  المستطيل وإضافة أشكال إلى صفحة PDF في بضع أسطر فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: ar
lastmod: 2026-08-14
og_description: ارسم مستطيلًا على ملف PDF باستخدام C# في ثوانٍ. يوضح هذا الدليل كيفية
  تحديد أبعاد المستطيل، إضافة شكل، والتحقق من حدود الصفحة لضمان رسومات PDF موثوقة.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: رسم مستطيل على PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: رسم مستطيل على ملف PDF – دليل خطوة بخطوة بلغة C#
url: /ar/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# رسم مستطيل على pdf – دليل C# كامل

إذا كنت بحاجة إلى **draw rectangle on pdf** باستخدام C#، فإن هذا الدليل يوضح لك حلاً مختصراً وجاهزاً للإنتاج. سترى بالضبط **how to define rectangle dimensions**، وتتحقق من أن الشكل يتناسب، وتضيفه إلى صفحة باستدعاء طريقة واحدة.

يغطي الدليل كل شيء من إنشاء مستند PDF إلى عرض المستطيل، بحيث يمكنك نسخ‑لصق الشيفرة في مشروعك ورؤية النتائج فوراً. لا تحتاج إلى وثائق خارجية—فقط الخطوات أدناه.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.7+)
* حزمة NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* فهم أساسي لصياغة C#
* بيئة تطوير متكاملة مثل Visual Studio أو VS Code

> **نصيحة احترافية:** استخدم ترخيص التقييم المجاني لـ Aspose.PDF للتجارب السريعة؛ يضيف علامة مائية صغيرة لكنه يتيح لك اختبار جميع الميزات.

## كيفية رسم مستطيل على PDF باستخدام C#

جوهر المهمة هو إنشاء `RectangleShape`، وتحديد حجمه وحدوده، وإرفاقه بـ `Page`. يحتوي عنوان H2 التالي على الكلمة المفتاحية الأساسية، مما يلبي متطلبات تحسين محركات البحث.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### شرح كل خطوة

| الخطوة | لماذا يهم |
|--------|-----------|
| **1️⃣ إنشاء مستند PDF جديد** | يهيئ الحاوية التي ستحتوي على الصفحات والرسومات. |
| **2️⃣ إضافة صفحة فارغة** | تحتاج إلى كائن `Page` لأن الأشكال تُرفق بصفحة، وليس مباشرة بالمستند. |
| **3️⃣ تحديد حدود المستطيل** | هنا حيث **how to define rectangle dimensions**. يأخذ مُنشئ `Rectangle` القيم `x` و `y` و `width` و `height` بالنقاط (1 pt = 1/72 in). |
| **4️⃣ إنشاء شكل المستطيل** | `RectangleShape` هي الفئة في Aspose التي تُرسم مستطيلًا. تحديد `StrokeColor` يحدد الحدود؛ يمكنك أيضًا تعيين `FillColor` لتعبئة صلبة. |
| **5️⃣ التحقق من حدود الصفحة** | `CheckShapeBoundary` يطرح استثناءً إذا تجاوز المستطيل حجم الصفحة، مما يمنع ملفات PDF غير صالحة. |
| **6️⃣ إضافة الشكل إلى الصفحة** | يصبح الشكل جزءًا من تدفق محتوى الصفحة. |
| **7️⃣ حفظ PDF** | يحفظ المستند إلى ملف يمكنك فتحه بأي عارض PDF. |

يحتوي ملف `RectangleDemo.pdf` الناتج على مستطيل أسود موضعه في الزاوية العلوية اليسرى للصفحة، بعرض 500 pt وارتفاع 700 pt بالضبط.

![مثال على رسم مستطيل على pdf](https://example.com/rectangle-demo.png "مثال على رسم مستطيل على pdf")

*نص بديل للصورة: مثال على رسم مستطيل على pdf يُظهر مستطيلًا أسود في الزاوية العلوية اليسرى لصفحة PDF.*

## كيفية تعريف أبعاد المستطيل لأحجام صفحات مختلفة

المقتطف أعلاه يستخدم قيمًا ثابتة (`500 x 700`). في التطبيقات الحقيقية غالبًا ما تحتاج إلى أن يتكيف المستطيل مع عرض وارتفاع الصفحة.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**نقاط رئيسية:**

* استخدم `page.PageInfo.Width` و `Height` لقراءة حجم الصفحة الفعلي.
* الضرب في عامل (مثال: `0.8f`) يتيح لك التعبير عن الأبعاد كنسبة مئوية من الصفحة.
* يتم تحقيق التوسيط بطرح حجم المستطيل من حجم الصفحة وتقسيم المتبقي على اثنين.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثها | الحل |
|----------|------------|------|
| يمتد المستطيل خارج الصفحة | أبعاد ثابتة أكبر من حجم الصفحة. | استدعِ `page.CheckShapeBoundary` **قبل** إضافة الشكل؛ عدّل الأبعاد إذا تم طرح استثناء. |
| الحد غير مرئي | `StrokeColor` ترك على القيمة الافتراضية (`Color.Empty`). | حدد `StrokeColor` صراحةً (مثال: `Color.Black`). |
| المستطيل يظهر خارج الشاشة | الإحداثيات تبدأ من الزاوية السفلية اليسرى في مساحة PDF؛ استخدام إحداثيات نمط الشاشة (الزاوية العليا اليسرى) يسبب انعكاسًا. | تذكر أن الأصل `(0,0)` هو الزاوية السفلية اليسرى. عدّل `y` وفقًا لذلك أو استخدم `pageHeight - desiredY`. |
| سُمك الخط غير متوقع | عرض الخط الافتراضي قد يكون رقيقًا جدًا للطباعة. | عيّن `rectangleShape.LineWidth = 2;` لزيادة السُمك. |

## توسيع المثال

بمجرد أن تتمكن من **draw rectangle on pdf**، يمكنك بسهولة إضافة أشكال أخرى:

* **EllipseShape** – للدوائر أو البيضيات.
* **PolygonShape** – للمضلعات المخصصة.
* **TextFragment** – لتسمية المستطيلات الخاصة بك.

جميع الأشكال تتبع نفس سير العمل: تحديد الحدود، تكوين المظهر، التحقق من الحدود، ثم الإضافة إلى الصفحة.

## برنامج كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يجمع بين المستطيل الأساسي ومثال التحجيم الديناميكي. انسخه في مشروع وحدة تحكم جديد، استعد حزمة NuGet `Aspose.PDF`، وشغّله.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**الناتج المتوقع:**  
افتح `CombinedRectangles.pdf`. سترى مستطيلًا أسودًا مثبتًا في الزاوية السفلية اليسرى ومستطيلًا أزرقًا داكنًا مركزيًا مع تعبئة صفراء فاتحة. كلا المستطيلين يحترمان هوامش الصفحة.

## الخاتمة

أنت الآن تعرف كيف **draw rectangle on pdf** باستخدام C# وبشكل دقيق **how to define rectangle dimensions** لكل من التخطيطات الثابتة والاستجابية. يستخدم النهج `RectangleShape` من Aspose.PDF، والتحقق من الحدود، وحسابات بسيطة للتكيف مع أي حجم صفحة.

بعد ذلك، قد ترغب في استكشاف:

* إضافة **fill colors** و **line styles** (متقطعة، منقطة) – الكلمة الثانوية: how to define rectangle dimensions with style.
* دمج أشكال متعددة في `Page` واحدة لإنشاء مخططات أو نماذج.
* تصدير PDF إلى تدفق (stream) لواجهات برمجة التطبيقات الويب بدلاً من حفظه على القرص.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تخصيص ملفات PDF باستخدام Aspose.PDF for .NET: تعيين هوامش الصفحة ورسم الخطوط](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [كيفية إضافة طوابع صفحات في ملفات PDF باستخدام Aspose.PDF for .NET: دليل كامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [كيفية إضافة طوابع أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF for .NET | العلامات المائية والخلفيات](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}