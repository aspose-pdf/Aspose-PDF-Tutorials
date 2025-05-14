---
"description": "تعلم كيفية البحث عن النصوص في ملفات PDF وتظليلها باستخدام مستطيلات باستخدام Aspose.PDF لـ .NET! دليل تعليمي سهل خطوة بخطوة لتحسين مهاراتك في التعامل مع ملفات PDF."
"linktitle": "البحث عن النص ورسم المستطيل"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "البحث عن النص ورسم المستطيل"
"url": "/ar/net/programming-with-text/search-text-and-draw-rectangle/"
"weight": 460
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# البحث عن النص ورسم المستطيل

## مقدمة

هل ترغب في تحسين مهاراتك في التعامل مع ملفات PDF؟ هل ترغب في تعلم كيفية البحث عن نص محدد في ملفات PDF وتظليله بمستطيل؟ لقد وجدتَ الدليل الأمثل! سأشرح لك اليوم كيفية استخدام Aspose.PDF لـ .NET للبحث عن نص في مستند PDF ورسم مستطيلات حوله. ستوفر هذه المقالة شرحًا تفصيليًا خطوة بخطوة، مصممًا بوضوح وفائدة، مما يضمن لك سهولة اتباع هذه التقنيات وتطبيقها في مشاريعك. 

## المتطلبات الأساسية

قبل الخوض في البرنامج التعليمي، دعنا نجهز ما تحتاجه لضمان سير العمل بسلاسة:

1. الفهم الأساسي لـ .NET: يجب أن تكون على دراية ببرمجة C# وإطار عمل .NET لمتابعة هذا البرنامج التعليمي بشكل فعال.
   
2. تثبيت Visual Studio: ستحتاج إلى بيئة تطوير متكاملة (IDE) لكتابة واختبار شفرتك البرمجية. يُعد Visual Studio Community خيارًا رائعًا، وهو مجاني.
   
3. Aspose.PDF لـ .NET: يجب تثبيت مكتبة Aspose.PDF في مشروعك. يمكنك تنزيلها. [هنا](https://releases.aspose.com/pdf/net/) أو فكر في [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) للحصول على ميزات موسعة.
   
4. نموذج مستند PDF: بالنسبة لهذا البرنامج التعليمي، ستحتاج إلى ملف PDF نموذجي باسم `SearchAndGetTextFromAll.pdf` تم تخزينها في دليل المشروع الخاص بك. 

## استيراد الحزم

للبدء، ستحتاج أولًا إلى استيراد الحزم اللازمة إلى مشروع .NET الخاص بك. اتبع الخطوات التالية:

### افتح برنامج Visual Studio

قم بتشغيل Visual Studio وإنشاء تطبيق وحدة تحكم جديد أو استخدم تطبيقًا موجودًا حيث تريد تنفيذ وظائف PDF.

### أضف Aspose.PDF إلى مشروعك

1. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
2. حدد "إدارة حزم NuGet".
3. بحث عن `Aspose.PDF` وتثبيت الإصدار الأحدث.

من خلال القيام بذلك، فإنك تضع الأساس لجميع عمليات التلاعب المذهلة بملفات PDF التي أنت على وشك القيام بها.

## استيراد مساحات الأسماء

في الجزء العلوي من ملف البرنامج الخاص بك، قد ترغب في استيراد المساحات ذات الصلة من مكتبة Aspose:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Facades;
```

يجعل هذا من الأسهل الوصول إلى الفئات والطرق داخل مكتبة Aspose.PDF لمهامك.


الآن بعد أن قمت بإعداد كل شيء، دعنا نقوم بتقسيم عملية البحث عن نص في ملف PDF ورسم مستطيل حوله إلى خطوات يمكن التحكم فيها.

## الخطوة 1: تعيين المسار للمستند الخاص بك

أولاً، حدد مسار ملف PDF. تأكد من استبدال `YOUR DOCUMENT DIRECTORY` مع المسار الفعلي الذي تريده `SearchAndGetTextFromAll.pdf` يتم تخزينها.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## الخطوة 2: افتح مستند PDF

بعد ذلك، قم بإنشاء مثيل لـ `Document` الفئة لتحميل ملف PDF الخاص بك:

```csharp
Document document = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

يفتح هذا السطر من التعليمات البرمجية ملف PDF المحدد، مما يسمح لك بمعالجته بشكل أكبر.

## الخطوة 3: إنشاء ممتص نص

الآن، ستحتاج إلى طريقة للبحث عن نص داخل المستند. لهذا، نستخدم `TextFragmentAbsorber`:

```csharp
TextFragmentAbsorber textAbsorber = new TextFragmentAbsorber(@"[\S]+");
```

التعبير العادي `@"[\S]+"` تم تصميمه ليتوافق مع أي سلسلة غير فارغة في ملف PDF. 

## الخطوة 4: تكوين خيارات البحث النصي

بعد ذلك، يجب عليك إعداد خيارات البحث النصي:

```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textAbsorber.TextSearchOptions = textSearchOptions;
```

هنا، `true` تعني هذه المعلمة أن البحث سيكون حساسًا لحالة الأحرف. يمكنك ضبطه على `false` إذا كنت تريد بحثًا لا يراعي حالة الأحرف.

## الخطوة 5: قبول امتصاص النص في المستند

معك `TextFragmentAbsorber` وبعد أن أصبحت خيارات البحث جاهزة، فقد حان الوقت لاستيعاب النص من المستند:

```csharp
document.Pages.Accept(textAbsorber);
```

تقوم هذه الطريقة بفحص كل صفحة في ملف PDF الخاص بك للعثور على أجزاء نصية تتطابق مع النمط المحدد.

## الخطوة 6: إنشاء محرر محتوى Pdf

لرسم الأشكال على المستند، ستحتاج إلى `PdfContentEditor`:

```csharp
var editor = new PdfContentEditor(document);
```

يتيح لك هذا المحرر التعامل مع محتوى PDF وتحريره بسهولة.

## الخطوة 7: تكرار أجزاء النص التي تم العثور عليها

الآن، قد ترغب في المرور عبر أجزاء النص التي تم العثور عليها لرسم مستطيلات حولها:

```csharp
foreach (TextFragment textFragment in textAbsorber.TextFragments)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        DrawBox(editor, textFragment.Page.Number, textSegment, System.Drawing.Color.Red);
    }
}
```

تتكرر هذه الحلقة على كل جزء من النص وأجزائه، وتستدعي `DrawBox` طريقة رسم المستطيل.

## الخطوة 8: تحديد طريقة DrawBox

يجب عليك تحديد `DrawBox` طريقة ستتولى رسم المستطيل. إليك تطبيق بسيط:

```csharp
private static void DrawBox(PdfContentEditor editor, int pageNumber, TextSegment textSegment, System.Drawing.Color color)
{
    // حساب أبعاد المستطيل بناءً على مقطع النص
    float x = textSegment.Rectangle.LLX;
    float y = textSegment.Rectangle.LLY;
    float width = textSegment.Rectangle.Width;
    float height = textSegment.Rectangle.Height;

    // ارسم مستطيلاً باستخدام القيم المحسوبة
    editor.DrawRectangle(pageNumber, x, y, width, height, color, 1);
}
```

تحدد هذه الطريقة موضع وحجم المستطيل استنادًا إلى المستطيل المحيط بالجزء وتستخدم المحرر لرسمه.

## الخطوة 9: حفظ المستند المعدّل

بعد رسم المستطيلات حول النص الموجود، يمكنك حفظ المستند المعدل:

```csharp
dataDir = dataDir + "SearchTextAndDrawRectangle_out.pdf";
document.Save(dataDir);
```

تأكد من حفظ الملف الجديد باسم مميز لتجنب الكتابة فوق المستند الأصلي.

## الخطوة 10: رسالة التأكيد

أخيرًا، اطبع رسالة تأكيد إلى وحدة التحكم لإعلامك بنجاح العملية:

```csharp
Console.WriteLine("\nRectangle drawn successfully on searched text.\nFile saved at " + dataDir);
```

وها أنت ذا! لقد أنشأتَ بنجاح برنامجًا نصيًا للبحث عن نص في ملف PDF وتظليله بمستطيلات.

## خاتمة

تهانينا! لقد اكتسبتَ مهارةً فعّالة تُحسّن بشكل كبير من قدراتك على التعامل مع ملفات PDF باستخدام Aspose.PDF لـ .NET. بخطوات بسيطة، يمكنك البحث عن أي نص في مستندك وتسليط الضوء عليه بصريًا، مما يجعل مستندات PDF أكثر تفاعليةً وسهولةً في الإدارة. لا تتردد في تجربة أنماط تعبيرات عادية وخيارات ألوان مختلفة لجعل هذه الأداة مُخصصة لك!

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة توفر طريقة شاملة لإنشاء مستندات PDF ومعالجتها وتحويلها برمجيًا.

### هل يمكنني استخدام Aspose.PDF مجانًا؟
نعم، يُقدّم Aspose نسخة تجريبية مجانية يُمكنك استخدامها لاختبار وظائف المكتبة. جرّبها. [هنا](https://releases.aspose.com/).

### ما هي لغة البرمجة التي يجب أن أستخدمها مع Aspose.PDF لـ .NET؟
تم تصميم Aspose.PDF لـ .NET ليتم استخدامه مع C# ولغات .NET الأخرى.

### كيف أحصل على المساعدة مع Aspose.PDF؟
يمكنك زيارة منتدى دعم Aspose للحصول على مساعدة بخصوص أي مشكلة أو استفسار لديك. ابحث عن الدعم [هنا](https://forum.aspose.com/c/pdf/10).

### أين يمكنني تنزيل Aspose.PDF لـ .NET؟
يمكنك تنزيل المكتبة من موقع Aspose، [هنا](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}