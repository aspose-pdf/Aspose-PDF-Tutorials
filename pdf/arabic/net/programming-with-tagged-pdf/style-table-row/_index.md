---
"description": "تعرف على كيفية تنسيق صفوف الجدول في ملف PDF باستخدام Aspose.PDF لـ .NET من خلال دليل خطوة بخطوة لتحسين تنسيق مستندك بسهولة."
"linktitle": "صف جدول الأنماط"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "صف جدول الأنماط"
"url": "/ar/net/programming-with-tagged-pdf/style-table-row/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# صف جدول الأنماط

## مقدمة

عندما يتعلق الأمر بإنشاء مستندات PDF جيدة الهيكلة والتنسيق، يُعد Aspose.PDF for .NET الحل الأمثل. سواء كنت تُؤتمت التقارير أو الفواتير أو تُنشئ جداول ديناميكية، فإن تنسيق الجداول بأنماط متنوعة هو مفتاح الحصول على مستند أنيق. في هذا البرنامج التعليمي، سنتعمق في تنسيق صف جدول باستخدام Aspose.PDF for .NET. ولا تقلق، سأرشدك خطوة بخطوة، تمامًا كما لو كنت تتبادل أطراف الحديث على فنجان قهوة!

## المتطلبات الأساسية

قبل أن ندخل في التفاصيل، لنتأكد من تجهيز كل شيء. ستحتاج إلى:

1. مكتبة Aspose.PDF لـ .NET  
   إذا لم يكن لديك بالفعل، يمكنك الحصول عليه من [هنا](https://releases.aspose.com/pdf/net/).يمكنك أيضًا الحصول على [نسخة تجريبية مجانية](https://releases.aspose.com/) للبدء.
2. بيئة التطوير  
   قم بتثبيت Visual Studio أو أي بيئة تطوير متكاملة C# من اختيارك. ستحتاج أيضًا إلى تثبيت .NET، ولكن أعتقد أنك على دراية به بالفعل.
3. المعرفة الأساسية بلغة C# و.NET  
   إن فهم لغة C# جيدًا سيجعل هذا البرنامج التعليمي سهلًا للغاية. ولكن لا تقلق، سأشرح كل خطوة بالتفصيل!

## استيراد الحزم

قبل البدء بالعمل مع Aspose.PDF، نحتاج إلى استيراد مساحات الأسماء اللازمة. في مشروع C# الخاص بك، تأكد من تضمين ما يلي:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

تعتبر هذه العناصر ضرورية لإنشاء الجدول وتصميمه، وبالطبع، للعمل مع المحتوى المميز من أجل التوافق.

الآن دعنا نقسم المهمة خطوة بخطوة، حتى تتمكن من تصميم صفوف الجدول الخاص بك مثل المحترفين!

## الخطوة 1: إنشاء مستند PDF جديد

أولاً: لننشئ مستند PDF جديدًا. سيحتوي هذا المستند على جميع صفوف الجدول المُنسّقة.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// إنشاء مستند
Document document = new Document();
```

هنا، نقوم ببساطة بتهيئة ملف جديد `Document` الكائن الذي سيمثل ملف PDF الخاص بنا. تأكد من تحديد مسار المجلد الذي ستحفظ فيه ملفات الإخراج.

## الخطوة 2: العمل مع المحتوى المُوسوم

لهيكلة ملف PDF الخاص بك لتسهيل الوصول إليه، سنعمل على محتوى مُعَلَّم. يُساعد هذا في إنشاء عناصر مُنَظَّمة، مثل الجداول، مما يضمن توافقها مع معايير إمكانية الوصول مثل PDF/UA.

```csharp
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table row style");
taggedContent.SetLanguage("en-US");
```

هنا، نُحدِّد عنوان ولغة محتوى ملف PDF المُعَلَّم. الأمر أشبه بتسمية ملف PDF وتحديد اللغة التي يجب أن يتحدث بها!

## الخطوة 3: تحديد بنية الجدول

الآن، لنُحدد بنية الجدول الذي سننشئه. يحتاج كل جدول إلى رأس ونص وتذييل، تمامًا مثل منشور مدونة منظم جيدًا!

```csharp
// الحصول على عنصر البنية الجذرية
StructureElement rootElement = taggedContent.RootElement;

// إنشاء عنصر هيكل الجدول
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

ما نقوم به هنا هو إنشاء جدول برأس (`THead`)، جسم (`TBody`)، والتذييل (`TFoot`). هذه العناصر سوف تحتوي على صفوفنا.

## الخطوة 4: إضافة صف رأس الجدول

الجداول بدون عناوين كالكتب بدون عناوين. لنُنشئ صف العناوين أولًا لتوفير سياق للبيانات.

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText(String.Format("Head {0}", colIndex));
}
```

هنا، نقوم بالمرور وإضافة ثلاث خلايا رأسية (`TableTHElement`)، مع إعطاء كلٍّ منها نصًا وصفيًا. بسيط، أليس كذلك؟

## الخطوة 5: إضافة صفوف الجسم المصممة

الآن يأتي الجزء الممتع - تنسيق الصفوف! لنُنشئ سبعة صفوف بأنماط مُخصصة. سنُحدد ألوان الخلفية، والحدود، والحشو، ومحاذاة النص.

```csharp
for (int rowIndex = 0; rowIndex < 7; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = String.Format("Row {0}", rowIndex);
    trElement.BackgroundColor = Color.LightGoldenrodYellow;
    trElement.Border = new BorderInfo(BorderSide.All, 0.75F, Color.DarkGray);
    trElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.Blue);
    trElement.MinRowHeight = 100.0;
    trElement.FixedRowHeight = 120.0;
    trElement.IsInNewPage = (rowIndex % 3 == 1);
    trElement.IsRowBroken = true;

    for (int colIndex = 0; colIndex < 3; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText(String.Format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}
```

- لون الخلفية: استخدمنا لون أصفر ذهبي فاتح للحصول على تلك اللمسة الاحترافية والدافئة.
- الحدود: يحصل كل صف على حدود خارجية باللون الرمادي الداكن وحدود خلايا زرقاء للحصول على مظهر حاد.
- الارتفاع والحشو: تم ضبط ارتفاعات الصفوف، وتمت إضافة الحشو للحصول على مظهر أنيق.
- فواصل الصفحات: لجعل الجدول أكثر قابلية للقراءة، يبدأ كل صف ثاني في صفحة جديدة.

## الخطوة 6: إضافة صف التذييل

كما هو الحال مع الرأس، يُثبّت التذييل الجدول. لنُنشئ واحدًا.

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText(String.Format("Foot {0}", colIndex));
}
```

ببساطة، نمرر ثلاث خلايا في التذييل ونضيف نصًا. النص البديل للتذييل هو "صف التذييل" لتسهيل الوصول إليه.

## الخطوة 7: حفظ مستند PDF

الآن بعد أن تم إعداد الطاولة بالكامل، حان الوقت لحفظ تحفتك الفنية!

```csharp
document.Save(dataDir + "StyleTableRow.pdf");
```

بهذه السهولة، سيتم حفظ ملف PDF الخاص بك مع جميع صفوف الجدول الجميلة التي قمنا بتصميمها للتو.

## الخطوة 8: التحقق من توافق PDF/UA

لضمان التزام ملف PDF الخاص بنا بمعايير إمكانية الوصول، سنقوم بالتحقق من توافقه مع PDF/UA.

```csharp
document = new Document(dataDir + "StyleTableRow.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableRow.xml", PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

هذا يضمن استيفاء ملف PDF الخاص بك لمعايير PDF/UA، مما يجعله متاحًا للجميع. سهولة الوصول هي سر النجاح!

## خاتمة

وها قد انتهيت! ببضعة أسطر برمجية فقط، أنشأت جدولاً بتنسيق كامل في ملف PDF باستخدام Aspose.PDF لـ .NET. من الرؤوس إلى التذييلات، قمنا بتنسيق كل صف، وأضفنا عناصر إمكانية الوصول، بل وتحققنا من توافق المستند. سواء كنت تعمل على تقارير الشركات أو العروض التقديمية أو تستمتع فقط بملفات PDF، فهذا الدليل يغطي كل شيء. الآن، ابدأ بتنسيق جداولك باحترافية!

## الأسئلة الشائعة

### هل يمكنني تغيير نمط الخط الخاص بالجدول أيضًا؟  
نعم! يمكنك تعديل نمط الخط باستخدام `TextState` كائن لكل خلية، مما يسمح بالتخصيص الكامل.

### كيف أضيف المزيد من الأعمدة إلى جدولي؟  
فقط قم بتعديل `colCount` متغير وإضافة المزيد من الخلايا في الحلقات للرؤوس والنص والتذييلات.

### ماذا يحدث إذا لم أقم بتعيين ارتفاع الصف؟  
إذا لم تقم بتعيين ارتفاع الصف، فسيتم تعديل الجدول تلقائيًا استنادًا إلى المحتوى.

### هل يمكنني استخدام هذا لعدد ديناميكي من الصفوف؟  
بالتأكيد! يمكنك جلب البيانات من قاعدة بيانات أو أي مصدر آخر وتعديل عدد الصفوف والأعمدة ديناميكيًا.

### هل استخدام Aspose.PDF لـ .NET مجاني؟  
يعد Aspose.PDF لـ .NET منتجًا مرخصًا، ولكن يمكنك تجربته باستخدام [نسخة تجريبية مجانية](https://releases.aspose.com/) أو احصل على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}