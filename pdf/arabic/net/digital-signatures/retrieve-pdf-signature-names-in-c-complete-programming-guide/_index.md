---
category: general
date: 2026-02-25
description: استرجع أسماء توقيعات PDF في C# بسرعة. تعلّم كيفية قراءة توقيعات PDF،
  وإدراج توقيعات PDF، وعرض توقيعات PDF باستخدام Aspose.PDF.
draft: false
keywords:
- retrieve pdf signature names
- read pdf signatures
- list pdf signatures
- how to list signatures
- display pdf signatures
language: ar
og_description: استرجع أسماء توقيعات PDF في C# بسرعة. يوضح هذا الدليل كيفية قراءة
  توقيعات PDF، وإدراج توقيعات PDF وعرض توقيعات PDF مع أمثلة شفرة واضحة.
og_title: استرجاع أسماء توقيعات PDF في C# – دليل خطوة بخطوة
tags:
- pdf
- csharp
- aspnet
- digital-signature
title: استرجاع أسماء توقيعات PDF في C# – دليل برمجي كامل
url: /ar/net/digital-signatures/retrieve-pdf-signature-names-in-c-complete-programming-guide/
---

output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استرجاع أسماء توقيعات PDF في C# – دليل برمجي كامل

هل تحتاج إلى **استرجاع أسماء توقيعات PDF** من مستند موقّع؟ لست الوحيد الذي يحاول حل ذلك. في العديد من التطبيقات التي تتطلب الامتثال، عليك *قراءة توقيعات PDF* للتحقق من من وقع ماذا، وأسرع طريقة في .NET هي سرد حقول التوقيع باستخدام Aspose.PDF.  

في هذا الدرس سنستعرض مثالًا واقعيًا **يسترجع أسماء توقيعات PDF**، يوضح لك كيفية **سرد توقيعات PDF**، وحتى يوضح كيفية **عرض توقيعات PDF** على وحدة التحكم. في النهاية ستحصل على مقتطف مستقل يمكنك إدراجه في أي مشروع C#—دون الحاجة إلى روابط “انظر الوثائق” المتبقية.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا على .NET Framework 4.6+).  
- حزمة NuGet **Aspose.PDF for .NET** (`Aspose.PDF`) – المكتبة التي توفر الفئات `Document` و `PdfFileSignature`.  
- ملف **PDF موقّع** يمكنك الإشارة إليه (سنسميه `signed.pdf`).  
- أي بيئة تطوير تفضّلها (Visual Studio، Rider، VS Code—اختيارك).

> **نصيحة احترافية:** إذا لم يكن لديك PDF موقّع جاهز، يمكنك إنشاء واحد باستخدام Adobe Acrobat أو استخدام واجهة التوقيع الخاصة بـ Aspose؛ منطق الاستخراج يبقى نفسه.

## نظرة عامة على العملية

1. **فتح** مستند PDF بأمان داخل كتلة `using`.  
2. **إنشاء** كائن `PdfFileSignature`، الواجهة التي تعرف كيفية التعامل مع التوقيعات.  
3. **استدعاء** `GetSignatureNames()` لجلب كل معرف توقيع.  
4. **التكرار** على المجموعة و**عرض** كل اسم على وحدة التحكم.

هذا هو سير العمل بالكامل—لا شيء أكثر ولا شيء أقل. لنبدأ في شرح كل خطوة.

---

## استرجاع أسماء توقيعات PDF – خطوة بخطوة

البرنامج **الكامل القابل للتنفيذ** أدناه. يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد والضغط على **F5**.

```csharp
// ---------------------------------------------------------------
// Retrieve PDF signature names with Aspose.PDF for .NET
// ---------------------------------------------------------------
using System;
using Aspose.Pdf;               // Core PDF classes
using Aspose.Pdf.Facades;       // Signature façade

namespace PdfSignatureDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 1: Open the signed PDF document
            // Replace the path with your actual file location.
            using (var pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf"))
            {
                // 👉 Step 2: Create a signature handler for the document
                using (var pdfSignature = new PdfFileSignature(pdfDocument))
                {
                    // 👉 Step 3: Retrieve all signature names present in the PDF
                    var signatureNames = pdfSignature.GetSignatureNames();

                    // 👉 Step 4: Output each signature name to the console
                    Console.WriteLine("=== PDF Signature Names ===");
                    foreach (var signatureName in signatureNames)
                    {
                        Console.WriteLine($"- {signatureName}");
                    }

                    // Edge case handling: no signatures found
                    if (signatureNames.Count == 0)
                    {
                        Console.WriteLine("No signatures were detected in this PDF.");
                    }
                }
            }

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

### شرح كل جزء

| الخطوة | ما يحدث | لماذا يهم |
|--------|----------|-----------|
| **Step 1** | `new Document("…/signed.pdf")` يحمل الملف في الذاكرة. | الفتح داخل `using` يضمن تحرير مقبض الملف، مما يمنع مشاكل قفل الملف على Windows. |
| **Step 2** | `PdfFileSignature` يلتف حول المستند ويكشف عن طرق متعلقة بالتوقيع. | هذه الواجهة تُجرد تفاصيل PDF الداخلية منخفضة المستوى، مما يسمح لك **بقراءة توقيعات PDF** بند واحد فقط. |
| **Step 3** | `GetSignatureNames()` تُعيد `StringCollection` تحتوي على جميع معرفات حقول التوقيع. | المجموعة تحتوي على *الأسماء* التي تحتاجها عندما تريد لاحقًا **سرد توقيعات PDF** أو التحقق من توقيع معين. |
| **Step 4** | حلقة `foreach` بسيطة تطبع كل اسم. | عرض الأسماء يجعل عملية التصحيح سهلة وتلبي متطلبات “**عرض توقيعات PDF**”. |

#### حالات خاصة ونصائح

- **PDF مشفر** – إذا كان ملف PDF محميًا بكلمة مرور، مرّر كلمة المرور إلى مُنشئ `Document`: `new Document(path, new LoadOptions { Password = "secret" })`.  
- **عدم وجود توقيعات** – العينة تتحقق بالفعل من `signatureNames.Count == 0` وتُعلم المستخدم.  
- **ملفات PDF الكبيرة** – تحميل ملف ضخم قد يستهلك الذاكرة؛ فكر في استخدام `LoadOptions` مع `MemoryUsageSetting` للقراءة المتدفقة بدلاً من التحميل الكامل.  

---

## قراءة توقيعات PDF مع Aspose.PDF

إذا كنت تتساءل *كيف تقرأ توقيعات PDF* بخلاف أسمائها فقط، فإن الفئة نفسها `PdfFileSignature` يمكنها إعطاؤك **تفاصيل التوقيع** (اسم الموقّع، وقت التوقيع، الشهادة). إليك مقتطفًا سريعًا:

```csharp
foreach (var name in signatureNames)
{
    // Retrieve the signature object for deeper inspection
    var signature = pdfSignature.GetSignature(name);
    Console.WriteLine($"Signature: {name}");
    Console.WriteLine($"  Signer: {signature.Signer}");
    Console.WriteLine($"  Signing Time: {signature.SignTime}");
    Console.WriteLine($"  Reason: {signature.Reason}");
}
```

> **لماذا هذا مهم:** في سجلات التدقيق تحتاج غالبًا إلى أكثر من مجرد اسم الحقل؛ تحتاج إلى **من**، **متى**، و**لماذا**. هذه المعلومات الإضافية تساعدك على بناء تقارير امتثال دون الحاجة إلى مكتبات إضافية.

---

## سرد توقيعات PDF بأمان – الأخطاء الشائعة

عند **سرد توقيعات PDF**، احرص على مراعاة هذه النقاط:

1. **تكرار أسماء الحقول** – قد تحتوي بعض ملفات PDF على نفس الاسم المنطقي في صفحات متعددة. `GetSignatureNames()` تُعيد كل معرف فريد مرة واحدة فقط، لذا لن تُحسب مرتين.  
2. **التوقيعات المنفصلة** – يمكن أن يوجد حقل توقيع دون توقيع تشفيري فعلي مرفق. في هذه الحالة تكون `signature.IsSigned` **false**.  
3. **توافق الإصدارات** – قد تخزن ملفات PDF القديمة (قبل 1.5) التوقيعات بطريقة غير معيارية. Aspose.PDF يتعامل مع معظم الحالات، لكن يفضَّل اختبار الملفات القديمة.  

---

## عرض توقيعات PDF – جعل المخرجات صديقة للمستخدم

الإخراج على وحدة التحكم أعلاه عملي، لكن قد ترغب في **جدول جميل** لتطبيقات الواجهة. إليك مساعدًا صغيرًا يستخدم تنسيق `Console.WriteLine`:

```csharp
Console.WriteLine("\n{0,-30} {1,-20} {2,-25}", "Signature Name", "Signer", "Signing Time");
Console.WriteLine(new string('-', 80));

foreach (var name in signatureNames)
{
    var sig = pdfSignature.GetSignature(name);
    Console.WriteLine("{0,-30} {1,-20} {2,-25}",
        name,
        sig.Signer ?? "N/A",
        sig.SignTime?.ToString("u") ?? "N/A");
}
```

الجدول الناتج:

```
Signature Name                 Signer               Signing Time             
--------------------------------------------------------------------------------
Signature1                     Alice                2024-11-03 14:22:01Z     
Signature2                     Bob                  2024-11-04 09:15:45Z     
```

هذه طريقة نظيفة **لعرض توقيعات PDF** في وحدة تحكم أو ملف سجل.

---

## ملخص المثال الكامل العامل

بجمع كل ما سبق، البرنامج النهائي يبدو هكذا (مع الإدراج الاختياري للتفاصيل):

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace PdfSignatureDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            using (var pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf"))
            using (var pdfSignature = new PdfFileSignature(pdfDocument))
            {
                var signatureNames = pdfSignature.GetSignatureNames();

                Console.WriteLine("=== PDF Signature Names ===");
                foreach (var name in signatureNames)
                    Console.WriteLine($"- {name}");

                if (signatureNames.Count == 0)
                {
                    Console.WriteLine("No signatures were detected in this PDF.");
                }
                else
                {
                    // Detailed listing (optional)
                    Console.WriteLine("\n{0,-30} {1,-20} {2,-25}", "Signature Name", "Signer", "Signing Time");
                    Console.WriteLine(new string('-', 80));

                    foreach (var name in signatureNames)
                    {
                        var sig = pdfSignature.GetSignature(name);
                        Console.WriteLine("{0,-30} {1,-20} {2,-25}",
                            name,
                            sig.Signer ?? "N/A",
                            sig.SignTime?.ToString("u") ?? "N/A");
                    }
                }
            }

            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**المخرجات المتوقعة** (افترض وجود توقيعين):

```
=== PDF Signature Names ===
- Signature1
- Signature2

Signature Name                 Signer               Signing Time             
--------------------------------------------------------------------------------
Signature1                     Alice                2024-11-03 14:22:01Z     
Signature2                     Bob                  2024-11-04 09:15:45Z     
```

إذا كان ملف PDF **لا يحتوي على توقيعات**، سترى:

```
=== PDF Signature Names ===
No signatures were detected in this PDF.
```

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات PDF موقعة باستخدام PAdES؟**  
ج: نعم. Aspose.PDF يتحقق من كل من توقيعات PKCS#7 الكلاسيكية وتوقيعات PAdES. كائن `GetSignature` يُظهر سلسلة الشهادات للمزيد من التحقق.

**س: ماذا لو كان ملف PDF محميًا بكلمة مرور؟**  
ج: مرّر كلمة المرور عبر `LoadOptions` عند إنشاء كائن `Document`:

```csharp
var loadOpts = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("signed.pdf", loadOpts);
```

**س: هل يمكنني استرجاع التوقيعات من تدفق (Stream) بدلاً من ملف؟**  
ج: بالتأكيد. استخدم التحميل الزائد `new Document(Stream)` ولف التدفق داخل كتلة `using`.

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن يمكنك **استرجاع توقيع PDF** 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}