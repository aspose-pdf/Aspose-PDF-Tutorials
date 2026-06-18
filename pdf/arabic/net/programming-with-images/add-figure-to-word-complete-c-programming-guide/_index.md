---
category: general
date: 2026-04-12
description: أضف الشكل إلى Word بسرعة باستخدام C#. تعلم كيفية وضع الشكل في Word، وإدراج
  الشكل في ملف docx، وإضافة XML مخصص لتخطيط متقدم.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: ar
og_description: أضف الشكل إلى Word بسرعة باستخدام C#. تعلم كيفية وضع الشكل في Word،
  وإدراج الشكل في ملف docx، وإضافة XML مخصص لتصميم متقدم.
og_title: إضافة شكل إلى Word – دليل برمجة C# الكامل
tags:
- C#
- Word Automation
- Document Generation
title: إضافة شكل إلى Word – دليل برمجة C# الكامل
url: /ar/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة شكل إلى Word – دليل برمجة C# الكامل

هل احتجت إلى **إضافة شكل إلى Word** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من مشاريع أتمتة المكتب القطعة المفقودة هي صورة أو مخطط موضعه بشكل جيد داخل جزء XML مخصص. يوضح هذا الدليل بالضبط كيفية **وضع الشكل في Word**، وإدراج الشكل في ملف *.docx*، وحتى تعديل XML المخصص الأساسي بحيث يتصرف الشكل كأي كائن Word أصلي.

سنستعرض مثالًا واقعيًا باستخدام مكتبة GemBox.Document (مجانية للملفات الصغيرة، تجارية للأحمال الأكبر). في النهاية ستحصل على برنامج مستقل قابل للتنفيذ يضع شكلًا عند الإحداثيات X = 50، Y = 200 داخل حاوية محتوى مُوسومة. لا اختصارات غامضة مثل “انظر الوثائق” — فقط شفرة واضحة، سبب عملها، ونصائح يمكنك نسخها مباشرة إلى مشروعك.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الشفرة تُجمّع أيضًا مع .NET Core 3.1)
- حزمة NuGet **GemBox.Document** (`Install-Package GemBox.Document`)
- ملف Word مبدئي (`input.docx`) يحتوي بالفعل على علامة XML مخصصة حيث تريد ظهور الشكل
- معرفة أساسية بـ C# (سترى لماذا كل سطر مهم)

> **نصيحة احترافية:** إذا لم يكن لديك مستند مُوسوم مسبقًا، يمكنك إنشاء واحد في Word عن طريق إدراج *Content Control* → *XML Mapping Pane* → ربط جزء XML مخصص. ستتعامل المكتبة مع ذلك التحكم كـ `TaggedContent`.

## الخطوة 1 – تحميل المستند المصدر

الخطوة الأولى هي فتح ملف *.docx* الموجود. `Document` هو نقطة الدخول لجميع عمليات GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*لماذا؟* تحميل الملف يمنحنا الوصول إلى أجزائه الداخلية، بما في ذلك أي حاويات XML مخصصة. بدون ذلك، لن نتمكن من تحديد عقدة `TaggedContent` التي ستحمل الشكل الخاص بنا.

## الخطوة 2 – الوصول إلى المحتوى المُوسوم (حاوية XML مخصصة)

يتم تخزين XML المخصص داخل *content control* في Word. تُظهره GemBox كـ `TaggedContent`.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

إذا كان المستند يحتوي على أقسام موسومة متعددة، فإن `TaggedContent` تُعيد **الأول** منها. يمكنك أيضًا تعداد `doc.TaggedContents` لاختيار علامة معينة بالاسم.

## الخطوة 3 – إنشاء عنصر الشكل

يمثل `FigureElement` صورة أو مخطط أو أي كائن بصري تعالجه Word كـ *shape*. سننشئه داخل الحاوية الموسومة.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*لماذا ننشئ الشكل هنا؟* بربطه بعقدة XML المخصصة، يعرف Word أن الشكل ينتمي إلى ذلك القسم المنطقي، وهو أمر حاسم لتعديلات لاحقة أو سير عمل يعتمد على محتوى التحكم.

## الخطوة 4 – تحديد موقع الشكل بدقة

يستخدم Word النقاط (1 pt ≈ 1/72 in) لتحديد المواقع. يتيح لنا هيكل `PointF` ضبط إحداثيات X/Y بسهولة.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **كيفية تحديد موقع الشكل في Word:** خاصية `Position` تقبل كائن `PointF` حيث القيمة الأولى هي الإزاحة الأفقية (اليسار) والثانية هي الإزاحة العمودية (الأعلى) نسبة إلى هوامش الصفحة. عدّل هذه القيم لضبط الموضع بدقة.

## الخطوة 5 – إدراج الشكل في شجرة المحتوى المُوسوم

الآن نرفق الشكل بالعنصر الجذري لشجرة XML المخصصة. هذا يضيف الشكل فعليًا إلى مستند Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

في هذه المرحلة يعيش الشكل داخل المستند، لكنه لا يملك مصدر صورة بعد. لنضيف ملف PNG بسيط من القرص.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## الخطوة 6 – حفظ المستند المعدل

أخيرًا، نكتب التغييرات إلى ملف *.docx* جديد.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

عند فتح `output.docx` في Word، سترى الصورة موضوعة بالضبط عند (50, 200) داخل كتلة XML المخصصة التي استهدفتها.

### مثال كامل يعمل

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**النتيجة المتوقعة:** فتح `output.docx` يُظهر PNG موضوعًا تمامًا حيث حددت، ومُدمجًا داخل جزء XML المخصص. إذا فحصت XML للمستند (`.docx` → فك ضغط → `word/document.xml`)، ستجد عنصر `<w:pict>` مع إحداثيات `<v:shape>` الصحيحة.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان للمستند أقسام موسومة متعددة؟

استخدم `doc.TaggedContents` لتعداد واختيار حسب اسم العلامة:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### كيف أضيف تسمية توضيحية للشكل؟

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### هل يعمل هذا مع Word 2010 وما بعده؟

نعم. تستهدف GemBox.Document معيار Open XML، المتوافق مع Word 2007 + (بما في ذلك 2010، 2013، 2016، 2019، وMicrosoft 365).

### ماذا لو احتجت إلى تدوير الشكل؟

```csharp
figure.Rotation = 45; // degrees
```

### كيف أضيف رسمًا متجهيًا بدلاً من صورة نقطية؟

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## نصائح احترافية ومخاطر محتملة

- **مسارات الملفات:** استخدم `Path.Combine` لتجنب الفواصل الصلبة، خاصة على الأنظمة غير Windows.
- **حدود الترخيص:** الترخيص المجاني لـ GemBox يحد حجم المستند إلى 20 KB. للملفات الأكبر، اشترِ مفتاحًا تجاريًا.
- **الأداء:** إعادة استخدام كائن `Document` واحد للمعالجة الدفعية يقلل من استهلاك الذاكرة بشكل كبير.
- **تجاوز الشكل:** إذا تجاوز أبعاد الشكل هوامش الصفحة، سيقوم Word بقصه. اضبط `figure.Width` و `figure.Height` وفقًا لذلك.

## الخلاصة

أنت الآن تعرف **كيفية إضافة شكل إلى Word**، و**تحديد موقع الشكل في Word** بدقة، وتعديل XML المخصص الأساسي لجعل الشكل يتصرف كأي عنصر أصلي. يُظهر المثال الكامل القابل للتنفيذ كل خطوة — من تحميل المستند، إنشاء `FigureElement`، ضبط إحداثياته، إرفاق صورة، وأخيرًا حفظ ملف *.docx* المحدث.

بعد ذلك، جرّب تجربة **إدراج شكل في docx** بإضافة أشكال متعددة، باستخدام الحلقات، أو توليد مخططات في الوقت الفعلي. يمكنك أيضًا استكشاف **كيفية إضافة XML مخصص** للتحكمات المحتوى الأكثر غنى أو تعلم **كيفية تحديد موقع الشكل في Word** داخل الجداول والرؤوس. الاحتمالات لا حصر لها، ومع الأساسيات التي غطيناها الآن، أنت جاهز لأتمتة مستندات Word كالمحترفين.

برمجة سعيدة، ولا تتردد في ترك تعليق إذا واجهت أي صعوبات!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}