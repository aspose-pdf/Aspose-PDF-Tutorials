---
"description": "تعلّم كيفية شطب الكلمات في ملف PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل الشامل خطوة بخطوة. طوّر مهاراتك في تحرير المستندات."
"linktitle": "شطب الكلمات"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "شطب الكلمات"
"url": "/ar/net/annotations/strikeoutwords/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# شطب الكلمات

## مقدمة

هل سبق لك أن وجدت نفسك بحاجة إلى إبراز نص معين في ملف PDF بشطبه؟ سواء كنت تراجع مستندات، أو تُعلّم نصًا، أو تحتاج ببساطة إلى تمييز أجزاء معينة، فإن شطب الكلمات أداة قيّمة. في هذا البرنامج التعليمي، سنستكشف كيفية القيام بذلك باستخدام Aspose.PDF لـ .NET. سيرشدك هذا الدليل الشامل خلال كل خطوة، مما يضمن حصولك على جميع المعلومات اللازمة لتطبيق هذه الميزة بفعالية في تطبيقات .NET الخاصة بك. 

## المتطلبات الأساسية

قبل أن ننتقل إلى الكود، هناك بعض المتطلبات الأساسية التي ستحتاج إلى تلبيتها لمتابعة هذا البرنامج التعليمي:

1. مكتبة Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF لـ .NET. يمكنك [قم بتحميله هنا](https://releases.aspose.com/pdf/net/).

2. .NET Framework: تأكد من تثبيت .NET Framework على جهازك. هذا البرنامج التعليمي مصمم لتطبيقات .NET.

3. بيئة التطوير: ستحتاج إلى بيئة تطوير متكاملة مثل Visual Studio لكتابة وتشغيل التعليمات البرمجية الخاصة بك.

4. مستند PDF: جهّز نموذجًا من ملف PDF ترغب بالعمل عليه. هذا هو المستند الذي سنشطب عليه النص.

5. المعرفة الأساسية بلغة C#: المعرفة ببرمجة C# ضرورية لفهم الخطوات المذكورة في هذا البرنامج التعليمي وتنفيذها.

## استيراد الحزم

قبل البدء بالبرمجة، علينا استيراد مساحات الأسماء اللازمة في مشروع .NET. سيُتيح لنا هذا الوصول إلى الفئات والأساليب اللازمة لمعالجة ملفات PDF باستخدام Aspose.PDF.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

تُعد هذه المساحات الأساسية ضرورية للعمل مع مستندات PDF ومعالجة النصوص وإضافة التعليقات التوضيحية مثل الشطب.

في هذا القسم، سنُقسّم عملية شطب الكلمات في مستند PDF إلى خطوات بسيطة وسهلة. ستُرفق كل خطوة بشرح مُفصّل لضمان فهمك لكيفية عملها.

## الخطوة 1: تحميل مستند PDF

الخطوة الأولى هي تحميل ملف PDF الذي ترغب في تعديله. هذا هو الملف الذي ستشطب منه كلمات أو عبارات محددة.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// افتح مستند PDF
Document document = new Document(dataDir + "input.pdf");
```

- `dataDir`:يحتوي هذا المتغير على مسار دليل المستند. استبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي يوجد به ملف PDF الخاص بك.
- `Document`: ال `Document` تُمثل الفئة مستند PDF. بتمرير مسار الملف إلى مُنشئه، نفتح ملف PDF للمعالجة.

## الخطوة 2: إنشاء ممتص TextFragment للعثور على نص محدد

بعد ذلك، سنقوم بإنشاء مثيل لـ `TextFragmentAbsorber` للبحث عن جزء نصي محدد في مستند PDF. هذا يسمح لنا بتحديد النص الذي نريد شطبه.

```csharp
// إنشاء مثيل لـ TextFragment Absorber للبحث عن جزء نص معين
Aspose.Pdf.Text.TextFragmentAbsorber textFragmentAbsorber = new Aspose.Pdf.Text.TextFragmentAbsorber("Estoque");
```

- `TextFragmentAbsorber`تُستخدم هذه الفئة للعثور على أجزاء نصية محددة والعمل عليها ضمن مستند PDF. في هذا المثال، نبحث عن كلمة "Estoque". استبدل "Estoque" بالكلمة أو العبارة التي تريد البحث عنها في مستندك.

## الخطوة 3: التكرار عبر صفحات مستند PDF

الآن بعد أن أصبح لدينا `TextFragmentAbsorber`، نحتاج إلى تكرار كل صفحة من مستند PDF للعثور على النص المحدد.

```csharp
// قم بالتكرار خلال صفحات مستند PDF
for (int i = 1; i <= document.Pages.Count; i++)
{
    // احصل على الصفحة الحالية من مستند PDF
    Page page = document.Pages[i];
    page.Accept(textFragmentAbsorber);
}
```

- `for (int i = 1; i <= document.Pages.Count; i++)`:تتكرر هذه الحلقة عبر كل صفحة من مستند PDF.
- `document.Pages[i]`:استرجاع الصفحة الحالية التي يتم معالجتها.
- `page.Accept(textFragmentAbsorber)`:تطبق هذه الطريقة `TextFragmentAbsorber` إلى الصفحة الحالية، والبحث عن النص المحدد.

## الخطوة 4: جمع ومعالجة أجزاء النص

بعد تكرار الصفحات، سنقوم بجمع أجزاء النص التي وجدناها وإعدادها للمعالجة الإضافية.

```csharp
// إنشاء مجموعة من أجزاء النص الممتصة
Aspose.Pdf.Text.TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`تخزّن هذه المجموعة جميع أجزاء النص الموجودة في المستند. سنستخدمها في الخطوة التالية لشطب النص.

## الخطوة 5: قم بتكرار أجزاء النص وشطبها

في هذه الخطوة، سننتقل عبر كل جزء من النص في مجموعتنا ونطبق عليه تعليقًا توضيحيًا مشطوبًا.

```csharp
// التكرار على مجموعة من أجزاء النص
for (int j = 1; j <= textFragmentCollection.Count; j++)
{
	Aspose.Pdf.Text.TextFragment textFragment = textFragmentCollection[j];

    // الحصول على الأبعاد المستطيلة لكائن TextFragment
    Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(
        (float)textFragment.Position.XIndent,
        (float)textFragment.Position.YIndent,
        (float)textFragment.Position.XIndent + (float)textFragment.Rectangle.Width,
        (float)textFragment.Position.YIndent + (float)textFragment.Rectangle.Height);

    // إنشاء مثيل لتعليق StrikeOut
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.Page, rect);

    // تعيين خصائص تعليق الشطب
    strikeOut.Opacity = .80f;
    strikeOut.Border = new Border(strikeOut);
    strikeOut.Color = Aspose.Pdf.Color.Red;

    // أضف التعليق التوضيحي إلى مجموعة التعليقات التوضيحية لصفحة جزء النص
    textFragment.Page.Annotations.Add(strikeOut);
}
```

- `TextFragment textFragment = textFragmentCollection[j]`:يستعيد هذا السطر جزء النص الحالي.
- `Aspose.Pdf.Rectangle`:نحسب الأبعاد المستطيلة لجزء النص لتحديد مكان تطبيق الشطب.
- `StrikeOutAnnotation`:تمثل هذه الفئة شرح الشطب. نُنشئ مثيلًا لها باستخدام المستطيل المحسوب والصفحة الحالية.
- `strikeOut.Opacity`:تحدد هذه الخاصية تعتيم النص المشطوب، مما يجعله مرئيًا بنسبة 80%.
- `strikeOut.Color`:حددنا لون الشطب باللون الأحمر. يمكنك تغييره إلى أي لون تفضله.
- `textFragment.Page.Annotations.Add(strikeOut)`:يؤدي هذا إلى إضافة تعليق الشطب إلى الصفحة.

## الخطوة 6: حفظ مستند PDF المعدّل

الخطوة الأخيرة هي حفظ مستند PDF المعدل مع تطبيق الشطب.

```csharp
// احفظ مستند PDF المحدث
dataDir = dataDir + "StrikeOutWords_out.pdf";
document.Save(dataDir);
```

- `dataDir + "StrikeOutWords_out.pdf"`: يؤدي هذا إلى إنشاء اسم ملف جديد للمستند المُعدَّل. يبقى الملف الأصلي دون تغيير.
- `document.Save(dataDir)`:يحفظ مستند PDF مع الشطب في الموقع المحدد.

## خاتمة

تهانينا! لقد نجحت في شطب كلمات محددة في مستند PDF باستخدام Aspose.PDF لـ .NET. باتباع هذا الدليل التفصيلي، يمكنك الآن تخصيص مستندات PDF عن طريق تمييز النصوص أو شطبها، مما يجعلها أكثر ديناميكية ومناسبة لاحتياجاتك. سواء كنت تُعلق على مستندات قانونية، أو تُعدّ تقارير، أو تُحدّد نصًا للمراجعة، فإن هذا البرنامج التعليمي يُزوّدك بالمهارات اللازمة للقيام بذلك بكفاءة.

## الأسئلة الشائعة

### هل يمكنني تغيير لون الشطب؟

نعم يمكنك تغيير اللون عن طريق تعديل `strikeOut.Color` الملكية. على سبيل المثال، يمكنك ضبطها على `Aspose.Pdf.Color.Blue` لضربة زرقاء.

### هل من الممكن شطب كلمات متعددة في وقت واحد؟

بالتأكيد! `TextFragmentAbsorber` يمكن استخدامه للبحث عن أي كلمة أو عبارة في المستند. يمكنك تطبيق الشطب على عدة حالات بالتكرار خلال `TextFragmentCollection`.

### ماذا لو أردت شطب النص في صفحات محددة فقط؟

يمكنك تعديل الحلقة التي تتكرر عبر الصفحات لتشمل فقط الصفحات التي تريد تعديلها. على سبيل المثال، `for (int i = 1; i <= 3; i++)` سيتم تطبيق الشطب على الصفحات الثلاث الأولى فقط.

### كيف يمكنني تعديل سمك خط الشطب؟

يمكنك تعديل سمك خط الشطب عن طريق تعديل `Border` ممتلكات `StrikeOutAnnotation`يسمح هذا بتخصيص مظهر الشطب.

### هل هناك طريقة للتراجع عن الشطب بعد حفظ المستند؟

بمجرد حفظ المستند، يصبح الشطب نهائيًا. إذا كنت ترغب في الاحتفاظ بالنص الأصلي دون الشطب، ففكّر في حفظ نسخة احتياطية من المستند الأصلي قبل إجراء أي تعديلات.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}