---
title: قارن ملفات PDF مع تجاهل مناطق محددة باستخدام Aspose.Pdf for .NET
weight: 201
limit:
description: تعلم كيفية مقارنة ملفات PDF جنبًا إلى جنب وتجاهل المناطق المختارة باستخدام Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: تعلم كيفية مقارنة ملفات PDF جنبًا إلى جنب وتجاهل المناطق المختارة باستخدام
    Aspose.Pdf for .NET.
  headline: قارن ملفات PDF مع تجاهل مناطق محددة باستخدام Aspose.Pdf for .NET
  type: TechArticle
- description: تعلم كيفية مقارنة ملفات PDF جنبًا إلى جنب وتجاهل المناطق المختارة باستخدام
    Aspose.Pdf for .NET.
  name: قارن ملفات PDF مع تجاهل مناطق محددة باستخدام Aspose.Pdf for .NET
  steps:
  - name: حدد مسارات الملفات للملفين PDF المصدرين وملف PDF الفرق الناتج.
    text: حدد مسارات الملفات للملفين PDF المصدرين وملف PDF الفرق الناتج.
  - name: تحقق من وجود ملفي PDF المصدرين، وإذا كان أحدهما مفقودًا أوقف العملية مع
      رسالة خطأ.
    text: تحقق من وجود ملفي PDF المصدرين، وإذا كان أحدهما مفقودًا أوقف العملية مع
      رسالة خطأ.
  - name: أنشئ مصفوفة تحتوي على المنطقة المستطيلة التي يجب تجاهلها في ملف PDF الأول.
    text: أنشئ مصفوفة تحتوي على المنطقة المستطيلة التي يجب تجاهلها في ملف PDF الأول.
  - name: أنشئ مصفوفة تحتوي على المنطقة المستطيلة التي يجب تجاهلها في ملف PDF الثاني.
    text: أنشئ مصفوفة تحتوي على المنطقة المستطيلة التي يجب تجاهلها في ملف PDF الثاني.
  - name: قم بتهيئة المقارنة جنبًا إلى جنب، مع تعيين مصفوفات مناطق التجاهل إلى الخصائص
      المناسبة.
    text: قم بتهيئة المقارنة جنبًا إلى جنب، مع تعيين مصفوفات مناطق التجاهل إلى الخصائص
      المناسبة.
  - name: حمّل ملفي PDF وشغّل المقارنة جنبًا إلى جنب، مما ينتج ملف الفرق في المسار
      المحدد.
    text: حمّل ملفي PDF وشغّل المقارنة جنبًا إلى جنب، مما ينتج ملف الفرق في المسار
      المحدد.
  - name: اعرض رسالة تأكيد تشير إلى أن المقارنة قد اكتملت وإلى مكان حفظ ملف PDF الفرق.
    text: اعرض رسالة تأكيد تشير إلى أن المقارنة قد اكتملت وإلى مكان حفظ ملف PDF الفرق.
  type: HowTo
- questions:
  - answer: الإحداثيات بوحدة النقاط (1/72 بوصة) مع الأصل في الزاوية السفلية اليسرى
      للصفحة، لذا فإن الرقمين الأولين يمثلان X/Y للزاوية السفلية اليسرى والرقمين الأخيرين
      يمثلان X/Y للزاوية العلوية اليمنى.
    question: ما نظام الإحداثيات الذي تستخدمه قيم `Rectangle` عند تعريف مناطق التجاهل؟
  - answer: نعم – قدم عدة كائنات `Aspose.Pdf.Rectangle` في مصفوفة `ExcludeAreas1`
      (أو `ExcludeAreas2`)؛ سيتم استبعاد كل مستطيل بشكل مستقل أثناء المقارنة.
    question: هل يمكنني تجاهل أكثر من منطقة مستطيلة في نفس المستند؟
  - answer: لا. `ExcludeAreas1` تُطبق على ملف PDF الأول و`ExcludeAreas2` على الثاني،
      لذا يمكنك تحديد إحداثيات مختلفة لكل مستند.
    question: هل يجب أن تكون المستطيلات المتجاهلة متطابقة في ملفي PDF؟
  - answer: يتجاهل Aspose.Pdf المستطيلات التي تقع خارج الصفحة تمامًا بصمت؛ ولا تؤثر
      على نتيجة المقارنة.
    question: ماذا يحدث إذا تم تعريف مستطيل خارج حدود الصفحة؟
  - answer: تُطبق مصفوفات `ExcludeAreas` على كل صفحة، لذا عليك إضافة نفس `Rectangle`
      إلى مجموعة كل صفحة (مثلاً، كرر عبر `pdf.Pages` وعيّن المصفوفة) قبل استدعاء `SideBySidePdfComparer.Compare`.
    question: كيف يمكنني استبعاد نفس المنطقة في كل صفحة من ملف PDF؟
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: تجاهل المناطق عند مقارنة ملفات PDF
og_description: اطلع على كيفية تخطي المناطق المختارة في مقارنة PDF جنبًا إلى جنب والحصول على ملف PDF فرق نظيف.
og_image_alt: دليل يوضح مقارنة PDF جنبًا إلى جنب مع استبعاد المناطق المستطيلة باستخدام Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# قارن ملفات PDF مع تجاهل مناطق محددة باستخدام Aspose.Pdf
يُظهر هذا البرنامج التعليمي كيفية مقارنة مستندي PDF جنبًا إلى جنب باستخدام Aspose.Pdf for .NET مع استبعاد المناطق المستطيلة المحددة من التحليل. من خلال تعريف مناطق الاستبعاد في كل ملف، يبرز ملف PDF الفرق الناتج فقط التغييرات المهمة، مما يسهل التركيز على الاختلافات ذات الصلة.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: ما نظام الإحداثيات الذي تستخدمه قيم `Rectangle` عند تعريف مناطق التجاهل؟**  
A: الإحداثيات بوحدة النقاط (1/72 بوصة) مع الأصل في الزاوية السفلية اليسرى للصفحة، لذا فإن الرقمين الأولين يمثلان X/Y للزاوية السفلية اليسرى والرقمين الأخيرين يمثلان X/Y للزاوية العلوية اليمنى.

**Q: هل يمكنني تجاهل أكثر من منطقة مستطيلة في نفس المستند؟**  
A: نعم – قدم عدة كائنات `Aspose.Pdf.Rectangle` في مصفوفة `ExcludeAreas1` (أو `ExcludeAreas2`)؛ سيتم استبعاد كل مستطيل بشكل مستقل أثناء المقارنة.

**Q: هل يجب أن تكون المستطيلات المتجاهلة متطابقة في ملفي PDF؟**  
A: لا. `ExcludeAreas1` تُطبق على ملف PDF الأول و`ExcludeAreas2` على الثاني، لذا يمكنك تحديد إحداثيات مختلفة لكل مستند.

**Q: ماذا يحدث إذا تم تعريف مستطيل خارج حدود الصفحة؟**  
A: يتجاهل Aspose.Pdf المستطيلات التي تقع خارج الصفحة تمامًا بصمت؛ ولا تؤثر على نتيجة المقارنة.

**Q: كيف يمكنني استبعاد نفس المنطقة في كل صفحة من ملف PDF؟**  
A: تُطبق مصفوفات `ExcludeAreas` على كل صفحة، لذا عليك إضافة نفس `Rectangle` إلى مجموعة كل صفحة (مثلاً، كرر عبر `pdf.Pages` وعيّن المصفوفة) قبل استدعاء `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}