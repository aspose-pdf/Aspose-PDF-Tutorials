---
category: general
date: 2026-02-23
description: كيفية حفظ ملفات PDF مع إضافة ترقيم باتس والعناصر باستخدام Aspose.Pdf
  في C#. دليل خطوة بخطوة للمطورين.
draft: false
keywords:
- how to save pdf
- how to add bates
- how to add artifact
- create pdf document
- add bates numbering
language: ar
og_description: كيفية حفظ ملفات PDF مع إضافة ترقيم بيتس والعناصر باستخدام Aspose.Pdf
  في C#. تعلم الحل الكامل في دقائق.
og_title: كيفية حفظ ملف PDF — إضافة ترقيم بيتس باستخدام Aspose.Pdf
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: كيفية حفظ ملف PDF — إضافة ترقيم بايتس باستخدام Aspose.Pdf
url: /ar/net/programming-with-stamps-and-watermarks/how-to-save-pdf-add-bates-numbering-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ ملف PDF — إضافة ترقيم Bates باستخدام Aspose.Pdf

هل تساءلت يومًا **how to save PDF** عن كيفية حفظ ملفات PDF بعد أن قمت بوضع رقم Bates عليها؟ لست وحدك. في مكاتب المحاماة، والمحاكم، وحتى فرق الامتثال الداخلية، الحاجة إلى تضمين معرف فريد على كل صفحة هي مشكلة يومية. الخبر السار؟ باستخدام Aspose.Pdf لـ .NET يمكنك القيام بذلك ببضع أسطر فقط، وستحصل على ملف PDF محفوظ بشكل مثالي يحمل الترميز الذي تحتاجه.

في هذا الدرس سنستعرض العملية بالكامل: تحميل ملف PDF موجود، إضافة *artifact* لترقيم Bates، وأخيرًا **how to save PDF** إلى موقع جديد. على طول الطريق سنتطرق أيضًا إلى **how to add bates**، **how to add artifact**، وحتى نناقش الموضوع الأوسع وهو **create PDF document** برمجيًا. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع C#.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- حزمة NuGet لـ Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- ملف PDF تجريبي (`input.pdf`) موجود في مجلد يمكنك القراءة/الكتابة فيه
- إلمام أساسي بصياغة C# — لا حاجة لمعرفة عميقة بـ PDF

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فعّل *nullable reference types* للحصول على تجربة تجميع أنظف.

## كيفية حفظ PDF مع ترقيم Bates

تكمن جوهر الحل في ثلاث خطوات بسيطة. كل خطوة محاطة بعنوان H2 خاص بها حتى تتمكن من الانتقال مباشرة إلى الجزء الذي تحتاجه.

### الخطوة 1 – تحميل مستند PDF المصدر

أولاً، نحتاج إلى جلب الملف إلى الذاكرة. تمثل فئة `Document` في Aspose.Pdf كامل ملف PDF، ويمكنك إنشاء كائن منها مباشرةً من مسار الملف.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
using Aspose.Pdf.Text;

namespace BatesNumberDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 1: Load the source PDF document
            string inputPdfPath = @"C:\MyDocs\input.pdf";

            // The Document constructor throws if the file is missing, so wrap it in a try/catch if you need resilience.
            using (var pdfDocument = new Document(inputPdfPath))
            {
                // The rest of the workflow continues inside this using block.
```

**لماذا هذا مهم:** تحميل الملف هو النقطة الوحيدة التي قد يحدث فيها فشل في الإدخال/الإخراج. من خلال الحفاظ على جملة `using` نضمن تحرير مقبض الملف بسرعة—وهو أمر حاسم عندما تقوم لاحقًا بـ **how to save pdf** إلى القرص.

### الخطوة 2 – كيفية إضافة Artifact لترقيم Bates

عادةً ما يتم وضع أرقام Bates في رأس أو تذييل كل صفحة. توفر Aspose.Pdf الفئة `BatesNumberArtifact`، التي تزيد الرقم تلقائيًا لكل صفحة يتم إضافتها إليها.

```csharp
                // 👉 Step 2: Add a Bates number artifact to the first page (you could loop for all pages)
                var batesArtifact = new BatesNumberArtifact
                {
                    // The Text property can contain a format string. "{0}" will be replaced by the page number.
                    Text = "Case-2026-{0}",
                    Position = new Position(50, 50), // X=50pt, Y=50pt from the bottom‑left corner
                    Font = FontRepository.FindFont("Helvetica"),
                    FontSize = 12,
                    // Optional: set color, opacity, etc.
                };

                // Attach the artifact to the first page; Aspose will replicate it on subsequent pages automatically.
                pdfDocument.Pages[1].Artifacts.Add(batesArtifact);
```

**How to add bates** عبر المستند بأكمله؟ إذا كنت تريد الـ artifact على *كل* صفحة، ما عليك سوى إضافته إلى الصفحة الأولى كما هو موضح—Aspose يتولى النشر. للتحكم بشكل أكثر تفصيلاً يمكنك تكرار `pdfDocument.Pages` وإضافة `TextFragment` مخصص بدلاً من ذلك، لكن الـ artifact المدمج هو الأكثر اختصارًا.

### الخطوة 3 – كيفية حفظ PDF إلى موقع جديد

الآن بعد أن يحمل PDF رقم Bates، حان وقت كتابة الملف. هنا يبرز الكلمة المفتاحية الأساسية مرة أخرى: **how to save pdf** بعد التعديلات.

```csharp
                // 👉 Step 3: Save the updated PDF to the desired location
                string outputPdfPath = @"C:\MyDocs\output.pdf";

                // Overwrite if the file already exists; you can also check File.Exists first.
                pdfDocument.Save(outputPdfPath);
                Console.WriteLine($"PDF saved successfully to {outputPdfPath}");
            } // using block disposes the Document
        }
    }
}
```

عند انتهاء طريقة `Save`، يحتوي الملف على القرص على رقم Bates في كل صفحة، وقد تعلمت للتو **how to save pdf** مع Artifact مرفق.

## كيفية إضافة Artifact إلى PDF (ما وراء Bates)

أحيانًا تحتاج إلى علامة مائية عامة، أو شعار، أو ملاحظة مخصصة بدلاً من رقم Bates. مجموعة `Artifacts` نفسها تعمل مع أي عنصر بصري.

```csharp
// Example: Adding a simple text watermark artifact
var watermark = new TextArtifact
{
    Text = "CONFIDENTIAL",
    Position = new Position(200, 400),
    Font = FontRepository.FindFont("Arial"),
    FontSize = 36,
    Color = Color.FromRgb(255, 0, 0),
    Opacity = 0.3
};
pdfDocument.Pages[1].Artifacts.Add(watermark);
```

**لماذا تستخدم artifact؟** الـ Artifacts هي كائنات *غير محتوى*، مما يعني أنها لا تتداخل مع استخراج النص أو ميزات إمكانية الوصول في PDF. لهذا السبب هي الطريقة المفضلة لتضمين أرقام Bates، العلامات المائية، أو أي طبقة تغطية يجب أن تظل غير مرئية لمحركات البحث.

## إنشاء مستند PDF من الصفر (إذا لم يكن لديك ملف إدخال)

الخطوات السابقة افترضت وجود ملف موجود، لكن أحيانًا تحتاج إلى **create PDF document** من الصفر قبل أن تتمكن من **add bates numbering**. إليك مثالًا بسيطًا للبدء:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Create a fresh PDF document
var newDoc = new Document();
Page page = newDoc.Pages.Add();

// Add a simple paragraph
var paragraph = new TextFragment("Hello, this is a newly created PDF.");
page.Paragraphs.Add(paragraph);

// Save it
newDoc.Save(@"C:\MyDocs\newfile.pdf");
```

من هنا يمكنك إعادة استخدام مقتطف *how to add bates* وروتين *how to save pdf* لتحويل لوحة فارغة إلى مستند قانوني مُعلَّم بالكامل.

## حالات الحافة الشائعة والنصائح

| الموقف | ما يجب مراقبته | الإصلاح المقترح |
|-----------|-------------------|---------------|
| **ملف PDF الإدخالي لا يحتوي على صفحات** | `pdfDocument.Pages[1]` يثير استثناء خارج النطاق. | تحقق من أن `pdfDocument.Pages.Count > 0` قبل إضافة الـ artifacts، أو أنشئ صفحة جديدة أولاً. |
| **الصفحات المتعددة تحتاج إلى مواضع مختلفة** | Artifact واحد يطبق نفس الإحداثيات على كل صفحة. | قم بالتكرار عبر `pdfDocument.Pages` واضبط `Artifacts.Add` لكل صفحة مع `Position` مخصص. |
| **ملفات PDF الكبيرة (مئات الميجابايت)** | ضغط الذاكرة أثناء بقاء المستند في الذاكرة. | استخدم `PdfFileEditor` للتعديلات في الموقع، أو عالج الصفحات على دفعات. |
| **تنسيق Bates مخصص** | تريد بادئة أو لاحقة أو أرقام مملوءة بالأصفار. | اضبط `Text = "DOC-{0:0000}"` – المتغير `{0}` يحترم سلاسل تنسيق .NET. |
| **الحفظ إلى مجلد للقراءة فقط** | `Save` يثير استثناء `UnauthorizedAccessException`. | تأكد من أن الدليل الهدف لديه أذونات كتابة، أو اطلب من المستخدم مسارًا بديلًا. |

## النتيجة المتوقعة

بعد تشغيل البرنامج بالكامل:

1. يظهر `output.pdf` في `C:\MyDocs\`.
2. عند فتحه في أي عارض PDF يظهر النص **“Case-2026-1”**، **“Case-2026-2”**، إلخ، موضعًا على بعد 50 pt من الحافة اليسرى والسفلية في كل صفحة.
3. إذا أضفت الـ artifact للعلامة المائية الاختيارية، تظهر كلمة **“CONFIDENTIAL”** شبه شفافة فوق المحتوى.

يمكنك التحقق من أرقام Bates عن طريق تحديد النص (يمكن تحديده لأنه artifacts) أو باستخدام أداة فحص PDF.

## ملخص – كيفية حفظ PDF مع ترقيم Bates في خطوة واحدة

- **Load** تحميل الملف المصدر باستخدام `new Document(path)`.
- **Add** إضافة `BatesNumberArtifact` (أو أي artifact آخر) إلى الصفحة الأولى.
- **Save** حفظ المستند المعدل باستخدام `pdfDocument.Save(destinationPath)`.

هذا هو الجواب الكامل على **how to save pdf** مع تضمين معرف فريد. لا سكريبتات خارجية، ولا تحرير يدوي للصفحات—فقط طريقة C# نظيفة وقابلة لإعادة الاستخدام.

## الخطوات التالية والمواضيع ذات الصلة

- **Add Bates numbering to every page manually** – تكرار عبر `pdfDocument.Pages` لتخصيص كل صفحة.
- **How to add artifact** للصور: استبدل `TextArtifact` بـ `ImageArtifact`.
- **Create PDF document** باستخدام الجداول، المخططات، أو حقول النماذج عبر API الغني لـ Aspose.Pdf.
- **Automate batch processing** – قراءة مجلد من ملفات PDF، تطبيق نفس رقم Bates، وحفظها دفعة واحدة.

لا تتردد في تجربة خطوط وألوان ومواقع مختلفة. مكتبة Aspose.Pdf مرنة بشكل مفاجئ، وبمجرد إتقانك **how to add bates** و **how to add artifact**، لا حدود للإمكانات.

### كود مرجعي سريع (جميع الخطوات في كتلة واحدة)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
using Aspose.Pdf.Text;

class BatesDemo
{
    static void Main()
    {
        string inputPath = @"C:\MyDocs\input.pdf";
        string outputPath = @"C:\MyDocs\output.pdf";

        using (var pdf = new Document(inputPath))
        {
            var bates = new BatesNumberArtifact
            {
                Text = "Case-2026-{0}",
                Position = new Position(50, 50),
                Font = FontRepository.FindFont("Helvetica"),
                FontSize = 12
            };
            pdf.Pages[1].Artifacts.Add(bates);
            pdf.Save(outputPath);
        }

        Console.WriteLine($"Saved PDF with Bates number to {outputPath}");
    }
}
```

شغّل هذا المقتطف، وستحصل على أساس قوي لأي مشروع أتمتة PDF مستقبلي.

*Happy coding! If

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}