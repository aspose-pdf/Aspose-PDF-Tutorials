---
"description": "تعرّف على كيفية إنشاء ملف PDF متعدد الطبقات باستخدام Aspose.PDF لـ .NET. اتبع دليلنا خطوة بخطوة لإضافة نصوص وصور وطبقات إلى ملف PDF الخاص بك بسهولة."
"linktitle": "إنشاء ملف PDF متعدد الطبقات - النهج الثاني"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إنشاء ملف PDF متعدد الطبقات - النهج الثاني"
"url": "/ar/net/programming-with-document/createmultilayerpdfsecondapproach/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF متعدد الطبقات - النهج الثاني

## مقدمة

في عالم اليوم الذي يعج بالمستندات الرقمية، تُعدّ القدرة على إنشاء ملفات PDF احترافية متعددة الطبقات أمرًا بالغ الأهمية. سواءً كنت تُضيف علامات مائية، أو تُدرج نصًا فوق الصور، أو تُنشئ تخطيطات مُعقدة، فأنت بحاجة إلى حل قوي يمنحك تحكمًا كاملاً في طبقات PDF. يُعدّ Aspose.PDF for .NET أداة فعّالة تُسهّل هذه العملية وتُسهّلها.

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من أن لديك ما يلي:

- Aspose.PDF لمكتبة .NET: إذا لم تقم بتثبيتها بعد، فقم بتنزيل [أحدث إصدار هنا](https://releases.aspose.com/pdf/net/).
- بيئة تطوير .NET: يمكنك استخدام Visual Studio أو أي بيئة تطوير متكاملة أخرى تدعم .NET.
- الفهم الأساسي للغة C#: يجب أن تكون على دراية ببرمجة C# لمتابعتها.
- ملف صورة اختبار: ستحتاج إلى ملف صورة (على سبيل المثال، "test_image.png") لاستخدامه في هذا البرنامج التعليمي.

إذا لم يكن لديك ترخيص Aspose.PDF لـ .NET حتى الآن، فيمكنك طلب [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/). للحصول على موارد إضافية، راجع [التوثيق](https://reference.aspose.com/pdf/net/) أو تواصل معنا [يدعم](https://forum.aspose.com/c/pdf/10).

## استيراد الحزم الضرورية

للبدء بإنشاء ملف PDF متعدد الطبقات، عليك استيراد مساحات الأسماء المناسبة. تتيح هذه الحزم استخدام جميع الفئات المطلوبة، مثل `Document`، `Page`، `TextFragment`، و `FloatingBox`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Drawing;
```

الآن بعد أن انتهينا من المتطلبات الأساسية، دعنا ننتقل إلى الجزء الرئيسي: إنشاء ملف PDF متعدد الطبقات.

صُمم هذا الدليل ليشرح كل خطوة بالتفصيل وبطريقة سهلة للمبتدئين. هيا بنا نبدأ!

## الخطوة 1: تهيئة المستند وإعداد المسار

أول شيء نحتاجه هو كائن مستند PDF وطريقة للإشارة إلى الموقع الذي سنحفظ فيه ملف PDF النهائي.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

في هذه القطعة، قمنا بإنشاء `Document` الكائن الذي يمثل ملف PDF الخاص بنا. `dataDir` يجب تعيين المتغير على الدليل الذي تريد حفظ ملف PDF الذي تم إنشاؤه فيه.

## الخطوة 2: إضافة صفحة إلى مستند PDF الخاص بك

يتكون كل مستند PDF من صفحة واحدة أو أكثر. لنُضِف صفحةً إلى مستندنا.

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

هذا الكود يُضيف صفحة فارغة إلى المستند. الأمر بسيط جدًا، أليس كذلك؟ لننتقل الآن إلى إضافة طبقات إلى هذه الصفحة.

## الخطوة 3: إنشاء جزء نصي وتخصيصه

بعد ذلك، سننشئ جزءًا نصيًا. هذا كتلة نصية يمكننا تعديل لونها وحجمها وموقعها.

```csharp
Aspose.Pdf.Text.TextFragment t1 = new Aspose.Pdf.Text.TextFragment("paragraph 3 segment");
t1.TextState.ForegroundColor = Color.Red;
t1.IsInLineParagraph = true;
t1.TextState.FontSize = 12;
```

وإليك ما يحدث:
- ال `TextFragment` هدف `t1` يتم تهيئة النص بالنص "الفقرة 3 المقطع".
- نقوم بتغيير لون النص إلى اللون الأحمر باستخدام `ForegroundColor` ملكية.
- تم ضبط حجم النص إلى 12 نقطة، وتم وضعه في السطر داخل الفقرة باستخدام `IsInLineParagraph`.

## الخطوة 4: إضافة جزء النص إلى FloatingBox

الآن وقد أصبح لدينا جزء نصي، علينا وضعه داخل ملف PDF. بدلًا من إضافته مباشرةً إلى الصفحة، سنستخدم `FloatingBox` لإعطائها موقعًا محددًا.

```csharp
Aspose.Pdf.FloatingBox TextFloatingBox1 = new Aspose.Pdf.FloatingBox(117, 21);
TextFloatingBox1.ZIndex = 1;
TextFloatingBox1.Left = -4;
TextFloatingBox1.Top = -4;
page.Paragraphs.Add(TextFloatingBox1);
TextFloatingBox1.Paragraphs.Add(t1);
```

دعونا نكسر هذا:
- نحن ننشئ `FloatingBox` وتحديد حجمه (117×21).
- ال `ZIndex` تم تعيين الخاصية على 1، مما يعني أنها ستكون في الطبقة السفلية.
- ال `Left` و `Top` الخصائص تحدد الموضع الدقيق للمربع على الصفحة.
- وأخيرا، جزء النص `t1` يتم إضافته داخل المربع العائم، والذي يتم إضافته بعد ذلك إلى الصفحة.

## الخطوة 5: إدراج صورة في صندوق عائم آخر

بعد ذلك، سنضيف صورة إلى ملف PDF. وكما هو الحال مع النص، سنضعها داخل `FloatingBox`.

```csharp
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
image1.File = dataDir + "test_image.png";
Aspose.Pdf.FloatingBox ImageFloatingBox = new Aspose.Pdf.FloatingBox(117, 21);
ImageFloatingBox.Left = -4;
ImageFloatingBox.Top = -4;
ImageFloatingBox.ZIndex = 2;
ImageFloatingBox.Paragraphs.Add(image1);
page.Paragraphs.Add(ImageFloatingBox);
```

وهنا التفصيل:
- نحن ننشئ `Image` الكائن وتعيين المسار إلى ملف الصورة.
- جديد `FloatingBox` يتم إنشاؤه للصورة، بنفس حجم مربع النص العائم.
- يتم وضع مربع الصورة العائمة فوق مربع النص العائم عن طريق ضبطه `ZIndex` الى 2.
- ال `Left` و `Top` الخصائص تضع الصورة بالضبط حيث نريدها.
- تتم إضافة الصورة إلى المربع العائم، والذي تتم إضافته بعد ذلك إلى الصفحة.

## الخطوة 6: حفظ مستند PDF

أخيرًا، سنقوم بحفظ ملف PDF متعدد الطبقات الذي تم إنشاؤه حديثًا في الدليل المحدد.

```csharp
doc.Save(dataDir + @"Multilayer-2ndApproach_out.pdf");
```

سيحفظ هذا السطر ملف PDF باسم "Multilayer-2ndApproach_out.pdf" في المجلد المحدد. تهانينا، لقد أنشأت ملف PDF متعدد الطبقات بنجاح باستخدام Aspose.PDF لـ .NET!

## خاتمة

إنشاء ملف PDF متعدد الطبقات باستخدام Aspose.PDF لـ .NET يتميز بالمرونة والفعالية. سواء كنت ترغب في تراكب النصوص أو الصور أو عناصر أخرى، فإن هذا النهج يمنحك تحكمًا كاملاً في بنية المستند وعرضه.

## الأسئلة الشائعة

### هل يمكنني إنشاء ملفات PDF تحتوي على صفحات متعددة باستخدام Aspose.PDF لـ .NET؟  
نعم، يمكنك إضافة عدد الصفحات الذي تريده عن طريق الاتصال `doc.Pages.Add()` لكل صفحة.

### كيف يمكنني إضافة المزيد من العناصر مثل الأشكال أو التعليقات التوضيحية إلى ملف PDF؟  
يمكنك استخدام `FloatingBox` لأي نوع من المحتوى، بما في ذلك الأشكال والتعليقات التوضيحية وحتى الجداول.

### ما هي تنسيقات الصور التي يدعمها Aspose.PDF لـ .NET؟  
يدعم Aspose.PDF تنسيقات الصور المختلفة، بما في ذلك PNG، وJPEG، وGIF، وBMP.

### هل يمكنني تغيير تعتيم العناصر في ملف PDF؟  
نعم، يمكنك تعديل التعتيم عن طريق ضبط `Alpha` مكون من `Color` هدف.

### كيف يمكنني نقل العناصر إلى مواضع مختلفة في ملف PDF؟  
يمكنك تعديل `Left` و `Top` خصائص `FloatingBox` لإعادة وضع أي عنصر.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}