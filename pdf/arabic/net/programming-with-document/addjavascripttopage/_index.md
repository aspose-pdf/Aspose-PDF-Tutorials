---
"description": "تعرّف على كيفية إضافة جافا سكريبت إلى ملف PDF باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة مع دروس برمجية لكتابة النصوص البرمجية على مستوى المستندات والصفحات."
"linktitle": "إضافة ملف PDF Java Script"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "إضافة Java Script إلى ملف PDF"
"url": "/ar/net/programming-with-document/addjavascripttopage/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة Java Script إلى ملف PDF

## مقدمة

هل تساءلت يومًا عن كيفية تحسين ملفات PDF الخاصة بك بعناصر تفاعلية مثل التنبيهات المنبثقة أو وظائف الطباعة التلقائية؟ حسنًا، الخبر السار هو أنه يمكنك ذلك! باستخدام Aspose.PDF لـ .NET، يمكنك إضافة JavaScript بسلاسة إلى مستندات PDF الخاصة بك. سواء كنت تقوم بأتمتة المهام أو إنشاء تجارب مستخدم ديناميكية، فإن تضمين JavaScript في ملفات PDF يمنح ملفاتك مستوى إضافيًا من الأداء.

## المتطلبات الأساسية

قبل أن ننتقل إلى جزء الترميز، هناك بعض الأشياء التي ستحتاج إلى إعدادها:

- Aspose.PDF لـ .NET: قم بتنزيل المكتبة من [إصدارات Aspose](https://releases.aspose.com/pdf/net/) أو احصل على [نسخة تجريبية مجانية](https://releases.aspose.com/).
- بيئة التطوير: أي بيئة تطوير متكاملة متوافقة مع .NET مثل Visual Studio.
- المعرفة الأساسية بلغة C#: يفترض هذا الدليل أنك على دراية بقواعد اللغة الأساسية بلغة C#.
- رخصة مؤقتة (اختياري): يمكنك الحصول على [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) إذا كنت تريد تجنب القيود أثناء التطوير.

## استيراد الحزم

قبل البدء بكتابة الكود، ستحتاج إلى استيراد مساحات الأسماء اللازمة من مكتبة Aspose.PDF. ستتيح لك هذه المساحات التعامل مع ملفات PDF وإضافة إجراءات JavaScript بسهولة.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

الآن بعد أن قمت باستيراد مساحات الأسماء الصحيحة، فأنت الآن جاهز لبدء الترميز.

## الخطوة 1: تحميل ملف PDF موجود

أولاً، عليك تحميل ملف PDF الذي تريد إضافة جافا سكريبت إليه. هذه الخطوة تُمهّد الطريق لجميع التعديلات الإضافية. تخيّل أن لديك ملف PDF وتريد تحسينه بوظائف ديناميكية، مثل طباعة المستند تلقائيًا عند فتحه.

إليك كيفية تحميل ملف PDF هذا:

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// تحميل ملف PDF موجود
Document doc = new Document(dataDir + "input.pdf");
```

في مقتطف الكود هذا، نستخدم `Document` لتحميل ملف PDF موجود من الدليل المحدد. تأكد من استبدال `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي لملف PDF الخاص بك.

## الخطوة 2: إضافة JavaScript على مستوى المستند

الآن، لنُضِف بعض أكواد جافا سكريبت التي ستُفعَّل عند فتح المستند. في هذا المثال، سنكتب نصًا برمجيًا يفتح نافذة الطباعة بمجرد فتح المستخدم لملف PDF.

جافا سكريبت على مستوى المستند مثالية للإجراءات التي تريد تطبيقها على ملف PDF بأكمله. تخيل الأمر كأنك تقوم بإعداد قاعدة عامة لمستندك.

هذا هو الكود:

```csharp
// إضافة JavaScript على مستوى المستند
// إنشاء JavascriptAction باستخدام بيان JavaScript المطلوب
JavascriptAction javaScript = new JavascriptAction("this.print({bUI:true,bSilent:false,bShrinkToFit:true});");

// تعيين كائن JavascriptAction إلى OpenAction للمستند
doc.OpenAction = javaScript;
```

في هذه الخطوة، نقوم بإنشاء `JavascriptAction` كائن يُعرّف دالة JavaScript لفتح مربع حوار الطباعة عند فتح المستند. `doc.OpenAction` يتم بعد ذلك تعيين هذا الإجراء JavaScript للخاصية.

## الخطوة 3: إضافة JavaScript على مستوى الصفحة

ليس بالضرورة أن يؤثر كل إجراء على المستند بأكمله. أحيانًا، قد ترغب في تنفيذ إجراءات محددة عند فتح أو إغلاق صفحات معينة. هنا، سنُعدّ إجراءات جافا سكريبت عند فتح وإغلاق صفحة معينة (لنفترض الصفحة ٢).

يُعدّ جافا سكريبت على مستوى الصفحة مفيدًا للتفاعلات المُستهدفة. قد يشمل ذلك أي شيء، بدءًا من عرض رسالة عند انتقال المستخدم إلى صفحة، وصولًا إلى إجراءات مُخصصة مثل ملء حقول النماذج تلقائيًا.

إليك كيفية القيام بذلك:

```csharp
// إضافة JavaScript على مستوى الصفحة
doc.Pages[2].Actions.OnOpen = new JavascriptAction("app.alert('Page 2 opened')");
doc.Pages[2].Actions.OnClose = new JavascriptAction("app.alert('Page 2 closed')");
```

في مقتطف التعليمات البرمجية هذا، نضيف إجراءين JavaScript:
1. إجراء OnOpen: يعرض تنبيهًا يقول "تم فتح الصفحة 2" عندما يفتح المستخدم الصفحة 2.
2. إجراء OnClose: يعرض تنبيهًا يقول "تم إغلاق الصفحة 2" عندما ينتقل المستخدم بعيدًا عن الصفحة 2.

يُضيف هذا مستوىً من التفاعلية إلى ملف PDF الخاص بك. تخيّل توجيه المستخدم عبر سلسلة من الخطوات على صفحات مختلفة، مع ظهور تنبيهات عند دخوله أو مغادرته صفحة.

## الخطوة 4: حفظ مستند PDF

لقد أضفتَ الآن جافا سكريبت إلى كلٍّ من المستند والصفحات المُحدَّدة. الخطوة الأخيرة هي حفظ ملف PDF المُعَدَّل في المكان المُناسب. هذا الجزء بسيط ولكنه بالغ الأهمية - لا تنسَ حفظ عملك!

هذا هو الكود:

```csharp
// تحديد مسار ملف الإخراج
dataDir = dataDir + "JavaScript-Added_out.pdf";

// احفظ مستند PDF المحدث
doc.Save(dataDir);

Console.WriteLine("\nJavaScript added successfully to the PDF.\nFile saved at " + dataDir);
```

في هذا المقطع، نقوم بحفظ المستند المحدث باستخدام JavaScript المضاف إلى ملف جديد يسمى `"JavaScript-Added_out.pdf"`يضمن هذا عدم استبدال ملفك الأصلي، ويمنحك نسخة احتياطية للعمل عليها.

## خاتمة

إضافة جافا سكريبت إلى ملفات PDF باستخدام Aspose.PDF لـ .NET طريقة فعّالة لإنشاء ملفات PDF تفاعلية وديناميكية. سواء كنت تُؤتمت مهام مثل الطباعة أو تُنشئ تنبيهات مخصصة، فإن إمكانية تضمين جافا سكريبت في ملف PDF تجعل مستنداتك أكثر جاذبية وفعالية.

## الأسئلة الشائعة

### هل يمكنني إضافة إجراءات JavaScript متعددة إلى صفحات مختلفة في ملف PDF؟
نعم، يمكنك تعيين إجراءات JavaScript مختلفة لصفحات فردية أو للمستند بأكمله.

### هل من الممكن إزالة JavaScript من ملف PDF بعد إضافته؟
نعم، يمكنك إزالة أو تعديل إجراءات JavaScript الموجودة عن طريق مسح `Actions` خصائص المستند أو الصفحة.

### ما هي أنواع وظائف JavaScript التي يمكنني استخدامها في ملف PDF؟
يمكنك استخدام أي JavaScript يدعمه محرك JavaScript الخاص بـ Adobe Acrobat، مثل الطباعة والتنبيهات ومعالجة النماذج.

### هل يعمل JavaScript في جميع برامج عرض PDF؟
تعمل معظم إجراءات JavaScript في برامج عرض PDF التي تدعم ملفات PDF التفاعلية، مثل Adobe Acrobat. مع ذلك، قد لا تدعم بعض برامج قراءة PDF الأساسية JavaScript.

### هل يمكنني تشغيل إجراءات JavaScript استنادًا إلى إدخال المستخدم في ملف PDF؟
نعم، يمكنك ربط JavaScript بحقول النموذج لتشغيل الإجراءات استنادًا إلى إدخال المستخدم.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}