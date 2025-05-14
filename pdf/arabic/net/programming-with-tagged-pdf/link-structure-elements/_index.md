---
"description": "تعرّف على كيفية إنشاء عناصر بنية الروابط في ملف PDF باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة لإضافة روابط وصور سهلة الوصول، والتحقق من التوافق."
"linktitle": "عناصر بنية الرابط"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "عناصر بنية الرابط"
"url": "/ar/net/programming-with-tagged-pdf/link-structure-elements/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# عناصر بنية الرابط

## مقدمة

يُعد إنشاء عناصر بنية الروابط وإدارتها داخل ملف PDF أمرًا بالغ الأهمية للمستندات التي تتطلب سهولة الوصول والتنقل السلس. في هذا البرنامج التعليمي، سنشرح لك كيفية القيام بذلك باستخدام Aspose.PDF لـ .NET. إذا كنت جديدًا على Aspose.PDF أو التعامل مع ملفات PDF بشكل عام، فلا تقلق. سأشرح كل خطوة بالتفصيل لتتمكن من متابعتها بسهولة!

## المتطلبات الأساسية  

قبل أن نتعمق في البرمجة، دعونا نوضح بعض الأمور أولاً. هذه هي المتطلبات الأساسية لضمان تجربة تطوير سلسة.

1. Aspose.PDF لـ .NET: يمكنك تنزيل الإصدار الأحدث [هنا](https://releases.aspose.com/pdf/net/).
2. بيئة تطوير .NET: سواء كان Visual Studio أو أي IDE متوافق مع .NET، تأكد من تثبيته وتجهيزه.
3. ترخيص Aspose: يمكنك استخدام النسخة التجريبية المجانية من Aspose.PDF [هنا](https://releases.aspose.com/) أو الحصول على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/).
4. المعرفة الأساسية بلغة C#: سنعمل مع بعض أكواد C#، لذا فإن فهم الأساسيات سيجعل الأمور أسهل كثيرًا.

## استيراد الحزم

ستحتاج إلى استيراد بعض الحزم قبل كتابة شيفرة عناصر بنية الرابط. ابدأ بالرجوع إلى مكتبات Aspose.PDF اللازمة في مشروعك:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

تتيح لنا هذه الواردات العمل مع مستندات PDF وإضافة العلامات وإدارة عناصر الهيكل.

سنقوم الآن بإنشاء مستند PDF يحتوي على أنواع مختلفة من هياكل الروابط، وسيتم تقسيم كل خطوة لمساعدتك على فهم العملية بشكل كامل.

## الخطوة 1: تهيئة المستند  

لنبدأ بإنشاء مستند PDF جديد وإعداد محتوى مميز لسهولة الوصول إليه.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "LinkStructureElements_Output.pdf";
string logFile = dataDir + "46035_log.xml";
string imgFile = dataDir + "google-icon-512.png";

// إنشاء مستند PDF جديد
Document document = new Document(); 

// استرداد واجهة TaggedContent
ITaggedContent taggedContent = document.TaggedContent;
```
  
هنا، نقوم بتهيئة `Document` الكائن الذي يمثل ملف PDF الخاص بنا. كما نسترد `TaggedContent` الواجهة، التي تسمح لنا بإضافة عناصر هيكلية مثل الفقرات والروابط والصور.

## الخطوة 2: تعيين العنوان واللغة  

يجب أن يحتوي كل ملف PDF على عنوان وإعدادات لغة، خاصة إذا كنت تهدف إلى التوافق مع معايير PDF/UA.

```csharp
// تعيين عنوان المستند واللغة
taggedContent.SetTitle("Link Elements Example");
taggedContent.SetLanguage("en-US");
```
  
تضمن هذه الخطوة أن يكون لملف PDF الخاص بك عنوان ذو معنى وتضبط اللغة على الإنجليزية (`en-US`يعد هذا أمرًا بالغ الأهمية لإمكانية الوصول ويضمن أن تتمكن برامج قراءة الشاشة أو التقنيات المساعدة الأخرى من تفسير مستندك بشكل صحيح.

## الخطوة 3: إنشاء الفقرات وإضافتها  

في هذه الخطوة، سنضيف فقرات لحمل عناصر الرابط الخاصة بنا.

```csharp
// إنشاء العنصر الجذر
StructureElement rootElement = taggedContent.RootElement;

// إنشاء فقرة وإضافتها إلى العنصر الجذر
ParagraphElement p1 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p1);
```
  
نُنشئ عنصر بنية جذرية، وهو في الأساس الحاوية العليا لجميع العناصر الأخرى. ثم نُنشئ فقرة (`p1`) وإضافته إلى عنصر الجذر.

## الخطوة 4: إضافة رابط بسيط  

الآن دعونا نضيف رابطًا أساسيًا يشير إلى Google.

```csharp
// إنشاء عنصر رابط وإضافته إلى الفقرة
LinkElement link1 = taggedContent.CreateLinkElement();
p1.AppendChild(link1);

// تعيين ارتباط تشعبي ونص للرابط
link1.Hyperlink = new WebHyperlink("http://google.com");
link1.SetText("Google");
link1.AlternateDescriptions = "Link to Google";
```
  
في هذه الخطوة، أنشأنا عنصر رابط، وضبطنا رابطه التشعبي إلى "http://google.com"، وأضفنا نصًا ("Google") للرابط. كما أضفنا وصفًا بديلًا لضمان سهولة الوصول.

## الخطوة 5: إضافة رابط مع Spans  

يمكننا أيضًا إنشاء روابط بامتدادات نصية مختلفة.

```csharp
// إنشاء فقرة أخرى
ParagraphElement p2 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p2);

// إنشاء رابط باستخدام عنصر span
LinkElement link2 = taggedContent.CreateLinkElement();
p2.AppendChild(link2);
link2.Hyperlink = new WebHyperlink("http://google.com");

SpanElement span2 = taggedContent.CreateSpanElement();
span2.SetText("Google");
link2.AppendChild(span2);

link2.AlternateDescriptions = "Link to Google";
```
  
هنا، استخدمنا عنصر span لإحاطة جزء من النص داخل الرابط، مما يسمح لنا بتخصيص كيفية ظهور أجزاء معينة من الرابط.

## الخطوة 6: رابط متعدد الأسطر  

ماذا لو كان نص الرابط طويلاً جدًا؟ لا تقلق، يمكنك تقسيمه إلى عدة أسطر.

```csharp
ParagraphElement p4 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p4);

LinkElement link4 = taggedContent.CreateLinkElement();
p4.AppendChild(link4);
link4.Hyperlink = new WebHyperlink("http://google.com");
link4.SetText("The multiline link: Google Google Google Google Google...");
link4.AlternateDescriptions = "Link to Google (multiline)";
```
  
في هذه الحالة، قمنا بإنشاء رابط متعدد السطور ببساطة عن طريق تعيين قيمة نصية طويلة، وسيتم التفاف النص تلقائيًا عبر أسطر متعددة.

## الخطوة 7: إضافة صورة إلى الرابط  

وأخيرًا، يمكنك أيضًا إضافة صور داخل الرابط.

```csharp
// إنشاء فقرة جديدة وعنصر رابط
ParagraphElement p5 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p5);

LinkElement link5 = taggedContent.CreateLinkElement();
p5.AppendChild(link5);
link5.Hyperlink = new WebHyperlink("http://google.com");

// أضف صورة إلى الرابط
FigureElement figure5 = taggedContent.CreateFigureElement();
figure5.SetImage(imgFile, 1200);
figure5.AlternativeText = "Google icon";
link5.AppendChild(figure5);

link5.AlternateDescriptions = "Link to Google";
```
  
توضح هذه الخطوة كيفية تحسين روابطك باستخدام صورة. في هذه الحالة، أضفنا أيقونة جوجل داخل الرابط. كما حرصنا على سهولة الوصول من خلال إضافة نص بديل للصورة.

## الخطوة 8: التحقق من صحة ملف PDF للتأكد من توافقه  

إذا كنت تهدف إلى التوافق مع PDF/UA (معيار إمكانية الوصول)، فمن الأفضل التحقق من صحة مستندك.

```csharp
// حفظ مستند PDF
document.Save(outFile);

// التحقق من صحة المستند للتوافق مع PDF/UA
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```
  
لقد قمنا بحفظ المستند وتحققنا من صحته وفقًا لمعيار PDF/UA، والذي يضمن أن ملف PDF يلبي متطلبات إمكانية الوصول.

## خاتمة  

في هذا البرنامج التعليمي، تناولنا كيفية إنشاء مستندات PDF منظمة باستخدام Aspose.PDF لـ .NET. بدءًا من إضافة روابط تشعبية أساسية وصولًا إلى هياكل أكثر تعقيدًا مثل الامتدادات والروابط متعددة الأسطر وحتى الصور، يوفر هذا الدليل أساسًا متينًا للتعامل مع عناصر الروابط في ملفات PDF. بفضل ميزة التوافق مع PDF/UA، أصبحت الآن جاهزًا لإنشاء ملفات PDF سهلة الوصول والتصفح.

## الأسئلة الشائعة

### هل يمكنني إضافة هياكل أكثر تعقيدًا مثل الجداول داخل الروابط؟  
لا، فالروابط مخصصة في المقام الأول للنصوص والصور، ولكن يمكنك تضمين عناصر معقدة بالقرب منها.

### هل التحقق من صحة PDF/UA إلزامي؟  
ليس دائمًا، ولكن يُنصح به بشدة إذا كنت مهتمًا بإمكانية الوصول.

### ماذا يحدث إذا كان مسار ملف الصورة غير صحيح؟  
لن يعرض المستند الصورة، وقد يتسبب في حدوث خطأ أثناء العرض.

### هل يمكنني تنسيق النص الموجود داخل الرابط؟  
نعم، يمكنك تطبيق أنماط النص باستخدام عناصر span.

### هل من الممكن إنشاء روابط داخلية للمستندات؟  
بالتأكيد! يمكنك ربط أقسام محددة داخل نفس المستند.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}