---
date: '2025-12-19'
description: تعرّف على كيفية تغيير تخطيط صفحات PDF، وتعديل إشارات PDF، وتخصيص إعدادات
  العارض باستخدام Aspose.PDF للغة Java. احكم التحكم في التنقل وتفضيلات التخطيط لتجربة
  مستخدم أكثر سلاسة.
keywords:
- edit PDF bookmarks Java
- Aspose.PDF viewer settings
- configure PDF navigation Java
title: 'تغيير تخطيط صفحة PDF في جافا - تعديل العلامات المرجعية والإعدادات'
url: /ar/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# تغيير تخطيط صفحة PDF في Java: تعديل العلامات المرجعية والإعدادات

## المقدمة
قد يكون التنقل في مستندات PDF المعقدة مرهقًا، خاصة عندما لا يتم تكوين إعداد **change PDF page layout** بشكل صحيح أو تشير العلامات المرجعية إلى المواقع الخاطئة. في هذا البرنامج التعليمي ستتعلم كيفية **change PDF page layout**، **edit PDF bookmarks**، و **configure PDF viewer settings** باستخدام Aspose.PDF for Java. في النهاية، ستحصل على سيطرة كاملة على التنقل، وجهات العلامات المرجعية، وكيفية عرض المستند للقراء.

**ما ستتعلمه**
- كيفية تعديل العلامات المرجعية الموجودة في PDF لتشير إلى بداية الصفحة.  
- كيفية تعيين وجهات العلامات المرجعية أثناء إنشاء PDF.  
- كيفية تغيير تفضيلات العارض مثل تخطيط الصفحة.  
- نصائح عملية لتحميل مستند PDF في Java وتحسين الأداء.

### إجابات سريعة
- **ما هي الطريقة الأساسية لتغيير تخطيط صفحة PDF؟** استخدم `PdfContentEditor.changeViewerPreference()` مع `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **هل يمكنني تعديل وجهات العلامات المرجعية بعد إنشاء PDF؟** نعم – قم بتحميل المستند، الوصول إلى المخطط، وتعيين `ExplicitDestination` جديد.  
- **هل أحتاج إلى ترخيص لهذه الميزات؟** النسخة التجريبية المجانية تعمل للتقييم؛ الترخيص الكامل يزيل جميع القيود.  
- **ما هي تبعية Maven المطلوبة؟** `com.aspose:aspose-pdf:25.3` (أو أحدث).  
- **هل هذا متوافق مع Java 11 وما فوق؟** بالتأكيد – Aspose.PDF يدعم Java 8+.

## ما هو “change PDF page layout”؟
تغيير تخطيط صفحة PDF يتحكم في كيفية عرض الصفحات في العارض—صفحة واحدة، مستمر، عرض صفحتين، إلخ. تعديل هذا الإعداد يحسن قابلية القراءة، خاصةً للتقارير أو الكتالوجات الطويلة.

## لماذا تعديل العلامات المرجعية في PDF وتعيين وجهات العلامات المرجعية؟
تعمل العلامات المرجعية كجدول محتويات. تضمن الوجهات الدقيقة أن يقفز القراء مباشرة إلى القسم المقصود، مما يقلل الإحباط ويحسن تجربة المستخدم العامة.

## المتطلبات المسبقة
- **المكتبات والتبعيات**: Aspose.PDF for Java v25.3 أو أحدث.  
- **البيئة**: JDK 8 أو أحدث، أداة بناء Maven أو Gradle.  
- **المعرفة**: برمجة Java الأساسية ومعرفة بمفاهيم PDF.

## إعداد Aspose.PDF for Java
### تثبيت Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### تثبيت Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**الحصول على الترخيص**: ابدأ بنسخة تجريبية مجانية أو اطلب ترخيصًا مؤقتًا للوصول إلى جميع الميزات. فكر في شراء ترخيص دائم للاستخدام في الإنتاج.

### التهيئة الأساسية
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## دليل التنفيذ
### كيفية تغيير تخطيط صفحة PDF في Java
**نظرة عامة**: تعديل تفضيلات العارض لعرض الصفحات بالطريقة التي تريدها.

#### تهيئة PdfContentEditor
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### تغيير تفضيلات العارض
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### حفظ المستند المحدث
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

### كيفية تعديل العلامات المرجعية في PDF
**نظرة عامة**: تعديل العلامات المرجعية الحالية لتشير بدقة إلى بداية صفحة معينة.

#### الوصول إلى العلامات المرجعية
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### تعيين وجهة جديدة
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### حفظ التغييرات
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

### كيفية تعيين وجهة العلامة المرجعية أثناء إنشاء PDF
**نظرة عامة**: إنشاء علامات مرجعية تقود المستخدمين مباشرة إلى المواقع المطلوبة في PDF تم إنشاؤه حديثًا.

#### إنشاء وتكوين العلامة المرجعية
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### تعريف وجهة العلامة المرجعية
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### إضافة وحفظ PDF
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## التطبيقات العملية
1. **الكتب الرقمية** – تأكد من أن كل علامة مرجعية للفصل تصل إلى أعلى الصفحة لتجربة قراءة سلسة.  
2. **الأدلة التقنية** – التنقل الدقيق يساعد المهندسين على العثور على الأقسام بسرعة، خاصةً في ملفات PDF الكبيرة.  
3. **كتالوجات المنتجات** – تخطيط الصفحة الواحدة يجعل تصفح الكتالوجات على الأجهزة اللوحية أكثر بديهية.

## اعتبارات الأداء
- **تحسين الموارد**: عند التعامل مع ملفات PDF الكبيرة، استخدم `Document.optimizeResources()` لتقليل استهلاك الذاكرة.  
- **إدارة ذاكرة Java**: أغلق التدفقات صراحةً ودع جامع القمامة يستعيد الكائنات بعد المعالجة.

## المشكلات الشائعة والحلول
- **عدم تحديث العلامات المرجعية**: تأكد من أنك تعدل الفهرس الصحيح للمخطط (`get_Item(1)` يشير إلى أول علامة مرجعية من المستوى الأعلى).  
- **عدم تطبيق تفضيل العارض**: تأكد من استدعاء `editor.save()` بعد تغيير التفضيلات؛ وإلا ستبقى التغييرات في الذاكرة فقط.  
- **استثناءات الترخيص**: قد تضيف نسخة الترخيص التجريبية علامات مائية؛ احصل على ترخيص كامل للإنتاج.

## الأسئلة المتكررة
**س: ما هي أسهل طريقة لتحميل مستند PDF في Java؟**  
ج: استخدم `new Document("path/to/file.pdf")`؛ Aspose.PDF يكتشف تنسيق الملف تلقائيًا.

**س: هل يمكنني تغيير تخطيط الصفحة دون استخدام PdfContentEditor؟**  
ج: نعم، يمكنك تعيين تفضيلات العارض مباشرةً على كائن `Document` عبر `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**س: هل يؤثر تغيير تخطيط العارض على الطباعة؟**  
ج: تخطيط العارض يؤثر فقط على العرض على الشاشة؛ ولا يغير مخرجات الطباعة.

**س: هل هناك حدود لعدد العلامات المرجعية التي يمكنني إنشاؤها؟**  
ج: لا يوجد حد صريح، لكن الأشجار المخططة الكبيرة جدًا قد تؤثر على الأداء؛ حافظ على تنظيمها.

**س: كيف أضمن دقة وجهات العلامات المرجعية بعد إضافة أو إزالة صفحات؟**  
ج: أعد حساب الوجهات باستخدام فهارس الصفحات الحالية بعد أي تغييرات هيكلية.

## الموارد
- **الوثائق**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **التنزيل**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **الشراء**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **التجربة المجانية**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **الترخيص المؤقت**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**آخر تحديث:** 2025-12-19  
**تم الاختبار مع:** Aspose.PDF for Java v25.3  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}