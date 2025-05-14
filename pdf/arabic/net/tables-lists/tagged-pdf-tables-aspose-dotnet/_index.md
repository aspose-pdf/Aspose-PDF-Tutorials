---
"date": "2025-04-11"
"description": "تعرّف على كيفية إنشاء جداول PDF سهلة الوصول ومُعلَّمة باستخدام Aspose.PDF لـ .NET. يغطي هذا الدليل كل شيء، بدءًا من إنشاء الجداول الأساسية ووصولًا إلى إضافة الرؤوس والتذييلات وسمات الملخص."
"title": "إنشاء جداول PDF مُعلَّمة باستخدام Aspose.PDF لـ .NET - دليل شامل"
"url": "/ar/net/tables-lists/tagged-pdf-tables-aspose-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# إنشاء جداول PDF مُعلَّمة باستخدام Aspose.PDF لـ .NET: دليل شامل

## مقدمة
يُعد إنشاء ملفات PDF سهلة الوصول ومنظمة أمرًا بالغ الأهمية لضمان سهولة استخدام مستنداتك من قِبل جميع المستخدمين، بمن فيهم مستخدمو التقنيات المساعدة مثل قارئات الشاشة. يُعلّمك هذا الدليل الشامل كيفية إنشاء جداول PDF مُعلَّمة باستخدام Aspose.PDF لـ .NET، وهي مكتبة فعّالة للتعامل مع مهام PDF المعقدة بكفاءة.

مع هذا البرنامج التعليمي، سوف تتعلم:
- كيفية استخدام Aspose.PDF لإنشاء جدول مُعَلَّم أساسي.
- تقنيات لإضافة الرؤوس ومحتوى النص والتذييلات وسمات الملخص.
- أفضل الممارسات لتحسين أداء PDF.

هل أنت مستعد لتحسين تطبيقات .NET لديك بإنشاء ملفات PDF ديناميكية؟ هيا بنا!

## المتطلبات الأساسية
قبل البدء في هذا البرنامج التعليمي، تأكد من أن لديك:
- **Aspose.PDF لـ .NET** تم تثبيت المكتبة. يمكنك استخدام مديري حزم مختلفين:
  - **.NET CLI:** `dotnet add package Aspose.PDF`
  - **وحدة تحكم مدير الحزمة:** `Install-Package Aspose.PDF`
- فهم أساسي للغة C# والبرمجة الكائنية التوجه.
- بيئة تطوير تم إعدادها باستخدام .NET، مثل Visual Studio.

### إعداد البيئة
1. قم بتثبيت مكتبة Aspose.PDF لـ .NET باستخدام الطريقة المفضلة لديك المذكورة أعلاه.
2. الحصول على ترخيص من [أسبوزي](https://purchase.aspose.com/buy) إذا كنت ترغب في استخدامه بعد انتهاء فترة التجربة، يمكنك طلب ترخيص مؤقت من [صفحة الترخيص المؤقت لـ Aspose](https://purchase.aspose.com/temporary-license/).

## إعداد Aspose.PDF لـ .NET
لبدء استخدام Aspose.PDF، قم بتهيئة المكتبة في مشروعك:

```csharp
// تهيئة مستند PDF جديد
document = new Document();

// الوصول إلى TaggedContent للمستند
taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example Table");
taggedContent.SetLanguage("en-US");
```
يتضمن هذا الإعداد إنشاء مثيل لـ `Document` وإعدادها `TaggedContent`، والتي سيتم استخدامها في هذا البرنامج التعليمي لبناء ملفات PDF منظمة.

## دليل التنفيذ

### إنشاء جدول مُعَلَّم أساسي
#### ملخص
إنشاء جدول مُعَلَّم بسيط هو الأساس لعمليات أكثر تعقيدًا. لنبدأ بإعداد هيكل جدول بسيط.

#### التنفيذ خطوة بخطوة:
```csharp
Document document = new Document();
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example Table");
taggedContent.SetLanguage("en-US");

StructureElement rootElement = taggedContent.RootElement;

// إنشاء جدول داخل بنية المستند
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// تعيين حدود للجدول بأكمله
tableElement.Border = new BorderInfo(BorderSide.All, 1.2F, Color.DarkBlue);
```
**توضيح:**
- نحن ننشئ مثيلًا لـ `Document` وأنشأ `TaggedContent`.
- أ `TableElement` يتم إنشاؤه وإضافته إلى بنية الجذر.
- يعمل تكوين الحدود على تعزيز الوضوح البصري.

### إضافة رأس إلى جدول PDF المُعَلَّم
#### ملخص
العناوين أساسية لتحديد أعمدة الجدول. توضح هذه الميزة كيفية إنشاء صف عناوين مُصمم.

#### التنفيذ خطوة بخطوة:
```csharp
TableElement tableElement = new TableElement();
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();

// إنشاء صف الرأس وتصميمه
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
headTrElement.BackgroundColor = Color.LightGray;

for (int colIndex = 0; colIndex < 4; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText(String.Format("Head {0}", colIndex));
    thElement.BackgroundColor = Color.GreenYellow;
    thElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
    thElement.IsNoBorder = true; // لا حدود للجماليات
    thElement.Margin = new MarginInfo(16.0, 2.0, 8.0, 2.0);
    thElement.Alignment = HorizontalAlignment.Right;
}
```
**توضيح:**
- أ `TableTHeadElement` يتم إنشاؤه لتحديد رأس الجدول.
- كل خلية رأسية (`TH`يتم تصميمه بلون الخلفية والحدود.

### ملء نص جدول PDF المُعَلَّم
#### ملخص
يتضمن ملء النص إضافة صفوف بيانات، والتي يمكن أن تتضمن تكوينات معقدة مثل نطاقات الصفوف/الأعمدة لتنظيم المحتوى بشكل أفضل.

#### التنفيذ خطوة بخطوة:
```csharp
TableElement tableElement = new TableElement();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();

for (int rowIndex = 0; rowIndex < 50; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = String.Format("Row {0}", rowIndex);

    for (int colIndex = 0; colIndex < 4; colIndex++)
    {
        int colSpan = 1, rowSpan = 1;

        if (colIndex == 1 && rowIndex == 1) { colSpan = 2; rowSpan = 2; }
        else if ((colIndex == 2 && (rowIndex == 1 || rowIndex == 2)) ||
                 (rowIndex == 2 && (colIndex == 1 || colIndex == 2))) continue;

        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText(String.Format("Cell [{0}, {1}]", rowIndex, colIndex));
        tdElement.BackgroundColor = Color.Yellow;
        tdElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
        tdElement.IsNoBorder = false;
        tdElement.Margin = new MarginInfo(8.0, 2.0, 8.0, 2.0);
        
        tdElement.Alignment = HorizontalAlignment.Center;

        TextState cellTextState = new TextState
        {
            ForegroundColor = Color.DarkBlue,
            FontSize = 7.5F,
            FontStyle = FontStyles.Bold,
            Font = FontRepository.FindFont("Arial")
        };
        tdElement.DefaultCellTextState = cellTextState;
        
        tdElement.IsWordWrapped = true;
        tdElement.VerticalAlignment = VerticalAlignment.Center;

        tdElement.ColSpan = colSpan;
        tdElement.RowSpan = rowSpan;
    }
}
```
**توضيح:**
- يتم ملء الجسم باستخدام حلقات متداخلة للتكرار عبر الصفوف والأعمدة.
- يتعامل المنطق الشرطي مع تطبيق نطاقات الأعمدة/الصفوف.

### إضافة تذييل إلى جدول PDF المُعَلَّم
#### ملخص
تلخص التذييلات أو تقدم معلومات إضافية حول محتوى الجدول، على غرار العناوين ولكن يتم وضعها في الأسفل.

#### التنفيذ خطوة بخطوة:
```csharp
TableElement tableElement = new TableElement();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// إنشاء صف تذييل وتصميمه
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
footTrElement.BackgroundColor = Color.LightSeaGreen;

for (int colIndex = 0; colIndex < 4; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText(String.Format("Foot {0}", colIndex));
    tdElement.Alignment = HorizontalAlignment.Center;
    
    tdElement.StructureTextState.FontSize = 7F;
    tdElement.StructureTextState.FontStyle = FontStyles.Bold;
}
```
**توضيح:**
- أ `TableTFootElement` يتم استخدامه لتحديد التذييل.
- كل خلية في صف التذييل (`TD`) تم تصميمها ومحاذاتها مركزيًا.

### إضافة سمة الملخص إلى جدول PDF المُوسوم
#### ملخص
تعمل سمة الملخص على تعزيز إمكانية الوصول من خلال توفير وصف نصي لبيانات الجدول، مما يساعد برامج قراءة الشاشة.

#### التنفيذ خطوة بخطوة:
```csharp
TableElement tableElement = new TableElement();
taggedContent.GetStructureRoot().AppendChild(tableElement);
tableElement.Summary = "This table provides an overview of data across four columns.";
```
**توضيح:**
- ال `Summary` تم تعيين الخاصية لتوفير وصف لمحتوى الجدول، مما يحسن إمكانية الوصول إليه.

## خاتمة
باتباع هذا الدليل، ستتعلم كيفية إنشاء جداول PDF مُعلَّمة باستخدام Aspose.PDF لـ .NET. تضمن هذه التقنيات سهولة الوصول إلى مستنداتك وتنظيمها بفعالية. واصل استكشاف ميزات Aspose.PDF لتحسين قدراتك على معالجة المستندات.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}