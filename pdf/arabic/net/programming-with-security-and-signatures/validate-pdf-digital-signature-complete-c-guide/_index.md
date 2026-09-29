---
category: general
date: 2026-03-29
description: تحقق من صحة التوقيع الرقمي لملف PDF بسرعة. تعلم كيفية التحقق من توقيع
  PDF، وفحص حالة توقيع PDF، واكتشاف ملفات PDF التي تم التلاعب بها باستخدام Aspose.Pdf
  في C#.
draft: false
keywords:
- validate pdf digital signature
- how to verify pdf signature
- check pdf signature
- verify pdf signature
- detect tampered pdf
language: ar
og_description: تحقق من صحة التوقيع الرقمي لملف PDF باستخدام C#. يوضح هذا الدرس كيفية
  التحقق من توقيع PDF، وفحص سلامة توقيع PDF، واكتشاف ملفات PDF التي تم تعديلها باستخدام
  Aspose.Pdf.
og_title: التحقق من التوقيع الرقمي لملف PDF – دليل C# الكامل
tags:
- C#
- Aspose.Pdf
- PDF Security
title: تحقق من صحة التوقيع الرقمي لملف PDF – دليل C# الكامل
url: /ar/net/programming-with-security-and-signatures/validate-pdf-digital-signature-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التحقق من التوقيع الرقمي لملف PDF – دليل C# كامل

هل تساءلت يومًا **كيف تتحقق من توقيع PDF** دون أن تفقد أعصابك؟ ربما استلمت عقدًا، فتحته، وتحتاج إلى أن تكون متأكدًا بنسبة 100 % أنه لم يتم تعديل محتواه. الخبر السار هو أنك لا تحتاج إلى مختبر جنائي—مجرد بضع أسطر من C# و Aspose.Pdf يمكنها **التحقق من التوقيع الرقمي لملف PDF** في لحظات.

في هذا الدرس سنستعرض كل ما تحتاج معرفته: من تثبيت المكتبة إلى تفسير النتيجة، وحتى التعامل مع الحالات الخاصة مثل وجود توقيعات متعددة أو ملف تالف. بنهاية الدرس، ستتمكن من **فحص حالة توقيع PDF** برمجيًا و**اكتشاف ملفات PDF المعدلة** قبل أن تسبب مشاكل.

## ما الذي ستحتاجه

- **.NET 6.0 أو أحدث** (الكود يعمل أيضًا على .NET Framework، لكن .NET 6 هو الخيار المثالي).
- **Aspose.Pdf for .NET** – يمكنك الحصول عليها من NuGet (`Install-Package Aspose.Pdf`).
- ملف **PDF موقع** تريد اختباره. إذا لم يكن لديك واحد، أنشئ مستندًا موقعًا بسيطًا باستخدام Adobe Acrobat أو أي برنامج توقيع PDF.

> نصيحة احترافية: احتفظ بملفات PDF خارج مجلد جذر المشروع؛ مسار نسبي مثل `./Samples/signed.pdf` يعمل جيدًا ويتجنب الالتزام غير المقصود بملفات سرية.

## التنفيذ خطوة بخطوة

نقسم الحل إلى أجزاء منطقية. كل جزء يحصل على عنوان H2 خاص به—أحدها يحتوي على الكلمة المفتاحية الأساسية، لتلبية قاعدة SEO.

### ## الخطوة 1 – تثبيت وإضافة مرجع Aspose.Pdf

أولًا، أضف حزمة NuGet إلى مشروعك:

```powershell
dotnet add package Aspose.Pdf
```

أو، إذا كنت تستخدم Package Manager Console:

```powershell
Install-Package Aspose.Pdf
```

بعد تثبيت الحزمة، سيضيف Visual Studio تلقائيًا مساحة الاسم `using Aspose.Pdf;`. لا حاجة لتعامل إضافي مع ملفات DLL.

### ## الخطوة 2 – تحميل مستند PDF الموقع

الآن نفتح الملف فعليًا. يضمن بيان `using` التخلص الصحيح من المستند، وهو أمر مهم خاصةً للملفات الكبيرة.

```csharp
using System;
using Aspose.Pdf;

class PdfSignatureValidator
{
    static void Main()
    {
        // Step 2: Load the signed PDF document
        var pdfPath = @"./Samples/signed.pdf";   // adjust the path as needed
        using var pdfDocument = new Document(pdfPath);
```

> **لماذا هذا مهم:** تحميل المستند يمنحنا الوصول إلى كائن `DigitalSignatureInfo`، وهو نقطة الدخول لجميع الاستعلامات المتعلقة بالتوقيع.

### ## الخطوة 3 – استرجاع معلومات التوقيع الرقمي

Aspose.Pdf يلف تفاصيل PKI منخفضة المستوى في واجهة برمجة تطبيقات سهلة. احصل على الخاصية `DigitalSignatureInfo` وستحصل على كل ما تحتاجه لـ **فحص صحة توقيع PDF**.

```csharp
        // Step 3: Retrieve digital signature information
        var signatureInfo = pdfDocument.DigitalSignatureInfo;
```

إذا كان PDF يحتوي على توقيعات متعددة، فإن `signatureInfo` يجمعها، مكشفًا عن خصائص مثل `Count` و `Certificates` و `IsCompromised`. بالنسبة لملف يحتوي على توقيع واحد، ستكون تلك المجموعات تحتوي على عنصر واحد فقط.

### ## الخطوة 4 – تحديد ما إذا كان التوقيع مخترقًا

علامة `IsCompromised` تخبرك إذا ما تم تعديل المستند **بعد** توقيعه. قيمة `true` تعني أن PDF تم العبث به—وهذا بالضبط ما نريد **اكتشاف PDF معدل**.

```csharp
        // Step 4: Determine whether the signature has been compromised (e.g., tampered)
        bool isCompromised = signatureInfo.IsCompromised;
```

إذا كنت بحاجة إلى **التحقق من توقيع PDF** بشكل أعمق (مثل التحقق من سلسلة الشهادات)، يمكنك أيضًا فحص `signatureInfo.Certificates` واستدعاء `Validate()` على كلٍ منها. بالنسبة لمعظم الاستخدامات، `IsCompromised` يكفي.

### ## الخطوة 5 – إخراج النتيجة إلى وحدة التحكم

أخيرًا، أخبر المستخدم بما حدث. سنطبع رسالة ودية ونُعيد رمز خروج مناسب لسكربتات الأتمتة.

```csharp
        // Step 5: Output the result
        Console.WriteLine($"Signature compromised: {isCompromised}");

        // Optional: return non‑zero exit code if compromised (useful for CI pipelines)
        Environment.Exit(isCompromised ? 1 : 0);
    }
}
```

#### النتيجة المتوقعة

```
Signature compromised: False
```

إذا قمت بتعديل PDF عمدًا (مثلاً بإضافة حرف عشوائي)، ستتغير النتيجة إلى `True`. هذه هي اللحظة التي تعرف فيها أن سلامة المستند قد انكسرت.

### ## التعامل مع الحالات الخاصة والمشكلات الشائعة

#### 1. توقيعات متعددة

عندما يحتوي PDF على أكثر من موقع، يعكس `IsCompromised` الحالة *الكلية*—إذا كان **أي** توقيع مكسور، تصبح العلامة `true`. لتحديد أي موقع هو المسبب:

```csharp
foreach (var sig in signatureInfo.Signatures)
{
    Console.WriteLine($"Signer: {sig.SignerName}, Compromised: {sig.IsCompromised}");
}
```

#### 2. توقيع مفقود

إذا لم يكن PDF موقعًا أصلاً، فإن `signatureInfo.Count` سيكون `0`. يجب الحذر من الشعور بالأمان الزائف:

```csharp
if (signatureInfo.Count == 0)
{
    Console.WriteLine("No digital signatures found in the document.");
    Environment.Exit(2);
}
```

#### 3. ملف PDF تالف

ملف تالف يرمي استثناء `PdfException`. غلف منطق التحميل بكتلة try‑catch لتقديم رسالة خطأ واضحة:

```csharp
try
{
    using var pdfDocument = new Document(pdfPath);
    // ...rest of the code
}
catch (PdfException ex)
{
    Console.WriteLine($"Failed to open PDF: {ex.Message}");
    Environment.Exit(3);
}
```

#### 4. التحقق من الشهادة (متقدم)

إذا كنت بحاجة إلى التأكد من أن شهادة التوقيع لا تزال صالحة (غير مُسحبّة، ضمن فترة صلاحيتها)، يمكنك استدعاء:

```csharp
bool certValid = signatureInfo.Signatures[0].Certificate.Validate();
Console.WriteLine($"Certificate valid: {certValid}");
```

هذه الخطوة تنقلك من مجرد **فحص توقيع PDF** إلى سير عمل كامل لـ **كيفية التحقق من توقيع PDF**.

### ## مثال كامل يعمل

بدمج كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using Aspose.Pdf;

class PdfSignatureValidator
{
    static void Main()
    {
        var pdfPath = @"./Samples/signed.pdf";

        try
        {
            using var pdfDocument = new Document(pdfPath);
            var signatureInfo = pdfDocument.DigitalSignatureInfo;

            if (signatureInfo.Count == 0)
            {
                Console.WriteLine("No digital signatures found in the document.");
                Environment.Exit(2);
                return;
            }

            bool isCompromised = signatureInfo.IsCompromised;
            Console.WriteLine($"Signature compromised: {isCompromised}");

            // Optional detailed per‑signer report
            for (int i = 0; i < signatureInfo.Count; i++)
            {
                var sig = signatureInfo.Signatures[i];
                Console.WriteLine($"Signer {i + 1}: {sig.SignerName}");
                Console.WriteLine($"  Compromised: {sig.IsCompromised}");
                Console.WriteLine($"  Certificate valid: {sig.Certificate.Validate()}");
            }

            Environment.Exit(isCompromised ? 1 : 0);
        }
        catch (PdfException ex)
        {
            Console.WriteLine($"Failed to open PDF: {ex.Message}");
            Environment.Exit(3);
        }
    }
}
```

شغّل البرنامج من سطر الأوامر:

```bash
dotnet run --project PdfSignatureValidator.csproj
```

ستظهر لك تقرير واضح يوضح ما إذا كان PDF سليمًا، ومن هو (الموقعون) المشاركون، وما إذا كانت شهاداتهم لا تزال موثوقة.

## نظرة بصرية عامة

فيما يلي مخطط سريع يوضح التدفق من **تحميل PDF** إلى **إخراج نتيجة التحقق**. إنه مرجع مفيد عندما تقوم بتصميم بنية خط أنابيب معالجة مستندات أكبر.

![validate pdf digital signature workflow diagram](image.png "Diagram showing PDF load → DigitalSignatureInfo → IsCompromised check")

*نص بديل: مخطط سير عمل التحقق من التوقيع الرقمي لملف PDF*

## الخلاصة

لقد غطينا الآن **حلًا كاملاً من البداية إلى النهاية للتحقق من التوقيع الرقمي لملف PDF** باستخدام Aspose.Pdf في C#. النقاط الرئيسية:

- تحميل PDF باستخدام `Document`.
- استخراج `DigitalSignatureInfo` وفحص `IsCompromised` لـ **اكتشاف PDF معدل**.
- التعامل مع توقيعات متعددة، توقيعات مفقودة، وملفات تالفة بشكل مرن.
- اختيارياً، التحقق من شهادة التوقيع للحصول على قائمة كاملة لـ **كيفية التحقق من توقيع PDF**.

من هنا يمكنك توسيع المنطق—تخزين نتائج التحقق في قاعدة بيانات، رفض تحميلات غير موقعة في واجهة ويب API، أو دمجه مع نظام إدارة مستندات. إذا كنت مهتمًا بميزات أمان PDF أخرى، استكشف **فحص طوابع توقيع PDF**، **إضافة توقيع جديد**، أو **تشفير ملفات PDF**.

هل لديك أسئلة حول الحالات الخاصة، أو تريد معرفة كيفية **التحقق من توقيع PDF** باستخدام مكتبة أخرى مثل iText 7؟ اترك تعليقًا أدناه، ولنستمر في النقاش. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}