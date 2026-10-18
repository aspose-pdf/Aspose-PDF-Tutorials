---
category: general
date: 2026-03-03
description: تحقق من التوقيعات في ملف PDF بسرعة باستخدام Aspose.PDF في C#. تعلّم كيفية
  الحصول على التوقيعات، استخراج التوقيعات الرقمية من PDF، وقائمة التوقيعات في بضع
  أسطر فقط.
draft: false
keywords:
- check pdf for signatures
- how to get signatures
- extract digital signatures pdf
- how to list signatures
language: ar
og_description: تحقق من وجود توقيعات في ملفات PDF باستخدام C# مع Aspose.PDF. يوضح
  هذا الدرس كيفية الحصول على التوقيعات، استخراج التوقيعات الرقمية من PDF، وقائمة التوقيعات
  بكفاءة.
og_title: تحقق من PDF للتوقيعات – دليل C#
tags:
- Aspose.PDF
- C#
- Digital Signature
title: تحقق من وجود توقيعات في PDF – كيفية سرد التوقيعات في C# باستخدام Aspose.PDF
url: /ar/net/programming-with-security-and-signatures/check-pdf-for-signatures-how-to-list-signatures-in-c-with-as/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# فحص PDF للتوقيعات – دليل C# الكامل

هل احتجت يومًا إلى **فحص PDF للتوقيعات** لكن لم تكن متأكدًا من أي استدعاء API سيظهرها فعليًا؟ لست وحدك. يواجه العديد من المطورين عقبة عندما يصل عقد أو تقرير يحتوي على توقيع رقمي غير معروف ويحتاجون إلى التحقق من وجوده برمجيًا.  

في هذا الدرس سنستعرض حلًا عمليًا باستخدام Aspose.PDF for .NET. بحلول النهاية ستعرف **كيفية الحصول على التوقيعات**، وكيفية **استخراج التوقيعات الرقمية من ملفات PDF**، وبالتحديد **كيفية سرد التوقيعات** الموجودة داخل مستند PDF—كل ذلك باستخدام كود C# نظيف وقابل للتنفيذ.

سنعرض كل شيء بدءًا من حزمة NuGet المطلوبة إلى التعامل مع الحالات الخاصة مثل PDF لا يحتوي على أي توقيعات. لا مراجع خارجية، مجرد إجابة مستقلة يمكنك نسخها ولصقها في مشروعك ورؤية النتائج فورًا.

---

## ما ستتعلمه

- تحميل مستند PDF بأمان.
- إنشاء كائن `PdfFileSignature` للوصول إلى بيانات التوقيع.
- استرجاع وتكرار قائمة أسماء التوقيعات.
- طباعة النتائج إلى وحدة التحكم (أو أي واجهة مستخدم تفضلها).
- نصائح للتعامل مع ملفات PDF غير موقعة وحل المشكلات الشائعة.

**المتطلبات المسبقة** – تحتاج إلى .NET 6 (أو أي إصدار حديث من .NET Framework) ومكتبة Aspose.PDF for .NET المثبتة عبر NuGet (`Install-Package Aspose.Pdf`). معرفة أساسية بـ C# وتطبيقات وحدة التحكم كافية؛ سنشرح كل سطر.

![مثال فحص PDF للتوقيعات](image.png "فحص PDF للتوقيعات")

*نص بديل: فحص PDF للتوقيعات – مخرجات وحدة التحكم تُظهر أسماء التوقيعات*

## فحص PDF للتوقيعات – دليل خطوة بخطوة

فيما يلي نقسم العملية إلى أربع خطوات واضحة. كل خطوة تتضمن كتلة كود، شرحًا قصيرًا عن **سبب** أهميتها، ونصيحة قد تجدها مفيدة.

### الخطوة 1: تحميل مستند PDF

قبل أن تتمكن من فحص ملف للتوقيعات، يجب فتحه كـ `Aspose.Pdf.Document`. استخدام جملة `using` يضمن تحرير مقبض الملف على الفور.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your signed PDF.
        const string pdfPath = @"C:\MyDocuments\signed.pdf";

        // Step 1: Open the PDF document that may contain signatures
        using (var pdfDocument = new Document(pdfPath))
        {
            // The rest of the workflow goes here...
        }
    }
}
```

**لماذا هذا مهم:** فتح المستند داخل كتلة `using` يضمن التخلص تلقائيًا من الموارد غير المُدارة (تدفقات الملفات، المقابض الأصلية)، مما يمنع مشاكل قفل الملف لاحقًا.

**نصيحة احترافية:** إذا كنت تتعامل مع ملفات PDF كبيرة، فكر في ضبط `pdfDocument.OptimizeMemoryUsage = true;` للحفاظ على استهلاك الذاكرة منخفضًا.

---

### الخطوة 2: تهيئة واجهة PdfFileSignature

تقوم Aspose بفصل معالجة PDF عالية المستوى عن عمليات التوقيع المحددة. فئة `PdfFileSignature` هي البوابة لقراءة والتحقق من التوقيعات الرقمية.

```csharp
// Step 2: Create a PdfFileSignature object to access signature information
var pdfSignature = new PdfFileSignature(pdfDocument);
```

**لماذا هذا مهم:** الواجهة تُجرد الفحوصات التشفيرية منخفضة المستوى، وتُظهر طرقًا بسيطة مثل `GetSignatureNames()`. هذا يبقي الكود نظيفًا ومركزًا على منطق الأعمال.

**حالة خاصة:** إذا كان PDF محميًا بكلمة مرور، فستحتاج إلى توفير كلمة المرور قبل إنشاء الواجهة:

```csharp
pdfDocument.Decrypt("yourPassword");
var pdfSignature = new PdfFileSignature(pdfDocument);
```

---

### الخطوة 3: استرجاع قائمة أسماء التوقيعات

الآن نطلب من المكتبة أسماء جميع التوقيعات المدمجة. تُعيد الطريقة `IList<string>` قد تكون فارغة.

```csharp
// Step 3: Retrieve the list of signature names present in the document
IList<string> signatureNames = pdfSignature.GetSignatureNames(); // IList<string>
```

**لماذا هذا مهم:** *اسم* التوقيع غالبًا ما يكون المعرف الذي تحتاج لعرضه للمستخدمين أو تسجيله لسجلات التدقيق. قد يكون بريد الموقّع، طابع زمني، أو تسمية مخصصة تم تعيينها أثناء التوقيع.

**مشكلة شائعة:** بعض ملفات PDF تحتوي على *تعدد* التوقيعات (مثل سلسلة من الموافقات). تعامل دائمًا مع النتيجة كمجموعة، حتى لو كنت تتوقع توقيعًا واحدًا.

---

### الخطوة 4: طباعة كل اسم توقيع

أخيرًا، نطبع الأسماء إلى وحدة التحكم. يمكنك بسهولة استبدال `Console.WriteLine` بمسجل أو عنصر واجهة مستخدم.

```csharp
// Step 4: Output each signature name to the console (if any)
if (signatureNames.Count == 0)
{
    Console.WriteLine("No digital signatures were found in the PDF.");
}
else
{
    Console.WriteLine("Signatures detected:");
    signatureNames.ForEach(Console.WriteLine);
}
```

**لماذا هذا مهم:** تقديم ملاحظات يُخبر المستدعي ما إذا كان PDF موقّعًا أم لا. في بيئة الإنتاج قد ترفع استثناءً أو تُعيد كائن نتيجة بدلاً من الكتابة إلى وحدة التحكم.

**المخرجات المتوقعة** (مثال عندما يوجد توقيعان):

```
Signatures detected:
JohnDoe@example.com
FinanceDept_Approval
```

إذا كان الملف لا يحتوي على توقيعات، سترى:

```
No digital signatures were found in the PDF.
```

---

## كيفية الحصول على التوقيعات من PDF – خيارات إضافية

طريقة `GetSignatureNames()` رائعة للحصول على نظرة سريعة، لكن Aspose.PDF يتيح لك أيضًا استرجاع كائن `Signature` الكامل، الذي يحتوي على تفاصيل الشهادة، وقت التوقيع، وحالة التحقق.

```csharp
// Example: Get detailed signature objects
IList<Signature> signatures = pdfSignature.GetSignatures(); // requires Aspose.Pdf.Facades

foreach (var sig in signatures)
{
    Console.WriteLine($"Name: {sig.SignatureName}");
    Console.WriteLine($"Signed on: {sig.SigningTime}");
    Console.WriteLine($"Valid: {sig.IsValid}");
    Console.WriteLine("---");
}
```

**متى تستخدم هذا:** إذا كانت متطلبات الامتثال تتطلب إثبات وقت التوقيع أو التحقق من سلسلة الشهادات، استخرج الكائنات الكاملة بدلاً من الأسماء فقط.

---

## استخراج التوقيعات الرقمية من PDF – حفظ تدفق التوقيع

أحيانًا تحتاج إلى بايتات التوقيع الخام (مثلاً لتضمينها في قاعدة بيانات). تسمح لك Aspose باستخراج تدفق التوقيع:

```csharp
// Save each signature as a separate file
int index = 1;
foreach (var sig in signatures)
{
    string outPath = $@"C:\Signatures\signature{index}.p7s";
    pdfSignature.ExtractSignature(sig.SignatureName, outPath);
    Console.WriteLine($"Extracted {sig.SignatureName} to {outPath}");
    index++;
}
```

**لماذا تقوم بذلك:** ملف `.p7s` هو حاوية PKCS#7 يمكن التحقق منها باستخدام أدوات خارجية مثل OpenSSL، مما يمنحك سجل تدقيق مستقل عن PDF الأصلي.

---

## كيفية سرد التوقيعات برمجيًا – مشكلات شائعة

| مشكلة | العَرَض | الحل |
|---------|---------|-----|
| PDF محمي بكلمة مرور | `GetSignatureNames()` تُعيد قائمة فارغة | فك تشفير المستند أولاً (`pdfDocument.Decrypt(password)`). |
| استخدام نسخة قديمة من Aspose.PDF | قد لا تتوفر طريقة `GetSignatureNames()` في الـ API | التحديث عبر NuGet إلى أحدث إصدار ثابت. |
| أسماء التوقيعات تحتوي على مسافات | مخرجات وحدة التحكم تبدو غير مرتبة | قم بقطع المسافات: `sig.Trim()` قبل الطباعة. |
| ملفات PDF الكبيرة تسبب ضغطًا على الذاكرة | OutOfMemoryException | تمكين `pdfDocument.OptimizeMemoryUsage = true;`. |

---

## مثال كامل يعمل

انسخ الكود أدناه إلى مشروع **Console App** جديد. عدّل المتغيّر `pdfPath` ليشير إلى ملف PDF الخاص بك، شغّله، وسترى أسماء التوقيعات مطبوعة.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        const string pdfPath = @"C:\MyDocuments\signed.pdf";

        // Open the document (ensures proper disposal)
        using (var pdfDocument = new Document(pdfPath))
        {
            // If the PDF is encrypted, uncomment the next line and provide the password
            // pdfDocument.Decrypt("yourPassword");

            // Access signature information
            var pdfSignature = new PdfFileSignature(pdfDocument);

            // Retrieve all signature names
            IList<string> signatureNames = pdfSignature.GetSignatureNames();

            // Display results
            if (signatureNames.Count == 0)
            {
                Console.WriteLine("No digital signatures were found in the PDF.");
            }
            else
            {
                Console.WriteLine("Signatures detected:");
                signatureNames.ForEach(Console.WriteLine);
            }
        }

        // Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

تشغيل هذا البرنامج ينتج قائمة واضحة من التوقيعات—أو رسالة ودية إذا لم توجد أي توقيعات. الآن يمكنك **فحص PDF للتوقيعات** بثقة، سواء كنت تبني خدمة للتحقق من المستندات، أو سير عمل آلي، أو سكريبت إداري بسيط.

---

## الخلاصة

لقد غطينا كل ما تحتاجه **لفحص PDF للتوقيعات** باستخدام Aspose.PDF في C#. من تحميل الملف، إنشاء واجهة `PdfFileSignature`، استرجاع أسماء التوقيعات، إلى التعامل مع ملفات PDF غير موقعة، لديك الآن حل كامل جاهز للنسخ واللصق.

إذا رغبت في التعمق أكثر، استكشف واجهة **كيفية الحصول على التوقيعات** للحصول على تفاصيل الشهادة، أو روتين **استخراج التوقيعات الرقمية من PDF** لتخزين البايتات الخام للتوقيع. كلا التقنيتين تتكاملان بسلاسة مع تدفق **كيفية سرد التوقيعات** الأساسي الذي عرضناه.

الخطوات التالية قد تشمل:

- التحقق من سلسلة شهادات كل توقيع مقابل مخزن الجذور الموثوق.
- بناء نقطة نهاية REST تستقبل ملفات PDF وتعيد مصفوفة JSON بأسماء التوقيعات.
- دمج هذه المنطق مع عرض PDF لتسليط الضوء على الحقول الموقعة في واجهة المستخدم.

جرّبه، عدّل الكود وفقًا لسيناريوك الخاص، ودع التوقيعات تتحدث عن نفسها. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}