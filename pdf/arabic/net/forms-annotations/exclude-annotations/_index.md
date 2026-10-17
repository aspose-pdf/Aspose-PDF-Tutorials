---
title: مقارنة PDF جنبًا إلى جنب مع استبعاد التعليقات التوضيحية باستخدام Aspose.Pdf for .NET
weight: 101
limit:
description: دليل خطوة بخطوة لمقارنة ملفات PDF واستبعاد مناطق التعليقات باستخدام Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: دليل خطوة بخطوة لمقارنة ملفات PDF واستبعاد مناطق التعليقات باستخدام
    Aspose.Pdf for .NET.
  headline: مقارنة PDF جنبًا إلى جنب مع استبعاد التعليقات التوضيحية باستخدام Aspose.Pdf
    for .NET
  type: TechArticle
- description: دليل خطوة بخطوة لمقارنة ملفات PDF واستبعاد مناطق التعليقات باستخدام
    Aspose.Pdf for .NET.
  name: مقارنة PDF جنبًا إلى جنب مع استبعاد التعليقات التوضيحية باستخدام Aspose.Pdf
    for .NET
  steps:
  - name: حدد مسارات الملفات لـ PDF الأساسي، وPDF الثانوي، وPDF الفرق الناتج.
    text: حدد مسارات الملفات لـ PDF الأساسي، وPDF الثانوي، وPDF الفرق الناتج.
  - name: تحقق من وجود ملفي PDF المدخلين، وإذا كان أحدهما مفقودًا أوقف العملية مع
      رسالة خطأ.
    text: تحقق من وجود ملفي PDF المدخلين، وإذا كان أحدهما مفقودًا أوقف العملية مع
      رسالة خطأ.
  - name: افتح ملفي PDF ككائنات Document (pdfA و pdfB) داخل كتلة using حتى يتم تحريرهما
      تلقائيًا.
    text: افتح ملفي PDF ككائنات Document (pdfA و pdfB) داخل كتلة using حتى يتم تحريرهما
      تلقائيًا.
  - name: اجمع مستطيلات الحدود لكل تعليق توضيحي في pdfA وخزنها في ignoredRectsA.
    text: اجمع مستطيلات الحدود لكل تعليق توضيحي في pdfA وخزنها في ignoredRectsA.
  - name: اجمع مستطيلات الحدود لكل تعليق توضيحي في pdfB وخزنها في ignoredRectsB.
    text: اجمع مستطيلات الحدود لكل تعليق توضيحي في pdfB وخزنها في ignoredRectsB.
  - name: أنشئ كائن SideBySideComparisonOptions وعيّن مستطيلات التعليقات التي تم جمعها
      مسبقًا إلى ExcludeAreas1 و ExcludeAreas2 بحيث يتم تجاهل تلك المناطق أثناء المقارنة.
    text: أنشئ كائن SideBySideComparisonOptions وعيّن مستطيلات التعليقات التي تم جمعها
      مسبقًا إلى ExcludeAreas1 و ExcludeAreas2 بحيث يتم تجاهل تلك المناطق أثناء المقارنة.
  - name: نفّذ مقارنة PDF جنبًا إلى جنب باستخدام كائنَي Document والخيارات المُكوَّنة،
      واكتب النتيجة إلى outputPdf.
    text: نفّذ مقارنة PDF جنبًا إلى جنب باستخدام كائنَي Document والخيارات المُكوَّنة،
      واكتب النتيجة إلى outputPdf.
  - name: حرّر كائنات Document واخرج من كتلة using.
    text: حرّر كائنات Document واخرج من كتلة using.
  - name: اطبع رسالة تأكيد تشير إلى أن المقارنة انتهت وأين تم حفظ ملف PDF للفرق.
    text: اطبع رسالة تأكيد تشير إلى أن المقارنة انتهت وأين تم حفظ ملف PDF للفرق.
  type: HowTo
- questions:
  - answer: نعم. الكود ببساطة لا يضيف أي مستطيلات إلى قائمة `ignoredRects` المقابلة،
      لذا تتلقى `ExcludeAreas1`/`ExcludeAreas2` مصفوفة فارغة ويعالج المقارن الصفحة
      بأكملها.
    question: ماذا يحدث إذا كانت صفحة PDF لا تحتوي على تعليقات توضيحية – هل ستظل المقارنة
      تعمل؟
  - answer: عيّن `ExcludeAreas1` (أو `ExcludeAreas2`) إلى المستطيلات المجمعة واترك
      الخاصية الأخرى كمصفوفة فارغة؛ سيستبعد المقارن المناطق فقط في المستند المحدد.
    question: هل يمكنني استبعاد التعليقات فقط من مستند واحد مع الحفاظ على تعليقات
      المستند الآخر في الفرق؟
  - answer: المستطيلات المتداخلة تُدمج داخليًا بواسطة المقارن، لذا يتم استبعاد حدود
      التعليقات المتداخلة بأمان دون عدّ مزدوج.
    question: هل تتسبب مستطيلات التعليقات المتداخلة في أي مشاكل مع `ExcludeAreas`؟
  - answer: نعم، عيّن `compareOpts.ExcludeTables = true;` – هذه العلامة تعمل جنبًا
      إلى جنب مع `ExcludeAreas1`/`ExcludeAreas2` لاستبعاد مناطق الجداول أيضًا.
    question: هل هناك طريقة لاستبعاد الجداول بالإضافة إلى التعليقات باستخدام نفس كائن
      الخيارات؟
  - answer: يتحقق الكود من `if (a != null && a.Rect != null)` قبل الإضافة إلى القائمة،
      لذا يتم تخطي المستطيلات ذات القيمة null ببساطة ولا يُرمى أي استثناء.
    question: ماذا لو كانت خاصية `Rect` للتعليق ذات قيمة null – هل سيتسبب الكود في
      استثناء؟
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: قارن ملفات PDF بدون تعليقات توضيحية
og_description: نفّذ مقارنة PDF جنبًا إلى جنب تتخطى جميع علامات التعليقات.
og_image_alt: دليل يوضح مقارنة PDF جنبًا إلى جنب تستثني مناطق التعليقات باستخدام Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# مقارنة PDF جنبًا إلى جنب مع استبعاد التعليقات التوضيحية باستخدام Aspose.Pdf
يوضح هذا البرنامج التعليمي كيفية مقارنة ملفي PDF باستخدام Aspose.Pdf for .NET مع تجاهل أي محتوى تعليقات توضيحية. يقوم باستخراج مربعات حدود جميع التعليقات من كل مستند، ويُدخل تلك المناطق في SideBySideComparisonOptions، ثم يُجري مقارنة جنبًا إلى جنب. النتيجة هي ملف PDF للفرق يبرز فقط التغييرات غير المتعلقة بالتعليقات.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: ماذا يحدث إذا كانت صفحة PDF لا تحتوي على تعليقات توضيحية – هل ستظل المقارنة تعمل؟**  
A: نعم. الكود ببساطة لا يضيف أي مستطيلات إلى قائمة `ignoredRects` المقابلة، لذا تتلقى `ExcludeAreas1`/`ExcludeAreas2` مصفوفة فارغة ويعالج المقارن الصفحة بأكملها.

**Q: هل يمكنني استبعاد التعليقات فقط من مستند واحد مع الحفاظ على تعليقات المستند الآخر في الفرق؟**  
A: عيّن `ExcludeAreas1` (أو `ExcludeAreas2`) إلى المستطيلات المجمعة واترك الخاصية الأخرى كمصفوفة فارغة؛ سيستبعد المقارن المناطق فقط في المستند المحدد.

**Q: هل تتسبب مستطيلات التعليقات المتداخلة في أي مشاكل مع `ExcludeAreas`؟**  
A: المستطيلات المتداخلة تُدمج داخليًا بواسطة المقارن، لذا يتم استبعاد حدود التعليقات المتداخلة بأمان دون عدّ مزدوج.

**Q: هل هناك طريقة لاستبعاد الجداول بالإضافة إلى التعليقات باستخدام نفس كائن الخيارات؟**  
A: نعم، عيّن `compareOpts.ExcludeTables = true;` – هذه العلامة تعمل جنبًا إلى جنب مع `ExcludeAreas1`/`ExcludeAreas2` لاستبعاد مناطق الجداول أيضًا.

**Q: ماذا لو كانت خاصية `Rect` للتعليق ذات قيمة null – هل سيتسبب الكود في استثناء؟**  
A: يتحقق الكود من `if (a != null && a.Rect != null)` قبل الإضافة إلى القائمة، لذا يتم تخطي المستطيلات ذات القيمة null ببساطة ولا يُرمى أي استثناء.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}