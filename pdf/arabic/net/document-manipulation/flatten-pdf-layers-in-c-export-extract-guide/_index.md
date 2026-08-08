---
category: general
date: 2026-06-08
description: قم بتسوية طبقات PDF في C# بسرعة وتعلم كيفية استخراج الطبقات من PDF، وتصدير
  طبقات PDF، وتسوية الطبقات للحصول على مستندات نظيفة.
draft: false
keywords:
- flatten pdf layers
- extract layers from pdf
- how to flatten layers
- how to export layers
- export pdf layers
language: ar
og_description: قم بتسوية طبقات PDF في C# بسرعة وتعلم كيفية استخراج الطبقات من PDF،
  وتصدير طبقات PDF، وتسوية الطبقات للحصول على مستندات نظيفة.
og_title: تسوية طبقات PDF في C# – دليل التصدير والاستخراج
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Flatten PDF layers in C# quickly and learn how to extract layers from
    PDF, export PDF layers, and flatten layers for clean documents.
  headline: Flatten PDF Layers in C# – Export & Extract Guide
  type: TechArticle
- description: Flatten PDF layers in C# quickly and learn how to extract layers from
    PDF, export PDF layers, and flatten layers for clean documents.
  name: Flatten PDF Layers in C# – Export & Extract Guide
  steps:
  - name: Expected Output
    text: '```text Exported Layer_1.pdf Exported Layer_2.pdf Exported Layer_3.pdf
      Flattened PDF saved as output_flattened.pdf ```'
  - name: What if the PDF has no layers?
    text: 'The `Layers` collection will be empty, and both loops will simply skip.
      It’s good practice to check `layers.Count` before proceeding:'
  - name: Can I flatten only a subset of layers?
    text: 'Absolutely. Just filter the collection before calling `Flatten`. For instance,
      to flatten only layers whose IDs are even:'
  - name: Does flattening affect vector quality?
    text: When you flatten, Aspose.PDF rasterizes the content **only if** the layer
      contains raster images. Pure vector layers stay vector, so the output remains
      crisp at any zoom level.
  - name: How does this differ from simply printing to PDF?
    text: Printing creates a new file but often loses metadata and can embed fonts
      unnecessarily. **Flatten PDF layers** preserves the original document structure
      while removing the layer hierarchy, resulting in a smaller, more portable file.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: تسوية طبقات PDF في C# – دليل التصدير والاستخراج
url: /ar/net/document-manipulation/flatten-pdf-layers-in-c-export-extract-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تسوية طبقات PDF في C# – دليل التصدير والاستخراج

هل احتجت يومًا إلى **تسوية طبقات PDF** لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. سواءً كنت تقوم بتنظيف ملف تصميم متعدد الطبقات أو تحضير PDF للأرشفة، فإن تعلم **كيفية تسوية الطبقات** سيوفر عليك الكثير من المتاعب لاحقًا.

في هذا الدرس سنستعرض استخراج الطبقات من ملف PDF، وتصدير كل طبقة كملف منفصل، وأخيرًا تسويتها مرة أخرى في صفحة واحدة. في النهاية ستحصل على مثال كامل وقابل للتنفيذ بلغة C# يوضح **كيفية تصدير الطبقات**، **كيفية تسوية الطبقات**، وحتى **كيفية استخراج الطبقات من PDF** باستخدام مكتبة Aspose.PDF الشهيرة.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (يمكنك أيضًا استهداف .NET Framework 4.7+)
- Visual Studio 2022 (أو أي محرر تفضله)
- حزمة NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
- ملف PDF يحتوي فعليًا على طبقات (غالبًا ما يتم إنشاؤه بواسطة أدوات CAD أو التصميم)

إذا كان أي من ذلك غير مألوف بالنسبة لك، لا تقلق—تثبيت حزمة NuGet سهل مثل كتابة `dotnet add package Aspose.PDF` في الطرفية.

![مخطط تسوية طبقات PDF](flatten-pdf-layers.png)

*نص بديل: مخطط تسوية طبقات PDF*

## الخطوة 1: تحميل ملف PDF والوصول إلى الصفحة الثانية

أولاً: نحتاج إلى فتح المستند والحصول على الصفحة التي تحتوي على الطبقات التي نريد العمل معها. في معظم ملفات PDF التصميمية تكون الطبقات على الصفحة 2 (الفهرس 1)، لكن يمكنك تعديل الفهرس ليتناسب مع ملفك.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the PDF
Document doc = new Document("input.pdf");

// Retrieve the collection of layers from the second page (index 1)
var layers = doc.Pages[1].Layers;
```

> **لماذا هذا مهم:** `doc.Pages[1]` يشير إلى الصفحة الثانية لأن Aspose.PDF يستخدم فهرسة تبدأ من الصفر. خاصية `Layers` تمنحنا وصولًا مباشرًا إلى كل طبقة متجهة أو نقطية مدمجة في تلك الصفحة.

## الخطوة 2: تصدير كل طبقة كملف PDF منفصل

الآن بعد أن لدينا مجموعة `layers`، دعنا **نصدر طبقات PDF** واحدة تلو الأخرى. الحلقة أدناه تحفظ كل طبقة في ملف يُسمى وفقًا للمعرف الداخلي لها.

```csharp
// Export each individual layer as a separate PDF file
foreach (var layer in layers)
{
    // The Save method writes only the current layer to a new PDF
    layer.Save($"Layer_{layer.Id}.pdf");
}
```

**ما ستراه:** بعد تشغيل هذا المقتطف ستحصل على `Layer_1.pdf`، `Layer_2.pdf`، … كل منها يحتوي على المحتوى المرئي لطبقة أصلية واحدة. هذا هو جوهر **كيفية تصدير الطبقات**—بدون أي تعقيدات إضافية.

## الخطوة 3: تسوية جميع الطبقات مرة أخرى في الصفحة

التصدير مفيد للفحص، لكن غالبًا ما تحتاج إلى صفحة واحدة مسطحة للتوزيع. طريقة `Flatten` تدمج كل طبقة مرئية في تدفق محتوى الصفحة مع الحفاظ على التخطيط الأصلي.

```csharp
// Flatten all layers into the page (the original content is preserved)
foreach (var layer in layers)
{
    // Pass true to remove the layer after flattening; false would keep it hidden.
    layer.Flatten(true);
}
```

> **نصيحة احترافية:** ضبط علم `flatten` إلى `true` يزيل الطبقة بعد الدمج، مما يحافظ على نظافة PDF النهائي. إذا كنت بحاجة إلى الاحتفاظ بالطبقات للتعديل لاحقًا، استخدم `false` بدلاً من ذلك.

## الخطوة 4: حفظ المستند المعدل

لقد استخرجنا، وصدرنا، وسوينا—الآن نحتاج فقط إلى كتابة التغييرات إلى القرص.

```csharp
// Save the final, flattened PDF
doc.Save("output_flattened.pdf");
```

تشغيل البرنامج بالكامل ينتج عن:

- ملفات PDF منفصلة لكل طبقة أصلية (`Layer_*.pdf`)
- ملف `output_flattened.pdf` جديد حيث تم دمج جميع الطبقات في صفحة واحدة قابلة للطباعة

## مثال عملي كامل

بجمع كل شيء معًا، إليك تطبيق console مستقل يمكنك نسخه ولصقه في مشروع جديد.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace FlattenPdfLayersDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document doc = new Document("input.pdf");

            // 2️⃣ Grab layers from the second page (index 1)
            var layers = doc.Pages[1].Layers;

            // 3️⃣ Export each layer as its own PDF
            foreach (var layer in layers)
            {
                string fileName = $"Layer_{layer.Id}.pdf";
                layer.Save(fileName);
                Console.WriteLine($"Exported {fileName}");
            }

            // 4️⃣ Flatten the layers back into the page
            foreach (var layer in layers)
            {
                layer.Flatten(true); // true → remove layer after flattening
            }

            // 5️⃣ Save the flattened result
            doc.Save("output_flattened.pdf");
            Console.WriteLine("Flattened PDF saved as output_flattened.pdf");
        }
    }
}
```

### النتيجة المتوقعة

```text
Exported Layer_1.pdf
Exported Layer_2.pdf
Exported Layer_3.pdf
Flattened PDF saved as output_flattened.pdf
```

افتح `output_flattened.pdf` في أي عارض وسترى صفحة واحدة نظيفة تحتوي على جميع الرسومات الأصلية دون أي طبقات مخفية.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان PDF لا يحتوي على طبقات؟

ستكون مجموعة `Layers` فارغة، وستتخطى كلا الحلقةين ببساطة. من الممارسات الجيدة التحقق من `layers.Count` قبل المتابعة:

```csharp
if (layers.Count == 0)
{
    Console.WriteLine("No layers found on the selected page.");
    return;
}
```

### هل يمكنني تسوية جزء فقط من الطبقات؟

بالطبع. فقط قم بفلترة المجموعة قبل استدعاء `Flatten`. على سبيل المثال، لتسوية الطبقات التي أرقام معرفاتها زوجية فقط:

```csharp
foreach (var layer in layers.Where(l => l.Id % 2 == 0))
{
    layer.Flatten(true);
}
```

### هل تؤثر التسوية على جودة المتجهات؟

عند التسوية، تقوم Aspose.PDF بتحويل المحتوى إلى نقطي **فقط إذا** كانت الطبقة تحتوي على صور نقطية. الطبقات المتجهة النقية تبقى متجهة، لذا يبقى الناتج واضحًا عند أي مستوى تكبير.

### كيف يختلف هذا عن الطباعة إلى PDF ببساطة؟

الطباعة تنشئ ملفًا جديدًا لكنها غالبًا ما تفقد البيانات الوصفية وقد تضمّن الخطوط دون حاجة. **تسوية طبقات PDF** تحافظ على بنية المستند الأصلي مع إزالة هيكل الطبقات، مما ينتج ملفًا أصغر وأكثر قابلية للنقل.

## أفضل الممارسات للعمل مع طبقات PDF

- **احرص دائمًا على عمل نسخة احتياطية** من ملف PDF الأصلي قبل التسوية—بمجرد دمج الطبقات، لا يمكنك استعادتها إلا إذا صدرتها أولاً.
- **قم بالتصدير قبل التسوية** إذا كنت تتوقع الحاجة إلى الطبقات الفردية لاحقًا (الكود أعلاه يفعل ذلك بالضبط).
- **استخدم أسماء ملفات وصفية** (`Layer_{layer.Name}.pdf` إذا كانت المكتبة تعرض خاصية `Name`) لتجنب الالتباس.
- **تحقق من النتيجة** بفتح PDF المسطح في عارض يُظهر معلومات الطبقات (مثل Adobe Acrobat). إذا كانت قائمة الطبقات فارغة، فقد نجحت.

## الخلاصة

أنت الآن تعرف كيفية **تسوية طبقات PDF** في C# بالإضافة إلى إتقان **استخراج الطبقات من PDF**، **كيفية تصدير الطبقات**، و**كيفية تسوية الطبقات** للحصول على مستند نهائي نظيف. المثال الكامل يوضح كل خطوة—من تحميل الملف، تصدير كل طبقة، تسويتها، إلى حفظ النتيجة النهائية—حتى يمكنك نسخه ولصقه وتشغيله فورًا.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة علامات مائية إلى كل طبقة مُصدَّرة، أو دمج PDF المسطح مع مستندات أخرى باستخدام `PdfFileEditor`. يمكنك أيضًا استكشاف **تصدير طبقات PDF** إلى صيغ صور إذا كان سير عملك يتطلب مخرجات نقطية.

If you hit any

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إضافة طبقات إلى ملف PDF](/pdf/english/net/programming-with-document/addlayers/)
- [إضافة طبقات خطوط ملونة إلى ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل شامل](/pdf/english/net/advanced-features/add-colored-lines-pdfs-using-aspose-pdf-net/)
- [كيفية إنشاء طبقات PDF باستخدام Aspose.PDF لـ Java – دليل خطوة بخطوة](/pdf/english/java/advanced-features/create-pdf-layers-aspose-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}