---
category: general
date: 2026-09-27
description: تعلم كيفية إضافة مستطيل إلى ملف PDF باستخدام C# أثناء تحميل مستند PDF
  بـ C# والوصول إلى الصفحة الأولى من PDF باستخدام Aspose.Pdf.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- access first page pdf
- load pdf document c#
- add graphics pdf c#
language: ar
lastmod: 2026-09-27
og_description: أضف مستطيلًا إلى PDF في C# عن طريق تحميل مستند PDF في C# والوصول إلى
  الصفحة الأولى من PDF. اتبع هذا الدليل خطوة بخطوة للحصول على نتائج موثوقة.
og_image_alt: Code editor showing how to add rectangle to PDF using C#
og_title: إضافة مستطيل إلى PDF في C# – دليل Aspose.Pdf الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to add rectangle to PDF in C# while you load PDF document
    C# and access first page PDF with Aspose.Pdf.
  headline: How to add rectangle to PDF in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: كيفية إضافة مستطيل إلى PDF في C# باستخدام Aspose.Pdf
url: /ar/net/images-graphics/how-to-add-rectangle-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة مستطيل إلى PDF في C# باستخدام Aspose.Pdf

إذا كنت بحاجة إلى **add rectangle to PDF** في تطبيق C#، فإن هذا الدليل يوضح الخطوات الدقيقة. ستقوم بتحميل مستند PDF، الوصول إلى الصفحة الأولى، إنشاء شكل مستطيل، وكتابة التغييرات مرة أخرى إلى القرص. الحل يعمل مع Aspose.Pdf .NET 2024‑R2 ولا يتطلب أدوات خارجية.

إضافة مستطيل إلى ملفات PDF هو طلب شائع لتسليط الضوء على الأقسام، إنشاء طبقات تشبه النماذج، أو بناء رسومات بسيطة. باتباع الشيفرة أدناه ستحصل على نمط قابل لإعادة الاستخدام يمكنك توسيعه بأشكال أخرى، ألوان، أو إعدادات الشفافية.

## ما ستتعلمه

* كيفية **load PDF document C#** باستخدام Aspose.Pdf.
* كيفية **access first page PDF** بأمان.
* كيفية إنشاء مستطيل و **add rectangle to PDF**.
* كيفية التحقق من أن المستطيل يتناسب داخل حدود الصفحة.
* كيفية حفظ الملف المحدث دون فقدان المحتوى الموجود.

يفترض الدليل أنك تمتلك بيئة تطوير C# أساسية (Visual Studio 2022 أو أحدث) ورخصة Aspose.Pdf صالحة. لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf`.

## الخطوة 1: Load PDF document C#  

تحميل ملف المصدر هو العملية الأولى. Aspose.Pdf يقرأ ملف PDF بالكامل إلى الذاكرة، مما يتيح لك تعديل الصفحات، التعليقات التوضيحية، والرسومات.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // for Color

// Load the PDF document
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

*لماذا هذه الخطوة مهمة* – كائن `Document` يمثل ملف PDF بالكامل. إذا تعذر فتح الملف، يتم رمي استثناء، لذا يجب التحقق من المسار قبل استدعاء المُنشئ في كود الإنتاج.

## الخطوة 2: Access first page PDF  

الصفحات في Aspose.Pdf تُرقم بدءًا من 1، لذا يتم استرجاع الصفحة الأولى باستخدام الفهرس 1. تُظهر هذه الخطوة العبارة الدقيقة **access first page PDF**.

```csharp
// Access the first page (pages are 1‑based)
Page page = doc.Pages[1];
```

*لماذا هذه الخطوة مهمة* – تعديل الصفحة الصحيحة يمنع التعديلات غير المقصودة على الصفحات اللاحقة. إذا كان PDF لا يحتوي على صفحات، فإن `doc.Pages[1]` يرفع استثناء `ArgumentOutOfRangeException`، والذي يمكنك التقاطه لتوفير رسالة خطأ ودية.

## الخطوة 3: Create the rectangle shape  

الآن تقوم بتعريف هندسة المستطيل الذي تريد إضافته. معلمات المُنشئ هي `(x, y, width, height)` حيث الأصل `(0,0)` هو الزاوية السفلية اليسرى للصفحة.

```csharp
// Define a rectangle shape (x, y, width, height)
Rectangle rect = new Rectangle(10, 10, 200, 200);

// Optional: customize the appearance
rect.GraphInfo = new GraphInfo
{
    Color = Color.Black,   // stroke color
    LineWidth = 2          // thickness in points
};
```

*لماذا هذه الخطوة مهمة* – ضبط `GraphInfo` يتحكم في كيفية عرض المستطيل. بدون ذلك، سيكون الشكل غير مرئي لأن الحد الافتراضي شفاف.

## الخطوة 4: Verify the rectangle fits within the page boundaries  

قبل إضافة الشكل، يجب التأكد من أنه لا يتجاوز حجم الصفحة. هذا يمنع حدوث عيوب في العرض ويحافظ على توافق ملف PDF مع المواصفات.

```csharp
// Verify the rectangle fits within the page boundaries
if (page.Rect.Contains(rect))
{
    // Step 5 will run here
}
else
{
    // Adjust rectangle or log a warning
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*لماذا هذه الخطوة مهمة* – فحص `Contains` يضمن أن المستطيل داخل المنطقة القابلة للطباعة بالكامل. إذا تخطيت هذه الخطوة وتجاوز المستطيل الحدود، قد تقوم بعض العارضات بقطع الشكل أو الإبلاغ عن أخطاء.

## الخطوة 5: Add rectangle to PDF  

عند نجاح فحص الحدود، تقوم بإضافة المستطيل إلى الصفحة. هذا هو الإجراء الأساسي الذي يحقق متطلب **add rectangle to PDF**.

```csharp
// Add the rectangle to the page
page.Add(rect);
```

*لماذا هذه الخطوة مهمة* – `page.Add` يدرج الشكل في تدفق محتوى الصفحة. يصبح المستطيل جزءًا من الطبقة البصرية وسيظهر في أي عارض PDF.

## الخطوة 6: Save the updated PDF  

أخيرًا، اكتب المستند المعدل مرة أخرى إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد.

```csharp
// Save the updated PDF
doc.Save("YOUR_DIRECTORY/output.pdf");
```

*لماذا هذه الخطوة مهمة* – الحفظ يُنهي جميع التغييرات. إذا كنت بحاجة إلى الحفاظ على الأصل، اختر مسار إخراج مختلف كما هو موضح.

## مثال كامل قابل للتنفيذ

فيما يلي برنامج وحدة تحكم مستقل يدمج كل خطوة. انسخ الشيفرة إلى مشروع C# جديد، عدل مسارات الملفات، وشغّله.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;

class AddRectangleExample
{
    static void Main()
    {
        // Load the PDF document (load pdf document c#)
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // Access first page PDF
        Page page = doc.Pages[1];

        // Create a rectangle shape
        Rectangle rect = new Rectangle(10, 10, 200, 200);
        rect.GraphInfo = new GraphInfo
        {
            Color = Color.Black,
            LineWidth = 2
        };

        // Verify bounds before adding
        if (page.Rect.Contains(rect))
        {
            // Add rectangle to PDF
            page.Add(rect);
        }
        else
        {
            System.Console.WriteLine("Rectangle does not fit on the page.");
            return;
        }

        // Save the result
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Rectangle added successfully.");
    }
}
```

**الناتج المتوقع** – بعد التنفيذ، يحتوي `output.pdf` على المحتوى الأصلي بالإضافة إلى مستطيل بحدود سوداء موضعه 10 pt من الزاوية السفلية اليسرى. فتح الملف في Adobe Acrobat أو أي عارض PDF يظهر طبقة المستطيل على الصفحة الأولى.

## التعامل مع الاختلافات الشائعة

| الحالة | التغيير الموصى به |
|-----------|--------------------|
| حجم الصفحة مختلف (مثال: A4 مقابل Letter) | استخدم `page.Rect.Width` و `page.Rect.Height` لحساب مستطيل يتناسب بشكل ديناميكي. |
| تحتاج إلى مستطيل مملوء | اضبط `rect.GraphInfo.FillColor = Color.LightGray;` واختياريًا `rect.GraphInfo.IsFilled = true;`. |
| تتطلب صفحات متعددة نفس المستطيل | قم بالتكرار على `doc.Pages` وكرر عملية الإضافة لكل صفحة. |
| الشفافية مطلوبة | اضبط `rect.GraphInfo.Transparency = 0.5;` (النطاق 0–1). |

هذه الاختلافات توضح كيف أن نهج **add graphics pdf c#** يتوسع إلى ما بعد شكل واحد.

## نصائح احترافية

* **نصيحة الأداء** – عند معالجة ملفات PDF الكبيرة، أعد استخدام نسخة واحدة من كائن `Document` وتجنب استدعاء `Save` داخل حلقة. احفظ مرة واحدة بعد معالجة جميع الصفحات.
* **معالجة الأخطاء** – قم بلف التدفق بالكامل داخل كتلة `try/catch` لالتقاط `FileNotFoundException`، `InvalidOperationException`، و `PdfException` الخاصة بـ Aspose.
* **الرخصة** – سجّل رخصة Aspose.Pdf الخاصة بك قبل إنشاء كائن `Document` لتجنب علامة التقييم المائية.

## الخلاصة

أنت الآن تعرف كيفية **add rectangle to PDF** في C# عن طريق تحميل a

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند PDF في C# – إضافة صفحة إلى PDF ومستطيل](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/)
- [إنشاء مستند PDF C# – إضافة صفحة فارغة ورسم مستطيل](/pdf/english/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/)
- [إنشاء مستند PDF C# – إضافة صفحة، رسم مستطيل وحفظ](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}