---
category: general
date: 2026-08-14
description: إنشاء قاموس PDF فارغ في C# باستخدام Aspose.Pdf – تعلم كيفية إضافة حالة
  رسومية إلى مجموعة ExtGState وتعديل ملفات PDF برمجيًا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: ar
lastmod: 2026-08-14
og_description: إنشاء قاموس PDF فارغ في C# باستخدام Aspose.Pdf. اتبع هذا الدليل الكامل
  لإضافة حالة رسومية مخصصة إلى مجموعة ExtGState في PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: إنشاء قاموس PDF فارغ في C# – دليل Aspose.Pdf خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: إنشاء قاموس PDF فارغ في C# باستخدام Aspose.Pdf
url: /ar/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء قاموس PDF فارغ في C# باستخدام Aspose.Pdf

إذا كنت بحاجة إلى **إنشاء كائنات قاموس PDF فارغة** أثناء العمل مع ملفات PDF، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك في C# باستخدام مكتبة Aspose.Pdf. سواءً كنت تبني حالة رسومية مخصصة، أو تضيف موردًا جديدًا، أو تُعد قالبًا للاستخدام لاحقًا، فإن الخطوات أدناه تُقدم لك حلًا كاملاً قابلاً للتنفيذ.

ستتعلم كيفية تحميل ملف PDF، الوصول إلى قاموس موارد الصفحة الأولى، بناء `CosPdfDictionary` جديد كليًا، وإدراجه في مجموعة `ExtGState`. في نهاية البرنامج التعليمي ستحصل على ملف `output.pdf` يحتوي على القاموس الذي تم إنشاؤه حديثًا.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- Visual Studio 2022 أو أي بيئة تطوير C# تفضلها
- ترخيص Aspose.Pdf for .NET (أو مفتاح تقييم مؤقت)
- ملف PDF تجريبي يُدعى **input.pdf** موجود في مجلد يمكنك التحكم فيه (سيُستخدم مسار المجلد كـ `dataDir`)

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf`.

## الخطوة 1: إعداد المشروع وإضافة مرجع Aspose.Pdf

1. أنشئ مشروع **Console App** جديد في Visual Studio.  
2. افتح **NuGet Package Manager** وقم بتثبيت `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. أضف توجيهات `using` التالية في أعلى ملف `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *لماذا هذه المساحات الاسمية؟* يحتوي `Aspose.Pdf` على الفئة الأساسية `Document`، بينما توفر `Aspose.Pdf.Operators.Gfx` الفئات `CosPdfDictionary`، `CosPdfNumber`، وغيرها من كائنات PDF منخفضة المستوى اللازمة **لإنشاء قاموس PDF فارغ**.

## الخطوة 2: تحميل ملف PDF المصدر

العملية الأولى هي تحميل ملف PDF الموجود إلى كائن `Document`. هذا يمنحك إمكانية الوصول إلى جميع الصفحات والموارد والقواميس منخفضة المستوى.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*شرح*: يقوم `Document` بقراءة الملف إلى الذاكرة ويُعد البُنى الداخلية. يضمن بيان `using` تحرير مقبض الملف بعد الانتهاء من المعالجة.

## الخطوة 3: الوصول إلى قاموس موارد الصفحة الأولى

كل صفحة PDF لديها قاموس **Resources** يجمع الخطوط، الصور، كائنات ExtGState، وغيرها من الموارد المشتركة. لإدراج حالة رسومية جديدة نحتاج إلى تعديل هذا القاموس.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` هو فئة مساعدة تسمح لك بمعاملة قاموس PDF كـ `Dictionary<string, object>` في C#.

## الخطوة 4: استرجاع (أو إنشاء) مجموعة ExtGState

`ExtGState` يحتوي على كائنات حالة الرسومات مثل الشفافية، وضع المزج، وعرض الخط. إذا كان ملف PDF المصدر يحتوي بالفعل على مدخل `ExtGState`، فسنستخدمه؛ وإلا سننشئ قاموسًا فارغًا جديدًا.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*لماذا هذا الفحص؟* بعض ملفات PDF لا تتضمن مدخل `ExtGState` على الإطلاق. من خلال معالجة الحالتين يبقى البرنامج التعليمي قويًا لأي ملف إدخال.

## الخطوة 5: **إنشاء قاموس PDF فارغ** لحالة رسومية جديدة

الآن نقوم فعليًا **بإنشاء كائنات قاموس PDF فارغة** تُعرّف معلمات حالة الرسومات. يبدأ القاموس فارغًا، ثم نضيف المفاتيح المطلوبة:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### ما يقوم به كل مدخل

| المفتاح | النوع | المعنى |
|--------|-------|--------|
| **CA** | `CosPdfNumber` | شفافية الخط (النطاق 0‑1). |
| **ca** | `CosPdfNumber` | شفافية التعبئة (النطاق 0‑1). |
| **BM** | `CosPdfName`   | وضع المزج؛ `"Normal"` هو الأكثر شيوعًا. |

نظرًا لأننا بدأنا بـ **قاموس PDF فارغ**، لدينا سيطرة كاملة على أي مدخلات نضيفها. يمكنك توسيع هذا القاموس بإضافة معلمات حالة رسومية إضافية مثل `LW` (عرض الخط) أو `LC` (نهاية الخط) عند الحاجة.

## الخطوة 6: إدراج حالة الرسومات الجديدة في ExtGState

يعمل قاموس `ExtGState` كخريطة حيث يُحدَّد كل مدخل باسم (مثل `GS0`، `GS1`). نضيف القاموس الذي أنشأناه حديثًا تحت مفتاح فريد.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

إذا كنت تخطط لإضافة حالات متعددة، قم بزيادة اللاحقة (`GS1`, `GS2`, …) لتجنب تصادم الأسماء.

## الخطوة 7: حفظ ملف PDF المعدل

أخيرًا، اكتب التغييرات إلى القرص. تقوم طريقة `Save` تلقائيًا بتسلسل القواميس المحدثة.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

افتح `output.pdf` في أي عارض PDF وتفقد مدخل **Resources → ExtGState** (معظم العارضات تُخفي هذا، لكن أدوات مثل Adobe Acrobat Preflight أو PDF‑Tron يمكنها إظهاره). يجب أن ترى مدخل `GS0` يحتوي على قيم الشفافية ووضع المزج التي عرّفتها.

## مثال عملي كامل

بدمج جميع الأجزاء معًا، إليك البرنامج الكامل الذي يمكنك نسخه‑لصقه في `Program.cs` وتشغيله:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
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

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**الناتج المتوقع** – يطبع الطرفية سطر تأكيد، ويحتوي `output.pdf` على المدخل الجديد `GS0` ضمن `ExtGState`. عندما تقوم برندر صفحة تُشير إلى `GS0` (مثلاً عبر مشغل تدفق المحتوى `gs`)، ستكون الخطوط غير شفافة تمامًا بينما تكون التعبئات شفافة بنسبة 50 %.

## أسئلة شائعة وتعامل مع الحالات الخاصة

| السؤال | الجواب |
|--------|--------|
| *ماذا لو كان PDF يحتوي على صفحات متعددة؟* | المثال يستهدف الصفحة الأولى (`Pages[1]`). لتطبيق التغييرات على جميع الصفحات، قم بالتكرار عبر `pdfDocument.Pages` وكرر الخطوات 3‑5 لكل موارد صفحة. |
| *هل يمكنني إضافة القاموس إلى صفحة لديها بالفعل مدخل ExtGState باسم “GS0”?* | نعم، لكن عليك استخدام مفتاح مختلف (`GS1`, `GS2`, …) لتجنب الكتابة فوق المدخل الموجود. |
| *هل من الآمن تعديل القاموس بعد الحفظ؟* | بمجرد استدعاء `Save`، يصبح تمثيل الذاكرة منفصلًا عن الملف. يمكنك الاستمرار في تعديل كائن `Document` واستدعاء `Save` مرة أخرى إذا لزم الأمر. |
| *هل أحتاج إلى ترخيص لـ Aspose.Pdf لاستخدام ` |  |

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء خطوط متقطعة في ملفات PDF باستخدام Aspose.PDF for .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [كيفية إزالة الرسومات من ملفات PDF باستخدام Aspose.PDF .NET: دليل شامل](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [كيفية إنشاء ملفات PDF متعددة الطبقات باستخدام Aspose.PDF for .NET: دليل شامل](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}