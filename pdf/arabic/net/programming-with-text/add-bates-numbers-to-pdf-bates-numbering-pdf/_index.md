---
category: general
date: 2026-01-15
description: أضف أرقام باتس إلى ملف PDF الخاص بك بسرعة باستخدام Aspose.Pdf. تعلم كيفية
  إضافة تذييل إلى PDF، إضافة أرقام الصفحات إلى PDF، وإضافة ترقيم صفحات مخصص.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: ar
og_description: أضف أرقام باتس إلى ملف PDF الخاص بك بسرعة باستخدام Aspose.Pdf. تعلّم
  كيفية إضافة تذييل إلى PDF، إضافة أرقام الصفحات إلى PDF، وإضافة ترقيم صفحات مخصص.
og_title: إضافة أرقام بايتس إلى PDF – ترقيم بايتس PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: إضافة أرقام بايتس إلى PDF – ترقيم بايتس PDF
url: /ar/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة أرقام باتس إلى PDF – دليل كامل

هل احتجت يوماً إلى **إضافة أرقام باتس** إلى ملف PDF لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—الفرق القانونية، المدققون، وأي شخص يتعامل مع مجموعات مستندات ضخمة يواجه هذه المشكلة يوميًا. الخبر السار؟ باستخدام Aspose.Pdf for .NET يمكنك رش هذه الأرقام على كل صفحة ببضع أسطر فقط.

في هذا الدرس سنستعرض العملية بالكامل: من استدعاء مكتبة Aspose.Pdf، تحميل ملف المصدر، تكوين *BatesNumberingArtifact*، ربطه كتذييل، وأخيرًا حفظ النتيجة. في النهاية ستعرف أيضًا كيفية **إضافة تذييل إلى pdf**، **إضافة أرقام صفحات pdf**، وحتى **إضافة ترقيم صفحات مخصص** للحالات الخاصة.

## ما ستحتاجه

- .NET 6+ (أو .NET Framework 4.8 إذا كنت لا تزال تستخدم النسخة الكلاسيكية)  
- إشارة إلى حزمة **Aspose.Pdf** على NuGet (`Install-Package Aspose.Pdf`)  
- ملف PDF تريد ختمه (سنسميه `source.pdf`)  

هذا كل ما تحتاجه—لا أدوات إضافية، لا محررات PDF ثقيلة. لنبدأ.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## الخطوة 1: إضافة أرقام باتس – تحميل مستند PDF

أولًا، نحتاج إلى كائن `Document` يمثل ملف PDF الذي سنقوم بتعديله. فكر فيه كفتح مستند Word قبل أن تبدأ الكتابة.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **لماذا هذا مهم:** تحميل الملف يمنحك الوصول إلى مجموعة `Pages` الخاصة به، وهي المكان الذي سنرفق فيه كائن ترقيم باتس لاحقًا. إذا تعذر العثور على الملف، سيطلق Aspose استثناء واضح `FileNotFoundException`، لذا تأكد من صحة المسار.

## الخطوة 2: تكوين إعدادات ترقيم باتس pdf

الآن نحدد *كيف* يجب أن تبدو الأرقام. يتيح لك `BatesNumberingArtifact` تعيين البادئة، رقم البداية، عدد الأصفار، اللاحقة، وموقع الإظهار. هذا هو جوهر **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **نصيحة محترف:** إذا أردت ظهور الأرقام في الترويسة بدلاً من ذلك، استبدل `BottomCenter` بـ `TopCenter`. يدعم تعداد المواقع أيضًا `BottomLeft`، `BottomRight`، إلخ، مما يمنحك مرونة لأنماط **add footer to pdf** المختلفة.

## الخطوة 3: إضافة أرقام صفحات pdf – ربط الكائن بكل صفحة

بعد تجهيز الكائن، نمر على كل صفحة ونضيفه إلى مجموعة `Artifacts`. هذه هي الخطوة التي **تضيف أرقام الصفحات pdf** فعليًا.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **ماذا يحدث خلف الكواليس؟** تُرسم مجموعة `Artifacts` بعد المحتوى الرئيسي للصفحة، مما يضمن أن رقم باتس يظهر فوق أي نص موجود لكن تحت التعليقات التوضيحية. إذا احتجت أن يكون الرقم خلف المحتوى (نادرًا)، يمكنك استخدام `page.Artifacts.Insert(0, batesArtifact)`.

## الخطوة 4: إضافة ترقيم صفحات مخصص – حفظ ملف PDF المحدث

أخيرًا، نكتب المستند المعدل إلى القرص. سيحتوي ملف الإخراج على أرقام باتس كجزء دائم من كل صفحة.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **نصيحة التحقق:** افتح `bates_out.pdf` بأي عارض. يجب أن ترى شيئًا مثل `CASE-01000-A` في أسفل وسط كل صفحة. إذا كانت الأرقام مفقودة، تأكد من أن خاصية `Placement` تتطابق مع الموقع المطلوب.

## مثال كامل يعمل

نجمع كل ما سبق في برنامج جاهز للتنفيذ:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### النتيجة المتوقعة

- **الملف:** `bates_out.pdf` في نفس المجلد مع `source.pdf`  
- **المظهر:** نص في أسفل‑الوسط `CASE-01000-A`، `CASE-01001-A`، … لكل صفحة تالية  
- **السلوك:** الأرقام مدمجة بشكل دائم؛ تبقى موجودة بعد الطباعة، والتسطير، وأي تعديل لاحق.

## الاختلافات الشائعة وحالات الحافة

| الحالة | كيفية التعديل |
|-----------|---------------|
| **رقم بداية مختلف** | غيّر `StartNumber` إلى أي عدد صحيح (مثال: `StartNumber = 500`). |
| **لاحقة حرفية لكل مجلد** | استخدم حلقة لتعديل `Suffix` لكل صفحة، أو أنشئ عدة كائنات بلاحقات مختلفة. |
| **ترقيم محاذاة يمين** | عيّن `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **مستندات ضخمة (أكثر من 10k صفحة)** | فكر في معالجة الصفحات على دفعات أو زيادة `NumberDigits` لتجنب الفيض. |
| **إخفاء الأرقام في صفحات معينة** | تخطَ تلك الصفحات داخل حلقة `foreach` (مثال: `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **احذر من:** استخدام `Prefix` أو `Suffix` يحتوي على أحرف غير صالحة لأسماء الملفات (مثل `*` أو `?`). سيظل Aspose يدمجها، لكن قد تسبب مشاكل عند استخراج النص لاحقًا.

## نصائح محترف للاستخدام في الإنتاج

- **خزن الكائن مؤقتًا** إذا كنت تعالج العديد من ملفات PDF متتالية؛ إن إنشاءه مرة واحدة يوفر بضع مليثانية لكل ملف.  
- **سلامة الخيوط:** كائن `BatesNumberingArtifact` غير آمن للاستخدام المتعدد الخيوط، لذا أعطِ كل خيط نسخة خاصة به.  
- **الأداء:** للدفعات الضخمة، عطل ضغط PDF (`pdfDocument.Compress = false`) قبل الحفظ، ثم أعد تفعيله إذا لزم الأمر.  
- **الاختبار:** دائمًا أجرِ فحصًا بصريًا سريعًا على أول ملف PDF مُنتج للتأكد من أن الموقع يطابق معايير فريقك القانوني.

## الخاتمة

أصبح لديك الآن وصفة شاملة من البداية إلى النهاية لكيفية **إضافة أرقام باتس** إلى أي ملف PDF باستخدام Aspose.Pdf، مع خيارات **إضافة تذييل إلى pdf**، **إضافة أرقام صفحات pdf**، و**إضافة ترقيم صفحات مخصص**. الكود مستقل تمامًا، يعمل مع .NET 6 وما بعده، ويمكن دمجه في أي خط أنابيب أتمتة موجود.

ما الخطوة التالية؟ جرّب استبدال موقع `BottomCenter` بنمط ترويسة، جرب البادئات الديناميكية (مثل معرفات القضايا من قاعدة بيانات)، أو اجمع هذا مع ميزات استخراج النص في Aspose لإنشاء فهرس قابل للبحث لمستنداتك المرقمة حديثًا. السماء هي الحد، وقد اكتسبت أداة قوية للتحكم في المستندات.

برمجة سعيدة، ولتظل ملفات PDF الخاصة بك دائمًا مرقمة بشكل مثالي!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}