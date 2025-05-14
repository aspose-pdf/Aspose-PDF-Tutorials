---
"description": "تعرف على كيفية إضافة صورة ورقم صفحة مضمنًا في قسم الرأس في ملف PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل خطوة بخطوة."
"linktitle": "الصورة ورقم الصفحة في قسم الرأس والتذييل المضمن"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "الصورة ورقم الصفحة في قسم الرأس والتذييل المضمن"
"url": "/ar/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section-inline/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# الصورة ورقم الصفحة في قسم الرأس والتذييل المضمن

## مقدمة

Aspose.PDF لـ .NET أداة فعّالة توفر إمكانيات واسعة لمعالجة وإنشاء ملفات PDF. سواءً كنت بحاجة إلى إضافة صور، أو تخصيص رؤوس وتذييلات، أو إدارة النصوص، فإن Aspose.PDF يلبي احتياجاتك. في هذا البرنامج التعليمي، سنستكشف كيفية إضافة صورة ورقم صفحة مضمّن في رأس أو تذييل مستند PDF. لنبدأ مباشرةً ونشرح العملية خطوة بخطوة.

## المتطلبات الأساسية

قبل أن ننتقل إلى الكود، دعنا نتأكد من أن كل شيء جاهز للمتابعة:

- Aspose.PDF لـ .NET: قم بتنزيل الإصدار الأحدث من [صفحة تنزيل ملف PDF من Aspose](https://releases.aspose.com/pdf/net/).
- بيئة التطوير: ستحتاج إلى بيئة تطوير متكاملة لـ C# مثل Visual Studio.
- الترخيص: إذا لم يكن لديك ترخيص بعد، يمكنك الحصول على [رخصة مؤقتة هنا](https://purchase.aspose.com/temporary-license/) أو شراء واحدة كاملة من [متجر أسبووز](https://purchase.aspose.com/buy).

الآن بعد أن أصبحت المتطلبات الأساسية جاهزة، فلنبدأ.

## استيراد الحزم

قبل البدء في الترميز، تأكد من استيراد المساحات الأساسية اللازمة:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

تتيح لك هذه الحزم العمل مع ملفات PDF ومعالجة النصوص.

## الخطوة 1: إعداد دليل المستندات

أول ما علينا فعله هو تحديد مسار المجلد الذي سيُحفظ فيه ملف PDF. يُمكن تخصيص هذا المسار لمجلد مشروعك أو أي مكان آخر على جهازك.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

يحتوي هذا المتغير على الموقع الذي سيتم تخزين مستندك فيه. استبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي.

## الخطوة 2: إنشاء مستند PDF

في هذه الخطوة، نقوم بإنشاء مثيل جديد لـ `Aspose.Pdf.Document` هذا الكائن سيكون بمثابة العمود الفقري لملف PDF الخاص بك.

```csharp
// إنشاء كائن مستند عن طريق استدعاء المنشئ الفارغ الخاص به
Aspose.Pdf.Document pdf1 = new Aspose.Pdf.Document();
```

هنا، نقوم بإنشاء ملف PDF فارغ يمكننا ملؤه بالمحتوى لاحقًا.

## الخطوة 3: إضافة صفحة إلى ملف PDF

يحتاج ملف PDF الخاص بك إلى صفحة واحدة على الأقل لإضافة الرؤوس والتذييلات والمحتوى. لنضف صفحة فارغة إلى مستندنا.

```csharp
// إنشاء صفحة في كائن Pdf
Aspose.Pdf.Page page = pdf1.Pages.Add();
```

عن طريق الاتصال `pdf1.Pages.Add()`، تتم إضافة صفحة جديدة إلى المستند، جاهزة لتخصيص الرأس والتذييل.

## الخطوة 4: إنشاء وتعيين الرأس

الآن حان وقت إنشاء رأس المستند. هنا سنضيف النص والصورة ورقم الصفحة.

```csharp
// إنشاء قسم رأس المستند
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
// تعيين رأس ملف PDF
page.Header = header;
```

نحن ننشئ `HeaderFooter` الكائن وتعيينه إلى `Header` خاصية الصفحة، مما يضمن ظهور أي شيء نضيفه إلى الرأس في أعلى الصفحة.

## الخطوة 5: إضافة نص مضمن إلى الرأس

إضافة النص أمر بسيط مثل إنشاء `TextFragment` وحدد خصائصه. لنُضِف نصًا ملونًا إلى رأس الصفحة.

```csharp
// إنشاء كائن نصي
Aspose.Pdf.Text.TextFragment txt1 = new Aspose.Pdf.Text.TextFragment("Aspose.Pdf is a Robust component by");
// حدد اللون
txt1.TextState.ForegroundColor = Color.Blue;
txt1.IsInLineParagraph = true;
```

في هذه الخطوة، نقوم بإنشاء `TextFragment` مع المحتوى "Aspose.Pdf هو مكون قوي من قِبل" وضبط لونه إلى الأزرق. `IsInLineParagraph` تضمن الخاصية أن يكون النص مضمنًا، مما يعني أنه سيظهر على نفس السطر مثل العناصر الأخرى (مثل الصورة والنص الإضافي).

## الخطوة 6: إدراج صورة مضمنة في الرأس

لجعل عنوانك جذابًا بصريًا، يمكنك إضافة صورة مضمنة مع النص. يمكن أن تكون هذه الصورة شعار شركتك أو أي رسم بياني آخر.

```csharp
// إنشاء كائن صورة في القسم
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
// تعيين مسار ملف الصورة
image1.File = dataDir + "aspose-logo.jpg";
// تعيين معلومات عرض الصورة
image1.FixWidth = 50;
image1.FixHeight = 20;
// يشير إلى أن InlineParagraph الخاص بـ seg1 عبارة عن صورة.
image1.IsInLineParagraph = true;
```

هنا نضيف صورة إلى العنوان عن طريق إنشاء `Image` الكائن، وتحديد مساره، وضبط العرض والارتفاع. `IsInLineParagraph` يتأكد من محاذاة الصورة مع النص.

## الخطوة 7: إضافة نص مضمن إضافي لإكمال العنوان

دعنا نضيف المزيد من النص لإكمال العنوان المضمن.

```csharp
Aspose.Pdf.Text.TextFragment txt2 = new Aspose.Pdf.Text.TextFragment(" Pty Ltd.");
txt2.IsInLineParagraph = true;
txt2.TextState.ForegroundColor = Color.Maroon;
header.Paragraphs.Add(txt1);
header.Paragraphs.Add(image1);
header.Paragraphs.Add(txt2);
```

في هذا الجزء نقوم بإنشاء جزء آخر `TextFragment` بمحتوى "Pty Ltd." ولونه كستنائي. تُضاف أجزاء النص والصورة إلى العنوان.

## الخطوة 8: احفظ ملف PDF

بمجرد إعداد الرأس، حان الوقت لحفظ ملف PDF.

```csharp
// احفظ ملف PDF
pdf1.Save(dataDir + "ImageAndPageNumberInHeaderFooter_UsingInlineParagraph_out.pdf");
```

ال `Save` تكتب الطريقة ملف PDF النهائي إلى الموقع المحدد.

## خاتمة

تهانينا! لقد نجحت في إضافة صورة ونص إلى رأس مستند PDF باستخدام Aspose.PDF لـ .NET. شرح لك هذا البرنامج التعليمي الخطوات الأساسية، بما في ذلك إنشاء مستند، وإضافة صفحات، وإدراج رؤوس، وإضافة محتوى مضمّن كالنصوص والصور. يمنحك Aspose.PDF مرونة فائقة لإدارة ملفات PDF، سواءً كنت ترغب في معالجة الرؤوس أو التذييلات أو المحتوى المعقد. 

## الأسئلة الشائعة

### هل يمكنني إضافة رقم الصفحة إلى الرأس أيضًا؟
نعم! يمكنك بسهولة إضافة رقم الصفحة باستخدام `TextFragment` قم بتصنيفها وتنسيقها حسب الحاجة. ما عليك سوى إدراجها في قسم الرأس كمحتوى مضمّن.

### كيف أقوم بتعيين صورة خلفية في الرأس؟
يمكنك استخدام `BackgroundImage` ممتلكات `HeaderFooter` فئة لتعيين صورة خلفية. مع ذلك، هذا ليس محتوىً مضمّنًا، وسيغطي منطقة الرأس بالكامل.

### هل من الممكن استخدام صيغ أخرى للصور غير JPEG؟
بالتأكيد! يدعم Aspose.PDF تنسيقات صور متنوعة مثل PNG وBMP وGIF.

### هل يمكنني تخصيص خط النص في العنوان؟
نعم يمكنك استخدام `TextState` كائن لتغيير الخط والحجم ونمط النص.

### هل أحتاج إلى ترخيص لاستخدام Aspose.PDF لـ .NET؟
نعم، يتطلب Aspose.PDF ترخيصًا للاستخدام الإنتاجي، ولكن يمكنك البدء بـ [تجربة مجانية هنا](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}