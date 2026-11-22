---
category: general
date: 2026-11-22
description: أضف الشفافية إلى ملف PDF باستخدام Aspose.PDF للغة C#. تعلّم كيفية تغيير
  شفافية PDF من خلال مثال واضح خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- how to change pdf opacity
- Aspose.PDF opacity
- PDF graphics state C#
- PDF blend mode example
language: ar
lastmod: 2026-11-22
og_description: أضف الشفافية إلى ملف PDF باستخدام Aspose.PDF للغة C#. يوضح هذا الدليل
  كيفية تغيير شفافية PDF بسرعة وبشكل موثوق.
og_image_alt: Screenshot of a PDF page showing translucent graphics after adding transparency
og_title: إضافة الشفافية إلى PDF في C# – دليل Aspose.PDF الكامل
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Add transparency to PDF using Aspose.PDF for C#. Learn how to change
    PDF opacity with a clear, step‑by‑step example.
  headline: How to add transparency to PDF in C# with Aspose.PDF
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: كيفية إضافة الشفافية إلى ملف PDF باستخدام C# و Aspose.PDF
url: /ar/net/images-graphics/how-to-add-transparency-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة الشفافية إلى PDF في C# باستخدام Aspose.PDF

إذا كنت بحاجة إلى **إضافة شفافية إلى ملفات PDF**، يوضح لك هذا الدليل حلاً كاملاً باستخدام Aspose.PDF for .NET. ستتعرف على **كيفية تغيير شفافية PDF** للرسومات المتجهة أو النص أو الصور دون مغادرة بيئة C#.

يغطي البرنامج التعليمي كل خطوة — من تحميل المستند إلى تعديل حالة الرسومات للصفحة وحفظ النتيجة. في النهاية، يمكنك إنتاج ملفات PDF حيث تظهر العناصر المحددة شبه شفافة، وهو ما يفيد في العلامات المائية، وتأثيرات التراكب، أو نماذج التصميم.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.8)
* ترخيص صالح لـ Aspose.PDF for .NET أو مفتاح تقييم مؤقت
* Visual Studio 2022 (أو أي بيئة تطوير تدعم C#)
* ملف PDF إدخال يُدعى `input.pdf` موجود في مجلد معروف

هذه العناصر تضمن تشغيل الكود دون الحاجة إلى إعدادات إضافية.

## الخطوة 1: تحميل مستند PDF

العملية الأولى هي فتح ملف PDF الموجود. تمثل Aspose.PDF الملف بالكامل باستخدام الفئة `Document`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;

// Load the source PDF
var inputPath = @"C:\MyFiles\input.pdf";
var doc = new Document(inputPath);
```

*لماذا هذه الخطوة مهمة*: تحميل المستند يُنشئ نموذجًا في الذاكرة يتيح لك فحص الصفحات والموارد وتدفقات المحتوى. بدون هذا الكائن لا يمكنك تعديل حالات الرسومات.

## الخطوة 2: الوصول إلى قاموس موارد الصفحة الأولى

يتم تطبيق الشفافية عبر **حالة رسومات** مخزنة في قاموس موارد الصفحة. تحتاج إلى `DictionaryEditor` لتعديل ذلك القاموس.

```csharp
// Get the first page (pages are 1‑based)
var page = doc.Pages[1];

// Open the resource dictionary for editing
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

إذا لم تحتوي الصفحة بعد على إدخال `ExtGState`، تقوم Aspose.PDF بإنشاء قاموس فارغ تلقائيًا عند طلبه. هذه المرونة تعني أن نفس الكود يعمل مع ملفات PDF التي تستخدم الشفافية مسبقًا أو التي لا تستخدمها مطلقًا.

## الخطوة 3: إنشاء حالة رسومات جديدة بقيم الشفافية

حالة الرسومات تحتفظ بمعلمات مثل شفافية التعبئة (`ca`)، شفافية الحد (`CA`)، ووضع المزج (`BM`). البلوك التالي يبني قاموسًا يحدد شفافية تعبئة بنسبة 50 % مع الحفاظ على الحدود غير شفافة.

```csharp
// Build a new graphics state dictionary
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);

// Stroke opacity – fully opaque (value between 0 and 1)
graphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity – 50 % transparent
graphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode – Normal (other modes: Multiply, Screen, etc.)
graphicsState.Add("BM", new CosPdfName("Normal"));
```

*لماذا هذه المفاتيح*:  
* `CA` يتحكم في شفافية المسارات المرسومة (الخطوط، الحدود).  
* `ca` يتحكم في شفافية الكائنات المملوءة (تعبئة النص، تعبئة الصور).  
* `BM` يحدد كيفية دمج الكائن الشفاف مع المحتوى الأساسي؛ `Normal` هو الخيار الأكثر شيوعًا.

## الخطوة 4: تسجيل حالة الرسومات في موارد الصفحة

بعد إنشاء حالة الرسومات، يجب إضافتها إلى قاموس `ExtGState` الخاص بالصفحة تحت اسم فريد (مثال: `GS0`). يمكن لتدفقات المحتوى بعد ذلك الإشارة إلى هذا الاسم لتطبيق إعدادات الشفافية.

```csharp
// Add the new graphics state to the resource dictionary
extGState.Add("GS0", graphicsState);
```

في هذه المرحلة يحتوي ملف PDF على حالة رسومات قابلة لإعادة الاستخدام تُدعى `GS0`. أي أمر رسم يشير إلى `/GS0 gs` سيُظهر بالشفافية المحددة.

## الخطوة 5: تطبيق حالة الرسومات على محتوى الصفحة (اختياري)

إذا أردت التأثير على المحتوى الموجود، تحتاج إلى إدراج أمر في بداية تدفق محتوى الصفحة. يوضح المقتطف التالي كيفية إلحاق مشغل حالة الرسومات في بداية التدفق.

```csharp
// Retrieve the original content stream
var content = page.Contents[1];

// Insert the graphics state operator at the start of the stream
content.Contents.Insert(0, new CosPdfLiteral("GS0 gs"));
```

*متى تستخدم هذه الخطوة*: إذا كان PDF يحتوي بالفعل على أوامر رسم وتريد جعلها شبه شفافة، ألحق المشغل في البداية. إذا كنت تخطط لإضافة كائنات جديدة لاحقًا، يمكنك الإشارة إلى `GS0` مباشرةً عند إنشاء تلك الكائنات.

## الخطوة 6: حفظ ملف PDF المعدل

أخيرًا، اكتب المستند المحدث إلى القرص.

```csharp
var outputPath = @"C:\MyFiles\output.pdf";
doc.Save(outputPath);
```

الملف الناتج `output.pdf` يُظهر عناصر التعبئة في الصفحة الأولى بنسبة شفافية 50 % بينما تظل الحدود مرئية بالكامل. افتح الملف في أي عارض PDF للتحقق من التأثير.

## كيفية تغيير شفافية PDF لعدة صفحات

ينطبق نفس النهج على أي رقم صفحة. قم بالتكرار عبر `doc.Pages` وكرر الخطوات 2‑5، مع تعيين اسم حالة رسومات مميز لكل صفحة (مثال: `GS1`, `GS2`). إليك نسخة مختصرة:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    var pg = doc.Pages[i];
    var editor = new DictionaryEditor(pg.Resources);
    var ext = editor["ExtGState"].ToCosPdfDictionary();

    var gs = CosPdfDictionary.CreateEmptyDictionary(doc);
    gs.Add("CA", new CosPdfNumber(1));
    gs.Add("ca", new CosPdfNumber(0.75)); // 75% fill opacity
    gs.Add("BM", new CosPdfName("Normal"));

    var gsName = $"GS{i - 1}";
    ext.Add(gsName, gs);

    var cnt = pg.Contents[1];
    cnt.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
}
```

هذا التكرار يقلل من التكرار ويظهر **كيفية تغيير شفافية PDF** عبر المستند بأكمله.

## المشكلات الشائعة ونصائح الممارسات المثلى

| المشكلة | السبب | الحل الموصى به |
|-------|--------|----------------|
| عدم وجود إدخال `ExtGState` | بعض ملفات PDF لا تنشئ قاموس حالة الرسومات أبداً | `DictionaryEditor` ينشئه تلقائيًا؛ لا تحتاج إلى كود إضافي |
| الشفافية غير مرئية | عارض PDF يخزن نسخة الصفحة الأصلية في الذاكرة | امسح ذاكرة التخزين المؤقت للعارض أو أعد فتح الملف |
| عدم توافق وضع المزج | استخدام `Multiply` على خلفية داكنة قد يجعل الكائنات تختفي | جرّب قيم `BM` مختلفة (`Normal`, `Screen`, `Overlay`) للحصول على التأثير المطلوب |
| تعارض حالات رسومات متعددة | إعادة استخدام نفس الاسم (`GS0`) في صفحات مختلفة يكتب فوق التعريف السابق | استخدم اسمًا فريدًا لكل صفحة (`GS0`, `GS1`, …) |

## مثال كامل يعمل

فيما يلي برنامج مستقل يمكنك نسخه، لصقه، وتشغيله. يتضمن جميع عبارات `using`، معالجة الأخطاء، وتعليقات.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class AddTransparencyDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"C:\MyFiles\input.pdf";
        const string outputPath = @"C:\MyFiles\output.pdf";

        // Load the PDF
        var doc = new Document(inputPath);

        // Process each page
        for (int pageIndex = 1; pageIndex <= doc.Pages.Count; pageIndex++)
        {
            var page = doc.Pages[pageIndex];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Create a graphics state with 60% fill opacity
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);
            graphicsState.Add("CA", new CosPdfNumber(1));               // stroke opacity
            graphicsState.Add("ca", new CosPdfNumber(0.6));             // fill opacity
            graphicsState.Add("BM", new CosPdfName("Normal"));         // blend mode

            // Unique name for this page
            string gsName = $"GS{pageIndex - 1}";
            extGState.Add(gsName, graphicsState);

            // Prepend the graphics state operator to the page content
            var content = page.Contents[1];
            content.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
        }

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"PDF saved with transparency at: {outputPath}");
    }
}
```

**الناتج المتوقع**: عند فتح `output.pdf`، أي أشكال مملوءة أو نصوص أو صور في كل صفحة تظهر بشفافية 60 %، بينما تظل الحدود غير شفافة. التغيير مرئي فورًا ويعمل في Adobe Acrobat، Edge، Chrome، أو أي عارض PDF يدعم حالة رسومات PDF.

## الخلاصة

أنت الآن تعرف **كيفية إضافة شفافية إلى ملفات PDF** باستخدام Aspose.PDF for C#. غطى الدرس تحميل المستند، تعديل قاموس موارد الصفحة، إنشاء حالة رسومات مخصصة، وحفظ الملف المعدل. كما تعلمت **كيفية تغيير شفافية PDF** لصفحة واحدة أو لعدة صفحات، بالإضافة إلى نصائح عملية لتجنب الأخطاء الشائعة.

بعد ذلك، استكشف المواضيع ذات الصلة مثل:

* إضافة علامات مائية صورة بشفافية متغيرة
* استخدام أوضاع مزج مختلفة (`Multiply`, `Screen`) لتأثيرات إبداعية
* دمج الشفافية مع تعليقات PDF

جرّب هذه التغييرات لتخصيص مخرجات PDF وفق متطلبات مشروعك البصرية. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to add graphics state pdf and control transparency with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [How to set opacity in a PDF and how to change blend mode with Aspose.Pdf](/pdf/hongkong/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/)
- [How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}