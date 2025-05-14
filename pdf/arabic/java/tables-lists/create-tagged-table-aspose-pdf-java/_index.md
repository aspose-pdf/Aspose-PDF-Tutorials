---
"date": "2025-04-14"
"description": "تعرّف على كيفية إنشاء وتكوين جداول مُعلّمة سهلة الوصول في مستندات PDF باستخدام Aspose.PDF لجافا. حسّن إمكانية الوصول إلى المستندات من خلال إرشادات خطوة بخطوة."
"title": "إنشاء جداول مُعلَّمة يمكن الوصول إليها في ملفات PDF باستخدام Aspose.PDF لـ Java"
"url": "/ar/java/tables-lists/create-tagged-table-aspose-pdf-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# إنشاء جداول مُعلَّمة يمكن الوصول إليها في ملفات PDF باستخدام Aspose.PDF لـ Java

إنشاء مستندات سهلة الوصول أمرٌ بالغ الأهمية لضمان تفاعل جميع المستخدمين، بغض النظر عن قدراتهم، بفعالية مع محتواك. سيرشدك هذا البرنامج التعليمي خلال إنشاء وتكوين الجداول داخل ملفات PDF المُعلَّمة باستخدام مكتبة Aspose.PDF القوية لجافا. باتباع هذه الخطوات، ستتعلم كيفية تحسين إمكانية الوصول إلى المستندات مع الاستفادة من ميزات Aspose.PDF القوية.

## ما سوف تتعلمه

- كيفية إعداد وتهيئة Aspose.PDF لـ Java
- عملية إنشاء جدول مُعَلَّم داخل مستند PDF
- تقنيات تكوين رؤوس الجداول وأجسامها وتذييلاتها
- إضافة سمات يمكن الوصول إليها لتحسين قابلية الاستخدام
- أفضل الممارسات لتحسين الأداء عند العمل مع مستندات كبيرة

دعونا نلقي نظرة على المتطلبات الأساسية التي ستحتاجها قبل أن نبدأ.

## المتطلبات الأساسية

لمتابعة هذا البرنامج التعليمي، تأكد من أن لديك:

- تم تثبيت Java Development Kit (JDK) على نظامك.
- بيئة التطوير المتكاملة (IDE) مثل IntelliJ IDEA أو Eclipse.
- المعرفة الأساسية ببرمجة Java والتعرف على مفاهيم PDF.

سنستخدم أيضًا Aspose.PDF لجافا. تأكد من إعداد المكتبات والتبعيات اللازمة في بيئة مشروعك.

## إعداد Aspose.PDF لـ Java

### تثبيت

يمكنك بسهولة دمج Aspose.PDF لجافا في مشروعك باستخدام Maven أو Gradle. فيما يلي تكوينات التبعيات لكلا نظامي البناء:

**مافن**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**جرادل**
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### الحصول على الترخيص

لاستخدام Aspose.PDF لجافا، يمكنك الحصول على نسخة تجريبية مجانية أو شراء النسخة الكاملة. إليك كيفية البدء:

- **نسخة تجريبية مجانية**:تنزيل ترخيص مؤقت من [نسخة تجريبية مجانية من Aspose](https://releases.aspose.com/pdf/java/).
- **شراء**:فكر في شراء ترخيص كامل للاستخدام التجاري في [شراء Aspose](https://purchase.aspose.com/buy).

### التهيئة الأساسية

قم بتهيئة مشروع Aspose.PDF الخاص بك عن طريق إنشاء مثيل لـ `Document` هذه الفئة هي بمثابة نقطة الدخول للعمل مع مستندات PDF.

```java
import com.aspose.pdf.Document;

// تهيئة مستند جديد
Document document = new Document();
```

## دليل التنفيذ

في هذا القسم، سنقوم بتقسيم العملية إلى خطوات منطقية لإنشاء جدول مُصنف وتكوينه داخل مستند PDF الخاص بك باستخدام Aspose.PDF.

### 1. إنشاء الهيكل الأساسي

ابدأ بإعداد الهيكل الأساسي لمستند PDF الذي قمت بوضع علامة عليه:

```java
import com.aspose.pdf.ITaggedContent;
import com.aspose.pdf.tagged.logicalstructure.elements.TableElement;

// تهيئة المحتوى المُوسوم
ITaggedContent taggedContent = document.getTaggedContent();
taggedContent.setTitle("Example Table in a Tagged PDF");
taggedContent.setLanguage("en-US");

// احصل على عنصر البنية الجذرية وقم بإنشاء TableElement جديد
StructureElement rootElement = taggedContent.getRootElement();
TableElement tableElement = taggedContent.createTableElement();
rootElement.appendChild(tableElement);
```

### 2. تكوين حدود الجدول

قم بتحديد حدود جدولك لتحسين الوضوح البصري:

```java
import com.aspose.pdf.BorderInfo;
import com.aspose.pdf.BorderSide;

// تعيين حدود للجدول بأكمله
tableElement.setBorder(new BorderInfo(BorderSide.All, 1.2F, Color.getDarkBlue()));
```

### 3. إعداد رأس الجدول (THead)

قم بإنشاء رأس الجدول الخاص بك وتكوينه لعرض عناوين الأعمدة:

```java
import com.aspose.pdf.tagged.logicalstructure.elements.TableTHeadElement;
import com.aspose.pdf.tagged.logicalstructure.elements.TableTHElement;

TableTHeadElement tableTHeadElement = tableElement.createTHead();
TableTRElement headTrElement = tableTHeadElement.createTR();
headTrElement.setAlternativeText("Header Row");
headTrElement.setBackgroundColor(Color.getLightGray());

int colCount = 4;
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTHElement thElement = headTrElement.createTH();
    thElement.setText(String.format("Header %s", colIndex));
    thElement.setBackgroundColor(Color.getGreenYellow());
    thElement.setBorder(new BorderInfo(BorderSide.All, 4.0F, Color.getLightGray()));
    thElement.setMargin(new MarginInfo(16.0, 2.0, 8.0, 2.0));
    thElement.setAlignment(HorizontalAlignment.Right);
}
```

### 4. تكوين نص الجدول (TBody)

املأ نص الجدول بالبيانات:

```java
import com.aspose.pdf.tagged.logicalstructure.elements.TableTBodyElement;
import com.aspose.pdf.tagged.logicalstructure.elements.TableTDElement;

TableTBodyElement tableTBodyElement = tableElement.createTBody();
int rowCount = 50;
for (int rowIndex = 0; rowIndex < rowCount; rowIndex++) {
    TableTRElement trElement = tableTBodyElement.createTR();
    trElement.setAlternativeText(String.format("Data Row %s", rowIndex));

    for (int colIndex = 0; colIndex < colCount; colIndex++) {
        int colSpan = 1;
        int rowSpan = 1;

        if (colIndex == 1 && rowIndex == 1) {
            colSpan = 2;
            rowSpan = 2;
        } else if (colIndex == 2 && (rowIndex == 1 || rowIndex == 2)) {
            continue;
        } else if (rowIndex == 2 && (colIndex == 1 || colIndex == 2)) {
            continue;
        }

        TableTDElement tdElement = trElement.createTD();
        tdElement.setText(String.format("Cell [%s, %s]", rowIndex, colIndex));
        tdElement.setBackgroundColor(Color.getYellow());
        tdElement.setBorder(new BorderInfo(BorderSide.All, 4.0F, Color.getGray()));
        tdElement.setMargin(new MarginInfo(8.0, 2.0, 8.0, 2.0));
        tdElement.setAlignment(HorizontalAlignment.Center);

        // تكوين حالة النص لمحتوى الخلية
        TextState cellTextState = new TextState();
        cellTextState.setForegroundColor(Color.getDarkBlue());
        cellTextState.setFontSize(7.5F);
        cellTextState.setFontStyle(FontStyles.Bold);
        cellTextState.setFont(FontRepository.findFont("Arial"));
        tdElement.setDefaultCellTextState(cellTextState);

        tdElement.isWordWrapped();
        tdElement.setVerticalAlignment(VerticalAlignment.Center);
        tdElement.setColSpan(colSpan);
        tdElement.setRowSpan(rowSpan);
    }
}
```

### 5. إعداد تذييل الجدول (TFoot)

أضف تذييلًا إلى جدولك للتلخيص أو للحصول على معلومات إضافية:

```java
import com.aspose.pdf.tagged.logicalstructure.elements.TableTFootElement;

TableTFootElement tableTFootElement = tableElement.createTFoot();
TableTRElement footTrElement = tableTFootElement.createTR();
footTrElement.setAlternativeText("Footer Row");
footTrElement.setBackgroundColor(Color.getLightSeaGreen());

for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTDElement tdElement = footTrElement.createTD();
    tdElement.setText(String.format("Footer %s", colIndex));
    tdElement.setAlignment(HorizontalAlignment.Center);
    tdElement.getStructureTextState().setFontSize(7F);
    tdElement.getStructureTextState().setFontStyle(FontStyles.Bold);
}
```

### 6. إضافة سمات إمكانية الوصول

قم بتعزيز إمكانية الوصول عن طريق إضافة سمة ملخص إلى الجدول الخاص بك:

```java
import com.aspose.pdf.tagged.logicalstructure.StructureAttributes;
import com.aspose.pdf.tagged.logicalstructure.StructureAttribute;
import com.aspose.pdf.tagged.logicalstructure.elements.TaggedPdfElements;

// إضافة وصف لإمكانية الوصول
StructureAttributes attributes = new StructureAttributes();
attributes.setLang("en-US");
taggedContent.setTagProperties(attributes);

// إضافة ملخص إلى الجدول
TableElement taggedTable = (TableElement) taggedContent.getTaggedPdfElements().get(TaggedPdfElements.Table);
taggedTable.setTitleAlternativeText("Summary of Data");
```

### 7. حفظ مستندك

وأخيرًا، احفظ مستندك:

```java
document.save("AccessibleTaggedTable.pdf");
```

## خاتمة

باتباع هذا البرنامج التعليمي، ستتعلم كيفية إنشاء جداول مُعلَّمة سهلة الوصول في ملفات PDF باستخدام Aspose.PDF لجافا. هذه العملية لا تُحسِّن سهولة استخدام مستنداتك فحسب، بل تضمن أيضًا الامتثال لمعايير إمكانية الوصول.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}