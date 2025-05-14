---
"description": "تعرف على كيفية استخدام الرموز القابلة للاستبدال في الرأس والتذييل لمستند PDF باستخدام Aspose.PDF لـ .NET."
"linktitle": "الرموز القابلة للاستبدال في رأس وتذييل الصفحة"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "الرموز القابلة للاستبدال في رأس وتذييل الصفحة"
"url": "/ar/net/programming-with-text/replaceable-symbols-in-header-footer/"
"weight": 320
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# الرموز القابلة للاستبدال في رأس وتذييل الصفحة

## مقدمة

عند العمل مع ملفات PDF، قد تحتاج أحيانًا إلى تخصيص الرؤوس والتذييلات بمحتوى ديناميكي، مثل أرقام الصفحات أو أسماء التقارير أو تواريخ التوليد. لحسن الحظ، يُبسّط Aspose.PDF for .NET هذه العملية، حيث يتيح لك إنشاء ملفات PDF برموز مُحدّثة تلقائيًا في الرؤوس والتذييلات، مثل أرقام الصفحات أو تفاصيل إنشاء التقارير. ستُرشدك هذه المقالة خطوة بخطوة خلال عملية استبدال الرموز في الرؤوس والتذييلات باستخدام Aspose.PDF for .NET، بطريقة ليست بسيطة فحسب، بل فعّالة للغاية.

## المتطلبات الأساسية

قبل الغوص في الدليل خطوة بخطوة، تأكد من أن لديك ما يلي:

- مكتبة Aspose.PDF لـ .NET – [تحميل](https://releases.aspose.com/pdf/net/) أو احصل على [نسخة تجريبية مجانية](https://releases.aspose.com/).
- Visual Studio أو أي C# IDE مثبت على نظامك.
- المعرفة الأساسية بتطوير C# و.NET.
- صالحة [رخصة](https://purchase.aspose.com/temporary-license/) بالنسبة لـ Aspose.PDF، أو يمكنك استخدام الإصدار التجريبي.

## استيراد الحزم

للبدء، عليك استيراد مساحات الأسماء اللازمة لتمكين وظيفة Aspose.PDF لـ .NET. فيما يلي الاستيراد اللازم:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

تُعد هذه ضرورية للتعامل مع إنشاء ملفات PDF، ومعالجة النصوص، وإدارة الرأس/التذييل.

دعنا نقسم كود المثال إلى خطوات سهلة الفهم.

## الخطوة 1: إعداد المستند والصفحة

أولاً، علينا تهيئة المستند وإضافة صفحة إليه. هذا يُمهّد الطريق لإضافة رؤوس وتذييلات الصفحات.

```csharp
// إعداد دليل المستندات
string dataDir = "YOUR DOCUMENT DIRECTORY";

// تهيئة كائن المستند
Document doc = new Document();

// إضافة صفحة إلى المستند
Page page = doc.Pages.Add();
```

هنا، نقوم بإعداد مستند PDF باستخدام `Document` الصف وإضافة صفحة بها `doc.Pages.Add()`ستحتوي هذه الصفحة على الرأس والتذييل والمحتوى الآخر.

## الخطوة 2: تكوين هوامش الصفحة

بعد ذلك، سنقوم بتحديد هوامش الصفحة للتأكد من أن المحتوى الخاص بنا لا يصل إلى الحافة.

```csharp
// تكوين الهوامش
MarginInfo marginInfo = new MarginInfo();
marginInfo.Top = 90;
marginInfo.Bottom = 50;
marginInfo.Left = 50;
marginInfo.Right = 50;
page.PageInfo.Margin = marginInfo;
```

هنا، قمنا بتحديد الهوامش العلوية والسفلية واليسرى واليمنى باستخدام `MarginInfo` الصف وتطبيقه على الصفحة باستخدام `page.PageInfo.Margin`.

## الخطوة 3: إنشاء وتكوين الرأس

الآن، لنُنشئ رأسًا ونُضيفه إلى الصفحة. سيتضمن الرأس عنوان التقرير واسمه.

```csharp
// إنشاء رأس الصفحة
HeaderFooter hfFirst = new HeaderFooter();
page.Header = hfFirst;

// تعيين هوامش الرأس
hfFirst.Margin.Left = 50;
hfFirst.Margin.Right = 50;

// إضافة عنوان إلى الرأس
TextFragment t1 = new TextFragment("report title");
t1.TextState.Font = FontRepository.FindFont("Arial");
t1.TextState.FontSize = 16;
t1.TextState.ForegroundColor = Aspose.Pdf.Color.Black;
t1.TextState.FontStyle = FontStyles.Bold;
t1.TextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
hfFirst.Paragraphs.Add(t1);

// إضافة اسم التقرير إلى الرأس
TextFragment t2 = new TextFragment("Report_Name");
t2.TextState.Font = FontRepository.FindFont("Arial");
t2.TextState.FontSize = 12;
t2.TextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
hfFirst.Paragraphs.Add(t2);
```

لقد أضفنا اثنين `TextFragment` كائنات للرأس: واحد لعنوان التقرير وآخر لاسم التقرير. تم تنسيق النص باستخدام `TextState` خصائص مثل الخط والحجم والمحاذاة.

## الخطوة 4: إنشاء التذييل وتكوينه

الآن حان الوقت لإعداد التذييل، الذي سيحمل محتوى ديناميكيًا مثل أرقام الصفحات وتاريخ الإنشاء.

```csharp
// إنشاء تذييل
HeaderFooter hfFoot = new HeaderFooter();
page.Footer = hfFoot;

// تعيين هوامش التذييل
hfFoot.Margin.Left = 50;
hfFoot.Margin.Right = 50;

// إضافة محتوى التذييل
TextFragment t3 = new TextFragment("Generated on test date");
TextFragment t4 = new TextFragment("Report Name");
TextFragment t5 = new TextFragment("Page $p of $P");
```

في التذييل، قمنا بتضمين أجزاء لتاريخ التوليد واسم التقرير وأرقام الصفحات الديناميكية (`$p` و `$P` تمثل رقم الصفحة الحالية والعدد الإجمالي للصفحات، على التوالي).

## الخطوة 5: إنشاء جدول في التذييل

يمكنك أيضًا إضافة عناصر أكثر تعقيدًا مثل الجداول في التذييل لتنظيم بياناتك بشكل أفضل.

```csharp
// إنشاء جدول للتذييل
Table tab2 = new Table();
hfFoot.Paragraphs.Add(tab2);
tab2.ColumnWidths = "165 172 165";

// إنشاء صفوف وخلايا للجدول
Row row3 = tab2.Rows.Add();
row3.Cells.Add();
row3.Cells.Add();
row3.Cells.Add();

// تعيين المحاذاة لكل خلية
row3.Cells[0].Alignment = Aspose.Pdf.HorizontalAlignment.Left;
row3.Cells[1].Alignment = Aspose.Pdf.HorizontalAlignment.Center;
row3.Cells[2].Alignment = Aspose.Pdf.HorizontalAlignment.Right;

// إضافة محتوى إلى خلايا الجدول
row3.Cells[0].Paragraphs.Add(t3);
row3.Cells[1].Paragraphs.Add(t4);
row3.Cells[2].Paragraphs.Add(t5);
```

يؤدي كتلة التعليمات البرمجية هذه إلى إنشاء جدول مكون من 3 أعمدة في التذييل، حيث يحتوي كل عمود على أجزاء مختلفة من المعلومات، مثل تاريخ التوليد واسم التقرير وأرقام الصفحات.

## الخطوة 6: إضافة المحتوى إلى الصفحة

بالإضافة إلى الرؤوس والتذييلات، يمكنك إضافة محتوى إلى نص صفحة PDF. هنا، نضيف جدولاً يحتوي على نص بديل.

```csharp
Table table = new Table();
table.ColumnWidths = "33% 33% 34%";
page.Paragraphs.Add(table);

// إضافة محتوى الجدول
for (int i = 0; i <= 10; i++)
{
    Row row = table.Rows.Add();
    for (int c = 0; c <= 2; c++)
    {
        Cell cell = row.Cells.Add("Content " + c);
        cell.Margin = new MarginInfo { Left = 30, Top = 10, Bottom = 10 };
    }
}
```

يُضيف هذا الكود جدولاً بسيطاً بثلاثة أعمدة إلى الصفحة. يُمكنك تعديله ليناسب احتياجاتك.

## الخطوة 7: احفظ ملف PDF

بمجرد إعداد كل شيء، فإن الخطوة الأخيرة هي حفظ مستند PDF في الموقع المطلوب.

```csharp
dataDir = dataDir + "ReplaceableSymbolsInHeaderFooter_out.pdf";
doc.Save(dataDir);
Console.WriteLine("Symbols replaced successfully in header and footer. File saved at " + dataDir);
```

تحدد مسار الملف وتحفظ المستند باستخدام `doc.Save()`هذا كل شيء! لقد أنشأت ملف PDF بنجاح مع رؤوس وتذييلات مخصصة.

## خاتمة

استبدال الرموز في الرؤوس والتذييلات باستخدام Aspose.PDF لـ .NET ليس سهلاً فحسب، بل فعّالاً أيضاً. باتباع الدليل المفصل أعلاه، يمكنك بسهولة تخصيص ملفات PDF بمحتوى ديناميكي، مثل أرقام الصفحات وأسماء التقارير والتواريخ. تتميز هذه الطريقة بمرونة عالية، حيث تتيح لك إدراج الجداول وتعديل التنسيق والتحكم في التصميم بما يتناسب مع متطلباتك الخاصة.

## الأسئلة الشائعة

### هل يمكنني تخصيص الخطوط للرؤوس والتذييلات؟  
نعم، يمكنك تخصيص الخطوط والأحجام والألوان والأنماط للنصوص في الرؤوس والتذييلات بشكل كامل.

### كيف أضيف الصور إلى الرؤوس والتذييلات؟  
يمكنك استخدام `ImageStamp` لإدراج الصور في الرؤوس والتذييلات.

### هل من الممكن إضافة روابط تشعبية في الرؤوس أو التذييلات؟  
نعم يمكنك استخدام `TextFragment` مع وجود رابط تشعبي عن طريق ضبط `Hyperlink` ملكية.

### هل يمكنني استخدام رؤوس مختلفة للصفحات الفردية والزوجية؟  
نعم، يسمح لك Aspose.PDF بتحديد رؤوس وتذييلات مختلفة للصفحات الفردية والزوجية.

### كيف يمكنني تعديل مواضع الرأس والتذييل؟  
يمكنك ضبط الهوامش وخصائص المحاذاة للتحكم في موضع الرؤوس والتذييلات.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}