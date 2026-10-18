---
title: تقسيم PDF بعد الصفحة العاشرة باستخدام Aspose.Pdf for .NET
weight: 360
limit:
description: شيفرة خطوة بخطوة لتقسيم مستند PDF مباشرةً بعد الصفحة العاشرة باستخدام Aspose.Pdf for .NET.
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: شيفرة خطوة بخطوة لتقسيم مستند PDF مباشرةً بعد الصفحة العاشرة باستخدام
    Aspose.Pdf for .NET.
  headline: تقسيم PDF بعد الصفحة العاشرة باستخدام Aspose.Pdf for .NET
  type: TechArticle
- description: شيفرة خطوة بخطوة لتقسيم مستند PDF مباشرةً بعد الصفحة العاشرة باستخدام
    Aspose.Pdf for .NET.
  name: تقسيم PDF بعد الصفحة العاشرة باستخدام Aspose.Pdf for .NET
  steps:
  - name: توضح تعليقات الرأس هدف المثال، وتذكر أن الشيفرة الكاملة قد نُقلت، وتوفر
      رابطًا إلى المصدر المحدث.
    text: توضح تعليقات الرأس هدف المثال، وتذكر أن الشيفرة الكاملة قد نُقلت، وتوفر
      رابطًا إلى المصدر المحدث.
  - name: السطر الوهمي لا يؤدي أي عملية وهو موجود فقط للحفاظ على عمل عنوان URL الأصلي.
    text: السطر الوهمي لا يؤدي أي عملية وهو موجود فقط للحفاظ على عمل عنوان URL الأصلي.
  type: HowTo
- questions:
  - answer: لن تقوم Aspose.Pdf بإلقاء خطأ؛ طريقة `Split` ستعيد ببساطة المستند الأصلي
      دون تعديل لأن لا توجد صفحة بعد العاشرة لبدء جزء جديد.
    question: ماذا يحدث إذا كان ملف PDF المصدر يحتوي على أقل من عشر صفحات؟
  - answer: تستدعي `PdfDocument.Split(pageNumber)` على كائن `PdfDocument`، مع تمرير
      القيمة `10` كـ `pageNumber` لإنشاء مستندين منفصلين.
    question: ما هو الصنف والطريقة المستخدمان لتقسيم PDF عند الصفحة العاشرة؟
  - answer: نعم، تقوم Aspose.Pdf بالحفاظ على جميع الكائنات على مستوى الصفحة (العلامات
      المرجعية، التعليقات التوضيحية، حقول النموذج، إلخ) في المستندات المقسمة الناتجة،
      وتبقيها مرتبطة بالصفحات التي نشأت منها.
    question: هل تبقى العلامات المرجعية، والتعليقات التوضيحية، وحقول النموذج مع صفحاتها
      الأصلية بعد التقسيم؟
  - answer: بعد استدعاء `Split`، ستحصل على كائنين من نوع `PdfDocument`؛ يجب عليك استدعاء
      `Save(\"FirstPart.pdf\")` على الأول و`Save(\"SecondPart.pdf\")` على الثاني،
      مع توفير أسماء ملفات مميزة بنفسك.
    question: كيف يجب أن أسمي ملفات الإخراج للجزءين الناتجين عن التقسيم؟
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: تقسيم PDF بعد الصفحة 10
og_description: برنامج تعليمي سريع لتقسيم PDF عند الصفحة 10 باستخدام Aspose.Pdf for .NET.
og_image_alt: دليل يوضح كيفية تقسيم PDF بعد الصفحة العاشرة باستخدام Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تقسيم PDF بعد الصفحة العاشرة باستخدام Aspose.Pdf
يمكن أن يؤدي تقسيم PDF إلى مستندات منفصلة إلى تبسيط التوزيع والمعالجة. يوجهك هذا البرنامج التعليمي لاستخدام Aspose.Pdf for .NET لتقسيم PDF مباشرةً بعد الصفحة العاشرة، مما ينتج ملفين مميزين. اتبع الشيفرة خطوة بخطوة لاستخراج الصفحات العشر الأولى والصفحات المتبقية ببضع أسطر فقط من C#.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/split-pdf" >}}


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

**Q: ماذا يحدث إذا كان ملف PDF المصدر يحتوي على أقل من عشر صفحات؟**  
A: لن تقوم Aspose.Pdf بإلقاء خطأ؛ طريقة `Split` ستعيد ببساطة المستند الأصلي دون تعديل لأن لا توجد صفحة بعد العاشرة لبدء جزء جديد.

**Q: ما هو الصنف والطريقة المستخدمان لتقسيم PDF عند الصفحة العاشرة؟**  
A: تستدعي `PdfDocument.Split(pageNumber)` على كائن `PdfDocument`، مع تمرير القيمة `10` كـ `pageNumber` لإنشاء مستندين منفصلين.

**Q: هل تبقى العلامات المرجعية، والتعليقات التوضيحية، وحقول النموذج مع صفحاتها الأصلية بعد التقسيم؟**  
A: نعم، تقوم Aspose.Pdf بالحفاظ على جميع الكائنات على مستوى الصفحة (العلامات المرجعية، التعليقات التوضيحية، حقول النموذج، إلخ) في المستندات المقسمة الناتجة، وتبقيها مرتبطة بالصفحات التي نشأت منها.

**Q: كيف يجب أن أسمي ملفات الإخراج للجزءين الناتجين عن التقسيم؟**  
A: بعد استدعاء `Split`، ستحصل على كائنين من نوع `PdfDocument`؛ يجب عليك استدعاء `Save(\"FirstPart.pdf\")` على الأول و`Save(\"SecondPart.pdf\")` على الثاني، مع توفير أسماء ملفات مميزة بنفسك.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}