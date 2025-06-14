---
"description": "تعرّف على كيفية إضافة رسومات إلى ملفات PDF باستخدام Aspose.PDF لـ .NET. يتناول هذا الدليل خطوة بخطوة إعدادات الألوان، وإضافة الأشكال، وحفظ ملف PDF."
"linktitle": "إضافة رسم في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة رسم في ملف PDF"
"url": "/ar/net/programming-with-graphs/add-drawing/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة رسم في ملف PDF

## مقدمة

عند العمل على مستندات PDF، تُحسّن إضافة الرسومات من مظهرها ووظائفها بشكل كبير. سواءً كنت تُنشئ تقارير أو عروضًا تقديمية أو نماذج تفاعلية، فإن إمكانية تضمين رسومات وأشكال مخصصة أمرٌ أساسي. في هذا البرنامج التعليمي، سنستكشف كيفية إضافة رسومات إلى ملف PDF باستخدام Aspose.PDF لـ .NET. سنشرح العملية خطوة بخطوة، لضمان فهمك الواضح لكل مرحلة.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، تأكد من أن لديك ما يلي:

1. Aspose.PDF لـ .NET: تأكد من تثبيت Aspose.PDF لـ .NET. يمكنك تنزيله من [موقع Aspose](https://releases.aspose.com/pdf/net/).
2. .NET Framework: يفترض هذا البرنامج التعليمي أنك تستخدم بيئة تطوير .NET.
3. Visual Studio: على الرغم من أنه ليس إلزاميًا، فإن تثبيت Visual Studio سيجعل من الأسهل متابعة أمثلة التعليمات البرمجية.
4. المعرفة الأساسية بلغة C#: إن الفهم الأساسي لبرمجة C# سيساعدك على استيعاب مقتطفات التعليمات البرمجية المقدمة.

## استيراد الحزم

لبدء العمل مع Aspose.PDF لـ .NET، ستحتاج إلى استيراد مساحات الأسماء اللازمة. إليك كيفية القيام بذلك:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

لنستعرض عملية إضافة رسم إلى ملف PDF. سنُنشئ مثالًا بسيطًا نضيف فيه مستطيلًا بلون تعبئة شفاف إلى مستند PDF. اتبع الخطوات التالية:

## الخطوة 1: إعداد مشروعك

ابدأ بإعداد دليل المشروع الخاص بك وتحديد معلمات اللون للرسم الخاص بك:

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
int alpha = 10;
int green = 0;
int red = 100;
int blue = 0;
```

في هذا المثال، نقوم بتعريف قيم ألفا (الشفافية) وقيم RGB للوننا. `alpha` تتحكم القيمة في شفافية اللون، بينما تحدد قيم RGB اللون نفسه.

## الخطوة 2: إنشاء كائن ملون

الآن قم بإنشاء `Color` الكائن باستخدام قيم ألفا وRGB:

```csharp
// إنشاء كائن ملون باستخدام Alpha RGB
Aspose.Pdf.Color alphaColor = Aspose.Pdf.Color.FromArgb(alpha, red, green, blue); // توفير قناة ألفا
```

تعمل هذه الخطوة على تهيئة اللون بالشفافية، مما يسمح لنا بإنشاء رسومات بمستويات تعتيم مختلفة.

## الخطوة 3: إنشاء كائن المستند

بعد ذلك، قم بإنشاء ملف جديد `Document` الكائن الذي سيعمل كحاوية لملف PDF الخاص بنا:

```csharp
// إنشاء كائن مستند
Document document = new Document();
```

## الخطوة 4: إضافة صفحة إلى المستند

أضف صفحة جديدة إلى المستند. هنا سنضع رسمنا:

```csharp
// إضافة صفحة إلى مجموعة صفحات ملف PDF
Page page = document.Pages.Add();
```

## الخطوة 5: إنشاء كائن رسم بياني

ال `Graph` يسمح لنا الكائن برسم الأشكال والرسومات الأخرى. حدد أبعاد الرسم البياني:

```csharp
// إنشاء كائن رسم بياني بأبعاد معينة
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(300.0, 400.0);
```

هنا، نقوم بإنشاء رسم بياني بعرض 300 وحدة وارتفاع 400 وحدة.

## الخطوة 6: تعيين حدود لكائن الرسم البياني

قم بتحديد حدود الرسم البياني لجعله مميزًا بصريًا:

```csharp
// تعيين حدود لكائن الرسم
graph.Border = (new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, Aspose.Pdf.Color.Black));
```

يؤدي هذا إلى إضافة حدود سوداء حول الرسم البياني.

## الخطوة 7: إضافة الرسم البياني إلى الصفحة

الآن، أضف كائن الرسم البياني إلى مجموعة فقرات الصفحة:

```csharp
// إضافة كائن الرسم البياني إلى مجموعة فقرات مثيل الصفحة
page.Paragraphs.Add(graph);
```

## الخطوة 8: إنشاء كائن مستطيل وتكوينه

إنشاء مستطيل وتعيين لونه وتعبئته:

```csharp
// إنشاء كائن مستطيل بأبعاد معينة
Aspose.Pdf.Drawing.Rectangle rectangle = new Aspose.Pdf.Drawing.Rectangle(0, 0, 100, 50);

// إنشاء كائن graphInfo لنسخة المستطيل
Aspose.Pdf.GraphInfo graphInfo = rectangle.GraphInfo;

// تعيين معلومات اللون لنسخة GraphInfo
graphInfo.Color = (Aspose.Pdf.Color.Red);

// تعيين لون التعبئة لـ GraphInfo
graphInfo.FillColor = (alphaColor);
```

في هذه الخطوة، نحدد مستطيلاً بعرض ١٠٠ وحدة وارتفاع ٥٠ وحدة. ثم نضبط لون تعبئته على اللون الشفاف الذي أنشأناه سابقًا.

## الخطوة 9: إضافة المستطيل إلى الرسم البياني

أضف المستطيل إلى مجموعة أشكال الرسم البياني:

```csharp
// إضافة شكل مستطيل إلى مجموعة أشكال كائن الرسم البياني
graph.Shapes.Add(rectangle);
```

## الخطوة 10: حفظ مستند PDF

وأخيرًا، احفظ المستند في ملف:

```csharp
dataDir = dataDir + "AddDrawing_out.pdf";

// حفظ ملف PDF
document.Save(dataDir);
```

## خاتمة

في هذا البرنامج التعليمي، شرحنا عملية إضافة رسم إلى ملف PDF باستخدام Aspose.PDF لـ .NET. بدءًا من إعداد المشروع وحتى حفظ المستند النهائي، تعلمت كيفية إنشاء عناصر رسومية وتكوينها داخل ملف PDF. تُعد هذه تقنية فعّالة لتحسين مستندات PDF الخاصة بك بعناصر مرئية مخصصة.

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟

Aspose.PDF for .NET هي مكتبة تسمح للمطورين بإنشاء ملفات PDF ومعالجتها وتحويلها برمجيًا باستخدام .NET.

### كيف يمكنني تنزيل Aspose.PDF لـ .NET؟

يمكنك تنزيل Aspose.PDF لـ .NET من [صفحة إصدارات Aspose](https://releases.aspose.com/pdf/net/).

### هل يمكنني استخدام Aspose.PDF لـ .NET مجانًا؟

تقدم Aspose نسخة تجريبية مجانية من Aspose.PDF لـ .NET. يمكنك الحصول عليها من [صفحة التجربة المجانية](https://releases.aspose.com/).

### أين يمكنني العثور على وثائق Aspose.PDF لـ .NET؟

الوثائق متاحة على [موقع توثيق Aspose](https://reference.aspose.com/pdf/net/).

### كيف أحصل على الدعم لـ Aspose.PDF لـ .NET؟

للحصول على الدعم، يمكنك زيارة [منتدى Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}