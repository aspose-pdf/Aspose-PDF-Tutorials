---
"description": "تعلّم كيفية استخراج الصور من ملفات PDF بسهولة باستخدام Aspose.PDF لـ .NET. اتبع هذا الدليل خطوة بخطوة لتحسين مهاراتك في معالجة ملفات PDF."
"linktitle": "البحث والحصول على الصور في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "البحث والحصول على الصور في ملف PDF"
"url": "/ar/net/programming-with-images/search-and-get-images/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# البحث والحصول على الصور في ملف PDF

## مقدمة

هل تبحث عن طريقة سهلة لاستخراج الصور من ملفات PDF باستخدام Aspose.PDF لـ .NET؟ أنت في المكان المناسب! في هذه المقالة، سنتناول بالتفصيل كيفية البحث عن الصور المضمنة في مستند PDF واسترجاعها بفعالية. سواء كنت مطورًا محترفًا أو مبتدئًا في التعامل مع ملفات PDF، سيرشدك هذا الدليل خلال العملية بأكملها خطوة بخطوة.

## المتطلبات الأساسية

قبل أن ننتقل إلى التفاصيل الدقيقة للكود، هناك بعض المتطلبات الأساسية التي يجب عليك التحقق منها من قائمتك. 

### إطار عمل .NET

تأكد من تثبيت .NET Framework على جهازك. Aspose.PDF لـ .NET متوافق مع إصدارات مختلفة، ولكن يُفضل استخدام أحدث إصدار مستقر للاستفادة من جميع الميزات والتحسينات الحديثة.

### مكتبة Aspose.PDF

ستحتاج إلى الوصول إلى مكتبة Aspose.PDF. إذا لم تكن قد فعلت ذلك بعد، يمكنك تنزيلها من هذا الرابط: [تنزيل Aspose.PDF لـ .NET](https://releases.aspose.com/pdf/net/)بالإضافة إلى ذلك، يمكنك استكشاف [تجربة مجانية لمدة شهر واحد](https://releases.aspose.com/) لبدء مشاريعك دون أي تكلفة.

### بيئة التطوير

يجب إعداد بيئة تطوير مناسبة مثل Visual Studio أو أي بيئة تطوير متكاملة تفضلها لكتابة التعليمات البرمجية وتشغيلها بسلاسة.

## استيراد الحزم

للعمل مع Aspose.PDF لـ .NET، ستحتاج أولًا إلى استيراد مساحات الأسماء المناسبة إلى مشروعك. إليك ما عليك فعله:

```csharp
using System.IO;
using Aspose.Pdf;
using System;
```

تخدم كل من هذه الحزم أغراضًا محددة عند معالجة مستندات PDF. `Aspose.Pdf` مساحة الاسم هي حجر الأساس لعملياتك، بينما يساعد الاثنان الآخران في التعامل مع الصور والنصوص داخل ملف PDF.

## الخطوة 1: تعيين مسار المستند الخاص بك

قبل أي شيء، عليك تحديد مسار ملف PDF. هذا الكود يُحدد ذلك:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

استبدل "دليل المستندات الخاص بك" بالمسار الفعلي للدليل الذي يحتوي على ملف PDF الخاص بك، على سبيل المثال، `C:\Documents\`.

## الخطوة 2: افتح مستند PDF

بعد ذلك، ستحتاج إلى تحميل مستند PDF إلى تطبيقك. يتم ذلك عن طريق إنشاء ملف جديد `Document` المثيل مع مسار الملف الذي حددته للتو:

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document(dataDir + "SearchAndGetImages.pdf");
```

## الخطوة 3: إنشاء ImagePlacementAbsorber

للبحث عن الصور داخل ملف PDF، تحتاج إلى `ImagePlacementAbsorber` يساعد هذا الفصل على استخراج الصور من ملف PDF أثناء عملية الاستخراج:

```csharp
ImagePlacementAbsorber abs = new ImagePlacementAbsorber();
```

## الخطوة 4: قبول الامتصاص لجميع الصفحات

هذه الخطوة مهمة لأنها تخبرك `Document` لتطبيق مُمتص الصور على جميع الصفحات. يضمن ذلك تحديد أي صور موجودة في أي مكان داخل المستند.

```csharp
doc.Pages.Accept(abs);
```

## الخطوة 5: تكرار مواضع الصور

بعد أن استوعبت الصور، حان وقت التعمق فيها. ستستعرض كل موضع صورة مستخرجة من ملف PDF:

```csharp
foreach (ImagePlacement imagePlacement in abs.ImagePlacements)
{
    // خطوات أخرى للحصول على خصائص الصورة
}
```

## الخطوة 6: استخراج خصائص الصورة

داخل الحلقة، يمكنك البدء في استرجاع خصائص قيّمة لكل صورة. باستخدام `imagePlacement` الكائن، يمكنك الوصول إلى الأبعاد والدقة:

```csharp
XImage image = imagePlacement.Image; // احصل على الصورة

Console.Out.WriteLine("image width:" + imagePlacement.Rectangle.Width);
Console.Out.WriteLine("image height:" + imagePlacement.Rectangle.Height);
Console.Out.WriteLine("image LLX:" + imagePlacement.Rectangle.LLX);
Console.Out.WriteLine("image LLY:" + imagePlacement.Rectangle.LLY);
Console.Out.WriteLine("image horizontal resolution:" + imagePlacement.Resolution.X);
Console.Out.WriteLine("image vertical resolution:" + imagePlacement.Resolution.Y);
```

## خاتمة

وهذا كل ما في الأمر! باتباع هذه الخطوات، يمكنك البحث عن الصور واسترجاعها بكفاءة من ملفات PDF باستخدام Aspose.PDF لـ .NET. ببضعة أسطر برمجية فقط، يمكنك استخراج صور قيّمة وخصائصها، مما يفتح آفاقًا واسعة لتطبيقك.

## الأسئلة الشائعة

### هل استخدام مكتبة Aspose.PDF مجاني؟  
Aspose.PDF for .NET هي مكتبة مدفوعة الأجر، ولكن يمكنك تنزيل نسخة تجريبية مجانية لمدة شهر واحد.

### هل يمكنني استخراج الصور من ملفات PDF المحمية بكلمة مرور؟  
نعم، ولكن يتعين عليك تقديم كلمة المرور أثناء فتح المستند.

### ما هي أنواع الصور التي يمكن استخراجها من ملف PDF؟  
يمكن استخراج جميع الصور المضمنة بغض النظر عن التنسيق (JPEG، PNG، وما إلى ذلك).

### هل هناك حد لعدد الصور التي يمكنني استخراجها؟  
لا يوجد حد أقصى، فهو يعتمد على ملف PDF نفسه.

### هل يمكنني حفظ الصور المستخرجة على القرص؟  
نعم، يمكنك حفظ الصور على القرص باستخدام `XImage` الكائن في الكود الخاص بك.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}