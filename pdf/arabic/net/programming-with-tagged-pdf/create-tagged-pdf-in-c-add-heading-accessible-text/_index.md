---
category: general
date: 2026-01-15
description: إنشاء ملف PDF مُوسَّم باستخدام Aspose.Pdf في C#. تعلّم كيفية إضافة عنوان
  إلى ملف PDF، وتعيين نص قابل للوصول، وإضافة صفحة إلى ملف PDF في دليل خطوة بخطوة.
draft: false
keywords:
- create tagged pdf
- add heading to pdf
- how to add heading
- add page to pdf
- set accessible text
language: ar
og_description: إنشاء ملف PDF مع علامات باستخدام Aspose.Pdf في C#. يوضح هذا الدليل
  كيفية إضافة عنوان إلى PDF، وتعيين نص قابل للوصول، وإضافة صفحة إلى PDF.
og_title: إنشاء ملف PDF مُوسَّم في C# – إضافة عنوان ونص قابل للوصول
tags:
- Aspose.Pdf
- C#
- PDF accessibility
title: إنشاء PDF مُوسوم في C# – إضافة عنوان ونص قابل للوصول
url: /ar/net/programming-with-tagged-pdf/create-tagged-pdf-in-c-add-heading-accessible-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF مع علامات في C# – إضافة عنوان ونص قابل للوصول

هل احتجت يومًا إلى **إنشاء PDF مع علامات** لكن لم تكن متأكدًا من أين تبدأ؟ في هذا الدرس سنستعرض الخطوات الدقيقة لإضافة عنوان إلى PDF، ضبط نص قابل للوصول، وحتى إضافة صفحة جديدة إلى PDF — كل ذلك باستخدام Aspose.Pdf لـ .NET.  

إذا تساءلت يومًا *كيف تضيف عنوانًا* يمكن لبرامج قراءة الشاشة فهمه، فأنت في المكان الصحيح. في النهاية ستحصل على PDF مع علامات بالكامل، قابل للوصول يمكنك تسليمه للعملاء الباحثين عن الامتثال أو المدققين الداخليين.

## ما ستتعلمه

- كيفية **إنشاء PDF مع علامات** من الصفر باستخدام Aspose.Pdf  
- الكود الدقيق لـ **إضافة عنوان إلى pdf** وتضمين فقرة تحته  
- طرق **ضبط نص قابل للوصول** بحيث تقرأ التقنيات المساعدة المحتوى الصحيح  
- نصيحة سريعة لـ **إضافة صفحة إلى pdf** عندما تحتاج إلى مساحة إضافية  
- أخطاء الممارسات الأفضل التي يجب تجنبها (وبعض النصائح الاحترافية)

> **المتطلبات المسبقة:** .NET 6+ (أو .NET Framework 4.6+) ورخصة Aspose.Pdf صالحة أو ملف DLL تجريبي. لا توجد مكتبات أخرى مطلوبة.

![Create tagged PDF example](image.png "Screenshot showing a tagged PDF with heading and paragraph – create tagged pdf")

## إنشاء PDF مع علامات – نظرة عامة

قبل أن نتعمق في الخطوات الفردية، دعنا نفهم الصورة الكبيرة. **PDF مع علامات** يحتوي على شجرة بنية منطقية تصف ترتيب القراءة والدلالات (العناوين، الفقرات، الجداول، إلخ). هذه الشجرة هي ما تستخدمه برامج قراءة الشاشة لنقل المعنى للمستخدمين ذوي الإعاقات البصرية.  

Aspose.Pdf يتيح كائن `TaggedContent` الذي يسمح لك ببناء تلك الشجرة برمجياً. فكر فيه كطقم LEGO: تنشئ قطعًا (عنوان، فقرة) وتربطها معًا بالترتيب الصحيح.

### مثال عملي كامل (جميع الخطوات مجمعة)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

namespace TaggedPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a page (add page to pdf)
            Document pdfDocument = new Document();
            Page pdfPage = pdfDocument.Pages.Add();

            // 2️⃣ Access the tagged content and create a level‑1 heading (add heading to pdf)
            TaggedContent taggedContent = pdfDocument.TaggedContent;
            HeadingElement heading = taggedContent.CreateHeadingElement(1);
            heading.Position = new Position { X = 50, Y = 750 }; // coordinates in points

            // 3️⃣ Create a paragraph and set its accessible text (set accessible text)
            ParagraphElement paragraph = taggedContent.CreateParagraphElement();
            paragraph.Text = "This is an accessible paragraph.";

            // 4️⃣ Build the hierarchy – heading contains the paragraph
            heading.AppendChild(paragraph);
            taggedContent.RootElement.AppendChild(heading);

            // 5️⃣ Save the tagged PDF to disk
            pdfDocument.Save("tagged_out.pdf");
        }
    }
}
```

شغّل البرنامج وافتح `tagged_out.pdf` في قارئ PDF يُظهر العلامات (مثال: Adobe Acrobat → View → Show/Hide → Navigation Panes → Tags). يجب أن ترى **Heading 1** متبوعًا بفقرة — بالضبط ما قصدنا.  

فيما يلي نقسم كل خطوة، نشرح *لماذا* هي مهمة، ونضيف بعض الخيارات الإضافية.

## إضافة صفحة إلى PDF

حتى المستند ذو الصفحة الواحدة يمكن أن يُوسم، لكن معظم ملفات PDF الواقعية تحتاج مساحة أكبر. إضافة صفحة أمر سهل:

```csharp
// Add a new page – this is the “add page to pdf” step
Page newPage = pdfDocument.Pages.Add();
```

> **لماذا إضافة صفحة؟**  
> العلامات تُرفق بإحداثيات صفحة محددة. إذا حاولت وضع عنوان عند إحداثيات Y تتجاوز ارتفاع الصفحة، سيُقطع النص. إضافة صفحة جديدة يمنحك لوحة نظيفة ويضمن بقاء التخطيط متسقًا.

**نصيحة احترافية:** إذا كنت بحاجة إلى صفحة أفقية، اضبط `newPage.PageInfo.Orientation = PageOrientation.Landscape;` قبل وضع العناصر.

## إضافة عنوان إلى PDF

العناوين توفر بنية. في الكود أعلاه استخدمنا `CreateHeadingElement(1)` لإنشاء عنوان **Level‑1**. يمكنك إنشاء مستويات أعمق (2، 3، …) للأقسام الفرعية.

```csharp
HeadingElement heading = taggedContent.CreateHeadingElement(1);
heading.Position = new Position { X = 50, Y = 750 };
```

- **X** و **Y** تُقاس بالنقاط (1 pt = 1/72 in).  
- ضبط `Y` لتحريك العنوان للأعلى أو الأسفل؛ القيم الأقل تدفعه نحو أسفل الصفحة.

> **خطأ شائع:** نسيان ضبط `heading.Position`. بدون إحداثيات يبقى العنوان في شجرة العلامات لكنه لا يظهر على الصفحة، مما يربك برامج قراءة الشاشة.

إذا كنت بحاجة إلى نمط غامق، يمكنك إرفاق `TextState`:

```csharp
heading.TextState = new TextState { FontSize = 18, FontStyle = FontStyles.Bold };
```

## ضبط نص قابل للوصول للفقرة

الفقرات تحمل الجزء الأكبر من المحتوى. لجعلها قابلة للقراءة بواسطة التقنيات المساعدة، يجب توفير *نص قابل للوصول*:

```csharp
ParagraphElement paragraph = taggedContent.CreateParagraphElement();
paragraph.Text = "This is an accessible paragraph.";
```

خاصية `Text` هي ما سيعلن عنه قارئ الشاشة. يمكنك أيضًا تضمين أحرف Unicode، رموز إيموجي، أو حتى نصوص من اليمين إلى اليسار — Aspose.Pdf يتعامل معها بسلاسة.  

**حالة خاصة:** إذا كنت بحاجة إلى فقرة تحتوي على رابط تشعبي، استخدم `LinkElement` داخل الفقرة واضبط خاصية `Alt` لتوفير تسمية وصفية.

## حفظ PDF مع علامات

```csharp
pdfDocument.Save("tagged_out.pdf");
```

يمكنك أيضًا بث الـ PDF مباشرةً إلى استجابة ويب:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    pdfDocument.Save(ms);
    // return File(ms.ToArray(), "application/pdf", "report.pdf");
}
```

> **لماذا لا تستخدم `pdfDocument.Save("output.pdf")` فقط؟**  
> لأن عندما تنوي تقديم ملفات PDF عبر HTTP، يتيح البث تجنب كتابة ملفات مؤقتة على القرص وتقليل عبء الإدخال/الإخراج.

## التحقق من بنية العلامات (اختياري لكن موصى به)

بعد إنشاء الملف، افتحه في Adobe Acrobat:

1. **View → Show/Hide → Navigation Panes → Tags**  
2. قم بتوسيع الشجرة؛ يجب أن ترى `H1` (العنوان الخاص بك) مع عنصر فرعي `P` (الفقرة).  

إذا كان التسلسل الهرمي يبدو صحيحًا، فقد نجحت في **إنشاء PDF مع علامات** يفي بمتطلبات WCAG 2.1 AA لإتاحة المستندات.

## الأخطاء الشائعة والنصائح الاحترافية

| المشكلة | كيفية التجنب |
|---------|--------------|
| نسيان استدعاء `AppendChild` على العنصر الجذر | دائمًا انتهِ بـ `taggedContent.RootElement.AppendChild(heading);` |
| استخدام إحداثيات خارج حدود الصفحة | استخدم `pdfPage.PageInfo.Width/Height` لحساب النطاقات الآمنة |
| عدم ضبط `TextState` للقراءة | حدد حجم خط افتراضي (12‑14 pt) وتباين كافٍ |
| الإفراط في الوسم (إضافة عناصر غير ضرورية) | التزم بالوسوم الدلالية: heading, paragraph, list, table |
| تجاهل بيانات اللغة الوصفية | اضبط `pdfDocument.Language = "en-US";` لتحسين اكتشاف قارئ الشاشة |

## الخطوات التالية

- **إضافة المزيد من أنواع المحتوى:** جداول (`TableElement`)، صور (`ImageElement`)، وقوائم (`ListElement`).  
- **التعريب:** غيّر `pdfDocument.Language` وقدم نصًا Unicode.  
- **التوقيعات الرقمية:** احمِ PDF مع العلامات باستخدام `SignatureField`.  

كل هذه تبني على الأساس الذي لديك الآن لإنشاء ملفات **PDF مع علامات** تكون قابلة للقراءة آليًا وإنسانيًا.

---

### ملخص

أنت الآن تعرف كيف **إنشاء PDF مع علامات** باستخدام Aspose.Pdf، **إضافة عنوان إلى pdf**، **ضبط نص قابل للوصول**، و**إضافة صفحة إلى pdf** عند الحاجة. المثال الكامل القابل للتنفيذ أعلاه جاهز للإدراج في أي مشروع .NET. جرّب مستويات عناوين مختلفة، خطوط، وعلامات إضافية — PDF القابل للوصول التالي لك على بعد بضع أسطر فقط. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}