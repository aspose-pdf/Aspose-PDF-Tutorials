---
category: general
date: 2026-02-20
description: أنشئ رابط PDF بسرعة ودمج رابط PDF باستخدام C#. تعلّم كيفية ربط صفحة PDF
  محددة وتحويل DOCX إلى رابط PDF في دقائق.
draft: false
keywords:
- create pdf hyperlink
- link specific pdf page
- embed link pdf
- create clickable pdf link
- convert docx pdf link
language: ar
og_description: أنشئ رابط PDF فورًا. يوضح هذا الدليل كيفية ربط صفحة PDF محددة، وتضمين
  رابط PDF، وتحويل DOCX إلى رابط PDF باستخدام C#.
og_title: إنشاء ارتباط تشعبي لملف PDF في C# – دليل كامل
tags:
- C#
- PDF
- Aspose
title: إنشاء ارتباط تشعبي لملف PDF في C# – دليل خطوة بخطوة
url: /ar/net/programming-with-links-and-actions/create-pdf-hyperlink-in-c-step-by-step-guide/
---

– keep as is.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ارتباط PDF في C# – دليل خطوة بخطوة

هل احتجت يوماً إلى **إنشاء ارتباط PDF** لكن لم تكن متأكدًا من أي استدعاء API يجعل الرابط يعمل فعليًا؟ لست وحدك—معظم المطورين يواجهون نفس المشكلة عند تحويل DOCX إلى PDF ينتقل مباشرة إلى صفحة معينة. الخبر السار؟ ببضع أسطر من C# يمكنك تضمين رابط، توجيهه إلى أي صفحة، وإصدار PDF مصقول في وقت قصير.

في هذا الدرس سنستعرض تحويل مستند Word إلى PDF **و** إضافة منطقة قابلة للنقر ترتبط بصفحة PDF محددة. سنتطرق أيضًا إلى كيفية **تضمين رابط PDF** في سير عمل آخر ولماذا قد ترغب في **ربط صفحة PDF محددة** بدلاً من إرفاق ملف فقط. بنهاية الدرس ستحصل على مقتطف جاهز للتنفيذ يمكنك وضعه في أي مشروع .NET.

## ما ستتعلمه

- تحميل ملف DOCX وتحويله إلى PDF باستخدام Aspose.Words (أو أي مكتبة متوافقة).  
- إنشاء **تعليق توضيحي قابل للنقر في PDF** يشير إلى صفحة الهدف.  
- تعريف منطقة المستطيل التي ينقر عليها المستخدم فعليًا.  
- حفظ PDF النهائي والتحقق من عمل الارتباط.  
- الأخطاء الشائعة عند **تحويل docx إلى pdf مع رابط** وكيفية تجنّبها.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+).  
- حزم NuGet الخاصة بـ Aspose.Words و Aspose.Pdf مثبتة (`dotnet add package Aspose.Words` و `dotnet add package Aspose.Pdf`).  
- ملف DOCX بسيط اسمه `input.docx` موجود في مجلد تتحكم فيه.  

لا حاجة لإعدادات معقدة—فقط بعض عبارات using وستكون جاهزًا.

![مثال على إنشاء ارتباط PDF](image.png "إنشاء ارتباط PDF")

## نظرة عامة على إنشاء ارتباط PDF

الفكرة الأساسية وراء عملية **إنشاء ارتباط PDF** مزدوجة:

1. **التعليق التوضيحي** – يستخدم PDF *تعليقات الروابط* لتحديد منطقة قابلة للنقر.  
2. **الوجهة** – يشير التعليق إلى كائن *الوجهة*، والذي يمكن أن يكون رقم صفحة، عرض مسمى، أو URL خارجي.

عند دمج هذين العنصرين تحصل على رابط يعمل تمامًا كما هو الحال في Adobe Reader. يتبع الكود أدناه هذا النمط بدقة.

## الخطوة 1: تحميل ملف DOCX المصدر

أولاً، نحتاج إلى جلب مستند Word إلى الذاكرة. تتولى Aspose.Words عملية تحويل DOCX إلى PDF خلف الكواليس.

```csharp
using Aspose.Words;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source DOCX file
Document docx = new Document("YOUR_DIRECTORY/input.docx");

// Convert the Word document to a PDF object (in memory)
using var pdfStream = new MemoryStream();
docx.Save(pdfStream, SaveFormat.Pdf);
pdfStream.Position = 0;

// Create an Aspose.Pdf Document from the memory stream
Document pdfDoc = new Document(pdfStream);
```

*لماذا هذه الخطوة؟*  
تحميل الـ DOCX باستخدام `Aspose.Words.Document` يضمن بقاء جميع الأنماط، الصور، وفواصل الصفحات بعد التحويل. بحفظه إلى `MemoryStream` نتجنب إنشاء ملف وسيط على القرص—ما يمنح أداءً أفضل وسير عمل أنظف عندما تقوم لاحقًا **بتضمين رابط pdf** في خدمات أخرى.

## الخطوة 2: إنشاء تعليق توضيحي للارتباط

الآن بعد أن لدينا كائن PDF، يمكننا إضافة تعليق توضيحي للارتباط. فكر فيه كملصق يخبّئ للمشاهد "انقر هنا".

```csharp
// Create a new link annotation object
LinkAnnotation link = pdfDoc.Pages[1].Annotations.AddLink(
    new Rectangle(0, 0, 0, 0)); // Temporary rectangle; we'll set proper coordinates next
```

*لماذا نستخدم `AddLink`؟*  
`AddLink` يسجل التعليق تلقائيًا في مجموعة تعليقات الصفحة، وهو أمر أساسي لكي يتعرف عارض PDF على المنطقة القابلة للنقر. يمكنك أيضًا إنشاء `LinkAnnotation` يدويًا، لكن الطريقة المساعدة تجعل الكود أكثر اختصارًا.

## الخطوة 3: تعريف المستطيل القابل للنقر

المستطيل يحدد المكان على الصفحة الذي يمكن للمستخدم النقر فيه. تُقاس إحداثيات PDF بالنقاط (1/72 بوصة)، مع الأصل في الزاوية السفلية اليسرى.

```csharp
// Define the rectangle (left, bottom, right, top) in points
// Here we place the link near the top of the page, spanning 150 points wide
link.Rect = new Rectangle(50, 700, 200, 720);
```

*لماذا هذه القيم؟*  
القيم `50, 700, 200, 720` تُنشئ صندوقًا عرضه 150 نقطة وارتفاعه 20 نقطة، موضعه تقريبًا بوصة واحدة من الحافة اليسرى وقريبًا من أعلى صفحة Letter القياسية. عدّل الإحداثيات لتتناسب مع تخطيطك—إذا وضعت الرابط تحت عنوان، ربما تحتاج قيمة `bottom` أصغر.

## الخطوة 4: تعيين صفحة الوجهة (ربط صفحة PDF محددة)

نريد أن ينتقل الرابط إلى الصفحة 2 (الفهرس صفر‑مبني 1) داخل نفس ملف PDF. هذا هو سيناريو **ربط صفحة PDF محددة** الكلاسيكي.

```csharp
// Destination page index is zero‑based; 1 points to the second page
Destination dest = new Destination(1);

// Assign the destination to the annotation
link.Destination = dest;

// Optional: Change the appearance to look like a typical hyperlink (blue, underlined)
link.Color = Color.Blue;
link.Border = new Border(link) { Width = 0 };
```

*لماذا كائن `Destination`؟*  
يدعم PDF أنواعًا متعددة من الوجهات (ملء الصفحة، تكبير، إلخ). باستخدام المُنشئ البسيط مع فهرس الصفحة نحصل على سلوك “ملء الصفحة” الافتراضي، وهو ما يتوقعه معظم المستخدمين عند النقر على رابط.

## الخطوة 5: حفظ PDF المعدل

أخيرًا، نكتب ملف PDF المحدث إلى القرص. الآن يحتوي الملف الناتج على **تعليق توضيحي قابل للنقر في PDF** ينتقل إلى الصفحة الثانية.

```csharp
// Save the PDF with the new hyperlink
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

هذا كل شيء—PDF جاهز، والرابط يعمل في أي عارض قياسي.

## اختبار الارتباط

افتح `output.pdf` في Adobe Reader أو أي عارض PDF حديث. مرّر المؤشر فوق المستطيل الأزرق؛ يجب أن يتحول إلى يد. النقر سيقلب الصفحة فورًا إلى الصفحة 2. إذا لم يحدث شيء، تحقق مرة أخرى من إحداثيات المستطيل وتأكد من أن فهرس الوجهة يطابق صفحة موجودة.

## الأخطاء الشائعة وكيفية تجنّبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| الرابط لا يعمل | فهرس صفحة الوجهة خارج النطاق | تحقق من `pdfDoc.Pages.Count` واستخدم فهرسًا صالحًا (صفر‑مبني). |
| المستطيل يظهر في الموضع الخطأ | ارتباك في نظام إحداثيات PDF (الأصل أسفل‑يسار) | تذكّر أن Y = 0 هو أسفل الصفحة؛ زد قيمة Y للتحرك للأعلى. |
| لون الرابط غير مرئي | لون التعليق غير محدد أو العارض يتجاهله | عيّن صراحةً `link.Color = Color.Blue` و `link.Border.Width = 0`. |
| حجم PDF يزداد كثيرًا | حفظ PDF وسيط على القرص قبل إضافة التعليق | استخدم `MemoryStream` كما هو موضح للحفاظ على العملية في الذاكرة. |

## حالات خاصة وتنوعات

### ربط URL خارجي

إذا احتجت إلى **تضمين رابط PDF** يشير إلى خارج المستند، استبدل تعيين `Destination` بـ `LinkAction`:

```csharp
link.Action = new LinkAction("https://example.com");
```

### إضافة روابط متعددة على صفحات مختلفة

استخدم حلقة تمر عبر الصفحات وتُنشئ `LinkAnnotation` جديد لكل منها. تذكّر تعديل إحداثيات المستطيل لتتناسب مع تخطيط كل صفحة.

```csharp
for (int i = 1; i <= pdfDoc.Pages.Count; i++)
{
    var page = pdfDoc.Pages[i];
    var link = page.Annotations.AddLink(new Rectangle(50, 50, 150, 70));
    link.Destination = new Destination(i - 1); // Jump to the same page (self‑link)
}
```

### استخدام الوجهات المسماة

بدلاً من الفهرس الرقمي يمكنك إنشاء وجهة مسماة، وهو مفيد عندما قد يتغير ترتيب الصفحات لاحقًا.

```csharp
pdfDoc.NamedDestinations.Add("ChapterTwo", new Destination(1));
link.Destination = new Destination("ChapterTwo");
```

## الخطوات التالية – تضمين رابط PDF في سير عمل أوسع

الآن بعد أن أصبحت قادرًا على **إنشاء ارتباط PDF** برمجيًا، فكر في الأفكار التالية:

- **معالجة دفعات**: تكرار عبر مجلد من ملفات DOCX، تحويل كل منها، وإضافة رابط إلى صفحة الفهرس.  
- **تقارير PDF ديناميكية**: توليد صفحة ملخص مع روابط لأقسام تفصيلية—مثالي لسجلات التدقيق.  
- **خدمات ويب**: إنشاء نقطة API تستقبل DOCX، تضيف **تعليق توضيحي قابل للنقر في PDF**، وتعيد بايتات PDF.  

جميع هذه السيناريوهات تعتمد على المفاهيم الأساسية التي غطيناها: التحميل، التعليق، والحفظ.

---

### TL;DR

أظهرنا كيفية **إنشاء ارتباط PDF** في C# عبر تحميل DOCX، إضافة تعليق توضيحي للارتباط، تعريف مستطيل قابل للنقر، تعيين وجهة إلى **صفحة PDF محددة**، وأخيرًا حفظ النتيجة. نفس النمط يتيح لك **تضمين رابط PDF**، **إنشاء رابط PDF قابل للنقر**، أو حتى **تحويل DOCX إلى PDF مع رابط** لأتمتة أكثر تعقيدًا.

لا تتردد في التجربة—غيّر حجم المستطيل، وجه إلى صفحات مختلفة، أو استبدل URL خارجي. إذا واجهت أي صعوبات، راجع جدول “الأخطاء الشائعة” أو اترك تعليقًا أدناه. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}