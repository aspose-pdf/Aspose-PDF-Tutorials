---
"description": "تعرّف على كيفية تنسيق خلايا الجدول في ملف PDF باستخدام Aspose.PDF لـ .NET من خلال هذا البرنامج التعليمي المفصل. اتبع التعليمات لإنشاء وتنسيق جداول PDF جميلة."
"linktitle": "خلية جدول الأنماط"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "خلية جدول الأنماط"
"url": "/ar/net/programming-with-tagged-pdf/style-table-cell/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# خلية جدول الأنماط

## مقدمة

إنشاء جداول PDF احترافية قد يكون صعبًا، ولكن مع Aspose.PDF لـ .NET، الأمر سهلٌ للغاية! سواءً كنت تُنسق رؤوس الصفحات أو تذييلاتها أو خلايا جدول مُحددة، تُوفر لك هذه المكتبة القوية جميع الأدوات اللازمة لإنشاء مستندات PDF بتنسيق رائع. في هذا البرنامج التعليمي، سنشرح كيفية تنسيق خلايا الجدول في مستند PDF باستخدام Aspose.PDF لـ .NET. لا تقلق، سنُفصّل كل شيء في خطوات سهلة.

## المتطلبات الأساسية

قبل الغوص في الكود، تأكد من أن لديك المتطلبات الأساسية التالية:

1. Aspose.PDF لـ .NET: قم بتنزيل أحدث إصدار من Aspose.PDF وتثبيته من [هنا](https://releases.aspose.com/pdf/net/).
2. IDE (مثل Visual Studio): قم بإعداد بيئة تطوير .NET.
3. المعرفة الأساسية ببرمجة C#: مطلوب القليل من الألفة مع C#.
4. ترخيص Aspose.PDF: احصل على ترخيص مؤقت أو كامل للاستفادة من جميع ميزات المكتبة. يمكنك الحصول على نسخة تجريبية مجانية. [هنا](https://purchase.aspose.com/temporary-license/).

## استيراد الحزم

قبل البدء، تأكد من استيراد مساحات الأسماء اللازمة. ستحتاج إلى ما يلي في مشروعك:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

الآن بعد أن تم إعداد كل شيء، دعنا ننتقل إلى الدليل خطوة بخطوة!

سننشئ جدولًا في مستند PDF وننسق خلاياه. ستشرح كل خطوة العملية بالتفصيل.

## الخطوة 1: إنشاء مستند PDF جديد

الخطوة الأولى هي إنشاء مستند PDF جديد. في Aspose.PDF، يمكنك تهيئة ملف جديد `Document` الكائن الذي يمثل ملف PDF الخاص بك.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// إنشاء مستند PDF جديد
Document document = new Document();
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table cell style");
taggedContent.SetLanguage("en-US");
```

هنا، نقوم بتهيئة مستند PDF وتحديد عنوانه ولغته. هذا يمنح مستندك هيكلًا مناسبًا، وهو أمر ضروري للتوافق مع معايير PDF/UA.

## الخطوة 2: إعداد هيكل الجدول

تُعرَّف الجداول في ملفات PDF ضمن عناصر هيكلية. لنُنشئ الجدول ونُحدِّد صفوفه وأعمدته.

```csharp
// احصل على عنصر البنية الجذرية
StructureElement rootElement = taggedContent.RootElement;

// إنشاء عنصر هيكل الجدول
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

لقد قمنا الآن بتعريف رأس الجدول (`TableTHeadElement`)، جسم (`TableTBodyElement`)، والقدم (`TableTFootElement`) الأقسام. يمكنك اعتبارها بمثابة الهيكل العظمي لجدولك.

## الخطوة 3: تصميم خلايا الرأس

تصميم خلايا الرأس يجعلها بارزة. هنا، نُطبّق ألوان الخلفية والحدود ومحاذاة النص.

```csharp
int colCount = 4;
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";

for (int colIndex = 0; colIndex < colCount; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
    thElement.BackgroundColor = Color.GreenYellow;
    thElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
    thElement.IsNoBorder = true;
    thElement.Margin = new MarginInfo(16.0, 2.0, 8.0, 2.0);
    thElement.Alignment = HorizontalAlignment.Right;
}
```

في هذه الخطوة، نمرر كل خلية رأسية بشكل متكرر، ونمنحها خلفية خضراء-صفراء، وحدودًا رمادية، ونصًا محاذيًا لليمين. يمكنك تعديل هذه الخصائص لتتناسب مع التصميم الذي تريده.

## الخطوة 4: ملء وتصميم نص الجدول

يحتوي نص الجدول على البيانات الفعلية. إليك كيفية تصميم كل خلية باستخدام هوامش وحدود وإعدادات نصية محددة.

```csharp
int rowCount = 4;

for (int rowIndex = 0; rowIndex < rowCount; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = $"Row {rowIndex}";

    for (int colIndex = 0; colIndex < colCount; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
        tdElement.BackgroundColor = Color.Yellow;
        tdElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
        tdElement.Margin = new MarginInfo(8.0, 2.0, 8.0, 2.0);
        tdElement.Alignment = HorizontalAlignment.Center;
        
        TextState cellTextState = new TextState();
        cellTextState.ForegroundColor = Color.DarkBlue;
        cellTextState.FontSize = 7.5F;
        cellTextState.FontStyle = FontStyles.Bold;
        cellTextState.Font = FontRepository.FindFont("Arial");
        tdElement.DefaultCellTextState = cellTextState;
    }
}
```

في هذه الخطوة، نملأ نص الجدول بأربعة صفوف، ونُزين كل خلية بخلفيات صفراء ونص أزرق غامق في المنتصف. نستخدم أيضًا `MarginInfo` فئة لتحديد الحشو حول النص.

## الخطوة 5: تصميم التذييل

لإعطاء الجدول بنية كاملة، نضيف خلايا التذييل وننسقها، تمامًا كما فعلنا مع الرأس.

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";

for (int colIndex = 0; colIndex < colCount; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText($"Foot {colIndex}");
}
```

تم تصميم قسم التذييل بشكل مشابه لقسم الرأس، مما يجعل من السهل على القراء متابعة بنية الجدول.

## الخطوة 6: حفظ مستند PDF والتحقق منه

وأخيرًا، نحفظ مستند PDF ونتحقق مما إذا كان متوافقًا مع PDF/UA.

```csharp
// احفظ مستند PDF المُعَلَّم
document.Save(dataDir + "StyleTableCell.pdf");

// التحقق من توافق PDF/UA
document = new Document(dataDir + "StyleTableCell.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableCell.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

نقوم بحفظ ملف PDF واستخدامه `Validate` طريقة للتأكد من أنها تلبي معايير إمكانية الوصول (التوافق مع PDF/UA).

## خاتمة

يتميز تصميم الجداول في ملفات PDF باستخدام Aspose.PDF لـ .NET بالقوة والمرونة. ببضعة أسطر من التعليمات البرمجية، يمكنك إنشاء تصميمات جداول مخصصة تُبرز مستندات PDF الخاصة بك. من تخصيص حدود الخلايا والخلفيات إلى ضمان توافقها مع متطلبات إمكانية الوصول، يُسهّل Aspose.PDF إنشاء ملفات PDF أنيقة.

## الأسئلة الشائعة

### هل يمكنني تطبيق أنماط مختلفة على خلايا الجدول الفردية؟  
نعم، يمكنك تصميم خلايا فردية عن طريق تخصيصها `TableTDElement` ملكيات.

### كيف يمكنني دمج خلايا الجدول؟  
يمكنك استخدام `ColSpan` و `RowSpan` خصائص لدمج الخلايا في جدول.

### هل من الممكن إنشاء جدول متوافق مع PDF/UA؟  
نعم، كما هو موضح في هذا الدليل، يمكنك ضمان توافق PDF/UA من خلال التحقق من صحة مستندك باستخدام `Validate` طريقة.

### هل يمكنني استخدام خطوط مختلفة في خلايا الجدول؟  
بالتأكيد! يمكنك تحديد خطوط مختلفة باستخدام `TextState` كائن لكل خلية.

### كيف يمكنني تنزيل Aspose.PDF لـ .NET؟  
يمكنك تنزيله من [صفحة الإصدارات](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}