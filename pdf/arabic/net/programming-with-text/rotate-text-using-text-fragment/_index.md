---
"description": "تعلّم كيفية تدوير النص في ملفات PDF باستخدام Aspose.PDF لـ .NET من خلال دليل خطوة بخطوة. اكتشف تقنيات معالجة النصوص، من تحديد الموقع إلى التدوير."
"linktitle": "تدوير النص باستخدام جزء النص في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تدوير النص باستخدام جزء النص في ملف PDF"
"url": "/ar/net/programming-with-text/rotate-text-using-text-fragment/"
"weight": 390
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تدوير النص باستخدام جزء النص في ملف PDF

## مقدمة

إنشاء ملفات PDF أمرٌ مهم، ولكن تعديلها لتلبية متطلبات محددة أمرٌ رائع! هنا يكمن السر! هل تساءلت يومًا عن كيفية تدوير النص في ملف PDF؟ سواءً كنت تُنشئ تقارير أو مستندًا بتصميم مُخصص، فإن تدوير أجزاء النص يُضفي على ملفات PDF مظهرًا أكثر جاذبية. في هذا البرنامج التعليمي، سنستكشف كيفية تدوير النص باستخدام Aspose.PDF لـ .NET، وهي مكتبة قوية تُتيح تعديلًا سلسًا لمستندات PDF.

## المتطلبات الأساسية

قبل أن نبدأ بشرح الكود، لنستعرض سريعًا الأدوات والإعدادات التي ستحتاجها. كل شيء جاهز لتتمكن من المتابعة بسهولة.

### مكتبة Aspose.PDF لـ .NET
أولاً، ستحتاج إلى تثبيت Aspose.PDF لـ .NET في مشروعك. هذه المكتبة غنية بالميزات التي تساعدك على إنشاء ملفات PDF وتعديلها وإدارتها برمجياً. إذا لم تقم بتنزيلها بعد، فإليك كيفية الحصول عليها:
- [تنزيل Aspose.PDF لـ .NET](https://releases.aspose.com/pdf/net/)

بالنسبة لهذا البرنامج التعليمي، تأكد من استخدام الإصدار الأحدث من المكتبة.

### بيئة التطوير
ستحتاج أيضًا إلى بيئة تطوير .NET مثل Visual Studio. إنها بيئة التطوير المتكاملة المثالية لتطوير C#، وستجعل تجربة البرمجة لديك سلسة وفعالة.

### رخصة مؤقتة أو كاملة
يمكنك البدء بفترة تجريبية مجانية من Aspose.PDF، ولكن لتجنب أي قيود، يُفضل استخدام ترخيص مؤقت أو كامل. إليك كيفية الحصول عليه:
- [نسخة تجريبية مجانية](https://releases.aspose.com/)
- [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/)
- [شراء الترخيص الكامل](https://purchase.aspose.com/buy)

بمجرد أن تكون مستعدًا لكل هذه الأساسيات، فلننتقل إلى الخطوة التالية!

## استيراد الحزم

قبل البدء بالبرمجة، عليك استيراد مساحات الأسماء الضرورية المرفقة مع Aspose.PDF. هذا ضروري للعمل مع المستندات والصفحات ومقاطع النصوص وغيرها. أضف الكود التالي في بداية ملف C#:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
```

الآن، دعنا نقوم بتقسيم كود المثال خطوة بخطوة حتى تتمكن من تدوير النص مثل المحترفين!

## الخطوة 1: تهيئة كائن المستند

تبدأ كل معالجة لملف PDF بإنشاء أو تحميل مستند PDF. هنا، سننشئ مستند PDF جديدًا من الصفر باستخدام Aspose.PDF.

نحن ننشئ جديدا `Document` الكائن الذي يُمثل ملف PDF. في البداية، هذا المستند فارغ.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
// تهيئة كائن المستند
Document pdfDocument = new Document();
```

توضيح:  
- `dataDir`:هذا هو الدليل الذي سيتم حفظ ملف PDF النهائي فيه.
- `Document pdfDocument = new Document();`:يؤدي هذا إلى تهيئة مستند PDF جديد فارغ. 

## الخطوة 2: إضافة صفحة إلى المستند

بعد ذلك، نحتاج إلى إضافة صفحة إلى المستند. ملف PDF هو في الأساس مجموعة من الصفحات، وتحتاج إلى صفحة واحدة على الأقل لإضافة المحتوى.

```csharp
// احصل على صفحة معينة
Page pdfPage = (Page)pdfDocument.Pages.Add();
```

بدون إضافة صفحة، لن يكون هناك قماش لرسم أو وضع النص عليه!

## الخطوة 3: إنشاء جزء النص الأول

الآن يأتي الجزء المثير! لنُضيف جزءًا نصيًا إلى ملف PDF. الجزء النصي هو نص بخصائص مُحددة، مثل الخط والحجم والموضع.

```csharp
// إنشاء جزء نصي
TextFragment textFragment1 = new TextFragment("main text");
textFragment1.Position = new Position(100, 600);
textFragment1.TextState.FontSize = 12;
textFragment1.TextState.Font = FontRepository.FindFont("TimesNewRoman");
```

- TextFragment("main text"): يؤدي هذا إلى إنشاء جزء نص جديد يحتوي على المحتوى "main text".
- الموضع (١٠٠، ٦٠٠): يُحدد موضع النص في الصفحة. الرقم الأول هو إحداثي س، والثاني هو إحداثي ص.
- TextState.FontSize: يحدد حجم خط النص.
- FontRepository.FindFont: يبحث عن الخط المحدد لتطبيقه على النص.

## الخطوة 4: إنشاء أجزاء النص الدائرية

دعونا نضيف المزيد من أجزاء النص، ولكن هذه المرة سنقوم بتدويرها إلى زوايا مختلفة!

### تدوير جزء النص إلى 45 درجة

```csharp
// إنشاء جزء نصي مُدار
TextFragment textFragment2 = new TextFragment("rotated text");
textFragment2.Position = new Position(200, 600);
textFragment2.TextState.FontSize = 12;
textFragment2.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment2.TextState.Rotation = 45;
```

وهنا التغيير الرئيسي هو:
- TextState.Rotation: تحدد هذه الخاصية زاوية الدوران لجزء النص، وفي هذه الحالة تكون 45 درجة.

### تدوير جزء النص إلى 90 درجة

```csharp
// إنشاء جزء نصي مُدار
TextFragment textFragment3 = new TextFragment("rotated text");
textFragment3.Position = new Position(300, 600);
textFragment3.TextState.FontSize = 12;
textFragment3.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment3.TextState.Rotation = 90;
```

في هذه الحالة، الدوران هو 90 درجة.

## الخطوة 5: إضافة أجزاء نصية إلى صفحة PDF

الآن بعد أن أصبح لدينا جميع أجزاء النص جاهزة، فقد حان الوقت لإضافتها إلى صفحة PDF باستخدام فئة TextBuilder.

```csharp
// إنشاء كائن TextBuilder
TextBuilder textBuilder = new TextBuilder(pdfPage);
// إضافة جزء النص إلى صفحة PDF
textBuilder.AppendText(textFragment1);
textBuilder.AppendText(textFragment2);
textBuilder.AppendText(textFragment3);
```

تساعد فئة TextBuilder في إضافة أجزاء نصية متعددة إلى صفحة واحدة، مما يمنحك المرونة اللازمة للتعامل معها بشكل فردي.

## الخطوة 6: حفظ مستند PDF

أخيرًا، احفظ المستند في المجلد المحدد. بدون هذه الخطوة، سيضيع كل جهدك هباءً!

```csharp
// حفظ المستند
pdfDocument.Save(dataDir + "TextFragmentTests_Rotated1_out.pdf");
```

لقد نجحت في تدوير نص في ملف PDF باستخدام Aspose.PDF لـ .NET. يمكنك الآن فتح ملف PDF لعرض أجزاء النص المُدارة!

## خاتمة

يُضفي تدوير النص في ملفات PDF لمسةً احترافيةً على مستنداتك، مما يجعلها جذابةً بصريًا وفريدةً. مع Aspose.PDF لـ .NET، يُمكنك بسهولةٍ فائقةٍ التعامل مع أجزاء النص، مما يمنحك تحكمًا كاملًا في كيفية ظهور محتواك. الآن وقد تعلّمت كيفية تدوير النص، يُمكنك تجربة زوايا وتخطيطاتٍ مختلفةٍ لتناسب احتياجات مشروعك.

## الأسئلة الشائعة

### هل يمكنني تدوير أجزاء النص في أي زاوية؟
نعم! يمكنك ضبط `TextState.Rotation` يمكنك تدوير النص حسب الحاجة إلى أي درجة (حتى الزوايا السلبية).

### هل يمكنني استخدام خطوط مختلفة لكل جزء من النص؟
بالتأكيد. يمكنك تخصيص خط كل جزء نصي باستخدام `FontRepository.FindFont` ومرر الخط الذي تريد تطبيقه.

### هل يدعم Aspose.PDF ملفات PDF متعددة الصفحات؟
نعم، يمكنك إضافة صفحات متعددة إلى مستند PDF الخاص بك ومعالجة كل صفحة بشكل مستقل.

### هل هناك حد لعدد أجزاء النص التي يمكنني إضافتها؟
لا، يمكنك إضافة أي عدد من النصوص. فقط تأكد من وضعها بشكل صحيح في الصفحة.

### هل يمكنني تعديل أجزاء النص بعد إضافتها؟
نعم، بمجرد إضافة جزء من النص، لا يزال بإمكانك تحديث خصائصه أو إزالته من الصفحة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}