---
"description": "تعرّف على كيفية تصدير بيانات ورقة عمل Excel إلى جدول PDF باستخدام Aspose.PDF لـ .NET. دليل تعليمي خطوة بخطوة مع أمثلة برمجية ومتطلبات أساسية ونصائح مفيدة."
"linktitle": "تصدير بيانات ورقة عمل Excel إلى جدول"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تصدير بيانات ورقة عمل Excel إلى جدول"
"url": "/ar/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تصدير بيانات ورقة عمل Excel إلى جدول

## مقدمة

هل سبق لك أن احتجت إلى تصدير بيانات من ورقة عمل Excel إلى ملف PDF، مُرتّبة بشكل منظم في جدول؟ تخيّل أن لديك مجموعة كبيرة من البيانات في Excel، ولكنك تحتاج إلى مشاركتها كملف PDF احترافي. قد يبدو الأمر معقدًا، أليس كذلك؟ ولكن مع Aspose.PDF لـ .NET، يمكنك جعل هذه المهمة في غاية السهولة. في هذا البرنامج التعليمي، سنشرح لك عملية تصدير بيانات ورقة عمل Excel إلى جدول داخل مستند PDF باستخدام Aspose.PDF لـ .NET. سنشرح لك خطوة بخطوة، ونُفصّل كل شيء حتى لو كنت جديدًا في هذا المجال، ستشعر بالاحترافية في النهاية.

## المتطلبات الأساسية

قبل أن نتعمق في الترميز، دعونا نقوم بإعداد بعض الأشياء:

1. مكتبة Aspose.PDF لـ .NET - تأكد من تثبيت أحدث إصدار. يمكنك [قم بتحميله هنا](https://releases.aspose.com/pdf/net/).
2. مكتبة Aspose.Cells لـ .NET - ستحتاجها لإدارة عمليات Excel. حمّلها من [هنا](https://releases.aspose.com/cells/net/).
3. بيئة تطوير .NET – أداة مثل Visual Studio ستعمل بشكل مثالي للترميز.
4. ملف Excel - قم بإعداد ملف Excel بالبيانات التي تريد تصديرها.

إذا لم يكن لديك مكتبات Aspose.PDF وAspose.Cells، فيمكنك البدء بـ [نسخة تجريبية مجانية](https://releases.aspose.com/).

## استيراد الحزم

أولاً، تأكد من تثبيت مكتبتي Aspose.PDF وAspose.Cells في مشروعك. يمكنك تثبيتهما باستخدام NuGet Package Manager في Visual Studio.

فيما يلي كيفية استيراد الحزم الضرورية في كود C# الخاص بك:

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

الآن بعد أن قمنا بتعيين المتطلبات الأساسية، دعنا ننتقل إلى عملية تصدير البيانات من ورقة Excel إلى جدول في مستند PDF.

## الخطوة 1: تحميل مصنف Excel

للبدء، عليك تحميل مصنف Excel الخاص بك إلى البرنامج. في هذه الخطوة، سنستخدم Aspose.Cells لفتح ملف Excel.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// تحميل مصنف Excel
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

الشرح: هنا، نحدد مسار الدليل الذي يوجد به ملف Excel الخاص بنا ونقوم بتحميل المصنف باستخدام `Aspose.Cells.Workbook`. تأكد من التعديل `"YOUR DOCUMENT DIRECTORY"` للإشارة إلى موقع ملفك.

## الخطوة 2: الوصول إلى ورقة العمل الأولى

بعد تحميل المصنف، نحتاج إلى الوصول إلى ورقة العمل الأولى التي يتم تخزين بياناتنا فيها.

```csharp
// الوصول إلى ورقة العمل الأولى في ملف Excel
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

التوضيح: هذه الخطوة واضحة ومباشرة - فنحن نأخذ ورقة العمل الأولى من المصنف، والتي تحتوي على البيانات التي سيتم تصديرها.

## الخطوة 3: تصدير البيانات إلى جدول البيانات

الآن، دعنا نقوم بتصدير البيانات من ورقة Excel إلى كائن DataTable، والذي سيعمل كوسيط لنقل البيانات إلى ملف PDF.

```csharp
// تصدير محتويات 7 صفوف و 2 عمود بدءًا من الخلية الأولى إلى DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

الشرح: `ExportDataTable` تستخرج هذه الطريقة البيانات بدءًا من الخلية الأولى في ورقة العمل، وتغطي جميع الصفوف والأعمدة. ثم تُخزَّن هذه البيانات في `DataTable` لمزيد من الاستخدام.

## الخطوة 4: إنشاء مستند PDF جديد

بعد ذلك، نحتاج إلى إنشاء مستند PDF جديد باستخدام Aspose.PDF.

```csharp
// إنشاء مثيل مستند
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// إنشاء صفحة في مثيل المستند
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

التوضيح: هنا، نقوم بتهيئة ملف جديد `Aspose.Pdf.Document` وأضف صفحة إليها. ستحتوي هذه الصفحة لاحقًا على الجدول الذي ننشئه من بيانات Excel.

## الخطوة 5: إنشاء كائن جدول في PDF

لننتقل الآن إلى إنشاء جدول داخل مستند PDF.

```csharp
// إنشاء كائن جدول
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// أضف كائن الجدول إلى مجموعة الفقرات في الصفحة
page.Paragraphs.Add(table);
```

الشرح: نقوم بإنشاء `Aspose.Pdf.Table` الكائن وإضافته إلى مجموعة الفقرات الخاصة بالصفحة، مما يضمن عرض الجدول على الصفحة.

## الخطوة 6: تعيين عرض الأعمدة والحدود

تحتاج جداول PDF إلى عرض أعمدة محدد. سنضيف أيضًا حدودًا لتسهيل قراءة الجدول.

```csharp
// تعيين عرض أعمدة الجدول
table.ColumnWidths = "40 100 100";

// تعيين حدود الخلية الافتراضية
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

التوضيح: قمنا بتعيين عرض الأعمدة الثلاثة وإعطاء جميع الخلايا حدودًا افتراضية بسُمك `0.1F`.

## الخطوة 7: استيراد البيانات من جدول البيانات إلى جدول PDF

الآن، حان الوقت لاستيراد البيانات من جدول البيانات إلى جدول PDF الخاص بنا.

```csharp
// استيراد البيانات إلى كائن الجدول من DataTable
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

الشرح: `ImportDataTable` الطريقة تنقل جميع البيانات من `DataTable` إلى جدول PDF. سيؤدي هذا إلى ملء الجدول بالبيانات من ورقة Excel الخاصة بك.

## الخطوة 8: تصميم صف الرأس

دعنا نقوم بتصميم صف رأس الجدول عن طريق تغيير لون الخلفية والخط والمحاذاة.

```csharp
// احصل على الصف الأول من الجدول
Aspose.Pdf.Row headerRow = table.Rows[0];

// تعيين التصميم لصف الرأس
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

التوضيح: نقوم بالمرور على جميع الخلايا في الصف الأول (الرأس) ونضبط لون خلفيتها إلى اللون الأزرق، ولون النص إلى اللون الأصفر، ونقوم بمحاذاة النص إلى المركز.

## الخطوة 9: تصميم الصفوف المتبقية

للتفريق بين الرأس وبقية الصفوف، دعنا نضيف نمطًا مختلفًا للصفوف المتبقية.

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

التوضيح: بالنسبة لجميع الصفوف باستثناء الرأس، قمنا بتعيين خلفية رمادية ولون نص أبيض.

## الخطوة 10: حفظ مستند PDF

وأخيرًا، احفظ مستند PDF بالجدول.

```csharp
// احفظ ملف PDF
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

شرح: نحفظ ملف PDF في المجلد المحدد. ها هي بيانات Excel الخاصة بك موجودة الآن داخل جدول PDF بتنسيق رائع.

## خاتمة

ها قد انتهيت! بخطوات قليلة فقط، صدّرت بياناتك من ورقة عمل Excel إلى جدول داخل ملف PDF باستخدام Aspose.PDF لـ .NET. بتقسيم العملية وتصميمها، يمكنك تخصيص مخرجاتك وضمان ظهور بياناتك بشكل أنيق واحترافي. لذا، في المرة القادمة التي يُسلمك فيها أحدهم ملف Excel ويطلب تقرير PDF، ستعرف تمامًا ما يجب عليك فعله.

## الأسئلة الشائعة

### هل يمكنني تخصيص الجدول أكثر؟
بالتأكيد! يمكنك تعديل الألوان والخطوط والمحاذاة، بل وإضافة حدود لخلايا محددة.

### هل Aspose.PDF لـ .NET مجاني؟
يقدم نسخة تجريبية مجانية، ولكن للاستخدام الموسع، ستحتاج إلى ترخيص. يمكنك [اشتريه هنا](https://purchase.aspose.com/buy).

### هل يمكنني تصدير صفوف وأعمدة محددة فقط؟
نعم، يمكنك تعديل المعلمات في `ExportDataTable` طريقة لتصدير نطاقات محددة.

### هل يعمل هذا مع ملفات Excel الكبيرة؟
نعم، تم تصميم Aspose.Cells للتعامل مع ملفات Excel الكبيرة بكفاءة.

### كيف يمكنني إضافة المزيد من الصفحات إلى ملف PDF؟
يمكنك استخدام `pdfDocument.Pages.Add()` لإضافة عدد الصفحات التي تحتاجها.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}