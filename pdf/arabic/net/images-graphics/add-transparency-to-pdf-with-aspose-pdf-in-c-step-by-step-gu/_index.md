---
category: general
date: 2026-03-19
description: أضف الشفافية إلى ملف PDF باستخدام Aspose.PDF للغة C#. تعلّم كيفية ضبط
  الشفافية، وضع الدمج، وExtGState في بضع أسطر من الشيفرة فقط.
draft: false
keywords:
- add transparency to pdf
- Aspose PDF transparency
- C# PDF graphics state
- PDF blend mode
- set PDF opacity
language: ar
og_description: أضف الشفافية إلى ملفات PDF بسرعة. يوضح هذا الدليل كيفية التحكم في
  الشفافية ووضع الدمج باستخدام Aspose.PDF في C#.
og_title: إضافة الشفافية إلى PDF باستخدام Aspose PDF – دليل C# الكامل
tags:
- Aspose.PDF
- C#
title: إضافة الشفافية إلى PDF باستخدام Aspose PDF في C# – دليل خطوة بخطوة
url: /ar/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة شفافية إلى PDF باستخدام Aspose PDF في C# – دليل كامل

هل تساءلت يومًا **كيف تضيف شفافية إلى ملفات PDF** دون الحاجة للغوص في صsyntax منخفض المستوى للـ PDF؟ لست وحدك. يحتاج العديد من المطورين إلى طريقة سريعة لجعل الأشكال أو النص شبه شفاف—مثل العلامات المائية، الرسومات المتراكبة، أو تلميحات واجهة المستخدم الخفيفة داخل المستند.  

في هذا الدليل سنستعرض **مثالًا كاملاً وقابلًا للتنفيذ** يوضح بالضبط كيفية تعيين شفافية التعبئة، شفافية الحد، ووضع المزج باستخدام Aspose.PDF for .NET. في النهاية ستحصل على PDF يظهر فيه مستطيل بشفافية 50 %، وستفهم لماذا يعتبر قاموس ExtGState المفتاح لتحقيق هذا التأثير.

سنغطي كل ما تحتاجه: حزمة NuGet المطلوبة، الكود نفسه، شرح كل سطر، وبعض النصائح لحالات الحافة مثل عارضات PDF القديمة. لا مراجع خارجية—حل مستقل يمكنك نسخه ولصقه وتشغيله اليوم.

## ما ستحتاجه

- **Aspose.PDF for .NET** (الإصدار 23.12 أو أحدث). تثبيت عبر NuGet: `Install-Package Aspose.PDF`.
- بيئة تطوير .NET (Visual Studio، Rider، أو سطر أوامر `dotnet` CLI).
- ملف PDF تجريبي اسمه `input.pdf` موجود في مجلد تتحكم فيه (يستخدم الدليل `YOUR_DIRECTORY/` كعنصر نائب).

هذا كل شيء. إذا كان لديك هذه المتطلبات، لنبدأ.

## إضافة شفافية إلى PDF – نظرة عامة

جوهر جعل شيء ما شفافًا في PDF هو **حالة الرسومات** (`ExtGState`). بإضافة كائن حالة رسومات مخصص إلى قاموس موارد الصفحة يمكنك تعريف:

| الخاصية | المعنى |
|----------|---------|
| `ca` | شفافية التعبئة (0 = شفاف تمامًا، 1 = معتم). |
| `CA` | شفافية الحد (نفس المقياس). |
| `BM` | وضع المزج (مثل `Normal`, `Multiply`). |

سننشئ حالة رسومات جديدة، ندرجها في قاموس `ExtGState` للصفحة، ثم نُشير إليها عند الرسم لاحقًا. المقتطف البرمجي أدناه يفعل ذلك بالضبط.

![add transparency to pdf diagram](add_transparency_to_pdf.png){alt="إضافة شفافية إلى PDF"}

## الخطوة 1: إعداد المشروع وتحميل PDF

أولاً ننشئ تطبيقًا بسيطًا من نوع console (أو أي مشروع C#) ونحمّل PDF المصدر.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;          // For low‑level PDF operators
using Aspose.Pdf.Text;               // Optional, if you want to add text later
using Aspose.Pdf.XObjects;          // For image handling, not needed here

// Define the folder that contains the PDF file
string inputDir = @"YOUR_DIRECTORY/";

// Load the PDF document
using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
{
    // All subsequent steps go inside this using block
```

**لماذا هذا مهم:**  
`Document` هو نقطة الدخول لأي تعديل على PDF باستخدام Aspose. وضعه داخل جملة `using` يضمن تفريغ جميع الموارد بشكل صحيح عند حفظ الملف لاحقًا.

## الخطوة 2: الوصول إلى الصفحة الأولى ومواردها

نحتاج إلى قاموس موارد الصفحة الأولى لأن مجموعة `ExtGState` توجد هناك.

```csharp
    // Grab the first page (pages are 1‑based in Aspose)
    Page firstPage = pdfDocument.Pages[1];

    // Helper to edit dictionaries (resources, etc.)
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);

    // Retrieve the existing ExtGState dictionary, or create a new one if missing
    CosPdfDictionary extGStateDict;
    if (resourcesEditor.ContainsKey("ExtGState"))
    {
        extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
    }
    else
    {
        extGStateDict = new CosPdfDictionary(pdfDocument);
        resourcesEditor.Add("ExtGState", extGStateDict);
    }
```

**شرح:**  
إذا كانت الصفحة تحتوي بالفعل على مدخل `ExtGState` نعيد استخدامه؛ وإلا ننشئ قاموسًا جديدًا. هذه الطريقة الوقائية تمنع حدوث أخطاء مرجعية عندما نتعامل مع PDFs لا تحتوي على أي حالات رسومات.

## الخطوة 3: إنشاء حالة رسومات جديدة مع الشفافية المطلوبة

الآن نحدد قيم الشفافية الفعلية.

```csharp
    // Create an empty dictionary that will represent our new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Stroke opacity – fully opaque (1.0)
    newGraphicsState.Add("CA", new CosPdfNumber(1));

    // Fill opacity – 50 % transparent (0.5)
    newGraphicsState.Add("ca", new CosPdfNumber(0.5));

    // Blend mode – Normal is the default, but you can experiment with Multiply, Screen, etc.
    newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**لماذا هذه المفاتيح؟**  
- `CA` يتحكم في شفافية الخطوط (الحدود، الإطارات).  
- `ca` يتحكم في شفافية التعبئة (الأشكال الصلبة، النص).  
- `BM` يحدد كيفية دمج الكائن الشفاف مع المحتوى الأساسي. استخدام `"Normal"` يبقي النتيجة مرئية بشكل متوقع عبر جميع العارضات.

## الخطوة 4: تسجيل حالة الرسومات في موارد الصفحة

نعطي حالة الرسومات اسمًا (`GS0`) ونضيفها إلى قاموس `ExtGState`.

```csharp
    // Add the graphics state to the ExtGState dictionary with a unique name
    extGStateDict.Add("GS0", newGraphicsState);
```

**نصيحة:**  
إذا احتجت إلى كائنات شفافة متعددة بشفافية مختلفة، أنشئ مدخلات إضافية (`GS1`, `GS2`, …) وعدّل قيم `ca`/`CA` وفقًا لذلك.

## الخطوة 5: رسم مستطيل شفاف باستخدام حالة الرسومات الجديدة

مع وجود حالة الرسومات، يمكننا الآن رسم شيء يستخدمها فعليًا. أدناه نضيف مستطيلًا أزرقًا شبه شفاف إلى الصفحة.

```csharp
    // Prepare a content stream for the page (adds to existing content)
    var canvas = new Aspose.Pdf.Drawing.Graphic(firstPage);

    // Set the graphics state we just created
    canvas.SetGraphicsState("GS0");

    // Choose a fill color (blue) and draw the rectangle
    canvas.SetColor(new Aspose.Pdf.Drawing.Color(0, 0, 255)); // RGB blue
    canvas.Rectangle(100, 500, 200, 100); // x, y, width, height

    // Close the canvas to flush commands
    canvas.Close();
```

**ما ستراه:**  
عند فتح PDF الناتج، سيظهر مستطيل أزرق في الموقع المحدد، لكن المحتوى الأساسي للصفحة سيظل مرئيًا من خلاله لأن شفافية التعبئة هي 0.5. إذا فحصت PDF بأداة مثل ميزة “Edit PDF” في Adobe Acrobat، ستلاحظ كائن `ExtGState` (`GS0`) المرتبط بهذا المستطيل.

## الخطوة 6: حفظ PDF المحدث

أخيرًا، نكتب المستند المعدل إلى القرص.

```csharp
    // Save the document with a new name so the original stays untouched
    pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
}
```

هذا هو سير العمل بالكامل. شغّل تطبيق console، افتح `ExtGStateAdded.pdf`، وتحقق من وجود التراكب الشفاف.

---

## مثال كامل يعمل (جاهز للنسخ‑اللصق)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddTransparencyDemo
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF file
        string inputDir = @"YOUR_DIRECTORY/";

        // Step 2: Load the PDF document
        using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
        {
            // Step 3: Get the first page and its resource dictionary
            Page firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", extGStateDict);
            }

            // Step 4: Create a new graphics state with opacity and blend mode settings
            CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity (fully opaque)
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));       // fill opacity (50% transparent)
            newGraphicsState.Add("BM", new CosPdfName("Normal"));   // blend mode

            // Step 5: Add the new graphics state to the page resources
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 6: Draw a rectangle using the new graphics state
            var canvas = new Graphic(firstPage);
            canvas.SetGraphicsState("GS0");
            canvas.SetColor(new Color(0, 0, 255)); // blue fill
            canvas.Rectangle(100, 500, 200, 100);
            canvas.Close();

            // Step 7: Save the updated PDF document
            pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
        }

        Console.WriteLine("PDF with transparency created successfully.");
    }
}
```

**النتيجة المتوقعة:**  
فتح `ExtGStateAdded.pdf` يُظهر مستطيلًا أزرقًا عند (100, 500) بشفافية تعبئة 50 %. تحت المستطيل، يظل أي نص أو صورة موجودة مرئية.

---

## الأسئلة المتكررة وحالات الحافة

### هل يعمل هذا مع عارضات PDF القديمة؟
معظم العارضات الحديثة (Adobe Reader, Foxit, Chrome) تدعم مفاتيح الشفافية الأساسية `ca`/`CA`. قد تتجاهب العارضات القديمة جدًا هذه المفاتيح وتعرض الشكل بملء كامل غير شفاف.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}