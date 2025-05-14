---
"description": "تعلّم كيفية استخراج حدود ملف PDF وحفظها كصورة باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة مع نماذج برمجية ونصائح للنجاح."
"linktitle": "استخراج الحدود في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "استخراج الحدود في ملف PDF"
"url": "/ar/net/programming-with-tables/extract-border/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# استخراج الحدود في ملف PDF

## مقدمة

عند العمل مع ملفات PDF، قد يبدو استخراج عناصر محددة، مثل الحدود أو المسارات الرسومية، مهمة شاقة. ولكن مع Aspose.PDF لـ .NET، يمكنك بسهولة استخراج الحدود أو الأشكال من ملف PDF وحفظها كصورة. في هذا البرنامج التعليمي، سنتعمق في عملية استخراج حدود من ملف PDF وحفظه كصورة PNG. استعد للتحكم في المحتوى الرسومي لملف PDF الخاص بك!

## المتطلبات الأساسية

قبل أن نتعمق في الكود، تأكد من إعداد كل شيء:

1. Aspose.PDF لـ .NET: إذا لم تقم بتثبيت مكتبة Aspose.PDF بعد، فيمكنك [قم بتحميله هنا](https://releases.aspose.com/pdf/net/). سيتعين عليك أيضًا تطبيق الترخيص، إما من خلال النسخة التجريبية المجانية أو شراء ترخيص.
2. إعداد بيئة التطوير المتكاملة: أنشئ مشروع C# في Visual Studio أو أي بيئة تطوير متكاملة أخرى لـ .NET. تأكد من إضافة المراجع اللازمة إلى مكتبة Aspose.PDF.
3. ملف PDF مُدخل: جهّز ملف PDF لاستخراج الحدود منه. سيشير هذا البرنامج التعليمي إلى ملف باسم `input.pdf`.

## استيراد الحزم المطلوبة

لنبدأ باستيراد مساحات الأسماء المطلوبة. توفر هذه الحزم الأدوات اللازمة للتعامل مع محتوى PDF.

```csharp
using System.IO;
using System;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;
using System.Collections;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
```

الآن بعد أن قمنا بتغطية الأساسيات، دعنا ننتقل إلى الدليل خطوة بخطوة حيث سنقوم بتقسيم كل جزء من الكود لشرحه بالتفصيل.


## الخطوة 1: تحميل مستند PDF

الخطوة الأولى هي تحميل ملف PDF الذي يحتوي على الإطار الذي تريد استخراجه. تخيل الأمر كما لو كنت تفتح كتابًا قبل البدء بقراءته - فأنت بحاجة إلى الوصول إلى محتواه!

سنبدأ بتحديد الدليل الذي سيتم تخزين ملف PDF الخاص بك فيه وتحميل المستند باستخدام `Aspose.Pdf.Document` فصل.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

يقوم هذا الكود بتحميل `input.pdf` الملف من الدليل المحدد. تأكد من صحة مسار الملف، وإلا فقد تظهر رسالة خطأ "لم يتم العثور على الملف".

## الخطوة 2: إعداد الرسومات والخرائط النقطية

قبل البدء بالاستخراج، نحتاج إلى إنشاء لوحة رسم للرسم عليها. في عالم .NET، يعني هذا إعداد كائنات Bitmap وGraphics. تُمثل Bitmap الصورة، بينما يُتيح لنا كائن Graphics رسم أشكال، مثل الحدود، مُستخرجة من ملف PDF.

```csharp
System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap((int)doc.Pages[1].PageInfo.Width, (int)doc.Pages[1].PageInfo.Height);
System.Drawing.Drawing2D.GraphicsPath graphicsPath = new System.Drawing.Drawing2D.GraphicsPath();
System.Drawing.Drawing2D.Matrix lastCTM = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, 0);
System.Drawing.Drawing2D.Matrix inversionMatrix = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, (float)doc.Pages[1].PageInfo.Height);
System.Drawing.PointF lastPoint = new System.Drawing.PointF(0, 0);
System.Drawing.Color fillColor = System.Drawing.Color.FromArgb(0, 0, 0);
System.Drawing.Color strokeColor = System.Drawing.Color.FromArgb(0, 0, 0);
```

فيما يلي تفصيل لذلك:
- نقوم بإنشاء صورة نقطية بحجم الصفحة الأولى من ملف PDF.
- يتم استخدام GraphicsPath لتحديد الأشكال (في هذه الحالة، الحدود).
- تعرف المصفوفة كيفية تحويل الرسومات؛ نحن بحاجة إلى مصفوفة عكسية لأن PDF و.NET لديهما أنظمة إحداثيات مختلفة.

## الخطوة 3: معالجة محتويات PDF


ملف PDF عبارة عن سلسلة من أوامر الرسم، ونحن بحاجة إلى معالجة كل من هذه الأوامر لتحديد معلومات الحدود واستخراجها.

```csharp
foreach (Operator op in doc.Pages[1].Contents)
{
    // معالجة الأوامر مثل حفظ/استعادة الحالة، رسم الخطوط، ملء الأشكال، وما إلى ذلك.
}
```

يتكرر الكود عبر كل مُعامل رسم في مجرى محتوى ملف PDF. قد يُمثل كل مُعامل خطًا أو مستطيلًا أو أي تعليمة رسومية أخرى.

## الخطوة 4: التعامل مع مشغلات PDF

يتحكم كل مُشغِّل في ملف PDF في إجراء. لاستخراج الحدود، نحتاج إلى تحديد أوامر مثل "نقل إلى"، و"خط إلى"، و"رسم مستطيل". تُدير المُشغِّلات التالية هذه الإجراءات:

- MoveTo: يحرك المؤشر إلى نقطة البداية.
- LineTo: يرسم خطًا من النقطة الحالية إلى نقطة جديدة.
- رد: رسم مستطيل (يمكن أن يكون جزءًا من الحدود).

```csharp
Aspose.Pdf.Operators.MoveTo opMoveTo = op as Aspose.Pdf.Operators.MoveTo;
Aspose.Pdf.Operators.LineTo opLineTo = op as Aspose.Pdf.Operators.LineTo;
Aspose.Pdf.Operators.Re opRe = op as Aspose.Pdf.Operators.Re;

if (opMoveTo != null)
{
    lastPoint = new System.Drawing.PointF((float)opMoveTo.X, (float)opMoveTo.Y);
}
else if (opLineTo != null)
{
    System.Drawing.PointF linePoint = new System.Drawing.PointF((float)opLineTo.X, (float)opLineTo.Y);
    graphicsPath.AddLine(lastPoint, linePoint);
    lastPoint = linePoint;
}
else if (opRe != null)
{
    System.Drawing.RectangleF re = new System.Drawing.RectangleF((float)opRe.X, (float)opRe.Y, (float)opRe.Width, (float)opRe.Height);
    graphicsPath.AddRectangle(re);
}
```

في هذه الخطوة:
- نقوم بالتقاط النقاط لكل خط أو شكل مرسوم.
- للمستطيلات (`opRe`), نضيفها مباشرة إلى `graphicsPath`، والتي سنستخدمها لاحقًا لرسم الحدود.

## الخطوة 5: رسم الحدود

بعد تحديد الخطوط والمستطيلات التي تُشكّل الحدود، علينا رسمها على كائن Bitmap. وهنا يأتي دور كائن Graphics.

```csharp
using (System.Drawing.Graphics gr = System.Drawing.Graphics.FromImage(bitmap))
{
    gr.SmoothingMode = SmoothingMode.HighQuality;
    gr.DrawPath(new System.Drawing.Pen(strokeColor), graphicsPath);
}
```

- نقوم بإنشاء كائن رسومي بناءً على الخريطة النقطية.
- SmoothingMode.HighQuality يضمن حصولنا على صورة ناعمة وجميلة.
- وأخيرًا، نستخدم DrawPath لرسم الحدود.

## الخطوة 6: حفظ الحدود المستخرجة

بعد استخراج الحدود، حان وقت حفظها كملف صورة. سيؤدي هذا إلى حفظ الحدود بصيغة PNG.

```csharp
dataDir = dataDir + "ExtractBorder_out.png";
bitmap.Save(dataDir, ImageFormat.Png);
```

- يتم حفظ الخريطة النقطية كصورة PNG.
- يمكنك الآن فتح هذه الصورة لعرض الحدود المستخرجة.

## خاتمة

قد يبدو استخراج الحدود من ملف PDF باستخدام Aspose.PDF لـ .NET أمرًا صعبًا في البداية، ولكن بمجرد فهمه، يصبح الأمر سهلًا. بفهم عوامل الرسم في ملف PDF واستخدام مكتبات .NET القوية، يمكنك معالجة واستخراج المحتوى الرسومي بكفاءة. يمنحك هذا الدليل أساسًا متينًا للبدء في معالجة ملفات PDF!

## الأسئلة الشائعة

### كيف أتعامل مع صفحات متعددة في ملف PDF؟  
يمكنك التنقل عبر كل صفحة في المستند عن طريق التكرار `doc.Pages` بدلا من الترميز الثابت `doc.Pages[1]`.

### هل يمكنني استخراج عناصر أخرى، مثل النص، باستخدام نفس النهج؟  
نعم، يوفر Aspose.PDF واجهات برمجة تطبيقات غنية لاستخراج النصوص والصور والمحتويات الأخرى من ملفات PDF.

### كيف يمكنني التقدم بطلب الترخيص لتجنب القيود؟  
أنت تستطيع [التقدم بطلب للحصول على ترخيص](https://purchase.aspose.com/temporary-license/) عن طريق تحميله من خلال `License` الفئة المقدمة من قبل Aspose.

### ماذا لو كان ملف PDF الخاص بي لا يحتوي على حدود؟  
إذا لم يكن ملف PDF يحتوي على حدود مرئية، فقد لا تُسفر عملية استخراج الرسومات عن أي نتيجة. تأكد من أن محتوى ملف PDF يتضمن حدودًا قابلة للرسم.

### هل يمكنني حفظ الإخراج بتنسيقات أخرى غير PNG؟  
نعم، قم بتغيير فقط `ImageFormat.Png` إلى تنسيق آخر مدعوم مثل `ImageFormat.Jpeg`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}