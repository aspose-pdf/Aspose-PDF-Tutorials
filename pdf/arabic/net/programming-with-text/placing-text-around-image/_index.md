---
"description": "تعرّف على كيفية إضافة نص حول الصور في ملفات PDF باستخدام Aspose.PDF لـ .NET. اتبع دليلنا خطوة بخطوة لإنشاء ملفات PDF احترافية تحتوي على صور ونصوص جنبًا إلى جنب."
"linktitle": "وضع نص حول الصورة في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "وضع نص حول الصورة في ملف PDF"
"url": "/ar/net/programming-with-text/placing-text-around-image/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# وضع نص حول الصورة في ملف PDF

## مقدمة

هل سبق لك أن حاولت وضع نص حول صورة في ملف PDF ولكن واجهت صعوبة؟ إذا كان الأمر كذلك، فأنت في المكان المناسب! يُسهّل Aspose.PDF for .NET هذه العملية، حيث يسمح لك بوضع نص بجانب الصور ببضعة أسطر برمجية فقط. سواء كنت تُنشئ تقارير أو مستندات أو عروضًا تقديمية، تُعد هذه الميزة طريقة رائعة لتحسين تصميم محتواك وجعله أكثر جاذبية بصريًا. سنشرح اليوم كيفية استخدام Aspose.PDF for .NET لوضع نص حول الصور في مستند PDF.

## المتطلبات الأساسية

قبل أن نبدأ في شرح الكود، لنتأكد من إعداد كل شيء. إليك ما ستحتاجه:

- Aspose.PDF لـ .NET: يمكنك تنزيله من [هنا](https://releases.aspose.com/pdf/net/).
- Visual Studio: تأكد من تثبيت الإصدار الأحدث لمتابعة العمل بسلاسة.
- .NET Framework: يستخدم هذا المثال .NET، لذا تأكد من إعداد البيئة الخاصة بك لتطوير .NET.
- ترخيص مؤقت: يمكنك طلب ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/) إذا كنت تقوم بتقييم المنتج.

إذا لم تقم بإعداد Aspose.PDF لـ .NET بعد، فاتبع تعليمات التثبيت الموجودة في [التوثيق](https://reference.aspose.com/pdf/net/).

## استيراد مساحات الأسماء

قبل البدء بالبرمجة، علينا استيراد مساحات الأسماء اللازمة. إليك مقتطف الكود للقيام بذلك:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

هذه المساحات الأساسية ضرورية لأنها توفر الوصول إلى فئات مثل `Document`، `Page`، `Image`، و `HtmlFragment`، والذي سنستخدمه لإنشاء ملف PDF ومعالجته.

بعد أن هيأنا المشهد، لنشرح بالتفصيل كيفية وضع نص حول صورة في ملف PDF باستخدام Aspose.PDF لـ .NET. سنشرح ذلك خطوة بخطوة.

## الخطوة 1: إنشاء كائن المستند

أولاً، عليك إنشاء مستند PDF. في Aspose.PDF، يتم ذلك عن طريق إنشاء مثيل لـ `Document` هذا الكائن سيكون بمثابة الأساس لجميع المحتوى الذي سنضيفه.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

هنا، أنشأنا مستند PDF فارغًا. لا يحتوي على أي صفحات بعد، ولكن لا تقلق، سنضيف صفحة في الخطوة التالية.

## الخطوة 2: إضافة صفحة إلى المستند

الآن وقد حصلنا على مستندنا، حان وقت إضافة صفحة. تخيل هذا كأنك تنشئ صفحة فارغة لإضافة محتواك.

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

يضيف هذا الكود صفحة جديدة إلى المستند. الصفحة فارغة افتراضيًا، لكننا سنغير ذلك قريبًا.

## الخطوة 3: إنشاء جدول لتنظيم المحتوى

للحفاظ على محاذاة الصورة والنص بشكل صحيح، سنستخدم جدولًا. تساعد الجداول في ملفات PDF على تنظيم تخطيطك، تمامًا كما هو الحال في مستندات Word أو HTML.

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
page.Paragraphs.Add(table1);
```

يُنشئ هذا المقطع جدولاً ويضيفه إلى الصفحة. تخيّل الجدول كإطار لمحاذاة صورتك ونصك.

## الخطوة 4: تعيين عرض الأعمدة للجدول

بعد إضافة الجدول، علينا تحديد عرض الأعمدة. هذا يضمن أن يكون حجم الصورة والنص مناسبًا للصفحة.

```csharp
table1.ColumnWidths = "120 270";
```

يُحدد هذا السطر عرض عمودين، أحدهما للصورة والآخر للنص. عدّل هذه القيم إذا كانت الصورة أو النص بحاجة إلى مساحة أكبر أو أقل.

## الخطوة 5: تحديد الهوامش والحشو

للتأكد من أن كل شيء يبدو أنيقًا، دعنا نضيف بعض الهوامش والحشو إلى الجدول.

```csharp
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;
table1.DefaultCellPadding = margin;
```

تضمن هذه الإعدادات أن يكون الجدول الخاص بك متباعدًا بشكل متسق، مما يجعل المحتوى جذابًا بصريًا.

## الخطوة 6: إدراج صورة في الجدول

الآن، لننتقل إلى الجزء الممتع: إضافة صورة. في هذه الحالة، سنضيف شعار Aspose، ولكن لا تتردد في استخدام أي صورة تُريدها.

```csharp
Aspose.Pdf.Row row1 = table1.Rows.Add();
Aspose.Pdf.Image logo = new Aspose.Pdf.Image();
logo.File = dataDir + "aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;
row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```

وإليك ما يحدث:
- نقوم بتحميل الصورة من الدليل المحدد.
- قمنا بتحديد ارتفاع وعرض الصورة.
- وأخيرًا، نضيف الصورة إلى الخلية الأولى في الجدول.

## الخطوة 7: إضافة نص بجوار الصورة

الآن وقد أصبحت الصورة جاهزة، لنُضِف نصًا بجانبها. في هذا المثال، سنستخدم نصًا بتنسيق HTML لتنسيق المحتوى.

```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component that enables .NET applications to <b>create PDF documents from scratch</b> without utilizing Adobe Acrobat.</font>";

Aspose.Pdf.HtmlFragment TitleText = new Aspose.Pdf.HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);
```

تضيف هذه الكتلة عنوانًا ووصفًا مُصممين في الخلية المجاورة للصورة. يمكنك تنسيق النص باستخدام وسوم HTML لمزيد من التخصيص.

## الخطوة 8: ضبط المحاذاة الرأسية

افتراضيًا، قد لا يكون محتوى خلايا الجدول محاذيًا بالشكل المطلوب. في هذه الحالة، نريد التأكد من محاذاة النص مع أعلى الخلية.

```csharp
row1.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
```

ويضمن هذا أن يكون النص في أعلى الخلية، مما يحافظ على التصميم نظيفًا واحترافيًا.

## الخطوة 9: إضافة المزيد من النص أسفل الصورة والوصف

قد ترغب في إضافة محتوى إضافي أسفل الصورة والنص. لنُضيف صفًا آخر إلى الجدول لهذا الغرض.

```csharp
Aspose.Pdf.Row SecondRow = table1.Rows.Add();
SecondRow.Cells.Add();
SecondRow.Cells[0].ColSpan = 2;
SecondRow.Cells[0].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;

string SecondRowString = "<font face=\"Arial\" size=2>Aspose.Pdf for .NET supports the creation of PDF files through API and XML or XSL-FO templates.</font>";
Aspose.Pdf.HtmlFragment SecondRowText = new Aspose.Pdf.HtmlFragment(SecondRowString);
SecondRow.Cells[0].Paragraphs.Add(SecondRowText);
```

هنا، أضفنا صفًا آخر بنص إضافي، يمتد على كلا العمودين للحفاظ على التوازن في التخطيط.

## الخطوة 10: حفظ مستند PDF

وأخيرًا، نحتاج إلى حفظ المستند حتى تتمكن من عرض التغييرات.

```csharp
doc.Save(dataDir + "PlacingTextAroundImage_out.pdf");
```

يؤدي هذا إلى حفظ ملف PDF مع الصورة والنص بتنسيق كما نريد.

## خاتمة

قد يبدو وضع نص حول الصور في ملف PDF مهمةً شاقة، لكن Aspose.PDF لـ .NET يُبسّط العملية. باستخدام الجداول والصور والنصوص المُنسّقة، يمكنك إنشاء ملفات PDF احترافية المظهر بأقل جهد. ببضعة أسطر فقط من التعليمات البرمجية، يمكنك وضع المحتوى في المكان الذي تريده بالضبط، مما يمنح مستنداتك مظهرًا أنيقًا ومنظمًا.

## الأسئلة الشائعة

### هل يمكنني استخدام هذه الطريقة لوضع صور متعددة مع النص؟
نعم، قم ببساطة بإضافة المزيد من الصفوف والخلايا إلى جدولك لتضمين صور ونصوص إضافية.

### هل يمكنني تغيير محاذاة الصورة؟
بالتأكيد! يمكنك تعديل محاذاة الصورة بتعديل خصائص محاذاة الخلية.

### كيف أقوم بتنسيق النص بشكل أكبر؟
يمكنك استخدام علامات HTML داخل `HtmlFragment` كائن لتطبيق أنماط مختلفة مثل الخط العريض أو المائل أو الخطوط المختلفة.

### هل يمكنني التحكم بالمسافة بين النص والصورة؟
نعم، باستخدام `MarginInfo` يسمح لك الكائن بالتحكم في الحشو والهوامش بين العناصر.

### هل من الممكن إضافة روابط للنص؟
بالتأكيد! يمكنك تضمين روابط تشعبية في النص بتنسيق HTML باستخدام `<a>` العلامة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}