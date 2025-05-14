---
"description": "تعرف على كيفية عرض الرموز القابلة للاستبدال في ملفات PDF باستخدام Aspose.PDF لـ .NET باستخدام هذا الدليل خطوة بخطوة."
"linktitle": "عرض الرموز القابلة للاستبدال في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "عرض الرموز القابلة للاستبدال في ملف PDF"
"url": "/ar/net/programming-with-text/rendering-replaceable-symbols/"
"weight": 310
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# عرض الرموز القابلة للاستبدال في ملف PDF

## مقدمة

إنشاء ملفات PDF والتعامل معها قد يبدو أشبه بخوض متاهة. مع توفر العديد من الخيارات والأدوات، قد يكون العثور على الحل المناسب لاحتياجاتك أمرًا صعبًا. لحسن الحظ، تُعد Aspose.PDF for .NET مكتبة قوية تُسهّل العمل مع مستندات PDF، بما في ذلك عرض الرموز القابلة للاستبدال. في هذا البرنامج التعليمي، سنشرح خطوات عرض الرموز القابلة للاستبدال في ملف PDF باستخدام Aspose.PDF for .NET. سواء كنت مطورًا محترفًا أو مبتدئًا، سيوفر لك هذا الدليل كل ما تحتاجه للبدء.

## المتطلبات الأساسية

قبل التعمق في الكود، تأكد من امتلاكك كل ما تحتاجه للمتابعة. إليك المتطلبات الأساسية:

1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. هنا ستكتب وتُشغّل شيفرة .NET.
2. .NET Framework: يجب أن يكون لديك إصدار متوافق من .NET Framework. يدعم Aspose.PDF الإصدار 4.0 والإصدارات الأحدث.
3. Aspose.PDF لـ .NET: يجب أن يكون لديك مكتبة Aspose.PDF. يمكنك تنزيلها من [موقع Aspose](https://releases.aspose.com/pdf/net/)إذا كنت تريد تجربته أولاً، يمكنك الحصول على نسخة تجريبية مجانية [هنا](https://releases.aspose.com/).
4. المعرفة الأساسية بلغة البرمجة C#: ستساعدك المعرفة بلغة البرمجة C# على فهم مقتطفات التعليمات البرمجية بشكل أفضل.
5. قارئ PDF: لعرض ملفات PDF الناتجة، تأكد من تثبيت قارئ PDF على جهازك.

## استيراد الحزم

قبل البدء بالبرمجة، علينا استيراد الحزم اللازمة. في مشروع C#، تأكد من إضافة مرجع إلى مكتبة Aspose.PDF. إليك كيفية القيام بذلك:

1. افتح مشروع Visual Studio الخاص بك.
2. انقر بزر الماوس الأيمن على المشروع في مستكشف الحلول وحدد "إدارة حزم NuGet".
3. ابحث عن "Aspose.PDF" وقم بتثبيت الحزمة.

بعد تثبيت المكتبة، يمكنك البدء بكتابة الكود. تجد أدناه دليلًا خطوة بخطوة لعرض الرموز القابلة للاستبدال في ملف PDF.

## الخطوة 1: إعداد مشروعك

### إنشاء مشروع جديد

أولاً وقبل كل شيء، دعنا ننشئ مشروع C# جديدًا حيث سننفذ وظيفة عرض PDF الخاصة بنا.

- افتح Visual Studio.
- حدد "إنشاء مشروع جديد".
- اختر "تطبيق وحدة التحكم (.NET Framework)" ثم انقر فوق "التالي".
- قم بتسمية مشروعك (على سبيل المثال، "PDFRenderingExample") وانقر فوق "إنشاء".

### إضافة باستخدام التوجيهات

في الجزء العلوي من `Program.cs` الملف، أضف التوجيهات اللازمة باستخدام Aspose.PDF:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## الخطوة 2: تهيئة مستند PDF

الآن، لنُنشئ مستند PDF جديدًا ونُضيف إليه صفحة. هنا سنُقدّم رموزنا القابلة للاستبدال.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // حدد دليل المستند الخاص بك
Document pdfDocument = new Document(); // إنشاء مستند PDF جديد
Page pdfPage = pdfDocument.Pages.Add(); // إضافة صفحة جديدة إلى المستند
```

- نبدأ بتعريف المتغير `dataDir` للاحتفاظ بالمسار الذي سنحفظ فيه ملف PDF الخاص بنا لاحقًا.
- نقوم بإنشاء مثيل جديد لـ `Document` الفئة التي تمثل ملف PDF الخاص بنا.
- ثم نضيف صفحة جديدة إلى هذه الوثيقة باستخدام `Pages.Add()` طريقة.

## الخطوة 3: إنشاء جزء النص

بعد ذلك، سننشئ جزءًا نصيًا يحتوي على النص الذي نريد عرضه في ملف PDF. هنا يمكننا تضمين الرموز القابلة للاستبدال.

```csharp
TextFragment textFragment = new TextFragment("Applicant Name: " + Environment.NewLine + " Joe Smoe");
```

- ال `TextFragment` يتم استخدام الفئة لإنشاء جزء من النص يمكن إضافته إلى ملف PDF. 
- نقوم بتضمين علامة سطر جديد (`Environment.NewLine`) لتنسيق النص بشكل صحيح.

## الخطوة 4: تعيين خصائص جزء النص

الآن، دعنا نقوم بتخصيص مظهر جزء النص الخاص بنا، مثل حجم الخط ونوع الخط والألوان.

```csharp
textFragment.TextState.FontSize = 12; // ضبط حجم الخط
textFragment.TextState.Font = FontRepository.FindFont("TimesNewRoman"); // تعيين نوع الخط
textFragment.TextState.BackgroundColor = Color.LightGray; // تعيين لون الخلفية
textFragment.TextState.ForegroundColor = Color.Red; // تعيين لون النص
```

- لقد وضعنا `FontSize` إلى 12 لجعل النص قابلاً للقراءة.
- استخدام `FontRepository.FindFont()`، نحدد نوع الخط.
- نقوم أيضًا بتخصيص ألوان الخلفية والأمامية لتحسين الرؤية.

## الخطوة 5: إنشاء فقرة نصية

بعد ذلك، سنقوم بإنشاء `TextParagraph` كائن لحمل جزء النص الخاص بنا.

```csharp
TextParagraph paragraph = new TextParagraph(); // إنشاء فقرة نصية جديدة
paragraph.AppendLine(textFragment); // أضف جزءًا من النص إلى الفقرة
```

- ال `TextParagraph` تسمح لنا الفئة بتجميع العديد من `TextFragment` أشياء.
- نحن نستخدم `AppendLine()` لإضافة جزء النص الخاص بنا إلى الفقرة، مع التأكد من ظهوره بشكل صحيح في ملف PDF.

## الخطوة 6: تعيين موضع الفقرة

الآن، دعونا نحدد موضع فقرتنا على صفحة PDF.

```csharp
paragraph.Position = new Position(100, 600); // تعيين موضع الفقرة
```

- ال `Position` تأخذ الخاصية معاملين: إحداثيات X وY. يحدد هذان المعاملان مكان ظهور النص في الصفحة. عدّل هذه القيم بما يتناسب مع تصميمك.

## الخطوة 7: إنشاء منشئ نص

لإضافة فقرتنا إلى صفحة PDF، سنستخدم `TextBuilder`.

```csharp
TextBuilder textBuilder = new TextBuilder(pdfPage); // إنشاء TextBuilder للصفحة
```

- ال `TextBuilder` تساعدنا هذه الفئة على إضافة نص إلى صفحة معينة. من خلال تمرير `pdfPage` إلى المنشئ، نحن على استعداد لإدراج فقرتنا.

## الخطوة 8: إضافة الفقرة إلى الصفحة

أخيرًا، سنقوم بإضافة فقرتنا إلى صفحة PDF باستخدام `TextBuilder`.

```csharp
textBuilder.AppendParagraph(paragraph); // أضف الفقرة إلى الصفحة
```

- يأخذ هذا السطر من التعليمات البرمجية الفقرة التي تم إنشاؤها مسبقًا ويضيفها إلى صفحة PDF، مما يجعلها مرئية في المستند النهائي.

## الخطوة 9: حفظ مستند PDF

الآن بعد أن أضفنا النص، حان الوقت لحفظ مستند PDF في الدليل المحدد.

```csharp
dataDir = dataDir + "RenderingReplaceableSymbols_out.pdf"; // تحديد اسم ملف الإخراج
pdfDocument.Save(dataDir); // حفظ المستند
```

- نضيف اسم ملف الإخراج إلى ملفنا `dataDir`.
- ال `Save()` تكتب الطريقة ملف PDF على القرص، مما يجعله متاحًا للعرض.

## الخطوة 10: إخراج رسالة النجاح

دعنا نقدم ملاحظات للمستخدم تشير إلى أنه تم إنشاء ملف PDF بنجاح.

```csharp
Console.WriteLine("\nReplaceable symbols rendered successfully during PDF creation.\nFile saved at " + dataDir);
```

- يقوم هذا السطر بطباعة رسالة نجاح في وحدة التحكم، مما يساعد المستخدمين على التأكد من اكتمال العملية دون أخطاء.

## خاتمة

وها قد انتهيت! لقد نجحت في عرض رموز قابلة للاستبدال في ملف PDF باستخدام Aspose.PDF لـ .NET. تتيح لك هذه المكتبة القوية التعامل مع مستندات PDF بسهولة، وباتباع الخطوات الموضحة أعلاه، يمكنك تخصيص مستنداتك لتناسب احتياجاتك تمامًا.

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وتحويلها داخل تطبيقات .NET.

### هل يمكنني استخدام Aspose.PDF مجانًا؟
نعم، يمكنك تنزيل نسخة تجريبية مجانية من [موقع Aspose](https://releases.aspose.com/).

### كيف أقوم بتثبيت Aspose.PDF في مشروعي؟
يمكنك تثبيته عبر NuGet Package Manager في Visual Studio عن طريق البحث عن "Aspose.PDF".

### ما هي لغات البرمجة التي يدعمها Aspose.PDF؟
يدعم Aspose.PDF بشكل أساسي لغات .NET، بما في ذلك C#، وVB.NET، وASP.NET.

### أين يمكنني العثور على مزيد من الوثائق حول Aspose.PDF؟
يمكنك العثور على وثائق مفصلة على [موقع Aspose](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}