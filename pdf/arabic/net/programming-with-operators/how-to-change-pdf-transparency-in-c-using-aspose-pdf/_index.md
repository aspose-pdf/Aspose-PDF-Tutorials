---
category: general
date: 2026-09-24
description: تعلم كيفية تغيير شفافية PDF في C# باستخدام Aspose.Pdf. يغطي هذا الدليل
  خطوة بخطوة شفافية PDF، وضع المزج وتحرير حالة الرسومات.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: ar
lastmod: 2026-09-24
og_description: تغيير شفافية PDF في C# باستخدام Aspose.Pdf. اتبع هذا الدليل لتعديل
  شفافية PDF، وضع المزج، وحالة الرسومات للحصول على مخرجات مستندات احترافية.
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: تغيير شفافية PDF في C# – دليل Aspose.Pdf الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: كيفية تغيير شفافية PDF في C# باستخدام Aspose.Pdf
url: /ar/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير شفافية PDF في C# باستخدام Aspose.Pdf

إذا كنت بحاجة إلى **تغيير شفافية PDF** في مشروع .NET، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Pdf. ستشاهد مثالًا كاملاً قابلاً للتنفيذ يغيّر شفافية PDF، يحدد وضع المزج، ويحدّث قاموس حالة الرسومات للصفحة.

تغيير شفافية PDF هو طلب شائع عندما تريد علامات مائية، رسومات متراكبة، أو تأثيرات بصرية مخصصة. في هذا البرنامج التعليمي ستتعلم تعديل **حالة رسومات Aspose.Pdf**، ضبط **شفافية PDF**، والعمل مع إعدادات **وضع المزج PDF** — كل ذلك باستخدام كود C# نظيف.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث مثبت  
* ترخيص Aspose.Pdf for .NET (أو مفتاح تقييم مؤقت)  
* ملف PDF اسمه `input.pdf` في مجلد يمكنك الإشارة إليه كـ `YOUR_DIRECTORY`  
* إلمام أساسي بـ C# و Visual Studio (أي بيئة تطوير متكاملة تعمل)

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf`. يعمل الكود على Windows أو Linux أو macOS لأن Aspose.Pdf متعدد المنصات.

## تغيير شفافية PDF – الخطوة 1: فتح مستند PDF

العملية الأولى هي تحميل ملف PDF المصدر. يضمن استخدام كتلة `using` تحرير مقبض الملف تلقائيًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

فتح المستند هو الأساس لأي مهمة **معالجة PDF بـ C#**. إذا تعذر العثور على الملف، يرمي Aspose.Pdf استثناء `FileNotFoundException`، لذا تحقق من المسار قبل تشغيل الكود.

## الوصول إلى موارد الصفحة باستخدام حالة رسومات Aspose.Pdf

بعد ذلك، استخرج الصفحة الأولى وقاموس مواردها. يحتوي قاموس الموارد على كائنات مثل الخطوط، الصور، وإدخالات **ExtGState** التي تتحكم في معلمات الرسومات.

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

توفر فئة `DictionaryEditor` غلافًا مريحًا لقراءة وكتابة قواميس PDF. نركز هنا على قاموس **ExtGState** لأنه يخزن إعدادات الشفافية.

## إنشاء وتكوين حالة رسومات جديدة لشفافية PDF

الآن نبني قاموس حالة رسومات جديد. سيحتوي هذا القاموس على المعلمات التي تحدد شفافية الخط (`CA`)، شفافية التعبئة (`ca`)، ووضع المزج (`BM`).

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** يتحكم في شفافية عمليات الخط (الخطوط، الحدود).  
* **`ca`** يتحكم في شفافية عمليات التعبئة (الأشكال المملوءة، النص).  
* **`BM`** يحدد وضع المزج؛ `"Normal"` هو الافتراضي، لكن يمكنك استخدام `"Multiply"` أو `"Screen"` لتأثيرات فنية.

هذه الإعدادات هي جوهر تعديل **شفافية PDF**. عدّل القيم الرقمية لتناسب تصميمك البصري — `0` يعني شفاف بالكامل، `1` يعني غير شفاف تمامًا.

## إدراج حالة الرسومات وحفظ المستند

بعد إنشاء الحالة الجديدة، نضيفها إلى قاموس **ExtGState** الحالي تحت اسم فريد (`GS0`). أخيرًا، نحفظ ملف PDF المعدل.

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

عند فتح PDF في عارض، سيُعرض أي محتوى يشير إلى `GS0` بالشفافية المحددة. يمكنك لاحقًا تطبيق هذه الحالة على كائنات محددة باستخدام خاصية `GraphicsState` لأوامر الرسم (مثال: `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`).

## التحقق من النتيجة

افتح `output.pdf` في Adobe Acrobat Reader أو Foxit أو أي عارض PDF يدعم الشفافية. يجب أن ترى عناصر التعبئة في الصفحة الأولى تُعرض بشفافية 50 % بينما تبقى الخطوط غير شفافة تمامًا. إذا لم تلاحظ أي تغيير، تأكد من أن الصفحة تستخدم حالة الرسومات الجديدة — وإلا يمكنك تعيين `GS0` صراحةً للكائنات التي تريد تعديلها.

![Change PDF transparency in C# code example](path/to/image.png){: .img-responsive alt="تغيير شفافية PDF في مثال كود C#"}

*الصورة أعلاه تُظهر الكود الكامل بـ C# الذي يغيّر شفافية PDF.*

## اختلافات شائعة وحالات حافة

| الحالة | كيفية تعديل الكود |
|-----------|-----------------------|
| **صفحات متعددة** | كرّر الحلقة على `document.Pages` وطبق الخطوات 2‑8 على كل صفحة. |
| **وضع مزج مختلف** | استبدل `"Normal"` بـ `"Multiply"` أو `"Screen"` أو أي اسم وضع مزج قياسي في PDF. |
| **زيادة شفافية التعبئة** | غير `new CosPdfNumber(0.5)` إلى قيمة بين `0` و `1`. |
| **عدم وجود ExtGState موجود** | إذا أرجع `resourcesEditor["ExtGState"]` قيمة `null`، أنشئ قاموسًا جديدًا: `var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

تُظهر هذه الاختلافات مرونة **تعديل موارد PDF** باستخدام Aspose.Pdf. من خلال تعديل المعلمات، يمكنك إنشاء علامات مائية، طبقات شبه شفافة، أو عناصر واجهة مستخدم مخصصة داخل PDF.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع تطبيق Console جديد. يحتوي على جميع توجيهات `using` اللازمة، معالجة الأخطاء، وتعليقات توضيحية.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change PDF Opacity in C# – Complete Aspose Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}