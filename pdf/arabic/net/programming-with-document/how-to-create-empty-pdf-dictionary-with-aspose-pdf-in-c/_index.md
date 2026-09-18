---
category: general
date: 2026-09-18
description: تعلم كيفية إنشاء قاموس PDF فارغ في C# باستخدام Aspose.PDF. يغطي هذا الدليل
  خطوة بخطوة ExtGState، حالة الرسومات، وتلاعب CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: ar
lastmod: 2026-09-18
og_description: إنشاء قاموس PDF فارغ في C# باستخدام Aspose.PDF. اتبع هذا الدليل الشامل
  لتعديل ExtGState وقواميس حالة الرسومات.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: إنشاء قاموس PDF فارغ في C# – دليل Aspose.PDF الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: كيفية إنشاء قاموس PDF فارغ باستخدام Aspose.PDF في C#
url: /ar/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء قاموس PDF فارغ باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **إنشاء قاموس PDF فارغ** أثناء معالجة ملف PDF، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.PDF لـ .NET. سواءً كنت تعدل الشفافية، أو أوضاع المزج، أو أي حالة رسومية مخصصة، فإن الخطوات أدناه تتيح لك تعديل قاموس `ExtGState` بأمان وكفاءة.

في هذا البرنامج التعليمي ستتعلم:

* تحميل مستند PDF باستخدام Aspose.PDF.
* الوصول إلى موارد الصفحة الأولى والقاموس `ExtGState` الموجود.
* بناء `CosPdfDictionary` جديد فارغ وتعبئته بمدخلات حالة الرسوميات.
* حفظ ملف PDF المعدل دون فقدان أي محتوى أصلي.

الحل يعمل مع أي ملف PDF يحتوي على صفحة واحدة على الأقل ويتطلب فقط مكتبة Aspose.PDF (الإصدار 23.10 أو أحدث).

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.8).
* إشارة إلى حزمة **Aspose.PDF** عبر NuGet.
* ملف PDF إدخال موجود في `YOUR_DIRECTORY/input.pdf`.
* إلمام أساسي بـ C# ومفاهيم PDF مثل الموارد وحالة الرسوميات.

> **نصيحة احترافية:** عند العمل مع ملفات PDF كبيرة، قم بلف كائن `Document` داخل كتلة `using` لضمان تحرير جميع مقابض الملفات على الفور.

## الخطوة 1: تحميل مستند PDF

العملية الأولى تفتح الملف المصدر. Aspose.PDF يقرأ المستند بالكامل في الذاكرة، مما يتيح لك تعديل الكائنات الداخلية.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*لماذا هذا مهم*: تحميل المستند يخلق نموذج كائن قابل للتعديل. بدون هذه الخطوة لا يمكنك الوصول إلى موارد الصفحة المطلوبة لتعديل القاموس.

## الخطوة 2: استرجاع موارد الصفحة الأولى

كل صفحة تخزن قاموس `Resources` يحتوي على الخطوط، الصور، وحالات الرسوميات. الوصول إليه يمنحك `DictionaryEditor` الذي يبسط عمليات القراءة/الكتابة.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*لماذا هذا مهم*: قاموس `ExtGState` يقع داخل موارد الصفحة. تعديل القاموس الخطأ لن يؤثر على عملية العرض.

## الخطوة 3: تحديد قاموس ExtGState الموجود

قد يحتوي إدخال `ExtGState` بالفعل على كائنات حالة الرسوميات. نقوم بجلبه كـ `CosPdfDictionary` حتى نتمكن من إضافة مدخلات جديدة.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

إذا لم يكن إدخال `ExtGState` موجودًا، فإن Aspose.PDF ينشئ تلقائيًا قاموسًا فارغًا عندما تقوم بتعيين واحد جديد لاحقًا.

## الخطوة 4: **إنشاء قاموس PDF فارغ** لحالة رسومية جديدة

هنا نبني `CosPdfDictionary` جديد كليًا — جوهر عملية **إنشاء قاموس PDF فارغ**. ثم نقوم بتعبئته بمفاتيح حالة الرسوميات القياسية:

* `CA` – شفافية الخط.
* `ca` – شفافية التعبئة.
* `BM` – وضع المزج.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*لماذا هذا مهم*: بتعريف كل مدخل صراحةً، تتحكم في كيفية دمج الكائنات على الصفحة وعرضها. القاموس **فارغ** حتى تضيف هذه المفاتيح، مما يحقق شرط **إنشاء قاموس PDF فارغ** قبل تعبئته.

## الخطوة 5: إضافة الحالة الرسومية الجديدة إلى قاموس ExtGState

كل حالة رسومية يجب أن يكون لها اسم فريد (مثلًا `GS0`). نقوم بإدراج القاموس المُنشأ حديثًا تحت ذلك الاسم.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

إذا كنت بحاجة إلى حالات متعددة، استمر في إضافة مدخلات مثل `GS1`، `GS2`، إلخ، مع التأكد من أن كل اسم فريد داخل قاموس `ExtGState`.

## الخطوة 6: حفظ مستند PDF المحدث

أخيرًا، اكتب التغييرات إلى القرص. يبقى الملف الأصلي دون تعديل لأننا نحفظ إلى مسار جديد.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

ملف `output.pdf` الناتج الآن يحتوي على حالة رسومية إضافية (`GS0`) يمكنك الإشارة إليها من أي تدفق محتوى صفحة باستخدام المشغل `/GS0`.

## مثال كامل يعمل

جمع جميع الخطوات معًا ينتج برنامجًا مستقلًا يمكنك تشغيله فورًا.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**الناتج المتوقع**: بعد تشغيل البرنامج، يحتوي `output.pdf` على نفس المحتوى البصري الموجود في `input.pdf`. فحص الـ PDF بأداة مثل Adobe Acrobat أو PDF‑Tron سيظهر مدخلًا جديدًا `GS0` تحت قاموس `ExtGState` للصفحة الأولى.

## الاختلافات الشائعة وحالات الحافة

| الحالة | ما الذي يجب تعديله |
|-----------|----------------|
| **عدم وجود إدخال ExtGState موجود** | استبدل `resourcesEditor["ExtGState"]` بـ `new CosPdfDictionary(pdfDocument)` ثم عيّنها مرة أخرى إلى `firstPage.Resources["ExtGState"]`. |
| **عدة صفحات تحتاج نفس الحالة** | أضف نفس مدخل `GS0` إلى كل صفحة في قاموس `ExtGState`، أو ارجع إلى القاموس من كائن مورد مشترك. |
| **وضع مزج مختلف** | غير قيمة `CosPdfName` من `"Normal"` إلى `"Multiply"` أو `"Screen"` وغيرها، حسب التأثير المطلوب. |
| **قيم شفافية أعلى** | استخدم `new CosPdfNumber(0.8)` لـ `ca` أو `CA` لزيادة شفافية التعبئة أو الخط. |
| **استخدام مشغل تدفق** | في تدفق المحتوى، اكتب `"/GS0 gs"` قبل عمليات الرسم لتطبيق الحالة الرسومية الجديدة. |

## اعتبارات الأداء

* **استخدام الذاكرة** – تحميل PDF كبير جدًا يستهلك ذاكرة تتناسب مع عدد الصفحات. إذا كنت تحتاج فقط لتعديل الصفحة الأولى، فكر في استخدام `pdfDocument.Pages.Delete(pageNumber)` بعد المعالجة لتحرير الموارد.
* **سلامة الخيوط** – كائنات Aspose.PDF غير آمنة للاستخدام عبر خيوط متعددة. نفّذ تعديلات القاموس على خيط واحد أو أنشئ نسخًا منفصلة من `Document` لكل خيط.

## الخلاصة

أنت الآن تعرف كيفية **إنشاء قاموس PDF فارغ** باستخدام Aspose.PDF، تعبئته بمدخلات حالة الرسوميات، وربطه بقاموس `ExtGState` لصفحة. تتيح لك هذه التقنية التحكم الدقيق في الشفافية، وضع المزج، وغيرها من معلمات العرض مباشرةً من C#.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **معالجة PDF بـ C#**، إضافة مدخلات مخصصة إلى **قاموس ExtGState** لتأثيرات شفافية متقدمة، أو استخدام **CosPdfDictionary** لتعديل أنواع موارد أخرى مثل الخطوط أو XObjects. جرّب عدة حالات رسومية لبناء تأثيرات بصرية متقنة في ملفات PDF الخاصة بك.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء وتعبئة المستطيلات في ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [كيفية إنشاء خطوط متقطعة في ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [كيفية إضافة صفحة فارغة في نهاية ملف PDF باستخدام Aspose.PDF لـ .NET | دليل خطوة بخطوة](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}