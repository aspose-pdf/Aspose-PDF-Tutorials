---
date: '2026-05-28'
description: تعلم كيفية ضبط عرض صفحة واحدة PDF، وتغيير تفضيلات المشاهد، وتحرير العلامات
  المرجعية، وتكوين إعدادات PDF باستخدام Aspose.PDF for Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: عرض صفحة واحدة PDF في Java – تغيير التخطيط وتحرير العلامات المرجعية
url: /ar/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# عرض صفحة واحدة PDF في Java – تغيير التخطيط وتعديل الإشارات المرجعية

## مقدمة
عند فتح القراء لملف PDF كبير، قد يكون تخطيط العارض الافتراضي يتنقل باستمرار، مما يصعب التركيز على صفحة واحدة. من خلال تكوين إعداد **single page view pdf**، تجبر العارض على عرض صفحة واحدة في كل مرة، وهو مثالي للتقارير، والكتب الإلكترونية، والكتالوجات. في هذا الدرس ستتعلم أيضًا كيفية تعديل إشارات PDF المرجعية الموجودة، وتعيين وجهات الإشارات أثناء إنشاء المستند، وتعديل تفضيلات العارض الأخرى باستخدام Aspose.PDF for Java. في النهاية ستحصل على تحكم كامل في التنقل، ودقة الإشارات، وتخطيط الشاشة.

**ما ستتعلمه**
- كيفية تعديل إشارات PDF المرجعية الموجودة لتشير إلى بداية الصفحة.  
- كيفية تعيين وجهات الإشارات أثناء إنشاء PDF.  
- كيفية تغيير تفضيلات العارض مثل تخطيط الصفحة الواحدة.  
- نصائح عملية لتحميل مستند PDF في Java وتحسين الأداء.

### إجابات سريعة
- **ما هي الطريقة الأساسية لتمكين عرض صفحة واحدة PDF؟** استدعِ `PdfContentEditor.changeViewerPreference()` مع `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **هل يمكن تعديل وجهات الإشارات بعد إنشاء PDF؟** نعم – قم بتحميل المستند، استرجع المخطط، وعيّن `ExplicitDestination` جديد.  
- **هل أحتاج إلى ترخيص لهذه الميزات؟** نسخة تجريبية مجانية تكفي للتقييم؛ الترخيص الكامل يزيل جميع القيود.  
- **ما هو الاعتماد Maven المطلوب؟** `com.aspose:aspose-pdf:25.3` (أو أحدث).  
- **هل هذا متوافق مع Java 11 وما فوق؟** بالتأكيد – Aspose.PDF يدعم Java 8+.

## ما هو “تغيير تخطيط صفحة PDF”؟
تغيير تخطيط صفحة PDF يتحكم في كيفية عرض الصفحات في العارض—صفحة واحدة، مستمر، عرض صفحتين، إلخ. تمكين **single page view pdf** يحسن القراءة للوثائق الطويلة ويضمن عرض كل صفحة بشكل منفصل، وهو مفيد بشكل خاص على الأجهزة المحمولة والأجهزة اللوحية.

## لماذا تعديل إشارات PDF المرجعية وتعيين وجهات الإشارات المرجعية؟
الإشارات المرجعية تعمل كفهرس ديناميكي. الوجهات الدقيقة تسمح للقراء بالقفز مباشرة إلى القسم المقصود، مما يلغي الحاجة للتمرير الزائد ويقلل من إحباط المستخدم. هذا يؤدي إلى تجربة تنقل أكثر سلاسة ورضا أعلى للكتابات التقنية، والكتالوجات، والكتب الرقمية.

## المتطلبات المسبقة
- **المكتبات والاعتمادات**: Aspose.PDF for Java v25.3 أو أحدث.  
- **البيئة**: JDK 8 أو أحدث، أداة بناء Maven أو Gradle.  
- **المعرفة**: برمجة Java أساسية وإلمام بمفاهيم PDF.

## إعداد Aspose.PDF لـ Java
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
**الحصول على الترخيص**: ابدأ بنسخة تجريبية مجانية أو اطلب ترخيصًا مؤقتًا للوصول إلى جميع الميزات. فكر في شراء ترخيص دائم للاستخدام الإنتاجي.

### التهيئة الأساسية
الفئة `Document` هي الكائن الأساسي في Aspose.PDF الذي يمثل ملف PDF في الذاكرة. بعد إنشاء نسخة، جميع عمليات القراءة/الكتابة تمر عبر هذا الكائن.  
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
`PdfContentEditor` هي فئة مساعدة تسمح لك بتعديل إعدادات العارض دون إعادة كتابة المستند بالكامل.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### تغيير تفضيلات المشاهد
لتمكين **single page view pdf**، استدعِ `changeViewerPreference()` مع قيمة الـ enum المناسبة. هذه العملية تحدث قاموس تفضيلات العارض الداخلي للـ PDF.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### حفظ المستند المحدث
بعد تعديل التفضيلات، استدعِ `save()` لكتابة التغييرات إلى القرص.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## كيفية تعديل إشارات PDF المرجعية
**الإجابة**: لتعديل الإشارات المرجعية الموجودة، حمّل الـ PDF باستخدام `Document`، استرجع مجموعة المخطط، حدد `OutlineItem` المطلوب، وعيّن `ExplicitDestination` جديد يشير إلى الصفحة والإحداثيات الصحيحة. بعد تحديث كل إشارة، احفظ المستند لتثبيت التغييرات. هذا يضمن توجيه المستخدمين بدقة إلى الأقسام المطلوبة دون تمرير إضافي.

#### الوصول إلى الإشارات المرجعية
`OutlineItemCollection` تمثل شجرة الإشارات المرجعية الهرمية. استخرجها من كائن `Document` للعمل مع الإدخالات الفردية.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### تعيين وجهة جديدة
`ExplicitDestination` يحدد الصفحة والموقع الدقيق الذي يجب أن تقفز إليه الإشارة. عيّنها إلى خاصية `Destination` للعنصر المخطط.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### حفظ التغييرات
ثبّت شجرة الإشارات المحدثة باستدعاء `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## كيفية تعيين وجهة الإشارة المرجعية أثناء إنشاء PDF
**الإجابة**: عند إنشاء PDF، يمكنك إنشاء إشارات مرجعية في الوقت الفعلي عن طريق إنشاء كائنات `OutlineItem`، تعيين عناوينها، وتعريف `ExplicitDestination` يستهدف صفحة معينة ووضع عرض محدد. أضف كل إشارة إلى مجموعة المخطط قبل الحفظ، بحيث يحتوي الملف الناتج على شجرة تنقل جاهزة للاستخدام.

#### إنشاء وتكوين الإشارة المرجعية
`OutlineItem` يمثل إدخال إشارة مرجعية واحد في مخطط PDF. عند بناء PDF من الصفر، أنشئ `OutlineItem` جديدًا وأضفه إلى مجموعة المخطط الخاصة بالمستند.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### تعريف وجهة الإشارة المرجعية
استخدم `ExplicitDestination.createFitH(page, top)` لتحديد العرض في أعلى الصفحة المستهدفة.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### إضافة وحفظ PDF
أخيرًا، أضف الإشارة إلى المخطط واحفظ المستند.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## تطبيقات عملية
1. **الكتب الرقمية** – تأكد من أن إشارة كل فصل تصل إلى أعلى الصفحة لتجربة قراءة سلسة.  
2. **الكتيبات التقنية** – التنقل الدقيق يساعد المهندسين على العثور على الأقسام بسرعة، خاصة في ملفات PDF الكبيرة.  
3. **كتالوجات المنتجات** – تخطيط الصفحة الواحدة يجعل تصفح الكتالوجات على الأجهزة اللوحية أكثر بديهية.

## اعتبارات الأداء
- **تحسين الموارد**: Aspose.PDF يمكنه معالجة ملفات PDF تصل إلى 2 GB دون تحميل الملف بالكامل إلى الذاكرة، بفضل بنية البث. استخدم `Document.optimizeResources()` لتقليل استهلاك الذاكرة أكثر.  
- **إدارة الذاكرة في Java**: أغلق التدفقات صراحةً واترك جامع القمامة يتولى تحرير الكائنات بعد المعالجة لتجنب تسرب الذاكرة.

## المشكلات الشائعة والحلول
- **الإشارات المرجعية لا تُحدَّث**: تأكد من تعديل الفهرس الصحيح للمخطط (`get_Item(1)` يشير إلى أول إشارة مرجعية من المستوى الأعلى).  
- **تفضيل المشاهد غير مطبق**: تأكد من استدعاء `editor.save()` بعد تغيير التفضيلات؛ وإلا ستبقى التغييرات في الذاكرة فقط.  
- **استثناءات الترخيص**: قد تضيف نسخة تجريبية علامة مائية؛ احصل على ترخيص كامل للإنتاج.

## الأسئلة المتكررة
**س: ما هي أسهل طريقة لتحميل مستند PDF في Java؟**  
ج: استخدم `new Document("path/to/file.pdf")`؛ Aspose.PDF يكتشف تنسيق الملف تلقائيًا.

**س: هل يمكنني تغيير تخطيط الصفحة دون استخدام PdfContentEditor؟**  
ج: نعم، يمكنك تعيين تفضيلات المشاهد مباشرة على كائن `Document` عبر `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**س: هل يؤثر تغيير تخطيط المشاهد على الطباعة؟**  
ج: تخطيط المشاهد يؤثر فقط على العرض على الشاشة؛ لا يغيّر مخرجات الطباعة.

**س: هل هناك حدود لعدد الإشارات المرجعية التي يمكن إنشاؤها؟**  
ج: لا حدود صريحة، لكن الأشجار الكبيرة جدًا قد تؤثر على الأداء؛ حافظ على تنظيمها.

**س: كيف أضمن دقة وجهات الإشارات بعد إضافة أو حذف صفحات؟**  
ج: أعد حساب الوجهات باستخدام فهارس الصفحات الحالية بعد أي تغييرات هيكلية.

## الموارد
- **التوثيق**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)  
- **التحميل**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)  
- **الشراء**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)  
- **تجربة مجانية**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)  
- **رخصة مؤقتة**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**آخر تحديث:** 2026-05-28  
**تم الاختبار مع:** Aspose.PDF for Java v25.3  
**المؤلف:** Aspose

## دروس ذات صلة

- [How to Change PDF Viewer Preferences Using Aspose.PDF for Java: A Comprehensive Guide](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [How to Create PDF Bookmarks and Manage Navigation Using Aspose.PDF for Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [PDF Bookmarks and Navigation Tutorials for Aspose.PDF Java](/pdf/java/bookmarks-navigation/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}