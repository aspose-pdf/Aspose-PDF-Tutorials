---
category: general
date: 2026-02-14
description: أضف ترقيم بايتس إلى ملفات PDF الخاصة بك بسهولة. تعلم كيفية إضافة أرقام
  الصفحات في التذييل وإضافة أرقام متسلسلة إلى PDF باستخدام Aspose.Pdf في دقائق.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: ar
og_description: أضف ترقيم بايتس لملف PDF بسرعة. يوضح هذا الدليل كيفية إضافة أرقام
  الصفحات في التذييل وترقيم تسلسلي لملف PDF باستخدام Aspose.Pdf، مع الكود الكامل والنصائح.
og_title: إضافة ترقيم بايتس إلى PDF – دليل خطوة بخطوة بلغة C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: إضافة ترقيم بايتس إلى PDF – دليل C# الكامل
url: /ar/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم Bates إلى ملفات PDF – دليل C# الكامل

هل احتجت يومًا إلى **add Bates numbering PDF** ملفات لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. الفرق القانونية، المدققون، وأي شخص يتعامل مع مجموعات مستندات كبيرة يسأل باستمرار، “كيف يمكنني إضافة أرقام Bates دون كسر التخطيط؟” الخبر السار هو أنه باستخدام Aspose.Pdf for .NET يمكنك حقن تلك الأرقام كتذييل بسيط—بدون الحاجة إلى تحرير يدوي.

في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية لا يضيف فقط **adds footer page numbers** بل يتيح لك أيضًا **add sequential numbers PDF** ملفات مع بادئة مخصصة، حجم الخط، والمحاذاة. بحلول النهاية ستحصل على برنامج C# جاهز للتشغيل، وفهم واضح لأسباب أهمية كل إعداد، وبعض النصائح الاحترافية لتجنب أكثر الأخطاء شيوعًا.

## ما ستتعلمه

- كيفية تحميل ملف PDF موجود وتحضيره لتطبيق ترقيم Bates.  
- أي خصائص **BatesNumberingOptions** تتحكم في المظهر والمكان.  
- كيفية تطبيق الترقيم على كل صفحة في استدعاء واحد.  
- طرق تخصيص البادئة، رقم البداية، والهوامش لتنسيقات قانونية مختلفة.  
- معالجة الحالات الخاصة—ماذا تفعل مع ملفات PDF المشفرة أو المستندات التي تحتوي بالفعل على تذييلات.

**المتطلبات المسبقة**: .NET 6+ (أو .NET Framework 4.7+)، نسخة حديثة من Aspose.Pdf (المثال يستخدم 23.10)، وملف PDF إدخال تملك حقوق تعديلّه. لا تحتاج إلى أي مكتبات طرف ثالث أخرى.

---

## الخطوة 1 – تحميل ملف PDF الذي تريد ترقيمه

أول شيء نقوم به هو إنشاء مثيل `Document` يشير إلى ملف المصدر. استخدام نمط `using var` يضمن تحرير مقبض الملف تلقائيًا.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **لماذا هذا مهم:** Aspose.Pdf يقرأ بنية PDF بالكامل إلى الذاكرة، مما يتيح لنا تعديل الصفحات، التعليقات التوضيحية، والبيانات الوصفية دون لمس الملف الأصلي على القرص. إذا كان PDF محميًا بكلمة مرور، يمكنك تمرير كلمة المرور إلى المُنشئ—انظر ملاحظة “Encrypted PDFs” في النهاية.

---

## الخطوة 2 – تعريف خيارات ترقيم Bates الخاصة بك

أرقام Bates هي في الأساس تذييلات صفحات مع بادئة قابلة للتكوين ومؤشر تسلسلي. تسمح لك فئة `BatesNumberingOptions` بضبط كل جانب بصري بدقة.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### نصيحة سريعة

- **Prefix**: استخدم معرفًا قصيرًا وفريدًا (مثلاً رقم القضية) للحفاظ على قابلية قراءة التذييل.  
- **StartNumber**: غالبًا ما تبدأ الشركات القانونية من `1` أو إزاحة مخصصة؛ اختر ما يتوافق مع نظام حفظ الملفات لديك.  
- **Margins**: الهوامش السفلية بقيمة `20` نقطة تحافظ على بقاء النص بعيدًا عن الحواشي أو التوقيعات التي قد تكون موجودة بالفعل بالقرب من حافة الصفحة.

---

## الخطوة 3 – تطبيق الترقيم على جميع الصفحات

مع تكوين الخيارات، يكون حقن الترقيم عملية سطر واحد. Aspose.Pdf يتعامل مع ترقيم الصفحات، يحدث تدفقات المحتوى الموجودة، ويحترم دوران الصفحة تلقائيًا.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **ما الذي يحدث خلف الكواليس؟** المكتبة تتكرر على كل كائن `Page`، تنشئ `TextFragment` يدمج البادئة والعداد الحالي، ثم ترسمه باستخدام نظام إحداثيات الصفحة. لأننا ضبطنا `HorizontalAlignment.Right` و `VerticalAlignment.Bottom`، فإن النص يلتصق بالزاوية السفلية اليمنى بغض النظر عن حجم الصفحة.

---

## الخطوة 4 – حفظ ملف PDF المعدل

أخيرًا، اكتب النتيجة إلى ملف جديد. يمكن استبدال الأصلي، لكن الاحتفاظ بنسخة يساعد في التحكم بالإصدارات.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

إذا كنت بحاجة إلى الحفاظ على البيانات الوصفية الأصلية (المؤلف، تاريخ الإنشاء)، فإن Aspose.Pdf ينسخها تلقائيًا. يمكنك أيضًا تحديد كائن `SaveOptions` للامتثال لـ PDF/A أو للضغط.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتشغيل. الصقه في مشروع تطبيق كونسول، عدل مسارات الملفات، واضغط **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**النتيجة المتوقعة:** كل صفحة من `output.pdf` الآن تعرض تذييلًا مثل `ABC-1000`، `ABC-1001`، … مثبتًا في الزاوية السفلية اليمنى. افتح الملف في أي قارئ PDF للتحقق.

---

## التعامل مع التغييرات الشائعة

### إضافة أرقام صفحات التذييل فقط

إذا كنت تحتاج فقط إلى أرقام صفحات بسيطة بدون بادئة، اضبط `Prefix = ""` وربما عدل الهوامش لتجنب التصادم مع التذييلات الموجودة.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### استخدام محاذاة مختلفة

أحيانًا تتطلب المستندات القانونية أن يكون الرقم في وسط الأسفل. غيّر المحاذاة إلى:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### التعامل مع ملفات PDF المشفرة

عندما يكون ملف PDF المصدر محميًا بكلمة مرور، قدم كلمة المرور هكذا:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

بقية سير العمل يظل متطابقًا.

### تخطي التذييلات الموجودة

إذا كان المستند يحتوي بالفعل على تذييل لا تريد استبداله، يمكنك إضافة سلسلة مخصصة مسبقًا تجعل الرقم الجديد مميزًا، أو يمكنك تكرار الصفحات يدويًا وإضافة `TextFragment` فقط حيث لا يوجد تذييل. فئة `Page` في المكتبة تعرض مجموعات `Annotations` و `Contents` للتحكم الدقيق.

---

## نصائح احترافية ومخاطر

- **Avoid clipping**: الهوامش السفلية الصغيرة جدًا قد تتسبب في قطع النص على الطابعات. اختبر بطباعة فعلية إذا كنت ستوزع نسخًا ورقية.  
- **Performance**: إضافة أرقام Bates إلى ملف PDF مكوّن من 500 صفحة تستغرق أقل من ثانية على لابتوب حديث، لكن الدفعات الكبيرة تستفيد من المعالجة المتوازية—فقط تذكر أن `Document` غير آمن للثريد، لذا يحتاج كل ثريد إلى نسخة خاصة به.  
- **Version compatibility**: الكود يعمل مع Aspose.Pdf 23.10 وما بعده. إذا كنت تستخدم نسخة أقدم، فإن أسماء الخصائص هي نفسها لكن مُنشئ `MarginInfo` قد يتطلب معاملات `float`.  
- **Legal compliance**: بعض الولايات القضائية تتطلب وضع رقم Bates في موقع محدد (مثلاً، أسفل اليسار). عدل `HorizontalAlignment` وفقًا لذلك.

---

## الخلاصة

لقد أوضحنا للتو كيفية **add Bates numbering PDF** الملفات باستخدام Aspose.Pdf for .NET، مع تغطية كل شيء من تحميل المستند إلى حفظ النسخة النهائية مع تذييل نظيف. من خلال تعديل عدد قليل من الخصائص يمكنك أيضًا **add footer page numbers**، **add sequential numbers PDF**، أو تخصيص المظهر لتلبية أي معيار قانوني.

هل أنت مستعد للخطوة التالية؟ جرّب دمج هذه التقنية مع استخراج النص عبر OCR لإدراج كلمات مفتاحية قابلة للبحث بجانب أرقام Bates الخاصة بك، أو أتمتة العملية لمجلدات كاملة باستخدام `Directory.GetFiles`. الاحتمالات لا حصر لها، والأساس الذي تملكه الآن سيجعل تلك الإضافات سهلة.

برمجة سعيدة، ولتكن ملفات PDF الخاصة بك دائمًا مرقمة بشكل مثالي!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}