---
category: general
date: 2026-04-10
description: أضف ترقيم بايتس إلى ملفات PDF باستخدام C# في دقائق. تعلّم كيفية إضافة
  أرقام صفحات مخصصة، وكيفية ترقيم ملفات PDF، وتطبيق ترقيم بايتس بكفاءة.
draft: false
keywords:
- add bates numbering
- add custom page numbers
- how to number pdf
- how to add bates
- apply bates numbering
language: ar
og_description: أضف ترقيم بايتس إلى ملفات PDF باستخدام C# في دقائق. يوضح هذا الدليل
  كيفية إضافة أرقام صفحات مخصصة، وكيفية ترقيم ملفات PDF، وتطبيق ترقيم بايتس خطوة بخطوة.
og_title: إضافة ترقيم بايتس إلى ملفات PDF باستخدام C# – دليل كامل
tags:
- PDF
- C#
- Bates numbering
title: إضافة ترقيم بايتس إلى ملفات PDF باستخدام C# – دليل كامل
url: /ar/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم Bates إلى ملفات PDF باستخدام C# – دليل كامل

هل احتجت يومًا إلى **add bates numbering** إلى ملف PDF لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—ففرق القانونية، المدققون، وأي شخص يتعامل مع مجموعات مستندات كبيرة يواجه هذه المشكلة بانتظام. الخبر السار؟ ببضع أسطر من C# يمكنك تلقائيًا وضع ختم على كل صفحة بمعرف مخصص، وستتعلم أيضًا **how to add custom page numbers** على طول الطريق.

في هذا الدرس سنستعرض كل ما تحتاجه: حزمة NuGet المطلوبة، تكوين خيارات الترقيم، تطبيق الأرقام، والتحقق من النتيجة. في النهاية ستعرف **how to number PDF** برمجياً، وستكون جاهزًا لتعديل البادئة، اللاحقة، حجم الخط، أو حتى استهداف صفحات محددة.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Framework 4.7+ أيضًا)
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)
- مكتبة **Aspose.PDF for .NET** (الإصدار التجريبي المجاني يكفي للتعلم)
- ملف PDF تجريبي اسمه `source.pdf` موجود في مجلد تتحكم فيه

إذا كنت قد تحققت من هذه النقاط، لنبدأ.

## الخطوة 1: تثبيت وإضافة مرجع Aspose.PDF

أولاً، أضف حزمة Aspose.PDF إلى مشروعك:

```bash
dotnet add package Aspose.PDF
```

أو استخدم واجهة مدير الحزم NuGet. بعد التثبيت، أدرج مساحة الاسم في أعلى ملفك:

```csharp
using Aspose.Pdf;
```

> **نصيحة احترافية:** حافظ على تحديث حزمك؛ الإصدار الأخير (اعتبارًا من أبريل 2026) يضيف عدة تحسينات في الأداء للمستندات الكبيرة.

## الخطوة 2: فتح مستند PDF المصدر

فتح الملف سهل. سنستخدم كتلة `using` حتى يتم تحرير مقبض الملف تلقائيًا.

```csharp
// Step 2: Open the source PDF document
using (var sourceDocument = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

فئة `Document` تمثل ملف PDF بالكامل، وتمنحنا الوصول إلى الصفحات، التعليقات، وبالطبع ترقيم Bates.

## الخطوة 3: تعريف إعدادات ترقيم Bates

الآن يأتي جوهر الأمر—تكوين خيارات **add bates numbering**. يمكنك التحكم في رقم البداية، البادئة، اللاحقة، حجم الخط، الهامش، وحتى تحديد الصفحات التي ستستقبل الختم.

```csharp
// Step 3: Define Bates numbering settings
var batesOptions = new BatesNumberingOptions
{
    StartNumber = 1,                 // First number in the sequence
    Prefix = "ABC-",                 // Text before the number
    Suffix = "-2024",                // Text after the number
    FontSize = 12,                   // Size of the numbering font
    Margin = 10,                     // Distance from the page edge (points)
    PageNumbers = new[] { 1, 2, 3 }  // Pages to which numbering is applied
};
```

### لماذا هذه الإعدادات مهمة

- **StartNumber** يتيح لك متابعة تسلسل من دفعة سابقة.
- **Prefix/Suffix** مفيدان لتحديد هوية القضايا أو طوابع السنة.
- **FontSize** و **Margin** يؤثران على قابلية القراءة؛ الخط الصغير جدًا قد يُفقد في الطباعة.
- **PageNumbers** هو المكان الذي **apply bates numbering** فيه بشكل انتقائي. احذف هذا المصفوفة لترقيم كل صفحة.

إذا كنت بحاجة إلى **add custom page numbers** غير متسلسلة، يمكنك إنشاء قائمة مثل `{5, 10, 15}` وتمريرها هنا.

## الخطوة 4: تطبيق ترقيم Bates على الصفحات المحددة

مع إعداد الخيارات، تقوم المكتبة بالعمل الشاق. الطريقة `AddBatesNumbering` تدرج الختم على كل صفحة مستهدفة.

```csharp
// Step 4: Apply the Bates numbering to the selected pages
sourceDocument.AddBatesNumbering(batesOptions);
```

خلف الكواليس، تقوم Aspose.PDF بإنشاء قطعة نصية لكل صفحة، وتضعها وفقًا للهامش، وتراعي حجم الخط المختار. هذا يضمن ظهور الأرقام بالضبط حيث تتوقع، سواءً عرضت PDF على الشاشة أو طبعتها.

## الخطوة 5: حفظ المستند المعدل

أخيرًا، احفظ التغييرات في ملف جديد حتى يبقى الأصل دون تعديل.

```csharp
// Step 5: Save the modified document with Bates numbers
sourceDocument.Save("YOUR_DIRECTORY/bates.pdf");
```

الآن لديك `bates.pdf` يحتوي على الصفحات المختومة. افتحه بأي عارض PDF وسترى شيئًا مثل:

```
ABC-1-2024   (on page 1, top‑right)
ABC-2-2024   (on page 2, top‑right)
ABC-3-2024   (on page 3, top‑right)
```

### التحقق من النتيجة

فحص سريع للتأكد هو قراءة نص الصفحة الأولى برمجيًا:

```csharp
using (var doc = new Document("YOUR_DIRECTORY/bates.pdf"))
{
    var text = doc.Pages[1].ExtractText();
    Console.WriteLine(text.Contains("ABC-1-2024") ? "Bates number applied!" : "Oops, something went wrong.");
}
```

إذا طبع الطرفية *Bates number applied!*, فأنت في وضع ممتاز.

## الحالات الخاصة والاختلافات الشائعة

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **رقم كل صفحة** | احذف `PageNumbers` أو عيّنها إلى `null` | واجهة API تفترض جميع الصفحات عندما لا يتم توفير المصفوفة. |
| **هامش مختلف لكل جانب** | استخدم `Margin = new MarginInfo { Top = 15, Right = 10 }` (يتطلب Aspose > 23.3) | يوفر لك تحكمًا دقيقًا في الموضع. |
| **مستندات كبيرة (> 500 صفحة)** | فعّل `batesOptions.StartNumber` بقيمة أعلى وفكّر في `batesOptions.FontSize = 10` لتجنب التداخل | يحافظ على وضوح الختم دون إزدحام الصفحة. |
| **تحتاج إلى خط مختلف** | عيّن `batesOptions.Font = FontRepository.FindFont("Arial")` | بعض الشركات القانونية تتطلب نوع خط محدد. |

> **احذر:** إذا قدمت رقم صفحة غير موجود (مثال، `PageNumbers = new[] { 999 }`)، فإن Aspose.PDF يتخطاه بصمت. تحقق دائمًا من النطاق إذا كنت تبني القائمة ديناميكيًا.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. الصقه في تطبيق Console، عدل المسارات، واضغط **F5**.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        // Open the source PDF
        using (var sourceDocument = new Document(sourcePath))
        {
            // Configure Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1,
                Prefix = "ABC-",
                Suffix = "-2024",
                FontSize = 12,
                Margin = 10,
                PageNumbers = new[] { 1, 2, 3 } // Change or remove to number all pages
            };

            // Apply the numbering
            sourceDocument.AddBatesNumbering(batesOptions);

            // Save the new PDF
            sourceDocument.Save(outputPath);
        }

        // Verify the first page contains the expected stamp
        using (var doc = new Document(outputPath))
        {
            string extracted = doc.Pages[1].ExtractText();
            bool success = extracted.Contains("ABC-1-2024");
            Console.WriteLine(success
                ? "Bates numbering added successfully!"
                : "Numbering failed – check your options.");
        }
    }
}
```

تشغيل هذا الكود سيولد `bates.pdf` مع الصفحات الثلاث المختومة المعروضة سابقًا. افتح الملف، وسترى الأرقام محاذاة لليمين، على بعد 10 نقاط من الحافة، بخط بحجم 12 نقطة.

## معاينة بصرية

![معاينة إضافة ترقيم bates](/images/bates-numbering-sample.png)

*توضح لقطة الشاشة أعلاه كيف يبدو ناتج **add bates numbering** بعد تشغيل السكريبت.*

## الخلاصة

لقد غطينا للتو كيفية **add bates numbering** إلى ملف PDF باستخدام C#. من خلال تكوين `BatesNumberingOptions`، تطبيق الختم، وحفظ المستند، لديك الآن حل قابل لإعادة الاستخدام يمكنه أيضًا **add custom page numbers**، **how to number pdf**، و **apply bates numbering** عبر أي مشروع.

الخطوات التالية؟ حاول دمج هذا مع معالج دفعي يتنقل عبر مجلد من ملفات PDF، أو جرب بادئات مختلفة لكل نوع قضية. يمكنك أيضًا استكشاف دمج ملفات PDF متعددة بعد ترقيمها—مفيد لإنشاء حزم قضايا شاملة.

هل لديك أسئلة حول الحالات الخاصة، أو تريد معرفة كيفية تضمين الأرقام في التذييل بدلاً من الرأس؟ اترك تعليقًا، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}