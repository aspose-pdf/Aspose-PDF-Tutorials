---
"description": "تعرّف على كيفية ملاءمة جدول تلقائيًا للنافذة باستخدام Aspose.PDF لـ .NET في هذا الدليل المفصل خطوة بخطوة. مثالي لإنشاء جداول أنيقة وملائمة تمامًا في ملفات PDF."
"linktitle": "ملاءمة تلقائية للنافذة"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "ملاءمة تلقائية للنافذة"
"url": "/ar/net/programming-with-tables/auto-fit-to-window/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ملاءمة تلقائية للنافذة

## مقدمة

عند العمل مع ملفات PDF، من الشائع التعامل مع الجداول، وفي بعض الأحيان تحتاج إلى أن تتناسب هذه الجداول تمامًا مع عرض الصفحة. في هذا البرنامج التعليمي، سنستكشف كيفية ضبط عرض جدول تلقائيًا في نافذة باستخدام Aspose.PDF لـ .NET. هذا سيجعل جداولك تبدو أنيقة ومنظمة، ويمنع مشاكل مثل امتلاء الأعمدة أو عدم استواءها. هل أنت مستعد للتعلم؟ هيا بنا!

## المتطلبات الأساسية

قبل أن ننتقل إلى الدليل خطوة بخطوة، هناك بعض الأشياء التي ستحتاج إليها:

1. تم تثبيت Aspose.PDF لـ .NET في مشروعك. إذا لم يكن لديك بعد، يمكنك [قم بتحميله هنا](https://releases.aspose.com/pdf/net/) أو استكشافهم [نسخة تجريبية مجانية](https://releases.aspose.com/).
2. فهم أساسي لبرمجة .NET.
3. Visual Studio أو أي IDE يدعم .NET مثبت على نظامك.

> ملاحظة: لا تنسَ أنك ستحتاج إلى ترخيص لاستخدام Aspose.PDF دون قيود. يمكنك شراء ترخيص [هنا](https://purchase.aspose.com/buy) أو احصل على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) لتجربة كافة الميزات.

## استيراد الحزم

قبل الغوص في الكود، ستحتاج إلى استيراد مساحات الأسماء الضرورية:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

الآن بعد أن أصبح كل شيء جاهزًا، دعنا نقسم هذا إلى خطوات بسيطة وسهلة الفهم لفهم كيفية ملاءمة جدول تلقائيًا للنافذة باستخدام Aspose.PDF لـ .NET.

## الخطوة 1: تهيئة كائن المستند

أولاً، عليك إنشاء مستند PDF. اعتبر هذا المستند صفحةً فارغةً لإضافة الصفحات والجداول.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// إنشاء كائن Pdf عن طريق استدعاء المنشئ الفارغ الخاص به
Document doc = new Document();
```
  
هنا، نقوم بإنشاء مستند جديد باستخدام `Document` فئة من Aspose.PDF. `dataDir` هو الموقع الذي سيتم حفظ ملف PDF الخاص بك فيه بعد الانتهاء.

## الخطوة 2: إضافة صفحة إلى المستند

مستند PDF يحتاج إلى صفحات، أليس كذلك؟ لنُضِف صفحةً واحدة.

```csharp
// إنشاء قسم (صفحة) في كائن Pdf
Page sec1 = doc.Pages.Add();
```
  
لقد أضفنا صفحة جديدة إلى المستند باستخدام `Pages.Add()` يمكنك اعتبار هذه الطريقة بمثابة إضافة ورقة جديدة إلى مستندك حيث ستضع الجدول.

## الخطوة 3: إنشاء جدول وتكوينه

الآن حان الوقت لإنشاء جدول وتعديله ليتناسب مع النافذة.

```csharp
// إنشاء كائن جدول
Aspose.Pdf.Table tab1 = new Aspose.Pdf.Table();
// أضف الجدول في مجموعة فقرات القسم المطلوب
sec1.Paragraphs.Add(tab1);
```
  
لقد قمنا بتهيئة ملف جديد `Table` الكائن وأضفناه إلى مجموعة فقرات الصفحة. يمكن أن تحتوي كل صفحة PDF على فقرات مختلفة، وهنا نتعامل مع الجدول كفقرة.

## الخطوة 4: تحديد عرض الأعمدة والملاءمة التلقائية للنافذة

بعد ذلك، قمنا بتعيين عرض الأعمدة والتأكد من أن الجدول يتكيف مع النافذة.

```csharp
// تعيين عرض الأعمدة للجدول
tab1.ColumnWidths = "50 50 50";
tab1.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```
  
لقد قمنا بتعيين عرض عمود ثابت للجدول ولكن أضفنا أيضًا `ColumnAdjustment.AutoFitToWindow`، مما يضمن أن الجدول يضبط حجمه ليناسب النافذة المتاحة.

## الخطوة 5: تعيين الحدود والهوامش للجدول والخلايا

الجداول التي لا تحتوي على حدود غالبًا ما تكون غير قابلة للقراءة. لنُعرّف الحدود والهوامش لجعلها تبدو منظمة.

```csharp
// تعيين حدود الخلية الافتراضية باستخدام كائن BorderInfo
tab1.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);

// تعيين حدود الجدول باستخدام كائن BorderInfo مخصص آخر
tab1.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 1F);

// إنشاء كائن MarginInfo وتعيين هوامشه اليسرى والسفلى واليمنى والعلوية
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;

// تعيين الحشو الافتراضي للخلية إلى كائن MarginInfo
tab1.DefaultCellPadding = margin;
```
  
تتم إضافة الحدود إلى كل من الجدول والخلايا باستخدام `BorderInfo` الفئة، حيث يمكنك تحديد السُمك. الهوامش مُعدّة لتوفير مساحة للحشو في الخلايا.

## الخطوة 6: إضافة الصفوف والخلايا إلى الجدول

جدول بلا محتوى؟ هذا ليس جيدًا! لنُضِف بعض الصفوف والخلايا.

```csharp
// إنشاء صفوف في الجدول ثم خلايا في الصفوف
Aspose.Pdf.Row row1 = tab1.Rows.Add();
row1.Cells.Add("col1");
row1.Cells.Add("col2");
row1.Cells.Add("col3");

Aspose.Pdf.Row row2 = tab1.Rows.Add();
row2.Cells.Add("item1");
row2.Cells.Add("item2");
row2.Cells.Add("item3");
```
  
سننشئ صفين ونضيف ثلاث خلايا لكل صف. هنا ستُدخل بياناتك الفعلية (التي قد تكون أي شيء، من سلاسل نصية إلى عناصر أكثر تعقيدًا).

## الخطوة 7: حفظ المستند

بمجرد إعداد كل شيء، ستحتاج إلى حفظ مستند PDF الذي قمت بإنشائه حديثًا.

```csharp
dataDir = dataDir + "AutoFitToWindow_out.pdf";
// حفظ المستند المحدث الذي يحتوي على كائن الجدول
doc.Save(dataDir);
```
  
ال `doc.Save()` تحفظ هذه الطريقة ملف PDF في المجلد المحدد. في هذه الحالة، سيتم حفظ المستند باسم `AutoFitToWindow_out.pdf` في الدليل المحدد الخاص بك.

## خاتمة

ها قد انتهيت! لقد أنشأتَ للتو جدولاً يناسب النافذة تلقائيًا باستخدام Aspose.PDF لـ .NET. هذا لا يضمن فقط مظهرًا احترافيًا وملائمًا لجدولك، بل يمنحك أيضًا مرونة عند العمل مع أحجام بيانات مختلفة. سواء كنت تُنشئ تقارير أو فواتير أو أي مستند يتطلب جداول، تُعد هذه الطريقة طريقة رائعة للحفاظ على تخطيطات واضحة وسهلة القراءة.

## الأسئلة الشائعة

### هل يمكنني إضافة المزيد من الصفوف بشكل ديناميكي؟  
نعم، يمكنك الاستمرار في إضافة الصفوف باستخدام `tab1.Rows.Add()` الطريقة تعتمد بشكل ديناميكي على المحتوى.

### كيف أقوم بتعديل الجدول إذا كنت لا أريد أن يتناسب تلقائيًا؟  
يمكنك ضبط يدويًا `ColumnWidths` بدون استخدام `ColumnAdjustment.AutoFitToWindow` للحفاظ على عرض ثابت للجدول.

### هل يمكنني إضافة صور أو محتوى آخر داخل الخلايا؟  
نعم، يسمح لك Aspose.PDF بإضافة الصور والنصوص وحتى الجداول الأخرى داخل الخلايا!

### ماذا لو كنت بحاجة إلى أنماط جدول أكثر تعقيدًا؟  
بإمكانك تخصيص أنماط الجدول والخلايا بشكل أكبر باستخدام خصائص مثل لون الخلفية ومحاذاة النص وإعدادات الخط.

### هل من الممكن تصدير هذا الجدول إلى تنسيقات أخرى غير PDF؟  
بالتأكيد! يدعم Aspose.PDF التصدير إلى صيغ مختلفة مثل HTML وDOCX وغيرها.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}