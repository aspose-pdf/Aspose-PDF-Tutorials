---
"description": "تعرّف على كيفية استبدال نص بناءً على تعبيرات عادية في ملف PDF باستخدام Aspose.PDF لـ .NET. اتبع دليلنا خطوة بخطوة لأتمتة تغييرات النص بكفاءة."
"linktitle": "استبدال تعبير Texton العادي في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "استبدال النص في التعبير العادي في ملف PDF"
"url": "/ar/net/programming-with-text/replace-text-on-regular-expression/"
"weight": 360
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# استبدال النص في التعبير العادي في ملف PDF

## مقدمة

Aspose.PDF for .NET أداة رائعة تُمكّن المطورين من التعامل مع ملفات PDF بسهولة. من ميزاتها الفعّالة إمكانية البحث عن نص باستخدام التعبيرات النمطية واستبداله. إذا سبق لك التعامل مع ملف PDF واحتجت فيه إلى تغيير أنماط نصية مُحددة، مثل التواريخ أو أرقام الهواتف أو الرموز، فهذا هو ما تبحث عنه بالضبط. في هذا البرنامج التعليمي، سأرشدك خلال عملية استبدال النص باستخدام التعبيرات النمطية في ملف PDF. سنُفصّلها في خطوات سهلة الاستخدام لتتمكن من دمج هذه الوظيفة بسلاسة في مشاريعك.

## المتطلبات الأساسية

قبل الغوص في الكود، دعنا نتأكد من إعداد كل شيء:

1. Aspose.PDF لـ .NET: ستحتاج إلى أحدث إصدار من Aspose.PDF لـ .NET. يمكنك تنزيله. [هنا](https://releases.aspose.com/pdf/net/).
2. IDE: Visual Studio أو أي بيئة تطوير متكاملة (IDE) متوافقة مع .NET.
3. .NET Framework: تأكد من تثبيت .NET Framework 4.0 أو إصدار أحدث.
4. مستند PDF: ملف PDF نموذجي حيث تريد البحث عن النص واستبداله.

بمجرد أن يكون كل شيء في مكانه، فأنت جاهز للبدء!

## استيراد الحزم

أول ما علينا فعله هو استيراد الحزم المطلوبة. هذا يضمن وصولنا إلى جميع الفئات والأساليب اللازمة من Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

يتيح لنا هذا العمل مع مستندات PDF والتعامل مع أجزاء النص داخل المستند.

لنبدأ الآن بشرح العملية خطوة بخطوة. تابع معنا خطوات استبدال النص بناءً على التعبيرات العادية.

## الخطوة 1: تحميل مستند PDF

أولاً، عليك تحميل مستند PDF الذي ستُجري عليه عملية استبدال النص. يتم ذلك باستخدام `Document` الفئة من Aspose.PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "SearchRegularExpressionPage.pdf");
```

في هذه الخطوة، استبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي لتخزين ملف PDF. يفتح هذا الكود ملف PDF ويحمّله إلى `pdfDocument` الكائن الذي سنقوم بمعالجته في الخطوات التالية.

## الخطوة 2: تحديد التعبيرات العادية

الآن بعد أن قمت بتحميل المستند، فإن الخطوة التالية هي تحديد التعبير العادي الذي سيبحث عن أنماط النص التي تهمك. على سبيل المثال، إذا كنت ترغب في استبدال نطاق سنة مثل "1999-2000"، يمكنك استخدام التعبير العادي `\d{4}-\d{4}`.

```csharp
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("\\d{4}-\\d{4}"); 
```

هذا الخط ينشئ `TextFragmentAbsorber` سيبحث هذا عن أي رقم مكون من أربعة أرقام، متبوعًا بواصلة، ثم رقم آخر مكون من أربعة أرقام. يمكنك تعديل التعبير العادي حسب الحاجة ليتناسب مع حالة استخدامك الخاصة.

## الخطوة 3: تمكين خيار البحث باستخدام التعبيرات العادية

يتيح لك Aspose.PDF ضبط آلية البحث في النص بدقة. في هذه الحالة، سنمكّن مطابقة التعابير العادية باستخدام `TextSearchOptions` فصل.

```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textFragmentAbsorber.TextSearchOptions = textSearchOptions;
```

من خلال ضبط هذا الخيار على `true`، يمكنك تمكين استخدام التعبيرات العادية للبحث داخل ملف PDF.

## الخطوة 4: تطبيق الممتص على صفحة محددة

بعد ذلك، سوف نطبق `TextFragmentAbsorber` لصفحة معينة من المستند. هذا المثال ينطبق على الصفحة الأولى.

```csharp
pdfDocument.Pages[1].Accept(textFragmentAbsorber);
```

تستخرج هذه الطريقة جميع أجزاء النص المطابقة للتعبير النمطي من الصفحة الأولى للمستند. إذا أردت البحث في المستند بأكمله، يمكنك تكرار البحث في جميع الصفحات.

## الخطوة 5: تكرار النص واستبداله

الآن يأتي الجزء الممتع! سنستعرض أجزاء النص المستخرجة، ونستبدل النص، ونخصص خصائص مثل حجم الخط ونوعه ولونه.

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;

foreach (TextFragment textFragment in textFragmentCollection)
{
    textFragment.Text = "New Phrase"; // استبدله بالنص الجديد
    textFragment.TextState.Font = FontRepository.FindFont("Verdana");
    textFragment.TextState.FontSize = 22;
    textFragment.TextState.ForegroundColor = Aspose.Pdf.Color.FromRgb(System.Drawing.Color.Blue);
    textFragment.TextState.BackgroundColor = Aspose.Pdf.Color.FromRgb(System.Drawing.Color.Green);
}
```

هنا، ستتم عملية تكرار كل جزء نصي يطابق التعبير العادي. في كل تطابق، يُستبدل النص بـ `"New Phrase"`يمكنك أيضًا تخصيص الخط إلى "Verdana"، وتعيين حجم الخط إلى 22، وتغيير ألوان النص والخلفية.

## الخطوة 6: حفظ مستند PDF المحدث

بمجرد إجراء جميع التغييرات، حان الوقت لحفظ مستند PDF المعدل.

```csharp
dataDir = dataDir + "ReplaceTextonRegularExpression_out.pdf";
pdfDocument.Save(dataDir);
```

سيؤدي هذا إلى حفظ ملف PDF المحدث مع جميع بدائل النص في ملف جديد يسمى `ReplaceTextonRegularExpression_out.pdf`.

## الخطوة 7: التحقق من التغييرات

أخيرًا، للتأكد من أن كل شيء يعمل بشكل جيد، اطبع رسالة إلى وحدة التحكم:

```csharp
Console.WriteLine("\nText replaced successfully based on a regular expression.\nFile saved at " + dataDir);
```

ستؤكد هذه الرسالة نجاح عملية استبدال النص وإظهار الموقع الذي تم حفظ ملف PDF الجديد فيه.

## خاتمة

لقد نجحت في استبدال نص في ملف PDF استنادًا إلى تعبيرات عادية باستخدام Aspose.PDF لـ .NET! سواء كنت تُؤتمت معالجة المستندات أو تُنقّي بعض المعلومات القديمة، فهذه الميزة فعّالة للغاية. ببضعة أسطر فقط من التعليمات البرمجية، يمكنك إجراء تغييرات نصية معقدة في مستندات كبيرة في ثوانٍ.

## الأسئلة الشائعة

### هل يمكنني استخدام تعبيرات عادية متعددة في مستند واحد؟
نعم، يمكنك إنشاء عدة `TextFragmentAbsorber` الكائنات، كل منها مع تعبيرات منتظمة مختلفة، وتطبيقها على المستند.

### هل Aspose.PDF لـ .NET متوافق مع .NET Core؟
نعم، يدعم Aspose.PDF لـ .NET كل من .NET Framework و.NET Core.

### هل يمكنني استبدال النص في صفحات متعددة مرة واحدة؟
بالتأكيد! بدلًا من تطبيق الممتص على صفحة واحدة، يمكنك تكراره على جميع الصفحات، أو حتى تطبيقه على المستند بأكمله دفعةً واحدة.

### ماذا لو أردت البحث عن نص لا يميز بين الأحرف الكبيرة والصغيرة؟
يمكنك تعديل التعبيرات العادية لتصبح غير حساسة لحالة الأحرف عن طريق استخدام علامات التعبيرات العادية المناسبة أو تعديل خيارات البحث.

### هل يمكنني استبدال الصور في ملف PDF؟
نعم، يدعم Aspose.PDF لـ .NET أيضًا استبدال الصور ومعالجتها داخل مستندات PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}