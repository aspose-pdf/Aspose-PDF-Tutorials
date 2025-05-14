---
"description": "تعرّف على كيفية توقيع ملفات PDF باستخدام بطاقة ذكية مع Aspose.PDF لـ .NET. اتبع هذا الدليل خطوة بخطوة للحصول على توقيعات رقمية آمنة."
"linktitle": "التوقيع باستخدام البطاقة الذكية باستخدام توقيع ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "التوقيع باستخدام البطاقة الذكية باستخدام توقيع ملف PDF"
"url": "/ar/net/programming-with-security-and-signatures/sign-with-smart-card-using-pdf-file-signature/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# التوقيع باستخدام البطاقة الذكية باستخدام توقيع ملف PDF

## مقدمة

في العصر الرقمي، أصبح تأمين المستندات أكثر أهمية من أي وقت مضى. سواءً أكانت عقدًا أم اتفاقية أم أي معلومات حساسة، فإن ضمان صحة المستند وعدم التلاعب به أمر بالغ الأهمية. انضموا إلينا في عالم التوقيعات الرقمية! سنتناول اليوم كيفية توقيع ملف PDF باستخدام بطاقة ذكية باستخدام Aspose.PDF لـ .NET. تتيح هذه المكتبة القوية للمطورين إنشاء مستندات PDF ومعالجتها بكفاءة، بما في ذلك إضافة توقيعات رقمية آمنة. هيا، احصلوا على بطاقتكم الذكية، ولنبدأ!

## المتطلبات الأساسية

قبل أن نتعمق في تفاصيل توقيع ملف PDF، لنتأكد من تجهيز كل ما تحتاجه. إليك قائمة مرجعية لمساعدتك في التحضير:

1. Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF. يمكنك تنزيلها من [موقع](https://releases.aspose.com/pdf/net/).
2. Visual Studio: بيئة تطوير حيث يمكنك كتابة وتشغيل الكود .NET الخاص بك.
3. البطاقة الذكية: ستحتاج إلى بطاقة ذكية مثبت عليها شهادة رقمية صالحة.
4. الفهم الأساسي لـ C#: سيكون من المفيد التعرف على برمجة C# لأننا سنكتب أجزاء من التعليمات البرمجية بهذه اللغة.
5. مستند PDF: ملف PDF نموذجي (مثل `blank.pdf`) لاختبار عملية التوقيع لدينا.

مع توفر هذه المتطلبات الأساسية، فأنت جاهز للبدء في تعلم الكود!

## استيراد الحزم

أولاً، لنستورد الحزم اللازمة. ستحتاج إلى إضافة مراجع إلى مكتبة Aspose.PDF في مشروعك. إليك كيفية القيام بذلك:

1. افتح Visual Studio.
2. إنشاء مشروع جديد أو فتح مشروع موجود.
3. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول وحدد `Manage NuGet Packages`.
4. بحث عن `Aspose.PDF` وتثبيت الإصدار الأحدث.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

الآن بعد أن قمنا باستيراد الحزم اللازمة، فلنبدأ بتقسيم الكود خطوة بخطوة.

## الخطوة 1: إعداد مستندك

الخطوة الأولى في عمليّتنا هي إعداد ملف PDF الذي نريد توقيعه. إليك كيفية القيام بذلك:

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
Document doc = new Document(dataDir + "blank.pdf");
```
في هذا المقطع، نقوم بتحديد المسار إلى دليل المستندات الخاص بنا وإنشاء مثيل لـ `Document` الفصل باستخدام ملف PDF عينة يسمى `blank.pdf`. تأكد من استبدال `"YOUR DOCUMENTS DIRECTORY"` مع المسار الفعلي الذي يوجد به ملف PDF الخاص بك.

## الخطوة 2: تهيئة PdfFileSignature

بعد ذلك، سنقوم بتهيئة `PdfFileSignature` الفئة المسؤولة عن التعامل مع عملية التوقيع.

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature())
{
    pdfSign.BindPdf(doc);
```
هنا، نقوم بإنشاء مثيل لـ `PdfFileSignature` وأرفقه بملف PDF الخاص بنا. هذا يُهيئ المستند للتوقيع.

## الخطوة 3: الوصول إلى شهادة البطاقة الذكية

الآن يأتي الجزء الأهم - الوصول إلى الشهادة الرقمية المخزنة على بطاقتك الذكية. إليك كيفية القيام بذلك:

### افتح مخزن الشهادات

```csharp
System.Security.Cryptography.X509Certificates.X509Store store = new System.Security.Cryptography.X509Certificates.X509Store(System.Security.Cryptography.X509Certificates.StoreLocation.CurrentUser);
store.Open(System.Security.Cryptography.X509Certificates.OpenFlags.ReadOnly);
```
نفتح مخزن الشهادات الموجود في ملف تعريف المستخدم الحالي. يتيح لنا هذا الوصول إلى الشهادات المثبتة على جهازك، بما في ذلك تلك الموجودة على بطاقتك الذكية.

### حدد الشهادة

```csharp
System.Security.Cryptography.X509Certificates.X509Certificate2Collection sel =
    System.Security.Cryptography.X509Certificates.X509Certificate2UI.SelectFromCollection(
        store.Certificates, null, null, System.Security.Cryptography.X509Certificates.X509SelectionFlag.SingleSelection);
```
يُطالب هذا الرمز المستخدم باختيار شهادة من المجموعة. ستعرض واجهة المستخدم جميع الشهادات المتاحة، مما يسمح لك باختيار الشهادة المرتبطة ببطاقتك الذكية.

## الخطوة 4: إنشاء التوقيع الخارجي

بمجرد تحديد الشهادة، فإن الخطوة التالية هي إنشاء توقيع خارجي باستخدام الشهادة المحددة.

```csharp
Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0]);
```
هنا، نقوم بإنشاء مثيل لـ `ExternalSignature` باستخدام الشهادة المحددة. سيتم استخدام هذا الكائن لتوقيع مستند PDF.

## الخطوة 5: تعيين مظهر التوقيع

الآن، لنُحدد مظهر توقيعنا. هنا يمكنك تخصيص مظهر توقيعك في المستند.

```csharp
pdfSign.SignatureAppearance = dataDir + "demo.png";
```
في هذا المقطع، نحدد مظهر التوقيع بتوفير مسار ملف صورة (مثل شعار أو رسم توقيع). تأكد من استبدال `"demo.png"` مع الصورة الفعلية التي تريد استخدامها.

## الخطوة 6: التوقيع على ملف PDF

بعد إعداد كل شيء، حان الوقت لتوقيع مستند PDF!

```csharp
pdfSign.Sign(1, "Reason", "Contact", "Location", true, new System.Drawing.Rectangle(100, 100, 200, 200), externalSignature);
pdfSign.Save(dataDir + "externalSignature2.pdf");
```
في هذه الخطوة، نسميها `Sign` الطريقة على موقعنا `pdfSign` الكائن. إليك ما يعنيه كل معلمة:
- `1`:رقم الصفحة التي سيظهر فيها التوقيع.
- `"Reason"`:سبب التوقيع على الوثيقة.
- `"Contact"`:معلومات الاتصال بالموقع.
- `"Location"`:مكان الموقع.
- `true`: يشير إلى ما إذا كان سيتم إنشاء توقيع مرئي.
- `new System.Drawing.Rectangle(100, 100, 200, 200)`:موضع وحجم التوقيع على ملف PDF.
- `externalSignature`:كائن التوقيع الذي أنشأناه سابقًا.

وأخيرًا، نحفظ المستند الموقع باسم `externalSignature2.pdf`.

## الخطوة 7: التحقق من التوقيع

بعد توقيع الوثيقة، من الضروري التحقق من صحة التوقيع. إليك كيفية القيام بذلك:

### تهيئة عملية التحقق

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature(new Document(dataDir + "externalSignature2.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
```
نقوم بإنشاء مثيل جديد لـ `PdfFileSignature` للوثيقة الموقّعة. ثم نسترد أسماء جميع التوقيعات الموجودة في الوثيقة.

### التحقق من صحة التوقيع

```csharp
for (int index = 0; index <= sigNames.Count - 1; index++)
{
    if (!pdfSign.VerifySigned(sigNames[index]) || !pdfSign.VerifySignature(sigNames[index]))
    {
        throw new ApplicationException("Not verified");
    }
}
```
نراجع كل اسم توقيع ونتحقق من صحته. إذا فشل أي توقيع في التحقق، يُطرح استثناء، مما يشير إلى عدم صحته.

## خاتمة

ها قد انتهيت! لقد وقّعت بنجاح مستند PDF باستخدام بطاقة ذكية مع Aspose.PDF لـ .NET. هذه العملية لا تؤمّن مستندك فحسب، بل تُضيف أيضًا طبقة من الموثوقية، وهو أمر بالغ الأهمية في عالمنا الرقمي اليوم. سواء كنت تتعامل مع عقود أو مستندات قانونية أو أي معلومات حساسة، فإن معرفة كيفية تطبيق التوقيعات الرقمية مهارة قيّمة. 

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة قوية تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وتحويلها داخل تطبيقات .NET.

### هل أحتاج إلى بطاقة ذكية لتوقيع ملفات PDF؟
على الرغم من أن البطاقة الذكية ليست إلزامية، إلا أنها يوصى بها بشدة للتوقيعات الرقمية الآمنة، حيث إنها توفر طبقة إضافية من الأمان.

### هل يمكنني استخدام أي ملف PDF للتوقيع؟
نعم، يمكنك استخدام أي ملف PDF، ولكن تأكد من أنه غير محمي بكلمة مرور. إذا كان كذلك، فسيتعين عليك إلغاء قفله أولاً.

### ماذا لو لم يكن لدي شهادة رقمية؟
يمكنك الحصول على شهادة رقمية من هيئة إصدار الشهادات الموثوقة (CA) أو استخدام شهادة موقعة ذاتيًا لأغراض الاختبار.

### هل هناك نسخة تجريبية من Aspose.PDF متاحة؟
نعم، يمكنك تنزيل نسخة تجريبية مجانية من [موقع Aspose](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}