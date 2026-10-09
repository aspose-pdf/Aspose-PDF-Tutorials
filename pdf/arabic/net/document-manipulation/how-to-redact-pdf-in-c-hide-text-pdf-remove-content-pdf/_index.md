---
category: general
date: 2026-03-01
description: كيفية تعديل محتوى ملف PDF بسرعة باستخدام Aspose.Pdf في C#. تعلم كيفية
  إخفاء النص في PDF، إزالة المحتوى من PDF، وتعديل المنطقة في PDF مع مثال كامل وقابل
  للتنفيذ.
draft: false
keywords:
- how to redact pdf
- hide text pdf
- remove content pdf
- create pdf document c#
- redact area in pdf
language: ar
og_description: كيفية تعديل محتوى PDF في C# باستخدام Aspose.Pdf. يوضح لك هذا الدليل
  كيفية إخفاء النص في PDF، وإزالة المحتوى من PDF، وتعديل منطقة في PDF مع توفير الكود
  المصدري الكامل.
og_title: كيفية تعديل PDF في C# – إخفاء نص PDF وإزالة محتوى PDF
tags:
- Aspose.Pdf
- C#
- PDF Redaction
title: كيفية تنقيح PDF في C# – إخفاء النص في PDF وإزالة المحتوى من PDF
url: /ar/net/document-manipulation/how-to-redact-pdf-in-c-hide-text-pdf-remove-content-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمويه PDF في C# – إخفاء نص PDF وإزالة محتوى PDF

هل تساءلت يومًا **how to redact pdf** دون قضاء ساعات في العبث بأدوات الطرف الثالث؟ لست وحدك. في العديد من المشاريع التي تتطلب امتثالًا عاليًا تحتاج إلى hide text pdf، وإزالة البيانات السرية، مع الحفاظ على باقي المستند كما هو.  

الأخبار السارة؟ مع Aspose.Pdf for .NET يمكنك فعل كل ذلك في بضع أسطر فقط. في هذا الدرس سنستعرض إنشاء مستند PDF في C#، تعريف منطقة التمويه، وأخيرًا حفظ نسخة نظيفة. بنهاية الدرس ستعرف بالضبط كيفية remove content pdf، hide text pdf، وredact area in pdf—كل ذلك من خلال كود يمكنك إدراجه في أي مشروع .NET.

## المتطلبات المسبقة وما ستبنيه

- **.NET 6+** (أو .NET Framework 4.6+ – الـ API هو نفسه)
- حزمة NuGet **Aspose.Pdf for .NET** (`Aspose.Pdf`)
- فهم أساسي لصياغة C# (لا شيء معقد مطلوب)

سننتج ملفًا يُسمى `redacted.pdf` يحتوي على مستطيل أحمر يغطي الإحداثيات (100, 100)‑(300, 200). أي شيء تحت ذلك المستطيل سيُحذف نهائيًا، وهو بالضبط ما تحتاجه عندما يُطلب منك **hide text pdf** لأسباب GDPR أو قانونية.

> **نصيحة محترف:** إذا احتجت إلى تمويه مناطق منفصلة متعددة، فقط أضف المزيد من كائنات `RedactionAnnotation` إلى نفس الصفحة – المكتبة تتعامل معها جميعًا في تمريرة واحدة.

---

## كيفية تمويه PDF – خطوة بخطوة

أسفل كل خطوة ستجد مقتطف كود مختصر، شرحًا *لسبب* أهمية السطر، ونصيحة سريعة لتجنب الأخطاء الشائعة.

### 1. إعداد المشروع وإضافة Aspose.Pdf

أولاً، أنشئ تطبيق console جديد (أو دمجه في خدمة موجودة) وقم بتثبيت حزمة NuGet:

```bash
dotnet new console -n PdfRedactionDemo
cd PdfRedactionDemo
dotnet add package Aspose.Pdf
```

> **لماذا؟** تثبيت الحزمة يجلب تجميع `Aspose.Pdf`، الذي يحتوي على `Document`، `RedactionAnnotation`، وجميع كائنات PDF منخفضة المستوى التي ستحتاجها. بدونها لا يمكنك **remove content pdf** برمجيًا.

### 2. إنشاء مستند PDF في الذاكرة

نبدأ بـ PDF فارغ – فكّر فيه كصفحة بيضاء يمكنك الكتابة عليها.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Redactions;

class Program
{
    static void Main()
    {
        // Step 2: Create a new PDF document in memory
        using var pdfDocument = new Document();

        // (Optional) Add a page with some sample text so you can see the redaction effect
        var page = pdfDocument.Pages.Add();
        page.Paragraphs.Add(new TextFragment("Sensitive data: 123‑45‑6789"));
```

**لماذا هذا مهم:**  
- `using var` يضمن تحرير المستند بشكل صحيح، محرّرًا الموارد الأصلية.  
- إضافة صفحة بنص مرئي يتيح لك التحقق من أن التمويه يزيل المحتوى فعليًا بدلاً من مجرد تغطيته.

### 3. تعريف تعليقة التمويه (منطقة “hide text pdf”)

هنا نحدد المستطيل الذي سيُحذف من الصفحة.

```csharp
        // Step 3: Define a redaction annotation covering the desired area
        var redactionRect = new Rectangle(100, 100, 300, 200);
        var redactionAnnotation = new RedactionAnnotation(redactionRect)
        {
            // Optional: set the fill color to a solid black for visual feedback
            FillColor = Color.Black,
            // Optional: set overlay text that will appear after redaction
            OverlayText = "REDACTED"
        };

        // Attach the annotation to the first page (index 1)
        pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);
```

**لماذا؟** `RedactionAnnotation` تخبر Aspose *أين* تُمحى البيانات. المستطيل يستخدم نظام إحداثيات PDF (الأصل في أسفل‑اليسار). إذا كنت معتادًا على إحداثيات Windows GDI، تذكر أن محور Y مقلوب.

> **خطأ شائع:** نسيان إضافة التعليقة إلى `Pages[1].Annotations`. ستظل التعليقة موجودة، لكن لا شيء سيُتموّه.

### 4. تحضير الموارد (مثل XObjects) – استخدام متقدم

إذا كنت تخطط لإدراج صور أو رسومات مخصصة داخل منطقة التمويه، يمكنك تحميلها مسبقًا في قاموس موارد التعليقة.

```csharp
        // Step 4: Access the annotation's resources dictionary (optional)
        var resources = redactionAnnotation.Resources;
        // Example: add an XObject later – omitted here for brevity
```

**لماذا نضيف هذه الخطوة؟** حتى عندما تحتاج فقط إلى صندوق أسود بسيط، فإن كشف قاموس الموارد يُشير إلى المحرك أنك *قد* تضيف محتوى إضافيًا لاحقًا. إنها نداء غير ضار يبقي الكود مرنًا لتوسعات مستقبلية.

### 5. تطبيق التمويه وحفظ PDF

استدعاء `Redact()` فعليًا يمحو المحتوى. ثم نقوم بحفظ الملف.

```csharp
        // Step 5: Apply the redaction and save the PDF
        pdfDocument.Redact();   // This processes all redaction annotations
        pdfDocument.Save("redacted.pdf");

        Console.WriteLine("Redacted PDF saved as redacted.pdf");
    }
}
```

**لماذا نستدعي `Redact()`؟** مجرد إضافة التعليقة لا يغيّر التيارات الأساسية. `Redact()` يمر عبر كل تعليقة، يزيل الكائنات المغطاة، ويضيف نصًا فوقيًا إذا لزم الأمر. تخطي هذه الخطوة سيترك البيانات الأصلية كما هي—مما يُفقد الهدف من **how to redact pdf**.

---

## مثال كامل يعمل

انسخ‑الصق القائمة الكاملة إلى `Program.cs` وشغّل `dotnet run`. ستظهر لك `redacted.pdf` في مجلد المشروع، مع استبدال السلسلة الحساسة بصندوق أسود مكتوب بداخله “REDACTED”.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Redactions;
using Aspose.Pdf.Text;   // For TextFragment
using Aspose.Pdf.Drawing; // For Color

class Program
{
    static void Main()
    {
        // Create a new PDF document in memory
        using var pdfDocument = new Document();

        // Add a page with sample text (so we can see the effect)
        var page = pdfDocument.Pages.Add();
        page.Paragraphs.Add(new TextFragment("Sensitive data: 123‑45‑6789"));

        // Define a redaction annotation covering the desired area
        var redactionRect = new Rectangle(100, 100, 300, 200);
        var redactionAnnotation = new RedactionAnnotation(redactionRect)
        {
            FillColor = Color.Black,
            OverlayText = "REDACTED"
        };
        pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);

        // (Optional) Access resources dictionary – useful for XObjects
        var resources = redactionAnnotation.Resources;

        // Apply redaction and save the PDF
        pdfDocument.Redact();
        pdfDocument.Save("redacted.pdf");

        Console.WriteLine("Redacted PDF saved as redacted.pdf");
    }
}
```

**النتيجة المتوقعة:** فتح `redacted.pdf` يُظهر صفحة واحدة حيث النص “Sensitive data: 123‑45‑6789” اختفى تمامًا، واستُبدل بمستطيل أسود صلب يحمل كلمة “REDACTED” في الوسط. لا توجد تدفقات مخفية متبقية، مما يفي بمتطلبات تدقيق الامتثال.

---

## الأسئلة المتكررة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تمويه عدة صفحات مرة واحدة؟** | نعم – فقط قم بالتكرار عبر `pdfDocument.Pages` وأضف `RedactionAnnotation` إلى مجموعة `Annotations` لكل صفحة. |
| **ماذا لو تداخلت منطقة التمويه مع صور موجودة؟** | محرك التمويه يزيل *جميع* الكائنات التي تتقاطع مع المستطيل، بما في ذلك الصور، المتجهات، والنص. |
| **هل يجب استدعاء `Redact()` بعد كل تعليقة جديدة؟** | لا. استدعِها مرة واحدة بعد إضافة *جميع* التعليقات التي تريد تطبيقها. |
| **كيف أحافظ على PDF الأصلي دون تعديل؟** | حمّل الملف المصدر إلى `Document`، استنسخه (`var clone = (Document)source.Clone();`)، طبّق التمويهات على النسخة، ثم احفظ النسخة. |
| **هل التمويه قابل للعكس؟** | لا. بمجرد تشغيل `Redact()`، يُحذف المحتوى الأصلي من تدفق PDF. احتفظ بنسخة احتياطية إذا قد تحتاج إلى النسخة غير المموهة لاحقًا. |

---

## مواضيع ذات صلة قد تستكشفها لاحقًا

- **Hide text pdf** باستخدام طبقات PDF (`OptionalContentGroup`) للتمويه القابل للعكس.  
- **Remove content pdf** بحذف صفحات أو كائنات محددة عبر نموذج كائن PDF منخفض المستوى.  
- **Create PDF document C#** مع جداول، صور، وتوقيعات رقمية.  
- **Redact area in PDF** باستخدام رسومات تغطية مخصصة (مثل شعار الشركة).  

كل هذه تبني على أساسيات `Aspose.Pdf` التي تعلمتها الآن، لذا سيسهل الانتقال بينها.

---

## الخلاصة

أصبحت الآن تمتلك حلًا جاهزًا للإنتاج حول **how to redact pdf** في C#. من خلال إنشاء `Document`، إضافة `RedactionAnnotation`، استدعاء `Redact()`، وحفظ الملف، يمكنك إخفاء نص PDF، إزالة محتوى PDF، وتمويه منطقة في PDF دون الحاجة إلى محررات طرف ثالث.  

جرّبه على ملفاتك الخاصة، جرب عدة مستطيلات، وربما أتمت العملية لسلاسل تمويه جماعية. إذا واجهت أي صعوبة، اترك تعليقًا أدناه – happy coding!

--- 

![how to redact pdf example](redaction-example.png){: .align-center alt="مثال على كيفية تمويه pdf"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}