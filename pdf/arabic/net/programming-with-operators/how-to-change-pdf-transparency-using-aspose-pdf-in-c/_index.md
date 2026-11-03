---
category: general
date: 2026-10-04
description: تعلم كيفية تغيير شفافية PDF باستخدام Aspose.Pdf في C#. يضيف هذا الدليل
  خطوة بخطوة حالة رسومية مخصصة لضبط الشفافية ووضع الدمج.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: ar
lastmod: 2026-10-04
og_description: تغيير شفافية PDF في C# باستخدام Aspose.Pdf. اتبع هذا الدرس المختصر
  لتعديل التعتيم، وضع الدمج، وحالة الرسومات في ملفات PDF الخاصة بك.
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: تغيير شفافية PDF باستخدام Aspose.Pdf – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: كيفية تغيير شفافية PDF باستخدام Aspose.Pdf في C#
url: /ar/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير شفافية PDF باستخدام Aspose.Pdf في C#

إذا كنت بحاجة إلى **تغيير شفافية PDF** في مشروع .NET، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Pdf. في نهاية البرنامج التعليمي ستحصل على ملف PDF حيث تستخدم الكائنات المحددة شفافية مخصصة ووضع دمج، دون الحاجة إلى أي أدوات خارجية.

التعامل مع شفافية PDF هو مطلب شائع للعلامات المائية، الرسومات المتراكبة، أو التأثيرات البصرية الدقيقة. تغطي الخطوات أدناه كل ما تحتاجه — من تحميل المستند إلى تحرير **قائمة ExtGState**، إنشاء حالة رسومية جديدة، وحفظ النتيجة.

## المتطلبات المسبقة

* **Aspose.Pdf for .NET** (الإصدار 23.12 أو أحدث). يمكنك تثبيته عبر NuGet:

```bash
dotnet add package Aspose.Pdf
```

* بيئة تطوير .NET (Visual Studio، VS Code، أو `dotnet` CLI).
* ملف PDF إدخال موجود في دليل معروف (المثال يستخدم `input.pdf`).

لا توجد مكتبات إضافية مطلوبة.

## الخطوة 1: تحميل مستند PDF

العملية الأولى هي فتح ملف PDF الموجود. استخدام كتلة `using` يضمن تحرير مقبض الملف تلقائيًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*لماذا هذا مهم*: تحميل المستند ينشئ تمثيلًا في الذاكرة يمكنك تعديله. كما أن فئة `Document` تمنحك الوصول إلى كائنات COS منخفضة المستوى، وهو أمر أساسي لتغيير شفافية PDF.

## الخطوة 2: الوصول إلى موارد الصفحة الأولى

حالات الرسومات تُخزن في قاموس موارد الصفحة. نسترجع الصفحة الأولى ونغلف مواردها باستخدام `DictionaryEditor` حتى نتمكن من تحريرها بسهولة.

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*شرح*: `DictionaryEditor` يُجرد التعامل مع قاموس COS، مما يتيح لك قراءة وكتابة الإدخالات مثل `ExtGState` دون الحاجة إلى التعامل مع صsyntax PDF الخام.

## الخطوة 3: الحصول على (أو إنشاء) قاموس ExtGState

قائمة **ExtGState** تحتفظ بكائنات حالة رسومية مسماة. إذا كانت موجودة بالفعل نعيد استخدامها؛ وإلا ننشئ واحدة جديدة.

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*لماذا هذه الخطوة*: بدون إدخال `ExtGState` لا يمتلك محرك PDF مكانًا للبحث عن إعدادات الشفافية المخصصة. إضافة القاموس تجعل الصفحة على علم بأي حالات رسومية جديدة تقوم بتعريفها.

## الخطوة 4: تعريف حالة رسومية جديدة مع الشفافية ووضع الدمج

حالة الرسومات هي مجموعة من معلمات عرض PDF. هنا نقوم بتعيين:

* **CA** – شفافية الخط (1 = معتم بالكامل)
* **ca** – شفافية التعبئة (0.5 = 50 % شفاف)
* **BM** – وضع الدمج (`Normal` هو الافتراضي، لكن يمكنك التجربة مع `Multiply`، `Screen`، إلخ)

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*ملاحظة*: قيم `CosPdfNumber` هي أعداد عائمة بين 0 و 1. تعديلها يتيح لك ضبط دقة ظهور الخطوط والتعبئات الشفافة. وضع الدمج يحدد كيفية تفاعل المحتوى الشفاف مع الرسومات الأساسية.

## الخطوة 5: تسجيل حالة الرسومات في ExtGState

نمنح الحالة الجديدة اسمًا (`GS0`). لاحقًا، عندما ترسم كائنات، تشير إلى هذا الاسم في تدفق المحتوى.

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*أفضل ممارسة*: استخدم نمط تسمية واضح (`GS0`، `GS_Watermark`، إلخ) حتى تتمكن من إدارة حالات متعددة دون ارتباك.

## الخطوة 6: تطبيق حالة الرسومات على محتوى الصفحة (اختياري)

إذا كنت ترغب في تطبيق الشفافية الجديدة على عناصر الصفحة الموجودة، تحتاج إلى تعديل تدفق محتوى الصفحة. أدناه مثال بسيط يضيف مستطيلًا شبه شفافًا فوق الصفحة.

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*لماذا يعمل*: عامل `SetGraphicsState` يخبر مفسر PDF باستخدام المعلمات المعرفة في `GS0` لجميع أوامر الرسم اللاحقة. وبالتالي يظهر المستطيل بشفافية تعبئة 50 % مع الحفاظ على حدوده غير شفافة بالكامل.

## الخطوة 7: حفظ ملف PDF المعدل

أخيرًا، اكتب التغييرات مرة أخرى إلى القرص.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

ملف `output.pdf` الناتج يحتوي على حالة الرسومات الجديدة، وأي محتوى يشير إلى `GS0` سيُعرض بالشفافية المحددة.

---

![مخطط يوضح تغيير شفافية PDF](/images/pdf-transparency-before-after.png "صفحة PDF قبل وبعد تطبيق حالة رسومات مخصصة")
*نص بديل للصورة (لتحسين محركات البحث وإمكانية الوصول):* **مثال على تغيير شفافية PDF – الأصل مقابل الصفحة المعدلة**

## مثال عملي كامل

بجمع كل شيء معًا، إليك برنامجًا واحدًا قابلًا للتنفيذ يغير شفافية PDF ويضيف مستطيلًا شبه شفاف.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### النتيجة المتوقعة

* يتم إنشاء الملف `output.pdf` في المجلد المحدد.
* إذا فتحت ملف PDF، سترى مستطيلًا أحمر تعبئته شفافة بنسبة 50 % بينما يبقى حدّه غير شفاف بالكامل.
* أي كائنات أخرى تشير إلى `GS0` (مثل العلامات المائية) ستورث نفس الشفافية ووضع الدمج.

## أسئلة شائعة ومعالجة الحالات الطرفية

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تغيير شفافية الخط فقط؟** | عيّن `CA` إلى القيمة المطلوبة واترك `ca` عند `1`. |
| **ما أوضاع الدمج المدعومة؟** | جميع أوضاع دمج PDF القياسية (`Normal`، `Multiply`، `Screen`، `Overlay`، إلخ) مقبولة عبر إدخال `BM`. |
| **هل أحتاج إلى تنظيف القاموس بعد الاستخدام؟** | لا. كائنات `CosPdfDictionary` تُدار بواسطة Aspose.Pdf وتُكتب إلى الملف عند استدعاء `Save`. |
| **كيف يعمل هذا مع ملفات PDF المشفرة؟** | حمّل المستند باستخدام كلمة المرور المناسبة (`new Document(path, password)`). تعديل حالة الرسومات يعمل بنفس الطريقة بمجرد فك تشفير المستند في الذاكرة. |
| **هل يمكن تطبيق نفس حالة الرسومات على صفحات متعددة؟** | نعم. أضف إدخال `GS0` إلى قاموس `ExtGState` لكل صفحة، أو أنشئ قاموسًا مشتركًا واحدًا في موارد المستند العامة وأشر إليه من كل صفحة. |

## نصائح وأفضل الممارسات

* **نصيحة احترافية:** احرص على أن تكون أسماء حالات الرسومات قصيرة ولكن وصفية (`GS_Watermark`، `GS_Overlay`). هذا يجنب تصادم الأسماء ويسهل عملية تصحيح الأخطاء.
* **احذر من:** الكتابة فوق إدخال `ExtGState` موجود عن طريق الخطأ. تحقق دائمًا من `resourcesEditor.ContainsKey("ExtGState")` قبل إنشاء قاموس جديد.
* **ملاحظة أداء:** تعديل كائنات COS منخفضة المستوى سريع، ولكن إذا كنت تحتاج إلى معالجة آلاف الصفحات فكر في تجميع التغييرات لتقليل الضغط على الذاكرة.

## الخطوات التالية

الآن بعد أن عرفت كيفية **تغيير شفافية PDF**، يمكنك استكشاف المواضيع ذات الصلة مثل:

* إضافة **علامات مائية** بشفافية مخصصة (`PDF opacity C#`).
* استخدام **أوضاع دمج مختلفة** لتحقيق تأثيرات فنية (`blend mode PDF`).
* إنشاء مكتبات **حالات رسومات** قابلة لإعادة الاستخدام لتوليد مستندات على نطاق واسع (`Aspose.Pdf graphics state`).

جرّب تعديل قيم `ca` و `CA`، أو استبدل المستطيل الأحمر بصورة أو نصًا متراكبًا. المبادئ نفسها تنطبق — فقط أشر إلى حالة الرسومات `GS0` قبل رسم المحتوى الجديد.

---

*لقد تعلمت كيفية تغيير شفافية PDF باستخدام Aspose.Pdf في C#. طبق هذه التقنيات لتحسين التقارير، الفواتير، أو أي مخرجات تعتمد على PDF حيث تكون التفاصيل البصرية مهمة.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من التعليمات البرمجية مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تغيير شفافية PDF باستخدام Aspose.PDF – دليل C# كامل](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [تغيير شفافية PDF في C# – دليل Aspose كامل](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [إضافة شفافية إلى PDF باستخدام Aspose – دليل C# كامل](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}