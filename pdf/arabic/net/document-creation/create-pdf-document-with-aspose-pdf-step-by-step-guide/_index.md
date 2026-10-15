---
category: general
date: 2026-04-12
description: إنشاء مستند PDF باستخدام Aspose.Pdf في C#. تعلم كيفية إضافة صفحة إلى
  PDF، ورسم شكل، وحفظ ملف PDF بسرعة.
draft: false
keywords:
- create pdf document
- add page to pdf
- add graphics to pdf
- save pdf file
- draw shape in pdf
language: ar
og_description: إنشاء مستند PDF في C# باستخدام Aspose.Pdf. يوضح هذا الدليل كيفية إضافة
  صفحة إلى PDF، وإضافة رسومات إلى PDF، ورسم شكل في PDF، وحفظ ملف PDF.
og_title: إنشاء مستند PDF باستخدام Aspose.Pdf – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF Generation
title: إنشاء مستند PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة
url: /ar/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مستند PDF باستخدام Aspose.Pdf – دليل خطوة بخطوة

هل احتجت يومًا إلى **إنشاء مستند PDF** برمجيًا ولم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند أتمتة التقارير أو الفواتير أو الشهادات. الخبر السار هو أنه باستخدام Aspose.Pdf لـ .NET يمكنك إنشاء PDF، إضافة صفحة، رسم شكل، وحفظ الملف في بضع سطور فقط.

في هذا الدرس سنستعرض العملية بالكامل: **إضافة صفحة إلى PDF**، إضافة بعض سحر **إضافة رسومات إلى PDF**، **رسم شكل في PDF**، وأخيرًا **حفظ ملف PDF**. في النهاية ستحصل على مثال جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- .NET 6+ (أو .NET Framework 4.7.2+) – المكتبة تعمل مع كلاهما.
- حزمة NuGet Aspose.Pdf لـ .NET (`Aspose.Pdf`) – قم بتثبيتها عبر `dotnet add package Aspose.Pdf`.
- محرر شفرة أو بيئة تطوير متكاملة (Visual Studio، VS Code، Rider… أيًا كان).
- معرفة أساسية بـ C# – إذا كنت تعرف كيف تكتب دالة `Main`، فأنت جاهز.

لا تحتاج إلى أصول إضافية؛ الشكل الذي نرسمه معرف بسلسلة مسار بسيطة.

## الخطوة 1: إنشاء مستند PDF وإضافة صفحة

أول شيء عليك فعله هو إنشاء كائن PDF جديد. فكر في `Document` كقماشك؛ بدونها لا شيء لترسمه.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // Step 1 – initialize a new PDF document (this creates the file in memory)
        Document pdfDoc = new Document();

        // Step 2 – add a blank page where we’ll later place graphics
        Page page = pdfDoc.Pages.Add();

        // The rest of the steps follow...
```

> **لماذا هذا مهم:** إنشاء المستند أولاً يمنحك صفحة نظيفة، وإضافة صفحة فورًا يضمن حصولك على كائن `Page` صالح لإرفاق الرسومات به. تخطي خطوة إضافة الصفحة سيسبب استثناءً عندما تحاول رسم أي شيء.

## الخطوة 2: تعريف مساحة الرسم (حدود الرسومات)

قبل أن نرسم، نحتاج إلى إخبار Aspose بمكان وجود الشكل. الـ `Rectangle` الذي ننشئه يعمل كصندوق حد—نقطة أصله هي (0,0) وعرضه 500 × 500 نقطة.

```csharp
        // Step 3 – define a rectangle that will contain our graphics
        Rectangle graphicsRect = new Rectangle(0, 0, 500, 500);
```

> **نصيحة احترافية:** نظام الإحداثيات في ملفات PDF يبدأ من الزاوية السفلية اليسرى. إذا كنت تحتاج الشكل بالقرب من أعلى الصفحة، فقط عدل قيم `LLX`/`LLY` للمستطيل.

## الخطوة 3: بناء الشكل (كائن Path)

الآن يأتي الجزء الممتع—رسم الشكل. Aspose.Pdf يستخدم بيانات مسار على نمط SVG. المثال أدناه يرسم مربعًا بسيطًا، لكن يمكنك استبدال السلسلة بأي مسار صالح (دوائر، نجوم، شعارات مخصصة، إلخ).

```csharp
        // Step 4 – create a Path describing the shape (a square in this case)
        Path squarePath = new Path
        {
            // "M" = move to, "L" = line to, "Z" = close path
            // This draws a 500x500 square starting at (0,0)
            PathData = "M 0,0 L 500,0 L 500,500 L 0,500 Z"
        };
```

> **لماذا نستخدم `Path`**: يمنحك تحكمًا على مستوى المتجهات، مما يعني أن الشكل يبقى واضحًا عند أي مستوى تكبير—مثالي للشعارات أو المخططات.

## الخطوة 4: التحقق من أن الشكل يتناسب داخل الحدود

Aspose.Pdf يقدم أداة مساعدة `CheckGraphicsBoundary`. هي تؤكد أن الشكل لن يخرج خارج المستطيل الذي حددته. هذه الخطوة اختيارية لكنها تمنع المفاجآت عندما تقوم لاحقًا بدمج الـ PDF في أنظمة أخرى.

```csharp
        // Step 5 – make sure the shape fits within the rectangle
        bool fits = page.CheckGraphicsBoundary(squarePath, graphicsRect);
        if (!fits)
        {
            Console.WriteLine("The shape exceeds the defined graphics boundary.");
            return;
        }
```

> **ملاحظة حالة حافة:** إذا كنت تستخدم مسارات معقدة (مثلًا مع منحنيات)، فإن فحص الحدود يمكنه اكتشاف الفائض غير المرئي الذي قد يسبب قصًا.

## الخطوة 5: إضافة الشكل إلى الصفحة

الآن بعد أن علمنا أن الشكل يتناسب، يمكننا إضافته بأمان إلى الصفحة. طريقة `AddGraphics` تأخذ الشكل والمستطيل الذي يحدد موقعه.

```csharp
        // Step 6 – actually draw the shape onto the page
        page.AddGraphics(squarePath, graphicsRect);
```

> **ما يحدث خلف الكواليس:** Aspose يحول الـ `Path` إلى أوامر رسم PDF (`m`, `l`, `h`, `re`, إلخ) ويكتبها في تدفق محتوى الصفحة.

## الخطوة 6: حفظ ملف PDF

كل هذا العمل لا فائدة منه إذا لم تتمكن من رؤية النتيجة. طريقة `Save` تكتب المستند الموجود في الذاكرة إلى القرص. يمكنك أيضًا بثه مباشرة إلى `MemoryStream` للاستجابات الويب.

```csharp
        // Step 7 – persist the PDF to disk (or a stream)
        string outputPath = @"C:\Temp\ShapeDemo.pdf"; // adjust to your environment
        pdfDoc.Save(outputPath);
        Console.WriteLine($"PDF saved successfully to {outputPath}");
    }
}
```

> **نصيحة للسيناريوهات السحابية:** استبدل `pdfDoc.Save(outputPath)` بـ `pdfDoc.Save(stream)` حيث `stream` هو `MemoryStream`. ثم أعد مصفوفة البايتات من نقطة نهاية API.

### الناتج المتوقع

افتح `ShapeDemo.pdf` وسترى صفحة واحدة تحتوي على مربع مثالي يملأ مساحة 500 × 500 بدءًا من الزاوية السفلية اليسرى. لا هوامش إضافية، لا قطع مخفية.

![مخطط يوضح شكلًا مرسومًا في ملف PDF تم إنشاؤه باستخدام Aspose.Pdf](https://example.com/images/shape-in-pdf.png "مخطط يوضح شكلًا مرسومًا في ملف PDF تم إنشاؤه باستخدام Aspose.Pdf")

*(نص بديل: مخطط يوضح شكلًا مرسومًا في ملف PDF تم إنشاؤه باستخدام Aspose.Pdf)*

## الاختلافات الشائعة والمشكلات

| السيناريو | ما الذي يجب تغييره | السبب |
|----------|-------------------|-------|
| **شكل مختلف** | استبدل `PathData` بـ `"M 250,0 L 500,500 L 0,500 Z"` للحصول على مثلث. | سلاسل المسار تتبع صيغة SVG؛ تعديلها يغيّر الهندسة. |
| **أشكال متعددة** | استدعِ `page.AddGraphics` عدة مرات مع كائنات `Path` مختلفة. | كل استدعاء يضيف عنصرًا متجهيًا جديدًا، مما يسمح برسومات مركبة. |
| **تحديد موضع آخر** | غيّر `graphicsRect` إلى `new Rectangle(100, 200, 300, 300)`. | يُغيّر موقع مساحة الرسم؛ مفيد للرؤوس/التذييلات. |
| **الحفظ إلى تدفق** | `using var ms = new MemoryStream(); pdfDoc.Save(ms); var bytes = ms.ToArray();` | مطلوب لواجهات برمجة التطبيقات الويب أو عندما لا تريد ملفًا فعليًا. |
| **دقة DPI أعلى** | عيّن `pdfDoc.PageInfo.Dpi = 300;` قبل إضافة الرسومات. | يحسن جودة الصورة النقطية عندما يتم تحويل PDF لاحقًا إلى PNG/JPEG. |

## ملخص

لقد **أنشأنا مستند PDF**، **أضفنا صفحة إلى PDF**، **أضفنا رسومات إلى PDF** عبر تعريف مستطيل حد، **رسمنا شكلًا في PDF**، وأخيرًا **حفظنا ملف PDF** إلى القرص. تدفق كامل يندمج في طريقة `Main` مرتبة يمكنك نسخها ولصقها في أي تطبيق كونسول.

## ما التالي؟

- **إضافة نص**: استخدم `TextFragment` لتسمية أشكالك.
- **إدراج صور**: `Image image = new Image(); image.File = "logo.png"; page.Paragraphs.Add(image);`
- **تطبيق الألوان وأنماط الخط**: عيّن `squarePath.GraphInfo.Color = Color.FromRgb(255, 0, 0);`
- **إنشاء تقارير متعددة الصفحات**: كرّر عبر صفوف البيانات، أضف صفحة جديدة لكل سجل، وأعد استخدام نفس منطق الرسم.

لا تتردد في التجربة—استبدل المربع بشعار شركتك، غير الألوان، أو اجمع مسارات متعددة في رسم مركب واحد. واجهة برمجة Aspose.Pdf مرنة بما يكفي لأي شيء من الفواتير البسيطة إلى الكتب الإلكترونية الكاملة.

---

*برمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع وثائق Aspose.Pdf الرسمية لمزيد من التفاصيل.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}