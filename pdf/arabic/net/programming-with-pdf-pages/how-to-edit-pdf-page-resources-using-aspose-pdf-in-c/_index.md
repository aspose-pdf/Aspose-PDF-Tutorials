---
category: general
date: 2026-10-20
description: تحرير موارد صفحات PDF في C# باستخدام Aspose.PDF – دليل خطوة بخطوة لتعديل
  حالة الرسومات وقاموس الموارد.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- edit pdf page resources
- Aspose.Pdf edit resources
- C# modify PDF
- PDF graphics state
- PDF page resource dictionary
language: ar
lastmod: 2026-10-20
og_description: تحرير موارد صفحات PDF في C# باستخدام Aspose.PDF. تعلّم كيفية إضافة
  حالة رسومية مخصصة إلى قاموس موارد الصفحة في بضع خطوات واضحة.
og_image_alt: Diagram showing PDF page resources structure after editing
og_title: تحرير موارد صفحات PDF في C# – دليل Aspose.PDF الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Edit PDF page resources in C# with Aspose.PDF – step‑by‑step guide
    to modify graphics state and the resource dictionary.
  headline: How to edit PDF page resources using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Graphics state
title: كيفية تحرير موارد صفحات PDF باستخدام Aspose.PDF في C#
url: /ar/net/programming-with-pdf-pages/how-to-edit-pdf-page-resources-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعديل موارد صفحة PDF باستخدام Aspose.PDF في C#

إذا كنت بحاجة إلى **تعديل موارد صفحة PDF** في C#، فإن هذا الدرس يوضح لك كيفية القيام بذلك باستخدام Aspose.PDF. ستتعلم طريقة موثوقة لتعديل قاموس الموارد للصفحة الأولى، إضافة حالة رسومية مخصصة، وحفظ الملف المحدث.

سنتناول كل ما تحتاج معرفته: حزمة NuGet المطلوبة، بنية قاموس موارد صفحة PDF، الشيفرة الدقيقة لإدراج حالة رسومية جديدة، ونصائح للتعامل مع الحالات الخاصة. في نهاية هذا الدليل، ستكون قادرًا على **تعديل ملفات PDF** برمجيًا باستخدام C# وفهم كيفية عمل حالة الرسومات في PDF تحت الغطاء.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 SDK أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير تدعم .NET)  
* رخصة Aspose.PDF for .NET (الإصدار التجريبي المجاني يكفي للتجربة)  

كما تحتاج إلى ملف PDF (`input.pdf`) تريد تعديله. ضع الملف في مجلد يمكنك الإشارة إليه من مشروعك.

## ما هو قاموس موارد صفحة PDF؟

تحتوي صفحة PDF على **قاموس موارد** يجمع كل الكائنات التي يمكن للصفحة استخدامها—الخطوط، الصور، XObjects، وحالات الرسومات. المدخل `ExtGState` يحتوي على *حالات رسومية موسعة*، التي تتحكم في معلمات مثل عرض الخط، الشفافية، ونمط الدمج.

عند تعديل موارد صفحة PDF، فإنك تتعامل مباشرة مع هذا القاموس. إضافة حالة رسومية جديدة تتيح لك إعادة استخدام نفس معلمات العرض عبر عدة تدفقات محتوى دون الحاجة لتكرار الإعدادات.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ مشروع console جديد (أو دمج الشيفرة في مشروع موجود) وأضف حزمة Aspose.PDF عبر NuGet:

```bash
dotnet new console -n PdfResourceEditor
cd PdfResourceEditor
dotnet add package Aspose.PDF
```

الآن استورد المساحات الاسمية المطلوبة:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.XObjects;
```

> **نصيحة احترافية:** إذا كنت تخطط لتعديل صفحات متعددة، احwrap كائن `Document` داخل كتلة `using` لضمان تحرير جميع مقابض الملفات بسرعة.

## الخطوة 2: تحميل PDF وتحديد موارد الصفحة الأولى

الخطوة العملية الأولى هي تحميل ملف PDF المصدر واسترجاع قاموس الموارد للصفحة الأولى.

```csharp
// Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Grab the first page (PDF pages are 1‑based)
    Page firstPage = pdfDocument.Pages[1];

    // Ensure the page has a Resources dictionary; Aspose creates it if missing
    DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

إذا لم تحتوي الصفحة بالفعل على مدخل `ExtGState`، سنقوم بإنشائه لاحقًا (انظر الخطوة 4).

## الخطوة 3: بناء قاموس حالة رسومية مخصصة

تمثل حالة الرسومات بـ `CosPdfDictionary`. سننشئ واحدًا يحتوي على ثلاثة معلمات:

* **CA** – شفافية الخط (`1` = غير شفاف تمامًا)  
* **ca** – شفافية التعبئة (`0.5` = 50 % شفافة)  
* **BM** – نمط الدمج (`Normal`)

```csharp
    // Access (or create) the ExtGState dictionary
    CosPdfDictionary extGState;
    if (resourcesEditor.ContainsKey("ExtGState"))
    {
        extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
    }
    else
    {
        // Create an empty ExtGState dictionary if it does not exist
        extGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        resourcesEditor.Add("ExtGState", extGState);
    }

    // Create a new empty graphics state dictionary
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters we want to set
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Add each parameter to the new graphics state
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

### لماذا هذه المفاتيح مهمة

* `CA` و `ca` يتحكمان في شفافية **الخط** و **التعبئة** على التوالي. هما جزء من مواصفات *حالة الرسومات الموسعة* (PDF 1.4+).  
* `BM` يحدد **نمط الدمج** المستخدم عند رسم كائنات متداخلة. “Normal” هو نمط الدمج الافتراضي، لكن يمكنك استخدام “Multiply”، “Screen”، إلخ، للحصول على تأثيرات فنية.

## الخطوة 4: إدراج الحالة الرسومية الجديدة في موارد الصفحة

الآن نضيف الحالة الرسومية التي أنشأناها حديثًا تحت اسم مخصص (`GS0`). يمكن أن يكون الاسم أي اسم PDF صالح؛ اخترنا `GS0` للبساطة.

```csharp
    // Register the new graphics state with a custom name
    extGState.Add("GS0", newGraphicsState);
```

في هذه المرحلة يحتوي قاموس موارد الصفحة على:

```text
Resources
 └─ ExtGState
     └─ GS0  →  << /CA 1 /ca 0.5 /BM /Normal >>
```

يمكنك الإشارة إلى `GS0` لاحقًا في تدفق المحتوى باستخدام المشغل `gs`.

## الخطوة 5: حفظ PDF المعدل

أخيرًا، اكتب المستند المحدث إلى القرص.

```csharp
    // Save the edited PDF
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

### النتيجة المتوقعة

فتح `output.pdf` في أي عارض PDF سيظهر المحتوى الأصلي دون تغيير (حالة الرسومات لا تؤثر على المظهر حتى تُستخدم). ومع ذلك، يحتوي الملف الآن على مدخل جديد `GS0` في قاموس `ExtGState` للصفحة الأولى، ويمكنك التحقق منه باستخدام أداة فحص PDF (مثل “Preflight” في Adobe Acrobat أو `pdfinfo`).

## التعامل مع الحالات الشائعة

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **الصفحة لا تحتوي على قاموس `Resources`** | يقوم Aspose بإنشائه تلقائيًا عند الوصول إلى `firstPage.Resources`. لا تحتاج إلى أي شفرة إضافية. |
| **`ExtGState` يحتوي بالفعل على مفتاح باسم `GS0`** | اختر اسمًا مختلفًا (`GS1`، `MyState`، إلخ) أو استبدله عمدًا باستخدام `extGState["GS0"] = newGraphicsState;`. |
| **تحتاج إلى تعديل صفحة لاحقة** | غيّر `pdfDocument.Pages[1]` إلى فهرس الصفحة المطلوب (`pdfDocument.Pages[5]` للصفحة 5). |
| **ترغب في تطبيق حالة الرسومات فورًا** | أدرج استدعاء `PdfContentEditor` بعد تحديث القاموس: <br>`new PdfContentEditor(pdfDocument).AddGraphicsState(firstPage, "GS0");` (يتطلب استدعاءات إضافية من Aspose). |
| **تشغيل على .NET Framework بدلاً من .NET 6** | الشيفرة نفسها تعمل؛ فقط تأكد من أن نسخة Aspose.PDF التي تستخدمها تستهدف الإطار الخاص بك. |

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs`. عدّل مسارات الملفات حسب الحاجة.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.XObjects;

namespace PdfResourceEditor
{
    class Program
    {
        static void Main()
        {
            // Path to the source PDF
            const string inputPath = "YOUR_DIRECTORY/input.pdf";
            // Path where the edited PDF will be saved
            const string outputPath = "YOUR_DIRECTORY/output.pdf";

            // Load the PDF document
            using (var pdfDocument = new Document(inputPath))
            {
                // Get the first page (pages are 1‑based)
                Page firstPage = pdfDocument.Pages[1];

                // Access the page's Resources dictionary
                DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

                // Retrieve or create ExtGState dictionary
                CosPdfDictionary extGState;
                if (resourcesEditor.ContainsKey("ExtGState"))
                {
                    extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
                }
                else
                {
                    extGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                    resourcesEditor.Add("ExtGState", extGState);
                }

                // Build a new graphics state
                CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                var parameters = new[]
                {
                    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
                };
                foreach (var p in parameters)
                    newGraphicsState.Add(p);

                // Add the new graphics state under a custom name
                const string gsName = "GS0";
                extGState.Add(gsName, newGraphicsState);

                // Save the modified PDF
                pdfDocument.Save(outputPath);
            }

            Console.WriteLine($"PDF page resources edited successfully. Output saved to {outputPath}");
        }
    }
}
```

شغّل البرنامج:

```bash


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Edit PDF Resource Dictionary with Aspose.PDF – C# Guide](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Add graphics state pdf with Aspose.Pdf – step‑by‑step guide](/pdf/english/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-step-by-step-guide/)
- [Save Updated PDF – Edit PDF Resources with Aspose.Pdf](/pdf/english/net/document-manipulation/save-updated-pdf-edit-pdf-resources-with-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}