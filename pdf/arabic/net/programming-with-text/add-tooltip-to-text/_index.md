---
"description": "تعرّف على كيفية إضافة تلميحات الأدوات إلى النصوص في ملفات PDF باستخدام Aspose.PDF لـ .NET. حسّن ملفات PDF الخاصة بك بنصوص توضيحية سهلة الاستخدام."
"linktitle": "إضافة تلميح الأدوات إلى النص في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة تلميح الأدوات إلى النص في ملف PDF"
"url": "/ar/net/programming-with-text/add-tooltip-to-text/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة تلميح الأدوات إلى النص في ملف PDF

## مقدمة

عندما يتعلق الأمر بإنشاء ملفات PDF جذابة وتفاعلية، تُعدّ التلميحات أداةً قيّمةً للغاية. هل تعرف تلك النوافذ المنبثقة الصغيرة التي تُقدّم لك معلومات إضافية عند تمرير مؤشر الماوس فوق شيء ما؟ يُمكنها توفير سياق ووصف، أو حتى نصائح مُختصرة دون إثقال مستندك. في هذا البرنامج التعليمي، سنشرح كيفية إضافة تلميحات إلى نص في ملف PDF باستخدام مكتبة Aspose.PDF لـ .NET. سواء كنت مطورًا محترفًا أو مبتدئًا في عالم ملفات PDF، فأنت في المكان المناسب! هيا بنا!

## المتطلبات الأساسية

قبل أن ننتقل إلى جزء الترميز، دعنا نتأكد من أن لديك كل ما تحتاجه لمتابعة الأمر بسلاسة.

### تم تثبيت Visual Studio
من الضروري تثبيت Visual Studio على جهازك، لأنه سيكون بيئة التطوير الأساسية لتطبيقات .NET.

### مكتبة Aspose.PDF لـ .NET
ستحتاج أيضًا إلى مكتبة Aspose.PDF. يمكنك [قم بتحميله هنا](https://releases.aspose.com/pdf/net/)تأكد من تضمينه في مراجع مشروعك.

### المعرفة الأساسية بلغة C#
ستكون لديك خبرة في لغة C#، لأننا سنبرمج بها. لكن لا تقلق، سأرشدك في كل خطوة!

### وثيقة PDF للعمل بها
يمكنك البدء بمستند PDF فارغ، كما نفعل في هذا المثال، أو استخدام مستند موجود إذا كنت تفضل ذلك.

الآن، دعونا ننتقل إلى جزء الترميز!

## استيراد الحزم 

الخطوة الأولى في رحلة البرمجة لدينا هي استيراد الحزم اللازمة. افتح مشروع Visual Studio، وفي أعلى ملف C#، ستحتاج إلى إضافة ما يلي: `using` التوجيهات:

```csharp
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
```

تتيح لك هذه الحزم الوصول إلى جميع الفئات والوظائف التي تحتاجها لإنشاء مستندات PDF ومعالجتها.

## الخطوة 1: إعداد دليل المستندات الخاص بك

أولاً، علينا تحديد المسار الذي ستحفظ فيه مستنداتك. تخيل هذا الأمر كأنك تبحث عن مكان آمن في نظام ملفاتك لحفظ جميع إبداعاتك.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outputFile = dataDir + "Tooltip_out.pdf";
```

تأكد من الاستبدال `YOUR DOCUMENT DIRECTORY` مع المسار الفعلي على جهازك.

## الخطوة 2: إنشاء مستند PDF نموذجي

الآن، حان وقت إنشاء ملف PDF بسيط مع بعض النصوص. هنا نبدأ عمليتنا الإبداعية!

```csharp
// إنشاء مستند نموذجي يحتوي على نص
Document doc = new Document();
doc.Pages.Add().Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a tooltip"));
doc.Pages[1].Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a very long tooltip"));
doc.Save(outputFile);
```

في هذه الخطوة نقوم بإنشاء مستند، ونضيف إليه قطعتين نصيتين، ونحفظه في المسار الذي حددناه مسبقًا.

## الخطوة 3: فتح المستند للمعالجة

الآن بعد أن قمنا بإنشاء المستند الخاص بنا، فلنفتحه حتى نتمكن من العمل على أدوات التلميح تلك!

```csharp
// فتح مستند يحتوي على نص
Document document = new Document(outputFile);
```

هنا، نقوم ببساطة بتحميل المستند الذي قمنا بإنشائه للتو.

## الخطوة 4: إنشاء أداة امتصاص نص للعثور على أجزاء نصية

نحتاج إلى العثور على أجزاء النص التي نريد إضافة التلميحات إليها. هذا يشبه استخدام عدسة مكبرة لتسليط الضوء على جزء محدد من خريطة كبيرة! 

```csharp
// إنشاء كائن TextAbsorber للعثور على جميع العبارات المطابقة للتعبير العادي
TextFragmentAbsorber absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a tooltip");
document.Pages.Accept(absorber);
```

## الخطوة 5: استخراج أجزاء النص

بعد ذلك، نقوم باستخراج أجزاء النص التي وجدناها من خطوتنا السابقة.

```csharp
// احصل على أجزاء النص المستخرجة
TextFragmentCollection textFragments = absorber.TextFragments;
```

يتيح لنا هذا المقطع الاحتفاظ بالمراجع لأجزاء النص التي نهتم بها.

## الخطوة 6: التنقل عبر الأجزاء وإضافة تلميحات الأدوات

الآن يأتي الجزء الممتع! سنستعرض كل جزء من النص ونضيف تلميحًا لكل جزء. تخيلوا تغليف عناصر محددة (أجزاء نصية) بهدايا صغيرة (تلميحات).

```csharp
// التكرار عبر الشظايا
foreach (TextFragment fragment in textFragments)
{
	// إنشاء زر غير مرئي في موضع جزء النص
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// سيتم عرض قيمة AlternateName كإشارة توضيحية بواسطة تطبيق المشاهد
	field.AlternateName = "Tooltip for text.";
	// إضافة حقل زر إلى المستند
	document.Form.Add(field);
}
```

في كل تكرار، نقوم بإنشاء حقل زر يتوافق مع موضع جزء النص ونقوم بتعيين نص الإرشاد إليه.

## الخطوة 7: كرر ذلك بالنسبة لأدوات التلميح الطويلة

كما أضفنا تلميحًا بسيطًا، يمكننا فعل الشيء نفسه للنصوص الأطول. لنُطلق العنان لإبداعنا!

```csharp
// ستكون الخطوة التالية عينة من تلميح الأدوات الطويل جدًا
absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a very long tooltip");
document.Pages.Accept(absorber);
textFragments = absorber.TextFragments;
foreach (TextFragment fragment in textFragments)
{
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// تعيين نص طويل جدًا
	field.AlternateName = "Lorem ipsum dolor sit amet, consectetur adipiscing elit," +
							" sed do eiusmod tempor incididunt ut labore et dolore magna" +
							" aliqua. Ut enim ad minim veniam, quis nostrud exercitation" +
							" ullamco laboris nisi ut aliquip ex ea commodo consequat." +
							" Duis aute irure dolor in reprehenderit in voluptate velit" +
							" esse cillum dolore eu fugiat nulla pariatur. Excepteur sint" +
							" occaecat cupidatat non proident, sunt in culpa qui officia" +
							" deserunt mollit anim id est laborum.";
	document.Form.Add(field);
}
```

هنا، نقوم بنفس نوع العمل كما في السابق، ولكن مع تلميح أداة أكثر توسعًا.

## الخطوة 8: احفظ مستندك

الخطوة الأخيرة هي حفظ مستندك مع كل أدوات التلميح الجديدة اللامعة. 

```csharp
// حفظ المستند
document.Save(outputFile);
```

وهكذا، انتهيت! أضفتَ تلميحات الأدوات إلى ملف PDF، مما يجعله أكثر سهولة في الاستخدام وتفاعلية.

## خاتمة

هذا كل ما في الأمر - دليل سهل الاستخدام حول كيفية إضافة تلميحات الأدوات إلى النصوص في ملفات PDF باستخدام Aspose.PDF لـ .NET. تُحسّن هذه التقنية تجربة المستخدم بشكل ملحوظ، مما يجعل مستنداتك أكثر إفادة دون إثقال القارئ بكمية كبيرة من النصوص دفعة واحدة. 

بمجرد تمرير مؤشر الفأرة فوق كلمة أو عبارة، يحصل القارئ على معلومات مهمة تُضيف قيمةً دون فوضى. لذا، استعد وجرّبه! قبل أن تُدرك، قد تُنشئ مستنداتٍ جذابةً ومتميزةً.

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة تتيح للمطورين إنشاء مستندات PDF ومعالجتها وتحويلها في تطبيقات .NET.

### هل يمكنني استخدام Aspose.PDF مجانًا؟
نعم، يُقدّم Aspose نسخة تجريبية مجانية لاستكشاف ميزاته! يمكنك العثور عليها [هنا](https://releases.aspose.com/).

### هل هناك أي خيارات ترخيص متاحة لـ Aspose.PDF؟
نعم، يمكنك شراء ترخيص أو الحصول على ترخيص مؤقت. اطلع على الخيارات المتاحة. [هنا](https://purchase.aspose.com/).

### هل يمكنني إضافة عناصر تفاعلية أخرى غير تلميحات الأدوات باستخدام Aspose.PDF؟
بالتأكيد! يتيح لك Aspose.PDF إضافة عناصر تفاعلية متنوعة، مثل الروابط التشعبية والأزرار والنماذج.

### أين يمكنني العثور على مزيد من الوثائق حول Aspose.PDF؟
يمكنك الاطلاع على الوثائق [هنا](https://reference.aspose.com/pdf/net/) لمزيد من الإرشادات المتعمقة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}