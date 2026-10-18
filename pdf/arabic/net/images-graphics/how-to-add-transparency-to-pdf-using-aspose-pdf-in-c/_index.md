---
category: general
date: 2026-10-17
description: أضف الشفافية إلى ملف PDF باستخدام Aspose.PDF لـ .NET، حرّر موارد PDF،
  واحفظ ملفات PDF المعدلة في مثال واحد قابل للتنفيذ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- save modified pdf
- edit pdf resources
- Aspose.PDF transparency
- C# PDF manipulation
language: ar
lastmod: 2026-10-17
og_description: أضف الشفافية إلى ملفات PDF باستخدام Aspose.PDF لـ .NET، حرّر موارد
  PDF، واحفظ ملفات PDF المعدلة مع مثال كامل بلغة C#.
og_image_alt: Screenshot showing a PDF with added transparency using Aspose.PDF in
  C#
og_title: إضافة الشفافية إلى PDF باستخدام Aspose.PDF – دليل
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Add transparency to PDF with Aspose.PDF for .NET, edit PDF resources,
    and save modified PDF files in a single, runnable example.
  headline: How to add transparency to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
title: كيفية إضافة الشفافية إلى PDF باستخدام Aspose.PDF في C#
url: /ar/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة الشفافية إلى PDF باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **إضافة شفافية إلى PDF** بشكل برمجي، يوضح لك هذا الدليل حلاً واضحًا من البداية إلى النهاية باستخدام Aspose.PDF لـ .NET. ستتعلم كيفية **تحرير موارد PDF**، وإنشاء حالة رسومية مخصصة، و**حفظ PDF المعدل** دون مغادرة مشروع C# الخاص بك.

التعامل مع شفافية PDF غالبًا ما يبدو مخفيًا وراء عمليات PDF منخفضة المستوى. بنهاية هذا الدرس ستحصل على مثال عملي كامل يمكنك نسخه‑ولصقه، تشغيله، وتعديله لعدة صفحات أو أوضاع دمج مختلفة.

## المتطلبات المسبقة

- .NET 6.0 (أو أي نسخة حديثة من .NET)  
- حزمة NuGet لـ Aspose.PDF for .NET (`Aspose.Pdf`)  
- معرفة أساسية بـ C#  
- ملف PDF إدخال (`input.pdf`) موجود في مجلد يمكنك الإشارة إليه

> **نصيحة احترافية:** قم بتثبيت الحزمة باستخدام `dotnet add package Aspose.Pdf` قبل البدء.

## الخطوة 1: تحميل مستند PDF

العملية الأولى هي فتح ملف PDF المصدر. تمثل Aspose.PDF ملف PDF ككائن `Document`، والذي يمنحك الوصول إلى الصفحات والموارد والقواميس منخفضة المستوى.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;   // for graphics‑state objects

// Path to the original PDF
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document in a using block so it disposes automatically
using (var document = new Document(pdfPath))
{
    // The rest of the steps are inside this block
```

*لماذا هذا مهم:* فتح المستند بهذه الطريقة يضمن تحرير مقبض الملف بعد الانتهاء من التحرير، مما يمنع مشاكل قفل الملف عندما نقوم لاحقًا **بحفظ PDF المعدل**.

## الخطوة 2: الوصول إلى الصفحة الأولى وقاموس مواردها

تخزن صفحات PDF كائنات الرسومات (الخطوط، الصور، إدخالات ExtGState) في *قاموس الموارد*. لتغيير الشفافية نحتاج إلى العمل مع القاموس الفرعي `ExtGState`.

```csharp
    // Get the first page (pages are 1‑based in Aspose.PDF)
    Page page = document.Pages[1];

    // Obtain a mutable editor for the page's resources
    var resourcesEditor = new DictionaryEditor(page.Resources);

    // Retrieve the ExtGState dictionary; create it if missing
    var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                         ?? new CosPdfDictionary(document);
```

*لماذا هذا مهم:* إذا كان PDF الأصلي يحتوي بالفعل على قاموس `ExtGState`، فإننا نقوم بتمديده؛ وإلا نخلق واحدًا جديدًا حتى نتمكن بأمان من **تحرير موارد PDF**.

## الخطوة 3: بناء حالة رسومية جديدة مع الشفافية

حالة الرسومات (`ExtGState`) تحتفظ بمعلمات مثل شفافية الخط (`CA`)، شفافية التعبئة (`ca`)، ووضع الدمج (`BM`). نقوم بإنشاء قاموس فارغ ونملأه بالقيم المطلوبة.

```csharp
    // Create an empty ExtGState dictionary for the new entry
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Define the transparency entries
    var entries = new[]
    {
        // CA – stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA",
            new CosPdfNumber(1)),

        // ca – fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca",
            new CosPdfNumber(0.5)),

        // BM – blend mode (Normal is the default)
        new KeyValuePair<string, ICosPdfPrimitive>("BM",
            new CosPdfName("Normal"))
    };

    // Add each entry to the new ExtGState dictionary
    foreach (var entry in entries)
        newGraphicsState.Add(entry);
```

*لماذا هذا مهم:* إدخال `ca` هو المفتاح لـ **إضافة شفافية إلى PDF** للمحتوى الذي يستخدم هذه الحالة الرسومية. يمكنك تعديل القيمة الرقمية (0 – 1) للتحكم في مدى شفافية الكائن.

## الخطوة 4: إدراج الحالة الرسومية في موارد الصفحة

يجب أن نعطي الحالة الرسومية الجديدة اسمًا (مثال، `"GS0"`). يمكن لاحقًا الإشارة إلى هذا الاسم من قبل تدفقات المحتوى لتطبيق الشفافية.

```csharp
    // Add the new ExtGState under the name "GS0"
    extGStateDict.Add("GS0", newGraphicsState);

    // Ensure the modified ExtGState dictionary is written back to the page
    resourcesEditor["ExtGState"] = extGStateDict;
```

*لماذا هذا مهم:* بإضافة `"GS0"` إلى قاموس `ExtGState`، أي عملية رسم تختار هذه الحالة ستُظهر الشفافية المحددة. هذا هو جوهر **تحرير موارد PDF** للشفافية.

## الخطوة 5: تطبيق الحالة الرسومية على محتوى الصفحة (اختياري)

إذا كنت تريد أن يستخدم محتوى الصفحة الحالي الشفافية الجديدة تلقائيًا، يجب أن تسبق تدفق محتوى الصفحة بمشغل حالة الرسومات. يوضح المقتطف التالي كيفية تغليف المحتوى الحالي بـ `gs` (تعيين حالة الرسومات) و `Q` (استعادة حالة الرسومات).

```csharp
    // Get the current content stream
    var content = page.Contents[1]; // assume a single content stream

    // Build a new stream that sets the graphics state, draws the original content, then restores
    string gsOperator = "/GS0 gs\n"; // select the graphics state we created
    string restoreOperator = "Q\n";   // restore graphics state after drawing

    // Prepend the gs operator and append the restore operator
    string newStream = gsOperator + content.Stream.ToString() + restoreOperator;

    // Replace the original stream with the modified one
    content.Stream = new CosPdfStream(document);
    content.Stream.SetData(newStream);
```

*لماذا هذا مهم:* بدون هذه الخطوة، تكون حالة الرسومات موجودة لكنها غير مستخدمة. إضافة مشغل `gs` يخبر عارض PDF بتطبيق الشفافية على كل ما يلي.

## الخطوة 6: **حفظ PDF المعدل** إلى القرص

أخيرًا، احفظ المستند المعدل إلى ملف جديد. طريقة `Save` تتعامل مع جميع التحديثات منخفضة المستوى تلقائيًا.

```csharp
    // Path for the output PDF
    string outputPath = @"YOUR_DIRECTORY\output.pdf";

    // Persist the changes
    document.Save(outputPath);
}
```

*لماذا هذا مهم:* استدعاء `document.Save` يضمن أن **PDF المعدل** يحتوي على إدخال `ExtGState` الجديد وتدفق المحتوى الذي يشير إليه. الملف الناتج سيظهر تعبئة شبه شفافة على الصفحة الأولى.

## النتيجة المتوقعة

افتح `output.pdf` في أي عارض PDF (Adobe Reader، Chrome، إلخ) ويجب أن ترى رسومات الصفحة الأولى مُعرضة بشفافية تعبئة 50 %. إذا فحصت الـ PDF بأداة مثل **PDF‑Tron** أو **iText**، ستجد إدخالًا في قاموس `ExtGState` باسم `GS0` مع قيمة `ca` مضبوطة على `0.5`.

## الحالات الخاصة والاختلافات

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **صفحات متعددة** | تكرار عبر `document.Pages` وإعادة الخطوات 2‑5 لكل صفحة، باستخدام اسم فريد مثل `GS1`, `GS2`, … |
| **تعارض اسم ExtGState موجود** | تحقق من `extGStateDict.ContainsKey("GS0")` قبل الإضافة؛ إذا كان موجودًا، أنشئ مفتاحًا جديدًا (`"GS" + Guid.NewGuid().ToString("N")`) |
| **أوضاع دمج مختلفة** | استبدل `"Normal"` بـ `"Multiply"`، `"Screen"`، إلخ، عن طريق تغيير إدخال `BM` |
| **الشفافية المطلوبة فقط للخط** | احذف إدخال `ca` أو اضبطه على `1` وعدل `CA` بدلاً من ذلك |

## مثال كامل قابل للتنفيذ



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إضافة شفافية إلى PDF باستخدام Aspose.PDF – دليل كامل C#](/pdf/english/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/)
- [كيفية إضافة طوابع صفحات في PDFs باستخدام Aspose.PDF لـ .NET: دليل كامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [كيفية إضافة صور إلى PDFs باستخدام Aspose.PDF لـ .NET: دليل كامل](/pdf/english/net/images-graphics/add-images-to-pdfs-using-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}