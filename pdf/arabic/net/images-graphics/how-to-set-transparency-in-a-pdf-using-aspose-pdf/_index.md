---
category: general
date: 2026-11-16
description: كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf عن طريق تعديل موارد
  PDF وتحميل الملف بكفاءة. اتبع هذا الدليل الكامل بلغة C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- edit pdf resources
- load pdf aspose
language: ar
lastmod: 2026-11-16
og_description: كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf، مما يتيح التحكم
  الدقيق في درجة التعتيم للرسومات مباشرةً من C#.
og_image_alt: C# code snippet that sets PDF transparency via Aspose.Pdf
og_title: ضبط شفافية PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to set transparency in a PDF with Aspose.Pdf by editing PDF resources
    and loading the PDF efficiently. Follow this complete C# guide.
  headline: How to set transparency in a PDF using Aspose.Pdf
  type: TechArticle
- description: How to set transparency in a PDF with Aspose.Pdf by editing PDF resources
    and loading the PDF efficiently. Follow this complete C# guide.
  name: How to set transparency in a PDF using Aspose.Pdf
  steps:
  - name: '**Load the PDF** with Aspose.Pdf (`load pdf aspose`).'
    text: '**Load the PDF** with Aspose.Pdf (`load pdf aspose`).'
  - name: '**Access the first page’s resources** dictionary (`edit pdf resources`).'
    text: '**Access the first page’s resources** dictionary (`edit pdf resources`).'
  - name: '**Create a custom ExtGState** that contains the desired transparency values.'
    text: '**Create a custom ExtGState** that contains the desired transparency values.'
  - name: '**Insert the ExtGState** back into the page resources.'
    text: '**Insert the ExtGState** back into the page resources.'
  - name: '**Save the modified PDF**.'
    text: '**Save the modified PDF**.'
  type: HowTo
tags:
- PDF
- Aspose.Pdf
- C#
title: كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf
url: /ar/net/images-graphics/how-to-set-transparency-in-a-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ضبط الشفافية في ملف PDF باستخدام Aspose.Pdf

إذا كنت بحاجة إلى **كيفية ضبط الشفافية** في مستند PDF، فإن هذا الدليل يوضح الخطوات الدقيقة باستخدام Aspose.Pdf لـ .NET. سواءً كنت تبني محرك تقارير أو تضيف علامات مائية، فإن التحكم في التعتيم يُعدّ مطلبًا شائعًا. بنهاية هذا الشرح ستحصل على برنامج C# قابل للتنفيذ يقوم بتحميل ملف PDF، تعديل موارده، وكتابة النتيجة مرة أخرى إلى القرص.

العمل مع ملفات PDF يعني غالبًا أنك تحتاج إلى **تحرير موارد PDF** مثل قاموس ExtGState، ويجب عليك أيضًا **تحميل PDF Aspose** بشكل صحيح لتجنب إنتاج ملف معطوب. يغطي هذا الدليل كلا الجانبين ويشرح لماذا كل عملية مهمة، بحيث يمكنك تعديل النمط للوثائق متعددة الصفحات أو حالات الرسومات المخصصة.

## نظرة عامة على كيفية ضبط الشفافية في PDF

تُعرّف الشفافية في PDF بواسطة كائن *ExtGState* (حالة رسومات خارجية). يخزن الكائن معلمات مثل تعتيم الخط (`CA`)، تعتيم التعبئة (`ca`)، ووضع المزج (`BM`). يتيح لك Aspose.Pdf تعديل هذه القواميس مباشرة، مما يمنحك تحكمًا دقيقًا دون الاعتماد على واجهات برمجة تطبيقات أعلى مستوى.

التدفق العام هو:

1. **تحميل ملف PDF** باستخدام Aspose.Pdf (`load pdf aspose`).
2. **الوصول إلى قاموس موارد الصفحة الأولى** (`edit pdf resources`).
3. **إنشاء ExtGState مخصص** يحتوي على قيم الشفافية المطلوبة.
4. **إدراج ExtGState** مرة أخرى في موارد الصفحة.
5. **حفظ ملف PDF المعدل**.

كل خطوة مُنفذة في طريقة C# مختصرة، والكود الكامل يظهر في نهاية المقال.

## الخطوة 1: تحميل ملف PDF باستخدام Aspose.Pdf (`load pdf aspose`)

قبل أن تتمكن من تحرير أي شيء، يجب فتح الملف باستخدام فئة `Document` الخاصة بـ Aspose. يضمن بيان `using` تحرير مقبض الملف حتى لو حدث استثناء.

```csharp
// Step 1: Load the PDF document
using (var pdfDocument = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf"))
{
    // All subsequent operations happen inside this block.
}
```

**لماذا هذا مهم:**  
يقوم Aspose.Pdf بتحليل بنية PDF إلى نموذج كائنات. تحميل المستند مرة واحدة وإبقائه في الذاكرة يجنب عمليات الإدخال/الإخراج المتكررة ويضمن تطبيق أي تغييرات تقوم بها على نفس النسخة.

**نصيحة:** إذا كان ملف PDF الأصلي محميًا بكلمة مرور، مرّر كلمة المرور إلى مُنشئ `Document`:

```csharp
var pdfDocument = new Aspose.Pdf.Document("input.pdf", new LoadOptions { Password = "mySecret" });
```

## الخطوة 2: الوصول إلى قاموس موارد الصفحة (`edit pdf resources`)

كل صفحة PDF تحتوي على قاموس *Resources* يحمل الخطوط، الصور، وحالات الرسومات. لإضافة ExtGState جديد، استرجع هذا القاموس واحصل على القاموس الفرعي `ExtGState` الموجود (أو أنشئ واحدًا إذا لم يكن موجودًا).

```csharp
// Step 2: Access the first page's resources dictionary
var firstPage = pdfDocument.Pages[1];                     // Aspose uses 1‑based indexing
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

// Ensure the ExtGState entry exists; if not, create an empty dictionary.
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    resourcesEditor["ExtGState"] = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
}
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

**لماذا هذا مهم:**  
قاموس `Resources` هو المكان الوحيد الذي يبحث فيه مُعالج PDF عن تعريفات حالات الرسومات. إذا كان إدخال `ExtGState` مفقودًا، سيتجاهل الصفحة أي إعدادات تعتيم تُشير إليها لاحقًا.

**حالة خاصة:** بعض ملفات PDF تحتوي بالفعل على قاموس `ExtGState` مع العديد من الإدخالات. في هذه الحالة يمكنك إعادة استخدام القاموس الموجود، كما هو موضح أعلاه، لتجنب الكتابة فوق الحالات غير المتعلقة.

## الخطوة 3: تعريف معلمات الشفافية

تُتحكم الشفافية بثلاث مفاتيح:

| المفتاح | المعنى | النطاق المعتاد |
|--------|--------|----------------|
| `CA` | تعتيم الخط | 0 (شفاف) … 1 (معتم) |
| `ca` | تعتيم التعبئة | 0 … 1 |
| `BM` | وضع المزج | `"Normal"`، `"Multiply"`، إلخ |

أنشئ `CosPdfDictionary` جديدًا واملأه بالقيم المطلوبة.

```csharp
// Step 3: Create a new ExtGState dictionary with desired entries
var customExtGState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var graphicsStateParameters = new[]
{
    // Stroke opacity = 1 (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA",
        new Aspose.Pdf.CosPdfNumber(1)),
    // Fill opacity = 0.5 (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca",
        new Aspose.Pdf.CosPdfNumber(0.5)),
    // Blend mode = Normal (standard source‑over composition)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM",
        new Aspose.Pdf.CosPdfName("Normal"))
};

foreach (var param in graphicsStateParameters)
    customExtGState.Add(param);
```

**لماذا هذا مهم:**  
ضبط `ca` إلى `0.5` يجعل أي شكل مملوء (مثل مستطيل أو نص) يظهر شبه شفاف. يمكنك تعديل هذه الأرقام للحصول على التأثير البصري الدقيق الذي تحتاجه. يحدد وضع المزج كيفية دمج المحتوى الشفاف مع الرسومات السفلية؛ `"Normal"` هو الخيار الأكثر شيوعًا.

**نصيحة احترافية:** إذا كنت بحاجة إلى وضع مزج مختلف، استبدل `"Normal"` بـ `"Multiply"` أو `"Screen"` لتحقيق تأثيرات فنية مثل تعتيم أو إضاءة المحتوى الأساسي.

## الخطوة 4: إدراج ExtGState المخصص في موارد الصفحة

الآن اربط القاموس باسم (مثلاً `GS0`) وأضفه إلى مجموعة `ExtGState` الخاصة بالصفحة.

```csharp
// Step 4: Add the custom ExtGState entry to the page resources
extGStateDict.Add("GS0", customExtGState);
```

**لماذا هذا مهم:**  
الاسم (`GS0`) يُشار إليه لاحقًا بواسطة عوامل الرسومات في تدفق المحتوى. إذا كنت تخطط لاستخدام الحالة على صفحات متعددة، يمكنك إعادة استخدام نفس الاسم أو إنشاء أسماء خاصة بالصفحات (`GS1`, `GS2`, …).

**تعديل متقدم:** لتطبيق الحالة على تدفق محتوى موجود، يمكنك إلحاق عامل PDF `q /GS0 gs` قبل أوامر الرسم. يوفر Aspose.Pdf فئة `PdfContentEditor` لهذا الغرض، لكن ذلك خارج نطاق هذا الدرس الأساسي.

## الخطوة 5: حفظ ملف PDF المعدل

أخيرًا، احفظ التغييرات إلى ملف جديد. الحفاظ على الأصل دون تعديل يجعل من السهل مقارنة النتائج قبل/بعد.

```csharp
// Step 5: Save the modified PDF
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

**التحقق:** افتح `output.pdf` في أي عارض PDF. أي شكل مملوء يستخدم حالة الرسومات المخصصة (مثل مستطيل مرسوم بـ `GS0`) سيظهر بتعتيم 50 ٪. إذا لم تلاحظ أي تغيير، تحقق من أن تدفق المحتوى فعلاً يشير إلى `GS0`. يمكنك إدراج مستطيل اختبار باستخدام `PdfContentEditor` كفحص اختياري.

## مثال كامل يعمل

جمع جميع الخطوات معًا ينتج برنامجًا مستقلًا يمكنك نسخه ولصقه في تطبيق Console.

```csharp
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Load the PDF (load pdf aspose)
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources (edit pdf resources)
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            if (!resourcesEditor.ContainsKey("ExtGState"))
                resourcesEditor["ExtGState"] = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create custom ExtGState with transparency
            var customExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) customExtGState.Add(p);
            extGStateDict.Add("GS0", customExtGState);

            // OPTIONAL: Apply the graphics state to a sample rectangle
            // This demonstrates that the transparency works.
            var canvas = new Aspose.Pdf.PageEditor(firstPage);
            canvas.AddRectangle(100, 500, 200, 600); // left, bottom, right, top
            // Set the graphics state before drawing
            canvas.ContentStream.Operators.Insert(0, new SetGraphicsState("GS0"));
            canvas.Save();

            // Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        System.Console.WriteLine("Transparency applied successfully.");
    }
}
```

**شرح الكتلة الاختيارية:**  
تضيف `PageEditor` مستطيلًا بسيطًا إلى الصفحة وتعيّن صراحةً حالة الرسومات إلى `GS0`. هذه الخطوة مفيدة للاختبار؛ في سيناريو حقيقي ستتوفر لديك محتويات بالفعل تشير إلى الحالة.

## شائع


## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to add graphics state pdf and control transparency with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [How to add transparency to PDF using Aspose.PDF in C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [How to change PDF transparency using Aspose.Pdf in C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}