---
category: general
date: 2026-06-18
description: أضف مربع نص إلى نموذج PDF بسرعة. تعلم كيفية إنشاء مربع نص PDF قابل للتعبئة
  وكيفية إضافة حقل تعليق PDF باستخدام Aspose.PDF لـ .NET.
draft: false
keywords:
- add text box to pdf form
- create fillable pdf textbox
- how to add comment field pdf
language: ar
og_description: إضافة مربع نص إلى نموذج PDF باستخدام Aspose.PDF لـ .NET. يوضح هذا
  الدليل كيفية إنشاء مربع نص PDF قابل للتعبئة وكيفية إضافة حقل تعليقات إلى PDF في
  بضع أسطر فقط.
og_title: إضافة صندوق نص إلى نموذج PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Add text box to PDF form quickly. Learn how to create fillable PDF
    textbox and how to add comment field PDF using Aspose.PDF for .NET.
  headline: Add Text Box to PDF Form – Complete C# Guide
  type: TechArticle
- description: Add text box to PDF form quickly. Learn how to create fillable PDF
    textbox and how to add comment field PDF using Aspose.PDF for .NET.
  name: Add Text Box to PDF Form – Complete C# Guide
  steps:
  - name: – Load the PDF document
    text: We need a `Document` object that represents the existing file. Aspose.PDF
      makes this a one‑liner.
  - name: – Create a TextBox field on the target page
    text: We’ll place the textbox on page 1 (index 0) inside a rectangle that defines
      its size and position. The rectangle uses points (1 inch = 72 points).
  - name: – Assign a name to the field
    text: Every form field needs a unique identifier. This name is what you’ll reference
      later when extracting data.
  - name: – Enable multiple widget annotations (optional but handy)
    text: If you want the same textbox to appear on several pages, set `MultipleWidgetAnnotations`
      to `true`. For a single‑page comment field you can skip this, but it doesn’t
      hurt.
  - name: – Add the TextBox field to the document’s form collection
    text: Now the field becomes part of the PDF’s interactive form.
  - name: – Save the modified PDF
    text: Finally, write the changes back to disk.
  - name: Can I set a default value?
    text: Yes. Just assign `textBox.Value = "Enter your comment here";` before adding
      the field.
  - name: What if I need a multiline textbox?
    text: 'Set the `IsMultiline` property:'
  - name: How do I change the appearance (border, background)?
    text: '```csharp textBox.BorderColor = Color.Black; textBox.BorderWidth = 1; textBox.BackgroundColor
      = Color.LightYellow; ```'
  - name: Does this work with PDF/A or encrypted PDFs?
    text: 'Aspose.PDF can handle PDF/A‑1b, PDF/A‑2b, and encrypted files as long as
      you provide the password when loading:'
  type: HowTo
tags:
- pdf
- csharp
- pdf-form
- textbox
- aspnet
title: إضافة مربع نص إلى نموذج PDF – دليل C# الكامل
url: /ar/net/programming-with-forms/add-text-box-to-pdf-form-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة مربع نص إلى نموذج PDF – دليل C# كامل

هل احتجت يوماً إلى **إضافة مربع نص إلى نموذج PDF** لكن لم تكن متأكدًا من أي استدعاءات API تستخدم؟ لست وحدك. سواءً كنت تبني أداة جمع ملاحظات، أو بوابة توقيع عقود، أو حقل تعليقات بسيط، فإن مربع النص القابل للملء هو الحل المثالي. في هذا الدليل سنستعرض الخطوات الدقيقة **لإنشاء مربع نص PDF قابل للملء** وسنجيب أيضًا على السؤال الشائع **كيفية إضافة حقل تعليقات PDF** باستخدام Aspose.PDF for .NET.

سنبدأ بملف PDF نظيف، نضيف مربع نص إلى الصفحة 1، نعطيه اسمًا ودودًا، نفعّل دعم الودجت المتعدد، وأخيرًا نحفظ النتيجة. في النهاية ستحصل على ملف PDF جاهز للاستخدام يمكن لأي شخص فتحه في Adobe Reader، كتابة تعليق، والضغط على حفظ. لا أدوات خارجية، لا تحرير يدوي—فقط كود C# نقي.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+ )  
- Visual Studio 2022 أو أي بيئة تطوير تفضلها  
- حزمة NuGet Aspose.PDF for .NET (`Install-Package Aspose.PDF`)  
- ملف PDF مصدر (`input.pdf`) موجود في مجلد يمكنك التحكم فيه  

هذا كل شيء. إذا كان لديك هذه المكونات، فأنت جاهز للبدء.

## إضافة مربع نص إلى نموذج PDF باستخدام C#

فيما يلي جوهر الشرح. كل خطوة موضحة، ثم يتبعها مقطع C# المناسب. يمكنك نسخ‑لصق الكتلة بالكامل إلى تطبيق Console؛ سيُترجم ويعمل كما هو.

### الخطوة 1 – تحميل مستند PDF

نحتاج إلى كائن `Document` يمثل الملف الموجود. Aspose.PDF يجعل ذلك سطرًا واحدًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using System.Drawing;

// Load the source PDF
Document doc = new Document(@"C:\MyPdfs\input.pdf");
```

*لماذا هذا مهم:* تحميل الـ PDF يتيح لنا الوصول إلى صفحاته، التعليقات، ومجموعة النماذج حيث توجد الحقول. بدون كائن `Document` لا يمكننا إضافة أي شيء.

### الخطوة 2 – إنشاء حقل TextBox على الصفحة المستهدفة

سنضع مربع النص على الصفحة 1 (الفهرس 0) داخل مستطيل يحدد حجمه وموقعه. يستخدم المستطيل النقاط (1 بوصة = 72 نقطة).

```csharp
// Define the rectangle: left, bottom, right, top
Rectangle rect = new Rectangle(100, 600, 300, 630);

// Create the TextBox field on page 1
TextBoxField textBox = new TextBoxField(doc.Pages[1], rect);
```

*لماذا هذا مهم:* يحدد المستطيل مكان ظهور الحقل للمستخدم. عدّل الإحداثيات لتتناسب مع تخطيطك. فئة `TextBoxField` ترث تلقائيًا خصائص بصرية مثل الحدود والخلفية.

### الخطوة 3 – تعيين اسم للحقل

كل حقل نموذج يحتاج إلى معرف فريد. هذا الاسم هو ما ستستخدمه لاحقًا لاستخراج البيانات.

```csharp
textBox.FieldName = "Comments";
```

*لماذا هذا مهم:* تسمية الحقل بـ `"Comments"` تتيح لك استرجاع إدخال المستخدم عبر `doc.Form["Comments"]` بعد ملء الـ PDF. كما يظهر الاسم في قائمة الحقول في قارئات الـ PDF.

### الخطوة 4 – تمكين ودجتات متعددة (اختياري لكن مفيد)

إذا أردت ظهور نفس مربع النص على عدة صفحات، اضبط `MultipleWidgetAnnotations` إلى `true`. لحقل تعليقات صفحة واحدة يمكنك تخطي هذه الخطوة، لكنها لا ضرر فيها.

```csharp
textBox.MultipleWidgetAnnotations = true;
```

*لماذا هذا مهم:* الويدجتات المتعددة تشارك نفس البيانات، لذا يمكن للمستخدم الكتابة مرة واحدة ورؤية التعليق نفسه على كل صفحة تحتوي على الويدجت. هذه حيلة مفيدة للعقود متعددة الصفحات.

### الخطوة 5 – إضافة حقل TextBox إلى مجموعة نماذج المستند

الآن يصبح الحقل جزءًا من نموذج PDF التفاعلي.

```csharp
doc.Form.Add(textBox);
```

*لماذا هذا مهم:* إضافة الحقل تسجّله في قاموس AcroForm الخاص بالـ PDF. بدون هذه الخطوة سيبقى مربع النص في الذاكرة ولن يظهر في الملف المحفوظ.

### الخطوة 6 – حفظ الـ PDF المعدل

أخيرًا، اكتب التغييرات إلى القرص.

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

*لماذا هذا مهم:* الحفظ يثبت حقل النموذج الجديد. افتح `output.pdf` في Adobe Reader وسترى مربع نص فارغ بعنوان “Comments” جاهز للكتابة.

## مثال كامل يعمل

بجمع كل ما سبق، إليك تطبيق Console مستقل يمكنك تشغيله فورًا:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using System.Drawing; // for Rectangle

namespace PdfFormDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the existing PDF
            string inputPath = @"C:\MyPdfs\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Define the rectangle where the textbox will live
            Rectangle rect = new Rectangle(100, 600, 300, 630);

            // 3️⃣ Create the TextBox field on page 1 (index 1)
            TextBoxField textBox = new TextBoxField(doc.Pages[1], rect)
            {
                // 4️⃣ Give it a meaningful name
                FieldName = "Comments",

                // 5️⃣ Allow the same widget on multiple pages (optional)
                MultipleWidgetAnnotations = true
            };

            // 6️⃣ Add the field to the form collection
            doc.Form.Add(textBox);

            // 7️⃣ Save the updated PDF
            string outputPath = @"C:\MyPdfs\output.pdf";
            doc.Save(outputPath);

            Console.WriteLine("✅ Text box added successfully! Check " + outputPath);
        }
    }
}
```

**الناتج المتوقع:** عند فتح `output.pdf` ستلاحظ منطقة إدخال مستطيلة على الصفحة 1. النقر داخلها يتيح لك كتابة أي تعليق. الحقل يبقى بعد الحفظ، مما يعني أنك نجحت في الإجابة على **كيفية إضافة حقل تعليقات PDF**.

## أسئلة شائعة وحالات خاصة

### هل يمكن تعيين قيمة افتراضية؟

نعم. فقط عيّن `textBox.Value = "Enter your comment here";` قبل إضافة الحقل.

### ماذا لو احتجت مربع نص متعدد الأسطر؟

اضبط الخاصية `IsMultiline`:

```csharp
textBox.IsMultiline = true;
textBox.MaxLength = 500; // optional limit
```

### كيف أغيّر المظهر (الحدود، الخلفية)؟

```csharp
textBox.BorderColor = Color.Black;
textBox.BorderWidth = 1;
textBox.BackgroundColor = Color.LightYellow;
```

### هل يعمل هذا مع PDF/A أو ملفات PDF مشفرة؟

Aspose.PDF يمكنه التعامل مع PDF/A‑1b، PDF/A‑2b، والملفات المشفرة طالما زودت كلمة المرور عند التحميل:

```csharp
Document doc = new Document(inputPath, new LoadOptions { Password = "secret" });
```

### ماذا لو أردت مربع النص في صفحة مختلفة؟

استبدل `doc.Pages[1]` بالفهرس المطلوب (`doc.Pages[2]` للصفحة 3، إلخ). تذكّر أن مجموعة الصفحات في Aspose.PDF هي **مؤشرة من 1**.

## نصائح احترافية

- **نصيحة احترافية:** استخدم `doc.Form.RefreshAppearance();` بعد إضافة عدة حقول لضمان عرض جميع الويدجتات بشكل صحيح في عارضات PDF القديمة.  
- **احذر من:** تداخل المستطيلات. إذا شاركت حقلان نفس المنطقة، قد يخفي Acrobat أحدهما.  
- **ملاحظة أداء:** عند معالجة آلاف ملفات PDF، أعد استخدام كائن `Document` واحد للقراءة ونسخ حقل النموذج فقط لتجنب تخصيصات متكررة.

## الخطوات التالية

الآن بعد أن عرفت كيف **تضيف مربع نص إلى نموذج PDF**، قد ترغب في استكشاف المواضيع ذات الصلة:

- **إنشاء مربع نص PDF قابل للملء** مع قواعد التحقق (`textBox.Validate = new RegExValidator("[A-Za-z0-9]+");`)  
- **إضافة أزرار راديو أو مربعات اختيار** لبناء استبيان كامل  
- **تسطيح النموذج** بعد الإرسال لمنع التعديل الإضافي (`doc.Form.Flatten();`)  
- **استخراج البيانات المدخلة** باستخدام `doc.Form["Comments"].Value` وتخزينها في قاعدة بيانات  

كل هذه تبني على المفاهيم الأساسية التي غطيناها، لذا أنت الآن في موقع جيد لتوسيع مجموعة أدوات أتمتة PDF الخاصة بك.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقًا أدناه وسنساعدك في حلها.*


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Add TextBox Fields in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/forms-annotations/add-textbox-field-aspose-pdf-net/)
- [How to Add and Extract PDF Form Fields Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)
- [How to Add Tooltips to PDF Text Using Aspose.PDF for .NET ( Forms & Annotations )](/pdf/english/net/forms-annotations/aspose-pdf-net-add-tooltips-pdfs/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}