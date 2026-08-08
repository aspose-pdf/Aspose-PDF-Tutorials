---
category: general
date: 2026-05-27
description: إضافة ترقيم بايتس إلى ملفات PDF باستخدام Aspose.Pdf في C#. تعلم كيفية
  إضافة ترقيم بايتس بسرعة، تخصيص الصيغة، وأتمتة وسم المستندات القانونية.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: ar
og_description: إضافة ترقيم بايتس إلى PDF باستخدام Aspose.Pdf في C#. يوضح هذا الدليل
  كيفية إضافة ترقيم بايتس، وتكوين البادئات، وحفظ النتيجة.
og_title: إضافة ترقيم بايتس إلى PDF في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: إضافة ترقيم بايتس إلى ملف PDF باستخدام C# – دليل كامل
url: /ar/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم بايتس إلى ملفات PDF في C# – دليل شامل

هل تساءلت يومًا **كيف تضيف ترقيم بايتس** إلى ملف PDF دون قضاء ساعات في الأدوات اليدوية؟ لست وحدك—ففرق القانونية، المدققون، ومتخصصو الاكتشاف الإلكتروني جميعهم يحتاجون إلى طريقة موثوقة **لإضافة ترقيم بايتس إلى ملفات PDF** برمجيًا.  

في هذا الدرس سنستعرض حلًا مختصرًا من البداية إلى النهاية باستخدام Aspose.Pdf لـ .NET، بحيث يمكنك وضع أرقام بايتس على أي مستند ببضع أسطر من كود C# فقط.

## ما ستتعلمه

- كيفية فتح ملف PDF موجود باستخدام Aspose.Pdf  
- كيفية إنشاء كائن ترقيم بايتس وضبط تنسيقه بدقة  
- كيفية إرفاق الكائن بكل صفحة (أو بالصفحة الأولى فقط)  
- كيفية حفظ الملف المحدث والتحقق من النتيجة  

لا تحتاج إلى خبرة سابقة مع Aspose—فقط فهم أساسي لـ C# و .NET. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك نسخه ولصقه في أي مشروع.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)  
- حزمة NuGet الخاصة بـ Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)  
- ملف PDF مصدر تريد وضع العلامة عليه (ضعه في مجلد يمكنك الإشارة إليه)

> **نصيحة احترافية:** إذا لم تكن لديك رخصة بعد، تقدم Aspose مفتاحًا مؤقتًا مجانيًا يزيل علامات التقييم.

## الخطوة 1 – فتح مستند PDF المصدر  

أولاً نحتاج إلى كائن `Document` يمثل الملف على القرص. فكر في ذلك كتحميل لوحة فارغة سنرسم عليها أرقام بايتس لاحقًا.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**لماذا هذا مهم:** فتح المستند داخل كتلة `using` يضمن تحرير جميع الموارد غير المدارة بسرعة، وهو أمر مهم خاصةً مع ملفات PDF الكبيرة.

## الخطوة 2 – إنشاء كائن ترقيم بايتس  

`BatesNumberingArtifact` هو طريقة Aspose لتحديد شكل الأرقام. يمكنك تعيين بادئة، رقم بداية، زيادة، وحتى سلسلة تنسيق مخصصة.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**لماذا قد تحتاج لتغيير هذه القيم:**  
- **Prefix** مفيد لمعرفات القضايا (“CASE‑”, “DOC‑”).  
- **StartNumber** يسمح لك بالاستمرار من سلسلة سابقة.  
- **Increment** يمكن ضبطه إلى 2 إذا كنت تحتاج ترقيمًا فرديًا/زوجيًا.  
- **Format** يدعم أي تنسيق مركب في .NET؛ `{0:D5}` يضمن خمسة أرقام مع أصفار بادئة.

## الخطوة 3 – إرفاق الكائن بالصفحات المطلوبة  

يمكنك إضافة الكائن إلى صفحة واحدة، نطاق، أو المستند بأكمله. في معظم سير عمل القانونية نرفقه إلى *كل* صفحة، لكن المثال أدناه يوضح الحالة الأدنى—إضافته إلى الصفحة الأولى فقط.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

إذا كنت بحاجة لتغطية جميع الصفحات، يمكنك حلقة عبرها:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**لماذا هذه الخطوة حاسمة:** يتم رسم الكائنات *بعد* محتوى الصفحة، لذا تظهر الأرقام فوق النص الموجود دون تعديل التخطيط الأصلي.

## الخطوة 4 – حفظ ملف PDF المعدل  

أخيرًا، اكتب التغييرات إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد—هنا سننشئ نسخة جديدة تسمى `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

عند فتح `bates.pdf` ستلاحظ وجود “ABC01000” (أو أي تنسيق اخترته) مطبوعًا في الموقع الافتراضي—عادةً الزاوية السفلية اليمنى.

## مثال كامل يعمل  

بدمج كل ما سبق، إليك البرنامج الكامل الذي يمكنك تجميعه وتشغيله:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج، سيطبع الطرفية:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

فتح `bates.pdf` يظهر البادئة “ABC” متبوعةً بتسلسل مكوّن من خمسة أرقام بصفر بادئ على كل صفحة—تمامًا ما طلبته من الكود.

## أسئلة شائعة وحالات خاصة

### هل يمكنني وضع رقم بايتس في موضع آخر؟

نعم. استخدم خاصية `Location` في `BatesNumberingArtifact` (مثال: `Location = new Position(10, 10)`) لتحديد إحداثيات X/Y مخصصة. يمكنك أيضًا ضبط `HorizontalAlignment` و `VerticalAlignment` لمزيد من التحكم.

### ماذا لو كان ملف PDF يحتوي على آلاف الصفحات؟

Aspose.Pdf يبث الصفحات بكفاءة، لكن من الأفضل معالجة المستند على دفعات إذا واجهت حدود الذاكرة. فئة `Document` تدعم أيضًا `PdfConverter` للحفظ التدريجي.

### كيف أغيّر الخط أو اللون؟

غلف الكائن داخل كائن `TextState`:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### هل أحتاج رخصة للاستخدام في الإنتاج؟

الإصدار المرخص يزيل علامات التقييم ويُفَعِّل الأداء الكامل. النسخة التجريبية المجانية تكفي للاختبار وإثبات المفهوم.

## التحقق – فحص بصري سريع  

إذا كنت تفضّل التحقق الآلي، يمكن لـ Aspose استخراج نص صفحة وتأكيد وجود البادئة:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

تشغيل هذا بعد خطوة الحفظ سيطبع `Bates number verified.` إذا سارت الأمور بسلاسة.

## الخلاصة  

أنت الآن تعرف **كيف تضيف ترقيم بايتس إلى ملفات PDF** باستخدام Aspose.Pdf في C#. من فتح المستند إلى ضبط الكائن، إرفاقه بالصفحات، وحفظ النتيجة، العملية بسيطة وقابلة للبرمجة بالكامل.  

ما الخطوة التالية؟ جرّب التجربة مع:

- قيم `Prefix` مختلفة لمجموعات قضايا متعددة  
- `Location` و `TextState` مخصصة للعلامة التجارية  
- إضافة بادئات خاصة بالصفحة (مثل “VOL‑1‑”، “VOL‑2‑”) عبر تعديل `StartNumber` في كل دورة حلقة  

هذه التعديلات تسمح لك بتكييف الحل مع أي سير عمل قانوني أو أرشيفي تقريبًا.  

هل لديك أسئلة إضافية حول **كيفية إضافة ترقيم بايتس** لملفات PDF متعددة اللغات أو المشفرة؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

## دروس ذات صلة

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Different Headers in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}