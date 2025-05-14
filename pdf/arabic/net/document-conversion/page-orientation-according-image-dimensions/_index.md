---
"description": "تعرف على كيفية إنشاء ملفات PDF باستخدام Aspose.PDF لـ .NET، وتعيين اتجاه الصفحة استنادًا إلى أبعاد الصورة في هذا الدليل خطوة بخطوة."
"linktitle": "اتجاه الصفحة حسب أبعاد الصورة"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "اتجاه الصفحة حسب أبعاد الصورة"
"url": "/ar/net/document-conversion/page-orientation-according-image-dimensions/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# اتجاه الصفحة حسب أبعاد الصورة

## مقدمة

مرحبًا بك في عالم Aspose.PDF لـ .NET! إذا كنت ترغب في إنشاء مستندات PDF أو تعديلها أو تحويلها برمجيًا، فأنت في المكان المناسب. Aspose.PDF مكتبة فعّالة تُمكّن المطورين من العمل مع ملفات PDF بسلاسة. في هذا الدليل، سنشرح لك عملية ضبط اتجاهات الصفحات بناءً على أبعاد الصورة. سواء كنت مطورًا محترفًا أو مبتدئًا، سيزودك هذا البرنامج التعليمي بالمعرفة اللازمة لبدء استخدام Aspose.PDF.

## المتطلبات الأساسية

قبل أن نتعمق في الكود، دعنا نتأكد من أن لديك كل ما تحتاجه للمتابعة:

1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. إنه أفضل بيئة تطوير متكاملة لتطوير .NET.
2. .NET Framework: يفترض هذا الدليل أنك تستخدم .NET Framework. تأكد من تثبيت الإصدار المناسب.
3. Aspose.PDF لـ .NET: يمكنك تنزيل المكتبة من [موقع Aspose](https://releases.aspose.com/pdf/net/)إذا كنت تريد تجربته أولاً، يمكنك الحصول على [نسخة تجريبية مجانية](https://releases.aspose.com/).
4. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم الأمثلة بشكل أفضل.

## استيراد الحزم

للبدء، عليك استيراد الحزم اللازمة. إليك كيفية القيام بذلك:

1. افتح مشروع Visual Studio الخاص بك.
2. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول وحدد "إدارة حزم NuGet".
3. بحث عن `Aspose.PDF` وتثبيته.

الآن بعد أن قمنا بإعداد كل شيء، دعنا نقوم بتقسيم المثال خطوة بخطوة.

## الخطوة 1: إعداد دليل المستندات الخاص بك

أولاً، عليك تحديد مسار مجلد المستندات الذي تُخزَّن فيه صورك. هنا سيبحث Aspose عن ملفات JPG.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

يستبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي لصورك. هذا أمر بالغ الأهمية، لأنه إذا لم يتمكن Aspose من العثور على صورك، فلن يتمكن من إنشاء ملف PDF.

## الخطوة 2: إنشاء مستند PDF جديد

بعد ذلك، أنشئ مستند PDF جديدًا. هنا ستُضاف جميع صورك.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

يقوم هذا الخط بتهيئة مثيل جديد لـ `Document` الفئة التي تمثل ملف PDF الخاص بك.

## الخطوة 3: استرداد ملفات الصور

الآن، لنسترد جميع ملفات JPG من المجلد المحدد. يتم ذلك باستخدام `Directory.GetFiles` طريقة.

```csharp
string[] fileEntries = Directory.GetFiles(dataDir, "*.JPG");
```

سيمنحك هذا السطر مجموعة من أسماء الملفات التي تُطابق صيغة JPG. تأكد من احتواء مجلدك على بعض صور JPG ليعمل هذا!

## الخطوة 4: تكرار كل صورة

ستحتاج إلى تصفح كل ملف صورة وإضافته إلى مستند PDF. إليك كيفية القيام بذلك:

```csharp
int counter;
for (counter = 0; counter < fileEntries.Length - 1; counter++)
{
    // إنشاء كائن صفحة
    Aspose.Pdf.Page page = doc.Pages.Add();
```

في هذه الحلقة، تقوم بإنشاء صفحة جديدة لكل صورة. `doc.Pages.Add()` تضيف الطريقة صفحة جديدة إلى مستند PDF الخاص بك.

## الخطوة 5: إنشاء كائن صورة

لكل صورة، تحتاج إلى إنشاء `Image` الكائن الذي سيحمل بيانات الصورة.

```csharp
    Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
    image1.File = fileEntries[counter];
```

هنا، يمكنك تعيين ملف الصورة الحالي إلى `Image` هذا ضروري لإضافة الصورة إلى ملف PDF.

## الخطوة 6: التحقق من أبعاد الصورة

قبل إضافة الصورة إلى ملف PDF، يجب عليك التحقق من أبعادها لتحديد اتجاه الصفحة.

```csharp
    Bitmap myimage = new Bitmap(fileEntries[counter]);
    if (myimage.Width > page.PageInfo.Width)
        page.PageInfo.IsLandscape = true;
    else
        page.PageInfo.IsLandscape = false;
```

يتحقق هذا المقتطف من أن عرض الصورة أكبر من عرض الصفحة. في هذه الحالة، يكون اتجاه الصفحة أفقيًا، وإلا، يبقى في الوضع الرأسي.

## الخطوة 7: إضافة الصورة إلى ملف PDF

الآن بعد أن قمت بتعيين الاتجاه، حان الوقت لإضافة الصورة إلى مستند PDF.

```csharp
    page.Paragraphs.Add(image1);
}
```

يُضيف هذا السطر الصورة إلى مجموعة فقرات الصفحة الحالية. يشبه الأمر وضع صورة في إطار!

## الخطوة 8: حفظ مستند PDF

وأخيرًا، يتعين عليك حفظ مستند PDF في الدليل المحدد.

```csharp
doc.Save(dataDir + "SetPageOrientation_out.pdf");
```

يحفظ هذا السطر المستند باسم `SetPageOrientation_out.pdf`تأكد من مراجعة دليل المستندات لديك للحصول على ملف PDF الذي تم إنشاؤه حديثًا!

## خاتمة

وها أنت ذا! لقد أنشأتَ بنجاح مستند PDF باستخدام Aspose.PDF لـ .NET، مع ضبط اتجاه الصفحة بناءً على أبعاد الصور. تفتح هذه المكتبة الفعّالة آفاقًا واسعة للعمل مع ملفات PDF في تطبيقاتك. سواءً كنتَ تُنشئ تقارير أو فواتير أو أي نوع آخر من المستندات، فإن Aspose.PDF يُلبّي جميع احتياجاتك.

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وتحويلها برمجيًا.

### كيف أقوم بتثبيت Aspose.PDF؟
يمكنك تثبيت Aspose.PDF عبر NuGet Package Manager في Visual Studio أو تنزيله من [موقع Aspose](https://releases.aspose.com/pdf/net/).

### هل يمكنني استخدام Aspose.PDF مجانًا؟
نعم، تقدم Aspose [نسخة تجريبية مجانية](https://releases.aspose.com/) لتتمكن من اختبار المكتبة قبل الشراء.

### أين يمكنني العثور على الدعم لـ Aspose.PDF؟
يمكنك العثور على الدعم على [منتدى Aspose](https://forum.aspose.com/c/pdf/10).

### ما هي أنواع الملفات التي يمكنني تحويلها إلى PDF باستخدام Aspose؟
يدعم Aspose.PDF مجموعة واسعة من تنسيقات الملفات، بما في ذلك الصور، ومستندات Word، وجداول بيانات Excel، والمزيد.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}