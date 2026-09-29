---
title: إضافة ارتباط خارجي معلم مع تلميح أدوات إلى PDF باستخدام Aspose.Pdf for .NET
weight: 440
limit:
description: تعلم كيفية إضافة ارتباط خارجي معلم مع نص عرض وتلميح أدوات إلى PDF باستخدام Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: تعلم كيفية إضافة ارتباط خارجي معلم مع نص عرض وتلميح أدوات إلى PDF باستخدام
    Aspose.Pdf for .NET.
  headline: إضافة ارتباط خارجي معلم مع تلميح أدوات إلى PDF باستخدام Aspose.Pdf for
    .NET
  type: TechArticle
- description: تعلم كيفية إضافة ارتباط خارجي معلم مع نص عرض وتلميح أدوات إلى PDF باستخدام
    Aspose.Pdf for .NET.
  name: إضافة ارتباط خارجي معلم مع تلميح أدوات إلى PDF باستخدام Aspose.Pdf for .NET
  steps:
  - name: حدد المسارات لملف PDF المصدر وملف النتيجة.
    text: حدد المسارات لملف PDF المصدر وملف النتيجة.
  - name: تحقق من وجود ملف PDF المصدر وأوقف التنفيذ إذا تعذر العثور عليه.
    text: تحقق من وجود ملف PDF المصدر وأوقف التنفيذ إذا تعذر العثور عليه.
  - name: افتح مستند PDF داخل كتلة using لضمان التخلص السليم.
    text: افتح مستند PDF داخل كتلة using لضمان التخلص السليم.
  - name: احصل على مدير المحتوى المعلم للمستند المفتوح.
    text: احصل على مدير المحتوى المعلم للمستند المفتوح.
  - name: عيّن لغة المستند إلى الإنجليزية (US) وأعطِ ملف PDF عنوانًا مشتقًا من اسم
      الملف.
    text: عيّن لغة المستند إلى الإنجليزية (US) وأعطِ ملف PDF عنوانًا مشتقًا من اسم
      الملف.
  - name: استرجع العنصر الجذر لشجرة الهيكل المنطقي الذي ستُضاف إليه العناصر الجديدة.
    text: استرجع العنصر الجذر لشجرة الهيكل المنطقي الذي ستُضاف إليه العناصر الجديدة.
  - name: أنشئ عنصر رابط، عيّن نصه المعروض، وعنوان URL الهدف، وعنوان تلميح الأدوات،
      ثم أدخله في هيكل المستند.
    text: أنشئ عنصر رابط، عيّن نصه المعروض، وعنوان URL الهدف، وعنوان تلميح الأدوات،
      ثم أدخله في هيكل المستند.
  - name: احفظ ملف PDF المحدث إلى ملف النتيجة المحدد.
    text: احفظ ملف PDF المحدث إلى ملف النتيجة المحدد.
  - name: اعرض رسالة تأكيد تشير إلى مكان حفظ ملف PDF المعدل.
    text: اعرض رسالة تأكيد تشير إلى مكان حفظ ملف PDF المعدل.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` يُعيد المحتوى المعلم الموجود إذا كان المستند معلمًا
      بالفعل؛ ولا ينشئ شجرة مكررة.'
    question: ماذا لو كان ملف PDF المصدر معلمًا بالفعل – هل سيؤدي استدعاء `pdfDoc.TaggedContent`
      إلى إنشاء شجرة علامات جديدة أم سيعيد استخدام الشجرة الموجودة؟
  - answer: نعم – حدد `StructureElement` المطلوب (مثل `Div` أو `Paragraph` على صفحة)
      عبر شجرة الهيكل المنطقي واستدعِ `AppendChild(externalLink)` على ذلك العنصر.
    question: هل يمكنني وضع الارتباط على صفحة معينة بدلاً من إلحاقه بالعنصر الجذر؟
  - answer: يظهر تلميح الأدوات فقط إذا تم تعيين `externalLink.Title` قبل `pdfDoc.Save`؛
      تعيينه بعد الحفظ لا يؤثر على ملف PDF المكتوب بالفعل.
    question: هل خاصية `Title` في `LinkElement` ضرورية لظهور تلميح الأدوات، وهل يمكن
      تعيينها بعد استدعاء `Save`؟
  - answer: 'عيّن `FileSpecification` (مثال: `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`)
      إلى `externalLink.Hyperlink` بدلاً من استخدام `WebHyperlink`.'
    question: كيف يمكنني إنشاء ارتباط إلى ملف محلي بدلاً من عنوان URL ويب؟
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: إدراج ارتباط خارجي معلم مع تلميح أدوات في PDF
og_description: ضم ارتباطًا يمكن الوصول إليه مع نص مرئي وتلميح أدوات إلى ملف PDF الخاص بك باستخدام Aspose.Pdf for .NET.
og_image_alt: دليل يوضح كيفية إضافة ارتباط خارجي معلم مع تلميح أدوات إلى PDF باستخدام Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ارتباط خارجي معلم مع تلميح أدوات إلى PDF باستخدام Aspose.Pdf
يوضح هذا البرنامج التعليمي كيفية فتح ملف PDF موجود باستخدام Aspose.Pdf for .NET، وإنشاء ارتباط خارجي معلم يتضمن نصًا عرضيًا مرئيًا وعنوانًا لتلميح الأدوات، وإدراج الرابط في الهيكل المنطقي للمستند، وحفظ الملف المحدث. باتباع الخطوات ستحصل على PDF يمكن الوصول إليه حيث يكون الرابط جزءًا من تسلسل العلامات ويقدم سياقًا إضافيًا للقراء.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: ماذا لو كان ملف PDF المصدر معلمًا بالفعل – هل سيؤدي استدعاء `pdfDoc.TaggedContent` إلى إنشاء شجرة علامات جديدة أم سيعيد استخدام الشجرة الموجودة؟**  
A: `pdfDoc.TaggedContent` يُعيد المحتوى المعلم الموجود إذا كان المستند معلمًا بالفعل؛ ولا ينشئ شجرة مكررة.

**Q: هل يمكنني وضع الارتباط على صفحة معينة بدلاً من إلحاقه بالعنصر الجذر؟**  
A: نعم – حدد `StructureElement` المطلوب (مثل `Div` أو `Paragraph` على صفحة) عبر شجرة الهيكل المنطقي واستدعِ `AppendChild(externalLink)` على ذلك العنصر.

**Q: هل خاصية `Title` في `LinkElement` ضرورية لظهور تلميح الأدوات، وهل يمكن تعيينها بعد استدعاء `Save`؟**  
A: يظهر تلميح الأدوات فقط إذا تم تعيين `externalLink.Title` قبل `pdfDoc.Save`؛ تعيينه بعد الحفظ لا يؤثر على ملف PDF المكتوب بالفعل.

**Q: كيف يمكنني إنشاء ارتباط إلى ملف محلي بدلاً من عنوان URL ويب؟**  
A: عيّن `FileSpecification` (مثال: `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`) إلى `externalLink.Hyperlink` بدلاً من استخدام `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}