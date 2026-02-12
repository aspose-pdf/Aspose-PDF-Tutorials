---
category: general
date: 2026-02-12
description: تحقق من صحة توقيع PDF بسرعة باستخدام Aspose.Pdf. تعلّم كيفية التحقق من
  صحة PDF، والتحقق من التوقيع الرقمي للـ PDF، وفحص توقيع PDF، وقراءة التوقيع الرقمي
  للـ PDF في مثال كامل.
draft: false
keywords:
- validate pdf signature
- how to validate pdf
- verify digital signature pdf
- check pdf signature
- read digital signature pdf
language: ar
og_description: تحقق من صحة توقيع PDF في C# باستخدام Aspose.Pdf. يوضح هذا الدليل كيفية
  التحقق من صحة PDF، والتحقق من التوقيع الرقمي للـ PDF، وفحص توقيع PDF، وقراءة التوقيع
  الرقمي للـ PDF في مثال واحد قابل للتنفيذ.
og_title: تحقق من توقيع PDF في C# – دليل برمجة كامل
tags:
- C#
- Aspose.Pdf
- Digital Signature
- PDF Validation
title: تحقق من صحة توقيع PDF في C# – دليل خطوة بخطوة
url: /ar/net/programming-with-security-and-signatures/validate-pdf-signature-in-c-step-by-step-guide/
---

text** keep bold but translate inside.

Also blockquote > lines.

Let's start.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التحقق من توقيع PDF في C# – دليل برمجة كامل

هل احتجت يوماً إلى **التحقق من توقيع PDF** لكن لم تكن متأكدًا أي استدعاء API يقوم بالعمل الفعلي؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند دمج سير عمل المستندات. في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح **كيفية التحقق من PDF**، **التحقق من التوقيع الرقمي PDF**، **فحص توقيع PDF**، وحتى **قراءة تفاصيل التوقيع الرقمي PDF** باستخدام Aspose.Pdf for .NET.

في نهاية هذا الدليل ستحصل على تطبيق console مستقل يحمل ملف PDF موقع، يتواصل مع سلطة الشهادات، ويطبع رسالة واضحة “Valid” أو “Invalid”. لا مراجع غامضة، لا أجزاء مفقودة—فقط شفرة جاهزة للنسخ واللصق مع شرح لكل سطر.

## ما الذي ستحتاجه

- **.NET 6.0+** (الكود يعمل أيضًا على .NET Framework 4.6.1، لكن .NET 6 هو الإصدار طويل الدعم الحالي)
- حزمة NuGet **Aspose.Pdf for .NET** (`Aspose.Pdf` الإصدار 23.9 أو أحدث)
- ملف **PDF موقع** على القرص (سنسميه `signed.pdf`)
- الوصول إلى **خدمة التحقق من سلطة الشهادات** (عنوان URL يقبل اسم التوقيع ويعيد قيمة Boolean)

إذا كان أي من هذه غير مألوف لك، لا تقلق—تثبيت حزمة NuGet يتم بأمر واحد، ويمكنك إنشاء PDF موقع تجريبي باستخدام واجهة التوقيع في Aspose.Pdf (انظر قسم “المكافأة” في النهاية).

## الخطوة 1: إعداد المشروع وتثبيت Aspose.Pdf

إنشاء مشروع console جديد وإضافة المكتبة:

```bash
dotnet new console -n PdfSignatureValidator
cd PdfSignatureValidator
dotnet add package Aspose.Pdf --version 23.9.0
```

> **Pro tip:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن *Aspose.Pdf* وقم بتثبيت أحدث نسخة مستقرة.

## الخطوة 2: تحميل مستند PDF الموقع

أول شيء نفعله هو فتح ملف PDF الذي يحتوي على توقيع رقمي واحد على الأقل. استخدام كتلة `using` يضمن تحرير مقبض الملف حتى لو حدث استثناء.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // Path to the signed PDF – adjust as needed
        const string pdfPath = "YOUR_DIRECTORY/signed.pdf";

        // Load the PDF document inside a using block for proper disposal
        using (var pdfDocument = new Document(pdfPath))
        {
            // Continue with validation logic...
```

> **Why this matters:** فتح الملف باستخدام `Document` يمنحنا الوصول إلى كل من المحتوى المرئي *و* مجموعة التوقيعات، وهو أمر أساسي عندما تحتاج إلى **قراءة التوقيع الرقمي PDF** لاحقًا.

## الخطوة 3: إنشاء معالج التوقيع واسترجاع اسم التوقيع

يفصل Aspose.Pdf بين تمثيل المستند (`Document`) وأدوات التوقيع (`PdfFileSignature`). نقوم بإنشاء المعالج ونستخرج اسم أول توقيع—هذا هو ما تتوقعه سلطة الشهادات.

```csharp
            // Step 3: Create the signature handler
            var signatureHandler = new PdfFileSignature(pdfDocument);

            // Get the collection of signature names; we’ll use the first one
            var signNames = signatureHandler.GetSignNames();

            if (signNames == null || signNames.Count == 0)
            {
                Console.WriteLine("No digital signatures found in the PDF.");
                return;
            }

            string signatureName = signNames[0];
            Console.WriteLine($"Found signature: {signatureName}");
```

> **Edge case:** يمكن أن يحتوي PDF على عدة توقيعات (مثل التوقيع المتزايد). هنا نختار الأول للبساطة، لكن يمكنك التجول عبر `signNames` والتحقق من كل واحد على حدة.

## الخطوة 4: التحقق من التوقيع عبر خدمة سلطة الشهادات

الآن نقوم فعليًا **بفحص توقيع PDF** عن طريق استدعاء `ValidateSignature`. الطريقة تتواصل مع الـ URL الذي تزوده، تمرر اسم التوقيع، وتعيد قيمة Boolean تدل على الصلاحية.

```csharp
            // Step 4: Validate the signature using the CA's validation endpoint
            var validationUri = new Uri("https://ca.example.com/validate");

            bool isValid = signatureHandler.ValidateSignature(signatureName, validationUri);

            // Display the result in a friendly way
            Console.WriteLine(isValid ? "Valid" : "Invalid");
```

> **Why we use a URI:** تتوقع واجهة Aspose API نقطة نهاية HTTP(S) قابلة للوصول تُنفّذ بروتوكول التحقق الخاص بسلطة الشهادات (عادةً POST مع بيانات التوقيع). إذا كانت سلطة الشهادات تستخدم مخططًا مختلفًا، يمكنك استدعاء التحميلات الزائدة لـ `ValidateSignature` التي تقبل بيانات الشهادة الخام.

## الخطوة 5: (اختياري) قراءة تفاصيل إضافية للتوقيع

إذا رغبت أيضًا في **قراءة التوقيع الرقمي PDF** للبيانات الوصفية—مثل وقت التوقيع، اسم الموقع، أو بصمة الشهادة—فـ Aspose يجعل ذلك سهلًا:

```csharp
            // Optional: Extract more info about the signature
            var signatureInfo = signatureHandler.GetSignatureInfo(signatureName);

            Console.WriteLine("\n--- Signature Details ---");
            Console.WriteLine($"Signer: {signatureInfo.Signer}");
            Console.WriteLine($"Signing Time (UTC): {signatureInfo.SignDate}");
            Console.WriteLine($"Certificate Subject: {signatureInfo.Certificate?.Subject}");
            Console.WriteLine($"Certificate Expiration: {signatureInfo.Certificate?.NotAfter}");
```

> **Practical tip:** بعض سلطات الشهادات تدمج فحص الإلغاء داخل خدمة التحقق. ومع ذلك، إظهار هذه المعلومات الإضافية قد يكون مفيدًا لسجلات التدقيق.

## مثال عملي كامل

بتجميع كل ما سبق، إليك البرنامج الكامل الجاهز للترجمة:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        const string pdfPath = "YOUR_DIRECTORY/signed.pdf";

        // Load the signed PDF document
        using (var pdfDocument = new Document(pdfPath))
        {
            // Create a signature handler for the document
            var signatureHandler = new PdfFileSignature(pdfDocument);

            // Get the name of the first digital signature in the PDF
            var signNames = signatureHandler.GetSignNames();

            if (signNames == null || signNames.Count == 0)
            {
                Console.WriteLine("No digital signatures found in the PDF.");
                return;
            }

            string signatureName = signNames[0];
            Console.WriteLine($"Found signature: {signatureName}");

            // Validate the signature using the certificate authority's validation service
            var validationUri = new Uri("https://ca.example.com/validate");
            bool isValid = signatureHandler.ValidateSignature(signatureName, validationUri);

            // Display whether the signature is valid
            Console.WriteLine(isValid ? "Valid" : "Invalid");

            // Optional: read extra signature details
            var signatureInfo = signatureHandler.GetSignatureInfo(signatureName);
            Console.WriteLine("\n--- Signature Details ---");
            Console.WriteLine($"Signer: {signatureInfo.Signer}");
            Console.WriteLine($"Signing Time (UTC): {signatureInfo.SignDate}");
            Console.WriteLine($"Certificate Subject: {signatureInfo.Certificate?.Subject}");
            Console.WriteLine($"Certificate Expiration: {signatureInfo.Certificate?.NotAfter}");
        }
    }
}
```

### النتيجة المتوقعة

إذا أكدت سلطة الشهادات صحة التوقيع، ستظهر لك رسالة مشابهة لـ:

```
Found signature: Signature1
Valid

--- Signature Details ---
Signer: Jane Doe
Signing Time (UTC): 2024-11-02 14:35:12Z
Certificate Subject: CN=Jane Doe, O=Acme Corp, C=US
Certificate Expiration: 2026-11-02 00:00:00Z
```

إذا تم تعديل التوقيع أو تم إلغاء الشهادة، سيطبع البرنامج `Invalid`.

## أسئلة شائعة وحالات خاصة

- **ماذا لو لم يحتوي PDF على توقيعات؟**  
  يتحقق الكود من `signNames.Count` ويخرج برفق مع رسالة ودية. يمكنك توسيع ذلك لإلقاء استثناء مخصص إذا تطلب سير عملك ذلك.

- **هل يمكنني التحقق من عدة توقيعات؟**  
  بالتأكيد. ضع منطق التحقق داخل حلقة `foreach (var name in signNames)` واجمع النتائج في قاموس.

- **ماذا لو كانت خدمة سلطة الشهادات متعطلة؟**  
  `ValidateSignature` يطرح استثناء `System.Net.WebException`. امسكه، سجّل الخطأ، وقرر ما إذا كنت ستعيد المحاولة أو تُعلّم PDF بأنه “قيد التحقق”.

- **هل خدمة التحقق دائمًا HTTPS؟**  
  تتطلب الواجهة `Uri`؛ رغم أن HTTP يعمل تقنيًا، يُنصح بشدة باستخدام HTTPS للأمان والامتثال.

- **هل أحتاج إلى الثقة بجذر شهادة سلطة الشهادات محليًا؟**  
  إذا كانت سلطة الشهادات تستخدم جذرًا موقّعًا ذاتيًا، أضفه إلى مخزن شهادات Windows أو زوده عبر التحميلات الزائدة لـ `ValidateSignature` التي تقبل مجموعة `X509Certificate2Collection` مخصصة.

## المكافأة: إنشاء PDF موقع تجريبي

إذا لم يكن لديك PDF موقع، يمكنك إنشاء واحد باستخدام ميزة التوقيع في Aspose.Pdf:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Security.Cryptography.X509Certificates;

// Create a simple PDF
var doc = new Document();
doc.Pages.Add();
doc.Save("unsigned.pdf");

// Load a certificate (pfx) – replace with your own path and password
var cert = new X509Certificate2("mycert.pfx", "password");

// Sign the PDF
var signer = new PdfFileSignature();
signer.BindPdf("unsigned.pdf");
signer.SignatureAppearance = new SignatureAppearance
{
    ContactInfo = "support@example.com",
    LocationInfo = "New York, USA",
    Reason = "Document approval"
};
signer.Sign(0, cert, "signed.pdf");
```

الآن لديك `signed.pdf` لتغذيته في درس التحقق أعلاه.

## الخاتمة

لقد **تحققنا من توقيع PDF** من البداية إلى النهاية، غطينا **كيفية التحقق من PDF** برمجيًا، عرضنا **التحقق من التوقيع الرقمي PDF** مع سلطة شهادات عن بُعد، أظهرنا نتائج **فحص توقيع PDF**، وحتى **قراءة بيانات التوقيع الرقمي PDF** للتدقيق. كل ذلك في تطبيق console واحد جاهز للنسخ واللصق يمكنك دمجه في سير عمل أكبر—سواء كنت تبني نظام إدارة مستندات، خط أنابيب فواتير إلكترونية، أو أداة تدقيق امتثال.

ما الخطوة التالية؟ جرّب التحقق من كل توقيع في PDF متعدد التوقيعات، أو اربط النتيجة بقاعدة بيانات للمعالجة الدفعية. يمكنك أيضًا استكشاف ميزة الطوابع الزمنية المدمجة في Aspose.Pdf وفحوصات CRL/OCSP لمزيد من الأمان.

هل لديك أسئلة إضافية أو تكامل مختلف مع سلطة شهادات؟ اترك تعليقًا، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}