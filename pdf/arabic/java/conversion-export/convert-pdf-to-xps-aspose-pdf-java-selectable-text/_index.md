---
date: '2026-07-03'
description: تعلم كيفية إضافة اعتماد Maven لـ Aspose PDF وتحويل PDF إلى XPS بنص قابل
  للتحديد باستخدام Aspose.PDF for Java. دليل خطوة بخطوة مع المتطلبات المسبقة والأسئلة
  الشائعة.
keywords:
- aspose pdf maven dependency
- how to convert pdf to xps
- java convert pdf xps
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  headline: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  type: TechArticle
- description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  name: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  steps:
  - name: Load the PDF Document
    text: 'First, load your PDF document from its directory:'
  - name: Configure Save Options
    text: 'Create an instance of `XpsSaveOptions` to set up the XPS conversion options:'
  - name: Save as XPS File
    text: 'Finally, save the document in XPS format to your desired output directory:'
  type: HowTo
- questions:
  - answer: Yes—pass the password to the `Document` constructor or use `Document.open(String
      path, String password)` before conversion.
    question: Can I convert password‑protected PDFs?
  - answer: Absolutely. All vector shapes, images, and text are preserved, and the
      text remains selectable.
    question: Does the XPS retain vector graphics?
  - answer: The trial works without a license but adds a watermark to the output;
      a permanent license removes all restrictions.
    question: Is a license mandatory for the trial version?
  - answer: It processes files in a streaming manner, allowing conversion of PDFs
      with hundreds of pages without loading the entire document into memory.
    question: How does Aspose.PDF handle large files?
  - answer: The library runs on any OS with a compatible JDK, including Windows, Linux,
      and macOS.
    question: Which platforms are supported?
  type: FAQPage
title: اعتماد Maven لـ Aspose PDF – تحويل PDF إلى XPS (Java)
url: /ar/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# اعتماد Aspose PDF Maven – تحويل PDF إلى XPS (Java)

## مقدمة

إذا كنت بحاجة إلى **إضافة اعتماد Aspose PDF Maven** ثم تحويل مستندات PDF إلى XPS مع الحفاظ على إمكانية اختيار النص، فأنت في المكان الصحيح. يشرح هذا الدليل كل خطوة — من تكوين Maven أو Gradle، إلى تحميل ملف PDF، وتكوين خيارات XPS، وأخيرًا حفظ ملف XPS بنص قابل للاختيار. في النهاية ستحصل على مقطع شفرة قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع Java.

## إجابات سريعة
- **ما هو الاعتماد الذي أحتاجه؟** `com.aspose:aspose-pdf` (Maven) أو القطعة المكافئة في Gradle.  
- **هل يمكن للـ XPS الاحتفاظ بنص قابل للاختيار؟** نعم — Aspose.PDF يحافظ على طبقات النص تلقائيًا.  
- **ما نسخة Java المطلوبة؟** JDK 8 أو أحدث.  
- **هل أحتاج إلى ترخيص للإنتاج؟** يلزم وجود ترخيص Aspose.PDF صالح للاستخدام غير المحدود.  
- **كم يستغرق التحويل من الوقت؟** عادةً أقل من ثانية للملفات التي تقل عن 100 صفحة على عتاد قياسي.

## ما هو اعتماد Aspose PDF Maven؟
توفر حزمة Maven `aspose-pdf` واجهة برمجة تطبيقات Aspose.PDF للـ Java الكاملة، مما يتيح إنشاء ومعالجة وتحويل ملفات PDF دون الحاجة إلى برامج خارجية. إضافة هذا الاعتماد إلى ملف `pom.xml` أو `build.gradle` يجلب جميع الثنائيات المطلوبة، بحيث يمكنك البدء بالبرمجة فورًا دون إدارة JAR يدويًا.

## لماذا تحويل PDF إلى XPS بنص قابل للاختيار؟
يدعم Aspose.PDF **أكثر من 50 تنسيقًا للمدخلات والمخرجات** ويمكنه توليد ملفات XPS تحتفظ بطبقة نصية قابلة للبحث والاختيار. هذا أمر حاسم للعمليات التي تتطلب مستندات بأرشفة عالية، أو الحفاظ على تخطيط دقيق، أو تحرير لاحق في أدوات تدعم XPS. تكتمل التحويلات في أقل من ثانية عادةً لملفات PDF ذات 20 صفحة على معالج حديث.

## المتطلبات المسبقة

- **مجموعة تطوير Java (JDK) 8+** مثبتة ومُعينة المتغير `JAVA_HOME`.  
- **Maven 3.6+** أو **Gradle 6+** لإدارة الاعتمادات.  
- إلمام أساسي بعمليات I/O في Java ومعالجة الاستثناءات.  

### المكتبات والاعتمادات المطلوبة

ستحتاج إلى مكتبة Aspose.PDF للـ Java الإصدار 25.3 أو أحدث. أدرجها باستخدام إحدى أدوات البناء التالية:

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

تأكد من أن بيئة التطوير المتكاملة أو بيئة البناء تشير إلى JDK الصحيح وأن الشبكة يمكنها الوصول إلى Maven Central أو المستودع الخاص بك.

## كيف تضيف اعتماد Aspose PDF Maven؟

`aspose-pdf` هو القطعة التي تضيفها إلى ملف بناء مشروعك، ثم تقوم بتحديث الاعتمادات حتى يتم تنزيل ملفات JAR تلقائيًا. بالنسبة لـ Maven، أدرج كتلة `<dependency>` داخل `<dependencies>`؛ بالنسبة لـ Gradle، ضع سطر `implementation` داخل كتلة `dependencies`. بعد التحديث، تصبح فئات Aspose متاحة في مسار الفئة، ويمكنك البدء بالبرمجة دون التعامل اليدوي مع ملفات JAR.

## إعداد Aspose.PDF للـ Java

### خطوات التثبيت

1. **إعداد Maven/Gradle:** أضف الاعتماد كما هو موضح أعلاه وشغّل `mvn clean install` أو `gradle build` لسحب المكتبة.  
2. **الحصول على الترخيص:**  
   - حمّل [نسخة تجريبية مجانية](https://releases.aspose.com/pdf/java/) أو احصل على [ترخيص مؤقت](https://purchase.aspose.com/temporary-license/).  
   - ضع ملف الترخيص (`Aspose.Pdf.lic`) في مجلد يمكن لتطبيقك الوصول إليه وحمّله عند بدء التشغيل.

### التهيئة الأساسية

`License` يطبق ملف ترخيص Aspose لفتح جميع الوظائف.  
حمّل الترخيص (إذا كان لديك) وأنشئ كائن `Document` للعمل مع ملفات PDF.  
`Document` يمثل ملف PDF ويوفر طرقًا لمعالجة محتوياته.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## كيف تحول PDF إلى XPS بنص قابل للاختيار؟

`XpsSaveOptions` يضبط الإعدادات لحفظ PDF كملف XPS، بما في ذلك الحفاظ على النص. حمّل PDF المصدر، اضبط `XpsSaveOptions` للحفاظ على النص، ثم استدعِ `save` بامتداد `.xps`. تقوم الواجهة البرمجية تلقائيًا بدمج طبقة نصية، لذا يمكن البحث والنسخ من ملف XPS الناتج كما هو في PDF الأصلي. عادةً ما يتطلب هذا العملية ثلاث أسطر من الشيفرة بعد إعداد المكتبة.

## دليل التنفيذ

### تحويل PDF إلى XPS

تتيح لك هذه الميزة تحويل مستند PDF إلى ملف XPS باستخدام Aspose.PDF للـ Java.

#### الخطوة 1: تحميل مستند PDF

أولاً، حمّل مستند PDF من الدليل الخاص به:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### الخطوة 2: تكوين خيارات الحفظ

أنشئ مثيلًا من `XpsSaveOptions` لتحديد خيارات تحويل XPS:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### الخطوة 3: حفظ كملف XPS

أخيرًا، احفظ المستند بتنسيق XPS إلى الدليل الذي ترغب به:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## المشكلات الشائعة والحلول

- **صفحات فارغة في ناتج XPS:** تأكد من أن PDF لا يستخدم تدفقات مشفرة؛ إذا كان كذلك، قدِّم كلمة المرور عند تحميل `Document`.  
- **أخطاء الذاكرة في ملفات PDF الكبيرة:** استخدم `Document.optimizeResources()` قبل الحفظ لتقليل استهلاك الذاكرة.  
- **خطوط مفقودة:** ثبّت الخطوط المطلوبة على الخادم أو دمجها في PDF قبل التحويل.

## الأسئلة المتكررة

**س: هل يمكنني تحويل ملفات PDF المحمية بكلمة مرور؟**  
ج: نعم — مرّر كلمة المرور إلى مُنشئ `Document` أو استخدم `Document.open(String path, String password)` قبل التحويل.

**س: هل يحتفظ XPS بالرسومات المتجهية؟**  
ج: بالتأكيد. جميع الأشكال المتجهية والصور والنصوص تُحفظ، ويظل النص قابلًا للاختيار.

**س: هل الترخيص إلزامي للإصدار التجريبي؟**  
ج: يعمل الإصدار التجريبي بدون ترخيص لكنه يضيف علامة مائية إلى الناتج؛ الترخيص الدائم يزيل جميع القيود.

**س: كيف يتعامل Aspose.PDF مع الملفات الكبيرة؟**  
ج: يعالج الملفات بطريقة تدفقية، مما يسمح بتحويل PDFs مئات الصفحات دون تحميل المستند بالكامل في الذاكرة.

**س: ما الأنظمة المدعومة؟**  
ج: تعمل المكتبة على أي نظام تشغيل يدعم JDK متوافق، بما في ذلك Windows وLinux وmacOS.

---

**آخر تحديث:** 2026-07-03  
**تم الاختبار مع:** Aspose.PDF للـ Java 25.3  
**المؤلف:** Aspose  

{{< blocks/products/products-backtop-button >}}

## الدروس ذات الصلة

- [تحويل PDF إلى JPEG باستخدام Aspose.PDF للـ Java: دليل خطوة بخطوة](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [كيفية تحويل PDF إلى Excel باستخدام Aspose.PDF للـ Java | دليل خطوة بخطوة](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [كيفية تحويل ملفات XPS إلى PDF باستخدام Aspose.PDF في Java: دليل كامل](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}