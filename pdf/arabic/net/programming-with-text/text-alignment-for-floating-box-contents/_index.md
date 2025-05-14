---
"description": "تعلّم كيفية محاذاة محتويات المربعات العائمة في ملفات PDF باستخدام Aspose.PDF لـ .NET. أنشئ مستندات رائعة بتخطيطات احترافية."
"linktitle": "محاذاة النص لمحتويات المربع العائم في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "محاذاة النص لمحتويات المربع العائم في ملف PDF"
"url": "/ar/net/programming-with-text/text-alignment-for-floating-box-contents/"
"weight": 520
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# محاذاة النص لمحتويات المربع العائم في ملف PDF

## مقدمة

يُعد إنشاء ملفات PDF جذابة بصريًا مهارةً أساسيةً في عالمنا الرقمي اليوم، حيث يتنافس الجميع على جذب الانتباه. يُسهّل Aspose.PDF لـ .NET هذه المهمة ويجعلها سهلةً ومرنةً للغاية، خاصةً فيما يتعلق بتخصيص تخطيط مستنداتك. في هذا البرنامج التعليمي، سنستكشف كيفية محاذاة محتويات المربعات العائمة داخل ملفات PDF. سيضفي هذا النهج على مستنداتك لمسةً أنيقةً واحترافيةً تُبرزها عن غيرها.

## المتطلبات الأساسية

قبل الغوص في البرنامج التعليمي، هناك بعض الأساسيات التي تحتاج إلى أن تكون لديك:

1. .NET Framework: تأكد من تثبيت .NET Framework متوافق على جهازك، حيث ستقوم بتشغيل الكود الخاص بك.
2. مكتبة Aspose.PDF: يجب أن يكون لديك مكتبة Aspose.PDF. إذا لم تقم بتنزيلها بعد، يمكنك القيام بذلك. [هنا](https://releases.aspose.com/pdf/net/).
3. IDE: ستكون بيئة التطوير المتكاملة (IDE) مثل Visual Studio مفيدة للترميز واستكشاف الأخطاء وإصلاحها.
4. المعرفة الأساسية بلغة C#: إن الإلمام ببرمجة C# سيجعل من الأسهل متابعة وفهم مقتطفات التعليمات البرمجية.

## استيراد الحزم

للبدء، يجب عليك استيراد الحزم اللازمة في مشروع C# الخاص بك. إليك كيفية القيام بذلك:

1. افتح مشروعك: قم بتشغيل IDE الخاص بك، وافتح المشروع الذي تريد تنفيذ وظيفة الصندوق العائم فيه.
2. تثبيت Aspose.PDF لـ .NET: استخدم مدير الحزم NuGet لتثبيت حزمة Aspose.PDF. للقيام بذلك، اتبع الخطوات التالية:
   - انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول، ثم اختر "إدارة حزم NuGet".
   - ابحث عن "Aspose.PDF" وانقر على "تثبيت".
   
```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

بمجرد إعداد الحزم، ستكون جاهزًا للبدء في إنشاء وتنسيق المربعات العائمة في ملف PDF الخاص بك.

الآن، لنشرح عملية إضافة ومحاذاة المربعات العائمة في مستند PDF. سننشئ عدة مربعات عائمة ونحاذي محتوياتها بشكل مختلف للتوضيح.

## الخطوة 1: إعداد المستند

الخطوة الأولى هي تهيئة مستند PDF جديد وإضافة صفحة إليه. هذه الصفحة بمثابة لوحة رسم للمربعات العائمة.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Document();
doc.Pages.Add();
```

في مقتطف التعليمات البرمجية هذا، استبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي تريد حفظ ملف PDF الخاص بك فيه.

## الخطوة 2: إنشاء الصندوق العائم الأول

الآن، لنُنشئ أول صندوق عائم ونضبط محاذاته. هنا، سيتم محاذاة المحتوى إلى أسفل يمين الصندوق.

```csharp
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox(100, 100);
floatBox.VerticalAlignment = VerticalAlignment.Bottom;
floatBox.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
floatBox.Paragraphs.Add(new TextFragment("FloatingBox_bottom"));
floatBox.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, Aspose.Pdf.Color.Blue);
doc.Pages[1].Paragraphs.Add(floatBox);
```

- FloatingBox(100, 100): يقوم هذا بتهيئة صندوق عائم بعرض وارتفاع 100 وحدة لكل منهما.
- المحاذاة الرأسية والأفقية: نحدد أن النص يجب أن يكون محاذيًا لأسفل وإلى اليمين.
- TextFragment: يمثل هذا النص الذي تريد عرضه داخل المربع العائم.
- BorderInfo: يؤدي ذلك إلى تعيين حدود حول المربع العائم، مما يجعله مميزًا بصريًا.

## الخطوة 3: إضافة الصندوق العائم الثاني

الآن، دعنا ننشئ صندوقًا عائمًا ثانيًا يركز محتواه.

```csharp
Aspose.Pdf.FloatingBox floatBox1 = new Aspose.Pdf.FloatingBox(100, 100);
floatBox1.VerticalAlignment = VerticalAlignment.Center;
floatBox1.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
floatBox1.Paragraphs.Add(new TextFragment("FloatingBox_center"));
floatBox1.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, Aspose.Pdf.Color.Blue);
doc.Pages[1].Paragraphs.Add(floatBox1);
```

كما هو الحال في المربع الأول، قمنا بضبط محاذاته الرأسية إلى المركز والأفقية إلى اليمين. تتيح هذه الطريقة تعديلات ديناميكية على المحتوى وتحسين المظهر البصري.

## الخطوة 4: إنشاء الصندوق العائم الثالث

الآن، بالنسبة لصندوقنا العائم الثالث والأخير، سنقوم بمحاذاة المحتوى إلى أعلى اليمين.

```csharp
Aspose.Pdf.FloatingBox floatBox2 = new Aspose.Pdf.FloatingBox(100, 100);
floatBox2.VerticalAlignment = VerticalAlignment.Top;
floatBox2.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
floatBox2.Paragraphs.Add(new TextFragment("FloatingBox_top"));
floatBox2.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, Aspose.Pdf.Color.Blue);
doc.Pages[1].Paragraphs.Add(floatBox2);
```

يُحاذي هذا المربع المحتوى في أعلى اليمين، مُظهرًا مرونة استخدام مكتبة Aspose.PDF. لكل مربع عائم غرض مُحدد، بناءً على كيفية عرض المعلومات بصريًا.

## الخطوة 5: حفظ المستند

أخيرًا، حان وقت حفظ مستندك. ستحفظه في المكان الذي حددته سابقًا.

```csharp
doc.Save(dataDir + "FloatingBox_alignment_review_out.pdf");
```

سيتم حفظ الملف باسم `FloatingBox_alignment_review_out.pdf` في الدليل المحدد. تأكد من تحديد هذا الموقع لعرض ملف PDF الذي أنشأته.

## خاتمة

يتيح لك استخدام Aspose.PDF لـ .NET لمعالجة تخطيطات ملفات PDF إنشاء مستندات احترافية وجذابة بصريًا بكفاءة. بفهم كيفية محاذاة محتويات المربعات العائمة، يمكنك تحسين تجربة استخدام ملفات PDF بشكل ملحوظ. وكما رأينا، فهو بسيط ولكنه قوي بما يكفي لإبراز ملفات PDF الخاصة بك.

## الأسئلة الشائعة

### ما هو المربع العائم في Aspose.PDF؟  
يتيح لك المربع العائم وضع المحتوى بشكل مرن داخل تخطيط PDF.

### هل يمكنني تغيير لون حدود الصندوق العائم؟  
نعم، يمكنك تحديد ألوان مختلفة للحدود عند إنشاء مربع عائم.

### هل استخدام Aspose.PDF لـ .NET مجاني؟  
يقدم Aspose.PDF نسخة تجريبية مجانية، ولكن يلزم الحصول على ترخيص مدفوع للحصول على الوظائف الكاملة.

### هل يمكنني إضافة صور إلى الصناديق العائمة؟  
بالتأكيد! يمكنك إضافة أنواع مختلفة من المحتوى، بما في ذلك الصور، إلى الصناديق العائمة.

### أين يمكنني العثور على مزيد من المعلومات حول Aspose.PDF؟  
يمكن العثور على وثائق مفصلة [هنا](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}