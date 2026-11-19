---
category: general
date: 2026-11-19
description: تعلم كيفية ضبط الشفافية وكيفية تغيير وضع المزج في ملف PDF باستخدام Aspose.Pdf.
  دليل خطوة بخطوة بلغة C# للرسومات الشفافة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set opacity
- how to change blend
- Aspose.Pdf graphics state
- PDF transparency C#
- modify PDF resources
language: ar
lastmod: 2026-11-19
og_description: كيفية ضبط الشفافية وكيفية تغيير وضع المزج في ملف PDF باستخدام Aspose.Pdf.
  اتبع هذا الدرس الكامل بلغة C# لجعل الرسومات شفافة.
og_image_alt: Code editor showing C# example that sets PDF opacity and blend mode
og_title: كيفية ضبط الشفافية وتغيير وضع الدمج في ملف PDF باستخدام Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to set opacity and how to change blend mode in a PDF using
    Aspose.Pdf. Step‑by‑step C# guide for transparent graphics.
  headline: How to set opacity in a PDF and how to change blend mode with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: كيفية ضبط الشفافية في ملف PDF وكيفية تغيير وضع المزج باستخدام Aspose.Pdf
url: /ar/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ضبط الشفافية وكيفية تغيير وضع المزج في ملف PDF باستخدام Aspose.Pdf

إذا كنت تحتاج إلى **كيفية ضبط الشفافية** للكائنات داخل ملف PDF، فإن هذا الدليل يوضح الخطوات الدقيقة. كما يغطي **كيفية تغيير وضع المزج** بحيث يتم دمج حالة الرسومات الجديدة بشكل صحيح مع محتوى الصفحة.

في هذا البرنامج التعليمي ستقوم بـ:

* تحميل ملف PDF موجود باستخدام Aspose.Pdf.
* الوصول إلى قاموس موارد الصفحة.
* إنشاء قاموس حالة رسومات جديد يحدد شفافية الخط، شفافية التعبئة، ووضع المزج.
* إضافة حالة الرسومات إلى مجموعة `ExtGState`.
* حفظ ملف PDF المحدث.

لا توجد أدوات خارجية مطلوبة—فقط مكتبة Aspose.Pdf لـ .NET وبيئة تطوير .NET.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+).
* حزمة NuGet الخاصة بـ Aspose.Pdf لـ .NET (`Install-Package Aspose.Pdf`).
* ملف PDF باسم `input.pdf` موجود في مجلد قابل للكتابة (استبدل `YOUR_DIRECTORY` بالمسار الفعلي الخاص بك).

## الخطوة 1: تثبيت Aspose.Pdf وإعداد المشروع

إنشاء مشروع وحدة تحكم جديد وإضافة مرجع Aspose.Pdf:

```bash
dotnet new console -n PdfOpacityDemo
cd PdfOpacityDemo
dotnet add package Aspose.Pdf
```

ملف المشروع الآن يتضمن تجميع Aspose.Pdf، الذي يوفر الفئات `Document` و `DictionaryEditor` و `CosPdfDictionary` المستخدمة لاحقًا.

## الخطوة 2: تحميل مستند PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

// Load the existing PDF
Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

**لماذا هذا مهم:** تحميل المستند ينشئ تمثيلًا في الذاكرة يمكنك تعديلّه. بدون هذه الخطوة لا يمكن الوصول إلى قواميس الموارد.

## الخطوة 3: الحصول على الصفحة الأولى وقاموس مواردها

```csharp
// Retrieve the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Open the page’s resource dictionary for editing
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

**التفسير:** يحتوي قاموس `Resources` على كائنات مثل الخطوط، الصور، ومجموعة `ExtGState`. تعديل هذا القاموس يتيح لك حقن حالات رسومات جديدة تتحكم في الشفافية والدمج.

## الخطوة 4: الوصول إلى (أو إنشاء) قاموس ExtGState

```csharp
// Try to get the existing ExtGState dictionary; create it if missing
CosPdfDictionary extGStateDict = null;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and add it to resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor["ExtGState"] = extGStateDict;
}
```

**لماذا هذه الخطوة ضرورية:** يحتوي إدخال `ExtGState` على كائنات حالة الرسومات. إذا لم يكن موجودًا، يجب إنشاءه قبل إضافة إدخالات جديدة.

## الخطوة 5: إنشاء حالة رسومات جديدة مع الشفافية ووضع المزج

```csharp
// Create a new empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Set stroke opacity (CA) – 1 = fully opaque, 0 = fully transparent
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Set fill opacity (ca) – 0.5 = 50 % transparent fill
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Set blend mode (BM) – "Normal" is the default; other options: Multiply, Screen, Overlay, etc.
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**كيف يحل هذا المشكلة:**
* `CA` يتحكم في شفافية المسارات المرسومة (مثل الخطوط).
* `ca` يتحكم في شفافية الأشكال المملوءة (مثل المستطيلات).
* `BM` يحدد كيفية دمج الرسومات الجديدة مع محتوى الصفحة الحالي. تغيير وضع المزج هو بالضبط **كيفية تغيير المزج** لملف PDF.

## الخطوة 6: تسجيل حالة الرسومات في مجموعة ExtGState

```csharp
// Use a unique key for the new graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

الآن يمكن للصفحة الإشارة إلى حالة الرسومات هذه عبر الاسم `/GS0`. أي تدفق محتوى يحدد `/GS0 gs` سيستخدم الشفافية ووضع المزج المحددين.

## الخطوة 7: تطبيق حالة الرسومات على المحتوى الموجود (اختياري)

إذا كنت تريد تعديل أوامر الرسم الموجودة، يمكنك إضافة عامل حالة الرسومات في بداية تدفق محتوى الصفحة:

```csharp
// Retrieve the content stream as a string
string pageContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string modifiedContent = "GS0 gs\n" + pageContent;

// Replace the original content
firstPage.Contents[1].Replace(modifiedContent);
```

**ملاحظة:** هذه الخطوة اختيارية. إذا أضفت أوامر رسم جديدة لاحقًا، فقط ابدأ التدفق بـ `GS0 gs`.

## الخطوة 8: حفظ ملف PDF المعدل

```csharp
pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");
```

الملف الناتج `out.pdf` يحتوي على حالة رسومات حيث شفافية التعبئة 50 % ووضع المزج هو `Normal`. أي محتوى يستخدم `/GS0 gs` سيُظهر الشفافية المحددة. وضع المزج `Normal` يضمن دمج الرسومات دون تأثيرات خاصة. يمكنك تغيير `"Normal"` إلى `"Multiply"` أو `"Screen"` لرؤية **كيفية تغيير المزج** للحصول على نتائج بصرية مختلفة.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs` وتشغيله:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

class Program
{
    static void Main()
    {
        // 1. Load the PDF document
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get the first page and its resource dictionary
        Page firstPage = pdfDocument.Pages[1];
        DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

        // 3. Access or create the ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourceEditor["ExtGState"] = extGStateDict;
        }

        // 4. Define a new graphics state with opacity and blend mode
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity (fully opaque)
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity (50 % transparent)
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode (Normal)

        // 5. Add the graphics state to ExtGState collection
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Apply the graphics state to existing page content
        if (firstPage.Contents.Count > 0)
        {
            string original = firstPage.Contents[1].ToString();
            string withGs = "GS0 gs\n" + original;
            firstPage.Contents[1].Replace(withGs);
        }

        // 7. Save the updated PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");

        Console.WriteLine("PDF updated successfully – opacity set and blend mode changed.");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
PDF updated successfully – opacity set and blend mode changed.
```

عند فتح `out.pdf` في عارض PDF، أي شكل يستخدم حالة الرسومات المعرفة حديثًا سيظهر بشفافية تعبئة 50 % بينما تبقى الخطوط غير شفافة بالكامل. وضع المزج `Normal` يضمن دمج الرسومات دون تأثيرات خاصة. يمكنك تغيير `"Normal"` إلى `"Multiply"` أو `"Screen"` لرؤية **كيفية تغيير المزج** للحصول على نتائج بصرية مختلفة.

## الأسئلة الشائعة والحالات الخاصة

| السؤال | الإجابة |
|----------|--------|
| **هل يمكنني ضبط قيم شفافية مختلفة لعدة كائنات؟** | نعم. أنشئ حالات رسومات إضافية (مثل `GS1`، `GS2`) بقيم `ca`/`CA` مختلفة وارجع إلى الاسم المناسب قبل رسم كل كائن. |
| **ماذا لو كان ملف PDF يحتوي بالفعل على إدخال `ExtGState` باسم `GS0`؟** | اختر مفتاحًا فريدًا (`GS1`، `MyOpacityState`، إلخ) أو استبدل الإدخال الموجود إذا لم تعد التعريف القديم مطلوبًا. |
| **هل يقتصر وضع المزج على `Normal`؟** | لا. تشمل الأسماء الصالحة `Multiply`، `Screen`، `Overlay`، `Darken`، `Lighten`، `ColorDodge`، `ColorBurn`، `HardLight`، `SoftLight`، `Difference`، `Exclusion`، بالإضافة إلى `Hue`، `Saturation`، `Color`، `Luminosity`. |
| **هل يعمل هذا مع ملفات PDF المشفرة؟** | يمكن لـ Aspose.Pdf فتح ملفات PDF المشفرة إذا قمت بتوفير كلمة المرور عبر `Document(string, LoadOptions)`. تعديل حالة الرسومات يعمل بنفس الطريقة بعد فك التشفير. |
| **هل ستؤثر التغييرات على جميع الصفحات؟** | المثال يغيّر الصفحة الأولى فقط. لتطبيق التغييرات على جميع الصفحات، قم بالتكرار عبر `pdfDocument.Pages` وكرر الخطوات 2‑6 لكل صفحة. |

## نصائح احترافية

* **إعادة استخدام حالات الرسومات:** إضافة حالة رسومات مرة واحدة والإشارة إليها في صفحات متعددة يقلل من حجم الملف.
* **الأداء:** تعديل ملفات PDF الكبيرة في الذاكرة قد يستهلك الكثير من الذاكرة. استخدم `pdfDocument.Save(..., SaveOptions)` مع التحديث المتدرج إذا كنت تحتاج فقط إلى تغييرات صغيرة.
* **اختبار أوضاع المزج:** لا يعرض جميع عارضي PDF كل وضع مزج بنفس الطريقة. اختبر النتيجة في Adobe Acrobat Reader وعارض بديل (مثل Foxit) للتحقق من التناسق البصري.

## الخلاصة

أنت الآن تعرف **كيفية ضبط الشفافية** و**كيفية تغيير وضع المزج** في ملف PDF باستخدام Aspose.Pdf لـ .NET. من خلال تعديل قاموس `ExtGState` تحصل على تحكم دقيق في الشفافية والدمج، مما يتيح رسومات PDF بمستوى احترافي دون أدوات خارجية.

بعد ذلك، قد ترغب في استكشاف:

* إضافة صور بخلفيات شفافة (**كيفية ضبط الشفافية** على الصور).
* إنشاء تدفقات محتوى قابلة لإعادة الاستخدام تشير إلى حالة الرسومات الجديدة.
* استخدام أوضاع مزج أخرى (**كيفية تغيير المزج** إلى `Multiply` أو `Screen`) للحصول على تأثيرات إبداعية.

برمجة سعيدة، واستمتع بجعل ملفات PDF الخاصة بك أكثر ديناميكية بصريًا!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تغيير الشفافية في PDF باستخدام Aspose.PDF – دليل كامل](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/)
- [كيفية تغيير الشفافية في PDF باستخدام Aspose.Pdf لـ .NET](/pdf/english/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/)
- [كيفية تغيير شفافية PDF باستخدام Aspose.Pdf في C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}