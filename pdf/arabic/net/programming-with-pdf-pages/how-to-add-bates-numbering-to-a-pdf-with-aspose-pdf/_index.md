---
category: general
date: 2026-10-07
description: تعلم كيفية إضافة ترقيم بايتس إلى ملف PDF باستخدام C#. يغطي هذا الدليل
  خطوة بخطوة أيضًا ترقيم صفحات PDF وغيرها من حيل الترقيم.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: ar
lastmod: 2026-10-07
og_description: أضف ترقيم باتس إلى ملف PDF بسرعة. اتبع هذا الدليل لإتقان ترقيم صفحات
  PDF، وترقيم الصفحات، وأتمتة تتبع المستندات.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: إضافة ترقيم باتس إلى ملفات PDF باستخدام C# – دليل Aspose الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: كيفية إضافة ترقيم باتس إلى ملف PDF باستخدام Aspose.Pdf
url: /ar/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة ترقيم بايتس إلى ملف PDF باستخدام Aspose.Pdf

إذا كنت بحاجة إلى **إضافة ترقيم بايتس** إلى ملف PDF، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك في C#. سواء كنت تُعد حزمًا قانونية، أو تدير ملفات القضايا، أو ترغب فقط في الحصول على **ترقيم صفحات PDF** موثوق، فإن الخطوات أدناه توفر لك حلاً كاملاً قابلاً للتنفيذ.

في هذا البرنامج التعليمي ستتعلم كيفية:

* تحميل ملف PDF موجود.
* تكوين خيارات ترقيم بايتس مثل البادئة، رقم البداية، عدد الأرقام، الفاصل، واللاحقة.
* تطبيق الترقيم على كل صفحة.
* حفظ المستند المحدث.

لا توجد أدوات خارجية مطلوبة بخلاف مكتبة Aspose.Pdf لـ .NET، ويعمل الكود مع .NET 6+ وكذلك .NET Framework 4.7.2+.

---

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

| المتطلب | لماذا يهم |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`) | يوفر الفئات `Document` و `BatesNumberingOptions` المستخدمة في الكود. |
| **.NET SDK** (6.0 or later recommended) | يمكنك من تجميع وتشغيل تطبيق وحدة التحكم C#. |
| **A source PDF** you want to number | يستخدم الدليل `source.pdf` كمثال؛ استبدل المسار بملفك الخاص. |
| **Write permission** to the output folder | تحتاج عملية `Save` إلى كتابة الملف الجديد. |

يمكنك تثبيت المكتبة بالأمر التالي في سطر الأوامر:

```bash
dotnet add package Aspose.Pdf
```

---

## الخطوة 1: إنشاء مشروع وحدة تحكم جديد

افتح الطرفية وشغّل:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

هذا ينشئ مشروع C# بسيط سنملأه بالكود اللازم **لإضافة ترقيم بايتس**.

---

## الخطوة 2: إضافة توجيهات `using` المطلوبة

افتح `Program.cs` وأضف مساحات الأسماء في أعلى الملف:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` يتيح لك الوصول إلى الفئة `Document` لتحميل وحفظ ملفات PDF.  
* `Aspose.Pdf.Text` يحتوي على `BatesNumberingOptions`، الكائن الذي يحدد كيفية ظهور الأرقام.

---

## الخطوة 3: تحميل ملف PDF المصدر

السطر القابل للتنفيذ الأول يحمل ملف PDF الذي تريد ترقيمه. استبدل `"YOUR_DIRECTORY/source.pdf"` بالمسار الفعلي لملفك.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

إذا تعذر العثور على الملف، تقوم Aspose بإلقاء استثناء `FileNotFoundException`. لتجنب ذلك، قد ترغب في التحقق من صحة المسار مسبقًا:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## الخطوة 4: تعريف خيارات ترقيم بايتس

`BatesNumberingOptions` يتيح لك التحكم في كل عنصر بصري للترقيم. المثال أدناه يوضح تكوينًا نموذجيًا لملفات القضايا القانونية:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**لماذا كل خاصية مهمة**

| الخاصية | الغرض |
|----------|---------|
| `Prefix` | يساعدك على تجميع المستندات حسب المشروع أو العميل أو القضية. |
| `StartNumber` | يضبط العداد الأولي؛ مفيد عندما يكون لديك ملفات مرقمة بالفعل. |
| `Digits` | يضمن عرضًا موحدًا، مما يسهل الفرز. |
| `Separator` | يحسن القراءة، خاصة عند دمج البادئة واللاحقة. |
| `Suffix` | يسمح لك بإضافة سنة أو نسخة أو أي معرف لاحق. |

يمكنك أيضًا التحكم في الموضع (أعلى، أسفل، يسار، يمين) ونمط الخط عبر `batesOptions.Position` و `batesOptions.Font`. بالنسبة لمعظم السيناريوهات، الإعدادات الافتراضية (أسفل‑يمين، 12‑pt Times New Roman) تعمل بشكل جيد.

---

## الخطوة 5: تطبيق الترقيم على كل صفحة

استدعاء `pdf.BatesNumbering.Add` يدرج الأرقام على كل صفحة بالترتيب الذي تظهر به.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

إذا كنت بحاجة إلى **ترقيم صفحات pdf** فقط على مجموعة فرعية (مثلاً تخطي صفحة الغلاف)، يمكنك تمرير `PageCollection` بدلاً من ذلك:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## الخطوة 6: حفظ ملف PDF المحدث

أخيرًا، اكتب المستند المعدل إلى القرص. عادةً ما يعكس اسم الملف أن PDF الآن يحتوي على أرقام بايتس.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

إذا لم يكن مجلد الإخراج موجودًا، تقوم Aspose بإنشائه تلقائيًا. ومع ذلك، يجب التأكد من وجود أذونات كتابة لتجنب استثناء `UnauthorizedAccessException`.

---

## مثال كامل وقابل للتنفيذ

بجمع كل الأجزاء معًا، إليك برنامج كامل يمكنك نسخه، لصقه، وتشغيله:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**الناتج المتوقع** (في وحدة التحكم):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

افتح `bates_numbered.pdf` وسترى كل صفحة مُعلمة بشيء مثل `CASE-001000-2025`, `CASE-001001-2025`, إلخ، موضوعة في الزاوية السفلية‑اليمنى الافتراضية.

---

## الأسئلة المتكررة (FAQ)

### 1. هل يمكنني تغيير موقع الأرقام؟
نعم. اضبط `batesOptions.Position = new Position(10, 10, 10, 10);` حيث تمثل القيم الأربع الهوامش من الأعلى، الأسفل، اليسار، واليمين. توفر Aspose أيضًا تعدادًا مسبقًا مثل `BatesNumberingPosition.BottomCenter`.

### 2. ماذا لو كان ملف PDF الخاص بي يحتوي بالفعل على أرقام الصفحات؟
إضافة أرقام بايتس ستُـ**تراكب** فوق الأرقام الموجودة. لتجنب الفوضى البصرية، إما إخفِ الأرقام الأصلية (إذا كانت جزءًا من طبقة نص) أو عدل حجم الخط وموقع `batesOptions`.

### 3. هل يعمل هذا مع ملفات PDF المشفرة؟
يمكن لـ Aspose فتح ملفات PDF المحمية بكلمة مرور إذا زودتها بكلمة المرور:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

ثم يتم تطبيق ترقيم بايتس بنفس الطريقة.

### 4. كيف يمكنني **ترقيم صفحات pdf** باستخدام عداد تسلسلي بسيط (بدون بادئة/لاحقة)؟
ما عليك سوى ضبط `Prefix = string.Empty` و `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. هل يمكنني استخدام هذا النهج في ASP.NET Core لتقديم ملفات PDF مباشرةً؟
بالطبع. حمّل المستند، طبّق الترقيم، ثم اكتب التيار إلى استجابة HTTP:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## الحالات الخاصة ونصائح أفضل الممارسات

| الحالة | النهج الموصى به |
|-----------|----------------------|
| **ملفات PDF الكبيرة (مئات الصفحات)** | استدعِ `pdf.BatesNumbering.Add` **بعد** إجراء أي تحويلات على مستوى الصفحات لتجنب إعادة معالجة نفس الصفحات عدة مرات. |
| **خطوط مخصصة** | اضبط `batesOptions.Font = FontRepository.FindFont("Arial")` وعدل `batesOptions.FontSize` لتحسين القراءة على المستندات الممسوحة ضوئيًا. |
| **وظائف الدُفعات ذات الأداء الحرج** | أعد استخدام كائن `Document` واحد عند معالجة العديد من الملفات في حلقة؛ حرره بعد كل تكرار لتفريغ الذاكرة. |
| **حروف دولية** | استخدم خطوطًا متوافقة مع Unicode (مثل `Times New Roman Unicode`) لضمان عرض البادئة أو اللاحقة بشكل صحيح. |
| **توافق الإصدارات** | يعمل الكود مع Aspose.Pdf 23.10 وما بعده. إذا استهدفت إصدارًا أقدم، تحقق من مرجع API لأي تغييرات في أسماء الخصائص. |

---

## الخاتمة

أنت الآن تعرف كيف **تضيف ترقيم بايتس** إلى ملف PDF باستخدام Aspose.Pdf لـ .NET. غطى البرنامج التعليمي تحميل PDF، تكوين `BatesNumberingOptions`، تطبيق الأرقام على كل صفحة، وحفظ النتيجة. باستخدام هذه المكوّنات يمكنك أيضًا تنفيذ **ترقيم صفحات PDF** عام، **ترقيم صفحات pdf** بصيغ مخصصة، ودمج العملية في خطوط أتمتة أكبر.

**الخطوات التالية**

* استكشف واجهة برمجة تطبيقات **bates numbering pdf** أكثر لتخصيص الخط واللون والموقع.  
* دمج هذه التقنية مع **التوقيعات الرقمية** لإنشاء حزم قانونية مقاومة للعبث.  
* اطلع على إمكانيات **دمج PDF** من Aspose إذا كنت بحاجة إلى ربط ملفات قضايا متعددة قبل الترقيم.

لا تتردد في تجربة بادئات، لاحقات، وأطوال أرقام مختلفة لتتناسب مع معايير حفظ الملفات في مؤسستك. Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند PDF C# – دليل إضافة ترقيم بايتس](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [كيفية إضافة ترقيم بايتس في PDF باستخدام C# – دليل كامل](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [دروس Aspose PDF – إدراج صفحة فارغة وتحديث ترقيم بايتس](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}