---
category: general
date: 2026-03-22
description: أضف ترقيم بايتس إلى ملفات PDF بسرعة باستخدام Aspose.Pdf. تعلم كيفية إضافة
  بايتس، وإضافة أرقام صفحات متسلسلة، وإضافة تذييل مخصص إلى PDF، وإضافة عنصر إلى PDF
  في دقائق.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: ar
og_description: إضافة ترقيم بايتس إلى PDF باستخدام Aspose.Pdf. يوضح هذا الدليل كيفية
  إضافة بايتس، إضافة أرقام صفحات متسلسلة، إضافة تذييل مخصص إلى PDF، وإضافة عنصر إلى
  PDF.
og_title: إضافة ترقيم بايتس إلى PDF – دليل C# خطوة بخطوة
tags:
- Aspose.Pdf
- C#
- PDF automation
title: إضافة ترقيم بايتس إلى PDF – دليل C# الكامل
url: /ar/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم Bates إلى PDF – دليل C# الكامل

هل احتجت يومًا إلى **add bates numbering pdf** لمجموعة من المستندات القانونية لكنك لم تكن متأكدًا من أين تبدأ؟ لست الأول—العديد من المطورين يواجهون هذه المشكلة عند بناء أدوات إدارة القضايا. الخبر السار؟ مع Aspose.Pdf يمكنك **add bates**, **add sequential page numbers**, وحتى **add custom footer pdf** ببضع أسطر من الشيفرة.  

في هذا الدرس سنستعرض العملية بالكامل، من تثبيت المكتبة إلى حفظ الملف النهائي، وسنضيف نصائح حول كيفية **add artifact to pdf** للملفات دون إتلاف المحتوى الموجود. في النهاية ستحصل على مقطع جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- .NET 6+ (الشيفرة تعمل على .NET Core و .NET Framework على حد سواء)  
- رخصة صالحة لـ Aspose.Pdf for .NET (يمكنك البدء بتقييم مجاني)  
- ملف PDF إدخال (`input.pdf`) موجود في مجلد يمكنك الإشارة إليه  
- Visual Studio أو Rider أو أي محرر C# تفضله  

هذا كل شيء—لا توجد حزم NuGet إضافية سوى Aspose.Pdf.

## الخطوة 1: تثبيت Aspose.Pdf عبر NuGet

أولًا وقبل كل شيء—لنقم بإحضار المكتبة إلى جهازك. افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.Pdf
```

أو، إذا كنت تستخدم وحدة التحكم الخاصة بـ Package Manager في Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*نصيحة احترافية:* بعد التثبيت، تأكد من ظهور مجلد `Aspose.Pdf` تحت `Dependencies → Packages` في مستكشف الحل الخاص بك.

## الخطوة 2: تحميل مستند PDF المصدر

الآن نقوم بإنشاء كائن `Document` الذي يمثل ملف PDF الذي نريد وضع العلامة عليه. استخدام جملة `using` يضمن تحرير مقبض الملف تلقائيًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

لماذا نستخدم `using var`؟ يضمن التخلص من الكائن حتى لو حدث استثناء، مما يمنع مشاكل قفل الملف لاحقًا عند محاولة استبدال نفس الملف.

## الخطوة 3: إنشاء وتكوين عنصر Bates Numbering Artifact

رقم Bates هو في الأساس عنصر نصي (artifact) يعيش في البنية المنطقية لملف PDF. يمكنك التعامل معه كـ **custom footer pdf** لأنه يظهر في كل صفحة دون أن يكون جزءًا من تدفق محتوى الصفحة.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### لماذا هذه الإعدادات مهمة

- **Prefix**: مفيد للتمييز بين أنواع المستندات (مثال، “INV‑” للفواتير).  
- **Start**: يحدد الرقم الأول؛ يمكنك إمداده من قاعدة بيانات إذا كنت تحتاج إلى استمرارية عبر الملفات.  
- **Format**: `"0000"` يفرض عرض بأربعة أرقام، مما يضمن المحاذاة عندما يزداد عدد الأرقام.  
- **X/Y**: تُقاس الإحداثيات من الزاوية السفلية اليسرى، لذا `Y = 20` يضع النص فوق هامش الصفحة مباشرة. عدل `X` إذا كنت تريد الرقم محاذيًا إلى اليسار أو مركّزًا.

إذا كنت تحتاج إلى **add sequential page numbers** بدلاً من أرقام Bates، ببساطة احذف `Prefix` واضبط `Format` إلى `"###"` أو أي نمط تفضله.

## الخطوة 4: تطبيق العنصر على جميع الصفحات

تتيح لك Aspose.Pdf إرفاق عنصر (artifact) إلى المستند بأكمله في نداء واحد. هذه هي الطريقة الأكثر كفاءة لـ **add artifact to pdf** دون الحاجة إلى التكرار عبر كل صفحة يدويًا.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

خلف الكواليس، تقوم Aspose بإضافة العنصر إلى قاموس الصفحة لكل صفحة، مما يعني أن الترقيم يصبح جزءًا من البنية المنطقية للـ PDF—مثالي للاستخراج أو البحث لاحقًا.

## الخطوة 5: حفظ ملف PDF المحدث

أخيرًا، احفظ التغييرات على القرص. يمكنك استبدال الملف الأصلي أو حفظه في ملف جديد؛ الخيار الأخير أكثر أمانًا أثناء التطوير.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

عند فتح `output.pdf` في عارض، سترى “INV‑1000”، “INV‑1001”، … في أسفل يمين كل صفحة.

### التحقق من النتيجة

افتح ملف PDF في Adobe Acrobat أو أي عارض وابحث عن الأرقام. إذا كنت بحاجة إلى التأكد برمجيًا، يمكنك قراءة العنصر مرة أخرى:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو كان ملف PDF الخاص بي يحتوي بالفعل على تذييل؟

إضافة عنصر لن يكتب فوق التذييلات الموجودة لأن العناصر تقع في طبقة منفصلة. ومع ذلك، إذا كان التداخل البصري مصدر قلق، عدل إحداثية `Y` أو زد إزاحة `X` لتحريك رقم Bates بعيدًا.

### هل يمكنني استخدام خط أو لون مختلف؟

بالطبع. `BatesNumberingArtifact` يرث من `Artifact`، لذا يمكنك ضبط `Font`، `FontColor`، وحتى `Opacity`. مثال:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### كيف أعيد ضبط العداد لمستند جديد؟

فقط غيّر `Start` قبل استدعاء `AddArtifact`. إذا كنت تولد العديد من ملفات PDF في حلقة، احتفظ بعداد مستمر في منطق التطبيق.

### هل هذا الأسلوب متوافق مع ملفات PDF المشفرة؟

يمكن لـ Aspose.Pdf فتح ملفات PDF المشفرة إذا زودتها بكلمة المرور:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

بعد فك التشفير، تعمل خطوات إضافة العنصر بنفس السلاسة.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. الصقه في تطبيق Console، عدل المسارات، واضغط **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**الناتج المتوقع:** يطبع الـ Console “Bates numbering added successfully!” وملف `output.pdf` يحتوي على تسميات متسلسلة مثل `INV‑1000`، `INV‑1001`، إلخ، موضوعة في أسفل يمين كل صفحة.

## ملخص سريع

- **الهدف الأساسي:** **add bates numbering pdf** باستخدام Aspose.Pdf.  
- غَطينا **how to add bates**, **add sequential page numbers**, و **add custom footer pdf** عبر عنصر واحد.  
- الدرس أظهر كيفية **add artifact to pdf**, التعامل مع الحالات الخاصة، والتحقق من النتيجة.  

## ما التالي؟

- **Dynamic prefixes:** سحب القيم من قاعدة بيانات لتوليد “CASE‑2023‑001”، “CASE‑2023‑002”، …  
- **Conditional placement:** استخدم كشف حجم الصفحة (`page.MediaBox`) لتوسيط الأرقام في الصفحات الأفقية.  
- **Combine with watermarks:** أضف شعارًا شبه شفاف بجانب رقم Bates للعلامة التجارية.  

لا تتردد في التجربة—ربما تكتشف طريقة أذكى لمعالجة آلاف الملفات دفعيًا. إذا واجهت مشكلة، اترك تعليقًا أو راجع وثائق Aspose الرسمية (إنها واضحة بشكل مدهش). برمجة سعيدة!  

![مثال على إضافة ترقيم Bates إلى PDF](https://example.com/bates-numbering-screenshot.png "لقطة شاشة تُظهر إضافة ترقيم bates إلى PDF في عارض PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}