---
"date": "2025-04-12"
"description": "تعرّف على كيفية تخصيص نص التوقيع الرقمي في ملفات PDF باستخدام Aspose.PDF لـ .NET. مثالي لإعداد وترجمة المستندات متعددة اللغات."
"title": "كيفية تغيير لغة توقيع PDF باستخدام Aspose.PDF لـ .NET"
"url": "/ar/net/digital-signatures/change-pdf-signature-language-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# كيفية تغيير لغة توقيع PDF باستخدام Aspose.PDF لـ .NET

## مقدمة

هل ترغب في تخصيص لغة التوقيعات الرقمية في مستندات PDF باستخدام .NET؟ سواء كنت تُعِدّ عقودًا أو اتفاقيات أو أي مستند آخر يتطلب توقيعًا، فإن ترجمة النصوص لمختلف اللغات أمرٌ أساسي. سيرشدك هذا البرنامج التعليمي خلال تغيير إعدادات لغة التوقيعات الرقمية في ملفات PDF باستخدام Aspose.PDF لـ .NET، لضمان توافق مستنداتك مع المعايير الدولية وتلبية احتياجات الجمهور العالمي.

**ما سوف تتعلمه:**
- كيفية إعداد Aspose.PDF لـ .NET.
- تغيير لغات نص التوقيع باستخدام Aspose.PDF `SignatureCustomAppearance` فصل.
- تكوين معلمات التوقيع مثل تنسيق التاريخ والموقع والسبب وما إلى ذلك.
- حفظ مستند PDF الموقع بإعدادات اللغة المخصصة.

مع تعمقنا في هذا الدليل، تأكد من استعدادك من خلال تلبية المتطلبات الأساسية المذكورة أدناه للبدء بسلاسة.

## المتطلبات الأساسية

قبل أن نبدأ في تنفيذ حلنا، دعونا نتأكد من إعداد كل شيء:

### المكتبات والتبعيات المطلوبة
ستحتاج إلى ملف Aspose.PDF لـ .NET. تأكد من أن مشروعك يستهدف إصدارًا متوافقًا مع .NET (يفضل .NET Framework 4.x أو أحدث).

### متطلبات إعداد البيئة
- تم تثبيت Visual Studio على جهازك.
- الوصول إلى محرر أكواد مثل Visual Studio Code أو أي بيئة تطوير متكاملة أخرى من اختيارك.

### متطلبات المعرفة
سيكون من المفيد، وإن لم يكن ضروريًا، فهم أساسيات برمجة C# والإلمام بمعالجة ملفات PDF. سنشرح لك كل خطوة، لضمان وضوح العملية.

## إعداد Aspose.PDF لـ .NET

لبدء استخدام Aspose.PDF، يجب تثبيته في مشروعك. إليك كيفية القيام بذلك:

**.NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**مدير الحزمة:**
```powershell
Install-Package Aspose.PDF
```

**واجهة مستخدم مدير حزمة NuGet:**  
ابحث عن "Aspose.PDF" وقم بتثبيت الإصدار الأحدث.

### خطوات الحصول على الترخيص
يمكنك البدء بفترة تجريبية مجانية من Aspose.PDF لاستكشاف ميزاته. للاستخدام طويل الأمد، فكّر في شراء ترخيص أو الحصول على ترخيص مؤقت باتباع الخطوات التالية:
- **نسخة تجريبية مجانية**:تحميل من [صفحة إصدار Aspose](https://releases.aspose.com/pdf/net/).
- **رخصة مؤقتة**: اطلبها عبر [صفحة الترخيص المؤقت لـ Aspose](https://purchase.aspose.com/temporary-license/) لإجراء اختبار موسع.
- **شراء**:تأمين ترخيص كامل في [صفحة شراء Aspose](https://purchase.aspose.com/buy) لفتح كافة الميزات دون قيود.

### التهيئة والإعداد الأساسي
بمجرد تثبيت Aspose.PDF، قم بتهيئته في مشروعك على النحو التالي:

```csharp
using Aspose.Pdf.Facades;
```
توفر مساحة الاسم هذه إمكانية الوصول إلى `PdfFileSignature` الصف، أمر حاسم لمهمتنا.

## دليل التنفيذ

دعونا نقوم بتقسيم عملية تغيير إعدادات اللغة للتوقيعات الرقمية إلى خطوات يمكن التحكم فيها.

### إعداد مظهر التوقيع

#### ملخص
سنقوم بتكوين كيفية ظهور التوقيع على ملف PDF الخاص بك، مع التركيز على تخصيص عناصر النص مثل التاريخ والسبب والموقع لتناسب اللغات المختلفة.

**قم بتحميل مستندك**
أولاً، قم بإنشاء مثيل لـ `PdfFileSignature` وربطه بملف PDF المدخل الخاص بك:

```csharp
using (Aspose.Pdf.Facades.PdfFileSignature pdfSign = new Aspose.Pdf.Facades.PdfFileSignature())
{
    pdfSign.BindPdf("input.pdf");
}
```

**تعريف مستطيل التوقيع**
حدد المنطقة على الصفحة التي سيظهر فيها التوقيع:

```csharp
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(310, 45, 200, 50);
```

### تكوين تفاصيل التوقيع

#### ملخص
حدّد معايير مختلفة، مثل سبب ومكان توقيعاتك الرقمية. خصّصها لتظهر بأي لغة.

**إنشاء كائن توقيع PKCS#7**
إنشاء مثيل `PKCS7` الكائن مع تفاصيل الشهادة اللازمة:

```csharp
PKCS7 pkcs = new PKCS7("certificate.pfx", "12345");
pkcs.Reason = "Pruebas Firma";
pkcs.ContactInfo = "Contacto Pruebas";
pkcs.Location = "Población (Provincia)";
pkcs.Date = DateTime.Now;
```

**تخصيص مظهر التوقيع**
يستخدم `SignatureCustomAppearance` لضبط خصائص النص وإعدادات اللغة:

```csharp
SignatureCustomAppearance signatureCustomAppearance = new SignatureCustomAppearance();
signatureCustomAppearance.DateSignedAtLabel = "Fecha";
signatureCustomAppearance.DigitalSignedLabel = "Digitalmente firmado por";
signatureCustomAppearance.ReasonLabel = "Razón";
signatureCustomAppearance.LocationLabel = "Localización";
signatureCustomAppearance.FontFamilyName = "Arial";
signatureCustomAppearance.FontSize = 10d;
signatureCustomAppearance.Culture = CultureInfo.InvariantCulture;
signatureCustomAppearance.DateTimeFormat = "yyyy.MM.dd HH:mm:ss";

pkcs.CustomAppearance = signatureCustomAppearance;
```

### توقيع ملف PDF
**تطبيق التوقيع**
استخدم `Sign` الطريقة لتطبيق التوقيع الذي قمت بتكوينه:

```csharp
pdfSign.Sign(1, true, rect, pkcs);
```

### حفظ ملف الإخراج
**حفظ المستند الموقع**
أخيرًا، احفظ ملف PDF الموقّع الخاص بك مع تطبيق إعدادات اللغة الجديدة:

```csharp
pdfSign.Save("output.pdf");
```

## التطبيقات العملية
فيما يلي بعض السيناريوهات الواقعية حيث يمكن الاستفادة من هذه الميزة:
1. **العقود التجارية الدولية**:ترجمة نص التوقيع للشركاء في بلدان مختلفة.
2. **الوثائق القانونية**:ضمان الامتثال للمتطلبات القانونية الإقليمية من خلال عرض التوقيعات باللغة المحلية.
3. **المواد التعليمية**:توفير الشهادات أو الوثائق للطلاب الدوليين بلغاتهم الأصلية.
4. **نماذج حكومية**:تخصيص النماذج التي تتطلب توقيعات رسمية، مثل التصاريح والتسجيلات.
5. **الشركات المتعددة الجنسيات**:تبسيط سير عمل المستندات للموظفين في مختلف المناطق.

## اعتبارات الأداء
عند العمل مع ملفات PDF كبيرة أو كميات كبيرة من المستندات، ضع في اعتبارك النصائح التالية:
- قم بتحسين استخدام الذاكرة عن طريق معالجة المستندات بشكل تسلسلي عندما يكون ذلك ممكنًا.
- استخدم ميزات إدارة الموارد في Aspose.PDF للتعامل مع الملفات الكبيرة بكفاءة.
- قم بتحديث Aspose.PDF بانتظام للاستفادة من تحسينات الأداء وإصلاحات الأخطاء.

## خاتمة
في هذا البرنامج التعليمي، استكشفنا كيفية تخصيص لغة التوقيعات الرقمية في ملفات PDF باستخدام Aspose.PDF لـ .NET. باتباع هذه الخطوات، يمكنك ضمان استيفاء مستنداتك للمعايير الدولية وإتاحتها للجمهور العالمي.

لمواصلة استكشاف إمكانيات Aspose.PDF، جرّب ميزات أخرى مثل التشفير أو تعبئة النماذج. لأي استفسار أو مساعدة إضافية، يُرجى التواصل معنا. [منتدى أسبوزي](https://forum.aspose.com/c/pdf/10) يعد مصدرًا ممتازًا.

## قسم الأسئلة الشائعة
**س1: كيف أتعامل مع تنسيقات التاريخ المختلفة في مواقع مختلفة؟**
أ1: الاستخدام `signatureCustomAppearance.DateTimeFormat` لتحديد التنسيق المطلوب لكل موقع تدعمه.

**س2: هل يمكنني استخدام Aspose.PDF بدون ترخيص لأغراض تجارية؟**
ج٢: يمكنك البدء بفترة تجريبية مجانية، ولكن شراء ترخيص ضروري للاستخدام التجاري طويل الأمد. تفضل بزيارة [صفحة شراء Aspose](https://purchase.aspose.com/buy) لمزيد من المعلومات.

**س3: ماذا لو تجاوز نص توقيعي حجم المستطيل المحدد؟**
ج3: تأكد من تعديل حجم الخط والمحتوى ليتناسب مع المساحة المخصصة، أو قم بزيادة أبعاد المستطيل وفقًا لذلك.

**س4: كيف يمكنني تطبيق توقيعات متعددة بلغات مختلفة في ملف PDF واحد؟**
A4: كرر عملية التوقيع لكل كتلة توقيع، مع تكوين `SignatureCustomAppearance` حسب الحاجة لكل لغة.

**س5: هل Aspose.PDF متوافق مع جميع إصدارات .NET؟**
A5: يدعم Aspose.PDF مجموعة واسعة من إصدارات .NET. تحقق من [توثيق Aspose](https://reference.aspose.com/pdf/net/) للحصول على أحدث تفاصيل التوافق.

## موارد
- **التوثيق**: [الوثائق الرسمية](https://reference.aspose.com/pdf/net/)
- **تحميل**: [أحدث الإصدارات](https://releases.aspose.com/pdf/net/)
- **شراء**: [شراء ترخيص](https://purchase.aspose.com/buy)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}