---
category: general
date: 2026-10-01
description: أضف ExtGState مخصصًا إلى ملف PDF باستخدام Aspose.PDF لتعيين الشفافية
  بسرعة. اتبع هذا الدليل لتتعلم كيفية تعيين شفافية PDF باستخدام حالة رسومية مخصصة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom extgstate pdf
- how to set transparency pdf
- Aspose.PDF graphics state
- PDF opacity settings
- PDF blend mode tutorial
language: ar
lastmod: 2026-10-01
og_description: أضف ExtGState مخصصًا إلى ملف PDF وتعلم كيفية ضبط شفافية PDF ببضع أسطر
  من C#. يغطي هذا الدليل كل خطوة من تحميل الملف إلى حفظ النتيجة.
og_image_alt: Screenshot of a PDF page showing transparent graphics after adding a
  custom ExtGState
og_title: إضافة ExtGState مخصص إلى PDF – دليل Aspose.PDF الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add custom ExtGState PDF using Aspose.PDF to set transparency PDF quickly.
    Follow this guide to learn how to set transparency PDF with a custom graphics
    state.
  headline: Add custom ExtGState PDF with Aspose.PDF – step‑by‑step guide
  type: TechArticle
tags:
- PDF
- Aspose.PDF
- C#
- GraphicsState
title: إضافة ExtGState مخصص إلى PDF باستخدام Aspose.PDF – دليل خطوة بخطوة
url: /ar/net/images-graphics/add-custom-extgstate-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ExtGState مخصص إلى PDF باستخدام Aspose.PDF – دليل خطوة بخطوة

إذا كنت بحاجة إلى **إضافة ExtGState مخصص إلى PDF** للتحكم في الشفافية وأنماط الدمج، فإن هذا الدليل يوضح لك بالضبط كيف تفعل ذلك. سترى مثالًا كاملًا قابلاً للتنفيذ يُظهر **كيفية ضبط شفافية PDF** باستخدام Aspose.PDF for .NET.

في الأقسام التالية سنغطي حزمة NuGet المطلوبة، وتحليل الكود خطوة بخطوة، ونصائح للتعامل مع الحالات الخاصة مثل الصفحات المتعددة أو أنماط الدمج المخصصة. في النهاية ستتمكن من تعديل أي PDF موجود وتطبيق حالة رسومية شفافة دون مغادرة بيئة التطوير المتكاملة.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
- Visual Studio 2022 (أو أي محرر C# تفضله)
- حزمة **Aspose.PDF for .NET** NuGet (الإصدار 23.12 أو أحدث)
- ملف PDF تجريبي اسمه `input.pdf` موجود في مجلد يمكنك الإشارة إليه من المشروع

> **نصيحة احترافية:** استخدم مجلد “Resources” مخصص في الحل الخاص بك للحفاظ على ملفات PDF الإدخال والإخراج معًا. هذا يتجنب الأخطاء المتعلقة بالمسارات عند تشغيل الكود.

## تثبيت Aspose.PDF

افتح وحدة تحكم مدير الحزم NuGet وشغّل:

```bash
dotnet add package Aspose.PDF
```

توفر الحزمة الفئات `Aspose.Pdf.Document`، `CosPdfDictionary`، والفئات المرتبطة المستخدمة في عينة الكود.

## الخطوة 1 – تحميل مستند PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;

// Load the source PDF
using var pdfDocument = new Document("Resources/input.pdf");
```

**لماذا هذه الخطوة مهمة:**  
`Document` تمثل ملف PDF بالكامل في الذاكرة. فتحه داخل كتلة `using` يضمن تحرير جميع الموارد غير المُدارة بعد الانتهاء من المعالجة.

## الخطوة 2 – الوصول إلى قاموس موارد الصفحة الأولى

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// The resource dictionary holds objects like fonts, XObjects, and ExtGState entries
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**شرح:**  
كل صفحة PDF لديها قاموس *Resources* يجمع الكائنات القابلة لإعادة الاستخدام. من خلال تعديل هذا القاموس يمكننا حقن حالة رسومية جديدة يمكن للصفحة الإشارة إليها لاحقًا.

## الخطوة 3 – استرجاع (أو إنشاء) قاموس ExtGState

```csharp
// Try to get the existing ExtGState dictionary; create one if it does not exist
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

**لماذا نتحقق أولًا:**  
بعض ملفات PDF تُعرّف مسبقًا إدخال `ExtGState`. إضافة نسخة مكررة سيؤدي إلى استبدال الحالات الموجودة وقد يتسبب في كسر محتوى آخر. هذا الكود الوقائي يحافظ على الإدخالات الأصلية دون تعديل.

## الخطوة 4 – بناء حالة رسومية مخصصة

```csharp
// Create an empty dictionary that will become our custom graphics state
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // CA – stroke opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // ca – fill opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // BM – blend mode (Normal, Multiply, Screen, etc.)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Add each entry to the dictionary
foreach (var entry in graphicsStateEntries)
{
    newGraphicsState.Add(entry);
}
```

**ما الذي يفعله كل مفتاح:**

| المفتاح | المعنى | القيم النموذجية |
|-----|---------|----------------|
| `CA` | شفافية الخط | `0.0` (شفاف تمامًا) → `1.0` (معتم) |
| `ca` | شفافية التعبئة | نفس النطاق كما في `CA` |
| `BM` | نمط الدمج | `Normal`, `Multiply`, `Screen`, `Overlay`, إلخ |

بتعيين `ca` إلى `0.5` نجعل الأشكال المملوءة شفافة بنسبة 50 %، بينما يبقى `CA` معتمًا بالكامل للخطوط. تغيير `BM` يتيح لك تجربة تأثيرات دمج مشابهة لتلك في Photoshop.

## الخطوة 5 – تسجيل الحالة الرسومية المخصصة تحت اسم فريد

```csharp
// Choose a unique name for the new state, e.g., "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

**قواعد التسمية:**  
توصي مواصفات PDF باستخدام معرفات قصيرة وعالية الأحرف. استخدام `GS0` (Graphics State 0) يجعل الاسم سهل الإشارة إليه من تدفقات المحتوى.

## الخطوة 6 – تطبيق الحالة الرسومية المخصصة في تدفق المحتوى (اختياري)

إذا أردت رسم مستطيل شفاف على الصفحة الأولى، يمكنك إضافة المشغلات التالية في البداية:

```csharp
// Build the content stream that uses the new graphics state
var content = new Operator[]
{
    new Operator("q"),                 // Save graphics state
    new Operator("GS0", "gs"),         // Set our custom ExtGState
    new Operator("0.5 0.5 1 rg"),      // Set fill color (light blue)
    new Operator("100 500 200 100 re"),// Rectangle (x, y, width, height)
    new Operator("f"),                 // Fill the rectangle using the fill opacity
    new Operator("Q")                  // Restore graphics state
};

// Add the operators to the page's content
firstPage.Contents.Add(content);
```

**لماذا هذه الخطوة اختيارية:**  
الخطوات السابقة فقط *تعرف* الحالة الرسومية. لرؤية التأثير يجب الإشارة إليها من تدفق محتوى الصفحة. المقتطف أعلاه يوضح حالة استخدام عملية، لكن يمكنك أيضًا تطبيق الحالة على أوامر الرسم الموجودة في PDF الخاص بك.

## الخطوة 7 – حفظ PDF المعدل

```csharp
// Persist the changes to a new file
pdfDocument.Save("Resources/output.pdf");
```

عند فتح `output.pdf` ستلاحظ أن المستطيل يُعرض بشفافية تعبئة 50 % بينما يبقى حدّه معتمًا بالكامل—وهو بالضبط نتيجة **كيفية ضبط شفافية PDF** باستخدام ExtGState مخصص.

## التعامل مع صفحات متعددة

إذا كنت بحاجة إلى نفس تأثير الشفافية على كل صفحة، قم بالتكرار عبر `pdfDocument.Pages` وكرر **الخطوة 2**‑**الخطوة 5** لكل موارد الصفحة. احرص على إضافة الحالة الرسومية مرة واحدة فقط لكل صفحة؛ إعادة استخدام القاموس نفسه عبر الصفحات غير مسموح به وفقًا لمواصفات PDF.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    var editor = new DictionaryEditor(page.Resources);
    // Ensure ExtGState exists, then add GS0 as shown earlier
    // (code omitted for brevity)
}
```

## الأخطاء الشائعة وكيفية تجنبها

| العَرَض | السبب | الحل |
|---------|-------|-----|
| لا تغيير في الشفافية | قيم `ca` أو `CA` خارج النطاق 0‑1 | استخدم قيم عشرية بين `0.0` و `1.0`. |
| اختفاء المحتوى | الحالة الرسومية غير مُطبقة (مشغل `gs` مفقود) | أدرج `GS0 gs` قبل أوامر الرسم. |
| فشل فتح PDF | مفتاح مكرر في قاموس `ExtGState` | تحقق من `extGStateDict.ContainsKey("GS0")` قبل الإضافة. |
| تجاهل نمط الدمج | العارض لا يدعم النمط المحدد | التزم بالأنماط القياسية مثل `Normal`, `Multiply`. |

## مثال كامل قابل للتنفيذ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF
        using var pdfDocument = new Document("Resources/input.pdf");

        // Work with the first page
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = new CosPdfDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create custom graphics state
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGraphicsState.Add(e);

        // Register under a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a transparent rectangle
        var ops = new Operator[]
        {
            new Operator("q"),
            new Operator("GS0", "gs"),
            new Operator("0.5 0.5 1 rg"),
            new Operator("100 500 200 100 re"),
            new Operator("f"),
            new Operator("Q")
        };
        firstPage.Contents.Add(ops);

        // Save result
        pdfDocument.Save("Resources/output.pdf");
    }
}
```

**الناتج المتوقع:**  
فتح `output.pdf` يُظهر مستطيلًا أزرق فاتحًا عند الإحداثيات (100, 500) بشفافية تعبئة 50 %. يبقى حد المستطيل معتمًا بالكامل لأن `CA` مُعيَّن إلى `1.0`.

## الخلاصة

أنت الآن تعرف كيف **تضيف ExtGState مخصص إلى PDF** باستخدام Aspose.PDF وتتحكم بدقة في الشفافية وأنماط الدمج—مجيبًا على السؤال الشائع **كيفية ضبط شفافية PDF**. غطى الدليل تحميل المستند، تعديل قاموس الموارد، تعريف حالة رسومية، تطبيقها، وحفظ النتيجة.

بعد ذلك قد ترغب في استكشاف:

- استخدام أنماط دمج مختلفة (`Multiply`, `Screen`) لتأثيرات إبداعية.  
- تطبيق نفس ExtGState على كائنات الصور XObjects لشعارات شبه شفافة.  
- أتمتة العملية لتعديلات PDF جماعية في خدمة خلفية.

لا تتردد في تجربة القيم، وإعادة تسمية الحالة الرسومية، أو

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [إضافة شفافية إلى PDF باستخدام Aspose – دليل C# كامل](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [كيفية إضافة ختم صفحة إلى ملفات PDF باستخدام Aspose.PDF للـ Java (دليل 2023)](/pdf/english/java/watermarks-backgrounds/add-page-stamp-aspose-pdf-java/)
- [كيفية إضافة ختم نص إلى PDF باستخدام Aspose.PDF للـ Java: دليل شامل](/pdf/english/java/document-manipulation/aspose-pdf-java-add-text-stamp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}