---
"description": "تعرف على كيفية إزالة الارتباطات التشعبية من مستندات HTML بعد تحويلها إلى PDF باستخدام Aspose.PDF لـ .NET في هذا الدليل خطوة بخطوة."
"linktitle": "إزالة الروابط التشعبية بعد التحويل من HTML"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إزالة الروابط التشعبية بعد التحويل من HTML"
"url": "/ar/net/document-conversion/remove-hyperlinks-after-converting-from-html/"
"weight": 250
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إزالة الروابط التشعبية بعد التحويل من HTML

## مقدمة

في العصر الرقمي، يُعد تحويل مستندات HTML إلى PDF أمرًا شائعًا. ومع ذلك، قد ترغب أحيانًا في إزالة الروابط التشعبية من ملف PDF المُحوّل لأسباب مختلفة، مثل تحسين قابلية القراءة أو منع التنقل غير المرغوب فيه. في هذا البرنامج التعليمي، سنستكشف كيفية تحقيق ذلك باستخدام Aspose.PDF لـ .NET. 

## المتطلبات الأساسية

قبل الغوص في الكود، تأكد من أن لديك المتطلبات الأساسية التالية:

1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. ستكون هذه بيئة التطوير الخاصة بك.
2. Aspose.PDF لـ .NET: يجب أن يكون لديك مكتبة Aspose.PDF. يمكنك تنزيلها من [هنا](https://releases.aspose.com/pdf/net/).
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم الكود بشكل أفضل.

## استيراد الحزم

للبدء، عليك استيراد الحزم اللازمة في مشروع C# الخاص بك. إليك كيفية القيام بذلك:

1. افتح مشروع Visual Studio الخاص بك.
2. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول وحدد "إدارة حزم NuGet".
3. بحث عن `Aspose.PDF` وتثبيته.

```csharp
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.IO;
```

الآن بعد أن قمت بإعداد كل شيء، دعنا نستعرض عملية إزالة الارتباطات التشعبية من ملف HTML بعد تحويله إلى PDF.

## الخطوة 1: إعداد دليل المستندات

أولاً، عليك تحديد مسار مجلد المستندات. هذا هو مكان ملف HTML، وهو المكان الذي سيتم حفظ ملف PDF الناتج فيه.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

يستبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي يتم تخزين ملف HTML الخاص بك فيه.

## الخطوة 2: تحميل مستند HTML

بعد ذلك، ستقوم بتحميل مستند HTML باستخدام `Document` فئة من Aspose.PDF. تتيح لك هذه الفئة العمل مع مستندات PDF بسهولة.

```csharp
Document doc = new Document(dataDir + "SampleHtmlFile.html", new HtmlLoadOptions());
```

هنا نقوم بتحميل ملف HTML المسمى `SampleHtmlFile.html`تأكد من وجود هذا الملف في الدليل المحدد.

## الخطوة 3: حفظ المستند في تدفق الذاكرة

قبل البدء بمعالجة التعليقات التوضيحية، علينا حفظ المستند في ذاكرة التخزين المؤقت. هذه الخطوة بالغة الأهمية لأنها تُهيئه لمزيد من المعالجة.

```csharp
doc.Save(new MemoryStream());
```

يحفظ هذا السطر المستند في الذاكرة، مما يسمح لنا بالعمل معه دون الحاجة إلى كتابته على القرص حتى الآن.

## الخطوة 4: التكرار من خلال التعليقات التوضيحية

سنتناول الآن التعليقات التوضيحية في المستند. التعليقات التوضيحية هي عناصر مثل الروابط والتعليقات والإشارات. نحن مهتمون تحديدًا بتعليقات الروابط التوضيحية.

```csharp
foreach (Annotation a in doc.Pages[1].Annotations)
{
    if (a.AnnotationType == AnnotationType.Link)
    {
        // معالجة تعليق الرابط
    }
}
```

في هذه الحلقة، نتحقق مما إذا كان نوع التعليق رابطًا. إذا كان كذلك، ننتقل إلى الخطوات التالية.

## الخطوة 5: إزالة إجراء الارتباط التشعبي

لكل تعليق على رابط، علينا التحقق من وجود إجراء ارتباط تشعبي. إذا كان الأمر كذلك، فسنحذف الرابط التشعبي عن طريق تعيين مُعرّف URI الخاص به إلى سلسلة فارغة.

```csharp
LinkAnnotation la = (LinkAnnotation)a;
if (la.Action is GoToURIAction)
{
    GoToURIAction gta = (GoToURIAction)la.Action;
    gta.URI = "";
```

يضمن مقتطف التعليمات البرمجية هذا إزالة إجراء الارتباط التشعبي بشكل فعال.

## الخطوة 6: استيعاب أجزاء النص

بعد ذلك، سنستوعب أجزاء النص المرتبطة بتعليق الرابط. هذا يسمح لنا بتعديل مظهر النص.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
tfa.TextSearchOptions = new TextSearchOptions(a.Rect);
doc.Pages[a.PageIndex].Accept(tfa);
```

هنا، نقوم بإنشاء `TextFragmentAbsorber` وضبط خيارات البحث على مستطيل التعليق التوضيحي. هذا يساعدنا في العثور على النص المرتبط.

## الخطوة 7: تعديل مظهر النص

بعد الحصول على أجزاء النص، يُمكننا تعديل مظهرها. في هذه الحالة، سنزيل التسطير ونُغيّر لون النص إلى الأسود.

```csharp
foreach (TextFragment tf in tfa.TextFragments)
{
    tf.TextState.Underline = false;
    tf.TextState.ForegroundColor = Color.Black;
}
```

تعمل هذه الخطوة على تحسين قابلية قراءة النص عن طريق إزالة نمط الارتباط التشعبي.

## الخطوة 8: حذف التعليق التوضيحي

بعد تعديل النص، يمكننا حذف تعليق الرابط من المستند بأمان.

```csharp
doc.Pages[a.PageIndex].Annotations.Delete(a);
}
```

يؤدي هذا السطر إلى إزالة الارتباط التشعبي من ملف PDF، مما يضمن عدم وجوده في الناتج النهائي.

## الخطوة 9: حفظ المستند المعدّل

أخيرًا، علينا حفظ المستند المُعدَّل في ملف PDF جديد. هذه هي الخطوة الأخيرة في عمليّتنا.

```csharp
doc.Save(dataDir + "RemoveHyperlinksFromText_out.pdf");
```

يحفظ هذا السطر المستند مع إزالة الارتباطات التشعبية، مما يؤدي إلى إنشاء ملف PDF جديد باسم `RemoveHyperlinksFromText_out.pdf`.

## خاتمة

وها أنت ذا! لقد نجحت في إزالة الروابط التشعبية من مستند HTML بعد تحويله إلى PDF باستخدام Aspose.PDF لـ .NET. هذه العملية لا تُحسّن فقط من قابلية قراءة ملف PDF، بل تمنحك أيضًا التحكم في المحتوى الذي تعرضه. 

## الأسئلة الشائعة

### هل يمكنني إزالة الروابط التشعبية من أي مستند PDF؟
نعم، يمكنك إزالة الارتباطات التشعبية من أي مستند PDF باستخدام Aspose.PDF لـ .NET.

### هل استخدام Aspose.PDF مجاني؟
يقدم Aspose.PDF نسخة تجريبية مجانية، ولكن للاستفادة من الميزات الكاملة، يلزمك شراء ترخيص. تحقق من [صفحة الشراء](https://purchase.aspose.com/buy).

### ماذا لو واجهت مشاكل أثناء استخدام Aspose.PDF؟
يمكنك طلب المساعدة على [منتدى الدعم](https://forum.aspose.com/c/pdf/10).

### هل يمكنني تحويل تنسيقات الملفات الأخرى إلى PDF باستخدام Aspose؟
نعم، يدعم Aspose تنسيقات ملفات مختلفة للتحويل إلى PDF.

### أين يمكنني تنزيل Aspose.PDF لـ .NET؟
يمكنك تنزيله من [رابط التحميل](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}