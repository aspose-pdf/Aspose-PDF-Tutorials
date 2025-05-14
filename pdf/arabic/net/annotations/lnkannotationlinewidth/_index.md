---
"description": "تعرّف على كيفية ضبط عرض سطر التعليق بالحبر في ملف PDF باستخدام Aspose.PDF لـ .NET. يرشدك هذا البرنامج التعليمي المفصل خلال كل خطوة، مما يضمن لك جودة عالية في الإخراج."
"linktitle": "عرض سطر التعليق التوضيحي lnk"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "عرض سطر التعليق التوضيحي lnk"
"url": "/ar/net/annotations/lnkannotationlinewidth/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# عرض سطر التعليق التوضيحي lnk

## مقدمة

عند العمل على مستندات PDF، تُعدّ إضافة التعليقات التوضيحية وسيلة فعّالة لإبراز المعلومات أو إضافة عناصر تفاعلية إلى ملفاتك. ومن هذه التعليقات التوضيحية "التعليق بالحبر"، الذي يسمح لك برسم خطوط حرة على ملف PDF. ولكن ماذا لو احتجت إلى تخصيص مظهر هذه الخطوط، وخاصةً عرضها؟ في هذا البرنامج التعليمي، سنشرح لك عملية ضبط عرض خط التعليق بالحبر باستخدام Aspose.PDF لـ .NET.

## المتطلبات الأساسية

قبل الغوص في الكود، دعنا نتأكد من إعداد كل شيء لمتابعة هذا البرنامج التعليمي بسلاسة:

1. Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF لـ .NET. يمكنك تنزيلها من [صفحة التحميل](https://releases.aspose.com/pdf/net/) أو قم بتثبيته عبر NuGet Package Manager في Visual Studio.
2. بيئة التطوير: يفترض هذا البرنامج التعليمي أنك تعمل في بيئة تطوير .NET مثل Visual Studio.
3. المعرفة الأساسية بلغة C#: إن الفهم الأساسي للغة C# سيساعدك على متابعة خطوات الترميز.
4. مستند PDF: استخدم مستند PDF موجودًا أو قم بإنشاء مستند جديد لهذا البرنامج التعليمي.

## استيراد مساحات الأسماء الضرورية

قبل البدء في الترميز، تأكد من استيراد المساحات الأساسية اللازمة في مشروعك:

```csharp
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;
using System.Collections;
using System.Collections.Generic;
```

توفر هذه المساحات الأسماء الفئات والطرق اللازمة للتعامل مع مستندات PDF والعمل مع التعليقات التوضيحية والتعامل مع العناصر الرسومية.

الآن بعد أن وضعنا المتطلبات الأساسية في مكانها، فلنبدأ في تقسيم عملية ضبط عرض خط التعليق بالحبر إلى خطوات واضحة وقابلة للإدارة.

## الخطوة 1: تهيئة مستند PDF

أولاً، علينا إنشاء أو فتح مستند PDF. في هذا البرنامج التعليمي، سننشئ مستند PDF جديدًا من البداية.

```csharp
// تهيئة مستند PDF
string dataDir = "YOUR DOCUMENT DIRECTORY"; // حدد دليل المستند الخاص بك
Document doc = new Document();
doc.Pages.Add(); // إضافة صفحة فارغة إلى المستند
```

هنا، نقوم بتهيئة ملف جديد `Document` كائن يُمثل ملف PDF الخاص بنا. ثم نضيف صفحة فارغة إلى هذا المستند للعمل عليها.

## الخطوة 2: إنشاء تعليق الحبر

بعد ذلك، سننشئ شرح الحبر نفسه. يتضمن ذلك تحديد النقاط التي تُشكّل خطوط الحبر.

```csharp
// إنشاء تعليق بالحبر
IList<Point[]> inkList = new List<Point[]>();
LineInfo lineInfo = new LineInfo();
lineInfo.VerticeCoordinate = new float[] { 55, 55, 70, 70, 70, 90, 150, 60 };
lineInfo.Visibility = true;
lineInfo.LineColor = Color.Red;
lineInfo.LineWidth = 2;
```

في هذه الخطوة، نقوم بتعريف `LineInfo` كائن يحتوي على إحداثيات ضربات الحبر، ووضوحها، ولونها، وعرض الخط الأولي. `VerticeCoordinate` تحتوي المصفوفة على إحداثيات X وY لكل نقطة في الخط.

## الخطوة 3: تحويل الإحداثيات إلى نقاط

الآن، نحتاج إلى تحويل هذه الإحداثيات إلى نقاط يمكن استخدامها بواسطة Ink Annotation.

```csharp
// تحويل الإحداثيات إلى نقاط
int length = lineInfo.VerticeCoordinate.Length / 2;
Aspose.Pdf.Point[] gesture = new Aspose.Pdf.Point[length];
for (int i = 0; i < length; i++)
{
    gesture[i] = new Aspose.Pdf.Point(lineInfo.VerticeCoordinate[2 * i], lineInfo.VerticeCoordinate[2 * i + 1]);
}

inkList.Add(gesture);
```

تعمل هذه الحلقة على معالجة مجموعة الإحداثيات، وتحويل كل زوج من الإحداثيات إلى `Point` الكائن، والذي يضاف بعد ذلك إلى `inkList`.

## الخطوة 4: إضافة تعليق الحبر إلى صفحة PDF

بعد أن أصبحت النقاط جاهزة، يمكننا الآن إنشاء تعليق بالحبر وإضافته إلى صفحة PDF.

```csharp
// إضافة تعليق الحبر إلى صفحة PDF
InkAnnotation a1 = new InkAnnotation(doc.Pages[1], new Aspose.Pdf.Rectangle(100, 100, 300, 300), inkList);
a1.Subject = "Test";
a1.Title = "Title";
a1.Color = Aspose.Pdf.Color.FromRgb(Color.Green);
```

في هذه الخطوة، نقوم بتهيئة `InkAnnotation` كائن، مع تحديد الصفحة، والمستطيل المحيط، وقائمة النقاط. كما حددنا موضوع التعليق التوضيحي، وعنوانه، ولونه.

## الخطوة 5: تخصيص حدود التعليقات التوضيحية

لتخصيص مظهر التعليقات التوضيحية الخاصة بنا بشكل أكبر، سنقوم بتعديل خصائص حدودها.

```csharp
// تخصيص حدود التعليقات التوضيحية
Border border = new Border(a1);
border.Width = 3;
border.Effect = BorderEffect.Cloudy;
border.Dash = new Dash(1, 1);
border.Style = BorderStyle.Solid;
doc.Pages[1].Annotations.Add(a1);
```

هنا، نقوم بإنشاء `Border` كائن لتعليقنا التوضيحي، مع تحديد عرضه وتأثيره ونمطه ونمطه. تضمن هذه الخطوة ظهور التعليق التوضيحي بصريًا على صفحة PDF.

## الخطوة 6: حفظ مستند PDF

وأخيرًا، بعد إجراء كافة التغييرات اللازمة، حان الوقت لحفظ المستند.

```csharp
// حفظ مستند PDF
dataDir = dataDir + "lnkAnnotationLineWidth_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nInk annotation line width setup successfully.\nFile saved at " + dataDir);
```

يحفظ هذا الكود مستند PDF المُعدَّل مع ملاحظة الحبر في الدليل المُحدَّد. `Console.WriteLine` يؤكد البيان التنفيذ الناجح للكود.

## خاتمة

تهانينا! لقد نجحت في إنشاء وتخصيص تعليق توضيحي بالحبر في مستند PDF باستخدام Aspose.PDF لـ .NET. غطى هذا البرنامج التعليمي العملية بأكملها، من تهيئة المستند إلى حفظ الملف النهائي. بفضل هذه المعرفة، يمكنك استكشاف الإمكانات الهائلة لـ Aspose.PDF لـ .NET بشكل أكبر، وتطبيق تقنيات مماثلة على أنواع أخرى من التعليقات التوضيحية أو معالجة ملفات PDF.

## الأسئلة الشائعة

### هل يمكنني استخدام ألوان مختلفة لأجزاء مختلفة من شرح الحبر؟  
نعم، يمكنك إنشاء عدة `InkAnnotation` كائنات بألوان مختلفة وإضافتها إلى نفس الصفحات أو صفحات مختلفة في ملف PDF الخاص بك.

### كيف يمكنني تغيير عرض الخط بشكل ديناميكي؟  
يمكنك تعديل `LineWidth` ممتلكات `LineInfo` الكائن قبل تحويل الإحداثيات إلى نقاط.

### هل من الممكن جعل تعليق الحبر شفافًا؟  
نعم يمكنك تعديل `Opacity` ممتلكات `InkAnnotation` كائن لجعله شفافًا.

### هل يمكنني إضافة تعليقات حبر متعددة إلى نفس الصفحة؟  
بالتأكيد! يمكنك إضافة أي عدد تريده من التعليقات بالحبر إلى صفحة واحدة بتكرار العملية.

### كيف يمكنني إزالة تعليق الحبر من ملف PDF؟  
يمكنك إزالة التعليق التوضيحي باستخدام `doc.Pages[1].Annotations.Delete(a1)` الطريقة، حيث `a1` هو كائن التعليق التوضيحي الخاص بك.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}