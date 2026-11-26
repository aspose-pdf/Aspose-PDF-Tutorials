---
category: general
date: 2026-11-25
description: إضافة حقل نص إلى ملف PDF باستخدام Aspose.PDF في C#. تعلم كيفية تحميل
  مستند PDF، وتطبيق وضع الدمج، وضبط شفافية التعبئة، وحفظ ملف PDF المعدل بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add text field pdf
- load pdf document
- save modified pdf
- apply blend mode
- set fill opacity
language: ar
lastmod: 2026-11-25
og_description: إضافة حقل نص إلى PDF باستخدام Aspose.PDF في C#. يوضح هذا الدليل كيفية
  تحميل مستند PDF، وتطبيق وضع المزج، وتعيين شفافية التعبئة، وحفظ PDF المعدل.
og_image_alt: C# code snippet that adds a text field to a PDF and configures blend
  mode and opacity
og_title: إضافة حقل نصي إلى PDF باستخدام Aspose.PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Add text field PDF using Aspose.PDF in C#. Learn to load pdf document,
    apply blend mode, set fill opacity, and save modified pdf efficiently.
  headline: How to add text field PDF with Aspose.PDF in C#
  type: TechArticle
- description: Add text field PDF using Aspose.PDF in C#. Learn to load pdf document,
    apply blend mode, set fill opacity, and save modified pdf efficiently.
  name: How to add text field PDF with Aspose.PDF in C#
  steps:
  - name: '**Load the source PDF** (`load pdf document`).'
    text: '**Load the source PDF** (`load pdf document`).'
  - name: (Optional) Convert the file to a PDF/X‑4 standard if your downstream workflow
      requires it.
    text: (Optional) Convert the file to a PDF/X‑4 standard if your downstream workflow
      requires it.
  - name: Retrieve any existing signature names—useful when you need to preserve digital
      signatures.
    text: Retrieve any existing signature names—useful when you need to preserve digital
      signatures.
  - name: Create a **multi‑widget `TextBoxField`** and place it on the first page.
    text: Create a **multi‑widget `TextBoxField`** and place it on the first page.
  - name: '**Apply blend mode** and **set fill opacity** by editing the page’s resource
      dictionary.'
    text: '**Apply blend mode** and **set fill opacity** by editing the page’s resource
      dictionary.'
  - name: '**Save the modified PDF** (`save modified pdf`) to a new file.'
    text: '**Save the modified PDF** (`save modified pdf`) to a new file.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: كيفية إضافة حقل نص إلى PDF باستخدام Aspose.PDF في C#
url: /ar/net/programming-with-forms/how-to-add-text-field-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة حقل نصي PDF باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **إضافة حقل نصي PDF** برمجيًا، فإن هذا الدليل يشرح لك العملية بالكامل باستخدام Aspose.PDF لـ .NET. ستتعرف على كيفية **تحميل مستند pdf**، تكوين صندوق نص متعدد الودجات، **تطبيق وضع المزج**، **تعيين شفافية التعبئة**، وأخيرًا **حفظ pdf المعدل** مع الحفاظ على الحقل الجديد.

التعامل مع ملفات PDF غالبًا ما يتطلب التعامل مع التوقيعات، قواميس الموارد، ومعايير PDF. يغطي هذا الشرح تلك الجوانب، بحيث تحصل على ملف نظيف ومتوافق مع المعايير ويتصرف تمامًا كما تتوقع.

## ما ستحققه

* فتح ملف PDF موجود (`load pdf document`) بأمان.
* إدراج `TextBoxField` متعدد الودجات في الصفحة الأولى.
* إضافة إدخال ExtGState مخصص للتحكم في الشفافية ووضع المزج (`apply blend mode`, `set fill opacity`).
* حفظ التغييرات باستخدام `save modified pdf` إلى موقع جديد.

لا توجد أدوات خارجية مطلوبة—فقط حزمة Aspose.PDF NuGet وبيئة تشغيل .NET 6+.

## المتطلبات المسبقة

* Visual Studio 2022 أو أي بيئة تطوير C#.
* .NET 6 SDK (أو أحدث).
* Aspose.PDF لـ .NET (التثبيت عبر `dotnet add package Aspose.PDF`).
* ملف PDF مصدر باسم `source.pdf` موجود في مجلد يمكنك الإشارة إليه من الشيفرة.

---

## إضافة حقل نصي PDF – سير العمل العام

الخطوات العامة التالية تتطابق مباشرةً مع مثال الشيفرة الذي ستراه لاحقًا:

1. **تحميل ملف PDF المصدر** (`load pdf document`).
2. (اختياري) تحويل الملف إلى معيار PDF/X‑4 إذا كان سير العمل اللاحق يتطلب ذلك.
3. استرجاع أي أسماء توقيعات موجودة—مفيد عندما تحتاج إلى الحفاظ على التوقيعات الرقمية.
4. إنشاء **`TextBoxField` متعدد الودجات** ووضعه في الصفحة الأولى.
5. **تطبيق وضع المزج** و**تعيين شفافية التعبئة** عن طريق تعديل قاموس موارد الصفحة.
6. **حفظ PDF المعدل** (`save modified pdf`) إلى ملف جديد.

يتم شرح كل خطوة بالتفصيل أدناه.

## الخطوة 1: تحميل مستند PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using Aspose.Pdf.Xmp;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;
using System.Drawing;

// Load the source PDF document
var pdfPath = @"YOUR_DIRECTORY\source.pdf";
var pdfDocument = new Document(pdfPath);
```

**لماذا هذا مهم:** `Document` هو نقطة الدخول لكل عملية في Aspose.PDF. بتحميل الملف أولاً، تحصل على إمكانية الوصول إلى الصفحات، التوقيعات، وقواميس الموارد. إذا تعذر فتح الملف، يتم إلقاء استثناء يمكنك التقاطه لتقديم رسالة خطأ صديقة للمستخدم.

## الخطوة 2: (اختياري) التحويل إلى PDF/X‑4

```csharp
var conversionOptions = new PdfFormatConversionOptions
{
    PdfStandard = PdfStandard.PdfX4   // PDF/X‑4 ensures proper color management
};
pdfDocument.Save(@"YOUR_DIRECTORY\converted.pdf", conversionOptions);
```

**لماذا هذا مهم:** التحويل المبكر يضمن أن أي موارد مضافة (مثل إدخالات ExtGState) ترث ملف التعريف اللوني الصحيح ومعالجة الشفافية المطلوبة من قبل PDF/X‑4.

## الخطوة 3: استرجاع أسماء التوقيعات الموجودة

```csharp
var signatureNames = pdfDocument.Signatures.GetSignatureNames();
if (signatureNames.Count > 0)
{
    Console.WriteLine("Existing signatures:");
    foreach (var name in signatureNames)
        Console.WriteLine($"- {name}");
}
```

**لماذا هذا مهم:** التوقيع بعد التعديلات قد يكسر سلسلة التوقيع. من خلال سرد التوقيعات مبكرًا، يمكنك اتخاذ قرار ما إذا كنت ستعيد التوقيع بعد خطوة `save modified pdf`.

## الخطوة 4: إضافة TextBoxField متعدد الودجات

```csharp
// Access the first page (pages are 1‑based in Aspose.PDF)
var firstPage = pdfDocument.Pages[1];

// Define the rectangle where the field will appear
var fieldRect = new Rectangle(100, 500, 200, 520);

// Create the TextBoxField
var multiWidgetField = new TextBoxField(firstPage, fieldRect)
{
    Name = "MultiBox",          // Logical name of the field
    Value = "Enter text here"   // Default text (optional)
};

// Add a widget annotation so the field is visible
var widget = new WidgetAnnotation(firstPage, fieldRect);
multiWidgetField.Widgets.Add(widget);

// Register the field with the document
pdfDocument.Form.Add(multiWidgetField);
```

**لماذا هذا مهم:** `TextBoxField` هو الودجت القياسي لإدخال النص الحر. إضافة `WidgetAnnotation` تجعل الحقل يظهر على سطح الصفحة. تسجيل الحقل مع `pdfDocument.Form` يضمن أنه جزء من هيكل AcroForm، والذي تعتمد عليه عارضات PDF.

## الخطوة 5: تطبيق وضع المزج وتعيين شفافية التعبئة

```csharp
// Access the page's resource dictionary editor
var resourcesEditor = new DictionaryEditor(firstPage.Resources);

// Ensure the ExtGState dictionary exists
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    resourcesEditor["ExtGState"] = new CosPdfDictionary(pdfDocument);
}

// Grab the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create a new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
graphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity (1 = fully opaque)
graphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity (0.5 = 50 % transparent)
graphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode (Normal is default)

// Add the graphics state to the ExtGState dictionary
extGStateDict.Add("GS0", graphicsState);
```

**لماذا هذا مهم:** `ca` يتحكم في شفافية التعبئة، بينما `CA` يتحكم في شفافية الحد. ضبط `BM` إلى `"Normal"` يحافظ على وضع المزج الافتراضي، لكن يمكنك استخدام `"Multiply"` أو `"Screen"` لتأثيرات فنية. بالإشارة إلى `GS0` لاحقًا في تدفق المحتوى (ليس مطلوبًا لحقل نص بسيط، لكنه مفيد للرسم المخصص)، تحصل على تحكم دقيق في كيفية دمج الحقل مع محتوى الصفحة الأساسي.

## الخطوة 6: حفظ PDF المعدل

```csharp
var outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Modified PDF saved to {outputPath}");
```

**لماذا هذا مهم:** استدعاء `Save` يكتب جميع التغييرات—بما في ذلك حقل النص الجديد وإدخال ExtGState—إلى القرص. إذا قمت بإجراء تحويل مسبقًا، قد ترغب في **حفظ pdf المعدل** باسم ملف مختلف للحفاظ على الأصلي.

---

## مثال كامل قابل للتنفيذ

فيما يلي برنامج مستقل يمكنك نسخه، لصقه، وتشغيله. عدل العنصر النائب `YOUR_DIRECTORY` ليشير إلى مجلد حقيقي على جهازك.




## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إضافة صندوق نص PDF – إنشاء حقل نموذج PDF وحفظ مستند PDF المعدل](/pdf/english/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/)
- [إنشاء مستند PDF باستخدام Aspose – إضافة حقل صندوق نص](/pdf/english/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/)
- [ضبط شفافية PDF وتغيير وضع المزج باستخدام Aspose.Pdf لـ .NET](/pdf/english/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}