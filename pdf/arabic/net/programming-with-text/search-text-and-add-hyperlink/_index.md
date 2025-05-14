---
"description": "تعرف على كيفية البحث عن النص وإضافة ارتباطات تشعبية في ملفات PDF باستخدام Aspose.PDF لـ .NET من خلال البرنامج التعليمي الخاص بنا خطوة بخطوة."
"linktitle": "البحث عن النص وإضافة ارتباط تشعبي"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "البحث عن النص وإضافة ارتباط تشعبي"
"url": "/ar/net/programming-with-text/search-text-and-add-hyperlink/"
"weight": 450
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# البحث عن النص وإضافة ارتباط تشعبي

## مقدمة

هل تبحث عن طريقة ليس فقط لمعالجة ملفات PDF، بل لتحسينها أيضًا بإضافة روابط تشعبية؟ أنت في المكان المناسب! مع مكتبة Aspose.PDF القوية لـ .NET، يمكنك البحث عن أنماط النصوص في مستندات PDF وإضافة روابط تشعبية بسلاسة. تخيل أن يكون لديك مستند لا ينقل المعلومات فحسب، بل يربط القراء أيضًا بالمصادر ذات الصلة بمجرد النقر على رابط. يبدو رائعًا، أليس كذلك؟ في هذا البرنامج التعليمي، سنرشدك خطوة بخطوة حول كيفية البحث عن نص باستخدام التعبيرات العادية وإضافة روابط تشعبية داخل ملفات PDF. سواء كنت مطورًا محترفًا أو مبتدئًا، ستجد هذه العملية بسيطة ومفيدة.

## المتطلبات الأساسية

قبل أن نتعمق في التفاصيل، لنتأكد من تجهيز كل ما تحتاجه للمتابعة. إليك قائمة مرجعية مفيدة:

- .NET Framework: يجب أن يكون لديك .NET Framework مثبتًا على جهازك (الإصدار 4.0 أو أعلى).
- مكتبة Aspose.PDF لـ .NET: لا تنسَ تنزيل مكتبة Aspose.PDF وإضافة مرجع إليها في مشروعك. يمكنك العثور عليها هنا. [هنا](https://releases.aspose.com/pdf/net/).
- IDE: ستحتاج إلى بيئة تطوير متكاملة (IDE) مثل Visual Studio لكتابة التعليمات البرمجية وتشغيلها.
- ملف PDF نموذجي: احصل على ملف PDF نموذجي لاختبار الكود. يمكنك إنشاء ملف PDF بسيط أو استخدام أحد مستنداتك الحالية.

بمجرد الانتهاء من كل شيء في هذه القائمة، سنكون جاهزين للانطلاق!

## استيراد الحزم

الخطوة الأولى في رحلتنا هي استيراد الحزم اللازمة. هنا نُحدد للمشروع الأدوات التي سنستخدمها. إليك كيفية القيام بذلك:

في ملف C# الخاص بك، ابدأ بتضمين المساحات التالية في الأعلى:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

من خلال استيراد هذه المساحات الاسمية، فإنك تمنح برنامجك إمكانية الوصول إلى جميع الميزات الرائعة التي يقدمها Aspose.PDF.

الآن وقد انتهينا من كل شيء، حان وقت العمل. سنتناول هذا الأمر في سلسلة من الخطوات، لذا تابعونا بعناية!

### الخطوة 1: تعيين دليل المستندات الخاص بك

أولاً، ستحتاج إلى تحديد مكان تخزين ملفات PDF. عدّل `dataDir` متغير للإشارة إلى دليل مستندك. إليك الطريقة:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

تأكد من الاستبدال `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي إلى مستنداتك.

### الخطوة 2: إنشاء TextFragmentAbsorber

بعد ذلك، نحتاج إلى أداة للعثور على النص الذي نريد ربطه. أدخل `TextFragmentAbsorber`سيساعدنا هذا الرجل الصغير في البحث عن نمط النص المحدد في ملف PDF الخاص بنا.

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber("\\d{4}-\\d{4}");
```

هنا، نبحث عن نمط محدد: أربعة أرقام، وشرطة، متبوعة بأربعة أرقام أخرى (مثل رقم الهاتف أو السنة).

### الخطوة 3: تمكين البحث باستخدام التعبيرات العادية

نحن نستخدم بالفعل تعبيرًا عاديًا للعثور على نمط النص الخاص بنا، ولكننا نحتاج إلى التأكد من أن `absorber` يعلم أنه مُفعّل. هذا ضروري ليتمكن من البحث بشكل صحيح.

```csharp
absorber.TextSearchOptions = new TextSearchOptions(true);
```

### الخطوة 4: تهيئة محرر محتوى Pdf

الآن بعد أن أصبح لدينا جهاز الامتصاص جاهزًا، نحتاج إلى `PdfContentEditor` للعمل مع ملف PDF الخاص بنا. تتيح لنا هذه الفئة الارتباط بملف PDF والتعامل معه.

```csharp
PdfContentEditor editor = new PdfContentEditor();
```

### الخطوة 5: ربط ملف PDF المصدر الخاص بك

بعد أن أصبح محرر المحتوى جاهزًا، حان الوقت لربطه بملف PDF الفعلي الذي نريد العمل عليه.

```csharp
editor.BindPdf(dataDir + "SearchRegularExpressionPage.pdf");
```

تأكد من الاستبدال `"SearchRegularExpressionPage.pdf"` مع اسم ملف PDF الخاص بك.

### الخطوة 6: قبول الممتص للصفحة

علينا إبلاغ المحرر برغبتنا في البحث في صفحة محددة من المستند. في هذه الحالة، لننتقل إلى الصفحة ١.

```csharp
editor.Document.Pages[1].Accept(absorber);
```

### الخطوة 7: الاستعداد للتكرار عبر أجزاء النص

الآن، أصبحنا جاهزين لتكرار جميع أجزاء النص التي وجدها مُمتصّنا. سنُعدّل مظهرها ونُنشئ رابطنا التشعبي.

```csharp
int[] dashArray = { };
String[] LEArray = { };
Color blue = Color.Blue;
```

هنا، نقوم بتعيين بعض المعلمات، مثل لون الرابط التشعبي الخاص بنا.

### الخطوة 8: تكرار كل جزء من النص

لكل جزء نصي يطابق بحثنا، سنغير لونه وننشئ رابطًا تشعبيًا. هكذا يبدو:

```csharp
foreach (TextFragment textFragment in absorber.TextFragments)
{
    textFragment.TextState.ForegroundColor = Aspose.Pdf.Color.Blue;
    Rectangle rect = new Rectangle((int)textFragment.Rectangle.LLX,
        (int)Math.Round(textFragment.Rectangle.LLY), (int)Math.Round(textFragment.Rectangle.Width + 2),
        (int)Math.Round(textFragment.Rectangle.Height + 1));
    Enum[] actionName = new Enum[2] { Aspose.Pdf.Annotations.PredefinedAction.Document_AttachFile, Aspose.Pdf.Annotations.PredefinedAction.Document_ExtractPages };
    
    editor.CreateWebLink(rect, "http://www.aspose.com"، 1، أزرق، اسم الإجراء)؛
    editor.CreateLine(rect, "", (float)textFragment.Rectangle.LLX + 1, (float)textFragment.Rectangle.LLY - 1,
        (float)textFragment.Rectangle.URX, (float)textFragment.Rectangle.LLY - 1, 1, 1, blue, "S", dashArray, LEArray);
}
```

### الخطوة 9: احفظ ملف PDF المحرر

لقد اقتربنا من الانتهاء! الآن حان وقت حفظ التغييرات في ملف PDF جديد.

```csharp
dataDir = dataDir + "SearchTextAndAddHyperlink_out.pdf";
editor.Save(dataDir);
```

### الخطوة 10: إغلاق المحرر

وأخيرًا، لا تنسَ إغلاق مستندك لتحرير الموارد!

```csharp
editor.Close();
Console.WriteLine("\nText replaced and hyperlink added successfully based on a regular expression.\nFile saved at " + dataDir);
```

لقد أنشأتَ الآن ملف PDF برابط تشعبي تم إنشاؤه ديناميكيًا بناءً على نتائج البحث. ما أروع هذا!

## خاتمة

وهذا كل ما في الأمر! باتباع هذه الخطوات، ستتعلم كيفية البحث في ملف PDF وإضافة روابط تشعبية باستخدام مكتبة Aspose.PDF لـ .NET. هذا يفتح آفاقًا واسعة من الإمكانيات، خاصةً إذا كنت تعمل على مستندات تتطلب التفاعل. تخيل إضافة روابط إلى مصادر ذات صلة، أو مواقع إلكترونية مرجعية، أو حتى صفحات داخلية - كل ذلك ببضعة أسطر برمجية فقط!
## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟  
Aspose.PDF for .NET هي مكتبة تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وإدارتها في تطبيقات .NET.

### كيف يمكنني تنزيل Aspose.PDF لـ .NET؟  
يمكنك تحميل المكتبة [هنا](https://releases.aspose.com/pdf/net/).

### هل يمكنني تجربة Aspose.PDF مجانًا؟  
بالتأكيد! يمكنك الحصول على نسخة تجريبية مجانية [هنا](https://releases.aspose.com/).

### هل يتوفر الدعم لمنتجات Aspose؟  
نعم، يمكنك العثور على الدعم ومناقشات المجتمع [هنا](https://forum.aspose.com/c/pdf/10).

### كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.PDF؟  
يمكنك طلب ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}