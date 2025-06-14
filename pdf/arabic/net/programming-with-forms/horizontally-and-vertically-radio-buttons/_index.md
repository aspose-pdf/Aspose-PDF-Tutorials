---
"description": "تعرف على كيفية إنشاء أزرار اختيارية محاذية أفقياً ورأسياً في PDF باستخدام Aspose.PDF لـ .NET من خلال هذا البرنامج التعليمي خطوة بخطوة."
"linktitle": "أزرار الراديو أفقيًا وعموديًا"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "أزرار الراديو أفقيًا وعموديًا"
"url": "/ar/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# أزرار الراديو أفقيًا وعموديًا

## مقدمة

إنشاء نماذج PDF تفاعلية يُحسّن تجربة المستخدم بشكل ملحوظ، خاصةً عند جمع المعلومات. يُعد زر الاختيار أحد أكثر عناصر النماذج شيوعًا، حيث يتيح للمستخدمين اختيار خيار واحد من مجموعة خيارات. في هذا البرنامج التعليمي، سنستكشف كيفية إنشاء أزرار اختيار متوازية أفقيًا ورأسيًا باستخدام Aspose.PDF لـ .NET. سواءً كنت مطورًا متمرسًا أو مبتدئًا، سيرشدك هذا الدليل خلال العملية خطوة بخطوة، مما يضمن لك فهمًا واضحًا لكل جزء.

## المتطلبات الأساسية

قبل الغوص في الكود، هناك بعض المتطلبات الأساسية التي يجب أن تكون موجودة لديك:

1. Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF. يمكنك تنزيلها من [موقع](https://releases.aspose.com/pdf/net/).
2. Visual Studio: بيئة تطوير يمكنك من خلالها كتابة واختبار الكود الخاص بك.
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم مقتطفات التعليمات البرمجية بشكل أفضل.

## استيراد الحزم

للبدء، عليك استيراد الحزم اللازمة في مشروع C# الخاص بك. إليك كيفية القيام بذلك:

### إنشاء مشروع جديد

افتح Visual Studio وأنشئ مشروع C# جديدًا. يمكنك اختيار تطبيق وحدة التحكم لتسهيل الأمر.

### إضافة مرجع Aspose.PDF

1. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
2. حدد "إدارة حزم NuGet".
3. ابحث عن "Aspose.PDF" وقم بتثبيت الإصدار الأحدث.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

الآن بعد أن قمت بإعداد كل شيء، دعنا نقوم بتقسيم الكود لإنشاء أزرار راديو محاذية أفقيًا ورأسيًا.

## الخطوة 1: إعداد دليل المستندات

في هذه الخطوة، سنقوم بتحديد المسار إلى الدليل الذي سيتم تخزين مستندات PDF الخاصة بك فيه.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

يستبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي تريد حفظ ملف PDF فيه. هذا أمر بالغ الأهمية لأنه يُحدد للبرنامج مكان البحث عن ملفات الإدخال ومكان حفظ المخرجات.

## الخطوة 2: تحميل مستند PDF الموجود

بعد ذلك، علينا تحميل ملف PDF الذي سنعمل عليه. يتم ذلك باستخدام `FormEditor` فصل.

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

هنا، نقوم بإنشاء مثيل لـ `FormEditor` وربطه بملف PDF موجود باسم `input.pdf`تأكد من وجود هذا الملف في الدليل المحدد.

## الخطوة 3: تكوين خصائص زر الاختيار

الآن، لنُحدد بعض خصائص أزرار الاختيار. يشمل ذلك المسافة بين الأزرار، واتجاهها، وحجمها.

```csharp
formEditor.RadioGap = 4; // المسافة بين خيارات أزرار الراديو
formEditor.RadioHoriz = true; // تم ضبطه على true للمحاذاة الأفقية
formEditor.RadioButtonItemSize = 20; // حجم زر الراديو
formEditor.Facade.BorderWidth = 1; // عرض الحدود
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // لون الحدود
```

ستساعدك هذه الخصائص في تحديد كيفية ظهور أزرار الاختيار في ملف PDF. `RadioGap` تتحكم الخاصية في المسافة بين الأزرار، بينما `RadioHoriz` يحدد تخطيطهم.

## الخطوة 4: إضافة أزرار راديو أفقية

الآن، دعونا نضيف أزرار الراديو الأفقية إلى ملف PDF.

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

في هذا الكود، نقوم بتعريف العناصر الخاصة بأزرار الراديو وإضافتها إلى ملف PDF. `AddField` تأخذ الطريقة عدة معلمات، بما في ذلك نوع الحقل، واسم الحقل، وإحداثيات الموضع.

## الخطوة 5: إضافة أزرار الراديو العمودية

بعد ذلك، سنضيف أزرار الاختيار العمودية. للقيام بذلك، علينا تغيير اتجاهها إلى الوضع العمودي.

```csharp
formEditor.RadioHoriz = false; // تم ضبطه على خطأ للمحاذاة الرأسية
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

تمامًا كما في السابق، نقوم بتعريف العناصر وإضافتها إلى ملف PDF، ولكن هذه المرة سيتم محاذاتها عموديًا.

## الخطوة 6: حفظ مستند PDF

وأخيرًا، نحتاج إلى حفظ مستند PDF المعدّل.

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

يحفظ هذا الكود ملف PDF بأزرار الاختيار المُضافة حديثًا. تأكد من تحديد المجلد المُحدد لملف الإخراج.

## خاتمة

إنشاء أزرار اختيار في ملف PDF باستخدام Aspose.PDF لـ .NET عملية سهلة وبسيطة. باتباع الخطوات الموضحة في هذا البرنامج التعليمي، يمكنك بسهولة إضافة أزرار اختيار محاذية أفقيًا ورأسيًا إلى نماذج PDF. هذا لا يُحسّن تفاعلية مستنداتك فحسب، بل يُحسّن أيضًا تجربة المستخدم بشكل عام. جرّبه الآن!

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة قوية تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وتحويلها برمجيًا.

### هل يمكنني استخدام Aspose.PDF مجانًا؟
نعم، يُقدّم Aspose نسخة تجريبية مجانية يُمكنك استخدامها لتقييم المكتبة. يُمكنك تنزيلها. [هنا](https://releases.aspose.com/).

### كيف أحصل على الدعم لـ Aspose.PDF؟
يمكنك الحصول على الدعم من خلال زيارة [منتدى Aspose](https://forum.aspose.com/c/pdf/10).

### هل من الممكن إنشاء عناصر نموذج أخرى باستخدام Aspose.PDF؟
بالتأكيد! يدعم Aspose.PDF عناصر نموذج متنوعة، بما في ذلك حقول النص، ومربعات الاختيار، والقوائم المنسدلة.

### أين يمكنني شراء Aspose.PDF لـ .NET؟
يمكنك شراء Aspose.PDF لـ .NET من [صفحة الشراء](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}