---
"description": "تعرّف على كيفية إضافة عناوين مختلفة إلى ملفات PDF باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة لتخصيص ملفات PDF."
"linktitle": "إضافة عناوين مختلفة في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة عناوين مختلفة في ملف PDF"
"url": "/ar/net/programming-with-stamps-and-watermarks/adding-different-headers/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة عناوين مختلفة في ملف PDF

## مقدمة

في هذه المقالة، سنتعمق في استخدام Aspose.PDF لـ .NET لإضافة عناوين مختلفة إلى ملفات PDF. سواءً كنت مطورًا محترفًا أو مبتدئًا في عالم معالجة ملفات PDF، سيرشدك هذا الدليل خطوة بخطوة. هل أنت مستعد؟ هيا بنا!

## المتطلبات الأساسية

قبل أن ننتقل إلى جانب الترميز، هناك بعض الأشياء التي ستحتاج إلى التأكد من وجودها لديك حتى تتمكن من متابعة هذا البرنامج التعليمي:

- Visual Studio: تأكد من تثبيت Visual Studio على جهاز الكمبيوتر الخاص بك، حيث سنستخدمه لتشغيل كود .NET الخاص بنا.
- مكتبة Aspose.PDF: ستحتاج إلى مكتبة Aspose.PDF. يمكنك تنزيلها من [هنا](https://releases.aspose.com/pdf/net/)إذا كنت جديدًا عليه، فقد ترغب في تجربة [نسخة تجريبية مجانية](https://releases.aspose.com/).
- .NET Framework: تأكد من تثبيت إصدار متوافق من .NET Framework لتشغيل مكتبة Aspose.PDF.

من خلال توفير هذه المتطلبات الأساسية، ستكون جاهزًا لإنشاء ملف PDF الخاص بك مع رؤوس قابلة للتخصيص!

## استيراد الحزم

بعد اكتمال الإعداد، لنبدأ باستيراد الحزم اللازمة. هذه خطوة بالغة الأهمية، إذ تتيح لنا الاستفادة من جميع الميزات الرائعة التي يقدمها Aspose.PDF.

إليك كيفية استيراد مساحة اسم Aspose.PDF المطلوبة في مشروع C# الخاص بك:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

تأكد من أن هذه العبارات موجودة في أعلى ملف C# الخاص بك حتى تتمكن من الوصول إلى جميع الفئات والطرق التي سنستخدمها.

## الخطوة 1: تحديد المسار إلى مستندك

أولاً، لنحدد مسار مجلد مستندات PDF. هنا سنتمكن من الوصول إلى ملف PDF وحفظ الملف المُحدّث. استبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي على نظامك.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## الخطوة 2: افتح مستند المصدر الخاص بك

بعد أن حددنا دليل المستندات، الخطوة التالية هي فتح ملف PDF الذي نريد إضافة رؤوس إليه. سنستخدم `Aspose.Pdf.Document` الصف لهذا.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document(dataDir + "AddingDifferentHeaders.pdf");
```

## الخطوة 3: إنشاء طوابع نصية

لنُنشئ ثلاثة طوابع نصية مختلفة لنستخدمها كعناوين. طوابع النص أشبه بالملصقات! يُمكننا تخصيصها كما نُريد.

```csharp
Aspose.Pdf.TextStamp stamp1 = new Aspose.Pdf.TextStamp("Header 1");
Aspose.Pdf.TextStamp stamp2 = new Aspose.Pdf.TextStamp("Header 2");
Aspose.Pdf.TextStamp stamp3 = new Aspose.Pdf.TextStamp("Header 3");
```

## الخطوة 4: تخصيص العنوان الأول

الآن، حان وقت تخصيص رأس الصفحة الأول. سنضبط محاذاته ونمطه ولونه وحجمه لجعله مميزًا.

```csharp
// تعيين محاذاة الطوابع
stamp1.VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
stamp1.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;

// تفاصيل التنسيق
stamp1.TextState.FontStyle = FontStyles.Bold;
stamp1.TextState.ForegroundColor = Color.Red;
stamp1.TextState.FontSize = 14;
```

## الخطوة 5: تخصيص العنوان الثاني

الآن، لنُركز على العنوان الثاني. سنُعدِّل أيضًا مستوى تكبيره، مما يُتيح تكبير النص أو تصغيره في ملف PDF.

```csharp
stamp2.VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
stamp2.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
stamp2.Zoom = 10;
```

## الخطوة 6: تخصيص العنوان الثالث

بالنسبة لعنواننا الثالث، سنضيف لمسةً مميزةً بتدويره بزاوية وتغيير لون خلفيته إلى الوردي. إليك الطريقة:

```csharp
stamp3.VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
stamp3.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
stamp3.RotateAngle = 35;
stamp3.TextState.BackgroundColor = Color.Pink;
stamp3.TextState.Font = FontRepository.FindFont("Verdana");
```

## الخطوة 7: إضافة الطوابع إلى صفحات PDF

بعد تجهيز طوابعنا، حان وقت وضعها على الصفحات المخصصة. تخيل الأمر كما لو أنك تضع ملصقاتك على صفحات مختلفة من سجل القصاصات!

```csharp
doc.Pages[1].AddStamp(stamp1); // إضافة الختم الأول
doc.Pages[2].AddStamp(stamp2); // إضافة الطابع الثاني
doc.Pages[3].AddStamp(stamp3); // إضافة الطابع الثالث
```

## الخطوة 8: حفظ المستند المحدث

الخطوة الأخيرة هي حفظ التغييرات. كما هو الحال في حفظ عملك في محرر مستندات، نحتاج إلى حفظ ملف PDF المعدّل حديثًا.

```csharp
dataDir = dataDir + "multiheader_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nDifferent headers added successfully.\nFile saved at " + dataDir);
```

هذا كل شيء! لقد نجحت في إضافة عناوين مختلفة إلى ملف PDF الخاص بك. 

## خاتمة

في هذا البرنامج التعليمي، تناولنا كيفية استخدام Aspose.PDF لـ .NET لإضافة عناوين مخصصة لصفحات متعددة في مستند PDF. ببضع جمل برمجية بسيطة، يمكنك بسهولة جعل مستنداتك أكثر احترافية وجاذبية بصريًا. 

## الأسئلة الشائعة

### هل يمكنني تغيير الخط في العنوان؟  
نعم يمكنك ذلك! تعديل `stamp.TextState.Font` الخاصية لتطبيق أي خط من الخطوط المتوفرة في Aspose.

### هل هناك حد لعدد العناوين التي يمكنني إضافتها؟  
لا، يمكنك إضافة عدد كبير من الرؤوس كما تريد؛ فقط تأكد من إنشاء طابع مطابق لكل منها.

### هل يمكنني استخدام هذه الطريقة لإضافة الصور كعناوين؟  
يركز هذا البرنامج التعليمي حاليًا على طوابع النص، ولكن Aspose.PDF يسمح أيضًا بإضافة طوابع الصور.

### كيف يمكنني محاذاة رأس الصفحة عموديًا في المنتصف؟  
يمكنك استخدام `VerticalAlignment.Center` ولتحقيق ذلك، يجب التأكد من محاذاته بشكل مثالي.

### أين يمكنني العثور على مزيد من المعلومات حول Aspose.PDF؟  
يمكنك التحقق من [التوثيق](https://reference.aspose.com/pdf/net/) للحصول على إرشادات وأمثلة مفصلة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}