---
"description": "تعرّف على كيفية إخفاء أرقام الصفحات في جدول المحتويات باستخدام Aspose.PDF لـ .NET. اتبع هذا الدليل المفصل مع أمثلة برمجية لإنشاء ملفات PDF احترافية."
"linktitle": "إخفاء أرقام الصفحات في جدول المحتويات"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إخفاء أرقام الصفحات في جدول المحتويات"
"url": "/ar/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إخفاء أرقام الصفحات في جدول المحتويات

## مقدمة

عند العمل مع ملفات PDF، قد ترغب أحيانًا في إنشاء جدول محتويات (TOC) مع الحفاظ على مظهر أنيق بإخفاء أرقام الصفحات. ربما يكون تنسيق المستند أفضل بدونها، أو ربما يكون ذلك خيارًا جماليًا. مهما كان سببك، إذا كنت تستخدم Aspose.PDF لـ .NET، فسيوضح لك هذا البرنامج التعليمي كيفية إخفاء أرقام الصفحات في جدول المحتويات.

## المتطلبات الأساسية

قبل أن نبدأ، هناك بعض الأمور التي ستحتاجها. إليك قائمة مرجعية سريعة:

- تم تثبيت Visual Studio: ستحتاج إلى إصدار عمل من Visual Studio للترميز معه.
- مكتبة Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF لـ .NET.
  - رابط التحميل: [Aspose.PDF لـ .NET](https://releases.aspose.com/pdf/net/)
- الترخيص المؤقت: إذا كنت تقوم باختبار الميزات، فمن المفيد أن يكون لديك ترخيص مؤقت.
  - رخصة مؤقتة: [احصل عليه هنا](https://purchase.aspose.com/temporary-license/)

## استيراد الحزم

قبل البدء في البرمجة، تأكد من استيراد مساحات الأسماء التالية في مشروع C# الخاص بك. ستوفر هذه المساحات الفئات والأساليب اللازمة للعمل مع مستندات PDF وإنشاء جدول المحتويات (TOC).

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

الآن وقد أصبحت بيئتك جاهزة وتم استيراد الحزم، فلنبدأ بشرح كل خطوة من خطوات العملية. سنغطي كل جزء من الكود لضمان الوضوح، ليسهل عليك متابعته.

## الخطوة 1: تهيئة مستند PDF الخاص بك

أول شيء يتعين علينا القيام به هو إنشاء مستند PDF جديد وإضافة صفحة لجدول المحتويات (TOC).


```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir: هذا هو الدليل الذي سيتم حفظ ملف الإخراج الخاص بك فيه.
- Document(): يقوم بتهيئة مستند PDF جديد.
- Pages.Add(): تقوم بإضافة صفحة فارغة جديدة إلى المستند، والتي ستحتوي لاحقًا على جدول المحتويات الخاص بك.

## الخطوة 2: إعداد معلومات جدول المحتويات والعنوان

بعد ذلك، سنقوم بتحديد معلومات جدول المحتويات، بما في ذلك تعيين العنوان الذي سيظهر في الجزء العلوي من جدول المحتويات.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo: يحتوي هذا الكائن على كافة المعلومات حول جدول المحتويات.
- TextFragment: يمثل نص عنوان جدول المحتويات، وهنا قمنا بتعيينه كـ "جدول المحتويات".
- نمط الخط: نقوم بتصميم عنوان جدول المحتويات عن طريق ضبط حجمه إلى 20 وجعله غامقًا.
- tocPage.TocInfo: نقوم بتعيين معلومات جدول المحتويات إلى الصفحة التي ستعرض جدول المحتويات.

## الخطوة 3: إخفاء أرقام الصفحات في جدول المحتويات

الآن، حان وقت المرح! هنا نُهيئ جدول المحتويات لإخفاء أرقام الصفحات.

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers: هذا هو المفتاح السحري الذي يُخفي أرقام الصفحات. اضبطه على `false`، ولن تظهر أرقام الصفحات في جدول المحتويات.
- FormatArrayLength: قمنا بتعيين هذا إلى 4، مما يشير إلى أننا نريد تحديد التنسيق لأربعة مستويات من عناوين جدول المحتويات.

## الخطوة 4: تخصيص تنسيق جدول المحتويات

لإضافة المزيد من الأناقة إلى جدول المحتويات الخاص بك، سنقوم الآن بتحديد التنسيق لمستويات مختلفة من العناوين.

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray: تتحكم هذه المصفوفة بتنسيق مدخلات جدول المحتويات. يمثل كل فهرس مستوى عنوان مختلفًا.
- الهامش ونمط النص: نقوم بتعيين الهوامش وتطبيق أنماط الخطوط مثل الغامق والمائل والتسطير لكل مستوى عنوان.

## الخطوة 5: إضافة عناوين إلى المستند

وأخيرًا، دعنا نضيف العناوين الفعلية التي ستكون جزءًا من جدول المحتويات.

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- العناوين وشرائح النص: تُمثّل هذه العناوين التي ستظهر في جدول المحتويات. لكل مستوى عنوانه الخاص.
- IsAutoSequence: ترقيم العناوين تلقائيًا.
- IsInList: يضمن ظهور كل عنوان في جدول المحتويات.

## الخطوة 6: حفظ المستند

بمجرد ضبط كل شيء، احفظ مستند PDF في ملف الإخراج المحدد.

```csharp
doc.Save(outFile);
```

وهذا كل شيء! لقد أنشأتَ بنجاح ملف PDF بجدول محتويات، وأرقام الصفحات مخفية!

## خاتمة

قد يبدو إنشاء جدول محتويات في ملف PDF وإخفاء أرقام الصفحات أمرًا صعبًا، ولكن مع Aspose.PDF لـ .NET، أصبح الأمر في غاية السهولة. باتباع هذا الدليل التفصيلي، ستتعلم كيفية تخصيص تنسيق جدول المحتويات، وإخفاء أرقام الصفحات، وتطبيق أنماط مختلفة على عناوينك. الآن يمكنك إنشاء ملفات PDF احترافية مصممة خصيصًا لتلبية احتياجاتك.

## الأسئلة الشائعة

### هل يمكنني إظهار أرقام الصفحات لعناوين محددة في جدول المحتويات؟
لا، يُخفي Aspose.PDF أرقام الصفحات لجدول المحتويات بأكمله أو يُظهرها. لا يُمكنك إخفاءها بشكل انتقائي لإدخالات مُحددة.

### هل من الممكن إضافة مستويات أخرى إلى جدول المحتويات؟
نعم يمكنك زيادة `FormatArrayLength` لتحديد المزيد من مستويات عناوين جدول المحتويات.

### كيف يمكنني تغيير الخط لجميع إدخالات جدول المحتويات؟
يمكنك تغيير الخط عن طريق تعديل `TextState.Font` الممتلكات لكل مستوى في `FormatArray`.

### هل يمكنني إدراج روابط تشعبية في جدول المحتويات؟
نعم، يمكنك ربط كل إدخال في جدول المحتويات بقسم محدد في المستند باستخدام `Heading.TocPage` ملكية.

### هل أحتاج إلى ترخيص لـ Aspose.PDF؟
نعم، يلزم ترخيص ساري المفعول للاستخدام الإنتاجي. يمكنك الحصول على ترخيص مؤقت. [هنا](https://purchase.aspose.com/temporary-license/) لاختبار الميزات.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}