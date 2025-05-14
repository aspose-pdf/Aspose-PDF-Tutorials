---
"date": "2025-04-14"
"description": "تعلّم كيفية إضافة تعليقات توضيحية إلى ملفات PDF بلغة جافا باستخدام Aspose.PDF بإضافة تعليقات توضيحية مشطوبة. اتبع هذا الدليل للحصول على تعليمات خطوة بخطوة حول تعديل محتوى PDF."
"title": "كيفية إضافة تعليقات توضيحية إلى ملفات PDF في Java باستخدام التعليقات التوضيحية المشطوبة باستخدام Aspose.PDF"
"url": "/ar/java/forms-annotations/annotate-pdfs-java-strikeout-aspose-pdf/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# كيفية إضافة تعليقات توضيحية إلى ملفات PDF في Java باستخدام التعليقات التوضيحية المشطوبة باستخدام Aspose.PDF

استغل كامل إمكانات معالجة ملفات PDF باستخدام Aspose.PDF لجافا من خلال تعلم كيفية إضافة التعليقات التوضيحية وحفظ ملفات PDF مع الشطب. سيرشدك هذا الدليل الشامل خلال تهيئة المستند، والبحث عن أجزاء النص، وإنشاء التعليقات التوضيحية، وحفظ المستند المُعلّق.

## مقدمة

قد يكون التعامل مع تعقيدات ملفات PDF أمرًا صعبًا، سواءً كان استخراج البيانات أو تعديل المحتوى. إذا كنت ترغب في إضافة تعليقات توضيحية مرئية، مثل الشطب، مباشرةً داخل تطبيقات Java باستخدام Aspose.PDF لـ Java، فهذا الدليل مثالي لك. ستتعلم كيفية دمج وظائف PDF بسلاسة في مشاريعك.

### ما سوف تتعلمه
- كيفية تهيئة وتحميل مستند PDF باستخدام Aspose.PDF
- تقنيات البحث عن أجزاء نصية محددة في ملف PDF
- خطوات إنشاء وتكوين التعليقات التوضيحية المشطوبة
- طرق حفظ مستند PDF المعدل

دعونا نلقي نظرة على المتطلبات الأساسية التي ستحتاجها قبل أن نبدأ.

## المتطلبات الأساسية

### المكتبات والإصدارات والتبعيات المطلوبة
لمتابعة هذا البرنامج التعليمي، تأكد من أن لديك:
- تم تثبيت Java Development Kit (JDK) 8 أو إصدار أحدث.
- IDE مثل IntelliJ IDEA أو Eclipse لتحرير الكود Java الخاص بك.

سنستخدم ملف Aspose.PDF لإصدار Java 25.3. يمكنك دمجه في مشروعك عبر Maven أو Gradle كما هو موضح أدناه.

### متطلبات إعداد البيئة
تأكد من إعداد بيئتك للتعامل مع التبعيات وأن لديك إمكانية الوصول إلى الدليل الذي يتم فيه تخزين مستندات PDF المدخلة، بالإضافة إلى دليل الإخراج لحفظ الملفات الموضحة.

### متطلبات المعرفة
ستكون المعرفة ببرمجة Java والفهم الأساسي للتعامل مع ملفات PDF برمجيًا أمرًا مفيدًا.

## إعداد Aspose.PDF لـ Java
دمج Aspose.PDF في مشروع Java الخاص بك سهل للغاية. إليك كيفية إضافته باستخدام Maven أو Gradle:

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
Aspose.PDF مكتبة تجارية، ولكن يمكنك البدء بالحصول على نسخة تجريبية مجانية أو ترخيص مؤقت لأغراض التقييم. تفضل بزيارة [صفحة شراء Aspose](https://purchase.aspose.com/buy) لاستكشاف خياراتك.

## دليل التنفيذ
سنقوم بتقسيم تنفيذنا إلى أقسام بناءً على الوظيفة: تهيئة المستند، والبحث عن جزء من النص، وإنشاء التعليقات التوضيحية، وحفظ المستند.

### تهيئة المستند وتحميلها
#### ملخص
أولاً، نحتاج إلى تحميل ملف PDF باستخدام Aspose.PDF لجافا. تتضمن هذه الخطوة تهيئة `Document` الفئة التي تحتوي على المسار إلى ملف PDF الخاص بك.

**الخطوة 1**:استيراد الفئات الضرورية.
```java
import com.aspose.pdf.Document;
```

**الخطوة 2**:قم بتحديد دليل المستند الخاص بك وقم بتهيئة كائن المستند.
```java
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document document = new Document(dataDir + "/input.pdf");
```
يقوم هذا الكود بتحميل ملف PDF من `dataDir` إلى `Document` على سبيل المثال، السماح بإجراء المزيد من العمليات.

### امتصاص جزء من النص
#### ملخص
يُعد البحث عن نص داخل ملف PDF أمرًا ضروريًا قبل إنشاء التعليقات التوضيحية. سنستخدم `TextFragmentAbsorber`.

**الخطوة 1**:استيراد الفصل.
```java
import com.aspose.pdf.TextFragmentAbsorber;
```

**الخطوة 2**:قم بإنشاء مثيل لـ TextFragmentAbsorber باستخدام استعلام البحث.
```java
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Sample");
```

**الخطوة 3**:قم بقبول الممتص في كل صفحة للعثور على جميع أجزاء النص المطابقة.
```java
for (int i = 1; i <= document.getPages().size(); i++) {
    document.getPages().get_Item(i).accept(textFragmentAbsorber);
}
```
تقوم هذه الحلقة بالبحث في كل صفحة، وجمع التطابقات لـ "العينة".

### استرداد مجموعة أجزاء النص
#### ملخص
بمجرد استيعاب أجزاء النص، نقوم باسترجاعها في مجموعة لمعالجة التعليقات التوضيحية.

**الخطوة 1**:استيراد الفئة المطلوبة.
```java
import com.aspose.pdf.TextFragmentCollection;
```

**الخطوة 2**:جلب المجموعة من الممتص.
```java
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.getTextFragments();
```
يتيح لنا هذا الوصول إلى جميع الحالات التي تم العثور عليها من "العينة".

### إنشاء تعليق توضيحي مشطوب
#### ملخص
سنضيف تعليقًا توضيحيًا على كل جزء من النص المحدد، مع تسليط الضوء عليه أو وضع علامة عليه بصريًا.

**الخطوة 1**:استيراد الفئات الضرورية.
```java
import com.aspose.pdf.StrikeOutAnnotation;
import com.aspose.pdf.Rectangle;
import com.aspose.pdf.Border;
import com.aspose.pdf.Color;
import com.aspose.pdf.Page;
```

**الخطوة 2**:قم بالتنقل عبر أجزاء النص وإنشاء التعليقات التوضيحية.
```java
for (int j = 1; j <= textFragmentCollection.size(); j++) {
    com.aspose.pdf.TextFragment textFragment = textFragmentCollection.get_Item(j);

    // قم بتحديد منطقة المستطيل للتعليق التوضيحي استنادًا إلى موقع جزء النص.
    Rectangle rect = new Rectangle((float) textFragment.getPosition().getXIndent(),
                                   (float) textFragment.getPosition().getYIndent(),
                                   (float) textFragment.getPosition().getXIndent() + (float) textFragment.getRectangle().getWidth(),
                                   (float) textFragment.getPosition().getYIndent() + (float) textFragment.getRectangle().getHeight());

    // إنشاء وتكوين تعليق الشطب.
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.getPage(), rect);
    strikeOut.setOpacity(0.80f);  // ضبط التعتيم إلى 80%
    strikeOut.setBorder(new Border(strikeOut));  // تهيئة حدود للتعليق التوضيحي
    strikeOut.setColor(Color.getRed());  // تعيين لون التعليق التوضيحي إلى اللون الأحمر

    // أضف التعليق التوضيحي إلى الصفحة.
    textFragment.getPage().getAnnotations().add(strikeOut);
}
```
يتم تكوين كل تعليق باستخدام إعدادات العتامة والحدود واللون قبل إضافته.

### حفظ المستند مع التعليقات التوضيحية
#### ملخص
بعد إنشاء التعليقات التوضيحية، نقوم بحفظ المستند الموضح.

**الخطوة 1**:استيراد الفئات الضرورية إذا لم يتم ذلك بالفعل.
```java
import com.aspose.pdf.Document;
```

**الخطوة 2**:قم بتحديد دليل الإخراج وحفظ المستند.
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
document.save(outputDir + "/StrikeOut.pdf");
```
تؤدي هذه الخطوة إلى الانتهاء من ملف PDF الموضح مع جميع التعديلات سليمة.

## التطبيقات العملية
يمكن استخدام Aspose.PDF لـ Java في سيناريوهات مختلفة، مثل:
1. **عمليات مراجعة المستندات**:أتمتة عملية المراجعة عن طريق تحديد التغييرات المطلوبة برمجيًا.
2. **التعامل مع الوثائق القانونية**:قم بشرح العقود أو الاتفاقيات بسرعة مع التحرير والتعديلات اللازمة.
3. **إنشاء المحتوى التعليمي**:تعزيز المواد التعليمية من خلال حذف المعلومات القديمة وتوضيح التصحيحات.

## اعتبارات الأداء
لضمان الأداء الأمثل:
- استخدم هياكل بيانات فعالة عند التعامل مع مجموعات كبيرة من أجزاء النص.
- إدارة الذاكرة بشكل فعال، وخاصة في البيئات ذات الموارد المحدودة.
- قم بالتحديث بانتظام إلى أحدث إصدار من Aspose.PDF للحصول على ميزات محسنة وإصلاحات.

## خاتمة
لقد تعلمتَ بنجاح كيفية استخدام Aspose.PDF لجافا لإضافة تعليقات توضيحية إلى ملفات PDF باستخدام أسطر مشطوبة. باتباع هذا الدليل، تكون قد خطوت خطوةً هامةً نحو أتمتة عمليات معالجة ملفات PDF. استكشف المزيد من خلال تجربة أنواع تعليقات توضيحية أخرى أو دمج وظائف إضافية من مكتبة Aspose.

هل أنت مستعد للمضي قدمًا؟ تفضل بزيارة [وثائق Aspose](https://reference.aspose.com/pdf/java/) لمزيد من الميزات والقدرات المتقدمة.

## قسم الأسئلة الشائعة
**1. كيف أقوم بتثبيت Aspose.PDF في مشروع Java الخاص بي؟**
يمكنك إضافته عبر تبعيات Maven أو Gradle كما هو موضح في هذا البرنامج التعليمي. تأكد من أن بيئة التطوير المتكاملة لديك مُهيأة للتعرف على هذه الإعدادات.

**2. هل يمكنني التعليق على ملفات PDF بطريقة أخرى غير الشطب باستخدام Aspose.PDF لـ Java؟**
نعم، يمكنك إنشاء تعليقات توضيحية مختلفة مثل التمييزات والتسطير وغير ذلك.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}