---
"description": "تعلم كيفية استخراج معلومات الصورة من ملفات PDF باستخدام Aspose.PDF لـ .NET من خلال دليلنا الشامل خطوة بخطوة."
"linktitle": "معلومات الصورة في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "معلومات الصورة في ملف PDF"
"url": "/ar/net/programming-with-images/image-information/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# معلومات الصورة في ملف PDF

## مقدمة

ملفات PDF منتشرة في كل مكان هذه الأيام، فكل مستند تقريبًا سواءً كان مهنيًا أو شخصيًا يُحوّل إلى هذا التنسيق في مرحلة ما. سواءً أكان تقريرًا أم كتيبًا أم كتابًا إلكترونيًا، فإن فهم كيفية التعامل مع هذه الملفات برمجيًا يوفر إمكانيات لا حصر لها. ومن المتطلبات الشائعة استخراج معلومات الصور من ملفات PDF. في هذا الدليل، سنتناول بالتفصيل كيفية استخدام مكتبة Aspose.PDF لـ .NET لاستخراج تفاصيل مهمة حول الصور المُضمّنة في مستند PDF.

## المتطلبات الأساسية

قبل أن ننتقل إلى التفاصيل الدقيقة للترميز، هناك بعض المتطلبات الأساسية التي ستحتاج إلى توافرها:

1. بيئة التطوير: ستحتاج إلى بيئة تطوير .NET مُعدّة. قد تكون Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة مع .NET.
2. مكتبة Aspose.PDF: تأكد من إمكانية الوصول إلى مكتبة Aspose.PDF. يمكنك تنزيلها من [موقع Aspose](https://releases.aspose.com/pdf/net/). 
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة بلغة C# ومفاهيم البرمجة الموجهة للكائنات على متابعة البرنامج التعليمي بسهولة.
4. مستند PDF: احتفظ بمستند PDF نموذجي في متناول يدك يحتوي على صور لاختبار الكود الخاص بك. 

## استيراد الحزم

للبدء باستخدام مكتبة Aspose.PDF، ستحتاج إلى استيراد مساحات الأسماء اللازمة إلى ملف C#. إليك شرح موجز:

```csharp
using System.IO;
using Aspose.Pdf;
using System;
```

ستوفر لك هذه المساحات الاسمية إمكانية الوصول إلى الفئات والطرق المطلوبة لمعالجة ملفات PDF واستخراج بيانات الصور.

بعد أن انتهيت من إعداد كل شيء، حان الوقت لتقسيمه إلى خطوات سهلة. سنكتب برنامجًا بلغة C# يُحمّل مستند PDF، ويفحص كل صفحة، ويستخرج أبعاد ودقة كل صورة فيه.

## الخطوة 1: تهيئة المستند

في هذه الخطوة، سنقوم بتهيئة مستند PDF باستخدام مسار ملف PDF الخاص بك. يجب استبدال `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي يوجد به ملف PDF الخاص بك.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// تحميل ملف PDF المصدر
Document doc = new Document(dataDir + "ImageInformation.pdf");
```
نحن ننشئ `Document` كائن يُحمّل ملف PDF من الدليل المُحدد. هذا سيسمح لنا بالتعامل مع محتويات الملف.

## الخطوة 2: تعيين الدقة الافتراضية وتهيئة هياكل البيانات

بعد ذلك، نحدد دقة افتراضية للصور، وهو أمر مفيد للحسابات. سنُعدّ أيضًا مصفوفة لحفظ أسماء الصور، ومكدسًا لإدارة الحالات الرسومية.

```csharp
// تحديد الدقة الافتراضية للصورة
int defaultResolution = 72;
System.Collections.Stack graphicsState = new System.Collections.Stack();
// قم بتعريف كائن قائمة المصفوفة الذي سيحمل أسماء الصور
System.Collections.ArrayList imageNames = new System.Collections.ArrayList(doc.Pages[1].Resources.Images.Names);
```
ال `defaultResolution` يساعدنا المتغير في حساب دقة الصور بشكل صحيح. `graphicsState` تُستخدم المكدس كوسيلة لتخزين الحالة الرسومية الحالية للمستند عندما نواجه مشغلي التحويل.

## الخطوة 3: معالجة كل عامل على الصفحة

نمر الآن على جميع العمليات في الصفحة الأولى من المستند. هنا تبدأ المهمة. 

```csharp
foreach (Operator op in doc.Pages[1].Contents)
{
    // مشغلي العملية...
}
```
كل عامل في ملف PDF هو أمر يخبر المعالج بكيفية إدارة العناصر الرسومية، بما في ذلك الصور.

## الخطوة 4: التعامل مع مشغلي GSave/GRestore

داخل الحلقة، سوف نقوم بمعالجة أوامر حفظ الرسومات واستعادتها لتتبع التغييرات التي تم إجراؤها على الحالة الرسومية.

```csharp
if (opSaveState != null) 
{
    // حفظ الحالة السابقة
    graphicsState.Push(((Matrix)graphicsState.Peek()).Clone());
} 
else if (opRestoreState != null) 
{
    // استعادة الحالة السابقة
    graphicsState.Pop();
}
```
`GSave` يحفظ الحالة الرسومية الحالية، بينما `GRestore` يستعيد الحالة المحفوظة الأخيرة، مما يسمح لنا بعكس أي تحويلات عند معالجة الصور.

## الخطوة 5: إدارة مصفوفات التحويل

بعد ذلك، نقوم بمعالجة سلسلة مصفوفات التحويل عند تطبيق التحويلات على الصور.

```csharp
else if (opCtm != null) 
{
    Matrix cm = new Matrix(
        (float)opCtm.Matrix.A,
        (float)opCtm.Matrix.B,
        (float)opCtm.Matrix.C,
        (float)opCtm.Matrix.D,
        (float)opCtm.Matrix.E,
        (float)opCtm.Matrix.F);
    
    ((Matrix)graphicsState.Peek()).Multiply(cm);
    continue;
}
```
عندما يتم تطبيق مصفوفة التحويل، نقوم بضربها بالمصفوفة الحالية المخزنة في حالة الرسومات حتى نتمكن من متابعة أي تغيير في القياس أو الترجمة يتم تطبيقه على الصورة.

## الخطوة 6: استخراج معلومات الصورة

وأخيرًا، نقوم بمعالجة عامل الرسم للصور واستخراج المعلومات الضرورية، مثل الأبعاد والدقة.

```csharp
else if (opDo != null) 
{
    // عامل التشغيل Do الذي يرسم الكائنات
    if (imageNames.Contains(opDo.Name)) 
    {
        Matrix lastCTM = (Matrix)graphicsState.Peek();
        XImage image = doc.Pages[1].Resources.Images[opDo.Name];
        double scaledWidth = Math.Sqrt(Math.Pow(lastCTM.Elements[0], 2) + Math.Pow(lastCTM.Elements[1], 2));
        double scaledHeight = Math.Sqrt(Math.Pow(lastCTM.Elements[2], 2) + Math.Pow(lastCTM.Elements[3], 2));
        double originalWidth = image.Width;
        double originalHeight = image.Height;
        
        double resHorizontal = originalWidth * defaultResolution / scaledWidth;
        double resVertical = originalHeight * defaultResolution / scaledHeight;
        
        // إخراج المعلومات
        Console.Out.WriteLine(string.Format(dataDir + "image {0} ({1:.##}:{2:.##}): res {3:.##} x {4:.##}",
                         opDo.Name, scaledWidth, scaledHeight, resHorizontal, resVertical));
    }
}
```
هنا، نتحقق مما إذا كان المُشغِّل مسؤولاً عن رسم الصورة. إذا كان كذلك، نحصل على كائن XImage المُقابل، ونحسب أبعاده المُقاسة ودقته، ونطبع المعلومات اللازمة.

## خاتمة

تهانينا! لقد أنشأتَ للتو مثالاً عمليًا لكيفية استخراج معلومات الصورة من ملف PDF باستخدام Aspose.PDF لـ .NET. هذه الإمكانية مفيدة للغاية للمطورين الذين يحتاجون إلى تحليل أو معالجة مستندات PDF لتطبيقات مختلفة، مثل إعداد التقارير، واستخراج البيانات، أو حتى برامج عرض PDF مخصصة. 


## الأسئلة الشائعة

### ما هي مكتبة Aspose.PDF؟
تُعد مكتبة Aspose.PDF أداة قوية لإنشاء ملفات PDF ومعالجتها وتحويلها في تطبيقات .NET.

### هل يمكنني استخدام المكتبة مجانًا؟
نعم، يُقدّم Aspose نسخة تجريبية مجانية. يُمكنك تنزيلها. [هنا](https://releases.aspose.com/).

### ما هي أنواع تنسيقات الصور التي يمكن استخراجها؟
تدعم المكتبة تنسيقات الصور المختلفة، بما في ذلك JPEG وPNG وTIFF، طالما أنها مضمنة في ملف PDF.

### هل يتم استخدام Aspose لأغراض تجارية؟
نعم، يمكنك استخدام منتجات Aspose تجاريًا. للحصول على الترخيص، تفضل بزيارة [صفحة الشراء](https://purchase.aspose.com/buy).

### كيف أحصل على الدعم لـ Aspose؟
يمكنك الوصول إلى منتدى الدعم [هنا](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}