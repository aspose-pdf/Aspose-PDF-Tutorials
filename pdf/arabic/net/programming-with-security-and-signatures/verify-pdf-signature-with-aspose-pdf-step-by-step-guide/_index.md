---
category: general
date: 2026-02-28
description: تحقق من توقيع PDF في C# باستخدام Aspose.Pdf – دليل سريع حول كيفية التحقق
  من صحة التوقيع وفحص سلامة التوقيع.
draft: false
keywords:
- verify pdf signature
- how to validate signature
- how to check signature
- validate digital pdf signature
language: ar
og_description: تحقق من توقيع PDF باستخدام C# و Aspose.Pdf. تعلم كيفية التحقق من صحة
  التوقيع، وفحص حالة التوقيع، والتعامل مع ملفات PDF المخترقة.
og_title: تحقق من توقيع PDF باستخدام Aspose.Pdf – الدليل الكامل
tags:
- Aspose.Pdf
- C#
- Digital Signature
title: تحقق من توقيع PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/programming-with-security-and-signatures/verify-pdf-signature-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحقق من توقيع PDF – دليل برمجة كامل

هل احتجت يومًا إلى **تحقق من توقيع PDF** لكنك لم تكن متأكدًا من أي استدعاء API يخبرك فعليًا ما إذا كان التوقيع لا يزال موثوقًا؟ لست وحدك. في العديد من سير عمل المؤسسات يكون ملف PDF الموقع هو الخطوة النهائية، ويمكن لتوقيع مكسور أن يوقف العملية بأكملها.  

في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية يوضح **كيفية التحقق من صحة التوقيع** في ملف PDF باستخدام مكتبة Aspose.Pdf لـ .NET. في النهاية ستعرف بالضبط **كيفية فحص حالة التوقيع**، ما هو شكل التوقيع المكسور، وكيفية التعامل مع الحالات الخاصة مثل وجود توقيعات متعددة أو فقدان بيانات التوقيع. لا مراجع غامضة—فقط مثال شفرة كامل قابل للتنفيذ مع الكثير من الشروحات التي توضح **لماذا الشفرة مهمة**.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* .NET 6+ (أو .NET Framework 4.7.2+) مثبت.
* نسخة مرخصة من **Aspose.Pdf for .NET** (الإصدار التجريبي المجاني يكفي للاختبار).
* ملف PDF يحتوي بالفعل على توقيع رقمي (سنسميه `signed.pdf`).
* Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#.

هذا كل شيء—لا تحتاج إلى حزم NuGet إضافية بخلاف Aspose.Pdf.

![مثال على التحقق من توقيع PDF](/images/verify-pdf-signature.png "تحقق من توقيع PDF")

*نص بديل: verify pdf signature*

## نظرة عامة – لماذا نتحقق من توقيع PDF؟

التوقيع الرقمي يربط هوية الموقع بمحتوى المستند. إذا تم تعديل ملف PDF بعد التوقيع، يتغير التجزئة (hash) المشفرة، ويصبح التوقيع **مكسورًا**. التحقق من التوقيع يضمن:

* أن المستند لم يتم العبث به.
* أن شهادة الموقع لا تزال صالحة.
* استيفاء متطلبات الامتثال (مثل FDA، EU eIDAS).

الآن بعد أن عرفنا **السبب**، دعنا نرى **الطريقة**.

## الخطوة 1: إعداد المشروع وإضافة Aspose.Pdf

أنشئ مشروعًا جديدًا من نوع console (أو أضفه إلى مشروع موجود) وأشر إلى تجميع Aspose.Pdf.

```csharp
// In a terminal or Package Manager Console
// dotnet add package Aspose.PDF
```

إذا كنت تفضل واجهة NuGet الكلاسيكية، ابحث عن *Aspose.PDF* وقم بتثبيتها. هذا السطر الواحد يجلب جميع الفئات التي سنحتاجها، بما في ذلك `PdfFileSignature`.

## الخطوة 2: تحميل مستند PDF الموقع

نحتاج إلى فتح ملف PDF الذي يحتوي على التوقيع الرقمي. فئة `Document` تمثل الملف بالكامل، بينما `PdfFileSignature` تمنحنا الوصول إلى عمليات التوقيع.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;

class Program
{
    static void Main()
    {
        // Path to the signed PDF – change this to your actual file location
        string pdfPath = @"C:\MyDocs\signed.pdf";

        // Load the PDF document
        using (var pdfDocument = new Document(pdfPath))
        {
            // Proceed to signature validation
            ValidateSignature(pdfDocument);
        }
    }
```

*لماذا نستخدم كتلة `using`؟* لأنها تضمن تحرير مقبض الملف بسرعة، مما يمنع مشاكل قفل الملفات على نظام Windows.

## الخطوة 3: تهيئة واجهة PdfFileSignature

فئة `PdfFileSignature` هي واجهة (Facade) تُجرد التعقيدات الثقيلة لمعالجة التوقيع. تعمل مباشرة على كائن `Document` الذي حمّلناه للتو.

```csharp
    static void ValidateSignature(Document pdfDocument)
    {
        using (var signatureFacade = new PdfFileSignature(pdfDocument))
        {
            // All subsequent steps happen inside this block
            // …
        }
    }
}
```

*نصيحة محترف:* إذا كنت تخطط للعمل مع عدة ملفات PDF دفعة واحدة، أعد استخدام كائن `PdfFileSignature` واحد لكل مستند لتقليل استهلاك الذاكرة.

## الخطوة 4: استرجاع أسماء التوقيعات

يمكن لملف PDF أن يحتوي على عدة توقيعات (تخيل عقدًا يتم توقيعه من قبل عدة أطراف). تُعيد الدالة `GetSignNames()` مصفوفة من معرفات التوقيع. للعرض السريع سنفحص التوقيع الأول فقط، لكن نفس المنطق ينطبق على أي فهرس.

```csharp
            // Get all signature names
            string[] signatureNames = signatureFacade.GetSignNames();

            if (signatureNames.Length == 0)
            {
                Console.WriteLine("No digital signatures found in the document.");
                return;
            }

            // We'll work with the first signature for simplicity
            string firstSignatureName = signatureNames[0];
            Console.WriteLine($"Found signature: {firstSignatureName}");
```

*لماذا نتحقق من الطول؟* محاولة الوصول إلى `[0]` في مصفوفة فارغة ستؤدي إلى استثناء، وهذا خطأ شائع عند معالجة ملفات PDF التي يزودها المستخدم.

## الخطوة 5: تحديد ما إذا كان التوقيع مكسورًا

الآن نصل إلى جوهر الموضوع: **كيفية فحص سلامة التوقيع**. تُعيد الدالة `IsSignatureCompromised` القيمة `true` إذا تغير محتوى المستند بعد التوقيع، أو إذا انقطعت سلسلة الشهادات.

```csharp
            // Verify whether the signature is compromised
            bool isCompromised = signatureFacade.IsSignatureCompromised(firstSignatureName);

            // Output the result in a human‑readable way
            Console.WriteLine(isCompromised
                ? "⚠️ The signature is compromised! The document may have been altered."
                : "✅ Signature is valid – the document is intact.");
```

*ماذا يعني “مكسور” فعليًا؟* داخليًا تقوم المكتبة بإعادة حساب تجزئة المستند ومقارنتها بالتجزئة المخزنة في التوقيع. أي عدم تطابق يؤدي إلى إرجاع `true`.

### التعامل مع توقيعات متعددة

إذا كان ملف PDF يحتوي على أكثر من توقيع واحد، قم بالتكرار عبر `signatureNames`:

```csharp
            foreach (var name in signatureNames)
            {
                bool compromised = signatureFacade.IsSignatureCompromised(name);
                Console.WriteLine($"{name}: {(compromised ? "Compromised" : "Valid")}");
            }
```

هذا النمط يتيح لك **التحقق من توقيع PDF الرقمي** لكل موقع، وهو غالبًا ما يكون مطلوبًا في العقود متعددة الأطراف.

## الخطوة 6: اختياري – استخراج تفاصيل الشهادة (متقدم)

أحيانًا تحتاج إلى عرض من قام بتوقيع PDF أو فحص تواريخ انتهاء صلاحية الشهادة. تُعيد الدالة `GetSignatureCertificate` كائن `X509Certificate2` يمكنك الاستعلام عنه.

```csharp
            var cert = signatureFacade.GetSignatureCertificate(firstSignatureName);
            Console.WriteLine($"Signer: {cert.Subject}");
            Console.WriteLine($"Issuer : {cert.Issuer}");
            Console.WriteLine($"Valid From: {cert.NotBefore}");
            Console.WriteLine($"Valid To  : {cert.NotAfter}");
```

*لماذا نهتم؟* المدققون يحبون رؤية سلسلة الشهادات، ويمكنك برمجيًا رفض التوقيعات التي على وشك الانتهاء.

## مثال كامل يعمل

بدمج كل ما سبق، إليك تطبيق console مستقل يمكنك نسخه ولصقه في `Program.cs` وتشغيله.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;

class Program
{
    static void Main()
    {
        string pdfPath = @"C:\MyDocs\signed.pdf";

        using (var pdfDocument = new Document(pdfPath))
        {
            ValidateSignature(pdfDocument);
        }
    }

    static void ValidateSignature(Document pdfDocument)
    {
        using (var signatureFacade = new PdfFileSignature(pdfDocument))
        {
            string[] signatureNames = signatureFacade.GetSignNames();

            if (signatureNames.Length == 0)
            {
                Console.WriteLine("No digital signatures found in the document.");
                return;
            }

            foreach (var name in signatureNames)
            {
                bool compromised = signatureFacade.IsSignatureCompromised(name);
                Console.WriteLine($"{name}: {(compromised ? "Compromised" : "Valid")}");

                // Optional: show certificate info
                var cert = signatureFacade.GetSignatureCertificate(name);
                Console.WriteLine($"  Signer: {cert.Subject}");
                Console.WriteLine($"  Issuer: {cert.Issuer}");
                Console.WriteLine($"  Valid From: {cert.NotBefore}");
                Console.WriteLine($"  Valid To  : {cert.NotAfter}");
                Console.WriteLine();
            }
        }
    }
}
```

**الناتج المتوقع** (عند كون التوقيع سليمًا):

```
Signature1: Valid
  Signer: CN=John Doe, O=Acme Corp, C=US
  Issuer: CN=Acme Root CA, O=Acme Corp, C=US
  Valid From: 1/1/2023 12:00:00 AM
  Valid To  : 12/31/2025 11:59:59 PM
```

إذا تم تعديل ملف PDF، ستظهر السطر `Signature1: Compromised` ويجب رفض الملف.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| **لم يتم العثور على توقيعات** | تم إنشاء PDF بدون توقيع رقمي أو تم إزالة التوقيع. | تحقق من ملف PDF الأصلي؛ استخدم عارضًا مثل Adobe Acrobat لتأكيد وجود التوقيع. |
| **استثناء عند `IsSignatureCompromised`** | يستخدم التوقيع خوارزمية غير مدعومة (مثل RSA‑PSS في إصدارات Aspose القديمة). | قم بالترقية إلى أحدث نسخة من Aspose.Pdf؛ فهي تدعم الخوارزميات الحديثة. |
| **فشل التحقق من سلسلة الشهادات** | شهادة الجذر الخاصة بالموقع غير موجودة في مخزن الثقة المحلي. | حمّل شهادات الجذر المطلوبة يدويًا عبر `X509Store` قبل التحقق. |
| **توقيعات متعددة، تم فحص الأول فقط** | العينة فحصت فقط `signatureNames[0]`. | كرّر العملية على جميع الأسماء (انظر الشفرة في الخطوة 5). |

## الخلاصة

لقد قمنا للتو **بالتحقق من صحة توقيع PDF** باستخدام Aspose.Pdf لـ .NET، وغطينا **كيفية التحقق من صحة التوقيع**، وعرضنا **كيفية فحص حالة التوقيع** لموقع واحد أو عدة مواقع، وحتى أظهرنا كيفية **التحقق من تفاصيل توقيع PDF الرقمي** مثل سلسلة الشهادات.  

مع هذه المعرفة يمكنك دمج التحقق من التوقيع في سير عمل المستندات الآلية، خطوط الامتثال، أو أي تطبيق C# يحتاج إلى الوثوق بملفات PDF. بعد ذلك قد تستكشف **كيفية التحقق من طوابع توقيع الوقت**، أو دمج خدمة PKI، أو استبدال Aspose ببديل مفتوح المصدر إذا كانت الترخيص مسألة.

هل لديك أسئلة حول حالات الحافة، أو تريد رؤية كيفية **التحقق من توقيع PDF الرقمي** في واجهة ويب API؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}