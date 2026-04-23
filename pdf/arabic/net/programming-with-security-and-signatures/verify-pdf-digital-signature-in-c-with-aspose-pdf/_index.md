---
category: general
date: 2026-03-24
description: تعلم كيفية التحقق من التوقيع الرقمي لملف PDF باستخدام Aspose.Pdf للغة
  C#. كما يمكنك معرفة كيفية سرد التوقيعات والتحقق من صحة توقيع PDF في بضع خطوات سهلة.
draft: false
keywords:
- verify pdf digital signature
- how to verify signature
- check pdf signature validity
- how to list signatures
language: ar
og_description: تحقق من التوقيع الرقمي لملف PDF باستخدام C# و Aspose.Pdf. اتبع هذا
  الدليل خطوة بخطوة لعرض التوقيعات والتحقق من صحة توقيع PDF.
og_title: تحقق من التوقيع الرقمي لملف PDF في C# – دليل شامل
tags:
- Aspose.Pdf
- C#
- Digital Signature
title: التحقق من التوقيع الرقمي لملف PDF باستخدام C# و Aspose.Pdf
url: /ar/net/programming-with-security-and-signatures/verify-pdf-digital-signature-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التحقق من التوقيع الرقمي للملف PDF باستخدام C# – دليل شامل

هل احتجت يومًا إلى **التحقق من التوقيع الرقمي للملف PDF** لكن لم تعرف من أين تبدأ؟ لست وحدك؛ يواجه العديد من المطورين هذه المشكلة عند التعامل مع ملفات PDF الموقعة في سير العمل الآلي. الخبر السار؟ باستخدام Aspose.Pdf for .NET يمكنك سرد كل توقيع في المستند والتحقق من صحته ببضع أسطر من الشيفرة فقط.  

في هذا الدرس سنستعرض العملية بالكامل — من تحميل ملف PDF الموقّع، تعداد توقيعاته، وحتى التحقق من كل توقيع وتفسير النتائج. في النهاية لن تعرف فقط **كيفية التحقق من التوقيع** برمجيًا، بل ستفهم أيضًا **كيفية سرد التوقيعات** و**التحقق من صحة توقيع PDF** في سيناريوهات خاصة مثل الملفات غير الموقعة أو ملفات PDF المحمية بكلمة مرور.

## ما ستتعلمه

- كيفية تحميل ملف PDF يحتوي على توقيع أو أكثر.  
- استدعاءات API الدقيقة اللازمة لـ **سرد التوقيعات** باستخدام `PdfFileSignature.GetSignNames()`.  
- كيفية استدعاء `VerifySignature` وقراءة بيانات `SignatureInfo` التفصيلية، بما في ذلك أسباب الفشل.  
- نصائح للتعامل مع توقيعات متعددة، ملفات PDF غير موقعة، ومستندات مشفرة.  
- عينة شيفرة جاهزة للتنفيذ يمكنك إدراجها في أي مشروع .NET.

> **المتطلبات المسبقة** – تحتاج إلى .NET 6+ (أو .NET Framework 4.7.2+) ورخصة صالحة لـ Aspose.Pdf for .NET (أو مفتاح تقييم مؤقت). لا توجد مكتبات طرف ثالث أخرى مطلوبة.

---

## الخطوة 1: تثبيت Aspose.Pdf وإعداد المشروع  

أولاً، أضف حزمة Aspose.Pdf إلى مشروعك. إذا كنت تستخدم .NET CLI، نفّذ الأمر:

```bash
dotnet add package Aspose.Pdf
```

أو، من مدير الحزم NuGet في Visual Studio، ابحث عن **Aspose.Pdf** وانقر *Install*.  

> **نصيحة احترافية:** حافظ على تحديث الحزمة. حتى مارس 2026 الإصدار المستقر الأخير هو **23.11**، والذي يتضمن تحسينات أداء لمعالجة التوقيعات.

---

## الخطوة 2: تحميل ملف PDF الموقّع  

الآن سنفتح ملف PDF الذي تريد فحصه. تمثل فئة `Document` الملف بالكامل، وسنمرّر مسار الملف إلى مُنشئها.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Replace with the actual path to your signed PDF
string pdfPath = @"C:\Docs\signed.pdf";

using var pdfDocument = new Document(pdfPath);
```

> **لماذا هذا مهم:** تحميل المستند داخل كتلة `using` يضمن تحرير مقبض الملف بسرعة، مما يمنع مشاكل قفل الملف في الخدمات طويلة التشغيل.

---

## الخطوة 3: إنشاء كائن PdfFileSignature  

`PdfFileSignature` هو البوابة لجميع عمليات التوقيع. يحتاج إلى نسخة `Document` التي أنشأناها للتو.

```csharp
// Step 3: Initialize the signature helper
var pdfSignature = new PdfFileSignature(pdfDocument);
```

فكر في `PdfFileSignature` كصندوق أدوات متخصص يعرف كيف يقرأ، يتحقق، ويتعامل مع التوقيعات الرقمية المدمجة في PDF.

---

## الخطوة 4: سرد جميع أسماء التوقيعات  

يمكن أن يحتوي PDF على عدة توقيعات، كل منها يُعرّف باسم فريد. لـ **كيفية سرد التوقيعات**، استدعِ `GetSignNames()` وتكرّر على النتيجة.

```csharp
// Step 4: Retrieve every signature name in the document
IEnumerable<string> signatureNames = pdfSignature.GetSignNames();

Console.WriteLine("Found signatures:");
foreach (var name in signatureNames)
{
    Console.WriteLine($"- {name}");
}
```

إذا لم يحتوي PDF على توقيعات، تُعيد `GetSignNames()` مجموعة فارغة — وهذا مثالي للتعامل مع حالة “عدم وجود توقيع” بأناقة.

---

## الخطوة 5: التحقق من كل توقيع واستخراج التفاصيل  

هذا هو جوهر الدرس: **التحقق من صحة توقيع PDF** لكل اسم قمنا بسرده للتو. تُعيد طريقة `VerifySignature` قيمة منطقية تشير إلى الصلاحية وتملأ معاملًا خارجيًا (`out`) كائنًا من نوع `SignatureDetails`.

```csharp
// Step 5: Verify each signature and print detailed info
foreach (var signatureName in signatureNames)
{
    // Verify the signature; the method also outputs detailed info
    bool isValid = pdfSignature.VerifySignature(signatureName, out var signatureDetails);

    // Optional: grab the compromise reason if the signature is invalid
    string compromiseReason = signatureDetails?.SignatureInfo?.CompromiseReason ?? "None";

    Console.WriteLine(
        $"Signature '{signatureName}' valid: {isValid}, Compromise Reason: {compromiseReason}");
}
```

### ما معنى المخرجات  

- **`isValid`** – `true` إذا نجحت الفحوصات التشفيرية وكانت سلسلة الشهادات موثوقة (حسب مخزن النظام الافتراضي).  
- **`CompromiseReason`** – يُملأ فقط عندما يفشل التوقيع؛ القيم الشائعة تشمل *“Certificate revoked”* أو *“Hash mismatch”*.  

إذا احتجت إلى مزيد من التفاصيل — مثل فحص شهادة التوقيع، الطابع الزمني، أو وقت التوقيع — فإن `signatureDetails.SignatureInfo` يحتوي على تلك الحقول.

---

## الخطوة 6: معالجة حالات الحافة الشائعة  

### 6.1 عدم العثور على توقيعات  

```csharp
if (!signatureNames.Any())
{
    Console.WriteLine("The PDF does not contain any digital signatures.");
    // You might decide to abort or continue with unsigned‑PDF logic here.
}
```

### 6.2 ملفات PDF محمية بكلمة مرور  

إذا كان PDF مشفرًا، حمّله أولًا باستخدام كلمة المرور:

```csharp
var loadOptions = new LoadOptions { Password = "yourPassword" };
using var protectedDoc = new Document(pdfPath, loadOptions);
var protectedSignature = new PdfFileSignature(protectedDoc);
```

### 6.3 توقيعات متعددة بحالات تحقق مختلفة  

من الممكن أن يكون توقيع واحد صالحًا بينما آخر غير صالح (مثلاً تم تعديل توقيع أقدم لاحقًا). التكرار عبر جميع الأسماء، كما هو موضح في الخطوة 5، يضمن اكتشاف كل حالة.

---

## الخطوة 7: مثال كامل يعمل  

فيما يلي تطبيق console مكتمل يمكنك تجميعه وتشغيله فورًا. استبدل `pdfPath` بمسار ملف PDF الموقّع لديك.

```csharp
// ------------------------------------------------------------
// Verify PDF Digital Signature – Complete Console Sample
// ------------------------------------------------------------
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF (add password here if needed)
        string pdfPath = @"C:\Docs\signed.pdf";
        using var doc = new Document(pdfPath);

        // 2️⃣ Create the signature helper
        var signatureHelper = new PdfFileSignature(doc);

        // 3️⃣ Get all signature names
        IEnumerable<string> names = signatureHelper.GetSignNames();

        // 4️⃣ If none, inform the user
        if (!names.Any())
        {
            Console.WriteLine("No digital signatures detected in the PDF.");
            return;
        }

        // 5️⃣ Verify each signature
        foreach (var name in names)
        {
            bool valid = signatureHelper.VerifySignature(name, out var details);
            string reason = details?.SignatureInfo?.CompromiseReason ?? "None";

            Console.WriteLine(
                $"Signature '{name}' valid: {valid}, Compromise Reason: {reason}");
        }
    }
}
```

**الناتج المتوقع في وحدة التحكم (مثال):**

```
Signature 'Signature1' valid: True, Compromise Reason: None
Signature 'Signature2' valid: False, Compromise Reason: Certificate revoked
```

إذا كان PDF غير موقّع، ستظهر رسالة “No digital signatures detected”.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات PDF موقعة باستخدام Adobe Acrobat؟**  
ج: بالتأكيد. يتبع Aspose.Pdf مواصفة PDF 1.7، لذا أي توقيع متوافق مع المعيار — بما في ذلك تلك التي تُنشئها Adobe — سيتم التعرف عليه.

**س: هل يمكنني التحقق من توقيع مقابل مخزن ثقة مخصص؟**  
ج: نعم. استخدم `PdfFileSignature.SetTrustedCertificates()` قبل استدعاء `VerifySignature`. مرّر مجموعة من كائنات `X509Certificate2` التي تمثل الجذور الموثوقة لديك.

**س: ماذا لو أردت تجاهل التحقق من الطابع الزمني؟**  
ج: عيّن `SignatureVerificationOptions.IgnoreTimestamp = true` على كائن `PdfFileSignature`.

**س: هل هناك طريقة لاستخراج عنوان البريد الإلكتروني للموقّع؟**  
ج: الخاصية `SignatureInfo.SignerInfo.Email` تحتفظ بهذه البيانات، بشرط أن تشمل شهادة الموقّع هذا الحقل.

---

## الخلاصة  

أصبح لديك الآن وصفة كاملة وجاهزة للإنتاج لـ **التحقق من التوقيع الرقمي للملف PDF** باستخدام Aspose.Pdf في C#. باتباع الخطوات السبع أعلاه، يمكنك **سرد التوقيعات**، **التحقق من صحة توقيع PDF**، ومعالجة التوقيعات المتعددة أو الغائبة بأناقة.  

في المراحل القادمة، قد تستكشف **كيفية التحقق من التوقيع** مقابل بنية PKI داخل مؤسستك، أو تغوص في **كيفية سرد التوقيعات** في خدمة معالجة دفعات تفحص مئات ملفات PDF كل ليلة. أياً كان الاتجاه، فإن المفاهيم الأساسية التي تعلمتها الآن ستشكل قاعدة صلبة لك.

هل لديك أسئلة إضافية أو تريد مشاركة حالة استخدام مميزة؟ اترك تعليقًا أدناه أو تواصل معي عبر Git

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}