---
category: general
date: 2026-10-07
description: إضافة حالة رسومية إلى ملف PDF باستخدام Aspose.Pdf في C# لتعديل شفافية
  PDF. اتبع هذا الدليل خطوة بخطوة لتضمين حالات رسومية مخصصة والتحكم في الشفافية.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: ar
lastmod: 2026-10-07
og_description: إضافة حالة رسومية إلى PDF باستخدام Aspose.Pdf في C#. تعلّم كيفية تعديل
  شفافية PDF بإنشاء قاموس حالة رسومية مخصص.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: إضافة حالة رسومات PDF باستخدام Aspose.Pdf – التحكم في شفافية PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: إضافة حالة الرسومات PDF باستخدام Aspose.Pdf في C#
url: /ar/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة حالة رسومات PDF باستخدام Aspose.Pdf في C#

إذا كنت بحاجة إلى **إضافة حالة رسومات PDF** إلى مستند، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك باستخدام Aspose.Pdf لـ .NET. بحلول نهاية الدليل، ستعرف أيضًا كيفية **تعديل شفافية PDF**، مما يتيح لك ضبط قيم التعتيم المخصصة لأي عملية رسم.

العمل مع حالات رسومات PDF يتيح لك التحكم في معلمات مثل عرض الخط، وضع المزج، والأهم لهذا المقال، شفافية المحتوى. الخطوات أدناه مكتوبة للمطورين الذين يجيدون C# ويرغبون في حل جاهز للتنفيذ دون الحاجة للغوص في وثائق SDK الرسمية.

## ما ستتعلمه

* كيفية إنشاء قاموس حالة رسومات جديد وتعبئته بالمدخلات `CA`، `ca`، و`BM`.  
* كيفية إدراج ذلك القاموس في مورد الصفحة `ExtGState` حتى يتعرف PDF عليه.  
* كيف تؤثر قيم `ca` (الحد) و`CA` (التعبئة) على **تعديل شفافية PDF** للأوامر الرسومية اللاحقة.  
* المشكلات الشائعة مثل تصادم الأسماء وتوافق الإصدارات، بالإضافة إلى نصائح احترافية لتوسيع حالة الرسومات لاحقًا.

**المتطلبات المسبقة**

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+).  
* ترخيص صالح لـ Aspose.Pdf for .NET (التقييم المجاني يعمل للاختبار).  
* Visual Studio 2022 أو أي بيئة تطوير متكاملة C# تفضلها.

---

## الخطوة 1: تثبيت Aspose.Pdf لـ .NET

أضف حزمة NuGet إلى مشروعك:

```bash
dotnet add package Aspose.Pdf
```

تحتوي الحزمة على مساحة الاسم `Aspose.Pdf` التي توفر الفئات `Document` و`DictionaryEditor` و`CosPdfDictionary` المستخدمة لاحقًا.

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة العديد من ملفات PDF دفعة واحدة، فعّل **الترخيص** مبكرًا في `Program.cs` لتجنب علامة التقييم.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## الخطوة 2: تحديد مسارات الإدخال والإخراج

يجب أن توجه SDK إلى ملف PDF موجود (`input.pdf`) وتحدد أين سيتم حفظ الملف المعدل (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **لماذا هذا مهم:** استخدام المسارات المطلقة يمنع SDK من البحث في دليل العمل الخاطئ، وهو مصدر شائع لاستثناء `FileNotFoundException`.

## الخطوة 3: فتح ملف PDF وتحديد موارد الصفحة الأولى

قاموس `ExtGState` موجود داخل قاموس موارد كل صفحة. سنقوم بتحرير الصفحة الأولى للبساطة، لكن النهج نفسه يعمل لأي فهرس صفحة.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**حالة حافة:** إذا لم تحتوي الصفحة على مدخل `ExtGState`، تحتاج إلى إنشائه:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## الخطوة 4: بناء قاموس حالة رسومات جديد

حالة الرسومات هي مجموعة من أزواج المفتاح/القيمة التي تصف سلوك عمليات الرسم. للشفافية نحتاج إلى ثلاثة مفاتيح:

| المفتاح | المعنى | القيمة النموذجية |
|-----|---------|---------------|
| `CA` | تعتيم التعبئة (0 = شفاف، 1 = معتم) | `1` (معتم بالكامل) |
| `ca` | تعتيم الحد (نفس المقياس) | `0.5` (50 % شفاف) |
| `BM` | وضع المزج (مثال: `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**لماذا هذه القيم؟**  
`ca = 0.5` يجعل أي مسار مرسوم (خطوط، حدود) يظهر بنسبة تعتيم 50 %، بينما `CA = 1` يترك الأشكال المملوءة معتمة بالكامل. اضبط كلا الرقمين لتحقيق تأثير **تعديل شفافية PDF** الدقيق الذي تحتاجه.

## الخطوة 5: إدراج حالة الرسومات في قاموس ExtGState

يجب أن تعطي الحالة الجديدة اسمًا فريدًا (مثال: `GS0`). إذا كان الاسم موجودًا بالفعل، سيقوم Aspose.Pdf بالكتابة فوق المدخل الموجود، مما قد يتسبب في كسر محتوى آخر يعتمد عليه.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

الآن تعرف موارد الصفحة عن `GS0`. لاستخدامه فعليًا، ستشير إلى حالة الرسومات في تدفق المحتوى عبر المشغل `gs` (مثال: `GS0 gs`). يتيح لك Aspose.Pdf حقن مشغلات PDF الخام إذا كنت بحاجة لرسم أشكال مخصصة.

## الخطوة 6: حفظ ملف PDF المعدل

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

يحتوي `output.pdf` الناتج على نفس المحتوى البصري كما في الأصل، لكن أي أوامر رسم لاحقة تختار `GS0` ستحترم إعدادات الشفافية التي حددتها.

### النتيجة المتوقعة

افتح `output.pdf` في Adobe Acrobat أو أي عارض PDF. إذا أضفت خطًا جديدًا مرسومًا باستخدام حالة الرسومات `GS0` (مثال: عبر `pdfDocument.Pages[1].Contents.Add(...)`)، سيظهر الخط شبه شفاف بينما تظل التعبئات معتمة. هذا يثبت أنك نجحت في **إضافة حالة رسومات PDF** و**تعديل شفافية PDF**.

---

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق وحدة تحكم. يتضمن تحميل الترخيص، معالجة الأخطاء، وتعليقات تشرح كل خطوة غير واضحة.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إضافة شفافية إلى PDF باستخدام Aspose PDF في C# – دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [إضافة شفافية إلى PDF باستخدام Aspose – دليل C# كامل](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [كيفية إضافة ختم صورة إلى PDF باستخدام Aspose.PDF لـ .NET: دليل شامل](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}