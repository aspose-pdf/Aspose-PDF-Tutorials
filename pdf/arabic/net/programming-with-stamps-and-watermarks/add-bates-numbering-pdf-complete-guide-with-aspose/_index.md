---
category: general
date: 2026-06-08
description: إضافة ترقيم باتس إلى ملف PDF باستخدام Aspose.Pdf في C#. تعلم كيفية إضافة
  ترقيم باتس، إضافة أرقام الصفحات إلى PDF، إضافة أرقام متسلسلة إلى PDF، وشاهد مثالًا
  على ترقيم باتس في PDF.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: ar
og_description: إضافة ترقيم باتس إلى ملف PDF باستخدام C#. يُظهر هذا الدرس كيفية إضافة
  ترقيم باتس، وإضافة أرقام الصفحات إلى PDF، وإضافة أرقام متسلسلة إلى PDF مع مثال كامل
  على ترقيم باتس للملف PDF.
og_title: إضافة ترقيم بايتس إلى PDF – دليل كامل مع Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: إضافة ترقيم بيتس إلى PDF – دليل شامل مع Aspose
url: /ar/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم بايتس PDF – دليل البرمجة الكامل

هل احتجت يومًا إلى **add bates numbering pdf** لكنك لم تكن متأكدًا من أين تبدأ؟ إذا تساءلت يومًا *how to add bates* إلى مستند قانوني، فأنت في المكان الصحيح. في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية لا يضيف أرقام بايتس فحسب، بل يوضح لك أيضًا كيفية **add page numbers pdf**، **add sequential numbers pdf**، وحتى يوفر لك **bates number pdf example** جاهزًا للتنفيذ.

سنستخدم مكتبة Aspose.Pdf لـ .NET، لأنها تُجرد التفاصيل الداخلية منخفضة المستوى لملفات PDF مع منحك تحكمًا دقيقًا. بنهاية هذا الدليل ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع C#، وستفهم لماذا كل سطر مهم.

## ما الذي ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا على .NET Framework 4.6+).  
- **رخصة** لـ Aspose.Pdf أو مفتاح تقييم مؤقت مجاني.  
- ملف PDF تجريبي يُدعى `input.pdf` موجود في مجلد يمكنك الإشارة إليه.  
- Visual Studio أو Rider أو أي محرر C# تفضله.

هذا كل شيء—لا أدوات إضافية، ولا تمارين سطر أوامر. هل أنت مستعد؟ لنبدأ.

## إضافة ترقيم بايتس PDF – تنفيذ خطوة بخطوة

فيما يلي نقسم العملية إلى ست خطوات منطقية. كل خطوة تتضمن مقتطف كود قصير، شرحًا لـ *لماذا* نقوم بذلك، ونصيحة قد تكون مفيدة.

### الخطوة 1: تثبيت حزمة Aspose.Pdf عبر NuGet

أولاً، أضف المكتبة إلى مشروعك. افتح نافذة Package Manager Console وشغّل:

```powershell
Install-Package Aspose.Pdf
```

> **نصيحة احترافية:** إذا كنت تستخدم .NET Core، يمكنك أيضًا استخدام `dotnet add package Aspose.Pdf`.

تثبيت الحزمة يمنحك الوصول إلى الفئة `Aspose.Pdf.Facades.BatesNumbering`، وهي المسؤولة عن **add bates numbering pdf**.

### الخطوة 2: فتح مستند PDF المصدر

الآن نقوم بتحميل ملف PDF الذي نريد وضع العلامة عليه. يضمن بيان `using` إغلاق الملف بشكل صحيح حتى في حال حدوث استثناء.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

لماذا نستخدم `Aspose.Pdf.Document`؟ لأنها تمثل ملف PDF بالكامل في الذاكرة، مما يتيح لنا تعديل الصفحات، الخطوط، والبيانات الوصفية دون لمس الملف الأصلي على القرص.

### الخطوة 3: إنشاء واجهة Bates Numbering

نمط *الواجهة* (facade) يخفي تعقيد بنية PDF الداخلية. إليك كيفية إنشاء الكائن:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

سيتم لاحقًا تكوين هذا الكائن بإضافة بادئة، رقم بدء، وخيارات تنسيق. فكر فيه كـ “المحرك” الذي سيقوم بـ **add page numbers pdf** بطريقة متوافقة مع Bates.

### الخطوة 4: ضبط رقم البداية والبادئة

غالبًا ما تتضمن أرقام Bates بادئة خاصة بالقضية. يمكنك أيضًا التحكم في عدد الأرقام، الفاصل، وموقعها على الصفحة.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**لماذا هذه الإعدادات؟**  
- `StartNumber` يتيح لك متابعة سلسلة سابقة.  
- `NumberOfDigits` يضمن طولًا موحدًا، وهو أمر حاسم للفهرسة القانونية.  
- `Location` يحدد مكان ظهور **add sequential numbers pdf**؛ يمكنك نقله إلى أعلى اليمين إذا رغبت.

### الخطوة 5: تطبيق ترقيم Bates على المستند

بعد تكوين الواجهة، نقوم الآن بوضع العلامة على كل صفحة:

```csharp
bates.AddBatesNumbering(doc);
```

في الخلفية، تقوم Aspose بالتكرار عبر كل صفحة، وترسم النص في الموقع المحدد، وتحترم أي محتوى موجود. هذا السطر الواحد هو ما يضيف فعليًا **add bates numbering pdf** إلى ملفك.

### الخطوة 6: حفظ ملف PDF المعدل

أخيرًا، اكتب النتيجة إلى القرص:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

الآن لديك ملف PDF حيث يحمل كل صفحة معرف Bates فريد، جاهز للاكتشاف أو تقديمه في المحكمة.

#### مثال كامل يعمل (Bates Number PDF Example)

بتجميع كل ذلك، إليك برنامج كامل ومستقل يمكنك تجميعه وتشغيله:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **الناتج المتوقع:** افتح `output.pdf` وسترى “CASE‑01000”، “CASE‑01001”، … في أسفل‑يسار كل صفحة.

![لقطة شاشة لصفحة PDF بأرقام Bates في الزاوية السفلية اليسرى – مثال إضافة ترقيم بايتس PDF](https://example.com/bates-numbering-screenshot.png "مثال إضافة ترقيم بايتس PDF")

*(نص بديل للصورة: *add bates numbering pdf example* – يُظهر أرقام Bates المطبقة على ملف PDF تجريبي.)*

## كيفية إضافة Bates – فهم الواجهة

قد تتساءل **how to add bates** بدون واجهة Aspose. البديل هو رسم النص يدويًا على كل صفحة باستخدام أوامر PDF منخفضة المستوى، لكن هذا الأسلوب عرضة للأخطاء ويتطلب معرفة عميقة بمواصفات PDF. الواجهة تُجرد هذه التفاصيل، مما يتيح لك التركيز على *ما* تريد (بادئة، رقم بدء) بدلاً من *كيف* يتم عرضه.

إذا احتجت يومًا إلى **add page numbers pdf** بنمط غير Bates (مثلًا، “Page 3 of 12”)، يمكنك إعادة استخدام نفس الفئة `BatesNumbering`—فقط غيّر `Prefix` إلى سلسلة فارغة واضبط `Location`. المحرك الأساسي هو نفسه، مما يعني حصولك على عرض متسق في الحالتين.

## إضافة أرقام الصفحات PDF – تخصيص الموضع والنمط

غالبًا ما تطلب الفرق القانونية رقم الصفحة في الرأس، بينما يفضّل فريق الدعم القضائي وضعه في التذييل. إليك تعديلًا سريعًا:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

ستقوم نفس استدعاء `AddBatesNumbering` الآن بـ **add page numbers pdf** في أعلى كل صفحة. نظرًا لأن الواجهة تعمل على كائن المستند، يمكنك التبديل بين Bates وترقيم الصفحات العادي ببضع تغييرات في الخصائص—دون الحاجة لإعادة كتابة الحلقة.

## إضافة أرقام متسلسلة PDF – تنسيق متقدم

افترض أنك تحتاج إلى تنسيق مثل `2023-CASE-00123`. يمكنك دمج بادئة تاريخ مع الإعدادات الحالية:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

الآن سيظهر على كل صفحة `2023-CASE-00123`، `2023-CASE-00124`، إلخ. هذا يوضح مدى سهولة **add sequential numbers pdf** التي تلبي تسميات معقدة.

## الحالات الخاصة والمشكلات الشائعة

| الحالة | ما الذي يجب الانتباه إليه | الإصلاح المقترح |
|-----------|----------------------|---------------|
| **ملفات PDF كبيرة جدًا ( > 500 MB )** | يمكن أن يرتفع استهلاك الذاكرة لأن المستند بالكامل يُحمَّل في الذاكرة العشوائية. | استخدم `Document` مع إعدادات `MemoryManagement` أو عالج الملف على أجزاء باستخدام `PdfFileEditor`. |
| **أرقام الصفحات الموجودة** |  |  |

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إضافة وتخصيص أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET | دليل معالجة المستندات](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [كيفية إضافة طوابع أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET | العلامات المائية والخلفيات](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: إضافة أرقام الصفحات إلى ملفات PDF باستخدام FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}