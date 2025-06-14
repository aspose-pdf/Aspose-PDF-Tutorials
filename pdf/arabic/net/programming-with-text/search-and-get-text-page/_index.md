---
"description": "تعرف على كيفية البحث والحصول على نص من صفحة معينة في ملف PDF باستخدام Aspose.PDF لـ .NET."
"linktitle": "البحث والحصول على صفحة نصية في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "البحث والحصول على صفحة نصية في ملف PDF"
"url": "/ar/net/programming-with-text/search-and-get-text-page/"
"weight": 430
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# البحث والحصول على صفحة نصية في ملف PDF

## مقدمة

هل سبق لك أن وجدت نفسك بحاجة للبحث عن نص معين داخل مستند PDF واستخراجه للاستخدام لاحقًا؟ ربما تُنشئ تطبيقًا لمعالجة المستندات ويتطلب استخراج بيانات دقيقًا، أو ربما تحتاج فقط إلى تحليل ملفات PDF بكفاءة. مهما كانت حالتك، فأنت في المكان المناسب! في هذا البرنامج التعليمي، سنتعمق في كيفية البحث عن نص واستخراجه من صفحة في ملف PDF باستخدام Aspose.PDF لـ .NET. سواء كنت مبتدئًا أو مطورًا محترفًا، سيرشدك هذا الدليل خلال كل خطوة بأسلوب شيق وتفاعلي. هل أنت مستعد؟ هيا بنا!

## المتطلبات الأساسية

قبل أن ننتقل إلى البرمجة، دعنا نتأكد من أن لديك كل ما تحتاجه:

1. مكتبة Aspose.PDF لـ .NET: يمكنك تنزيلها من [هنا](https://releases.aspose.com/pdf/net/) أو احصل على نسخة تجريبية مجانية من نفس الرابط. للشراء، تفضل بزيارة [متجر أسبووز](https://purchase.aspose.com/buy).
2. .NET Framework: ستحتاج إلى بيئة تطوير .NET عاملة مثل Visual Studio.
3. ملف PDF: ستحتاج إلى ملف PDF نموذجي للبحث عن النص واستخراجه. في هذا البرنامج التعليمي، لنفترض أن اسم الملف هو `SearchAndGetTextPage.pdf`.

## استيراد الحزم

أولاً، نحتاج إلى استيراد مساحات الأسماء اللازمة للعمل مع Aspose.PDF لـ .NET. تأكد من تضمينها في أعلى الكود.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System
```

بعد أن غطينا المتطلبات الأساسية، لنبدأ بشرح الكود خطوة بخطوة. كل خطوة مُوضحة بوضوح ليسهل متابعتها.

## الخطوة 1: تعيين المسار إلى دليل المستندات الخاص بك

قبل التعامل مع ملف PDF، ستحتاج إلى تحديد مسار تخزينه. هذا يضمن وصول البرنامج إليه.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- dataDir: هذا هو المسار إلى المجلد الذي تُخزَّن فيه ملفات PDF. استبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي يقع فيه ملف PDF.

## الخطوة 2: تحميل مستند PDF

الخطوة التالية هي تحميل ملف PDF إلى الذاكرة لتتمكن من العمل عليه. إليك الطريقة:

```csharp
Document pdfDocument = new Document(dataDir + "SearchAndGetTextPage.pdf");
```

- المستند: هذه هي فئة Aspose.PDF التي تقوم بتحميل ملف PDF.
- pdfDocument: المتغير الذي سيتم تخزين ملف PDF الخاص بك فيه بعد تحميله.

## الخطوة 3: إنشاء كائن امتصاص النص

ال `TextFragmentAbsorber` تتيح لك هذه الفئة البحث عن نص محدد داخل ملف PDF. لننشئ مثيلًا لهذه الفئة للعثور على جميع مثيلات عبارة بحث معينة.

```csharp
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Figure");
```

- TextFragmentAbsorber: هذه الفئة مسؤولة عن العثور على النص واستخراجه من ملف PDF.
- "الشكل": استبدل هذا بأي نص تريد البحث عنه داخل ملف PDF.

## الخطوة 4: تطبيق Text Absorber على ملف PDF بأكمله

بمجرد إعداد ممتص النص، ستحتاج إلى إخبار البرنامج بالبحث خلال جميع صفحات ملف PDF.

```csharp
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Accept(): تطبق هذه الطريقة أداة امتصاص النص على ملف PDF، وتفحص كل صفحة بحثًا عن النص الذي حددته.

## الخطوة 5: استرجاع النص المستخرج وتكراره

بعد مسح ملف PDF ضوئيًا، حان وقت استرجاع النتائج وعرضها. سنستعرض أجزاء النص المستخرجة.

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- TextFragmentCollection: تحتوي هذه المجموعة على جميع حالات أجزاء النص التي تم العثور عليها بواسطة ممتص النص.

## الخطوة 6: تكرار كل جزء واستخراج البيانات

سنقوم الآن بالمرور عبر `textFragmentCollection` واستخراج خصائص مختلفة لكل جزء من النص، مثل موضعه وتفاصيل الخط واللون.

```csharp
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

- جزء نصي: يحتوي كل جزء على أجزاء من النص الموجود.
- جزء النص: يمكن أن يحتوي كل جزء على أجزاء متعددة، تمثل أجزاء مختلفة من النص.
- حالة النص: توفر هذه الحالة معلومات مفصلة حول خط النص وحجمه ولونه.

في هذه الحلقة، نقوم بطباعة التفاصيل مثل النص الفعلي، وموضعه (إحداثيات X وY)، والخط، وما إذا كان الخط مضمنًا في ملف PDF، ولون مقدمة النص.

## خاتمة

وها أنت ذا! لقد نجحتَ الآن في البحث عن نص واستخراجه من ملف PDF باستخدام Aspose.PDF لـ .NET. ستدهشك مرونة هذه المكتبة. سواءً كنتَ بحاجة إلى البحث عن نص معين في مستند كبير، أو استخراجه، أو تحليل خصائصه، فإن Aspose.PDF يُسهّل عليك الأمر. بالإضافة إلى ذلك، بفضل الكود الذي شرحناه، ستكون جاهزًا تمامًا لتكييفه مع احتياجاتك. 

## الأسئلة الشائعة

### هل يمكنني البحث عن عبارات متعددة في وقت واحد؟  
نعم يمكنك تعديل الكود للبحث عن عبارات متعددة عن طريق إنشاء عدة `TextFragmentAbsorber` أشياء.

### كيف يمكنني استخراج النص من صفحة معينة؟  
يمكنك استهداف صفحة معينة عن طريق تطبيق `TextFragmentAbsorber` إلى صفحة واحدة بدلاً من المستند بأكمله. على سبيل المثال: `pdfDocument.Pages[1].Accept(textFragmentAbsorber);`.

### هل Aspose.PDF لـ .NET مجاني؟  
Aspose.PDF هو منتج تجاري، ولكن يمكنك استخدامه مع [نسخة تجريبية مجانية](https://releases.aspose.com/).

### هل يمكنني استخراج الصور من ملف PDF باستخدام Aspose.PDF؟  
نعم، يتيح لك Aspose.PDF استخراج الصور بالإضافة إلى النص. تحقق من [التوثيق](https://reference.aspose.com/pdf/net/) لمزيد من التفاصيل.

### ماذا لو كنت بحاجة إلى مزيد من المساعدة أو الدعم؟  
يمكنك دائمًا الحصول على المساعدة من [منتدى دعم Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}