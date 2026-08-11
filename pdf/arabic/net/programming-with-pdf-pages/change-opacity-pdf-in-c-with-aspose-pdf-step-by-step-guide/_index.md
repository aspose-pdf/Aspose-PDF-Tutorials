---
category: general
date: 2026-08-11
description: تغيير شفافية PDF باستخدام Aspose.Pdf في C#. تعلم كيفية إضافة الشفافية
  إلى صفحات PDF، وضبط حالة الرسومات، وحفظ النتيجة بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change opacity PDF
- how to add transparency
- add pdf transparency
language: ar
lastmod: 2026-08-11
og_description: تغيير شفافية PDF باستخدام Aspose.Pdf في C#. اتبع هذا الدليل لمعرفة
  كيفية إضافة الشفافية إلى أي مستند PDF، وتخصيص حالات الرسومات، وتصدير النتيجة.
og_image_alt: Screenshot illustrating change opacity PDF example in C# code
og_title: تغيير شفافية PDF في C# – دليل Aspose.Pdf الكامل
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  headline: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  name: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
    text: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
  - name: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
    text: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
  - name: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
    text: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
  - name: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
    text: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: تغيير شفافية PDF في C# باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تغيير شفافية PDF في C# باستخدام Aspose.Pdf – دليل خطوة بخطوة

إذا كنت بحاجة إلى **تغيير شفافية PDF** للملفات برمجيًا، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. باستخدام Aspose.Pdf for .NET يمكنك التحكم في شفافية كائنات الرسومات، النصوص، والصور دون مغادرة كود C# الخاص بك.

في الأقسام التالية ستتعلم **كيفية إضافة الشفافية** إلى صفحة PDF، ما معنى كائنات حالة الرسومات الأساسية، وكيفية حفظ المستند المعدل. يغطي الدليل أيضًا الأخطاء الشائعة عند **إضافة شفافية PDF** ويقدم نصائح للسيناريوهات الواقعية.

## ما ستحققه

* تحميل مستند PDF موجود.
* إنشاء قاموس حالة رسومات جديد يحدد قيم الشفافية.
* إدراج حالة الرسومات في قاموس موارد الصفحة.
* حفظ المستند مع تأثير **تغيير شفافية PDF** المحدث.

لا تحتاج إلى أدوات خارجية—فقط مكتبة Aspose.Pdf for .NET (الإصدار 23.10 أو أحدث) وبيئة تطوير .NET.

## المتطلبات المسبقة

* .NET 6.0 (أو .NET Framework 4.7.2+) مثبت.
* Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#.
* إشارة إلى حزمة NuGet `Aspose.Pdf`.
* ملف PDF إدخال (`input.pdf`) موجود في دليل قابل للكتابة.

> **نصيحة احترافية:** عند اختبار تغييرات الشفافية، اعمل على PDF يحتوي بالفعل على رسومات متجهة أو نص؛ الصور النقطية تتجاهل معلمات `ca` و `CA` ما لم تُوضع داخل مجموعة شفافية.

## تغيير شفافية PDF باستخدام Aspose.Pdf

جوهر الحل هو تعديل قاموس **ExtGState** (حالة الرسومات الخارجية) لصفحة. هذا القاموس يخزن معلمات مثل **ca** (شفافية الخط) و **CA** (شفافية التعبئة). بإضافة إدخال جديد يمكنك الإشارة إليه لاحقًا في تدفقات المحتوى.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;

class ChangeOpacityPdfExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var document = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 2: Access the first page and its resource dictionary
            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Step 3: Create a new graphics state dictionary with desired opacity values
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                // Fill opacity (CA) – 1.0 means fully opaque
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                // Stroke opacity (ca) – 0.5 makes lines semi‑transparent
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                // Blend mode (BM) – Normal is the default blend mode
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // Step 4: Add the new graphics state to the ExtGState dictionary
            // “GS0” is the identifier you will reference later in the content stream
            extGState.Add("GS0", newGraphicsState);

            // Optional: Demonstrate usage by drawing a semi‑transparent rectangle
            // This part shows how the new graphics state affects drawing commands.
            var canvas = new Aspose.Pdf.Drawing.Graphic(page);
            canvas.SetGraphicsState("GS0"); // Apply the opacity settings
            canvas.Rectangle(100, 500, 200, 600);
            canvas.FillColor = Color.FromRgb(255, 0, 0); // Red fill
            canvas.StrokeColor = Color.FromRgb(0, 0, 255); // Blue border
            canvas.Draw();

            // Step 5: Save the modified PDF
            document.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF saved with changed opacity.");
    }
}
```

### لماذا يعمل هذا

* **ExtGState** هو مورد PDF يخزن معلمات رسومات قابلة لإعادة الاستخدام. بإضافة إدخال مخصص (`GS0`) تقوم بإنشاء تكوين شفافية قابل لإعادة الاستخدام.
* المفتاح **ca** يتحكم في شفافية عمليات الخط (الخطوط، الحدود). المفتاح **CA** يتحكم في عمليات التعبئة (الأشكال الملونة، النص). ضبط `ca = 0.5` يجعل الخطوط شفافة بنسبة 50 %، بينما `CA = 1` يترك التعبئة غير شفافة بالكامل.
* استدعاء `SetGraphicsState("GS0")` يخبر Aspose.Pdf بإصدار عامل `/GS0 gs` في تدفق المحتوى، مما يفعّل إعدادات الشفافية الجديدة لأي أوامر رسم لاحقة.

## كيفية إضافة الشفافية إلى المحتوى الموجود

إذا كان لديك نص أو صور على الصفحة وتريد جعلها شبه شفافة دون إعادة رسمها، يمكنك حقن عامل **gs** قبل المحتوى الموجود. يوضح المقتطف التالي كيفية إضافة العامل في بداية تدفق محتوى الصفحة.

```csharp
// Retrieve the existing content stream
var content = page.Contents[1];
var originalBytes = content.ToByteArray();

// Build the new content with the graphics state applied
var gsOperator = System.Text.Encoding.ASCII.GetBytes("/GS0 gs\n");
var newBytes = new List<byte>(gsOperator);
newBytes.AddRange(originalBytes);

// Replace the page content
page.Contents[1].Replace(newBytes.ToArray());
```

### الحالات الخاصة والاعتبارات

| Situation | Recommended handling |
|-----------|----------------------|
| **صفحات متعددة** | التكرار عبر `document.Pages` وتكرار الخطوات 2‑4 لكل صفحة تريد تعديلها. |
| **شفافية مختلفة لكل عنصر** | إنشاء حالات رسومات إضافية (`GS1`, `GS2`, …) بقيم `ca`/`CA` مميزة وتطبيقها بشكل انتقائي. |
| **ملفات PDF ذات إدخالات ExtGState موجودة** | استخدام `dictEditor["ExtGState"]` بأمان؛ إذا لم يكن المفتاح موجودًا، إنشاء `CosPdfDictionary` جديد وتعيينه إلى `page.Resources`. |
| **مجموعات الشفافية** | للتجميع المعقد (مثل تداخل الصور)، ضبط قاموس `/Group` بـ `S /Transparency` و `CS /DeviceRGB`. هذا يتجاوز **تغيير شفافية PDF** الأساسي لكنه قد يكون مطلوبًا لتصاميم متقدمة. |

## إضافة شفافية PDF إلى الرسومات المتجهة

بخلاف المستطيلات، يمكنك تطبيق حالة الرسومات نفسها على أي رسم متجه—خطوط، منحنيات، أو حتى نص. إليك مثال سريع يكتب نصًا شبه شفاف:

```csharp
var textFragment = new TextFragment("Transparent text")
{
    Position = new Position(100, 400),
    TextState = { FontSize = 36, ForegroundColor = Color.Black }
};
page.Paragraphs.Add(textFragment);

// Apply the graphics state to the text fragment
textFragment.TextState.GraphicsState = "GS0";
```

خاصية `GraphicsState` في `TextState` تخبر محرك PDF بأن يرسم النص باستخدام الشفافية المعرفة في `GS0`. هذه هي أبسط طريقة لـ **إضافة شفافية PDF** إلى المحتوى النصي.

## الأخطاء الشائعة عند تغيير شفافية PDF

1. **قاموس ExtGState مفقود** – بعض ملفات PDF لا تحتوي على إدخال `ExtGState` بشكل افتراضي. في هذه الحالة، قم بإنشاء واحد:
   ```csharp
   if (!dictEditor.ContainsKey("ExtGState"))
       dictEditor.Add("ExtGState", new CosPdfDictionary(document));
   ```
2. **اسم المورد غير صحيح** – يجب أن يتطابق الاسم الذي تستخدمه في `SetGraphicsState` تمامًا مع المفتاح الذي أضفته (`GS0`). أي خطأ إملائي يؤدي إلى عرض افتراضي غير شفاف بالكامل.
3. **استبدال حالات الرسومات الموجودة** – إضافة إدخال جديد لا تستبدل الحالات الحالية. إذا أعدت استخدام اسم موجود بالفعل، قد تقوم بتغيير عناصر صفحة أخرى تشير إليه عن غير قصد.
4. **توافق المشاهد** – قد تتجاهل عارضات PDF القديمة (قبل الإصدار 1.4) الشفافية. تأكد من أن جمهورك المستهدف يستخدم عارضًا حديثًا مثل Adobe Reader DC أو عارض PDF المدمج في Chrome.

## مثال كامل يعمل

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه، لصقه، وتشغيله. يتضمن جميع توجيهات `using` اللازمة، معالجة الأخطاء، والتعليقات.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إضافة ختم نصي إلى PDF باستخدام Aspose.PDF .NET: دليل شامل](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [كيفية إضافة أختام صفحات في ملفات PDF باستخدام Aspose.PDF for .NET: دليل كامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [كيفية إضافة أختام صفحات في ملفات PDF باستخدام Aspose.PDF for .NET | دليل العلامات المائية والخلفيات](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}