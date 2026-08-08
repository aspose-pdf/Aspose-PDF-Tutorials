---
category: general
date: 2026-04-02
description: تحقق من توقيع PDF بسرعة وتعلم كيفية إضافة ترقيم باتس باستخدام Aspose.Pdf.
  يتضمن كودًا خطوة بخطوة ونصائح.
draft: false
keywords:
- verify pdf signature
- add bates numbering
- how to verify signature
- how to add bates
- check pdf signature
language: ar
og_description: تحقق من توقيع PDF بسرعة وتعلم كيفية إضافة ترقيم بايتس باستخدام Aspose.Pdf.
  اتبع المثال الكامل وتجنب الأخطاء الشائعة.
og_title: تحقق من توقيع PDF وإضافة ترقيم بيتس – دليل C# الكامل
tags:
- Aspose.Pdf
- C#
- Digital Signature
- Document Automation
title: تحقق من توقيع PDF وإضافة ترقيم بايتس – دليل C# الكامل
url: /ar/net/digital-signatures/verify-pdf-signature-and-add-bates-numbering-complete-c-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحقق من توقيع PDF وإضافة ترقيم Bates – دليل C# الكامل

هل احتجت يومًا إلى **التحقق من توقيع PDF** قبل إرسال العقد، لكن لم تكن متأكدًا من أي استدعاء API تستخدمه؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند التعامل مع ملفات PDF القانونية. في هذا الدرس سنستعرض خطوة بخطوة **كيفية التحقق من توقيع PDF** باستخدام Aspose.Pdf ثم نوضح **كيفية إضافة ترقيم Bates** حتى تظل ملفاتك جاهزة للتدقيق.  

سنناقش أيضًا **كيفية التحقق من التوقيع** برمجيًا، ونغطي **كيفية إضافة Bates** في خطوة واحدة، ونشرح نتائج **check pdf signature** حتى يمكنك الوثوق بالمخرجات. في النهاية ستحصل على تطبيق C# Console يعمل على إنجاز المهمتين—بدون غموض، فقط كود واضح.

---

## ما الذي ستحتاجه

- **.NET 6.0** أو أحدث (المثال يعمل أيضًا مع .NET Framework 4.7+)  
- حزمة **Aspose.Pdf for .NET** عبر NuGet (الإصدار 23.11 أو أحدث)  
- ملف PDF موقّع (`signed.pdf`) تريد التحقق منه  
- ملف PDF عادي (`input.pdf`) سيُضاف إليه ترقيم Bates  

إذا كان لديك هذه المتطلبات، فأنت جاهز للبدء. لا تحتاج إلى أي SDK إضافي، ولا ملفات إعداد مخفية.

---

## الخطوة 1: إعداد المشروع

ابدأ بإنشاء مشروع Console:

```bash
dotnet new console -n PdfSignatureAndBatesDemo
cd PdfSignatureAndBatesDemo
dotnet add package Aspose.Pdf
```

افتح `Program.cs` واحذف الكود الافتراضي. سنبني كل شيء من الصفر حتى تتمكن من نسخ‑لصق النسخة النهائية لاحقًا.

---

## الخطوة 2: التحقق من توقيع PDF

### لماذا يُعد التحقق مهمًا

يمكن أن يصبح التوقيع الرقمي **مُعرضًا للخطر** إذا تم إلغاء الشهادة الأساسية أو تم تعديل المستند بعد التوقيع. توفر Aspose.Pdf طريقة `IsSignatureCompromised` التي تُعيد قيمة منطقية—بسيطة، لكنها قوية بما يكفي لمعظم خطوط تدقيق البيانات.

### مقتطف الكود

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace PdfSignatureAndBatesDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------- Verify PDF Signature ----------
            string signedPdfPath = @"YOUR_DIRECTORY\signed.pdf";

            // Load the signed document inside a using block to ensure disposal
            using (Document signedDoc = new Document(signedPdfPath))
            using (PdfFileSignature pdfSignature = new PdfFileSignature(signedDoc))
            {
                // The name "Signature1" is the default for the first signature.
                // Change it if your PDF uses a custom field name.
                bool isCompromised = pdfSignature.IsSignatureCompromised("Signature1");

                Console.WriteLine($"Signature compromised: {isCompromised}");
                // Expected output: "Signature compromised: False" if everything is fine.
            }

            // The rest of the program (Bates numbering) continues below...
```

**شرح**

- `Document` يقوم بتحميل ملف PDF إلى الذاكرة.  
- `PdfFileSignature` يلتف حول المستند ويُظهر طرقًا متعلقة بالتوقيع.  
- `IsSignatureCompromised("Signature1")` يتحقق من سلامة التوقيع المسمى *Signature1*.  
- النتيجة المنطقية تُخبرك ما إذا كان التوقيع لا يزال موثوقًا.

> **نصيحة احترافية:** إذا لم تكن متأكدًا من اسم حقل التوقيع، استدعِ `pdfSignature.GetSignatureNames()` أولًا؛ سيُعيد قائمة بجميع معرفات التوقيع.

---

## الخطوة 3: إعداد خيارات ترقيم Bates

### ما هو ترقيم Bates؟

ترقيم Bates هو معرفات متسلسلة تُطبع على كل صفحة من المستندات القانونية أو الجنائية. يجعل الإشارة إلى الصفحات أمرًا سهلًا أثناء عمليات الاكتشاف أو التدقيق. تسمح لك `BatesNumberingOptions` في Aspose.Pdf بتخصيص البادئة، رقم البداية، عدد الأرقام، المحاذاة، والهامش—كل ذلك في كائن واحد.

### استمرار الكود

```csharp
            // ---------- Configure Bates Numbering ----------
            string sourcePdfPath = @"YOUR_DIRECTORY\input.pdf";
            using (Document pdfWithBates = new Document(sourcePdfPath))
            {
                // Set up the numbering style
                BatesNumberingOptions batesOptions = new BatesNumberingOptions
                {
                    Prefix = "INV-",          // Anything before the numeric part
                    StartNumber = 1000,      // First number to use
                    NumberOfDigits = 5,      // Pads numbers with leading zeros (e.g., 01000)
                    Alignment = HorizontalAlignment.Right,
                    BottomMargin = 20        // Distance from the bottom edge (points)
                };

                // Apply the numbering to every page in the document
                pdfWithBates.AddBatesNumbering(batesOptions);

                // Save the newly numbered PDF
                string outputPdfPath = @"YOUR_DIRECTORY\BatesNumbered.pdf";
                pdfWithBates.Save(outputPdfPath);

                Console.WriteLine($"Bates numbering added. File saved to: {outputPdfPath}");
                // Expected output: "Bates numbering added. File saved to: ...\BatesNumbered.pdf"
            }
        }
    }
}
```

**شرح**

- `BatesNumberingOptions` يجمع كل خيارات التنسيق.  
- `AddBatesNumbering` يمر تلقائيًا على كل صفحة—دون الحاجة إلى حلقة يدوية.  
- البادئة `INV-` ورقم البداية `1000` ينتجان تسميات مثل `INV-01000`، `INV-01001`، إلخ.  
- عدل `BottomMargin` إذا أردت وضع الرقم أعلى أو أسفل الصفحة.

---

## الخطوة 4: تشغيل المثال الكامل

احفظ الملف، ثم نفّذ:

```bash
dotnet run
```

يجب أن ترى سطرين في وحدة التحكم:

```
Signature compromised: False
Bates numbering added. File saved to: YOUR_DIRECTORY\BatesNumbered.pdf
```

إذا طبع السطر الأول `True`، فهذا يعني أن التوقيع **مُعرض للخطر**—أي أن المستند ربما تم تعديله بعد التوقيع أو أن الشهادة لم تعد صالحة. في هذه الحالة، أوقف أي معالجة لاحقة.

---

## الخطوة 5: الحالات الخاصة الشائعة وكيفية التعامل معها

| الحالة | ما الذي يجب مراقبته | الحل المقترح |
|-----------|-------------------|---------------|
| **تعدد التوقيعات** | `IsSignatureCompromised` يتحقق من حقل واحد في كل مرة. | قم بعمل حلقة عبر `pdfSignature.GetSignatureNames()` وتحقق من كل توقيع. |
| **اسم حقل توقيع مخصص** | استخدام `"Signature1"` قد يسبب استثناء إذا كان الاسم مختلفًا. | احصل أولًا على قائمة الأسماء، أو مرّر الاسم الدقيق الذي تراه في Acrobat. |
| **ملفات PDF كبيرة (100+ صفحة)** | إضافة ترقيم Bates قد تستهلك الذاكرة بشكل كبير. | استخدم `Document.Save` مع `SaveOptions` التي تدعم البث (`PdfSaveOptions { Compress = true }`). |
| **حروف غير لاتينية في البادئة** | بعض الخطوط لا تدعم Unicode افتراضيًا. | عيّن `pdfWithBates.Font` إلى خط يدعم Unicode مثل `Arial Unicode MS`. |
| **الرغبة في وضع الأرقام على اليسار** | المحاذاة مُحددة مسبقًا إلى `Right`. | غيّر `Alignment = HorizontalAlignment.Left` في `BatesNumberingOptions`. |

---

## الخطوة 6: التحقق من النتيجة يدويًا (اختياري)

افتح `BatesNumbered.pdf` بأي عارض PDF:

1. تصفح الصفحات—يجب أن يظهر على كل صفحة تسمية مثل **INV‑01000** في الزاوية السفلية اليمنى.  
2. استخدم **لوحة التوقيع** في Acrobat وانقر مزدوجًا على التوقيع لتتأكد من أن الحالة تتطابق مع مخرجات وحدة التحكم.

إذا كان كل شيء متطابقًا، فقد نجحت في **check pdf signature** وتطبيق **add bates numbering** في خطوة واحدة.

---

## الأسئلة المتكررة

**س: هل يمكنني التحقق من التوقيع دون تحميل المستند بالكامل؟**  
ج: تقوم Aspose.Pdf ببث الملف في الخلفية، لكن لا يزال عليك إنشاء كائن `Document`. للملفات الضخمة، يمكنك استخدام `PdfFileSignature` مباشرة مع تدفق ملف لتقليل استهلاك الذاكرة.

**س: هل أحتاج إلى ترخيص لـ Aspose.Pdf؟**  
ج: النسخة التجريبية المجانية تعمل، لكنها تضيف علامة مائية. للإنتاج ستحتاج إلى ترخيص صالح؛ وإلا ستحمل ملفات PDF الناتجة شعار Aspose.

**س: ماذا لو أردت إضافة ترقيم Bates فقط إلى مجموعة فرعية من الصفحات؟**  
ج: استخدم `pdfWithBates.AddBatesNumbering(batesOptions, new[] { 1, 3, 5 })` حيث يحدد المصفوفة أرقام الصفحات التي تريد ترقيمها.

---

## الخلاصة

أنت الآن تعرف **كيفية التحقق من توقيع PDF** باستخدام Aspose.Pdf، وتفهم معنى النتيجة المنطقية، ويمكنك بثقة **إضافة ترقيم Bates** إلى أي PDF تملكه. المثال الكامل القابل للتنفيذ يجمع المهمتين، مما يمنحك أداة Console واحدة تتحقق من أصالة المستند وتضع عليه معرفات جاهزة للتدقيق.  

بعد ذلك، قد تستكشف **كيفية التحقق من التوقيع** مقابل مخزن الجذور الموثوق، أو تجرب أنماط **add bates numbering** مخصصة مثل الطوابع المائلة أو البادئات حسب القسم. كلا الموضوعين يبنيان على الأساس الذي أتممته الآن، وسيجعلان خط أنابيب معالجة المستندات أكثر قوة.

برمجة سعيدة، وتذكر—التحقق من التوقيعات وترقيم الصفحات سهل بمجرد وجود الكود المناسب! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}