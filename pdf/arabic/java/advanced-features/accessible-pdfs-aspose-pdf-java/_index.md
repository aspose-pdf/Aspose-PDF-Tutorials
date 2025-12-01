---
date: '2025-12-01'
description: تعلم كيفية إنشاء ملفات PDF قابلة للوصول باستخدام Java و Aspose.PDF. يوضح
  لك هذا الدليل كيفية تعيين عنوان PDF واللغة، وإنشاء PDF معلم يحتوي على رؤوس وفقرات.
keywords:
- accessible PDFs
- Aspose.PDF for Java
- Java PDF generation
language: ar
title: إنشاء ملف PDF يمكن الوصول إليه في Java باستخدام Aspose.PDF – دليل كامل
url: /java/advanced-features/accessible-pdfs-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# إنشاء ملف PDF قابل للوصول في Java باستخدام Aspose.PDF – دليل كامل

في هذا الدرس ستقوم **بإنشاء ملفات PDF قابلة للوصول** باستخدام Aspose.PDF for Java. سنستعرض كيفية تعيين عنوان PDF، اللغة، وتوليد **PDF مع علامات** (tagged PDF) مع رؤوس صحيحة (H1‑H6) وبُنى الفقرات بحيث يمكن لقارئات الشاشة التنقل في ملفاتك بسهولة.

## ما ستتعلمه
- كيفية إعداد Aspose.PDF for Java في Maven أو Gradle.
- كيفية **تعيين عنوان PDF** و **تعيين لغة PDF** لتحسين إمكانية الوصول.
- كيفية **توليد محتوى PDF مع علامات** باستخدام العناوين والفقرات.
- كيفية حفظ المستند مع الحفاظ على جميع علامات إمكانية الوصول.

هيا نبدأ!

## إجابات سريعة
- **ما هي الفائدة الأساسية من PDF مع علامات؟** يوفر بنية منطقية يمكن لتقنيات المساعدة قراءتها.
- **ما المكتبة التي تساعدك على إنشاء ملفات PDF قابلة للوصول في Java؟** Aspose.PDF for Java.
- **هل أحتاج إلى ترخيص للتطوير؟** الترخيص المؤقت يزيل حدود التقييم؛ الترخيص الكامل مطلوب للإنتاج.
- **هل يمكنني تعيين لغة PDF؟** نعم، باستخدام طريقة `setLanguage` على المحتوى المعلَّم.
- **هل هذا الدليل متوافق مع Java 8+؟** بالتأكيد – الشيفرة تعمل مع JDK 8 والإصدارات الأحدث.

## ما هو PDF مع علامات ولماذا إنشاء PDF قابل للوصول؟
**PDF مع علامات** يحتوي على بيانات وصفية مخفية تحدد ترتيب القراءة، العناوين، الفقرات، الجداول، والعناصر الهيكلية الأخرى. هذه البيانات الوصفية حيوية لقارئات الشاشة، مما يتيح للمستخدمين ضعاف البصر التنقل في المستندات كما لو كانوا يتصفحون صفحة ويب.

## لماذا استخدام Aspose.PDF for Java؟
Aspose.PDF يقدم API غني لإنشاء، تعديل، وتحويل ملفات PDF دون الحاجة إلى Adobe Acrobat. دليل **إمكانية الوصول** الخاص به يتضمن دعمًا مدمجًا للعلامات، إعدادات اللغة، والهياكل المخصصة، مما يجعله خيارًا مثاليًا للمطورين الذين يحتاجون إلى **إنشاء ملفات PDF قابلة للوصول** بسرعة وموثوقية.

## المتطلبات المسبقة
- **Java Development Kit (JDK)** – الإصدار 8 أو أعلى.
- **Maven** أو **Gradle** – لإدارة التبعيات.
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse.
- ترخيص مؤقت أو كامل لـ Aspose.PDF (اختياري للتقييم).

### المكتبات المطلوبة
أضف تبعية Aspose.PDF إلى ملف البناء الخاص بك.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### الحصول على الترخيص
يمكنك الحصول على ترخيص مؤقت من Aspose لاستكشاف جميع الميزات دون قيود التقييم. زر صفحة [Aspose Temporary License Page](https://purchase.aspose.com/temporary-license/) للحصول على التفاصيل.

## إعداد Aspose.PDF for Java

### 1. تثبيت المكتبة
إذا كنت تستخدم Maven أو Gradle، ستقوم التبعية بتنزيل ملفات JAR تلقائيًا. وإلا، قم بتحميل أحدث JAR من [Aspose PDF Java download page](https://releases.aspose.com/pdf/java/) وأضفه إلى مسار الفئة (classpath) في مشروعك.

### 2. تطبيق الترخيص الخاص بك
تطبيق الترخيص يزيل علامة مائية التقييم ويفتح جميع الميزات.

```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file");
```

### 3. تهيئة كائن Document
أنشئ مثيلًا جديدًا من `Document` – هذا هو نقطة الدخول لجميع عمليات PDF.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.tagged.ITaggedContent;

// Create a new PDF document instance
Document document = new Document();
```

## تكوين ميزات إمكانية الوصول

### تعيين عنوان PDF واللغة
تعيين عنوان ومعنى للغة يساعد تقنيات المساعدة على الإعلان عن المستند بشكل صحيح.

```java
ITaggedContent taggedContent = document.getTaggedContent();
taggedContent.setTitle("Tagged Pdf Document");
taggedContent.setLanguage("en-US");
```

## بناء بنية المستند

### الوصول إلى العنصر الجذري
العنصر الجذري هو الحاوية لجميع عناصر البنية المنطقية (العناوين، الفقرات، إلخ).

```java
import com.aspose.pdf.tagged.logicalstructure.elements.StructureElement;
import com.aspose.pdf.tagged.logicalstructure.elements.bls.HeaderElement;

StructureElement rootElement = taggedContent.getRootElement();
```

### إضافة عناصر العناوين (H1‑H6)
العناوين توفر تسلسلًا هرميًا واضحًا. أدناه ننشئ عنوان H1؛ كرر النمط لعناوين H2‑H6 حسب الحاجة.

```java
HeaderElement h1 = taggedContent.createHeaderElement(1);
headerElements(rootElement, h1, "Level 1 Header");

// Repeat for other levels H2-H6...
```

#### طريقة مساعدة لإضافة العناوين
الطريقة التالية تبسط إضافة عنوان مع النص المرتبط به.

```java
public void headerElements(StructureElement parent, HeaderElement header, String text) {
    SpanElement spanPrefix = taggedContent.createSpanElement();
    spanPrefix.setText(text.startsWith("H1.") ? "H" + header.getLevel() + ". " : "");
    parent.appendChild(spanPrefix);
    
    SpanElement spanText = taggedContent.createSpanElement();
    spanText.setText(text);
    header.appendChild(spanText);
    parent.appendChild(header);
}
```

### إضافة عناصر الفقرة مع عناصر Span
الفقرات تجمع الجمل ذات الصلة. استخدام عناصر span يتيح لك تطبيق تنسيق نص غني مع الحفاظ على إمكانية الوصول.

```java
import com.aspose.pdf.tagged.logicalstructure.elements.ParagraphElement;
import com.aspose.pdf.tagged.logicalstructure.elements.ils.SpanElement;

ParagraphElement p = taggedContent.createParagraphElement();
rootElement.appendChild(p);
```

#### طريقة مساعدة للفقرات ذات النص الغني
هذه الطريقة تضيف بادئة ومصفوفة من قطع النص إلى الفقرة.

```java
public void taggedTextElements(ParagraphElement paragraph, String prefix, String[] texts) {
    SpanElement spanPrefix = taggedContent.createSpanElement();
    spanPrefix.setText(prefix);
    paragraph.appendChild(spanPrefix);

    for (String text : texts) {
        SpanElement spanText = taggedContent.createSpanElement();
        spanText.setText(text);
        paragraph.appendChild(spanText);
    }
}

// Example usage:
taggedTextElements(p, "P. ", new String[] {
    "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    // Add additional sentences as needed
});
```

## حفظ مستند PDF مع محتوى معلم
بعد بناء البنية، احفظ الملف. سيحتفظ PDF المحفوظ بجميع علامات إمكانية الوصول.

```java
import com.aspose.pdf.Document;

// Save the document in the specified directory
document.save(outputDir + "/InlineStructureElements.pdf");
```

## تطبيقات عملية
إنشاء **PDFs قابلة للوصول** مع علامات صحيحة ذات قيمة في العديد من الصناعات:

- **التعليم** – توفير مواد قراءة قابلة للوصول للطلاب باستخدام قارئات الشاشة.
- **الحكومة** – تلبية المتطلبات القانونية لإمكانية الوصول للوثائق العامة.
- **التقارير المؤسسية** – تحسين التنقل في التقارير المالية الطويلة.

يمكنك دمج سير العمل هذا في تطبيقات الويب، سكريبتات المعالجة الدفعية، أو أدوات التقارير الآلية لضمان أن كل PDF تنشئه شامل.

## اعتبارات الأداء
على الرغم من كفاءة Aspose.PDF، احرص على مراعاة النصائح التالية للوثائق الكبيرة:

- إعادة استخدام كائن `Document` عند إنشاء عدة ملفات PDF في تشغيل واحد.
- استدعاء `document.optimizeResources()` قبل الحفظ لتقليل حجم الملف.
- مراقبة استهلاك الذاكرة (heap) في Java وتمكين الحفظ المتدرج للملفات الضخمة.

## المشكلات الشائعة والحلول

| المشكلة | الحل |
|-------|----------|
| **Headers not appearing in the PDF outline** | Verify that you called `headerElements` for each header level and that the root element is correctly referenced. |
| **Screen readers ignore paragraph text** | Ensure each paragraph and its spans are appended to the root element as shown in the helper methods. |
| **License not applied** | Double‑check the file path in `license.setLicense()` and confirm the license file is valid for the version you’re using. |

## الأسئلة المتكررة

**س: ما الفرق بين PDF عادي وPDF مع علامات؟**  
ج: PDF العادي يحتوي على معلومات بصرية فقط، بينما PDF مع علامات يتضمن علامات بنية مخفية (عناوين، فقرات، جداول) تستخدمها تقنيات المساعدة لقراءة المستند منطقيًا.

**س: كيف يمكنني تعيين لغة PDF لإمكانية الوصول؟**  
ج: استخدم `taggedContent.setLanguage("en-US")` (أو أي رمز لغة BCP‑47 آخر) بعد الحصول على مثيل `ITaggedContent`.

**س: هل يمكنني توليد PDF مع علامات بدون ترخيص؟**  
ج: يمكنك تقييم المكتبة باستخدام ترخيص مؤقت، لكن الترخيص الكامل مطلوب للاستخدام الإنتاجي لإزالة حدود التقييم.

**س: هل يدعم Aspose.PDF ميزات إمكانية وصول أخرى مثل النص البديل للصور؟**  
ج: نعم، يمكنك إضافة نص بديل للصور باستخدام خاصية `alternativeText` لكائن `Image` داخل بنية المحتوى المعلَّم.

**س: هل هذا النهج متوافق مع Java 11 والإصدارات الأحدث؟**  
ج: بالتأكيد. الـ API متوافق مع JDK 8 ويعمل بسلاسة على إصدارات Java الأحدث.

## الخلاصة
الآن لديك دليل كامل، خطوة بخطوة، لـ **إنشاء ملفات PDF قابلة للوصول** في Java باستخدام Aspose.PDF. من خلال تعيين العنوان، اللغة، وتوليد **PDF مع علامات** بهياكل عناوين وفقرات منظمة، تصبح مستنداتك شاملة ومتوافقة مع معايير إمكانية الوصول.

**الخطوات التالية**
- جرب إضافة العلامات المرجعية (bookmarks)، الجداول، ونص بديل للصور.
- استكشف كامل وثائق [Aspose PDF Java](https://reference.aspose.com/pdf/java/) للحصول على ميزات متقدمة.
- دمج هذا سير العمل في تطبيقات Java الحالية لتوليد ملفات PDF قابلة للوصول تلقائيًا.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**آخر تحديث:** 2025-12-01  
**تم الاختبار مع:** Aspose.PDF for Java 25.3  
**المؤلف:** Aspose  

---