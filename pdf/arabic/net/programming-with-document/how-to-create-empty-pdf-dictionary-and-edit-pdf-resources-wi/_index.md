---
category: general
date: 2026-10-26
description: تعلم كيفية إنشاء قاموس PDF فارغ وتعديل موارد PDF باستخدام Aspose.PDF
  للغة C#. دليل خطوة بخطوة مع مثال كامل للكود.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: ar
lastmod: 2026-10-26
og_description: إنشاء قاموس PDF فارغ وتعديل موارد PDF باستخدام Aspose.PDF للغة C#.
  اتبع هذا الدرس الكامل لتعديل حالات الرسومات في ملفات PDF.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: إنشاء قاموس PDF فارغ وتعديل موارد PDF في C# – دليل Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: كيفية إنشاء قاموس PDF فارغ وتعديل موارد PDF باستخدام Aspose.PDF في C#
url: /ar/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء قاموس PDF فارغ وتعديل موارد PDF باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **إنشاء قاموس PDF فارغ** ثم **تعديل موارد PDF** في تطبيق C#، فإن هذا الدليل يوضح لك الخطوات الدقيقة. سترى مثالًا كاملاً قابلاً للتنفيذ يضيف حالة رسومية مخصصة إلى الصفحة الأولى من ملف PDF موجود.

التعامل مع كائنات PDF منخفضة المستوى قد يبدو صعبًا، لكن Aspose.PDF يوفر واجهة برمجة تطبيقات واضحة لتعامل القواميس. بنهاية هذا الدرس ستفهم لماذا كل عملية مهمة وكيفية تعديل الشيفرة لأنواع موارد أخرى.

## المتطلبات المسبقة

* .NET 6.0 (أو أحدث) مثبت.
* نسخة مرخصة من **Aspose.PDF for .NET** – النسخة التجريبية المجانية تعمل للاختبار.
* بيئة تطوير متكاملة مثل Visual Studio 2022.
* ملف PDF باسم `input.pdf` موجود في مجلد يمكنك الإشارة إليه من الشيفرة.

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf`.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ مشروعًا جديدًا من نوع console وأضف حزمة Aspose.PDF:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

في `Program.cs` استورد المساحات الاسمية التي ستستخدمها:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

تتيح لك هذه الاستيرادات الوصول إلى الفئات `Document` و `DictionaryEditor` و COS (Canonical Object Structure) التي تسمح لك **بإنشاء قاموس PDF فارغ** وتعديل قواميس الموارد الموجودة.

## الخطوة 2: تحديد المجلد الذي يحتوي على ملفات PDF

حدد الدليل الذي يحتوي على `input.pdf`. استخدام مسار مطلق يجنب الغموض عندما يُشغَّل البرنامج من دليل عمل مختلف.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

استبدل `C:\PdfDemo\` بالمسار على جهازك. حفظ المسار في متغيّر يجعل من السهل إعادة استخدامه لكل من ملفات الإدخال والإخراج.

## الخطوة 3: فتح مستند PDF المصدر

حمِّل ملف PDF الذي تريد تعديله داخل كتلة `using` حتى يتم تحرير مقبض الملف تلقائيًا.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

فتح المستند يمنحك الوصول إلى مجموعة صفحاته، قواميس الموارد، وكائنات COS منخفضة المستوى.

## الخطوة 4: الوصول إلى الصفحة الأولى وقاموس مواردها

الصفحة الأولى مُرقَّمة بـ `1` (صفحات PDF تبدأ من 1). استخرج قاموس `Resources` للصفحة ولفه في `DictionaryEditor` لتمكين التحرير الآمن.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` يُجرد بنية COS الأساسية، مما يسمح لك بقراءة أو إنشاء إدخالات دون إفساد ملف PDF.

## الخطوة 5: **إنشاء قاموس PDF فارغ** لحالة رسومية جديدة

حالة الرسوميات تتحكم في الشفافية، وضع المزج، ومعلمات الرسم الأخرى. لإضافة حالة مخصصة تحتاج أولاً إلى قاموس فارغ، ثم تعبئته بالإدخالات المطلوبة.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

النداء إلى `CreateEmptyDictionary` هو جوهر **إنشاء قاموس PDF فارغ**. يُعيد قاموس COS ينتمي إلى نفس المستند، مما يضمن سلامة الإشارات المتبادلة.

### تعبئة إدخالات حالة الرسوميات

أضف المفاتيح القياسية:

* `CA` – ثابت ألفا للخط (النطاق 0 – 1).
* `ca` – ثابت ألفا غير الخط.
* `BM` – اسم وضع المزج.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

يُضاف كل إدخال إلى القاموس الفارغ الذي أنشأته للتو. بفصل التعريف عن حلقة الإدراج، يبقى الشيفرة قابلة للقراءة ويسهل توسيعها بمفاتيح إضافية لاحقًا.

### تسجيل الحالة الرسومية الجديدة في قاموس الموارد

امنح الحالة اسمًا (`GS0`) وأضفه إلى قاموس `ExtGState` الموجود داخل موارد الصفحة.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

الآن يحتوي قاموس موارد الصفحة على إشارة إلى الحالة الرسومية المخصصة، والتي يمكنك لاحقًا تطبيقها على تدفقات المحتوى.

## الخطوة 6: حفظ ملف PDF المحدث

أخيرًا، احفظ المستند المعدل إلى ملف جديد. الحفاظ على الأصل دون تعديل يساعدك على التحقق من التغييرات.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

عند فتح `output.pdf` في عارض يدعم فحص حالة الرسوميات (مثل Adobe Acrobat Pro)، سترى أن قاموس `ExtGState` يحتوي على إدخال باسم `GS0` مع القيم التي حددتها.

## الشيفرة المصدرية الكاملة

جمع جميع الأجزاء معًا ينتج برنامجًا مستقلًا:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
PDF updated successfully.
```

وينشئ `output.pdf` في نفس المجلد. فتح الملف يكشف عن إدخال جديد تحت **Resources → ExtGState → GS0** مع المعلمات التي حددتها.

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية تعديل الشيفرة |
|-----------|-----------------------|
| **صفحات متعددة** تحتاج إلى نفس حالة الرسوميات | إنشاء القاموس مرة واحدة، ثم إضافة إشارة `GS0` نفسها إلى قاموس `ExtGState` لكل صفحة. |
| **وضع مزج مختلف** (مثال، `Multiply`) | غيّر قيمة `CosPdfName("Normal")` إلى `CosPdfName("Multiply")`. |
| **عدم وجود قاموس ExtGState موجود** | قبل الوصول إلى `resourcesEditor["ExtGState"]`، تحقق من `resourcesEditor.ContainsKey("ExtGState")`. إذا كان مفقودًا، أنشئ قاموسًا فارغًا جديدًا وأضفه إلى `firstPage.Resources`. |
| **ملفات PDF الكبيرة** تسبب ضغطًا على الذاكرة | استخدم overload `PdfDocument.Load` الذي يبث الصفحات، أو عالج الصفحات واحدةً تلو الأخرى داخل كتلة `using`. |
| **الحاجة لتعديل موارد أخرى** (الخطوط، XObjects) | استبدل "ExtGState" بـ "Font" أو "XObject" في عملية البحث `resourcesEditor`، ثم اتبع نفس نمط إنشاء قاموس فارغ وتعبئته. |

تظهر هذه الاختلافات كيف أن نمط **إنشاء قاموس PDF فارغ** ينطبق على أي نوع من الموارد التي ترغب في **تعديل موارد PDF**.

## نصائح احترافية

* **تحقق من النتيجة** – بعد الحفظ، افتح ملف PDF بأداة يمكنها عرض قاموس الموارد الخام (مثل `PDFDebugger` من PDF‑Box) للتأكد من وجود الإدخال.
* **إعادة استخدام القواميس** – إذا أضفت نفس حالة الرسوميات إلى عدة صفحات، احفظ القاموس في متغيّر واستخدمه بدلاً من إنشائه في كل مرة.
* **توافق الإصدارات** – الشيفرة تعمل مع Aspose.PDF 23.12 وما بعده. الإصدارات الأقدم قد تتطلب `CosDictionary` بدلاً من `CosPdfDictionary`.

## الخلاصة

أنت الآن تعرف كيفية **إنشاء كائنات قاموس PDF فارغ** و**تعديل موارد PDF** باستخدام Aspose.PDF للغة C#. غطى الدرس فتح مستند، الوصول إلى قاموس موارد الصفحة، بناء حالة رسومية مخصصة، تسجيلها، وحفظ النتيجة. من هنا يمكنك تجربة أنواع موارد أخرى، دمج حالات رسومية متعددة، أو دمج التقنية في خط أنابيب معالجة PDF أكبر.

---

*هل أنت مستعد لاستكشاف المزيد؟ جرّب إضافة **ExtGState** مخصص إلى تدفق المحتوى، أو تعديل قاموس **Font** لتضمين خطوط جديدة. كلاهما يتبع نفس نمط إنشاء قاموس فارغ وتعديل موارد PDF.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة قابلة للتنفيذ مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تحرير قاموس موارد PDF باستخدام Aspose.PDF – دليل C#](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [إنشاء حالة رسومية مخصصة في PDF باستخدام Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [كيفية إنشاء حالة رسومية فارغة في PDF باستخدام C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}