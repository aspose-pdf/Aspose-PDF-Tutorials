---
category: general
date: 2026-03-01
description: كيفية إنشاء ملف PDF باستخدام مكتبة Aspose PDF. تعلم كيفية إضافة حقل إلى
  مجموعة، إضافة عنصر واجهة، وحفظ ملف PDF باستخدام كود C# واضح.
draft: false
keywords:
- how to create pdf
- add field to collection
- how to add widget
- add textbox page
- save pdf aspose
language: ar
og_description: كيفية إنشاء ملف PDF باستخدام مكتبة Aspose PDF. يوضح هذا الدليل كيفية
  إضافة حقل إلى مجموعة، إضافة عنصر واجهة مستخدم، وحفظ ملف PDF باستخدام C#.
og_title: كيفية إنشاء PDF باستخدام Aspose – إضافة حقل إلى المجموعة
tags:
- Aspose.PDF
- C#
- PDF Forms
title: كيفية إنشاء PDF باستخدام Aspose – إضافة حقل إلى مجموعة
url: /ar/net/programming-with-forms/how-to-create-pdf-with-aspose-add-field-to-collection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء PDF باستخدام Aspose – إضافة حقل إلى المجموعة

هل تساءلت يومًا **كيف تنشئ PDF** برمجيًا وتحتاج إلى حقل نموذج يظهر في عدة صفحات؟ لست وحدك. في العديد من تطبيقات الأعمال نحتاج إلى إنشاء فواتير أو عقود أو تقارير تسمح للمستخدم بملء نفس المعلومات في عدة صفحات. الخبر السار؟ Aspose.PDF يجعل الأمر سهلًا للغاية.

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ بلغة C# **يضيف حقل صندوق نص إلى مجموعة**، ويضع عنصرًا مرئيًا ثانيًا في صفحة أخرى، وأخيرًا **يحفظ ملف PDF**. في النهاية ستفهم ليس فقط *ما* يتم فعله بل أيضًا *لماذا* يتم ذلك في كل سطر، وستحصل على نمط قابل لإعادة الاستخدام لأي نموذج متعدد العناصر تحتاج إلى بنائه.

---

## ما ستقوم ببنائه

- مستند PDF جديد يتم إنشاؤه بالكامل في الذاكرة.  
- حقل `TextBoxField` باسم **MultiWidget** موجود في الصفحة 1.  
- عنصر مرئي ثاني لنفس الحقل في الصفحة 2 (ليرى المستخدم نفس الإدخال مرتين).  
- تسجيل الحقل في مجموعة نماذج المستند (`add field to collection`).  
- حفظ النتيجة على القرص باستخدام طريقة Aspose‑PDF `Save` (`save pdf aspose`).  

- لا خدمات خارجية، ولا تكوين معقد—فقط بضع أسطر من كود C# نظيف.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| **Aspose.PDF for .NET** (v23.12 أو أحدث) | يوفر الفئات `Document` و `Forms` و `Rectangle` المستخدمة أدناه. |
| **.NET 6+** (أو .NET Framework 4.6+) | المكتبة تستهدف .NET Standard، لذا أي بيئة تشغيل حديثة تعمل. |
| **Visual Studio 2022** (أو محرّرك المفضّل) | يجعل تشغيل وتصحيح العينة سهلًا. |
| **إذن كتابة** إلى مجلد الإخراج | مطلوب لـ `pdfDocument.Save(...)`. |

إذا لم تقم بتثبيت Aspose.PDF بعد، نفّذ:

```bash
dotnet add package Aspose.PDF
```

هذا كل شيء—لا حاجة لحزم NuGet إضافية.

---

## كيفية إنشاء PDF – نظرة عامة

فيما يلي البرنامج الكامل القابل للتنفيذ. لا تتردد في نسخه ولصقه في تطبيق console واضغط **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // Step 1: Create a new PDF document (blank canvas)
        using (var pdfDocument = new Document())
        {
            // Step 2: Add a TextBox field (first widget) to page 1
            var textBoxField = new TextBoxField(
                pdfDocument.Pages[1],
                new Rectangle(100, 600, 300, 620));

            // Step 3: Give the field a logical name – this is how we reference it later
            textBoxField.PartialName = "MultiWidget";

            // Step 4: Add a second widget for the same field on page 2
            var secondWidget = textBoxField.AddWidgetAnnotation(
                pdfDocument.Pages[2],
                new Rectangle(100, 500, 300, 520));

            // Step 5: Register the field (with both widgets) in the document's form collection
            pdfDocument.Form.Add(textBoxField, "MultiWidget");

            // Optional: Set a default value so you can see something when you open the PDF
            textBoxField.Value = "Enter your text here";

            // Step 6: Save the resulting PDF to disk
            pdfDocument.Save("multiWidget.pdf");
        }

        Console.WriteLine("PDF created successfully – check the file 'multiWidget.pdf' in the output folder.");
    }
}
```

> **النتيجة المتوقعة:** افتح *multiWidget.pdf* في أي عارض PDF. سترى صندوق نص في الصفحة 1 وصندوقًا مماثلًا في الصفحة 2. اكتب في أي من الصندوقين—سيتم عكس التغيير تلقائيًا لأن كلا العنصرين المرئيين يشتركان في نفس الحقل الأساسي.

---

## شرح خطوة بخطوة

### 1. إنشاء مستند PDF (كيفية إنشاء PDF)

```csharp
using (var pdfDocument = new Document())
```

فئة `Document` هي الكائن الجذري. فكر فيها كدفتر فارغ؛ كل صفحة أو تعليقة أو نموذج تضيفه يعيش داخلها. تغليفه داخل كتلة `using` يضمن تحرير جميع الموارد غير المُدارة بمجرد الانتهاء—ممارسة جيدة، خاصةً عند توليد العديد من ملفات PDF في مهمة دفعة.

### 2. إضافة حقل TextBox – العنصر المرئي الأول (`add textbox page`)

```csharp
var textBoxField = new TextBoxField(
    pdfDocument.Pages[1],
    new Rectangle(100, 600, 300, 620));
```

- **`pdfDocument.Pages[1]`** – تقوم Aspose بإنشاء الصفحة 1 تلقائيًا إذا لم تكن موجودة، لذا يمكننا الإشارة إليها مباشرة.  
- **`Rectangle`** – يحدد موقع العنصر المرئي (X/Y أسفل اليسار) وحجمه (X/Y أعلى اليمين). الإحداثيات بوحدات النقاط (1 بوصة = 72 نقطة).  
- **لماذا TextBox؟** – هو أكثر عنصر نموذج شائع لإدخال المستخدم الحر، مثالي للأسماء أو التعليقات أو المعرفات.

### 3. تسمية الحقل (`add field to collection`)

```csharp
textBoxField.PartialName = "MultiWidget";
```

ال*اسم الجزئي* هو المعرف المنطقي الذي ستستخدمه لاحقًا عندما تريد قراءة أو تعيين قيمة الحقل برمجيًا. اختيار اسم واضح وفريد يجنب التصادمات عندما يكون لديك العديد من الحقول في نفس المستند.

### 4. إضافة عنصر مرئي ثاني (`how to add widget`)

```csharp
var secondWidget = textBoxField.AddWidgetAnnotation(
    pdfDocument.Pages[2],
    new Rectangle(100, 500, 300, 520));
```

ال**widget** هو التمثيل البصري لحقل في صفحة محددة. من خلال استدعاء `AddWidgetAnnotation` نخبر Aspose، "أريد أن تظهر نفس البيانات الأساسية في الصفحة 2 أيضًا". يمكن أن يختلف المستطيل، مما يتيح لك وضع الصندوق الثاني في أي مكان تحتاجه.

> **نصيحة احترافية:** إذا كنت بحاجة إلى العنصر المرئي في أكثر من صفحتين، ما عليك سوى تكرار استدعاء `AddWidgetAnnotation` مع فهرس الصفحة المناسب.

### 5. تسجيل الحقل في مجموعة النماذج (`add field to collection`)

```csharp
pdfDocument.Form.Add(textBoxField, "MultiWidget");
```

مجموعة `Form` هي القائمة الرئيسية في PDF لجميع العناصر التفاعلية. إضافة الحقل هنا يجعلها جزءًا من قاموس AcroForm الخاص بالمستند، وهو ما يبحث عنه قارئو PDF عند عرض حقول النماذج.

### 6. (اختياري) تعيين قيمة افتراضية

```csharp
textBoxField.Value = "Enter your text here";
```

توفير عنصر نائب يساعد المستخدمين النهائيين على فهم غرض الحقل. ليس إلزاميًا، لكنه يحسن تجربة المستخدم.

### 7. حفظ PDF (`save pdf aspose`)

```csharp
pdfDocument.Save("multiWidget.pdf");
```

يدعم Aspose.PDF العديد من صيغ الإخراج (PDF/A، PDF/E، تدفق، مصفوفة بايت). هنا نبقي الأمر بسيطًا ونكتب مباشرة إلى نظام الملفات. إذا كنت بحاجة لإرسال PDF عبر HTTP، فقط استدعِ `Save(Stream)` بدلاً من ذلك.

---

## الأسئلة الشائعة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **هل أحتاج إلى إنشاء الصفحات يدويًا قبل إضافة العناصر المرئية؟** | لا. الوصول إلى `pdfDocument.Pages[1]` أو `[2]` ينشئ الصفحات تلقائيًا إذا لم تكن موجودة. |
| **ماذا لو أردت أن يكون الحقل للقراءة فقط؟** | عيّن `textBoxField.ReadOnly = true;` قبل الحفظ. |
| **كيف يمكنني تغيير المظهر (الخط، الحدود، اللون)؟** | استخدم `textBoxField.DefaultAppearance` أو أنشئ كائن `Appearance` مخصص وعيّنه إلى العنصر المرئي. |
| **هل يمكنني إضافة أكثر من عنصرين مرئيين؟** | بالتأكيد. استدعِ `AddWidgetAnnotation` لكل صفحة إضافية. |
| **هل هذا النهج متوافق مع توافق PDF/A؟** | نعم، لكن قد تحتاج إلى ضبط مستوى توافق المستند (`pdfDocument.Convert(new PdfFormat.PdfA_1b))`) قبل إضافة العناصر المرئية. |
| **ماذا لو احتجت إلى ملء الحقل بعد إنشاء PDF؟** | حمّل PDF لاحقًا باستخدام `new Document("multiWidget.pdf")`، ابحث عن الحقل عبر `pdfDocument.Form["MultiWidget"]`، عيّن `Value`، ثم `Save`. |

---

## ملخص بصري

![مثال على كيفية إنشاء PDF يظهر صندوقين نصيين في صفحات مختلفة](https://example.com/images/multi-widget-screenshot.png "مثال على كيفية إنشاء PDF")

*نص بديل:* **كيفية إنشاء PDF** لقطة شاشة تُظهر حقل صندوق نص في الصفحة 1 والنسخة المكررة من العنصر المرئي في الصفحة 2.

---

## ملخص – ما تم تغطيته

- **كيفية إنشاء PDF** من الصفر باستخدام Aspose.PDF.  
- **إضافة حقل إلى المجموعة** لجعل النموذج جزءًا من قاموس AcroForm.  
- **كيفية إضافة عنصر مرئي** إلى صفحة ثانية، مما يمنح الحقل المنطقي تمثيلين بصريين.  
- **إضافة صفحة صندوق نص** بتحديد `Rectangle` لكل عنصر مرئي.  
- **حفظ PDF Aspose** باستخدام طريقة `Save`، لإنتاج ملف جاهز للاستخدام.

كل هذه الخطوات معًا تمنحك نمطًا قويًا للنماذج متعددة الصفحات. يمكنك الآن تكرار نفس النهج لأزرار الاختيار، أو أزرار الراديو، أو حتى التوقيعات الرقمية—فقط استبدل نوع الحقل.

---

## الخطوات التالية والمواضيع ذات الصلة

- **تنسيق حقول النماذج:** استكشف `FieldAppearance` لتخصيص الخطوط والألوان وأنماط الحدود.  
- **تسطيح النماذج:** عندما تحتاج إلى نسخة غير قابلة للتحرير، استدعِ `pdfDocument.Form.Flatten();`.  
- **دمج ملفات PDF:** استخدم `Document.AppendDocument` لدمج عدة ملفات PDF تحتوي بالفعل على حقول نماذج.  
- **التوقيعات الرقمية:** استكشف `DigitalSignatureField` في Aspose.PDF لإضافة توقيعات معتمدة.  

كل من هذه يبني على الأساسيات التي غطيناها، لذا لا تتردد في التجربة. كلما لعبت أكثر، كلما زادت ثقتك في أتمتة سير عمل PDF.

---

## أفكار ختامية

أصبح لديك الآن مثال شامل ومتكامل حول **كيفية إنشاء PDF** باستخدام Aspose، وكيفية **إضافة حقل إلى المجموعة**، وكيفية **إضافة عنصر مرئي**، وكيفية **حفظ PDF**.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}