---
category: general
date: 2026-02-10
description: إنشاء مستند PDF في C# باستخدام Aspose.Pdf. تعلم كيفية إضافة صفحة إلى
  PDF وكيفية إضافة مستطيل إلى PDF بأمان، باستخدام فحص الحدود.
draft: false
keywords:
- create pdf document
- add page to pdf
- how to add rectangle pdf
language: ar
og_description: إنشاء مستند PDF في C# باستخدام Aspose.Pdf. يوضح هذا الدليل كيفية إضافة
  صفحة إلى PDF وكيفية إضافة مستطيل إلى PDF مع التحقق من الحدود.
og_title: إنشاء مستند PDF في C# – إضافة صفحة إلى PDF ومستطيل
tags:
- pdf
- csharp
- aspose
title: إنشاء مستند PDF في C# – إضافة صفحة إلى PDF ومستطيل
url: /ar/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/
---

Now produce final output with all translations.

Check for any missed markdown elements: code block placeholders are fine.

Make sure to preserve bullet list formatting.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF في C# – إضافة صفحة إلى PDF ومستطيل

هل احتجت يومًا إلى **create pdf document** في C# ولم تكن متأكدًا من أين تبدأ؟ لست وحدك—معظم المطورين يواجهون نفس العقبة عندما يبدؤون أول مرة باستخدام مكتبات توليد PDF. الخبر السار هو أنه باستخدام Aspose.Pdf يمكنك إنشاء PDF، إضافة صفحة إلى PDF، وحتى رسم أشكال مثل المستطيل دون عناء.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ لا يقوم فقط **creates a PDF document** بل يوضح أيضًا **how to add rectangle PDF** بأمان من خلال تفعيل فحص الحدود العالمي. في النهاية ستحصل على فهم قوي للـ API، وتعرف لماذا كل خطوة مهمة، وسترى النتيجة الدقيقة التي يجب أن تتوقعها.

## ما ستحتاجه

- .NET 6+ (or .NET Framework 4.6+). الكود يعمل بنفس الطريقة على كلاهما.
- حزمة NuGet Aspose.Pdf for .NET (`Aspose.Pdf`) – قم بتثبيتها عبر `dotnet add package Aspose.Pdf`.
- أي محرر C# (Visual Studio، VS Code، Rider… اختر ما يناسبك).

لا يلزم أي تكوين إضافي؛ المكتبة تأتي مع كل ما تحتاجه لبدء توليد ملفات PDF فورًا.

## الخطوة 1: إنشاء مستند PDF وتفعيل فحص الحدود

أول شيء نقوم به هو إنشاء كائن `Document`. فكر فيه كقماش فارغ لمغامرة **create pdf document** الخاصة بك. مباشرةً بعد ذلك نقوم بتفعيل إعداد عالمي يجبر المكتبة على التحقق من أن كل كائن رسومي يبقى داخل مساحة الصفحة. هذا أمر حاسم عندما تحاول لاحقًا رسم أشكال قد تمتد خارج الحدود.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Initialise a new PDF document
using var document = new Document();

// Step 1b: Turn on boundary checking for all graphics objects
document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;
```

*لماذا تفعيل فحص الحدود؟*  
إذا وضعت مستطيلًا عن طريق الخطأ خارج الصفحة، سيقوم Aspose بإلقاء استثناء `PdfException`. التقاط هذا الاستثناء مبكرًا يحفظك من ملفات PDF تالفة يرفض بعض المشاهدين فتحها.

## الخطوة 2: إضافة صفحة إلى PDF

ملف PDF بدون صفحات يشبه كتابًا بلا صفحات—غير مفيد. إضافة صفحة بسيطة كاستدعاء `Pages.Add()`. تُعيد هذه الدالة كائن `Page` ستستخدمه لوضع المحتوى.

```csharp
// Step 2: Add a new page (this is the “add page to pdf” part)
Page page = document.Pages.Add();
```

> **نصيحة احترافية:** حجم الصفحة الافتراضي في Aspose هو 595 × 842 نقطة (A4). إذا كنت بحاجة إلى حجم مختلف، يمكنك ضبط `page.PageInfo.Width` و `page.PageInfo.Height` قبل إضافة المحتوى.

## الخطوة 3: تعريف المستطيل الذي سيكون خارج الحدود

الآن نصل إلى جوهر **how to add rectangle pdf**. نقوم عمدًا بإنشاء مستطيل يتجاوز أبعاد الصفحة لرؤية الاستثناء عمليًا. يأخذ مُنشئ `Rectangle` أربعة معطيات: *X السفلية اليسرى، Y السفلية اليسرى، X العليا اليمنى، Y العليا اليمنى*.

```csharp
// Step 3: Create a rectangle that goes beyond the page edges
// Page size: 595x842, so X=800 and Y=900 are out of bounds
var outOfBoundsRect = new Rectangle(400, 750, 800, 900);
```

إذا شغلت الكود مع إلغاء فحص الحدود، سيُقص المستطيل ببساطة. مع تفعيل الفحص، سيُطلق Aspose خطأً، وهذا ما نريده لتدفقات توليد PDF القوية.

## الخطوة 4: بناء الشكل وإعطائه حدًا مرئيًا

المستطيل بمفرده غير مرئي ما لم تضف حدًا أو تعبئة. هنا نغلف `Rectangle` داخل كائن شكل `Rectangle` (نعم، اسم الفئة قد يسبب بعض الارتباك) ونُعطيه حدًا أسودًا رفيعًا.

```csharp
// Step 4: Turn the rectangle into a shape and add a border
var rectangleShape = new Rectangle(outOfBoundsRect)
{
    Border = new BorderInfo(BorderSide.All, 1f)   // 1‑point black border
};
```

*لماذا حد؟*  
بدون حد لن ترى أي شيء على الصفحة، مما يجعل عملية التصحيح أصعب. الحد الرفيع يجعل من الواضح أيضًا عندما يكون الشكل خارج الحدود.

## الخطوة 5: إضافة الشكل إلى الصفحة – توقع استثناء

الآن نضع الشكل فعليًا على الصفحة. لأن المستطيل يتجاوز حدود الصفحة وقد فعلنا فحص الحدود، سيُطلق Aspose استثناءً `PdfException`. نغلف الاستدعاء داخل كتلة `try/catch` لتوضيح معالجة الأخطاء بأناقة.

```csharp
// Step 5: Attempt to add the shape – this will raise an exception
try
{
    page.Paragraphs.Add(rectangleShape);
}
catch (PdfException ex)
{
    Console.WriteLine("Caught PdfException: " + ex.Message);
    // Handle the error – maybe adjust the rectangle or log the issue
}
```

إذا علق سطر `CheckGraphicsObjectBoundaries` في الخطوة 1، سينجح الكود وسيُقص المستطيل إلى حواف الصفحة. هذا السلوك مفيد للنماذج الأولية السريعة، لكن في الإنتاج عادةً ما تحتاج إلى شبكة الأمان.

## الخطوة 6: حفظ ملف PDF

أخيرًا، نقوم بحفظ المستند على القرص. سيتم إنشاء الملف في المجلد الذي تحدده؛ تأكد من وجود المسار أو استخدم `Path.Combine` مع `Environment.CurrentDirectory`.

```csharp
// Step 6: Save the resulting PDF
string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
document.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

عند فتح `checked_shapes.pdf` سترى صفحة فارغة (لأن المستطيل رُفض). إذا أزلت فحص الحدود، سترى مستطيلًا مرسومًا جزئيًا مقصوصًا عند الحافة اليمنى والعلوية.

---

![مثال إنشاء مستند PDF يُظهر فحص حدود المستطيل](https://example.com/images/checked_shapes.png "مثال إنشاء مستند PDF مع فحص حدود المستطيل")

*اللقطة أعلاه توضح ملف PDF بعد تشغيل الدرس مع إلغاء فحص الحدود (المستطيل مقصوص). مع تفعيل الفحص، يتم حذف الشكل وتُسجل الاستثناء.*

## ملخص: مثال كامل يعمل

بتجميع كل شيء معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise document and enable boundary checking
        using var document = new Document();
        document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;

        // 2️⃣ Add a page (add page to pdf)
        Page page = document.Pages.Add();

        // 3️⃣ Define an out‑of‑bounds rectangle (how to add rectangle pdf)
        var outOfBoundsRect = new Rectangle(400, 750, 800, 900);

        // 4️⃣ Create shape with a visible border
        var rectangleShape = new Rectangle(outOfBoundsRect)
        {
            Border = new BorderInfo(BorderSide.All, 1f)
        };

        // 5️⃣ Try to add the shape – expect an exception
        try
        {
            page.Paragraphs.Add(rectangleShape);
        }
        catch (PdfException ex)
        {
            Console.WriteLine("Caught PdfException: " + ex.Message);
        }

        // 6️⃣ Save the PDF
        string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
        document.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

شغّل البرنامج، وسترى مخرجات وحدة التحكم التي تؤكد ما إذا تم التقاط الاستثناء. افتح ملف PDF المُولد للتحقق من النتيجة.

## أسئلة شائعة وحالات خاصة

- **ماذا لو احتجت إلى حجم صفحة مختلف؟**  
  قم بتعيين `page.PageInfo.Width` و `page.PageInfo.Height` قبل إضافة الأشكال. سيتعامل فاحص الحدود تلقائيًا مع الأبعاد الجديدة.

- **هل يمكنني إلغاء فحص الحدود لشكل واحد فقط؟**  
  ليس مباشرة. الإعداد عالمي، لكن يمكنك إيقافه مؤقتًا، إضافة الشكل، ثم إعادة تشغيله—مع العلم أنك تفقد شبكة الأمان لتلك العملية.

- **هل رسالة الاستثناء مفيدة؟**  
  نعم، يتضمن Aspose إحداثيات العنصر المخالف، بحيث يمكنك تعديل المستطيل برمجيًا أو تسجيل تشخيصات مفصلة.

- **هل سيعمل هذا على .NET Core على لينكس؟**  
  بالتأكيد. Aspose.Pdf مستقل عن المنصة؛ فقط تأكد من توفر ملفات الخطوط التي تشير إليها على نظام التشغيل المستهدف.

## الخطوات التالية

الآن بعد أن عرفت **how to add rectangle pdf** وكيفية **add page to pdf**, قد ترغب في استكشاف:

- إضافة أنواع رسومية أخرى (إهليلجات، خطوط) مع نفس فحص الحدود.
- إدراج نصوص، صور، أو جداول—Aspose يقدم واجهات برمجة تطبيقات غنية لكل منها.
- استخدام overloads لـ `Document.Save` لإخراج مباشرة إلى `MemoryStream` لواجهات برمجة تطبيقات الويب.

لا تتردد في تجربة إحداثيات مستطيلات مختلفة، حدود، وألوان تعبئة. كلما لعبت أكثر، كلما فهمت أفضل كيف يعمل Aspose.P

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}