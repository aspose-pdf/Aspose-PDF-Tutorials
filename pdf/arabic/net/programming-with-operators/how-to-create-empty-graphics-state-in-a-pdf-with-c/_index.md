---
category: general
date: 2026-08-17
description: إنشاء حالة رسومية فارغة في ملف PDF باستخدام C# و Aspose.Pdf. اتبع هذا
  الدليل خطوة بخطوة لتعديل موارد ExtGState بأمان.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: ar
lastmod: 2026-08-17
og_description: إنشاء حالة رسومية فارغة في ملف PDF باستخدام C#. يوضح هذا الدرس كيفية
  تعديل موارد ExtGState باستخدام Aspose.Pdf لتعديلات PDF موثوقة.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: إنشاء حالة رسومية فارغة في PDF باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: كيفية إنشاء حالة رسومية فارغة في ملف PDF باستخدام C#
url: /ar/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء حالة رسومية فارغة في ملف PDF باستخدام C#

إذا كنت بحاجة إلى **إنشاء حالة رسومية فارغة** في ملف PDF، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام C# و Aspose.Pdf. ستشاهد مثالًا كاملاً قابلاً للتنفيذ يضيف إدخالًا جديدًا إلى القاموس ExtGState للصفحة دون التأثير على المحتوى الموجود.

يُعد العمل مع حالات الرسومات في PDF مطلبًا شائعًا عندما تريد التحكم في الشفافية، أو أوضاع الدمج، أو غيرها من معلمات العرض على أساس كل كائن. يوضح الكود أدناه النهج الموصى به، ويشرح لماذا كل خطوة مهمة، ويغطي الاختلافات النموذجية التي قد تواجهها.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث (العينة تُجمع أيضًا مع .NET Core).
* ترخيص Aspose.Pdf for .NET (أو مفتاح تقييم مؤقت).
* مجلد يحتوي على ملف `input.pdf` الذي تريد تعديله.
* إلمام أساسي بصياغة C# ومفاهيم PDF مثل قواميس الموارد.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيقًا كونسول جديدًا أو دمج الكود في مشروع موجود. أضف حزمة NuGet الخاصة بـ Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

ثم استورد المساحات الاسمية المطلوبة:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

تمنحك هذه الاستيرادات الوصول إلى الفئات `Document` و `DictionaryEditor` وفئات PDF الأولية اللازمة **لإنشاء حالة رسومية فارغة**.

## الخطوة 2: تعريف المجلد الذي يحتوي ملفات PDF

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

استبدل المسار بموقع ملفات PDF الخاصة بك. يجعل تخزين الدليل في متغير الكود قابلًا لإعادة الاستخدام وأسهل للاختبار.

## الخطوة 3: تحميل مستند PDF المصدر

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

فتح المستند داخل عبارة `using` يضمن تحرير مقبض الملف تلقائيًا بعد حفظ التغييرات.

## الخطوة 4: الوصول إلى الصفحة الأولى وقاموس Resources الخاص بها

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` يسترجع الصفحة الأولى (أرقام صفحات PDF تبدأ من 1).
* `DictionaryEditor` يوفر طريقة مريحة لقراءة وتعديل قواميس PDF.
* إدخال `ExtGState` يحتوي على جميع كائنات حالة الرسومات للصفحة. إذا لم يكن المفتاح موجودًا، يقوم Aspose.Pdf بإنشاء قاموس فارغ تلقائيًا.

## الخطوة 5: بناء قاموس حالة رسومية فارغ جديد

يمكن أن تكون حالة الرسومات التي تضيفها فارغة أو مُعبأة مسبقًا بمعلمات مثل الشفافية (`CA`, `ca`) أو وضع الدمج (`BM`). في هذا الدرس ننشئ **حالة رسومية فارغة** ثم نضبط بعض القيم النموذجية لتوضيح كيفية عمل القاموس.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` ينشئ حاوية نظيفة يمكنك ملؤها بأي مفاتيح حالة رسومية.
* إضافة `CA` و `ca` و `BM` اختياري؛ يمكنك حذفها إذا كنت بحاجة فعلًا إلى حالة فارغة. يوضح الكود كيفية إضافة الإدخالات عندما تقرر لاحقًا التحكم في العرض.

## الخطوة 6: إدراج حالة الرسومات الجديدة في قاموس ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

تسمية الإدخال `"GS0"` تتبع الاتفاقية الشائعة لبدء أسماء حالات الرسومات بـ “GS”. يمكنك اختيار أي اسم PDF صالح لا يتعارض مع المفاتيح الموجودة.

## الخطوة 7: حفظ مستند PDF المعدل

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

نداء `Save` يكتب الملف المحدث إلى `output.pdf`. فتح هذا الملف في عارض PDF يؤكد وجود حالة الرسومات الجديدة؛ يمكنك الإشارة إليها لاحقًا باستخدام المشغل `gs` في تدفقات المحتوى.

### قائمة المصدر الكاملة

بجمع كل ما سبق، يبدو البرنامج الكامل كالتالي:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

تشغيل البرنامج يطبع سطر تأكيد وينتج `output.pdf` مع حالة الرسومات التي أضيفت حديثًا.

## لماذا يعمل هذا النهج بأفضل شكل

* **تحرير القاموس مباشرة** – استخدام `DictionaryEditor` يتجنب الحاجة إلى تحليل تدفق المحتوى بالكامل. أنت تعدل فقط الموارد التي تهمك.
* **أنواع PDF الأولية** – `CosPdfNumber` و `CosPdfName` و `CosPdfDictionary` تضمن أن PDF المُولد يتوافق مع مواصفة PDF 1.7.
* **الأمان** – كتلة `using` تُفرغ كائن `Document`، مما يمنع أقفال الملفات التي قد تُفسد عمليات البناء اللاحقة.
* **القابلية للتوسيع** – بمجرد وجود حالة الرسومات الفارغة، يمكنك الإشارة إليها من أي مشغل محتوى (`gs`) لتغيير الشفافية أو وضع الدمج أو معلمات أخرى لأوامر الرسم المختارة.

## الاختلافات الشائعة والحالات الحدية

| الحالة | التعديل الموصى به |
|-----------|-------------------|
| **صفحات متعددة** | كرر الحلقة على `pdfDocument.Pages` وكرر إدراج القاموس لكل صفحة تحتاج إلى تعديلها. |
| **عدم وجود إدخال ExtGState موجود** | `resourcesEditor["ExtGState"]` ينشئ قاموسًا فارغًا تلقائيًا إذا لم يكن موجودًا. لا يلزم أي كود إضافي. |
| **اسم حالة رسومية مختلف** | استبدل `"GS0"` باسم يتوافق مع نمط التسمية الخاص بك، مثل `"MyTransparentState"`. |
| **إضافة حالة فارغة فقط** | احذف مصفوفة `parameters` وحلقة `foreach`؛ سيبقى القاموس فارغًا. |
| **العمل مع ملفات PDF مشفرة** | قدم كلمة المرور عند إنشاء `new Document(path, password)` قبل تعديل الموارد. |

## التحقق من النتيجة

يمكنك التحقق من إضافة حالة الرسومات بفحص PDF باستخدام عارض منخفض المستوى مثل **PDF‑Tron** أو **iText Sharp**. ابحث عن إدخال مشابه لـ:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

إذا ظهر الإدخال، فإن عملية **إنشاء حالة رسومية فارغة** نجحت.

## الخلاصة

أنت الآن تعرف كيف **تنشئ حالة رسومية فارغة** في ملف PDF باستخدام C# و Aspose.Pdf. غطى الدرس كل خطوة — من تحميل المستند إلى تعديل قاموس `ExtGState` وحفظ النتيجة — مع شرح السبب وراء كل إجراء.

من هنا يمكنك:

* استخدام حالة الرسومات الجديدة في تدفقات المحتوى (`gs /GS0`).
* تجربة مفاتيح إضافية مثل `/SM` (تعديل الخط) أو `/OPM` (وضع الطباعة فوق).
* تطبيق نفس التقنية على أنواع موارد أخرى مثل `/XObject` أو `/ColorSpace`.

نتمنى لك تجربة ممتعة مع PDF، ولا تتردد في استكشاف سيناريوهات **حالة رسومات Aspose PDF** أخرى مثل تغييرات الشفافية الديناميكية أو أوضاع الدمج المخصصة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}