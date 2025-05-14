---
"description": "تعرف على كيفية تخصيص أرقام الصفحات أثناء إضافة جدول المحتويات إلى مستندات PDF الخاصة بك باستخدام Aspose.PDF لـ .NET في هذا البرنامج التعليمي الشامل."
"linktitle": "تخصيص أرقام الصفحات أثناء إضافة جدول المحتويات"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تخصيص أرقام الصفحات أثناء إضافة جدول المحتويات"
"url": "/ar/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تخصيص أرقام الصفحات أثناء إضافة جدول المحتويات

## مقدمة

في عالم إدارة المستندات، تُعدّ ملفات PDF هي الصيغة المُفضّلة لمشاركة المستندات وحفظها عبر مختلف المنصات. ولكن ماذا لو أردتَ تحسين مستندات PDF بميزات مثل جدول المحتويات (TOC)؟ هنا يأتي دور Aspose.PDF لـ .NET! تُتيح هذه المكتبة الفعّالة للمطورين التعامل مع ملفات PDF بسهولة، مما يُمكّنهم من إضافة وتعديل وتخصيص المحتوى بسهولة. في هذا البرنامج التعليمي، سنتناول بالتفصيل كيفية تخصيص أرقام الصفحات مع إضافة جدول المحتويات إلى مستندات PDF باستخدام Aspose.PDF لـ .NET. هيا، هيا بنا نبدأ!

## المتطلبات الأساسية

قبل أن ننتقل إلى الكود، هناك بعض الأشياء التي تحتاج إلى وضعها في مكانها:

1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. هذه ستكون بيئة التطوير الخاصة بنا.
2. Aspose.PDF لـ .NET: عليك تنزيل مكتبة Aspose.PDF وتثبيتها. يمكنك العثور عليها هنا. [هنا](https://releases.aspose.com/pdf/net/).
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم مقتطفات التعليمات البرمجية بشكل أفضل.
4. ملف PDF نموذجي: جهّز ملف PDF نموذجيًا للعمل عليه. يمكنك إنشاء ملف بسيط أو تنزيل ملف PDF موجود.

## استيراد الحزم

للبدء، نحتاج إلى استيراد الحزم اللازمة. افتح مشروع Visual Studio وأضف مرجعًا إلى مكتبة Aspose.PDF. يمكنك القيام بذلك باستخدام مدير الحزم NuGet:

1. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
2. حدد "إدارة حزم NuGet".
3. ابحث عن "Aspose.PDF" وقم بتثبيته.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

بمجرد تثبيت المكتبة، يمكنك البدء في الترميز!

## الخطوة 1: إعداد دليل المستندات الخاص بك

أولاً، علينا إعداد مجلد المستندات. هنا سنخزن ملفات PDF المدخلة والمخرجة. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

في هذه القطعة، استبدل `YOUR DOCUMENT DIRECTORY` مع المسار الفعلي لملفات PDF. سيساعدنا هذا في تحميل ملف PDF الحالي وحفظ النسخة المعدّلة.

## الخطوة 2: تحميل ملف PDF الموجود

الآن بعد أن قمنا بإعداد دليل المستندات الخاص بنا، فلنقم بتحميل ملف PDF الموجود. 

```csharp
Document doc = new Document(inFile);
```

هنا نقوم بإنشاء جديد `Document` الكائن عن طريق تمرير مسار ملف الإدخال. هذا يسمح لنا بتعديل محتوى PDF برمجيًا.

## الخطوة 3: إدراج صفحة جديدة لجدول المحتويات

بعد ذلك، نحتاج إلى إنشاء صفحة جديدة في ملف PDF الخاص بنا حيث سيتم وضع جدول المحتويات.

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

يُضيف هذا السطر صفحة جديدة في بداية المستند. سيُعرض جدول المحتويات على هذه الصفحة.

## الخطوة 4: إنشاء معلومات جدول المحتويات

الآن، دعنا نقوم بإنشاء كائن لتمثيل معلومات جدول المحتويات.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

في هذه الخطوة، نقوم بإنشاء `TocInfo` الكائن وضبط عنوانه إلى "جدول المحتويات". كما قمنا بتخصيص حجم الخط ونمطه. `PageNumbersPrefix` تم ضبطه على "P"، والذي سيضيف بادئة لأرقام الصفحات في جدول المحتويات.

## الخطوة 5: إضافة عناوين إلى جدول المحتويات

الآن يأتي الجزء الممتع! سنتصفح صفحات المستند ونضيف عناوين إلى جدول المحتويات.

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

في هذه الحلقة، نقوم بإنشاء حلقة جديدة `Heading` كائن لكل صفحة. نحدد صفحة الوجهة لكل عنوان، ونحدد النص المراد عرضه، وهو "الصفحة س"، حيث س هو رقم الصفحة. وأخيرًا، نضيف العنوان إلى صفحة جدول المحتويات.

## الخطوة 6: حفظ المستند المحدث

بعد إضافة جميع العناوين الضرورية، حان الوقت لحفظ المستند المحدث.

```csharp
doc.Save(outFile);
```

يحفظ هذا السطر ملف PDF المُعدَّل مع جدول المحتويات. يمكنك الآن فتح ملف الإخراج والاطلاع على جدول المحتويات المُخصَّص.

## خاتمة

ها قد انتهيت! لقد نجحت في تخصيص أرقام الصفحات وإضافة جدول محتويات إلى مستند PDF باستخدام Aspose.PDF لـ .NET. تُسهّل هذه المكتبة القوية التعامل مع ملفات PDF، وببضعة أسطر برمجية فقط، يمكنك تحسين مستنداتك بشكل ملحوظ. سواء كنت تُنشئ تقارير أو كتبًا إلكترونية أو أي نوع آخر من ملفات PDF، فإن وجود جدول محتويات يُحسّن بشكل كبير من تجربة تصفح قرائك. فماذا تنتظر؟ انغمس في Aspose.PDF وابدأ بإنشاء ملفات PDF رائعة اليوم!

## الأسئلة الشائعة

### ما هو Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة تسمح للمطورين بإنشاء مستندات PDF ومعالجتها وتحويلها برمجيًا.

### هل يمكنني استخدام Aspose.PDF مجانًا؟
نعم، يُقدّم Aspose نسخة تجريبية مجانية يُمكنك استخدامها لاستكشاف ميزات المكتبة. يُمكنك تنزيلها. [هنا](https://releases.aspose.com/).

### كيف أحصل على الدعم لـ Aspose.PDF؟
يمكنك الحصول على الدعم من خلال زيارة منتدى Aspose [هنا](https://forum.aspose.com/c/pdf/10).

### هل يوجد ترخيص مؤقت متاح؟
نعم، يمكنك طلب ترخيص مؤقت لـ Aspose.PDF [هنا](https://purchase.aspose.com/temporary-license/).

### أين يمكنني شراء Aspose.PDF لـ .NET؟
يمكنك شراء Aspose.PDF لـ .NET [هنا](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}