---
"description": "تعرف على كيفية إضافة صورة وأرقام الصفحات إلى رأس وتذييل ملف PDF الخاص بك باستخدام Aspose.PDF لـ .NET في هذا البرنامج التعليمي خطوة بخطوة."
"linktitle": "الصورة ورقم الصفحة في قسم الرأس والتذييل"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "الصورة ورقم الصفحة في قسم الرأس والتذييل"
"url": "/ar/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# الصورة ورقم الصفحة في قسم الرأس والتذييل

## مقدمة

عند إنشاء مستندات PDF احترافية، يُعدّ التحكم في التفاصيل الدقيقة، مثل الرؤوس والتذييلات، أمرًا بالغ الأهمية. هل ترغب في أن تبدو مستنداتك أنيقة ومنظمة؟ مع Aspose.PDF لـ .NET، يمكنك إضافة الصور وأرقام الصفحات بسلاسة إلى أقسام الرؤوس والتذييلات في مستندك. في هذا البرنامج التعليمي، سنرشدك خلال كل خطوة، مما يُسهّل عليك اتباعها.

## المتطلبات الأساسية

قبل الخوض في تفاصيل هذا البرنامج التعليمي، تأكد من أنك قمت بما يلي:

1. إطار عمل .NET: يجب تثبيت أي إصدار من إطار عمل .NET على جهاز الكمبيوتر الخاص بك. إذا لم يكن لديك، يمكنك تنزيله بسهولة من موقع Microsoft.
2. Aspose.PDF لـ .NET: بما أننا سنستخدم Aspose.PDF، فتأكد من تثبيته في مشروعك. يمكنك تنزيل نسخة تجريبية. [هنا](https://releases.aspose.com/pdf/net/).
3. المعرفة الأساسية بلغة C#: إن الإلمام ببرمجة C# الأساسية سوف يساعدك بالتأكيد على فهم الكود دون الكثير من المتاعب.
4. ملف صورة: ستحتاج إلى صورة ترغب في وضعها في رأس مستند PDF، مثل شعار. احفظها في مجلد يسهل الوصول إليه. 
5. IDE: استخدم بيئة التطوير المتكاملة (IDE) حسب اختيارك، مثل Visual Studio، للعمل مع مشروع .NET الخاص بك.

بمجرد إعداد المتطلبات الأساسية، ستكون جاهزًا لإنشاء ملف PDF رائع!

## استيراد الحزم

لبدء استخدام Aspose.PDF لـ .NET، عليك استيراد مساحات الأسماء اللازمة. في أعلى ملف C#، أضف:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Image;
```

ستوفر لك هذه المساحات الاسمية إمكانية الوصول إلى الفئات اللازمة للتعامل مع ملفات PDF.

الآن، لنبدأ العمل الفعلي! اتبع هذه الخطوات لإنشاء مستند PDF، مع إضافة صورة في الرأس وأرقام الصفحات في التذييل.

## الخطوة 1: تعيين دليل المستندات الخاص بك

كل مشروع ناجح يبدأ بالتنظيم. حدد مجلد المستندات الذي ستحفظ فيه ملفاتك ومكان حفظ صورك. إليك كيفية القيام بذلك:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

تذكر أن تستبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي تريد حفظ ملف PDF الخاص بك فيه والمكان الذي توجد فيه صورتك.

## الخطوة 2: إنشاء مستند PDF جديد

بعد ذلك، سنقوم بإنشاء مستند PDF جديد حيث سيحدث كل السحر:

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

في هذه المرحلة، أنشأتَ مستند PDF فارغًا. أليس هذا مثيرًا للاهتمام؟

## الخطوة 3: إضافة صفحة إلى المستند

ملف PDF عبارة عن صفحات. لنُضِف صفحة جديدة إلى مستندنا باستخدام:

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

الآن أصبح لديك لوحة قماشية يمكنك البدء في التصميم عليها!

## الخطوة 4: إنشاء قسم الرأس

سيحتوي رأس الصفحة على الصورة (مثل الشعار) التي تريد عرضها. أنشئ قسم الرأس بالكود التالي:

```csharp
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
page.Header = header;
```

الآن أصبح لديك رأس يمكنك تخصيصه!

## الخطوة 5: إضافة صورة إلى العنوان

الآن وصلنا إلى الجزء الممتع! عليك إضافة الصورة إلى رأس الصفحة. أولًا، أنشئ كائن صورة:

```csharp
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
```

تعيين مسار الملف الخاص بصورتك:

```csharp
image1.File = dataDir + "aspose-logo.jpg";
```

وأخيرًا، أضف الصورة إلى رأس الصفحة:

```csharp
header.Paragraphs.Add(image1);
```

تهانينا! لقد أضفت للتو صورةً إلى رأس ملف PDF الخاص بك.

## الخطوة 6: إنشاء قسم التذييل

الآن لنبدأ بالتذييل. كما في عملية الرأس، أنشئ كائن تذييل:

```csharp
Aspose.Pdf.HeaderFooter footer = new Aspose.Pdf.HeaderFooter();
page.Footer = footer;
```

هذا هو المكان الذي ستضع فيه رقم صفحتك. 

## الخطوة 7: إضافة نص إلى التذييل

إنشاء جزء نصي يحتوي على رقم الصفحة:

```csharp
Aspose.Pdf.Text.TextFragment txt = new Aspose.Pdf.Text.TextFragment("Page: ($p of $P ) ");
```

ثم أضف هذا الجزء من النص إلى التذييل:

```csharp
footer.Paragraphs.Add(txt);
```

هل رأيتَ كم كان ذلك سهلاً؟ لقد حدّدتَ رقم صفحتك ديناميكيًا!

## الخطوة 8: حفظ مستند PDF

الخطوة الأخيرة في مغامرتنا هي حفظ المستند. استخدم هذا الأمر لحفظ ملف PDF الذي أنشأته حديثًا:

```csharp
doc.Save(dataDir + "ImageAndPageNumberInHeaderFooter_out.pdf");
```

وهكذا، أصبح ملف PDF الخاص بك جاهزًا ومحملًا بصورة رأسية وأرقام الصفحات في التذييل!

## خاتمة

وها أنت ذا! لقد أنشأتَ للتو ملف PDF بصورة في الرأس وأرقام صفحات ديناميكية في التذييل باستخدام Aspose.PDF لـ .NET. من المذهل كيف يُمكن لبضعة أسطر من التعليمات البرمجية أن تُنتج هذا القدر من الدقة. سواءً كان ذلك لتقرير شركة أو مستندًا شخصيًا، فإن إضافة هذه العناصر تُغيّر طابع ملف PDF واحترافيته.

## الأسئلة الشائعة

### هل يمكنني استخدام Aspose.PDF على أي منصة .NET؟
نعم، يدعم Aspose.PDF لـ .NET منصات .NET المتعددة بما في ذلك .NET Framework، و.NET Core، والمزيد.

### هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.PDF؟
بالتأكيد! يمكنك تنزيل نسخة تجريبية مجانية [هنا](https://releases.aspose.com/).

### ما هي تنسيقات الصور المدعومة للرؤوس؟
يدعم Aspose.PDF تنسيقات الصور الأكثر شيوعًا مثل JPG وPNG وBMP للرؤوس والتذييلات.

### هل يمكنني تخصيص تنسيق رقم الصفحة؟
نعم، يمكنك بسهولة تخصيص نص التذييل وتنسيقه وفقًا لاحتياجاتك.

### هل الدعم الفني متوفر؟
نعم، تقدم Aspose دعمًا متخصصًا عبر منتداها. يمكنك التواصل للحصول على المساعدة. [هنا](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}