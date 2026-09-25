---
category: general
date: 2026-04-10
description: إنشاء مستند PDF باستخدام C# مع مثال واضح. تعلم كيفية إضافة صفحات متعددة
  إلى PDF، إضافة حقل صندوق نص، كيفية إضافة عنصر واجهة (widget)، وحفظ PDF مع النموذج.
draft: false
keywords:
- create pdf document c#
- add multiple pages pdf
- save pdf with form
- how to add widget
- add text box field
language: ar
og_description: إنشاء مستند PDF باستخدام C# بسرعة. يوضح هذا الدليل كيفية إضافة صفحات
  متعددة إلى PDF، إضافة حقل صندوق نص، كيفية إضافة عنصر واجهة، وحفظ PDF مع النموذج.
og_title: إنشاء مستند PDF باستخدام C# – دليل شامل لإنشاء نموذج متعدد الصفحات
tags:
- C#
- PDF
- Form handling
title: إنشاء مستند PDF باستخدام C# – دليل خطوة بخطوة للنماذج متعددة الصفحات
url: /ar/net/programming-with-forms/create-pdf-document-c-step-by-step-guide-to-multi-page-forms/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF باستخدام C# – دليل خطوة بخطوة للنماذج متعددة الصفحات

هل تساءلت يومًا كيف **تنشئ مستند PDF باستخدام C#** يمتد لعدة صفحات ويحتوي على حقول تفاعلية؟ ربما تقوم بإنشاء مولد فواتير، نموذج تسجيل، أو تقرير بسيط يمكن للمستخدمين ملؤه لاحقًا. في هذا الدرس سنستعرض العملية بالكامل – من تهيئة PDF، إضافة صفحات متعددة، إدراج حقل صندوق نص، إرفاق تعليقات توضيحية من نوع widget، وأخيرًا **حفظ PDF مع بيانات النموذج**. لا إطالة، مجرد مثال عملي يمكنك نسخه ولصقه وتشغيله اليوم.

سنضيف أيضًا نصائح عملية مثل *كيفية إضافة widget* بشكل صحيح ولماذا قد ترغب في إعادة استخدام حقل عبر الصفحات. في النهاية ستحصل على ملف `multibox.pdf` يعمل ويظهر صندوق نص مشترك عبر صفحتين.

## المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.7 أو أعلى) – أي نسخة حديثة من runtime تعمل.
- مكتبة معالجة PDF توفر الفئات `Document`، `TextBoxField`، و `WidgetAnnotation`. يستخدم المثال أدناه مكتبة **Aspose.PDF for .NET** الشهيرة، لكن المفاهيم قابلة للتطبيق على iTextSharp، PdfSharp أو غيرها.
- Visual Studio 2022 أو أي بيئة تطوير تفضلها.
- إلمام أساسي بـ C# – لا تحتاج إلى معرفة عميقة بداخلية PDF، فقط استدعاءات الـ API.

> **نصيحة محترف:** إذا لم تقم بتثبيت المكتبة بعد، نفّذ الأمر `dotnet add package Aspose.PDF` من الطرفية.

## الخطوة 1: إنشاء مستند PDF باستخدام C# – تهيئة الـ Document

أولاً، نحتاج إلى لوحة فارغة. كائن `Document` يمثل ملف PDF بالكامل.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Create a new PDF document
using (var document = new Document())
{
    // The rest of the code lives inside this using block
}
```

لماذا نغلف الـ document داخل جملة `using`؟ لأنها تضمن تحرير جميع الموارد غير المُدارة، وتكتب الملف إلى القرص عند استدعاء `Save`. هذا النمط هو الطريقة الموصى بها للعمل مع ملفات PDF في C#.

## الخطوة 2: إضافة صفحات متعددة إلى PDF

ملف PDF بدون صفحات يكون، حسنًا، غير مرئي. لنضيف صفحتين – الأولى ستستضيف الحقل نفسه، والثانية ستحمل widget يشير إلى نفس الحقل.

```csharp
// Step 2: Add two pages – one for the field, one for the widget
var firstPage = document.Pages.Add();
var secondPage = document.Pages.Add();
```

> **لماذا صفحتان؟** عندما تريد أن يظهر نفس الإدخال في عدة صفحات، تنشئ *حقلًا* مرة واحدة ثم تُشير إليه باستخدام *تعليقات توضيحية من نوع widget* في الصفحات الأخرى. هذا يبقي البيانات متزامنة تلقائيًا.

فيما يلي مخطط بسيط يوضح العلاقة (النص البديل يتضمن الكلمة المفتاحية الأساسية لتسهيل الوصول).

![Create PDF document C# diagram showing field on page 1 and widget on page 2](image.png)

*النص البديل: مخطط إنشاء مستند PDF باستخدام C# يوضح حقل صندوق نص مشترك عبر صفحتين.*

## الخطوة 3: إضافة حقل صندوق نص إلى PDF الخاص بك

الآن نضع صندوق نص في الصفحة الأولى. المستطيل يحدد موقعه وحجمه (الإحداثيات بوحدات النقاط، 72 نقطة = 1 بوصة).

```csharp
// Step 3: Create a text box field on the first page and give it a shared name and value
var sharedTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 620));
sharedTextBox.PartialName = "MultiBox";
sharedTextBox.Value = "Shared value";
```

- **PartialName** هو المعرف الذي سيشاركه كل من الحقل وأي widget.
- تعيين `Value` هنا يعطي الحقل مظهرًا افتراضيًا، سيظهر أيضًا في صفحة الـ widget.

## الخطوة 4: كيفية إضافة Widget – الإشارة إلى نفس الحقل في صفحة أخرى

الـ widget هو في الأساس عنصر مرئي يشير إلى الحقل الأصلي. بإعادة استخدام نفس المستطيل، يبدو الـ widget مطابقة للحقل، لكنه موجود في صفحة مختلفة.

```csharp
// Step 4: Create a widget annotation on the second page that references the same field rectangle
var sharedWidget = new WidgetAnnotation(secondPage, sharedTextBox.Rect);
sharedWidget.PartialName = sharedTextBox.PartialName;
secondPage.Annotations.Add(sharedWidget);
```

> **خطأ شائع:** نسيان إضافة الـ widget إلى `secondPage.Annotations`. بدون هذا السطر لا يظهر الـ widget، رغم وجود الكائن.

## الخطوة 5: تسجيل الحقل وحفظ PDF مع النموذج

الآن نخبر مجموعة النماذج في المستند عن الحقل الجديد. طريقة `Add` تستقبل كائن الحقل واسمه. أخيرًا، نكتب الملف إلى القرص.

```csharp
// Step 5: Register the field with the document form
document.Form.Add(sharedTextBox, "MultiBox");

// Step 6: Save the PDF containing the multi‑page field
document.Save("YOUR_DIRECTORY/multibox.pdf");
```

عند فتح `multibox.pdf` في Adobe Acrobat أو أي عارض PDF يدعم النماذج، ستلاحظ وجود صندوق النص نفسه في الصفحتين. تعديل النص في إحدى الصفحات يحدث التحديث فورًا في الأخرى لأنهما يشتركان في نفس الحقل الأساسي.

## مثال كامل يعمل

نجمع كل شيء معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Step 1: Create a new PDF document
        using (var document = new Document())
        {
            // Step 2: Add two pages – one for the field, one for the widget
            var firstPage = document.Pages.Add();
            var secondPage = document.Pages.Add();

            // Step 3: Create a text box field on the first page and give it a shared name and value
            var sharedTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 620));
            sharedTextBox.PartialName = "MultiBox";
            sharedTextBox.Value = "Shared value";

            // Step 4: Create a widget annotation on the second page that references the same field rectangle
            var sharedWidget = new WidgetAnnotation(secondPage, sharedTextBox.Rect);
            sharedWidget.PartialName = sharedTextBox.PartialName;
            secondPage.Annotations.Add(sharedWidget);

            // Step 5: Register the field with the document form
            document.Form.Add(sharedTextBox, "MultiBox");

            // Step 6: Save the PDF containing the multi‑page field
            document.Save("multibox.pdf");
        }

        Console.WriteLine("PDF created successfully! Check the file 'multibox.pdf'.");
    }
}
```

### النتيجة المتوقعة

- **صفحتان**: الصفحة 1 تُظهر صندوق نص بالنص الافتراضي “Shared value”.  
- **الصفحة 2** تعكس نفس الصندوق. كتابة نص في إحداهما تُحدّث الأخرى فورًا.  
- حجم الملف صغير (بضع كيلوبايت) لأننا أضفنا فقط كائنات نموذج بسيطة.

## الأسئلة المتكررة وحالات الحافة

### هل يمكن إضافة أكثر من widget لنفس الحقل؟

بالتأكيد. فقط كرّر خطوة إنشاء الـ widget لكل صفحة إضافية، مع إعادة استخدام نفس `PartialName`. هذا مفيد للعقود متعددة الصفحات حيث يظهر حقل التوقيع نفسه في أسفل كل صفحة.

### ماذا لو أردت حجمًا أو موقعًا مختلفًا في الصفحة الثانية؟

يمكنك إنشاء `Rectangle` جديد للـ widget مع الحفاظ على نفس `PartialName`. ستظل قيمة الحقل متزامنة، لكن التخطيط البصري يمكن أن يختلف بين الصفحات.

### هل يعمل هذا مع ملفات PDF محمية بكلمة مرور؟

نعم، لكن عليك فتح المستند باستخدام كلمة المرور الصحيحة أولًا:

```csharp
var document = new Document("protected.pdf", "ownerPassword");
```

ثم تابع بنفس الخطوات. المكتبة ستحافظ على التشفير عند استدعاء `Save`.

### كيف يمكن استرجاع القيمة المدخلة برمجيًا؟

بعد أن يملأ المستخدم النموذج وتعيد تحميل الـ PDF مرة أخرى:

```csharp
var loaded = new Document("multibox.pdf");
var field = loaded.Form["MultiBox"] as TextBoxField;
Console.WriteLine("User entered: " + field.Value);
```

### ماذا لو أردت تسطيح النموذج (جعل الحقول غير قابلة للتحرير)?

استدعِ `document.Form.Flatten()` قبل الحفظ. هذا يحول الحقول التفاعلية إلى محتوى ثابت، وهو مفيد للفواتير النهائية.

## الخاتمة

لقد **أنشأنا مستند PDF باستخدام C#** يمتد لعدة صفحات، أضفنا حقل صندوق نص قابل لإعادة الاستخدام، عرضنا **كيفية إضافة widget**، وأخيرًا **حفظنا PDF مع بيانات النموذج**. الفكرة الأساسية هي أن حقلًا واحدًا يمكن عرضه في أي عدد من الصفحات عبر الـ widgets، مما يحافظ على إدخال المستخدم متسقًا عبر المستند بأكمله.

هل أنت مستعد للتحدي التالي؟ جرّب:

- إضافة **مربع اختيار** أو **قائمة منسدلة** باستخدام نفس النمط.  
- تعبئة الـ PDF ببيانات من قاعدة بيانات بدلًا من القيمة الصلبة.  
- تصدير الـ PDF المملوء إلى مصفوفة بايت للتحميل عبر HTTP في API مبني على ASP.NET Core.

لا تتردد في التجربة، كسر الأشياء، ثم إصلاحها – فهذه هي الطريقة لتصبح محترفًا في توليد PDF باستخدام C#. إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو راجع الوثائق الرسمية للمكتبة لمزيد من التفاصيل.

برمجة سعيدة، واستمتع بإنشاء ملفات PDF أذكى!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}