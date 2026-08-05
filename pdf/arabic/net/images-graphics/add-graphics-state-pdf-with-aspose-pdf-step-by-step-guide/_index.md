---
category: general
date: 2026-08-04
description: إضافة حالة رسومية إلى ملف PDF باستخدام Aspose.Pdf للتحكم في الشفافية
  ووضع الدمج. اتبع هذا الدليل الكامل لتعديل موارد PDF بأمان.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose.Pdf
- PDF opacity
- PDF blend mode
- ExtGState dictionary
language: ar
lastmod: 2026-08-04
og_description: إضافة حالة رسومية إلى ملف PDF باستخدام Aspose.Pdf لتعيين الشفافية
  ووضع الدمج. يوضح هذا الدليل الكود الكامل، ويشرح كل خطوة، ويغطي الأخطاء الشائعة.
og_image_alt: Screenshot of a PDF page showing modified graphics state after using
  add graphics state pdf
og_title: إضافة حالة الرسومات في PDF باستخدام Aspose.Pdf – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  headline: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  name: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Locate (or create) the `ExtGState` dictionary.
    text: Locate (or create) the `ExtGState` dictionary.
  - name: Build a new graphics‑state dictionary with the desired entries.
    text: Build a new graphics‑state dictionary with the desired entries.
  - name: Reference the new state from drawing commands (outside the scope of this
      tutorial).
    text: Reference the new state from drawing commands (outside the scope of this
      tutorial).
  type: HowTo
tags:
- PDF
- Aspose
- C#
- Graphics state
title: إضافة حالة الرسومات في PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة حالة رسومية PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة

إذا كنت بحاجة إلى **إضافة حالة رسومية PDF** للتحكم في الشفافية أو وضع الدمج، فإن هذا الدرس يوضح لك حلاً كاملاً وجاهزًا للإنتاج. ستتعلم كيفية تعديل قاموس ExtGState لصفحة PDF باستخدام Aspose.Pdf، وسترى الشيفرة الدقيقة التي يمكنك نسخها إلى مشروعك.

يغطي الدليل كل شيء من إعداد المشروع إلى التعامل مع الحالات الحدية مثل عدم وجود مدخلات ExtGState. في النهاية ستحصل على PDF تُظهر صفحته الأولى الحالة الرسومية التي عرّفتها.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* SDK .NET 6.0 أو أحدث مثبت.
* إصدار حديث من حزمة **Aspose.Pdf** على NuGet (مثلاً 23.12 أو أحدث).
* ملف PDF إدخال موجود في مجلد يمكنك الإشارة إليه من الشيفرة.
* بيئة تطوير مثل Visual Studio 2022 أو VS Code.

## نظرة عامة على سير عمل الحالة الرسومية

تتحكم حالة الرسومات في PDF في كيفية عرض عمليات الرسم. خاصيتان هما الأكثر شيوعًا للتأثيرات البصرية:

* **الشفافية** – مدخلات `ca` (ملء) و `CA` (حد).
* **وضع الدمج** – مدخل `BM`.

تعيش هذه القيم في **قاموس ExtGState** المرفق بقاموس موارد الصفحة. إضافة حالة رسومية جديدة تتكون من ثلاث خطوات:

1. تحديد (أو إنشاء) قاموس `ExtGState`.
2. بناء قاموس حالة رسومية جديد بالمدخلات المطلوبة.
3. الإشارة إلى الحالة الجديدة من أوامر الرسم (خارج نطاق هذا الدرس).

## الخطوة 1: إنشاء مشروع وحدة تحكم .NET جديد

```bash
dotnet new console -n PdfGraphicsStateDemo
cd PdfGraphicsStateDemo
dotnet add package Aspose.Pdf
```

أمر `dotnet add package` يجلب مكتبة **Aspose.Pdf**، التي توفر الـ API المستخدمة طوال الدليل.

## الخطوة 2: تحميل PDF والوصول إلى الصفحة الأولى

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

// Load the source PDF
using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

// PDF pages are 1‑based; page 1 is the first page
Page firstPage = pdfDoc.Pages[1];
```

*لماذا هذا مهم*: نموذج كائن PDF يستخدم فهرسة تبدأ من 1، لذا طلب `Pages[0]` سيتسبب في استثناء. تحميل المستند داخل كتلة `using` يضمن تحرير مقبض الملف تلقائيًا.

## الخطوة 3: التأكد من وجود قاموس ExtGState

```csharp
// The page’s Resources dictionary holds many sub‑dictionaries (Font, XObject, etc.)
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

// Try to get the existing ExtGState dictionary; create one if it is missing
CosCosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and attach it to the page resources
    extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**نصيحة محترف**: تحقق دائمًا من وجود `ExtGState`. بعض ملفات PDF تُنشأ بدون هذا القاموس، ومحاولة تعديل مدخل غير موجود ستؤدي إلى رفع استثناء `KeyNotFoundException`.

## الخطوة 4: بناء الحالة الرسومية الجديدة

```csharp
// Create a fresh dictionary for the new graphics state
CosCosPdfDictionary newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Stroke opacity (CA) – 1.0 means fully opaque
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes the fill 50 % transparent
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing operation
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

*لماذا هذه المدخلات*:
- `CA` يؤثر على الخطوط والحدود (الحد).
- `ca` يؤثر على الأشكال المملوءة والنص.
- `BM` يحدد كيفية دمج لون المصدر مع الوجهة؛ `"Normal"` يحافظ على المظهر الأصلي مع احترام الشفافية.

## الخطوة 5: إدراج الحالة الرسومية في قاموس ExtGState

```csharp
// Choose a unique name for the graphics state; "GS0" is common for the first entry
extGStateDict.Add("GS0", newGraphicsState);
```

إذا كنت تحتاج إلى حالات متعددة، زد اللاحقة (`GS1`, `GS2`, …) وأشر إلى الاسم الصحيح لاحقًا في تدفقات المحتوى الخاصة بك.

## الخطوة 6: حفظ PDF المعدل

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
Console.WriteLine("PDF saved with new graphics state.");
```

الملف الناتج (`output.pdf`) يحتوي على نفس المحتوى البصري للمصدر، لكن أي أوامر رسم تُشير لاحقًا إلى `/GS0` ستُعرض ب**شفافية PDF** 0.5 و**وضع دمج PDF** `Normal`.

## مثال كامل قابل للتنفيذ

انسخ البرنامج التالي إلى `Program.cs` في المشروع الذي أنشأته في الخطوة 1. عدّل عناصر `YOUR_DIRECTORY` لتتناسب مع بيئتك.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

namespace PdfGraphicsStateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the PDF document
            using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Access the first page's resources
            Page firstPage = pdfDoc.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // 3️⃣ Retrieve or create ExtGState dictionary
            CosCosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
            {
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            }
            else
            {
                extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // 4️⃣ Define a new graphics state (opacity & blend mode)
            var newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            newGraphicsState.Add("CA", new CosPdfNumber(1));           // stroke opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));         // fill opacity
            newGraphicsState.Add("BM", new CosPdfName("Normal"));     // blend mode

            // 5️⃣ Add the graphics state to the ExtGState dictionary
            extGStateDict.Add("GS0", newGraphicsState);

            // 6️⃣ Save the modified PDF
            pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("PDF saved with new graphics state.");
        }
    }
}
```

### النتيجة المتوقعة

افتح `output.pdf` في أي عارض. إذا أضفت لاحقًا أوامر رسم تُشير إلى `/GS0` (على سبيل المثال عبر تدفق محتوى أو استدعاء API آخر من Aspose.Pdf)، سيظهر الملء بنسبة شفافية 50 % بينما تظل الحدود غير شفافة تمامًا. يبقى وضع الدمج `"Normal"`، وهو مناسب لمعظم سيناريوهات التركيب.

## التعامل مع الاختلافات الشائعة

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|--------|
| **عدة صفحات تحتاج إلى نفس الحالة** | كرّر الحلقة على `pdfDoc.Pages` وكرر الخطوات 3‑5 لكل صفحة، أو أنشئ قاموس ExtGState واحد في موارد المستند العامة وأشر إليه من كل صفحة. | يتجنب القواميس المكررة ويحافظ على صغر حجم الملف. |
| **قيم شفافية مختلفة لكل صفحة** | استخدم أسماء مميزة (`GS0`, `GS1`, …) واضبط `ca`/`CA` وفقًا لذلك قبل الإضافة إلى ExtGState لكل صفحة. | يمنح تحكمًا دقيقًا في العرض. |
| **ExtGState يحتوي بالفعل على مفتاح باسم “GS0”** | اختر اسم مفتاح مختلف (`GS1`, `MyState`, …) وقم بتحديث أي تدفقات محتوى تُشير إليه. | يمنع الكتابة فوق حالات الرسومات الموجودة عن طريق الخطأ. |
| **PDF تم إنشاؤه بدون قاموس ExtGState** | الشيفرة في الخطوة 3 تنشئ واحدًا بالفعل، لذا لا يلزم أي عمل إضافي. | يضمن نجاح العملية لأي ملف PDF مدخل. |

## نصائح وممارسات أفضل

* **تحقق من صحة PDF بعد التعديل** – استخدم `pdfDoc.Validate()` (متاح في إصدارات Aspose.Pdf الأحدث) لاكتشاف المشكلات الهيكلية مبكرًا.
* **احفظ قاموس الحالة الرسومية صغيرًا** – أدرج فقط المدخلات التي تحتاجها؛ المفاتيح الزائدة تزيد حجم الملف دون فائدة.
* **عند إضافة تدفقات محتوى تستخدم الحالة الجديدة**، أضف `/GS0 gs` قبل عوامل الرسم. مثال: `contentStream.Append("/GS0 gs 100 100 m 200 200 l S");`
* **تخلص من ملفات PDF الكبيرة بسرعة** – جملة `using` في المثال تضمن تحرير مقبض الملف، وهو أمر أساسي في سيناريوهات الخدمات الويب.

## الخلاصة

أنت الآن تعرف كيف **تضيف حالة رسومية PDF** باستخدام Aspose.Pdf، وتتحكم في **شفافية PDF**، وتحدد **وضع دمج PDF**، وتعمل بأمان مع **قاموس ExtGState**. عينة الشيفرة الكاملة جاهزة للإدراج في أي مشروع .NET، وتساعدك النصائح المرفقة على تجنّب المشكلات الشائعة.

بعد ذلك، استكشف كيفية تطبيق الحالة الرسومية التي أنشأتها حديثًا على النصوص أو الصور أو الأشكال المتجهية. يمكنك أيضًا فحص مدخلات ExtGState أخرى مثل `SM` (تعديل الحد) أو قيم `CA` أكبر من 1 للحصول على تأثيرات متخصصة. استمتع بتعديل PDF!

## ما الذي يجب أن تتعلمه لاحقًا؟

تغطي الدروس التالية مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية إضافة طوابع الصفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل كامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [إضافة طوابع الصور إلى ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)
- [كيفية إزالة الرسومات من ملفات PDF باستخدام Aspose.PDF .NET: دليل كامل](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}