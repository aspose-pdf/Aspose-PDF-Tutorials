---
category: general
date: 2026-10-10
description: تعلم كيفية تغيير شفافية PDF في C# باستخدام Aspose.PDF. يغطي هذا الدليل
  خطوة بخطوة شفافية PDF، وتحرير حالة الرسومات، وتعديل قاموس ExtGState.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.PDF graphics state
- PDF opacity
- C# PDF manipulation
- ExtGState dictionary
language: ar
lastmod: 2026-10-10
og_description: غيّر شفافية PDF في C# باستخدام Aspose.PDF. اتبع هذا الدليل المختصر
  لتعديل شفافية PDF، كائنات حالة الرسومات، وقاموس ExtGState.
og_image_alt: Screenshot showing C# code that changes PDF transparency using Aspose.PDF
og_title: تغيير شفافية PDF في C# – دليل Aspose.PDF الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to change PDF transparency in C# using Aspose.PDF. This step‑by‑step
    guide covers PDF opacity, graphics state editing, and ExtGState dictionary manipulation.
  headline: How to change PDF transparency in C# with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF transparency
- Graphics state
title: كيفية تغيير شفافية PDF في C# باستخدام Aspose.PDF
url: /ar/net/programming-with-operators/how-to-change-pdf-transparency-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تغيير شفافية PDF في C# باستخدام Aspose.PDF

إذا كنت بحاجة إلى **تغيير شفافية PDF** في مشروع C#، يوضح لك هذا الدليل حلاً كاملاً وجاهزًا للتنفيذ. من خلال تعديل حالة الرسومات (graphics state) في PDF يمكنك التحكم في شفافية الخطوط، شفافية التعبئة، ووضع المزج (blend mode) دون الحاجة إلى إعادة إنشاء المستند من الصفر.  

سترى كيفية تحميل PDF، تعديل **قاموس ExtGState**، ضبط **شفافية PDF** المطلوبة، وحفظ النتيجة — كل ذلك باستخدام مكتبة Aspose.PDF. لا توجد أدوات خارجية مطلوبة، والكود يعمل مع .NET 6+.

## المتطلبات المسبقة

- Visual Studio 2022 (أو أي بيئة تطوير C#)  
- .NET 6 أو إصدار أحدث  
- حزمة NuGet Aspose.PDF for .NET (`Install-Package Aspose.PDF`)  
- ملف PDF اسمه `input.pdf` في مجلد تتحكم فيه  

توفر هذه المتطلبات يضمن تشغيل الدرس دون فقدان أي تبعيات.

## الخطوة 1: تحميل مستند PDF

العملية الأولى هي فتح ملف PDF الموجود. تمثل Aspose.PDF ملف PDF ككائن `Document`، والذي يمنحك وصولًا كاملاً إلى الصفحات، الموارد، والقواميس منخفضة المستوى.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Cosmos;

// Load the source PDF
var document = new Document("YOUR_DIRECTORY/input.pdf");
```

*لماذا هذا مهم:* تحميل الملف ينشئ نموذجًا في الذاكرة يمكنك تعديلّه. فئة `Document` تُجسّد بنية PDF مع إبقاء إمكانية الوصول إلى الكائنات منخفضة المستوى اللازمة لتغيير الشفافية.

## الخطوة 2: استرجاع الصفحة الأولى وقاموس مواردها

تعيش إعدادات الشفافية في قاموس موارد الصفحة تحت مدخل **ExtGState**. يجب الحصول على هذا القاموس قبل أن تتمكن من إضافة أو تعديل حالات الرسومات.

```csharp
// Get the first page (pages are 1‑based)
var page = document.Pages[1];

// The DictionaryEditor simplifies access to resource entries
var resourcesEditor = new DictionaryEditor(page.Resources);
```

*لماذا هذا مهم:* مجموعة `Resources` تحتوي على الخطوط، الصور، وحالات الرسومات المستخدمة في الصفحة. من خلال تعديلها، تؤثر فقط على الصفحة المستهدفة، مع ترك باقي المستند دون تغيير.

## الخطوة 3: الوصول إلى (أو إنشاء) قاموس ExtGState

إذا كان PDF يحتوي بالفعل على قاموس `ExtGState`، يمكنك إعادة استخدامه؛ وإلا، ستقوم Aspose.PDF بإنشاء واحد فارغ عندما تضيف أول مدخل.

```csharp
// Retrieve the ExtGState dictionary; create if missing
var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
               ?? new CosPdfDictionary(document);
```

*لماذا هذا مهم:* قاموس `ExtGState` يحمل **كائنات حالة الرسومات**. كل كائن يحدد معلمات مثل شفافية الخط (`CA`)، شفافية التعبئة (`ca`)، ووضع المزج (`BM`). تغيير هذه القيم يؤثر مباشرةً على طريقة عرض العناصر الشفافة في PDF.

## الخطوة 4: تعريف حالة رسومات جديدة بالشفافية المطلوبة

أنشئ حالة رسومات جديدة (`GS0`) واضبط معلماتها. المثال أدناه يحدد شفافية خط 100 %، شفافية تعبئة 50 %، ووضع المزج القياسي “Normal”.

```csharp
// Name for the new graphics state
string graphicsStateName = "GS0";

// Create an empty dictionary for the graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

// Populate the dictionary with transparency parameters
var graphicsStateEntries = new[]
{
    // Stroke opacity (CA) – 1 = fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // Fill opacity (ca) – 0.5 = 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – "Normal" is the most common mode
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*لماذا هذا مهم:* مدخل `CA` يتحكم في كيفية مزج الخطوط (الحدود)، بينما `ca` يؤثر على التعبئات (الأشكال، النص). تعديل هذه القيم هو جوهر **تغيير شفافية PDF**. وضع المزج يحدد كيفية تفاعل المحتوى الشفاف مع الرسومات السفلية.

## الخطوة 5: إدراج حالة الرسومات الجديدة في قاموس ExtGState

الآن أضف حالة الرسومات إلى مجموعة `ExtGState` الخاصة بالصفحة وتأكد من أن الصفحة تشير إليها.

```csharp
// Add the new graphics state to the ExtGState dictionary
extGState.Add(graphicsStateName, newGraphicsState);

// Update the Resources dictionary with the modified ExtGState
resourcesEditor["ExtGState"] = extGState;
```

*لماذا هذا مهم:* إضافة المدخل تسجّل حالة الرسومات في PDF. أي عملية رسم لاحقة تختار `GS0` ستستخدم قيم الشفافية التي حددتها.

## الخطوة 6: تطبيق حالة الرسومات على محتوى الصفحة (اختياري لكن شائع)

إذا أردت أن يتبنى المحتوى الموجود على الصفحة الشفافية الجديدة، يجب أن تُسبق محتوى الصفحة بمُعامل `gs` الذي يختار حالة الرسومات. فيما يلي طريقة بسيطة لإضافة هذا المُعامل إلى محتويات الصفحة.

```csharp
// Create a content stream that selects the new graphics state
var selectStateOperator = new GraphicsStateOperator(graphicsStateName);

// Insert the operator at the beginning of the page's content
page.Contents.Insert(0, selectStateOperator);
```

*لماذا هذا مهم:* بدون هذه الخطوة، توجد حالة الرسومات لكنها لا تُستَخدم أبدًا. مُعامل `gs` (`GraphicsStateOperator`) يخبر مُعالج PDF بتطبيق إعدادات الشفافية المعرفة على كل ما يليه.

## الخطوة 7: حفظ PDF المعدل

أخيرًا، اكتب المستند المحدث إلى القرص.

```csharp
document.Save("YOUR_DIRECTORY/output.pdf");
```

سيتم عرض `output.pdf` بالشفافية التي حددتها للتعبئة (50 % شفافة) مع الحفاظ على التخطيط الأصلي.

---

## الكود الكامل (قابل للتنفيذ)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cosmos;
using System.Collections.Generic;

class ChangePdfTransparency
{
    static void Main()
    {
        // 1️⃣ Load the PDF
        var document = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Get first page and its resource dictionary
        var page = document.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3️⃣ Access (or create) the ExtGState dictionary
        var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                       ?? new CosPdfDictionary(document);

        // 4️⃣ Define a new graphics state (GS0) with desired opacity
        string gsName = "GS0";
        var newGs = CosPdfDictionary.CreateEmptyDictionary(document);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGs.Add(e);

        // 5️⃣ Add the graphics state to ExtGState and update resources
        extGState.Add(gsName, newGs);
        resourcesEditor["ExtGState"] = extGState;

        // 6️⃣ Apply the graphics state to existing content (optional)
        var gsOperator = new GraphicsStateOperator(gsName);
        page.Contents.Insert(0, gsOperator);

        // 7️⃣ Save the modified PDF
        document.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**الناتج المتوقع:** فتح `output.pdf` في Adobe Acrobat أو أي عارض PDF يُظهر أي أشكال مملوءة في الصفحة الأولى بشفافية 50 %، بينما تبقى الخطوط غير شفافة تمامًا. التغيير البصري يؤكد أنك نجحت في **تغيير شفافية PDF**.

---

## الأسئلة الشائعة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني تغيير الشفافية لكائن معين بدلاً من الصفحة بأكملها؟* | نعم. بدلاً من إدراج مُعامل `gs` في بداية الصفحة، ضعّه مباشرةً قبل أوامر الرسم التي تستهدف الكائن. استخدم `page.Contents.Insert(index, gsOperator)` حيث يشير `index` إلى الموقع المطلوب. |
| *ماذا لو كان PDF يحتوي بالفعل على مدخل ExtGState باسم “GS0”؟* | اختر اسمًا فريدًا (مثل `GS1`) أو استبدل المدخل الموجود إذا كنت تنوي استبداله. يجب أن يكون مفتاح القاموس فريدًا داخل موارد الصفحة. |
| *هل قيمة `ca` مقصورة على 0‑1؟* | صحيح. `ca` (شفافية التعبئة) و`CA` (شفافية الخط) تقبل قيمًا من 0 (شفافية كاملة) إلى 1 (عتمة كاملة). القيم خارج هذا النطاق تُقيد تلقائيًا. |
| *هل يعمل هذا مع PDFs التي تستخدم التوافقية PDF/A أو PDF/X؟* | تعديل حالة الرسومات قد يخل بالتوافقية الصارمة. إذا كنت بحاجة للحفاظ على التوافقية، تحقق من صحة الناتج باستخدام أداة تدقق PDF/A وعدّل القاموس وفقًا لذلك (مثلاً، أضف مدخلات `/PDFXConformance`). |
| *هل يمكنني ضبط وضع مزج مختلف، مثل “Multiply”؟* | بالتأكيد. استبدل `new CosPdfName("Normal")` بـ `new CosPdfName("Multiply")` أو أي وضع مزج معرف في مواصفات PDF. |

---

## نصائح وممارسات أفضل (E‑E‑A‑T)

- **نصيحة احترافية:** خزن قاموس `ExtGState` في الذاكرة بعد أول تعديل إذا كنت تخطط لتعديل صفحات متعددة؛ هذا يقلل من تكلفة إنشاء الكائنات.  
- **احذر من:** إعادة استخدام نفس اسم حالة الرسومات عبر صفحات مختلفة دون تحديث الموارد قد يسبب خلطًا غير متوقع في الشفافية. احرص على تخصيص الاسم للصفحة أو استخدم معرفًا عالميًا فريدًا.  
- **الأداء:** بالنسبة لملفات PDF الكبيرة، فكر في معالجة الصفحات بشكل متوازي (`Parallel.ForEach`) لكن قم بمزامنة الوصول إلى كائن `Document` لتجنب مشاكل سلامة الخيوط.  
- **الاختبار:** تحقق من تغيّر الشفافية على الأقل في عارضين (Adobe Acrobat Reader وإضافة PDF في المتصفح) لأن بعض العارضين يتعاملون مع أوضاع المزج بشكل مختلف.

---

## الخلاصة

أنت الآن تعرف **كيفية تغيير شفافية PDF** في C# عبر تعديل **قاموس ExtGState** باستخدام Aspose.PDF. غطى الدرس تحميل PDF، إنشاء حالة رسومات مخصصة، تطبيقها على محتوى الصفحة، وحفظ الملف المحدث.  

من هنا يمكنك استكشاف مواضيع أكثر تقدمًا في **معالجة PDF باستخدام C#** مثل طبقة حالات رسومات متعددة، تطبيق قيم **شفافية PDF** مختلفة لكل كائن، أو دمج واجهات برمجة التطبيقات عالية المستوى في Aspose.PDF لإدراج النصوص والصور.

لا تتردد في تجربة أوضاع مزج أخرى، مستويات شفافية مختلفة، أو تطبيق حالة الرسومات على صفحات مختارة فقط. إذا واجهت أي صعوبات، توفر وثائق Aspose.PDF رؤى أعمق حول نموذج كائنات PDF وتعامل حالة الرسومات.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تغيير شفافية PDF باستخدام Aspose.PDF – دليل C# كامل](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [إضافة شفافية إلى PDF باستخدام Aspose PDF في C# – دليل خطوة بخطوة](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [إضافة شفافية إلى PDF باستخدام Aspose – دليل C# كامل](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}