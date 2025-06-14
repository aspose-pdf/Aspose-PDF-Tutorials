---
"description": "تعرّف على كيفية تحديد تاريخ انتهاء الصلاحية لملفات PDF باستخدام Aspose.PDF لـ .NET. عزّز أمان مستنداتك بهذا الدليل المفصل."
"linktitle": "تعيين تاريخ انتهاء الصلاحية في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تعيين تاريخ انتهاء الصلاحية في ملف PDF"
"url": "/ar/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تعيين تاريخ انتهاء الصلاحية في ملف PDF

## مقدمة

في عصرنا الرقمي، أصبحت إدارة المستندات وتأمينها أكثر أهمية من أي وقت مضى. تخيل إرسال ملف PDF يصبح غير قابل للوصول تلقائيًا بعد تاريخ معين. يبدو الأمر سحريًا، أليس كذلك؟ مع Aspose.PDF لـ .NET، يمكنك بسهولة تحديد تاريخ انتهاء صلاحية ملفات PDF. هذه الميزة مفيدة بشكل خاص للمستندات الحساسة التي يجب تقييد الوصول إليها بعد فترة زمنية محددة. في هذا البرنامج التعليمي، سنشرح لك عملية تحديد تاريخ انتهاء الصلاحية في ملف PDF خطوة بخطوة. هيا، هيا بنا!

## المتطلبات الأساسية

قبل أن نبدأ، هناك بعض الأشياء التي تحتاج إلى وضعها في مكانها:

1. بيئة التطوير: تأكد من إعداد بيئة تطوير .NET لديك. قد تكون هذه البيئة Visual Studio أو أي بيئة تطوير متكاملة أخرى تدعم .NET.
2. Aspose.PDF لـ .NET: يجب تثبيت مكتبة Aspose.PDF. إذا لم تقم بذلك بعد، يمكنك تنزيلها من [هنا](https://releases.aspose.com/pdf/net/).
3. المعرفة الأساسية بلغة C#: يفترض هذا البرنامج التعليمي أن لديك فهمًا أساسيًا لبرمجة C#. إذا كنت جديدًا على C#، فلا تقلق! سنجعله بسيطًا ومباشرًا.

## استيراد الحزم

لبدء استخدام Aspose.PDF، عليك استيراد مساحات الأسماء اللازمة في مشروع C#. إليك كيفية القيام بذلك:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

توفر لك هذه المساحات الاسمية إمكانية الوصول إلى الوظائف الأساسية المطلوبة للعمل مع مستندات PDF في Aspose.PDF.

## الخطوة 1: إعداد دليل المستندات الخاص بك

أولاً، عليك تحديد مسار مجلد المستندات. هنا سيتم حفظ ملف PDF الناتج. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

يستبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي تريد حفظ ملف PDF فيه. الأمر أشبه بإخبار برنامجك: "مرحبًا، هذا هو المكان الذي أحفظ فيه ملفاتي!"

## الخطوة 2: إنشاء كائن المستند

بعد ذلك، ستحتاج إلى إنشاء مثيل جديد لـ `Document` هذه هي لوحتك التي ستنشئ عليها ملف PDF الخاص بك.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

فكر في `Document` كصفحة بيضاء. يمكنك إضافة محتوى إليها كما يحلو لك!

## الخطوة 3: إضافة صفحة إلى ملف PDF

بعد إعداد مستندك، حان الوقت لإضافة صفحة إليه. هنا سيُعرض محتواك.

```csharp
doc.Pages.Add();
```

لقد أنشأتَ للتو صفحةً جديدةً في ملف PDF الخاص بك. الأمر أشبه بإضافة صفحةٍ جديدةٍ إلى دفتر ملاحظاتك لتدوين أفكارك.

## الخطوة 4: إضافة نص إلى الصفحة

لنجعل هذه الصفحة أكثر تشويقًا بإضافة نص. سنضيف رسالة "مرحبًا بالعالم" البسيطة.

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

يضيف هذا السطر من التعليمات البرمجية جزءًا نصيًا إلى الصفحة الأولى من ملف PDF. يشبه الأمر كتابة عنوان في أعلى الصفحة!

## الخطوة 5: إنشاء JavaScript لتاريخ انتهاء الصلاحية

الآن يأتي الجزء الممتع! ستُنشئ إجراءً في جافا سكريبت للتحقق من تاريخ انتهاء صلاحية ملف PDF. إذا تجاوز التاريخ الحالي تاريخ انتهاء الصلاحية، ستظهر رسالة تنبيه للمستخدم.

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

وإليك ما يحدث:
- أنت تحدد سنة وشهر انتهاء الصلاحية.
- تحصل على تاريخ اليوم.
- قارن تاريخ اليوم مع تاريخ انتهاء الصلاحية.
- إذا كان تاريخ اليوم بعد تاريخ انتهاء الصلاحية، ستظهر رسالة!

## الخطوة 6: تعيين JavaScript كإجراء فتح PDF

الآن، عليك ضبط إجراء JavaScript لفتح مستند PDF. هذا يعني أن JavaScript سيعمل فور فتح ملف PDF.

```csharp
doc.OpenAction = javaScript;
```

هذا السطر يُوجِّه ملف PDF لتنفيذ شفرة جافا سكريبت عند فتحه. يشبه الأمر ضبط تذكير يُصدر صوتًا فور فتح التقويم!

## الخطوة 7: حفظ مستند PDF

وأخيرًا، حان الوقت لحفظ مستند PDF الخاص بك مع ميزة تاريخ انتهاء الصلاحية. 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

هذا السطر يحفظ ملف PDF الخاص بك في المجلد المحدد باسم "SetExpiryDate_out.pdf". يشبه وضع عملك الفني النهائي في إطار!

## خاتمة

وها أنت ذا! لقد أنشأتَ بنجاح ملف PDF بتاريخ انتهاء صلاحية باستخدام Aspose.PDF لـ .NET. لا تُحسّن هذه الميزة الأمان فحسب، بل تضمن أيضًا الحفاظ على المعلومات الحساسة تحت السيطرة. سواءً كنت تُرسل عقودًا أو تقارير أو أي مستندات مهمة أخرى، فإن تحديد تاريخ انتهاء الصلاحية يُمكن أن يُحدث فرقًا كبيرًا.

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة قوية تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وتحويلها في تطبيقات .NET.

### هل يمكنني استخدام Aspose.PDF مجانًا؟
نعم، يمكنك استخدام نسخة تجريبية مجانية من Aspose.PDF. يمكنك تنزيلها. [هنا](https://releases.aspose.com/).

### كيف يمكنني شراء Aspose.PDF؟
يمكنك شراء Aspose.PDF من خلال زيارة [صفحة الشراء](https://purchase.aspose.com/buy).

### ماذا لو كنت بحاجة إلى الدعم؟
إذا كان لديك أي أسئلة أو تحتاج إلى مساعدة، يمكنك زيارة [منتدى دعم Aspose](https://forum.aspose.com/c/pdf/10).

### هل يمكنني الحصول على ترخيص مؤقت لـ Aspose.PDF؟
نعم يمكنك طلب ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}