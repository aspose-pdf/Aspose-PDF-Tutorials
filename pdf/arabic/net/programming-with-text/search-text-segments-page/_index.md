---
"description": "تعرّف على كيفية البحث عن مقاطع نصية في ملفات PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل المفصل خطوة بخطوة. استخرج النص، وحلل المقاطع، والمزيد."
"linktitle": "البحث عن أجزاء النص في صفحة ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "البحث عن أجزاء النص في صفحة ملف PDF"
"url": "/ar/net/programming-with-text/search-text-segments-page/"
"weight": 470
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# البحث عن أجزاء النص في صفحة ملف PDF

## مقدمة

هل تساءلت يومًا عن كيفية تحديد أجزاء نصية محددة في مستند PDF باستخدام Aspose.PDF لـ .NET؟ حسنًا، أنت محظوظ! في هذا الدليل، سنشرح لك العملية خطوة بخطوة وبطريقة مبسطة. سواء كنت تحاول استخراج معلومات، أو تحليل نصوص، أو مجرد فهم تعقيدات معالجة ملفات PDF، فإن Aspose.PDF لـ .NET سيُلبي احتياجاتك. هيا بنا!

## المتطلبات الأساسية

قبل أن نبدأ، دعونا نتأكد من أنك حصلت على كل ما تحتاجه:

- Aspose.PDF لـ .NET: تأكد من تثبيت المكتبة. يمكنك الحصول عليها من [هنا](https://releases.aspose.com/pdf/net/).
- .NET Framework: تأكد من تثبيت .NET على جهازك.
- بيئة التطوير: يوصى باستخدام Visual Studio أو أي بيئة تطوير متكاملة تدعم .NET.
- مستند PDF: ملف PDF حيث ستبحث عن أجزاء نصية.

إذا لم يكن لديك Aspose.PDF لـ .NET بعد، فلا تقلق! يمكنك الحصول على نسخة تجريبية مجانية من [هنا](https://releases.aspose.com/) أو شرائه [هنا](https://purchase.aspose.com/buy).

## استيراد الحزم

قبل البدء بالبرمجة، من الضروري استيراد الحزم اللازمة إلى مشروعك. هذا يضمن توفر جميع الفئات والأساليب اللازمة لمهام معالجة ملفات PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

وبعد أن وضعنا الأساسيات في مكانها الصحيح، فلننتقل مباشرة إلى الدليل خطوة بخطوة.


## الخطوة 1: تحميل مستند PDF

الخطوة الأولى في العملية هي تحميل ملف PDF إلى البرنامج. بدون تحميل الملف، لن تجد ما تبحث عنه، أليس كذلك؟ إليك الطريقة.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// فتح المستند
Document pdfDocument = new Document(dataDir + "SearchTextSegmentsPage.pdf");
```

- `dataDir`:يحتوي هذا المتغير على مسار ملف PDF الخاص بك. استبدل `"YOUR DOCUMENT DIRECTORY"` مع الدليل الفعلي الذي يتم تخزين ملفك فيه.
- `pdfDocument`:باستخدام `Document` الصف، نقوم بتحميل ملف PDF إلى الذاكرة.

## الخطوة 2: إعداد البحث النصي

الآن بعد أن تم تحميل مستندك، فإن الخطوة التالية هي إنشاء `TextFragmentAbsorber` الكائن الذي يسمح لنا بالبحث عن نص محدد داخل المستند.

```csharp
// إنشاء كائن TextAbsorber للعثور على جميع حالات عبارة البحث المدخلة
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- `TextFragmentAbsorber`:يُستخدم هذا الكائن لالتقاط جميع تكرارات النص الذي تبحث عنه. استبدل `"text"` مع النص الفعلي الذي تريد البحث عنه.

## الخطوة 3: قبول الامتصاص لصفحات محددة

قد لا ترغب دائمًا في البحث في مستند PDF بأكمله. في هذا المثال، سنقتصر البحث على صفحة محددة.

```csharp
// قبول الممتص لجميع الصفحات
pdfDocument.Pages[2].Accept(textFragmentAbsorber);
```

- `pdfDocument.Pages[2]`هذا يعني أننا نبحث فقط في الصفحة الثانية من المستند. يمكنك تعديل الفهرس لاستهداف صفحات أخرى.
- `Accept()`:هذه الطريقة تسمح بـ `TextFragmentAbsorber` لمعالجة النص داخل الصفحة المحددة.

## الخطوة 4: استخراج أجزاء النص

بعد البحث في الصفحة، نقوم باستخراج أجزاء النص التي تم العثور عليها إلى مجموعة.

```csharp
// احصل على أجزاء النص المستخرجة
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`:تحتوي هذه المجموعة على جميع حالات أجزاء النص التي تم العثور عليها أثناء عملية البحث.

## الخطوة 5: تكرار أجزاء النص واستخراج البيانات

الآن، دعنا ننتقل عبر كل جزء من النص ونستخرج تفاصيله، مثل الموضع والخط واللون.

```csharp
// التكرار عبر الشظايا
foreach (TextFragment textFragment in textFragmentCollection)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        Console.WriteLine("Text : {0} ", textSegment.Text);
        Console.WriteLine("Position : {0} ", textSegment.Position);
        Console.WriteLine("XIndent : {0} ", textSegment.Position.XIndent);
        Console.WriteLine("YIndent : {0} ", textSegment.Position.YIndent);
        Console.WriteLine("Font - Name : {0}", textSegment.TextState.Font.FontName);
        Console.WriteLine("Font - IsAccessible : {0} ", textSegment.TextState.Font.IsAccessible);
        Console.WriteLine("Font - IsEmbedded : {0} ", textSegment.TextState.Font.IsEmbedded);
        Console.WriteLine("Font - IsSubset : {0} ", textSegment.TextState.Font.IsSubset);
        Console.WriteLine("Font Size : {0} ", textSegment.TextState.FontSize);
        Console.WriteLine("Foreground Color : {0} ", textSegment.TextState.ForegroundColor);
    }
}
```

- `foreach (TextFragment textFragment in textFragmentCollection)`:نحن نمر عبر كل `TextFragment` في المجموعة.
- `foreach (TextSegment textSegment in textFragment.Segments)`داخل كل جزء، توجد عدة أجزاء. نتصفحها بشكل متكرر لجمع كل المعلومات ذات الصلة.
- خصائص مختلفة من `textSegment`:وهي تعطينا معلومات مفصلة حول النص، مثل موضعه (X وY)، وتفاصيل الخط، والحجم، واللون.

## الخطوة 6: إخراج النتائج

أخيرًا، بعد استخراج جميع المعلومات، تُطبع النتائج في وحدة التحكم. يساعدك هذا على رؤية مكان النص وتفاصيل تنسيقه بدقة.

فيما يلي عينة من النتائج من أجل الوضوح:

```
Text : text
Position : X: 45.0, Y: 75.0
XIndent : 45.0
YIndent : 75.0
Font - Name : Arial
Font - IsAccessible : True
Font - IsEmbedded : False
Font - IsSubset : False
Font Size : 12.0
Foreground Color : System.Drawing.Color [Black]
```

- يتيح لك هذا الإخراج معرفة الموقع الدقيق ومعلومات التنسيق للنص "النص" على الصفحة المحددة.

## خاتمة

وها أنت ذا! لقد تعلمت للتو كيفية البحث عن مقاطع نصية محددة داخل مستند PDF باستخدام Aspose.PDF لـ .NET. هذه العملية مفيدة للغاية عند التعامل مع ملفات PDF كبيرة الحجم، مما يتيح لك تحديد النصوص الرئيسية واستخراجها بكفاءة. سواء كنت ترغب في تحليل البيانات، أو استخراج المعلومات، أو حتى تصفح المستند، يوفر لك Aspose.PDF أدوات فعّالة لإنجاز المهمة.

## الأسئلة الشائعة

### هل يمكنني البحث عن كلمات أو عبارات متعددة؟
نعم يمكنك تعديل `TextFragmentAbsorber` للبحث عن نص مختلف عن طريق تغيير سلسلة الإدخال.

### هل من الممكن البحث عبر صفحات متعددة؟
بالتأكيد! يمكنك تصفح جميع صفحات ملف PDF بالتكرار. `pdfDocument.Pages`.

### كيف أبحث عن نص لا يميز بين الأحرف الكبيرة والصغيرة؟
يمكنك استخدام `TextSearchOptions` لتفعيل البحث غير الحساس لحالة الأحرف.

### هل يمكنني تعديل النص بعد العثور عليه؟
نعم، بمجرد تحديد موقع `TextFragment`، يمكنك تعديل خصائص النص الخاصة به.

### هل هذه الطريقة قابلة للتطبيق على ملفات PDF المشفرة؟
نعم، طالما قمت بإلغاء قفل ملف PDF باستخدام كلمة المرور الصحيحة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}