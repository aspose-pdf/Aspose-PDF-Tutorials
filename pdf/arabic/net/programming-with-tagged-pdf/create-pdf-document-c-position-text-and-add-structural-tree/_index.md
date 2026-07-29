---
category: general
date: 2026-07-20
description: 'إنشاء مستند PDF باستخدام C# و Aspose.Pdf: وضع النص في PDF وإضافة شجرة
  هيكلية لإمكانية الوصول. اتبع هذا الدليل خطوة بخطوة.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: ar
lastmod: 2026-07-20
og_description: أنشئ مستند PDF باستخدام C# فورًا. تعلّم كيفية وضع النص في PDF وإضافة
  شجرة هيكلية باستخدام Aspose.Pdf للامتثال لمعيار PDF/A‑2b.
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: إنشاء مستند PDF باستخدام C# – دليل كامل لتحديد موضع النص وبنية العلامات
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: إنشاء مستند PDF باستخدام C# – وضع النص وإضافة شجرة هيكلية
url: /ar/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF C# – وضع النص وإضافة شجرة بنية

هل احتجت يوماً إلى **create PDF document C#** الذي لا يضع النص فقط في المكان الذي تريده بالضبط، بل يضم أيضاً شجرة بنية مناسبة لإمكانية الوصول؟ لست وحدك—المطورون الذين يبنون الفواتير، التقارير، أو الكتب الإلكترونية يواجهون هذه الحاجة طوال الوقت. في هذا الدرس سنستعرض مثالاً كاملاً وجاهزاً للتنفيذ يفعل ذلك بالضبط، باستخدام مكتبة Aspose.Pdf القوية.

سنغطي كيفية **position text in PDF**، إرفاق علامة دلالية عبر خطوة **add structural tree**، وأخيراً حفظ الملف كوثيقة متوافقة مع PDF/A‑2b. في النهاية ستحصل على قطعة شفرة قابلة لإعادة الاستخدام يمكنك إدراجها في أي مشروع .NET.

---

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.6+)  
- حزمة NuGet **Aspose.Pdf for .NET** (`Install-Package Aspose.Pdf`)  
- بيئة تطوير C# أساسية (Visual Studio، Rider، أو VS Code)  

لا توجد أدوات طرف ثالث إضافية مطلوبة؛ المكتبة تتعامل مع كل شيء من تخطيط الصفحات إلى توافق PDF/A.

---

## الخطوة 1: تهيئة مستند PDF (Create PDF Document C#)

الأول ما نفعله هو إنشاء كائن `Document` جديد. فكر فيه كقماش نظيف—لا شيء عليه بعد، لكنه جاهز لاستقبال الصفحات، النص، والبيانات الوصفية البنيوية.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **لماذا هذا مهم:** فئة `Document` هي نقطة الدخول لجميع عمليات Aspose.Pdf. إضافة صفحة مبكراً تمنحنا سطحاً لربط المحتوى البصري والشجرة البنيوية لاحقاً.

---

## الخطوة 2: تعريف فقرة وتحديد موقعها (Position Text in PDF)

الآن ننشئ كائن `Paragraph` ونخبر Aspose بالضبط أين يجب أن يظهر على الصفحة. تُقاس إحداثيات PDF بالنقاط (1 inch = 72 pt)، لذا نستخدم `Position(72, 720)` لوضع الفقرة بإنش واحد من الحافة اليسرى و10 إنشات من الأسفل.

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى وضع عدة أسطر، عدّل إحداثية `Y` لكل فقرة لاحقة، أو استخدم `TextBuilder` للتحكم الدقيق.

---

## الخطوة 3: إنشاء عنصر بنيوي (Add Structural Tree)

تعتمد ملفات PDF المراعية لإمكانية الوصول على *شجرة بنية* تصف الترتيب المنطقي للمحتوى. هنا ننشئ `StructureElement` بالعلامة `"P"` (فقرة) ونرفق الفقرة المحددة كطفل له.

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **لماذا نضيف شجرة بنية:** تقرأ القارئات الشاشة وغيرها من تقنيات المساعدة هذه العلامات لتصفح المستند. بدونها قد يكون ملف PDF مثالياً بصرياً لكنه غير قابل للوصول.

---

## الخطوة 4: ربط العنصر البنيوي بالصفحة

كل صفحة تحتفظ بمجموعة خاصة بها من العناصر البنيوية. بإضافة `structElement` إلى `pdfPage.StructElements`، ندمج الهرم المنطقي مع التخطيط البصري.

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **مشكلة شائعة:** نسيان هذه الخطوة يعني أن العلامة موجودة في الذاكرة لكنها غير مرتبطة بأي صفحة، مما يجعل معلومات إمكانية الوصول غير مرئية للقراء.

---

## الخطوة 5: حفظ كـ PDF/A‑2b (ضمان الحفظ طويل الأمد)

PDF/A‑2b هو مجموعة فرعية من PDF مخصصة للأرشفة. يمكن لـ Aspose.Pdf إنتاج هذا التنسيق بنداء واحد. استبدل `"YOUR_DIRECTORY"` بمسار فعلي على جهازك.

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **النتيجة:** لديك الآن ملف PDF حيث النص يقع بالضبط حيث وضعته، ويحتوي المستند على شجرة بنية صحيحة لأدوات إمكانية الوصول.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في تطبيق Console. يتم تجميعه وتشغيله كما هو (بعد إضافة مرجع NuGet لـ Aspose.Pdf).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**الإخراج المتوقع:** بعد التشغيل، افتح `TaggedWithPosition.pdf`. سترى الجملة “Tagged paragraph at a specific location.” موضوعة بالقرب من الزاوية السفلية‑اليمنى للصفحة الأولى. إذا فحصت علامات PDF (مثلاً عبر لوحة “Tags” في Adobe Acrobat)، ستجد عنصر `<P>` مرتبط بهذه الفقرة.

---

![لقطة شاشة للنص الموضّع في PDF تم إنشاؤه باستخدام Aspose.Pdf](/images/pdf-positioned.png){: .align-center }

*نص بديل للصورة:* **create pdf document c#** – لقطة شاشة تُظهر النص الموضّع داخل PDF تم إنشاؤه باستخدام Aspose.Pdf.

---

## أسئلة شائعة وحالات خاصة

### هل يمكنني استخدام وحدات أخرى (mm, cm) لتحديد الموقع؟

تعمل Aspose.Pdf أصلاً بالنقاط. إذا كنت تفضّل المليمترات، حوّل باستخدام `1 mm ≈ 2.83465 pt`. على سبيل المثال، `Position(25.4, 254)` يضع الفقرة بإنش واحد من اليسار و9 سم من الأسفل.

### ماذا لو احتجت لإضافة عدة علامات (عناوين، جداول)؟

ما عليك سوى إنشاء كائنات `StructureElement` إضافية بالعلامات مثل `"H1"` للعناوين أو `"Table"` للجداول، وإضافة المحتوى المقابل كأطفال. التداخل يعمل بنفس الطريقة—الأطفال يرثون ترتيب الوالد المنطقي.

### هل يعمل هذا النهج مع PDF/A‑1b أو PDF/A‑3b؟

نعم. استبدل `SaveFormat.PdfA2b` بـ `SaveFormat.PdfA1b` أو `SaveFormat.PdfA3b`. ضع في اعتبارك أن كل نسخة من PDF/A لها مجموعة من البيانات الوصفية المطلوبة؛ سيُظهر لك Aspose.Pdf رسالة إذا كان هناك شيء مفقود.

---

## ملخص

استعرضنا سيناريو **create pdf document c#** يتضمن:

1. إنشاء مستند PDF جديد باستخدام Aspose.Pdf.  
2. **position text in PDF** عبر تعيين إحداثيات دقيقة.  
3. **add structural tree** لإضافة عناصر بنيوية من أجل إمكانية الوصول.  
4. حفظ النتيجة كملف PDF/A‑2b متوافق مع المعايير.

جميع الخطوات مكتفية ذاتياً، ويمكنك تعديل المقتطف لتصاميم أكثر تعقيداً، صفحات متعددة، أو أنواع علامات مختلفة.

---

## ما التالي؟

- **تنسيق النص** – استكشف `TextState` لتغيير الخطوط، الألوان، والأحجام.  
- **إدراج صور** – استخدم `ImageFragment` وضعها جنب الفقرة.  
- **إنشاء جداول** – أنشئ كائنات `Table` وضع علامة `"Table"` لها للحصول على دلالات أغنى.  
- **خطوط الأتمتة** – دمج هذا الكود في خدمة خلفية تُنشئ الفواتير كل ليلة.

لا تتردد في التجربة، وأخبرنا بأي تنويعات تجدها مفيدة. برمجة سعيدة!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء ملفات PDF ذات علامات مع Aspose.PDF لـ .NET: دليل كامل لتعزيز إمكانية الوصول وبنية المستند](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [إنشاء مستند PDF باستخدام Aspose.PDF – دليل خطوة بخطوة](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [إنشاء وتدوير النص في ملفات PDF باستخدام Aspose.PDF .NET: دليل شامل للمطورين](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}