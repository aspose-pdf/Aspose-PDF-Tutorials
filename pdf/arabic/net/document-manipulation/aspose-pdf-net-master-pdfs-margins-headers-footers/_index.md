---
"date": "2025-04-11"
"description": "أتقن فن ضبط هوامش الصفحات وتخصيص الرؤوس والتذييلات في ملفات PDF باستخدام Aspose.PDF لـ .NET. اتبع هذا الدليل المفصل لتحسين تناسق تخطيط المستند."
"title": "Aspose.PDF .NET - تعيين هوامش PDF وتخصيص الرؤوس والتذييلات"
"url": "/ar/net/document-manipulation/aspose-pdf-net-master-pdfs-margins-headers-footers/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.PDF .NET: تعيين هوامش PDF وتخصيص الرؤوس والتذييلات

## مقدمة
إنشاء مستندات PDF احترافية أمرٌ أساسي، سواءً كنت تُنشئ تقارير أو فواتير أو مواد تسويقية. قد يكون ضمان تناسق تخطيطات الصفحات، بما في ذلك الهوامش والرؤوس والتذييلات، أمرًا صعبًا. يُرشدك هذا البرنامج التعليمي إلى كيفية استخدام Aspose.PDF لـ .NET لضبط هوامش الصفحات وتخصيص الرؤوس والتذييلات بسلاسة في ملفات PDF.

بحلول نهاية هذه المقالة، سوف تتعلم كيفية:
- تعيين هوامش الصفحة المخصصة
- إضافة محتوى نصي إلى العناوين
- إدراج الجداول مع النص في التذييلات
- تخصيص حدود الجدول والحشو

دعونا نلقي نظرة على المتطلبات الأساسية قبل أن نبدأ في تنفيذ هذه الميزات.

### المتطلبات الأساسية
للمتابعة، تأكد من أن لديك:
- **مكتبة Aspose.PDF لـ .NET**:قم بتثبيت Aspose.PDF لـ .NET عبر مديري الحزم أو NuGet.
- **بيئة التطوير**:استخدم بيئة تطوير .NET مثل Visual Studio أو VS Code مع دعم C#.
- **المعرفة الأساسية بلغة C#**:إن المعرفة بقواعد لغة C# ومبادئ البرمجة الموجهة للكائنات أمر مفيد.

## إعداد Aspose.PDF لـ .NET

### تثبيت
قم بتثبيت Aspose.PDF لـ .NET باستخدام إحدى الطرق التالية:

**.NET CLI**
```bash
dotnet add package Aspose.PDF
```

**وحدة تحكم مدير الحزم**
```powershell
Install-Package Aspose.PDF
```

**واجهة مستخدم مدير الحزم NuGet**
ابحث عن "Aspose.PDF" في NuGet Package Manager وقم بتثبيت الإصدار الأحدث.

### الحصول على الترخيص
لاستخدام Aspose.PDF، يمكنك:
- ابدأ بـ **نسخة تجريبية مجانية** لاختبار قدراتها.
- احصل على **رخصة مؤقتة** لإجراء اختبار موسع.
- قم بشراء ترخيص للوصول الكامل دون قيود.

للحصول على تفاصيل الترخيص، قم بزيارة [صفحة شراء Aspose](https://purchase.aspose.com/buy).

### التهيئة الأساسية
لبدء استخدام Aspose.PDF في مشروعك:
```csharp
using Aspose.Pdf;

// تهيئة كائن المستند
document doc = new Document();
```

## دليل التنفيذ
سنقوم بتقسيم الميزات إلى أقسام منطقية لتسهيل الفهم والتنفيذ.

### ضبط هوامش الصفحة (H2)
#### ملخص
يضمن ضبط هوامش الصفحات توحيدًا في مستندات PDF. إليك كيفية تحديد الهوامش باستخدام Aspose.PDF لـ .NET.

##### التنفيذ خطوة بخطوة
1. **تهيئة كائن المستند**
   ابدأ بإنشاء جديد `Document` الكائن الذي يعمل بمثابة الحاوية لمحتوى PDF الخاص بك.
2. **إضافة صفحة وتعيين الهوامش**
   أضف صفحة إلى مستندك وحدد هوامشها باستخدام `MarginInfo`.
```csharp
using Aspose.Pdf;

public class SetPageMargins {
    public static void Run() {
        // تهيئة كائن المستند
        Document doc = new Document();
        
        // إضافة صفحة جديدة
        Page page = doc.Pages.Add();
        
        // إنشاء MarginInfo لتعيين الهوامش
        MarginInfo marginInfo = new MarginInfo {
            Top = 90,
            Bottom = 50,
            Left = 50,
            Right = 50
        };
        
        // تعيين معلومات الهامش للصفحة
        page.PageInfo.Margin = marginInfo;
    }
}
```
**توضيح**: 
- `MarginInfo` يسمح لك بتحديد الهوامش العلوية والسفلية واليسرى واليمنى.
- تكون هذه القيم بالنقاط (1 نقطة = 1/72 بوصة).

### إضافة محتوى الرأس (H2)
#### ملخص
تُوفّر العناوين السياق في أعلى كل صفحة. إليك كيفية إضافة نص إلى عنوان ملف PDF.

##### التنفيذ خطوة بخطوة
1. **تهيئة المستند وإضافة الصفحة**
   كما في السابق، ابدأ بإنشاء مستندك وإضافة صفحة جديدة.
2. **إنشاء محتوى الرأس**
   يستخدم `HeaderFooter` لتحديد ما يوضع في العنوان.
```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

public class AddHeaderContent {
    public static void Run() {
        // تهيئة كائن المستند وإضافة الصفحة
        Document doc = new Document();
        Page page = doc.Pages.Add();
        
        // إنشاء HeaderFooter للرأس
        HeaderFooter hfFirst = new HeaderFooter { MarginLeft = 50, MarginRight = 50 };
        page.Header = hfFirst;
        
        // إضافة نص إلى الرأس
        TextFragment t1 = new TextFragment("Report Title") {
            TextState = {
                Font = FontRepository.FindFont("Arial"),
                FontSize = 16,
                ForegroundColor = Aspose.Pdf.Color.Black,
                FontStyle = FontStyles.Bold,
                HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center,
                LineSpacing = 5f
            }
        };
        
hfFirst.Paragraphs.Add(t1);
        
        TextFragment t2 = new TextFragment("Report_Name") {
            TextState = {
                Font = FontRepository.FindFont("Arial"),
                ForegroundColor = Aspose.Pdf.Color.Black,
                HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center,
                LineSpacing = 5f,
                FontSize = 12
            }
        };
        
hfFirst.Paragraphs.Add(t2);
    }
}
```
**توضيح**: 
- `HeaderFooter` يتم استخدامه لتحديد محتوى الرأس.
- يتم تكوين خصائص النص مثل الخط والحجم واللون والمحاذاة باستخدام `TextFragment`.

### إضافة محتوى التذييل باستخدام الجدول (H2)
#### ملخص
يمكن أن تحتوي التذييلات على معلومات إضافية، مثل أرقام الصفحات أو التواريخ. لنُدرج جدولاً في التذييل.

##### التنفيذ خطوة بخطوة
1. **تهيئة المستند وإضافة الصفحة**
   ابدأ بإنشاء كائن المستند الخاص بك وإضافة صفحة جديدة.
2. **إنشاء محتوى التذييل باستخدام الجدول**
   يستخدم `HeaderFooter` لإعداد التذييل وإضافة `Table`.
```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

public class AddFooterContentWithTable {
    public static void Run() {
        // تهيئة كائن المستند وإضافة الصفحة
        Document doc = new Document();
        Page page = doc.Pages.Add();
        
        // إنشاء HeaderFooter للتذييل
        HeaderFooter hfFoot = new HeaderFooter { MarginLeft = 50, MarginRight = 50 };
        page.Footer = hfFoot;
        
        // إضافة جدول إلى مجموعة فقرات التذييل
        Table tab2 = new Table {
            ColumnWidths = "165 172 165" // تعيين عرض الأعمدة
        };
        
hfFoot.Paragraphs.Add(tab2);
        
        // إنشاء وإضافة صفوف تحتوي على خلايا تحتوي على أجزاء نصية
        Row row3 = tab2.Rows.Add();
        
        TextFragment t3 = new TextFragment("Generated on test date");
        TextFragment t4 = new TextFragment("Report Name");
        TextFragment t5 = new TextFragment("Page $p of $P");

        // تكوين محاذاة الخلايا وإضافة أجزاء نصية
        row3.Cells[0].Alignment = Aspose.Pdf.HorizontalAlignment.Left;
        row3.Cells.Add(t3);
        
        row3.Cells[1].Alignment = Aspose.Pdf.HorizontalAlignment.Center;
        row3.Cells.Add(t4);

        row3.Cells[2].Alignment = Aspose.Pdf.HorizontalAlignment.Right;
        row3.Cells.Add(t5);
    }
}
```
**توضيح**: 
- أ `Table` تمت إضافته إلى التذييل، مما يسمح بعرض البيانات المنظمة.
- `$p` و `$P` هي عناصر نائبة لرقم الصفحة الحالية وإجمالي الصفحات.

### إضافة جدول بحدود مخصصة (H2)
#### ملخص
الجداول أساسية لعرض البيانات المنظمة. لنقم بتخصيص حدود الجداول وحشوها.

##### التنفيذ خطوة بخطوة
1. **تهيئة المستند وإضافة الصفحة**
   كما هو الحال دائمًا، ابدأ بإنشاء كائن المستند وإضافة صفحة جديدة.
2. **إنشاء جدول وتخصيصه**
   قم بتحديد عرض الأعمدة، وتعيين حشو الخلايا الافتراضي، وتخصيص الحدود.
```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;

public class AddCustomTable {
    public static void Run() {
        // تهيئة كائن المستند
        Document doc = new Document();
        
        // أضف صفحة
        Page page = doc.Pages.Add();
        
        // إنشاء جدول وتعيين عرض الأعمدة
        Table table = new Table {
            ColumnWidths = "100 200 100",
            DefaultCellPadding = new MarginInfo(10, 5, 10, 5)
        };
        
        // تخصيص الحدود للجدول والخلايا
        table.Border = new BorderInfo(BorderSide.All, .5f, Aspose.Pdf.Color.Black);
        table.DefaultCellBorder = new BorderInfo(BorderSide.All, .2f, Aspose.Pdf.Color.Gray);
        
        // إضافة صفوف تحتوي على بيانات
        Row row1 = table.Rows.Add();
        row1.Cells.Add("Header 1");
        row1.Cells[0].Background = Color.LightGray;
        row1.Cells.Add("Header 2");
        row1.Cells.Add("Header 3");
        
        Row row2 = table.Rows.Add();
        row2.Cells.Add("Data 1");
        row2.Cells.Add("Data 2");
        row2.Cells.Add("Data 3");

        // أضف الجدول إلى مجموعة فقرات الصفحة
        page.Paragraphs.Add(table);
    }
}
```
**توضيح**: 
- ال `Table` يتم استخدام الكائن بعرض أعمدة محدد وحشو خلية.
- يتم تخصيص الحدود لكل من الجدول والخلايا الفردية باستخدام `BorderInfo`.
- تمت إضافة الصفوف وخلايا البيانات لعرض المعلومات المنظمة.

### خاتمة
يوضح هذا الدليل بالتفصيل كيفية ضبط هوامش الصفحات، وإضافة رؤوس/تذييلات الصفحات، وتخصيص الجداول في ملفات PDF باستخدام Aspose.PDF لـ .NET. باتباع هذه الخطوات، يمكنك تحسين تخطيطات المستندات وتحسين عرض محتوى PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}