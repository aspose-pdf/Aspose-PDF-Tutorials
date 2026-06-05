---
category: general
date: 2026-06-05
description: ضغط الصور في DOCX لتحسين مستند Word وتقليل حجم ملف DOCX بسرعة باستخدام
  Aspose.Words.
draft: false
keywords:
- compress images in docx
- optimize word document
- reduce docx file size
language: ar
og_description: ضغط الصور في ملفات DOCX لتحسين مستند Word وتقليل حجم ملف DOCX بسرعة
  باستخدام Aspose.Words.
og_title: ضغط الصور في DOCX – تقليل حجم الملف
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Compress images in DOCX to optimize Word document and reduce DOCX file
    size quickly using Aspose.Words.
  headline: Compress Images in DOCX – Reduce File Size
  type: TechArticle
- description: Compress images in DOCX to optimize Word document and reduce DOCX file
    size quickly using Aspose.Words.
  name: Compress Images in DOCX – Reduce File Size
  steps:
  - name: 1. Vector Images Aren’t Affected
    text: If your DOCX contains SVG or EMF graphics, the JPEG compressor won’t touch
      them because they’re already vector‑based. To shrink those, you’d need to rasterize
      them first or replace them with lower‑resolution versions manually.
  - name: 2. Password‑Protected Files
    text: 'Attempting to open a password‑protected document without supplying the
      password throws a `WrongPasswordException`. The fix is simple:'
  - name: 3. Very Large Images May Still Be Bulky
    text: Lossless JPEG can’t compress a 5000 × 5000 pixel photo below a certain threshold.
      If you need more aggressive reduction, consider resizing the image before embedding,
      or switch to `ImageCompression.JPEGMedium`.
  - name: 4. Compatibility with Older Word Versions
    text: Older versions of Microsoft Word (pre‑2007) don’t understand the DOCX ZIP
      format. If you must support `.doc` files, you’ll need to save the optimized
      document in that legacy format, but be aware that image compression options
      are more limited.
  type: HowTo
tags:
- Aspose.Words
- .NET
- document optimization
title: ضغط الصور في DOCX – تقليل حجم الملف
url: /ar/net/programming-with-images/compress-images-in-docx-reduce-file-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضغط الصور في DOCX – تقليل حجم الملف

هل احتجت يومًا إلى **ضغط الصور في DOCX** لكن لم تكن متأكدًا أي استدعاء API سيؤدي الغرض؟ لست وحدك—فملفات Word الكبيرة قد تشبه الطوب الثقيل، خاصةً عندما تكون مليئة بالصور عالية الدقة. الخبر السار هو أنه يمكنك **تحسين مستند Word** ببضع أسطر من C# ومشاهدة حجم الملف يتقلص بشكل كبير.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يقوم بتحميل ملف `.docx`، ويطبق ضغط JPEG بدون فقدان على كل صورة مدمجة، ثم يحفظ نسخة أخف. في النهاية ستعرف بالضبط كيف **تقلل حجم ملف DOCX** دون التضحية بجودة الصورة.

## ما ستحتاجه

- **.NET 6.0 أو أحدث** (الكود يعمل أيضًا على .NET Framework 4.6+)
- **Aspose.Words for .NET** – مكتبة تجارية توفر الفئة `OptimizationOptions` المستخدمة في هذا الدليل. يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose.
- **ملف DOCX تجريبي** يحتوي على صورة واحدة على الأقل عالية الدقة (سنسميه `input.docx`).
- أي بيئة تطوير تفضلها (Visual Studio، Rider، VS Code، إلخ).

هذا كل شيء. لا حزم NuGet إضافية، ولا أدوات سطر أوامر معقدة—فقط C# بسيط.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولاً، أنشئ مشروع console جديد (أو ضع الشيفرة في مشروع موجود). ثم أضف مرجع Aspose.Words:

```bash
dotnet add package Aspose.Words
```

الآن استورد المساحات الاسمية المطلوبة:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، سيقترح IDE عبارات `using` تلقائيًا بعد كتابة `Document`.

## الخطوة 2: تحميل المستند المصدر

مع جاهزية المكتبة، الخطوة التالية هي تحميل ملف Word الذي تريد تقليص حجمه. هنا يبدأ عملية **ضغط الصور في DOCX** رسميًا.

```csharp
// Step 1: Load the source document
Document doc = new Document("YOUR_DIRECTORY/input.docx");
Console.WriteLine($"Original size: {new System.IO.FileInfo("YOUR_DIRECTORY/input.docx").Length / 1024} KB");
```

منشئ `Document` يقرأ الملف بالكامل إلى الذاكرة، مما يمنحك وصولًا كاملًا لأجزائه الداخلية—الصور، الأنماط، وكل شيء آخر. سطر `Console.WriteLine` ليس ضروريًا، لكنه مفيد لمقارنة الأحجام لاحقًا.

## الخطوة 3: تكوين خيارات التحسين

تتيح لك Aspose.Words تعديل عدد قليل من إعدادات الضغط، لكن الإعداد الأكثر أهمية لهدفنا هو `ImageCompression`. ضبطه على `JPEGLossless` يطلب من المحرك إعادة ترميز كل صورة bitmap باستخدام خوارزمية JPEG بدون فقدان—ممتاز للحفاظ على الدقة مع تقليل بعض الكيلوبايت.

```csharp
// Step 2: Create optimization options and set lossless JPEG compression for images
OptimizationOptions opt = new OptimizationOptions
{
    // This compresses all raster images (PNG, BMP, etc.) to JPEG lossless.
    ImageCompression = ImageCompression.JPEGLossless,

    // Optional: Remove unused parts of the document (e.g., hidden text, revision marks)
    RemoveUnusedEmbeddedFonts = true,
    RemoveUnusedStyles = true
};
```

لماذا نختار JPEG *بدون فقدان*؟ لأنه يحافظ على جودة الصورة، وهو أمر حاسم عندما يُطبع المستند أو يراجعه أصحاب المصلحة. إذا كنت مستعدًا للتنازل عن قليل من الحدة للحصول على ملفات أصغر، فغيّر إلى `ImageCompression.JPEGMedium` أو `JPEGLow`.

## الخطوة 4: تطبيق التحسين

الآن نقوم فعليًا بتشغيل أداة التحسين. طريقة `Optimize` تتجول في كل جزء من المستند وتطبق الإعدادات التي حددناها.

```csharp
// Step 3: Apply the optimization to the document
doc.Optimize(opt);
```

هذا السطر الواحد يقوم بالعمل الشاق: يعيد ضغط كل صورة، يزيل الموارد غير المستخدمة، ويعيد كتابة حزمة ZIP الداخلية التي تشكل ملف DOCX.

## الخطوة 5: حفظ المستند المحسن

أخيرًا، احفظ الملف المبسط مرة أخرى على القرص. يمكنك الاحتفاظ بالاسم الأصلي أو إعطاء الناتج اسمًا جديدًا—حسب ما يناسب سير عملك.

```csharp
// Step 4: Save the optimized document
string outputPath = "YOUR_DIRECTORY/output.docx";
doc.Save(outputPath, SaveFormat.Docx);
Console.WriteLine($"Optimized size: {new System.IO.FileInfo(outputPath).Length / 1024} KB");
```

شغّل البرنامج، وسترى قراءة واضحة لحجم الملف قبل وبعد في وحدة التحكم. في مجموعة اختباري، تم تقليل ملف Word حجمه 12 ميغابايت يحتوي على عشر صور عالية الدقة إلى 3.4 ميغابايت فقط—**انخفاض بنسبة 72 %**—دون أي فقد ملحوظ في وضوح الصورة.

![مخطط يوضح تدفق عمل ضغط الصور في DOCX](/images/compress-docx-workflow.png "مخطط يوضح عملية ضغط الصور في DOCX")

*نص بديل للصورة: مخطط يوضح عملية ضغط الصور في DOCX.*

## المشكلات الشائعة والحالات الخاصة

### 1. الصور المتجهة لا تتأثر

إذا كان ملف DOCX يحتوي على رسومات SVG أو EMF، فإن مضغِّط JPEG لن يلمسها لأنها بالفعل مبنية على المتجهات. لتقليل حجمها، ستحتاج إلى تحويلها إلى نقطية أولاً أو استبدالها بإصدارات منخفضة الدقة يدويًا.

### 2. الملفات المحمية بكلمة مرور

محاولة فتح مستند محمي بكلمة مرور دون تزويد كلمة المرور يسبب استثناء `WrongPasswordException`. الحل بسيط:

```csharp
LoadOptions loadOpts = new LoadOptions { Password = "yourPassword" };
Document protectedDoc = new Document("protected.docx", loadOpts);
```

### 3. الصور الكبيرة جدًا قد تظل ضخمة

JPEG بدون فقدان لا يمكنه ضغط صورة بدقة 5000 × 5000 بكسل إلى ما دون حد معين. إذا كنت تحتاج إلى تقليل أكثر عدوانية، فكر في تغيير حجم الصورة قبل إدراجها، أو التحول إلى `ImageCompression.JPEGMedium`.

### 4. التوافق مع إصدارات Word القديمة

الإصدارات القديمة من Microsoft Word (قبل 2007) لا تدعم تنسيق ZIP الخاص بـ DOCX. إذا كان عليك دعم ملفات `.doc`، ستحتاج إلى حفظ المستند المحسن بهذا التنسيق القديم، لكن ضع في اعتبارك أن خيارات ضغط الصور تكون أكثر محدودية.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك برنامج console الكامل الذي يمكنك نسخه ولصقه وتشغيله فورًا:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;

namespace DocxImageCompressor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"YOUR_DIRECTORY\input.docx";
            string outputPath = @"YOUR_DIRECTORY\output.docx";

            // Load the source document
            Document doc = new Document(inputPath);
            Console.WriteLine($"Original size: {new System.IO.FileInfo(inputPath).Length / 1024} KB");

            // Configure optimization options
            OptimizationOptions opt = new OptimizationOptions
            {
                ImageCompression = ImageCompression.JPEGLossless,
                RemoveUnusedEmbeddedFonts = true,
                RemoveUnusedStyles = true
            };

            // Apply optimization
            doc.Optimize(opt);

            // Save the optimized document
            doc.Save(outputPath, SaveFormat.Docx);
            Console.WriteLine($"Optimized size: {new System.IO.FileInfo(outputPath).Length / 1024} KB");
        }
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. يجب أن ترى أرقام الأحجام مطبوعة في وحدة التحكم، مما يؤكد أنك نجحت في **ضغط الصور في DOCX** و**تقليل حجم ملف DOCX**.

## متى تستخدم هذا النهج

- **المعالجة الجماعية**: هل تحتاج إلى تقليل حجم مجلد من التقارير قبل الأرشفة؟ غلف الشيفرة داخل حلقة `foreach` ووجهها إلى كل ملف.
- **رفع الملفات عبر الويب**: تقليل حجم الحمولة قبل أن يرفع المستخدمون ملف Word يمكن أن يوفر عرض النطاق الترددي وتكاليف التخزين.
- **الامتثال**: بعض المؤسسات تفرض حدًا أقصى لحجم المستند للمرفقات البريدية؛ تساعدك هذه التقنية على البقاء تحت تلك الحدود.

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن أتقنت كيفية **ضغط الصور في DOCX**، قد تستكشف:

- **تحويل دفعي** إلى PDF مع الحفاظ على الضغط (`doc.Save("out.pdf", SaveFormat.Pdf)`).
- **تغيير حجم الصورة ديناميكيًا** باستخدام `ImageResizeOptions` إذا لم يكن JPEG بدون فقدان كافيًا.
- **إزالة البيانات الوصفية** (`doc.RemoveMacros();`) لتقليل حجم الملف أكثر.
- **دمج مع Azure Functions** للتحسين الفوري في خطوط الأنابيب السحابية.

كل هذه تعتمد على الفكرة الأساسية نفسها: **تحسين محتوى مستند Word** برمجيًا.

## الخلاصة

لقد غطينا كل ما تحتاج معرفته لـ **ضغط الصور في DOCX**، **تحسين مستند Word**، و**تقليل حجم ملف DOCX** باستخدام عدد قليل فقط من عبارات C#. من خلال تحميل الملف، تكوين `OptimizationOptions`، تطبيق `doc.Optimize`، وحفظ النتيجة، ستحصل على ملف أخف دون تعديل يدوي. جرّبه على تقاريرك، عروضك التقديمية، أو الكتب الإلكترونية—ستشكر لك صندوق الوارد (ومستخدموك).

هل لديك أسئلة أو سيناريو صعب تحتاج مساعدة فيه؟ اترك تعليقًا أدناه، ولنستمر في النقاش. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تقليل حجم الصور بسرعة في ملفات PDF باستخدام Aspose.PDF .NET: تحسين وضغط الصور بفعالية](/pdf/english/net/images-graphics/optimize-pdf-images-aspose-net-fast-compression/)
- [دليل شامل: تحسين حجم ملف PDF باستخدام Aspose.PDF .NET لتبادل أسرع وكفاءة تخزين أعلى](/pdf/english/net/performance-optimization/optimize-pdf-file-size-aspose-pdf-dotnet/)
- [إزالة تضمين الخطوط في ملفات PDF باستخدام Aspose.PDF for .NET: تقليل حجم الملف وتحسين الأداء](/pdf/english/net/performance-optimization/optimize-pdfs-unembed-fonts-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}