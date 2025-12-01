---
date: '2025-12-01'
description: تعرّف على كيفية إنشاء ملفات PDF قابلة للوصول، وإنشاء جداول PDF، ووضع
  علامات على ملفات PDF لتعمل مع قارئات الشاشة باستخدام Aspise.PDF للغة Java.
keywords:
- accessible PDFs with Java
- Aspose.PDF for Java
- tagged PDF creation
language: ar
title: إنشاء ملف PDF قابل للوصول مع محتوى مُوسوم في Java باستخدام Aspose.PDF
url: /java/advanced-features/create-accessible-pdfs-tagged-content-java-aspose-pdf/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# إنشاء PDF يمكن الوصول إليه مع محتوى معلم في Java باستخدام Aspose.PDF

إنشاء مستندات **PDF يمكن الوصول إليها** أمر أساسي لضمان أن جميع المستخدمين، بما في ذلك أولئك الذين يعتمدون على تقنيات المساعدة، يمكنهم قراءة محتواك والتفاعل معه. في هذا البرنامج التعليمي ستتعلم كيفية **إنشاء ملفات PDF يمكن الوصول إليها** مع محتوى معلم، إنشاء جداول PDF، وتعيين لغة المستند بحيث يمكن لقارئات الشاشة تفسير البنية بشكل صحيح.

## إجابات سريعة
- **ما المكتبة التي يجب استخدامها؟** Aspose.PDF for Java.  
- **كم من الوقت يستغرق التنفيذ؟** حوالي 15‑20 دقيقة لإنشاء PDF معلم أساسي.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتطوير؛ يلزم الحصول على ترخيص دائم للإنتاج.  
- **هل يمكنني إنشاء جداول؟** نعم – تتيح لك الـ API إنشاء وتنسيق جداول PDF مع بنية معلمة.  
- **كيف أجعل PDF قابلًا للقراءة بواسطة قارئات الشاشة؟** ضع العلامات على المحتوى، عيّن اللغة، وقدّم نصًا بديلًا للعناصر الهيكلية.

## ما هو “إنشاء PDF يمكن الوصول إليه”؟
**PDF يمكن الوصول إليه** يحتوي على بنية منطقية (علامات) تصف العناوين، الجداول، الفقرات، والعناصر الأخرى. تتيح هذه البنية لقارئات الشاشة وأدوات المساعدة الأخرى تقديم المستند بطريقة ذات معنى للمستخدمين ذوي الإعاقات البصرية أو المعرفية.

## لماذا نضع علامات على PDF؟
وضع العلامات على PDF (عملية **كيفية وضع علامات على PDF**) يمنحك:
- **تحسين التنقل** لقارئات الشاشة ومستخدمي لوحة المفاتيح.  
- **الامتثال** لمعايير WCAG 2.1 و PDF/UA الخاصة بإمكانية الوصول.  
- **تحسين قابلية البحث** لأن النص يُفهرس دلاليًا.  

## المتطلبات المسبقة
قبل أن تبدأ، تأكد من وجود:
- مجموعة تطوير جافا (JDK) مثبتة.  
- بيئة تطوير متكاملة مثل IntelliJ IDEA أو Eclipse.  
- معرفة أساسية بجافا وإلمام بمفاهيم PDF.  

### المكتبات والاعتمادات المطلوبة
أضف Aspose.PDF for Java إلى مشروعك باستخدام Maven أو Gradle.

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### الحصول على الترخيص
توفر Aspose.PDF for Java نسخة تجريبية مجانية. يمكنك الحصول على ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/). للاستخدام في الإنتاج، قم بشراء ترخيص كامل.

## إعداد Aspose.PDF for Java
إذا لم تكن تستخدم Maven/Gradle، حمّل ملف JAR من [موقع إصدارات Aspose](https://releases.aspose.com/pdf/java/) وأضفه إلى مسار بناء مشروعك.

إليك مقتطف بسيط يتحقق من إعدادك بإنشاء PDF فارغ:

```java
import com.aspose.pdf.Document;

public class PdfCreator {
    public static void main(String[] args) {
        // Initialize Aspose.PDF
        Document doc = new Document();
        
        // Save the empty document to check setup
        doc.save("output/EmptyDocument.pdf");
        
        System.out.println("Setup complete and document created successfully.");
    }
}
```

## دليل التنفيذ

### إنشاء PDF جديد بمحتوى معلم
**نظرة عامة** – المحتوى المعلم يوفر تسلسل هرمي منطقي يحسن إمكانية الوصول. الخطوات أدناه ترشدك إلى إنشاء PDF، تمكين العلامات، وتعبئة جدول منسق.

#### الخطوة 1: تهيئة المستند وتمكين العلامات
أولاً، أنشئ كائن `Document` واحصل على واجهة `ITaggedContent`. كما **نعيّن لغة PDF** (خطوة **تعيين لغة PDF**) حتى تعرف قارئات الشاشة لغة المستند.

```java
import com.aspose.pdf.*;

public class TaggedPdfCreator {
    public static void main(String[] args) {
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        // Create a new PDF document
        Document document = new Document();

        // Obtain tagged content
        ITaggedContent taggedContent = document.getTaggedContent();
        
        // Set the title and language for accessibility purposes
        taggedContent.setTitle("Example table row style");
        taggedContent.setLanguage("en-US");

        // Proceed to add structured elements
    }
}
```

#### الخطوة 2: إضافة عناصر البنية (كيفية إنشاء جدول PDF)
بعد ذلك، عرّف العنصر الجذري وأنشئ بنية جدول مع رأس، جسم، وتذييل. يوضح هذا **وظيفة إنشاء جدول PDF** مع الحفاظ على المحتوى معلم بالكامل.

```java
import com.aspose.pdf.tagged.logicalstructure.elements.bls.*;

// Get root structure element
StructureElement rootElement = taggedContent.getRootElement();

// Create a new table structure element
TableElement tableElement = taggedContent.createTableElement();
rootElement.appendChild(tableElement);

// Add header, body, and footer to the table
TableTHeadElement tableTHeadElement = tableElement.createTHead();
TableTBodyElement tableTBodyElement = tableElement.createTBody();
TableTFootElement tableTFootElement = tableElement.createTFoot();
```

#### الخطوة 3: تعبئة عناصر الجدول (تنسيق الصفوف لقارئ الشاشة PDF)
الآن نضيف الصفوف، ننسقها، ونقدّم نصًا بديلًا. يضمن النص البديل أن يكون الجدول مفهومًا لمستخدمي **قارئ الشاشة PDF**.

```java
int rowCount = 7;
int colCount = 3;

// Add a header row with column titles
TableTRElement headTrElement = tableTHeadElement.createTR();
headTrElement.setAlternativeText("Head Row");
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTHElement thElement = headTrElement.createTH();
    thElement.setText(String.format("Head %s", colIndex));
}

// Add rows to the table body with styled cells
for (int rowIndex = 0; rowIndex < rowCount; rowIndex++) {
    TableTRElement trElement = tableTBodyElement.createTR();
    trElement.setAlternativeText(String.format("Row %s", rowIndex));

    // Set row styles
    trElement.setBackgroundColor(Color.getLightSeaGreen());
    trElement.setBorder(new BorderInfo(BorderSide.All, 0.75F, Color.getDarkGray()));
    trElement.setDefaultCellBorder(new BorderInfo(BorderSide.All, 0.50F, Color.getBlue()));
    trElement.setMinRowHeight(100.0);
    trElement.setFixedRowHeight(120.0);

    // Set default text state for cells in this row
    TextState cellTextState = new TextState();
    cellTextState.setForegroundColor(Color.getRed());
    trElement.setDefaultCellTextState(cellTextState);

    // Add cells to the row
    for (int colIndex = 0; colIndex < colCount; colIndex++) {
        TableTDElement tdElement = trElement.createTD();
        tdElement.setText(String.format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}

// Add a footer row to the table
TableTRElement footTrElement = tableTFootElement.createTR();
footTrElement.setAlternativeText("Foot Row");
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTDElement tdElement = footTrElement.createTD();
    tdElement.setText(String.format("Foot %s", colIndex));
}
```

### حفظ مستند PDF
أخيرًا، احفظ المستند. الملف المحفوظ يحتفظ بجميع العلامات، إعدادات اللغة، وبنية الجدول، مما يجعله جاهزًا تمامًا لـ **إنشاء PDF يمكن الوصول إليه** للتوزيع.

```java
// Save the tagged PDF document
document.save(outputDir + "/StyleTableRow.pdf");
System.out.println("Document saved successfully.");
```

## تطبيقات عملية
إنشاء PDF يمكن الوصول إليه أمر حيوي في العديد من السيناريوهات الواقعية:

1. **المواد التعليمية** – توفير كتب ودروس شاملة لجميع الطلاب.  
2. **المنشورات الحكومية** – تلبية المتطلبات القانونية لإمكانية الوصول للوثائق العامة.  
3. **التقارير المؤسسية** – ضمان أن المساهمين والموظفين يمكنهم الوصول إلى القوائم المالية باستخدام قارئات الشاشة.  

## اعتبارات الأداء
عند العمل مع ملفات PDF كبيرة:

- راقب استهلاك الذاكرة؛ حرّر الموارد فور الانتهاء.  
- قلل عدد العناصر الديناميكية التي تضيفها.  
- اتبع أفضل ممارسات جافا لجمع القمامة وإعادة استخدام الكائنات.  

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| العلامات لا تظهر في قارئ PDF | تأكد من الحصول على `taggedContent` واستدعاء `setTitle`/`setLanguage` قبل إضافة العناصر. |
| خلايا الجدول تفتقد النص البديل | استخدم `setAlternativeText` على كل `TableTRElement` وعلى صفوف الرأس/التذييل. |
| الملفات الكبيرة تسبب OutOfMemoryError | عالج المستند على أقسام أو زد حجم ذاكرة JVM (`-Xmx`). |

## الأسئلة المتكررة

**س: كيف يمكنني التحقق من أن PDF الخاص بي قابل للوصول فعلاً؟**  
ج: استخدم أدوات مثل مدقق إمكانية الوصول في Adobe Acrobat أو افتح الملف باستخدام قارئ شاشة (NVDA، JAWS) لتأكيد التنقل الصحيح.

**س: هل تدعم Aspose.PDF لغات أخرى غير الإنجليزية؟**  
ج: نعم. عيّن رمز اللغة عبر `taggedContent.setLanguage("fr-FR")` للفرنسية، `es-ES` للإسبانية، إلخ.

**س: هل يمكنني إضافة صور بنص بديل إلى PDF معلم؟**  
ج: بالتأكيد. استخدم فئة `Image` واضبط خاصية `AlternativeText` لتوضيح المحتوى البصري.

**س: هل هناك حد لعدد الصفوف التي يمكنني إنشاؤها في جدول PDF؟**  
ج: لا حد صريح، لكن الجداول الضخمة قد تزيد استهلاك الذاكرة؛ فكر في التقسيم إلى صفحات أو تقسيم المستند.

**س: هل سيعمل PDF المُنشأ على جميع قارئات الشاشة؟**  
ج: عندما تُضبط العلامات، اللغة، والنص البديل بشكل صحيح، يكون PDF متوافقًا مع PDF/UA ويجب أن يكون قابلًا للقراءة بواسطة معظم قارئات الشاشة الرئيسية.

## الخلاصة
أصبح لديك الآن دليل شامل خطوة بخطوة لإنشاء مستندات **PDF يمكن الوصول إليها** مع محتوى معلم، إنشاء جداول منسقة، وضمان التوافق مع قارئات الشاشة. باستخدام Aspose.PDF for Java، يمكنك دمج إمكانية الوصول مباشرة في خط أنابيب إنشاء PDF الخاص بك، وتقديم محتوى شامل لكل الجمهور.

### الخطوات التالية
- استكشف ميزات العلامة الإضافية مثل العناوين، القوائم، والروابط.  
- دمج هذا التدفق العمل في خدمات جافا الحالية أو وظائف المعالجة الدفعية.  
- شارك تجاربك واسأل أسئلتك على [منتدى Aspose PDF](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**آخر تحديث:** 2025-12-01  
**تم الاختبار مع:** Aspose.PDF for Java 25.3  
**المؤلف:** Aspose