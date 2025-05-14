---
"description": "تعرّف على كيفية إضافة وحذف جافا سكريبت إلى مستند PDF باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة مع دروس تعليمية حول البرمجة النصية على مستوى المستند."
"linktitle": "إضافة إزالة JavaScript إلى المستند"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة إزالة JavaScript إلى مستند PDF"
"url": "/ar/net/programming-with-document/addremovejavascripttodoc/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة إزالة JavaScript إلى مستند PDF

## مقدمة

في هذا الدليل، سنشرح كيفية استخدام Aspose.PDF لـ .NET لإدراج جافا سكريبت في ملف PDF، وكيفية إزالته عند الحاجة. بنهاية هذا البرنامج التعليمي، ستفهم بوضوح كيفية التعامل مع جافا سكريبت في ملفات PDF بسهولة.

## المتطلبات الأساسية

قبل أن نتعمق في الكود، هناك بعض الأشياء التي ستحتاج إلى إعدادها:

1. Aspose.PDF لـ .NET: ستحتاج إلى تثبيت مكتبة Aspose.PDF لـ .NET في مشروعك. إذا لم تكن لديك المكتبة بعد، فاحصل عليها من [صفحة تنزيل Aspose.PDF لـ .NET](https://releases.aspose.com/pdf/net/).
2. IDE أو محرر النصوص: يمكنك استخدام أي IDE متوافق مع .NET مثل Visual Studio.
3. المعرفة الأساسية بلغة C#: يفترض هذا البرنامج التعليمي أنك مرتاح في استخدام لغة C# ومطلع على كيفية التعامل مع ملفات PDF.
4. الترخيص: تأكد من الحصول على ترخيص ساري المفعول لتجنب القيود. يمكنك الحصول على ترخيص مؤقت من [هنا](https://purchase.aspose.com/temporary-license/).

## استيراد الحزم

لبدء استخدام Aspose.PDF لـ .NET، ستحتاج إلى استيراد مساحات الأسماء اللازمة إلى مشروعك. إليك الطريقة:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Collections;
```

هذه المساحتان الاسميتان ضروريتان. `Aspose.Pdf` يسمح لك بالعمل مع مستندات PDF، بينما `System.Collections` سيتم استخدامها للتعامل مع مفاتيح JavaScript.

دعنا نقوم بتقسيم العملية الكاملة لإضافة وإزالة JavaScript من ملف PDF إلى خطوات سهلة المتابعة.

## الخطوة 1: تهيئة مستند PDF جديد

أول ما عليك فعله هو إنشاء مستند PDF جديد. سيكون هذا المستند بمثابة لوحة فارغة لإضافة جافا سكريبت.

```csharp
Document doc = new Document();
doc.Pages.Add();
```

هنا، نقوم بتهيئة ملف جديد `Document` إضافة صفحة فارغة إليه. اعتبر هذا أساس ملف PDF الخاص بك.

## الخطوة 2: إضافة JavaScript إلى ملف PDF

الآن وقد أصبح لدينا مستند، حان الوقت لإضافة بعض جافا سكريبت إليه. يمكن استخدام جافا سكريبت في ملفات PDF لإضافة سلوكيات مخصصة، مثل التنبيهات أو التحقق من صحة النماذج.

```csharp
doc.JavaScript["func1"] = "function func1() { hello(); }";
doc.JavaScript["func2"] = "function func2() { hello(); }";
```

في مقتطف التعليمات البرمجية هذا، نضيف دالتين JavaScript (`func1` و `func2`) إلى ملف PDF. يمكن لهذه الدوال تنفيذ مهام متنوعة، حسب احتياجاتك. هنا، نقوم فقط باستدعاء دالة مؤقتة تُسمى `hello()`.

## الخطوة 3: حفظ ملف PDF باستخدام JavaScript

بمجرد إضافة JavaScript المطلوب، حان الوقت لحفظ ملف PDF.

```csharp
doc.Save(dataDir + "AddJavascript.pdf");
```

سيؤدي هذا إلى حفظ المستند باستخدام JavaScript تحت الاسم `AddJavascript.pdf` في الدليل المحدد (`dataDir`).

## الخطوة 4: تحميل وعرض JavaScript في ملف PDF الموجود

لنفترض أنك بحاجة إلى التحقق من وظائف JavaScript أو تعديلها ضمن ملف PDF موجود. الخطوة الأولى هي تحميل ملف PDF والوصول إلى مفاتيح JavaScript.

```csharp
Document doc1 = new Document(dataDir + "AddJavascript.pdf");
IList keys = (System.Collections.IList)doc1.JavaScript.Keys;
```

نحن نقوم بتحميل الموجود `AddJavascript.pdf` وتخزين مفاتيح JavaScript في قائمة. `Keys` تقوم الخاصية بإرجاع أسماء جميع وظائف JavaScript المرفقة بالمستند.

## الخطوة 5: عرض وظائف JavaScript

بعد ذلك، يمكننا تكرار وظائف JavaScript لمعرفة ما هو متاح في المستند.

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
```

سيؤدي هذا إلى طباعة اسم كل دالة جافا سكريبت وشيفرتها المقابلة في وحدة التحكم. هذا مفيد للتحقق من الدوال الموجودة حاليًا في المستند.

## الخطوة 6: إزالة JavaScript من ملف PDF

الآن، لنفترض أنك تريد إزالة وظيفة JavaScript معينة، مثل `func1`. إليك كيفية القيام بذلك:

```csharp
doc1.JavaScript.Remove("func1");
Console.WriteLine("Key 'func1' removed ");
```

ال `Remove` تأخذ الطريقة اسم دالة JavaScript كحجة وتحذفها من المستند.

## الخطوة 7: التحقق من إزالة JavaScript

بعد إزالة JavaScript، يمكنك إعادة طباعة الوظائف المتبقية للتأكيد على ذلك `func1` تم حذفه بنجاح.

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
Console.WriteLine("Javascript added/removed successfully.");
```

يضمن هذا الجزء الأخير من الكود أن كل شيء في مكانه وأن وظائف JavaScript يتم تحديثها بشكل صحيح.

## خاتمة

تهانينا! لقد تعلمتَ للتو كيفية إضافة وحذف جافا سكريبت من مستند PDF باستخدام Aspose.PDF لـ .NET. يمكن استخدام هذه الميزة الفعّالة في مهام متنوعة، بدءًا من إضافة رسائل ديناميكية وصولًا إلى إجراء حسابات أو عمليات تحقق مخصصة. من خلال معالجة جافا سكريبت داخل ملف PDF، يمكنك تحسين تجربة المستخدم بشكل ملحوظ.

## الأسئلة الشائعة

### هل يمكنني إضافة وظائف JavaScript متعددة إلى ملف PDF واحد؟
بالتأكيد! يمكنك إضافة أي عدد من وظائف JavaScript حسب حاجتك باستخدام `doc.JavaScript` مجموعة.

### ماذا يحدث إذا حاولت إزالة وظيفة JavaScript غير موجودة؟
إذا لم تكن الوظيفة موجودة، `Remove` لن تؤدي الطريقة إلى حدوث خطأ، ولكنها أيضًا لن تزيل أي شيء.

### هل من الممكن تشغيل JavaScript بمجرد فتح ملف PDF؟
نعم! يمكنك تهيئة JavaScript للعمل عند تشغيل مُحفِّزات مُعيَّنة، مثل فتح مستند أو النقر على زر.

### هل يمكنني تعديل JavaScript بعد إضافته إلى ملف PDF؟
نعم، يمكنك تحميل ملف PDF موجود، والوصول إلى JavaScript الخاص به، وتعديل الكود، وحفظ المستند مرة أخرى.

### هل يؤثر إزالة JavaScript على بقية محتوى PDF؟
لا، إزالة جافا سكريبت تؤثر فقط على النص البرمجي، بينما يبقى محتوى ملف PDF دون تغيير.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}