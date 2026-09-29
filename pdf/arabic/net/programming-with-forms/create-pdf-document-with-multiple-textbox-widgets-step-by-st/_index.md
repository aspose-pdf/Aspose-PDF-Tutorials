---
category: general
date: 2026-02-12
description: إنشاء مستند PDF وإضافة صفحة PDF فارغة أثناء بناء حقل نموذج – تعلّم كيفية
  إضافة عناصر نصية (textbox) في PDF باستخدام C# بسرعة.
draft: false
keywords:
- create pdf document
- add blank page pdf
- create pdf form field
- how to create pdf form
- how to add textbox pdf
language: ar
og_description: إنشاء مستند PDF بصفحة فارغة والعديد من أدوات النص. اتبع هذا الدليل
  لتعلم كيفية إضافة حقول نصية في PDF باستخدام Aspose.Pdf.
og_title: إنشاء مستند PDF – إضافة عناصر صندوق النص في C#
tags:
- pdf
- csharp
- aspose
- form-fields
title: إنشاء مستند PDF مع عدة أدوات TextBox – دليل خطوة بخطوة
url: /ar/net/programming-with-forms/create-pdf-document-with-multiple-textbox-widgets-step-by-st/
---

الإحداثيات، أضف المزيد من العناصر Widget، وشاهد نموذجك ينبض بالحياة.*"

Then closing shortcodes.

Now ensure we didn't translate any code block placeholders, shortcodes, URLs.

We have image alt and title translated.

Check for any markdown links: none.

Check for any other code fences: placeholders only.

Now produce final content with same structure.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF مع عدة عناصر TextBox – دليل كامل

هل احتجت يوماً إلى **create pdf document** يحتوي على نموذج به أكثر من عنصر TextBox؟ لست وحدك—غالباً ما يسأل المطورون، *“كيف أضيف حقول textbox pdf تظهر في مكانين؟”* الخبر السار هو أن Aspose.Pdf يجعل الأمر سهلًا. في هذا الدليل سنستعرض إنشاء PDF، إضافة صفحة فارغة pdf، بناء حقل نموذج، وأخيراً إظهار **how to add textbox pdf** برمجياً.

سنغطي كل ما تحتاج معرفته: من تهيئة المستند إلى حفظ الملف النهائي. في النهاية ستحصل على PDF جاهز للاستخدام يوضح **how to create pdf form** مع عناصر متعددة، وستفهم التفاصيل الصغيرة التي تجعل النموذج موثوقاً عبر عارضات PDF.

## ما ستحتاجه

- **Aspose.Pdf for .NET** (أي نسخة حديثة؛ الـ API المستخدمة هنا تعمل مع 23.x وما بعدها).  
- بيئة تطوير .NET (Visual Studio، Rider، أو حتى VS Code مع امتداد C#).  
- إلمام أساسي بصياغة C#—لا حاجة لمعرفة عميقة بـ PDF.

إذا كان لديك كل ما سبق، فلنبدأ.

## الخطوة 1: إنشاء مستند PDF – التهيئة وإضافة صفحة فارغة

أول ما نقوم به هو إنشاء كائن **create pdf document** ومنحه مساحة نظيفة. إضافة صفحة فارغة pdf بسيطة كاستدعاء `Pages.Add()`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

public class MultiWidgetExample
{
    public static void Main()
    {
        // Step 1: Create a new PDF document (the canvas)
        using (var pdfDocument = new Document())
        {
            // Step 2: Add a blank page pdf to the document
            var pdfPage = pdfDocument.Pages.Add();

            // The rest of the steps follow...
```

*لماذا هذا مهم:* تمثل فئة `Document` الملف بأكمله. بدون صفحة، لا مكان لوضع حقول النموذج، لذا فإن صفحة pdf الفارغة هي أساس أي نموذج ستبنيه.

## الخطوة 2: إنشاء حقل نموذج PDF – تعريف TextBox يمكنه احتواء عدة عناصر Widget

الآن نقوم بإنشاء **create pdf form field** الفعلي. تُسميه Aspose `TextBoxField`. ضبط `MultipleWidgets = true` يخبر المحرك أن هذا الحقل يمكن أن يظهر أكثر من مرة.

```csharp
            // Step 3: Create a TextBox field that supports multiple widgets
            var multiWidgetTextBox = new TextBoxField(
                pdfPage,
                new Rectangle(50, 700, 250, 730)); // position on the first page
            multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
            multiWidgetTextBox.Value = "First widget";
```

*نصيحة احترافية:* إحداثيات المستطيل تُعبّر بالنقاط (1 pt = 1/72 in). عدّلها لتناسب تخطيطك؛ المثال يضع الصندوق قرب الزاوية العلوية اليسرى.

## الخطوة 3: إضافة العنصر Widget الأول إلى النموذج

بعد تعريف الحقل، نرفعه إلى مجموعة نماذج المستند. هذه هي خطوة **how to add textbox pdf** للعنصر Widget الأساسي.

```csharp
            // Step 4: Add the TextBox field to the form (first widget)
            pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);
```

الوسيط الثالث (`1`) هو فهرس الـ widget—يبدأ من 1 لأن لدينا بالفعل عنصر Widget على الصفحة التي أنشأناها في الخطوة السابقة.

## الخطوة 4: إرفاق عنصر Widget ثانٍ برمجياً – القوة الحقيقية للـ Multiple Widgets

إذا تساءلت يوماً عن **how to create pdf form** التي تتكرر، هنا يحدث السحر. نقوم بإنشاء كائن `WidgetAnnotation` ونضيفه إلى مجموعة `Widgets` الخاصة بالحقل.

```csharp
            // Step 5: Create and attach a second widget programmatically
            var secondWidget = new WidgetAnnotation(
                new Rectangle(300, 700, 500, 730)); // position on the same page
            multiWidgetTextBox.Widgets.Add(secondWidget);
```

*لماذا إضافة عنصر Widget ثانٍ؟* قد يحتاج المستخدمون لملء نفس القيمة في مكانين—مثل حقل “Customer Name” الذي يظهر في أعلى النموذج ثم مرة أخرى في قسم التوقيع. بمشاركة نفس اسم الحقل (`MultiTB`)، أي تعديل في مكان يحدّث الآخر تلقائياً.

## الخطوة 5: حفظ PDF – التحقق من ظهور كلا العنصرين Widget

أخيراً، نكتب المستند إلى القرص. سيحتوي الملف على عنصرين TextBox متزامنين.

```csharp
            // Step 6: Save the PDF with both widgets
            pdfDocument.Save("multiWidget.pdf");
        }
    }
}
```

عند فتح `multiWidget.pdf` في Adobe Acrobat أو Foxit أو حتى عارض PDF بالمتصفح، سترى صندوقي نص بجانب بعضهما. الكتابة في أحدهما تُحدّث الآخر فوراً—دليل على أننا نجحنا في **how to add textbox pdf** مع عدة عناصر Widget.

### النتيجة المتوقعة

- ملف PDF من صفحة واحدة اسمه `multiWidget.pdf`.  
- عنصران TextBox مسميين “First widget”.  
- كلا الصندوقين يشتركان في نفس اسم الحقل، لذا يعكسان محتوى بعضهما البعض.

![إنشاء مستند PDF مع عدة عناصر TextBox](https://example.com/images/multi-widget.png "مثال على إنشاء مستند PDF")

*نص بديل للصورة:* create pdf document showing two textbox widgets

## أسئلة شائعة وحالات خاصة

### هل يمكنني وضع عناصر Widget على صفحات مختلفة؟

بالطبع. فقط أنشئ كائن `Page` جديد للـ widget الثاني واستخدم إحداثياته. سيظل الحقل مرتبطاً لأن الاسم (`"MultiTB"`) يبقى نفسه.

```csharp
var secondPage = pdfDocument.Pages.Add();
var thirdWidget = new WidgetAnnotation(new Rectangle(50, 700, 250, 730));
multiWidgetTextBox.Widgets.Add(thirdWidget);
```

### ماذا لو احتجت قيمة افتراضية مختلفة لكل عنصر Widget؟

خاصية `Value` تنطبق على الحقل بأكمله، لا على كل عنصر Widget منفرد. إذا احتجت قيم افتراضية مميزة، سيتعين عليك إنشاء حقول منفصلة بدلاً من استخدام `MultipleWidgets`.

### هل يعمل هذا مع التوافق PDF/A أو PDF/UA؟

نعم، لكن قد تحتاج إلى ضبط خصائص مستند إضافية (مثال: `pdfDocument.ConvertToPdfA()`) بعد إضافة حقول النموذج. يبقى ربط العناصر Widget دون تغيير.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الجاهز للتنفيذ. فقط ضعّه في مشروع Console، أشر إلى حزمة Aspose.Pdf عبر NuGet، واضغط **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

namespace AsposePdfMultiWidget
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Add a blank page pdf
                var pdfPage = pdfDocument.Pages.Add();

                // Create a TextBox field that can contain multiple widgets
                var multiWidgetTextBox = new TextBoxField(
                    pdfPage,
                    new Rectangle(50, 700, 250, 730));
                multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
                multiWidgetTextBox.Value = "First widget";

                // Add the TextBox field to the form (first widget)
                pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);

                // Create and attach a second widget programmatically
                var secondWidget = new WidgetAnnotation(
                    new Rectangle(300, 700, 500, 730));
                multiWidgetTextBox.Widgets.Add(secondWidget);

                // Save the PDF with both widgets
                pdfDocument.Save("multiWidget.pdf");
            }
        }
    }
}
```

شغّل البرنامج وافتح `multiWidget.pdf`. سترى صندوقي نص متزامنين—بالضبط ما أردت عندما سألت **how to create pdf form** مع عدة مدخلات.

## ملخص وخطوات مستقبلية

لقد استعرضنا للتو كيفية **create pdf document**، إضافة **blank page pdf**، تعريف **create pdf form field**، وأخيراً الإجابة على **how to add textbox pdf** التي تشارك البيانات. الفكرة الأساسية هي أن اسم حقل واحد يمكن عرضه عدة مرات، مما يمنحك تخطيطات نماذج مرنة دون كتابة كود إضافي.

هل تريد التقدم أكثر؟ جرّب هذه الأفكار:

- **Style the textbox** – غيّر لون الحدود أو الخلفية أو الخط باستخدام خصائص `TextBoxField`.  
- **Add validation** – استخدم إجراءات JavaScript (`TextBoxField.Actions.OnValidate`) لفرض الصيغ.  
- **Combine with other fields** – أضف مربعات اختيار، أزرار راديو، أو توقيعات رقمية لبناء نموذج كامل المميزات.  
- **Export form data** – استدعِ `pdfDocument.Form.ExportFields()` لاستخراج مدخلات المستخدم كـ JSON أو XML.

كل من هذه الأفكار يبني على الأساس نفسه الذي غطيناه، لذا أنت في موقع جيد لإنشاء نماذج PDF متقدمة للفواتير، العقود، الاستبيانات، أو أي احتياج تجاري آخر.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقاً أدناه أو استكشف وثائق Aspose.Pdf للمزيد من التفاصيل. تذكر، أفضل طريقة لإتقان توليد PDF هي التجربة—فعدل الإحداثيات، أضف المزيد من العناصر Widget، وشاهد نموذجك ينبض بالحياة.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}