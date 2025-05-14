---
"description": "تعرّف على كيفية توقيع ملفات PDF بأمان باستخدام بطاقة ذكية باستخدام Aspose.PDF لـ .NET. اتبع دليلنا خطوة بخطوة لسهولة التنفيذ."
"linktitle": "التوقيع باستخدام البطاقة الذكية باستخدام حقل التوقيع"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "التوقيع باستخدام البطاقة الذكية باستخدام حقل التوقيع"
"url": "/ar/net/programming-with-security-and-signatures/sign-with-smart-card-using-signature-field/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# التوقيع باستخدام البطاقة الذكية باستخدام حقل التوقيع

## مقدمة

في عالمنا الرقمي اليوم، أصبح تأمين المستندات أكثر أهمية من أي وقت مضى. سواء كنت مطورًا، أو صاحب عمل، أو مجرد شخص يتعامل مع معلومات حساسة، فإن معرفة كيفية توقيع ملفات PDF إلكترونيًا توفر لك الوقت وتضمن مصادقة مستنداتك. في هذا الدليل، سنشرح لك عملية توقيع ملف PDF باستخدام بطاقة ذكية وحقل توقيع باستخدام Aspose.PDF لـ .NET. 

## المتطلبات الأساسية

قبل أن نتعمق في تفاصيل عملية التوقيع، دعونا نتأكد من توفر كل ما تحتاجه للبدء. إليك قائمة بالمتطلبات الأساسية:

1. Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF في بيئة .NET لديك. يمكنك تنزيلها من [موقع](https://releases.aspose.com/pdf/net/).

2. Visual Studio: ستحتاج إلى بيئة تطوير متكاملة لكتابة وتشغيل شيفرة .NET. يُعد Visual Studio Community Edition خيارًا مجانيًا رائعًا.

3. البطاقة الذكية: ضرورية لتوقيع ملف PDF. تأكد من تثبيت قارئ بطاقات ذكية والشهادات اللازمة على جهازك.

4. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم مقتطفات التعليمات البرمجية التي سنستخدمها.

5. نموذج مستند PDF: جهّز نموذجًا لمستند PDF للاختبار. يمكنك إنشاء ملف PDF فارغ أو استخدام ملف موجود.

## استيراد الحزم

قبل البدء بالبرمجة، لنستورد الحزم اللازمة. ستحتاج إلى تضمين مساحات الأسماء التالية في ملف C#:

```csharp
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

ستتيح لك هذه المساحات الوصول إلى الفئات والطرق المطلوبة للعمل مع ملفات PDF ومعالجة التوقيعات الرقمية.

## دليل خطوة بخطوة لتوقيع ملف PDF باستخدام بطاقة ذكية

بعد أن حددنا متطلباتنا الأساسية، لنُقسّم عملية التوقيع إلى خطوات سهلة. سنشرح كل خطوة بالتفصيل، لنضمن فهمك الكامل لما يحدث.

### الخطوة 1: إعداد دليل المستندات الخاص بك

ماذا تفعل: قم بتحديد المسار إلى دليل المستندات الخاص بك.

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
```

شرح: استبدال `"YOUR DOCUMENTS DIRECTORY"` مع المسار الفعلي لملفات PDF. هنا سنقرأ ملف PDF الفارغ ونحفظ المستند الموقّع.

### الخطوة 2: نسخ ملف PDF الفارغ

ما يجب فعله: قم بإنشاء نسخة من ملف PDF الفارغ الخاص بك للعمل عليها.

```csharp
File.Copy(dataDir + "blank.pdf", dataDir + "externalSignature1.pdf", true);
```

الشرح: هذا الخط ينسخ `blank.pdf` ملف إلى ملف جديد يسمى `externalSignature1.pdf`. ال `true` تسمح المعلمة بالكتابة فوق الملف إذا كان موجودًا بالفعل.

### الخطوة 3: افتح مستند PDF

ماذا تفعل: افتح ملف PDF المنسوخ للقراءة والكتابة.

```csharp
using (FileStream fs = new FileStream(dataDir + "externalSignature1.pdf", FileMode.Open, FileAccess.ReadWrite))
{
    using (Document doc = new Document(fs))
    {
        // سيتم اتخاذ الخطوات التالية هنا
    }
}
```

الشرح: نحن نستخدم `FileStream` لفتح ملف PDF الخاص بنا. `Document` تسمح لنا الفئة من Aspose.PDF بالتلاعب بمحتوى PDF.

### الخطوة 4: إنشاء حقل التوقيع

ما يجب فعله: قم بتحديد حقل التوقيع في ملف PDF حيث سيتم وضع التوقيع.

```csharp
SignatureField field1 = new SignatureField(doc.Pages[1], new Rectangle(100, 400, 10, 10));
```

التوضيح: هنا، نقوم بإنشاء `SignatureField` في الصفحة الثانية (يبدأ فهرس الصفحة من 1) من ملف PDF. `Rectangle` يحدد موضع وحجم حقل التوقيع.

### الخطوة 5: الوصول إلى مخزن شهادات البطاقة الذكية

ما يجب فعله: افتح مخزن الشهادات لتحديد شهادة البطاقة الذكية الخاصة بك.

```csharp
X509Store store = new X509Store(StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly);
```

شرح: نصل إلى مخزن الشهادات للمستخدم الحالي. هنا تُخزَّن شهادات بطاقتك الذكية.

### الخطوة 6: حدد الشهادة

ماذا تفعل: مطالبة المستخدم باختيار شهادة من المتجر.

```csharp
X509Certificate2Collection sel = X509Certificate2UI.SelectFromCollection(store.Certificates, null, null, X509SelectionFlag.SingleSelection);
```

توضيح: يفتح هذا السطر مربع حوار لاختيار شهادة. يمكنك اختيار الشهادة المرتبطة ببطاقتك الذكية.

### الخطوة 7: إنشاء توقيع خارجي

ما يجب فعله: إنشاء مثيل لـ `ExternalSignature` باستخدام الشهادة المحددة.

```csharp
Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0])
{
    Authority = "Me",
    Reason = "Reason",
    ContactInfo = "Contact"
};
```

الشرح: نقوم بتهيئة `ExternalSignature` بالشهادة المُختارة. يمكنك أيضًا تحديد الصلاحية، وسبب التوقيع، ومعلومات الاتصال.

### الخطوة 8: إضافة حقل التوقيع إلى المستند

ماذا تفعل: أضف حقل التوقيع إلى المستند.

```csharp
field1.PartialName = "sig1";
doc.Form.Add(field1, 1);
```

توضيح: نُسمّي حقل التوقيع ونُضيفه إلى الصفحة الأولى من المستند. هذا يُهيئ ملف PDF للتوقيع.

### الخطوة 9: توقيع الوثيقة

ماذا تفعل: استخدم التوقيع الخارجي لتوقيع ملف PDF.

```csharp
field1.Sign(externalSignature);
doc.Save();
```

توضيح: هذا السطر يُوقّع المستند باستخدام التوقيع الخارجي، ويحفظ التغييرات في ملف PDF. تم توقيع مستندك الآن!

### الخطوة 10: التحقق من التوقيع

ماذا تفعل: تحقق من صحة التوقيع.

```csharp
using (PdfFileSignature pdfSign = new PdfFileSignature(new Document(dataDir + "externalSignature1.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
    for (int index = 0; index <= sigNames.Count - 1; index++)
    {
        if (!pdfSign.VerifySigned(sigNames[index]) || !pdfSign.VerifySignature(sigNames[index]))
        {
            throw new ApplicationException("Not verified");
        }
    }
}
```

الشرح: نقوم بإنشاء مثيل لـ `PdfFileSignature` للتحقق من صحة التوقيعات في المستند. إذا لم يكن التوقيع صحيحًا، فسيتم طرح استثناء.

## خاتمة

تهانينا! لقد تعلمتَ للتو كيفية توقيع مستند PDF باستخدام بطاقة ذكية وحقل توقيع باستخدام Aspose.PDF لـ .NET. هذه العملية لا تُؤمّن مستنداتك فحسب، بل تضمن أيضًا مصداقيتها، مما يجعلها مهارة أساسية في عالمنا الرقمي اليوم. سواء كنت تُوقّع عقودًا أو فواتير أو أي مستندات مهمة أخرى، فإن معرفة كيفية استخدام التوقيعات الرقمية تُوفّر عليك الوقت وتُشعرك براحة البال.

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة قوية تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وتحويلها في تطبيقات .NET.

### هل أحتاج إلى بطاقة ذكية لتوقيع ملفات PDF؟
نعم، هناك حاجة إلى بطاقة ذكية لتوقيع ملفات PDF بشكل آمن باستخدام شهادة رقمية.

### هل يمكنني استخدام Aspose.PDF مجانًا؟
يقدم Aspose.PDF نسخة تجريبية مجانية، والتي يمكنك تنزيلها [هنا](https://releases.aspose.com/).

### كيف يمكنني التحقق من ملف PDF الموقّع؟
يمكنك استخدام `PdfFileSignature` يمكنك استخدام الفئة الموجودة في Aspose.PDF للتحقق من التوقيعات في مستند PDF الخاص بك.

### أين يمكنني العثور على مزيد من الوثائق حول Aspose.PDF؟
يمكنك التحقق من [وثائق Aspose.PDF](https://reference.aspose.com/pdf/net/) لمزيد من التفاصيل والأمثلة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}