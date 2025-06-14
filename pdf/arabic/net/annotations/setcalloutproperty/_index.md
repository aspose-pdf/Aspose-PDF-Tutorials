---
"description": "تعرف على كيفية تعيين خاصية الاستدعاء في ملف PDF باستخدام Aspose.PDF لـ .NET في هذا البرنامج التعليمي المفصل خطوة بخطوة."
"linktitle": "تعيين خاصية التعليق في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تعيين خاصية التعليق في ملف PDF"
"url": "/ar/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تعيين خاصية التعليق في ملف PDF

## مقدمة

غالبًا ما يتطلب إنشاء مستندات PDF احترافية وجذابة بصريًا إضافة تعليقات توضيحية تلفت الانتباه إلى محتوى محدد. ومن هذه التعليقات التوضيحية، وهي تشبه فقاعات الكلام التي تراها في القصص المصورة. تساعد هذه التعليقات التوضيحية على توضيح النص أو إبرازه داخل ملف PDF. تُسهّل مكتبة Aspose.PDF لـ .NET إضافة هذه التعليقات التوضيحية إلى مستنداتك بشكل كبير، وفي هذا البرنامج التعليمي، سنشرح كيفية تعيين خاصية التعليقات التوضيحية في ملف PDF باستخدام هذه المكتبة القوية. سواء كنت مطورًا متمرسًا أو مبتدئًا، ستفهم بنهاية هذا الدليل كيفية استخدام التعليقات التوضيحية في ملفات PDF.

## المتطلبات الأساسية

قبل أن نتعمق في الكود، دعنا نغطي الأساسيات التي تحتاجها للبدء.

1. Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF لـ .NET. يمكنك تنزيلها من [هنا](https://releases.aspose.com/pdf/net/).
2. IDE: بيئة تطوير مثل Visual Studio.
3. .NET Framework: تأكد من تثبيت .NET على جهازك.
4. ترخيص مؤقت: إذا كنت تريد تجربة الميزات الكاملة لـ Aspose.PDF دون قيود، فاحصل على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/).

## استيراد الحزم

قبل أن تبدأ في كتابة الكود، يجب عليك استيراد الحزم اللازمة التي ستسمح لك بالعمل مع ملفات PDF والتعليقات التوضيحية.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

ستوفر لك هذه الواردات جميع الفئات والأساليب اللازمة للتعامل مع مستندات PDF وإنشاء التعليقات التوضيحية مثل التعليق التوضيحي.

## الخطوة 1: تهيئة مستند PDF

الخطوة الأولى في رحلتنا هي تهيئة مستند PDF جديد لإضافة شرحنا التوضيحي. تخيل هذا كإعداد لوحة فارغة للبدء بإضافة العناصر.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// تهيئة مستند PDF جديد
Document doc = new Document();
```
هنا، نقوم بإنشاء جديد `Document` الكائن الذي سيعمل كملف PDF الخاص بنا. `dataDir` يتم تعيين المتغير على الدليل الذي تريد حفظ ملف PDF الخاص بك فيه بعد الانتهاء.

## الخطوة 2: إضافة صفحة جديدة إلى المستند

يمكن أن يحتوي مستند PDF على عدة صفحات، وفي هذه الخطوة، سنضيف صفحة جديدة إلى مستندنا. ستكون هذه الصفحة هي المكان الذي سيُوضع فيه تعليقنا التوضيحي.

```csharp
// إضافة صفحة جديدة إلى المستند
Page page = doc.Pages.Add();
```
ال `Pages.Add()` يتم استخدام الطريقة لإضافة صفحة جديدة إلى `doc` الكائن. يتم تخزين الصفحة الجديدة في `page` متغير سنستخدمه لاحقًا عند إضافة التعليق التوضيحي.

## الخطوة 3: تحديد المظهر الافتراضي

للتعليقات التوضيحية، مثل التعليقات التوضيحية، مظهر مرئي يمكنك تخصيصه. في هذه الخطوة، سنحدد شكل النص داخل التعليقات التوضيحية.

```csharp
// تحديد المظهر الافتراضي للتعليق التوضيحي
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
نحن ننشئ `DefaultAppearance` كائن يُحدد لون النص وحجم الخط. هنا، سيكون النص أحمر، وحجم الخط مُعيَّن على 10. سيتم تطبيق هذا المظهر على شرح التعليق التوضيحي.

## الخطوة 4: إنشاء التعليق النصي الحر

الآن حان وقت إنشاء التعليق التوضيحي. يتيح لنا التعليق النصي الحر إضافة تعليق توضيحي بنص ونمط محددين.

```csharp
// إنشاء FreeTextAnnotation مع تعليق توضيحي
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
نحن ننشئ `FreeTextAnnotation` كائن بإحداثيات محددة، تحدد موقعه على الصفحة. `Intent` تم ضبطه على `FreeTextCallout`، مما يشير إلى أن هذا تعليق توضيحي. `EndingStyle` تم ضبطه على `OpenArrow`، مما يعني أن خط التعليق سينتهي بسهم مفتوح.

## الخطوة 5: تحديد نقاط خط التعليق

يحتوي التعليق التوضيحي على خط يشير إلى منطقة الاهتمام. سنحدد هنا النقاط التي تُشكّل هذا الخط.

```csharp
// تحديد النقاط لخط التعليق
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
ال `Callout` الخاصية عبارة عن مجموعة من `Point` كائنات، كل منها يمثل إحداثيًا على الصفحة. تحدد هذه النقاط مسار سطر التعليق، مما يمنحه مظهر فقاعة الكلام الكلاسيكية.

## الخطوة 6: إضافة التعليق التوضيحي إلى الصفحة

بعد إنشاء التعليقات التوضيحية وتكوينها، فإن الخطوة التالية هي إضافتها إلى الصفحة.

```csharp
// أضف التعليق التوضيحي إلى الصفحة
page.Annotations.Add(fta);
```
ال `Annotations.Add()` تُستخدم هذه الطريقة لإضافة التعليق التوضيحي على الصفحة التي أنشأناها سابقًا. تُرسِم هذه الخطوة التعليق التوضيحي على صفحة PDF.

## الخطوة 7: تعيين محتوى النص الغني

يمكن أن تتضمن تعليقات التعليقات التوضيحية نصًا منسقًا، مما يسمح بتنسيق المحتوى داخل الفقاعة. لنُضِف نصًا نموذجيًا.

```csharp
// تعيين النص الغني للتعليق التوضيحي
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">هذه عينة</span></p></body>";
```
ال `RichText` يتم ضبط الخاصية بمحتوى HTML. هذا يسمح بتنسيق مُفصّل داخل النص، مثل تحديد حجم الخط ولونه ونمطه.

## الخطوة 8: حفظ مستند PDF

أخيرًا، بعد إعداد كل شيء، نحتاج إلى حفظ المستند. تُنهي هذه الخطوة إنشاء ملف PDF مع التعليق التوضيحي.

```csharp
// حفظ المستند
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
ال `Save()` تحفظ هذه الطريقة المستند في المجلد المحدد باسم "SetCalloutProperty.pdf". بهذه الخطوة، نختتم عملية إنشاء ملف PDF.

## خاتمة

ها قد انتهيت! لقد أنشأتَ للتو مستند PDF مع شرح توضيحي باستخدام Aspose.PDF لـ .NET. يُمكن أن يكون هذا الشرح مفيدًا للغاية لتسليط الضوء على أجزاء مُحددة من مستندك أو شرحها. يُوفر Aspose.PDF واجهة برمجة تطبيقات قوية تُسهّل التعامل مع ملفات PDF وتجعلها أكثر مرونة. سواءً كنت تُضيف شروحًا توضيحية، أو تُحوّل مستندات، أو تُدير مهام PDF مُعقدة، فإن Aspose.PDF يُلبي جميع احتياجاتك.

## الأسئلة الشائعة

### هل يمكنني تخصيص مظهر النداء بشكل أكبر؟

بالتأكيد! يمكنك تخصيص جوانب مختلفة، مثل لون الخط، وسمكه، ونوع خط النص ونمطه.

### هل من الممكن إضافة عدة تعليقات توضيحية إلى صفحة واحدة؟

نعم، يمكنك إضافة عدد كبير من التعليقات التوضيحية حسب الحاجة عن طريق تكرار الخطوات لكل تعليق توضيحي.

### كيف يمكنني تغيير موضع النداء؟

قم ببساطة بتعديل الإحداثيات في `Rectangle` و `Callout` خصائص لإعادة وضع التعليق التوضيحي.

### هل يمكنني إضافة أنواع أخرى من التعليقات التوضيحية باستخدام Aspose.PDF؟

نعم، يدعم Aspose.PDF أنواعًا مختلفة من التعليقات التوضيحية، بما في ذلك التمييزات والطوابع ومرفقات الملفات.

### هل يقتصر محتوى النص الغني على HTML؟

ال `RichText` تدعم الخاصية مجموعة فرعية من HTML، مما يسمح لك بتضمين نص مصمم وتنسيق أساسي.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}