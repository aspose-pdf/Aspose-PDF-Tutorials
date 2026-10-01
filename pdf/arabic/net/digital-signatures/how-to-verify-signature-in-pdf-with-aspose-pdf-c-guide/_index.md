---
category: general
date: 2026-02-10
description: كيفية التحقق من التوقيع في ملف PDF باستخدام Aspose.Pdf لـ .NET. تعلم
  فحص توقيع PDF، والتحقق من صحة PDF الموقع، واستخراج حالة التوقيع في دقائق.
draft: false
keywords:
- how to verify signature
- check pdf signature
- validate signed pdf
- verify pdf signature
- extract signature status
language: ar
og_description: كيفية التحقق من التوقيع في ملف PDF باستخدام Aspose.Pdf. دليل خطوة
  بخطوة للتحقق من توقيع PDF، التحقق من صحة PDF الموقع، واستخراج حالة التوقيع.
og_title: كيفية التحقق من التوقيع في ملف PDF باستخدام Aspose.Pdf – دليل C#
tags:
- PDF
- C#
- Aspose.Pdf
- Digital Signature
title: كيفية التحقق من التوقيع في ملف PDF باستخدام Aspose.Pdf – دليل C#
url: /ar/net/digital-signatures/how-to-verify-signature-in-pdf-with-aspose-pdf-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التحقق من التوقيع في PDF باستخدام Aspose.Pdf – دليل C# كامل

هل تساءلت يومًا **كيف تتحقق من التوقيع** في ملف PDF استلمته للتو؟ ربما تقوم ببناء خط أنابيب لمعالجة المستندات وتحتاج إلى التأكد بنسبة 100 % أن التوقيع المرفق لم يتم العبث به. في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية **يفحص توقيع PDF**، يتحقق من صحة ملف PDF الموقع، وحتى يستخرج حالة التوقيع باستخدام مكتبة Aspose.Pdf لـ .NET.

بنهاية هذا الدليل ستكون قادرًا على:

* تحميل أي ملف PDF موقع.
* التحقق من أن توقيعًا رقميًا معينًا (مثل *Signature1*) لا يزال سليمًا.
* استرجاع كائن حالة مفصل يوضح لك بالضبط لماذا قد يكون التوقيع غير صالح.
* طباعة النتائج على وحدة التحكم أو تسجيلها لمعالجة إضافية.

> **المتطلبات المسبقة** – ستحتاج إلى .NET 6+ (أو .NET Core 3.1) ورخصة صالحة لـ Aspose.Pdf for .NET أو مفتاح تقييم مؤقت. لا توجد أدوات طرف ثالث أخرى مطلوبة.

هيا نغوص في الإجابة على السؤال الكبير: **كيف تتحقق من التوقيع** في PDF برمجيًا.

![how to verify signature](/images/how-to-verify-signature.png "Illustration of verifying a PDF signature using Aspose.Pdf")

---

## الخطوة 1 – تثبيت Aspose.Pdf وإعداد المشروع الخاص بك

قبل أن نتمكن من **فحص توقيع PDF**، يجب أن نضيف حزمة NuGet الخاصة بـ Aspose.Pdf.

```bash
dotnet add package Aspose.Pdf
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن *Aspose.Pdf* وثبت أحدث نسخة مستقرة (في وقت كتابة هذا الدليل، 23.9).

بعد إضافة الحزمة، أنشئ تطبيقًا جديدًا من نوع Console بلغة C# (أو دمج الشيفرة في الخدمة الحالية). المثال أدناه يفترض وجود مشروع Console اسمه `PdfSignatureVerifier`.

---

## الخطوة 2 – تحميل مستند PDF الموقع

أول شيء نفعله عندما نريد **التحقق من PDF موقع** هو تحميله إلى كائن `Aspose.Pdf.Document`. استخدام جملة `using` يضمن تحرير مقبض الملف بشكل صحيح.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Replace with the actual path to your signed PDF
const string signedPdfPath = @"C:\Docs\signed.pdf";

using var signedDocument = new Document(signedPdfPath);
```

لماذا نستخدم `Document` بدلاً من `PdfFileSignature` مباشرةً؟ `Document` يمنحك وصولًا كاملًا إلى محتوى PDF (الصفحات، البيانات الوصفية، إلخ) مع السماح لواجهة التوقيع بالعمل على نفس الكائن في الذاكرة. هذا النهج فعال من حيث الذاكرة ومؤمن للمستقبل إذا احتجت لاحقًا لاستخراج معلومات أخرى من نفس الملف.

---

## الخطوة 3 – إنشاء مُتحقق التوقيع

الآن نقوم بإنشاء كائن `PdfFileSignature`، وهو الواجهة المسؤولة عن جميع عمليات التوقيع. تمرير الـ `signedDocument` الذي تم تحميله مسبقًا يربط المتحقق بالنسخة الدقيقة من PDF التي فتحناها.

```csharp
using var signatureVerifier = new PdfFileSignature(signedDocument);
```

> **لماذا هذا مهم:** المتحقق يقرأ تجزئات النطاقات (byte‑range hashes) المخزنة داخل PDF ويقارنها بالمحتوى الحالي للملف. إذا تم تعديل الملف بعد التوقيع، سيفشل التحقق.

---

## الخطوة 4 – التحقق من توقيع محدد (How to Verify Signature)

معظم ملفات PDF تحتوي على توقيع واحد، لكن العديد من سير عمل الشركات يدمج توقيعات متعددة (مثل *Signature1*، *Signature2*). للتحقق من **توقيع PDF** لاسم معين، استدعِ `VerifySignature` مع المعرف الدقيق.

```csharp
// The name of the signature you want to verify.
// You can discover available names via signatureVerifier.GetSignatureNames()
const string signatureName = "Signature1";

bool isSignatureIntact = signatureVerifier.VerifySignature(signatureName);
Console.WriteLine($"Signature intact: {isSignatureIntact}");
```

إذا كان `isSignatureIntact` يساوي `true`، فإن التجزئة المشفرة تتطابق ولم يتم تعديل المستند منذ تطبيق التوقيع.

---

## الخطوة 5 – استخراج حالة التوقيع المفصلة (Extract Signature Status)

الإجابة بنعم/لا مفيدة، لكن غالبًا ما تحتاج إلى معرفة *سبب* فشل التحقق. `GetSignatureStatus` تُعيد كائن `SignatureStatus` يحتوي على مجموعة من كائنات `SignatureVerificationResult`، كل واحدة تصف مشكلة معينة (مثل إلغاء الشهادة، مشاكل الطابع الزمني، أو مُوقّع غير معروف).

```csharp
var signatureStatus = signatureVerifier.GetSignatureStatus(signatureName);

// Print a human‑readable summary
Console.WriteLine($"Signature status for \"{signatureName}\":");
foreach (var result in signatureStatus.Results)
{
    Console.WriteLine($"- {result.Status}: {result.Message}");
}
```

الناتج النموذجي يكون كالتالي:

```
Signature status for "Signature1":
- Valid: The signature is valid and the document has not been altered.
```

أو إذا كان هناك شيء غير صحيح:

```
Signature status for "Signature1":
- Invalid: The document has been modified after signing.
- Warning: Signer's certificate is not trusted.
```

امتلاك هذه المعلومات التفصيلية أمر أساسي عندما **تتحقق من PDF موقع** في بيئات ذات متطلبات امتثال عالية (المالية، القانونية، الرعاية الصحية).

---

## الخطوة 6 – مثال كامل يعمل (جميع الخطوات معًا)

فيما يلي برنامج مستقل يمكنك نسخه ولصقه في `Program.cs`. يوضح **كيفية التحقق من التوقيع**، **فحص توقيع PDF**، **التحقق من PDF موقع**، و**استخراج حالة التوقيع** في خطوة واحدة.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace PdfSignatureVerifier
{
    class Program
    {
        static void Main()
        {
            // ---------------------------------------------------------
            // Step 1 – Load the signed PDF document
            // ---------------------------------------------------------
            const string pdfPath = @"C:\Docs\signed.pdf";
            using var signedDoc = new Document(pdfPath);

            // ---------------------------------------------------------
            // Step 2 – Create the signature verifier façade
            // ---------------------------------------------------------
            using var verifier = new PdfFileSignature(signedDoc);

            // ---------------------------------------------------------
            // Step 3 – Choose the signature name you want to verify
            // ---------------------------------------------------------
            const string sigName = "Signature1";

            // ---------------------------------------------------------
            // Step 4 – Verify the signature integrity (how to verify signature)
            // ---------------------------------------------------------
            bool intact = verifier.VerifySignature(sigName);
            Console.WriteLine($"Signature intact: {intact}");

            // ---------------------------------------------------------
            // Step 5 – Retrieve and display detailed status (extract signature status)
            // ---------------------------------------------------------
            var status = verifier.GetSignatureStatus(sigName);
            Console.WriteLine($"Signature status for \"{sigName}\":");
            foreach (var result in status.Results)
            {
                Console.WriteLine($"- {result.Status}: {result.Message}");
            }

            // ---------------------------------------------------------
            // Optional: List all signatures present in the document
            // ---------------------------------------------------------
            Console.WriteLine("\nAll signatures found:");
            foreach (var name in verifier.GetSignatureNames())
            {
                Console.WriteLine($"* {name}");
            }
        }
    }
}
```

**الناتج المتوقع على وحدة التحكم (توقيع صالح):**

```
Signature intact: True
Signature status for "Signature1":
- Valid: The signature is valid and the document has not been altered.

All signatures found:
* Signature1
```

إذا تم العبث بالمستند، ستكون قيمة `Signature intact` `False` وستحتوي قائمة الحالة على إدخال أو أكثر من نوع `Invalid`.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو لم أكن أعرف اسم التوقيع؟

`PdfFileSignature.GetSignatureNames()` تُعيد مجموعة من السلاسل تحتوي على جميع معرفات التوقيع. يمكنك تعدادها والسماح للمستخدم باختيار أحدها، أو ببساطة التحقق من كلٍ منها داخل حلقة.

```csharp
foreach (var name in verifier.GetSignatureNames())
{
    bool ok = verifier.VerifySignature(name);
    Console.WriteLine($"{name}: {(ok ? "Valid" : "Invalid")}");
}
```

### هل يمكنني التحقق من التوقيعات بدون رخصة؟

Aspose.Pdf يعمل في وضع التقييم، لكن المخرجات ستحتوي على علامة مائية وبعض الميزات المتقدمة (مثل التحقق المفصل من الشهادة) قد تكون محدودة. للاستخدام الإنتاجي، احصل على رخصة صحيحة لتجنب هذه القيود.

### كيف أتعامل مع الشهادات غير الموثوقة؟

كائنات `SignatureVerificationResult` تتضمن حقل `Status` (`Valid`, `Invalid`, `Warning`). إذا حصلت على تحذير بخصوص شهادة غير موثوقة، يمكنك تزويد المتحقق بمجموعة مخصصة من `X509Certificate2` عبر `PdfFileSignature.SetTrustedCertificates()`.

### هل يعمل هذا مع ملفات PDF/A أو PDF/X؟

نعم. Aspose.Pdf يتعامل مع PDF/A، PDF/X، وPDF العادي بنفس الطريقة عند التحقق من التوقيع. الاختلاف الوحيد هو أن PDF/A قد يضم بيانات وصفية إضافية، لكنها لا تؤثر على عملية التحقق المشفر.

---

## الخلاصة

لقد غطينا الآن **كيفية التحقق من التوقيع** في PDF باستخدام Aspose.Pdf لـ .NET، عرضنا طريقة نظيفة **لفحص توقيع PDF**، شرحنا **كيفية التحقق من PDF موقع**، وكشفنا كيفية **استخراج حالة التوقيع** لتشخيص أعمق. الشيفرة القابلة للتنفيذ أعلاه يمكن دمجها مباشرة في أي خدمة C# تحتاج إلى فرض سلامة المستندات.

الخطوات التالية قد تشمل:

* **أتمتة التحقق الجماعي** – تكرار عبر مجلد من ملفات PDF وإنشاء تقرير CSV.
* **دمج مع مخزن الشهادات** – سحب شهادات الجذر الموثوقة من Windows أو Azure Key Vault.
* **إضافة التحقق من الطابع الزمني** – التأكد من أن طابع توقيع الوقت لا يزال ضمن فترة صلاحية الشهادة.

لا تتردد في التجربة، تعديل المقاطع، ومشاركة ما توصلت إليه. برمجة سعيدة، ولتظل ملفات PDF الخاصة بك خالية من العبث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}