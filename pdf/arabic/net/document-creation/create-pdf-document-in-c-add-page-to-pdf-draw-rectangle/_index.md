---
category: general
date: 2026-03-24
description: إنشاء مستند PDF في C# باستخدام Aspose.Pdf – تعلم كيفية إضافة صفحة إلى
  PDF، ورسم مستطيل، وحفظ PDF إلى ملف.
draft: false
keywords:
- create pdf document
- add page to pdf
- save pdf to file
- how to create pdf
- how to add rectangle
language: ar
og_description: إنشاء مستند PDF في C# باستخدام Aspose.Pdf. تعلّم كيفية إضافة صفحة
  إلى PDF، ورسم مستطيل، وحفظ PDF إلى ملف في بضع خطوات سهلة.
og_title: إنشاء مستند PDF في C# – إضافة صفحة إلى PDF ورسم مستطيل
tags:
- pdf
- csharp
- aspose
title: إنشاء مستند PDF في C# – إضافة صفحة إلى PDF ورسم مستطيل
url: /ar/net/document-creation/create-pdf-document-in-c-add-page-to-pdf-draw-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF في C# – إضافة صفحة إلى PDF ورسم مستطيل

هل احتجت يومًا إلى **إنشاء مستند pdf** في C# لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—معظم المطورين يواجهون هذه المشكلة عندما يتعاملون لأول مرة مع إنشاء ملفات PDF برمجيًا. الخبر السار هو أنه باستخدام Aspose.Pdf يمكنك إنشاء PDF، إضافة صفحة إلى pdf، وضع مستطيل عليها، ثم حفظ pdf إلى ملف في بضع أسطر فقط.

في هذا البرنامج التعليمي سنستعرض العملية بالكامل، من تهيئة المستند إلى حفظه على القرص. بنهاية الدرس ستعرف **كيفية إنشاء pdf** في الوقت الفعلي، **كيفية إضافة مستطيل**، وأين يتم حفظ الملف على نظامك.

## ما ستتعلمه

- كيف تستخدم **إنشاء مستند pdf** باستخدام فئة `Document` الخاصة بـ Aspose.Pdf.  
- الطريقة الصحيحة لـ **إضافة صفحة إلى pdf** دون حدوث أخطاء تخطيط.  
- إرشادات خطوة بخطوة حول **كيفية إضافة مستطيل** إلى صفحة.  
- الطريقة الأكثر أمانًا لـ **حفظ pdf إلى ملف** ومعالجة المشكلات الشائعة.  

لا توجد متطلبات مسبقة معقدة—فقط بيئة تطوير .NET وحزمة NuGet Aspose.Pdf for .NET.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#.  
- تثبيت Aspose.Pdf for .NET (`dotnet add package Aspose.Pdf`).  

إذا كان لديك كل ذلك، لنبدأ.

## نظرة عامة على إنشاء مستند PDF

أول شيء عليك فعله هو إنشاء كائن `Document`. فكر فيه كقماش فارغ ينتظر الصفحات والنصوص والصور أو الأشكال.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document in memory
using var pdfDocument = new Document();
```

لماذا نستخدم `using var`؟ فهو يضمن أن تدفقات الملفات الأساسية تُغلق تلقائيًا، مما يمنع حدوث أخطاء قفل الملفات لاحقًا عندما تحاول **حفظ pdf إلى ملف**.

## إضافة صفحة إلى PDF

PDF بدون صفحات هو في الأساس غلاف فارغ. إضافة صفحة بسيطة كاستدعاء `Pages.Add()`. تُعيد هذه الطريقة كائن `Page` يمكنك البدء بالعمل عليه فورًا.

```csharp
// Step 2: Add a blank page to the document
var pdfPage = pdfDocument.Pages.Add();
```

**نصيحة محترف:** حجم الصفحة الافتراضي هو A4 (595 × 842 نقطة). إذا كنت تحتاج حجمًا مختلفًا، مرّر تعداد `PageSize` أو أبعادًا مخصصة إلى `Add()`.

```csharp
// Example: Add a Letter‑sized page
var letterPage = pdfDocument.Pages.Add(PageSize.Letter);
```

## كيفية إضافة مستطيل إلى صفحة PDF

الآن للجزء الممتع—رسم مستطيل. فئة `Rectangle` في Aspose.Pdf تتوقع إحداثيات الزاوية السفلية اليسرى متبوعة بالعرض والارتفاع. تُقاس هذه القيم بالنقاط (1 pt ≈ 1/72 in).

```csharp
// Step 3: Insert a rectangle shape onto the page
// Lower‑left corner at (0,0), width 600 pt, height 800 pt
pdfPage.Paragraphs.Add(new Rectangle(0, 0, 600, 800));
```

### لماذا هذه الأرقام مهمة

- **(0,0)** يضع المستطيل في أسفل اليسار من الصفحة.  
- **600 × 800** يتناسب بشكل مريح داخل صفحة A4 (التي قياسها 595 × 842).  
- إذا تجاوز المستطيل حدود الصفحة، سيطرح Aspose استثناءً—لذا تحقق دائمًا من الأبعاد، خاصةً عند تغيير حجم الصفحة.

### تخصيص المستطيل

يمكنك تغيير نمط الخط، اللون، والملء:

```csharp
var rect = new Rectangle(50, 700, 200, 100)
{
    Border = new BorderInfo(BorderSide.All, .5f, Color.Black),
    FillColor = Color.LightGray
};
pdfPage.Paragraphs.Add(rect);
```

هذا المقتطف يرسم مستطيل بحجم 200 × 100 pt، إزاحة 50 pt من اليسار و700 pt من الأسفل، بحدود سوداء رفيعة وملء رمادي فاتح.

## حفظ PDF إلى ملف

بمجرد أن تبدو صفحتك كما تريد، حفظ الملف هو الخطوة الأخيرة. طريقة `Save` تقبل مسار ملف، أو `Stream`، أو حتى `MemoryStream` إذا رغبت بإرسال PDF عبر الشبكة.

```csharp
// Step 4: Save the PDF to a file on disk
pdfDocument.Save("C:\\Temp\\output.pdf");
```

**تذكر:** عند تشغيل هذا على Linux، استخدم الشرطات المائلة للأمام (`/`) أو `Path.Combine` لتجنب مشاكل فواصل المسار.

### معالجة الاستثناءات

قد يفشل الحفظ لأسباب مثل عدم كفاية أذونات الكتابة أو وجود ملف للقراءة فقط. غلف الاستدعاء داخل try/catch لتظهر تشخيصات مفيدة:

```csharp
try
{
    pdfDocument.Save("C:\\Temp\\output.pdf");
}
catch (IOException ex)
{
    Console.WriteLine($"Unable to write file: {ex.Message}");
}
```

## مثال كامل يعمل

فيما يلي برنامج مستقل يمكنك نسخه ولصقه في تطبيق Console. يوضح **كيفية إنشاء pdf**، **إضافة صفحة إلى pdf**، **كيفية إضافة مستطيل**، و**حفظ pdf إلى ملف**—كل ذلك في خطوة واحدة.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing; // For Color struct

class Program
{
    static void Main()
    {
        // 1️⃣ Create the PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Add a new page (default A4)
        var page = pdfDocument.Pages.Add();

        // 3️⃣ Draw a rectangle – fits inside the page
        var rect = new Rectangle(0, 0, 600, 800)
        {
            Border = new BorderInfo(BorderSide.All, 1.0f, Color.Blue),
            FillColor = Color.AliceBlue
        };
        page.Paragraphs.Add(rect);

        // 4️⃣ Persist the PDF to disk
        const string outputPath = "output.pdf";
        try
        {
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF successfully saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error saving PDF: {ex.Message}");
        }
    }
}
```

**النتيجة المتوقعة:** افتح `output.pdf` وسترى صفحة A4 واحدة تحتوي على مستطيل بحدود زرقاء وملء أزرق فاتح مثبت في الزاوية السفلية اليسرى. لا تحتاج إلى نص؛ المستطيل نفسه يثبت أن الشكل أُضيف بشكل صحيح.

## المشكلات الشائعة والنصائح

| المشكلة | لماذا يحدث | كيفية الإصلاح |
|-------|----------------|---------------|
| **يتجاوز المستطيل حجم الصفحة** | إحداثيات أو أبعاد أكبر من أبعاد الصفحة تسبب `ArgumentException`. | تحقق مرة أخرى من حجم الصفحة (`page.PageInfo.Width`, `.Height`) قبل الرسم. |
| **مسار الملف غير قابل للكتابة** | تشغيل البرنامج بحساب مستخدم مقيد أو محاولة الكتابة إلى مجلد محمي. | استخدم دليلًا يمكن للمستخدم الكتابة فيه مثل `%TEMP%` أو `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)`. |
| **نسيان إغلاق الكائن** | عدم إغلاق `Document` قد يقفل الملف حتى انتهاء العملية. | استخدم `using var` أو استدعِ `pdfDocument.Dispose()` صراحة. |
| **غياب مرجع Aspose.Pdf** | حزمة NuGet غير مثبتة أو المشروع يستهدف إطارًا غير متوافق. | نفّذ `dotnet add package Aspose.Pdf` وتأكد من دعم إطار العمل المستهدف. |

### الحالات الخاصة

- **صفحات متعددة:** استدعِ `pdfDocument.Pages.Add()` لكل صفحة إضافية، ثم أضف الأشكال إلى كائنات `Page` المقابلة.  
- **أبعاد ديناميكية:** إذا كنت تحتاج أن يملأ المستطيل الصفحة بالكامل، استخدم `page.PageInfo.Width` و `page.PageInfo.Height` للعرض/الارتفاع.  
- **البث إلى عميل ويب:** استبدل `pdfDocument.Save(filePath)` بـ `pdfDocument.Save(stream, SaveFormat.Pdf)` واكتب الـ stream إلى استجابة HTTP.

## الخطوات التالية

الآن بعد أن عرفت **كيفية إنشاء pdf**، فكر في توسيع المستند:

- أضف نصًا باستخدام `TextFragment`.  
- أدخل صورًا عبر فئة `Image`.  
- أنشئ جداول للفواتير أو التقارير.  

كل هذه تتبع النمط نفسه: أنشئ كائنًا، اضبط خصائصه، وأضفه إلى `page.Paragraphs`.

إذا كنت فضوليًا حول تنسيقات أكثر تقدمًا—مثل التدرجات، الدورانات، أو تشفير PDF—اطلع على الوثائق الرسمية لـ Aspose أو سلسلة دروس “معالجة PDF المتقدمة”.

## الخلاصة

غطّينا كل ما تحتاجه **لإنشاء مستند pdf** في C# باستخدام Aspose.Pdf: تهيئة المستند، **إضافة صفحة إلى pdf**، رسم مستطيل باستخدام **كيفية إضافة مستطيل**، وأخيرًا **حفظ pdf إلى ملف**. المثال الكامل يعمل فورًا، والنصائح أعلاه ستجنبك معظم المشكلات الشائعة.

Give it

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}