---
category: general
date: 2026-09-27
description: إنشاء مستند PDF وإضافة صفحات إلى PDF أثناء بناء نموذج PDF تفاعلي. تعلّم
  كيفية إضافة مربع نص إلى PDF وإنشاء نموذج AcroForm PDF باستخدام Aspose.Pdf.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add pages to pdf
- create interactive pdf form
- how to add textbox to pdf
- how to create acroform pdf
language: ar
lastmod: 2026-09-27
og_description: إنشاء مستند PDF وإضافة صفحات إلى PDF أثناء بناء نموذج PDF تفاعلي.
  اتبع هذا الدليل لتعلم كيفية إضافة مربع نص إلى PDF وإنشاء نموذج AcroForm PDF باستخدام
  Aspose.Pdf.
og_image_alt: Screenshot showing a PDF document with a textbox field on two pages
og_title: إنشاء مستند PDF مع حقول نموذج تفاعلية – دليل C# خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  headline: How to create PDF document with interactive form fields in C#
  type: TechArticle
- description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  name: How to create PDF document with interactive form fields in C#
  steps:
  - name: '**Create PDF document** and add the needed pages.'
    text: '**Create PDF document** and add the needed pages.'
  - name: '**Initialize AcroForm** and define a `TextBoxField`.'
    text: '**Initialize AcroForm** and define a `TextBoxField`.'
  - name: '**Add widget annotations** on each page to place the textbox.'
    text: '**Add widget annotations** on each page to place the textbox.'
  - name: '**Save** the document and test the interactive behavior.'
    text: '**Save** the document and test the interactive behavior.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF forms
title: كيفية إنشاء مستند PDF مع حقول نموذج تفاعلية في C#
url: /ar/net/programming-with-forms/how-to-create-pdf-document-with-interactive-form-fields-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مستند PDF مع حقول نموذج تفاعلية في C#

إذا كنت بحاجة إلى **إنشاء مستند PDF** يحتوي على عدة صفحات ونموذج تفاعلي، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. سنستعرض إضافة صفحات إلى PDF، بناء AcroForm، ووضع حقل TextBox على كل صفحة باستخدام Aspose.Pdf لـ .NET. ستحصل في النهاية على ملف PDF واحد يتيح للمستخدمين كتابة تعليقات على الصفحتين. لا أدوات خارجية، فقط بضع أسطر من C# ومكتبة Aspose.Pdf القوية.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
* ترخيص صالح لـ Aspose.Pdf for .NET أو مفتاح تقييم مؤقت
* Visual Studio 2022 (أو أي بيئة تطوير تدعم C#)
* إلمام أساسي بصياغة C# ومفاهيم البرمجة الكائنية

> **نصيحة احترافية:** إذا كنت تستخدم النسخة التجريبية المجانية، تذكر ضبط كائن `License` مبكرًا في برنامجك لتجنب العلامات المائية للتقييم.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيقًا جديدًا من نوع console وأضف حزمة Aspose.Pdf عبر NuGet:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
dotnet add package Aspose.Pdf
```

في `Program.cs` استورد المساحات الاسمية المطلوبة:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

هذه المساحات الاسمية تمنحك الوصول إلى كائنات PDF الأساسية، وأنواع التعليقات التوضيحية، وفئات حقول النموذج المطلوبة في هذا الشرح.

## الخطوة 2: إنشاء مستند PDF وإضافة صفحات إلى PDF

الخطوة الوظيفية الأولى هي **إنشاء مستند PDF** ثم **إضافة صفحات إلى PDF**. ستستضيف كل صفحة نفس حقل TextBox.

```csharp
// Initialize a new PDF document
var pdfDocument = new Document();

// Add two blank pages
var firstPage = pdfDocument.Pages.Add();
var secondPage = pdfDocument.Pages.Add();
```

*لماذا هذا مهم:*  
`Document` يمثل ملف PDF بالكامل. إضافة الصفحات صراحةً يضمن وجود مساحة لوضع عناصر النموذج. يمكنك إضافة عدد الصفحات الذي تحتاجه؛ المثال يستخدم صفحتين للتوضيح.

## الخطوة 3: إنشاء نموذج PDF تفاعلي (AcroForm)

يتم بناء **نموذج PDF تفاعلي** على كائن AcroForm موجود داخل `Document`. سننشئ حقل `TextBoxField` واحد سيتم مشاركته عبر الصفحتين.

```csharp
// Initialize the AcroForm if it doesn't exist
if (!pdfDocument.AcroForm.IsPresent)
{
    pdfDocument.AcroForm = new AcroForm(pdfDocument);
}

// Create a TextBox field named "Comments"
var textBoxField = new TextBoxField(pdfDocument.AcroForm)
{
    Name = "Comments",
    // Optional: set default appearance (font size, color)
    DefaultAppearance = new DefaultAppearance("Helvetica", 12, Color.Black)
};
```

*لماذا هذا مهم:*  
حاوية AcroForm تحتفظ بجميع العناصر التفاعلية. بإنشاء حقل `TextBoxField` واحد، يمكننا إعادة استخدام نفس الحقل المنطقي على صفحات متعددة، مما يحافظ على تزامن البيانات عندما يقوم المستخدم بملئه.

## الخطوة 4: كيفية إضافة TextBox إلى PDF – وضع تعليقات توضيحية Widget

**تعليق توضيحي widget** يربط مستطيلًا مرئيًا على الصفحة بالحقل المنطقي للنموذج. سنضيف widget واحد على كل صفحة.

```csharp
// Widget on the first page (coordinates: lower‑left X,Y – upper‑right X,Y)
var firstPageWidget = new WidgetAnnotation(
    firstPage,
    new Rectangle(50, 700, 200, 750))
{
    Parent = textBoxField,
    // Optional visual properties
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};

// Widget on the second page, positioned slightly lower
var secondPageWidget = new WidgetAnnotation(
    secondPage,
    new Rectangle(50, 600, 200, 650))
{
    Parent = textBoxField,
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};
```

*لماذا هذا مهم:*  
`WidgetAnnotation` يحدد مكان ظهور صندوق النص وكيفية مظهره. من خلال تعيين نفس `Parent` (`textBoxField`)، يشير كلا الـ widget إلى نفس حقل البيانات الأساسي. المستخدمون الذين يكتبون في أحد الـ widget سيشاهدون نفس القيمة على الصفحة الأخرى.

## الخطوة 5: حفظ PDF والتحقق من النتيجة

أخيرًا، اكتب المستند إلى القرص:

```csharp
// Save the PDF to the output folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);

Console.WriteLine($"PDF saved to {outputPath}");
```

عند فتح `output.pdf` في Adobe Acrobat Reader:

* يعرض المستند صفحتين.
* كل صفحة تحتوي على صندوق نص معنون بـ “Comments”.
* الكتابة في صندوق النص على أي من الصفحتين تُحدّث الآخر فورًا (فهما يشتركان في نفس اسم الحقل).

### لقطة شاشة للنتيجة المتوقعة

![PDF مع صندوق نص على صفحتين](https://example.com/pdf-form-screenshot.png "إنشاء مستند PDF مع حقول نموذج تفاعلية")

*(نص alt للصورة يحتوي على الكلمة المفتاحية الأساسية من أجل إمكانية الوصول وتحسين محركات البحث.)*

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية التعامل معها |
|-----------|------------------|
| **أكثر من صفحتين** | إنشاء كائنات `WidgetAnnotation` إضافية لكل صفحة جديدة، مع إعادة استخدام نفس `textBoxField`. |
| **أسماء حقول مختلفة لكل صفحة** | إنشاء مثيلات `TextBoxField` منفصلة (مثل `CommentsPage1`، `CommentsPage2`) وتعيين كل widget للـ parent الخاص به. |
| **صندوق نص متعدد الأسطر** | تعيين `textBoxField.Multiline = true;` قبل إضافة الـ widgets. |
| **حقول للقراءة فقط** | تعيين `textBoxField.ReadOnly = true;` لمنع تحرير المستخدم. |
| **خطوط مخصصة** | تحميل `TrueTypeFont` وتعيينه عبر `textBoxField.DefaultAppearance = new DefaultAppearance(font, 12, Color.Black);` |

هذه الاختلافات توضح مدى مرونة واجهة برمجة تطبيقات AcroForm مع الحفاظ على النمط الأساسي نفسه.

## ملخص خطوة بخطوة (مرجع سريع)

1. **إنشاء مستند PDF** وإضافة الصفحات المطلوبة.  
2. **تهيئة AcroForm** وتعريف `TextBoxField`.  
3. **إضافة تعليقات توضيحية widget** على كل صفحة لوضع صندوق النص.  
4. **حفظ** المستند واختبار السلوك التفاعلي.

## الخطوات التالية

الآن بعد أن عرفت **كيفية إضافة صندوق نص إلى PDF** و **كيفية إنشاء PDF بنموذج AcroForm**، يمكنك توسيع النموذج:

* إضافة مربعات اختيار، أزرار راديو، أو قوائم منسدلة باستخدام `CheckBoxField`، `RadioButtonField`، و `ComboBoxField`.
* تصدير بيانات النموذج إلى FDF أو XFDF للمعالجة على الخادم.
* تطبيق إجراءات JavaScript على الحقول للتحقق الديناميكي.

استكشف وثائق Aspose.Pdf الرسمية للحصول على قائمة كاملة بأنواع حقول النموذج وخيارات التنسيق المتقدمة.

---

*لقد تعلمت كيفية **إنشاء مستند PDF**، **إضافة صفحات إلى PDF**، **إنشاء نموذج PDF تفاعلي**، **كيفية إضافة صندوق نص إلى PDF**، و **كيفية إنشاء PDF بنموذج AcroForm** باستخدام مثال مختصر وقابل للتنفيذ. لا تتردد في تجربة أنواع حقول إضافية وتعديلات التخطيط لتناسب احتياجات تطبيقك.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات إضافية للواجهة البرمجية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج والصفحات](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [كيفية إضافة Text Box إلى PDF – إنشاء حقل نموذج PDF وحفظ مستند PDF المعدل](/pdf/english/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/)
- [إنشاء مستند PDF باستخدام Aspose – إضافة صفحة، Text Box، ونموذج](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}