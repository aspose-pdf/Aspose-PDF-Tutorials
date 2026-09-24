---
category: general
date: 2026-03-03
description: إنشاء ملف PDF مع صفحات وإضافة حقول نموذج PDF من نوع مربع نص باستخدام
  Aspose.PDF في C#. تعلم كيفية إضافة مربع نص، إنشاء حقل نموذج PDF، وإضافة صفحات متعددة
  إلى ملف PDF بسرعة.
draft: false
keywords:
- create pdf with pages
- add text box pdf
- how to add textbox
- create pdf form field
- add multiple pages pdf
language: ar
og_description: إنشاء ملف PDF مع صفحات باستخدام Aspose.PDF. يوضح هذا الدليل كيفية
  إضافة حقول نصية إلى PDF، وإنشاء حقل نموذج PDF، وإضافة صفحات متعددة إلى PDF باستخدام
  C#.
og_title: إنشاء PDF باستخدام Pages – دليل C# الكامل
tags:
- pdf
- csharp
- aspose
title: إنشاء PDF مع الصفحات وحقول مربعات النص – دليل C# الكامل
url: /ar/net/programming-with-forms/create-pdf-with-pages-and-text-box-fields-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF مع صفحات وحقول صندوق النص – دليل C# الكامل

هل احتجت يومًا إلى **إنشاء pdf مع صفحات** تسمح للمستخدمين بكتابة ملاحظات؟ ربما تبني بوابة عقود، نموذج ملاحظات، أو استبيان بسيط. في هذه الحالة، ستحتاج إلى PDF لا يحتوي فقط على عدة صفحات بل يحتوي أيضًا على صندوق نص قابل لإعادة الاستخدام. خبر سار: باستخدام Aspose.PDF for .NET يمكنك فعل كل ذلك ببضع أسطر فقط.

في هذا البرنامج التعليمي سنستعرض **كيفية إضافة عناصر تحكم textbox**، وتسجيل **إنشاء حقل نموذج pdf**، وأخيرًا **إضافة صفحات متعددة pdf** لإنتاج مستند تفاعلي مصقول. لا إطالة—فقط الكود الذي يمكنك نسخه‑لصقه، بالإضافة إلى “السبب” وراء كل قرار. في النهاية ستحصل على PDF باسم `TextBoxTwoWidgets.pdf` يحتوي على نفس صندوق النص في صفحتين منفصلتين.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)  
- حزمة Aspose.PDF for .NET عبر NuGet (`Install-Package Aspose.PDF`)  
- فهم أساسي لفئات C# وإدارة الكائنات (سنستخدم كتلة `using`)  

> **نصيحة محترف:** إذا كنت تستخدم Visual Studio، فعّل *nullable reference types* لتجربة أنظف، لكن ذلك ليس ضروريًا لهذا المثال.

## الخطوة 1: إنشاء PDF مع صفحات – إعداد المستند

أول شيء عليك فعله هو إنشاء مستند PDF فارغ. فكر في فئة `Document` كدفتر ملاحظات جديد؛ ستضيف صفحات إليه لاحقًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

using (var pdfDocument = new Document())
{
    // The document is now ready for pages and form fields.
```

*لماذا نستخدم كتلة `using`؟* لأنها تضمن تحرير جميع الموارد غير المُدارة (مقابض الملفات، مخازن الذاكرة) فور الانتهاء، مما يمنع التسرب—وذلك مهم خاصةً عند توليد العديد من ملفات PDF في خدمة ويب.

## الخطوة 2: إضافة حقل صندوق نص PDF إلى الصفحة الأولى

الآن بعد أن أصبح المستند موجودًا، نحتاج إلى صفحة واحدة على الأقل لاستضافة حقل النموذج. سنضيف **صفحتين** لأننا نريد ظهور نفس صندوق النص في كلٍ منهما.

```csharp
    // Add the first page
    var firstPage = pdfDocument.Pages.Add();

    // Add the second page (will host the widget copy)
    var secondPage = pdfDocument.Pages.Add();

    // Create a TextBoxField on the first page
    var notesField = new TextBoxField(
        firstPage,
        new Rectangle(50, 700, 300, 750))   // left, bottom, right, top
    {
        Name = "Notes",
        Value = "Type here..."
    };
```

إحداثيات المستطيل تتبع نظام إحداثيات PDF (الأصل في الزاوية السفلية‑اليسرى). خاصية `Name` هي المعرف الداخلي؛ ستستخدمها لاحقًا عندما تسترجع القيمة بعد أن يملأ المستخدم النموذج.

## الخطوة 3: كيفية إضافة عنصر Widget لصندوق النص في صفحة ثانية

الـ *widget* هو التمثيل البصري لحقل النموذج. بشكل افتراضي يحصل الحقل على widget واحد في الصفحة التي تم إنشاؤه فيها. إذا أردت نفس صندوق النص في صفحة أخرى، تضيف annotation widget آخر.

```csharp
    // Place a second widget of the same field on the second page
    notesField.AddWidgetAnnotation(
        secondPage,
        new Rectangle(50, 500, 300, 550));
```

لاحظ إحداثيات Y المختلفة—هذا يضع صندوق النص الثاني أدنى في الصفحة. يمكنك بالطبع استخدام نفس المستطيل إذا أردت وضعًا متماثلًا.

## الخطوة 4: إنشاء حقل نموذج PDF وتسجيله

على الرغم من أننا قد أنشأنا بالفعل `notesField`، لا يزال علينا تسجيله في مجموعة `Form` الخاصة بالمستند. هذه الخطوة تجعل الحقل جزءًا من بنية النموذج التفاعلية.

```csharp
    // Register the field with the PDF form
    pdfDocument.Form.Add(notesField, notesField.Name);
```

إذا تخطيت هذا السطر، سيظهر صندوق النص بصريًا لكنه لن يُحفظ كحقل نموذج، مما يعني أن محتواه لن يُرسل عند معالجة الـ PDF.

## الخطوة 5: حفظ الـ PDF والتحقق من وجود صفحات متعددة

أخيرًا، نكتب المستند إلى القرص. اسم الملف اختياري؛ فقط تأكد من وجود المجلد ومن أن تطبيقك يملك صلاحية الكتابة.

```csharp
    // Save the resulting PDF
    pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
}
```

عند فتح `TextBoxTwoWidgets.pdf` في Adobe Acrobat Reader، سترى صفحتين، كل واحدة تحتوي على نفس صندوق النص “Notes”. اكتب شيئًا في الصفحة الأولى، ثم انتقل إلى الثانية—كلا الحقلين يبقيان مستقلين لأنهما يشتركان في نفس كائن البيانات الأساسي.

### النتيجة المتوقعة

- **الصفحة 1:** صندوق نص عند الإحداثيات (50, 700) مع نص افتراضي “Type here…”.  
- **الصفحة 2:** صندوق نص مماثل موضعه أدنى (50, 500).  
- كلا الصفحتين تنتميان إلى **نموذج PDF واحد** باسم “Notes”.  

يمكنك اختبار النموذج بتصدير البيانات (Acrobat → Tools → Prepare Form → Export Data) وسترى إدخالًا واحدًا لـ `Notes`.

## الاختلافات الشائعة وحالات الحافة

| السيناريو | ما الذي يجب تغييره | السبب |
|----------|-------------------|-------|
| **نص افتراضي مختلف لكل صفحة** | إنشاء كائنين منفصلين من `TextBoxField` بقيم `Name` مختلفة. | يجب أن ينتمي كل widget إلى حقل خاص به ليحمل قيمًا مستقلة. |
| **صندوق نص للقراءة فقط** | تعيين `notesField.ReadOnly = true;` قبل إضافة الـ widget. | يمنع المستخدمين من تعديل الحقل مع الاستمرار في عرض المعلومات. |
| **صندوق نص متعدد الأسطر** | تعيين `notesField.Multiline = true;` وزيادة ارتفاع المستطيل. | يسمح بملاحظات أطول دون الحاجة للتمرير. |
| **PDF محمي بكلمة مرور** | بعد الحفظ، استدعاء `pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AESx128);`. | يحمي المستند مع الحفاظ على حقول النموذج. |

## نصائح محترف للعمل مع نماذج Aspose.PDF

- **إنشاء دفعات:** إذا كنت تحتاج إلى عشرات الـ widgets المتطابقة، استخدم حلقة `foreach` على `pdfDocument.Pages` واستدعِ `AddWidgetAnnotation` داخل الحلقة.  
- **اتفاقيات تسمية الحقول:** استخدم بادئة مثل `txt_` أو `fld_` لتجنب التصادمات عند دمج ملفات PDF لاحقًا.  
- **الأداء:** أعد استخدام كائن `Rectangle` واحد قدر الإمكان؛ المكتبة تنسخ القيم داخليًا، لذا لن تواجه عنق زجاجة في الذاكرة.  

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // 2️⃣ Add two pages – we’ll place a widget on each
            var firstPage = pdfDocument.Pages.Add();
            var secondPage = pdfDocument.Pages.Add();

            // 3️⃣ Define the textbox field (add text box pdf)
            var notesField = new TextBoxField(
                firstPage,
                new Rectangle(50, 700, 300, 750))
            {
                Name = "Notes",
                Value = "Type here..."
            };

            // 4️⃣ Add a second widget on the second page (how to add textbox)
            notesField.AddWidgetAnnotation(
                secondPage,
                new Rectangle(50, 500, 300, 550));

            // 5️⃣ Register the field (create pdf form field)
            pdfDocument.Form.Add(notesField, notesField.Name);

            // 6️⃣ Save the file (add multiple pages pdf)
            pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
        }

        System.Console.WriteLine("PDF created successfully!");
    }
}
```

شغّل البرنامج، افتح الملف الناتج، وسترى بالضبط ما وصفه البرنامج التعليمي.

## الخلاصة

لقد **أنشأنا pdf مع صفحات** يحتوي على عنصر نموذج **إضافة صندوق نص pdf** قابل لإعادة الاستخدام، وأظهرنا **كيفية إضافة widget لصندوق النص** في صفحات متعددة، وسجلنا **إنشاء حقل نموذج pdf** بشكل صحيح. المستند النهائي يثبت أنه يمكنك **إضافة صفحات متعددة pdf** مع الحفاظ على تفاعل النموذج وخفته.

ما الخطوة التالية؟ جرّب إضافة مربعات اختيار، أزرار راديو، أو حتى إجراءات JavaScript لجعل الـ PDF ديناميكيًا حقًا. يمكنك أيضًا استكشاف دمج عدة ملفات PDF من هذا النوع في تقرير واحد—Aspose.PDF يجعل ذلك سهلًا.

هل لديك أسئلة أو حالة استخدام مميزة تريد مشاركتها؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}