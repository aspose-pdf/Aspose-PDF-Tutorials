---
category: general
date: 2026-08-20
description: إنشاء حالة رسومات مخصصة في PDF باستخدام Aspose.Pdf. تعلم كيفية تعديل
  موارد PDF وإضافة شفافية إلى PDF في بضع خطوات فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: ar
lastmod: 2026-08-20
og_description: إنشاء حالة رسومات مخصصة في PDF باستخدام Aspose.Pdf. يوضح هذا الدرس
  كيفية تعديل موارد PDF وإضافة شفافية إلى PDF بسرعة.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: إنشاء حالة رسومات مخصصة في PDF – دليل Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: إنشاء حالة رسومية مخصصة في PDF باستخدام Aspose.Pdf
url: /ar/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء حالة رسومات مخصصة في PDF باستخدام Aspose.Pdf

إذا كنت بحاجة إلى **إنشاء حالة رسومات مخصصة** في PDF، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Pdf لـ .NET. في نهاية البرنامج التعليمي ستكون قادرًا على **تحرير موارد PDF**، وإدخال قاموس حالة رسومات جديد، و**إضافة محتوى شفافية PDF** دون مغادرة مشروع C# الخاص بك.

سترى مثالًا كاملًا قابلًا للتنفيذ، وشرحًا لأهمية كل سطر، ونصائح للتعامل مع مستندات متعددة الصفحات أو أوضاع المزج المختلفة. لا تحتاج إلى أدوات خارجية—فقط مكتبة Aspose.Pdf وبيئة تطوير .NET أساسية.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
* نسخة مرخصة من **Aspose.Pdf for .NET** (الإصدار التجريبي المجاني يعمل للاختبار)
* ملف PDF إدخال باسم `input.pdf` موجود في مجلد يمكنك الإشارة إليه من الكود
* Visual Studio 2022 أو أي بيئة تطوير تدعم تطوير C#

يفترض البرنامج التعليمي أنك على دراية بأساسيات صياغة C# ومفهوم صفحات PDF.

## الخطوة 1: تحميل ملف PDF المصدر والوصول إلى الصفحة الأولى

العملية الأولى هي فتح ملف PDF واسترجاع الصفحة التي تريد تعديل مواردها. تمثل Aspose.Pdf كل صفحة ككائن `Page`، وتحتوي كل صفحة على **قاموس الموارد** الذي يخزن حالات الرسومات، الخطوط، XObjects، وأكثر.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*لماذا هذا مهم:* تقوم فئة `Document` بتحميل الملف إلى الذاكرة، و`Pages[1]` يمنحك وصولًا مباشرًا إلى قاموس موارد الصفحة الأولى، وهو المكان الذي توجد فيه حالة الرسومات.

## الخطوة 2: فتح قاموس الموارد للتحرير

توفر Aspose.Pdf أداة مساعدة `DictionaryEditor` التي تتيح لك التعامل مع قاموس الموارد كـ `Dictionary` عادي في .NET. هذا يجعل من السهل قراءة، إضافة، أو استبدال الإدخالات مثل `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*لماذا هذا مهم:* يقوم `DictionaryEditor` بتجريد كائنات COS منخفضة المستوى، مما يتيح لك العمل مع أزواج المفتاح/القيمة المألوفة مع الحفاظ على توافق PDF.

## الخطوة 3: استرجاع (أو إنشاء) قاموس ExtGState

الإدخال **ExtGState** يحتوي على جميع كائنات حالة الرسومات الخارجية للصفحة. إذا لم يكن القاموس موجودًا، ستقوم Aspose.Pdf بإنشاء واحد فارغ لك.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*لماذا هذا مهم:* عدم وجود إدخال `ExtGState` سيتسبب في حدوث `KeyNotFoundException` لاحقًا. هذه الحماية تسمح للكود بالعمل على ملفات PDF التي لم تقم أبدًا بتعريف حالة رسومات مخصصة من قبل—وهي جزء أساسي من صلابة **تحرير موارد PDF**.

## الخطوة 4: بناء قاموس حالة الرسومات المخصصة

حالة الرسومات تصف كيفية عرض عمليات الرسم. لإ **إضافة شفافية PDF**، تحتاج إلى ضبط الإدخالات `ca` (شفافية التعبئة) و `CA` (شفافية الحد)، واختيارياً وضع المزج (`BM`). الكود التالي يبني قاموسًا جديدًا بهذه المعلمات.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*لماذا هذا مهم:* تتحكم إدخالات `ca` و `CA` في الشفافية لعمليات التعبئة والحد على التوالي. ضبط `BM` يتيح لك تجربة تأثيرات تركيب مختلفة، وهو مفيد عندما تقوم لاحقًا **بإضافة محتوى شفافية PDF** مثل أشكال أو صور شبه شفافة.

## الخطوة 5: تسجيل حالة الرسومات الجديدة تحت اسم فريد

كل حالة رسومات في قاموس `ExtGState` يجب أن يكون لها اسم فريد (مثال: `GS0`، `GS1`). يمكنك اختيار أي اسم لا يتعارض مع الإدخالات الموجودة.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*لماذا هذا مهم:* بإدراج القاموس الجديد تحت `GS0`، تجعل الحالة قابلة للوصول من تدفقات محتوى الصفحة. يضمن الشرط وجود إدخال `ExtGState` حتى لملفات PDF التي بدأت بدون واحد—حماية إضافية لـ **تحرير موارد PDF**.

## الخطوة 6: استخدام حالة الرسومات المخصصة في محتوى الصفحة (اختياري)

الخطوات السابقة فقط *تعرف* حالة الرسومات. لرؤية التأثير فعليًا، يجب الإشارة إليها في تدفق محتوى الصفحة. أدناه مثال سريع يرسم مستطيلًا شبه شفاف باستخدام الحالة التي أنشأناها للتو.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*لماذا هذا مهم:* عامل `SetExtGState` (`gs`) يخبر عارض PDF بتطبيق المعلمات المعرفة في `GS0`. سيظهر المستطيل بشفافية تعبئة 50 % بينما يبقى حدّه غير شفاف بالكامل.

## الخطوة 7: حفظ ملف PDF المعدل

أخيرًا، اكتب التغييرات مرة أخرى إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

عند فتح `output_with_custom_gs.pdf` في عارض PDF، يجب أن ترى مستطيلًا شبه شفاف على الصفحة الأولى. هذا يؤكد أنك نجحت في **إنشاء حالة رسومات مخصصة**، **تحرير موارد PDF**، و**إضافة محتوى شفافية PDF**.

## الاختلافات الشائعة وحالات الحافة

| الحالة | ما الذي يجب تعديله |
|-----------|----------------|
| **عدة صفحات تحتاج نفس الحالة** | سجّل حالة الرسومات مرة واحدة (الخطوات 1‑5) وأشر إلى `GS0` في تدفق محتوى أي صفحة. |
| **شفافية مختلفة لكل عنصر** | عرّف حالات إضافية (`GS1`، `GS2`، …) بقيم `ca`/`CA` مختلفة وتبديل بينها باستخدام `SetExtGState`. |
| **وضع المزج غير Normal** | استبدل `"Normal"` بـ `"Multiply"` أو `"Screen"` أو أي وضع مزج قياسي في PDF في إدخال `BM`. |
| **تصادم الأسماء** | قبل الإضافة، تحقق من `extGStateDict.ContainsKey(yourName)` واختر لاحقة فريدة إذا لزم الأمر. |
| **PDF يحتوي بالفعل على قاموس ExtGState** | الكود في الخطوة 3 يعيد استخدام القاموس الموجود بالفعل، لذا لا يلزم أي معالجة إضافية. |

**نصيحة احترافية:** عند العمل مع ملفات PDF الكبيرة، احيط استخدام `Document` بكتلة `using` (كما هو موضح) لتحرير الموارد الأصلية بسرعة. أيضًا، فكر في تمكين خاصية `PdfCompliance` في Aspose.Pdf إذا كنت بحاجة لضمان توافق PDF/A أو PDF/X بعد تحرير الموارد.

## مثال كامل يعمل

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء PDF باستخدام Aspose – إضافة حقل نموذج وصفحات](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [كيفية إنشاء جداول مخصصة في PDFs باستخدام Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [إنشاء طوابع PDF مخصصة Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}