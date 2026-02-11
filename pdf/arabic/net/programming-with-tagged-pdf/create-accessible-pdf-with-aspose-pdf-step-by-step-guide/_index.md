---
category: general
date: 2026-02-10
description: إنشاء ملف PDF قابل للوصول باستخدام Aspose.Pdf في C#. تعلم كيفية إضافة
  صفحة PDF فارغة، إضافة وسوم الوصول، تحديد موضع النص في PDF، وإنشاء صفحة PDF برمجيًا.
draft: false
keywords:
- create accessible pdf
- add blank page pdf
- add accessibility tags
- position text pdf
- create pdf page programmatically
language: ar
og_description: إنشاء PDF يمكن الوصول إليه باستخدام C#. يشرح هذا الدليل كيفية إضافة
  صفحة PDF فارغة، وضع العلامات على المحتوى، تحديد موضع النص في PDF، وإنشاء صفحة PDF
  برمجيًا.
og_title: إنشاء ملف PDF قابل للوصول باستخدام Aspose.Pdf – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF Accessibility
title: إنشاء PDF قابل للوصول باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/programming-with-tagged-pdf/create-accessible-pdf-with-aspose-pdf-step-by-step-guide/
---

All preserved.

Make sure to keep markdown formatting, code block placeholders unchanged.

Now produce final answer with only translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للوصول باستخدام Aspose.Pdf – دليل خطوة‑بخطوة

هل احتجت يومًا إلى **إنشاء PDF قابل للوصول** لكن لم تكن متأكدًا من أين تبدأ؟ في العديد من المشاريع—فكر في تقارير الامتثال أو وحدات التعلم الإلكتروني—الوصولية ليست اختيارية، بل إلزامية. لحسن الحظ، توفر لك Aspose.Pdf واجهة برمجة تطبيقات نظيفة لإضافة صفحة PDF فارغة، وإضافة علامات الوصول، وتحديد موضع النص بدقة، كل ذلك دون مغادرة قاعدة شفرة C# الخاصة بك.

في هذا الدرس ستتعرف بالضبط على كيفية **إنشاء PDF قابل للوصول** برمجيًا، إضافة صفحة PDF فارغة، وضع علامة على المحتوى لقارئات الشاشة، والتحكم في المستطيل البصري حيث يظهر النص. في النهاية، ستحصل على ملف يعمل يمكنك فتحه في أي قارئ PDF والتحقق من وجود العلامات.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core أيضًا)  
- حزمة NuGet لـ Aspose.Pdf for .NET (`Aspose.Pdf`) – الإصدار 23.12 أو أحدث  
- مشروع بسيط من نوع console أو class‑library في Visual Studio أو Rider أو بيئتك المفضلة IDE  

هذا كل شيء. لا أطر إضافية، ولا ملفات إعدادات غامضة—فقط C# عادي و Aspose.Pdf.

## نظرة عامة على إنشاء PDF قابل للوصول

التدفق العام بسيط:

1. **Initialize** كائن `Document` جديد (حاوية PDF).  
2. **Add a blank page PDF** حتى تحصل على مساحة للعمل عليها.  
3. **Create a paragraph** مع النص الذي تريد أن يكون قابلًا للوصول.  
4. **Define a rectangle** الذي يخبر PDF أين يجب أن يظهر هذا الفقرة—هذه هي خطوة “position text PDF”.  
5. **Wrap the paragraph in an accessibility tag** وإرفاقه بشجرة المحتوى الموسومة للصفحة.  
6. **Save** الملف، مع الحفاظ على العلامات لتقنيات المساعدة.  

فيما يلي سنفصل كل خطوة، نشرح *لماذا* هي مهمة، ونظهر الكود الدقيق الذي يمكنك نسخه‑ولصقه.

## الخطوة 1: تهيئة المستند (إنشاء صفحة PDF برمجيًا)

أولًا وقبل كل شيء—تحتاج إلى نسخة `Document`. فكر فيها ككتاب فارغ ستملأه لاحقًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tags;

// Step 1: Create a new PDF document (this is the programmatic page creation)
using var pdfDocument = new Document();
```

> **لماذا؟**  
> `Document` هو الكائن الجذري الذي يحتوي على الصفحات والموارد وشجرة المحتوى الموسومة. بدون هذا لا يمكنك إضافة صفحة PDF فارغة أو أي علامات.

## الخطوة 2: إضافة صفحة PDF فارغة

PDF بدون صفحات يكون غير مرئي أساسًا. إضافة صفحة فارغة تمنحك سطحًا لتحديد موضع المحتوى.

```csharp
// Step 2: Add a blank page PDF to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **نصيحة احترافية:**  
> إذا كنت بحاجة إلى صفحات متعددة، فقط استدعِ `pdfDocument.Pages.Add()` بشكل متكرر. كل استدعاء يُعيد كائن `Page` جديد يمكنك تعديل كلٍ منه بشكل منفرد.

## الخطوة 3: بناء فقرة قابلة للوصول (إضافة علامات الوصول)

الآن نقوم بإنشاء النص الفعلي الذي سيقرأه قارئ الشاشة. من خلال تغليفه في كائن `Paragraph`، نحن نجهزه للوسم.

```csharp
// Step 3: Build a paragraph that contains accessible text
var accessibleParagraph = new Paragraph
{
    // The text that will be announced by assistive tech
    Text = "Accessible paragraph"
};
```

> **لماذا الوسم؟**  
> إضافة علامات الوصول (`Add accessibility tags`) تخبر الأدوات مثل NVDA أو VoiceOver أين يبدأ ترتيب القراءة المنطقي، مما يجعل PDF قابلًا للاستخدام حقًا للجميع.

## الخطوة 4: تحديد موضع النص في PDF باستخدام مستطيل بصري

إحداثيات PDF تُعبّر عنها كمستطيل: السفل‑يسار‑x (LLX)، السفل‑يسار‑y (LLY)، العلوي‑يمين‑x (URX)، العلوي‑يمين‑y (URY). هذه هي خطوة “position text PDF”.

```csharp
// Step 4: Define where the paragraph will appear on the page
var visualRect = new Rectangle(50, 700, 550, 720);
```

> **ماذا يعني هذا؟**  
> يبدأ المستطيل 50 نقطة من الحافة اليسرى و700 نقطة من الأسفل، ويمتد إلى 550 نقطة أفقياً و720 نقطة عمودياً. عدّل هذه القيم لتناسب تخطيطك.

## الخطوة 5: وضع علامة على الفقرة وإلحاقها بشجرة المحتوى الموسومة

هنا جوهر **add accessibility tags**: نقوم بإنشاء عنصر فقرة يعرف كلًا من محتواه المنطقي وموقعه البصري، ثم نرفقه بعنصر الجذر للعلامة في الصفحة.

```csharp
// Step 5: Create a tagged paragraph element with position info
var taggedParagraph = pdfPage.TaggedContent.CreateParagraphElement(accessibleParagraph, visualRect);

// Append the tagged element to the page's root element
pdfPage.TaggedContent.RootElement.AppendChild(taggedParagraph);
```

> **لماذا هذا مهم:**  
> API `TaggedContent` يبني شجرة هيكلية يستخدمها قارئو PDF للتنقل. من خلال إلحاق العنصر بـ `RootElement`، تضمن ظهور الفقرة بترتيب القراءة الصحيح.

## الخطوة 6: حفظ المستند (الحفاظ على جميع العلامات)

أخيرًا، نقوم بحفظ الملف. طريقة `Save` تكتب كلًا من الصفحة البصرية ومعلومات الوصول المخفية.

```csharp
// Step 6: Save the PDF with all tags intact
pdfDocument.Save("YOUR_DIRECTORY/tagged_with_position.pdf");
```

> **نصيحة للتحقق:**  
> افتح الملف الناتج في Adobe Acrobat Reader، انتقل إلى *View → Show/Hide → Navigation Panes → Tags*. يجب أن ترى عقدة `P` (Paragraph) تحت الصفحة—هذا يؤكد وجود العلامات.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ‑واللصق. يتضمن كل الاستيرادات، كل التعليقات، وكل الخطوات المذكورة أعلاه.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tags;

namespace AccessiblePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the PDF document
            using var pdfDocument = new Document();

            // 2️⃣ Add a blank page PDF
            var pdfPage = pdfDocument.Pages.Add();

            // 3️⃣ Create an accessible paragraph
            var accessibleParagraph = new Paragraph
            {
                Text = "Accessible paragraph"
            };

            // 4️⃣ Define the visual rectangle (LLX, LLY, URX, URY)
            var visualRect = new Rectangle(50, 700, 550, 720);

            // 5️⃣ Tag the paragraph with its position
            var taggedParagraph = pdfPage.TaggedContent.CreateParagraphElement(
                accessibleParagraph, visualRect);
            pdfPage.TaggedContent.RootElement.AppendChild(taggedParagraph);

            // 6️⃣ Save the PDF (ensure the output folder exists)
            pdfDocument.Save("tagged_with_position.pdf");

            // Optional: let the user know we're done
            System.Console.WriteLine("Accessible PDF created successfully!");
        }
    }
}
```

**النتيجة المتوقعة:**  
- ملف PDF من صفحة واحدة اسمه `tagged_with_position.pdf`.  
- النص “Accessible paragraph” يظهر قرب أعلى الصفحة.  
- المستند يحتوي على شجرة علامات منطقية، مما يجعله قابلًا للقراءة بواسطة برامج قراءة الشاشة.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى فقرات متعددة على نفس الصفحة؟

أنشئ كائنات `Paragraph` إضافية، عرّف مثيلات `Rectangle` منفصلة لكل منها، واستدعِ `CreateParagraphElement` لكل واحدة. ألحقها بالترتيب الذي تريد تسلسل القراءة فيه.

### هل يمكنني ضبط أنماط الخط مع الحفاظ على العلامات؟

بالطبع. بعد إنشاء `Paragraph`، يمكنك تعيين `TextState`:

```csharp
accessibleParagraph.TextState.Font = FontRepository.FindFont("Arial");
accessibleParagraph.TextState.FontSize = 12;
accessibleParagraph.TextState.FontStyle = FontStyles.Bold;
```

العلامة تظل سليمة لأن التنسيق هو خاصية بصرية، وليس هيكلية.

### هل يعمل هذا مع توافق PDF/A‑2b (الأرشفة)؟

نعم. تسمح لك Aspose.Pdf بتحديد مستوى توافق PDF/A قبل الحفظ:

```csharp
pdfDocument.Convert(new PdfFormatConversionOptions { ConvertToPdfA = PdfAStandard.PdfA2b });
```

علامات الوصول تُحفظ في نسخة PDF/A.

### كيف يمكنني التحقق من العلامات برمجيًا؟

يمكنك تعداد شجرة العلامات:

```csharp
var root = pdfPage.TaggedContent.RootElement;
foreach (var child in root.ChildElements)
{
    System.Console.WriteLine($"Tag: {child.ElementType}");
}
```

إذا رأيت إدخالات `Paragraph`، فأنت جاهز.

## الخلاصة

لقد استعرضنا العملية الكاملة لإنشاء ملفات **create accessible PDF** باستخدام Aspose.Pdf، مع تغطية كيفية **add blank page PDF**، **add accessibility tags**، **position text PDF**، و**create PDF page programmatically**. الكود جاهز للتنفيذ، والمفاهيم مشروحة، والآن لديك أساس قوي لبناء ملفات PDF متوافقة في أي مشروع .NET.

ما التالي؟ جرّب إضافة صور باستخدام `ImageFragment`، بناء جداول، أو حتى إنشاء تقرير متعدد الصفحات قابل للوصول. كل عنصر جديد يمكن تغليفه بالعلامات بنفس الطريقة التي فعلناها للفقرة، لضمان شمولية مستنداتك.

هل لديك سيناريو غير مغطى هنا؟ اترك تعليقًا، ولنحل المشكلة معًا. ترميز سعيد، واحرص على أن تكون ملفات PDF قابلة للوصول!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}