---
category: general
date: 2026-09-28
description: تعلم كيفية إضافة حالة الرسومات PDF باستخدام Aspose.PDF في C#. يوضح لك
  هذا الدليل خطوة بخطوة كيفية ضبط الشفافية ووضع المزج لصفحات PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose PDF graphics state
- PDF opacity settings
- modify PDF resources
- Aspose.Pdf DictionaryEditor
language: ar
lastmod: 2026-09-28
og_description: أضف حالة رسومية PDF باستخدام Aspose.PDF في C#. اتبع هذا الدليل لتغيير
  شفافية الخط/الملء ووضع المزج في أي صفحة PDF.
og_image_alt: Screenshot of a PDF page after adding graphics state pdf with opacity
  settings
og_title: إضافة حالة الرسومات في PDF باستخدام Aspose.PDF – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to add graphics state pdf with Aspose.PDF in C#. This step‑by‑step
    guide shows you how to set opacity and blend mode for PDF pages.
  headline: How to add graphics state pdf using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: كيفية إضافة حالة الرسومات PDF باستخدام Aspose.PDF في C#
url: /ar/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة حالة رسومية PDF باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **add graphics state pdf** للتحكم في الشفافية أو وضع الدمج، يوضح لك هذا الدليل الطريقة بالضبط. باستخدام Aspose.PDF يمكنك تعديل قاموس موارد الصفحة وإدخال حالة رسومية مخصصة في بضع أسطر من الشيفرة فقط.

ستتعلم كيفية تحميل ملف PDF، إنشاء قاموس حالة رسومية جديد، ضبط شفافية الخط، شفافية التعبئة، ووضع الدمج، ثم حفظ المستند المعدل. لا تحتاج إلى أدوات خارجية—فقط مكتبة Aspose.PDF لـ .NET.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Core 3.1 و .NET Framework 4.7+)
* ترخيص صالح لـ **Aspose.PDF for .NET** (الإصدار التجريبي المجاني يكفي للتقييم)
* ملف PDF إدخال (`input.pdf`) موجود في مجلد معروف
* Visual Studio 2022 أو أي محرر C# تفضله

> **نصيحة احترافية:** احتفظ بملفات PDF خارج مجلد المشروع لتجنب ارتكاب خطأ إضافة ملفات ثنائية كبيرة إلى المستودع.

## الخطوة 1: تثبيت حزمة Aspose.PDF NuGet

افتح طرفية في دليل مشروعك وشغّل:

```bash
dotnet add package Aspose.Pdf
```

تحتوي الحزمة على مساحة الأسماء `Aspose.Pdf`، التي توفر الفئات `Document`، `DictionaryEditor`، و `CosPdfDictionary` المستخدمة لاحقًا.

## الخطوة 2: تحميل مستند PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the source PDF
string pdfPath = @"C:\MyPdfs\input.pdf";

// The `using` statement ensures the document is disposed automatically
using var pdfDocument = new Document(pdfPath);
```

*لماذا هذه الخطوة مهمة*: تحميل الـ PDF ينشئ تمثيلًا في الذاكرة يمكنك التلاعب به. كائن `Document` يمنحك الوصول إلى الصفحات، الموارد، وكائنات COS منخفضة المستوى اللازمة لـ **add graphics state pdf**.

## الخطوة 3: الوصول إلى موارد الصفحة الأولى

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// Create a DictionaryEditor to work with the page’s resource dictionary
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

قاموس `Resources` يحتوي على كائنات مثل الخطوط، الصور، وإدخالات **ExtGState**. تعديل هذا القاموس هو الطريقة الوحيدة لتعديل **PDF resources** بأمان.

## الخطوة 4: استرجاع (أو إنشاء) قاموس ExtGState

```csharp
// Try to get the existing ExtGState dictionary; if it does not exist, create one
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
```

*لماذا هذا مهم*: إدخال `ExtGState` يخزن كائنات الحالة الرسومية. إذا كان الـ PDF يحتوي بالفعل على واحد، نعيد استخدامه؛ وإلا ننشئ قاموسًا جديدًا حتى لا تفشل عملية **add graphics state pdf**.

## الخطوة 5: بناء قاموس حالة رسومية جديد

```csharp
// Create an empty dictionary that will hold our graphics state parameters
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1.0 means fully opaque strokes
graphicsStateDict.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes filled shapes 50 % transparent
graphicsStateDict.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default PDF blend mode
graphicsStateDict.Add("BM", new CosPdfName("Normal"));
```

المفاتيح `CA`، `ca`، و `BM` معرفة في مواصفة PDF. ضبطها يتيح لك التحكم في **PDF opacity settings** وسلوك الدمج لأي أوامر رسم تالية.

## الخطوة 6: تسجيل الحالة الرسومية الجديدة في ExtGState

```csharp
// Choose a unique name for the graphics state, e.g., GS0
extGStateDict.Add("GS0", graphicsStateDict);
```

الآن يحتوي قاموس موارد الصفحة على إدخال جديد اسمه `GS0`. عندما تشير لاحقًا إلى `GS0` في تدفقات المحتوى، سيطبق عارض الـ PDF الشفافية ووضع الدمج الذي حددته.

## الخطوة 7: (اختياري) تطبيق الحالة الرسومية على المحتوى الموجود

إذا أردت تعديل أوامر الرسم الحالية، يجب تعديل تدفق محتوى الصفحة. المثال التالي يضيف مسبقًا عامل `gs` لتعيين الحالة الرسومية قبل أي رسم:

```csharp
// Retrieve the page’s content stream as a string
string originalContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string updatedContent = "GS0 gs\n" + originalContent;

// Replace the page content with the updated stream
firstPage.Contents[1].Replace(updatedContent);
```

> **ملاحظة:** التلاعب المباشر بتدفقات المحتوى قد يكون حساسًا. اختبر دائمًا على نسخة من الـ PDF أولاً.

## الخطوة 8: حفظ الـ PDF المعدل

```csharp
string outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

بعد الحفظ، افتح `output.pdf` في عارض PDF. أي أشكال مملوءة ترسمها بعد عامل `GS0 gs` ستظهر بشفافية تعبئة 50 % بينما تبقى الخطوط غير شفافة بالكامل، مما يثبت نجاحك في **add graphics state pdf**.

### النتيجة المتوقعة

| قبل | بعد (مع GS0) |
|--------|------------------|
| ![Before PDF page](placeholder-before.png){.img-fluid alt="صفحة PDF الأصلية"} | ![After PDF page](placeholder-after.png){.img-fluid alt="صفحة PDF بعد إضافة حالة رسومية PDF مع إعدادات الشفافية"} |

عمود “بعد” يُظهر تعبئات شبه شفافة بينما تبقى الخطوط صلبة، تمامًا كما تم تعريفه في قاموس الحالة الرسومية.

## الأسئلة الشائعة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني إضافة حالات رسومية متعددة؟** | نعم. فقط أضف إدخالات إضافية (`GS1`، `GS2`، …) إلى `extGStateDict` واشر إلى الاسم المطلوب في تدفق المحتوى. |
| **ماذا لو كان الـ PDF يستخدم بالفعل اسمًا مثل `GS0`؟** | اختر معرفًا فريدًا (مثل `GS_custom1`). يمكنك فحص `extGStateDict.Keys` قبل الإضافة. |
| **هل يعمل هذا مع ملفات PDF مشفرة؟** | يجب فتح الـ PDF باستخدام كلمة المرور الصحيحة. استخدم `new Document(pdfPath, new LoadOptions { Password = "secret" })`. |
| **هل وضع الدمج مقيد بـ “Normal”؟** | لا. مواصفة PDF تدعم العديد من أوضاع الدمج (`Multiply`، `Screen`، `Overlay`، إلخ). استبدل `"Normal"` بأي اسم مدعوم. |
| **هل سيؤثر هذا على صفحات أخرى؟** | فقط على الصفحة التي عدلت مواردها. إذا كنت بحاجة إلى نفس الحالة على صفحات متعددة، كرّر الخطوات 3‑6 لكل صفحة أو عدّل موارد المستند العامة. |

## الخلاصة

أنت الآن تعرف كيف **add graphics state pdf** باستخدام Aspose.PDF لـ .NET، ضبط شفافية الخط والتعبئة، اختيار وضع الدمج، وتطبيق الحالة اختياريًا على المحتوى الموجود. هذه التقنية تمنحك تحكمًا دقيقًا في عرض الـ PDF دون الحاجة لتحويل الملف إلى صورة.

التالي، قد ترغب في استكشاف:

* **PDF opacity settings** للصور وكتل النص
* استخدام **Aspose.Pdf DictionaryEditor** لاستبدال الخطوط أو تضمين ملفات ICC مخصصة
* دمج حالات رسومية متعددة لإنشاء تأثيرات بصرية معقدة

لا تتردد في تجربة قيم شفافية مختلفة، أوضاع دمج، ونطاقات موارد مختلفة. إتقان هذه التلاعبات منخفضة المستوى في PDF يفتح لك باب إنشاء مستندات متقدمة وإخفاء معلومات بطريقة احترافية.

---


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Add Stamp to PDF with Aspose.Pdf – Step‑by‑Step Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/)
- [How to Add Images to PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}