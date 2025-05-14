---
"description": "تعرّف على كيفية تحسين مستندات PDF باستخدام الإشارات المرجعية الفرعية باستخدام Aspose.PDF لجافا. دليل خطوة بخطوة مع أمثلة برمجية لتحسين التنقل والتنظيم."
"linktitle": "إضافة إشارات مرجعية فرعية إلى ملفات PDF"
"second_title": "واجهة برمجة تطبيقات معالجة PDF في Java لـ Aspose.PDF"
"title": "إضافة إشارات مرجعية فرعية إلى ملفات PDF"
"url": "/ar/java/pdf-bookmarks/add-child-bookmarks-pdfs/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة إشارات مرجعية فرعية إلى ملفات PDF


## مقدمة حول إضافة إشارات مرجعية فرعية إلى ملفات PDF

في هذه المقالة، سنستكشف كيفية إضافة إشارات مرجعية فرعية إلى مستندات PDF باستخدام Aspose.PDF لجافا. تُعد الإشارات المرجعية الفرعية طريقة سهلة لتنظيم محتوى مستند PDF والتنقل فيه، مما يُسهّل على المستخدمين العثور على أقسام أو مواضيع محددة داخل المستند.

## المتطلبات الأساسية

قبل أن نتعمق في التنفيذ، تأكد من توفر المتطلبات الأساسية التالية:

- بيئة تطوير Java مثبتة على نظامك.
- مكتبة Aspose.PDF لجافا. يمكنك تنزيلها من [هنا](https://releases.aspose.com/pdf/java/).

## تهيئة البيئة

1. قم بتنزيل مكتبة Aspose.PDF لـJava من الرابط المقدم.
2. أضف المكتبة إلى مشروع Java الخاص بك.

الآن، لنبدأ بإنشاء مستند PDF جديد وإضافة إشارات مرجعية فرعية إليه خطوة بخطوة.

## إنشاء مستند PDF جديد

للبدء، نحتاج إلى تهيئة مستند PDF وإضافة صفحات إليه. إليك مقتطف الكود للبدء:

```java
// تهيئة مستند PDF
Document pdfDocument = new Document();

// إضافة صفحات إلى ملف PDF
pdfDocument.getPages().add();
pdfDocument.getPages().add();
```

في هذا المثال، قمنا بإنشاء مستند PDF جديد وأضفنا إليه صفحتين.

## إضافة إشارات مرجعية للوالدين

تُعدّ العلامات المرجعية الرئيسية الأقسام أو الفئات الرئيسية في مستند PDF. لنُنشئ بعض العلامات المرجعية الرئيسية:

```java
// إنشاء إشارات مرجعية للوالدين
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);
```

لقد أضفنا إشارتين مرجعيتين رئيسيتين، "الإشارة المرجعية الرئيسية 1" و"الإشارة المرجعية الرئيسية 2".

## إضافة إشارات مرجعية فرعية

الآن، حان وقت إضافة إشارات مرجعية فرعية إلى الإشارات المرجعية الأصلية التي أنشأناها سابقًا. تُمثل الإشارات المرجعية الفرعية مواضيع أو أقسامًا فرعية محددة داخل كل إشارة مرجعية أصلية. إليك كيفية القيام بذلك:

```java
// إضافة إشارات مرجعية فرعية إلى الإشارة المرجعية الأصلية 1
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// إضافة إشارات مرجعية فرعية إلى الإشارة المرجعية الأصلية 2
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);
```

لقد أضفنا إشارات مرجعية فرعية إلى كل من "الإشارة المرجعية الأصلية 1" و"الإشارة المرجعية الأصلية 2".

## تخصيص مظهر الإشارة المرجعية

يمكنك تخصيص مظهر الإشارات المرجعية بتغيير نصها ونمطها. كما يمكنك إضافة أيقونات إليها لتحسين عرضها بصريًا. إليك مثال على كيفية القيام بذلك:

```java
// تخصيص مظهر الإشارة المرجعية
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());
```

في هذا المثال، قمنا بجعل الإشارة المرجعية الأصلية مائلة، وقمنا بتغيير لون نص الإشارة المرجعية الفرعية إلى اللون الأخضر، وأضفنا رمزًا مائلًا إلى الإشارة المرجعية الفرعية.

## التعامل مع الأحداث

يمكن أيضًا ربط الإشارات المرجعية بإجراءات. على سبيل المثال، يمكنك إضافة إجراءات تُفعّل عند نقر المستخدم على إشارة مرجعية. إليك كيفية التعامل مع أحداث نقر الإشارات المرجعية:

```java
// إضافة إجراء إلى الإشارة المرجعية
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);
```

في هذا الكود، أضفنا إجراء "GoTo" إلى إشارة مرجعية فرعية والتي ستأخذ المستخدم إلى الصفحة الثانية من ملف PDF عند النقر عليها.

## حفظ ملف PDF

بمجرد إضافة جميع الإشارات المرجعية الضرورية وتخصيص مظهرها وإجراءاتها، يمكنك حفظ مستند PDF المعدل:

```java
// حفظ مستند PDF
pdfDocument.save("output.pdf");
```

الآن أصبح مستند PDF الخاص بك مع الإشارات المرجعية الفرعية جاهزًا.

## الكود المصدر الكامل

فيما يلي الكود المصدر الكامل لإضافة إشارات مرجعية فرعية إلى مستند PDF باستخدام Aspose.PDF لـ Java:

```java
// تهيئة مستند PDF
Document pdfDocument = new Document();

// إضافة صفحات إلى ملف PDF
pdfDocument.getPages().add();
pdfDocument.getPages().add();

// إنشاء إشارات مرجعية للوالدين
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);

// إضافة إشارات مرجعية فرعية إلى الإشارة المرجعية الأصلية 1
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// إضافة إشارات مرجعية فرعية إلى الإشارة المرجعية الأصلية 2
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);

// تخصيص مظهر الإشارة المرجعية
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());

// إضافة إجراء إلى الإشارة المرجعية
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);

// حفظ مستند PDF
pdfDocument.save("output.pdf");
```

## خاتمة

إضافة إشارات مرجعية فرعية إلى ملفات PDF باستخدام Aspose.PDF لجافا ميزة فعّالة تُحسّن سهولة التنقل وتنظيم مستنداتك. باتباع الخطوات الموضحة في هذه المقالة، يمكنك إنشاء ملفات PDF منظمة بشكل جيد مع إشارات مرجعية فرعية، وتخصيص مظهرها، وحتى إضافة إجراءات لتحسين تجربة المستخدم.

## الأسئلة الشائعة

### كيف يمكنني تنزيل Aspose.PDF لـJava؟

يمكنك تنزيل Aspose.PDF لـ Java من موقع الويب [هنا](https://releases.aspose.com/pdf/java/).

### هل يتم دعم الإشارات المرجعية للأطفال في كافة برامج عرض PDF؟

نعم، يتم دعم الإشارات المرجعية الفرعية في معظم برامج عرض PDF الحديثة، كما توفر تجربة مستخدم محسنة للتنقل عبر مستندات PDF.

### هل يمكنني تخصيص مظهر الإشارات المرجعية بشكل أكبر؟

نعم، يمكنك تخصيص مظهر الإشارات المرجعية عن طريق ضبط أنماط النص والألوان والأيقونات لتناسب تصميم مستندك.

### ما هي الإجراءات الأخرى التي يمكنني إضافتها إلى الإشارات المرجعية؟

بالإضافة إلى إجراءات "GoTo"، يمكنك إضافة إجراءات مثل إجراءات "URI" لفتح روابط الويب أو إجراءات "JavaScript" لتنفيذ البرامج النصية المخصصة عند النقر فوق إشارة مرجعية.

### هل Aspose.PDF لـ Java مناسب للمشاريع التجارية؟

نعم، يعد برنامج Aspose.PDF for Java مناسبًا للمشاريع الشخصية والتجارية على حد سواء، كما أنه يوفر مجموعة واسعة من الميزات لمعالجة وإنشاء ملفات PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}