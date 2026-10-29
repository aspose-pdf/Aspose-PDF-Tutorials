---
category: general
date: 2026-08-08
description: ضبط شفافية PDF في C# باستخدام Aspose.PDF – تعلّم كيفية تعديل شفافية الخط
  والملء ببضع أسطر من الشيفرة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set pdf opacity
- Aspose.PDF for .NET
- C# graphics state
- PDF resource dictionary
- blend mode
- PDF transparency
language: ar
lastmod: 2026-08-08
og_description: قم بتعيين شفافية PDF في C# بسرعة. يوضح لك هذا الدليل كيفية تعديل شفافية
  الخط والملء باستخدام واجهة برمجة حالة الرسومات في Aspose.PDF.
og_image_alt: Screenshot of C# code that sets PDF opacity with Aspose.PDF
og_title: ضبط شفافية PDF في C# باستخدام Aspose.PDF – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Set PDF opacity in C# using Aspose.PDF – learn how to adjust stroke
    and fill transparency with a few lines of code.
  headline: Set PDF opacity in C# with Aspose.PDF – complete guide
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: ضبط شفافية PDF في C# باستخدام Aspose.PDF – دليل كامل
url: /ar/net/images-graphics/set-pdf-opacity-in-c-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين شفافية PDF في C# باستخدام Aspose.PDF – دليل كامل

إذا كنت بحاجة إلى **تعيين شفافية PDF** لعمليات الرسم المحددة، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.PDF for .NET. سواءً كنت تنشئ علامات مائية، أو طبقات نصف شفافة، أو رسومات مخصصة، ستتعلم نهجًا مختصرًا وجاهزًا للإنتاج.

في الأقسام التالية سنغطي كل شيء من تحميل ملف PDF إلى تعديل حالة الرسومات، إضافة تعريف شفافية جديد، وحفظ النتيجة. لا تحتاج إلى أي وثائق خارجية—فقط الكود أدناه وشرح موجز لكل خطوة.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
* رخصة صالحة لـ Aspose.PDF for .NET (الإصدار التجريبي المجاني يعمل للتقييم)
* ملف PDF إدخال (`input.pdf`) موجود في مجلد يمكنك القراءة/الكتابة فيه
* Visual Studio 2022 أو أي بيئة تطوير C# تفضلها

## الخطوة 1 – تحميل مستند PDF (Aspose.PDF for .NET)

المهمة الأولى هي فتح ملف PDF الموجود. تمثل Aspose.PDF ملف PDF باستخدام الفئة `Document`، والتي تمنحك وصولًا كاملاً إلى الصفحات والموارد والكائنات منخفضة المستوى.

```csharp
// Load the PDF document from disk
string inputPath = @"C:\MyFolder\input.pdf";
using var doc = new Aspose.Pdf.Document(inputPath);
```

*لماذا هذا مهم*: تحميل المستند ينشئ نموذجًا في الذاكرة يمكنك تعديلّه بأمان. يضمن بيان `using` تحرير مقبض الملف تلقائيًا بعد الانتهاء.

## الخطوة 2 – الحصول على الصفحة الأولى التي تريد تعديلها

يتم تعريف الشفافية لكل صفحة من خلال قاموس موارد الصفحة. هنا نستهدف الصفحة الأولى، ولكن يمكنك التكرار عبر `doc.Pages` لإجراء عملية دفعة.

```csharp
// Access the first page (pages are 1‑based in Aspose.PDF)
var page = doc.Pages[1];
```

*لماذا هذا مهم*: كل صفحة لديها مجموعة `Resources` الخاصة بها، التي تخزن حالات الرسومات، الخطوط، الصور، إلخ. تعديل الصفحة الصحيحة يضمن ظهور تأثير الشفافية حيث تتوقع.

## الخطوة 3 – فتح قاموس موارد الصفحة للتعديل

توفر Aspose.PDF أداة مساعدة `DictionaryEditor` للتعامل مع قواميس PDF منخفضة المستوى دون كسر بنية الملف.

```csharp
// Prepare a dictionary editor for the page's resources
var dictEditor = new Aspose.Pdf.DictionaryEditor(page.Resources);
```

*لماذا هذا مهم*: تعديل قواميس COS (Content Object System) في PDF مباشرة هو الطريقة الوحيدة لإدخال حالة رسومات مخصصة. تُجرد الأداة الصياغة منخفضة المستوى مع الحفاظ على صحة PDF.

## الخطوة 4 – استرجاع قاموس ExtGState الموجود

قاموس **ExtGState** (حالة الرسومات الخارجية) يحتوي على الشفافية، وضع المزج، عرض الخط، إلخ. إذا لم يكن موجودًا، تقوم Aspose.PDF بإنشائه تلقائيًا عند إضافة إدخال جديد.

```csharp
// Get the ExtGState dictionary; create it if missing
var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary()
                ?? new Aspose.Pdf.Cos.CosPdfDictionary(doc);
```

*لماذا هذا مهم*: بدون إدخال `ExtGState` لا يمكنك الإشارة إلى شفافية مخصصة لاحقًا في تدفق محتوى الصفحة. تضمن هذه الخطوة وجود الحاوية.

## الخطوة 5 – إنشاء حالة رسومات جديدة بالشفافية المطلوبة

حالة الرسومات هي مجموعة من المعلمات. للشفافية نحدد `CA` (شفافية الخط) و `ca` (شفافية التعبئة). كما نحدد وضع المزج (`BM`) للتحكم في كيفية تفاعل البكسلات الشفافة مع المحتوى الأساسي.

```csharp
// Build a new graphics state dictionary
var newGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(doc);
newGs.Add("CA", new Aspose.Pdf.Cos.CosPdfNumber(0.8)); // 80 % stroke opacity
newGs.Add("ca", new Aspose.Pdf.Cos.CosPdfNumber(0.4)); // 40 % fill opacity
newGs.Add("BM", new Aspose.Pdf.Cos.CosPdfName("Normal")); // standard blend mode
```

*لماذا هذا مهم*: القيم `CA` و `ca` تقبل أرقامًا من 0 (شفافية كاملة) إلى 1 (عتمة كاملة). اضبط هذه القيم لتحقيق التأثير البصري المطلوب. وضع المزج `"Normal"` هو الأكثر شيوعًا، لكن يمكنك تجربة `"Multiply"` أو `"Screen"` للحصول على تأثيرات فنية.

## الخطوة 6 – تسجيل حالة الرسومات الجديدة في مجموعة ExtGState

كل حالة رسومات يجب أن يكون لها اسم فريد (مثال، `GS0`). نضيف القاموس إلى مجموعة `ExtGState`، ثم نحدّث موارد الصفحة.

```csharp
// Add the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);

// Ensure the ExtGState entry is stored back in the page resources
dictEditor["ExtGState"] = extGState;
```

*لماذا هذا مهم*: بتسمية الحالة (`GS0`)، يمكنك الإشارة إليها لاحقًا في تدفق محتوى الصفحة باستخدام المشغل `gs`. إذا كنت بحاجة إلى مستويات شفافية متعددة، أنشئ إدخالات إضافية (`GS1`, `GS2`, …).

## الخطوة 7 – تطبيق حالة الرسومات على أوامر الرسم (اختياري)

إذا كنت تريد تطبيق الشفافية فورًا على المحتوى الموجود، يجب تعديل تدفق محتوى الصفحة. أدناه مثال بسيط يرسم مستطيلًا نصف شفاف باستخدام الحالة التي تم إنشاؤها حديثًا.

```csharp
// Build a content stream that uses the graphics state GS0
var content = new Aspose.Pdf.Operator.GSave();
content.Operators.Add(new Aspose.Pdf.Operator.SetGraphicsState("GS0"));
content.Operators.Add(new Aspose.Pdf.Operator.SetFillColorRgb(1, 0, 0)); // red fill
content.Operators.Add(new Aspose.Pdf.Operator.Rectangle(100, 500, 200, 100));
content.Operators.Add(new Aspose.Pdf.Operator.FillPath());
content.Operators.Add(new Aspose.Pdf.Operator.GRestore());

page.Contents.Add(content);
```

*لماذا هذا مهم*: المشغل `gs` (`SetGraphicsState`) يخبر مُعالج PDF باستخدام قيم الشفافية المعرفة في `GS0` لأي أوامر رسم لاحقة. يضمن الزوج `grestore`/`gsave` بقاء عناصر الصفحة الأخرى غير متأثرة.

## الخطوة 8 – حفظ ملف PDF المعدل

أخيرًا، اكتب المستند المحدث مرة أخرى إلى القرص.

```csharp
// Save the PDF with the new opacity settings
string outputPath = @"C:\MyFolder\output.pdf";
doc.Save(outputPath);
```

*لماذا هذا مهم*: الحفظ ينهى جميع التغييرات، يدمج حالة الرسومات الجديدة، وينتج ملف PDF يمكن لأي عارض (Adobe Acrobat، Chrome، إلخ) عرضه بالشفافية المقصودة.

### النتيجة المتوقعة

افتح `output.pdf` في عارض PDF. يجب أن ترى مستطيلًا أحمر حدوده عتمة بنسبة 80 % وتعبئته عتمة بنسبة 40 %، يندمج بسلاسة مع أي محتوى خلفية. باقي الصفحة يبقى دون تغيير.

## الاختلافات الشائعة وحالات الحافة

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|--------|
| **مستويات شفافية متعددة** | إنشاء حالات رسومات إضافية (`GS1`, `GS2`, …) بقيم `CA`/`ca` مختلفة والإشارة إليها حيثما تحتاج | يسمح بالتحكم الدقيق في العناصر المختلفة |
| **وضعيات مزج مختلفة** | استخدم `"Multiply"`، `"Screen"`، `"Overlay"` إلخ، بدلاً من `"Normal"` في إدخال `BM` | ينتج تأثيرات مزج فنية |
| **التطبيق على تدفق محتوى موجود** | أدخل `SetGraphicsState` قبل المشغلات الرسم المحددة التي تريد التأثير عليها | يمنع الشفافية غير المرغوبة على الكائنات غير المتعلقة |
| **ملفات PDF الكبيرة** | معالجة الصفحات في حلقة `foreach (Page p in doc.Pages)` لتجنب تحميل الملف بالكامل في الذاكرة مرة واحدة | يحسن الأداء ويقلل من ضغط الذاكرة |
| **عدم وجود ExtGState موجود** | الكود في الخطوة 4 ينشئ واحدًا إذا كان مفقودًا، لذا لا يلزم أي معالجة إضافية | يضمن وجود القاموس |

### نصيحة احترافية

عند إضافة العديد من حالات الرسومات المخصصة، حافظ على تسمية متسقة (`GS0`, `GS1`, …) ووثّق هدف كل حالة في كتلة تعليق. هذا يجعل الصيانة المستقبلية أسهل، خاصةً في المشاريع التعاونية.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله. يتضمن جميع الخطوات، وتعليمات `using` الضرورية، وتعليقات.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

namespace PdfOpacityDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the PDF
            string inputPath = @"C:\MyFolder\input.pdf";
            using var doc = new Document(inputPath);

            // 2. Get the first page (adjust index for other pages)
            var page = doc.Pages[1];

            // 3. Open the page's resource dictionary
            var dictEditor = new DictionaryEditor(page.Resources);

            // 4. Retrieve or create the ExtGState dictionary
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary()
                            ?? new CosPdfDictionary(doc);

            // 5. Create a new graphics state with desired opacity
            var newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            newGs.Add("CA", new CosPdfNumber(0.8));          // stroke opacity (80%)
            newGs.Add("ca", new CosPdfNumber(0.4));          // fill opacity (40%)
            newGs.Add("BM", new CosPdfName("Normal"));      // blend mode

            // 6. Register the graphics state as "GS0"
            extGState.Add("GS0", newGs);
            dictEditor["ExtGState"] = extGState; // write back to resources

            // 7. (Optional) Draw a rectangle using the new opacity
            var content = new Operator.GSave();
            content.Operators.Add(new Operator.SetGraphicsState("GS0"));
            content.Operators.Add(new Operator.SetFillColorRgb(1, 0, 0)); // red
            content.Operators.Add(new Operator.Rectangle(100, 500, 200, 100));
            content.Operators.Add(new Operator.FillPath());
            content.Operators.Add(new Operator.GRestore());

            page.Contents.Add(content);

            // 8. Save the modified PDF
            string outputPath = @"C:\MyFolder\output.pdf";
            doc.Save(outputPath);

            Console.WriteLine("PDF saved with new opacity settings at: " + outputPath);
        }
    }
}
```

شغّل البرنامج،

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تعيين خلفيات الصور في ملفات PDF باستخدام Aspose.PDF for .NET: دليل شامل](/pdf/english/net/images-graphics/aspose-pdf-net-set-image-backgrounds/)
- [كيفية إنشاء خطوط متقطعة في ملفات PDF باستخدام Aspose.PDF for .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [كيفية تخصيص ملفات PDF باستخدام Aspose.PDF for .NET: تعيين هوامش الصفحة ورسم خطوط](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}