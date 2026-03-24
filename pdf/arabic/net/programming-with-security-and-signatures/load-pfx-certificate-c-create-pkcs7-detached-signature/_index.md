---
category: general
date: 2026-03-24
description: تحميل شهادة PFX في C# بسرعة وأمان لإنشاء توقيع PKCS7 منفصل من ملف. دليل
  خطوة بخطوة مع الكود الكامل والمخاطر.
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: ar
og_description: تحميل شهادة PFX باستخدام C# وإنشاء توقيع PKCS7 منفصل من ملف. مثال
  كامل مع شروحات ومعالجة الحالات الخاصة.
og_title: تحميل شهادة PFX C# – إنشاء توقيع PKCS7 منفصل
tags:
- C#
- PKCS7
- X509
- Cryptography
title: تحميل شهادة PFX C# – إنشاء توقيع PKCS7 منفصل
url: /ar/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحميل شهادة PFX في C# – إنشاء توقيع PKCS7 منفصل

هل احتجت يوماً إلى **تحميل شهادة PFX في C#** فقط لتوقيع بعض البيانات، لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—فالكثير من المطورين يواجهون نفس الصعوبة عندما يتعاملون لأول مرة مع شهادات X.509 و PKCS#7.  

الأخبار السارة؟ في هذا الدرس ستحصل على حل جاهز للتنفيذ **يقوم بتحميل شهادة PFX في C#**، وينشئ **توقيع PKCS7 منفصل**، وحتى يوضح لك كيفية استخراج التوقيع من ملف. لا مراجع غامضة، فقط كود ملموس وتفسير لكل سطر.

> **ما ستستفيده**  
> * فهم واضح لعملية تحميل الشهادة.  
> * مثال كامل وقابل للترجمة يبني توقيع PKCS7 منفصل.  
> * نصائح للتعامل مع المشكلات الشائعة (كلمة مرور خاطئة، ملف مفقود، عدم توافق الخوارزميات).  

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (واجهات برمجة التطبيقات المستخدمة هي جزء من مكتبة الفئة الأساسية).  
- ملف `.pfx` صالح وكلمة مروره.  
- Visual Studio 2022 أو أي محرر تفضله—لا حاجة لحزم NuGet خاصة للمثال الأساسي.  

إذا كان لديك ذلك، فلنغص.

---

## تحميل شهادة PFX في C# – خطوة بخطوة

فيما يلي الحد الأدنى من توجيهات `using` التي ستحتاجها. احتفظ بها في أعلى ملفك حتى يعرف المترجم أين يجد الأنواع.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ تحديد مسار الشهادة وكلمة المرور

أولاً، أخبر وقت التشغيل بمكان وجود ملف `.pfx` وما هي كلمة مروره. كتابة المسارات مباشرة في الكود مقبولة للعرض التجريبي، لكن **أبدًا** لا تُضمّن كلمات المرور في كود الإنتاج.

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **نصيحة احترافية:** احفظ كلمة المرور في Azure Key Vault أو AWS Secrets Manager أو متغيّر بيئي—لا تقم أبدًا بدمجها في نظام التحكم بالمصادر.

### 2️⃣ تحميل الشهادة بأمان

نحن نغلف عملية التحميل داخل كتلة `try / catch` لإظهار الأخطاء الشائعة مثل ملف مفقود أو كلمة مرور غير صحيحة.

```csharp
X509Certificate2 LoadCertificate(string path, string password)
{
    try
    {
        // The X509KeyStorageFlags ensure the private key is exportable for signing
        var cert = new X509Certificate2(path, password,
            X509KeyStorageFlags.MachineKeySet |
            X509KeyStorageFlags.PersistKeySet |
            X509KeyStorageFlags.Exportable);

        if (!cert.HasPrivateKey)
            throw new InvalidOperationException("The certificate does not contain a private key.");

        return cert;
    }
    catch (Exception ex) when (ex is CryptographicException || ex is IOException)
    {
        Console.Error.WriteLine($"Failed to load certificate: {ex.Message}");
        throw;
    }
}
```

### 3️⃣ إنشاء كائن **توقيع PKCS7 منفصل**

بافتراض أنك تستخدم مكتبة طرف ثالث تُظهر فئة `PKCS7Detached` (العديد من SDKs التجارية تفعل ذلك)، نقوم بإنشاء كائن منها باستخدام الشهادة التي حمّلناها للتو.

```csharp
// Step 3: Build the signer
var certificate = LoadCertificate(certificatePath, certificatePassword);

var pkcs7Signer = new PKCS7Detached(certificate)
{
    // Provide a custom hash‑signing callback.
    // The library will invoke this delegate for each hash it needs to sign.
    CustomSignHash = (hash, algorithm) => MySigner.Sign(hash, algorithm)
};
```

> **لماذا رد نداء (callback)؟** تسمح بعض SDKs بدمج وحدات أمان الأجهزة (HSMs) أو خدمات التوقيع عن بُعد. من خلال إتاحة `CustomSignHash`، تحتفظ بمنطق التوقيع مرنًا.

### 4️⃣ تنفيذ التفويض (delegate) الخاص بالتوقيع

إليك تنفيذ بسيط يستخدم المفتاح الخاص من الشهادة المحمّلة. استبدل `MySigner.Sign` بنداء HSM الخاص بك إذا لزم الأمر.

```csharp
static class MySigner
{
    public static byte[] Sign(byte[] hash, HashAlgorithmName algorithm)
    {
        // The certificate's private key is an RSA key in most cases.
        using RSA rsa = certificate.GetRSAPrivateKey()
            ?? throw new InvalidOperationException("RSA private key not available.");

        // RSA-PKCS#1 v1.5 signing – adjust if your policy requires PSS.
        return rsa.SignHash(hash, algorithm, RSASignaturePadding.Pkcs1);
    }
}
```

### 5️⃣ توقيع بيانات عشوائية واسترجاع كائن PKCS7 المنفصل

الآن نقوم فعليًا بتوقيع شيء ما. قد تكون البيانات ملفًا، أو حمولة JSON، أو أي شيء تحتاج إلى حمايته.

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**الناتج المتوقع**

```
Detached PKCS7 signature created successfully.
```

الآن لديك **توقيع PKCS7 من ملف** (`sample.txt.sig`) يمكن التحقق منه بشكل مستقل عن البيانات الأصلية.

---

## إنشاء توقيع PKCS7 منفصل – خيارات متقدمة

بينما يعمل التدفق الأساسي لمعظم السيناريوهات، غالبًا ما تحتاج أنظمة الإنتاج إلى إعدادات إضافية:

| الميزة | كيفية التفعيل | متى يُستخدم |
|---------|---------------|-------------|
| **اختيار الخوارزمية** | تمرير `HashAlgorithmName.SHA256` (أو SHA384/SHA512) إلى `SignHash` | إذا كان نظام الامتثال الخاص بك يتطلب تجزئة محددة |
| **إضافة طابع زمني** | إلحاق طابع زمني RFC‑3161 بعد التوقيع | للتصديق على المدى الطويل |
| **موقّعين متعددين** | إنشاء مثيلات إضافية من `PKCS7Detached` ودمجها | عند الحاجة إلى توقيع مشترك للوثائق |
| **سمات CMS مخصصة** | استخدام طريقة المكتبة `AddAttribute` قبل `Sign` | لإدراج وقت التوقيع، معرف الموقّع، إلخ. |

فيما يلي مقتطف سريع يُظهر اختيار SHA‑256:

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

---

## التحقق من توقيع PKCS7 المنفصل (اختياري)

التحقق هو النصف الآخر من القصة. معظم المكتبات تُظهر طريقة `Verify` التي تأخذ البيانات الأصلية والتوقيع المنفصل.

```csharp
bool VerifySignature(byte[] originalData, byte[] signature, X509Certificate2 cert)
{
    var verifier = new PKCS7Detached(cert);
    return verifier.Verify(originalData, signature);
}

// Usage
bool isValid = VerifySignature(dataToSign, detachedSignature, certificate);
Console.WriteLine(isValid ? "Signature valid!" : "Signature invalid!");
```

إذا كنت تستخدم SDK مختلف، ابحث عن فئة `CmsSignedData` أو `SignedCms` في مساحة الأسماء `System.Security.Cryptography.Pkcs` في .NET—فهذه يمكنها أيضًا معالجة التواقيع المنفصلة.

---

## المشكلات الشائعة وكيفية تجنّبها

1. **كلمة مرور خاطئة** – سيظهر استثناء `CryptographicException` الرسالة *“The specified network password is not correct.”* احفظ كلمات المرور بأمان واختبرها بشكل مستقل قبل تحميل الشهادة.  
2. **شهادة بدون مفتاح خاص** – بعض ملفات `.pfx` تُصدّر بدون المفتاح الخاص. تحقق من إعدادات التصدير في سلطة الشهادات (CA) أو مخزن المفاتيح (Key Vault).  
3. **عدم تطابق الخوارزمية** – إذا كان الموقّع يتوقع SHA‑256 لكنك تستخدم SHA‑1، سيفشل التحقق. احرص على توافق الخوارزمية بين خطوات التوقيع والتحقق.  
4. **مشكلات مسار الملف** – المسارات النسبية تعمل في بيئة التطوير لكنها تتعطل عند النشر. يفضَّل استخدام `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` أو مسارات مطلقة تُحدَّد عبر الإعدادات.  
5. **اختلافات المنصات** – يتعامل Windows و Linux مع مخزن المفتاح الخاص بصورة مختلفة. استخدام `X509KeyStorageFlags.Exportable` يخفف معظم المشكلات عبر المنصات.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;

// ------------------------------------------------------------
// Helper class that encapsulates signing logic
// ------------------------------------------------------------
static class MySigner
{
    private static X509Certificate2 _cert;

    public static void Init(X509Certificate2 cert) => _cert = cert;

    public static byte[] Sign(byte[] hash, HashAlgorithmName algorithm)
    {
        using RSA rsa = _cert.GetRSAPrivateKey()
            ?? throw new InvalidOperationException("RSA private key not available.");

        return rsa.SignHash(hash, algorithm, RSASignaturePadding.Pkcs1);
    }
}

// ------------------------------------------------------------
// Main program
// ------------------------------------------------------------
class Program
{
    static X509Certificate2 LoadCertificate(string path, string password)
    {
        try
        {
            var cert = new X509Certificate2(path, password,
                X509KeyStorageFlags.MachineKeySet |
                X509KeyStorageFlags.PersistKeySet |
                X509KeyStorageFlags.Exportable);

            if (!cert.HasPrivateKey)
                throw new InvalidOperationException("Certificate lacks a private key.");

            return cert;
        }
        catch (Exception ex) when (ex is CryptographicException || ex is IOException)
        {
            Console.Error.WriteLine($"Failed to load certificate: {ex.Message}");
            throw;
        }
    }

    static void Main()
    {
        // 1️⃣ Path & password
        string certPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
        string certPassword = "yourPassword";

        // 2️⃣ Load the cert
        X509Certificate2 cert = LoadCertificate(certPath, certPassword);
        MySigner.Init(cert);

        // 3️⃣ Create PKCS7 signer (replace with your library's class)
        var pkcs7Signer = new PKCS7Detached(cert)
        {
            CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
        };

        // 4️⃣ Data to sign
        string dataFile = "sample.txt";
        byte[] data = File.ReadAllBytes(dataFile);

        // 5️⃣ Generate detached signature
        byte[] signature = pkcs7Signer.Sign(data);
        File.WriteAllBytes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}