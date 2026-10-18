---
title: تدوير صفحة PDF واحدة بزاوية 180 درجة باستخدام Aspose.PDF for .NET
weight: 260
limit:
description: تعلم كيفية تدوير الصفحة الثالثة من ملف PDF بزاوية 180° باستخدام Aspose.PDF for .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: تعلم كيفية تدوير الصفحة الثالثة من ملف PDF بزاوية 180° باستخدام Aspose.PDF
    for .NET.
  headline: تدوير صفحة PDF واحدة بزاوية 180 درجة باستخدام Aspose.PDF for .NET
  type: TechArticle
- description: تعلم كيفية تدوير الصفحة الثالثة من ملف PDF بزاوية 180° باستخدام Aspose.PDF
    for .NET.
  name: تدوير صفحة PDF واحدة بزاوية 180 درجة باستخدام Aspose.PDF for .NET
  steps:
  - name: يحتوي الملف على تعليقات توضيحية فقط ولا يحتوي على أي شفرة قابلة للتنفيذ،
      ويعمل كعنصر نائب للمثال الأصلي.
    text: يحتوي الملف على تعليقات توضيحية فقط ولا يحتوي على أي شفرة قابلة للتنفيذ،
      ويعمل كعنصر نائب للمثال الأصلي.
  type: HowTo
- questions:
  - answer: استخدم مجموعة الصفحات في SDK مع الفهرسة التي تبدأ من الصفر، مثل `pdfDocument.Pages[2]`،
      لأن الفهرس 2 يشير إلى الصفحة الثالثة.
    question: كيف يمكنني استهداف الصفحة الثالثة من ملف PDF للتدوير؟
  - answer: خاصية التدوير تقبل فقط القيم الأربع القياسية 0، 90، 180، و270 درجة؛ أي
      قيمة أخرى تُقرب إلى أقرب زاوية مسموح بها.
    question: هل يمكنني تدوير صفحة بزاوية غير 180 درجة؟
  - answer: يُطبق التدوير فقط على كائن `PdfDocument` الموجود في الذاكرة؛ يجب عليك
      استدعاء `pdfDocument.Save("output.pdf")` (أو طريقة حفظ مماثلة) لكتابة التغييرات
      إلى ملف جديد، مع ترك المصدر دون تعديل.
    question: هل يؤدي تدوير الصفحة إلى تعديل الملف الأصلي تلقائيًا؟
  - answer: يقوم SDK تلقائيًا بإعادة حساب مواضع التعليقات التوضيحية وحقول النموذج
      بحيث تظل محاذية بشكل صحيح مع الاتجاه الجديد.
    question: ماذا يحدث للتعليقات التوضيحية أو حقول النموذج بعد تدوير الصفحة؟
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: تدوير صفحة PDF بزاوية 180° باستخدام Aspose.PDF
og_description: قم بسرعة بقلب الصفحة الثالثة من ملف PDF رأسًا على عقب باستخدام بضع أسطر من شفرة Aspose.PDF for .NET.
og_image_alt: دليل يوضح الشفرة التي تدور الصفحة الثالثة من ملف PDF بزاوية 180 درجة باستخدام Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تدوير صفحة PDF واحدة بزاوية 180 درجة باستخدام Aspose.PDF
في هذا البرنامج التعليمي ستتعلم كيفية تدوير الصفحة الثالثة من مستند PDF بزاوية 180 درجة باستخدام Aspose.PDF for .NET. يوضح المثال خطوات تحميل ملف PDF، اختيار الصفحة 3، تطبيق التدوير، وحفظ الملف المحدث. يتيح لك هذا الأسلوب قلب صفحة محددة دون تغيير اتجاه الصفحات المتبقية.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: كيف يمكنني استهداف الصفحة الثالثة من ملف PDF للتدوير؟**  
A: استخدم مجموعة الصفحات في SDK مع الفهرسة التي تبدأ من الصفر، مثل `pdfDocument.Pages[2]`، لأن الفهرس 2 يشير إلى الصفحة الثالثة.

**Q: هل يمكنني تدوير صفحة بزاوية غير 180 درجة؟**  
A: خاصية التدوير تقبل فقط القيم الأربع القياسية 0، 90، 180، و270 درجة؛ أي قيمة أخرى تُقرب إلى أقرب زاوية مسموح بها.

**Q: هل يؤدي تدوير الصفحة إلى تعديل الملف الأصلي تلقائيًا؟**  
A: يُطبق التدوير فقط على كائن `PdfDocument` الموجود في الذاكرة؛ يجب عليك استدعاء `pdfDocument.Save("output.pdf")` (أو طريقة حفظ مماثلة) لكتابة التغييرات إلى ملف جديد، مع ترك المصدر دون تعديل.

**Q: ماذا يحدث للتعليقات التوضيحية أو حقول النموذج بعد تدوير الصفحة؟**  
A: يقوم SDK تلقائيًا بإعادة حساب مواضع التعليقات التوضيحية وحقول النموذج بحيث تظل محاذية بشكل صحيح مع الاتجاه الجديد.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}