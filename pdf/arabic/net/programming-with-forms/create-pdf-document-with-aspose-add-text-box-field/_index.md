---
category: general
date: 2026-03-24
description: إنشاء مستند PDF باستخدام Aspose.PDF في C#. تعلم كيفية إضافة حقل نموذج
  PDF من نوع مربع نص وإضافة حقل نموذج PDF بسرعة.
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: ar
og_description: إنشاء مستند PDF باستخدام Aspose.PDF في C#. يوضح هذا الدليل كيفية إضافة
  حقل نموذج PDF من نوع مربع نص وإضافة حقل نموذج PDF في دقائق.
og_title: إنشاء مستند PDF باستخدام Aspose – إضافة حقل صندوق نص
tags:
- Aspose.PDF
- C#
- PDF Forms
title: إنشاء مستند PDF باستخدام Aspose – إضافة حقل صندوق نص
url: /ar/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF باستخدام Aspose – إضافة حقل صندوق نص

هل احتجت يوماً إلى **إنشاء مستند PDF** برمجياً وتساءلت من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما تحتاج تطبيقاتهم إلى جمع مدخلات المستخدم دون استدعاء مكتبة واجهة مستخدم ثقيلة. الخبر السار؟ باستخدام Aspose.PDF for .NET يمكنك إنشاء PDF، وضع صندوق نص على أي صفحة، وحتى ربط الحقل نفسه بعدة صفحات—كل ذلك في بضع أسطر فقط.

في هذا الدرس سنستعرض العملية بالكامل: من تهيئة الـ PDF، إلى **إضافة حقل صندوق نص PDF**، إلى **تسجيل حقل نموذج PDF**، وأخيراً كيفية التحقق من أن كل شيء يعمل. في النهاية ستعرف **كيفية إنشاء ملفات PDF** تفاعلية، وسترى **كيفية إضافة صندوق نص** يتحكم به تماماً مثل حقول Acrobat الأصلية.

---

## ما ستحتاجه

- **ASP.NET Core** أو أي مشروع .NET 6+ (الكود يعمل أيضاً على .NET Framework 4.6+).  
- حزمة **Aspose.PDF for .NET** عبر NuGet (الإصدار 23.9 أو أحدث).  
- قليل من الخبرة في C#—ليس شيئاً معقداً، فقط الأساسيات.  

إذا كان لديك كل ما سبق، فأنت جاهز للبدء. لا أدوات إضافية، لا خدمات خارجية، فقط كود C# نقي يمكنك لصقه في تطبيق Console وتشغيله.

---

## إنشاء مستند PDF وإضافة حقل نموذج صندوق نص

الخطوة الأولى، كما هو متوقع، هي **إنشاء مستند PDF**. فكر في فئة `Document` كقماش فارغ؛ بمجرد حصولك عليه، يمكنك البدء في رسم الصفحات، الأشكال، والعناصر التفاعلية.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **لماذا هذا مهم:** إنشاء كائن `Document` دون أي صفحات يثير استثناءً في اللحظة التي تحاول فيها وضع عنصر واجهة. إضافة صفحة أولاً يضمن وجود فهرس صفحة صالح (`Pages[1]`) للخطوات التالية.

---

## إضافة حقل نموذج صندوق نص PDF إلى الصفحة 1

الآن بعد أن لدينا صفحة، دعنا **نضيف حقل صندوق نص PDF**. تمثل فئة `TextBoxField` حقلًا منطقيًا واحدًا؛ يمكنك التفكير فيه كـ “اسم” الإدخال الذي قد يظهر في عدة مواضع.

```csharp
// Step 3: Define the rectangle where the textbox will appear (x, y, width, height)
var textBoxRect = new Rectangle(100, 500, 300, 520);

// Step 4: Create the text box field on page 1
var textBoxField = new TextBoxField(document.Pages[1], textBoxRect)
{
    // This logical name is used later when you retrieve the value
    PartialName = "MultiWidget"
};
```

> **نصيحة محترف:** المستطيل يستخدم النقاط (1/72 بوصة). عدّل الإحداثيات لتتناسب مع تخطيطك؛ الأصل (0,0) يقع في الزاوية السفلية‑اليسرى للصفحة.

---

## إنشاء عنصر واجهة ثانٍ في صفحة أخرى

يمكن لحقل منطقي واحد أن يمتلك عدة عناصر واجهة مرئية—مثالي للنماذج متعددة الصفحات. إليك **كيفية إضافة صندوق نص** في صفحة ثانية، مع إعادة استخدام نفس اسم الحقل.

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **لماذا نفعل ذلك:** غالبًا ما يحتاج المستخدمون إلى ملء نفس المعلومات في أقسام مختلفة (مثال: “الاسم” في الأعلى ومرة أخرى في الملخص). بمشاركة الاسم المنطقي، يضمن Aspose تزامن كلا العنصرين.

---

## تسجيل حقل النموذج في الـ PDF

إنشاء كائن الحقل ليس كافيًا؛ يجب إضافته إلى مجموعة النماذج في المستند. هذه هي الخطوة التي **تضيف حقل نموذج PDF** إلى البنية الداخلية.

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **ما يحدث خلف الكواليس:** `Form.Add` يكتب تعريف الحقل إلى قاموس AcroForm، مما يجعل الـ PDF تفاعليًا عند فتحه في Acrobat Reader أو أي عارض PDF يدعم النماذج.

---

## تشغيل البرنامج والتحقق من النتيجة

قم بترجمة وتشغيل تطبيق الـ Console. افتح `MultiWidgetExample.pdf` في Adobe Acrobat (أو أي عارض يدعم النماذج) وسترى صندوقين نصيين متطابقين في الصفحتين 1 و 2. اكتب شيئًا في أحد الصناديق—ستلاحظ تحديث الصندوق الآخر فورًا. هذه هي قوة الحقل المنطقي المشترك.

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

إذا لم تظهر الصناديق، تحقق مرة أخرى من أن المستطيلات داخل حدود الصفحة وأنك حفظت المستند بعد إضافة الحقل.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو أردت مظهرًا مختلفًا في كل صفحة؟

يمكنك تخصيص كل عنصر واجهة بعد إنشائه:

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### هل يمكنني تعيين قيمة افتراضية؟

بالتأكيد—فقط عيّن `Value` قبل الحفظ:

```csharp
textBoxField.Value = "Enter your name here";
```

ستظهر جميع العناصر ذلك النص الافتراضي حتى يقوم المستخدم بتغييره.

### كيف أجعل الحقل إلزاميًا؟

```csharp
textBoxField.Required = true;
```

سيُظهر Acrobat تحذيرًا للمستخدم إذا حاول إرسال النموذج دون ملء الحقل.

### هل يعمل هذا مع توافق PDF/A؟

يدعم Aspose.PDF معايير PDF/A‑1b،‑2b،‑3b. بعد الانتهاء من بناء النموذج، يمكنك التحويل إلى أحد هذه المعايير:

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. احفظه كـ `Program.cs` في مشروع Console .NET، أضف حزمة Aspose.PDF عبر NuGet، ثم شغّله.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var document = new Document();

        // 2️⃣ Add two pages (page 1 will host the first widget, page 2 the second)
        var page1 = document.Pages.Add();
        var page2 = document.Pages.Add();

        // 3️⃣ Define the rectangle for the first widget
        var rect1 = new Rectangle(100, 500, 300, 520);

        // 4️⃣ Create the text box field (logical name = "MultiWidget")
        var textBoxField = new TextBoxField(document.Pages[1], rect1)
        {
            PartialName = "MultiWidget",
            Value = "Sample text",        // optional default value
            Required = true               // makes the field mandatory
        };

        // 5️⃣ Add a second widget on page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}