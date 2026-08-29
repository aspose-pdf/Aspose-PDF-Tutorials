---
category: general
date: 2026-07-07
description: تعلم كيفية إضافة ExtGState إلى ملف PDF باستخدام Aspose.Pdf. يغطي هذا
  الدليل خطوة بخطوة قاموس حالة الرسومات، تحرير موارد PDF، وإعدادات وضع الدمج.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add extgstate to pdf
- Aspose.Pdf
- graphics state dictionary
- PDF resources
- blend mode
language: ar
lastmod: 2026-07-07
og_description: إضافة ExtGState إلى PDF باستخدام Aspose.Pdf. اتبع هذا الدليل لتعديل
  موارد PDF، وإنشاء قاموس حالة الرسومات، وتعيين الشفافية ووضع الدمج، وحفظ النتيجة.
og_image_alt: Screenshot showing Aspose.Pdf code to add ExtGState to a PDF document
og_title: إضافة ExtGState إلى PDF – دليل Aspose.Pdf خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-07'
  description: Learn how to add ExtGState to PDF using Aspose.Pdf. This step‑by‑step
    guide covers graphics state dictionary, PDF resources editing, and blend mode
    settings.
  headline: Add ExtGState to PDF with Aspose.Pdf – Complete Guide
  type: TechArticle
tags:
- Aspose.Pdf
- PDF manipulation
- C#
- ExtGState
title: إضافة ExtGState إلى PDF باستخدام Aspose.Pdf – دليل كامل
url: /ar/net/images-graphics/add-extgstate-to-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ExtGState إلى PDF – دليل برمجة كامل

هل احتجت يومًا إلى **إضافة ExtGState إلى PDF** لكن لم تكن متأكدًا من أي استدعاءات API تستخدم؟ لست وحدك. في هذا الدرس سنستعرض الخطوات الدقيقة باستخدام **Aspose.Pdf** لتعديل موارد الصفحة، وإنشاء **قائمة حالة الرسومات** مخصصة، وتعيين الشفافية ووضع المزج — كل ذلك في بضع أسطر فقط من C#.

سنبدأ بتحميل ملف PDF موجود، ثم نتعمق في **موارد PDF** الخاصة به، ونُدخل إدخال ExtGState جديد، وأخيرًا نحفظ المستند المعدل. في النهاية ستحصل على قطعة شفرة قابلة لإعادة الاستخدام يمكنك إدراجها في أي مشروع .NET يحتاج إلى تحكم دقيق في الرسومات.

## ما ستحتاجه

- .NET 6 (أو أي نسخة حديثة من .NET Framework)  
- حزمة NuGet **Aspose.Pdf for .NET** (`Aspose.Pdf`)  
- ملف PDF إدخال (`input.pdf`) موجود في مجلد يمكنك الإشارة إليه  
- فهم أساسي لصياغة C# (لا حاجة لمعرفة عميقة بداخلية PDF)

إذا كان لديك كل ذلك، هيا نبدأ.

![Add ExtGState to PDF using Aspose.Pdf](placeholder.png){alt="إضافة ExtGState إلى PDF باستخدام Aspose.Pdf"}

## الخطوة 1: إضافة ExtGState إلى PDF – تحميل المستند

أول شيء علينا القيام به هو فتح ملف PDF الذي نريد تعديله. استخدام كتلة `using` يضمن تحرير مقبض الملف تلقائيًا، وهو أمر مفيد خاصةً عندما تقوم لاحقًا بالكتابة فوق نفس الملف.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf"))
{
    // The document is now loaded and ready for manipulation.
```

*لماذا هذا مهم:* تحميل الملف يمنحك الوصول إلى مجموعة `Pages`، حيث توجد **موارد PDF** لكل صفحة. بدون فتح المستند لا يمكنك تعديل قاموس ExtGState.

## الخطوة 2: الوصول إلى موارد PDF باستخدام Aspose.Pdf

كل صفحة في PDF تحتوي على قاموس `/Resources` الذي يخزن الخطوط، الصور، وحالات الرسومات. نحتاج إلى الحصول على موارد الصفحة الأولى وتغليفها في `DictionaryEditor` حتى نتمكن من قراءة وكتابة الإدخالات.

```csharp
    // Step 2: Get the first page's resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*نصيحة احترافية:* إذا كان ملف PDF يحتوي على عدة صفحات وتحتاج إلى نفس ExtGState على جميعها، قم بالتكرار عبر `pdfDocument.Pages` وكرر الخطوات التالية لكل صفحة.

## الخطوة 3: استرجاع قاموس ExtGState الموجود (أو إنشاء واحد)

قد يكون إدخال `/ExtGState` موجودًا بالفعل. نقوم بجلبه حتى نضيف حالة الرسومات الجديدة تحت مفتاح فريد. إذا لم يكن موجودًا، سيُصدر Aspose.Pdf استثناء، لذا نحمي من ذلك بإنشاء قاموس جديد عند الحاجة.

```csharp
    // Step 3: Retrieve the existing ExtGState dictionary
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

*ما يحدث:* `resourcesEditor["ExtGState"]` يُعيد كائن COS؛ استدعاء `ToCosPdfDictionary()` يحوله إلى قاموس قابل للتعديل يمكننا إضافة إدخالات إليه.

## الخطوة 4: بناء قاموس حالة الرسومات بالمعلمات المطلوبة

الآن يأتي جوهر الدرس: إنشاء **قاموس حالة الرسومات** الذي يحدد شفافية الخط (`CA`)، شفافية التعبئة (`ca`)، ووضع المزج (`BM`). هذه المفاتيح تتبع مواصفات PDF لإدخالات ExtGState.

```csharp
    // Step 4: Create a new graphics‑state dictionary with desired parameters
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA",
            new Aspose.Pdf.CosPdfNumber(1)),   // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca",
            new Aspose.Pdf.CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM",
            new Aspose.Pdf.CosPdfName("Normal")) // Blend mode (standard normal blending)
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

*لماذا نضبط هذه القيم:*  
- **CA** و **ca** يتيحان لك التحكم في كيفية دمج الأحبار مع خلفية الصفحة — مثالي للعلامات المائية أو الطبقات شبه الشفافة.  
- **BM** (وضع المزج) يحدد كيفية دمج ألوان المصدر والوجهة؛ `"Normal"` هو الوضع الافتراضي، لكن يمكنك التحويل إلى `"Multiply"` أو `"Screen"` للحصول على تأثيرات إبداعية.

## الخطوة 5: إدراج ExtGState الجديد في موارد الصفحة

نُعطي حالة الرسومات الجديدة اسمًا (`GS0`) ونضعه في قاموس ExtGState الخاص بالصفحة. من الآن فصاعدًا، أي تدفق محتوى يشير إلى `/GS0` سيورث الشفافية ووضع المزج الذي عرّفناه.

```csharp
    // Step 5: Add the new ExtGState to the page resources under a chosen name
    extGStateDict.Add("GS0", newGraphicsState);
```

*ملاحظة حالة حافة:* إذا كان `GS0` موجودًا بالفعل، سيقوم Aspose.Pdf بالكتابة فوقه. لتجنب التصادمات غير المقصودة، فكر في إنشاء اسم يعتمد على GUID مثل `"GS_" + Guid.NewGuid().ToString("N")`.

## الخطوة 6: حفظ PDF المعدل

أخيرًا، نكتب التغييرات مرة أخرى إلى القرص. يمكنك الكتابة فوق الملف الأصلي أو إنشاء نسخة جديدة — حسب ما يناسب سير عملك.

```csharp
    // Step 6: Save the modified PDF
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

*ما المتوقع:* افتح `output.pdf` في أي عارض PDF. أي أوامر رسم تُشير لاحقًا إلى `GS0` ستُظهر الآن شفافية تعبئة بنسبة 50 % وشفافية خط كاملة، باستخدام وضع المزج العادي.

---

## إضافي: تطبيق ExtGState الجديد في تدفق المحتوى

إضافة قاموس ExtGState وحده لا يكفي؛ يجب إخبار تدفق محتوى PDF باستخدامه. إليك مقتطف سريع يرسم مستطيلًا شبه شفاف باستخدام الحالة التي أنشأناها للتو:

```csharp
// Assuming 'firstPage' is still in scope
var content = firstPage.Contents[1]; // Get the first content stream
content.Add("q\n");                 // Save graphics state
content.Add("/GS0 gs\n");           // Apply our ExtGState
content.Add("0.5 0 0 0.5 100 500 cm\n"); // Scale and position
content.Add("0 0 200 100 re\n");    // Rectangle
content.Add("0.2 0.6 0.8 rg\n");    // Fill color (RGB)
content.Add("B\n");                 // Fill and stroke
content.Add("Q\n");                 // Restore graphics state
```

*شرح:*  
- `q`/`Q` يدفعان ويُعيدان حالة الرسومات من المكدس، مما يضمن عدم تسرب تغييراتنا إلى عناصر أخرى.  
- `/GS0 gs` يختار حالة الرسومات التي أضفناها.  
- المشغل `re` يرسم مستطيلًا، و`B` يملأه ويُحدده باستخدام الشفافية المحددة.

لا تتردد في تعديل إحداثيات المستطيل، الألوان، أو حتى استبدال الشكل بنص — أي أمر رسم سيحترم الآن إعدادات ExtGState.

## الأخطاء الشائعة وكيفية تجنبها

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **غياب إدخال `/ExtGState`** | بعض ملفات PDF لا تُعرّف القاموس أبدًا. | تحقق من `resourcesEditor.ContainsKey("ExtGState")` قبل الوصول؛ إذا كان false، أنشئ قاموسًا فارغًا جديدًا وأضفه إلى `resourcesEditor`. |
| **الشفافية غير مطبقة** | تدفق المحتوى لا يشير أبدًا إلى الحالة الجديدة. | أدخل `/GS0 gs` قبل أي أوامر رسم تريد أن تتأثر. |
| **تجاهل وضع المزج** | العارض لا يدعم بعض أوضاع المزج. | التزم بالأوضاع المدعومة على نطاق واسع مثل `"Normal"` أو `"Multiply"` لتحقيق أقصى توافق. |
| **الصفحات المتعددة تحتاج إلى نفس الحالة** | تم تعديل الصفحة الأولى فقط. | كرّر عبر `pdfDocument.Pages` وكرر الخطوات 2‑5 لكل صفحة. |

## مثال عملي كامل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق والذي يدمج جميع الخطوات، معالجة الأخطاء، وعرضًا لاستخدام ExtGState الجديد.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إضافة كائن خط في PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [إضافة طوابع صور إلى ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)
- [كيفية إضافة صور إلى ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}