---
"description": "تعرّف على كيفية إضافة ختم التاريخ والوقت إلى ملفات PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل المفصل. مثالي لتعزيز مصداقية المستندات."
"linktitle": "إضافة طابع التاريخ والوقت في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة طابع التاريخ والوقت في ملف PDF"
"url": "/ar/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة طابع التاريخ والوقت في ملف PDF

## مقدمة

عندما يتعلق الأمر بإدارة المستندات، وخاصةً ملفات PDF، فإن إضافة ختم التاريخ والوقت تُحدث نقلة نوعية. سواء كنت تعمل على مستندات قانونية أو تقارير مشاريع أو فواتير، فإن ختم التاريخ لا يُضفي مصداقية فحسب، بل يُوفر أيضًا سجلًا واضحًا لتاريخ إنشاء المستند أو تعديله. في هذا الدليل، سنشرح لك عملية إضافة ختم التاريخ والوقت إلى ملف PDF باستخدام مكتبة Aspose.PDF لـ .NET. 

صُممت هذه المقالة لتكون واضحة وسهلة الفهم، لذا حتى لو كنت جديدًا في البرمجة أو استخدام مكتبة Aspose.PDF، ستتمكن من تطبيق هذه الميزة بثقة. هيا بنا!

## المتطلبات الأساسية

قبل أن نبدأ، هناك بعض المتطلبات الأساسية التي يجب أن تتوفر لديك:

1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. هنا ستكتب وتنفذ شفرتك البرمجية.
2. Aspose.PDF لـ .NET: عليك تنزيل وتثبيت مكتبة Aspose.PDF. يمكنك العثور على أحدث إصدار [هنا](https://releases.aspose.com/pdf/net/).
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم الأمثلة بشكل أفضل، ولكن لا تقلق إذا كنت بدأت للتو؛ فسنشرح كل شيء خطوة بخطوة.
4. ملف PDF: جهّز ملف PDF نموذجيًا. في مثالنا، سنستخدم ملفًا باسم `AddTextStamp.pdf`.

بمجرد حصولك على هذه المتطلبات الأساسية، ستكون جاهزًا لبدء إضافة طوابع التاريخ والوقت إلى ملفات PDF الخاصة بك!

## استيراد الحزم

للبدء، عليك استيراد مساحات الأسماء اللازمة في مشروع C# الخاص بك. إليك كيفية القيام بذلك:

### إنشاء مشروع جديد

1. افتح Visual Studio: قم بتشغيل تطبيق Visual Studio الخاص بك.
2. إنشاء مشروع جديد: حدد "إنشاء مشروع جديد" من شاشة البدء.
3. اختر تطبيق وحدة التحكم: حدد "تطبيق وحدة التحكم (.NET Framework)" من قائمة قوالب المشروع.
4. قم بتسمية مشروعك: امنح مشروعك اسمًا، على سبيل المثال، `PDFDateTimeStamp`.

### إضافة مرجع Aspose.PDF

1. انقر بزر الماوس الأيمن فوق المراجع: في مستكشف الحلول، انقر بزر الماوس الأيمن فوق مجلد "المراجع" الخاص بمشروعك.
2. حدد "إضافة مرجع": اختر "إضافة مرجع" من قائمة السياق.
3. ابحث عن Aspose.PDF: انتقل إلى المكان الذي نزّلت فيه Aspose.PDF وحدده. انقر على "موافق" لإضافته إلى مشروعك.

### استيراد مساحات الأسماء المطلوبة

في الجزء العلوي من `Program.cs` الملف، تحتاج إلى استيراد المساحات التالية:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

الآن بعد أن قمنا بإعداد كل شيء، دعنا نقسم عملية إضافة طابع التاريخ والوقت إلى ملف PDF إلى خطوات واضحة وقابلة للإدارة.

## الخطوة 1: تعيين دليل المستندات

أولاً، عليك تحديد المجلد الذي يوجد فيه ملف PDF. هذا مهم لأن الكود سيبحث عن الملف في هذا المجلد.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // استبدل بالمسار الفعلي الخاص بك
```

تأكد من الاستبدال `YOUR DOCUMENT DIRECTORY` مع المسار الفعلي لملف PDF الخاص بك.

## الخطوة 2: افتح مستند PDF

بعد ذلك، ستفتح مستند PDF الذي تريد إضافة الطابع الزمني إليه. 

```csharp
// فتح المستند
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

يقوم هذا السطر من التعليمات البرمجية بتهيئة `Document` الفصل ويحمل ملف PDF الخاص بك إلى `pdfDocument` هدف.

## الخطوة 3: إنشاء طابع التاريخ والوقت

الآن حان وقت إنشاء طابع التاريخ والوقت. نسقه لعرضه بطريقة محددة. 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

هنا، `DateTime.Now` يحصل على التاريخ والوقت الحاليين، و `ToString` تنسيقه إلى التنسيق المطلوب.

## الخطوة 4: إنشاء ختم نصي

بعد إعداد سلسلة التاريخ والوقت، يمكنك الآن إنشاء طابع نصي سيتم إضافته إلى ملف PDF الخاص بك.

```csharp
// إنشاء ختم نصي
TextStamp textStamp = new TextStamp(annotationText);
```

يؤدي هذا الخط إلى إنشاء مثيل جديد لـ `TextStamp` باستخدام سلسلة التاريخ والوقت المنسقة.

## الخطوة 5: تعيين خصائص الختم

يمكنك تخصيص مظهر وموقع الختم. إليك كيفية ضبط خصائصه:

```csharp
// تعيين خصائص الطوابع
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

في هذه الخطوة، قمنا بتعيين الهوامش ومحاذاة الختم إلى الزاوية اليمنى السفلية لصفحة PDF.

## الخطوة 6: إضافة الختم إلى ملف PDF

الآن حان الوقت لإضافة ختم النص إلى مستند PDF الخاص بك. 

```csharp
// إضافة طابع بريدي إلى مجموعة الطوابع
pdfDocument.Pages[1].AddStamp(textStamp);
```

يُضيف هذا السطر الطابع إلى الصفحة الأولى من ملف PDF. يمكنك تغيير رقم الصفحة إذا أردت وضعه في صفحة أخرى.

## الخطوة 7: إنشاء تعليق نصي مجاني (اختياري)

إذا كنت تريد إضافة تعليق توضيحي إلى الختم، يمكنك إنشاء `FreeTextAnnotation` على النحو التالي:

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

تؤدي هذه الخطوة الاختيارية إلى إنشاء تعليق نصي مجاني يمكنه توفير سياق أو معلومات إضافية حول الختم.

## الخطوة 8: تكوين حدود التعليقات التوضيحية

إذا كنت تريد تخصيص حدود التعليقات التوضيحية الخاصة بك، فيمكنك القيام بذلك أيضًا:

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

يقوم مقتطف التعليمات البرمجية هذا بتعيين عرض الحدود إلى 0، مما يجعلها غير مرئية، ويضيف التعليق التوضيحي إلى ملف PDF.

## الخطوة 9: حفظ مستند PDF

وأخيرًا، عليك حفظ مستند PDF المعدّل. 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // حدد اسم ملف الإخراج
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

يحفظ هذا السطر ملف PDF مع الطابع الزمني المُضاف في ملف جديد. يمكنك مراجعة المجلد المُحدد للاطلاع على النتيجة.

## خاتمة

تهانينا! لقد نجحت في إضافة ختم التاريخ والوقت إلى ملف PDF باستخدام Aspose.PDF لـ .NET. هذه الميزة البسيطة والفعّالة تُحسّن مستنداتك، وتجعلها أكثر احترافية، وتوفر سجلاً واضحاً لوقت إنشائها أو تعديلها. 

## الأسئلة الشائعة

### هل يمكنني تخصيص تنسيق التاريخ في الطابع الزمني؟
نعم يمكنك تعديل `ToString` طريقة لتغيير تنسيق التاريخ حسب تفضيلاتك.

### هل استخدام Aspose.PDF مجاني؟
يقدم Aspose.PDF نسخة تجريبية مجانية، ولكن للاستفادة من الميزات الكاملة، يلزمك شراء ترخيص. يمكنك الحصول على ترخيص مؤقت. [هنا](https://purchase.aspose.com/temporary-license/).

### هل يمكنني إضافة عدة طوابع زمنية إلى ملف PDF؟
بالتأكيد! يمكنك إنشاء عدة `TextStamp` الحالات وإضافتها إلى صفحات أو مواضع مختلفة في ملف PDF.

### ماذا لو لم يكن لدي Visual Studio؟
يمكنك استخدام أي بيئة تطوير متكاملة أو محرر نصوص C#، ولكن لتشغيل مشروعك واستكشاف أخطائه وإصلاحها، يوصى باستخدام Visual Studio.

### أين يمكنني العثور على المزيد من الأمثلة لاستخدام Aspose.PDF؟
يمكنك استكشاف المزيد من الأمثلة والبرامج التعليمية في [وثائق Aspose.PDF](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}