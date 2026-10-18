---
title: تخصيص خلفية خلايا الجدول والحدود والمسافة الداخلية في ملفات PDF باستخدام Aspose.Pdf for .NET
weight: 101
limit:
description: تعلم كيفية إنشاء ملف PDF يحتوي على جدول من عمودين وتطبيق ألوان خلفية مخصصة، وحدود، ومسافة داخلية على كل خلية باستخدام Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: تعلم كيفية إنشاء ملف PDF يحتوي على جدول من عمودين وتطبيق ألوان خلفية
    مخصصة، وحدود، ومسافة داخلية على كل خلية باستخدام Aspose.Pdf for .NET.
  headline: تخصيص خلفية خلايا الجدول والحدود والمسافة الداخلية في ملفات PDF باستخدام
    Aspose.Pdf for .NET
  type: TechArticle
- description: تعلم كيفية إنشاء ملف PDF يحتوي على جدول من عمودين وتطبيق ألوان خلفية
    مخصصة، وحدود، ومسافة داخلية على كل خلية باستخدام Aspose.Pdf for .NET.
  name: تخصيص خلفية خلايا الجدول والحدود والمسافة الداخلية في ملفات PDF باستخدام Aspose.Pdf
    for .NET
  steps:
  - name: أنشئ مستند PDF فارغ جديد داخل كتلة using.
    text: أنشئ مستند PDF فارغ جديد داخل كتلة using.
  - name: أضف صفحة فارغة إلى مستند PDF.
    text: أضف صفحة فارغة إلى مستند PDF.
  - name: أنشئ كائن Table بعمودين كل منهما 200 نقطة، وحدود خارجية رقيقة سوداء، ومسافة
      داخلية افتراضية للخلية مقدارها 5 نقاط.
    text: أنشئ كائن Table بعمودين كل منهما 200 نقطة، وحدود خارجية رقيقة سوداء، ومسافة
      داخلية افتراضية للخلية مقدارها 5 نقاط.
  - name: أضف الصف الأول إلى الجدول.
    text: أضف الصف الأول إلى الجدول.
  - name: أنشئ الخلية الأولى، أدخل النص "First cell"، اضبط خلفية باللون الأصفر الفاتح،
      حدًا أحمر بسُمك نقطتين، وهوامش 4 نقاط.
    text: أنشئ الخلية الأولى، أدخل النص "First cell"، اضبط خلفية باللون الأصفر الفاتح،
      حدًا أحمر بسُمك نقطتين، وهوامش 4 نقاط.
  - name: أنشئ الخلية الثانية، أضف النص "Second cell"، أعطها خلفية باللون الأخضر الفاتح،
      حدًا أزرق بسُمك نقطتين، وهوامش 4 نقاط.
    text: أنشئ الخلية الثانية، أضف النص "Second cell"، أعطها خلفية باللون الأخضر الفاتح،
      حدًا أزرق بسُمك نقطتين، وهوامش 4 نقاط.
  - name: أضف الصف الثاني إلى الجدول.
    text: أضف الصف الثاني إلى الجدول.
  - name: أنشئ الخلية الثالثة، أدخل "Third cell"، اضبط خلفية باللون السماوي الفاتح،
      حدًا رماديًا داكنًا بسُمك نقطتين، وهوامش 4 نقاط.
    text: أنشئ الخلية الثالثة، أدخل "Third cell"، اضبط خلفية باللون السماوي الفاتح،
      حدًا رماديًا داكنًا بسُمك نقطتين، وهوامش 4 نقاط.
  - name: أنشئ الخلية الرابعة، أضف "Fourth cell"، أعطها خلفية باللون الوردي الفاتح،
      حدًا بنفسجيًا بسُمك نقطتين، وهوامش 4 نقاط.
    text: أنشئ الخلية الرابعة، أضف "Fourth cell"، أعطها خلفية باللون الوردي الفاتح،
      حدًا بنفسجيًا بسُمك نقطتين، وهوامش 4 نقاط.
  - name: أضف الجدول المُنسق بالكامل إلى الصفحة حتى يصبح مرئيًا في ملف PDF.
    text: أضف الجدول المُنسق بالكامل إلى الصفحة حتى يصبح مرئيًا في ملف PDF.
  - name: احفظ مستند PDF إلى ملف وأغلق كتلة using.
    text: احفظ مستند PDF إلى ملف وأغلق كتلة using.
  - name: اطبع رسالة تأكيد إلى وحدة التحكم.
    text: اطبع رسالة تأكيد إلى وحدة التحكم.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` يوفر مسافة داخلية أساسية لكل خلية، ولكن إذا قمت
      بتعيين `Margin` (مثال: `cellA1.Margin = new MarginInfo(...)`) فإن قيم الهامش
      تتجاوز المسافة الداخلية الافتراضية لتلك الخلية المحددة.'
    question: هل يؤثر `DefaultCellPadding` المحدد على `Table` على الخلايا التي لديها
      أيضًا `Margin` معرفة؟
  - answer: 'بدون `Table.Border`، يتم حذف المستطيل الخارجي حول الجدول بأكمله؛ وستظهر
      فقط حدود الخلايا الفردية التي قمت بتعيينها (مثال: `cellA2.Border`).'
    question: كيف سيظهر ملف PDF إذا أزلت خاصية `Border` من كائن `Table`؟
  - answer: 'نعم، أنشئ `BorderInfo` مع `BorderSide` محدد (مثال: `new BorderInfo(BorderSide.Left,
      3, Aspose.Pdf.Color.Black)`) وعيّنها إلى خاصية `Border` للخلية.'
    question: هل يمكنني إعطاء خلية عرض حد مختلف على كل جانب؟
  - answer: أنشئ كائن `Row` جديد باستخدام `Row newRow = dataTable.Rows.Add();` ثم
      أضف خلايا إلى `newRow.Cells` كما في الصفوف السابقة.
    question: كيف أضيف صفًا ثالثًا إلى الجدول بعد الشيفرة المعروضة؟
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: تنسيق خلايا جدول PDF – الخلفية، الحد، المسافة الداخلية
og_description: قم بتنسيق خلايا الجدول في ملف PDF بسرعة باستخدام ألوان مخصصة، حدود، وتباعد باستخدام Aspose.Pdf for .NET.
og_image_alt: دليل يوضح كيفية تنسيق لون الخلفية، الحد، والمسافة الداخلية لخلايا الجدول في ملف PDF باستخدام Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تخصيص خلفية خلايا الجدول والحدود والمسافة الداخلية في ملفات PDF باستخدام Aspose.Pdf
في هذا البرنامج التعليمي ستتعرف على كيفية إنشاء مستند PDF، وإضافة جدول من عمودين، والتحكم بدقة في مظهر كل خلية. من خلال ضبط ألوان الخلفية، وتحديد الحدود، وتعديل المسافة الداخلية يمكنك إبراز بيانات الجدول وجعلها تبدو مصقولة. يستخدم المثال فئتي Aspose.Pdf Document و Table لتوضيح كل خيار تنسيق.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: هل يؤثر `DefaultCellPadding` المحدد على `Table` على الخلايا التي لديها أيضًا `Margin` معرفة؟**  
A: `DefaultCellPadding` يوفر مسافة داخلية أساسية لكل خلية، ولكن إذا قمت بتعيين `Margin` (مثال: `cellA1.Margin = new MarginInfo(...)`) فإن قيم الهامش تتجاوز المسافة الداخلية الافتراضية لتلك الخلية المحددة.

**Q: كيف سيظهر ملف PDF إذا أزلت خاصية `Border` من كائن `Table`؟**  
A: بدون `Table.Border`، يتم حذف المستطيل الخارجي حول الجدول بأكمله؛ وستظهر فقط حدود الخلايا الفردية التي قمت بتعيينها (مثال: `cellA2.Border`).

**Q: هل يمكنني إعطاء خلية عرض حد مختلف على كل جانب؟**  
A: نعم، أنشئ `BorderInfo` مع `BorderSide` محدد (مثال: `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) وعيّنها إلى خاصية `Border` للخلية.

**Q: كيف أضيف صفًا ثالثًا إلى الجدول بعد الشيفرة المعروضة؟**  
A: أنشئ كائن `Row` جديد باستخدام `Row newRow = dataTable.Rows.Add();` ثم أضف خلايا إلى `newRow.Cells` كما في الصفوف السابقة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}