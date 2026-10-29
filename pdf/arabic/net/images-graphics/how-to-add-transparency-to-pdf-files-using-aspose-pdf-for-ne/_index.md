---
category: general
date: 2026-09-08
description: أضف الشفافية إلى ملفات PDF باستخدام Aspose.PDF لـ .NET – تعلّم كيفية
  ضبط شفافية الخط والملء، وضع الدمج، وحفظ النتيجة في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- aspose.pdf transparency
- pdf graphics state
- extgstate dictionary
- pdf opacity settings
language: ar
lastmod: 2026-09-08
og_description: أضف الشفافية إلى PDF باستخدام Aspose.PDF لـ .NET. يوضح هذا البرنامج
  التعليمي كيفية تعديل قاموس ExtGState، وتعيين الشفافية ووضع المزج، وحفظ الملف المحدث.
og_image_alt: Screenshot of a PDF page showing semi‑transparent shapes created with
  Aspose.PDF
og_title: إضافة الشفافية إلى PDF باستخدام Aspose.PDF – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Add transparency to PDF with Aspose.PDF for .NET – learn to set stroke
    and fill opacity, blend mode, and save the result in minutes.
  headline: How to add transparency to PDF files using Aspose.PDF for .NET
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: كيفية إضافة الشفافية إلى ملفات PDF باستخدام Aspose.PDF لـ .NET
url: /ar/net/images-graphics/how-to-add-transparency-to-pdf-files-using-aspose-pdf-for-ne/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة الشفافية إلى ملفات PDF باستخدام Aspose.PDF for .NET

إذا كنت بحاجة إلى **إضافة شفافية إلى مستندات PDF**، فإن هذا الدليل يوضح لك بالضبط كيفية تعديل حالة الرسومات باستخدام Aspose.PDF for .NET. ستتعلم كيفية ضبط شفافية الخط، شفافية التعبئة، ووضع المزج على صفحة واحدة، ثم حفظ النتيجة كملف جديد.

الشفافية هي متطلب شائع للعلامات المائية، الرسومات المتراكبة، أو التأثيرات البصرية في التقارير. في هذا البرنامج التعليمي سترى الكود الكامل القابل للتنفيذ، وتفهم لماذا كل استدعاء API مهم، وتحصل على نصائح للتعامل مع الحالات الحدية مثل فقدان مدخلات الموارد.

## ما ستحتاجه

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
* رخصة صالحة لـ Aspose.PDF for .NET (الإصدار التجريبي المجاني يعمل للاختبار)
* ملف PDF إدخال باسم `input.pdf` موجود في مجلد يمكنك الإشارة إليه من الكود
* بيئة تطوير C# (Visual Studio، Rider، أو VS Code)

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf`.

## نظرة عامة على حالة رسومات PDF

حالة رسومات PDF تُخزن في **قاموس ExtGState** داخل قاموس موارد الصفحة. كل مدخل يحدد معلمات العرض مثل عرض الخط، الشفافية، ووضع المزج. بإنشاء كائن حالة رسومات جديد وإضافته إلى قاموس `ExtGState`، يمكنك إعادة استخدام إعدادات الشفافية نفسها عبر أوامر رسم متعددة.

فهم هذا الهيكل يساعدك على تجنب المشكلات الشائعة، مثل محاولة ضبط الشفافية مباشرة على كائن `Page` (الذي لا يدعم API ذلك). بدلاً من ذلك، تتعامل مع كائنات COS منخفضة المستوى التي تتطابق واحدًا لواحد مع مواصفات PDF.

## الخطوة 1: تحميل مستند PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Cos;

// Load the source PDF
var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");
```

*لماذا هذه الخطوة؟*  
`Document` هو نقطة الدخول لأي تعديل على PDF. تحميل الملف ينشئ تمثيلًا في الذاكرة يمكنك تحريره دون لمس الملف الأصلي على القرص.

## الخطوة 2: الحصول على الصفحة الأولى ومحرر قاموس الموارد الخاص بها

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor provides convenient access to the page’s resources
var resourceEditor = new DictionaryEditor(page.Resources);
```

*لماذا هذه الخطوة؟*  
جميع مدخلات حالة الرسومات تعيش داخل موارد الصفحة. `DictionaryEditor` ي抽象 التعامل مع قاموس COS منخفض المستوى، مما يتيح لك قراءة أو إنشاء مدخلات مثل `ExtGState`.

## الخطوة 3: استرجاع قاموس ExtGState من موارد الصفحة

```csharp
// The ExtGState entry may already exist; if not, create it
CosPdfDictionary extGStateDict;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a new ExtGState dictionary and attach it to the page resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourceEditor.Add("ExtGState", extGStateDict);
}
```

*لماذا هذه الخطوة؟*  
قد يتجاهل PDF قاموس `ExtGState` تمامًا. الكود أعلاه يتعامل بأمان مع الحالتين، سواء كان القاموس موجودًا أو مفقودًا، مما يضمن أن البرنامج التعليمي يعمل مع أي ملف PDF إدخال.

## الخطوة 4: إنشاء قاموس حالة رسومات جديد وتعريف مدخلاته

```csharp
// Create an empty dictionary that will hold our transparency settings
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Define the entries:
//   CA – stroke opacity (0 = fully transparent, 1 = opaque)
//   ca – fill opacity
//   BM – blend mode (Normal, Multiply, etc.)
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity = 100%
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity = 50%
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Standard blend mode
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*لماذا هذه الخطوة؟*  
`CA` و `ca` هما المشغلان في PDF الذين يتحكمان في الشفافية للخط (stroke) وللتعبئة (fill) على التوالي. ضبط `BM` إلى `Normal` يحافظ على سلوك التركيب الافتراضي، لكن يمكنك تجربة `Multiply` أو `Screen` للحصول على تأثيرات فنية.

## الخطوة 5: إضافة حالة الرسومات الجديدة إلى قاموس ExtGState

```csharp
// Choose a unique name for the graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

*لماذا هذه الخطوة؟*  
الاسم `GS0` يصبح مرجعًا يمكنك استخدامه لاحقًا في تدفقات المحتوى (`/GS0 gs`). إضافته إلى `ExtGState` يجعل PDF على علم بمعلمات الشفافية الجديدة.

## الخطوة 6: تطبيق حالة الرسومات في تدفق المحتوى (اختياري)

إذا أردت رؤية التأثير فورًا، يمكنك إضافة أمر رسم بسيط يستخدم الحالة الجديدة:

```csharp
// Build a content stream that draws a semi‑transparent rectangle
var content = new PageContent();
content.Operators.Add(new Operator("q"));                     // Save graphics state
content.Operators.Add(new Operator("GS0", "gs"));            // Set our custom graphics state
content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg")); // Set fill color (light blue)
content.Operators.Add(new Operator("100", "500", "200", "100", "re")); // Rectangle
content.Operators.Add(new Operator("f"));                    // Fill
content.Operators.Add(new Operator("Q"));                     // Restore graphics state

// Insert the new content at the beginning of the page
page.Contents.Insert(0, content);
```

*لماذا هذه الخطوة؟*  
المقتطف الاختياري يوضح كيف يتم فعليًا استخدام حالة الرسومات التي أضفتها (`GS0`). سيظهر المستطيل بشفافية تعبئة 50 % بينما يبقى حدّه غير شفاف تمامًا.

## الخطوة 7: حفظ مستند PDF المعدل

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

الملف الناتج، `output.pdf`، يحتوي على مدخل `ExtGState` الجديد، وإذا أضفت المحتوى الاختياري، فستظهر طبقة مستطيلة شبه شفافة.

### النتيجة المتوقعة

عند فتح `output.pdf` في Adobe Acrobat Reader أو أي عارض PDF، يجب أن ترى:

* محتوى الصفحة الأصلي دون تغيير.
* إذا نفذت كود الرسم الاختياري، مستطيل أزرق فاتح شفافيته 50 %، مما يسمح للصفحة الأساسية بالظهور من خلاله.

## قائمة المصدر الكاملة

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class AddTransparencyExample
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2. Get the first page and its resources
        var page = pdfDoc.Pages[1];
        var resourceEditor = new DictionaryEditor(page.Resources);

        // 3. Retrieve or create ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
            extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            resourceEditor.Add("ExtGState", extGStateDict);
        }

        // 4. Create new graphics state with transparency settings
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // 5. Add the graphics state to ExtGState with a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Draw a rectangle using the new state
        var content = new PageContent();
        content.Operators.Add(new Operator("q"));
        content.Operators.Add(new Operator("GS0", "gs"));
        content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg"));
        content.Operators.Add(new Operator("100", "500", "200", "100", "re"));
        content.Operators.Add(new Operator("f"));
        content.Operators.Add(new Operator("Q"));
        page.Contents.Insert(0, content);

        // 7. Save the updated PDF
        pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

انسخ الكود إلى تطبيق console، استبدل `YOUR_DIRECTORY` بمسار المجلد الفعلي، وشغّله. سيُنتج البرنامج `output.pdf` مع إعدادات الشفافية المضافة.

## المشكلات الشائعة وكيفية تجنبها

| العَرَض | السبب | الحل |
|---------|-------|-----|
| `KeyNotFoundException` على "ExtGState" | الصفحة لا تحتوي على مدخل `ExtGState`. | الدليل بالفعل ينشئ القاموس إذا كان مفقودًا؛ تأكد من استخدام كتلة الشرط المقدمة. |
| الشفافية غير مرئية في العارض | أوامر الرسم لا تشير أبدًا إلى `GS0`. | أضف عامل `gs` (`"GS0 gs"`) قبل أي عملية رسم/تعبئة، كما هو موضح في المقتطف الاختياري. |
| PDF يصبح معطوبًا بعد الحفظ | خلط واجهات برمجة التطبيقات عالية المستوى `Page` مع كائنات COS منخفضة المستوى بشكل غير صحيح. | التزم بنمط استرجاع `CosPdfDictionary` عبر `DictionaryEditor` وتجنب تعديل القاموس نفسه مرتين. |
| وضع المزج لا يؤثر | العارض لا يدعم وضع المزج المحدد. | استخدم `Normal` لتوافق واسع؛ جرب `Multiply` فقط في العارضات التي تقرّب الدعم. |

## الخطوات التالية

الآن بعد أن عرفت كيفية **إضافة شفافية إلى ملفات PDF**، يمكنك:

* تطبيق نفس حالة الرسومات على صفحات متعددة عن طريق التكرار عبر `pdfDoc.Pages`.
* دمج الشفافية مع مسارات القص للحصول على علامات مائية متقدمة.
* استكشاف مدخلات ExtGState أخرى مثل `SM` (تعديل الخط) أو `CA

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إضافة وتنسيق طوابع النص في ملفات PDF باستخدام Aspose.PDF for .NET | العلامات المائية والخلفيات](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [كيفية إضافة علامة مائية صورة دوارة إلى ملفات PDF باستخدام Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [كيفية إضافة طوابع الصفحات في ملفات PDF باستخدام Aspose.PDF for .NET: دليل شامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}