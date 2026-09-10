---
category: general
date: 2026-02-20
description: كيفية إضافة صندوق نص إلى PDF في C# – تعلم إنشاء حقل نموذج PDF، تحويل
  Word إلى نموذج PDF، وحفظ مستند PDF المُعدل بسرعة.
draft: false
keywords:
- how to add text box pdf
- create pdf form field
- convert word to pdf form
- save edited pdf document
language: ar
og_description: كيف تضيف مربع نص إلى PDF؟ يوضح لك هذا الدليل كيفية إنشاء حقول نموذج
  PDF، وتحويل Word إلى نموذج PDF، وحفظ مستندات PDF المعدلة باستخدام C#.
og_title: كيفية إضافة صندوق نص إلى PDF – دليل كامل لمطوري C#
tags:
- PDF
- C#
- Document Automation
title: كيفية إضافة مربع نص إلى PDF – إنشاء حقل نموذج PDF وحفظ مستند PDF المُعدل
url: /ar/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة مربع نص PDF – دليل C# كامل

هل تساءلت يوماً **كيفية إضافة مربع نص PDF** إلى ملفاتك دون قضاء ساعات في أدوات الواجهة الرسومية؟ لست وحدك. تحويل مستند Word إلى نموذج PDF تفاعلي هو ما يحتاجه العديد من المطورين، خاصةً عند بناء بوابات onboarding أو مولدات تقارير آلية.

في هذا الدرس سنستعرض العملية بالكامل: إنشاء حقل نموذج PDF، تحويل مستند Word إلى نموذج PDF، وأخيرًا **حفظ مستند PDF المعدل**. في النهاية ستحصل على مقتطف C# قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET—بدون الحاجة إلى واجهة مستخدم خارجية.

## ما ستتعلمه

- تحميل ملف `.docx` وتحويله إلى كائن مستند PDF.  
- **إنشاء كائنات حقل نموذج PDF** برمجياً، بما في ذلك مربع نص.  
- إضافة عدة واجهات (تمثيلات بصرية) لنفس الحقل على صفحات مختلفة.  
- **حفظ مستند PDF المعدل** مرة أخرى على القرص.  

لا حاجة لأي واجهة مستخدم طرف ثالث؛ كل شيء يتم عبر الشيفرة، مما يتيح لك أتمتة سير العمل في وظائف دفعية، خدمات ويب، أو تطبيقات سطح مكتب.

> **نصيحة احترافية:** إذا كنت تستخدم مكتبة Aspose.PDF for .NET (الكود أدناه يفترض ذلك)، ستحصل على دعم أصلي لتحويل Word إلى PDF ومعالجة النماذج دون تبعيات إضافية.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث (أو .NET Framework 4.7.2+) | المكتبة التي نستخدمها تستهدف بيئات تشغيل حديثة. |
| Aspose.PDF for .NET (NuGet `Aspose.PDF`) | توفر `Document`، `FormField`، `TextBoxField`، إلخ. |
| ملف Word تجريبي (`input.docx`) | هذا هو المصدر الذي سنحوّله إلى نموذج PDF. |
| معرفة أساسية بـ C# | ستفهم مقتطفات الشيفرة دون الحاجة إلى شرح عميق. |

> **ملاحظة:** نفس المفاهيم تنطبق على مكتبات PDF أخرى (iTextSharp، PDFSharp). استبدل الفئات وفقاً للمكتبة التي تفضلها.

## الخطوة 1 – تحميل مستند Word وتحويله إلى PDF

أولاً نحتاج إلى كائن `Document` يمثل نسخة PDF من ملف Word الخاص بنا. يمكن لـ Aspose.PDF قراءة `.docx` مباشرة، لذا لا توجد خطوة تحويل منفصلة.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Drawing;

// Load the Word document and automatically convert it to PDF
Document doc = new Document("YOUR_DIRECTORY/input.docx");

// Verify that the conversion succeeded
Console.WriteLine($"Document loaded with {doc.Pages.Count} page(s).");
```

**لماذا هذا مهم:** التحويل المبكر يمنحنا لوحة PDF يمكننا إرفاق حقول النموذج عليها. كما يضمن أن أبعاد الصفحات تتطابق مع PDF النهائي، وهو أمر أساسي لتحديد موقع مربع النص بدقة.

## الخطوة 2 – إنشاء حقل نموذج مربع نص في الصفحة الأولى

الآن سنضيف عنصر **مربع نص PDF** يمكن للمستخدمين ملؤه. إحداثيات المستطيل تُعبّر بالنقاط (1/72 بوصة). في هذا المثال يقع الصندوق بالقرب من أعلى‑يسار الصفحة 1.

```csharp
// Define the rectangle where the text box will appear (x‑min, y‑min, x‑max, y‑max)
Rectangle headerRect = new Rectangle(50, 750, 200, 770);

// Create the visual widget (TextBoxField) and give it a logical name
TextBoxField headerBox = new TextBoxField(doc.Pages[1], headerRect)
{
    PartialName = "Header" // This is the field’s internal identifier
};

// Add the widget to the document’s form collection and assign a field name
FormField headerField = doc.Form.Add(headerBox, "HeaderField");

// Optional: set default text or appearance properties
headerBox.Value = "Enter title here";
headerBox.Border = new Border(headerBox) { Width = 1, Color = Color.Black };
```

> **لماذا نستخدم `PartialName` واسم حقل منفصل:** `PartialName` هو المعرف الذي يستخدمه عارض PDF، بينما الاسم الذي تمرره إلى `Add` (`"HeaderField"`) هو المفتاح الذي ستشير إليه عند استخراج البيانات لاحقاً.

### توضيح بصري

![How to add text box PDF example](/images/add-textbox-pdf.png "Screenshot showing the text box placed on the first page of the PDF")

*النص البديل:* *كيفية إضافة مربع نص PDF – توضيح لمربع نص موضع على صفحة PDF.*

## الخطوة 3 – إضافة واجهة ثانية لنفس الحقل في الصفحة 2

يمكن لحقول نموذج PDF أن تحتوي على تمثيلات بصرية متعددة (widgets). هذا مفيد عندما تريد نقطة إدخال بيانات واحدة تظهر في عدة صفحات—مثل رأس يتكرر.

```csharp
// Define a second rectangle on page 2 (different position)
Rectangle secondRect = new Rectangle(50, 50, 200, 70);

// Attach the same logical field to page 2
headerField.AddWidget(secondRect, doc.Pages[2]);
```

**لماذا هذا مفيد:** يمكن للمستخدمين ملء الحقل مرة واحدة، وتظهر القيمة في كل واجهة تلقائياً. يقلل ذلك من التكرار ويحافظ على نظافة النموذج.

## الخطوة 4 – (اختياري) تحويل محتوى Word إضافي إلى عناصر نموذج PDF

إذا كان ملف Word الأصلي يحتوي على نواقل أخرى (مثال: `{{Name}}`)، يمكنك استبدالها برمجياً بحقول نموذج. إليك نمط سريع:

```csharp
// Example: replace a placeholder text with a new text box field
foreach (Page page in doc.Pages)
{
    foreach (TextFragment fragment in page.TextFragments)
    {
        if (fragment.Text.Contains("{{Name}}"))
        {
            // Remove placeholder
            fragment.Text = fragment.Text.Replace("{{Name}}", string.Empty);

            // Create a new text box at the placeholder’s location
            Rectangle nameRect = fragment.Rectangle;
            TextBoxField nameBox = new TextBoxField(page, nameRect) { PartialName = "Name" };
            doc.Form.Add(nameBox, "NameField");
        }
    }
}
```

> **حالة حافة:** بعض ملفات PDF تخزن النص كقطعات منفصلة لكل حرف، لذا قد تحتاج إلى دمج القطعات أو استخدام خوارزمية بحث أكثر قوة للمستندات المعقدة.

## الخطوة 5 – حفظ مستند PDF المعدل

أخيراً، اكتب ملف PDF المعدل مرة أخرى على القرص. يمكنك اختيار أي صيغة إخراج يدعمها المكتبة (PDF، XPS، إلخ). هنا نلتزم بـ PDF.

```csharp
// Save the final PDF that now contains interactive text boxes
doc.Save("YOUR_DIRECTORY/output.pdf");

Console.WriteLine("PDF saved successfully at YOUR_DIRECTORY/output.pdf");
```

**ما يجب التحقق منه:** افتح `output.pdf` في Adobe Acrobat Reader أو أي عارض PDF يدعم النماذج. يجب أن ترى مربعين نص متطابقين—واحد في الصفحة 1 والآخر في الصفحة 2—كلاهما قابل للتحرير ومتزامن.

## مثال كامل يعمل

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه ولصقه في تطبيق Console. يتضمن جميع الخطوات السابقة بالإضافة إلى معالجة أخطاء بسيطة.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load Word and convert to PDF
            Document doc = new Document("YOUR_DIRECTORY/input.docx");
            Console.WriteLine($"Loaded document with {doc.Pages.Count} page(s).");

            // 2️⃣ Create a text box on page 1
            Rectangle rect1 = new Rectangle(50, 750, 200, 770);
            TextBoxField txtBox = new TextBoxField(doc.Pages[1], rect1)
            {
                PartialName = "Header"
            };
            FormField headerField = doc.Form.Add(txtBox, "HeaderField");
            txtBox.Value = "Enter header";
            txtBox.Border = new Border(txtBox) { Width = 1, Color = Color.DarkGray };

            // 3️⃣ Add a second widget on page 2
            Rectangle rect2 = new Rectangle(50, 50, 200, 70);
            headerField.AddWidget(rect2, doc.Pages[2]);

            // 4️⃣ (Optional) Replace placeholders with fields – omitted for brevity

            // 5️⃣ Save the edited PDF
            string outputPath = "YOUR_DIRECTORY/output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved successfully at {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**النتيجة المتوقعة:** بعد تشغيل البرنامج، يحتوي `output.pdf` على مربعين نص متزامنين معنونين بـ “Header”. أي نص يُدخل في أحد الصناديق يظهر تلقائياً في الصندوق الآخر.

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني إضافة مربع نص إلى PDF موجود (بدون مصدر Word؟)* | نعم—تجاوز خطوة تحويل Word وحمّل PDF مباشرة (`new Document("file.pdf")`). |
| *ماذا لو كان فهرس الصفحة خارج النطاق؟* | تُطلق Aspose.PDF استثناء `IndexOutOfRangeException`. تحقق دائماً من `doc.Pages.Count` قبل الوصول إلى `doc.Pages[n]`. |
| *هل يجب ضبط خاصية `ReadOnly` للحقل؟* | فقط إذا أردت منع التحرير. اضبط `txtBox.ReadOnly = true;`. |
| *كيف أستخرج البيانات المدخلة لاحقاً؟* | استخدم `doc.Form["HeaderField"].Value` بعد أن يحفظ المستخدم النموذج. |
| *هل نظام الإحداثيات يبدأ من الزاوية السفلية اليسرى؟* | صحيح—(0,0) هو الزاوية السفلية اليسرى للصفحة. عدّل قيم Y وفقاً لذلك. |

## الخطوات التالية

الآن بعد أن عرفت **كيفية إضافة مربع نص PDF** برمجياً، قد ترغب في استكشاف:

- **إنشاء أنواع حقول نموذج PDF** أخرى غير مربعات النص (مربعات اختيار، أزرار راديو، قوائم منسدلة).  
- **تحويل Word إلى نموذج PDF** مع معالجة تخطيطات أكثر تعقيداً (جداول، صور).  
- **حفظ مستند PDF المعدل** إلى خدمة تخزين سحابي (Azure Blob، AWS S3) لتدفقات عمل موزعة.  
- **التحقق من صحة إدخال النموذج** على الخادم قبل المعالجة.  

كل من هذه المواضيع يبني على الأساس الذي غطيناه هنا، مما يتيح لك إنشاء حلول PDF آلية ومتقدمة بالكامل.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقاً أدناه—دعنا نحل المشكلة معاً.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}