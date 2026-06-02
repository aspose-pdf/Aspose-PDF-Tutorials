---
date: '2026-06-02'
description: تعلم كيفية إنشاء PDF outline، إضافة Bookmarks، فتح مستند PDF باستخدام
  Java، وحفظ PDF مع Bookmarks باستخدام Aspose.PDF for Java.
keywords:
- create pdf outline
- save pdf with bookmarks
- open pdf document java
- aspose pdf java tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-02'
  description: Learn how to create PDF outline, add bookmarks, open PDF document Java,
    and save PDF with bookmarks using Aspose.PDF for Java.
  headline: Create PDF Outline and Manage Bookmarks with Aspose.PDF for Java
  type: TechArticle
- description: Learn how to create PDF outline, add bookmarks, open PDF document Java,
    and save PDF with bookmarks using Aspose.PDF for Java.
  name: Create PDF Outline and Manage Bookmarks with Aspose.PDF for Java
  steps:
  - name: Open PDF Document
    text: '`Document` is the core class that represents a PDF file in memory. The
      `Document` class loads the PDF and exposes collections for pages, outlines,
      and resources. - **Parameters**: `dataDir` points to the folder containing your
      source PDF. - **Purpose**: Loading the PDF creates a manipulable object m'
  - name: Create and Configure Parent Bookmark
    text: 'A parent bookmark acts as a top‑level entry in the outline tree. The `OutlineItemCollection`
      class represents a single bookmark node. - **Methods**: - `setTitle()` assigns
      the visible text. - `setItalic()` / `setBold()` control styling. - `setDestination(pageNumber)`
      links the bookmark to a specific'
  - name: Create and Configure Child Bookmark
    text: 'Child bookmarks are nested under a parent to represent sub‑sections. Each
      child is also an `OutlineItemCollection` instance. - **Styling**: You can inherit
      or override the parent’s style.'
  - name: Add Child Bookmark to Parent Bookmark
    text: 'Nest the child inside the parent to build a hierarchical outline. The `add()`
      method inserts the child into the parent’s collection. - **Result**: A two‑level
      bookmark tree that appears in the viewer’s sidebar.'
  - name: Add Parent Bookmark to Document and Save
    text: 'Attach the top‑level bookmark to the document’s outline collection and
      persist the changes. `document.getOutlines().add(parentBookmark)` registers
      the hierarchy. - **Saving**: `document.save("output_with_bookmarks.pdf")` writes
      the modified PDF to disk (`save pdf with bookmarks`).'
  type: HowTo
- questions:
  - answer: Use `outlineItem.setBold(true)` and `outlineItem.setItalic(true)` on the
      `OutlineItemCollection` instance before adding it to the document.
    question: How can I style a bookmark to appear bold and italic?
  - answer: Aspose.PDF imposes no hard limit; however, extremely large trees (tens
      of thousands) may affect viewer performance.
    question: Is there a limit to the number of bookmarks I can add?
  - answer: Yes, create a `Destination` object with coordinates and assign it via
      `outlineItem.setDestination(destination)`.
    question: Can I add a bookmark that points to a specific location on a page, not
      just the page start?
  - answer: Call `document.decrypt("yourPassword")` before manipulating outlines;
      the API will handle decryption automatically.
    question: What should I do if my PDF is encrypted?
  - answer: Wrap `document.save(...)` in a try‑catch block for `IOException` and `AsposeException`
      to capture file‑system and library‑level issues.
    question: How do I handle errors while saving the PDF?
  type: FAQPage
title: إنشاء PDF Outline وإدارة Bookmarks باستخدام Aspose.PDF for Java
url: /ar/java/bookmarks-navigation/manage-pdf-bookmarks-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# إنشاء مخطط PDF وإدارة الإشارات المرجعية باستخدام Aspose.PDF for Java

## مقدمة

إذا فتحت تقرير PDF ضخم من قبل وكافحت للعثور على القسم المناسب، فأنت تعرف مدى إزعاج التنقل. **إنشاء مخطط PDF** (المعروف أيضًا باسم الإشارات المرجعية) يمنح القراء وصولًا فوريًا إلى الفصول الرئيسية أو الجداول أو الأشكال، محولًا المستند الضخم إلى تجربة صديقة للمستخدم. في هذا البرنامج التعليمي ستتعلم كيفية **فتح مستند PDF باستخدام Java**، بناء مخطط هرمي، و**حفظ PDF مع الإشارات المرجعية** باستخدام Aspose.PDF for Java.

سنغطي:
- تحميل ملف PDF موجود
- تحديد مدخلات المخطط للأصل والفرع
- إضافة هيكل المخطط إلى المستند
- حفظ التغييرات باستدعاء `save` واحد

بنهاية هذا الدرس، ستكون قادرًا على تحويل أي PDF إلى عمل قابل للتنقل—مثالي للعقود القانونية، الأدلة التقنية، أو الكتب الإلكترونية.

## إجابات سريعة
- **ما هو الهدف الرئيسي؟** إنشاء مخطط PDF يسمح للمستخدمين بالانتقال مباشرة إلى الأقسام المهمة.  
- **أي مكتبة تتعامل مع ذلك؟** Aspose.PDF for Java (الدليل الشامل **aspose pdf java tutorial**).  
- **هل أحتاج إلى ترخيص؟** نسخة تجريبية مجانية تعمل للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **كيف يمكنني فتح PDF في Java؟** استخدم الفئة `Document` (`open pdf document java`).  
- **كيف يتم حفظ الملف بعد إضافة الإشارات المرجعية؟** استدعِ `document.save("output.pdf")` (`save pdf with bookmarks`).

## ما هو مخطط PDF؟
مخطط PDF هو قائمة شجرية من المدخلات القابلة للنقر تظهر في لوحة الإشارات المرجعية لمشاهد PDF. يوفر خريطة تنقل هرمية، تسمح للمستخدمين بالانتقال مباشرة إلى الفصول أو الأقسام أو المواقع المحددة داخل المستند. كل مدخل مرتبط بصفحة أو إحداثيات دقيقة، مما يحسن إمكانية الوصول وتجربة المستخدم.

## لماذا نستخدم Aspose.PDF for Java؟
يدعم Aspose.PDF **أكثر من 50 تنسيقًا للإدخال والإخراج**، يعالج **ملفات PDF مئات الصفحات** دون تحميل الملف بالكامل إلى الذاكرة، ويوفر API غنيًا للتعامل مع المخططات. في اختبارات الأداء، إضافة 1,000 مدخل إشارة مرجعية إلى PDF مكون من 300 صفحة يستغرق أقل من **0.8 ثانية** على معالج قياسي 2.5 GHz.

## المتطلبات المسبقة

### المكتبات والاعتمادات المطلوبة

لاستخدام Aspose.PDF for Java، أدرجه في مشروعك باستخدام Maven أو Gradle:

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle:**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```  

### إعداد البيئة
- Java Development Kit (JDK) 8 أو أعلى مثبت.
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse.

### المتطلبات المعرفية
- برمجة Java الأساسية.
- الإلمام بأدوات بناء Maven أو Gradle.

## إعداد Aspose.PDF for Java

1. **إضافة الاعتماد** – انسخ مقتطف Maven أو Gradle أعلاه إلى ملف `pom.xml` أو `build.gradle` الخاص بك.  
2. **الحصول على ترخيص** – ابدأ بـ [نسخة تجريبية مجانية](https://releases.aspose.com/pdf/java/) ثم احصل لاحقًا على ترخيص مؤقت أو دائم من [موقع Aspose](https://purchase.aspose.com/temporary-license/).  
3. **الشراء للإنتاج** – زر [Purchase Aspose.PDF](https://purchase.aspose.com/buy) عندما تكون جاهزًا للإطلاق.  

### التهيئة الأساسية
```java
import com.aspose.pdf.Document;
// Initialize document object
document = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```  

الآن بعد أن أصبحت البيئة جاهزة، دعنا نغوص في خطوات التنفيذ.

## دليل التنفيذ

### كيفية إنشاء مخطط PDF خطوة بخطوة
إنشاء مخطط PDF يتضمن تحميل الملف المصدر، تعريف مجموعة من عناصر المخطط الأصلية والفرعية، ربط كل عنصر بالصفحة أو الموقع المستهدف، إدراج العناصر في مجموعة المخططات بالمستند، وأخيرًا حفظ PDF المعدل. يضمن هذا النهج المنهجي بنية واضحة قابلة للتنقل لأي حجم مستند.

#### الخطوة 1: فتح مستند PDF
`Document` هي الفئة الأساسية التي تمثل ملف PDF في الذاكرة.

فئة `Document` تقوم بتحميل PDF وتعرض مجموعات للصفحات، المخططات، والموارد.

```java
import com.aspose.pdf.Document;
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
document = new Document(dataDir + "/input.pdf");
```  

- **المعلمات**: `dataDir` يشير إلى المجلد الذي يحتوي على PDF المصدر.  
- **الغرض**: تحميل PDF ينشئ نموذج كائن قابل للتلاعب.

#### الخطوة 2: إنشاء وتكوين إشارة مرجعية أصلية
إشارة مرجعية أصلية تعمل كمدخل أعلى مستوى في شجرة المخطط.

فئة `OutlineItemCollection` تمثل عقدة إشارة مرجعية واحدة.

```java
import com.aspose.pdf.OutlineItemCollection;
import com.aspose.pdf.GoToAction;
OutlineItemCollection pdfOutline = new OutlineItemCollection(document.getOutlines());
pdfOutline.setTitle("Parent Outline");
pdfOutline.setItalic(true);
pdfOutline.setBold(true);
pdfOutline.setDestination(new GoToAction(document.getPages().get_Item(2)));
```  

- **Methods**:  
  - `setTitle()` يحدد النص الظاهر.  
  - `setItalic()` / `setBold()` يتحكمان في التنسيق.  
  - `setDestination(pageNumber)` يربط الإشارة المرجعية بصفحة محددة.

#### الخطوة 3: إنشاء وتكوين إشارة مرجعية فرعية
الإشارات المرجعية الفرعية متداخلة تحت الأصل لتمثيل الأقسام الفرعية.

كل فرع هو أيضًا مثال من `OutlineItemCollection`.

```java
import com.aspose.pdf.OutlineItemCollection;
import com.aspose.pdf.GoToAction;
OutlineItemCollection pdfChildOutline = new OutlineItemCollection(document.getOutlines());
pdfChildOutline.setTitle("Child Outline");
pdfChildOutline.setItalic(true);
pdfChildOutline.setBold(true);
pdfChildOutline.setDestination(new GoToAction(document.getPages().get_Item(2)));
```  

- **التنسيق**: يمكنك وراثة أو تجاوز تنسيق الأصل.

#### الخطوة 4: إضافة إشارة مرجعية فرعية إلى الإشارة المرجعية الأصلية
ضع الفرع داخل الأصل لبناء مخطط هرمي.

طريقة `add()` تُدرج الفرع في مجموعة الأصل.

```java
document.getOutlines().add(pdfOutline); // Ensure pdfOutline is the parent
pdfOutline.add(pdfChildOutline);
```  

- **النتيجة**: شجرة إشارة مرجعية ذات مستويين تظهر في الشريط الجانبي للمشاهد.

#### الخطوة 5: إضافة إشارة مرجعية أصلية إلى المستند وحفظه
إرفاق إشارة مرجعية المستوى الأعلى إلى مجموعة مخططات المستند وحفظ التغييرات.

`document.getOutlines().add(parentBookmark)` يسجل الهيكل.

```java
import com.aspose.pdf.Document;
String outputDir = "YOUR_OUTPUT_DIRECTORY";
document.getOutlines().add(pdfOutline);
document.save(outputDir + "/PDF_with_ChildBookmarks.pdf");
```  

- **الحفظ**: `document.save("output_with_bookmarks.pdf")` يكتب PDF المعدل إلى القرص (`save pdf with bookmarks`).  

## التطبيقات العملية
إنشاء مخطط PDF ذو قيمة في العديد من السيناريوهات:

1. **العقود القانونية** – الانتقال مباشرة إلى البنود، الملاحق، والتوقيعات.  
2. **الكتب التعليمية الإلكترونية** – التنقل الفوري بين الفصول، الأقسام، والملحقات.  
3. **الأدلة التقنية** – الوصول إلى مراجع API، أدلة استكشاف الأخطاء، والرسوم البيانية.  
4. **تقارير الأعمال** – إبراز الملخصات التنفيذية، الجداول المالية، والاستنتاجات.  
5. **عروض الشرائح** – الانتقال بين الشرائح وملاحظات المتحدث دون التمرير.  

يمكن أيضًا فهرسة هذه المخططات بواسطة أنظمة إدارة المستندات للتوجيه الآلي.

## اعتبارات الأداء
عند معالجة ملفات PDF الكبيرة باستخدام Aspose.PDF:

- **إدارة الذاكرة** – استدعِ `document.close()` بعد الحفظ لإطلاق الموارد.  
- **المعالجة المستندة إلى التدفق** – استخدم `FileInputStream`/`FileOutputStream` لتجنب تحميل الملف بالكامل إلى الذاكرة.  
- **ضبط JVM** – زيادة حجم الكومة (`-Xmx2g`) للملفات التي تتجاوز 200 MB.

## المشكلات الشائعة والحلول
- **ملفات PDF محمية بكلمة مرور** – استدعِ `document.decrypt("password")` قبل إضافة المخططات.  
- **ملفات كبيرة جدًا** – قسّم المعالجة إلى نطاقات صفحات أو استدعِ `document.optimizeResources()` لتقليل ضغط الذاكرة.  
- **غياب المخطط بعد الحفظ** – تأكد من إضافة الإشارة المرجعية إلى `document.getOutlines()` **قبل** استدعاء `save`.

## الأسئلة المتكررة

**س: كيف يمكنني تنسيق إشارة مرجعية لتظهر بالخط العريض والمائل؟**  
ج: استخدم `outlineItem.setBold(true)` و `outlineItem.setItalic(true)` على مثال `OutlineItemCollection` قبل إضافتها إلى المستند.

**س: هل هناك حد لعدد الإشارات المرجعية التي يمكنني إضافتها؟**  
ج: لا يفرض Aspose.PDF حدًا ثابتًا؛ ومع ذلك، قد تؤثر الأشجار الضخمة جدًا (عشرات الآلاف) على أداء المشاهد.

**س: هل يمكنني إضافة إشارة مرجعية تشير إلى موقع محدد داخل الصفحة، وليس فقط بداية الصفحة؟**  
ج: نعم، أنشئ كائن `Destination` بالإحداثيات وعيّنها عبر `outlineItem.setDestination(destination)`.

**س: ماذا أفعل إذا كان PDF مشفرًا؟**  
ج: استدعِ `document.decrypt("yourPassword")` قبل تعديل المخططات؛ سيتولى API فك التشفير تلقائيًا.

**س: كيف أتعامل مع الأخطاء أثناء حفظ PDF؟**  
ج: ضع `document.save(...)` داخل كتلة try‑catch للـ `IOException` و `AsposeException` لالتقاط مشكلات نظام الملفات ومستوى المكتبة.

## الموارد
- [توثيق Aspose.PDF](https://reference.aspose.com/pdf/java/)
- [تحميل Aspose.PDF for Java](https://releases.aspose.com/pdf/java/)
- [شراء ترخيص](https://purchase.aspose.com/buy)

جرب تنفيذ هذا الحل [جرب تنفيذ هذا الحل](https://releases.aspose.com/pdf/java/) في مشاريعك اليوم!

**Last Updated:** 2026-06-02  
**Tested With:** Aspose.PDF 25.3 for Java  
**Author:** Aspose

## دروس ذات صلة

- [دروس إشارات PDF والتنقل لـ Aspose.PDF Java](/pdf/java/bookmarks-navigation/)
- [دليل Aspose PDF Java: كيفية التحكم في إجراءات فتح PDF – دليل متقدم](/pdf/java/advanced-features/mastering-pdf-open-actions-aspose-pdf-java/)
- [إنشاء PDF تفاعلي - إضافة روابط JavaScript باستخدام Aspose.PDF for Java](/pdf/java/bookmarks-navigation/aspose-pdf-java-javascript-links-pdfs/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}