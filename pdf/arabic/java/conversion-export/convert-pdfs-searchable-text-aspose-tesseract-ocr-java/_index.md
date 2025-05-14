---
"date": "2025-04-14"
"description": "تعرّف على كيفية تحويل مستندات PDF المبنية على الصور إلى نص قابل للبحث باستخدام Aspose.PDF وTesseract OCR مع Java. يغطي هذا الدليل الإعداد والتنفيذ والتطبيقات العملية."
"title": "كيفية تحويل ملفات PDF إلى نص قابل للبحث باستخدام Aspose.PDF وTesseract OCR في Java"
"url": "/ar/java/conversion-export/convert-pdfs-searchable-text-aspose-tesseract-ocr-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# كيفية تحويل ملفات PDF إلى نص قابل للبحث باستخدام Aspose.PDF وTesseract OCR في Java

## مقدمة

هل تواجه صعوبة في استخراج النصوص من مستندات PDF الممسوحة ضوئيًا أو الصور؟ تحويل هذه الملفات غير القابلة للبحث إلى صيغ قابلة للبحث يُحدث ثورة في استخراج البيانات وأرشفتها وإمكانية الوصول إليها. سيرشدك هذا البرنامج التعليمي إلى كيفية استخدام Aspose.PDF لـ Java مع Tesseract OCR لتحقيق هذا التحويل بكفاءة.

**ما سوف تتعلمه:**
- تحويل صور PDF إلى نص باستخدام Tesseract OCR في Java
- تنفيذ ميزات Aspose.PDF القوية لمعالجة المستندات
- حفظ المستند المعالج كملف PDF قابل للبحث

بفضل هذه المهارات، يمكنك إطلاق العنان لإمكانات مستنداتك. قبل البدء بالتنفيذ، تأكد من جاهزية كل شيء.

## المتطلبات الأساسية

لمتابعة هذا البرنامج التعليمي بشكل فعال، تأكد من أن لديك:
- فهم أساسيات برمجة جافا.
- المعرفة بـ Maven أو Gradle لإدارة التبعيات.
- إصدار مثبت من برنامج Tesseract OCR (متوفر مجانًا من Google).

بالإضافة إلى ذلك، قم بإعداد بيئة التطوير الخاصة بك للتعامل مع مشاريع Java والتأكد من الوصول إلى مكتبة Aspose.PDF.

## إعداد Aspose.PDF لـ Java

لبدء استخدام Aspose.PDF في مشروع Java الخاص بك، أضفه كتبعية عبر Maven أو Gradle:

**مافن:**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**جرادل:**

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### الحصول على الترخيص

يمكنك الحصول على ترخيص تجريبي مجاني لاختبار إمكانيات Aspose.PDF أو شراء ترخيص مؤقت لاختبار موسع. تفضل بزيارة [صفحة ترخيص Aspose](https://purchase.aspose.com/temporary-license/) لمزيد من التفاصيل.

لتهيئة Aspose.PDF وإعداده، تأكد من أن ملف الترخيص جاهز وقم بتطبيقه كما هو موضح:

```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file.lic");
```

## دليل التنفيذ

### الميزة 1: تحويل OCR باستخدام Tesseract

توضح هذه الميزة كيفية تحويل الصور داخل ملف PDF إلى نص باستخدام Tesseract OCR.

#### الخطوة 1: إنشاء معاودة الاتصال لمعالجة التعرف الضوئي على الحروف

وظيفة الاستدعاء `CallBackGetHocr` معالجة كل صورة من ملف PDF:

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.Document.CallBackGetHocr;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Scanner;

CallBackGetHocr cbgh = new CallBackGetHocr() {
    @Override
    public String invoke(BufferedImage img) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        File outputfile = new File(dataDir + "/test.jpg");
        try {
            // اكتب الصورة المخزنة مؤقتًا كملف JPEG
            ImageIO.write(img, "jpg", outputfile);
        } catch (IOException e1) {
            e1.printStackTrace();
        }
        
        try {
            // قم بتنفيذ Tesseract OCR لتحويل الصورة إلى نص وتخزينها بتنسيق HOCR
            java.lang.Process process = Runtime.getRuntime().exec(
                "tesseract " + dataDir + "/test.jpg " + outputDir + "/out hocr"
            );
            process.waitFor();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }

        // قراءة ملف HTML HOCR الناتج في سلسلة
        File file = new File(outputDir + "/out.html");
        StringBuilder fileContents = new StringBuilder((int) file.length());
        Scanner scanner = null;
        try {
            scanner = new Scanner(file);
            String lineSeparator = System.getProperty("line.separator");
            while (scanner.hasNextLine()) {
                fileContents.append(scanner.nextLine() + lineSeparator);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (scanner != null)
                scanner.close();
        }

        // حذف الملفات المؤقتة
        File fileOut = new File(outputDir + "/out.html");
        if (fileOut.exists()) {
            fileOut.delete();
        }
        File fileTest = new File(dataDir + "/test.jpg");
        if (fileTest.exists()) {
            fileTest.delete();
        }
        return fileContents.toString();
    }
};
```

#### الخطوة 2: تحويل ملف PDF إلى نص قابل للبحث

قم بتحميل ملف PDF غير القابل للبحث الموجود وتحويله باستخدام معاودة الاتصال:

```java
// تحديد مسارات الدليل النائبة
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
String outputDir = "YOUR_OUTPUT_DIRECTORY";

// قم بتحميل مستند PDF الموجود
Document doc = new Document(dataDir + "/outFile.pdf");

// تحويل المستند باستخدام معاودة الاتصال لمعالجة التعرف الضوئي على الحروف
doc.convert(cbgh);

// حفظ المستند المُحوّل كملف PDF قابل للبحث
doc.save(outputDir + "/output971.pdf");
```

### الميزة 2: تحويل مستندات PDF وحفظها

بعد تطبيق OCR، احفظ ملف PDF الخاص بك بتنسيق قابل للبحث.

## التطبيقات العملية

1. **الأرشفة:** تحويل المستندات القديمة الممسوحة ضوئيًا إلى تنسيقات قابلة للبحث لاسترجاعها بسهولة.
2. **إمكانية الوصول:** تحسين إمكانية الوصول عن طريق جعل النص متاحًا لقارئات الشاشة.
3. **استخراج البيانات:** استخراج البيانات النصية من التقارير أو الكتب المعتمدة على الصور لتحليلها.
4. **الوثائق القانونية:** تحويل سجلات المحكمة والوثائق القانونية لتحسين إمكانية البحث.
5. **اندماج:** استخدم عملية التحويل في تطبيقات الويب أو أنظمة إدارة المستندات.

## اعتبارات الأداء

- **تحسين جودة الصورة:** توفر الصور ذات الدقة العالية نتائج OCR أكثر دقة ولكنها تتطلب قوة معالجة أكبر.
- **معالجة الدفعات:** تعامل مع ملفات متعددة في دفعات لتحسين الكفاءة.
- **إدارة الذاكرة:** راقب استخدام ذاكرة Java وقم بتكوين أحجام الكومة بشكل مناسب للمستندات الأكبر حجمًا.

## خاتمة

يُعد تحويل ملفات PDF إلى نص قابل للبحث باستخدام Aspose.PDF وTesseract OCR طريقة فعّالة للحصول على معلومات قيّمة من مستندات الصور. باتباع هذا الدليل، يمكنك دمج هذه الميزة في تطبيقاتك بسهولة. استكشف المزيد من خلال تخصيص الكود ليناسب حالات استخدام محددة أو دمجه مع أنظمة أخرى.

هل أنت مستعد لتجربتها؟ ابدأ بتطبيق هذه التقنيات في مشاريعك اليوم!

## قسم الأسئلة الشائعة

**س1: هل يمكنني استخدام Aspose.PDF لـ Java بدون ترخيص؟**
- ج١: نعم، يمكنك تجربة Aspose.PDF بنسخته التجريبية المجانية، والتي تتضمن بعض القيود. للاستفادة الكاملة من جميع وظائفه، يُنصح بالحصول على ترخيص مؤقت أو دائم.

**س2: ما هي تنسيقات الصور التي يدعمها Tesseract OCR؟**
- ج٢: يدعم Tesseract تنسيقات صور متنوعة، بما في ذلك JPEG وPNG وTIFF وBMP. تأكد من استخدام هذه التنسيقات للحصول على أفضل النتائج.

**س3: كيف أتعامل مع الأخطاء أثناء عملية التعرف الضوئي على الحروف؟**
- A3: تنفيذ معالجة قوية للأخطاء باستخدام كتل try-catch حول كود تنفيذ OCR لإدارة الاستثناءات بشكل فعال.

**س4: هل من الممكن دمج هذا الحل في تطبيق الويب؟**
- ج٤: بالتأكيد! يمكنك نشر Aspose.PDF وTesseract في بيئات الخوادم، مما يتيح لك معالجة المستندات عبر واجهات برمجة التطبيقات (APIs) أو التكامل المباشر مع أنظمة الواجهة الخلفية لديك.

**س5: ما هي متطلبات النظام لتشغيل Tesseract OCR؟**
- ج٥: يتطلب Tesseract دعمًا أساسيًا لنظام التشغيل. تأكد من تثبيت Java على جهازك، بالإضافة إلى الأذونات اللازمة لتنفيذ عمليات خارجية مثل Tesseract.

## موارد

- **التوثيق:** استكشف الأدلة التفصيلية ومراجع واجهة برمجة التطبيقات على [توثيق Aspose.PDF](https://reference.aspose.com/pdf/java/).
- **تحميل:** قم بالوصول إلى أحدث إصدارات Aspose.PDF عبر [صفحة التنزيلات](https://releases.aspose.com/pdf/java/).
- **شراء:** احصل على التراخيص مباشرة من [صفحة شراء Aspose](https://purchase.aspose.com/buy).
- **نسخة تجريبية مجانية:** جرب الميزات من خلال النسخة التجريبية المجانية في [تجارب مجانية لـ Aspose](https://releases.aspose.com/pdf/java/#downloads).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}