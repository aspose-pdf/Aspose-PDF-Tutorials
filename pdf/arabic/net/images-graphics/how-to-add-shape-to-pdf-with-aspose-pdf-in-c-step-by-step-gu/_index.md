---
category: general
date: 2026-06-18
description: كيفية إضافة شكل إلى ملف PDF باستخدام Aspose.PDF في C# – تحميل ملف PDF،
  رسم مستطيل، وحفظه.
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: ar
og_description: كيفية إضافة شكل إلى ملف PDF باستخدام Aspose.PDF في C#. تعلم كيفية
  تحميل مستند PDF، رسم مستطيل، وحفظ الملف المحدث.
og_title: كيفية إضافة شكل إلى PDF باستخدام Aspose.PDF في C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: كيفية إضافة شكل إلى ملف PDF باستخدام Aspose.PDF في C# – دليل خطوة بخطوة
url: /ar/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة شكل إلى PDF باستخدام Aspose.PDF في C# – دليل كامل

هل تساءلت يومًا **كيفية إضافة شكل إلى PDF** دون التعامل مع تدفقات البايت منخفضة المستوى؟ في العديد من التطبيقات الواقعية تحتاج إلى تمييز منطقة، تسطير فقرة، أو ببساطة رسم مربع حدود لحقل التوقيع. الخبر السار هو أن Aspose.PDF يجعل ذلك سهلًا. في هذا الدليل سنقوم بتحميل مستند PDF في C#، رسم مستطيل، وحفظ النتيجة—لا أكثر ولا أقل.

سنستعرض كل سطر من الشيفرة، نشرح *لماذا* كل جزء مهم، ونظهر لك طريقة سريعة للتحقق من أن الشكل تم وضعه فعلاً في المكان المتوقع. بنهاية الدليل ستتمكن من **كيفية رسم الأشكال في ملفات PDF**، وستحصل على مقتطف يمكن إعادة استخدامه في أي مشروع .NET.

## المتطلبات المسبقة

- **.NET 6.0** (أو أي نسخة .NET حديثة) مثبتة على جهازك.  
- **رخصة Aspose.PDF for .NET صالحة** (أو مفتاح تقييم مجاني).  
- Visual Studio 2022، Rider، أو أي محرر تفضله.  
- ملف PDF موجود مسبقًا (`input.pdf`) موجود في مجلد يمكنك الإشارة إليه.

> **نصيحة احترافية:** إذا كنت تقوم بالاختبار فقط، فإن نسخة التقييم المجانية مناسبة تمامًا—تضيف علامة مائية صغيرة ولكنها تعمل كالنظام الكامل.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولاً، أنشئ مشروع وحدة تحكم جديد (أو أضف إلى مشروع موجود) واستورد المساحات الاسمية الضرورية.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

لماذا هذا مهم: `Aspose.Pdf` يوفر لك نموذج المستند الأساسي، بينما `Aspose.Pdf.Drawing` يحتوي على فئة الشكل `Rectangle` التي سنستخدمها لاحقًا. بدون الأخيرة سيظهر خطأ في المترجم بأن `Rectangle` غير معرف.

## الخطوة 2: تحميل مستند PDF في C#

الآن نقوم فعليًا **بتحميل مستند PDF في C#**. هذه هي العملية الأولى التي تقوم بها دائمًا عندما تنوي تعديل ملف موجود.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*شرح*:  
- `Document` هو تمثيل Aspose للملف بالكامل.  
- تمرير المسار الكامل إلى المُنشئ يقرأ الملف إلى الذاكرة.  
- سطر `Console.WriteLine` اختياري لكنه مفيد للتصحيح—إذا كان عدد الصفحات صفرًا فإنك تعرف أن هناك خطأ حدث مبكرًا.

## الخطوة 3: تعريف شكل المستطيل

هنا نصل إلى جوهر **كيفية إضافة شكل إلى PDF**. نقوم بإنشاء كائن `Rectangle` يحدد موقعه وحجمه باستخدام نظام الإحداثيات حيث (0,0) هو الزاوية السفلية اليسرى للصفحة.

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

لماذا نضبط `FillColor` على شفاف: معظم الحالات تحتاج فقط إلى حدود (مثل صندوق تمييز). خاصية `Border` تسمح لك بالتحكم في السماكة واللون؛ اللون الأحمر يجعل المستطيل بارزًا على صفحة بيضاء عادية.

## الخطوة 4: التحقق من أن الشكل يندرج داخل حدود الصفحة

قبل أن **نضيف المستطيل**، من العادة الجيدة التأكد من أن الشكل لا يتجاوز حدود الصفحة. توفر Aspose الدالة `ValidateShapeBounds` لهذا الغرض بالضبط.

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*السبب*: محاولة الرسم خارج الصفحة قد تتسبب في تشوهات في العرض أو حتى رمي استثناء. هذا الفحص يجعل الدليل قويًا لأي حجم PDF.

## الخطوة 5: إضافة المستطيل إلى الصفحة المطلوبة

الآن نضيف أخيرًا **الشكل إلى PDF**. طريقة `AddRectangle` تُرفق الشكل بمجموعة التعليقات التوضيحية للصفحة، مما يعني أن عارضات PDF ستعرضه كأي رسم آخر.

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

إذا كنت بحاجة إلى استهداف صفحة مختلفة، استبدل الفهرس `1` برقم الصفحة المناسب (Aspose يستخدم الفهرسة بدءًا من 1).

## الخطوة 6: حفظ ملف PDF المعدل

الخطوة الأخيرة هي كتابة التغييرات إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد—هنا سننشئ `output.pdf`.

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*ما المتوقع*: افتح `output.pdf` في Adobe Reader أو أي عارض وسترى مستطيلًا أحمر واضحًا مثبتًا في الزاوية السفلية اليسرى للصفحة الأولى.

![مخطط يوضح إضافة مستطيل إلى PDF](https://example.com/rectangle-diagram.png "مثال على كيفية إضافة شكل إلى PDF")

*نص بديل*: "كيفية إضافة شكل إلى PDF – مستطيل مرسوم على الصفحة الأولى من ملف PDF"

## الخطوة 7: مثال كامل جاهز للنسخ واللصق

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله فورًا. تذكر استبدال `YOUR_DIRECTORY` بمسار المجلد الفعلي على جهازك.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

شغّل البرنامج، افتح `output.pdf`، وسترى المستطيل الأحمر بالضبط حيث وضعناه. إذا كنت تحتاج إلى شكل مختلف—إهليلج، خط، أو مضلع—فقط استبدل `Rectangle` بـ `Ellipse` أو `Line` أو `Polygon` مع الحفاظ على نفس سير العمل. هذا هو أساس **كيفية رسم الأشكال في PDF** باستخدام Aspose.

## أسئلة شائعة وحالات حافة

### ماذا لو احتجت للرسم على صفحات متعددة؟

ببساطة قم بالتكرار على `pdfDoc.Pages` واستدعِ `AddRectangle` (أو أي شكل آخر) لكل صفحة. تذكر تعديل الإحداثيات إذا كانت الصفحات بأحجام مختلفة.

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### هل يمكن ملء المستطيل بلون؟

بالطبع. غيّر `FillColor` من `Transparent` إلى أي `Color` تريدها، مثلًا `Color.Yellow`. سيظهر الشكل ككتلة صلبة.

### هل يعمل هذا مع ملفات PDF محمية بكلمة مرور؟

يمكن لـ Aspose.PDF فتح الملفات المشفرة إذا زودتها بكلمة المرور:

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### كيف تضيف مستطيل بزوايا مستديرة؟

استخدم الفئة `RoundedRectangle` بدلاً من `Rectangle`. باقي الخطوات تبقى كما هي.

## ملخص

لقد غطينا **كيفية إضافة شكل إلى PDF** باستخدام Aspose.PDF في C#. العملية اختصرت إلى:

1. **تحميل مستند PDF في C#** – إنشاء كائن `Document`.  
2. **تعريف مستطيل** (أو أي شكل آخر).  
3. **التحقق من الحدود** لتجنب التجاوز.  
4. **إضافة المستطيل** إلى الصفحة المستهدفة.  
5. **حفظ** الملف المعدل.

هذا هو سير العمل الكامل لـ **aspose pdf add rectangle**، والآن لديك قالب يمكنك تعديله للدوائر أو الخطوط أو المضلعات المخصصة.

## ما التالي؟

- **استكشاف بدائل الرسم الأخرى**: `Ellipse`، `Line`، `Polygon`.  
- **إضافة تعليقات نصية** بجانب أشكالك لمزيد من التفاعل.  
- **دمج مع حقول نماذج PDF** إذا كنت تبني عقدًا قابلًا للملء.  
- **الاطلاع على ميزات تحويل PDF من Aspose** لتحويل ملفات PDF المعلّقة إلى صور لمعاينات المصغرات.

لا تتردد في التجربة—ربما ترسم علامة مائية، تمييز خلية جدول، أو تحديد حقل توقيع. الـ API مرن، والآن تعرف الأساسيات.

برمجة سعيدة، ولتظهر ملفات PDF دائمًا كما تريد!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مستند PDF باستخدام Aspose.PDF – إضافة صفحة، شكل وحفظ](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [كيفية إضافة وتخصيص أرقام الصفحات في ملفات PDF باستخدام Aspose.PDF لـ .NET | دليل تعديل المستندات](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [كيفية إضافة روابط تشعبية في ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل شامل](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}