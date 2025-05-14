---
"description": "تعلّم كيفية استخراج ومعالجة مواضع الصور في مستندات PDF باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة مع أمثلة ومقاطع برمجية."
"linktitle": "مواضع الصور"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "مواضع الصور"
"url": "/ar/net/programming-with-images/image-placements/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# مواضع الصور

## مقدمة

قد يكون التعامل مع الصور في ملفات PDF أمرًا صعبًا، ولكن مع Aspose.PDF لـ .NET، يمكنك بسهولة معالجة واستخراج خصائص الصورة دون عناء. سواء كنت ترغب في الحصول على أبعاد الصورة أو استخراجها أو استرجاع خصائص أخرى مثل الدقة، فإن Aspose.PDF يوفر لك الأدوات اللازمة. سيرشدك هذا البرنامج التعليمي خطوة بخطوة حول كيفية استخراج مواضع الصور في مستند PDF باستخدام Aspose.PDF لـ .NET. سنغطي كل شيء، من استيراد الحزم إلى استرجاع خصائص الصورة مثل العرض والارتفاع والدقة.

## المتطلبات الأساسية

قبل أن نبدأ بالشرح، هناك بعض الأمور التي يجب عليك توافرها. إليك قائمة مرجعية سريعة:

1. Aspose.PDF لـ .NET: تأكد من تثبيت مكتبة Aspose.PDF لـ .NET. يمكنك تنزيلها. [هنا](https://releases.aspose.com/pdf/net/).
2. بيئة التطوير: ستحتاج إلى تثبيت Visual Studio أو أي بيئة تطوير متكاملة أخرى تدعم .NET على جهازك.
3. مستند PDF: جهّز نموذجًا لمستند PDF يحتوي على صور. في هذا المثال، سنستخدم ملفًا باسم `ImagePlacement.pdf`.
4. المعرفة الأساسية بلغة C#: على الرغم من أن هذا الدليل مناسب للمبتدئين، فإن المعرفة الأساسية بلغة C# سوف تساعدك على فهم مقتطفات التعليمات البرمجية بشكل أفضل.

## استيراد الحزم

قبل الخوض في تفاصيل الكود، أول ما عليك فعله هو استيراد مساحات الأسماء اللازمة. هذه الحزم ضرورية للعمل مع مستندات PDF ومعالجة الصور في Aspose.PDF لـ .NET.

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Drawing;
```

تتيح لك هذه الحزم العمل مع ملفات PDF (`Aspose.Pdf`), التلاعب بمواضع الصور (`Aspose.Pdf.ImagePlacement`)، والتعامل مع تدفقات الصور والرسومات (`System.Drawing` و `System.IO`).

الآن بعد أن أصبح لدينا المتطلبات الأساسية والحزم في مكانها، دعنا نقوم بتقسيم كل جزء من البرنامج التعليمي إلى دليل بسيط وسهل المتابعة.

## الخطوة 1: تحميل مستند PDF

الخطوة الأولى هي تحميل ملف PDF إلى مشروعك. سيشكل هذا أساسًا للعمل مع الصور داخل ملف PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; 
Aspose.Pdf.Document doc = new Aspose.Pdf.Document(dataDir + "ImagePlacement.pdf");
```

في هذه الخطوة، نقوم بتحديد مسار ملف مستند PDF باستخدام `dataDir` ومن ثم إنشاء مثيل جديد من `Aspose.Pdf.Document` هذا يسمح لنا بتحميل ملف PDF إلى برنامجنا. الأمر بسيط، أليس كذلك؟ تمامًا كما لو كنا نفتح كتابًا لنبدأ القراءة، نحن الآن جاهزون لاستكشاف محتواه.

## الخطوة 2: تهيئة ممتص وضع الصورة

لاستخراج الصور، نحتاج إلى ما يُسمى "مُمتصّ وضع الصور". تخيّلوه كأداة تستوعب جميع معلومات الصورة على صفحة مُحدّدة.

```csharp
ImagePlacementAbsorber abs = new ImagePlacementAbsorber();
```

هنا، نقوم بإنشاء مثيل لـ `ImagePlacementAbsorber`سيجمع هذا الكائن ويخزن معلومات حول جميع مواضع الصور على صفحة PDF محددة. تخيل الأمر كما لو أنك تمسح صفحةً بعدسة مكبرة وتتعرف على جميع الصور فيها!

## الخطوة 3: قبول الامتصاص في الصفحة الأولى

بعد ذلك، علينا تحديد صفحة PDF التي يجب مسحها ضوئيًا. في هذا المثال، سنركز على الصفحة الأولى.

```csharp
doc.Pages[1].Accept(abs);
```

ال `Accept` تقوم الطريقة بمسح الصفحة الأولى من مستند PDF بحثًا عن أي صور وتخزين النتائج داخل `ImagePlacementAbsorber`إنه مثل إخبار العدسة المكبرة بمكان البحث عن الصور.

## الخطوة 4: تكرار كل موضع للصورة

الآن بعد أن قمنا بمسح الصفحة، نحتاج إلى المرور على كل صورة موجودة في الصفحة واسترجاع خصائصها.

```csharp
foreach (ImagePlacement imagePlacement in abs.ImagePlacements)
{
    Console.Out.WriteLine("image width:" + imagePlacement.Rectangle.Width);
    Console.Out.WriteLine("image height:" + imagePlacement.Rectangle.Height);
    Console.Out.WriteLine("image LLX:" + imagePlacement.Rectangle.LLX);
    Console.Out.WriteLine("image LLY:" + imagePlacement.Rectangle.LLY);
    Console.Out.WriteLine("image horizontal resolution:" + imagePlacement.Resolution.X);
    Console.Out.WriteLine("image vertical resolution:" + imagePlacement.Resolution.Y);
}
```

تمر هذه الحلقة عبر كل صورة موجودة في الصفحة. نقوم بطباعة العرض، والارتفاع، وإحداثيات x السفلية اليسرى (LLX)، وy السفلية اليسرى (LLY)، ودقة الصورة (أفقيًا ورأسيًا). تساعدك هذه التفاصيل على فهم حجم كل صورة وموقعها داخل ملف PDF.

## الخطوة 5: استخراج الصورة ذات الأبعاد المرئية

بعد جمع معلومات الصور، قد ترغب في استخراج الصورة الأصلية مع أبعادها. إليك كيفية القيام بذلك.

```csharp
Bitmap scaledImage;
using (MemoryStream imageStream = new MemoryStream())
{
    imagePlacement.Image.Save(imageStream, System.Drawing.Imaging.ImageFormat.Png);
    Bitmap resourceImage = (Bitmap)Bitmap.FromStream(imageStream);
    scaledImage = new Bitmap(resourceImage, (int)imagePlacement.Rectangle.Width, (int)imagePlacement.Rectangle.Height);
}
```

يقوم مقتطف التعليمات البرمجية هذا باسترجاع الصورة من ملف PDF ويقوم بقياسها إلى أبعادها الفعلية كما هو محدد في `ImagePlacement` بحفظ الصورة في مجرى ذاكرة وتغيير حجمها، تضمن أن الصورة التي تستخرجها تحافظ على الحجم الدقيق الذي عُرضت به في ملف PDF.

## خاتمة

استخراج مواضع الصور من مستند PDF باستخدام Aspose.PDF لـ .NET سهلٌ للغاية بمجرد شرحه خطوة بخطوة. لقد غطينا كل شيء، بدءًا من تحميل ملف PDF وصولًا إلى استرجاع خصائص الصورة واستخراجها بأبعادها الفعلية. يُسهّل Aspose.PDF العمل مع ملفات PDF ومعالجة محتواها بشكل كبير، مما يتيح لك العمل بكفاءة مع الصور والنصوص وغيرها الكثير.

## الأسئلة الشائعة

### هل يمكنني استخراج الصور من صفحة معينة من ملف PDF؟  
نعم، عن طريق تحديد رقم الصفحة عند استخدام `Accept` بهذه الطريقة، يمكنك التركيز على أي صفحة معينة.

### ما هي تنسيقات الصور المدعومة للاستخراج؟  
يدعم Aspose.PDF تنسيقات مختلفة، بما في ذلك PNG وJPEG وBMP والمزيد.

### هل من الممكن التلاعب بالصورة المستخرجة؟  
بالتأكيد! بمجرد استخراجه، يمكنك استخدامه `System.Drawing` مساحة اسمية للتلاعب بالصورة.

### هل يمكنني استخراج الصور من ملفات PDF المحمية بكلمة مرور؟  
نعم، يمكنك القيام بذلك، ولكنك ستحتاج إلى إلغاء قفل ملف PDF باستخدام بيانات الاعتماد المناسبة قبل استخراج الصور.

### هل يعمل Aspose.PDF لـ .NET على كافة أطر عمل .NET؟  
نعم، فهو يدعم .NET Framework، و.NET Core، و.NET 5 وما فوق.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}