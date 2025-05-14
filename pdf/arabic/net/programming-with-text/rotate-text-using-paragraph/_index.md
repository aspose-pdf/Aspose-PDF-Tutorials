---
"description": "تعلّم كيفية تدوير النص في ملف PDF باستخدام Aspose.PDF لـ .NET. اتبع هذا الدليل خطوة بخطوة لإنشاء مستنداتك."
"linktitle": "تدوير النص باستخدام الفقرة في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تدوير النص باستخدام الفقرة في ملف PDF"
"url": "/ar/net/programming-with-text/rotate-text-using-paragraph/"
"weight": 380
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تدوير النص باستخدام الفقرة في ملف PDF

## مقدمة

إنشاء ملفات PDF بنصوص ديناميكية يُعدّ طريقةً جذابةً لعرض المعلومات. إذا كنت ترغب في إضافة لمسةٍ جماليةٍ إلى مستنداتك، فإن تدوير النص يُساعد في إبراز النقاط الرئيسية أو ببساطة يُضفي تصميمًا جذابًا بصريًا. في هذا الدليل، سأشرح لك كيفية تدوير النص باستخدام Aspose.PDF لـ .NET، مما يجعل مستندات PDF الخاصة بك أكثر تفاعليةً وإثارةً للاهتمام!

## المتطلبات الأساسية

قبل أن نتعمق في عالم تدوير النصوص المثير في ملفات PDF، لنتأكد من إعداد كل شيء بشكل صحيح. إليك المتطلبات الأساسية التي ستحتاجها:

1. Aspose.PDF لـ .NET: تأكد من تثبيت Aspose.PDF لـ .NET في مشروعك. يمكنك تنزيله من [موقع إلكتروني](https://releases.aspose.com/pdf/net/).
2. Visual Studio: يفترض هذا البرنامج التعليمي أنك تستخدم Visual Studio لتطوير .NET.
3. المعرفة الأساسية بلغة C#: ستساعدك معرفة برمجة C# على فهم الأمثلة بشكل أفضل. إذا كنت جديدًا، فلا تقلق؛ سنشرح لك خطوة بخطوة!
4. إطار عمل .NET: تأكد من تثبيت الإصدار المناسب من إطار عمل .NET على مشروعك. يدعم Aspose.PDF إصدارات مختلفة، لذا راجع الوثائق للتأكد من التوافق.

بمجرد توفر هذه المتطلبات الأساسية، سنكون جاهزين لبدء كتابة بعض التعليمات البرمجية!

## استيراد الحزم

لاستخدام Aspose.PDF بفعالية، ستحتاج إلى استيراد مساحات الأسماء اللازمة. إليك كيفية القيام بذلك:

### افتح مشروعك

قم بتشغيل Visual Studio وافتح المشروع الذي تريد تنفيذ تدوير النص فيه في PDF.

### إضافة مرجع

انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول، ثم حدد "إدارة حزم NuGet". 

### البحث عن Aspose.PDF وتثبيته

في مدير حزم NuGet، ابحث عن "Aspose.PDF" وثبّته. سيُمكّنك هذا الإجراء من الوصول إلى جميع الفئات والوظائف المتوفرة في مكتبة Aspose.PDF.

### استيراد مساحة الاسم

في أعلى ملف C# الخاص بك، تحتاج إلى استيراد مساحة اسم Aspose.PDF:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
```

وبهذا، تكون جاهزًا لبدء البرمجة!

حسنًا! لننتقل الآن إلى جوهر الموضوع - تدوير النص في ملف PDF. سنشرح الكود خطوة بخطوة.

## الخطوة 1: تهيئة المستند

الخطوة الأولى هي إنشاء نسخة جديدة من مستند PDF. هنا ستُخزَّن جميع أعمالك.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // حدد دليل المستند الخاص بك
Document pdfDocument = new Document(); // تهيئة كائن المستند
```
هنا، نحدد دليلًا للمستند وننشئ كائن مستند جديدًا. سيُستخدم هذا الكائن كحاوية لملف PDF.

## الخطوة 2: الحصول على صفحة معينة

الآن، دعنا نضيف صفحة حيث سنقوم بتدوير النص:

```csharp
Page pdfPage = (Page)pdfDocument.Pages.Add(); // احصل على صفحة معينة
```
يضيف هذا السطر صفحة جديدة إلى ملف PDF ويسمح لنا ببدء إضافة المحتوى إليه.

## الخطوة 3: إنشاء فقرة نصية

بعد ذلك، دعنا ننشئ فقرة حيث سنضيف أجزاء النص:

```csharp
TextParagraph paragraph = new TextParagraph();
paragraph.Position = new Position(200, 600); // تعيين موضع الفقرة
```
هنا، نُنشئ فقرة نصية ونحدد موقعها في الصفحة. تُحدد الإحداثيات (٢٠٠، ٦٠٠) مكان بداية الفقرة في الصفحة.

## الخطوة 4: إنشاء أجزاء نصية 

الآن يأتي الجزء الممتع: إنشاء شظايا النص! سننشئ ثلاثة شظايا نصية، اثنان منها سيكونان قابلين للدوران.

### 4.1: إنشاء جزء نصي مُدار

```csharp
TextFragment textFragment1 = new TextFragment("rotated text");
textFragment1.TextState.FontSize = 12;
textFragment1.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment1.TextState.Rotation = 45; // ضبط الدوران
```
هنا، نُنشئ أول جزء نصي يحمل اسم "نص مُدار". نُحدد حجم الخط ونوعه، ثم نُطبق تدويرًا بمقدار 45 درجة.

### 4.2: إنشاء جزء النص الرئيسي

الآن، دعونا نضيف جزء النص الرئيسي.

```csharp
TextFragment textFragment2 = new TextFragment("main text");
textFragment2.TextState.FontSize = 12;
textFragment2.TextState.Font = FontRepository.FindFont("TimesNewRoman");
```
ستبقى هذه القطعة دون تدوير وستكون بمثابة النص الرئيسي في الفقرة.

### 4.3: إنشاء جزء نصي مُدار آخر

وأخيرًا، سنقوم بإنشاء جزء نصي مدور آخر.

```csharp
TextFragment textFragment3 = new TextFragment("another rotated text");
textFragment3.TextState.FontSize = 12;
textFragment3.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment3.TextState.Rotation = -45; // ضبط الدوران
```
مثل القطعة الأولى، تتميز هذه القطعة بدوران بمقدار -45 درجة، مما يضيف تباينًا بصريًا مثيرًا للاهتمام.

## الخطوة 5: إضافة أجزاء نصية إلى الفقرة

الآن، حان الوقت لإضافة كل هذه الأجزاء النصية إلى الفقرة التي أنشأناها سابقًا:

```csharp
paragraph.AppendLine(textFragment1);
paragraph.AppendLine(textFragment2);
paragraph.AppendLine(textFragment3);
```
نحن ببساطة نضيف كل جزء من النص إلى فقرتنا. `AppendLine` تضمن الطريقة أن يتم تكديس كل جزء من النص عموديًا.

## الخطوة 6: إنشاء كائن TextBuilder

بعد ذلك، سنستخدم TextBuilder لإضافة فقرتنا إلى صفحة PDF:

```csharp
TextBuilder textBuilder = new TextBuilder(pdfPage);
textBuilder.AppendParagraph(paragraph); // إضافة فقرة النص إلى صفحة PDF
```
يعمل كائن TextBuilder كأداة لتطبيق الفقرة على صفحة PDF المحددة.

## الخطوة 7: حفظ المستند

بعد كل هذا العمل الشاق، حان الوقت لحفظ المستند ورؤية ما أنشأناه!

```csharp
pdfDocument.Save(dataDir + "TextFragmentTests_Rotated2_out.pdf");
```
يحفظ هذا السطر المستند في الدليل المحدد باسم "TextFragmentTests_Rotated2_out.pdf". 

وفويلا! لديك الآن ملف PDF بنص مُدوّر!

## خاتمة

يُمكن أن يُضفي تدوير النص في ملف PDF لمسةً إبداعيةً وجاذبيةً كبيرةً على مستنداتك. مع Aspose.PDF لـ .NET، يُمكنك تنفيذه وتخصيصه بسهولةٍ تامةٍ ليناسب احتياجات تصميمك. باتباع هذا الدليل المُفصّل، ستتعلم كيفية إنشاء نص مُدور داخل ملف PDF، مما يُتيح إمكانياتٍ جديدةً لعرض المعلومات بطريقةٍ جذابة. 

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة قوية تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وتحويلها مباشرة داخل تطبيقات .NET.

### كيف أقوم بتثبيت Aspose.PDF في مشروعي؟
يمكنك تثبيت Aspose.PDF عبر NuGet Package Manager في Visual Studio أو عن طريق تنزيله من  [صفحة تنزيلات Aspose](https://releases.aspose.com/pdf/net/).

### هل يمكنني استخدام Aspose.PDF مجانًا؟
نعم، يُقدّم Aspose.PDF نسخة تجريبية مجانية. يمكنك البدء بـ [نسخة تجريبية مجانية](https://releases.aspose.com/) واستكشاف ميزاته.

### هل يتوفر الدعم لـ Aspose.PDF؟
بالتأكيد! يمكنك التواصل معنا [دعم Aspose](https://forum.aspose.com/c/pdf/10) للحصول على المساعدة بشأن أي مشكلات تواجهها.

### كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.PDF؟
يمكنك شراء ترخيص مؤقت من [موقع Aspose](https://purchase.aspose.com/temporary-license/) لتجربة الميزات الكاملة للمكتبة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}