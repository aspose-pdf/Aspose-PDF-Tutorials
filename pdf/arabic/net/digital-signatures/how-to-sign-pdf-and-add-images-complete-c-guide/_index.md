---
category: general
date: 2026-03-29
description: كيفية توقيع ملف PDF بتوقيع رقمي وإضافة صورة مقصوصة في C#. تعلم كيفية
  إضافة توقيع رقمي إلى PDF، قص الصورة للـ PDF، وإضافة صورة إلى PDF بسهولة.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: ar
og_description: كيفية توقيع ملف PDF باستخدام توقيع رقمي وإدراج صورة مقصوصة باستخدام
  Aspose.Pdf في C#. اتبع هذا الدليل للحصول على حل كامل.
og_title: كيفية توقيع ملفات PDF وإضافة الصور – دليل C# خطوة بخطوة
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: كيفية توقيع ملفات PDF وإضافة الصور – دليل C# الكامل
url: /ar/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية توقيع ملفات PDF وإضافة الصور – دليل C# كامل

هل تساءلت يومًا **كيفية توقيع ملفات PDF** برمجيًا مع إدراج صورة مخصصة؟ ربما تقوم ببناء سير عمل للموافقة وتحتاج إلى توقيع قانونيًا ملزم *و* صورة مصغرة لصورة الموقع على نفس الصفحة. باختصار، تريد **إضافة توقيع رقمي pdf**، قص تلك الصورة، ثم **إضافة صورة إلى pdf** دون عناء.  

هذا الدليل يشرح لك كل خطوة — من تحميل شهادة ECDSA PKCS#7 إلى قص صورة JPEG ووضعها على الصفحة الموقعة. في النهاية ستحصل على ملف C# واحد قابل للتنفيذ يوقع الصفحة 1، يقص صورة إلى 400 × 400 بكسل، ويضعها في موقع دقيق. لا سكريبتات خارجية، لا سحر، فقط كود واضح وتفسيرات.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
- **Aspose.Pdf for .NET** حزمة NuGet (الإصدار 23.9 أو أحدث)
- شهادة ECDSA P‑256 بصيغة PKCS#7 (`.pfx`) وكلمة المرور الخاصة بها
- صورة JPEG تريد تضمينها (مثال: `photo.jpg`)

> **نصيحة احترافية:** احتفظ بملف الشهادة خارج نظام التحكم في المصدر واحمِ كلمة المرور باستخدام مدير أسرار.

---

## الخطوة 1: إعداد المشروع والاستيرادات

أولاً، أنشئ تطبيقًا سطريًا (أو دمجه في أي خدمة موجودة). أضف مرجع Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

ثم قم بتضمين المساحات الاسمية المطلوبة:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

تمنحك هذه التعليمات `using` إمكانية الوصول إلى الفئات `Document` و `Signature` و `Rectangle` التي سنحتاجها لاحقًا.

## الخطوة 2: تحميل ملف PDF وتحضير التوقيع

سنفتح ملف PDF موجود (`source.pdf`) وننشئ كائن **digital signature pdf** يستخدم توقيع PKCS#7 منفصل. الشهادة هي مفتاح ECDSA P‑256، وهو مقبول على نطاق واسع للامتثال.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**لماذا هذا مهم:** استخدام توقيع PKCS#7 منفصل يحافظ على محتوى PDF الأصلي دون تعديل بينما يدمج تجزئة تشفيرية. هذا هو النهج القياسي في الصناعة للملفات PDF القانونية.

## الخطوة 3: تطبيق التوقيع الرقمي على صفحة محددة

الآن سنضع حقل التوقيع المرئي على **page 1**. المستطيل يحدد مكان ظهور صندوق التوقيع (الإحداثيات بوحدات النقاط، حيث 1 inch = 72 points).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

إذا لم تحتاج إلى صندوق مرئي، اضبط `isVisible` إلى `false`. يمكن تعديل `signatureRect` ليتناسب مع تخطيط المستند الخاص بك.

## الخطوة 4: فتح تدفق الصورة وتحديد مناطق القص

سنقرأ ملف JPEG إلى تدفق ونحدد **source rectangle** يختار الجزء العلوي‑الأيسر 400 × 400 بكسل. هذه هي عملية **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **حالة حافة:** إذا كانت صورتك أصغر من 400 × 400، سيقوم القص تلقائيًا بالتحجيم إلى أبعاد الصورة الفعلية — لا يُرمى استثناء.

## الخطوة 5: تحديد مكان ظهور الصورة المقصوصة

بعد ذلك، عيّن **destination rectangle** على صفحة PDF. في هذا المثال نضع الصورة عند (50, 50) بحجم 200 × 200 points (≈2.78 بوصة مربع).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

لا تتردد في التجربة: غيّر إحداثيات X/Y لتحريك الصورة، أو عدّل العرض/الارتفاع للتكبير أو التصغير.

## الخطوة 6: إدراج الصورة المقصوصة على الصفحة الموقعة

أخيرًا، نضيف الصورة إلى **page 1** (نفس الصفحة التي تحمل الآن التوقيع). التحميل الزائد `AddImage` الذي نستخدمه يقبل المستطيلات المصدر والوجهة، مما يؤدي إلى تنفيذ القص والموضع في نداء واحد.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

خلف الكواليس، تقوم Aspose.Pdf باستخراج المنطقة 400 × 400 بكسل، وتعيد تحجيمها إلى 200 × 200 points، وتكتبها في تدفق محتوى PDF.

## الخطوة 7: حفظ ملف PDF الموقّع والمُعزز بالصورة

بعد جميع التعديلات، احفظ المستند. يمكنك استبدال الملف الأصلي أو الكتابة إلى ملف جديد.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

عند فتح `output_signed.pdf` في Adobe Acrobat أو أي عارض PDF، ستلاحظ:

- حقل توقيع مرئي عند الإحداثيات التي حددتها.
- الصورة المقصوصة موضوعة عند (50, 50) على الصفحة 1.
- التوقيع الرقمي مُتحقق (بشرط أن يثق العارض بشهادتك).

## الأسئلة المتكررة (FAQ)

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني توقيع صفحة مختلفة؟** | غيّر قيمة `pageNumber` في `signature.Sign` إلى أي فهرس صفحة صالح (مبني على 1). |
| **ماذا لو احتجت إلى توقيعات متعددة؟** | أنشئ كائن `Signature` جديد لكل صفحة أو موقع، مع إعادة استخدام `pkcsSignature` إذا كانت الشهادة نفسها مطبقة. |
| **هل يقتصر قص الصورة على المستطيلات فقط؟** | نعم، `AddImage` في Aspose.Pdf يعمل مع مناطق مستطيلة. للأشكال المعقدة تحتاج إلى معالجة مسبقة للصورة (مثلاً باستخدام System.Drawing) قبل الإدراج. |
| **كيف أجعل التوقيع غير مرئي؟** | اضبط `isVisible` إلى `false` وتجاهل `signatureRect`. سيظل التوقيع صالحًا تشفيريًا. |
| **ما الصيغ التي يمكنني تضمينها غير JPEG؟** | تدعم PNG, BMP, GIF, و TIFF. فقط غيّر مسار الملف وتأكد من أن التدفق يقرأ البايتات الصحيحة. |

## مثال كامل يعمل

فيما يلي البرنامج الكامل المتكامل. انسخه إلى `Program.cs`، عدّل المسارات، ثم شغّله.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**النتيجة المتوقعة:** فتح `output_signed.pdf` يُظهر حقل توقيع (100 × 100 → 300 × 300 points) وصورة بحجم 200 × 200 point مأخوذة من الزاوية العلوية‑اليسرى لـ `photo.jpg`. التوقيع يُتحقق مقابل شهادة ECDSA المقدمة.

## الخاتمة

لقد غطينا **كيفية توقيع ملفات PDF**، وكيفية **إضافة توقيع رقمي pdf** إلى صفحة محددة، وكيفية **قص صورة للـ pdf**، وأخيرًا **إضافة صورة إلى pdf** باستخدام Aspose.Pdf في C#. تدفق العمل الكامل — من تحميل الشهادة إلى حفظ المستند النهائي — يتضمن ملف مصدر واحد سهل القراءة.

إذا كنت مستعدًا للتحدي التالي، فكر في:

- إضافة **توقيعات متعددة** على صفحات مختلفة (استخدم مفهوم “digital signature pdf page”).
- تضمين **رموز QR** ترتبط بخدمات التحقق.
- أتمتة العملية في API ASP.NET Core لإنشاء PDF في الوقت الفعلي.

تذكر، المفتاح لأتمتة PDF قوية هو الفصل الواضح بين المهام: معالجة التوقيع، معالجة الصورة، وتجميع المستند النهائي. العب بالإحداثيات، بدّل صيغة الصورة، أو جرّب إضافة طوابع زمنية — سير عملك الآن قابل للتوسيع بالكامل.

هل لديك أسئلة، أو سيناريوهات حافة، أو حالة استخدام مميزة تريد مشاركتها؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}