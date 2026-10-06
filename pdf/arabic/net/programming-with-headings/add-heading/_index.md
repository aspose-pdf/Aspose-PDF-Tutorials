---
title: إضافة عنوان، لغة، وعنوان إلى ملف PDF باستخدام Aspose.PDF for .NET
weight: 110
limit:
description: أنشئ ملف PDF، عيّن لغته وعنوانه، وأضف عنوانًا من المستوى‑1 باستخدام Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: أنشئ ملف PDF، عيّن لغته وعنوانه، وأضف عنوانًا من المستوى‑1 باستخدام
    Aspose.PDF for .NET.
  headline: إضافة عنوان، لغة، وعنوان إلى ملف PDF باستخدام Aspose.PDF for .NET
  type: TechArticle
- description: أنشئ ملف PDF، عيّن لغته وعنوانه، وأضف عنوانًا من المستوى‑1 باستخدام
    Aspose.PDF for .NET.
  name: إضافة عنوان، لغة، وعنوان إلى ملف PDF باستخدام Aspose.PDF for .NET
  steps:
  - name: حدد اسم ملف الإخراج للمستند PDF المُولد.
    text: حدد اسم ملف الإخراج للمستند PDF المُولد.
  - name: أنشئ كائنًا جديدًا فارغًا من مستند PDF (`pdfDoc`) داخل كتلة `using`.
    text: أنشئ كائنًا جديدًا فارغًا من مستند PDF (`pdfDoc`) داخل كتلة `using`.
  - name: احصل على واجهة `ITaggedContent` للعمل مع هياكل PDF الموسومة.
    text: احصل على واجهة `ITaggedContent` للعمل مع هياكل PDF الموسومة.
  - name: عيّن اللغة الافتراضية للمستند إلى الإنجليزية (الولايات المتحدة) وعيّن بيانات
      تعريف العنوان.
    text: عيّن اللغة الافتراضية للمستند إلى الإنجليزية (الولايات المتحدة) وعيّن بيانات
      تعريف العنوان.
  - name: استرجع العنصر الجذر لشجرة البنية المنطقية.
    text: استرجع العنصر الجذر لشجرة البنية المنطقية.
  - name: أنشئ عنصر رأس من المستوى‑1، عيّن النص المعروض له، وحدد لغته.
    text: أنشئ عنصر رأس من المستوى‑1، عيّن النص المعروض له، وحدد لغته.
  - name: أضف عنصر الرأس إلى الجذر، مما يجعل العنوان يظهر في ملف PDF.
    text: أضف عنصر الرأس إلى الجذر، مما يجعل العنوان يظهر في ملف PDF.
  - name: احفظ ملف PDF إلى الملف المحدد وأغلق نطاق المستند.
    text: احفظ ملف PDF إلى الملف المحدد وأغلق نطاق المستند.
  - name: اعرض رسالة تأكيد في وحدة التحكم.
    text: اعرض رسالة تأكيد في وحدة التحكم.
  type: HowTo
- questions:
  - answer: '`SetLanguage` يحدد اللغة الافتراضية للبنية المنطقية لكامل المستند؛ أي
      عنصر لا يملك لغة محددة سيورث "en-US".'
    question: ما هو تأثير استدعاء `tagContent.SetLanguage("en-US")` على ملف PDF؟
  - answer: تعيين `header.Language` اختياري؛ سيورث العنوان اللغة الافتراضية للمستند
      ما لم تقم بتعيين قيمة مختلفة، كما هو موضح في المثال.
    question: هل يجب عليّ تعيين `header.Language` إذا كنت قد استدعيت `SetLanguage`
      على المستند مسبقًا؟
  - answer: استخدم `tagContent.CreateHeaderElement(2)` لإنشاء عنوان من المستوى‑2؛
      المعامل الرقمي يحدد مستوى العنوان الذي سيظهر في شجرة بنية PDF.
    question: كيف يمكنني إنشاء عنوان من المستوى‑2 بدلاً من المستوى‑1؟
  - answer: '`SetTitle` يكتب السلسلة المقدمة إلى حقل عنوان بيانات تعريف المستند في
      PDF، ويمكن رؤيته في قارئات PDF واستخدامه للبحث أو الفهرسة.'
    question: ماذا يفعل `tagContent.SetTitle("PDF Example with Header")`؟
  - answer: لن يتم إضافة عنصر العنوان إلى شجرة البنية المنطقية، وبالتالي لن يظهر في
      مخرجات PDF ولن يتم التعرف عليه كعنوان لأدوات إمكانية الوصول.
    question: ماذا يحدث إذا حذفت `rootElement.AppendChild(header)`؟
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: إدراج عنوان وتعيين اللغة في ملف PDF
og_description: تعلم كيفية إنشاء ملف PDF، تعيين لغته وعنوانه، ثم إضافة عنوان من المستوى‑1 باستخدام بضع أسطر من كود .NET.
og_image_alt: دليل يوضح كيفية إضافة عنوان، تعيين اللغة، والعنوان في ملف PDF باستخدام Aspose.PDF for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة عنوان، لغة، وعنوان إلى ملف PDF باستخدام Aspose.PDF
يُرشدك هذا البرنامج التعليمي إلى إنشاء مستند PDF جديد باستخدام Aspose.PDF for .NET، وتعيين لغة افتراضية وعنوان للمستند، وإدراج عنوان من المستوى‑1. ستتعرف على كيفية العمل مع الفئات Document و ITaggedContent و StructureElement و HeaderElement لإنتاج PDF مُوسوم بشكل صحيح ومناسب لأدوات إمكانية الوصول.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


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

**Q: ما هو تأثير استدعاء `tagContent.SetLanguage("en-US")` على ملف PDF؟**  
A: `SetLanguage` يحدد اللغة الافتراضية للبنية المنطقية لكامل المستند؛ أي عنصر لا يملك لغة محددة سيورث "en-US".

**Q: هل يجب عليّ تعيين `header.Language` إذا كنت قد استدعيت `SetLanguage` على المستند مسبقًا؟**  
A: تعيين `header.Language` اختياري؛ سيورث العنوان اللغة الافتراضية للمستند ما لم تقم بتعيين قيمة مختلفة، كما هو موضح في المثال.

**Q: كيف يمكنني إنشاء عنوان من المستوى‑2 بدلاً من المستوى‑1؟**  
A: استخدم `tagContent.CreateHeaderElement(2)` لإنشاء عنوان من المستوى‑2؛ المعامل الرقمي يحدد مستوى العنوان الذي سيظهر في شجرة بنية PDF.

**Q: ماذا يفعل `tagContent.SetTitle("PDF Example with Header")`؟**  
A: `SetTitle` يكتب السلسلة المقدمة إلى حقل عنوان بيانات تعريف المستند في PDF، ويمكن رؤيته في قارئات PDF واستخدامه للبحث أو الفهرسة.

**Q: ماذا يحدث إذا حذفت `rootElement.AppendChild(header)`؟**  
A: لن يتم إضافة عنصر العنوان إلى شجرة البنية المنطقية، وبالتالي لن يظهر في مخرجات PDF ولن يتم التعرف عليه كعنوان لأدوات إمكانية الوصول.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}