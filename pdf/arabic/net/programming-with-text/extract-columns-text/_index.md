---
"description": "تعرّف على كيفية استخراج أعمدة نصية من ملفات PDF باستخدام Aspose.PDF لـ .NET. يُفصّل هذا الدليل كل خطوة مع أمثلة برمجية وشروحات."
"linktitle": "استخراج نص الأعمدة في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "استخراج نص الأعمدة في ملف PDF"
"url": "/ar/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# استخراج نص الأعمدة في ملف PDF

## مقدمة

هل تعمل على ملفات PDF وتحتاج إلى استخراج نص بتنسيق عمود محدد؟ سواء كنت تعالج فواتير أو تقارير أو أي مستندات منظمة، فإن استخراج النص بدقة من ملف PDF قد يكون مهمة شاقة. وهنا يأتي دور Aspose.PDF لـ .NET لتبسيط العملية. في هذا البرنامج التعليمي، سنشرح لك كيفية استخراج أعمدة النص من ملف PDF بسهولة. 

## المتطلبات الأساسية

قبل الغوص في الكود، دعنا نغطي الأشياء الأساسية التي ستحتاجها:

- Aspose.PDF لـ .NET: تأكد من تثبيت أحدث إصدار من Aspose.PDF لـ .NET. إذا لم يكن لديك، يمكنك [قم بتحميله هنا](https://releases.aspose.com/pdf/net/).
- بيئة التطوير: ستحتاج إلى Visual Studio أو بيئة تطوير .NET أخرى للعمل مع الكود.
- مستند PDF: احتفظ بعينة من مستند PDF في متناول يدك، ويفضل أن يحتوي على أعمدة من النص، حيث سنقوم باستخراج النص منه.

إذا لم تقم بتثبيت Aspose.PDF لـ .NET بعد، فيمكنك الحصول على [نسخة تجريبية مجانية](https://releases.aspose.com/) أو [شراء ترخيص](https://purchase.aspose.com/buy) للحصول على الميزات الكاملة. يمكنك أيضًا التقدم بطلب للحصول على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license) إذا لزم الأمر.

## استيراد مساحات الأسماء

لاستخدام Aspose.PDF لـ .NET في مشروعك، ستحتاج إلى استيراد المساحات التالية:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## دليل خطوة بخطوة: استخراج أعمدة النص من ملف PDF

الآن، لنُحلل كل جزء من الكود لفهم آلية عمله بشكل أفضل. تابع معنا خطوة بخطوة، شارحًا كل جزء من العملية.

## الخطوة 1: تحميل مستند PDF

أول شيء عليك فعله هو تحميل ملف PDF الخاص بك إلى `Document` هذا هو كيفية تفاعل Aspose.PDF مع مستندك.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

في هذه الخطوة، نقوم ببساطة بتحديد الدليل الذي سيتم تخزين مستند PDF فيه. استبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار إلى ملف PDF المحلي الخاص بك. `Document` يقوم الكائن بتحميل ملف PDF في الذاكرة، مما يجعله متاحًا لمزيد من المعالجة.

## الخطوة 2: إعداد أداة امتصاص شظايا النص

بعد ذلك، سوف نستخدم `TextFragmentAbsorber` لامتصاص أو التقاط كامل النص من ملف PDF. صُممت هذه الفئة من الامتصاص لاستخراج أجزاء نصية من مناطق محددة في ملف PDF، مما يجعلها مثالية لاستخراج أعمدة من النص.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

هنا، نقوم بإنشاء مثيل لـ `TextFragmentAbsorber` وتطبيقه على جميع صفحات PDF باستخدام `Accept()`. ال `TextFragmentCollection` يخزن النص المستخرج، ومن هذه المجموعة، يمكننا معالجة النص أو استخراجه حسب الحاجة.

## الخطوة 3: ضبط حجم الخط للنص المستخرج

بعد التقاط أجزاء النص، قد ترغب في تصغير حجم الخط، خاصةً إذا كان النص الأصلي كبيرًا جدًا. في هذا المثال، سنُقلل حجم الخط بنسبة 70%.

```csharp
foreach (TextFragment tf in tfc)
{
    // تقليل حجم الخط بنسبة 70%
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

هذا الكود يتكرر في كل مرة `TextFragment` في المجموعة، ويُقلل حجم الخط بنسبة 70%. يُسهّل تعديل حجم الخط إدارة النص المُستخرج، خاصةً إذا كنت تُنسّقه لأغراض مُختلفة.

## الخطوة 4: حفظ المستند في مجرى الذاكرة

بعد تعديل النص نقوم بحفظ ملف PDF في `MemoryStream`. وهذا يسمح لنا بالاحتفاظ بالمستند في الذاكرة لمزيد من المعالجة دون الحاجة إلى كتابته مرة أخرى على القرص.

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

هنا، نحفظ ملف PDF في ذاكرة التخزين المؤقت، ثم نعيد تحميله. هذه الطريقة مفيدة عند العمل على ملفات كبيرة الحجم وترغب في تجنب عمليات القرص غير الضرورية.

## الخطوة 5: استخراج كل النص باستخدام Text Absorber

بعد أن جهّزنا ملف PDF، حان وقت استخراج النص. سنستخدم `TextAbsorber` للحصول على كل النص من المستند.

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

في هذه الخطوة، `TextAbsorber` يمتص كل النص من ملف PDF، ويتم تخزين النص المستخرج في `extractedText` سلسلة نصية. وهنا يأتي السحر - أصبحت أعمدة النص لديك الآن بتنسيق نص عادي!

## الخطوة 6: حفظ النص المستخرج في ملف

وأخيرًا، نقوم بحفظ النص المستخرج في `.txt` ملف لسهولة الوصول إليه ومزيد من الاستخدام.

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

يكتب هذا الكود النص المستخرج في ملف جديد `.txt` الملف وحفظه في المجلد المحدد. ستظهر رسالة في وحدة التحكم لتأكيد نجاح العملية.

## خاتمة

هذا كل ما في الأمر! استخراج أعمدة نصية من ملف PDF باستخدام Aspose.PDF لـ .NET أسهل مما تظن. ببضعة أسطر فقط من التعليمات البرمجية، يمكنك تحميل ملف PDF، واستخراج نص محدد، وتعديل التنسيق، وحفظ النتائج في ملف نصي.

هذه التقنية مفيدة للغاية لمعالجة المستندات المنظمة، مثل الجداول والتقارير، أو أي محتوى مُنظّم في أعمدة. سواءً كنتَ بحاجة إلى أتمتة استخراج البيانات أو معالجة مستندات ضخمة، يوفر Aspose.PDF الأدوات اللازمة لتحقيق ذلك بكفاءة.

## الأسئلة الشائعة

### هل يمكنني استخراج النص من صفحات معينة من ملف PDF؟  
نعم! يمكنك تعديل `TextFragmentAbsorber` لاستهداف صفحات محددة باستخدام `pdfDocument.Pages[pageIndex].Accept(tfa);` طريقة.

### هل من الممكن استخراج النص من عمود واحد فقط في ملف PDF متعدد الأعمدة؟  
نعم، ولكنك ستحتاج إلى العمل مع إحداثيات أجزاء النص باستخدام `TextFragment.Rectangle` لاستهداف مناطق محددة من المستند.

### كيف يمكنني تحسين دقة استخراج النص؟  
لتحسين الدقة، تأكد من أن بنية ملف PDF محددة جيدًا وتجنب المستندات ذات التخطيطات المعقدة. يمكنك أيضًا ضبط `TextFragmentAbsorber` لاستخراج النص بناءً على أنماط الخطوط أو أحجامها أو مناطقها.

### هل يدعم Aspose.PDF استخراج النص من المستندات الممسوحة ضوئيًا؟  
نعم، ولكن ستحتاج إلى استخدام تقنية التعرف الضوئي على الحروف (OCR). يوفر Aspose أدواتٍ لذلك أيضًا.

### كيف أتعامل مع ملفات PDF كبيرة الحجم تحتوي على آلاف الصفحات؟  
بالنسبة لملفات PDF الكبيرة، قم بمعالجة المستند في أجزاء عن طريق استخراج النص من بضع صفحات في كل مرة لتجنب استخدام قدر كبير من الذاكرة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}