---
"description": "أنشئ ملفات PDF احترافية بسهولة عن طريق عرض الجداول باستخدام Aspose.PDF لـ .NET. اتبع دليلنا خطوة بخطوة لإتقان إنشاء المستندات."
"linktitle": "عرض الجدول في مستند PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "عرض الجدول في مستند PDF"
"url": "/ar/net/programming-with-tables/render-table/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# عرض الجدول في مستند PDF

## مقدمة

قد يبدو إنشاء ملفات PDF احترافية برمجيًا مهمة شاقة، ولكن مع Aspose.PDF لـ .NET، يصبح الأمر في غاية السهولة. سواء كنت تُنشئ تقارير أو فواتير أو أي نوع آخر من المستندات يتطلب بيانات جدولية، يوفر Aspose.PDF الأدوات اللازمة. في هذا البرنامج التعليمي، سنستكشف كيفية عرض الجداول في مستند PDF خطوة بخطوة. في النهاية، ستكتسب فهمًا متينًا لكيفية التعامل مع الجداول وإدارة خصائص الصفحات وحفظ ملفات PDF بسهولة.

## المتطلبات الأساسية

قبل أن نتعمق في الكود، إليك ما تحتاجه:

- فيجوال ستوديو: تأكد من تثبيت فيجوال ستوديو على جهازك. يمكنك تنزيله. [هنا](https://visualstudio.microsoft.com/downloads/).
- Aspose.PDF لـ .NET: يمكنك بسهولة تنزيل مكتبة Aspose.PDF من [صفحة إصدار Aspose](https://releases.aspose.com/pdf/net/).
- المعرفة الأساسية بلغة C#: إن فهم أساسيات لغة C# سوف يساعدك على المتابعة بشكل أفضل.
- .NET Framework: من الناحية المثالية، تأكد من أنك تعمل في بيئة .NET متوافقة.

بمجرد تعيين هذه المتطلبات الأساسية، ستكون جاهزًا لبدء إنشاء مستندات PDF الخاصة بك!

## استيراد الحزم

في بداية ملف C#، ستحتاج إلى استيراد مساحات أسماء Aspose.PDF اللازمة. هذا يسمح لك بالاستفادة من وظائف المكتبة في مشروعنا.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

تأكد من إضافة المراجع اللازمة إلى مكتبة Aspose.PDF في مشروعك. إذا كنت تستخدم NuGet، يمكنك إضافتها بسهولة بالبحث عن `Aspose.PDF`.

بعد أن أعددنا كل شيء، لنُقسّم العملية إلى خطوات سهلة لعرض جدول في مستند PDF. لا تقلق، سأشرح لك كل خطوة بتعليمات واضحة!

## الخطوة 1: إعداد معلومات المستند والصفحة

أولاً، علينا إنشاء مستند جديد وضبط إعدادات صفحته. إليك كيفية القيام بذلك:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document();
PageInfo pageInfo = doc.PageInfo;
Aspose.Pdf.MarginInfo marginInfo = pageInfo.Margin;

marginInfo.Left = 37;
marginInfo.Right = 37;
marginInfo.Top = 37;
marginInfo.Bottom = 37;

pageInfo.IsLandscape = true;
```

توضيح: 
- نبدأ بتحديد المكان الذي سيتم حفظ مستندنا فيه (`dataDir`). 
- ثم نقوم بإنشاء مثيل جديد لـ `Document` فصل. 
- نقوم بتهيئة هوامش الصفحة لإنشاء مساحة للتنفس حول طاولتنا.
- وأخيرًا، قمنا بتعيين المستند إلى الاتجاه الأفقي، مما يساعد عند عرض الجداول الأوسع.

## الخطوة 2: إنشاء الجدول الأول

بعد ذلك، دعنا نقوم بإنشاء جدولنا الأول ونملأه ببعض بيانات العينة:

```csharp
Aspose.Pdf.Table table = new Aspose.Pdf.Table();
table.ColumnWidths = "50 100"; // تحديد عرض الأعمدة
```

الشرح: هنا، نقوم بإنشاء مثيل لـ `Table` حدّد عرضَي العمود. سيكون عرض العمود الأول ٥٠ وحدة، والثاني ١٠٠ وحدة.

## الخطوة 3: ملء الجدول بالصفوف

الآن، دعنا نضيف صفوفًا إلى جدولنا في حلقة:

```csharp
Page curPage = doc.Pages.Add(); // إضافة صفحة جديدة
for (int i = 1; i <= 120; i++)
{
    Aspose.Pdf.Row row = table.Rows.Add();
    row.FixedRowHeight = 15; // تعيين ارتفاع ثابت للصفوف
    
    Aspose.Pdf.Cell cell1 = row.Cells.Add();
    cell1.Paragraphs.Add(new TextFragment("Content 1"));
    
    Aspose.Pdf.Cell cell2 = row.Cells.Add();
    cell2.Paragraphs.Add(new TextFragment("HHHHH"));
}
```

توضيح: 
- هنا نقوم بإنشاء صفحة جديدة لإضافة الجدول الخاص بنا.
- نحن نستخدم `for` حلقة لإضافة ١٢٠ صفًا إلى جدولنا. لكل صف ارتفاع ثابت قدره ١٥ وحدة.
- داخل كل صف، نضيف خليتين ونملأهما بالنص.

## الخطوة 4: إضافة الجدول الأول إلى الصفحة

بمجرد ملء الجدول، سنضيفه إلى الصفحة الحالية:

```csharp
Aspose.Pdf.Paragraphs paragraphs = curPage.Paragraphs;
paragraphs.Add(table);
```

التوضيح: هذه الخطوة تقوم ببساطة بإضافة الجدول الذي أنشأناه إلى فقرات الصفحة الحالية، مما يجعل الجدول مرئيًا في مستند PDF.

## الخطوة 5: إنشاء جدول ثانٍ

الآن، دعنا ننشئ جدولًا ثانيًا بمحتوى مختلف ونضيفه إلى صفحة جديدة:

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
table1.ColumnWidths = "100 100";
for (int i = 1; i <= 10; i++)
{
    Aspose.Pdf.Row row = table1.Rows.Add();
    Aspose.Pdf.Cell cell1 = row.Cells.Add();
    cell1.Paragraphs.Add(new TextFragment("LAAAAAAA"));
    
    Aspose.Pdf.Cell cell2 = row.Cells.Add();
    cell2.Paragraphs.Add(new TextFragment("LAAGGGGGG"));
}
table1.IsInNewPage = true; // إعداد الجدول الثاني ليظهر في صفحة جديدة
paragraphs.Add(table1);
```

توضيح: 
- يؤدي مقتطف التعليمات البرمجية هذا إلى إنشاء جدول جديد يحتوي على عمودين، يبلغ عرض كل منهما 100 وحدة.
- أ `for` تضيف الحلقة 10 صفوفًا بمحتوى العينة.
- عن طريق الإعداد `table1.IsInNewPage` إذا أردنا التأكد من ذلك، فإننا نضمن ظهور هذا الجدول على صفحة جديدة، مما يحافظ على الأشياء منظمة وغير مزدحمة.

## الخطوة 6: حفظ المستند

الآن بعد أن أصبحت جداولنا جاهزة، فلنحفظ مستندنا:

```csharp
dataDir = dataDir + "IsNewPageProperty_Test_out.pdf";
doc.Save(dataDir);
```

شرح: نحدد اسم الملف ونحفظ المستند في المجلد المحدد. عند تشغيل هذا الكود، يظهر ملف PDF بعنوان `IsNewPageProperty_Test_out.pdf` سيتم إنشاؤه في الموقع المحدد الخاص بك.

## الخطوة 7: رسالة التأكيد

أخيرًا، لإعلام المستخدم بأن كل شيء يعمل بسلاسة، يمكننا إضافة رسالة وحدة تحكم ودية:

```csharp
Console.WriteLine("\nTable rendered successfully on a page.\nFile saved at " + dataDir);
```

التوضيح: هذه طريقة بسيطة للتأكد من نجاح العملية ومكان العثور على ملف PDF الجديد للمستخدم.

## خاتمة

ها قد انتهيت! لقد نجحت في عرض الجداول في مستند PDF باستخدام Aspose.PDF لـ .NET. ببضعة أسطر برمجية فقط، يمكنك معالجة وعرض كميات كبيرة من البيانات بتنسيق منظم، مما يجعل مستنداتك غنية بالمعلومات وجذابة بصريًا. سواء كنت تعمل على قوائم جرد أو تقارير مالية أو مستندات تعليمية، تُعد الجداول وسيلة ممتازة لعرض المعلومات المعقدة بلمحة.

## الأسئلة الشائعة

### هل يمكنني تخصيص مظهر الجداول في Aspose.PDF؟  
بالتأكيد! يمكنك تعديل الألوان والحدود وأنماط الخطوط وخصائص أخرى لتحسين مظهر جداولك.

### هل استخدام Aspose.PDF مجاني؟  
يقدم Aspose.PDF نسخة تجريبية مجانية، ولكن للاستخدام التجاري، يلزم الشراء. يمكنك الاطلاع على الأسعار. [هنا](https://purchase.aspose.com/buy).

### كيف يمكنني الحصول على الدعم لمشاكل Aspose.PDF؟  
يمكنك طلب المساعدة من منتدى دعم Aspose [هنا](https://forum.aspose.com/c/pdf/10).

### هل هناك أية قيود على النسخة التجريبية المجانية؟  
نعم، قد تتضمن النسخة التجريبية بعض القيود، مثل وضع علامات مائية على المستندات المُنشأة. للاستفادة الكاملة من الميزات، يُرجى الحصول على ترخيص مؤقت. [هنا](https://purchase.aspose.com/temporary-license/).

### أين يمكنني العثور على مزيد من المعلومات حول ميزات Aspose.PDF؟  
يمكنك استكشاف الوثائق الشاملة المتاحة [هنا](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}