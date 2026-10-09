---
category: general
date: 2026-06-08
description: قص الصورة في ملف PDF باستخدام Aspose.PDF في C#. تعلّم كيفية إنشاء ملف
  PDF يحتوي على صورة، حفظ ملف PDF مع صورة، وإضافة صورة إلى ملف PDF في بضع أسطر فقط.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: ar
og_description: قص الصورة في ملف PDF باستخدام Aspose.PDF في C#. يوضح هذا البرنامج
  التعليمي كيفية إنشاء ملف PDF يحتوي على صورة، حفظ ملف PDF مع الصورة، وإضافة صورة
  إلى ملف PDF بسرعة.
og_title: قص الصورة في PDF باستخدام Aspose.PDF – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: قص الصورة في ملف PDF باستخدام Aspose.PDF – دليل شامل
url: /ar/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# قص الصورة في PDF باستخدام Aspose.PDF – دليل كامل

هل تساءلت يومًا كيف **تقص صورة في PDF** دون الحاجة إلى محرر رسومات؟ لست وحدك. في العديد من التقارير، الفواتير، أو الكتب الإلكترونية تحتاج فقط إلى جزء من صورة—ربما زاوية الشعار أو جزء من مخطط—وتريدها مباشرة داخل PDF.  

هذا الدليل يوضح لك ذلك بالضبط: سنقوم **بإنشاء PDF مع صورة**، **إضافة صورة إلى PDF**، ثم **قص صورة في PDF** باستخدام مكتبة Aspose.PDF للغة C#. في النهاية ستعرف أيضًا كيف **تحفظ PDF مع صورة** لتتمكن من إرسال الملف لأي شخص.

---

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)  
- نسخة مرخصة أو تجريبية من **Aspose.PDF for .NET** (التثبيت عبر NuGet `Install-Package Aspose.PDF`)  
- ملف صورة (JPEG/PNG) على القرص – سنسميه `image.jpg`  
- أي بيئة تطوير تفضلها (Visual Studio, Rider, VS Code)

هذا كل شيء. لا خدمات إضافية، لا أدوات خارجية.

---

## الخطوة 1: إعداد المشروع والاستيرادات

أولاً، أنشئ تطبيق console وأدرج المساحات الاسمية التي سنستخدمها. جمل `using` تحافظ على نظافة الكود وتسهّل قراءة الخطوات اللاحقة.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Pro tip:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن “Aspose.PDF” وقم بالتثبيت. المكتبة تتعامل داخليًا مع كل من وضع الصورة والقص، لذا لن تحتاج إلى أي مكتبات صور من طرف ثالث.

---

## الخطوة 2: إنشاء PDF مع صورة

الآن نقوم فعليًا **بإنشاء pdf مع صورة**. المقتطف أدناه يبني كائن `Document` جديد، يضيف صفحة فارغة، ويجهز تدفق الصورة.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

تشغيل هذا الكود سيعطيك PDF يحتوي على الصورة كاملة ممتدة إلى الأبعاد التي حددتها. هذا فحص مبدئي جيد قبل أن تبدأ بالقص.

---

## الخطوة 3: كيفية إضافة صورة إلى PDF (والتحضير للقص)

إذا كنت تعرف بالفعل المنطقة الدقيقة التي تريدها، يمكنك تخطي خطوة الصورة بحجمها الكامل والانتقال مباشرة إلى جزء **كيفية إضافة صورة إلى pdf**. طريقة `AddImage` تقبل ثلاثة معلمات:

1. **Image stream** – البايتات الخام لصورتك.  
2. **Placement rectangle** – الموقع على الصفحة حيث تُوضع الصورة.  
3. **Crop rectangle** – الجزء من الصورة الذي تريد عرضه فعليًا.

فيما يلي النسخة المختصرة التي تقوم بالوضع **والقص** في استدعاء واحد.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Why this works:** Aspose.PDF داخليًا يطابق مستطيل القص مع أبعاد بكسل الصورة، ثم يرسم فقط تلك القطعة داخل مساحة `placement`. لا حاجة لمعالجة bitmap إضافية، مما يعني بقاء حجم PDF صغيرًا.

---

## الخطوة 4: كيفية قص صورة PDF – خيارات متقدمة

أحيانًا لا يكون القص الربع كافيًا. ربما تحتاج إلى مستطيل مخصص أو ترغب في الحفاظ على نسبة أبعاد الصورة. إليك نهج أكثر مرونة:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**معالجة الحالات الخاصة:**  
- **Null streams** – احرص دائمًا على تغليف `FileStream` داخل كتلة `using`، كما هو موضح، لتجنب التسريبات.  
- **Large images** – إذا كانت الصورة الأصلية ضخمة، فكر في تقليل حجم مستطيل `placement`؛ Aspose سيقلصها تلقائيًا.  
- **Transparent PNGs** – المكتبة تحترم قنوات alpha، لذا سيحتفظ الجزء المقصوص بالشفافية.

---

## الخطوة 5: حفظ PDF مع صورة (وتحقق)

أخيرًا، نحن **نحفظ pdf مع صورة**. طريقة `Save` تكتب المستند إلى القرص. يمكنك أيضًا بثه مرة أخرى إلى عميل ويب إذا كنت تبني API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

عند فتح `output.pdf`، يجب أن ترى فقط الجزء المقصوص من `image.jpg` موضعًا بالضبط حيث حددته. إذا بدت الصورة مشوهة، عدل عرض/ارتفاع مستطيل `placement` ليتطابق مع نسبة أبعاد مستطيل القص.

---

## أسئلة شائعة ومشكلات

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني قص عدة صور على نفس الصفحة؟** | بالتأكيد. استدعِ `page.AddImage` لكل صورة مع مستطيل وضع وقطع خاص بها. |
| **ماذا لو كانت صوري بصيغة مختلفة (مثال: BMP)؟** | Aspose.PDF يدعم JPEG, PNG, BMP, GIF, و TIFF مباشرة. فقط غير امتداد الملف. |
| **هل أحتاج إلى رخصة للاستخدام في الإنتاج؟** | النسخة التجريبية تعمل حتى 5 صفحات. للنشر الحقيقي، اشترِ رخصة لإزالة العلامة المائية. |
| **كيف يمكنني تدوير الصورة المقصوصة؟** | بعد إضافة الصورة، احصل على كائن `Image` واضبط خاصية `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **هل هناك طريقة للقص باستخدام النسب المئوية بدلاً من النقاط المطلقة؟** | نعم—احسب أبعاد المستطيل بناءً على `image.Width * 0.25` وما إلى ذلك، ثم حوّلها إلى نقاط كما هو موضح في الخطوة 4. |

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

شغّل البرنامج، افتح `output.pdf`، وسترى فقط الربع العلوي‑الأيسر من `image.jpg` معروضًا في الزاوية العلوية‑اليسرى من الصفحة. غيّر قيم مستطيل `crop` لتجربة قطع مختلفة.

---

## الخلاصة

لقد استعرضنا العملية الكاملة لـ **قص صورة في pdf** باستخدام Aspose.PDF للغة C#. بدءًا من مستند جديد، قمنا **بإنشاء pdf مع صورة**، عرضنا **كيفية إضافة صورة إلى pdf**، طبقنا مستطيل **كيفية قص صورة pdf** مخصص، وأخيرًا **حفظ pdf مع صورة**.  

الآن يمكنك تضمين صور مقصوصة بدقة في أي PDF تُنشئه—مثالي للفواتير، الكتيبات التسويقية، أو التقارير الآلية. في الخطوة التالية، فكر في إضافة تسميات نصية (`TextFragment`) أو رسم أشكال حول الصورة المقصوصة لتسليط الضوء عليها أكثر.  

هل لديك سيناريوهات أخرى ترغب في استكشافها؟ اترك تعليقًا، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية ضبط حجم الصورة في PDF باستخدام Aspose.PDF لـ .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [كيفية إضافة ختم صورة إلى PDF باستخدام Aspose.PDF لـ .NET&#58; دليل شامل](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [كيفية استخراج معلومات الصورة من ملفات PDF باستخدام Aspose.PDF لـ .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}