---
"description": "تعرف على كيفية تدوير النص باستخدام فقرة النص والمنشئ في ملف PDF باستخدام Aspose.PDF لـ .NET."
"linktitle": "تدوير النص باستخدام فقرة النص والمنشئ في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تدوير النص باستخدام فقرة النص والمنشئ في ملف PDF"
"url": "/ar/net/programming-with-text/rotate-text-using-text-paragraph-and-builder/"
"weight": 410
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تدوير النص باستخدام فقرة النص والمنشئ في ملف PDF

## مقدمة

إنشاء مستندات PDF ديناميكية طريقة رائعة لعرض بياناتك وتقاريرك وأفكارك بصريًا. ومن الأدوات الفعّالة التي تساعدك على تحقيق ذلك بطريقة منظمة Aspose.PDF لـ .NET. في هذا الدليل، سنستكشف كيفية استخدام Aspose.PDF لتدوير النص داخل ملف PDF باستخدام `TextParagraph` و `TextBuilder` سواءً كنت ترغب في إنشاء تقارير مُعلّقة أو مستندات جذابة بصريًا، فإن إتقان التعامل مع النصوص في ملفات PDF أمرٌ أساسي. هل أنت مستعد لقلب نصك رأسًا على عقب - حرفيًا؟ هيا بنا!

## المتطلبات الأساسية

قبل أن نبدأ في مغامرة تدوير النصوص، هناك بعض الأساسيات التي يجب أن تكون موجودة لديك:

- المعرفة الأساسية بلغة C#: إن الإلمام ببرمجة C# سيجعل التنقل عبر الكود أسهل.
- إعداد Visual Studio: تأكد من تثبيت Visual Studio على جهازك لتتمكن من كتابة التعليمات البرمجية وتشغيلها.
- مكتبة Aspose.PDF: يجب أن يكون لديك مكتبة Aspose.PDF مُشار إليها في مشروعك. إذا لم تكن مُثبّتة لديك بعد، يُمكنك تنزيلها من [هنا](https://releases.aspose.com/pdf/net/).
- .NET Framework: تأكد من أن بيئتك تدعم .NET؛ يمكنك استخدام .NET Framework أو .NET Core حسب احتياجاتك.

الآن بعد أن أصبح لدينا الأساس، دعنا نستورد الحزم اللازمة للبدء في العمل مع ملفات PDF.

## استيراد الحزم

للعمل مع Aspose.PDF لـ .NET، عليك استيراد مساحات الأسماء الصحيحة. في أعلى ملف C#، أضف ما يلي باستخدام التوجيهات:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
```

ستوفر لك هذه الحزم جميع الفئات التي تحتاجها للتعامل مع النصوص وجوانب المستندات الأخرى بشكل فعال.

بعد أن انتهينا من الإعداد، لنبدأ بشرح خطوات تدوير النص داخل مستند PDF. سنبدأ من تهيئة المستند إلى حفظه. هيا بنا!

## الخطوة 1: تهيئة كائن المستند

الخطوة الأولى هي إنشاء وتفعيل `Document` هذا الكائن بمثابة اللوحة التي ستضيف إليها النص.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
// تهيئة كائن المستند
Document pdfDocument = new Document();
```

ال `Document` الفصل هو أساس ملف PDF الخاص بك، ويساعد في إدارة الصفحات ومحتوياتها.

## الخطوة 2: إضافة صفحة

الآن، دعونا نضيف صفحة جديدة إلى مستندنا حيث سيتم وضع النص.

```csharp
// احصل على صفحة معينة
Page pdfPage = (Page)pdfDocument.Pages.Add();
```

هنا نضيف صفحة جديدة إلى ملف PDF. هذه الصفحة ستكون مكان فقرات نصنا.

## الخطوة 3: إنشاء فقرات النص وتكوينها

الآن تبدأ المتعة! سننشئ العديد من `TextParagraph` الكائنات وتكوين خصائصها بما في ذلك موضعها وزاوية دورانها.

```csharp
for (int i = 0; i < 4; i++)
{
    TextParagraph paragraph = new TextParagraph();
    paragraph.Position = new Position(200, 600);
    // تحديد الدوران
    paragraph.Rotation = i * 90 + 45;
}
```

في هذه الحلقة، نُنشئ أربع فقرات، مع تدوير كل فقرة بمقدار 90 درجة إضافية. وُضعت كل فقرة مبدئيًا عند الإحداثيات (200، 600).

## الخطوة 4: إنشاء أجزاء نصية

بعد إعداد الفقرات، حان وقت إضافة بعض النصوص! سننشئ `TextFragment` الكائنات التي تحتوي على النص الفعلي الذي نريد عرضه.

```csharp
TextFragment textFragment1 = new TextFragment("Paragraph Text");
textFragment1.TextState.FontSize = 12;
textFragment1.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment1.TextState.BackgroundColor = Aspose.Pdf.Color.LightGray;
textFragment1.TextState.ForegroundColor = Aspose.Pdf.Color.Blue;
```

يمكن تخصيص خصائص كل جزء، مثل حجم الخط ونوعه ولون الخلفية ولون المقدمة. نكرر هذه العملية لعدة أجزاء نصية:

```csharp
TextFragment textFragment2 = new TextFragment("Second line of text");
textFragment2.TextState = ConfigureText("Second line of text");
TextFragment textFragment3 = new TextFragment("And some more text...");
textFragment3.TextState = ConfigureText("And some more text...", true);
```

الطريقة `ConfigureText` يمكن أن تكون طريقة مساعدة تقوم بإنشائها لتغليف خصائص تنسيق النص، مما يؤدي إلى تحسين إعادة استخدام التعليمات البرمجية والوضوح.

## الخطوة 5: إضافة أجزاء نصية إلى الفقرات

بعد ذلك، سنضيف أجزاء النص إلى فقرتنا. هذا يُنشئ تسلسلًا منظمًا للنص في الفقرة.

```csharp
paragraph.AppendLine(textFragment1);
paragraph.AppendLine(textFragment2);
paragraph.AppendLine(textFragment3);
```

استخدام `AppendLine`، تأكد من إضافة كل جزء من النص عموديًا كخطوط مميزة داخل الفقرة.

## الخطوة 6: إضافة الفقرة إلى صفحة PDF

الآن بعد أن أصبحت فقرتنا مليئة بالنص، نحتاج إلى وضعها على صفحة PDF باستخدام `TextBuilder` هدف.

```csharp
TextBuilder textBuilder = new TextBuilder(pdfPage);
textBuilder.AppendParagraph(paragraph);
```

هنا يحدث السحر! أنت تأخذ الفقرة المُعدّة وتخبر `TextBuilder` لوضعها على القماش (صفحة PDF) التي قمت بإنشائها مسبقًا.

## الخطوة 7: حفظ المستند

أخيرًا، حان وقت حفظ عملنا الشاق! حدد المجلد واسم ملف PDF الناتج.

```csharp
pdfDocument.Save(dataDir + "TextFragmentTests_Rotated4_out.pdf");
```

في هذا السطر، استبدل `dataDir` مع مسار مجلد الإخراج المطلوب. سيتم حفظ ملف PDF باسم "TextFragmentTests_Rotated4_out.pdf".

## خاتمة

ها هي ذي - شرح شامل لكيفية تدوير النص في ملف PDF باستخدام Aspose.PDF لـ .NET! الأمر كله يتعلق بتقسيم المهام إلى خطوات سهلة، وسرعان ما ستُحوّل ملف PDF إلى مستند ديناميكي يُبرز أسلوبك وإبداعك. سواء كنت تُنشئ تقارير، أو تُنشئ دعوات، أو تُجرّب فقط ترتيب النصوص، يُقدّم Aspose.PDF أدوات مرنة تُلبّي احتياجاتك. فلماذا الانتظار؟ ابدأ التجربة وشاهد مدى إبداعك في مستندات PDF!

## الأسئلة الشائعة

### هل يمكنني تدوير النص في أي اتجاه؟
نعم، يمكنك تحديد أي زاوية دوران (مضاعفات 90 درجة) لتحقيق اتجاهات مختلفة.

### ماذا لو أردت إضافة صور بدلاً من النص؟
يتيح لك Aspose.PDF أيضًا معالجة الصور! يمكنك إضافة الصور باستخدام `Image` الفصول الدراسية بطريقة مماثلة.

### هل Aspose.PDF لـ .NET مجاني؟
يُقدّم نسخة تجريبية مجانية، ولكن للاستمرار في الاستخدام، يجب شراء ترخيص. تفقّد [شراء](https://purchase.aspose.com/buy) الصفحة للتفاصيل!

### هل يمكنني الحصول على الدعم لاستخدام Aspose.PDF؟
نعم، يمكنك العثور على الدعم ونشر استفساراتك على [منتدى أسبوزي](https://forum.aspose.com/c/pdf/10).

### كيف أحصل على ترخيص مؤقت لـ Aspose.PDF؟
يمكنك الحصول على ترخيص مؤقت لأغراض الاختبار من [صفحة الترخيص المؤقت](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}