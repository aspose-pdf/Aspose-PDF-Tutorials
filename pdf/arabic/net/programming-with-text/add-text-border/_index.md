---
"description": "تعرّف على كيفية إضافة إطار نصي إلى ملف PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل التفصيلي. حسّن جودة مستندات PDF الخاصة بك."
"linktitle": "إضافة حدود نصية في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة حدود نصية في ملف PDF"
"url": "/ar/net/programming-with-text/add-text-border/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة حدود نصية في ملف PDF

## مقدمة

أصبح إنشاء مستندات PDF ومعالجتها مهارة أساسية في عالمنا الرقمي اليوم. سواء كنت تُنشئ تقارير أو فواتير أو أي نوع آخر من المستندات، فإن التحكم في كيفية ظهور النص يُحدث فرقًا كبيرًا. ومن التحسينات التي قد ترغب في تطبيقها إضافة إطار حول النص في ملف PDF. في هذا الدليل، سنشرح لك خطوات إضافة إطار نصي في ملف PDF باستخدام مكتبة Aspose.PDF لـ .NET. هيا بنا!

## المتطلبات الأساسية

قبل أن نبدأ، هناك بعض الأمور التي يجب عليك إعدادها. لا تقلق، الأمر بسيط جدًا!

1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. ستكون هذه بيئة التطوير التي ستكتب فيها وتُشغّل شفرتك البرمجية.
2. Aspose.PDF لـ .NET: ستحتاج إلى تنزيل مكتبة Aspose.PDF وتثبيتها. يمكنك الحصول عليها من [صفحة تنزيل Aspose PDF لـ .NET](https://releases.aspose.com/pdf/net/)إذا كنت تريد تجربته أولاً، يمكنك أيضًا الحصول على [تجربة مجانية هنا](https://releases.aspose.com/).
3. المعرفة الأساسية للغة البرمجة C#: إن الفهم الأساسي للغة البرمجة C# سيساعدك على متابعة الأمثلة بسهولة.
4. .NET Framework: تأكد من تثبيت .NET Framework وإعداده في مشروعك.

بمجرد توفر هذه المتطلبات الأساسية لديك، ستكون جاهزًا لبدء الترميز!

## استيراد الحزم

بعد أن انتهينا من إعداد كل شيء، لنستورد الحزم اللازمة لاستخدام Aspose.PDF في مشروعنا. يمكنك القيام بذلك بإضافة توجيهات الاستخدام التالية في أعلى ملف C#:

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

```

ستتيح لك هذه المساحات الاسمية العمل مع مستندات PDF وأجزاء النص بشكل فعال. 

الآن، لنُقسّم عملية إضافة إطار نصي إلى خطوات مُفصّلة. سنشرح كل خطوة لتفهم ما يحدث بالضبط.

## الخطوة 1: إعداد المستند

أولاً، علينا إنشاء مستند PDF جديد. هنا ستُنجز مهمتنا.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// إنشاء كائن مستند جديد 
Document pdfDocument = new Document();
```

في هذه الخطوة، نحدد المجلد الذي نريد حفظ ملف PDF فيه. ثم ننشئ نسخة جديدة من `Document` الفئة التي تمثل مستند PDF الخاص بنا.

## الخطوة 2: إضافة صفحة جديدة

بعد ذلك، نحتاج إلى إضافة صفحة إلى مستندنا. تخيل هذا كإضافة لوحة فارغة لوضع النص فيها.

```csharp
// احصل على صفحة معينة
Page pdfPage = (Page)pdfDocument.Pages.Add();
```

هنا نسميها `Add()` الطريقة على `Pages` مجموعة من `pdfDocument` الكائن. يؤدي هذا إلى إضافة صفحة جديدة إلى المستند، ونقوم بتخزين مرجع لها في `pdfPage` عامل.

## الخطوة 3: إنشاء جزء نصي

الآن، لنُنشئ النص الذي نريد عرضه في ملف PDF. هنا نُحدد محتوى جزء النص.

```csharp
// إنشاء جزء نصي
TextFragment textFragment = new TextFragment("main text");
textFragment.Position = new Position(100, 600);
```

في هذا الكود نقوم بإنشاء كود جديد `TextFragment` الكائن الذي يحتوي على النص "النص الرئيسي". كما نحدد موقعه على الصفحة باستخدام `Position` الصف. تحدد الإحداثيات (100، 600) مكان وضع النص على الصفحة.

## الخطوة 4: تعيين خصائص النص

بعد ذلك، سنُخصّص نصّنا لجعله جذابًا بصريًا. يشمل ذلك ضبط حجم الخط ونوعه ولون الخلفية ولون المقدمة.

```csharp
// تعيين خصائص النص
textFragment.TextState.FontSize = 12;
textFragment.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment.TextState.BackgroundColor = Aspose.Pdf.Color.LightGray;
textFragment.TextState.ForegroundColor = Aspose.Pdf.Color.Red;
```

هنا، حدّدنا حجم الخط إلى ١٢، واستخدمنا خط "Times New Roman"، وطبّقنا لون خلفية رمادي فاتح مع نص أحمر. تُحسّن هذه الخصائص وضوح النص.

## الخطوة 5: تعيين لون الحدود

الآن وصلنا إلى الجزء المثير للاهتمام، وهو إضافة حدود حول النص الخاص بنا!

```csharp
// تعيين خاصية StrokingColor لرسم الحدود (الرسم) حول مستطيل النص
textFragment.TextState.StrokingColor = Aspose.Pdf.Color.DarkRed;
```

في هذه الخطوة، نحدد لون الإطار الذي نريد رسمه حول النص. هنا، اخترنا اللون الأحمر الداكن.

## الخطوة 6: تمكين حدود مستطيل النص

لكي نرسم الحدود حول النص فعليًا، نحتاج إلى تمكين `DrawTextRectangleBorder` ملكية.

```csharp
// تعيين قيمة خاصية DrawTextRectangleBorder إلى true
textFragment.TextState.DrawTextRectangleBorder = true;
```

من خلال تعيين هذه الخاصية إلى `true`، نطلب من Aspose.PDF رسم الحدود حول مستطيل النص استنادًا إلى لون التحديد المحدد.

## الخطوة 7: إضافة جزء النص إلى الصفحة

الآن بعد أن أصبح لدينا جزء النص جاهزًا مع تعيين جميع الخصائص، فقد حان الوقت لإضافته إلى الصفحة.

```csharp
TextBuilder tb = new TextBuilder(pdfPage);
tb.AppendText(textFragment);
```

هنا، نقوم بإنشاء `TextBuilder` الشيء المرتبط بنا `pdfPage`. ثم نستخدم `AppendText` طريقة إضافة `textFragment` الى الصفحة. 

## الخطوة 8: حفظ المستند

أخيرًا، علينا حفظ مستند PDF في المجلد المحدد. هذه هي لحظة الحقيقة!

```csharp
// حفظ المستند
pdfDocument.Save(dataDir + "PDFWithTextBorder_out.pdf");
```

في هذه الخطوة، نسميها `Save` الطريقة على موقعنا `pdfDocument` الكائن، مع تحديد المسار الذي نريد حفظ الملف فيه. بعد تشغيل الكود، ستجد ملف PDF الذي أنشأته حديثًا مع إطار النص في الدليل المحدد!

## خاتمة

وها قد انتهيت! لقد نجحت في إضافة إطار نصي إلى ملف PDF باستخدام Aspose.PDF لـ .NET. هذه الميزة البسيطة والفعّالة تُحسّن بشكل كبير من سهولة قراءة مستندات PDF وجمالياتها. سواء كنت تُنشئ تقارير أو كتيبات أو أي نوع آخر من الوثائق، فإن معرفة كيفية التعامل مع تنسيق النص تُعدّ أمرًا مفيدًا.

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة قوية تسمح للمطورين بإنشاء مستندات PDF ومعالجتها ومعالجتها برمجيًا باستخدام إطار عمل .NET.

### هل يمكنني تجربة Aspose.PDF مجانًا؟
نعم! تقدم Aspose [نسخة تجريبية مجانية](https://releases.aspose.com/) من مكتبة PDF الخاصة بهم، مما يسمح لك باختبار ميزاتها قبل إجراء عملية شراء.

### كيف يمكنني شراء Aspose.PDF لـ .NET؟
يمكنك شراء Aspose.PDF لـ .NET مباشرة من موقعهم [صفحة الشراء](https://purchase.aspose.com/buy).

### هل يتوفر الدعم لـ Aspose.PDF؟
بالتأكيد! يمكنك الحصول على الدعم بزيارة [منتدى دعم Aspose](https://forum.aspose.com/c/pdf/10).

### ماذا لو كنت بحاجة إلى ترخيص مؤقت؟
يوفر Aspose [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) خيار للمطورين الذين يحتاجون إلى تقييم المكتبة لفترة محدودة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}