---
category: general
date: 2026-02-09
description: تحقق من توقيع PDF باستخدام Aspose.PDF في C#. تعلم كيفية إضافة مستطيل
  إلى PDF، حفظ PDF المحدث، واستخدام ميزات توقيع Aspose PDF.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: ar
og_description: تحقق من توقيع PDF في C# بسرعة. يوضح هذا الدليل كيفية إضافة رسومات
  إلى PDF، حفظ PDF المحدث، واستخدام واجهات برمجة تطبيقات توقيع Aspose PDF.
og_title: تحقق من توقيع PDF وإضافة مستطيل إلى PDF – دليل Aspose الكامل
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: تحقق من توقيع PDF وإضافة مستطيل إلى PDF باستخدام Aspose
url: /ar/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التحقق من توقيع PDF وإضافة مستطيل PDF باستخدام Aspose

هل احتجت يومًا إلى **تحقق من توقيع PDF** في مشروع C# لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—التوقيعات الرقمية ضرورية للامتثال، ومع ذلك يواجه العديد من المطورين صعوبات عندما يحتاجون إلى تعديل المستند بعد ذلك.  

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ ي **يتحقق من توقيع PDF**، يضيف **مستطيلًا** إلى الصفحة الأولى، يتحقق من أن الشكل يبقى داخل حدود الصفحة، وأخيرًا **يحفظ PDF محدثًا**—كل ذلك باستخدام واجهة برمجة التطبيقات الحديثة Aspose.PDF. في النهاية ستحصل على برنامج واحد مستقل يمكنك إدراجه في أي حل .NET.

## ما ستتعلمه

- تحميل PDF موقّع باستخدام Aspose.PDF.
- استخدام فئات **aspose pdf signature** للتحقق من كل توقيع واكتشاف الاختراقات.
- **إضافة مستطيل PDF** بأمان، مع ضمان ملاءمته للصفحة.
- **حفظ PDF محدث** مع الحفاظ على التوقيعات الموجودة.
- نصائح، معالجة الحالات الحدية، والمشكلات الشائعة.

لا توجد مستندات خارجية مطلوبة—كل ما تحتاجه موجود هنا.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).
- حزمة Aspose.PDF for .NET من NuGet (≥ 23.10). تثبيت باستخدام:

```bash
dotnet add package Aspose.Pdf
```

- ملف PDF موقّع باسم `signed.pdf` موجود في مجلد تتحكم فيه (استبدل `YOUR_DIRECTORY` في الكود).
- إلمام أساسي بـ C# و Visual Studio أو VS Code.

> **نصيحة احترافية:** إذا لم يكن لديك PDF موقّع جاهز، توفر Aspose ملفًا تجريبيًا مجانيًا على موقعهم يمكنك تنزيله للاختبار.

---

## التحقق من توقيع PDF – خطوة بخطوة

أول شيء نحتاج إلى القيام به هو فتح المستند والتكرار عبر كل توقيع رقمي. توفر Aspose.PDF طريقتين مفيدتين: `VerifySignature` تخبرك ما إذا كان الفحص التشفيري قد نجح، بينما `IsSignatureCompromised` الأحدث يحدد أي تعديل قد حدث بعد التوقيع.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**لماذا هذا مهم:**  
- `VerifySignature` بمفردها تؤكد فقط أن شهادة الموقّع لا تزال موثوقة.  
- `IsSignatureCompromised` يكتشف التغييرات الدقيقة—مثل إضافة كائن مخفي—حتى تعرف ما إذا تم تعديل المحتوى المرئي للـ PDF بعد التوقيع.

**الناتج المتوقع** (مثال مع توقيعين):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

إذا أبلغ أي توقيع عن `compromised=True`، يجب إيقاف المعالجة الإضافية أو تنبيه المستخدم، لأن سلامة المستند لا يمكن ضمانها.

---

## إضافة مستطيل PDF إلى صفحة

الآن بعد أن تأكدنا من أن التوقيعات سليمة (أو على الأقل على علم بأي اختراق)، دعنا نضيف رسمًا بسيطًا لمستطيل. هذا مفيد لوضع علامات “مراجعة”، تسليط الضوء على أقسام، أو مجرد جذب الانتباه إلى منطقة.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**ما معنى الأرقام:**  
- نظام إحداثيات PDF يبدأ من الزاوية السفلية اليسرى.  
- في المثال، يمتد المستطيل 100 نقطة أفقيًا و100 نقطة عموديًا، موضعه تقريبًا في وسط صفحة A4 النموذجية.

> **ملاحظة:** تدعم Aspose أيضًا `AddEllipse`، `AddPolygon`، إلخ، إذا كنت بحاجة إلى أشكال أكثر تعقيدًا.

---

## التحقق من حدود الرسومات – ضمان ملاءمة المستطيل

قبل تطبيق التغييرات، من الحكمة التحقق من أن رسوماتنا تبقى داخل مساحة الطباعة للصفحة. طريقة `CheckGraphicsBounds` الجديدة تقوم بذلك بالضبط.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

إذا أعادت `shapeFits` القيمة `false`، ستحتاج إلى تعديل إحداثيات المستطيل—ربما تصغيره أو تحريكه إلى أسفل الصفحة. هذا يمنع القطع العرضي الذي قد يبدو غير مهني، خاصةً عندما يُطبع الـ PDF لاحقًا.

---

## حفظ PDF محدث – الحفاظ على التوقيعات والرسومات الجديدة

أخيرًا، نكتب المستند المعدل مرة أخرى إلى القرص. طريقة `Save` تحترم التوقيعات الموجودة؛ لن تُبطلها إلا إذا تغير المحتوى فعليًا (وهو ما تحققنا منه بالفعل باستخدام `IsSignatureCompromised`).

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**لماذا استخدام ملف جديد؟**  
حفظ الملف فوق الأصلي قد يمحو التوقيعات الأصلية، مما يجعل من المستحيل مقارنة الحالة قبل/بعد. بكتابة إلى `output.pdf` تحتفظ بالمصدر لأغراض التدقيق.

---

## مثال كامل وقابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق كونسول. جميع الخطوات مدمجة، التعليقات تشرح كل جزء، وسترى الناتج المتوقع في وحدة التحكم في النهاية.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**الناتج المتوقع في وحدة التحكم** (بافتراض توقيع واحد صالح وغير مخترق):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

إذا كان التوقيع مخترقًا، سترى `compromised=True` ويمكنك اتخاذ قرار بالاستمرار أم لا.

---

## أسئلة شائعة ومعالجة الحالات الحدية

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كان PDF لا يحتوي على توقيعات؟** | `GetSignNames()` تُعيد مجموعة فارغة؛ الحلقة تتخطى ببساطة، ولا يزال بإمكانك إضافة الرسومات. |
| **هل يمكنني إضافة عدة مستطيلات؟** | نعم—فقط استدعِ `AddRectangle` بشكل متكرر مع كائنات `Rectangle` مختلفة. |
| **ماذا عن ملفات PDF المحمية بكلمة مرور؟** | حمّلها باستخدام `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` قبل التحقق. |
| **هل سيؤدي إضافة رسومات إلى إبطال توقيع صالح؟** | فقط إذا كان التوقيع يغطي الصفحة التي تُدخل فيها الرسومات. استخدم `IsSignatureCompromised` لاكتشاف ذلك؛ وإلا يبقى التوقيع سليمًا. |
| **هل أحتاج إلى إغلاق الموارد؟** | كائنات Aspose.PDF مُدارة؛ الإغلاق اختياري لكن يمكنك وضع الكود داخل كتلة `using` لمزيد من الأمان. |

---

## نصائح احترافية للاستخدام في الإنتاج

- **معالجة دفعات:** غلف الروتين بالكامل في طريقة تقبل مسارات الإدخال/الإخراج؛ ثم زوّد قائمة من الملفات إلى `Parallel.ForEach` للسرعة.
- **التسجيل (Logging):** استبدل `Console.WriteLine` بمسجل مناسب (مثل Serilog) لالتقاط نتائج التحقق في سجلات التدقيق.
- **سياسة التوقيع:** اجمع بين `VerifySignature` وفحص إبطال الشهادة (OCSP/CRL) للحصول على امتثال أكثر صرامة.
- **تنسيق الرسومات:** استخدم `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });` لجعل المستطيل بارزًا.
- **قفل الإصدار:** ثبّت نسخة Aspose.PDF في NuGet لتجنب التغييرات المكسرة عند تحديث المكتبة.

---

## الخلاصة

أنت الآن تمتلك مثالًا قويًا وشاملًا ي **يتحقق من توقيع PDF**، ي **يضيف مستطيل PDF**، و ي **يحفظ PDF محدث** باستخدام أحدث واجهات Aspose.PDF. يتحقق الكود من وجود توقيعات مخترقة، يضمن بقاء الرسومات داخل حدود الصفحة، ويحافظ على التوقيعات الرقمية الأصلية—بالضبط ما يتطلبه سير عمل الامتثال في العالم الحقيقي.

بعد ذلك، قد ترغب في استكشاف:

- إضافة **رسومات PDF** مثل العلامات المائية أو رموز QR.
- استخدام واجهة **aspose pdf signature** لإنشاء توقيعات جديدة برمجيًا.
- أتمتة العملية في خدمة ويب ASP.NET Core للتحقق من المستندات في الوقت الفعلي.

جرّبه، عدّل إحداثيات المستطيل، وشاهد كيف تتفاعل المكتبة مع هياكل PDF المختلفة. برمجة سعيدة، ولتظل ملفات PDF الخاصة بك موقعة وأنيقة! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}