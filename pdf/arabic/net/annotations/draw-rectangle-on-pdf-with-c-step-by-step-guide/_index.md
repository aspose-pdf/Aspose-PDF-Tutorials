---
category: general
date: 2026-06-21
description: ارسم مستطيلًا على ملف PDF باستخدام C#. تعلم كيفية تحميل مستند PDF، وإنشاء
  تعليقة مستطيل أسود، وحفظ ملف PDF المعدل بكفاءة.
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: ar
og_description: ارسم مستطيلًا على ملف PDF باستخدام C# عن طريق تحميل مستند PDF، وإنشاء
  تعليق مستطيل أسود، وحفظ ملف PDF المعدل. يتضمن الكود الكامل.
og_title: رسم مستطيل على PDF باستخدام C# – دليل برمجة كامل
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: رسم مستطيل على PDF باستخدام C# – دليل خطوة بخطوة
url: /ar/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# رسم مستطيل على PDF باستخدام C# – دليل برمجة كامل

هل احتجت يومًا إلى **رسم مستطيل على ملفات PDF** من تطبيق .NET لكن لم تعرف من أين تبدأ؟ لست وحدك. سواء كان ذلك لتسليط الضوء على قسم، أو إخفاء بيانات حساسة، أو مجرد إضافة إشارة بصرية، فإن تعلم كيفية *رسم مستطيل على PDF* برمجيًا يمكن أن يوفر لك ساعات من التحرير اليدوي.

في هذا الدليل سنستعرض مثالًا عمليًا يقوم **بتحميل مستند PDF**، **بإنشاء مستطيل أسود**، ثم **بحفظ PDF المعدل**. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع C#—بدون غموض، فقط كود واضح وشروحات.

## ما يغطيه هذا الدرس

- كيفية **تحميل مستند PDF** باستخدام مكتبة Aspose.PDF for .NET  
- تعريف إحداثيات المستطيل وضمان بقائه داخل حدود الصفحة  
- استخدام طريقة **إضافة مستطيل أسود** لتوضيح الصفحة  
- **حفظ PDF المعدل** في موقع ملف جديد  
- معالجة الحالات الخاصة (صفحات متعددة، مستطيلات خارج الحدود، ألوان مخصصة)  

بدون أدوات خارجية، بدون مراجع غامضة—فقط مثال كامل قابل للتنفيذ يمكنك نسخه ولصقه.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

1. .NET 6.0 SDK (أو أي نسخة حديثة من .NET) مثبتة  
2. إشارة إلى **Aspose.PDF for .NET** (متاحة عبر NuGet: `Install-Package Aspose.PDF`)  
3. ملف PDF موجود (`input.pdf`) في مجلد يمكنك القراءة والكتابة فيه  

هذا كل ما تحتاجه. إذا كنت مرتاحًا مع أساسيات لغة C#، فأنت جاهز للانطلاق.

---

## الخطوة 1: تحميل مستند PDF

أول شيء نحتاجه هو استدعاء **تحميل مستند PDF**. فئة `Document` في Aspose.PDF تأخذ مسار الملف وتقرأ الملف بالكامل إلى الذاكرة.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*لماذا هذا مهم*: تحميل الـ PDF يمنحك الوصول إلى صفحاته، بياناته الوصفية، وسطح الرسم. بدون هذه الخطوة لا يمكنك وضع أي أشكال.

---

## الخطوة 2: اختيار الصفحة المستهدفة

صفحات PDF تُرقم بدءًا من 1 في Aspose، لذا الصفحة الأولى هي الفهرس 1. احصل على الصفحة التي تريد توضيحها—عادةً الأولى لتجربة سريعة.

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

إذا احتجت للعمل على صفحة مختلفة، فقط غير الفهرس. تذكر التحقق من وجود الفهرس لتجنب `ArgumentOutOfRangeException`.

---

## الخطوة 3: تعريف هندسة المستطيل

المستطيل يُعرّف بإحداثيات الزاوية السفلية اليسرى (X,Y) والزاوية العليا اليمنى (X,Y). بنية `Rectangle` تخزن هذه القيم كـ `LLX`, `LLY`, `URX`, `URY`.

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

يمكنك تعديل هذه الأرقام بحرية—`100,100` يضع الزاوية السفلية اليسرى على بعد 100 نقطة من الحافة اليسرى والسفلية، بينما `300,300` يحدد الزاوية العليا اليمنى على بعد 300 نقطة من الحواف.

---

## الخطوة 4: التحقق من أن المستطيل يناسب داخل الصفحة

محاولة الرسم خارج حدود الصفحة إما تُهمل أو تتسبب في استثناء، حسب نسخة المكتبة. فحص سريع يجعل كودك أكثر صلابة.

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*نصيحة محترف*: إذا كنت تخطط لدعم ملفات PDF بأحجام مختلفة، قد تحسب أبعاد المستطيل بناءً على نسبة مئوية من عرض/ارتفاع الصفحة بدلاً من النقاط المطلقة.

---

## الخطوة 5: إضافة توضيح مستطيل أسود

الجزء الممتع الآن—**إضافة مستطيل أسود** إلى الصفحة. توفر Aspose الدالة `AddRectangle` التي تأخذ الهندسة و`Color`. سنستخدم `Color.Black` لإنشاء **مستطيل أسود**.

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

هذا السطر الواحد يقوم بالعمل الرئيسي: ينشئ كائن توضيح، يضبط لون الحدود إلى الأسود، ويضيفه إلى مجموعة توضيحات الصفحة.

إذا احتجت يومًا إلى تعبئة أو نمط حد مختلف، استكشف النسخة المتعددة المعاملات التي تقبل كائن `Annotation` حيث يمكنك تعديل سمك الخط، نمط الشرط، أو حتى الشفافية.

---

## الخطوة 6: حفظ PDF المعدل

أخيرًا، احفظ تغييراتك باستخدام **حفظ PDF المعدل**. يمكنك استبدال الملف الأصلي أو الكتابة إلى ملف جديد—هنا سننشئ ملف إخراج.

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

هذا هو سير العمل بالكامل. شغّل البرنامج وافتح `output.pdf`؛ يجب أن ترى مستطيلًا أسودًا صلبًا في الموقع الذي حددته.

---

## مثال كامل يعمل

فيما يلي تطبيق console مكتمل يضم جميع الخطوات معًا. انسخه إلى مشروع `.csproj` جديد واضغط **Run**.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**الناتج المتوقع** في وحدة التحكم:

```
Successfully drew rectangle on PDF and saved the file.
```

افتح `output.pdf` وسترى مستطيلًا أسودًا موضعه عند الإحداثيات التي حددتها.

---

## معالجة التغييرات الشائعة

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|-----|
| **صفحات متعددة** | كرّر عبر `pdfDocument.Pages` وطبق نفس المنطق على كل كائن `Page`. | يتيح توضيح دفعة على كامل المستند. |
| **ألوان مختلفة** | استبدل `Color.Black` بـ `Color.Red` أو أي `System.Drawing.Color`. | مفيد للتسليط الضوئي بدلاً من الإخفاء. |
| **تعبئة شفافة** | استخدم `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`. | يعطي طبقة نصف شفافة بدلًا من كتلة صلبة. |
| **حجم مستطيل ديناميكي** | احسب `URX` و `URY` بناءً على `PageInfo.Width * 0.5` إلخ. | يجعل المستطيل يتكيف مع أبعاد صفحات مختلفة. |
| **معالجة الأخطاء** | غلف الكتلة بالكامل بـ `try…catch` وسجل `Aspose.Pdf.IOException`. | يمنع الانهيارات عندما يكون الملف المصدر مفقودًا أو مقفولًا. |

هذه التعديلات توضح كيف يمكنك **إنشاء توضيح مستطيل أسود** في سياقات متعددة دون إعادة كتابة المنطق الأساسي.

---

## نصائح احترافية ومخاطر محتملة

- **تحرير كائن Document**: رغم أن Aspose.PDF تنفذ `IDisposable`، فإن نمط `using` ليس ضروريًا لتطبيقات console قصيرة العمر. في الخدمات طويلة التشغيل، اح.wrap `Document` داخل `using` لتحرير الموارد الأصلية بسرعة.  
- **نظام الإحداثيات**: إحداثيات PDF تبدأ من الزاوية السفلية اليسرى. إذا كنت معتادًا على الأصل العلوي الأيسر (كما في WinForms)، ستحتاج إلى عكس محور Y: `pageHeight - y`.  
- **الأداء**: إضافة توضيحات إلى ملفات PDF ضخمة قد تستهلك الذاكرة. فكر في معالجة الصفحات على دفعات أو استخدم `PdfFileEditor` لتعديلات أخف وزنًا.  
- **القانونية**: تأكد من أن لديك حقوق تعديل ملف PDF الأصلي—بعض المستندات محمية ضد التعديل.

---

## الخلاصة

لقد استعرضنا كيفية **رسم مستطيل على PDF** باستخدام C#—بدءًا من **تحميل مستند PDF**، تعريف الهندسة، **إضافة مستطيل أسود**، وأخيرًا **حفظ PDF المعدل**. المثال كامل، قابل للتنفيذ، وقابل للتكيف مع سيناريوهات العالم الحقيقي مثل المعالجة الدفعية أو التنسيق المخصص.

بعد ذلك، قد ترغب في استكشاف إضافة أنواع توضيحات أخرى (نص، تظليل) أو دمج ملفات PDF متعددة بعد التوضيح. خطوات **تحميل مستند PDF** و **حفظ PDF المعدل** تبقى كما هي، لذا يمكنك توسيع هذا النمط بثقة.

هل جربت تعديلًا مختلفًا؟ شاركنا في التعليقات، وتمنياتنا لك ببرمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Create Filled Rectangle Object in PDF using Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}