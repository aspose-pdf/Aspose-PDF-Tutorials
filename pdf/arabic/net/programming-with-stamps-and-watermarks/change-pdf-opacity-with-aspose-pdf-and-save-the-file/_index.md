---
category: general
date: 2026-11-12
description: تعلم كيفية تغيير شفافية PDF باستخدام Aspose.Pdf، إضافة الشفافية، تعيين
  وضع الدمج، وحفظ PDF المعدل في C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: ar
lastmod: 2026-11-12
og_description: غيّر شفافية ملف PDF باستخدام Aspose.Pdf، وتعلم كيفية إضافة الشفافية،
  وتعيين وضع الدمج، وحفظ ملفات PDF المعدلة في C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: تغيير شفافية PDF باستخدام Aspose.Pdf – إضافة الشفافية وحفظها
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: تغيير شفافية PDF باستخدام Aspose.Pdf وحفظ الملف
url: /ar/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تغيير شفافية PDF باستخدام Aspose.Pdf وحفظ الملف

إذا كنت بحاجة إلى **تغيير شفافية PDF** في مستند، فإن Aspose.Pdf يوفر واجهة برمجة تطبيقات بسيطة لضبط شفافية الخط والملء. يوضح هذا الدليل بالضبط **كيفية إضافة الشفافية**، **كيفية تعيين وضع المزج**، و**حفظ ملفات PDF المعدلة** ببضع أسطر من كود C#.

ستمرّ بكل خطوة — من تحميل ملف PDF موجود إلى تعريف حالة رسومية جديدة وتثبيت التغييرات. في نهاية هذا الدليل يمكنك:

* تقليل وضوح الرسومات المتجهية أو الصور.
* تطبيق وضع مزج مخصص مثل *Normal* أو *Multiply*.
* تصدير الملف المحدث دون فقدان أي محتوى آخر.

المتطلب الوحيد هو بيئة تطوير .NET صالحة وإشارة إلى مكتبة Aspose.Pdf (الإصدار 23.9 أو أحدث). لا تحتاج إلى أدوات خارجية.

## المتطلبات المسبقة

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| .NET 6.0 SDK أو أحدث | يضمن التوافق مع أحدث واجهات Aspose.Pdf. |
| حزمة Aspose.Pdf for .NET عبر NuGet | تزودك بـ `Document`، `CosPdfDictionary`، والفئات ذات الصلة المستخدمة في الكود. |
| ملف PDF لتعديله (مثال: `input.pdf`) | يُستخدم كمصدر لتغييرات الشفافية. |

قم بتثبيت حزمة NuGet باستخدام:

```bash
dotnet add package Aspose.Pdf
```

## تغيير شفافية PDF باستخدام Aspose.Pdf

### الخطوة 1: تحميل مستند PDF

ابدأ بإنشاء كائن `Document` يشير إلى ملف المصدر الخاص بك. يقوم المُنشئ بقراءة ملف PDF بالكامل إلى الذاكرة، مما يسمح لك بالتلاعب بالكائنات الداخلية.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **لماذا هذه الخطوة؟** تحميل الملف يُنشئ نموذج كائن يمكن التلاعب به. جميع التغييرات اللاحقة تُطبق على هذا النموذج في الذاكرة، مما يضمن بقاء الملف الأصلي غير متأثر حتى تقوم بالحفظ صراحةً.

### الخطوة 2: الوصول إلى موارد الصفحة الأولى

كل صفحة PDF تخزن *قاموس الموارد* الذي يحتوي على كائنات مثل الخطوط، الصور، وحالات الرسومات. تحتاج إلى تعديل هذا القاموس لإدخال إدخال `ExtGState` جديد.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **نصيحة:** إذا كان ملف PDF يحتوي على عدة صفحات تحتاج نفس الشفافية، كرّر هذه الخطوة لكل صفحة أو شارك `ExtGState` واحد عبر الصفحات.

### الخطوة 3: التأكد من وجود قاموس ExtGState

قاموس `ExtGState` يحمل حالات رسومية مخصصة. إذا لم يكن موجودًا، ينشئ الكود واحدًا تلقائيًا.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **لماذا هذه الخطوة؟** بدون حاوية `ExtGState`، أي محاولة للإشارة إلى حالة رسومية جديدة ستفشل، مما ينتج PDF يتجاهل إعدادات الشفافية الخاصة بك.

### الخطوة 4: تعريف حالة رسومية جديدة (ExtGState)

حالة الرسومات تُحدد سلوك عمليات الرسم. القاموس التالي يحدد شفافية الخط (`CA`)، شفافية الملء (`ca`)، ووضع المزج (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **كيفية تعيين شفافية الملء:** يتحكم الإدخال `ca` في شفافية الأشكال المملوءة (النص، المسارات). اضبط القيمة الرقمية بين `0` (شفاف تمامًا) و `1` (معتم تمامًا) لتلبية متطلبات التصميم الخاصة بك.

> **كيفية تعيين وضع المزج:** يحدد الإدخال `BM` خوارزمية التركيب. القيم الشائعة تشمل `Normal`، `Multiply`، `Screen`، و `Overlay`. اختر ما يتناسب مع النتيجة البصرية المطلوبة.

### الخطوة 5: تسجيل الحالة الرسومية في قاموس الموارد

امنح الحالة الجديدة اسمًا (مثال: `GS0`) وأضفه إلى قاموس `ExtGState`. سيُشار إلى هذا الاسم لاحقًا في تدفق محتوى الصفحة.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **نصيحة احترافية:** استخدم نظام تسمية مثل `GS0`، `GS1` … عندما تنشئ حالات متعددة. هذا يمنع تصادم الأسماء ويسهل عملية تصحيح الأخطاء.

### الخطوة 6: تطبيق الحالة الرسومية على محتوى الصفحة

لرؤية تأثير الشفافية فعليًا، أدخل المشغل `/GS0 gs` قبل أوامر الرسم التي تريد تعديلها. المثال أدناه يرسم مستطيلًا شبه شفاف.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **لماذا المشغلان `q` و `Q`؟** إنهما يدفعان ويسحبان مكدس الحالة الرسومية، مما يضمن أن تغيير الشفافية يؤثر فقط على المستطيل وليس على باقي الصفحة.

### الخطوة 7: حفظ PDF المعدل

أخيرًا، اكتب المستند المحدث إلى القرص. طريقة `Save` تستبدل الملف الهدف أو تنشئ ملفًا جديدًا إذا لم يكن موجودًا.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **كيفية حفظ PDF المعدل:** استدعاء `Save` يكتب جميع التعديلات في الذاكرة، بما في ذلك `ExtGState` الجديد، إلى المسار المحدد. يمكنك أيضًا بث النتيجة إلى `MemoryStream` للاستجابات الويب.

## مثال كامل يعمل

فيما يلي برنامج واحد مكتمل يحتوي على كل خطوة تم شرحها أعلاه. انسخه إلى تطبيق كونسول وشغّله للتحقق من تغيير الشفافية.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [How to save modified PDF with Aspose.Pdf and add transparency](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [How to add transparency to PDF using Aspose.PDF in C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [How to add graphics state pdf and control transparency with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}