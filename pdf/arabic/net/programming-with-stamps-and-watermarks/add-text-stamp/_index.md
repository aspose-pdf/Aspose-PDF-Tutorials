---
"description": "تعرف على كيفية إضافة طابع نصي في ملف PDF باستخدام Aspose.PDF لـ .NET من خلال دليلنا خطوة بخطوة ورفع مستوى عروض المستندات الخاصة بك."
"linktitle": "إضافة ختم نصي في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة ختم نصي في ملف PDF"
"url": "/ar/net/programming-with-stamps-and-watermarks/add-text-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ختم نصي في ملف PDF

## مقدمة

في عصرنا الرقمي، تُعدّ ملفات PDF تنسيقًا شائعًا لمشاركة المستندات وتسليمها. سواء كنت مطورًا، أو منشئ محتوى، أو مجرد شخص يبحث عن تحسين ملفات PDF الخاصة به، فإن معرفة كيفية التعامل مع ملفات PDF برمجيًا تُحدث فرقًا كبيرًا. من الميزات الرائعة التي قد ترغب في الاستفادة منها إمكانية إضافة طوابع نصية إلى ملفات PDF. تُضفي هذه الطوابع لمسة احترافية على مستنداتك أو تُبرز معلومات مهمة، مثل "نموذج" أو "سري" أو حتى علامة مائية.

## المتطلبات الأساسية

قبل أن نبدأ بشرح الكود، هناك بعض المتطلبات الأساسية لضمان إعداد كل شيء بشكل صحيح. إليك ما ستحتاجه:

1. Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF في مشروعك. إذا لم تقم بذلك بعد، يمكنك تنزيلها من [موقع Aspose](https://releases.aspose.com/pdf/net/).
2. Visual Studio أو بيئة تطوير متكاملة متوافقة: ستحتاج إلى بيئة تطوير لكتابة وتشغيل أكواد .NET. يُعد Visual Studio الخيار الأكثر شيوعًا بين المطورين.
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة بلغة C# ومبادئ البرمجة الكائنية التوجه على فهم الأمثلة بشكل أفضل.
4. ملف PDF نموذجي: يجب أن يكون لديك ملف PDF جاهز للعمل عليه. يمكنك إنشاء ملف PDF أساسي أو استخدام أي ملف PDF موجود لاختبار الأداء.

بمجرد الانتهاء من هذه المتطلبات الأساسية، يمكننا الانتقال إلى الترميز!

## استيراد الحزم

الآن، لنستورد الحزم اللازمة. هذه الخطوة بالغة الأهمية لأنها تُتيح الفئات والأساليب من مكتبة Aspose في مشروعك.

### استيراد تجميع Aspose.PDF

للبدء، عليك استيراد مساحة اسم Aspose.PDF. في أعلى ملف C#، أضف الأمر التالي باستخدام:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

سيسمح لك هذا بالوصول إلى الفئات الأساسية لإنشاء مستندات PDF ومعالجتها.

الآن، لنبدأ بجوهر الدرس. سنُقسّم العملية إلى خطوات واضحة وموجزة. ستُرشدك كل خطوة خلال شرح الكود لإضافة ختم نصي إلى ملف PDF.

## الخطوة 1: إعداد دليل المستندات

أولاً، عليك تحديد المجلد الذي تُخزَّن فيه وثيقة PDF. هذا يعني أن الكود البرمجي الخاص بك يجب أن يعرف مكان ملف PDF الذي تريد تعديله.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

شرح: استبدال `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي يوجد به ملف PDF الخاص بك (`AddTextStamp.pdf`) يتم تخزينه. سيتم استخدام هذا المسار لاحقًا لفتح ملف PDF المعدّل وحفظه.

## الخطوة 2: افتح مستند PDF

بعد ذلك، سنفتح مستند PDF باستخدام `Document` الفئة من مساحة اسم Aspose.PDF.

```csharp
// فتح المستند
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

التوضيح: هنا، نقوم بإنشاء مثيل لـ `Document` الصف، ثم تمرير المسار إلى ملف PDF. سيؤدي هذا إلى تحميل ملف PDF حتى نتمكن من التعامل معه.

## الخطوة 3: إنشاء ختم نصي

الآن، سنقوم بإنشاء ختم نصي سنقوم بتطبيقه لاحقًا على مستند PDF الخاص بنا.

```csharp
// إنشاء ختم نصي
TextStamp textStamp = new TextStamp("Sample Stamp");
```

الشرح: `TextStamp` تم إنشاء الكائن بالنص الذي تريد عرضه. في هذه الحالة، نستخدم "نموذج الختم" كنص للختم.

## الخطوة 4: تعيين خصائص الطوابع

لتخصيص طابعتك، يمكننا ضبط خصائص متنوعة، مثل لون الخلفية، والموضع، والدوران. لنبدأ الآن:

```csharp
// تعيين ما إذا كان الختم هو الخلفية
textStamp.Background = true;

// مجموعة الأصل
textStamp.XIndent = 100;
textStamp.YIndent = 100;

// تدوير الختم
textStamp.Rotate = Rotation.on90;
```

توضيح:
- الخلفية: ضبط هذا على `true` يعني أن الختم سيظهر خلف محتوى ملف PDF.
- XIndent وYIndent: تحدد هاتان الخاصيتان موضع الطابع على الصفحة. في هذا المثال، سيتم وضع الطابع على بُعد ١٠٠ وحدة من الحافتين اليسرى والعلوية للصفحة.
- التدوير: يُدوّر الختم بزاوية 90 درجة. يمكنك اختيار خيارات تدوير مختلفة بناءً على متطلبات تصميمك.

## الخطوة 5: تخصيص خصائص النص

بعد ذلك، دعنا نتحلى بالإبداع من خلال تخصيص مظهر النص داخل طابعتنا:

```csharp
// تعيين خصائص النص
textStamp.TextState.Font = FontRepository.FindFont("Arial");
textStamp.TextState.FontSize = 14.0F;
textStamp.TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
textStamp.TextState.ForegroundColor = Aspose.Pdf.Color.FromRgb(Color.Aqua);
```

توضيح:
- الخط: نحن نستخدم الخط Arial ونجعله غامقًا ومائلًا.
- حجم الخط: تم ضبطه على 14 نقطة.
- لون المقدمة: باستخدام RGB لتعيين لون النص إلى أزرق مائي. لا تتردد في تغيير اللون ليناسب احتياجات علامتك التجارية أو تصميمك!

## الخطوة 6: إضافة الختم إلى صفحة PDF

الآن حان الوقت لإضافة الختم إلى صفحة معينة من مستند PDF.

```csharp
// إضافة طابع إلى صفحة معينة
pdfDocument.Pages[1].AddStamp(textStamp);
```

شرح: في هذا المثال، أُضيف الطابع إلى الصفحة الأولى من ملف PDF (الصفحات مُفهرسة بصفحة واحدة). عدّل رقم الصفحة حسب الحاجة لمستندك.

## الخطوة 7: احفظ ملف PDF المعدّل

وأخيرًا، دعنا نحفظ المستند باستخدام ختم النص المضاف حديثًا.

```csharp
dataDir = dataDir + "AddTextStamp_out.pdf";

// حفظ مستند الإخراج
pdfDocument.Save(dataDir);
Console.WriteLine("\nText stamp added successfully.\nFile saved at " + dataDir);
```

توضيح: نُحدد مسارًا جديدًا لملف الإخراج، ثم نحفظ المستند المُعدَّل. بعد الحفظ، يُطبع المسار في وحدة التحكم، مُؤكِّدًا نجاح العملية.

## خاتمة

تهانينا! لقد نجحت في إضافة ختم نصي إلى ملف PDF باستخدام Aspose.PDF لـ .NET. تتيح لك هذه الطريقة إضافة تعليقات توضيحية إلى مستنداتك بكفاءة، مما يعزز احترافيتها وسهولة استخدامها. سواءً كنت تضيف علامات مائية أو توقيعات أو ملاحظات بسيطة، توفر مكتبة Aspose أدوات فعّالة للتعامل مع ملفات PDF بسهولة.

## الأسئلة الشائعة

### ما هو ختم النص في ملف PDF؟
ختم النص هو طبقة رسومية تحتوي على نص يمكن وضعه على مستند PDF، وغالبًا ما يستخدم للتعليقات التوضيحية أو العلامات المائية.

### هل يمكنني تخصيص الختم بالصور؟
نعم، يدعم Aspose.PDF أيضًا إضافة طوابع الصور، مما يوفر مرونة أكبر في التصميم.

### ما هي لغات البرمجة التي يمكنني استخدامها مع Aspose.PDF؟
يركز Aspose.PDF في المقام الأول على .NET، ولكن هناك إصدارات متوفرة للغات أخرى مثل Java وPython.

### كيف أحصل على ترخيص مؤقت لـ Aspose.PDF؟
يمكنك التقدم بطلب للحصول على ترخيص مؤقت عن طريق زيارة [رابط الشراء](https://purchase.aspose.com/temporary-license/) على موقعهم الإلكتروني.

### أين يمكنني العثور على الدعم لـ Aspose.PDF؟
يتوفر الدعم لـ Aspose.PDF على [منتدى الدعم](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}