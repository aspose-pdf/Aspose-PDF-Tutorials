---
"description": "تعرف على كيفية إنشاء عنصر جدول وتصميمه في Aspose.PDF لـ .NET باستخدام الإرشادات خطوة بخطوة والتصميم المخصص والتوافق مع PDF/UA."
"linktitle": "عنصر جدول الأنماط"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "عنصر جدول الأنماط"
"url": "/ar/net/programming-with-tagged-pdf/style-table-element/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# عنصر جدول الأنماط

## مقدمة

في هذه المقالة، سنتعمق في كيفية إنشاء عناصر جدول وتنسيقها باستخدام Aspose.PDF لـ .NET. ستتعلم كيفية هيكلة الجدول، وتطبيق أنماط مخصصة، والتحقق من توافق مستندك مع PDF/UA. بنهاية هذا البرنامج التعليمي، ستتمكن من إنشاء جداول احترافية في ملفات PDF بسهولة!

## المتطلبات الأساسية

قبل القفز إلى البرنامج التعليمي، ستحتاج إلى التأكد من أن لديك ما يلي:

1. تم تثبيت Visual Studio أو IDE مماثل على جهازك.
2. .NET Framework أو .NET Core SDK لتشغيل التطبيق.
3. تم تنزيل مكتبة Aspose.PDF لـ .NET والرجوع إليها في مشروعك. يمكنك الحصول على أحدث إصدار من [هنا](https://releases.aspose.com/pdf/net/).
4. ترخيص Aspose صالح أو [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) لفتح كافة وظائف المكتبة.

## استيراد الحزم

للبدء، قم باستيراد المساحات الأساسية اللازمة إلى مشروعك:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

تغطي هذه المساحات الأساسية عمليات PDF والمحتوى المميز والجداول وتنسيق النص.

الآن، لنبدأ بشرح عملية إنشاء جدول وتصميمه في Aspose.PDF. سنشرح كل قسم بالتفصيل لتتمكن من متابعته.

## الخطوة 1: إنشاء مستند PDF جديد وإعداد المحتوى المميز

في هذه الخطوة الأولى، سنقوم بإنشاء مستند PDF فارغ وإعداد المحتوى المميز له.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// إنشاء مستند PDF جديد
Document document = new Document();

// إعداد المحتوى المُوسوم
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table style");
taggedContent.SetLanguage("en-US");
```

نبدأ بإنشاء جديد `Document` الكائن الذي يمثل ملف PDF الخاص بنا. `TaggedContent` يُستخدم الكائن لإدارة بنية المستند، وضمان توافقه مع معايير إمكانية الوصول. نُحدد عنوان المستند ولغة استخدامه لوضع العلامات المناسبة.

## الخطوة 2: تحديد العنصر الجذر

بعد ذلك، سنقوم بإنشاء عنصر البنية الجذرية، والذي يعمل كحاوية لجميع المحتوى الموجود في ملف PDF الخاص بنا.

```csharp
// احصل على عنصر البنية الجذرية
StructureElement rootElement = taggedContent.RootElement;
```

ال `RootElement` يعمل كحاوية أساسية لجميع العناصر المُهيكلة، بما في ذلك جدولنا. فهو يُساعد في الحفاظ على التسلسل الهرمي الهيكلي للمستند، وهو أمرٌ مهمٌّ للتنظيم وسهولة الوصول.

## الخطوة 3: إنشاء عنصر الجدول وتصميمه

الآن بعد إعداد العنصر الجذر، سنقوم بإنشاء `TableElement` وتطبيق أنماط مثل لون الخلفية والحدود والمحاذاة.

```csharp
// إنشاء عنصر هيكل الجدول
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// تصميم الجدول
tableElement.BackgroundColor = Color.Beige;
tableElement.Border = new BorderInfo(BorderSide.All, 0.80F, Color.Gray);
tableElement.Alignment = HorizontalAlignment.Center;
tableElement.Broken = TableBroken.Vertical;
tableElement.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```

نحن ننشئ `TableElement`، الذي يحدد بنية الجدول لدينا. `BackgroundColor`، `Border`، و `Alignment` الخصائص تسمح لنا بتخصيص مظهر الجدول. `Broken` تضمن الخاصية أنه في حالة انقسام الجدول عبر الصفحات، فإنه سينكسر عموديًا.

## الخطوة 4: تعيين أبعاد الجدول وأنماط الخلايا

في هذه الخطوة، سنقوم بتحديد عدد الأعمدة، وحشو الخلايا، وخصائص الجدول المهمة الأخرى.

```csharp
tableElement.ColumnWidths = "80 80 80 80 80";
tableElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.DarkBlue);
tableElement.DefaultCellPadding = new MarginInfo(16.0, 2.0, 8.0, 2.0);
tableElement.DefaultCellTextState.ForegroundColor = Color.DarkCyan;
tableElement.DefaultCellTextState.FontSize = 8F;
```

نحدد عرض الأعمدة لضمان تباعد كل عمود في الجدول بشكل متساوٍ. `DefaultCellBorder`، `DefaultCellPadding`، و `DefaultCellTextState` قم بتحديد الأنماط الافتراضية للخلايا، بما في ذلك الحدود، والحشو، ولون النص، وحجم الخط.

## الخطوة 5: إضافة صفوف متكررة وأنماط مخصصة

يمكننا أيضًا تحديد أنماط لتكرار الصفوف وعناصر الجدول المحددة الأخرى مثل الرؤوس والتذييلات.

```csharp
tableElement.RepeatingRowsCount = 3;
TextState rowStyle = new TextState();
rowStyle.BackgroundColor = Color.LightCoral;
tableElement.RepeatingRowsStyle = rowStyle;
```

ال `RepeatingRowsCount` يضمن تكرار الصفوف الثلاثة الأولى إذا كان الجدول يمتد على عدة صفحات. نضبط `RepeatingRowsStyle` لتطبيق لون خلفية مخصص لهذه الصفوف.

## الخطوة 6: إضافة عناصر رأس الجدول والجسم والقاعدة

الآن، دعنا نقوم بإنشاء أقسام رأس الجدول، والجسم، والتذييل ونملأها بالمحتوى.

```csharp
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// إنشاء صف الرأس
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 5; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
}

// ملء نص الجدول
for (int rowIndex = 0; rowIndex < 10; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    for (int colIndex = 0; colIndex < 5; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
    }
}
```

ينقسم الجدول إلى ثلاثة أجزاء: الرأس، والنص، والتذييل. نُنشئ أولًا صف الرأس باستخدام `TableTHElement` وأضف عناوين الأعمدة. ثم نملأ نص الجدول بـ `TableTDElement`، ملء كل خلية بتسمية تتضمن موقعها.

## الخطوة 7: حفظ المستند

وأخيرًا، نقوم بحفظ مستند PDF في الدليل المحدد.

```csharp
// احفظ مستند PDF المُعَلَّم
document.Save(dataDir + "StyleTableElement.pdf");
```

تنهي هذه الخطوة عملية إنشاء المستند عن طريق حفظ ملف PDF بالجدول المصمم.

## الخطوة 8: التحقق من توافق PDF/UA

بعد حفظ المستند، من الضروري التأكد من أنه يتوافق مع معايير PDF/UA (إمكانية الوصول الشامل).

```csharp
// التحقق من توافق PDF/UA
document = new Document(dataDir + "StyleTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableElement.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

هنا، نعيد تحميل المستند ونتحقق من توافقه مع معايير PDF/UA. يضمن التوافق استيفاء ملف PDF لمتطلبات إمكانية الوصول، مما يجعله مناسبًا لمجموعة واسعة من المستخدمين.

## خاتمة

مع Aspose.PDF لـ .NET، أصبح إنشاء الجداول وتنسيقها في مستندات PDF أمرًا بسيطًا وبديهيًا. باتباع الخطوات الموضحة في هذا البرنامج التعليمي، يمكنك إنشاء جداول بأنماط مخصصة وضمان استيفاء ملفات PDF لمعايير إمكانية الوصول. سواء كنت تُنشئ تقارير أو مستندات منظمة، تُعد الجداول أداة فعّالة لعرض البيانات بوضوح.

## الأسئلة الشائعة

### هل يمكنني إضافة صور داخل خلايا الجدول؟
نعم، يمكنك إدراج الصور في خلايا الجدول باستخدام `Image` عنصر.

### كيف يمكنني تعديل عرض الأعمدة بشكل ديناميكي؟
يمكنك ضبط `ColumnAdjustment` الممتلكات إلى `AutoFitToWindow` لضبط عرض الأعمدة تلقائيًا استنادًا إلى المحتوى.

### هل الامتثال لـ PDF/UA إلزامي لجميع المستندات؟
على الرغم من أنه ليس إلزاميًا، فمن المستحسن بالنسبة للمستندات التي تتطلب معايير إمكانية وصول عالية.

### هل يمكنني تطبيق أنماط مختلفة على صفوف محددة؟
نعم، يمكنك تخصيص الصفوف أو الخلايا الفردية عن طريق ضبطها `TextState` أو `BackgroundColor`.

### ما هي فائدة استخدام المحتوى المميز؟
يساعد المحتوى المميز على تحسين إمكانية الوصول إلى المستندات ويساعد في ضمان الامتثال للمعايير مثل PDF/UA.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}