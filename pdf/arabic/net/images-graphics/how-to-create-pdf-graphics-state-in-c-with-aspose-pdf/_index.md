---
category: general
date: 2026-11-16
description: تعلم كيفية إنشاء حالة رسومات PDF في C# باستخدام Aspose.Pdf. يغطي هذا
  الدليل الشفافية، وضع الدمج، ومثالًا كاملاً للكود.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: ar
lastmod: 2026-11-16
og_description: إنشاء حالة رسومات PDF في C# باستخدام Aspose.Pdf. اتبع هذا الدرس الكامل
  لضبط الشفافية وضعية الدمج برمجيًا.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: إنشاء حالة رسومات PDF في C# – دليل Aspose.Pdf خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: كيفية إنشاء حالة رسومات PDF في C# باستخدام Aspose.Pdf
url: /ar/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء حالة رسومات PDF في C# باستخدام Aspose.Pdf

إذا كنت بحاجة إلى **إنشاء حالة رسومات PDF** في مشروع .NET، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك باستخدام Aspose.Pdf. سواء كنت تريد التحكم في الشفافية، أو تغيير وضع المزج، أو إعادة استخدام حالة رسومات مخصصة عبر الصفحات، فإن الخطوات أدناه توفر لك حلاً كاملاً وجاهزًا للتنفيذ.

في هذا الدليل ستتعلم كيفية الوصول إلى موارد الصفحة، إضافة إدخال **ExtGState**، وحفظ التغييرات إلى ملف جديد. المثال يعمل مع Aspose.Pdf 23.12 (أو أحدث) ويستهدف .NET 6+، لكن المفاهيم تنطبق على الإصدارات السابقة أيضًا.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* Visual Studio 2022 (أو أي بيئة تطوير C#) مع تثبيت .NET 6 SDK.  
* رخصة Aspose.Pdf for .NET أو مفتاح تقييم مؤقت.  
* ملف PDF اسمه `input.pdf` موجود في مجلد يمكنك الإشارة إليه من الكود.  

لا تحتاج إلى حزم NuGet إضافية بخلاف `Aspose.Pdf`.

## ما يغطيه الدليل

* تحميل مستند PDF موجود.  
* الانتقال إلى قاموس موارد الصفحة الأولى.  
* إنشاء قاموس حالة رسومات جديد يحدد شفافية الخط (`CA`)، شفافية التعبئة (`ca`)، ووضع المزج (`BM`).  
* إضافة حالة الرسومات الجديدة إلى مجموعة **ExtGState** باسم مخصص (`GS0`).  
* حفظ ملف PDF المحدث بحيث يمكن لأوامر الرسم اللاحقة الإشارة إلى الحالة الجديدة.

بنهاية الدليل ستكون قادرًا على **إنشاء حالة رسومات PDF** برمجيًا وإعادة استخدامها في أي عملية رسم.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيقًا جديدًا من نوع console (أو دمج الكود في مشروع موجود). أضف مرجع Aspose.Pdf وضمن المساحات الاسمية المطلوبة:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **نصيحة احترافية:** إذا كنت تستخدم نسخة التقييم المجانية، أضف `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` قبل تحميل المستند لتجنب رسائل العلامة المائية.

## الخطوة 2: تحميل مستند PDF

فتح الملف سهل. تمثل الفئة `Document` المستند PDF بالكامل وتمنحك الوصول إلى صفحاته وموارده.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

وضع الكود داخل كتلة `using` يضمن تحرير مقبض الملف بعد العملية، وهو أمر أساسي لـ **معالجة PDF في C#** في بيئات الإنتاج.

## الخطوة 3: استرجاع قاموس موارد الصفحة الأولى

كل صفحة PDF لديها قاموس *Resources* يخزن الخطوط، الصور، وحالات الرسومات. نحتاج إلى `DictionaryEditor` لتعديل هذا الهيكل.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

إذا كان ملف PDF يحتوي بالفعل على إدخال `ExtGState`، فإن `resourcesEditor["ExtGState"]` سيعيده؛ وإلا، سيقوم Aspose.Pdf بإنشاء قاموس فارغ لنا عند إضافة أول إدخال.

## الخطوة 4: الوصول إلى قاموس ExtGState أو إنشائه

قاموس **ExtGState** يحتوي على كائنات حالة رسومات مسماة. إما نستخرج واحدًا موجودًا أو ننشئ حاوية جديدة.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

عند عدم وجود `ExtGState`، تُعيد `resourcesEditor["ExtGState"]` قاموسًا فارغًا جديدًا تلقائيًا، مما يضمن عمل الكود مع أي ملف PDF.

## الخطوة 5: بناء قاموس حالة الرسومات الجديد

حالة الرسومات هي `CosPdfDictionary` تحتوي على مفاتيح محددة:

* `CA` – شفافية الخط (0‑1)  
* `ca` – شفافية التعبئة (0‑1)  
* `BM` – وضع المزج (`Normal`, `Multiply`, إلخ)

ننشئ قاموسًا فارغًا، نملأه، ثم نضيفه إلى `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

يمكنك تغيير `0.5` إلى أي قيمة بين `0` و `1` لتعديل شفافية التعبئة، أو استبدال `"Normal"` بـ `"Multiply"` للحصول على **وضع مزج PDF** مختلف. هذه المرونة هي السبب في أن إنشاء حالة رسومات مخصصة يُعد تقنية قوية في التعامل مع **حالة رسومات Aspose.Pdf**.

## الخطوة 6: تسجيل حالة الرسومات باسم

تُشير تدفقات محتوى PDF إلى حالات الرسومات بالاسم. هنا نستخدم `GS0`، لكن أي اسم فريد يعمل.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

إذا كنت بحاجة إلى حالات متعددة، كرر خطوة الإنشاء مع معلمات مختلفة وأضفها كـ `GS1`، `GS2`، إلخ. هذا النمط يتوسع جيدًا للوثائق المعقدة التي تتطلب إعدادات شفافية أو مزج مختلفة على طبقات متعددة.

## الخطوة 7: حفظ ملف PDF المعدل

أخيرًا، اكتب المستند المحدث إلى ملف جديد. الحفاظ على الأصل سيسهل عملية تصحيح الأخطاء.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

بعد التنفيذ، يحتوي `output.pdf` على إدخال `ExtGState` باسم `GS0`. يمكن لأي مشغل رسم لاحق الإشارة إليه باستخدام عامل `gs` (مثال: `GS0 gs` في تدفق المحتوى).  

> **لماذا هذا مهم:** بإنشاء حالة رسومات قابلة لإعادة الاستخدام تتجنب تكرار إعدادات الشفافية والمزج لكل أمر رسم، مما يحسن الأداء وسهولة الصيانة.

## استخدام حالة الرسومات الجديدة في تدفق المحتوى (اختياري)

إذا أردت رؤية التأثير فورًا، يمكنك إضافة مستطيل بسيط يستخدم الحالة التي أنشأناها للتو:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

سيُرسم المستطيل بشفافية تعبئة 50 % بينما يبقى الخط غير شفاف تمامًا، تمامًا كما تم تعريفه في قاموس **إنشاء حالة رسومات PDF**.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| عدم العثور على إدخال `ExtGState` | بعض ملفات PDF لا تتضمن القاموس أصلاً. | يقوم `DictionaryEditor` بإنشائه تلقائيًا عند إضافة أول إدخال، لذا لا حاجة لفحص إضافي. |
| قيم الشفافية > 1 أو < 0 | مواصفات PDF تقيد الشفافية بالنطاق `[0,1]`. | قيد القيم قبل إنشاء `CosPdfNumber`. |
| خطأ إملائي في وضع المزج | أسماء أوضاع المزج في PDF حساسة لحالة الأحرف. | استخدم الأسماء الدقيقة مثل `"Normal"`، `"Multiply"`، `"Screen"`. |
| علامة مائية للترخيص | نسخة التقييم تضيف علامة مائية على الصفحة الأولى. | طبق ملف ترخيص صالح قبل فتح المستند. |

معالجة هذه الحالات الطرفية تضمن أن تنفيذ **إنشاء حالة رسومات PDF** يعمل بثبات عبر مصادر PDF المختلفة.

## مثال كامل قابل للتنفيذ

فيما يلي برنامج مستقل يمكنك نسخه، لصقه، وتشغيله. استبدل `YOUR_DIRECTORY` بمسار مجلد فعلي على جهازك.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء حالة رسومات مخصصة في PDF باستخدام Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [إضافة حالة رسومات إلى PDF باستخدام Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [كيفية إنشاء حالة رسومات فارغة في PDF باستخدام C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}