---
category: general
date: 2026-03-27
description: أضف صفحات إلى ملف PDF وتعلم كيفية إنشاء مستند PDF يحتوي على حقول نموذج.
  اتبع هذا الدرس لإضافة مربع نص إلى PDF وإضافة حقل نموذج إلى PDF باستخدام C#.
draft: false
keywords:
- add pages to pdf
- how to create pdf document
- how to add text box pdf
- add form field to pdf
language: ar
og_description: أضف صفحات إلى ملف PDF وأنشئ مستند PDF يحتوي على حقول نموذج. تعلم كيفية
  إضافة مربع نص إلى PDF وإضافة حقل نموذج إلى PDF في دليل واضح وعملي.
og_title: إضافة صفحات إلى PDF – دليل C# الكامل
tags:
- PDF
- C#
- FormFields
title: إضافة صفحات إلى PDF – دليل خطوة بخطوة لمطوري C#
url: /ar/net/programming-with-pdf-pages/add-pages-to-pdf-step-by-step-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة صفحات إلى PDF – دليل C# كامل

هل احتجت يوماً إلى **إضافة صفحات إلى PDF** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. سواءً كنت تبني مولد عقود أو نموذج ملاحظات بسيط، فإن القدرة على تعديل ملفات PDF برمجيًا هي مهارة أساسية لأي مطور .NET.  

في هذا الدليل سنستعرض العملية بالكامل: من **كيفية إنشاء مستند PDF** في C#، إلى إدراج مربع نص، وأخيرًا **إضافة حقل نموذج إلى PDF** حتى يتمكن المستخدمون من كتابة تعليقاتهم مباشرة في الملف. في النهاية ستحصل على مقتطف شفرة جاهز يمكنك وضعه في مشروعك—بدون قطع مفقودة، ولا اختصارات “انظر الوثائق”.

## ما ستتعلمه

- تهيئة مستند PDF باستخدام مكتبة .NET شائعة (Aspose.Pdf، iTextSharp، أو أي API متوافق).  
- **إضافة صفحات إلى PDF** بشكل ديناميكي وتحديد موضعها بدقة.  
- **كيفية إضافة حقل نصي PDF**، إعطائه أسماء ذات معنى، وتعيين قيم افتراضية.  
- **إضافة حقل نموذج إلى PDF** على صفحات متعددة عن طريق تكرار الودجت.  
- الأخطاء الشائعة (تكرار أسماء الحقول، الودجت غير المرئية) والحلول السريعة.  

### المتطلبات المسبقة

- .NET 6+ (الكود يعمل على .NET Core و .NET Framework على حد سواء).  
- مكتبة PDF تدعم حقول النماذج؛ المثال يستخدم **Aspose.Pdf for .NET**، لكن المفاهيم قابلة للتطبيق على iText7 أو PdfSharp.  
- معرفة أساسية بـ C#—إذا كتبت `Console.WriteLine` من قبل، فأنت جاهز.

> **نصيحة احترافية:** إذا لم تكن لديك مكتبة PDF بعد، احصل على النسخة المجانية من Aspose.Pdf عبر NuGet (`dotnet add package Aspose.Pdf`). فهي تأتي بدعم كامل للحقول ولا تحتاج إلى تبعيات خارجية.

---

## الخطوة 1 – إنشاء مستند PDF وإضافة صفحات

أول ما تحتاجه هو كائن PDF فارغ. فكر في `Document` كدفتر ملاحظات خالٍ سيحمل كل صفحة تضيفها لاحقًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();

// Add the first page
Page firstPage = pdfDocument.Pages.Add();

// Add a second page – you can add as many as you like
Page secondPage = pdfDocument.Pages.Add();
```

**لماذا هذا مهم:**  
إنشاء المستند مسبقًا يمنحك لوحة رسم نظيفة. إضافة الصفحات مباشرةً يضمن وجود مكان لوضع حقول النماذج. إذا تخطيت هذه الخطوة وحاولت إرفاق ودجت إلى صفحة غير موجودة، ستلقي المكتبة استثناء `NullReferenceException`.

---

## الخطوة 2 – تعريف حقل TextBox في الصفحة الأولى

الآن سننشئ **حقل نصي PDF**. إحداثيات المستطيل تُقاس بالنقاط (1 pt ≈ 1/72 in). عدّلها لتتناسب مع تخطيطك.

```csharp
// Step 2: Create a TextBox field on the first page at the desired location
TextBoxField textBoxField = new TextBoxField(firstPage, new Rectangle(100, 100, 200, 120));
```

*شرح:*  
- `firstPage` يخبر المكتبة أين يعيش الودجت في البداية.  
- `Rectangle(100, 100, 200, 120)` يحدد الزاوية السفلية اليسرى (x, y) والزاوية العلوية اليمنى (x, y). جرّب هذه القيم حتى يجلس الصندوق في الموضع المطلوب على الصفحة.

---

## الخطوة 3 – تسمية الحقل، تعيين قيمة افتراضية، وتسجيله

الحقل بدون اسم يكون غير مرئي لقارئ PDF. التسمية تتيح لك استرجاع القيمة لاحقًا عندما يملأ المستخدم النموذج.

```csharp
// Step 3: Give the field a meaningful name and set its initial content
textBoxField.Name = "Comments";
textBoxField.Value = "Enter your feedback here...";

// Register the field with the document's form collection
pdfDocument.Form.Add(textBoxField, "Comments", 1);
```

**لماذا التسمية حاسمة:**  
عند استخراج البيانات لاحقًا (`pdfDocument.Form["Comments"].Value`)، يكون الاسم هو المفتاح. أيضًا، تكرار الأسماء يجعل القارئ يتعامل مع الودجت كحقل واحد، وهو ما قد يكون مفيدًا (كما سنرى) أو مربكًا إذا لم تقصده.

---

## الخطوة 4 – تكرار الودجت في صفحة ثانية

غالبًا ما تحتاج إلى نفس منطقة الإدخال في صفحات متعددة—مثل حقل “التوقيع” الذي يظهر في كل صفحة من العقد. بدلاً من إنشاء حقل جديد، نكرر الودجت.

```csharp
// Step 4: Duplicate the widget on a second page with a different rectangle
textBoxField.AddWidget(secondPage, new Rectangle(120, 150, 220, 170));
```

*ما يحدث خلف الكواليس:*  
`AddWidget` ينشئ تمثيلًا بصريًا آخر لنفس الحقل المنطقي (`Comments`). يرى المستخدم صندوقين، لكن النص الذي يكتبه في أحدهما يظهر في الآخر—مثالي لإدخال بيانات متسقة.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console. ينشئ PDF من صفحتين، يضيف مربع نص في كل صفحة، ويحفظ الملف باسم `FeedbackForm.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add two pages
        Page firstPage = pdfDocument.Pages.Add();
        Page secondPage = pdfDocument.Pages.Add();

        // 3️⃣ Create the TextBox field on the first page
        TextBoxField textBoxField = new TextBoxField(
            firstPage,
            new Rectangle(100, 100, 200, 120) // left, bottom, right, top
        );

        // 4️⃣ Set name and default text
        textBoxField.Name = "Comments";
        textBoxField.Value = "Initial text";

        // 5️⃣ Register the field with the form collection
        pdfDocument.Form.Add(textBoxField, "Comments", 1);

        // 6️⃣ Duplicate the widget on the second page
        textBoxField.AddWidget(
            secondPage,
            new Rectangle(120, 150, 220, 170)
        );

        // 7️⃣ Save the PDF
        pdfDocument.Save("FeedbackForm.pdf");

        Console.WriteLine("PDF generated successfully – check FeedbackForm.pdf");
    }
}
```

**الناتج المتوقع:**  
افتح `FeedbackForm.pdf` في Adobe Acrobat Reader. ستلاحظ وجود صندوقي نص متطابقين يحملان التسمية “Comments”. اكتب شيئًا في الصندوق العلوي؛ سيظهر النص نفسه فورًا في الصندوق السفلي لأنهما يشتركان في نفس اسم الحقل. احفظ الملف، وسيظل النص المدخل محفوظًا.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت قيم افتراضية *مختلفة* في كل صفحة؟

بدلاً من مشاركة نفس الحقل، أنشئ `TextBoxField` ثانيًا باسم فريد (مثلاً `"CommentsPage2"`). ثم أضفه فقط إلى الصفحة الثانية.

### كيف أخفي حدود مربع النص؟

عيّن خاصية `Border`:

```csharp
textBoxField.Border = new Border(BorderStyle.None);
```

### هل يمكن جعل الحقل **إلزاميًا**؟

نعم—عيّن علم `Required`:

```csharp
textBoxField.Required = true;
```

عند محاولة المستخدم إرسال النموذج دون ملء الحقل، سيحذره قارئ PDF.

### ماذا عن توافق PDF/A؟

إذا كنت تحتاج مستند PDF/A‑2b، استدعِ:

```csharp
pdfDocument.Convert(new PdfFormatConversionOptions
{
    ConvertToPdfA = true,
    PdfAStandard = PdfAStandard.PdfA2b
});
```

يجب تنفيذ هذه الخطوة **بعد** إضافة جميع الصفحات والحقول ولكن **قبل** حفظ الملف.

---

## نصائح احترافية للعمل مع حقول النماذج

- **تجنب تكرار الأسماء** إلا إذا كنت تريد مشاركة القيم عمدًا. إعادة استخدام الاسم بطريق الخطأ قد يؤدي إلى كتابة البيانات فوق بعضها.  
- **استخدم وحدات قياس موحدة**—Aspose يستخدم النقاط؛ إذا كنت تمزج مع PDF مُنشأ بـ CSS، تذكر أن 1 pt = 1/72 in.  
- **اختبر في قراء متعددين** (Adobe Reader, Foxit, Chrome). بعض العارضات قد تُظهر الودجت بسمك حدود مختلف.  
- **قفل الحقول** بعد أن يملأها المستخدم (`field.ReadOnly = true`) لمنع التلاعب لاحقًا.

---

## الخلاصة

غطينا كل ما تحتاجه لـ **إضافة صفحات إلى PDF**، **كيفية إنشاء مستند PDF** برمجيًا، **كيفية إضافة حقل نصي PDF**، وأخيرًا **إضافة حقل نموذج إلى PDF** عبر صفحات متعددة. الشيفرة جاهزة للتنفيذ، والشرح يوضح “السبب” وراء كل سطر، مما يمنحك الثقة لتكييف النمط مع سيناريوهات أكثر تعقيدًا—مثل مربعات الاختيار، مجموعات الراديو، أو حتى التوقيعات الرقمية.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة زر **إرسال** يرسل بيانات النموذج إلى خدمة ويب، أو جرب تنسيق مربع النص (خط، لون، متعدد الأسطر). السماء هي الحد عندما تتحكم في ملفات PDF من خلال الكود.

إذا وجدت هذا الدليل مفيدًا، لا تتردد في مشاركته، أو وضع نجمة على المستودع، أو ترك تعليق بأي أسئلة. برمجة سعيدة!  

![مثال لإضافة صفحات إلى pdf يظهر صندوقي نص على صفحتين منفصلتين](https://example.com/images/add-pages-to-pdf.png "مثال لإضافة صفحات إلى pdf")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}