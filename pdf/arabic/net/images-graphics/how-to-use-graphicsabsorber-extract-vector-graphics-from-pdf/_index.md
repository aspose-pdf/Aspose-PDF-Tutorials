---
category: general
date: 2026-06-27
description: كيفية استخدام GraphicsAbsorber لاستخراج الرسومات المتجهة من ملفات PDF.
  تعلم خطوة بخطوة استخراج الرسومات باستخدام Aspose.Pdf للحصول على مخرجات SVG نظيفة.
draft: false
keywords:
- how to use graphicsabsorber
- extract vector graphics pdf
- how to extract pdf vectors
- aspose pdf graphics extraction
language: ar
og_description: كيفية استخدام GraphicsAbsorber لاستخراج ملفات PDF التي تحتوي على رسومات
  متجهية. يشرح هذا الدرس استخراج الرسومات باستخدام Aspose.Pdf مع الكود الكامل.
og_title: كيفية استخدام GraphicsAbsorber – دليل Aspose.Pdf الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to use GraphicsAbsorber to extract vector graphics PDF files. Learn
    step‑by‑step Aspose.Pdf graphics extraction for clean SVG output.
  headline: How to Use GraphicsAbsorber – Extract Vector Graphics from PDF with Aspose.Pdf
  type: TechArticle
- description: How to use GraphicsAbsorber to extract vector graphics PDF files. Learn
    step‑by‑step Aspose.Pdf graphics extraction for clean SVG output.
  name: How to Use GraphicsAbsorber – Extract Vector Graphics from PDF with Aspose.Pdf
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works with .NET Core, .NET Framework, and
      .NET 5+). - A valid Aspose.Pdf for .NET license (or a free evaluation key).
      - Basic C# knowledge—no advanced graphics expertise required. - The PDF you
      want to analyze (we’ll use `vector.pdf` as an example).'
  - name: – Load the PDF Document
    text: Before you can extract anything, you need an in‑memory representation of
      the file. Using `using var` ensures the document is disposed automatically,
      which is especially handy in long‑running services.
  - name: – Create a GraphicsAbsorber to Capture Vector Objects
    text: '`GraphicsAbsorber` is a specialized collector that walks through the PDF
      content stream and gathers every drawing operator (lines, curves, shapes, etc.).
      Think of it as a net you throw over the page to catch all vector pieces.'
  - name: – Apply the Absorber to the Desired Page
    text: You can run the absorber on a single page or loop through the whole document.
      Here we focus on the first page for simplicity.
  - name: – Iterate Through Extracted Elements and Display Their Details
    text: Now the fun part—reading the data. Each element tells you which page it
      came from, the number of operators (i.e., drawing commands), and its position
      within the page.
  - name: 'Advanced: Extracting Vectors from All Pages'
    text: 'If you need to **extract vector graphics PDF** files across an entire document,
      just wrap the `Visit` call in a loop:'
  - name: Exporting Extracted Vectors to SVG (Optional)
    text: Aspose.Pdf can render the captured vectors directly to SVG, which is handy
      when you want a web‑ready format.
  - name: Next Steps
    text: '- Dive deeper into **aspose pdf graphics extraction** by exploring `GraphicsAbsorber`’s
      `Operators` collection for fine‑grained path data. - Combine the extracted coordinates
      with a custom SVG builder if you need more control than the built‑in `SvgSaveOptions`.
      - Experiment with rasterizing specific'
  type: HowTo
- questions:
  - answer: '`GraphicsAbsorber.Elements` will be empty; the loop simply skips output.
      No error is thrown.'
    question: What if a page has no vectors?
  - answer: Yes. Set `graphicsAbsorber.OperatorsFilter` to an array of `OperatorType`
      values (e.g., `OperatorType.Path`, `OperatorType.Stroke`). This reduces noise
      when you only care about paths.
    question: Can I filter only certain operator types?
  - answer: Using `using var` ensures each `Document` and `GraphicsAbsorber` is disposed
      promptly. For massive files, process pages one at a time as shown to keep the
      footprint low.
    question: Is the extractor memory‑intensive for large PDFs?
  - answer: 'Load the document with a password: `new Document("file.pdf", new LoadOptions
      { Password = "secret" })`.'
    question: Does this work with encrypted PDFs?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- VectorGraphics
title: كيفية استخدام GraphicsAbsorber – استخراج الرسومات المتجهة من PDF باستخدام Aspose.Pdf
url: /ar/net/images-graphics/how-to-use-graphicsabsorber-extract-vector-graphics-from-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام GraphicsAbsorber – استخراج الرسومات المتجهة من PDF باستخدام Aspose.Pdf

هل تساءلت يومًا **كيف تستخدم GraphicsAbsorber** عندما تحتاج إلى استخراج الأشكال المتجهة من ملف PDF؟ لست وحدك. سواء كنت تبني خط أنابيب من التصميم إلى الكود أو تحتاج فقط إلى ملفات SVG نظيفة لمشروع ويب، قد يشعر استخراج الرسومات المتجهة من ملفات PDF كالبحث عن إبرة في كومة قش.  

في هذا الدليل سنعرض لك حلاً مختصرًا وجاهزًا للتنفيذ يستخدم `GraphicsAbsorber` من Aspose.Pdf. في النهاية ستعرف بالضبط **كيفية استخراج المتجهات من PDF**، وسترى إحداثياتها، وستمتلك أساسًا قويًا للمعالجة الإضافية.

## ما ستتعلمه

- تحميل مستند PDF باستخدام Aspose.Pdf.
- إنشاء وتكوين `GraphicsAbsorber`.
- تطبيق الـ absorber على صفحة معينة.
- التكرار عبر العناصر المستخرجة وقراءة تفاصيلها.
- نصائح للتعامل مع ملفات PDF متعددة الصفحات وتصديرها إلى SVG.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core، .NET Framework، و .NET 5+).
- ترخيص صالح لـ Aspose.Pdf for .NET (أو مفتاح تقييم مجاني).
- معرفة أساسية بـ C# — لا تحتاج إلى خبرة متقدمة في الرسومات.
- ملف PDF الذي تريد تحليله (سنستخدم `vector.pdf` كمثال).

> **Pro tip:** إذا لم يكن لديك ترخيص بعد، احصل على مفتاح مؤقت من موقع Aspose؛ تعمل الواجهة البرمجية (API) بنفس الطريقة أثناء التقييم.

<img src="graphicsabsorber-diagram.png" alt="مخطط كيفية استخدام GraphicsAbsorber" style="max-width:100%;">

## كيفية استخدام GraphicsAbsorber – دليل خطوة بخطوة

فيما يلي نقسم العملية إلى أربع خطوات منطقية. كل خطوة تحتوي على مقتطف شفرة قصير، شرح **لماذا** هي مهمة، ونصيحة سريعة لتجنب الأخطاء الشائعة.

### الخطوة 1 – تحميل مستند PDF

قبل أن تتمكن من استخراج أي شيء، تحتاج إلى تمثيل للملف في الذاكرة. استخدام `using var` يضمن التخلص التلقائي من المستند، وهو مفيد بشكل خاص في الخدمات طويلة التشغيل.

```csharp
using Aspose.Pdf;
using System;

// Step 1: Load the PDF document
using var document = new Document("YOUR_DIRECTORY/vector.pdf");

// Verify the document loaded correctly
Console.WriteLine($"Document loaded: {document.Pages.Count} page(s) found.");
```

**لماذا هذه الخطوة؟**  
`Document` هو نقطة الدخول لجميع عمليات Aspose.Pdf. تحميله مرة واحدة وإعادة استخدام المثيل يحافظ على استهلاك الذاكرة منخفضًا ويتجنب عمليات الإدخال/الإخراج المتكررة.

### الخطوة 2 – إنشاء GraphicsAbsorber لالتقاط الكائنات المتجهة

`GraphicsAbsorber` هو جامع متخصص يتجول عبر تدفق محتوى PDF ويجمع كل مشغل رسم (خطوط، منحنيات، أشكال، إلخ). فكر فيه كشبكة تلقيها على الصفحة لالتقاط جميع القطع المتجهة.

```csharp
using Aspose.Pdf.Vector;

// Step 2: Initialize the GraphicsAbsorber
using var graphicsAbsorber = new GraphicsAbsorber();

// Optional: filter by specific operator types (e.g., only paths)
// graphicsAbsorber.OperatorsFilter = new[] { OperatorType.Path };
```

**لماذا هذه الخطوة؟**  
بدون الـ absorber، سيتعين عليك تحليل محتوى PDF الخام بنفسك — مهمة شاقة. الـ absorber يُجرد هذه التعقيدات ويعطيك مجموعة نظيفة من العناصر المتجهة.

### الخطوة 3 – تطبيق الـ Absorber على الصفحة المطلوبة

يمكنك تشغيل الـ absorber على صفحة واحدة أو التكرار عبر المستند بأكمله. هنا نركز على الصفحة الأولى للبساطة.

```csharp
// Step 3: Apply the absorber to page 1
graphicsAbsorber.Visit(document.Pages[1]);

Console.WriteLine($"Absorber visited page {document.Pages[1].Number}.");
```

**لماذا هذه الخطوة؟**  
`Visit` يتجول في تدفق محتوى الصفحة المقدمة ويملأ `graphicsAbsorber.Elements`. إذا تخطيت هذه الخطوة، ستبقى المجموعة فارغة ولن تستخرج أي متجهات.

### الخطوة 4 – التكرار عبر العناصر المستخرجة وعرض تفاصيلها

الآن الجزء الممتع — قراءة البيانات. كل عنصر يخبرك بالصفحة التي جاء منها، عدد المشغلات (أي أوامر الرسم)، وموقعه داخل الصفحة.

```csharp
// Step 4: Enumerate extracted graphics elements
foreach (var element in graphicsAbsorber.Elements)
{
    Console.WriteLine(
        $"Page {element.SourcePage.Number}: {element.Operators.Count} operators at ({element.Position.X:F2}, {element.Position.Y:F2})");
}
```

**لماذا هذه الخطوة؟**  
رؤية عدد المشغلات والإحداثيات تساعدك على تحديد ما إذا كان العنصر خطًا، أو شكلًا، أو مسارًا معقدًا. يمكنك أيضًا تمرير هذه البيانات إلى أدوات لاحقة (مثل مولدات SVG).

### متقدم: استخراج المتجهات من جميع الصفحات

إذا كنت بحاجة إلى **استخراج رسومات متجهة من PDF** عبر مستند كامل، فقط ضع استدعاء `Visit` داخل حلقة:

```csharp
foreach (var page in document.Pages)
{
    graphicsAbsorber.Visit(page);
    foreach (var element in graphicsAbsorber.Elements)
    {
        Console.WriteLine(
            $"[Page {page.Number}] {element.Operators.Count} ops at ({element.Position.X:F2},{element.Position.Y:F2})");
    }
    // Clear elements before moving to the next page
    graphicsAbsorber.Elements.Clear();
}
```

**لماذا مسح المجموعة؟**  
`GraphicsAbsorber.Elements` يحتفظ بالبيانات من الصفحات السابقة. مسحه يمنع التكرار في التقارير ويحافظ على استهلاك الذاكرة بصورة متوقعة.

### تصدير المتجهات المستخرجة إلى SVG (اختياري)

يمكن لـ Aspose.Pdf تحويل المتجهات الملتقطة مباشرة إلى SVG، وهو مفيد عندما تريد تنسيقًا جاهزًا للويب.

```csharp
using Aspose.Pdf.Saving;

// After visiting a page...
var svgSaveOptions = new SvgSaveOptions
{
    PageIndex = 0, // zero‑based index of the page we just visited
    PageCount = 1
};

document.Save("output_page1.svg", svgSaveOptions);
Console.WriteLine("Page saved as SVG.");
```

**لماذا التصدير؟**  
SVG يحافظ على قابلية توسعة المتجهات، مما يجعل الناتج مثاليًا للتصاميم المتجاوبة أو للتحرير الإضافي في أدوات مثل Inkscape.

## مثال كامل يعمل

انسخ الشفرة أدناه إلى مشروع وحدة تحكم جديد (`dotnet new console`) وشغّله. يوضح **كيفية استخدام GraphicsAbsorber**، **استخراج رسومات متجهة من PDF**، ويطبع تشخيصات مفيدة.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Vector;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF
        using var document = new Document("YOUR_DIRECTORY/vector.pdf");
        Console.WriteLine($"Loaded PDF with {document.Pages.Count} page(s).");

        // 2️⃣ Create the absorber
        using var absorber = new GraphicsAbsorber();

        // 3️⃣ Visit each page (you can target a single page if you prefer)
        foreach (var page in document.Pages)
        {
            absorber.Visit(page);

            // 4️⃣ Output element details
            foreach (var element in absorber.Elements)
            {
                Console.WriteLine(
                    $"Page {element.SourcePage.Number}: {element.Operators.Count} operators at ({element.Position.X:F2},{element.Position.Y:F2})");
            }

            // Optional: export the page to SVG
            var svgOptions = new SvgSaveOptions
            {
                PageIndex = page.Number - 1,
                PageCount = 1
            };
            document.Save($"page_{page.Number}.svg", svgOptions);
            Console.WriteLine($"Exported page {page.Number} to SVG.");

            // Reset for next iteration
            absorber.Elements.Clear();
        }

        Console.WriteLine("Extraction complete.");
    }
}
```

**الناتج المتوقع (مثال):**

```
Loaded PDF with 3 page(s).
Page 1: 42 operators at (72.00,540.00)
Exported page 1 to SVG.
Page 2: 15 operators at (72.00,720.00)
Exported page 2 to SVG.
Page 3: 0 operators at (0.00,0.00)
Exported page 3 to SVG.
Extraction complete.
```

الأرقام ستختلف بناءً على المحتوى الفعلي لـ `vector.pdf`، لكن يجب أن ترى سطرًا لكل عنصر متجه وملف SVG مرفق لكل صفحة.

## أسئلة شائعة وحالات خاصة

- **ماذا لو كانت الصفحة لا تحتوي على متجهات؟**  
  `GraphicsAbsorber.Elements` ستكون فارغة؛ الحلقة تتخطى الإخراج ببساطة. لا يتم إلقاء أي خطأ.

- **هل يمكنني تصفية أنواع مشغلات معينة فقط؟**  
  نعم. اضبط `graphicsAbsorber.OperatorsFilter` إلى مصفوفة من قيم `OperatorType` (مثل `OperatorType.Path`، `OperatorType.Stroke`). هذا يقلل الضوضاء عندما تهتم بالمسارات فقط.

- **هل المستخرج يستهلك الكثير من الذاكرة لملفات PDF الكبيرة؟**  
  استخدام `using var` يضمن التخلص السريع من كل من `Document` و `GraphicsAbsorber`. للملفات الضخمة، عالج الصفحات واحدةً تلو الأخرى كما هو موضح للحفاظ على استهلاك منخفض للذاكرة.

- **هل يعمل هذا مع ملفات PDF المشفرة؟**  
  حمّل المستند باستخدام كلمة مرور: `new Document("file.pdf", new LoadOptions { Password = "secret" })`.

## ملخص

لقد استعرضنا **كيفية استخدام GraphicsAbsorber** لـ **استخراج رسومات متجهة من PDF**، فحصنا هدف كل خطوة، وقدمنا مثالًا كاملًا وقابلًا للتنفيذ. لديك الآن أساس قوي لـ **كيفية استخراج المتجهات من PDF** باستخدام Aspose.Pdf ويمكنك توسيع المنطق لتصدير SVGs، تصفية المشغلات، أو دمجه مع خطوط أنابيب الرسومات اللاحقة.

### الخطوات التالية

- تعمق أكثر في **استخراج رسومات Aspose PDF** من خلال استكشاف مجموعة `Operators` في `GraphicsAbsorber` للحصول على بيانات مسار دقيقة.
- دمج الإحداثيات المستخرجة مع مُنشئ SVG مخصص إذا كنت تحتاج إلى تحكم أكبر من `SvgSaveOptions` المدمج.
- جرّب تحويل المتجهات المحددة فقط إلى نقطية باستخدام `Rasterizer` بالتزامن مع الـ absorber.

هل لديك PDF معقد أو حالة استخدام خاصة؟ اترك تعليقًا أدناه، ولنحل المشكلة معًا. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إزالة الرسومات من ملفات PDF باستخدام Aspose.PDF .NET&#58; دليل كامل](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [كيفية استخراج العلامات المائية من ملفات PDF باستخدام Aspose.PDF .NET&#58; دليل خطوة بخطوة](/pdf/english/net/watermarks-backgrounds/extract-pdf-watermarks-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}