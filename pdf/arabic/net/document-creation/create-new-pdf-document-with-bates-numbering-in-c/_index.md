---
category: general
date: 2026-08-04
description: إنشاء مستند PDF جديد في C# وإضافة ترقيم بايتس بسرعة باستخدام Aspose.Pdf
  – تعلم كيفية إضافة صفحة فارغة إلى PDF وأرقام صفحات مخصصة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: ar
lastmod: 2026-08-04
og_description: إنشاء مستند PDF جديد باستخدام C# وإضافة ترقيم بايتس تلقائيًا إلى ملف
  PDF لإدارة القضايا القانونية – مثال كامل على الكود مرفق.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: إنشاء مستند PDF جديد مع ترقيم بايتس في C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: إنشاء مستند PDF جديد مع ترقيم بايتس في C#
url: /ar/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF جديد مع ترقيم Bates في C#

إذا كنت بحاجة إلى **إنشاء مستند PDF جديد** في C#، يوضح لك هذا الدليل كيفية **إضافة ترقيم Bates إلى PDF** باستخدام Aspose.Pdf. ستتعلم كيفية **إضافة صفحة فارغة إلى PDF**، وتكوين **إضافة أرقام صفحات مخصصة**، وحفظ الملف النهائي.

يغطي الدليل كل خطوة من تثبيت المكتبة إلى إنشاء PDF يتوافق مع معايير ملفات القضايا القانونية. في النهاية ستتمكن من إنشاء PDF، وإدراج صفحة فارغة، وتطبيق أرقام Bates، وتخصيص تنسيق الترقيم—كل ذلك ببرنامج واحد قابل للتنفيذ.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 SDK أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير C#)  
* ترخيص Aspose.Pdf for .NET ساري أو مفتاح تقييم مجاني  

لا تحتاج إلى أي حزم NuGet إضافية؛ يقوم الدليل بتثبيت كل شيء تلقائيًا.

## الخطوة 1: تثبيت Aspose.Pdf عبر NuGet

افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.Pdf
```

يضيف هذا الأمر أحدث نسخة مستقرة من Aspose.Pdf إلى مشروعك، والتي توفر الفئات `Document`، `BatesNumbering`، وغيرها من فئات معالجة PDF التي ستستخدمها.

## الخطوة 2: إنشاء مستند PDF جديد – الإعداد الأولي

إنشاء ملف PDF هو الأساس لكل عملية لاحقة. تمثل فئة `Document` الحاوية الكاملة للـ PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*لماذا هذا مهم*: إنشاء كائن `Document` يخصص البنى الداخلية المطلوبة للصفحات، الخطوط، والرسومات. استخدام `using var` يضمن التخلص الصحيح من الملف بعد الحفظ.

## الخطوة 3: إضافة صفحة فارغة إلى PDF

يجب أن يحتوي PDF على صفحة واحدة على الأقل قبل أن تتمكن من وضع محتوى عليها. إضافة صفحة فارغة يمنحك مساحة نظيفة لأرقام Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

طريقة `Pages.Add()` تُضيف صفحة جديدة فارغة في نهاية مجموعة صفحات المستند. يمكنك تكرار هذه الدعوة لإضافة المزيد من الصفحات إذا احتجت لاحقًا إلى **إضافة أرقام صفحات مخصصة** عبر صفحات متعددة.

## الخطوة 4: تكوين ترقيم Bates – كيفية إضافة Bates

ترقيم Bates هو معرف تسلسلي يُستخدم عادة في المستندات القانونية. يمكنك تكوينه عبر فئة `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*لماذا هذا مهم*: `StartNumber` يحدد الرقم الأول، `Prefix` يضيف تسمية قابلة للقراءة، و`Increment` يتحكم في حجم الخطوة. يمكنك أيضًا تعديل `HorizontalAlignment`، `VerticalAlignment`، `FontSize`، و`Margins` للتحكم في مظهر الرقم على كل صفحة.

## الخطوة 5: تطبيق ترقيم Bates على الصفحة

الآن بعد أن أصبحت خيارات الترقيم جاهزة، طبّقها على الصفحة (أو على المستند بأكمله).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

استدعاء `Apply` يُدرج الرقم المُنسق في تذييل الصفحة افتراضيًا. إذا كنت تحتاج الرقم في موضع آخر، عيّن `bates.Position` قبل استدعاء `Apply`.

## الخطوة 6: حفظ PDF مع تطبيق أرقام Bates

أخيرًا، اكتب المستند الموجود في الذاكرة إلى القرص.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

الملف المحفوظ الآن يحتوي على صفحة واحدة مع رقم Bates **CaseA-1000** معروض في أسفل الصفحة. افتح الـ PDF بأي عارض للتحقق من الترقيم.

## النتيجة المتوقعة

عند فتح `BatesNumbered.pdf`، يجب أن ترى:

* صفحة فارغة واحدة (أو أكثر إذا أضفت صفحات إضافية)  
* النص **CaseA-1000** موضعًا في أسفل الصفحة (الموقع الافتراضي)  

إذا أضفت صفحات أخرى وأعدت استخدام نفس كائن `BatesNumbering`، ستزداد الأرقام تلقائيًا (CaseA-1001، CaseA-1002، …).

## نصيحة احترافية: إضافة أرقام صفحات مخصصة بالإضافة إلى أرقام Bates

في بعض الأحيان تحتاج إلى كل من أرقام Bates وأرقام الصفحات التقليدية. يمكنك دمجهما بإضافة `TextFragment` بعد تطبيق ترقيم Bates:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

هذا المقتطف يوضح **إضافة أرقام صفحات مخصصة** مع الحفاظ على تسمية Bates.

## حالة خاصة: تطبيق ترقيم Bates على صفحات متعددة

إذا كان المستند يحتوي على عدة صفحات، يمكنك تطبيق نفس كائن `BatesNumbering` على كل صفحة داخل حلقة:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

تضمن الحلقة أن كل صفحة تتلقى رقمًا تسلسليًا بناءً على `StartNumber` و`Increment` اللذين حددتهما.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| الأرقام تظهر غير متمركزة | قد لا يتطابق المحاذاة الافتراضية مع تخطيطك | عيّن `bates.HorizontalAlignment` و`bates.VerticalAlignment` صراحةً |
| الأرقام تتداخل مع المحتوى الموجود | لا توجد هوامش معرفة | عدّل `bates.Margin` أو استخدم `bates.Position` لتحريك الرقم |
| استثناء الترخيص أثناء التشغيل | نسخة التقييم تقيد الإخراج | طبّق ترخيص Aspose.Pdf صالح قبل إنشاء المستند (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## مثال كامل يعمل

فيما يلي برنامج مستقل يمكنك نسخه، لصقه، وتشغيله.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إضافة وتخصيص أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF for .NET | دليل معالجة المستندات](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET: إضافة أرقام صفحات إلى PDF باستخدام FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [إنشاء مستند PDF باستخدام Aspose.PDF – إضافة صفحة، شكل وحفظ](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}