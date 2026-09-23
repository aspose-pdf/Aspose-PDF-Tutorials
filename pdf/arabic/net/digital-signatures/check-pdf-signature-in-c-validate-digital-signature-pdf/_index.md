---
category: general
date: 2026-02-28
description: تحقق من توقيع PDF في C# باستخدام Aspose.Pdf – تعلم كيفية فحص التوقيع،
  والتحقق من صحة التوقيع الرقمي للملف PDF، وتأكيد توقيع PDF بسرعة.
draft: false
keywords:
- check pdf signature
- how to check signature
- validate digital signature pdf
- verify pdf signature
- read pdf digital signatures
language: ar
og_description: تحقق من توقيع PDF في C# باستخدام Aspose.Pdf. تعلم كيفية فحص التوقيع،
  والتحقق من صحة التوقيع الرقمي للـ PDF، وتأكيد توقيع PDF في دقائق.
og_title: فحص توقيع PDF في C# – التحقق من صحة التوقيع الرقمي للملف PDF
tags:
- C#
- Aspose.Pdf
- Digital Signature
- PDF
title: تحقق من توقيع PDF في C# – التحقق من صحة التوقيع الرقمي للـ PDF
url: /ar/net/digital-signatures/check-pdf-signature-in-c-validate-digital-signature-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحقق من توقيع PDF في C# – التحقق من صحة التوقيع الرقمي للـ PDF

هل تساءلت يومًا **كيف تتحقق من توقيع PDF** دون الحاجة إلى أداة واجهة مستخدم رسومية ضخمة؟ لست وحدك. في العديد من سير عمل المؤسسات نحتاج إلى **التحقق من توقيع PDF** برمجيًا، خاصةً عند أتمتة خطوط معالجة المستندات.  

في هذا البرنامج التعليمي سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح لك بالضبط كيف **تتحقق من توقيع PDF** باستخدام Aspose.Pdf لـ .NET، وسنتطرق أيضًا إلى أفضل ممارسات **التحقق من صحة التوقيع الرقمي للـ PDF**. لا مراجع غامضة، فقط شفرة صافية يمكنك نسخها ولصقها اليوم.

## ما ستتعلمه

- تحميل مستند PDF موقع من القرص.
- استرجاع كل توقيع رقمي مدمج في الملف.
- تحديد ما إذا كان كل توقيع مخترقًا.
- إظهار نتيجة واضحة قابلة للقراءة البشرية.
- نصائح إضافية للتعامل مع الحالات الخاصة مثل التواقيع المتعددة أو ملفات PDF المحمية بكلمة مرور.

**المتطلبات المسبقة**  
تحتاج إلى .NET 6+ (أو .NET Framework 4.6+) ورخصة صالحة لـ Aspose.Pdf (أو مفتاح تقييم مؤقت). إذا لم تقم بتثبيت حزمة NuGet بعد، نفّذ:

```bash
dotnet add package Aspose.Pdf
```

هذا كل شيء—لا توجد تبعيات إضافية.

![مخطط يوضح تدفق التحقق من توقيع PDF](/images/check-pdf-signature-flow.png){: .align-center alt="مخطط تدفق التحقق من توقيع PDF"}

## الخطوة 1 – إعداد المشروع واستيراد المساحات الاسمية

أولاً، أنشئ تطبيقًا جديدًا من نوع console (أو دمج الشفرة في خدمة موجودة). توجيهات `using` تجلب الفئات الضرورية إلى النطاق.

```csharp
// Step 1: Project setup – import Aspose.Pdf namespaces
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;
```

> **لماذا هذا مهم:** `Document` يتعامل مع بنية PDF، بينما `PdfFileSignature` يمنحك الوصول إلى عمليات التوقيع. إبقاء الاستيرادات في الأعلى يجعل بقية الشفرة أنظف وأسهل للقراءة.

## الخطوة 2 – تحميل مستند PDF الموقع

تحتاج إلى ملف PDF يحتوي بالفعل على توقيع أو أكثر رقمي. استبدل `YOUR_DIRECTORY/signed.pdf` بالمسار الفعلي على جهازك.

```csharp
// Step 2: Load the signed PDF document
using var signedPdf = new Document("YOUR_DIRECTORY/signed.pdf");

// Quick sanity check – does the file even exist?
if (signedPdf == null)
{
    Console.WriteLine("Unable to load the PDF. Verify the path and try again.");
    return;
}
```

> **نصيحة احترافية:** إذا كان ملف PDF محميًا بكلمة مرور، استخدم النسخة الزائدة `new Document(path, password)` لفتحه بأمان.

## الخطوة 3 – إنشاء كائن PdfFileSignature

`PdfFileSignature` هو العامل الأساسي لجميع الاستعلامات المتعلقة بالتوقيع. إنه يلف الـ `Document` الذي حمّلناه للتو.

```csharp
// Step 3: Initialise the signature handler
using var signatureHandler = new PdfFileSignature(signedPdf);
```

> **لماذا نستخدم `using`** – كل من `Document` و `PdfFileSignature` يطبقان `IDisposable`. يضمن بيان `using` تحرير الموارد غير المُدارة (مقابض الملفات، المخازن الأصلية) بسرعة، مما يمنع تسرب الذاكرة في الخدمات طويلة التشغيل.

## الخطوة 4 – استرجاع جميع أسماء التوقيعات

يمكن أن يحتوي PDF على عدة توقيعات، كل منها يُعرف باسم فريد. تُعيد طريقة `GetSignNames` مصفوفة من السلاسل التي تحتوي على تلك المعرفات.

```csharp
// Step 4: Grab every signature name present in the PDF
string[] signatureNames = signatureHandler.GetSignNames();

if (signatureNames.Length == 0)
{
    Console.WriteLine("No signatures were found in this document.");
    return;
}
```

> **سؤال شائع:** *ماذا لو كان PDF يحتوي على توقيعات غير مرئية؟*  
> يتعامل Aspose.Pdf مع التوقيعات غير المرئية والمرئية بنفس الطريقة؛ سيظهر كلاهما في مجموعة `GetSignNames`.

## الخطوة 5 – التحقق من سلامة كل توقيع

الآن نمر عبر المصفوفة ونطلب من Aspose معرفة ما إذا تم العبث بأي توقيع. تُعيد طريقة `IsSignatureCompromised` القيمة `true` إذا لم يعد التجزئة التشفيرية للتوقيع تتطابق مع محتوى المستند الحالي.

```csharp
// Step 5: Check each signature for compromise
foreach (var name in signatureNames)
{
    bool isCompromised = signatureHandler.IsSignatureCompromised(name);

    // Step 6: Output the result
    Console.WriteLine($"{name}: compromised = {isCompromised}");
}
```

**الناتج المتوقع** (مثال):

```
Signature1: compromised = False
Signature2: compromised = True
```

إذا كان التوقيع *ليس* مخترقًا، يمكنك الوثوق بسلامة المستند بأمان. إذا ظهرت القيمة `True`، فقد تم تعديل المستند منذ تطبيق التوقيع—مفيد لسجلات التدقيق.

## الخطوة 6 – معالجة الحالات الخاصة والسيناريوهات المتقدمة

### توقيعات متعددة بخوارزميات مختلفة

أحيانًا يحتوي PDF على توقيعات تم إنشاؤها باستخدام RSA أو ECDSA أو حتى رموز الطابع الزمني. `IsSignatureCompromised` يخفِّي تفاصيل الخوارزمية، لكن قد ترغب في **قراءة توقيعات PDF الرقمية** لتسجيل اسم الخوارزمية، وقت التوقيع، أو تفاصيل الشهادة.

```csharp
// Optional: Retrieve detailed info for each signature
foreach (var name in signatureNames)
{
    var info = signatureHandler.GetSignatureInfo(name);
    Console.WriteLine($"--- {name} Details ---");
    Console.WriteLine($"Signer: {info.SignerName}");
    Console.WriteLine($"Reason: {info.Reason}");
    Console.WriteLine($"Signing Time: {info.SigningTime}");
    Console.WriteLine($"Algorithm: {info.SignatureAlgorithm}");
}
```

### التحقق من توقيع دون تحميل المستند بالكامل

إذا كنت بحاجة فقط إلى **التحقق من توقيع PDF** لملف ضخم، يمكنك استخدام مُنشئ `PdfFileSignature` الذي يقبل مسار الملف مباشرة، متجنبًا عبء تحميل كائن `Document` بالكامل.

```csharp
using var signatureHandler = new PdfFileSignature("large_signed.pdf");
bool compromised = signatureHandler.IsSignatureCompromised("Signature1");
```

### ملفات PDF المحمية بكلمة مرور

عند تشفير PDF، يجب توفير كلمة مرور المالك أو المستخدم عند إنشاء الـ `Document`. عملية التحقق من التوقيع تظل كما هي بعد ذلك.

```csharp
using var signedPdf = new Document("protected.pdf", "myPassword");
using var signatureHandler = new PdfFileSignature(signedPdf);
```

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله كما هو. يتضمن جميع الخطوات السابقة، بالإضافة إلى معالجة الأخطاء بشكل سلس.

```csharp
// Full example – Check PDF Signature with Aspose.Pdf
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the signed PDF (adjust the path as needed)
        using var signedPdf = new Document("YOUR_DIRECTORY/signed.pdf");
        if (signedPdf == null)
        {
            Console.WriteLine("Failed to load PDF. Check the file path.");
            return;
        }

        // 2️⃣ Initialise the signature handler
        using var signatureHandler = new PdfFileSignature(signedPdf);

        // 3️⃣ Get all signature names
        string[] signatureNames = signatureHandler.GetSignNames();

        if (signatureNames.Length == 0)
        {
            Console.WriteLine("No signatures detected in the document.");
            return;
        }

        // 4️⃣ Iterate and check each signature
        foreach (var name in signatureNames)
        {
            bool isCompromised = signatureHandler.IsSignatureCompromised(name);
            Console.WriteLine($"{name}: compromised = {isCompromised}");

            // Optional: Dump extra info (demonstrates read pdf digital signatures)
            var info = signatureHandler.GetSignatureInfo(name);
            Console.WriteLine($"   Signer: {info.SignerName}");
            Console.WriteLine($"   Time  : {info.SigningTime}");
            Console.WriteLine($"   Algo  : {info.SignatureAlgorithm}");
        }
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. إذا تم إعداد كل شيء بشكل صحيح، سترى قائمة بالتواقيع وعلمًا منطقيًا يُظهر ما إذا كان كل توقيع مخترقًا.

## الخلاصة

أنت الآن تعرف **كيف تتحقق من توقيع PDF** برمجيًا في C#، وكيف **تتحقق من صحة التوقيع الرقمي للـ PDF**، وكيف **تتحقق من سلامة توقيع PDF** باستخدام Aspose.Pdf. المنطق الأساسي يختصر في تحميل المستند، استخراج أسماء التوقيعات، واستدعاء `IsSignatureCompromised`. من هنا يمكنك التوسع إلى تسجيل تفاصيل الشهادة، معالجة الملفات المحمية بكلمة مرور، أو دمج الفحص في خط معالجة مستندات أكبر.

**الخطوات التالية**  
- استكشف **قراءة توقيعات PDF الرقمية** لاستخراج شهادات الموقعين لتقارير الامتثال.  
- دمج هذا الفحص مع خدمة مراقبة الملفات لرفض التحميلات المعدلة تلقائيًا.  
- اختبر مع خوارزميات توقيع مختلفة (RSA, ECDSA) لضمان بقاء منطق التحقق قويًا.

هل لديك تعديل تحاول تنفيذه؟ اترك تعليقًا، ولنحل المشكلة معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}