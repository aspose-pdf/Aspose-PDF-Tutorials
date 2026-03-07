---
category: general
date: 2026-03-06
description: إنشاء مستند PDF باستخدام C# وإضافة أرقام باتس بسهولة. تعلم كيفية إضافة
  صفحة فارغة إلى PDF، وضع ختم على الصفحة، وتنفيذ ترقيم باتس.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: ar
og_description: إنشاء مستند PDF في C# وإضافة رقم بَيتس. يوضح هذا الدليل كيفية إضافة
  صفحة فارغة إلى PDF، وضع ختم على الصفحة، وتطبيق ترقيم بَيتس.
og_title: إنشاء مستند PDF مع ترقيم بيتس – دليل C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: إنشاء مستند PDF مع ترقيم بيتس في C# – دليل كامل
url: /ar/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF مع ترقيم Bates في C#

هل احتجت يوماً إلى **إنشاء مستند PDF** باستخدام C# وتساءلت كيف تضيف رقم Bates دون أن تفقد أعصابك؟ لست وحدك—مكاتب المحاماة والمحاكم وحتى بعض فرق الامتثال في الشركات تواجه هذا اللغز يوميًا. الخبر السار؟ ببضع أسطر من كود Aspose.Pdf يمكنك إنشاء PDF جديد تمامًا، إضافة صفحة فارغة، وختم رقم Bates بشكل صحيح في تدفق واحد سلس.

في هذا الدرس سنستعرض العملية بالكامل: من إعداد المشروع، إلى إضافة صفحة PDF فارغة، إلى معرفة **كيفية إضافة ترقيم Bates**، وأخيرًا **وضع الختم على الصفحة** وحفظ النتيجة. في النهاية ستحصل على مقتطف جاهز يمكنك إدراجه في أي تطبيق .NET. لا مراجع غامضة، مجرد مثال كامل وقابل للتنفيذ.

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+ – Aspose.Pdf يعمل مع كلاهما)
- حزمة NuGet **Aspose.Pdf for .NET** (`Install-Package Aspose.Pdf`)
- بيئة تطوير متكاملة جيدة (Visual Studio، Rider، أو VS Code مع امتداد C#)

هذا كل ما تحتاجه. لا ملفات DLL إضافية، ولا خدمات خارجية. هيا نبدأ.

## الخطوة 1: إنشاء مستند PDF – الإعداد الأولي

أولاً، نحتاج إلى كائن `Document` جديد. فكر فيه كقماش فارغ سيُملأ بكل ما يلي.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **لماذا هذا مهم:** فئة `Document` هي نقطة الدخول لكل عملية في Aspose. إنشاء كائن منها يمنحك الوصول إلى مجموعة `Pages`، والبيانات الوصفية، وإعدادات الأمان—كل اللبنات الأساسية لإنشاء PDF احترافي.

## الخطوة 2: إضافة صفحة PDF فارغة

PDF بدون صفحات يشبه كتابًا بلا صفحات—غير مفيد. إضافة صفحة فارغة أمر بسيط، وتوفر لنا سطحًا لختم رقم Bates عليه.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **نصيحة محترف:** إذا كنت بحاجة إلى عدة صفحات، فقط استدعِ `pdfDocument.Pages.Add()` داخل حلقة. كل استدعاء يُعيد كائن `Page` جديد يمكنك تخصيصه بشكل مستقل.

## الخطوة 3: كيفية إضافة ترقيم Bates – إنشاء TextStamp

الآن يأتي جوهر الموضوع: **رقم Bates**. في Aspose.Pdf هو مجرد `TextStamp` مع علامة `Artifact` خاصة.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **لماذا نحدد `Artifact`**: بعض قارئات PDF تعرض أرقام Bates كبيانات وصفية قابلة للبحث. وضع العلامة `BatesNumbering` على الختم يضمن أن الأدوات اللاحقة يمكنها التعرف عليه تلقائيًا.

## الخطوة 4: وضع الختم على الصفحة

مع جاهزية الختم، الآن **نضع الختم على الصفحة**. هذه هي الخطوة التي يظهر فيها الرقم بصريًا داخل PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **حالة حافة:** إذا كنت بحاجة إلى زيادة الرقم في كل صفحة، يمكنك المرور على `pdfDocument.Pages` وتحديث `batesStamp.Value` قبل استدعاء `AddStamp`. المثال هنا يبقي الأمر بسيطًا برقم ثابت “Bates‑001”.

## الخطوة 5: حفظ والتحقق من النتيجة

أخيرًا، نقوم بحفظ PDF على القرص. اختر مجلدًا لديك صلاحية كتابة فيه؛ وإلا ستواجه استثناء `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

عند فتح `BatesStamped.pdf` في أي عارض يجب أن ترى “Bates‑001” صغيرًا مُثبتًا في الزاوية السفلية اليمنى للصفحة الفارغة.

> **الناتج المتوقع:**  
> ![PDF مع ختم رقم Bates](image-placeholder.png "PDF مع ختم رقم Bates")  
> *نص بديل: PDF مع ختم رقم Bates في الزاوية السفلية اليمنى.*

إذا لم يظهر الرقم، تحقق من قيم الهوامش وتأكد من أن حجم الصفحة ليس صغيرًا جدًا (A4 الافتراضي يعمل جيدًا). كما تأكد أن علامة `Artifact` لم تُحذف بواسطة أي أدوات معالجة لاحقة.

## مثال كامل يعمل

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. يتضمن جميع توجيهات `using` والتعليقات لتبقى موجهًا.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

شغّل البرنامج، افتح الـ PDF، وسترى رقم Bates بالضبط حيث أخبرناه أن يضعه. 🎉

## الاختلافات الشائعة والمفاجآت

| السيناريو | ما الذي يجب تغييره | السبب |
|----------|-------------------|-------|
| **عدة صفحات، أرقام متزايدة** | كرّر `pdfDocument.Pages`، وضع `batesStamp.Value = $"Bates-{i:D3}"` قبل `AddStamp` | يمنح كل صفحة معرفًا فريدًا، وهو شائع في حزم المستندات القانونية |
| **موضع مختلف (أعلى‑يسار)** | غيّر `HorizontalAlignment = HorizontalAlignment.Left` و `VerticalAlignment = VerticalAlignment.Top` | بعض المؤسسات تفضّل الرقم في الرأس بدلاً من التذييل |
| **خط أو لون مخصص** | اضبط `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | يحسن القابلية للقراءة أو يطابق إرشادات العلامة التجارية |
| **إضافة PDF موجود كخلفية** | حمّل PDF المصدر بـ `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | مفيد عندما تحتاج إلى الختم فوق نموذج مُولد مسبقًا |

## الخلاصة

لقد أظهرنا لك كيفية **إنشاء مستند PDF**، **إضافة صفحة PDF فارغة**، و**إضافة رقم Bates** باستخدام Aspose.Pdf for .NET، ثم **وضع الختم على الصفحة** وحفظ الملف. الكود مختصر عمدًا لتتمكن من تعديله ليتناسب مع سير عمل أكبر—سواءً كنت تُعالج عشرات الملفات دفعيًا أو تدمجه في خدمة ويب.

إذا كنت مستعدًا للخطوة التالية، فكر في:

- أتمتة منطق الزيادة للأرشيفات الكبيرة.
- دمج توليد PDF في API باستخدام ASP.NET Core.
- إضافة أمان (حماية بكلمة مرور) عبر `pdfDocument.Encrypt(...)`.

لا تتردد في التجربة، واكتشاف الأخطاء، وطرح الأسئلة في التعليقات. برمجة سعيدة، ولتكن ملفات PDF دائمًا مختومة بشكل مثالي!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}