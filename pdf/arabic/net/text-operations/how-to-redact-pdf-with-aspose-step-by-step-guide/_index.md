---
category: general
date: 2026-03-03
description: كيفية تعديل PDF باستخدام Aspose PDF SDK. تعلم إضافة تعليقات PDF، إخفاء
  النص، وحفظ PDF المعدل في دقائق.
draft: false
keywords:
- how to redact pdf
- add pdf annotation
- how to hide text
- save redacted pdf
- aspose pdf redaction
language: ar
og_description: كيفية تعديل PDF بسرعة باستخدام Aspose. يوضح هذا الدرس كيفية إضافة
  تعليقات توضيحية إلى PDF، إخفاء النص، وحفظ PDF المعدل بأمان.
og_title: كيفية إزالة المعلومات الحساسة من PDF باستخدام Aspose – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF Redaction
title: كيفية تعتيم PDF باستخدام Aspose – دليل خطوة بخطوة
url: /ar/net/text-operations/how-to-redact-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حذف محتوى PDF باستخدام Aspose – دليل خطوة بخطوة

هل تساءلت يومًا **how to redact PDF** دون الإخلال بهيكل المستند؟ لست وحدك—العديد من المطورين يحتاجون إلى إخفاء المعلومات الحساسة، لكنهم غير متأكدين أي استدعاءات API تحذف المحتوى فعليًا. في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يُظهر **how to redact PDF** باستخدام مكتبة Aspose.Pdf، وكيفية **add PDF annotation**، وكيفية **save redacted PDF** بأمان.

سنغطي كل شيء من فتح الملف المصدر إلى التحقق من أن النص المخفي اختفى فعلاً. في النهاية ستعرف **how to hide text** باستخدام تعليمة حذف، لماذا إدخال ExtGState مهم، وما الخطوات الإضافية التي يمكنك اتخاذها إذا احتجت إلى مسح أكثر شدة. لا حاجة لمستندات خارجية—فقط انسخ‑الصق الكود وشغّله.

---

## ما ستحتاجه

- **Aspose.Pdf for .NET** (الإصدار 23.12 أو أحدث). يمكنك الحصول عليه من NuGet باستخدام `Install-Package Aspose.Pdf`.
- بيئة تطوير .NET (Visual Studio، Rider، أو VS Code مع امتداد C#).
- ملف PDF إدخال (`input.pdf`) يحتوي على النص الذي تريد إخفائه.
- إلمام أساسي بـ C#—لا شيء معقد، فقط القدرة على تشغيل تطبيق كونسول.

> **Pro tip:** إذا كنت تعمل على خط أنابيب CI، تأكد من توفر ملف ترخيص Aspose؛ وإلا ستظهر علامة تقييم مائية.

---

## الخطوة 1 – فتح مستند PDF المصدر

الأول الذي تقوم به عندما تريد **how to redact PDF** هو تحميل الملف إلى كائن `Aspose.Pdf.Document`. هذا يمنحك وصولًا كاملًا إلى الصفحات، التعليقات التوضيحية، وكائنات PDF منخفضة المستوى.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.DataEditor;

class PdfRedactionDemo
{
    static void Main()
    {
        // Path to the original PDF
        string inputPath = @"YOUR_DIRECTORY\input.pdf";

        // Load the document (this is where the redaction process begins)
        using (var pdfDocument = new Document(inputPath))
        {
            // The rest of the steps go here...
```

*لماذا هذا مهم:* تحميل المستند ينشئ تمثيلًا في الذاكرة يمكنك تعديلّه. إذا تخطيت هذه الخطوة، لن يكون هناك ما يتم حذفه، وستطلق SDK استثناء `FileNotFoundException`.

---

## الخطوة 2 – تعريف منطقة الحذف (Add PDF Annotation)

الحذف هو في الأساس نوع خاص من التعليقات التوضيحية يخبر عارض PDF بإخفاء مستطيل. هنا ننشئ `RedactionAnnotation` يغطي الإحداثيات **left = 50, bottom = 500, right = 200, top = 550**.

```csharp
            // Step 2: Define a redaction area (left, bottom, right, top)
            var redactionRect = new Rectangle(50, 500, 200, 550);
            var redactionAnnotation = new RedactionAnnotation(redactionRect);
```

*لماذا نستخدم تعليمة توضيحية:* نهج **add pdf annotation** هو الأنظف لإخبار محرك PDF أي أجزاء من المحتوى يجب أن تختفي. على عكس رسم صندوق أسود فوق النص، يمكن لتعليمة الحذف فعليًا إزالة الأحرف الأساسية عند تسوية المستند.

---

## الخطوة 3 – إرفاق تعليمة الحذف بالصفحة المطلوبة

تقوم Aspose.Pdf بترقيم الصفحات بدءًا من **1**، لذا `pdfDocument.Pages[1]` يشير إلى الصفحة الأولى. إضافة التعليمة إلى الصفحة تسجلها للمعالجة لاحقًا.

```csharp
            // Step 3: Attach the redaction annotation to the first page
            pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);
```

*مشكلة شائعة:* نسيان إضافة التعليمة إلى الصفحة يعني أن الحذف لن يُظهر أبدًا. تأكد دائمًا من فهرس الصفحة، خاصةً عندما يحتوي PDF المصدر على أكثر من صفحة واحدة.

---

## الخطوة 4 – التحكم في المظهر باستخدام إدخال ExtGState

بشكل افتراضي قد تظهر تعليمة الحذف كصندوق أبيض. لجعلها تبدو كشريط أسود صلب (أو أي مظهر مخصص) نقوم بحقن إدخال **ExtGState** اسمه `GS0`. هذا حالة رسومية منخفضة المستوى في PDF تُجبر لون التعبئة على أن يكون أسود.

```csharp
            // Step 4: Add a custom ExtGState entry to control the redaction appearance
            var dictEditor = new DictionaryEditor(redactionAnnotation);
            dictEditor["ExtGState"] = new CosPdfName("GS0");
```

*لماذا هذه الخطوة اختيارية لكنها مفيدة:* إذا كنت تحتاج فقط إلى **how to hide text** بصريًا، يمكنك تخطي ExtGState. ومع ذلك، يضمن ضبطه أن يبدو الحذف متسقًا عبر المشاهدين وأن النص الأساسي لا يُكشف عن طريق الخطأ عند طباعة PDF.

---

## الخطوة 5 – حفظ PDF المحذوف (Save Redacted PDF)

الآن بعد أن وضعت التعليمة، استدعِ `pdfDocument.Save`. تقوم Aspose تلقائيًا بتطبيق الحذف، إزالة المحتوى المخفي، وكتابة النتيجة إلى ملف جديد.

```csharp
            // Step 5: Save the redacted PDF
            string outputPath = @"YOUR_DIRECTORY\redacted.pdf";
            pdfDocument.Save(outputPath);
        } // using block disposes the document
    }
}
```

*ما يفعله “save redacted pdf” فعليًا:* تقوم SDK بتسوية التعليمة، مسح النص داخل المستطيل، وكتابة PDF نظيف. يبقى `input.pdf` الأصلي دون تعديل، وهو ما يناسب سجلات التدقيق.

---

## الخطوة 6 – التحقق من أن النص قد اختفى فعلاً

سؤال شائع هو **“how to hide text”** دون ترك أثر قابل للبحث. بعد الحفظ، افتح `redacted.pdf` في عارض يدعم تحديد النص (مثل Adobe Acrobat). حاول تحديد المنطقة المظلمة—إذا لم تتمكن من نسخ أي أحرف، فنجح الحذف.

يمكنك أيضًا التحقق برمجيًا:

```csharp
using (var checkDoc = new Document(@"YOUR_DIRECTORY\redacted.pdf"))
{
    string extracted = new TextAbsorber().ExtractText();
    if (extracted.Contains("SensitiveString"))
        Console.WriteLine("Redaction failed!");
    else
        Console.WriteLine("Redaction succeeded.");
}
```

*حالة خاصة:* إذا كان PDF الخاص بك يستخدم طبقات نص مخفية (مثل طبقات OCR)، قد تحتاج إلى تشغيل `RedactionAnnotation` على كل طبقة أو استخدام الخاصية `RedactionAnnotation.RemoveText = true` لمسح أكثر شدة.

---

## نصائح إضافية ومشكلات شائعة

| الحالة | ما يجب فعله |
|-----------|------------|
| **Multiple pages need redaction** | كرّر عبر `pdfDocument.Pages` وأضف `RedactionAnnotation` إلى كل صفحة مستهدفة. |
| **Dynamic coordinates** | استخدم `TextFragmentAbsorber` لتحديد المستطيل الدقيق للكلمة المفتاحية، ثم أدخل تلك الإحداثيات في مستطيل الحذف. |
| **Different appearance (red instead of black)** | أنشئ قاموس ExtGState مخصص مع `CA` (شفافية الخط) و`ca` (شفافية التعبئة) مضبوطة على اللون المطلوب. |
| **Performance on large PDFs** | افتح المستند في وضع **read‑only** (`new Document(inputPath, new LoadOptions { LoadMode = LoadMode.Memory })`) لتقليل استهلاك الذاكرة. |
| **License issues** | تأكد من استدعاء `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` قبل تحميل المستند. |

---

## مثال كامل جاهز للتنفيذ (Copy‑Paste Ready)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.DataEditor;

class PdfRedactionDemo
{
    static void Main()
    {
        // License (optional but recommended for production)
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\redacted.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            // Define the redaction rectangle
            var redactionRect = new Rectangle(50, 500, 200, 550);
            var redactionAnnotation = new RedactionAnnotation(redactionRect);

            // Attach to page 1
            pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);

            // Set ExtGState for solid black appearance
            var dictEditor = new DictionaryEditor(redactionAnnotation);
            dictEditor["ExtGState"] = new CosPdfName("GS0");

            // Save the redacted file
            pdfDocument.Save(outputPath);
        }

        // Optional verification step
        using (var checkDoc = new Document(outputPath))
        {
            var absorber = new TextAbsorber();
            checkDoc.Pages.Accept(absorber);
            string extracted = absorber.Text;
            Console.WriteLine("Verification complete. Extracted text length: " + extracted.Length);
        }
    }
}
```

تشغيل هذا التطبيق الكونسولي سيُنتج `redacted.pdf` حيث يتم تغطية المستطيل المحدد باللون الأسود وإزالة النص الأساسي—وهو الجواب الدقيق على **how to redact PDF** الذي كنت تبحث عنه.

---

## الخاتمة

في هذا الدليل أظهرنا **how to redact PDF** باستخدام Aspose.Pdf، وبيّنّا كيفية **add PDF annotation**، وشرحنا **how to hide text**، ومَرَرنا بخطوات **save redacted PDF** بأمان. الآن لديك أساس قوي لبناء خطوط معالجة حذف تلقائية، سواءً كنت تنظف عقودًا قانونية، أو تزيل معلومات تعريفية شخصية، أو تُعدّ مستندات للنشر العام.

بعد ذلك، قد تستكشف سيناريوهات أكثر تقدمًا مثل معالجة مجموعة من ملفات PDF دفعيًا، دمج OCR لتحديد النص الديناميكي، أو استخدام خاصية `RedactionAnnotation`’s `OverlayText` لوضع كلمة “REDACTED” فوق الشريط الأسود. جميع هذه المواضيع ترتبط بكلماتنا المفتاحية الثانوية—**add pdf annotation**, **how to hide text**, **save redacted pdf**, و**aspose pdf redaction**—لذا أنت في موقع جيد للغوص أعمق.

هل لديك أسئلة حول حالات خاصة أو تحتاج مساعدة في تعديل إحداثيات المستطيل؟ اترك تعليقًا أدناه، وتمنياتنا لك بحذف موفق!

---

![How to redact PDF example](/images/how-to-redact-pdf.png){: .align-center alt="how to redact pdf visual example"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}