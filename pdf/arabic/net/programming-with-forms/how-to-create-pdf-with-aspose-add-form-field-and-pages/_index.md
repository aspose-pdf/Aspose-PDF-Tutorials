---
category: general
date: 2026-01-02
description: كيفية إنشاء ملف PDF باستخدام Aspose.Pdf في C#. تعلم كيفية إضافة حقل نموذج
  إلى PDF، إضافة صفحات إلى PDF، تضمين مربع نص، وحفظ PDF مع النماذج—كل ذلك في دليل
  واحد.
draft: false
keywords:
- how to create pdf
- add form field pdf
- add pages pdf
- pdf with text box
- save pdf with forms
language: ar
og_description: كيفية إنشاء ملف PDF باستخدام Aspose.Pdf في C#. دليل خطوة بخطوة لإضافة
  حقل نموذج إلى PDF، إضافة صفحات إلى PDF، إدراج مربع نص، وحفظ PDF مع النماذج.
og_title: كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج والصفحات
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج والصفحات
url: /ar/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج وصفحات

هل تساءلت يومًا **كيفية إنشاء PDF** يحتوي على حقول تفاعلية دون أن تشعر بالإحباط؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى مربع نص متعدد الصفحات أو يرغبون في إرفاق نفس حقل النموذج إلى عدة صفحات.  

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ يوضح لك كيفية **add form field PDF**, **add pages PDF**, تضمين **pdf with text box**, وأخيرًا **save PDF with forms**. في النهاية ستحصل على ملف واحد يمكنك فتحه في Acrobat وسترى نفس مربع النص يظهر على ثلاث صفحات مختلفة.

> **نصيحة احترافية:** Aspose.Pdf يعمل مع .NET 6+، .NET Framework 4.6+، وحتى .NET Core. تأكد من أنك قمت بتثبيت حزمة NuGet `Aspose.Pdf` قبل البدء.

## المتطلبات المسبقة

- Visual Studio 2022 (أو أي بيئة تطوير C# تفضلها)
- .NET 6 SDK مثبت
- حزمة NuGet `Aspose.Pdf` (أحدث إصدار حتى عام 2026)
- إلمام أساسي بصياغة C#

إذا كان أي من ذلك غير مألوف لك، فقط قم بتثبيت الـ SDK وإضافة الحزمة – باقي الدليل يفترض أنك مرتاح لفتح مشروع وحدة تحكم.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولاً، أنشئ تطبيق وحدة تحكم جديد:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
dotnet add package Aspose.Pdf
```

الآن افتح `Program.cs` وأضف عبارات `using` المطلوبة في الأعلى:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

هذه المساحات الاسمية تمنحك الوصول إلى الفئات `Document` و `Page` و `TextBoxField` التي سنستخدمها.

## الخطوة 2: إنشاء مستند PDF جديد

نحتاج إلى لوحة فارغة قبل أن نضيف أي حقول إليها. تمثل الفئة `Document` ملف PDF بالكامل.

```csharp
// Step 2: Initialize a new PDF document
using (var pdfDocument = new Document())
{
    // All further steps will live inside this block
}
```

إحاطة المستند بكتلة `using` تضمن تحرير الموارد تلقائيًا بمجرد الانتهاء من حفظ الملف.

## الخطوة 3: إضافة الصفحة الأولية

PDF بدون صفحات هو، في الواقع، لا شيء. لنضيف الصفحة الأولى حيث سيظهر مربع النص في البداية.

```csharp
// Step 3: Add the first page (the field will be placed on this page initially)
Page firstPage = pdfDocument.Pages.Add();
```

طريقة `Pages.Add()` تُرجع كائن `Page` يمكننا الإشارة إليه لاحقًا عند تحديد موضع الأدوات.

## الخطوة 4: تعريف حقل TextBox متعدد الصفحات

هذا هو جوهر الحل: حقل `TextBoxField` واحد سنرفقه إلى عدة صفحات. فكر في الحقل كحاوية للبيانات، وكل أداة (widget) كتمثيل بصري على صفحة محددة.

```csharp
// Step 4: Create a TextBox field that will span multiple pages
var multiPageTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 650))
{
    PartialName = "MultiPageComment",
    Value = "Enter comment here..."
};
```

- **PartialName** هو المعرف الداخلي؛ يجب أن يكون فريدًا داخل النموذج.  
- **Value** يحدد النص الافتراضي الذي سيشاهده المستخدمون.  
- `Rectangle` يحدد موقع الأداة (اليسار، الأسفل، اليمين، الأعلى) بالنقاط.

## الخطوة 5: إضافة صفحات إضافية وإرفاق الأدوات

الآن سنتأكد من أن المستند يحتوي على ثلاث صفحات على الأقل ثم نرفق نفس مربع النص إلى الصفحات 2 و 3 باستخدام `AddWidgetAnnotation`.

```csharp
// Ensure the document has at least three pages
pdfDocument.Pages.Add(); // page 2
pdfDocument.Pages.Add(); // page 3

// Attach the same field to the new pages (widgets)
multiPageTextBox.AddWidgetAnnotation(pdfDocument.Pages[2], new Rectangle(100, 600, 300, 650));
multiPageTextBox.AddWidgetAnnotation(pdfDocument.Pages[3], new Rectangle(100, 600, 300, 650));
```

كل استدعاء ينشئ أداة بصرية على الصفحة المستهدفة لكنه يرتبط بحقل `TextBoxField` الأصلي. تعديل مربع النص في أي صفحة سيُحدّث القيمة تلقائيًا في جميع الأماكن — ميزة مفيدة لنماذج المراجعة أو العقود.

## الخطوة 6: تسجيل الحقل في مجموعة النماذج

إذا تخطيت هذه الخطوة، لن يظهر الحقل في هيكل النموذج التفاعلي للـ PDF، وسيتجاهله Acrobat.

```csharp
// Step 6: Add the field to the form collection
pdfDocument.Form.Add(multiPageTextBox, "MultiPageComment");
```

الوسيط الثاني هو اسم الحقل كما سيظهر في القاموس الداخلي للنموذج داخل الـ PDF. الحفاظ على تناسق الأسماء يساعد عند استخراج البيانات برمجيًا لاحقًا.

## الخطوة 7: حفظ الـ PDF على القرص

أخيرًا، احفظ المستند إلى ملف. اختر مجلدًا لديك صلاحية كتابة فيه؛ في هذا المثال سنستخدم مجلدًا فرعيًا يسمى `output`.

```csharp
// Step 7: Save the PDF with the multi‑page textbox
pdfDocument.Save("output/MultiWidgetTextBox.pdf");
```

عند فتح `output/MultiWidgetTextBox.pdf` في Adobe Acrobat Reader، سترى نفس مربع النص على الصفحات 1‑3. الكتابة في أي نسخة تُحدّثها جميعًا — بالضبط ما كنا نسعى لتحقيقه.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في `Program.cs`. يَتَجَمَّع ويعمل كما هو.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

namespace PdfFormDemo
{
    internal class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add the first page (the field will be placed on this page initially)
                Page firstPage = pdfDocument.Pages.Add();

                // Step 3: Create a TextBox field that will span multiple pages
                var multiPageTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 650))
                {
                    PartialName = "MultiPageComment",
                    Value = "Enter comment here..."
                };

                // Step 4: Ensure the document has at least three pages
                pdfDocument.Pages.Add(); // page 2
                pdfDocument.Pages.Add(); // page 3

                // Step 5: Attach the same field to additional pages (widgets)
                multiPageTextBox.AddWidgetAnnotation(pdfDocument.Pages[2], new Rectangle(100, 600, 300, 650));
                multiPageTextBox.AddWidgetAnnotation(pdfDocument.Pages[3], new Rectangle(100, 600, 300, 650));

                // Step 6: Add the field to the form collection
                pdfDocument.Form.Add(multiPageTextBox, "MultiPageComment");

                // Step 7: Save the PDF with the multi‑page textbox
                pdfDocument.Save("output/MultiWidgetTextBox.pdf");
            }
        }
    }
}
```

### النتيجة المتوقعة

- **ثلاث صفحات** في الـ PDF.  
- **مربع نص واحد** يُعرض على كل صفحة عند الإحداثيات (100, 600)‑(300, 650).  
- **محتوى متزامن**: تعديل مربع النص في أي صفحة يُحدّث البقية.  
- الملف يُحفظ باسم `output/MultiWidgetTextBox.pdf`.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت مربع النص على أكثر من ثلاث صفحات؟

فقط أضف المزيد من الصفحات باستخدام `pdfDocument.Pages.Add()` وكرر استدعاء `AddWidgetAnnotation` لكل صفحة جديدة. يبقى كائن الحقل كما هو، لذا تدفع فقط تكلفة إنشاء الأدوات الإضافية.

### هل يمكنني تغيير مظهر كل أداة (الخط، اللون) بشكل مستقل؟

نعم. بعد إنشاء أداة، يمكنك استرجاعها عبر `multiPageTextBox.Widgets` وتعديل خصائص `Appearance` الخاصة بها. ومع ذلك، ضع في اعتبارك أن تغيير مظهر أداة واحدة لن يؤثر على الأخرى إلا إذا قمت بتعديل كل أداة على حدة.

```csharp
var widget = multiPageTextBox.Widgets[1]; // second widget (page 2)
widget.Appearance.NormalGraphicsState.Font = FontRepository.FindFont("Helvetica");
widget.Appearance.NormalGraphicsState.FontSize = 12;
widget.Appearance.NormalGraphicsState.TextColor = Color.GetBlue();
```

### كيف يمكنني استخراج القيمة المدخلة لاحقًا؟

عندما يملأ المستخدم الـ PDF وتستلم الملف مرة أخرى، استخدم Aspose.Pdf لقراءة حقل النموذج:

```csharp
var filledDoc = new Document("filled.pdf");
var field = (TextBoxField)filledDoc.Form["MultiPageComment"];
Console.WriteLine($"User entered: {field.Value}");
```

### ماذا عن توافق PDF/A؟

إذا كنت بحاجة إلى توافق PDF/A‑1b، اضبط `pdfDocument.ConvertToPdfA()` قبل الحفظ. سيظل حقل النموذج يعمل، لكن بعض عارضات PDF/A قد تقيد التحرير. اختبر ذلك مع جمهورك المستهدف.

## نصائح وممارسات أفضل

- **استخدم أسماء حقول ذات معنى** – تجعل استخراج البيانات سهلًا.  
- **تجنب تداخل الأدوات** – قد يُظهر Acrobat أخطاء “field name already exists” إذا احتلت أداتان نفس المساحة على نفس الصفحة.  
- **اضبط `ReadOnly = false`** فقط عندما تريد فعلاً أن يحرر المستخدمون؛ وإلا قم بقفل الحقل لمنع التغييرات غير المقصودة.  
- **حافظ على تناسق إحداثيات المستطيل** عبر الصفحات للحصول على مظهر موحد، ما لم تكن ترغب عمدًا في أحجام مختلفة.

## الخلاصة

أنت الآن تعرف **كيفية إنشاء PDF** باستخدام Aspose.Pdf يحتوي على حقل نموذج قابل لإعادة الاستخدام يمتد عبر عدة صفحات. باتباع الخطوات السبع — تهيئة المستند، إضافة الصفحات، تعريف `TextBoxField`، إرفاق الأدوات، تسجيل الحقل، وحفظه — يمكنك بناء ملفات PDF تفاعلية متقدمة دون الحاجة إلى مصممي نماذج من طرف ثالث.

بعد ذلك، جرّب توسيع هذا النمط: أضف مربعات اختيار، قوائم منسدلة، أو حتى توقيعات رقمية. جميع هذه العناصر يمكن إرفاقها إلى عدة صفحات باستخدام نفس تقنية إرفاق الأدوات — وبالتالي ستتمكن من **add form field PDF**, **add pages PDF**, و **save PDF with forms** في قاعدة شفرة واحدة قابلة للصيانة.

برمجة سعيدة، ولتكن ملفات PDF الخاصة بك دائمًا تفاعلية بقدر خيالك!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}