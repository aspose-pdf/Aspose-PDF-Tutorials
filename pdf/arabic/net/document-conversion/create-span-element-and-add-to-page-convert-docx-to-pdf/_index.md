---
category: general
date: 2026-03-27
description: إنشاء عنصر <span> في C# وتعلم كيفية إضافة <span> إلى صفحة أثناء تحويل
  ملف DOCX إلى PDF وحفظه كملف PDF. دليل خطوة بخطوة للمطورين.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: ar
og_description: إنشاء عنصر <span> في C# وتعلم كيفية إضافة <span> إلى صفحة أثناء تحويل DOCX إلى PDF،
  ثم حفظه كملف PDF. مثال كامل على الكود مرفق.
og_title: إنشاء عنصر <span> وإضافته إلى الصفحة – تحويل DOCX إلى PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: إنشاء عنصر <span> وإضافته إلى الصفحة – تحويل DOCX إلى PDF
url: /ar/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء عنصر span وإضافته إلى الصفحة – تحويل DOCX إلى PDF

إنشاء **عنصر span** في ملف DOCX هو مهمة شائعة عندما تحتاج إلى التحكم الدقيق في التخطيط. في هذا الدرس سنوضح لك **كيفية إضافة span** إلى صفحة، **تحويل DOCX إلى PDF**، و**حفظه كملف PDF**—كل ذلك في بضع خطوات مرتبة.

إذا سبق لك وأن نظرت إلى مستند Word وفكرت، “أتمنى لو أستطيع وضع صندوق نص صغير عند إحداثيات دقيقة”، فأنت في المكان الصحيح. سنستعرض سير العمل بالكامل، من تحميل الملف المصدر إلى الحصول على ملف PDF مصقول.

## ما ستحققه

بنهاية هذا الدليل ستكون قادرًا على:

* تحميل ملف `.docx` باستخدام فئة `Document` من مكتبة المستندات.  
* **إنشاء عنصر span** باستخدام API `TaggedContent`.  
* وضع هذا الـ span عند إحداثيات X/Y دقيقة على الصفحة المختارة.  
* **إضافة العنصر إلى الصفحة** بثقة، حتى وإن لم تكن الصفحة الأولى.  
* **تحويل DOCX إلى PDF** و**حفظه كملف PDF** باستدعاء واحد لـ `Save`.

بدون أدوات خارجية، بدون إعدادات غامضة—فقط كود C# بسيط يمكنك نسخه ولصقه في مشروعك.

## المتطلبات المسبقة

* .NET 6+ (أو أي بيئة تشغيل .NET حديثة تدعمها المكتبة).  
* مجموعة تطوير SDK لمعالجة المستندات التي توفر `Document`، `TaggedContent`، `Position`، إلخ.  
* فهم أساسي لصياغة C#—إذا كنت تستطيع كتابة `Console.WriteLine` فأنت جاهز.

> **نصيحة احترافية:** حافظ على تحديث نسخة SDK الخاصة بك؛ الإصدار الأخير (v3.2 اعتبارًا من مارس 2026) يتضمن تحسينات أداء لعمليات مستوى الصفحة.

---

![مخطط يوضح كيفية إنشاء عنصر span ووضعه على صفحة PDF](https://example.com/images/create-span-element.png "مخطط وضع عنصر span")

## إنشاء عنصر span – تحديد الموقع وإضافته إلى الصفحة

فيما يلي الكود الكامل القابل للتنفيذ الذي يقوم بكل شيء من تحميل ملف DOCX المصدر إلى كتابة ملف PDF النهائي. يمكنك وضعه في تطبيق console، تعديل المسارات، وتشغيله.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### شرح خطوة بخطوة

#### الخطوة 1 – تحميل مستند DOCX  
نقوم بإنشاء كائن `Document` يشير إلى `input.docx`. هذا الكائن يمثل ملف Word بالكامل في الذاكرة، ويمنحنا الوصول إلى الصفحات والمحتوى والبيانات الوصفية.

#### الخطوة 2 – إنشاء عنصر span  
استدعاء `TaggedContent.CreateSpanElement()` يُعيد حاوية مضمنة خفيفة الوزن. فكر فيها كصندوق صغير غير مرئي يمكنه احتواء نص أو صور أو عناصر مضمنة أخرى. إضافة نص (`span.Text`) اختياري لكنه مفيد للتصحيح.

#### الخطوة 3 – تحديد موقع الـ span  
`new Position(50, 750)` يضع الزاوية العلوية اليسرى للـ span على بعد 50 نقطة من الهامش الأيسر و750 نقطة من أعلى الصفحة. هذه القيم مطلقة، لذا يمكنك وضع الـ span في أي مكان—مثالي للتخطيطات الدقيقة.

#### الخطوة 4 – إضافة الـ span إلى الصفحة المستهدفة  
`doc.Pages[1].Add(span)` يدرج الـ span في الصفحة الثانية. يستخدم الـ API فهرسة تبدأ من الصفر، لذا الصفحة 0 هي الصفحة الأولى. إذا أردت إضافته إلى الصفحة الأولى، استخدم ببساطة `doc.Pages[0]`.

#### الخطوة 5 – تحويل DOCX إلى PDF وحفظه كملف PDF  
استدعاء `doc.Save("output.pdf")` يقوم بشيئين: يكتب المستند المعدل إلى القرص **ويحول المحتوى إلى PDF** بفضل امتداد `.pdf`. لا حاجة لخطوة تحويل إضافية—هذه أسهل طريقة لـ **حفظ كملف PDF**.

---

## كيفية إضافة span إلى صفحة مختلفة (متقدم)

أحيانًا لا تعرف فهرس الصفحة مسبقًا. يمكنك تحديد صفحة بناءً على رقمها (الذي يقرأه الإنسان) أو بالبحث عن كلمة مفتاحية معينة.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**لماذا هذا مهم:** في التقارير التي يختلف عدد صفحاتها، قد يؤدي الترميز الثابت `Pages[1]` إلى كسر التخطيط. يوضح هذا المقتطف نمطًا قويًا لـ **كيفية إضافة span** بشكل ديناميكي.

---

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | ما يحدث | الحل |
|-------|--------------|-----|
| **الـ span غير مرئي** | الإحداثيات خارج الصفحة أو الـ span له عرض/ارتفاع صفر. | تحقق مرة أخرى من قيم `Position`؛ استخدم مسطرة في عارض PDF. |
| **فهرس الصفحة خاطئ** | تضيف إلى الصفحة 0 لكن تتوقعها في الصفحة 2. | تذكر أن الـ API يستخدم الفهرسة من الصفر؛ أضف 1 إلى رقم الصفحة البشري. |
| **الحفظ يكتب فوق المصدر** | `doc.Save("input.docx")` يستبدل الملف الأصلي. | احفظ دائمًا إلى مسار جديد (`output.pdf`) عند التحويل. |
| **غياب مرجع SDK** | خطأ تجميع على فئة `Document`. | ثبّت حزمة NuGet: `dotnet add package DocumentProcessing.SDK`. |

---

## التحقق من النتيجة

بعد تشغيل البرنامج، افتح `output.pdf` في أي عارض PDF. يجب أن ترى النص “Hello, world!” موضعًا بالضبط عند (50, 750) على الصفحة الثانية. إذا ظهر النص في مكان آخر، عدّل قيم `Position` وأعد التشغيل.

للاختبار الآلي، يمكنك استخدام محلل PDF (مثل iTextSharp) للتحقق من إحداثيات النص برمجيًا.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## الخطوات التالية

* **تنسيق الـ span** – استكشف `span.Font`، `span.Color`، وغيرها من خصائص التنسيق.  
* **إضافة صور** – استخدم `CreateImageElement()` بدلًا من الـ span للرسومات.  
* **معالجة دفعات** – كرّر العملية على مجلد من ملفات DOCX

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}