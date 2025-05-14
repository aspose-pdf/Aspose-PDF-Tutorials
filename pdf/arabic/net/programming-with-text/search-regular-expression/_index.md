---
"description": "تعرّف على كيفية البحث عن التعبيرات العادية في ملفات PDF باستخدام Aspose.PDF لـ .NET في هذا البرنامج التعليمي خطوة بخطوة. عزّز إنتاجيتك باستخدام التعبيرات العادية."
"linktitle": "البحث عن تعبير عادي في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "البحث عن تعبير عادي في ملف PDF"
"url": "/ar/net/programming-with-text/search-regular-expression/"
"weight": 440
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# البحث عن تعبير عادي في ملف PDF

## مقدمة

عند التعامل مع مستندات PDF كبيرة الحجم، قد تجد نفسك تبحث عن أنماط أو تنسيقات محددة، مثل التواريخ أو أرقام الهواتف أو غيرها من البيانات المنظمة. قد يكون البحث اليدوي في ملف PDF أمرًا شاقًا، أليس كذلك؟ وهنا يأتي دور استخدام التعبيرات النمطية (regex). في هذا البرنامج التعليمي، سنستكشف كيفية البحث عن نمط تعبير نمطي داخل ملف PDF باستخدام Aspose.PDF لـ .NET. سيشرح لك هذا الدليل كل خطوة لتتمكن من تطبيقه بسهولة في تطبيق .NET الخاص بك.

## المتطلبات الأساسية

قبل أن نتعمق في البرنامج التعليمي خطوة بخطوة، دعنا نستعرض ما تحتاج إلى وضعه في مكانه:

- Aspose.PDF لـ .NET: يجب تثبيت هذه المكتبة. إذا لم تقم بتثبيتها بعد، يمكنك [قم بتحميله هنا](https://releases.aspose.com/pdf/net/).
- IDE: Visual Studio أو أي IDE آخر متوافق مع C#.
- .NET Framework: تأكد من إعداد مشروعك باستخدام الإصدار المناسب من .NET Framework.
- المعرفة الأساسية بلغة C#: على الرغم من أن هذا الدليل مفصل، إلا أن الفهم الأساسي للغة C# سيكون مفيدًا.

### استيراد الحزم

للبدء، ستحتاج إلى استيراد مساحات الأسماء اللازمة من Aspose.PDF لـ .NET إلى مشروعك. هذه الحزم ضرورية للعمل مع ملفات PDF وإجراء عمليات البحث باستخدام التعابير العادية.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

دعونا نقسم عملية البحث عن التعبيرات العادية في ملف PDF باستخدام Aspose.PDF إلى خطوات متعددة.

## الخطوة 1: إعداد دليل المستندات

تبدأ كل عملية PDF بتحديد مكان مستندك. ستحتاج إلى تحديد مسار ملف PDF المُخزّن في `dataDir` عامل.

### الخطوة 1.1: تحديد مسار المستند الخاص بك

```csharp
// حدد المسار إلى مستند PDF الخاص بك
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

يستبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي لملف PDF. هذه الخطوة بالغة الأهمية لأنها تُوجِّه الكود إلى الملف الذي تريد العمل عليه.

### الخطوة 1.2: افتح مستند PDF

بعد ذلك، ستحتاج إلى فتح مستند PDF باستخدام `Document` الفئة من Aspose.PDF.

```csharp
// افتح المستند
Document pdfDocument = new Document(dataDir + "SearchRegularExpressionAll.pdf");
```

هنا، `"SearchRegularExpressionAll.pdf"` هو ملف PDF النموذجي الذي سنقوم من خلاله بإجراء بحث regex.

## الخطوة 2: إعداد TextFragmentAbsorber

هذا هو المكان الذي يحدث فيه السحر! `TextFragmentAbsorber` تساعد الفئة في التقاط أجزاء من النص تتطابق مع نمط معين أو تعبير منتظم.

لنُعِدّ أداة الامتصاص للعثور على أنماط باستخدام تعبير عادي. في هذه الحالة، نبحث عن نمط سنوات مثل "١٩٩٩-٢٠٠٠".

```csharp
// إنشاء كائن TextAbsorber للعثور على جميع العبارات المطابقة للتعبير العادي
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("\\d{4}-\\d{4}"); // مثل 1999-2000
```

التعبير العادي `\\d{4}-\\d{4}` يبحث عن نمط مكون من أربعة أرقام متبوعة بواصلة وأربعة أرقام أخرى، وهو أمر نموذجي لنطاقات السنوات.

## الخطوة 3: تمكين البحث باستخدام التعبيرات العادية

للتأكد من أن عملية البحث تفسر النمط كتعبير عادي، تحتاج إلى تكوين خيارات البحث باستخدام `TextSearchOptions` فصل.

```csharp
// تعيين خيار البحث النصي لتحديد استخدام التعبيرات العادية
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textFragmentAbsorber.TextSearchOptions = textSearchOptions;
```

ضبط `TextSearchOptions` ل `true` يضمن أن الممتص يستخدم البحث المبني على التعابير العادية بدلاً من النص العادي.

## الخطوة 4: قبول امتصاص النص

في هذه المرحلة، يمكنك تطبيق مُمتص النص على مستند PDF ليتمكن من إجراء عملية البحث. يتم ذلك عن طريق استدعاء `Accept` الطريقة على `Pages` هدف مستند PDF.

```csharp
// قبول الامتصاص لجميع الصفحات
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

تعمل هذه الأوامر على معالجة كافة صفحات ملف PDF، والبحث عن أي نص يتطابق مع التعبير العادي.

## الخطوة 5: استخراج النتائج وعرضها

بعد اكتمال البحث، ستحتاج إلى استخراج النتائج. `TextFragmentAbsorber` يخزن هذه النتائج في `TextFragmentCollection`يمكنك التنقل عبر هذه المجموعة للوصول إلى كل جزء نصي مطابق وعرضه.

### الخطوة 5.1: استرداد أجزاء النص المستخرجة

```csharp
// احصل على أجزاء النص المستخرجة
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

الآن بعد أن قمت بجمع الأجزاء، حان الوقت لتصفحها وعرض التفاصيل ذات الصلة مثل النص والموضع وتفاصيل الخط والمزيد.

### الخطوة 5.2: تكرار الأجزاء

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

لكل `TextFragment`تُطبع تفاصيل مثل حجم الخط واسمه وموضعه. هذا لا يساعد فقط في العثور على النص، بل يُظهر لك أيضًا تنسيقه وموقعه الدقيق.

## خاتمة

هذا كل ما في الأمر! يُعد البحث عن الأنماط في ملفات PDF باستخدام التعبيرات النمطية أداةً فعّالة للغاية، خاصةً للنصوص المنظمة كالتواريخ وأرقام الهواتف والأنماط المشابهة. يوفر Aspose.PDF لـ .NET طريقةً سلسةً لإجراء هذه العمليات بسهولة. الآن، يمكنك الاستفادة من قوة التعبيرات النمطية لأتمتة البحث عن نصوص PDF، مما يزيد من كفاءة سير عملك.

## الأسئلة الشائعة

### هل يمكنني البحث عن أنماط متعددة في ملف PDF واحد؟
نعم، يمكنك تشغيل عدة `TextFragmentAbsorber` الكائنات، كل منها بأنماط تعبيرات عادية مختلفة، عبر نفس ملف PDF.

### هل يدعم Aspose.PDF البحث عن الأنماط غير الحساسة لحالة الأحرف؟
بالتأكيد! يمكنك تكوين `TextSearchOptions` لجعل البحث غير حساس لحالة الأحرف.

### هل هناك حد لحجم ملف PDF الذي يمكنني البحث فيه؟
لا يوجد حد صارم، ولكن الأداء قد يختلف اعتمادًا على حجم ملف PDF وتعقيد نمط التعبيرات العادية.

### هل يمكنني تسليط الضوء على النص الموجود في ملف PDF؟
نعم، يسمح لك Aspose.PDF بتسليط الضوء على النص أو حتى استبداله بمجرد العثور عليه باستخدام الممتص.

### كيف أتعامل مع الأخطاء إذا لم يتم العثور على النمط؟
إذا لم يتم العثور على أي تطابقات، `TextFragmentCollection` سيكون فارغًا. يمكنك التعامل مع هذا السيناريو بفحص بسيط قبل تكرار النتائج.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}