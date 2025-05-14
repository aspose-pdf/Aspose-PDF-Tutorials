---
"description": "تعرّف على كيفية إضافة حقول نماذج تفاعلية إلى مستندات PDF باستخدام Java وAspose.PDF لـ Java. أنشئ نماذج PDF سهلة الاستخدام بكل سهولة."
"linktitle": "إضافة حقل النموذج في مستند PDF باستخدام Java"
"second_title": "واجهة برمجة تطبيقات معالجة PDF في Java لـ Aspose.PDF"
"title": "إضافة حقل النموذج في مستند PDF باستخدام Java"
"url": "/ar/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة حقل النموذج في مستند PDF باستخدام Java


## مقدمة

تُحسّن إضافة حقول النماذج إلى مستند PDF من وظائفه، إذ تتيح للمستخدمين إدخال البيانات مباشرةً فيه. يُعدّ هذا مفيدًا للغاية لأغراض متعددة، مثل إنشاء نماذج قابلة للتعبئة، أو استبيانات، أو تقارير بمحتوى من إنشاء المستخدم.

سنستخدم Aspose.PDF لجافا، وهي مكتبة فعّالة تُسهّل التعامل مع ملفات PDF في تطبيقات جافا. مع Aspose.PDF، يمكنك بسهولة إنشاء مستندات PDF وتعديلها ومعالجتها، بما في ذلك إضافة حقول النماذج ديناميكيًا.

## تهيئة البيئة

قبل التعمق في الكود، عليك إعداد بيئة التطوير الخاصة بك. اتبع الخطوات التالية:

1. تنزيل Aspose.PDF لجافا: تفضل بزيارة موقع Aspose الإلكتروني وتنزيل أحدث إصدار من Aspose.PDF لجافا. يمكنك العثور عليه [هنا](https://releases.aspose.com/pdf/java/).

2. تثبيت Aspose.PDF: بعد التنزيل، قم بتثبيت Aspose.PDF باتباع تعليمات التثبيت المقدمة على الموقع الإلكتروني.

3. إنشاء مشروع Java: قم بإنشاء مشروع Java جديد في بيئة التطوير المتكاملة (IDE) المفضلة لديك وقم بتضمين مكتبة Aspose.PDF في مشروعك.

## إنشاء مستند PDF جديد

لنبدأ بإنشاء مستند PDF جديد. في هذا المثال، سننشئ ملف PDF بسيطًا بعنوان وبعض التعليمات.

```java
// استيراد مكتبة Aspose.PDF
import com.aspose.pdf.*;

public class AddFormFieldPDF {
    public static void main(String[] args) {
        // إنشاء مستند PDF جديد
        Document doc = new Document();

        // إضافة صفحة إلى المستند
        Page page = doc.getPages().add();

        // أضف عنوانًا
        TextFragment title = new TextFragment("Feedback Form");
        title.getTextState().setFontSize(18);
        title.getTextState().setFont(FontRepository.findFont("Arial"));
        page.getParagraphs().add(title);

        // إضافة التعليمات
        TextFragment instructions = new TextFragment("Please provide your feedback below:");
        instructions.getTextState().setFontSize(12);
        page.getParagraphs().add(instructions);

        // حفظ المستند في ملف
        doc.save("FeedbackForm.pdf");
    }
}
```

في مقتطف التعليمات البرمجية هذا، نقوم بإنشاء مستند PDF جديد، وإضافة صفحة، وإدراج عنوان وبعض التعليمات.

## إضافة حقول النموذج

الآن، لننتقل إلى إضافة حقول النماذج إلى مستند PDF. سنضيف حقولًا نصية، ومربعات اختيار، وأزرار اختيار لإنشاء نموذج ملاحظات تفاعلي.

### حقول النص

تتيح حقول النص للمستخدمين إدخال نص. إليك كيفية إضافة حقل نص:

```java
// إنشاء حقل نصي
TextField textField = new TextField(page, new Rectangle(100, 300, 200, 20));
textField.getPdfObject().setBorderStyle(new BorderStyle(1)); // تعيين نمط الحدود
textField.setPartialName("txtName"); // تعيين اسم الحقل
textField.setMultiline(false); // تعطيل تعدد الأسطر
page.getAnnotations().add(textField);
```

### مربعات الاختيار

تُستخدم مربعات الاختيار للخيارات الثنائية (مثل أسئلة نعم/لا). إليك كيفية إضافة مربع اختيار:

```java
// إنشاء مربع اختيار
CheckboxField checkboxField = new CheckboxField(page, new Rectangle(100, 250, 20, 20));
checkboxField.setPartialName("chkAgree"); // تعيين اسم الحقل
checkboxField.setChecked(false); // لم يتم التحقق منه في البداية
page.getAnnotations().add(checkboxField);
```

### أزرار الراديو

تُستخدم أزرار الاختيار عند الحاجة لاختيار خيار واحد من مجموعة. كل خيار هو زر اختيار منفصل، ولكنه ينتمي إلى المجموعة نفسها. إليك كيفية إضافة أزرار الاختيار:

```java
// إنشاء أزرار الراديو
RadioButtonOptionField option1 = new RadioButtonOptionField(page, new Rectangle(100, 200, 20, 20));
RadioButtonOptionField option2 = new RadioButtonOptionField(page, new Rectangle(100, 180, 20, 20));
option1.setPartialName("optYes"); // تعيين اسم الحقل للخيار 1
option2.setPartialName("optNo"); // تعيين اسم الحقل للخيار 2

// إضافة خيارات إلى مجموعة أزرار الاختيار
RadioButtonOptionField[] options = {option1, option2};
RadioButtonField radioButtonField = new RadioButtonField(page, options);
page.getAnnotations().add(radioButtonField);
```

باستخدام أمثلة التعليمات البرمجية هذه، يمكنك إضافة حقول نصية ومربعات اختيار وأزرار اختيار إلى مستند PDF. تأكد من تخصيص خصائصها حسب الحاجة، مثل أسماء الحقول والقيم الافتراضية.

## تخصيص حقول النموذج

يتيح لك تخصيص حقول النماذج التحكم في مظهرها وسلوكها. يمكنك تغيير خصائص مثل حجم الخط، ولون النص، ونمط الحدود، وغيرها.

### تغيير خصائص الحقل

لنفترض أنك تريد تغيير حجم الخط ولون النص في حقل النص:

```java
textField.getTextState().setFontSize(14);
textField.getTextState().setForegroundColor(Color.getGreen());
```

### التحقق من صحة الحقل

يمكنك أيضًا ضبط قواعد التحقق من صحة حقول النماذج. على سبيل المثال، يمكنك مطالبة المستخدمين بإدخال عنوان بريد إلكتروني صالح في حقل نصي:

```java
textField.getValidation().add(ValidationType.EMAIL);
```

## تعيين قيم الحقول

لملء حقول النماذج بالبيانات مسبقًا، يمكنك تعيين قيمها الافتراضية برمجيًا. هذا مفيد لإنشاء قوالب أو ملء معلومات معروفة مسبقًا.

```java
textField.setValue("John Doe"); // تعيين القيمة الافتراضية لحقل النص
checkboxField.setChecked(true); // حدد مربع الاختيار افتراضيًا
```

## إرسال النموذج والتحقق منه

إن إضافة حقول النموذج ليست سوى نصف القصة؛ ستحتاج أيضًا إلى

 لتمكين إرسال النموذج والتحقق من صحته.

### إرسال النموذج

للسماح للمستخدمين بإرسال بيانات النموذج، يجب تحديد إجراء، مثل إرسال بريد إلكتروني أو إرساله إلى خادم ويب. إليك مثال لكيفية إعداد زر الإرسال:

```java
ButtonField submitButton = new ButtonField(page, new Rectangle(100, 50, 80, 30));
submitButton.getPdfObject().setBorderStyle(new BorderStyle(1));
submitButton.getActions().getOnPushButton().add(new SubmitFormAction("https://yourserver.com/submit، SubmitFormActionType.URL، "FeedbackForm.pdf"));
page.getAnnotations().add(submitButton);
```

### التحقق من صحة النموذج

يضمن التحقق أن مدخلات المستخدم تستوفي معايير محددة. على سبيل المثال، يمكنك التحقق من حقل رقم الهاتف لقبول الأرقام فقط:

```java
textField.getValidation().add(ValidationType.NUMBER);
```

## الحفظ والتصدير

بعد إنشاء مستند PDF وتخصيصه باستخدام حقول النماذج، حان وقت حفظه أو تصديره. يوفر Aspose.PDF خيارات متعددة لذلك.

### حفظ في ملف محلي

لحفظ مستند PDF في ملف محلي، استخدم الكود التالي:

```java
doc.save("FeedbackForm.pdf");
```

### حفظ في تيار

لحفظ مستند PDF في تيار، يمكنك استخدام `OutputStream` فصل:

```java
OutputStream outputStream = new FileOutputStream("FeedbackForm.pdf");
doc.save(outputStream);
outputStream.close();
```

## خاتمة

في هذا الدليل الشامل، استكشفنا كيفية إضافة حقول نماذج إلى مستند PDF باستخدام Java وAspose.PDF لـ Java. تعلمت كيفية إنشاء حقول نصية، ومربعات اختيار، وأزرار اختيار، وتخصيص خصائصها، وتعيين قيم افتراضية، وتفعيل إرسال النماذج والتحقق منها، وحفظ/تصدير مستند PDF.

## الأسئلة الشائعة

### كيف يمكنني إعداد قائمة منسدلة في نموذج PDF؟

لإنشاء قائمة منسدلة (مربع منسدل) في نموذج PDF، يمكنك استخدام `ComboBoxField` الفئة التي يوفرها Aspose.PDF لجافا. اتبع نفس النهج الموضح لحقول النماذج الأخرى، وقم بتخصيص الخيارات باستخدام `AddItem` الطريقة. يمكنك العثور على وثائق مفصلة حول هذا الموضوع على موقع Aspose.

### هل Aspose.PDF for Java متوافق مع مكتبات Java وأطر العمل الأخرى؟

نعم، Aspose.PDF لجافا متوافق مع مختلف مكتبات وأطر عمل جافا. يمكنك دمجه في تطبيقات جافا، سواء كنت تستخدم Spring أو JavaFX أو أطر عمل شائعة أخرى. تأكد من مراجعة الوثائق والموارد للاطلاع على إرشادات التكامل المحددة.

### هل يمكنني حماية نموذج PDF تم إنشاؤه باستخدام Aspose.PDF لـ Java بكلمة مرور؟

بالتأكيد! يتيح لك Aspose.PDF لجافا حماية مستندات PDF، بما في ذلك النماذج، بكلمة مرور. يمكنك تعيين كلمات مرور على مستوى المستخدم ومستوى المالك لتقييد الوصول والأذونات. راجع الوثائق للاطلاع على تعليمات مفصلة حول كيفية تطبيق ميزة الأمان هذه.

### كيف يمكنني استخراج البيانات المرسلة من خلال نموذج PDF؟

لاستخراج البيانات المُرسلة عبر نموذج PDF، ستحتاج إلى إدارة عملية إرسال النموذج على خادمك أو واجهة تطبيقك. عندما يُرسل المستخدم النموذج، يمكنك استلام البيانات ومعالجتها حسب الحاجة. يوفر Aspose.PDF الأدوات اللازمة لاستخراج بيانات النموذج برمجيًا من مستند PDF على جانب الخادم.

### هل يمكنني إنشاء نماذج PDF بشكل ديناميكي استنادًا إلى إدخال المستخدم؟

نعم، يمكنك إنشاء نماذج PDF ديناميكيًا بناءً على مدخلات المستخدم باستخدام Aspose.PDF لجافا. بناءً على مدخلات المستخدم أو منطق التطبيق، يمكنك إنشاء مستندات PDF بحقول وتخطيطات نماذج متنوعة. تتيح هذه المرونة إنشاء نماذج مخصصة مصممة خصيصًا لاحتياجات المستخدم أو سيناريوهاته.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}