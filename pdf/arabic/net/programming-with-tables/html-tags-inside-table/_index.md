---
"description": "تعرّف على كيفية تضمين وسوم HTML داخل خلايا الجدول في ملف PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل المفصل. أنشئ مستندات PDF ديناميكية واحترافية."
"linktitle": "علامات HTML داخل الجدول في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "علامات HTML داخل الجدول في ملف PDF"
"url": "/ar/net/programming-with-tables/html-tags-inside-table/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# علامات HTML داخل الجدول في ملف PDF

## مقدمة

عند العمل مع ملفات PDF في .NET، تُعد مكتبة Aspose.PDF أداةً استثنائيةً لإنشاء مستندات PDF ومعالجتها وتحويلها. من الميزات المتقدمة التي توفرها Aspose.PDF إمكانية تضمين محتوى HTML داخل خلايا الجدول في ملف PDF. سيرشدك هذا الدليل إلى كيفية تحقيق ذلك باستخدام Aspose.PDF لـ .NET. بنهاية هذا الدليل، ستتمكن من إنشاء جداول ديناميكيًا تتضمن محتوى HTML في خلاياها.

## المتطلبات الأساسية

قبل الغوص في الدليل خطوة بخطوة، دعنا نتأكد من أن لديك الأدوات والموارد اللازمة للمتابعة.

- Aspose.PDF لـ .NET: ستحتاج إلى الإصدار الأحدث من Aspose.PDF. [تحميله هنا](https://releases.aspose.com/pdf/net/).
- بيئة .NET: تأكد من إعداد Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة مع إطار عمل .NET.
- الترخيص: إذا كنت لا تستخدم إصدارًا مرخصًا من Aspose.PDF، فيمكنك الحصول على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/).
- الفهم الأساسي للغة C#: إن المعرفة بلغة C# والبرمجة الموجهة للكائنات مفيدة.
- معرفة HTML: سيكون من المفيد لهذا البرنامج التعليمي الحصول على بعض الفهم لبنية HTML.

## استيراد الحزم الضرورية

قبل البدء بكتابة الكود، من الضروري استيراد مساحات الأسماء اللازمة. تتيح لنا هذه المساحات العمل مع فئات وطرق Aspose.PDF التي سنستخدمها لمعالجة مستندات PDF.

```csharp
using System;
using System.Data;
```

الآن، دعونا نقسم المهمة إلى خطوات مفصلة، حيث نشرح كل جزء من العملية بوضوح ودقة.

## الخطوة 1: إعداد دليل المستندات الخاص بك

الخطوة الأولى هي تحديد مسار مجلد المستندات. هنا سيتم حفظ ملف PDF بعد إنشائه وتعديله.

```csharp
// قم بتحديد المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

تأكد من الاستبدال `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي تريد حفظ ملف PDF فيه. هذا ضروري لتسهيل تحديد موقع المستند عند إنشائه.

## الخطوة 2: إنشاء جدول البيانات وملئه بمحتوى HTML

الآن، نقوم بإنشاء `DataTable` لحفظ البيانات التي سيتم عرضها داخل الجدول في ملف PDF الخاص بنا. هذا `DataTable` سيتم تخزين محتوى HTML، مثل `<li>` العلامات التي نريد تضمينها داخل الخلايا.

```csharp
// إنشاء جدول بيانات وإضافة أعمدة
DataTable dt = new DataTable("Employee");
dt.Columns.Add("data", System.Type.GetType("System.String"));
```

بمجرد `DataTable` عند إنشاء جدول، ستحتاج إلى ملئه بمحتوى HTML الذي ترغب في ظهوره فيه. في هذه الحالة، نضيف عناصر قائمة HTML مع عناوين.

```csharp
// إضافة صفوف تحتوي على محتوى HTML
DataRow dr = dt.NewRow();
dr[0] = "<li>Department of Emergency Medicine: 3400 Spruce Street Ground Silverstein Bldg Philadelphia PA 19104-4206</li>";
dt.Rows.Add(dr);
dr = dt.NewRow();
dr[0] = "<li>Penn Observation Medicine Service: 3400 Spruce Street Ground Floor Donner Philadelphia PA 19104-4206</li>";
dt.Rows.Add(dr);
dr = dt.NewRow();
dr[0] = "<li>UPHS/Presbyterian - Dept. of Emergency Medicine: 51 N. 39th Street . Philadelphia PA 19104-2640</li>";
dt.Rows.Add(dr);
```

تضمن هذه الخطوة أن خلايا الجدول ستحتوي على محتوى بتنسيق HTML، والذي سيتم عرضه بشكل صحيح داخل مستند PDF.

## الخطوة 3: إنشاء مستند PDF جديد

بعد الحصول على بياناتنا، الخطوة التالية هي إنشاء مستند PDF جديد. سيُستخدم هذا المستند كلوحة لإضافة جدولنا.

```csharp
// تهيئة مستند PDF جديد
Document doc = new Document();
doc.Pages.Add();
```

يؤدي مقتطف التعليمات البرمجية البسيط هذا إلى إنشاء مستند PDF فارغ وإضافة صفحة جديدة إليه، والتي ستحتوي لاحقًا على الجدول.

## الخطوة 4: إعداد الجدول

الآن، سننشئ ونُعدّ جدولًا داخل مستند PDF. سيُحدّد هذا الجدول عرض أعمدته وإعدادات حدوده.

```csharp
// تهيئة مثيل جديد للجدول
Aspose.Pdf.Table tableProvider = new Aspose.Pdf.Table();
// تعيين عرض أعمدة الجدول
tableProvider.ColumnWidths = "400 50";
// تعيين لون حدود الجدول إلى LightGray
tableProvider.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.5F, Aspose.Pdf.Color.FromRgb(System.Drawing.Color.LightGray));
// تعيين الحدود لخلايا الجدول الفردية
tableProvider.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.5F, Aspose.Pdf.Color.FromRgb(System.Drawing.Color.LightGray));
```

في هذه الخطوة، أنشأتَ جدولًا بنجاح، وحددتَ عرض أعمدة وحدودًا مخصصةً لكلٍّ من الجدول وخلاياه. تضمن عروض الأعمدة محاذاةً سليمةً للبيانات داخل الجدول.

## الخطوة 5: تحديد الحشو واستيراد البيانات

لتحسين المظهر الجمالي للجدول، سنُعرّف حشو الخلايا. ثم نستورد `DataTable` مع محتوى HTML في جدول PDF.

```csharp
// تعيين الحشو لخلايا الجدول
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 2.5F;
margin.Left = 2.5F;
margin.Bottom = 1.0F;
tableProvider.DefaultCellPadding = margin;

// استيراد جدول البيانات إلى جدول PDF
tableProvider.ImportDataTable(dt, false, 0, 0, 3, 1, true);
```

من خلال تحديد الهوامش، نمنح خلايا الجدول مساحة للتنفس، مما يجعل المحتوى أكثر جاذبية بصريًا. `ImportDataTable` الطريقة تسحب في `DataTable` لقد قمنا بإنشائها مسبقًا، مع التأكد من تضمين محتوى HTML في الخلايا.

## الخطوة 6: أضف الجدول إلى ملف PDF واحفظه

وأخيرًا نضيف الجدول إلى الصفحة الأولى من مستند PDF ونحفظ الملف.

```csharp
// أضف الجدول إلى الصفحة الأولى من مستند PDF
doc.Pages[1].Paragraphs.Add(tableProvider);

// حفظ مستند PDF
doc.Save(dataDir + "HTMLInsideTableCell_out.pdf");
```

في هذه الخطوة، يتم وضع الجدول الذي يحتوي على محتوى HTML في الصفحة الأولى من ملف PDF، ويتم حفظ الملف في الدليل المحدد.

## خاتمة

باتباع الخطوات المذكورة أعلاه، نجحت في تضمين وسوم HTML داخل خلايا جدول في مستند PDF باستخدام Aspose.PDF لـ .NET. يوضح هذا البرنامج التعليمي كيفية الاستفادة من الميزات القوية لـ Aspose.PDF لإنشاء مستندات PDF ديناميكية وجذابة بصريًا في تطبيقات .NET. سواء كنت تُنشئ فواتير أو تقارير أو جداول مفصلة بمحتوى HTML، توفر هذه الطريقة أساسًا متينًا لمعالجة ملفات PDF.

## الأسئلة الشائعة

### هل يمكن لـ Aspose.PDF التعامل مع محتوى HTML المعقد داخل خلايا الجدول؟  
نعم، يمكن لـ Aspose.PDF معالجة وعرض مجموعة واسعة من علامات HTML داخل خلايا الجدول، بما في ذلك القوائم والصور والروابط.

### كيف يمكنني تعديل حجم الأعمدة في الجدول؟  
يمكنك التحكم في عرض الأعمدة باستخدام `ColumnWidths` الخاصية عن طريق تحديد العرض لكل عمود.

### هل من الممكن تنسيق النص داخل خلايا الجدول؟  
بالتأكيد! يمكنك استخدام علامات HTML مثل `<b>`، `<i>`، و `<u>` داخل المحتوى لتنسيق النص داخل خلايا الجدول.

### ماذا يحدث إذا كان محتوى HTML الخاص بي كبيرًا جدًا بالنسبة لخلية الجدول؟  
إذا تجاوز المحتوى حجم الخلية، فسيتم تعديل الجدول تلقائيًا، ولكن يمكنك تخصيص حجم الخلية وخيارات التفاف الكلمات للتحكم في كيفية عرض المحتوى.

### هل يمكنني إضافة أكثر من جدول إلى مستند PDF؟  
نعم، يمكنك إضافة جداول متعددة إلى مستند PDF ببساطة عن طريق تكرار الخطوات الخاصة بإضافة الجداول، كل منها على صفحة أو قسم جديد من ملف PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}