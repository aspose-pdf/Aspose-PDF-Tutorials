---
category: general
date: 2026-03-14
description: تحقق من توقيع PDF باستخدام Aspose.Pdf في C#. تعلّم كيفية التحقق من صحة
  التوقيع الرقمي لملف PDF وفحص توقيع PDF بفعالية في بضع خطوات.
draft: false
keywords:
- verify pdf signature
- validate pdf digital signature
- check pdf signature
- c# verify pdf signature
language: ar
og_description: تحقق من توقيع PDF باستخدام Aspose.Pdf للغة C#. يوضح هذا الدليل كيفية
  التحقق من صحة التوقيع الرقمي لملف PDF وفحص توقيع PDF في مثال مختصر وقابل للتنفيذ.
og_title: تحقق من توقيع PDF في C# – دليل كامل
tags:
- C#
- Aspose.Pdf
- PDF Security
- Digital Signature
title: تحقق من توقيع PDF في C# – دليل برمجي شامل
url: /ar/net/programming-with-security-and-signatures/verify-pdf-signature-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التحقق من توقيع PDF في C# – دليل برمجة كامل

هل احتجت يوماً إلى **التحقق من توقيع PDF** بشكل فوري؟ في العديد من سير عمل المؤسسات يمكن أن يتوقف المعالجة إذا كان الختم الرقمي مكسوراً أو منتهي الصلاحية، لذا فإن معرفة كيفية فحص أصالة PDF برمجياً أمر حيوي. يوضح لك هذا الدرس كيفية التحقق من توقيع PDF باستخدام Aspose.Pdf في C#، وسنظهر لك أيضاً كيفية **التحقق من صحة التوقيع الرقمي للـ PDF** و**فحص حالة توقيع PDF** دون مغادرة بيئة التطوير المتكاملة الخاصة بك.

سنغطي كل شيء بدءاً من تثبيت المكتبة إلى التعامل مع الحالات الخاصة مثل وجود توقيعات متعددة على نفس المستند. في النهاية ستحصل على مقتطف جاهز للتنفيذ يخبرك ما إذا كان التوقيع معرضاً للخطر، بالإضافة إلى نصائح لتوسيع المنطق إلى خط أنابيب الأمان الخاص بك.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث (الكود يعمل أيضاً على .NET Framework 4.7+)
- Visual Studio 2022 (أو أي محرر C# تفضله)
- رخصة **Aspose.Pdf for .NET** أو مفتاح تقييم مؤقت
- ملف PDF موقع تريد اختباره (سنسميه `Signed.pdf`)

لا توجد حزم طرف ثالث أخرى مطلوبة.

![مخطط يوضح سير عمل التحقق من توقيع PDF](verify-pdf-signature-workflow.png "مخطط سير عمل التحقق من توقيع PDF")

## الخطوة 1 – تثبيت Aspose.Pdf for .NET

أول شيء تحتاجه هو مكتبة Aspose.Pdf. يمكنك الحصول عليها من NuGet:

```bash
dotnet add package Aspose.Pdf
```

أو، إذا كنت تستخدم وحدة تحكم مدير الحزم داخل Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

> **نصيحة احترافية:** النسخة التجريبية المجانية تضيف علامة مائية إلى ملف PDF الناتج، لكنها لا تزال تسمح لك **بفحص حالة توقيع PDF** بدقة.

## الخطوة 2 – إعداد مسار ملف PDF الموقع

يحتاج الكود إلى معرفة مكان وجود ملف PDF الموقع. احتفظ بمسار الملف في متغير لتتمكن من إعادة استخدامه لاحقاً:

```csharp
// Adjust the path to point at your actual signed PDF
string inputPdfPath = @"C:\MyDocuments\Signed.pdf";
```

إذا كان ملف PDF موجوداً في نفس مجلد الملف التنفيذي، يمكنك استخدام مسار نسبي مثل `@"Signed.pdf"`.

## الخطوة 3 – تحميل المستند وإنشاء معالج التوقيع

توفر Aspose.Pdf فئتين تعملان معاً: `Document` للعمليات العامة على PDF و`PdfFileSignature` للمهام الخاصة بالتوقيع. إليك كيفية ربطهما:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the PDF document
using (var pdfDocument = new Document(inputPdfPath))
{
    // Create a handler that can inspect signatures
    using (var pdfSignature = new PdfFileSignature(pdfDocument))
    {
        // The rest of the logic lives inside this block
    }
}
```

تضمن عبارات `using` تحرير الموارد غير المُدارة بسرعة—وهو ما ستقدره في خدمة ذات حجم مرور عالي.

## الخطوة 4 – التحقق مما إذا كان التوقيع معرضاً للخطر

طريقة `IsSignatureCompromised` في Aspose.Pdf تقوم بالعمل الشاق. تُعيد **true** إذا فشل التوقيع في أي من الفحوصات التالية:

1. سلامة التشفير (الهاش لا يتطابق)
2. صلاحية الشهادة (منتهية أو مُسحوبة)
3. وجود قائمة إبطال (الشهادة تظهر في CRL أو OCSP)

يمكنك استهداف صفحة معينة وفهرس توقيع محدد. في معظم الحالات يكون أول توقيع على الصفحة 1 هو ما يهمك:

```csharp
// Checks the first signature on page 1
bool isCompromised = pdfSignature.IsSignatureCompromised(1); // page 1, first signature
```

إذا كان لديك توقيعات متعددة، ما عليك سوى تغيير رقم الصفحة أو استدعاء النسخة التي تقبل فهرس التوقيع.

## الخطوة 5 – تفسير النتيجة

الآن بعد أن عرفت ما إذا كان التوقيع معرضاً للخطر، يمكنك اتخاذ الإجراء المناسب. نمط شائع هو تسجيل النتيجة وربما إيقاف المعالجة الإضافية:

```csharp
Console.WriteLine(isCompromised
    ? "Signature is compromised!"
    : "Signature looks OK.");
```

عندما تكون النتيجة `false`، يمكنك أن تكون واثقاً إلى حد كبير أن عملية **التحقق من صحة التوقيع الرقمي للـ PDF** نجحت وأن المستند لم يتعرض لأي تعديل.

## الخطوة 6 – التعامل مع توقيعات متعددة (حالات حافة)

غالباً ما تحتوي ملفات PDF الواقعية على عدة توقيعات—تخيل عقداً يتم توقيعه من قبل عدة أطراف. للتكرار على جميع التوقيعات، يمكنك استخدام طريقة `GetSignatureCount` والقيام بحلقة:

```csharp
int totalSignatures = pdfSignature.GetSignatureCount();

for (int i = 1; i <= totalSignatures; i++)
{
    bool compromised = pdfSignature.IsSignatureCompromised(i);
    Console.WriteLine($"Signature #{i} on page {pdfSignature.GetSignaturePageNumber(i)}: " +
                      (compromised ? "Compromised" : "Valid"));
}
```

هذا المقتطف **يفحص حالة توقيع PDF** لكل إدخال، مما يمنحك مسار تدقيق كامل. تذكر أن أرقام الصفحات تبدأ من 1 في Aspose.Pdf.

## الخطوة 7 – مثال كامل يعمل

بدمج كل ما سبق، إليك برنامج مستقل يمكنك نسخه ولصقه في تطبيق Console:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // 1️⃣ Path to the signed PDF
        string inputPdfPath = @"C:\MyDocuments\Signed.pdf";

        // 2️⃣ Load the PDF and create a signature handler
        using (var pdfDocument = new Document(inputPdfPath))
        using (var pdfSignature = new PdfFileSignature(pdfDocument))
        {
            // 3️⃣ Verify the first signature on page 1
            bool isSignatureCompromised = pdfSignature.IsSignatureCompromised(1);

            // 4️⃣ Output the verification result
            Console.WriteLine(isSignatureCompromised
                ? "Signature is compromised!"
                : "Signature looks OK.");

            // 5️⃣ (Optional) Loop through all signatures for a complete audit
            int count = pdfSignature.GetSignatureCount();
            for (int i = 1; i <= count; i++)
            {
                bool compromised = pdfSignature.IsSignatureCompromised(i);
                int page = pdfSignature.GetSignaturePageNumber(i);
                Console.WriteLine($"Signature #{i} on page {page}: " +
                                  (compromised ? "Compromised" : "Valid"));
            }
        }

        // Keep console window open
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

**الناتج المتوقع (عند كون التوقيع صالحاً):**

```
Signature looks OK.
Signature #1 on page 1: Valid
Press any key to exit...
```

إذا فشل التوقيع في أي من فحوصات السلامة، سيظهر السطر الأول `Signature is compromised!` وستُعلم الحلقة الإدخال المخالف.

## أسئلة شائعة وملاحظات

- **ماذا لو لم يحتوي PDF على توقيعات؟**  
  ستُعيد `GetSignatureCount` القيمة `0`، واستدعاء `IsSignatureCompromised(1)` سيؤدي إلى رمي استثناء `ArgumentOutOfRangeException`. تحقق دائماً من العدد أولاً.

- **هل أحتاج إلى رخصة لاستخدام `IsSignatureCompromised`؟**  
  النسخة التجريبية تعمل بشكل جيد للفحص؛ تحتاج إلى رخصة كاملة فقط إذا كنت تخطط لتعديل أو توقيع ملفات PDF لاحقاً.

- **هل يمكنني التحقق من توقيع مقابل مخزن ثقة مخصص؟**  
  نعم. تسمح Aspose.Pdf لك بتمرير كائن `CertificateStore` إلى مُنشئ `PdfFileSignature`. هذا موضوع أعمق، لكن مبدأ **التحقق من صحة التوقيع الرقمي للـ PDF** يبقى نفسه.

- **هل الطريقة آمنة للاستخدام في بيئات متعددة الخيوط؟**  
  يجب حصر كل نسخة من `Document` إلى خيط واحد. إذا كنت بحاجة إلى معالجة متوازية، أنشئ نسخة `Document` منفصلة لكل خيط.

## الخلاصة

أنت الآن تعرف كيف **تتحقق من توقيع PDF** في C# باستخدام Aspose.Pdf، وكيف **تتحقق من صحة التوقيع الرقمي للـ PDF**، وكيف **تفحص حالة توقيع PDF** عبر صفحات متعددة. يوضح المثال الكامل القابل للتنفيذ التدفق الكامل—من تحميل المستند إلى تفسير النتيجة والتعامل مع حالات الحافة.

هل أنت مستعد للخطوة التالية؟ جرّب دمج منطق التحقق هذا في واجهة ويب API ترفض ملفات PDF المرفوعة التي تحتوي على توقيعات معرضة للخطر، أو استكشف كيفية استخراج تفاصيل الموقع للتدقيق. كلا السيناريوهين يبنيان على نفس المفاهيم الأساسية التي إتقنتها الآن.

برمجة سعيدة، ولتظل ملفات PDF الخاصة بك موقعة بأمان!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}