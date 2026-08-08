---
category: general
date: 2026-06-08
description: إنشاء صورة PDF في C# عن طريق تحويل HEIC إلى PDF. تعلم كيفية إضافة صورة
  إلى PDF وإنشاء PDF من صورة باستخدام كود خطوة بخطوة.
draft: false
keywords:
- create pdf image
- convert heic to pdf
- add image to pdf
- generate pdf from image
- how to read heic
language: ar
og_description: إنشاء صورة PDF في C# عن طريق تحويل HEIC إلى PDF. اتبع هذا الدليل لإضافة
  صورة إلى PDF وإنشاء PDF من الصورة بسرعة.
og_title: إنشاء صورة PDF من HEIC – دليل C# كامل
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  headline: Create PDF Image from HEIC – Complete C# Guide
  type: TechArticle
- description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  name: Create PDF Image from HEIC – Complete C# Guide
  steps:
  - name: What if the HEIC file is corrupted?
    text: The `HeicImage.Load` method throws a `HeicException`. Wrap the call in a
      try/catch (as shown) and log the error. In production you might fall back to
      a default placeholder image.
  - name: Can I batch‑process multiple HEIC files?
    text: Absolutely. Just move the core logic into a method like `ConvertHeicToPdf(string
      input, string output)` and iterate over a directory with `Directory.GetFiles("*.heic")`.
  - name: Does this approach preserve EXIF metadata?
    text: No, Aspose.Pdf does not automatically copy EXIF data into the PDF. If you
      need metadata, extract it with `HeicImage.Metadata` and add it to the PDF using
      `Document.Info` properties.
  - name: What about memory usage for huge images?
    text: For images larger than 10 MP, consider down‑sampling before creating `BitmapInfo`.
      You can use `HeicImage.Resize` (if supported) or a third‑party bitmap library
      to reduce dimensions.
  type: HowTo
tags:
- C#
- Aspose.Pdf
- HEIC
- ImageConversion
title: إنشاء صورة PDF من HEIC – دليل C# الكامل
url: /ar/net/document-creation/create-pdf-image-from-heic-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء صورة PDF من HEIC – دليل C# كامل

هل تساءلت يومًا كيف يمكنك **إنشاء صورة PDF** من ملف HEIC دون أن تشد شعرك؟ لست وحدك. في العديد من التطبيقات التي تركز على الهواتف المحمولة تُصدر الكاميرا ملفات HEIC، بينما لا تزال الأنظمة القديمة تحتاج إلى PDF التقليدي. يوضح لك هذا الدرس بالضبط كيفية **تحويل HEIC إلى PDF**، وإضافة الصورة إلى صفحة PDF جديدة، وأخيرًا **إنشاء PDF من صورة** باستخدام Aspose.Pdf.

سنستعرض كل سطر من الشيفرة، نشرح لماذا كل جزء مهم، ونزودك بمثال جاهز للتنفيذ. في النهاية ستتمكن من وضع ملف HEIC في مجلد والحصول على PDF واضح منه—دون الحاجة إلى أدوات خارجية.

## ما ستتعلمه

* كيفية **قراءة ملفات HEIC** في C# باستخدام مُحلل `FileFormat.Heic`.
* الخطوات الدقيقة **لتحويل HEIC إلى PDF** باستخدام Aspose.Pdf.
* طرق **إضافة صورة إلى PDF** والتحكم في تنسيق البكسل.
* نصائح للتعامل مع الصور الكبيرة والمشكلات الشائعة.
* برنامج كامل جاهز للترجمة يمكنك نسخه ولصقه.

*المتطلبات المسبقة*: .NET 6+ (أو .NET Framework 4.6+)، Aspose.Pdf for .NET، وحزمة NuGet `FileFormat.Heic`. إذا لم تستخدم هذه المكتبات من قبل، لا تقلق—ستتم تغطية عملية التثبيت في الخطوة الأولى.

---

## الخطوة 0: تثبيت الحزم المطلوبة

قبل أن نغوص في الشيفرة، تأكد من أن المكتبتين مضافتين إلى مشروعك:

```powershell
dotnet add package Aspose.Pdf
dotnet add package FileFormat.Heic
```

كلا الحزمتين مجانيين للتطوير ويدعمان .NET Standard، لذا يمكنهما العمل في تطبيقات الكونسول، ASP.NET، أو حتى Unity.

---

## الخطوة 1: كيفية قراءة HEIC – تحميل الملف كدفق

قراءة ملف HEIC مشابهة لفتح أي ملف ثنائي، لكنك تحتاج إلى مُحلل يفهم حاوية HEIC. مكتبة `FileFormat.Heic` توفر لنا طريقة ثابتة `Load` مفيدة.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using FileFormat.Heic.Decoder;

// ...

// Open the HEIC file safely with a using block
using (FileStream heicStream = new FileStream(
           @"C:\Images\input.heic", FileMode.Open, FileAccess.Read))
{
    // Decode the HEIC image into a HeicImage object
    HeicImage heicImage = HeicImage.Load(heicStream);
```

**لماذا نستخدم تدفقًا؟**  
التدفق يسمح للمُحلل بقراءة الملف بشكل كسول، مما يقلل الضغط على الذاكرة للصور الضخمة. جملة `using` تضمن أيضًا تحرير مقبض الملف، مما يمنع أخطاء قفل الملف لاحقًا.

---

## الخطوة 2: تحويل HEIC إلى PDF – استخراج بيانات البكسل

Aspose.Pdf يتوقع بيانات bitmap خام، وليس كائن HEIC. لذا نستخرج بايتات البكسل بصيغة يفهمها—`Rgb24` تعمل لمعظم الحالات.

```csharp
    // Grab the raw RGB24 pixel array from the HEIC image
    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);

    // Capture image dimensions for later use
    int width  = (int)heicImage.Width;
    int height = (int)heicImage.Height;
```

**ملاحظة حالة الحافة:** إذا كان ملف HEIC المصدر يحتوي على قناة ألفا، فإن `Rgb24` ستتجاهلها. للحصول على الشفافية يمكنك التحويل إلى `Rgba32` وتعديل `BitmapInfo` وفقًا لذلك.

---

## الخطوة 3: إضافة صورة إلى PDF – بناء كائن Aspose Image

الآن نغلف البايتات الخام في كائن `Aspose.Pdf.Image`. مُنشئ `BitmapInfo` يخبر Aspose بخطوة العرض (stride)، الحجم، وتنسيق البكسل.

```csharp
    // Create an Aspose PDF Image using the pixel buffer
    Image pdfImage = new Image
    {
        BitmapInfo = new BitmapInfo(
            pixelData,
            width,
            height,
            BitmapInfo.PixelFormat.Rgb24)
    };
```

**نصيحة محترف:** إذا كنت تخطط لإدراج العديد من الصور في نفس المستند، أعد استخدام نسخة واحدة من كائن `Document` وأنشئ كائنات `Image` جديدة فقط لكل صفحة. هذا يوفر عبء إنشاء الكائنات.

---

## الخطوة 4: إنشاء PDF من صورة – تجميع المستند

مع جاهزية الصورة، ننشئ مستند PDF جديد، نضيف صفحة، ونضع الصورة عليها. مجموعة `Paragraphs` في Aspose تجعل ذلك سهلًا جدًا.

```csharp
    // Initialize a new PDF document
    Document pdfDoc = new Document();

    // Add a blank page to the document
    Page page = pdfDoc.Pages.Add();

    // Insert the image into the page's paragraph collection
    page.Paragraphs.Add(pdfImage);
```

إذا كنت بحاجة إلى تموضع الصورة (في الوسط، تعديل الحجم، إلخ)، يمكنك تغليفها في `ImageStamp` أو تعديل `pdfImage.Margin`. بالنسبة لمعظم التحويلات من صورة إلى PDF مباشرة، يكون الوضع الافتراضي كافيًا.

---

## الخطوة 5: حفظ النتيجة – كتابة ملف PDF إلى القرص

الخطوة الأخيرة هي ببساطة حفظ ملف PDF. Aspose يدعم العديد من الصيغ؛ هنا نستخدم الصيغة الكلاسيكية `.pdf`.

```csharp
    // Define the output path and save the PDF
    string outputPath = @"C:\Images\output.pdf";
    pdfDoc.Save(outputPath);
}
```

**الناتج المتوقع:** فتح `output.pdf` في أي عارض سيظهر الصورة الأصلية من HEIC معروضة بدقتها الأصلية. لا فقدان جودة يتجاوز ضغط HEIC الأصلي.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه إلى تطبيق كونسول. يتضمن جميع توجيهات `using` ومعالجة الأخطاء لتجربة جاهزة للإنتاج.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using FileFormat.Heic.Decoder;

namespace HeicToPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath  = @"C:\Images\input.heic";
            string outputPath = @"C:\Images\output.pdf";

            try
            {
                // 1️⃣ Open the HEIC file as a stream
                using (FileStream heicStream = new FileStream(
                           inputPath, FileMode.Open, FileAccess.Read))
                {
                    // 2️⃣ Load the HEIC image from the stream
                    HeicImage heicImage = HeicImage.Load(heicStream);

                    // 3️⃣ Extract pixel data in RGB24 format
                    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);
                    int width  = (int)heicImage.Width;
                    int height = (int)heicImage.Height;

                    // 4️⃣ Create an Aspose.Pdf.Image using the pixel data
                    Image pdfImage = new Image
                    {
                        BitmapInfo = new BitmapInfo(
                            pixelData,
                            width,
                            height,
                            BitmapInfo.PixelFormat.Rgb24)
                    };

                    // 5️⃣ Add the image to a new PDF page
                    Document pdfDoc = new Document();
                    Page page = pdfDoc.Pages.Add();
                    page.Paragraphs.Add(pdfImage);

                    // 6️⃣ Save the resulting PDF
                    pdfDoc.Save(outputPath);
                }

                Console.WriteLine($"✅ Success! PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Error: {ex.Message}");
            }
        }
    }
}
```

شغّل البرنامج، وسترى رسالة الكونسول التي تؤكد إنشاء ملف PDF. افتح الملف، ويجب أن تكون الصورة مطابقة للـ HEIC الأصلي.

---

## أسئلة شائعة ومشكلات محتملة

### ماذا لو كان ملف HEIC تالفًا؟

طريقة `HeicImage.Load` تُطلق استثناء `HeicException`. ضع الاستدعاء داخل try/catch (كما هو موضح) وسجّل الخطأ. في بيئة الإنتاج قد تلجأ إلى صورة بديلة افتراضية.

### هل يمكنني معالجة عدة ملفات HEIC دفعةً واحدة؟

بالطبع. فقط انقل المنطق الأساسي إلى دالة مثل `ConvertHeicToPdf(string input, string output)` وكرر عبر دليل باستخدام `Directory.GetFiles("*.heic")`.

### هل يحافظ هذا الأسلوب على بيانات EXIF الوصفية؟

لا، Aspose.Pdf لا ينسخ بيانات EXIF تلقائيًا إلى PDF. إذا كنت بحاجة إلى البيانات الوصفية، استخرجها باستخدام `HeicImage.Metadata` وأضفها إلى PDF عبر خصائص `Document.Info`.

### ماذا عن استهلاك الذاكرة للصور الضخمة؟

بالنسبة للصور التي تتجاوز 10 MP، فكر في تقليل الدقة قبل إنشاء `BitmapInfo`. يمكنك استخدام `HeicImage.Resize` (إذا كان مدعومًا) أو مكتبة bitmap من طرف ثالث لتقليل الأبعاد.

---

## الخلاصة

أنت الآن تعرف كيف **إنشاء صورة PDF** من مصدر HEIC، وتقوم **بتحويل HEIC إلى PDF** بفعالية، وتضيف **صورة إلى PDF** باستخدام Aspose.Pdf في C#. الخطوات—قراءة HEIC، استخراج بيانات البكسل، تغليفها في صورة PDF، وحفظها—بسيطة، لكنها قوية بما يكفي لخطوط الإنتاج.

بعد ذلك، جرّب توسيع السكريبت: أنشئ PDF متعدد الصفحات حيث تحمل كل صفحة HEIC مختلف، أو أدمج طبقات نص OCR للحصول على PDF قابل للبحث. يمكنك أيضًا استكشاف صيغ صور أخرى (`jpeg`, `png`) بنفس النمط، لتعزيز مهارة **إنشاء PDF من صورة**.

لا تتردد في التجربة، مشاركة ما توصلت إليه، أو طرح أسئلة في التعليقات. برمجة سعيدة!

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إضافة رأس صورة إلى ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-image-header-pdf-aspose-dotnet/)
- [كيفية إضافة ختم صورة إلى PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [إضافة ختم صورة إلى تذييل PDF باستخدام Aspose.PDF .NET: دليل خطوة بخطوة](/pdf/english/net/document-manipulation/add-image-stamp-pdf-footer-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}