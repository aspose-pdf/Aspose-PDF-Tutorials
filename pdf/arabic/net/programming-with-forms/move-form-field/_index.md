---
"description": "تعرّف على كيفية نقل حقول النماذج في مستندات PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل. اتبع هذا الدليل المفصل لتعديل مواقع مربعات النص بسهولة."
"linktitle": "نقل حقل النموذج"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "نقل حقل النموذج"
"url": "/ar/net/programming-with-forms/move-form-field/"
"weight": 200
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# نقل حقل النموذج

## مقدمة

قد يبدو تعديل حقول النماذج في مستندات PDF صعبًا في البداية، ولكن مع Aspose.PDF لـ .NET، الأمر في غاية السهولة! سواء كنت تعمل على نقل مربعات النص، أو تحسين التخطيطات، أو تعديل العناصر التفاعلية، فإن Aspose.PDF يوفر حلاً فعالاً لمشاريع .NET الخاصة بك. في هذا البرنامج التعليمي، سنرشدك خلال خطوات نقل حقل نموذج في مستند PDF باستخدام Aspose.PDF لـ .NET.

## المتطلبات الأساسية

قبل أن نبدأ، إليك بعض الأشياء التي ستحتاجها:

1. تم تثبيت Aspose.PDF لـ .NET في بيئة التطوير الخاصة بك.
2. ملف PDF يحتوي على حقل نموذج (في هذه الحالة، مربع نص) المراد تعديله.
3. المعرفة الأساسية ببرمجة C#.
4. Visual Studio أو أي بيئة تطوير C# أخرى.

### تثبيت Aspose.PDF لـ .NET

يمكنك تنزيل أحدث إصدار من Aspose.PDF لـ .NET من [صفحة تنزيل Aspose](https://releases.aspose.com/pdf/net/)بعد التنزيل، يمكنك تثبيته عبر NuGet في Visual Studio عن طريق تشغيل الأمر التالي:

```bash
Install-Package Aspose.PDF
```

سوف تحتاج أيضًا إلى الحصول على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) أو شراء ترخيص من [متجر أسبووز](https://purchase.aspose.com/buy).

## استيراد الحزم

قبل أن تتمكن من استخدام Aspose.PDF، ستحتاج إلى استيراد المساحات المطلوبة في كود C# الخاص بك:

```csharp
using System;
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
```

ستتيح لك هذه الحزم الوصول إلى ميزات معالجة مستندات PDF الأساسية ووظائف النماذج المحددة التي تحتاجها.

الآن بعد أن أصبحت كل الأمور جاهزة، دعنا نستعرض عملية نقل حقل نموذج في مستند PDF باستخدام Aspose.PDF لـ .NET.

## الخطوة 1: إعداد مشروعك وتحميل مستند PDF

أول ما عليك فعله هو إعداد مشروعك وتحميل ملف PDF الذي يحتوي على حقل النموذج الذي تريد تعديله. إليك كيفية القيام بذلك:

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// فتح المستند
Document pdfDocument = new Document(dataDir + "MoveFormField.pdf");
```

يقوم هذا الكود بتهيئة المستند بتحميله من الدليل المحدد. تأكد من استبدال `"YOUR DOCUMENT DIRECTORY"` مع مسار الملف الفعلي الذي يُخزَّن فيه ملف PDF. يجب أن يحتوي هذا الملف على حقل نموذج واحد على الأقل لتتمكن من العمل عليه.

## الخطوة 2: الوصول إلى حقل النموذج المراد نقله

بعد تحميل ملف PDF، الخطوة التالية هي الوصول إلى حقل النموذج الذي ترغب بنقله. في هذه الحالة، ننقل حقل نموذج مربع نص، ولكن يمكن تطبيق هذه الطريقة على أنواع أخرى من حقول النماذج أيضًا.

```csharp
// الحصول على حقل النموذج حسب اسمه (في هذه الحالة، "textbox1")
TextBoxField textBoxField = pdfDocument.Form["textbox1"] as TextBoxField;
```

هنا، نقوم بالوصول إلى حقل نموذج يسمى `"textbox1"`تأكد من أنك تعرف اسم حقل النموذج الذي تريد التعامل معه، أو يمكنك استخدام تقنيات أخرى لإدراج حقول النموذج أو البحث فيها إذا لزم الأمر.

## الخطوة 3: تعديل موقع الحقل

الآن يأتي الجزء المثير: نقل حقل النموذج! نحقق ذلك بتعديل حدوده المستطيلة، التي تُحدد موضع وحجم حقل النموذج على الصفحة.

```csharp
// تعديل موقع حقل النموذج (إحداثيات جديدة)
textBoxField.Rect = new Aspose.Pdf.Rectangle(300, 400, 600, 500);
```

في سطر التعليمات البرمجية أعلاه، نحدد موضع مربع النص بتحديد إحداثيات مستطيله. تمثل الأرقام الزوايا السفلية اليسرى والعلوية اليمنى للمستطيل (`300, 400, 600, 500`يمكنك تخصيص هذه القيم استنادًا إلى المكان الذي تريد أن يظهر فيه الحقل على الصفحة.

## الخطوة 4: حفظ المستند المعدّل

بعد نقل حقل النموذج، الخطوة الأخيرة هي حفظ ملف PDF المُعدَّل. يمكنك حفظه باسم جديد لتجنب الكتابة فوق المستند الأصلي.

```csharp
// احفظ مستند PDF المحدث
dataDir = dataDir + "MoveFormField_out.pdf";
pdfDocument.Save(dataDir);
Console.WriteLine("\nForm field moved successfully to a new location.\nFile saved at " + dataDir);
```

سيتم حفظ المستند في نفس الدليل باسم محدث (`MoveFormField_out.pdf`بعد الحفظ، يمكنك فتح الملف للتأكد من نقل حقل النموذج إلى الموقع المطلوب.

## خاتمة

يعد نقل حقول النموذج داخل ملف PDF باستخدام Aspose.PDF لـ .NET أمرًا بسيطًا بمجرد فهمك لأساسيات العمل مع `Rectangle` حقول الكائنات والنماذج. باستخدام الكود أعلاه، يمكنك بسهولة تعديل موضع أي حقل نموذج، مما يساعدك على تخصيص تخطيطات ملفات PDF وتفاعلات المستخدم.

## الأسئلة الشائعة

### هل يمكنني نقل أنواع أخرى من حقول النموذج باستخدام هذه الطريقة؟
نعم، يمكنك نقل أي حقل نموذج، بما في ذلك مربعات الاختيار، وأزرار الاختيار، والتوقيعات، باستخدام نفس الطريقة عن طريق الوصول إلى نوع الحقل المحدد.

### كيف يمكنني استرجاع أسماء جميع حقول النموذج في ملف PDF؟
يمكنك التكرار خلال حقول النموذج باستخدام `pdfDocument.Form.Fields` لإدراج جميع حقول النموذج وأسمائها.

### ماذا لو أردت تغيير حجم حقل النموذج بدلاً من نقله؟
يمكنك تعديل كل من الموقع والحجم عن طريق ضبط `Rectangle` عرض وارتفاع الكائن أثناء تعيين الإحداثيات الجديدة.

### هل أحتاج إلى ترخيص لاستخدام Aspose.PDF لـ .NET؟
نعم، يتطلب Aspose.PDF ترخيصًا للاستخدام الإنتاجي، ولكن يمكنك الحصول عليه [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) لأغراض التقييم.

### هل يمكنني نقل حقول نماذج متعددة مرة واحدة؟
نعم، عن طريق الوصول إلى كل حقل نموذج وتعديله `Rect` الخاصية، يمكنك نقل حقول متعددة في وقت واحد.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}