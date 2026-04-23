---
date: '2026-02-09'
description: تعلم كيفية وضع علامات على ملفات PDF في Java باستخدام Aspose.PDF، وإنشاء
  مستندات PDF قابلة للوصول، وتعيين عنوان PDF، وإضافة علامات لتوافق قارئ الشاشة.
keywords:
- tagged PDFs in Java
- Aspose.PDF for Java
- accessible PDF creation
title: 'كيفية إضافة وسوم إلى PDF في Java باستخدام Aspose.PDF: دليل شامل للوصولية والهيكلة'
url: /ar/java/advanced-features/master-tagged-pdfs-java-aspose-pdf-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# كيفية وضع علامات على PDF في Java باستخدام Aspose.PDF: دليل شامل لإمكانية الوصول والهيكلة

## المقدمة
إنشاء مستندات PDF قابلة للوصول وتعلم **how to tag PDF** أمر حيوي للمستخدمين الذين يعتمدون على قارئات الشاشة وغيرها من التقنيات المساعدة. ضمان أن تكون ملفات PDF الخاصة بك قابلة للوصول ومنظمة جيدًا قد يكون تحديًا، لكن Aspose.PDF for Java يجعل العملية بسيطة من خلال السماح لك بتعيين العناوين واللغات والمحتوى الهيكلي مباشرةً في ملف PDF.

في هذا الدرس، ستكتشف كيفية:
- **Set PDF title** وسمات اللغة لتحسين إمكانية الوصول.  
- **Add paragraph and span elements** لبناء هيكل منطقي للمستند.  
- **Nest span elements** داخل الفقرات لتصاميم معقدة.  

سنستعرض كل خطوة، نشرح أهميتها، ونقدم لك نصائح عملية يمكنك تطبيقها فورًا.

### إجابات سريعة
- **What is PDF accessibility tagging?** إنها عملية إضافة بنية منطقية (علامات) إلى PDF بحيث يمكن لقارئات الشاشة تفسير المحتوى بشكل صحيح.  
- **Why use Aspose.PDF for tagging?** توفر API سلس لإنشاء وتعديل ووضع علامات على ملفات PDF دون الحاجة إلى Adobe Acrobat.  
- **How long does the basic implementation take?** حوالي 10–15 دقيقة لمستند بسيط.  
- **Do I need a license?** النسخة التجريبية تعمل للتقييم، لكن يلزم وجود ترخيص للاستخدام الإنتاجي.  
- **Which Java versions are supported?** Java 8 وما بعده (بما في ذلك Java 11، 17، و21).

## ما هو وضع علامات إمكانية الوصول لملفات PDF؟
يتضمن وضع علامات إمكانية الوصول لملفات PDF دمج بنية منطقية (عناوين، عناوين فرعية، فقرات، spans، جداول، إلخ) داخل ملف PDF. تتيح هذه البنية للتقنيات المساعدة عرض المحتوى بترتيب ذو معنى، مما يجعل المستند ينتج **generate accessible PDF**.

## لماذا نستخدم Aspose.PDF for Java؟
Aspose.PDF for Java هو حل **aspose pdf java tutorial**‑grade يتيح لك:
- يعمل على أي منصة تدعم Java.  
- يتيح لك إنشاء وتحرير ووضع علامات على ملفات PDF برمجيًا.  
- يوفر تحكمًا دقيقًا في عناصر العلامات مثل الفقرات والـ spans — مثالي لسيناريوهات **add paragraph pdf java**.

## إعداد Aspose.PDF for Java
لبدء العمل مع Aspose.PDF في مشاريع Java الخاصة بك، تحتاج إلى تضمين المكتبة كاعتماد. إليك كيفية القيام بذلك باستخدام Maven وGradle:

### تثبيت Maven
أضف الاعتماد التالي إلى ملف `pom.xml` الخاص بك:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### تثبيت Gradle
أدرج هذا في ملف `build.gradle` الخاص بك:
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### الحصول على الترخيص
لاستخدام Aspose.PDF بما يتجاوز حدود النسخة التجريبية، يمكنك الحصول على ترخيص مؤقت أو شراء ترخيص كامل. إليك الطريقة:
- **Free Trial:** قم بتنزيل أحدث نسخة من [Aspose PDF Java Releases](https://releases.aspose.com/pdf/java/).  
- **Temporary License:** اطلب ترخيصًا مؤقتًا مجانيًا عبر [Aspose Temporary License Page](https://purchase.aspose.com/temporary-license/).  
- **Purchase License:** اشترِ ترخيصًا كاملاً من [Aspose Purchase Page](https://purchase.aspose.com/buy).

بمجرد حصولك على ملف الترخيص، طبقه في تطبيق Java الخاص بك لفتح جميع الميزات.

## كيفية وضع علامات PDF في Java باستخدام Aspose.PDF
سنقسم التنفيذ إلى ثلاث ميزات رئيسية: تعيين العناوين واللغات، إضافة عناصر الفقرة والـ Span، وتضمين الـ spans داخل الفقرات. كل قسم يحتوي على تعليمات واضحة خطوة بخطوة.

### تعيين العنوان واللغة لمستند PDF
**Overview:** تعريف العنوان واللغة لمستند PDF الموسوم يضمن أن تقنيات المساعدة تعلن عن المستند بشكل صحيح.

#### تنفيذ خطوة بخطوة
1. **Initialize the Aspose.PDF Document:**
   ```java
   import com.aspose.pdf.Document;
   import com.aspose.pdf.tagged.ITaggedContent;

   String dataDir = "YOUR_DOCUMENT_DIRECTORY";
   String outFile = dataDir + "SetTitleAndLanguage_Output.pdf";

   Document document = new Document();
   ITaggedContent taggedContent = document.getTaggedContent();
   ```
2. **Set Title and Language:**
   ```java
   // Set the title of the PDF document
   taggedContent.setTitle("Text Elements Example");

   // Define the language (e.g., English - United States)
   taggedContent.setLanguage("en-US");
   ```
3. **Save the Document:**
   ```java
   document.save(outFile);
   ```
**Explanation:** من خلال تعيين العنوان واللغة، توفر بيانات تعريف أساسية تساعد في **pdf accessibility tagging** وتساعد قارئات الشاشة على إعلان المستند بشكل صحيح.

### إضافة عناصر الفقرة والـ Span
**Overview:** علامات الفقرة والـ span تعطي ملف PDF تدفقًا منطقيًا، مما يسهل على المستخدمين والأدوات التنقل.

#### تنفيذ خطوة بخطوة
1. **Create Document and Tagged Content:**
   ```java
   String dataDir = "YOUR_DOCUMENT_DIRECTORY";
   String outFile = dataDir + "AddParagraphAndSpanElements_Output.pdf";

   Document document = new Document();
   ITaggedContent taggedContent = document.getTaggedContent();
   ```
2. **Append Paragraph and Span Elements:**
   ```java
   import com.aspose.pdf.tagged.logicalstructure.elements.StructureElement;
   import com.aspose.pdf.tagged.logicalstructure.elements.bls.ParagraphElement;
   import com.aspose.pdf.tagged.logicalstructure.elements.ils.SpanElement;

   StructureElement rootElement = taggedContent.getRootElement();

   ParagraphElement p1 = taggedContent.createParagraphElement();
   rootElement.appendChild(p1);

   SpanElement span11 = taggedContent.createSpanElement();
   span11.setText("Span_11");
   SpanElement span12 = taggedContent.createSpanElement();
   span12.setText(" and Span_12.");

   // Append spans to the paragraph
   p1.setText("Paragraph with ");
   p1.appendChild(span11);
   p1.appendChild(span12);
   ```
3. **Save Your Document:**
   ```java
   document.save(outFile);
   ```
**Explanation:** يوضح هذا سيناريو **add paragraph pdf java** كلاسيكي، حيث يتم إنشاء تدفق نصي منظم يحسن من قابلية القراءة والتنقل.

### تضمين عناصر Span داخل عنصر الفقرة
**Overview:** تضمين الـ spans يتيح لك بناء هياكل نصية أغنى—على سبيل المثال، تطبيق أنماط مختلفة أو تجميعات منطقية داخل فقرة واحدة.

#### تنفيذ خطوة بخطوة
1. **Initialize Document Structure:**
   ```java
   String dataDir = "YOUR_DOCUMENT_DIRECTORY";
   String outFile = dataDir + "NestSpanElements_Output.pdf";

   Document document = new Document();
   ITaggedContent taggedContent = document.getTaggedContent();
   ```
2. **Create and Nest Span Elements:**
   ```java
   StructureElement rootElement = taggedContent.getRootElement();

   ParagraphElement p4 = taggedContent.createParagraphElement();
   rootElement.appendChild(p4);

   SpanElement span41 = taggedContent.createSpanElement();
   SpanElement span411 = taggedContent.createSpanElement();
   span411.setText("Span_411, ");
   span41.setText("Span_41, ");
   span41.appendChild(span411);

   SpanElement span42 = taggedContent.createSpanElement();
   SpanElement span421 = taggedContent.createSpanElement();
   span421.setText("Span 421 and ");
   span42.appendChild(span421);
   span42.setText("Span_42");

   // Append to paragraph
   p4.appendChild(span41);
   p4.appendChild(span42);

   p4.setText(".");
   ```
3. **Save the Document:**
   ```java
   document.save(outFile);
   ```
**Explanation:** يتيح التضمين بناء هياكل معقدة، وهو أمر أساسي لإنشاء مستندات **generate accessible PDF** تلتزم بمعايير الوصول الصارمة.

## التطبيقات العملية
لدى قدرات وضع العلامات في Aspose.PDF العديد من الاستخدامات الواقعية:
- **Digital Publishing:** إنشاء كتب إلكترونية قابلة للوصول مع محتوى منظم.  
- **Government Documentation:** ضمان الامتثال للوائح إمكانية الوصول.  
- **Corporate Reports:** تحسين التنقل والقراءة لأصحاب المصلحة.  
- **Educational Materials:** توفير موارد تعليمية قابلة للوصول للطلاب.

## اعتبارات الأداء
عند العمل مع ملفات PDF كبيرة أو هياكل علامات معقدة، ضع في اعتبارك النصائح التالية:
- **Memory Management:** تخلص من الكائنات فورًا بعد الاستخدام.  
- **Batch Processing:** معالجة المستندات على دفعات للتحكم في استهلاك الموارد.  
- **Stay Updated:** استخدم أحدث نسخة من Aspose.PDF لتحسين الأداء وإصلاح الأخطاء.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **Tags not appearing in PDF viewer** | تحقق من أن `taggedContent.setTitle()` و `setLanguage()` تم استدعاؤهما قبل الحفظ. |
| **Large file size** | استدعِ `document.optimizeResources()` قبل `save()` لضغط الموارد. |
| **Unexpected text order** | تأكد من إلحاق الـ spans بالفقرات بالترتيب المطلوب. |

## الأسئلة المتكررة

**س: كيف أضمن أن ملفات PDF الخاصة بي تلتزم بمعايير WCAG 2.1 لإمكانية الوصول؟**  
ج: استخدم Aspose.PDF لتعيين عنوان المستند، اللغة، ووضع العلامات بشكل صحيح (فقرات، spans، عناوين). شغّل PDF عبر أداة فحص إمكانية الوصول (مثل PAC 3) للتحقق من الامتثال.

**س: هل يمكنني وضع علامات على ملفات PDF موجودة تم إنشاؤها بدون علامات؟**  
ج: نعم. حمّل ملف PDF، استرجع `ITaggedContent` الخاص به، أضف العلامات المفقودة برمجيًا، ثم احفظه.

**س: هل يدعم Aspose.PDF لغات أخرى ونصوص من اليمين إلى اليسار؟**  
ج: بالتأكيد. عيّن رمز اللغة المناسب (مثال: `ar-SA` للغة العربية) وأضف نصًا Unicode إلى الـ spans.

**س: ما هي أفضل طريقة للتعامل مع مستندات ضخمة جدًا (مئات الصفحات)؟**  
ج: عالج المستند على أقسام، استخدم `Document.optimizeResources()`، وفكّر في بث الإخراج لتجنب استهلاك الذاكرة العالي.

**س: هل هناك طريقة للتحقق من تسلسل الهرم للعلامات بعد الإنشاء؟**  
ج: يمكنك تصدير شجرة هيكل PDF باستخدام `document.getTaggedContent().getRootElement()` وفحصها برمجيًا أو باستخدام أدوات تحليل PDF.

## الخلاصة
لقد أتقنت الآن **how to tag PDF** في Java باستخدام Aspose.PDF—تعيين العناوين، اللغات، وبناء محتوى منظم باستخدام الفقرات والـ spans المتداخلة. هذه التقنيات تمكنك من إنشاء ملفات PDF قابلة للوصول تلتزم بالمعايير الحديثة وتوفر تجربة قراءة متفوقة لجميع المستخدمين.

**الخطوات التالية:**  
- جرّب أنواع علامات إضافية مثل الجداول والقوائم والرسوم.  
- دمج سير عمل وضع العلامات في خطوط إنتاج المستندات الحالية.  
- استكشف ميزات OCR والتحويل في Aspose.PDF لتوسيع قدرات معالجة المستندات.

---

**آخر تحديث:** 2026-02-09  
**تم الاختبار مع:** Aspose.PDF for Java 25.3  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}