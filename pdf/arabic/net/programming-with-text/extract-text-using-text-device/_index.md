---
"description": "تعرف على كيفية استخراج النص من مستند PDF باستخدام جهاز النص في Aspose.PDF لـ .NET."
"linktitle": "استخراج النص باستخدام أداة النص"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "استخراج النص باستخدام أداة النص"
"url": "/ar/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص باستخدام أداة النص

## مقدمة

قد يكون استخراج النص من ملف PDF أمرًا صعبًا، خاصةً عند التعامل مع مستندات ذات تنسيقات مختلفة أو خطوط مُضمنة أو تخطيطات مُعقدة. لكن مع Aspose.PDF لـ .NET، تُصبح هذه العملية في غاية السهولة! سواءً كنت ترغب في تحويل صفحات من ملف PDF إلى نص عادي لمزيد من التحليل أو كنت ترغب ببساطة في استخراج أقسام مُحددة، فإن Aspose.PDF يُلبي احتياجاتك. في هذا البرنامج التعليمي، سنشرح خطوة بخطوة كيفية استخراج النص من ملف PDF باستخدام فئة TextDevice في Aspose.PDF. سنقدم أيضًا شروحات واضحة، لتتمكن من تطبيق نفس الطرق على مشاريعك الخاصة بسهولة.

## المتطلبات الأساسية

قبل البدء في شرح الكود، تأكد من تجهيز كل شيء لمتابعته. إليك ما ستحتاجه:

1. Aspose.PDF لـ .NET: قم بتنزيل الإصدار الأحدث من [صفحة تنزيل Aspose.PDF لـ .NET](https://releases.aspose.com/pdf/net/).
2. بيئة التطوير: Visual Studio أو أي بيئة تطوير C# أخرى.
3. .NET Framework: تأكد من أن مشروعك يستهدف .NET Framework 4.x أو أعلى.
4. ملف PDF للإدخال: ملف PDF ستستخدمه لاستخراج النص. ضعه في مجلد على جهازك (سنشير إليه باسم `YOUR DOCUMENT DIRECTORY`).

## استيراد الحزم

في الجزء العلوي من الكود الخاص بك، ستحتاج إلى استيراد المساحات الأساسية اللازمة للعمل مع Aspose.PDF:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## الخطوة 1: تحميل مستند PDF الخاص بك

قبل استخراج النص، نحتاج إلى تحميل ملف PDF إلى الذاكرة. في هذه الخطوة، ستفتح ملف PDF باستخدام Aspose.PDF. `Document` سيسمح لك هذا بالوصول إلى جميع الصفحات والمحتوى داخل الملف.

```csharp
// حدد المسار إلى مستند PDF الخاص بك
string dataDir = "YOUR DOCUMENT DIRECTORY";

// تحميل مستند PDF
Document pdfDocument = new Document(dataDir + "input.pdf");
```

هنا، نحن نستخدم `Document pdfDocument = new Document(dataDir + "input.pdf");` لتحميل ملف PDF. `dataDir` يحتوي المتغير على مسار مجلد ملف PDF. يتيح لنا هذا الوصول إلى المستند بأكمله، مما يسمح لنا بتصفح الصفحات واستخراج محتواه.

## الخطوة 2: إعداد منشئ سلسلة لتخزين النصوص

بعد تحميل المستند، نحتاج إلى طريقة لتخزين النص المستخرج. لهذا، سنستخدم `StringBuilder` الذي يسمح بتسلسل السلسلة بكفاءة.

```csharp
// StringBuilder لحفظ النص المستخرج
StringBuilder builder = new StringBuilder();
```

نحن نقوم بتهيئة `StringBuilder` مثال، يجمع النص المستخرج من كل صفحة. إنها طريقة أكثر فعالية للتعامل مع السلاسل الكبيرة مقارنةً بتسلسل السلاسل المعتاد في حلقة.

## الخطوة 3: التنقل عبر صفحات PDF

بعد ذلك، نستعرض كل صفحة من مستند PDF لاستخراج النص. سنعالج كل صفحة على حدة باستخدام `TextDevice` الفئة المسؤولة عن تحويل محتوى PDF إلى تنسيق نصي.

```csharp
// قم بالتنقل عبر جميع الصفحات في ملف PDF
foreach (Page pdfPage in pdfDocument.Pages)
{
    // معالجة كل صفحة لاستخراج النص
}
```

تمر هذه الحلقة عبر كل صفحة من صفحات ملف PDF (`pdfDocument.Pages`). لكل صفحة، سوف نقوم باستخراج النص وإضافته إلى `StringBuilder`.

## الخطوة 4: استخراج النص من كل صفحة

الآن، نُعِدّ عملية استخراج النص لكل صفحة. هنا، سننشئ `TextDevice` الكائن واستخدامه لمعالجة صفحات PDF. `TextDevice` يستخرج النص الخام أو المنسق استنادًا إلى خيارات الاستخراج التي نحددها.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // إنشاء جهاز نصي لاستخراج النص
    TextDevice textDevice = new TextDevice();
    
    // تعيين خيارات استخراج النص إلى الوضع "الخالص"
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // استخراج النص من الصفحة الحالية وحفظه في مجرى الذاكرة
    textDevice.Process(pdfPage, textStream);

    // تحويل تدفق الذاكرة إلى نص
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // إضافة النص المستخرج إلى StringBuilder
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: ال `TextDevice` يتم استخدام الفئة لاستخراج النص من ملف PDF.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`:يستخرج هذا الخيار النص الخام دون الاحتفاظ بأي تنسيق، مثل الخطوط أو المواضع. يمكنك أيضًا استخدام `TextFormattingMode.Raw` إذا كنت بحاجة إلى مزيد من التحكم في التنسيق.
- `textDevice.Process(pdfPage, textStream);`:تقوم هذه العملية بمعالجة كل صفحة من ملف PDF وتخزين النص المستخرج في `MemoryStream`.
- وأخيرًا، نقوم بتحويل النص من `MemoryStream` إلى سلسلة وإضافتها إلى `StringBuilder`.

## الخطوة 5: حفظ النص المستخرج في ملف

بعد معالجة كافة الصفحات، يتم تخزين النص في `StringBuilder`الخطوة الأخيرة هي حفظ النص المستخرج في ملف.

```csharp
// تحديد مسار الإخراج لملف النص
dataDir = dataDir + "input_Text_Extracted_out.txt";

// حفظ النص المستخرج في ملف
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`:هذا يكتب المحتوى بأكمله `StringBuilder` في ملف نصي.
- يتم تعيين مسار ملف الإخراج عن طريق إلحاق اسم الملف (`"input_Text_Extracted_out.txt"`) إلى `dataDir` طريق.

## خاتمة

استخراج النص من ملف PDF باستخدام Aspose.PDF لـ .NET عملية بسيطة وفعالة. باتباع الخطوات الموضحة في هذا الدليل، يمكنك بسهولة فتح مستندات PDF، والتنقل بين صفحاتها، واستخراج النص إلى ملف نصي. هذا مفيد بشكل خاص لمعالجة كميات كبيرة من بيانات PDF، أو إجراء تحليل نصي، أو تحويل المستندات لمزيد من المعالجة.

مع Aspose.PDF، لن تقتصر على استخراج النصوص فحسب، بل يمكنك أيضًا إضافة التعليقات التوضيحية، ومعالجة الصور، أو حتى تحويل ملفات PDF إلى صيغ أخرى مثل HTML أو Word. بفضل مرونة هذه المكتبة وقوتها، تُعدّ أداة قيّمة لإدارة ملفات PDF في تطبيقات .NET.

## الأسئلة الشائعة

### هل يمكن لـ Aspose.PDF استخراج النص من ملفات PDF المستندة إلى الصور؟
لا، صُمم Aspose.PDF لاستخراج النصوص من ملفات PDF التي تحتوي على محتوى. أما بالنسبة لملفات PDF التي تحتوي على صور، فتتطلب تقنية التعرف الضوئي على الحروف (OCR).

### هل يحتفظ Aspose.PDF بالتنسيق عند استخراج النص؟
افتراضيًا، يتم استخراج النص دون تنسيق، ولكن يمكنك تعديل خيارات الاستخراج إذا كنت تريد الاحتفاظ ببعض التنسيق.

### هل يمكنني استخراج النص من نطاق صفحة محددة؟
نعم، يمكنك تعديل الكود ليتم تكراره على نطاق محدد من الصفحات بدلاً من كل الصفحات.

### ما هي أوضاع استخراج النص في Aspose.PDF؟
يوفر Aspose.PDF وضعين: خام ونقيّ. يحاول الوضع الخام الحفاظ على التنسيق الأصلي، بينما يستخرج الوضع النقي النص فقط دون تنسيق.

### هل Aspose.PDF لـ .NET متوافق مع .NET Core؟
نعم، Aspose.PDF لـ .NET متوافق تمامًا مع .NET Core و.NET Framework.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}