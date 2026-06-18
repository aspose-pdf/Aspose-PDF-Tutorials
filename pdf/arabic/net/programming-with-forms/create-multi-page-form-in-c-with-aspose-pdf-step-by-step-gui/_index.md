---
category: general
date: 2026-06-08
description: إنشاء نموذج متعدد الصفحات في C# باستخدام Aspose.Pdf. تعلم كيفية إضافة
  مربع نص إلى PDF، وإنشاء حقل نموذج PDF، وحفظ PDF المحدث مع أمثلة شفرة واضحة.
draft: false
keywords:
- create multi page form
- add textbox to pdf
- create pdf form field
- how to save pdf
- save updated pdf
language: ar
og_description: إنشاء نموذج متعدد الصفحات في C# باستخدام Aspose.Pdf. يوضح هذا الدليل
  كيفية إضافة مربع نص إلى PDF، وإنشاء حقل نموذج PDF، وحفظ PDF المحدث في دقائق.
og_title: إنشاء نموذج متعدد الصفحات في C# – دليل Aspose.Pdf الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  headline: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  type: TechArticle
- description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  name: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  steps:
  - name: '**Load** the existing PDF.'
    text: '**Load** the existing PDF.'
  - name: '**Create** a `TextBoxField` on the first page – this is our form field.'
    text: '**Create** a `TextBoxField` on the first page – this is our form field.'
  - name: '**Add** a widget annotation on the second page so the same field appears
      there too.'
    text: '**Add** a widget annotation on the second page so the same field appears
      there too.'
  - name: '**Save** the modified document as a new file.'
    text: '**Save** the modified document as a new file.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: إنشاء نموذج متعدد الصفحات في C# باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/programming-with-forms/create-multi-page-form-in-c-with-aspose-pdf-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء نموذج متعدد الصفحات في C# باستخدام Aspose.Pdf – دليل كامل

هل تساءلت يومًا كيف **إنشاء نموذج متعدد الصفحات** في C# دون الخوض في مواصفات PDF منخفضة المستوى؟ لست وحدك. سواء كنت تبني بوابة طلب وظيفة أو معالج إقرار ضريبي، يمكن لنموذج PDF متعدد الصفحات أن يجعل جمع البيانات يبدو سلسًا واحترافيًا.

في هذا الدرس سنستعرض مثالًا واقعيًا **يضيف مربع نص إلى pdf**، **ينشئ حقل نموذج pdf**، وأخيرًا **يحفظ pdf المحدث**. في النهاية ستحصل على نموذج من صفحتين يعمل بالكامل يمكنك إدراجه في أي مشروع .NET.

> **نصيحة احترافية:** Aspose.Pdf يعمل على .NET 6+، .NET Framework 4.6+ وحتى .NET Core، لذا أنت مغطى سواء كنت على Windows أو Linux.

## ما الذي ستحتاجه

- **Aspose.Pdf for .NET** (حزمة NuGet `Aspose.Pdf`).  
- ملف PDF بسيط (`input.pdf`) يحتوي بالفعل على صفحتين على الأقل.  
- Visual Studio 2022 أو أي محرر يدعم C#.  
- مجلد يمكنك القراءة/الكتابة فيه – سنشير إليه بـ `YOUR_DIRECTORY`.

لا توجد تبعيات أخرى. جاهز؟ هيا نبدأ.

![مثال إنشاء نموذج متعدد الصفحات في C# باستخدام Aspose.Pdf](image.png "مثال إنشاء نموذج متعدد الصفحات")

## نظرة عامة على إنشاء نموذج متعدد الصفحات

قبل أن نبدأ بكتابة الكود، دعنا نحدد سير العمل على مستوى عالٍ:

1. **Load** المستند PDF الموجود.  
2. **Create** `TextBoxField` على الصفحة الأولى – هذا هو حقل النموذج الخاص بنا.  
3. **Add** تعليقة widget على الصفحة الثانية بحيث يظهر الحقل نفسه هناك أيضًا.  
4. **Save** المستند المعدل كملف جديد.

كل خطوة معزولة عمدًا حتى يمكنك استبدال الأجزاء (مثل تغيير حجم المستطيل أو إضافة صفحات أخرى) دون كسر الكل.

## الخطوة 1 – تحميل مستند PDF

أول شيء تفعله عند العمل مع أي مكتبة PDF هو فتح ملف المصدر. Aspose.Pdf يجعل ذلك سطرًا واحدًا.

```csharp
// Step 1: Load the PDF document from disk
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document(@"YOUR_DIRECTORY\input.pdf");
```

*لماذا هذا مهم:* تحميل المستند يمنحك الوصول إلى مجموعة `Pages`، وهي المكان الذي سنرفق فيه حقل النموذج والـ widget لاحقًا. إذا لم يُعثر على الملف سيتم رمي استثناء، لذا تأكد من صحة المسار.

## الخطوة 2 – إنشاء حقل نموذج TextBox (إضافة مربع نص إلى pdf)

الآن نحن فعليًا **ننشئ حقل نموذج pdf** – وهو `TextBoxField`. فكر فيه كحاوية للبيانات التي ستحمل ما يكتبه المستخدم.

```csharp
// Step 2: Instantiate a TextBoxField on page 1
Aspose.Pdf.Forms.TextBoxField commentsField = new Aspose.Pdf.Forms.TextBoxField(
    pdfDocument.Pages[1],                                   // target page (1‑based index)
    new Aspose.Pdf.Rectangle(100, 100, 300, 120));         // position & size (LLX, LLY, URX, URY)
```

بعض الملاحظات:

- إحداثيات المستطيل تُعبّر عنها بالنقاط (1 pt = 1/72 in). اضبطها لتناسب تخطيطك.
- `pdfDocument.Pages[1]` تشير إلى الصفحة **الأولى** لأن Aspose يستخدم مجموعة تبدأ من 1.
- بإنشاء الحقل على الصفحة 1 نعطيه أيضًا مظهرًا افتراضيًا، سنعيد استخدامه على الصفحة 2.

## الخطوة 3 – تعيين اسم الحقل والقيمة الأولية

كل حقل نموذج يحتاج إلى معرف. هذه هي السلسلة التي ستشير إليها لاحقًا عند استخراج مدخلات المستخدم.

```csharp
// Step 3: Assign a name and an empty default value
commentsField.Name = "Comments";   // unique field name
commentsField.Value = "";          // start with a blank textbox
```

*لماذا تسميه “Comments”?* إنه وصفي، لكن يمكنك تسميته بأي شيء (`"Address"`, `"PhoneNumber"`). فقط احرص على أن يكون فريدًا عبر كامل PDF؛ الأسماء المكررة تسبب تصادمات في البيانات عند إرسال النموذج.

## الخطوة 4 – إضافة تعليقة Widget على الصفحة الثانية

*الـ widget* هو التمثيل البصري لحقل النموذج على صفحة معينة. بشكل افتراضي الحقل الذي أنشأناه موجود فقط على الصفحة 1. لجعل نفس مربع النص يظهر على الصفحة 2 نضيف تعليقة widget.

```csharp
// Step 4: Place the same TextBoxField on page 2 via a widget
commentsField.Widgets.Add(
    new Aspose.Pdf.Forms.WidgetAnnotation(
        pdfDocument.Pages[2],                               // second page
        new Aspose.Pdf.Rectangle(50, 50, 250, 70)));       // widget rectangle
```

لماذا الـ widget؟ لأن نماذج PDF تفصل بين **تعريف الحقل** (البيانات) و**مظهر الـ widget** (ما يراه المستخدم). إضافة widget تسمح للمستخدم بملء نفس الحقل على صفحات متعددة – وهو مطلب كلاسيكي للنماذج متعددة الصفحات.

### نصيحة للحالات الخاصة

إذا كان PDF المصدر يحتوي على أكثر من صفحتين وتريد مربع النص على كل صفحة، قم بالتكرار عبر `pdfDocument.Pages` وأضف widget لكل واحدة. فقط تذكر أن تحافظ على حجم المستطيل مناسبًا لتخطيط كل صفحة.

## الخطوة 5 – حفظ PDF المحدث (كيفية حفظ pdf)

أخيرًا نحفظ تغييراتنا. Aspose.Pdf يقدم طريقة `Save` بسيطة التي تستبدل أو تنشئ ملفًا جديدًا.

```csharp
// Step 5: Save the updated PDF to a new file
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

*لماذا لا نستبدل `input.pdf`؟* الحفاظ على الأصل دون تعديل يجعل عملية التصحيح أسهل ويسمح لك بمقارنة النتائج قبل/بعد. إذا كنت بحاجة فعلًا لاستبدال المصدر، فقط استدعِ `Save` بنفس المسار.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك البرنامج الكامل الجاهز للتنفيذ.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // Load the existing PDF (make sure the file exists)
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Create a TextBoxField on the first page
        TextBoxField commentsField = new TextBoxField(
            pdfDocument.Pages[1],
            new Rectangle(100, 100, 300, 120));

        // Configure the field
        commentsField.Name = "Comments";
        commentsField.Value = ""; // blank by default

        // Add a widget on the second page so the same field appears there
        commentsField.Widgets.Add(
            new WidgetAnnotation(
                pdfDocument.Pages[2],
                new Rectangle(50, 50, 250, 70)));

        // Save the modified PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        // Optional: inform the user
        System.Console.WriteLine("Multi‑page form created successfully!");
    }
}
```

### النتيجة المتوقعة

عند فتح `output.pdf` في Adobe Acrobat Reader:

- الصفحة 1 تُظهر مربع نص فارغ عند الإحداثيات (100, 100)‑(300, 120).
- الصفحة 2 تُظهر نفس مربع النص عند (50, 50)‑(250, 70).
- كلا الصندوقين يشتركان في **اسم الحقل** `Comments`، مما يعني أن البيانات المدخلة في أي صفحة تتزامن تلقائيًا.

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني إضافة أكثر من مربع نص؟* | بالتأكيد. فقط كرر الخطوات 2‑4 مع نسخة جديدة من `TextBoxField` ومع `Name` فريد. |
| *ماذا لو لم يكن للـ PDF صفحة ثانية؟* | سيُطلق الكود استثناء `ArgumentOutOfRangeException`. احمِه بـ `if (pdfDocument.Pages.Count >= 2) { … }`. |
| *هل أحتاج لتعيين خطوط؟* | Aspose يستخدم Helvetica الافتراضية. للخطوط المخصصة، عيّن `commentsField.DefaultAppearance.Font` قبل الحفظ. |
| *هل الحقل قابل للطباعة؟* | نعم – Aspose يضع العلامة القابلة للطباعة على الـ widgets افتراضيًا. يمكنك تبديل `WidgetAnnotation.Flags` إذا لزم الأمر. |
| *كيف أستخرج القيمة المدخلة لاحقًا؟* | بعد أن يملأ المستخدمون النموذج وتستلم الـ PDF، استدعِ `pdfDocument.Form["Comments"].Value` لقراءة البيانات. |

## الخطوات التالية

الآن بعد أن عرفت **كيفية حفظ pdf** بعد إضافة مربع نص، قد ترغب في استكشاف:

- إضافة **مربعات اختيار** أو **أزرار راديو** (`CheckBoxField`, `RadioButtonField`).  
- استخدام إجراءات **JavaScript** للتحقق من صحة الجانب العميل (`commentsField.Actions.OnMouseUp = "…"`).  
- **تسوية** (Flatten) النموذج لمنع التعديلات الإضافية (`pdfDocument.Form.Flatten()`).  

جميع هذه تعتمد على نفس المفاهيم التي غطيناها أثناء **إنشاء نموذج متعدد الصفحات**.

---

**الخلاصة:** لقد تعلمت الآن كيفية **إنشاء نموذج متعدد الصفحات** في C# باستخدام Aspose.Pdf، وكيفية **إضافة مربع نص إلى pdf**، وكيفية **إنشاء حقل نموذج pdf**، والخطوات الدقيقة **لحفظ pdf المحدث**. لا تتردد في تعديل المستطيلات، إضافة المزيد من الحقول، أو التكرار عبر جميع الصفحات للحصول على حل ديناميكي حقًا.

هل لديك تعديل ترغب في مشاركته؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة للكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج وصفحات](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [إنشاء مستند PDF باستخدام Aspose – إضافة صفحة، مربع نص، ونموذج](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [كيفية إضافة واستخراج حقول نموذج PDF باستخدام Aspose.PDF لـ .NET: دليل شامل](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}