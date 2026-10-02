---
category: general
date: 2026-03-27
description: أضف ترقيم بايتس في C# بسرعة. تعلم كيفية إضافة أرقام صفحات مخصصة، وإضافة
  أرقام صفحات متسلسلة، وإضافة أرقام مخصصة إلى مستندات Word.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: ar
og_description: إضافة ترقيم بايتس في C# مع مثال واضح. يوضح هذا الدليل كيفية إضافة
  أرقام صفحات مخصصة، إضافة أرقام صفحات متسلسلة، وأكثر من ذلك.
og_title: إضافة ترقيم بايتس في C# – دليل كامل
tags:
- C#
- Document Processing
- Bates Numbering
title: إضافة ترقيم بايتس في C# – دليل خطوة بخطوة
url: /ar/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم بايتس في C# – دليل خطوة بخطوة

هل تساءلت يومًا كيف **تضيف ترقيم بايتس** إلى مستند Word دون أن تصيب نفسك بالصداع؟ لست وحدك. في العديد من المشاريع القانونية أو الامتثال، يحتاج كل صفحة إلى معرف فريد، والقيام بذلك يدويًا كالكابوس.  

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ **يضيف ترقيم بايتس**، يوضح لك **كيفية إضافة بايتس** في بضع أسطر، ويتناول أيضًا **إضافة أرقام صفحات مخصصة** و**إضافة أرقام صفحات متسلسلة** عندما تحتاجها. في النهاية ستحصل على ملف .docx مختوم بالأرقام التي تختارها—بدون الحاجة إلى أدوات طرف ثالث.

## ما ستتعلمه

- تحميل ملف DOCX باستخدام Aspose.Words for .NET API (أو أي مكتبة متوافقة).  
- ضبط **إضافة أرقام مخصصة** مثل البادئة، قيمة البداية، وحجم الخط.  
- تطبيق الترقيم على كل صفحة باستدعاء واحد.  
- حفظ النتيجة والتحقق من ظهور الأرقام كما هو متوقع.  

لا تحتاج إلى خبرة سابقة في ترقيم بايتس؛ فقط إعداد أساسي لـ C# ونسخة من المستند الأصلي. هيا نبدأ.

## المتطلبات المسبقة

- .NET 6+ (الكود يعمل على .NET Core و .NET Framework على حد سواء).  
- Aspose.Words for .NET مثبت عبر NuGet (`Install-Package Aspose.Words`).  
- مستند Word اسمه `input.docx` موجود في مجلد يمكنك الإشارة إليه (`YOUR_DIRECTORY`).  
- Visual Studio، VS Code، أو أي بيئة تطوير C# تفضلها.

> **نصيحة احترافية:** إذا كنت تستخدم مكتبة مختلفة (مثل Open XML SDK)، فإن المفاهيم تبقى نفسها—فقط استبدل استدعاءات الـ API.

## الخطوة 1: تحميل المستند المصدر

أولًا نحتاج إلى جلب ملف Word إلى الذاكرة.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*لماذا هذا مهم:* تحميل الملف يُنشئ كائن `Document` يمنحك الوصول إلى الصفحات، الأقسام، وشجرة العقد منخفضة المستوى. بدون ذلك لا يمكنك إرفاق أي ترقيم.

## الخطوة 2: ضبط خيارات ترقيم بايتس

الآن نحدد بالضبط كيف يجب أن تبدو الأرقام. هنا يمكنك **إضافة أرقام صفحات مخصصة** أو **إضافة أرقام صفحات متسلسلة**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*لماذا هذا مهم:* الخاصية `Prefix` تسمح لك **بإضافة أرقام مخصصة** مثل معرف القضية، بينما `Start` يحدد عداد البداية. تعديل `FontSize` يضمن أن الأرقام لا تبتلع هوامش الصفحة.

## الخطوة 3: تطبيق ترقيم بايتس على كل صفحة

بعد تجهيز الخيارات، نخبر المكتبة بوضع الطابع على كل صفحة.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*لماذا هذا مهم:* طريقة `AddBatesNumbering` تمر عبر مجموعة الصفحات الداخلية وتدرج صندوق نص في الزاوية السفلية اليمنى (الموقع الافتراضي). إنها جوهر **كيفية إضافة بايتس** دون كتابة حلقة يدوية.

## الخطوة 4: حفظ المستند المحدث

أخيرًا، نكتب الملف المعدل مرة أخرى إلى القرص.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*لماذا هذا مهم:* الحفظ يُنشئ ملف `output.docx` جديد يمكنك فتحه في Word أو LibreOffice أو أي عارض لتأكيد ظهور الأرقام.

## النتيجة المتوقعة

افتح `output.docx`. يجب أن تظهر كل صفحة شيئًا مثل:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

إذا فتحت معاينة الطباعة للمستند، سترى الأرقام في الزاوية السفلية اليمنى، مطابقة لحجم الخط الذي ضبطته.

## الحالات الخاصة والاختلافات

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|-----|
| **لا حاجة للبادئة** | `Prefix = string.Empty` | يزيل الجزء “ABC‑”، ويترك فقط التسلسل الرقمي. |
| **البدء من 1** | `Start = 1` | مفيد لـ **إضافة أرقام صفحات متسلسلة** بسيطة بدون بادئة مخصصة. |
| **مستندات كبيرة (>10,000 صفحة)** | زيادة `FontSize` أو تعديل `Location` (استخدام التحميلات الزائدة لـ `AddBatesNumbering`) | يمنع التداخل مع التذييلات أو الرؤوس. |
| **ملف المصدر للقراءة فقط** | فتحه باستخدام `LoadOptions` التي تسمح بالكتابة، أو نسخ الملف أولًا | وإلا سيتسبب `document.Save` في استثناء. |
| **موضع مختلف** | `batesOptions.Position = BatesNumberingPosition.TopLeft` (أو أي قيمة أخرى من الـ enum) | بعض الشركات تطلب الأرقام في أعلى الصفحة. |

> **ملاحظة:** ليست كل المكتبات تعرض فئة `BatesNumberingOptions`. مع Open XML SDK ستحتاج إلى إدراج `TextBox` يدويًا—نفس المبدأ، لكن مع المزيد من الكود.

## مثال كامل يعمل

إليك البرنامج بالكامل في مكان واحد. انسخه‑الصقه في تطبيق Console وشغّله.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

شغّل البرنامج، افتح `output.docx`، وسترى الترقيم بالضبط حيث توقعت. 🎉

## الأسئلة المتكررة

**س: هل يمكنني تغيير لون الأرقام؟**  
ج: نعم. بعد استدعاء `AddBatesNumbering`، يمكنك الحصول على كائنات `Shape` المُنشأة وتعيين خاصية `FillColor` لها.

**س: ماذا لو أردت الأرقام على الجانب الأيسر بدلًا من الأيمن؟**  
ج: استخدم `batesOptions.Position = BatesNumberingPosition.BottomLeft` (أو `TopLeft`, `TopRight`). الـ API يدعم جميع الزوايا الأربعة.

**س: هل يعمل هذا مع إخراج PDF؟**  
ج: بالتأكيد. بعد إضافة الترقيم، استدعِ `document.Save("output.pdf")`. تُرسم الأرقام في الـ PDF كما هي في Word.

## الخلاصة

أنت الآن تعرف **كيفية إضافة ترقيم بايتس** إلى ملف Word باستخدام C#. غطى الدرس تحميل المستند، ضبط **إضافة أرقام مخصصة**، تطبيق **إضافة أرقام صفحات متسلسلة**، وحفظ النتيجة النهائية. مع عينة الكود الكاملة، يمكنك إدراجها في أي مشروع والبدء في ختم المستندات فورًا.

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذا مع معالج دفعي يمر عبر مجلد من الملفات، أو استكشف **إضافة أرقام صفحات مخصصة** في الرأس/التذييل لمظهر أكثر احترافية. في كلتا الحالتين، لديك أساس قوي لأي مهمة تقنية قانونية أو أتمتة امتثال.

هل لديك أسئلة أو حالة استخدام مميزة؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}