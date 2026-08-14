---
category: general
date: 2026-08-14
description: إنشاء حقل نموذج PDF بسرعة باستخدام C#. تعلم كيفية إضافة مربع نص إلى PDF
  وتعديل PDF لتضمين مربع النص باستخدام Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf form field
- add text box to pdf
- modify pdf to include text box
- Aspose.PDF form field
- C# PDF manipulation
language: ar
lastmod: 2026-08-14
og_description: إنشاء حقل نموذج PDF باستخدام C#. يوضح هذا البرنامج التعليمي كيفية
  إضافة مربع نص إلى ملف PDF وتعديل ملف PDF لتضمين مربع نص باستخدام Aspose.PDF.
og_image_alt: Screenshot of a PDF page showing a newly added text box form field
og_title: إنشاء حقل نموذج PDF في C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  headline: Create pdf form field in C# – step‑by‑step guide
  type: TechArticle
- description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  name: Create pdf form field in C# – step‑by‑step guide
  steps:
  - name: Load the existing PDF document.
    text: Load the existing PDF document.
  - name: Instantiate a `TextBoxField` and configure its name and appearance.
    text: Instantiate a `TextBoxField` and configure its name and appearance.
  - name: Add a widget annotation that defines the visual rectangle on the target
      page.
    text: Add a widget annotation that defines the visual rectangle on the target
      page.
  - name: Insert the field into the document’s form collection.
    text: Insert the field into the document’s form collection.
  - name: Save the modified PDF.
    text: Save the modified PDF.
  - name: Open `output.pdf` in Adobe Acrobat Reader.
    text: Open `output.pdf` in Adobe Acrobat Reader.
  - name: Click inside the “Comments” box; the cursor should appear.
    text: Click inside the “Comments” box; the cursor should appear.
  - name: Type any text and press **Tab** or click elsewhere.
    text: Type any text and press **Tab** or click elsewhere.
  - name: Choose **File → Save As** to persist the entered value.
    text: Choose **File → Save As** to persist the entered value.
  - name: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
    text: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
  type: HowTo
tags:
- pdf
- csharp
- form-fields
title: إنشاء حقل نموذج PDF في C# – دليل خطوة بخطوة
url: /ar/net/programming-with-forms/create-pdf-form-field-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء حقل نموذج PDF في C# – دليل خطوة بخطوة

إذا كنت بحاجة إلى **إنشاء حقل نموذج PDF** في مستند، فإن هذا الدليل سيرشدك خلال العملية بأكملها. سترى بالضبط كيفية **إضافة مربع نص إلى PDF** في الصفحات، وكيفية **تعديل PDF لتضمين مربع نص** باستخدام مكتبة Aspose.PDF لـ .NET.

التعامل مع نماذج PDF هو مطلب شائع لأنظمة الفوترة، الاستطلاعات، أو أي سير عمل يجمع مدخلات المستخدم. بنهاية هذا الدرس ستحصل على مقتطف شفرة قابل لإعادة الاستخدام ينشئ حقل مربع نص يعمل بالكامل، يضعه في المكان الذي تريد، ويحفظ ملف PDF المحدث—كل ذلك دون مغادرة مشروع C# الخاص بك.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
* Visual Studio 2022 أو أي بيئة تطوير تدعم C#
* رخصة Aspose.PDF for .NET سارية (الإصدار التجريبي المجاني يعمل للتطوير)
* ملف PDF اسمه `input.pdf` موجود في دليل معروف (يستخدم الدرس `YOUR_DIRECTORY` كعنصر نائب)

> **نصيحة احترافية:** إذا لم يكن لديك رخصة بعد، يمكنك طلب مفتاح مؤقت من موقع Aspose؛ المكتبة تعمل في وضع التقييم دون الحاجة لتغييرات في الشفرة.

## كيفية إنشاء حقل نموذج PDF في C# (نظرة عامة)

1. تحميل مستند PDF الموجود.  
2. إنشاء كائن `TextBoxField` وتكوين اسمه ومظهره.  
3. إضافة تعليقة widget تحدد المستطيل البصري على الصفحة المستهدفة.  
4. إدراج الحقل في مجموعة نماذج المستند.  
5. حفظ PDF المعدل.

يتم شرح كل خطوة بالتفصيل أدناه، مع أمثلة شفرة كاملة وتبرير الاستدعاءات API.

## الخطوة 1: تحميل مستند PDF

العملية الأولى هي قراءة ملف PDF المصدر. تمثل Aspose.PDF ملف PDF باستخدام الفئة `Document`. تحميل المستند يمنحك الوصول إلى صفحاته، مجموعة النماذج، والهياكل الأخرى.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

// Adjust the path to match your environment
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

// Load the PDF you want to modify
Document pdfDocument = new Document(inputPath);
```

**لماذا هذا مهم:**  
تحميل الملف ينشئ نموذجًا في الذاكرة من PDF، مما يتيح لك إضافة أو إزالة أو تعديل الكائنات دون إتلاف الملف الأصلي. كما أن كائن `Document` يعرض الخاصية `Form`، وهي المكان الذي ستقوم فيه لاحقًا **بإضافة مربع نص إلى PDF**.

## الخطوة 2: إنشاء حقل مربع نص

حقل مربع النص هو نوع من حقول النموذج يسمح للمستخدمين بكتابة نص حر. في Aspose.PDF تقوم بإنشائه عن طريق إنشاء كائن `TextBoxField`، وتمرير الصفحة المستهدفة ومستطيل يحدد الحجم الأولي للـ widget.

```csharp
// Choose the page index (0‑based). Here we use page 2 (index 1).
Page targetPage = pdfDocument.Pages[1];

// Define the rectangle for the field’s *initial* size.
// Rectangle(left, bottom, right, top) – values are in points (1/72 inch).
Rectangle fieldRect = new Rectangle(100, 500, 200, 530);

// Create the TextBoxField with a partial name that will be used in form data.
TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
{
    PartialName = "Comments", // This identifier appears in the PDF form data.
    // Optional: set default appearance (font, size, color)
    DefaultAppearance = new DefaultAppearance(FontRepository.FindFont("Helvetica"), 12, Color.Black)
};
```

**لماذا هذا مهم:**  
* `PartialName` هو المفتاح الذي تستخدمه أدوات معالجة النماذج (مثل Adobe Acrobat، المحللات على الخادم) لاسترجاع القيمة المدخلة.  
* المستطيل الذي تمرره هنا يحدد فقط حجم الـ widget *الأولي*؛ يمكنك لاحقًا تعديل موقعه البصري باستخدام تعليقة widget (الخطوة التالية).  
* ضبط `DefaultAppearance` يضمن أن النص داخل المربع يُعرض بشكل متسق عبر عارضات PDF.

## الخطوة 3: تعريف تعليقة widget البصرية

يمكن لحقل النموذج أن يحتوي على واحد أو أكثر من **تعليقات widget** التي تتحكم في مكان ظهور الحقل في كل صفحة. بإضافة widget يمكنك وضع الحقل المنطقي نفسه في موقع مختلف أو حتى على صفحات متعددة.

```csharp
// Define where the field will actually be displayed on the page.
// This rectangle can differ from the one used in the constructor.
Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
textBox.AddWidgetAnnotation(widgetRect);
```

**لماذا هذا مهم:**  
مستطيل الـ widget يحدد الإحداثيات على الشاشة التي يراها المستخدمون. إذا تخطيت هذه الخطوة، قد يكون الحقل موجودًا في بنية بيانات PDF لكنه لن يكون مرئيًا للمستخدم النهائي. إضافة widget هي الخطوة التي فعليًا **تضيف مربع نص إلى PDF**.

## الخطوة 4: إضافة الحقل المكوَّن إلى نموذج المستند

الآن بعد أن تم تكوين `TextBoxField` بالكامل، تحتاج إلى تسجيله في مجموعة نماذج PDF. هذا يجعل الحقل جزءًا من النموذج التفاعلي ويضمن حفظه.

```csharp
pdfDocument.Form.Add(textBox);
```

**لماذا هذا مهم:**  
بدون إضافة الحقل إلى `pdfDocument.Form`، سيتجاهل عارض PDF تعليقة widget، ولن يتم إرسال بيانات الحقل أبدًا. هذا السطر يُكمل عملية **تعديل PDF لتضمين مربع نص**.

## الخطوة 5: حفظ PDF المحدث

أخيرًا، اكتب التغييرات مرة أخرى إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد؛ المثال يحفظ إلى `output.pdf`.

```csharp
string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");

// Save the document with the new form field
pdfDocument.Save(outputPath);
```

عند فتح `output.pdf` في Adobe Acrobat Reader، سترى مربع نص مستطيل بعنوان “Comments” في الصفحة 2. يمكن للمستخدمين النقر داخل المربع، الكتابة، وستصبح النصوص المدخلة جزءًا من بيانات نموذج PDF.

## مثال كامل يعمل

بتجميع كل الأجزاء معًا، إليك برنامج كامل وجاهز للتنفيذ. انسخه إلى مشروع وحدة تحكم جديد، استبدل `YOUR_DIRECTORY` بمسار مجلد حقيقي، وشغّله.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Drawing; // For Color

namespace PdfFormFieldDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the existing PDF
            string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
            Document pdfDocument = new Document(inputPath);

            // 2️⃣ Create a TextBoxField on page 2 (index 1)
            Page targetPage = pdfDocument.Pages[1];
            Rectangle fieldRect = new Rectangle(100, 500, 200, 530);
            TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
            {
                PartialName = "Comments",
                DefaultAppearance = new DefaultAppearance(
                    FontRepository.FindFont("Helvetica"), 12, Color.Black)
            };

            // 3️⃣ Add a widget annotation to control visual placement
            Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
            textBox.AddWidgetAnnotation(widgetRect);

            // 4️⃣ Register the field with the document's form collection
            pdfDocument.Form.Add(textBox);

            // 5️⃣ Save the modified PDF
            string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
            pdfDocument.Save(outputPath);

            Console.WriteLine("PDF form field created successfully.");
            Console.WriteLine($"Output saved to: {outputPath}");
        }
    }
}
```

**الناتج المتوقع:**  
تشغيل البرنامج يطبع سطرين تأكيديين إلى وحدة التحكم. فتح `output.pdf` يظهر مربع نص في الصفحة 2 حيث يمكن للمستخدم كتابة تعليقات. عند إرسال النموذج (مثلاً عبر زر “Submit” في Adobe Acrobat)، يظهر اسم الحقل `Comments` في بيانات FDF أو XFDF المصدرة.

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية تعديل الشفرة |
|-----------|-----------------------|
| **إضافة الحقل إلى صفحة مختلفة** | غيّر `pdfDocument.Pages[1]` إلى فهرس الصفحة المطلوب (`0`‑مبني). |
| **إنشاء مربع نص متعدد الأسطر** | اضبط `textBox.Multiline = true;` قبل إضافة الـ widget. |
| **تعيين قيمة افتراضية** | عيّن `textBox.Value = "Enter your comments here";`. |
| **جعل الحقل مطلوبًا** | اضبط `textBox.Required = true;`. |
| **وضع الحقل على صفحات متعددة** | استدعِ `textBox.AddWidgetAnnotation` لكل مستطيل إضافي على الصفحات المستهدفة. |
| **استخدام خط مخصص** | حمّل الخط باستخدام `FontRepository.AddFont("path/to/font.ttf")` وأشر إليه في `DefaultAppearance`. |

**نصيحة احترافية:** دائمًا تحقق من إحداثيات المستطيل مقابل حجم الصفحة (`pdfDocument.Pages[1].Rect`). إذا كان الـ widget يقع خارج حدود الصفحة، قد تقوم العارضات بقطع أو إخفاء الحقل.

## اختبار حقل النموذج

1. افتح `output.pdf` في Adobe Acrobat Reader.  
2. انقر داخل صندوق “Comments”؛ يجب أن يظهر المؤشر.  
3. اكتب أي نص واضغط **Tab** أو انقر في مكان آخر.  
4. اختر **File → Save As** لحفظ القيمة المدخلة.  
5. (اختياري) استخدم API `Form` في Aspose.PDF لاستخراج القيمة برمجيًا:

```csharp
string commentValue = pdfDocument.Form["Comments"].Value;
Console.WriteLine($"Submitted comment: {commentValue}");
```

هذا المقتطف يوضح أن الحقل ليس مرئيًا فحسب، بل يمكن استرجاعه عبر الشفرة—وهو أمر أساسي للمعالجة على جانب الخادم.

## الخلاصة

أنت الآن تعرف كيف **إنشاء حقل نموذج PDF** في C# من البداية إلى النهاية. غطى الدرس تحميل PDF، تكوين `TextBoxField`، إضافة تعليقة widget، تسجيل الحقل، وحفظ النتيجة. باستخدام هذه اللبنات الأساسية يمكنك **إضافة مربع نص إلى PDF**، **تعديل PDF لتضمين مربع نص**، وتوسيع النهج إلى أنواع حقول أخرى مثل مربعات الاختيار، أزرار الراديو، أو القوائم المنسدلة.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **استخراج بيانات النموذج**، **تسطيح نماذج PDF**، أو **تنسيق الحقول بالحدود والألوان**. كل من هذه المفاهيم يبني على نفس API الأساسي الذي تعلمته للتو، مما يتيح لك إنشاء ملفات PDF تفاعلية متقدمة بالكامل في C#.

برمجة سعيدة، ولا تتردد في تجربة مستطيلات مختلفة، خطوط، وقواعد التحقق لتناسب احتياجات تطبيقك!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند PDF باستخدام Aspose – إضافة صفحة، مربع نص، ونموذج](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج وصفحات](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [كيفية إضافة ختم نصي إلى PDF باستخدام Aspose.PDF .NET: دليل شامل](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}