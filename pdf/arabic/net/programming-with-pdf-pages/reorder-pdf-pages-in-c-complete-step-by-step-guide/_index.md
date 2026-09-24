---
category: general
date: 2026-03-27
description: تعلم كيفية إعادة ترتيب صفحات PDF، وإدراج صفحة PDF، وإضافة صفحة PDF فارغة،
  وإلحاق صفحة PDF باستخدام Aspose.PDF. أخيرًا، احفظ ملف PDF المحدث ببضع أسطر فقط من
  C#.
draft: false
keywords:
- reorder pdf pages
- insert pdf page
- add blank pdf page
- append pdf page
- save updated pdf
language: ar
og_description: إعادة ترتيب صفحات PDF، إدراج صفحة PDF، إضافة صفحة PDF فارغة وإلحاق
  صفحة PDF في C#. احفظ PDF المحدث فورًا باستخدام Aspose.PDF.
og_title: إعادة ترتيب صفحات PDF في C# – دليل خطوة بخطوة كامل
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: إعادة ترتيب صفحات PDF في C# – دليل خطوة بخطوة كامل
url: /ar/net/programming-with-pdf-pages/reorder-pdf-pages-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إعادة ترتيب صفحات PDF في C# – دليل خطوة‑ بخطوة كامل

هل احتجت يومًا إلى **إعادة ترتيب صفحات PDF** لكن لم تعرف من أين تبدأ؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يكتشفون ملف PDF غير متسلسل، أو غياب صفحة الغلاف، أو الحاجة إلى إدراج صفحة جديدة في وسط تقرير. الخبر السار؟ ببضع أسطر من C# و Aspose.PDF يمكنك إعادة ترتيب صفحات PDF، **إدراج صفحة PDF**، **إضافة صفحة PDF فارغة**، **إلحاق صفحة PDF**، ثم **حفظ PDF المحدث** دون عناء.

في هذا الدرس سنستعرض سيناريو واقعي: أخذ مستند موجود، نقل الصفحة 5 إلى الموضع 2، إضافة صفحة فارغة جديدة في النهاية، تحديث جميع أرقام الصفحات، وأخيرًا حفظ التغييرات. بنهاية الدرس ستحصل على حل مستقل يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- **Aspose.PDF for .NET** (أي نسخة حديثة؛ الـ API المستخدم هنا يعمل مع 23.10 وما بعده).  
- بيئة تطوير .NET (Visual Studio، Rider، أو سطر أوامر `dotnet`).  
- ملف PDF موجود (للتجربة سنستخدم `DocWithHeaders.pdf`).  

لا تحتاج إلى أي حزم NuGet إضافية بخلاف Aspose.PDF، والكود يعمل على .NET 6، .NET 7، أو .NET Framework الكلاسيكي.

## الخطوة 1: تحميل مستند PDF (إعادة ترتيب صفحات PDF)

أول شيء تقوم به عندما تريد **إعادة ترتيب صفحات PDF** هو تحميل الملف إلى الذاكرة. تمثل فئة `Document` في Aspose.PDF الـ PDF بالكامل، وتوفر مجموعة `Pages` وصولًا مباشرًا إلى كل صفحة.

```csharp
using Aspose.Pdf;

// Load the source PDF – replace the path with your own file location
using (var pdfDocument = new Document("YOUR_DIRECTORY/DocWithHeaders.pdf"))
{
    // The document is now ready for manipulation
}
```

> **لماذا هذا مهم:** تحميل المستند يُنشئ رسمًا بيانيًا كائنًا يمكن إدارته. جميع العمليات اللاحقة—سواء كنت تُدخل صفحة أو تُحدّث ترقيم الصفحات—تعمل على هذا التمثيل في الذاكرة، وهو أسرع بكثير من عمليات الإدخال/الإخراج على القرص لكل تعديل.

## الخطوة 2: إدراج صفحة PDF في موضع محدد

الآن بعد تحميل المستند، لنـ **نُدرج صفحة PDF** 5 في الموضع 2. الصفحات في Aspose.PDF تُرقم من 1، لذا يمكن الإشارة إليها مباشرة.

```csharp
// Inside the using block from Step 1
// Insert a copy of page 5 at position 2 (pages are 1‑based)
pdfDocument.Pages.Insert(2, pdfDocument.Pages[5]);
```

> **نصيحة احترافية:** طريقة `Insert` تنسخ الصفحة المصدر، وتترك الأصل في مكانه. إذا كنت تريد *نقل* الصفحة بدلاً من نسخها، استدعِ `pdfDocument.Pages.RemoveAt(5)` بعد الإدراج.

## الخطوة 3: إضافة صفحة PDF فارغة في النهاية (إضافة صفحة PDF فارغة)

متطلب شائع بعد إعادة الترتيب هو إعطاء المستند ختامًا نظيفًا—ربما غلاف خلفي أو صفحة توقيع. هنا يأتي دور **إضافة صفحة PDF فارغة**.

```csharp
// Append a new blank page at the end of the document
pdfDocument.Pages.Add();
```

> **لماذا قد تحتاج هذا:** الصفحات الفارغة مفيدة للفصل، أو متطلبات الطباعة، أو ببساطة للحفاظ على عدد الصفحات زوجيًا.

## الخطوة 4: تحديث أرقام الصفحات تلقائيًا (إلحاق صفحة PDF وتحديث الترقيم)

إذا كان PDF يحتوي على حقول أرقام الصفحات (مثل تقرير يحتوي على تذييل “Page 1 of 10”)، فستحتاج إلى **إلحاق صفحة PDF** بأرقام تعكس الترتيب الجديد. يمكن لـ Aspose.PDF القيام بذلك في استدعاء واحد:

```csharp
// Refresh all page‑number and date fields automatically
pdfDocument.Pages.UpdatePagination();
```

> **ما يحدث خلف الكواليس:** `UpdatePagination` يمسح كل صفحة بحثًا عن عناصر نائبة مثل `{PageNumber}` و `{PageCount}` ويحدّثها بناءً على ترتيب الصفحات الحالي. لا حاجة للتكرار اليدوي.

## الخطوة 5: حفظ PDF المحدث (حفظ PDF محدث)

أخيرًا، **نحفظ PDF المحدث** على القرص. يمكنك استبدال الملف الأصلي، أو—لأمان أكثر—الكتابة إلى ملف جديد.

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/UpdatedPagination.pdf");
```

> **نصيحة:** إذا كنت بحاجة إلى بث الـ PDF إلى عميل ويب، استخدم `pdfDocument.Save(stream, SaveFormat.Pdf)` بدلاً من مسار ملف.

## مثال كامل يعمل

نجمع كل ما سبق في برنامج كامل قابل للتنفيذ. انسخه‑الصقه في تطبيق Console، عدّل مسارات الملفات، ثم اضغط **Run**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var pdfDocument = new Document("YOUR_DIRECTORY/DocWithHeaders.pdf"))
        {
            // Step 2: Insert a copy of page 5 at position 2 (pages are 1‑based)
            pdfDocument.Pages.Insert(2, pdfDocument.Pages[5]);

            // Step 3: Append a new blank page at the end of the document
            pdfDocument.Pages.Add();

            // Step 4: Refresh all page‑number and date fields automatically
            pdfDocument.Pages.UpdatePagination();

            // Step 5: Save the updated PDF
            pdfDocument.Save("YOUR_DIRECTORY/UpdatedPagination.pdf");
        }

        System.Console.WriteLine("PDF reordering complete! Check UpdatedPagination.pdf.");
    }
}
```

### النتيجة المتوقعة

- **الترتيب الأصلي:** 1 2 3 4 5 6 7 …  
- **بعد الخطوة 2:** 1 5 2 3 4 6 7 … (الصفحة 5 أصبحت الآن الثانية).  
- **بعد الخطوة 3:** تظهر صفحة فارغة كآخر صفحة (مثلاً الصفحة N+1).  
- **بعد الخطوة 4:** جميع حقول `{PageNumber}` الآن تعكس التسلسل الجديد (الصفحة 2 تُظهر “2”، إلخ).  
- **بعد الخطوة 5:** الملف `UpdatedPagination.pdf` يحتوي على المحتوى المعاد ترتيبه، الصفحة الفارغة الإضافية، والترقيم الصحيح.

يمكنك فتح الـ PDF الناتج بأي عارض للتحقق من أن الصفحات بالترتيب المطلوب وأن التذييلات تعرض الأرقام الصحيحة.

![مثال على إعادة ترتيب صفحات PDF](reorder-pdf-pages.png "لقطة شاشة تُظهر صفحات PDF المعاد ترتيبها")

*نص بديل للصورة:* **إعادة ترتيب صفحات PDF** لقطة شاشة توضح ترتيب الصفحات الجديد

## تنوعات شائعة وحالات حافة

### إدراج صفحات متعددة

إذا احتجت إلى **إدراج صفحة PDF** متعددة المرات (مثلاً إخلاء مسؤولية بعد كل فصل)، ببساطة كرّر الحلقة على الصفحات المصدر:

```csharp
for (int i = 1; i <= pdfDocument.Pages.Count; i++)
{
    if (ShouldInsertAfter(i))
        pdfDocument.Pages.Insert(i + 1, pdfDocument.Pages[disclaimerPageIndex]);
}
```

### إضافة صفحة فارغة مخصصة (الحجم، الاتجاه)

الطريقة الافتراضية `Add()` تُنشئ صفحة بحجم A4 بوضعية عمودية. للتحكم في الحجم:

```csharp
var blank = pdfDocument.Pages.Add();
blank.PageInfo.Width = 595;   // 8.27 in (A4 width in points)
blank.PageInfo.Height = 842;  // 11.69 in (A4 height in points)
blank.PageInfo.Orientation = PageOrientation.Landscape;
```

### إلحاق صفحات من مستند آخر

أحيانًا تريد **إلحاق صفحة PDF** من ملف مختلف تمامًا:

```csharp
var extraDoc = new Document("ExtraSection.pdf");
pdfDocument.Pages.Append(extraDoc.Pages);
```

### الحفظ إلى تدفق للواجهات البرمجية للويب

عند بناء نقطة نهاية ASP.NET Core، قد تفضّل **حفظ PDF محدث** مباشرة إلى تدفق ذاكرة:

```csharp
using var ms = new MemoryStream();
pdfDocument.Save(ms, SaveFormat.Pdf);
ms.Position = 0; // Reset for reading
return File(ms, "application/pdf", "Updated.pdf");
```

## نصائح احترافية ومخاطر

- **تجنّب تكرار أرقام الصفحات:** إذا أضفت حقول نصية لأرقام الصفحات يدويًا، تأكّد من أنها ليست ثابتة. استخدم العنصر النائب `{PageNumber}` في Aspose حتى يتمكن `UpdatePagination` من أداء مهمته.  
- **نصيحة الأداء:** للـ PDFs الضخمة (مئات الصفحات)، فكر في تعطيل `pdfDocument.Compress` أثناء التلاعب وأعد تفعيله قبل الحفظ لتقليل حجم الملف.  
- **سلامة الخيوط:** فئة `Document` غير آمنة للاستخدام المتعدد الخيوط. إذا كنت تعالج العديد من ملفات PDF بالتوازي، أنشئ نسخة `Document` منفصلة لكل خيط.

## الخلاصة

غطّينا كل ما تحتاجه لـ **إعادة ترتيب صفحات PDF** في C#: تحميل المستند، **إدراج صفحة PDF**، **إضافة صفحة PDF فارغة**، **إلحاق صفحة PDF**، تحديث الترقيم، وأخيرًا **حفظ PDF محدث**. النهج بسيط، يتطلب فقط Aspose.PDF، ويتوسع من التقارير الصغيرة إلى الأدلة المؤسسية الكبيرة.

هل أنت مستعد للتحدي التالي؟ جرّب استخراج صفحات محددة، دمج عدة PDFs، أو إضافة علامات مائية—كل هذه المهام تبني على مجموعة `Pages` التي استخدمناها هنا. جرّب، واختبر، ودع المكتبة تتولى الأعمال الثقيلة.

إذا وجدت هذا الدليل مفيدًا، شاركه، اترك تعليقًا بحالتك الخاصة، أو استكشف وثائق Aspose.PDF لمزيد من التخصيصات المتعمقة. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}