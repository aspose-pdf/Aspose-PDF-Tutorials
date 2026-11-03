---
category: general
date: 2026-10-23
description: كيفية تغيير شفافية PDF باستخدام Aspose.Pdf في C#. تعلم تعديل ExtGState،
  ضبط شفافية الخط/الملء، وتطبيق أوضاع المزج في بضع أسطر من الشيفرة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change PDF opacity
- Aspose.Pdf opacity
- PDF graphics state
- ExtGState dictionary
- C# PDF manipulation
- PDF blend mode
language: ar
lastmod: 2026-10-23
og_description: كيفية تغيير شفافية PDF باستخدام Aspose.Pdf في C#. اتبع هذا الدليل
  المختصر لتعديل شفافية الخط والملء، وتعيين أوضاع الدمج، وحفظ المستند المحدث.
og_image_alt: Screenshot of a PDF page with semi‑transparent graphics created by Aspose.Pdf
  in C#
og_title: كيفية تغيير شفافية PDF في C# – دليل Aspose.Pdf الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  headline: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  name: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf;'
  - name: Get the first page and its resource dictionary
    text: '```csharp // Step 2: Get the first page and its resource dictionary var
      firstPage = pdfDocument.Pages[1]; var resourcesEditor = new DictionaryEditor(firstPage.Resources);
      ```'
  - name: Retrieve (or create) the ExtGState dictionary
    text: '```csharp // Step 3: Retrieve the ExtGState dictionary from the page resources
      // If ExtGState does not exist, create an empty one. CosPdfDictionary extGStateDict;
      if (resourcesEditor.ContainsKey("ExtGState")) { extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
      } else { extGStateDic'
  - name: Create a new graphics state dictionary and define opacity entries
    text: '```csharp // Step 4: Create a new graphics state dictionary and define
      its entries var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
      var graphicsStateEntries = new[] { new KeyValuePair<string, ICosPdfPrimitive>("CA",
      new CosPdfNumber(1.0)), // Stroke opacity (fully opaque)'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Step 5: Add the new graphics state to the ExtGState dictionary
      (named "GS0") extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: Save the updated PDF document
    text: '```csharp // Step 6: Save the updated PDF document pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      } ```'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Opacity
- GraphicsState
title: كيفية تغيير شفافية ملف PDF في C# باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/programming-with-operators/how-to-change-pdf-opacity-in-c-with-aspose-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير شفافية PDF في C# باستخدام Aspose.Pdf – دليل خطوة بخطوة

إذا كنت بحاجة إلى **كيفية تغيير شفافية PDF** لعناصر معينة، فإن هذا الدليل يوضح حلاً كاملاً قابلاً للتنفيذ. ستتعرف على كيفية تعديل قاموس ExtGState، وتعيين شفافية الخط والملء، واختيار وضع المزج—كل ذلك ببضع أسطر واضحة من كود C#.

تغيير شفافية PDF مفيد عندما تريد علامات مائية، رسومات فوقية، أو تأثيرات بصرية خفيفة دون الحاجة إلى إعادة بناء المستند بالكامل. يفترض الدليل أنك تمتلك بيئة C# أساسية ومكتبة Aspose.Pdf for .NET مثبتة.

![كيفية تغيير شفافية PDF باستخدام Aspose.Pdf في C#](https://example.com/og-image.png)

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.7+)
* نسخة مرخصة من **Aspose.Pdf for .NET** (الإصدار التجريبي المجاني يكفي للاختبار)
* ملف PDF إدخال موجود في مجلد يمكنك الإشارة إليه من الكود
* Visual Studio 2022 أو أي محرر C# تفضله

لا توجد حزم NuGet إضافية مطلوبة—Aspose.Pdf يحتوي على جميع الأنواع المستخدمة في هذا الدليل.

## فهم حالة الرسومات في PDF

تخزن صفحة PDF معلمات الرسم في كائن **graphics state**. يحتوي قاموس **ExtGState** على مدخلات مثل:

* **CA** – شفافية الخط (0 = شفاف، 1 = معتم)
* **ca** – شفافية الملء
* **BM** – وضع المزج (مثال: *Normal*، *Multiply*، *Screen*)

من خلال إنشاء قاموس حالة رسومات جديد وإضافته إلى مجموعة ExtGState الخاصة بالصفحة، يمكنك الإشارة إلى الحالة لاحقاً في تدفقات المحتوى. هذه الطريقة تتجنب إعادة كتابة محتوى الصفحة بالكامل وتعمل مع أي PDF موجود.

## كيفية تغيير شفافية PDF باستخدام Aspose.Pdf

الخطوات الست التالية تغطي العملية بالكامل—من تحميل المستند إلى حفظ الملف المعدل. كل خطوة تتضمن الكود الدقيق الذي تحتاجه وتفسيراً لأهمية الخطوة.

### الخطوة 1: تحميل مستند PDF

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

**لماذا هذا مهم** – فتح الملف باستخدام `Aspose.Pdf.Document` يمنحك وصولاً كاملاً إلى بنية PDF الداخلية، بما في ذلك موارد الصفحة حيث يعيش قاموس **ExtGState**.

### الخطوة 2: الحصول على الصفحة الأولى وقاموس مواردها

```csharp
// Step 2: Get the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**لماذا هذا مهم** – كل صفحة لديها قاموس *Resources* يجمع الخطوط، الصور، وحالات الرسومات. `DictionaryEditor` يوفر وصولاً مريحاً للقراءة/الكتابة إلى تلك المجموعة.

### الخطوة 3: استرجاع (أو إنشاء) قاموس ExtGState

```csharp
// Step 3: Retrieve the ExtGState dictionary from the page resources
// If ExtGState does not exist, create an empty one.
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**لماذا هذا مهم** – بعض ملفات PDF تحتوي بالفعل على مدخل **ExtGState**؛ وبعضها لا. يضمن المنطق الشرطي أن يعمل الدليل في الحالتين، مما يجعله قوياً للملفات الواقعية.

### الخطوة 4: إنشاء قاموس حالة رسومات جديد وتعريف مدخلات الشفافية

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

**لماذا هذا مهم** – المدخلات الثلاث الرئيسية تتحكم في كيفية عرض أوامر الرسم:

* `CA = 1.0` يحافظ على خطوط الرسم مرئية بالكامل.
* `ca = 0.5` يجعل الأشكال المملوءة شبه شفافة.
* `BM = Normal` يستخدم وضع المزج الافتراضي؛ يمكنك استبدال `"Normal"` بـ `"Multiply"` أو `"Screen"` للحصول على تأثيرات إبداعية.

### الخطوة 5: إضافة حالة الرسومات الجديدة إلى قاموس ExtGState

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary (named "GS0")
extGStateDict.Add("GS0", graphicsStateDict);
```

**لماذا هذا مهم** – تسمية المدخل `"GS0"` تنشئ مرجعاً يمكنك لاحقاً استخدامه في تدفق المحتوى (`/GS0 gs`). إذا احتجت إلى مستويات شفافية متعددة، أضف مدخلات إضافية (`"GS1"`، `"GS2"`، …) بقيم `CA`/`ca` مختلفة.

### الخطوة 6: حفظ مستند PDF المحدث

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**لماذا هذا مهم** – حفظ التغييرات يكتب قاموس **ExtGState** المعدل مرة أخرى إلى الملف. الآن يحتوي PDF الناتج على حالة رسومات قابلة لإعادة الاستخدام يمكن لأي أمر رسم استدعاؤها.

## تطبيق حالة الرسومات الجديدة على محتوى الصفحة

الخطوات أعلاه تنشئ فقط حالة الرسومات؛ لا يزال عليك الإشارة إليها في تدفق محتوى الصفحة. إليك مثال سريع يرسم مستطيلاً شبه شفافاً باستخدام الحالة التي أضفناها للتو:

```csharp
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    var page = pdfDocument.Pages[1];
    var content = new PageContentEditor(page);
    // Begin the graphics state GS0
    content.InsertContent(0, "q /GS0 gs\n"); // Save graphics state and apply GS0
    // Draw a rectangle (100,100) to (300,300)
    content.InsertContent(0, "0.2 0.6 0.8 rg\n"); // Set fill color (light blue)
    content.InsertContent(0, "100 100 200 200 re\n");
    content.InsertContent(0, "f\n"); // Fill rectangle with current fill opacity
    // Restore graphics state
    content.InsertContent(0, "Q\n");
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**التفسير** – المشغل `q` يحفظ حالة الرسومات الحالية، `/GS0 gs` يطبق إعدادات الشفافية، يُرسم المستطيل، و`Q` يستعيد الحالة الأصلية. يمكنك وضع هذا المقتطف في أي مكان على الصفحة، قبل أو بعد المحتوى الموجود، حسب الطبقة البصرية التي تحتاجها.

## المشكلات الشائعة وكيفية تجنّبها

| العرض | السبب | الحل |
|-------|-------|------|
| الشفافية لا تتغير | لا توجد مدخل ExtGState في الصفحة أو المحتوى لا يشير إلى الحالة الجديدة. | تأكد من وجود `ExtGState` وأن تدفق المحتوى يحتوي على `/GS0 gs` (أو الاسم الذي اخترته). |
| وضع المزج لا يُظهر أي تأثير | استخدام مساحة ألوان أو نسخة PDF غير متوافقة. | تأكد من أن نسخة PDF لا تقل عن 1.4 (مطلوبة للشفافية) وأنك لا تخلط ألوان البقعة مع أوضاع المزج. |
| المستند لا يفتح في عارضات قديمة | الشفافية غير مدعومة في PDF 1.3 أو أقدم. | اضبط `pdfDocument.Version = 1.4;` قبل الحفظ، أو قم بترقية نسخة PDF صراحة. |

## اختبار النتيجة

افتح `output.pdf` في Adobe Acrobat Reader أو Foxit أو أي عارض PDF حديث. يجب أن ترى المستطيل مرسماً بشفافية ملء 50 % بينما يبقى حدّه غير شفاف بالكامل. استخدم خيارات *Edit → Preferences → Accessibility* لتبديل “Use high‑contrast colors” وتأكد من بقاء تأثير الشفافية شبه الشفافة قائمًا.

إذا كنت بحاجة إلى التحقق برمجياً، يتيح لك Aspose.Pdf قراءة حالة الرسومات مرة أخرى:

```csharp
var gs = pdfDocument.Pages[1].Resources["ExtGState"]["GS0"].ToCosPdfDictionary();
var fillOpacity = ((CosPdfNumber)gs["ca"]).Value; // Should be 0.5
```

## توسيع التقنية

* **مستويات شفافية متعددة** – أضف المزيد من المدخلات (`"GS1"`، `"GS2"`) بقيم `ca` مختلفة وأشر إليها حيثما تحتاج.
* **أوضاع مزج مختلفة** – استبدل `"Normal"` بـ `"Multiply"` أو `"Screen"` لتحقيق تغطيات فنية.
* **التطبيق على الصور** – استخدم نفس حالة الرسومات قبل مشغل `Do` الذي يرسم صورة XObject.

هذه المتغيّرات تتيح لك بناء علامات مائية، إبراز أقسام، أو إنشاء تصاميم بصرية معقدة دون تحويل PDF إلى صورة نقطية.

## الخلاصة

أنت الآن تعرف **كيفية تغيير شفافية PDF** في C# باستخدام Aspose.Pdf. من خلال إنشاء حالة رسومات مخصصة، إضافتها إلى قاموس ExtGState للصفحة، واستدعاء الحالة في تدفق المحتوى، تحصل على تحكم دقيق في شفافية الخط والملء بالإضافة إلى أوضاع المزج. المثال الكامل جاهز للنسخ، التشغيل، والتكييف مع أي سيناريو معالجة PDF تواجهه.

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذه التقنية مع **شفافية Aspose.Pdf** على الصور، أو استكشف تأثيرات **وضع مزج PDF** لإنتاج تغطيات احترافية. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [تغيير شفافية PDF باستخدام Aspose.PDF – دليل C# كامل](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [تغيير شفافية PDF في C# مع Aspose.Pdf – دليل خطوة بخطوة](/pdf/english/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/)
- [كيفية تغيير شفافية PDF في C# باستخدام Aspose.Pdf](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}