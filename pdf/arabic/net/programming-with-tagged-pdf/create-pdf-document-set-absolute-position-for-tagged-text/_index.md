---
category: general
date: 2026-03-24
description: إنشاء مستند PDF وتعلم كيفية تعيين موضع مطلق للنص الموسوم. يوضح هذا الدرس
  كيفية إضافة عنصر <span>، وكيفية إضافة محتوى موسوم وتحديد موضع النص على الصفحة.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: ar
og_description: أنشئ مستند PDF وشاهد فورًا كيفية ضبط الموضع المطلق، إضافة عنصر <span>،
  وتحديد موضع النص على الصفحة باستخدام محتوى PDF الموسوم.
og_title: إنشاء مستند PDF – التموضع المطلق للنص المعلَّم
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: إنشاء مستند PDF – تعيين الموضع المطلق للنص الموسوم
url: /ar/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF – تعيين موضع مطلق للنص الموسوم

هل احتجت يوماً إلى **create pdf document** يحتوي على نص موسوم يمكن الوصول إليه ومُحدد بالضبط حيث تريد؟ ربما تقوم بإنشاء PDF يشبه النموذج حيث يجب أن يكون التسمية في إحداثيات دقيقة، أو أنك تولد شهادة ويجب أن يتطابق الاسم تماماً مع صورة الخلفية.  

في هذا الدليل سنستعرض مثالاً كاملاً قابلاً للتنفيذ يوضح **how to add tagged** المحتوى، **set absolute position**، و **add span element** حتى تتمكن من **position text on page** دون تخمين. لا مراجع خارجية—فقط الشيفرة التي يمكنك نسخ‑لصقها، بالإضافة إلى شرح “السبب” وراء كل سطر.

## المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.6+) مع مترجم C#
- Aspose.Pdf for .NET (أحدث إصدار وقت كتابة هذا الدليل، 23.12) مثبت عبر NuGet
- إلمام أساسي بصياغة C#

إذا كان لديك ذلك، لنبدأ.

---

## إنشاء مستند PDF – تعيين الموضع المطلق

الخطوة الأولى التي نقوم بها هي إنشاء كائن `Document` فارغ. هذا الكائن يمثل ملف PDF بالكامل ويمنحنا الوصول إلى شجرة المحتوى الموسوم.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**لماذا هذا مهم:**  
`Document` هو الجذر لهياكل PDF. بإنشائه أولاً نضمن وجود مساحة لكل من العناصر البصرية (الصفحات، الرسومات) والبنية المنطقية (الوسوم). جملة `using` تضمن إغلاق الملف بشكل صحيح، مما يمنع تسرب مقبض الملف على نظام Windows.

---

## تمكين المحتوى الموسوم (كيفية إضافة الوسوم)

قبل أن نتمكن من إدراج أي عناصر موسومة، يجب أن يتم وضع علامة *موسوم* على المستند. تقوم Aspose.Pdf بإنشاء كائن `TaggedContent` تلقائياً، لكن لا يزال عليك تشغيل العلامة.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**ماذا يحدث خلف الكواليس؟**  
ضبط `TaggedContent` إلى `true` يخبر قارئات PDF أن الملف يحتوي على شجرة بنية منطقية. هذا أمر حاسم لقارئات الشاشة ولطريقة `SetPosition` لتعمل بشكل صحيح على عنصر span.

---

## الحصول على العنصر الجذري لشجرة المحتوى الموسوم

العنصر الجذري هو نقطة الدخول لجميع الوسوم الهيكلية (مثل `<Document>`، `<Section>`، `<Span>`). فكر فيه كـ “body” غير مرئي للـ PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**لماذا نحتاج الجذر:**  
يجب إرفاق جميع الوسوم اللاحقة في مكان ما داخل الشجرة؛ وإلا لن تظهر في هيكلية إمكانية الوصول.

---

## إضافة عنصر Span – الوحدة الأساسية للنص داخل السطر

*span* هو ما يعادل PDF لعنصر HTML `<span>`—مثالي لقطع النص القصيرة التي تريد تحديد موضعها بدقة.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**ملاحظة تصميمية:**  
إذا كنت بحاجة إلى تنسيق أغنى (غامق، مائل، روابط)، يمكنك تغليف الـ span داخل `<Paragraph>` أو استخدام كائنات `TextFragment` لاحقاً. بالنسبة للتحديد المطلق، فإن الـ span العادي هو الأخف وزنًا.

---

## تعيين الموضع المطلق – X=100, Y=200

الآن يأتي الجزء الممتع: وضع الـ span في موقع دقيق على الصفحة. يبدأ نظام الإحداثيات من الزاوية السفلية اليسرى (0,0) ويستخدم النقاط (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**لماذا التحديد المطلق؟**  
عندما تحتاج إلى تخطيط بدقة البكسل—مثل الشهادات، الفواتير، أو النماذج—التدفق النسبي (مثل النص من اليسار إلى اليمين) لا يكفي. `SetPosition` يتجاوز تدفق النص العادي ويثبت العنصر في الموضع الذي تحدده.

---

## إضافة نص إلى الـ Span

بعد تحديد موضع الـ span، نقوم الآن بإدخال السلسلة الفعلية.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**نصيحة:**  
إذا كنت بحاجة إلى أحرف Unicode أو نصوص من اليمين إلى اليسار، فقط مرّر السلسلة؛ Aspose.Pdf يتعامل مع الترميز تلقائيًا.

---

## إلحاق الـ Span بالعنصر الجذري

أخيرًا، نرفق الـ span بشجرة المستند المنطقية لتصبح جزءًا من ملف PDF النهائي.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**ماذا لو نسيت هذه الخطوة؟**  
سيبقى الـ span في الذاكرة لكنه لن يُسلسل إلى الملف، لذا لن ترى أي نص وستكون شجرة إمكانية الوصول غير مكتملة.

---

## مثال كامل وقابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك وضعه في تطبيق كونسول. يقوم بإنشاء PDF من صفحة واحدة، يضيف span موسوم عند (100, 200)، ويحفظ الملف باسم `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**الناتج المتوقع:**  
افتح `TaggedPositioned.pdf` في أي عارض (Adobe Acrobat، Foxit، إلخ). سترى العبارة **“Positioned tagged text”** بالضبط 100 pt من الحافة اليسرى و200 pt من الحافة السفلية للصفحة. إذا فحصت لوحة *Tags*، سيظهر عنصر `<Span>` تحت الجذر الخاص بالمستند، مؤكدًا أن المحتوى موسوم بشكل صحيح.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى وضع النص على صفحة معينة غير الأولى؟

أضف الصفحة التي تريدها (`var page = pdfDocument.Pages[3];`) قبل استدعاء `SetPosition`. سيُرفق الـ span تلقائيًا بسياق الصفحة النشطة.

### هل يمكنني تحديد الموضع بالبوصة أو السنتيمتر؟

`SetPosition` تقبل النقاط. حوّل باستخدام الصيغ:

- **البوصة → نقاط:** `points = inches * 72`
- **السنتيمتر → نقاط:** `points = cm * 28.3465`

### كيف يمكنني تغيير الخط أو لون الـ span؟

بعد إنشاء الـ span، يمكنك الحصول على `TextState` الخاص به وتعديله:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### ماذا لو كان المستند يحتوي بالفعل على وسوم موجودة؟

ما زال بإمكانك إنشاء span جديد وإلحاقه بأي عنصر موجود (`rootElement`، `<Section>` محدد، إلخ). فقط تأكد من الحفاظ على التسلسل الهرمي المنطقي—قوارئ الشاشة تتوقع شجرة منظمة جيدًا.

### هل يعمل هذا مع توافق PDF/A أو PDF/UA؟

نعم. الـ PDFs الموسومة هي متطلب أساسي لـ PDF/UA. إذا كنت بحاجة إلى PDF/A، اضبط `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` بعد بناء المحتوى.

---

## نصائح احترافية ومخاطر

- **نصيحة احترافية:** دائمًا أضف صفحة قبل تحديد موضع المحتوى. بدون صفحة، `SetPosition` يفشل بصمت لأنه لا يوجد مكان للعرض.
- **احذر الوحدات:** خلط البكسل من تصميم واجهة المستخدم مع نقاط PDF سيؤدي إلى وضع النص في مكان غير صحيح. تحقق مرتين من التحويل.
- **تلميح الأداء:** إذا كنت تولد آلاف ملفات PDF، أعد استخدام كائن `Document` واحد واستدعِ `pdfDocument.Pages.Clear()` بين كل تشغيل لتجنب استهلاك الذاكرة الزائد.
- **تذكير بإمكانية الوصول:** الوسم ليس مجرد ميزة إضافية؛ العديد من اللوائح (Section 508, EN 301 549) تتطلبه. استخدام `CreateSpanElement` يضمن أن النص قابل للاكتشاف بواسطة تقنيات المساعدة.

---

## الخلاصة

لقد **أنشأنا pdf document** من الصفر، **حددنا الموضع المطلق**، **أضفنا عنصر span**، وأظهرنا **how to add tagged** المحتوى حتى تتمكن من **position text on page** بدقة البكسل. المثال الكامل جاهز للتنفيذ، والشرح غطى كلًا من *كيفية* و*سبب*—بالضبط ما يبحث عنه المطورون (والمساعدون الذكائيون) عندما يحتاجون إلى حل موثوق.

بعد ذلك، قد تستكشف:

- إضافة صور خلف النص المحدد لإنشاء شهادات مائية.
- استخدام `CreateParagraphElement` للكتل متعددة الأسطر التي لا تزال تحتاج إلى تحديد مطلق.
- التصدير إلى PDF/UA لتلبية تدقيقات إمكانية الوصول الصارمة.

لا تتردد في تعديل الإحداثيات أو الخطوط أو الألوان—التجربة هي أسرع طريقة لإتقان إنشاء PDF الموسوم. إذا واجهت أي مشكلة، اترك تعليقًا أدناه؛ برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}