---
"description": "تعرف على كيفية البحث والحصول على نص من جميع صفحات مستند PDF باستخدام Aspose.PDF لـ .NET."
"linktitle": "ابحث واحصل على النص بالكامل"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "ابحث واحصل على النص بالكامل"
"url": "/ar/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ابحث واحصل على النص بالكامل

## مقدمة

هل سبق لك أن احتجت إلى استخراج نص معين من ملف PDF ولكن واجهت صعوبة في ذلك؟ قد تبدو ملفات PDF أحيانًا وكأنها حاويات مغلقة، مما يُصعّب الحصول على المعلومات التي تحتاجها. لكن إليك الخبر السار: مع Aspose.PDF لـ .NET، يمكنك بسهولة البحث عن نص واسترجاعه من أي ملف PDF. توفر هذه المكتبة القوية كل ما تحتاجه للعمل مع ملفات PDF في تطبيقات .NET، مما يجعل استخراج النص في غاية السهولة. في هذا البرنامج التعليمي، سنشرح لك عملية البحث عن نص واستخراجه من ملف PDF باستخدام Aspose.PDF لـ .NET. سواء كنت تُنشئ أداة تحليل نصوص أو تحتاج فقط إلى أتمتة استخراج البيانات من تقارير PDF، فأنت في المكان المناسب!

## المتطلبات الأساسية

قبل أن ننتقل إلى الكود، دعنا نتأكد من إعداد كل شيء:

1. Aspose.PDF لـ .NET: ستحتاج إلى تنزيل Aspose.PDF لـ .NET وتثبيته. يمكنك الحصول عليه من صفحة التنزيل. [هنا](https://releases.aspose.com/pdf/net/).
2. بيئة .NET: تأكد من إعداد .NET Framework أو .NET Core على جهاز التطوير الخاص بك.
3. المعرفة الأساسية بلغة C##: يوصى ببعض المعرفة بلغة C# والعمل مع مشاريع .NET.
4. مستند PDF: نموذج لملف PDF سنستخرج منه النص. في هذا المثال، سنستخدم `SearchAndGetTextFromAll.pdf`.

## استيراد الحزم

قبل كتابة أي كود، يجب عليك استيراد المساحات الأساسية اللازمة إلى مشروعك للعمل مع Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

توفر هذه المساحات الاسمية إمكانية الوصول إلى نموذج كائن المستند الخاص بملف PDF وتسمح لنا بمعالجة النص داخل الملف.

دعونا نقسم العملية إلى خطوات بسيطة حتى تتمكن من متابعتها بسهولة.

## الخطوة 1: تعيين دليل المستندات

أولاً، عليك تحديد مسار المجلد الذي يحتوي على ملف PDF. هذا يساعد التطبيق على تحديد الملف الذي ستستخرج منه النص.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- ال `dataDir` يجب أن يشير المتغير إلى الدليل الذي يوجد به `SearchAndGetTextFromAll.pdf` تم تخزين الملف.
- يستبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي على جهازك.

## الخطوة 2: افتح مستند PDF

بعد ذلك، سنفتح مستند PDF باستخدام Aspose.PDF `Document` هدف.

```csharp
// فتح المستند
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- نقوم بإنشاء مثيل جديد لـ `Document` الفئة عن طريق تمرير مسار الملف الكامل لملف PDF.
- سيؤدي هذا إلى تحميل ملف PDF في الذاكرة، مما يجعله جاهزًا للمعالجة.

## الخطوة 3: إنشاء ممتص نص

ال `TextFragmentAbsorber` يُستخدم الكائن للبحث عن نص محدد داخل ملف PDF. في هذه الحالة، سنبحث عن كلمة "نص".

```csharp
// إنشاء كائن TextAbsorber للعثور على جميع حالات عبارة البحث المدخلة
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- ال `TextFragmentAbsorber` يتم تهيئة الأمر بالسلسلة `"text"`وهذا يعني أنه سيبحث عن أي ظهور لكلمة "نص" داخل مستند PDF.

## الخطوة 4: قبول الامتصاص لجميع الصفحات

الآن سنقوم بتوجيه مستند PDF لقبول الممتص والبحث عن النص عبر جميع صفحاته.

```csharp
// قبول الممتص لجميع الصفحات
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- ال `Accept` يتم تطبيق هذه الطريقة على صفحات المستند. سيؤدي هذا إلى البحث في جميع الصفحات عن النص المحدد.

## الخطوة 5: استخراج أجزاء النص

بمجرد أن يقوم الممتص بمسح المستند ضوئيًا، يمكننا استرجاع أجزاء النص المستخرجة.

```csharp
// احصل على أجزاء النص المستخرجة
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- ال `TextFragments` ممتلكات `TextFragmentAbsorber` يقوم بإرجاع مجموعة من كل أجزاء النص التي تتطابق مع مصطلح البحث.

## الخطوة 6: تكرار أجزاء النص

الآن بعد أن أصبح لدينا مجموعة من أجزاء النص، سنقوم بالمرور عليها واستخراج التفاصيل.

```csharp
// التكرار عبر الشظايا
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- ال `foreach` تتكرر الحلقة خلال كل `TextFragment` في المجموعة.
- نقوم بطباعة خصائص مختلفة لكل جزء، مثل النص الفعلي، وموقعه على الصفحة، وتفاصيل الخط، وحجم الخط.
- ال `XIndent` و `YIndent` تعطي الخصائص الإحداثيات الدقيقة لشظية النص داخل ملف PDF.

## خاتمة

وها قد انتهينا! ببضعة أسطر برمجية فقط، نجحنا في البحث عن نص واستخراجه من ملف PDF باستخدام Aspose.PDF لـ .NET. تتيح لك مرونة Aspose.PDF التعامل مع ملفات PDF بطرق متعددة، مما يجعلها خيارًا ممتازًا للمطورين الذين يحتاجون إلى حلول PDF فعّالة في بيئات .NET. يمكنك بسهولة توسيع هذا المثال للبحث عن كلمات أخرى، أو استخراج تفاصيل أكثر، أو حتى التعامل مع محتوى PDF حسب احتياجاتك. نأمل أن يكون هذا الدليل قد قدّم لك نهجًا واضحًا ومباشرًا للتعامل مع ملفات PDF. جرّبه الآن مع ملفات PDF الخاصة بك!

## الأسئلة الشائعة

### هل يمكنني البحث عن كلمات متعددة في وقت واحد؟  
نعم يمكنك تعديل `TextFragmentAbsorber` للبحث عن عبارات متعددة عن طريق تعديل سلسلة البحث وفقًا لذلك.

### ماذا لو كان النص يمتد على عدة أسطر؟  
سيتمكن Aspose.PDF من التعرّف على النص واستخراجه حتى لو امتدّ على عدة أسطر. يمكنك معالجة هذه الأجزاء بشكل فردي.

### كيف أحفظ النص المستخرج في ملف؟  
يمكنك كتابة النص المستخرج إلى ملف باستخدام عمليات الإدخال/الإخراج القياسية لملف C#، مثل `StreamWriter`.

### هل يدعم Aspose.PDF استخراج النص من ملفات PDF الممسوحة ضوئيًا؟  
لا يدعم Aspose.PDF تقنية التعرف الضوئي على الحروف (OCR). بالنسبة لملفات PDF الممسوحة ضوئيًا، ستحتاج إلى أداة OCR للتعرف على النص.

### كيف أتعامل مع ملفات PDF المشفرة؟  
إذا كان ملف PDF الخاص بك محميًا بكلمة مرور، فيمكنك إلغاء قفله باستخدام Aspose.PDF عن طريق تقديم كلمة المرور عند تحميل المستند.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}