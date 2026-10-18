---
category: general
date: 2026-07-14
description: إضافة الشفافية إلى ملفات PDF باستخدام Aspose.PDF في C#. يوضح هذا الدليل
  كيفية تعديل موارد PDF، وضبط الشفافية، وتحديد أوضاع الدمج بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- edit pdf resources
- aspnet pdf opacity
- c# pdf manipulation
- aspose pdf graphics state
language: ar
lastmod: 2026-07-14
og_description: أضف الشفافية إلى ملفات PDF على الفور. تعلم كيفية تحرير موارد PDF،
  والتحكم في الشفافية وأنماط الدمج باستخدام Aspose.PDF في C#.
og_image_alt: Screenshot showing a PDF page with semi‑transparent shapes after applying
  Aspose.PDF code
og_title: إضافة الشفافية إلى PDF – دليل كامل بلغة C# مع Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Add transparency to PDF using Aspose.PDF in C#. This guide shows how
    to edit PDF resources, set opacity, and define blend modes quickly.
  headline: Add transparency to PDF with Aspose.PDF – Complete C# Guide
  type: TechArticle
- description: Add transparency to PDF using Aspose.PDF in C#. This guide shows how
    to edit PDF resources, set opacity, and define blend modes quickly.
  name: Add transparency to PDF with Aspose.PDF – Complete C# Guide
  steps:
  - name: – Load the source PDF
    text: '```csharp using Aspose.Pdf; using Aspose.Pdf.Collections; using Aspose.Pdf.Devices;'
  - name: – Grab the first page’s resource dictionary
    text: '```csharp var firstPage = pdfDocument.Pages[1]; // PDF pages are 1‑based
      var resourcesEditor = new DictionaryEditor(firstPage.Resources); var extGStateDict
      = resourcesEditor["ExtGState"] .ToCosPdfDictionary(); ```'
  - name: – Build a new graphics state dictionary
    text: '```csharp // Create an empty dictionary that will hold our transparency
      settings var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: – Register the graphics state in the resource dictionary
    text: '```csharp // "GS0" is an arbitrary name; you can choose any identifier
      you like extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: – Apply the graphics state and save
    text: 'At this point the PDF knows about the new graphics state, but you still
      need to tell the page’s content stream to use it. The simplest way is to prepend
      a small snippet that sets the state before any drawing commands:'
  type: HowTo
- questions:
  - answer: Aspose.PDF automatically creates it when you access `resourcesEditor["ExtGState"]`.
      If you encounter a `null`, instantiate a new `CosPdfDictionary` and assign it
      back.
    question: What if the page has no `ExtGState` dictionary yet?
  - answer: Yes. Define `GS1`, `GS2`, … with distinct `ca`/`CA` values and switch
      between them in the content stream (`/GS1 gs`, `/GS2 gs`).
    question: Can I set different opacities for multiple objects?
  - answer: You must provide the password when constructing `new Document(inputPath,
      password)`. After decryption, the same resource‑editing steps apply.
    question: Will this work on encrypted PDFs?
  - answer: PDF names are case‑sensitive, so use the exact spelling (`Normal`, `Multiply`,
      `Screen`, etc.) as defined in the PDF spec.
    question: Is the blend mode case‑sensitive?
  type: FAQPage
tags:
- PDF
- C#
- Aspose.PDF
- Transparency
title: إضافة الشفافية إلى ملفات PDF باستخدام Aspose.PDF – دليل C# الكامل
url: /ar/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة شفافية إلى PDF باستخدام Aspose.PDF – دليل C# كامل

هل تساءلت يومًا كيف **تضيف شفافية إلى ملفات PDF** دون الحاجة إلى محرر رسومات ثقيل؟ لست وحدك. يحتاج العديد من المطورين إلى تعديل ملفات PDF بسرعة—مثل العلامات المائية، الرسومات المتراكبة، أو التظليل الخفيف—وأبسط طريقة هي تعديل موارد PDF الأساسية مباشرة.

في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية **يضيف شفافية إلى PDF** باستخدام Aspose.PDF for .NET. بنهاية الدرس ستعرف بالضبط كيف **تعدل موارد PDF**، وتضبط شفافية الخط والملء، وتختار وضع المزج الذي يتوافق مع أهداف التصميم الخاصة بك.

## ما ستتعلمه

- كيفية تحميل ملف PDF موجود باستخدام Aspose.PDF.
- آلية عمل مدخل **ExtGState** داخل قاموس موارد الصفحة.
- كيفية إنشاء قاموس حالة رسومية يحدد الشفافية (`CA`/`ca`) ووضع المزج (`BM`).
- حفظ المستند المعدل لتفعيل الشفافية.
- الأخطاء الشائعة عند العمل مع موارد PDF وكيفية تجنبها.

*المتطلبات المسبقة:* .NET 6+ (أو .NET Framework 4.6+)، رخصة أو نسخة تجريبية من Aspose.PDF، وبيئة تطوير C# أساسية (Visual Studio، Rider، أو VS Code). لا تحتاج إلى معرفة مسبقة بداخلية PDF—فقط اتبع الخطوات.

![Add transparency to PDF example](https://example.com/og-image.png){alt="لقطة شاشة تُظهر صفحة PDF بأشكال شبه شفافة بعد تطبيق كود Aspose.PDF"}

## إضافة شفافية إلى PDF – نظرة عامة

قبل أن نغوص في الكود، دعونا نوضح ما يعنيه “إضافة شفافية” في عالم PDF. تخزن ملفات PDF تعليمات الرسم في *تدفقات المحتوى*. تلك التدفقات تشير إلى كائنات **حالة الرسومات** التي تتحكم في كيفية عرض الأشكال. مفتاحان أساسيان:

| المفتاح | المعنى |
|-----|---------|
| `CA` | شفافية الخط (1 = معتم بالكامل، 0 = شفاف) |
| `ca` | شفافية الملء (نفس المقياس) |
| `BM` | وضع المزج (مثل `Normal`، `Multiply`) |

عند إنشاء مدخل **ExtGState** جديد وتوجيه أوامر الرسم إليه، يرث كل شكل لاحق الشفافية المحددة. الفكرة هي **تعديل موارد PDF**—وبشكل محدد قاموس `ExtGState`—حتى يتعرف محرك PDF على الحالة المخصصة الخاصة بك.

## تعديل موارد PDF باستخدام Aspose.PDF

يُجرد Aspose.PDF بنية PDF منخفضة المستوى خلف واجهة برمجة تطبيقات سهلة، لكن لا يزال بإمكانك الوصول إلى قواميس الموارد عندما تحتاج إلى تحكم دقيق. المقتطف البرمجي أدناه يفعل ذلك بالضبط: يقوم بتحميل PDF، إنشاء قاموس حالة رسومية جديد، وإدراجه في موارد الصفحة الأولى.

### الخطوة 1 – تحميل ملف PDF المصدر

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Devices;

// Adjust these paths to point at your actual files
string inputPath  = "YOUR_DIRECTORY/input.pdf";
string outputPath = "YOUR_DIRECTORY/output.pdf";

using (var pdfDocument = new Document(inputPath))
{
    // The rest of the steps go here
}
```

*لماذا هذا مهم:* فئة `Document` هي نقطة الدخول لـ **تعديل موارد PDF**. باستخدام كتلة `using` نضمن تحرير مقبض الملف بسرعة—نصيحة أداء صغيرة لكنها مهمة.

### الخطوة 2 – الحصول على قاموس موارد الصفحة الأولى

```csharp
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
var extGStateDict = resourcesEditor["ExtGState"]
                    .ToCosPdfDictionary();
```

*شرح:* كل صفحة لديها قاموس `/Resources` يجمع الخطوط، الصور، وحالات الرسومات. يتيح لنا `DictionaryEditor` التعامل مع تلك المجموعة كقائمة .NET عادية، مما يجعل جلب القاموس الفرعي `ExtGState` سهلًا.

### الخطوة 3 – بناء قاموس حالة رسومية جديد

```csharp
// Create an empty dictionary that will hold our transparency settings
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the entries we care about
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),    // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*لماذا نضيف هذه المفاتيح:*  
- `CA = 1` يحافظ على حدود الأشكال صلبة، وهو مفيد للحدود.  
- `ca = 0.5` يجعل الداخل شبه شفاف، وهو تأثير العلامة المائية الكلاسيكي.  
- `BM = Normal` هو وضع المزج الافتراضي؛ يمكنك استبداله بـ `Multiply` أو `Screen` إذا احتجت إلى تأثيرات فنية.

### الخطوة 4 – تسجيل حالة الرسومات في قاموس الموارد

```csharp
// "GS0" is an arbitrary name; you can choose any identifier you like
extGStateDict.Add("GS0", graphicsStateDict);
```

*نصيحة:* إذا كنت تخطط لإضافة كائنات شفافة متعددة، أعط كل واحدة اسمًا فريدًا (`GS1`، `GS2`، …) وأشر إلى المناسب في تدفق المحتوى.

### الخطوة 5 – تطبيق حالة الرسومات وحفظ الملف

في هذه المرحلة يعرف PDF حالة الرسومات الجديدة، لكن لا يزال عليك إخبار تدفق محتوى الصفحة باستخدامها. أبسط طريقة هي إضافة مقطع صغير في البداية يحدد الحالة قبل أي أوامر رسم:

```csharp
// Insert a small content stream that selects our graphics state
var content = "q\n/GS0 gs\n"; // 'q' saves graphics state, '/GS0 gs' sets it
firstPage.Contents.Insert(0, new MemoryStream(System.Text.Encoding.ASCII.GetBytes(content)));
```

الآن يمكننا حفظ الملف المعدل بأمان:

```csharp
pdfDocument.Save(outputPath);
```

**مثال كامل يعمل**

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Devices;
using System.Collections.Generic;
using System.IO;

string inputPath  = "YOUR_DIRECTORY/input.pdf";
string outputPath = "YOUR_DIRECTORY/output.pdf";

using (var pdfDocument = new Document(inputPath))
{
    // Access first page resources
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"]
                        .ToCosPdfDictionary();

    // Build new graphics state
    var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };
    foreach (var entry in graphicsStateEntries)
        graphicsStateDict.Add(entry);

    // Add to ExtGState dictionary
    extGStateDict.Add("GS0", graphicsStateDict);

    // Prepend content that selects the new graphics state
    var prepend = "q\n/GS0 gs\n";
    firstPage.Contents.Insert(0, new MemoryStream(System.Text.Encoding.ASCII.GetBytes(prepend)));

    // Save the result
    pdfDocument.Save(outputPath);
}
```

#### النتيجة المتوقعة

افتح `output.pdf` في أي عارض (Adobe Reader، Foxit، إلخ). أي شكل يُرسم بعد أوامر `q /GS0 gs`—مثل مستطيل قد تضيفه لاحقًا—سيظهر بـ **شفافية ملء 50 %** بينما يبقى حدّه معتمًا بالكامل. إذا أضفت أوامر رسم إضافية لاحقًا في تدفق المحتوى، فستورث نفس الشفافية حتى يُواجه `Q` (استعادة حالة الرسومات).

## أسئلة شائعة وحالات خاصة

- **ماذا لو لم توجد بعد قاموس `ExtGState` في الصفحة؟**  
  يقوم Aspose.PDF بإنشائه تلقائيًا عندما تصل إلى `resourcesEditor["ExtGState"]`. إذا صادفت `null`، أنشئ `CosPdfDictionary` جديدًا وعينه مرة أخرى.

- **هل يمكن ضبط شفافية مختلفة لعدة كائنات؟**  
  نعم. عرّف `GS1`، `GS2`، … بقيم `ca`/`CA` مختلفة وتبديل بينها في تدفق المحتوى (`/GS1 gs`، `/GS2 gs`).

- **هل سيعمل هذا على ملفات PDF مشفرة؟**  
  يجب توفير كلمة المرور عند إنشاء `new Document(inputPath, password)`. بعد فك التشفير، تُطبق نفس خطوات تعديل الموارد.

- **هل وضع المزج حساس لحالة الأحرف؟**  
  أسماء PDF حساسة لحالة الأحرف، لذا استخدم التهجئة الدقيقة (`Normal`، `Multiply`، `Screen`، إلخ) كما هو معرف في مواصفات PDF.

- **نصيحة أداء:** إذا كنت تعالج مئات الصفحات، عدل قاموس الموارد مرة واحدة لكل مستند وأعد استخدام نفس حالة الرسومات عبر الصفحات. هذا يقلل من استهلاك الذاكرة ويحافظ على حجم الملف أصغر.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET&#58; Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}