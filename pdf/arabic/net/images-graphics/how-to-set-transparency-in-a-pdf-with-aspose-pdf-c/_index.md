---
category: general
date: 2026-10-13
description: تعلم كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf للغة C#. كما يمكنك
  الاطلاع على كيفية حفظ ملف PDF المعدل وتغيير قيمة ألفا للملء.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: ar
lastmod: 2026-10-13
og_description: كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf للغة C#. اتبع هذا
  الدليل لتعديل موارد PDF، وتغيير قيمة ألفا للملء، وحفظ ملفات PDF المعدلة.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf C#
url: /ar/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf C#

إذا كنت بحاجة إلى ضبط الشفافية في ملف PDF باستخدام C#، فإن هذا الدليل يوضح الخطوات الدقيقة. ستتعلم أيضًا كيفية حفظ ملفات PDF المعدلة وتغيير قيمة ألفا للملء دون مغادرة بيئة Aspose.Pdf.

الدليل يمر بعملية تحميل المستند، تعديل موارد PDF، إنشاء حالة رسومية تحدد شفافية الملء، وحفظ التغييرات. لا تحتاج إلى أدوات خارجية؛ كل شيء يعمل داخل مشروع .NET قياسي.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* .NET 6.0 أو أحدث مثبت  
* ترخيص صالح لـ Aspose.Pdf for .NET (أو مفتاح تقييم مجاني)  
* ملف PDF إدخال موجود في مسار معروف  

يمكنك إضافة حزمة Aspose.Pdf عبر NuGet:

```bash
dotnet add package Aspose.Pdf
```

## كيفية ضبط الشفافية في ملف PDF

هذا القسم يحتوي على التنفيذ الأساسي. كل خطوة تشرح **لماذا** الكود ضروري، وليس فقط **ماذا** يفعل.

### الخطوة 1: تحميل مستند PDF

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*لماذا هذه الخطوة؟*  
`Document` يمثل ملف PDF بالكامل في الذاكرة. فتح الملف يمنحك الوصول إلى الصفحات والموارد والكائنات منخفضة المستوى التي ستقوم بتعديلها.

### الخطوة 2: تعديل موارد PDF لإضافة حالة رسومية

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*لماذا هذه الخطوة؟*  
صفحات PDF تخزن كائنات قابلة لإعادة الاستخدام—الخطوط، الصور، والحالات الرسومية—في قاموس الموارد. يحتوي الإدخال `ExtGState` على إعدادات الشفافية. من خلال تعديل هذا القاموس يمكنك إدخال حالة جديدة يمكن للصفحة الإشارة إليها.

### الخطوة 3: تغيير ألفا للملء وضبط شفافية الملء

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*لماذا هذه الخطوة؟*  
`ca` يتحكم في **شفافية الملء**، بينما `CA` يتحكم في **شفافية الحد**. ضبط `ca` إلى `0.5` يجعل الأشكال المملوءة شفافة بنسبة 50 %. الإدخال `BM` يحدد وضع المزج؛ `"Normal"` هو الخيار الأكثر شيوعًا للشفافية القياسية.

### الخطوة 4: إضافة الحالة الرسومية الجديدة إلى قاموس ExtGState

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*لماذا هذه الخطوة؟*  
تسمية الحالة الرسومية (`"GS0"`) تسمح لتدفقات المحتوى على الصفحة بالإشارة إليها باستخدام المشغل `gs`. بعد هذا التسجيل يمكن للصفحة تطبيق الشفافية التي عرّفتها للتو.

### الخطوة 5: (اختياري) تطبيق الحالة الرسومية في تدفق محتوى

إذا أردت رسم مستطيل باستخدام شفافية الملء الجديدة، أضف ما يلي بعد الخطوات السابقة:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*لماذا هذه الخطوة؟*  
المشغلان `q`/`Q` يحفظان ويستعيدان حالة الرسومات، مما يضمن أن الشفافية تؤثر فقط على أوامر الرسم المقصودة. المشغل `gs` يتحول إلى الحالة الرسومية المسماة `"GS0"`.

### الخطوة 6: حفظ ملف PDF المعدل

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*لماذا هذه الخطوة؟*  
الحفظ يكتب قاموس الموارد المحدث وأي تدفقات محتوى جديدة إلى القرص. الملف الناتج (`output.pdf`) يحتوي على المستطيل الشفاف الذي تم تعريفه في الخطوة السابقة.

## مثال كامل قابل للتنفيذ

بجمع كل الأجزاء معًا، إليك برنامج كامل يمكنك تجميعه وتشغيله:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**النتيجة المتوقعة** – `output.pdf` يظهر مستطيلًا مملوءًا بلون أرجواني فاتح شفاف بنسبة 50 %، مما يسمح برؤية محتوى الخلفية جزئيًا.

## أسئلة شائعة وحالات خاصة

* **هل يمكنني تغيير شفافية الحد بدلاً من شفافية الملء؟**  
  اضبط قيمة `CA` (الأحرف الكبيرة) إلى رقم بين `0` (شفاف تمامًا) و `1` (معتم تمامًا). المثال يضبط `CA` إلى `1`، مما يعني أن الحدود تبقى غير شفافة.

* **ماذا لو لم يكن للصفحة قاموس ExtGState بالفعل؟**  
  `resourceEditor["ExtGState"]` سيُنشئ قاموسًا فارغًا تلقائيًا. إضافة `"GS0"` تعمل بنفس الطريقة.

* **هل يمكن إعادة استخدام الحالة الرسومية عبر صفحات متعددة؟**  
  نعم. بمجرد إضافة الإدخال إلى قاموس موارد المستند، أي صفحة تشير إلى `"GS0"` ستحصل على نفس إعدادات الشفافية.

* **كيف يختلف هذا النهج عن استخدام واجهة `Graphics` عالية المستوى؟**  
  تعديل قاموس الموارد منخفض المستوى يمنحك تحكمًا دقيقًا في داخلية PDF وينتج ملفات أصغر لأنّه يتجنب تضمين كائنات إضافية.

## الخلاصة

أنت الآن تعرف **كيفية ضبط الشفافية في ملف PDF** باستخدام Aspose.Pdf للـ C#. غطى الدليل تعديل موارد PDF، تغيير ألفا للملء، ضبط شفافية الملء، وحفظ ملف PDF المعدل. مع هذه الأساسيات يمكنك تجربة أوضاع مزج مختلفة، تطبيق الشفافية على النص، أو إنشاء حالات رسومية قابلة لإعادة الاستخدام لمستندات معقدة.

### الخطوات التالية

* استكشف أوضاع المزج الأخرى (`Multiply`, `Screen`, إلخ) بتغيير الإدخال `BM`.  
* اضبط ألفا للحد (`CA`) لإنشاء حدود شبه شفافة.  
* اجمع عدة حالات رسومية لبناء مكتبة من التأثيرات البصرية القابلة لإعادة الاستخدام.  

لا تتردد في مشاركة نتائجك أو طرح أسئلة في التعليقات. برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}