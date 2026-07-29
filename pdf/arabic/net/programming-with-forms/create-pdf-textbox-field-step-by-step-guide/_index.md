---
category: general
date: 2026-06-21
description: إنشاء حقل نصي في PDF باستخدام C# وتعلم كيفية تكرار حقل نموذج PDF أو إضافة
  حقل نصي إلى نموذج PDF ببضع أسطر من الشيفرة فقط.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: ar
og_description: إنشاء حقل نصي في PDF بسرعة. يوضح هذا الدليل كيفية نسخ حقل نموذج PDF
  وإضافة حقل نصي إلى نموذج PDF باستخدام مكتبة PDF حديثة بلغة C#.
og_title: إنشاء حقل نصي في PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: إنشاء حقل نصي في PDF – دليل خطوة بخطوة
url: /ar/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء حقل نصي في PDF – دليل C# كامل

هل احتجت يوماً إلى **إنشاء حقل نصي في PDF** لكن لم تكن متأكدًا من أي استدعاءات API تستخدم؟ لست وحدك. سواء كنت تبني بوابة لتوقيع العقود أو ورقة بسيطة لالتقاط البيانات، فإن إضافة مربعات نص تفاعلية إلى PDF هي مهارة أساسية لأي مطور أتمتة نماذج.

في هذا الدليل سنستعرض مثالًا عمليًا لا يضيف **مربع نص إلى نموذج PDF** فحسب، بل يوضح أيضًا كيفية **تكرار حقل نموذج PDF** بحيث يظهر الإدخال نفسه على صفحات متعددة. بنهاية الدليل ستحصل على برنامج قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما الذي ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core أيضًا)  
- مكتبة PDF لـ C# – المقتطف أدناه يستخدم **PDFTron SDK**، لكن المفاهيم قابلة للتطبيق على iText 7، PdfSharp، أو مكتبات أخرى.  
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)  

هذا كل ما تحتاجه – لا خدمات إضافية، لا تبعيات غامضة. إذا كان لديك PDF تريد تعديله، فقط وجه الكود إليه.

---

## الخطوة 1: إعداد المشروع واستيراد الـ SDK

أولاً، أنشئ تطبيق console:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

أضف حزمة PDFTron عبر NuGet:

```bash
dotnet add package PDFTron.NET
```

الآن افتح `Program.cs` واستورد المساحات الاسم التي سنحتاجها:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **نصيحة محترف:** إذا كنت تستخدم مكتبة مختلفة، استبدل عبارات `using` بما يعادلها (مثلاً `iText.Kernel.Pdf` لـ iText 7).

## الخطوة 2: تهيئة مستند PDF والنموذج

سنبدأ بـ PDF جديد يحتوي على صفحتين – صفحة المصدر للمربع النصي الأصلي وصفحة الهدف للنسخة المكررة.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

كائن `Form` هو المكان الذي تعيش فيه جميع الحقول التفاعلية. إذا لم يكن للمستند نموذج مسبقًا، فإن `GetForm()` ينشئ واحدًا لنا.

## الخطوة 3: **إنشاء حقل نصي في PDF** على الصفحة الأولى

الآن يأتي جوهر الدرس – إنشاء حقل نصي. إحداثيات المستطيل معبر عنها بالنقاط (1 بوصة = 72 نقطة). المثال يضع المربع بالقرب من أعلى‑وسط الصفحة الأولى.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

لماذا نحدد `Value` فورًا؟ ملء الحقل مسبقًا يعطي المستخدم إشارة عن الإدخال المتوقع، كما يوضح أن الحقل يعمل بالكامل.

## الخطوة 4: إضافة الحقل إلى النموذج – **إضافة مربع نص إلى نموذج PDF**

بعد ذلك، نسجل الحقل في النموذج باستخدام اسم منطقي. هذا الاسم هو ما ستستخدمه لاحقًا لقراءة أو تعديل بيانات الحقل برمجيًا.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

اختيار اسم واضح (مثل `"multiBox"`) يجعل الكود اللاحق أسهل للفهم، خاصةً عندما يكون لديك العشرات من الحقول.

## الخطوة 5: **تكرار حقل نموذج PDF** على صفحة أخرى

متطلب شائع هو إظهار نفس الحقل على صفحات متعددة – فكر في مربع “اسم العميل” الذي يظهر على كل صفحة فاتورة. يتيح لنا PDFTron استنساخ ويدجت الـ annotation، وهو التمثيل البصري للحقل.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

الويدجت المستنسخ يشارك نفس البيانات الأساسية مع المربع النصي الأصلي. عندما يكتب المستخدم في أحد النسخ، يتحديث الآخر تلقائيًا – هذه هي سحر **تكرار حقل نموذج PDF**.

## الخطوة 6: حفظ المستند وتنظيف الموارد

أخيرًا، اكتب الـ PDF إلى القرص وأغلق بيئة تشغيل PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

تشغيل البرنامج ينتج PDF من صفحتين (`output.pdf`). افتحه في Adobe Acrobat Reader، انقر على المربع النصي في الصفحة 1، اكتب شيئًا، ثم انتقل إلى الصفحة 2 – يظهر النص نفسه فورًا. هذا مثال كامل وظيفيًا على **إنشاء حقل نصي في PDF** مع حقل مكرر.

---

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**الناتج المتوقع:** ملف اسمه `output.pdf` يحتوي على صفحتين. كلا الصفحتين تعرضان نفس المربع النصي القابل للتحرير بعنوان “Sample”. تعديل أحدهما يحدّث الآخر فورًا.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو أردت الحقل على *أكثر* من صفحتين؟

ما عليك سوى تكرار خطوات الاستنساخ‑والإضافة لكل صفحة إضافية. يبقى كائن البيانات الأساسي هو نفسه، لذا تبقى جميع الويدجتات متزامنة.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### كيف أغيّر المظهر (الخط، الحدود، الخلفية)؟

كل `Widget` يمتلك طرق `SetBorderColor`، `SetBorderWidth`، و `SetBackgroundColor`. يمكنك أيضًا تعيين سلسلة المظهر الافتراضي (`DA`) للتحكم في الخط والحجم.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### هل يمكن جعل الحقل للقراءة فقط بعد أن يملأه المستخدم؟

نعم. اضبط علم `ReadOnly` على الحقل بعد جمع البيانات، أو بدّل ذلك بناءً على سير العمل الخاص بك.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### ماذا عن ملفات PDF التي تحتوي بالفعل على نموذج؟

إذا كان المستند يحتوي بالفعل على AcroForm، فإن `doc.GetForm()` سيعيده ببساطة. يمكنك حينها إضافة حقول جديدة دون إزعاج الحقول الموجودة. فقط احرص على استخدام أسماء حقول فريدة.

---

## نصائح للمشاريع الواقعية

- **نمط التسمية:** أضف بادئة لأسماء الحقول مع رقم الصفحة أو القسم (مثلاً `invoice_customer_name`) لتجنب التضارب.  
- **التحقق:** استخدم إجراءات JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) إذا احتجت إلى تحقق من جانب العميل.  
- **الأداء:** عند التعامل مع ملفات PDF كبيرة، استدعِ `doc.Lock()` قبل العمليات الجماعية لتقليل عبء الإدخال/الإخراج.  
- **إمكانية الوصول:** عيّن خاصية `AlternateName` حتى يتمكن قارئ الشاشة من وصف الحقل.

---

## الخلاصة

لقد **أنشأنا حقل نصي في PDF**، وأظهرنا كيفية **تكرار حقل نموذج PDF** عبر الصفحات، وبيّنّا أبسط طريقة لـ **إضافة مربع نص إلى نموذج PDF** باستخدام C#. الكود الكامل القابل للتنفيذ موجود أعلاه، ويمكنك توسيعه بإضافة تنسيقات، تحقق، أو صفحات إضافية حسب الحاجة.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة قائمة منسدلة (`ChoiceField`) أو عنصر توقيع، أو استكشف كيفية تسطيح النموذج بعد إدخال البيانات لأغراض الأرشفة. يوفر لك PDFTron SDK (أو أي مكتبة مماثلة) اللبنات الأساسية—خيالك هو ما يحدد الشكل النهائي.

إذا واجهت أي مشكلة، اترك تعليقًا أدناه أو راجع الوثائق الرسمية للمكتبة؛ فهي مليئة بأمثلة تكمل ما غطينا هنا. برمجة سعيدة، ولتظل نماذجك دائمًا متزامنة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج وصفحات](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [إضافة حقل نموذج في مستند PDF باستخدام Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [إضافة حقل نموذج في مستند PDF باستخدام Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}