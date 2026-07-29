---
category: general
date: 2026-07-29
description: أضف الشفافية إلى ملف PDF باستخدام Aspose.Pdf لـ .NET. تعلم كيفية ضبط
  شفافية PDF، وضع الدمج، وحالة الرسومات في دليل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- Aspose.Pdf for .NET
- ExtGState dictionary
- PDF opacity
- graphics state
- Blend mode
language: ar
lastmod: 2026-07-29
og_description: أضف الشفافية إلى PDF بسرعة. يوضح هذا الدليل كيفية ضبط شفافية PDF ووضع
  الدمج باستخدام Aspose.Pdf لـ .NET.
og_image_alt: Screenshot of a PDF page showing transparent overlay created with Aspose.Pdf
og_title: إضافة الشفافية إلى PDF باستخدام Aspose.Pdf – دليل كامل لـ .NET
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Add transparency to PDF using Aspose.Pdf for .NET. Learn to set PDF
    opacity, blend mode, and graphics state in a step‑by‑step tutorial.
  headline: Add Transparency to PDF with Aspose.Pdf – Complete .NET Guide
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- .NET
title: إضافة الشفافية إلى PDF باستخدام Aspose.Pdf – دليل .NET الكامل
url: /ar/net/advanced-features/add-transparency-to-pdf-with-aspose-pdf-complete-net-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة الشفافية إلى PDF باستخدام Aspose.Pdf – دليل .NET كامل

هل احتجت يومًا إلى **إضافة شفافية إلى ملفات PDF** لكنك لم تكن متأكدًا من أي خصائص API يجب تعديلها؟ لست وحدك. في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية يوضح بالضبط كيفية ضبط شفافية PDF، وتحديد وضع المزج، وإدخال حالة رسومية جديدة باستخدام **Aspose.Pdf for .NET**.

سنبدأ بملف PDF فارغ، نضيف مستطيلًا شبه شفاف، ثم نحفظ النتيجة—كل ذلك في بضع أسطر فقط. في النهاية ستفهم لماذا يعتبر **قاموس ExtGState** مهمًا، وكيف تتحكم **الحالة الرسومية** في شفافية الخط والملء، وما يفعله **وضع المزج** خلف الكواليس.

## ما ستتعلمه

- كيفية تحميل ملف PDF موجود باستخدام Aspose.Pdf.  
- كيفية الوصول إلى **قاموس ExtGState** وتعديله في صفحة.  
- كيفية إنشاء **حالة رسومية** جديدة تحدد الإدخالات `CA` و `ca` و `BM`.  
- كيفية حفظ المستند المعدل بحيث يكون تأثير الشفافية مرئيًا في أي عارض PDF.  
- الأخطاء الشائعة (مثل نسيان إضافة الحالة الجديدة إلى قاموس الموارد) والحلول السريعة.

> **المتطلبات المسبقة:** Visual Studio 2022 (أو أي بيئة تطوير تفضلها)، .NET 6 أو أحدث، ورخصة Aspose.Pdf for .NET (التجربة المجانية تكفي لهذا العرض).  

---

## الخطوة 1: تحميل مستند PDF

أولًا—افتح الملف الذي تريد تعديله. تتولى فئة `Aspose.Pdf.Document` كل شيء من التحليل إلى الكتابة.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"C:\Temp\input.pdf";   // replace with your actual path
using var document = new Aspose.Pdf.Document(pdfPath);
```

*لماذا هذا مهم:* تحميل المستند يمنحك الوصول إلى كائنات COS (Concrete Object Structure) الداخلية، حيث تكمن **الحالة الرسومية**. بدون كائن `Document` صالح لا يمكنك الوصول إلى **قاموس ExtGState**.

---

## الخطوة 2: الحصول على الصفحة الأولى وقاموس مواردها

يتم تطبيق الشفافية على مستوى موارد الصفحة، لذا نحتاج إلى مجموعة موارد الصفحة.

```csharp
// Step 2: Access the first page and its resource dictionary
var page = document.Pages[1];                     // pages are 1‑based in Aspose
var resourcesEditor = new Aspose.Pdf.Text.DictionaryEditor(page.Resources);
```

> **نصيحة:** إذا كنت تعمل مع ملفات PDF متعددة الصفحات، ما عليك سوى التكرار عبر `document.Pages` وتكرار الخطوات لكل صفحة تريد تعديلها.

---

## الخطوة 3: تحديد (أو إنشاء) قاموس ExtGState

تخزن إدخالة **ExtGState** جميع الحالات الرسومية الموسعة للصفحة. إذا لم يكن موجودًا بعد، سيقوم Aspose بإنشاء واحد فارغ لنا.

```csharp
// Step 3: Retrieve the ExtGState dictionary where graphics states are stored
var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                ?? new Aspose.Pdf.Cos.CosPdfDictionary(document);
```

*شرح:*  
- `resourcesEditor["ExtGState"]` يجلب القاموس الموجود.  
- عامل الـ null‑coalescing (`??`) يضمن أن لدينا دائمًا قاموسًا للعمل معه، مما يمنع حدوث `NullReferenceException`.

---

## الخطوة 4: بناء حالة رسومية جديدة مع شفافية PDF

الآن نحدد معلمات الشفافية الفعلية. `CA` يتحكم في شفافية الخط، `ca` يتحكم في شفافية الملء، و `BM` يحدد وضع المزج (مثل “Normal”، “Multiply”، إلخ).

```csharp
// Step 4: Create a new graphics state dictionary and define its parameters
var newGraphicsState = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(document);

var parameters = new (string Name, Aspose.Pdf.Cos.ICosPdfPrimitive Value)[]
{
    ("CA", new Aspose.Pdf.Cos.CosPdfNumber(1.0)),      // Stroke opacity = 100%
    ("ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),      // Fill opacity = 50%
    ("BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))   // Blend mode = Normal
};

foreach (var (name, value) in parameters)
{
    newGraphicsState.Add(name, value);
}
```

*لماذا هذه المفاتيح؟*  
- `CA` (`Stroke opacity`) و `ca` (`Fill opacity`) هما الإدخالان الرقميان الذين يستخدمهما معيار PDF للتعبير عن الشفافية.  
- `BM` (`Blend mode`) يخبر المُعالج كيف يجمع الكائن الشفاف مع الخلفية؛ “Normal” هو الخيار الأكثر شيوعًا.

---

## الخطوة 5: تسجيل الحالة الجديدة في قاموس ExtGState

نُعطي حالتنا الرسومية اسمًا (`GS0` في هذا المثال) ونضعه في مجموعة **ExtGState** الخاصة بالصفحة.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a name
extGState.Add("GS0", newGraphicsState);

// Ensure the page's Resources point to the updated ExtGState
resourcesEditor["ExtGState"] = extGState;
```

> **نصيحة احترافية:** اختر اسمًا فريدًا (`GS1`، `GS2`، …) إذا كنت تخطط لإضافة حالات متعددة. إعادة استخدام اسم سيؤدي إلى استبدال الإدخال السابق.

---

## الخطوة 6: تطبيق الحالة الرسومية على المحتوى (اختياري لكن مُستحسن)

إذا أردت رؤية تأثير الشفافية فورًا، يمكنك رسم مستطيل باستخدام الحالة التي أنشأتها للتو. هذه الخطوة ليست ضرورية تمامًا لـ *إضافة شفافية إلى PDF*—الحالة الآن متاحة لأي تدفقات محتوى مستقبلية—لكنها تساعدك على التحقق من أن كل شيء يعمل.

```csharp
// Optional: Draw a semi‑transparent rectangle using the new graphics state
var canvas = new Aspose.Pdf.Drawing.Graphic(page);
canvas.SetExtGState("GS0");                     // reference the state we just added
canvas.Rectangle(100, 500, 200, 100);          // x, y, width, height
canvas.FillColor = Aspose.Pdf.Drawing.Color.FromRgba(255, 0, 0, 128); // red with 50% alpha
canvas.StrokeColor = Aspose.Pdf.Drawing.Color.Black;
canvas.Draw();
```

*شرح:*  
- `SetExtGState("GS0")` يخبر تدفق المحتوى باستخدام الحالة الرسومية التي عرّفناها.  
- سيظهر المستطيل بشفافية ملء 50 %، مؤكدًا أن إعدادات **شفافية PDF** فعّالة.

---

## الخطوة 7: حفظ ملف PDF المعدل

أخيرًا، اكتب التغييرات إلى القرص.

```csharp
// Step 7: Save the modified PDF
string outputPath = @"C:\Temp\output.pdf";
document.Save(outputPath);
```

افتح `output.pdf` في Adobe Acrobat أو Foxit أو حتى المتصفح—يجب أن ترى المستطيل شبه الشفاف يغطي محتوى الصفحة.

---

## مثال عملي كامل

لنجمع كل شيء معًا، إليك البرنامج الكامل جاهزًا للنسخ واللصق:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        string pdfPath = @"C:\Temp\input.pdf";
        using var document = new Document(pdfPath);

        // Access first page and its resources
        var page = document.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // Retrieve or create ExtGState dictionary
        var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                        ?? new CosPdfDictionary(document);

        // Build new graphics state (stroke opacity 1, fill opacity 0.5, normal blend)
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
        var parameters = new (string, ICosPdfPrimitive)[]
        {
            ("CA", new CosPdfNumber(1.0)),
            ("ca", new CosPdfNumber(0.5)),
            ("BM", new CosPdfName("Normal"))
        };
        foreach (var (name, value) in parameters)
            newGraphicsState.Add(name, value);

        // Add graphics state to ExtGState with a unique name
        extGState.Add("GS0", newGraphicsState);
        resourcesEditor["ExtGState"] = extGState;   // update page resources

        // OPTIONAL: draw a rectangle using the new state to verify
        var canvas = new Graphic(page);
        canvas.SetExtGState("GS0");
        canvas.Rectangle(100, 500, 200, 100);
        canvas.FillColor = Color.FromRgba(255, 0, 0, 128); // 50% transparent red
        canvas.StrokeColor = Color.Black;
        canvas.Draw();

        // Save the output PDF
        string outputPath = @"C:\Temp\output.pdf";
        document.Save(outputPath);
    }
}
```

### النتيجة المتوقعة

- يحتوي `output.pdf` على الصفحات الأصلية **بالإضافة إلى** مستطيل أحمر شفاف بنسبة 50 %.  
- إدخال **ExtGState** `GS0` أصبح الآن جزءًا من قاموس موارد الصفحة، جاهزًا لإعادة الاستخدام.

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **هل أحتاج إلى رخصة لتشغيل هذا؟** | رخصة تجريبية تعمل للتطوير والاختبار. للإنتاج ستحتاج إلى رخصة مدفوعة، وإلا سيظهر علامة مائية في الناتج. |
| **ماذا لو كان ملف PDF يحتوي بالفعل على إدخال ExtGState؟** | يتحقق الكود من وجود القاموس ويعيد استخدامه، لذا لن تفقد أي حالات معرفة مسبقًا. |
| **هل يمكنني تعيين وضع مزج مختلف؟** | بالتأكيد. استبدل `"Normal"` بـ `"Multiply"` أو `"Screen"` أو أي وضع مزج معرف في PDF. |
| **هل `CA` إلزامي؟** | لا. إذا حذفت `CA`، فإن شفافية الخط تُفترض 1 (معتمة بالكامل). يمكنك أيضًا تعيين `ca` فقط لشفافية الملء. |
| **كيف أطبق الحالة على النص؟** | استخدم `canvas.SetExtGState("GS0")` قبل استدعاء `canvas.ShowText(...)`. نفس الحالة الرسومية تعمل مع النص والمسارات والصور. |

---

## الخطوات التالية

الآن

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [إضافة طوابع الصور إلى ملفات PDF باستخدام Aspose.PDF for .NET&#58; دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)
- [كيفية إضافة طابع نصي إلى PDF باستخدام Aspose.PDF .NET&#58; دليل شامل](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [كيفية إضافة طوابع الصفحات في ملفات PDF باستخدام Aspose.PDF for .NET&#58; دليل كامل](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}