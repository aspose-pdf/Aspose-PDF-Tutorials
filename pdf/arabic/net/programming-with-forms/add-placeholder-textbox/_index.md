---
title: إنشاء حقل نموذج مربع نص كعنصر نائب قابل للوصول في PDF باستخدام Aspose.Pdf for .NET
weight: 390
limit:
description: دليل خطوة بخطوة لإضافة حقل نموذج مربع نص كعنصر نائب ووضع علامة عليه لتسهيل الوصول باستخدام Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, placeholder textbox, PDF form field, accessibility tagging, PDF form creation, accessible PDF forms]
url: /net/programming-with-forms/add-placeholder-textbox/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: دليل خطوة بخطوة لإضافة حقل نموذج مربع نص كعنصر نائب ووضع علامة عليه
    لتسهيل الوصول باستخدام Aspose.Pdf for .NET.
  headline: إنشاء حقل نموذج مربع نص كعنصر نائب قابل للوصول في PDF باستخدام Aspose.Pdf
    for .NET
  type: TechArticle
- description: دليل خطوة بخطوة لإضافة حقل نموذج مربع نص كعنصر نائب ووضع علامة عليه
    لتسهيل الوصول باستخدام Aspose.Pdf for .NET.
  name: إنشاء حقل نموذج مربع نص كعنصر نائب قابل للوصول في PDF باستخدام Aspose.Pdf
    for .NET
  steps:
  - name: حدد مسارات ملفات الإدخال والإخراج وتحقق من وجود ملف PDF المصدر.
    text: حدد مسارات ملفات الإدخال والإخراج وتحقق من وجود ملف PDF المصدر.
  - name: افتح ملف PDF الموجود وأنشئ كائن Document للعمل معه.
    text: افتح ملف PDF الموجود وأنشئ كائن Document للعمل معه.
  - name: أدرج TextBoxField في الصفحة الأولى، عيّن نص العنصر النائب له، وأضفه إلى
      مجموعة النماذج.
    text: أدرج TextBoxField في الصفحة الأولى، عيّن نص العنصر النائب له، وأضفه إلى
      مجموعة النماذج.
  - name: أنشئ عنصر بنية /Form منطقي، اربطه بشجرة المحتوى الموسوم، واربطه بحقل مربع
      النص.
    text: أنشئ عنصر بنية /Form منطقي، اربطه بشجرة المحتوى الموسوم، واربطه بحقل مربع
      النص.
  - name: احفظ ملف PDF المعدل إلى ملف الإخراج المحدد وأغلق المستند.
    text: احفظ ملف PDF المعدل إلى ملف الإخراج المحدد وأغلق المستند.
  - name: اكتب رسالة تأكيد إلى وحدة التحكم توضح مكان حفظ ملف PDF الجديد.
    text: اكتب رسالة تأكيد إلى وحدة التحكم توضح مكان حفظ ملف PDF الجديد.
  type: HowTo
- questions:
  - answer: الـ `Rectangle` التي تمررها إلى `TextBoxField` تستخدم إحداثيات نسبية إلى
      الزاوية السفلية اليسرى للصفحة؛ إذا كانت القيم خارج أبعاد الصفحة فسيتم قطع الحقل
      أو يصبح غير مرئي، لذا تحقق من الإحداثيات مقابل `firstPage.PageInfo.Width` و
      `firstPage.PageInfo.Height`.
    question: لماذا لا يظهر مربع النص في الموضع الذي أتوقعه على الصفحة؟
  - answer: نعم، يمكنك تعديل `placeholderField.Value` في أي وقت قبل الحفظ؛ ستستبدل
      القيمة الجديدة العنصر النائب المعروض عند فتح ملف PDF.
    question: هل يمكنني تغيير نص العنصر النائب بعد إضافة الحقل إلى النموذج؟
  - answer: كل تعليقة واجهة (مثل `TextBoxField`) يجب أن يكون لها `FormElement` منطقي
      خاص بها؛ أنشئ عنصرًا جديدًا باستخدام `taggedContent.CreateFormElement()`، أضفه
      إلى جذر البنية، واستدعِ `logicalFormElement.Tag(yourField)` لكل حقل.
    question: هل أحتاج إلى إنشاء `FormElement` منفصل لكل حقل نموذج أضيفه؟
  - answer: يقوم Aspose.Pdf تلقائيًا بإنشاء بنية موسومة عند الوصول إلى `pdfDocument.TaggedContent`،
      لذا يعمل البرنامج التعليمي حتى مع ملف PDF مصدر غير موسوم؛ سيتم إنشاء `RootElement`
      في الوقت الفعلي.
    question: ماذا يحدث إذا لم يكن ملف PDF المصدر مُوسومًا مسبقًا – هل سيظل الكود
      يعمل؟
  type: FAQPage
images:
- /net/programming-with-forms/add-placeholder-textbox/og-image.png
og_title: إضافة مربع نص كعنصر نائب قابل للوصول إلى PDF
og_description: تعلم كيفية إدراج مربع نص كعنصر نائب ووضع علامة عليه لتسهيل الوصول في PDF باستخدام Aspose.Pdf for .NET.
og_image_alt: دليل يوضح كيفية إضافة حقل نموذج مربع نص كعنصر نائب ووضع علامة عليه لتسهيل الوصول في PDF باستخدام Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء حقل نموذج مربع نص كعنصر نائب قابل للوصول في PDF باستخدام Aspose.Pdf
يُرشدك هذا البرنامج التعليمي إلى إضافة حقل نموذج مربع نص كعنصر نائب إلى مستند PDF وتطبيق العلامات المناسبة لتسهيل الوصول. ستظهر لك الشيفرة الدقيقة المطلوبة لإدراج مربع النص، تعيين نص العنصر النائب له، ووضع علامة عليه حتى يتمكن قارئ الشاشة من التعرف على الحقل. اتبع الخطوات لجعل نماذج PDF الخاصة بك عملية وقابلة للوصول.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-forms/add-placeholder-textbox" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: لماذا لا يظهر مربع النص في الموضع الذي أتوقعه على الصفحة؟**  
A: الـ `Rectangle` التي تمررها إلى `TextBoxField` تستخدم إحداثيات نسبية إلى الزاوية السفلية اليسرى للصفحة؛ إذا كانت القيم خارج أبعاد الصفحة فسيتم قطع الحقل أو يصبح غير مرئي، لذا تحقق من الإحداثيات مقابل `firstPage.PageInfo.Width` و `firstPage.PageInfo.Height`.

**Q: هل يمكنني تغيير نص العنصر النائب بعد إضافة الحقل إلى النموذج؟**  
A: نعم، يمكنك تعديل `placeholderField.Value` في أي وقت قبل الحفظ؛ ستستبدل القيمة الجديدة العنصر النائب المعروض عند فتح ملف PDF.

**Q: هل أحتاج إلى إنشاء `FormElement` منفصل لكل حقل نموذج أضيفه؟**  
A: كل تعليقة واجهة (مثل `TextBoxField`) يجب أن يكون لها `FormElement` منطقي خاص بها؛ أنشئ عنصرًا جديدًا باستخدام `taggedContent.CreateFormElement()`، أضفه إلى جذر البنية، واستدعِ `logicalFormElement.Tag(yourField)` لكل حقل.

**Q: ماذا يحدث إذا لم يكن ملف PDF المصدر مُوسومًا مسبقًا – هل سيظل الكود يعمل؟**  
A: يقوم Aspose.Pdf تلقائيًا بإنشاء بنية موسومة عند الوصول إلى `pdfDocument.TaggedContent`، لذا يعمل البرنامج التعليمي حتى مع ملف PDF مصدر غير موسوم؛ سيتم إنشاء `RootElement` في الوقت الفعلي.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}