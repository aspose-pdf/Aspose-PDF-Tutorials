---
category: general
date: 2026-08-14
description: إنشاء خيارات التوقيع في C# لتطبيق التوقيع الرقمي. تعلم كيفية تكوين التوقيع،
  وتنفيذ دالة تجزئة مخصصة، وتوقيع المستندات برمجياً.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: ar
lastmod: 2026-08-14
og_description: إنشاء خيارات التوقيع في C# وتطبيق توقيع رقمي. يشرح هذا الدليل كيفية
  تكوين التوقيع، وإضافة دالة تجزئة مخصصة، وتوقيع مستند.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: إنشاء خيارات التوقيع في C# – دليل التوقيع الرقمي خطوة بخطوة
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  headline: Create signature options in C# – full guide to digital signing
  type: TechArticle
- description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  name: Create signature options in C# – full guide to digital signing
  steps:
  - name: '**Hash calculation** – now delegated to your custom hash function.'
    text: '**Hash calculation** – now delegated to your custom hash function.'
  - name: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
    text: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
  - name: '**Embedding** – the generated signature is attached to the output file.'
    text: '**Embedding** – the generated signature is attached to the output file.'
  type: HowTo
tags:
- digital signature
- C#
- security
title: إنشاء خيارات التوقيع في C# – دليل كامل للتوقيع الرقمي
url: /ar/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء خيارات التوقيع في C# – دليل كامل للتوقيع الرقمي

إنشاء خيارات التوقيع في C# لتكوين سير عمل التوقيع الرقمي. يوضح هذا الدرس كيفية تطبيق التوقيع الرقمي، وتنفيذ دالة تجزئة مخصصة، وتوقيع مستند باستخدام الفئة `SignatureOptions`. إذا احتجت يومًا إلى توقيع ملف PDF أو XML أو أي حمولة ثنائية من تطبيق .NET، فإن الخطوات أدناه توفر لك حلاً جاهزًا للتنفيذ.

ستتعلم كيف أن:

* تهيئة `SignatureOptions` باستخدام خوارزمية تجزئة مخصصة،
* استدعاء طريقة التوقيع بشكل صحيح،
* التحقق من أن التوقيع تم تطبيقه،
* تجنب المشكلات الشائعة عند تكوين التوقيع.

المتطلبات المسبقة الوحيدة هي .NET SDK حديث (≥ .NET 6) ومكتبة توقيع تُظهر `SignatureOptions` (مثلاً، **GroupDocs.Signature**، **Aspose.Signature**، أو واجهة برمجة تطبيقات مشابهة). لا توجد أدوات خارجية مطلوبة.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|---------|-----------|
| .NET 6 SDK أو أحدث | يوفر ميزات اللغة الحديثة المستخدمة في الأمثلة. |
| حزمة NuGet لمكتبة توقيع (مثال، `GroupDocs.Signature`) | تزود بنوع `SignatureOptions` وطريقة الامتداد `Sign`. |
| الوصول إلى مفتاح خاص أو شهادة | مطلوب لإنشاء توقيع رقمي قابل للتحقق. |

ثبت المكتبة باستخدام سطر الأوامر القياسي:

```bash
dotnet add package GroupDocs.Signature
```

---

## الخطوة 1: إنشاء خيارات التوقيع

الخطوة الأولى هي إنشاء كائن `SignatureOptions` وتعيين الخصائص التي تتحكم في عملية التوقيع. هذا الكائن يخبر المكتبة *ماذا* يتم توقيعه و*كيف* يتم توقيعه.

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

// Create a new SignatureOptions instance
var signatureOptions = new SignatureOptions
{
    // The signing algorithm (e.g., RSA‑SHA256) is defined by the library.
    // You can also set visual appearance, page number, etc., here.
    // For this tutorial we focus on the custom hash function.
};
```

**لماذا هذا مهم:** `SignatureOptions` يعمل كعقد بين الشيفرة الخاصة بك ومحرك التوقيع. من خلال تكوينه مسبقًا تتجنب تكرار الكود الروتيني عند توقيع مستندات متعددة.

---

## الخطوة 2: تنفيذ دالة تجزئة مخصصة

تمنحك *دالة التجزئة المخصصة* تحكمًا كاملاً في الخلاصة التي يوقعها خوارزمية التوقيع. يكون هذا مفيدًا عندما لا يلبي التجزئة الافتراضية (SHA‑256) متطلبات الامتثال أو عندما تحتاج إلى تجزئة جزء من المستند.

```csharp
using System.Security.Cryptography;
using System.Text;

// Define a delegate that matches the library’s expected signature
Func<byte[], byte[]> MyHash = data =>
{
    // Example: compute SHA‑512 and then truncate to 256 bits
    using var sha512 = SHA512.Create();
    var fullHash = sha512.ComputeHash(data);

    // Truncate to the first 32 bytes (256 bits)
    var truncated = new byte[32];
    Buffer.BlockCopy(fullHash, 0, truncated, 0, truncated.Length);
    return truncated;
};

// Attach the custom hash to the options
signatureOptions.CustomSignHash = hash => MyHash(hash);
```

**لماذا هذا مهم:** من خلال تعيين `CustomSignHash`، تستبدل خطوة التجزئة الداخلية للمكتبة بـ `MyHash`. سيقوم محرك التوقيع الآن بتوقيع البايتات التي تُرجعها دالتك، مما يضمن الامتثال لأي سياسة مخصصة.

---

## الخطوة 3: تحميل المستند وتطبيق التوقيع الرقمي

بعد إعداد الخيارات، يمكنك الآن فتح الملف المستهدف واستدعاء طريقة التوقيع. الطريقة `Sign` مقدمة من المكتبة وتستخدم `SignatureOptions` المُكوَّنة.

```csharp
using System.IO;

// Path to the file you want to sign
string inputPath = @"C:\Docs\contract.pdf";
string outputPath = @"C:\Docs\contract.signed.pdf";

// Load the document into the Signature object
using var signature = new Signature(inputPath);

// Sign the document using the previously created options
bool result = signature.Sign(outputPath, signatureOptions);

if (!result)
{
    throw new InvalidOperationException("The document could not be signed.");
}
```

**لماذا هذا مهم:** استدعاء `Sign` ينفّذ ثلاث عمليات داخليًا:

1. **حساب التجزئة** – الآن يتم تفويضه إلى دالة التجزئة المخصصة الخاصة بك.  
2. **إنشاء التوقيع** – باستخدام المفتاح الخاص المقدم إلى تكوين المكتبة.  
3. **الإدماج** – يتم إرفاق التوقيع المُنشأ بالملف الناتج.

إذا فشل أي خطوة، تُعيد الطريقة `false`، مما يتيح لك معالجة الخطأ بشكل سلس.

---

## الخطوة 4: التحقق من توقيع المستند

تحقق سريع يثبت أن التوقيع تم تطبيقه بشكل صحيح. معظم المكتبات توفر طريقة `Verify` التي تتحقق من سلامة الملف الموقع.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**لماذا هذا مهم:** التحقق يضمن أن المستند الموقع لم يتم العبث به بعد التوقيع وأن التجزئة المخصصة أنتجت خلاصة متوافقة.

---

## كيفية تكوين التوقيع لأنواع الملفات المختلفة

يمكن إعادة استخدام كائن `SignatureOptions` نفسه لملفات PDF، ومستندات Word، والصور، أو الملفات الثنائية العادية. التغيير الوحيد المطلوب هو فئة الخيارات المحددة (مثل `PdfSignatureOptions`، `WordSignatureOptions`). إليك مثال سريع لصورة JPEG:

```csharp
using GroupDocs.Signature.Options;

var imageOptions = new ImageSignatureOptions
{
    // Position the signature on the image
    Left = 100,
    Top = 50,
    Width = 150,
    Height = 50,
    CustomSignHash = hash => MyHash(hash)   // reuse the same custom hash
};

using var imgSignature = new Signature(@"C:\Images\photo.jpg");
imgSignature.Sign(@"C:\Images\photo.signed.jpg", imageOptions);
```

**لماذا هذا مهم:** فهم كيفية *تكوين التوقيع* لكل تنسيق يتيح لك توسيع قاعدة الشيفرة نفسها عبر أنواع مستندات متعددة دون إعادة كتابة منطق التجزئة.

---

## المشكلات الشائعة وأفضل الممارسات

| المشكلة | الحل الموصى به |
|----------|----------------|
| نسيان تعيين `CustomSignHash` بعد إنشاء `SignatureOptions` | عيّن المُفوض مباشرةً بعد إنشاء كائن الخيارات. |
| استخدام خوارزمية تجزئة لا يدعمها شهادة التوقيع | تحقق من أن استخدام المفتاح في الشهادة يتطابق مع طول التجزئة (مثال، RSA‑2048 مع SHA‑512). |
| إغفال الحاجة إلى تحرير كائنات `Signature` | ضع كائن `Signature` داخل كتلة `using` لتحرير مقابض الملفات. |
| حفظ الملف الموقع فوق المصدر الأصلي | دائمًا احفظ إلى مسار ملف جديد (`outputPath`) للحفاظ على المستند الأصلي. |

---

## مثال كامل يعمل

فيما يلي برنامج مستقل يجمع جميع الأجزاء معًا. انسخه إلى مشروع وحدة تحكم جديد وشغّله؛ سيظهر وحدة التحكم نجاح العملية أو فشلها.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

class Program
{
    // Custom hash implementation (SHA‑512 truncated to 256 bits)
    private static byte[] MyHash(byte[] data)
    {
        using var sha512 = SHA512.Create();
        var full = sha512.ComputeHash(data);
        var truncated = new byte[32];
        Buffer.BlockCopy(full, 0, truncated, 0, truncated.Length);
        return truncated;
    }

    static void Main()
    {
        // Paths
        string input = @"C:\Docs\contract.pdf";
        string output = @"C:\Docs\contract.signed.pdf";

        // Step 1: create signature options
        var signatureOptions = new SignatureOptions
        {
            CustomSignHash = hash => MyHash(hash)
        };

        // Step 2: sign the document
        using var signer = new Signature(input);
        bool signed = signer.Sign(output, signatureOptions);
        if (!signed)
        {
            Console.WriteLine("Signing failed.");
            return;
        }

        // Step 3: verify the signature
        using var verifier = new Signature(output);
        bool verified = verifier.Verify();
        Console.WriteLine(verified
            ? "Signature verified successfully."
            : "Signature verification failed.");
    }
}
```

**الناتج المتوقع**

```
Signature verified successfully.
```

إذا طبع وحدة التحكم “Signing failed.” أو “Signature verification failed.”، فتحقق مرة أخرى من تكوين الشهادة وتأكد من أن دالة التجزئة المخصصة تُعيد مصفوفة بايت بالحجم المتوقع.

---

## الخلاصة

أنت الآن تعرف كيف **تنشئ خيارات التوقيع** في C#، وترفق **دالة تجزئة مخصصة**، وت **تطبق التوقيع الرقمي** على أي مستند مدعوم. غطى الدرس دورة الحياة الكاملة: تكوين الخيارات، توقيع الملف، والتحقق من النتيجة. من خلال إعادة استخدام نفس كائن `SignatureOptions` يمكنك أيضًا **كيفية تكوين التوقيع** للصور، ملفات Word، أو الملفات الثنائية الخام.

---

## ما التالي؟

* استكشف خصائص `SignatureOptions` الإضافية مثل الطوابع البصرية، خوادم الطوابع الزمنية، وسلاسل الشهادات – هذه تتماشى مع كلمة **apply digital signature**.  
* جرّب خوارزميات تجزئة أخرى (مثال، Blake2b) عن طريق استبدال التنفيذ داخل `MyHash`.  
* دمج تدفق التوقيع في واجهة برمجة تطبيقات ويب لتمكين توقيع المستندات أثناء التشغيل – امتداد طبيعي لـ **how to sign document** في بنية معمارية موجهة للخدمات.

لا تتردد في تعديل الشيفرة لتتناسب مع سياسات الأمان الخاصة بك، ومشاركة تجربتك في التعليقات. توقيع سعيد!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تغيير لغة توقيع PDF باستخدام Aspose.PDF لـ .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [دورة توقيع رقمي Aspose Pdf .NET (ألمانية)](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [دورة توقيع رقمي Aspose Pdf .NET (فرنسية)](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}