---
category: general
date: 2026-07-17
description: كيفية تغيير الشفافية في ملف PDF باستخدام Aspose.PDF. تعلّم كيفية ضبط
  الشفافية، تعديل شفافية التعبئة، وحفظ ملفات PDF المعدلة ببضع أسطر فقط من C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change opacity
- how to set transparency
- save modified pdf
- set fill opacity
language: ar
lastmod: 2026-07-17
og_description: كيفية تغيير الشفافية في ملف PDF بسهولة. يوضح لك هذا البرنامج التعليمي
  كيفية ضبط الشفافية، تعديل شفافية التعبئة، وحفظ ملفات PDF المعدلة باستخدام Aspose.PDF.
og_image_alt: Code snippet showing how to change opacity in a PDF using Aspose.PDF
og_title: كيفية تغيير الشفافية في PDF – Aspose.PDF خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-17'
  description: How to change opacity in a PDF using Aspose.PDF. Learn how to set transparency,
    adjust fill opacity, and save modified PDF files in just a few lines of C#.
  headline: How to Change Opacity in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
- opacity
- transparency
title: كيفية تغيير الشفافية في ملفات PDF باستخدام Aspose.PDF – دليل كامل
url: /ar/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير الشفافية في PDF باستخدام Aspose.PDF – دليل كامل

هل تساءلت يومًا **كيف تغير الشفافية** في ملف PDF موجود دون فتح Adobe Acrobat؟ ربما تحتاج إلى علامة مائية شبه شفافة أو صورة خلفية باهتة وتواجه ملفًا ثابتًا. الخبر السار؟ باستخدام Aspose.PDF for .NET يمكنك تعديل معلمات حالة الرسومات برمجيًا، وستتعلم أيضًا **كيفية ضبط الشفافية**، تعديل **شفافية التعبئة**، و**حفظ ملفات PDF المعدلة** بسرعة.

في هذا الدرس سنستعرض مثالًا عمليًا: تحميل ملف PDF، إنشاء قاموس حالة رسومات جديد، تعريف شفافية الخط والتعبئة، وأخيرًا حفظ التغييرات. في النهاية ستحصل على مقتطف كود قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع C#.

---

## ما الذي ستحتاجه

قبل أن نغوص في التفاصيل، تأكد من وجود ما يلي:

- **Aspose.PDF for .NET** (أحدث نسخة، 2026.x) مثبت عبر NuGet  
  ```bash
  dotnet add package Aspose.PDF
  ```
- بيئة تطوير **.NET 6+** (Visual Studio، Rider، أو VS Code).
- ملف PDF إدخال (`input.pdf`) موجود في مجلد تملكه.
- إلمام أساسي بـ C# ومفاهيم PDF (الصفحات، الموارد، القواميس).

هذا كل شيء—لا مكتبات إضافية، ولا حزم SDK ثقيلة. لنبدأ العمل.

---

## كيفية تغيير الشفافية في PDF باستخدام Aspose.PDF

فيما يلي المثال الكامل القابل للتنفيذ. كل خطوة مشروحة بلغة بسيطة، بحيث يمكنك تعديلها لتناسب سيناريوهات أخرى (مثل تغيير وضع المزج، إضافة حالات رسومية جديدة).

![How to Change Opacity in PDF](/images/opacity-example.png "How to Change Opacity in PDF")

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.IO;
using Aspose.Pdf.InteractiveFeatures;
using System.Collections.Generic;

class OpacityDemo
{
    static void Main()
    {
        // Step 1: Load the PDF document
        string dataDir = "YOUR_DIRECTORY/";
        using (var document = new Aspose.Pdf.Document(dataDir + "input.pdf"))
        {
            // Step 2: Access the first page's resource dictionary
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // Step 3: Retrieve the ExtGState dictionary (holds graphics state parameters)
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Step 4: Create a new empty graphics state dictionary
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

            // Step 5: Define the graphics state entries
            // CA  – stroke opacity (1 = fully opaque)
            // ca  – fill opacity   (0.5 = 50 % transparent)
            // BM  – blend mode     (Normal is the default)
            var entries = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                newGraphicsState.Add(entry);

            // Step 6: Add the new graphics state to the ExtGState dictionary
            extGState.Add("GS0", newGraphicsState);

            // Step 7: Save the modified PDF
            document.Save(dataDir + "output.pdf");
        }
    }
}
```

### لماذا يعمل هذا

- **ExtGState** هو قاموس PDF خاص يخزن معلمات *حالة الرسومات* مثل الشفافية ووضع المزج. بإضافة إدخال (`GS0`) نمنح PDF “نمطًا” قابلًا لإعادة الاستخدام يمكن الإشارة إليه لاحقًا في تدفقات المحتوى.
- المفتاح **`ca`** يتحكم في *شفافية التعبئة* (الكلمة الثانوية “set fill opacity”). قيمة `0.5` تعني أن التعبئة ستكون شفافة بنسبة 50 %.
- المفتاح **`CA`** يفعل نفس الشيء لـ *شفافية الخط*—مفيد عند رسم الخطوط أو الحدود.
- **وضع المزج (`BM`)** يحدد كيفية تفاعل الرسومات الجديدة مع المحتوى الأساسي؛ “Normal” هو الإعداد الافتراضي الأكثر أمانًا.

---

## كيفية ضبط الشفافية لمحتوى محدد

الآن بعد أن أصبح لدينا حالة رسومات (`GS0`) مخزنة في PDF، الخطوة المنطقية التالية هي *استخدامها*. المقتطف التالي يوضح كيفية تطبيق الشفافية الجديدة على قطعة نصية. هذا يوضح **كيفية ضبط الشفافية** على أساس كل كائن.

```csharp
// Assume 'document' and 'page' are already defined as above
var content = new PageContent();
content.Operators.Add(new SetGraphicsState("GS0")); // Apply our custom graphics state

var textFragment = new TextFragment("Semi‑transparent text")
{
    TextState = { FontSize = 24, Font = FontRepository.FindFont("Arial") }
};
page.Paragraphs.Add(textFragment);
page.Contents.Add(content);
```

- `SetGraphicsState` هو عامل PDF الذي يبدل حالة الرسومات الحالية إلى الحالة التي عرفناها (`GS0`).
- إذا حذفت هذا السطر، سيُعرض PDF بالإعدادات الافتراضية (معتمة بالكامل).
- يمكنك إنشاء حالات رسومات متعددة (`GS1`, `GS2`, …) لمستويات شفافية أو أوضاع مزج مختلفة.

---

## حفظ PDF المعدل – ما المتوقع

بعد تشغيل البرنامج الكامل، ستجد `output.pdf` في نفس المجلد. افتحه بأي عارض (Adobe Reader، Edge، Chrome) وسترى:

- أي أشكال *معبأة* (مثل المستطيلات، خلفية النص) ستُعرض بشفافية 50 %.
- الخطوط (الخطوط، الحدود) ستظل معتمة بالكامل لأننا تركنا `CA` عند `1`.
- لا توجد عيوب بصرية—Aspose.PDF يتعامل مع بنية PDF منخفضة المستوى نيابةً عنك.

إذا كنت بحاجة إلى **حفظ ملفات PDF المعدلة** بصيغة مختلفة (مثل PDF/A، PDF/X)، ما عليك سوى استبدال استدعاء `Save` بـ:

```csharp
document.Save(dataDir + "output.pdf", SaveFormat.PdfA_1b);
```

---

## المشكلات الشائعة والنصائح الاحترافية

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **`resourcesEditor["ExtGState"]` returns null** | ملف PDF المصدر لم يُعرّف قاموس ExtGState أبداً (شائع في ملفات PDF البسيطة). | أنشئه يدويًا: `var extGState = new CosPdfDictionary(document); resourcesEditor["ExtGState"] = extGState;` |
| **Opacity appears unchanged** | قمت بإضافة حالة الرسومات لكن لم تُشر إليها في تدفق المحتوى. | استخدم `SetGraphicsState("GS0")` قبل رسم العنصر الذي تريد جعله شفافًا. |
| **Blend mode not respected** | بعض عارضات PDF تتجاهل أوضاع المزج غير القياسية. | التزم بـ `"Normal"` ما لم تكن تستهدف PDF/X‑4 أو عارض يدعم المزج المتقدم. |
| **Performance slowdown on large PDFs** | تعديل العديد من الصفحات واحدةً تلو الأخرى قد يكون مكلفًا. | قم بتجميع التغييرات: حرر قاموس ExtGState المشترك مرة واحدة، ثم أشر إليه في كل صفحة. |

---

## مثال كامل يعمل (جميع الخطوات في مكان واحد)

للتسهيل، إليك البرنامج الكامل من تحميل المستند إلى حفظ النتيجة، بما في ذلك عرض النص الاختياري الذي يستخدم الشفافية الجديدة:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.IO;
using System.Collections.Generic;

class OpacityDemo
{
    static void Main()
    {
        string dataDir = "YOUR_DIRECTORY/";
        using (var document = new Aspose.Pdf.Document(dataDir + "input.pdf"))
        {
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
                resourcesEditor["ExtGState"] = new CosPdfDictionary(document);
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create new graphics state (GS0)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) newGraphicsState.Add(e);
            extGState.Add("GS0", newGraphicsState);

            // Apply the graphics state to a text fragment
            var content = new PageContent();
            content.Operators.Add(new SetGraphicsState("GS0"));
            page.Contents.Add(content);

            var tf = new TextFragment("Semi‑transparent text")
            {
                TextState = { FontSize = 28, Font = FontRepository.FindFont("Arial") }
            };
            page.Paragraphs.Add(tf);

            // Save the altered PDF
            document.Save(dataDir + "output.pdf");
        }
    }
}
```

انسخ‑الصق، استبدل `YOUR_DIRECTORY` بالمسار الفعلي، ثم شغّل. سترى النص معروضًا بنصف شفافية، مما يثبت أن **كيفية تغيير الشفافية** أمر بسيط للغاية.

---

## الخطوات التالية: ما بعد الشفافية

الآن بعد أن أصبحت متمكنًا من الأساسيات، فكر في استكشاف:

- **شفافية ديناميكية**: تكرار عبر الصفحات وتعيين قيم `ca` مختلفة لتدرجات شفافية متتالية.  
- **حالات رسومات متعددة**: إنشاء `GS1`، `GS2`، إلخ، لمستويات شفافية مختلفة عبر مستند واحد.  
- **أوضاع مزج متقدمة**: جرّب `"Multiply"` أو `"Screen"` لتأثيرات فنية—لكن تذكر أن ليس كل العارضات تدعمها.  
- **دمج مع الصور**: إدراج شعار شبه شفاف باستخدام `ImageFragment` ونفس حالة الرسومات.

جميع هذه الأمور تعتمد على الفكرة الأساسية نفسها: تعديل قاموس **ExtGState** لإبلاغ مُعالج PDF بكيفية مزج المحتوى. النمط يبقى نفسه، فقط القيم تتغير.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تخصيص ملفات PDF باستخدام Aspose.PDF for .NET: ضبط هوامش الصفحة ورسم الخطوط](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [كيفية ضبط حجم الصورة في PDF باستخدام Aspose.PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [كيفية تغيير أحجام صفحات PDF باستخدام Aspose.PDF for .NET (دليل خطوة بخطوة)](/pdf/english/net/document-manipulation/change-pdf-page-sizes-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}