---
category: general
date: 2026-01-15
description: أضف صفحات إلى PDF باستخدام Aspose PDF للغة C#. تعلّم كيفية إضافة مربع
  نص، وكيفية إضافة حقل، وإنشاء مستند PDF باستخدام Aspose في دقائق.
draft: false
keywords:
- add pages to pdf
- how to add textbox
- how to add field
- create pdf document aspose
language: ar
og_description: أضف صفحات إلى PDF بسرعة باستخدام Aspose PDF للغة C#. يوضح هذا الدرس
  كيفية إضافة مربع نص وحقل أثناء إنشاء مستند PDF باستخدام Aspose.
og_title: إضافة صفحات إلى PDF باستخدام Aspose – دليل C# الكامل
tags:
- Aspose.PDF
- C#
- PDF forms
title: إضافة صفحات إلى PDF باستخدام Aspose – دليل C# الكامل
url: /ar/net/programming-with-pdf-pages/add-pages-to-pdf-with-aspose-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة صفحات إلى PDF باستخدام Aspose – دليل C# كامل

هل تساءلت يومًا **كيف تضيف صفحات إلى PDF** عندما تقوم بإنشاء مولد تقارير أو أداة أتمتة عقود؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما تظهر الصفحة الأولى لكن الصفحة الثانية تختفي في الهواء.  

في هذا الدرس سنستعرض **مثالًا كاملاً وقابلًا للتنفيذ** لا يضيف فقط صفحات إلى PDF بل يُظهر أيضًا **كيفية إضافة صندوق نص**, **كيفية إضافة حقل**, وأخيرًا **إنشاء مستند PDF باستخدام Aspose** يعمل في أي بيئة .NET. لا إطالة، فقط الشيفرة الدقيقة التي يمكنك نسخ‑لصقها، بالإضافة إلى شرح كل سطر حتى لا تظل تتساءل لاحقًا.

> **المتطلبات المسبقة** – .NET 6+ (أو .NET Framework 4.6+), Visual Studio 2022 (أو أي بيئة تطوير تفضّلها), ورخصة صالحة لـ Aspose.PDF for .NET (الإصدار التجريبي المجاني يكفي للاختبار).  

إذا كنت جاهزًا، لننطلق مباشرة.

![مثال على إضافة صفحات إلى PDF](add_pages_to_pdf.png "لقطة شاشة تُظهر PDF بصفحتين وصندوق نص متعدد الودجت – إضافة صفحات إلى PDF")

## الخطوة 1 – إضافة صفحات إلى PDF

أول شيء تحتاجه هو لوحة فارغة. في مصطلحات Aspose هذا هو كائن `Document`. بمجرد حصولك عليه، يمكنك البدء في رش الصفحات عليه.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Geometry;

// Create a fresh PDF document – this is where we’ll add pages.
Document pdfDocument = new Document();

// Add the first page (page numbers start at 1)
Page firstPage = pdfDocument.Pages.Add();

// Add a second page – now we have two pages to work with.
Page secondPage = pdfDocument.Pages.Add();
```

**لماذا هذا مهم:** طريقة `Pages.Add()` تُعيد كائن `Page` يمكنك لاحقًا الإشارة إليه لوضع الودجتات أو النص أو الصور. إضافة الصفحات مسبقًا يبسط منطق التخطيط لأنك تعرف بالضبط أين سيقع كل عنصر.

## الخطوة 2 – كيفية إضافة صندوق نص (متعدد الودجت)

*صندوق النص* في نموذج PDF هو **حقل** يمكن أن يظهر في أكثر من صفحة. يُطلق على ذلك حقل *متعدد الودجت*. فكر فيه كصندوق إدخال واحد يظهر في الصفحة 1 والصفحة 2، ويشارك نفس القيمة.

```csharp
// Define the rectangle where the textbox will appear on the first page.
Rectangle firstRect = new Rectangle(100, 700, 300, 720);

// Create the TextBoxField and give it a meaningful name.
TextBoxField multiWidgetField = new TextBoxField(pdfDocument.Pages[1], firstRect)
{
    Name = "MultiWidget",
    // Optional: set default text so you see something when you open the PDF.
    Value = "Enter your comment here..."
};

// Add a second widget (appearance) of the same field on the second page.
Rectangle secondRect = new Rectangle(100, 600, 300, 620);
multiWidgetField.AddWidget(secondPage, secondRect);
```

**الشرح:**  
- `new TextBoxField(pdfDocument.Pages[1], firstRect)` يربط الحقل بالصفحة 1 باستخدام الإحداثيات التي زوّدت بها.  
- `AddWidget(secondPage, secondRect)` ينسخ التمثيل البصري إلى الصفحة 2 مع الحفاظ على مشاركة البيانات الأساسية.  
- يجب أن يكون اسم الحقل **فريدًا** عبر المستند؛ وإلا ستطرح Aspose استثناءً.

## الخطوة 3 – كيفية إضافة الحقل إلى مجموعة النماذج

إنشاء الحقل ليس كافيًا؛ عليك تسجيله في مجموعة نماذج المستند. هذه الخطوة تجعل صندوق النص تفاعليًا عندما يُفتح PDF في Acrobat أو أي عارض PDF يدعم النماذج.

```csharp
// Register the multi‑widget textbox with the document's form.
pdfDocument.Form.Add(multiWidgetField, "MultiWidget");
```

**نصيحة:** الوسيط الثاني (`"MultiWidget"`) هو *اسم الحقل المستعار*. يمكن أن يكون هو نفسه `Name` لكن يمكنك أيضًا استخدام اسم عرض أكثر ودية إذا رغبت.

## الخطوة 4 – حفظ PDF – إنشاء مستند PDF باستخدام Aspose

الآن بعد أن وضعت الصفحات وصندوق النص في مكانه، كل ما عليك هو كتابة الملف إلى القرص. هذه هي اللحظة التي يكتمل فيها خطوة **إنشاء مستند PDF باستخدام Aspose**.

```csharp
// Choose a folder that exists on your machine.
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "textbox_multi.pdf");

// Save the document – the file will contain two pages and a shared textbox.
pdfDocument.Save(outputPath);

Console.WriteLine($"PDF saved successfully to {outputPath}");
```

عند فتحك للملف `textbox_multi.pdf` ستلاحظ صفحتين، كل واحدة تحتوي على نفس صندوق النص. الكتابة في أحدهما تُحدّث الآخر تلقائيًا—تمامًا ما يُفترض أن يفعله حقل متعدد الودجت.

## مثال كامل يعمل (جاهز للنسخ‑اللصق)

فيما يلي البرنامج بالكامل، جاهز للترجمة. يتضمن جميع عبارات `using`، معالجة الأخطاء، وتعليقات تشرح “السبب” وراء كل عملية.

```csharp
// ------------------------------------------------------------
// Full example: add pages to PDF, add a multi‑widget textbox,
// and save the document using Aspose.Pdf for .NET.
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Geometry;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document.
        Document pdfDocument = new Document();

        // 2️⃣ Add two pages – this satisfies the “add pages to pdf” requirement.
        Page firstPage = pdfDocument.Pages.Add();
        Page secondPage = pdfDocument.Pages.Add();

        // 3️⃣ Create a textbox field on the first page.
        Rectangle firstRect = new Rectangle(100, 700, 300, 720);
        TextBoxField multiWidgetField = new TextBoxField(pdfDocument.Pages[1], firstRect)
        {
            Name = "MultiWidget",
            Value = "Enter your comment here..."
        };

        // 4️⃣ Add the same textbox appearance to the second page.
        Rectangle secondRect = new Rectangle(100, 600, 300, 620);
        multiWidgetField.AddWidget(secondPage, secondRect);

        // 5️⃣ Register the field with the form collection.
        pdfDocument.Form.Add(multiWidgetField, "MultiWidget");

        // 6️⃣ Save the PDF – “create PDF document Aspose” step.
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "textbox_multi.pdf");

        try
        {
            pdfDocument.Save(outputPath);
            Console.WriteLine($"✅ PDF saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Failed to save PDF: {ex.Message}");
        }
    }
}
```

### ما يمكن توقعه

- **صفحتان** تظهران في الملف النهائي.  
- كل صفحة تُظهر **صندوق نص** بعنوان “Enter your comment here…”.  
- تعديل صندوق النص في صفحة واحدة يُحدّث الآخر فورًا (بفضل تنفيذ متعدد الودجت).  

إذا فتحت الـ PDF في Adobe Acrobat Reader، ستلاحظ تمييز حقول النموذج. جرّب كتابة “Hello world” في الصفحة 1—الصفحة 2 ستعكس نفس النص دون أي كود إضافي.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني إضافة أكثر من ودجتين؟* | بالتأكيد. استدعِ `AddWidget` بقدر ما تحتاج، مع تمرير `Page` و`Rectangle` مختلفين في كل مرة. |
| *ماذا لو احتجت إلى خط أو لون مختلف؟* | بعد إنشاء `TextBoxField`، عيّن خاصية `DefaultAppearance` (مثال: `multiWidgetField.DefaultAppearance = new AppearanceCharacteristics { Font = FontRepository.FindFont("Helvetica"), FontSize = 12, ForegroundColor = Color.Black };`). |
| *هل يظل الحقل قابلاً للتحرير بعد تسطيح الـ PDF؟* | لا. عملية التسطيح تدمج المظهر مع محتوى الصفحة، مما يجعل الحقل للقراءة فقط. استخدم `pdfDocument.FlattenPages()` فقط عندما تنتهي من تفاعلات النموذج. |
| *هل أحتاج إلى رخصة لـ Aspose؟* | النسخة التجريبية مجانية للتطوير والاختبار، لكنها تضيف علامة مائية. للإنتاج، اشترِ رخصة لإزالة العلامة المائية وإتاحة جميع الميزات. |
| *هل يمكنني استخدام هذا الكود في .NET Core؟* | نعم. الـ API متطابقة عبر .NET Framework و .NET Core و .NET 5/6+. ما عليك سوى الإشارة إلى حزمة NuGet `Aspose.PDF`. |

## الخلاصة

غطّينا كل ما تحتاجه **لإضافة صفحات إلى PDF**, **كيفية إضافة صندوق نص**, **كيفية إضافة حقل**, وأخيرًا **إنشاء مستند PDF باستخدام Aspose** جاهز للاستخدام الفعلي. المقتطف أعلاه يُعد أساسًا قويًا—يمكنك الآن توسيعه بإضافة صور، جداول، أو حتى توقيعات رقمية.

ما الخطوة التالية؟ جرّب إضافة **حقل خانة اختيار** في صفحة ثالثة، جرب **مواضع ودجت مختلفة**, أو انتقل إلى **Aspose.PDF Cloud** إذا كنت تفضّل نهج REST‑ful. السماء هي الحد، ومع Aspose لديك محرك موثوق تحت الغطاء.

برمجة سعيدة، ولتظهر ملفات PDF دائمًا كما تريد!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}