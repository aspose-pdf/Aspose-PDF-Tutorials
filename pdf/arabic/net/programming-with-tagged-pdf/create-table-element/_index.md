---
"description": "دليل خطوة بخطوة لإنشاء عنصر مصفوفة باستخدام Aspose.PDF لـ .NET. أنشئ ملفات PDF ديناميكية مع جداول بسهولة."
"linktitle": "إنشاء عنصر الجدول"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إنشاء عنصر الجدول"
"url": "/ar/net/programming-with-tagged-pdf/create-table-element/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء عنصر الجدول

## مقدمة

هل تساءلت يومًا كيف يمكنك إنشاء وتخصيص عناصر جدول في ملف PDF بسهولة باستخدام .NET؟ حسنًا، Aspose.PDF لـ .NET هو حلك الأمثل! سواء كنت تُؤتمت إنشاء التقارير أو تُنشئ جداول ديناميكيًا لمستندات متنوعة، يوفر Aspose.PDF واجهة برمجة تطبيقات غنية للتعامل مع عناصر الجدول. سيشرح لك هذا الدليل خطوة بخطوة كيفية إنشاء جدول، وتصميمه، وحتى ضمان توافقه مع معايير PDF/UA. يبدو الأمر مثيرًا للاهتمام، أليس كذلك؟ لنبدأ!

## المتطلبات الأساسية

قبل أن نبدأ، ستحتاج إلى بعض الأشياء في مكانها:
1. Aspose.PDF لـ .NET: قم بتنزيل الإصدار الأحدث من [تنزيل Aspose.PDF لـ .NET](https://releases.aspose.com/pdf/net/).
2. بيئة التطوير: أي بيئة تطوير متكاملة تدعم .NET (على سبيل المثال، Visual Studio).
3. المعرفة الأساسية بلغة C#: يوصى بالتعرف على برمجة C#.

أخيرًا، لا تنسَ ترخيص Aspose.PDF. إذا لم يكن لديك ترخيص، يمكنك استخدام [نسخة تجريبية مجانية](https://releases.aspose.com/) أو اطلب [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) لاختبار كل شيء.

## استيراد الحزم

أولاً، لنستورد الحزم اللازمة. سيسمح لنا هذا بالعمل مع جميع الفئات ذات الصلة لإنشاء الجداول في مستندات PDF.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

في هذا القسم، سنُقسّم عملية إنشاء جدول إلى عدة خطوات. تُركّز كل خطوة على جوانب مختلفة من عملية إنشاء الجدول وتخصيصه.

## الخطوة 1: إنشاء مستند PDF جديد

أول ما علينا فعله هو إنشاء مستند PDF جديد. سيكون هذا المستند بمثابة حاوية لجدولنا.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// إنشاء مستند PDF جديد
Document document = new Document();
```

هنا، نقوم بتهيئة مثيل جديد لـ `Document` الصف، الذي سيكون ملف PDF الفارغ. لا تنسَ تحديد مسار الملف!

## الخطوة 2: إعداد المحتوى المُوسوم

بعد ذلك، نحتاج إلى تفعيل المحتوى المُعلَّم، مما يضمن سهولة الوصول إلى الجدول. ملفات PDF المُعلَّمة مطلوبة للامتثال لمعايير PDF/UA (إمكانية الوصول الشامل).

```csharp
// تمكين المحتوى المُوسوم
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example Table");
taggedContent.SetLanguage("en-US");
```

تُحدد هذه الخطوة عنوان المستند ولغته، مما يضمن توافق الجدول مع معايير إمكانية الوصول. يُعدّ توفير مستندات سهلة الوصول أمرًا بالغ الأهمية لتحسين تجربة المستخدم والمتطلبات القانونية في بعض القطاعات.

## الخطوة 3: إنشاء عنصر الجدول

والآن يأتي الجزء الممتع - إنشاء الجدول نفسه!

```csharp
// احصل على عنصر البنية الجذرية
StructureElement rootElement = taggedContent.RootElement;
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
```

هنا، نحن نستخدم `RootElement` المحتوى المُعلَّم لإضافة جدولنا. هذا يُضيف جدولًا كعقدة فرعية إلى بنية المستند.

## الخطوة 4: تخصيص حدود الجدول والرؤوس

لا تريد أن تبدو طاولتك باهتة، أليس كذلك؟ لنضف لمسةً من الأناقة!

```csharp
tableElement.Border = new BorderInfo(BorderSide.All, 1.2F, Color.DarkBlue);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

نقوم بتحديد الحدود وإضافة الرؤوس والنصوص والتذييلات إلى الجدول. لاحظ استخدام `BorderInfo` لتزيين حدود الجدول باللون الأزرق الداكن.

## الخطوة 5: إضافة الصفوف والخلايا إلى الجدول

الآن، لنملأ جدولنا بالصفوف والخلايا. في هذا الجزء من العملية، نُحدد تخطيط جدولنا.

### الخطوة 5.1: إنشاء صف الرأس

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
headTrElement.BackgroundColor = Color.LightGray;

for (int colIndex = 0; colIndex < 4; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
    thElement.BackgroundColor = Color.GreenYellow;
    thElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
    thElement.Alignment = HorizontalAlignment.Right;
}
```

نحن نقوم بإنشاء صف رأس يحتوي على 4 أعمدة، ويتم تصميم كل خلية رأس بلون خلفية `GreenYellow`لقد قمنا أيضًا بتعيين حدود ومحاذاة للرؤوس.

### الخطوة 5.2: إضافة صفوف الجسم

```csharp
for (int rowIndex = 0; rowIndex < 50; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = $"Row {rowIndex}";

    for (int colIndex = 0; colIndex < 4; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
        tdElement.BackgroundColor = Color.Yellow;
        tdElement.Alignment = HorizontalAlignment.Center;
    }
}
```

هنا، نُنشئ ديناميكيًا ٥٠ صفًا و٤ أعمدة، ونملأها بالنص ونُنسق الخلايا. لون الخلفية أصفر، مع تركيز النص في المنتصف.

### الخطوة 5.3: إضافة صف التذييل

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
footTrElement.BackgroundColor = Color.LightSeaGreen;

for (int colIndex = 0; colIndex < 4; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText($"Foot {colIndex}");
    tdElement.Alignment = HorizontalAlignment.Center;
}
```

لإكمال الجدول، نضيف تذييلًا يحتوي على نص مركزي و `LightSeaGreen` خلفية.

## الخطوة 6: التحقق من توافق PDF/UA

بمجرد إنشاء الجدول، من المهم التأكد من أن ملف PDF متوافق مع PDF/UA.

```csharp
document.Save(dataDir + "CreateTableElement.pdf");

// التحقق من صحة توافق PDF/UA
document = new Document(dataDir + "CreateTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "table.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

يحفظ هذا المقطع ملف PDF ويتحقق من استيفائه لمعايير توافق PDF/UA. إذا كان المستند متوافقًا، فسيكون متاحًا للمستخدمين ذوي الإعاقة.

## خاتمة

تهانينا! لقد نجحت في إنشاء جدول مُخصّص بالكامل في ملف PDF باستخدام Aspose.PDF لـ .NET. بدءًا من تصميم الجدول ووصولًا إلى ضمان توافقه مع PDF/UA، أصبح لديك الآن أساس متين لإنشاء جداول ديناميكية في مستندات PDF. لا تنسَ استكشاف الميزات الشاملة لـ Aspose.PDF لتحسين مستنداتك بشكل أكبر!

## الأسئلة الشائعة

### هل يمكنني تخصيص الخط ونمط النص للجدول؟
نعم، يسمح لك Aspose.PDF بتخصيص الخطوط وأنماط النص والمحاذاة بالكامل باستخدام `TextState` فصل.

### كيف يمكنني إضافة المزيد من الأعمدة أو الصفوف بشكل ديناميكي؟
يمكنك تعديل عدد الأعمدة أو الصفوف عن طريق تعديل `rowIndex` و `colIndex` في الحلقات.

### هل من الممكن دمج الخلايا في الجدول؟
نعم يمكنك استخدام `ColSpan` و `RowSpan` خصائص لدمج الخلايا عبر الأعمدة أو الصفوف.

### ما هو التوافق مع PDF/UA؟
يضمن توافق PDF/UA إمكانية وصول المستخدمين ذوي الإعاقة إلى المستند، مع الالتزام بمعايير إمكانية الوصول الدولية.

### كيف يمكنني اختبار التوافق مع PDF/UA في Aspose.PDF؟
يمكنك استخدام `Validate` طريقة للتحقق من أن المستند يتوافق مع معايير PDF/UA.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}