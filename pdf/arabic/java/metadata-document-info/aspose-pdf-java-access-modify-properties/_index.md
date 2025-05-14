---
"date": "2025-04-14"
"description": "تعرّف على كيفية الوصول إلى خصائص PDF وتعديلها باستخدام Aspose.PDF لجافا. يغطي هذا الدليل بيانات تعريف المستند، وإعدادات النوافذ، وترتيب القراءة، والمزيد."
"title": "كيفية الوصول إلى خصائص PDF وتعديلها باستخدام Aspose.PDF لـ Java - دليل شامل"
"url": "/ar/java/metadata-document-info/aspose-pdf-java-access-modify-properties/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# كيفية الوصول إلى خصائص PDF وتعديلها باستخدام Aspose.PDF لـ Java

## مقدمة

قم بتعزيز تفاعل تطبيقك مع ملفات PDF من خلال الوصول إلى خصائصها وتعديلها بسهولة باستخدام **Aspose.PDF لـ Java**سوف يرشدك هذا الدليل الشامل خلال كيفية استخدام Aspose.PDF لإدارة خصائص المستند المختلفة، بما في ذلك موضع النافذة، وترتيب القراءة، وإعدادات عنوان العرض، والمزيد.

**ما سوف تتعلمه:**
- إعداد Aspose.PDF لـJava في مشروعك.
- الوصول إلى خصائص المستندات المختلفة باستخدام طرق Aspose.PDF.
- تكوين إعدادات عرض النافذة وترتيب القراءة.
- استكشاف الأخطاء الشائعة وإصلاحها عند العمل مع ملفات PDF.

دعونا نستكشف المتطلبات الأساسية التي تحتاجها للبدء!

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من أن إعدادك يتضمن:

### المكتبات المطلوبة
- **Aspose.PDF لـ Java**يُنصح باستخدام الإصدار 25.3 أو أحدث. يُمكنك إضافته عبر Maven أو Gradle كما هو موضح في هذا البرنامج التعليمي.

### إعداد البيئة
- مجموعة تطوير Java (JDK) مثبتة على جهازك.
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA، أو Eclipse، أو NetBeans.

### متطلبات المعرفة
- فهم أساسيات برمجة جافا.
- المعرفة بأدوات إدارة المشاريع مثل Maven أو Gradle لإدارة التبعيات.

بعد وضع المتطلبات الأساسية، دعنا ننتقل إلى إعداد Aspose.PDF لـJava.

## إعداد Aspose.PDF لـ Java

للبدء في الاستخدام **Aspose.PDF لـ Java**عليك تضمينه في مشروعك. إليك الطريقة:

### مافن
أضف التبعية التالية إلى ملفك `pom.xml` ملف:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### جرادل
قم بتضمين هذا السطر في `build.gradle` ملف:
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### الحصول على الترخيص

يمكنك الحصول على **نسخة تجريبية مجانية** من Aspose.PDF عن طريق تنزيله من [صفحة الإصدار](https://releases.aspose.com/pdf/java/). للاستخدام المستمر، قد تحتاج إلى شراء ترخيص أو التقدم بطلب للحصول على ترخيص مؤقت عبر [صفحة الشراء](https://purchase.aspose.com/buy).

### التهيئة الأساسية

بمجرد إعداد مشروعك باستخدام Aspose.PDF، قم بتهيئته على النحو التالي:
```java
import com.aspose.pdf.Document;

public class PdfPropertiesExample {
    public static void main(String[] args) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        
        // تهيئة كائن المستند
        Document pdfDocument = new Document(dataDir + "/Original.pdf");
        
        // انتقل إلى الوصول إلى خصائص المستند
    }
}
```

بعد تكوين Aspose.PDF، يمكننا الآن استكشاف كيفية الوصول إلى خصائص مستند PDF وتكوينها.

## دليل التنفيذ

سيرشدك هذا القسم خلال الوصول إلى الخصائص المختلفة لمستند PDF باستخدام Aspose.PDF.

### خاصية النافذة المركزية

**ملخص**:تحدد هذه الخاصية ما إذا كان يجب أن تكون نافذة PDF في المنتصف عند فتحها. افتراضيًا، يتم ضبطها على `false`.

#### خطوات
1. **الوصول إلى العقار**
   ```java
   boolean centerWindow = pdfDocument.isCenterWindow();
   System.out.println("Is center window enabled? " + centerWindow);
   ```

2. **ضبط الخاصية**
   لتمكين التمركز:
   ```java
   pdfDocument.setCenterWindow(true);
   ```

### ترتيب القراءة

**ملخص**: ال `Direction` تحدد الخاصية ترتيب القراءة، مثل من اليسار إلى اليمين (L2R) أو من اليمين إلى اليسار (R2L).

#### خطوات
1. **الوصول إلى العقار**
   ```java
   String direction = pdfDocument.getDirection();
   System.out.println("Reading direction: " + direction);
   ```

2. **ضبط ترتيب القراءة**
   تغييره إلى اليمين إلى اليسار:
   ```java
   pdfDocument.setDirection(com.aspose.pdf.Document.DirectionType.R2L);
   ```

### عرض عنوان المستند

**ملخص**:يتحكم فيما إذا كان شريط عنوان النافذة يعرض عنوان المستند أو اسم الملف.

#### خطوات
1. **الوصول إلى العقار**
   ```java
   boolean displayDocTitle = pdfDocument.isDisplayDocTitle();
   System.out.println("Is document title displayed? " + displayDocTitle);
   ```

2. **تعديل الإعداد**
   لتفعيل عرض عنوان المستند:
   ```java
   pdfDocument.setDisplayDocTitle(true);
   ```

### نافذة ملائمة

**ملخص**:تعمل هذه الخاصية على تغيير حجم النافذة لتناسب الصفحة الأولى عند فتحها.

#### خطوات
1. **الوصول إلى العقار**
   ```java
   boolean fitWindow = pdfDocument.isFitWindow();
   System.out.println("Is fit window enabled? " + fitWindow);
   ```

2. **ضبط الإعداد**
   تمكين تغيير الحجم:
   ```java
   pdfDocument.setFitWindow(true);
   ```

### إخفاء شريط القوائم وأشرطة الأدوات

**ملخص**:تتحكم هذه الخصائص في رؤية عناصر واجهة المستخدم مثل شريط القائمة وأشرطة الأدوات.

#### خطوات
1. **الوصول إلى الخصائص**
   ```java
   boolean hideMenuBar = pdfDocument.isHideMenubar();
   System.out.println("Is menu bar hidden? " + hideMenuBar);

   boolean hideToolBar = pdfDocument.isHideToolBar();
   System.out.println("Is tool bar hidden? " + hideToolBar);
   ```

2. **تكوين الرؤية**
   لإخفاء كليهما:
   ```java
   pdfDocument.setHideMenubar(true);
   pdfDocument.setHideToolBar(true);
   ```

### إخفاء واجهة المستخدم للنافذة

**ملخص**:عند تعيينه على true، تقوم هذه الخاصية بإخفاء جميع عناصر واجهة المستخدم باستثناء محتويات الصفحة.

#### خطوات
1. **الوصول إلى العقار**
   ```java
   boolean hideWindowUI = pdfDocument.isHideWindowUI();
   System.out.println("Is window UI hidden? " + hideWindowUI);
   ```

2. **تمكين الإعداد**
   ```java
   pdfDocument.setHideWindowUI(true);
   ```

### وضع الصفحة غير الكاملة

**ملخص**:يحدد وضع الصفحة عند الخروج من عرض ملء الشاشة.

#### خطوات
1. **الوصول إلى العقار**
   ```java
   String nonFullScreenPageMode = pdfDocument.getNonFullScreenPageMode();
   System.out.println("Non-full screen page mode: " + nonFullScreenPageMode);
   ```

2. **ضبط وضع الصفحة**
   تغيير إلى الصور المصغرة:
   ```java
   pdfDocument.setNonFullScreenPageMode(com.aspose.pdf.Document.PageModeType.Thumbnails);
   ```

### تخطيط الصفحة

**ملخص**:يحدد كيفية تخطيط الصفحات، مثل صفحة واحدة أو عمودين.

#### خطوات
1. **الوصول إلى العقار**
   ```java
   String pageLayout = pdfDocument.getPageLayout();
   System.out.println("Page layout: " + pageLayout);
   ```

2. **تكوين التخطيط**
   تعيين إلى عمودين:
   ```java
   pdfDocument.setPageLayout(com.aspose.pdf.Document.PageLayoutType.TwoColumnLeft);
   ```

### وضع الصفحة

**ملخص**:يتحكم في كيفية عرض المستند عند فتحه، مع خيارات مثل الصور المصغرة والمخططات التفصيلية.

#### خطوات
1. **الوصول إلى العقار**
   ```java
   String pageMode = pdfDocument.getPageMode();
   System.out.println("Page mode: " + pageMode);
   ```

2. **ضبط وضع الصفحة**
   عرض كإشارات مرجعية:
   ```java
   pdfDocument.setPageMode(com.aspose.pdf.Document.PageModeType.Outlines);
   ```

## التطبيقات العملية

يمكن أن يكون فهم خصائص PDF ومعالجتها مفيدًا للغاية في سيناريوهات مختلفة:

1. **إنشاء التقارير تلقائيًا**:تخصيص إعدادات النافذة لعروض العملاء.
2. **النشر الرقمي**:التحكم في ترتيب القراءة للمستندات متعددة اللغات.
3. **تخصيص واجهة المستخدم**:تحسين تجربة المستخدم من خلال ضبط عناصر واجهة المستخدم مثل أشرطة الأدوات.
4. **وضع العرض**:استخدم أوضاع الصفحة غير المخصصة للشاشة الكاملة وتعديلات التخطيط للحصول على تجارب مشاهدة أفضل.

## خاتمة

يشرح هذا الدليل عملية الوصول إلى خصائص PDF وتعديلها باستخدام Aspose.PDF لجافا. باستخدام هذه الإمكانيات، يمكنك تحسين تفاعل تطبيقاتك مع ملفات PDF، مما يوفر تجربة أكثر ملاءمة للمستخدمين.

لمزيد من الاستكشاف، فكر في الغوص في الوثائق الشاملة لـ Aspose.PDF واستكشاف الميزات الإضافية التي يمكن أن تفيد مشاريعك.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}