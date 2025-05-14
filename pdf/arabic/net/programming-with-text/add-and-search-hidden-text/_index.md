---
"description": "تعلم كيفية إضافة النصوص المخفية والبحث عنها في مستندات PDF باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة مع أمثلة برمجية."
"linktitle": "إضافة وبحث النص المخفي في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة وبحث النص المخفي في ملف PDF"
"url": "/ar/net/programming-with-text/add-and-search-hidden-text/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة وبحث النص المخفي في ملف PDF

## مقدمة

في هذا البرنامج التعليمي، سنشرح لك خطوة بخطوة كيفية إضافة نص مخفي والبحث عنه في ملف PDF باستخدام Aspose.PDF لـ .NET. سواء كنت مطورًا محترفًا أو مبتدئًا تسعى إلى تحسين مهاراتك البرمجية، ستوفر لك هذه المقالة الأفكار اللازمة لدمج وظيفة النص المخفي في تطبيقاتك.

## المتطلبات الأساسية

قبل الخوض في جزء الترميز، هناك بعض المتطلبات الأساسية التي تحتاج إلى الاهتمام بها:

### قائمة التحقق من المتطلبات
- Visual Studio: تأكد من تثبيت Visual Studio. يفترض هذا البرنامج التعليمي أنك تستخدم .NET Framework.
- Aspose.PDF لـ .NET: يجب أن يكون لديك مكتبة Aspose.PDF لـ .NET. يمكنك تنزيلها. [هنا](https://releases.aspose.com/pdf/net/).
- المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم مقتطفات التعليمات البرمجية بشكل أفضل.

## استيراد الحزم

قبل البدء في استخدام الكود، تأكد من استيراد مساحات أسماء Aspose.PDF اللازمة. إليك كيفية القيام بذلك:

### قم بإعداد مشروعك
1. افتح Visual Studio وقم بإنشاء مشروع C# جديد أو استخدم مشروعًا موجودًا.
2. ثبّت Aspose.PDF بإضافة حزمة NuGet. يمكنك القيام بذلك بالانتقال إلى مدير حزم NuGet والبحث عن `Aspose.PDF`. 
3. وبدلاً من ذلك، يمكنك تنزيل المكتبة مباشرةً من [هنا](https://releases.aspose.com/pdf/net/) وأضفه كمرجع في مشروعك.

### استيراد مساحات الأسماء المطلوبة
في أعلى ملف C# الخاص بك، قم باستيراد مساحات الأسماء التالية:

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

تعتبر هذه الخطوة بالغة الأهمية لأن هذه المساحات تحتوي على الفئات والطرق اللازمة للتعامل مع مستندات PDF.

## إنشاء مستند PDF بنص مخفي

الآن بعد أن قمت بالإعداد، دعنا ننتقل إلى الخطوات اللازمة لإنشاء مستند PDF يحتوي على نص مرئي وغير مرئي.

### الخطوة 1: تحديد دليل المستندات
أولاً، عليك تحديد مسار حفظ ملف PDF. هنا تبدأ العملية!

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // قم بتغيير هذا إلى الدليل الخاص بك
```

يُحدد هذا السطر مكان تخزين ملف PDF المُنشأ. لا تنسَ استبدال `YOUR DOCUMENT DIRECTORY` مع مسارك الفعلي.

### الخطوة 2: إنشاء مستند PDF
الآن، لنقم بإنشاء مستند PDF جديد وإضافة صفحات إليه.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
Page page = doc.Pages.Add();
```

هنا، نقوم بتهيئة مستند جديد وإضافة صفحة سنضع فيها أجزاء النص الخاصة بنا.

### الخطوة 3: إضافة نص مرئي ومخفي
سنقوم الآن بإضافة النص المرئي وغير المرئي إلى ملف PDF الخاص بنا.

```csharp
TextFragment frag1 = new TextFragment("This is common text.");
TextFragment frag2 = new TextFragment("This is invisible text.");
```

في هذه المقتطفة، `frag1` سوف تكون مرئية، في حين `frag2` سيتم تعيينه على غير مرئي في المرة القادمة.

### الخطوة 4: اضبط النص على أنه غير مرئي
لجعل النص `frag2` غير مرئية، يمكنك ببساطة تعديلها `TextState`.

```csharp
frag2.TextState.Invisible = true;
```

من خلال تعيين هذه الخاصية، سيتم عرض أي نص مرتبط بـ `frag2` لن يتم عرضه عند عرض ملف PDF.

### الخطوة 5: إضافة أجزاء نصية إلى الصفحة
وأخيرًا، نضيف أجزاء النص هذه إلى الصفحة ونحفظ ملف PDF.

```csharp
page.Paragraphs.Add(frag1);
page.Paragraphs.Add(frag2);
doc.Save(dataDir + "39400_out.pdf");
doc.Dispose();
```

هذا الجزء من الكود يُضيف أجزاء النص إلى الصفحة. بعد ذلك، نحفظ المستند ونتخلص منه بشكل صحيح.

## البحث عن النص المخفي في ملف PDF

بعد أن أنشأنا ملف PDF بنص مرئي ومخفي، كيف نبحث عن النص المخفي؟ لنبدأ بالشرح.

### الخطوة 1: تحميل مستند PDF
للبحث عن نص داخل ملف PDF، نحتاج أولاً إلى تحميل المستند الذي أنشأناه للتو.

```csharp
doc = new Aspose.Pdf.Document(dataDir + "39400_out.pdf");
```

### الخطوة 2: إنشاء ممتص شظايا النص
سوف نستخدم `TextFragmentAbsorber` لالتقاط كافة أجزاء النص في ملف PDF.

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber();
absorber.Visit(doc.Pages[1]);
```

هنا نحدد أننا نريد استيعاب كافة أجزاء النص من الصفحة الأولى.

### الخطوة 3: التكرار عبر الأجزاء
الآن، يمكننا تكرار أجزاء النص المجمعة لمعرفة أي منها مرئي وأي منها مخفي.

```csharp
foreach (TextFragment fragment in absorber.TextFragments)
{
    Console.WriteLine("Text '{0}' on pos {1} invisibility: {2}",
        fragment.Text, fragment.Position.ToString(), fragment.TextState.Invisible);
}
```

تتحقق هذه الحلقة من كل جزء نصي وتطبع محتوياته مع موقعه وحالة رؤيته. إذا `fragment.TextState.Invisible` إذا تم ضبطه على true، فهذا يعني أن النص مخفي!

### الخطوة 4: التخلص من المستند
وأخيرًا، تذكر التخلص من المستند مرة أخرى بعد الانتهاء منه.

```csharp
doc.Dispose();
```

## خاتمة

في هذا البرنامج التعليمي، شرحنا العملية الشيقة لإضافة النصوص المخفية والبحث عنها في ملفات PDF باستخدام Aspose.PDF لـ .NET. تعلمنا كيفية إنشاء مستند PDF يحتوي على نص مرئي ومخفي، بالإضافة إلى كيفية البحث عن النص المخفي برمجيًا. تُعد هذه الميزة مفيدة للغاية في تطبيقات متنوعة، سواءً كنت ترغب في تخزين معلومات سرية أو توفير تجربة مستخدم فريدة داخل مستنداتك.

مع ازدياد معرفتك بـ ASPose.PDF، تصبح الإمكانيات لا حصر لها. استمر في التجربة وتجاوز حدود إمكانياتك مع مستندات PDF!

## الأسئلة الشائعة

### هل يمكن لـ Aspose.PDF التعامل مع ملفات PDF المشفرة؟  
نعم، يدعم Aspose.PDF تشفير وفك تشفير مستندات PDF. يمكنك بسهولة تأمين ملفات PDF الخاصة بك بكلمات مرور.

### هل هناك نسخة تجريبية متاحة لـ Aspose.PDF؟  
بالتأكيد! يمكنك تنزيل النسخة التجريبية المجانية من [هنا](https://releases.aspose.com/).

### ما هي لغات البرمجة التي يدعمها Aspose.PDF؟  
يوفر Aspose.PDF الدعم للعديد من اللغات، بما في ذلك C# وJava وPython.

### أين يمكنني العثور على الوثائق الخاصة بـ Aspose.PDF؟  
يمكنك الوصول إلى الوثائق [هنا](https://reference.aspose.com/pdf/net/).

### كيف يمكنني الحصول على الدعم إذا واجهت مشاكل؟  
للحصول على الدعم، يمكنك زيارة منتديات Aspose [هنا](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}