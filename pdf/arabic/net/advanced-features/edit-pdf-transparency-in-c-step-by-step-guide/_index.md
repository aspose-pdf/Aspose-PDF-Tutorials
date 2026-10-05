---
category: general
date: 2026-02-10
description: تعلم كيفية تعديل شفافية ملفات PDF وحفظ ملفات PDF المعدلة باستخدام Aspose.Pdf
  في C#. يتضمن مثالًا كاملاً على الشيفرة.
draft: false
keywords:
- edit pdf transparency
- save modified pdf
language: ar
og_description: تحرير شفافية PDF وحفظ PDF المعدل باستخدام Aspose.Pdf. كود C# كامل
  قابل للتنفيذ ونصائح عملية للمطورين.
og_title: تحرير شفافية PDF في C# – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: تحرير شفافية PDF في C# – دليل خطوة بخطوة
url: /ar/net/advanced-features/edit-pdf-transparency-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحرير شفافية PDF – دليل C# كامل

هل احتجت يومًا إلى **تحرير شفافية PDF** لكن لم تعرف من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون صعوبة عندما يحاولون جعل أجزاء من PDF شبه شفافة دون إعادة كتابة الملف بالكامل. الخبر السار؟ باستخدام Aspose.Pdf يمكنك تعديل التعتيم (opacity) وأنماط الدمج (blend modes) مباشرة في قاموس الموارد، ثم **حفظ PDF المعدل** في بضع أسطر من الشيفرة فقط.

في هذا الدرس سنستعرض الخطوات الدقيقة لتغيير تعتيم الخط (stroke) وتعبئة (fill) على صفحة، نشرح لماذا كل عملية مهمة، ونظهر لك كيفية حفظ التغييرات. في النهاية ستحصل على مقتطف جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET. لا مراجع غامضة، فقط شيفرة ملموسة قابلة للنسخ واللصق.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6 (أو أي نسخة حديثة من .NET) مثبتة.
- حزمة NuGet الخاصة بـ Aspose.Pdf for .NET (`Aspose.Pdf`) مضافة إلى مشروعك.
- ملف PDF (`input.pdf`) موجود في مجلد يمكنك الإشارة إليه (استبدل `YOUR_DIRECTORY` بالمسار الفعلي).

هذا كل شيء—لا مكتبات إضافية، لا إعدادات غامضة.

## الخطوة 1 – تحميل مستند PDF

أول شيء نقوم به هو فتح ملف PDF الموجود. تمثل فئة `Document` في Aspose.Pdf الملف بالكامل، واستخدام جملة `using` يضمن تحرير مقبض الملف بسرعة.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.DataEditor;

// Load the PDF you want to edit
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*لماذا هذا مهم*: تحميل المستند يمنحنا الوصول إلى هيكله الداخلي، بما في ذلك موارد الصفحة حيث توجد إعدادات الشفافية. استخدام `using var` هو نمط حديث في C# يتيح التخلص التلقائي من الكائن، مما يحافظ على نظافة التطبيق.

## الخطوة 2 – الحصول على الصفحة الأولى ومواردها

صفحات PDF تبدأ من الرقم 1، لذا `Pages[1]` تُعيد الصفحة الأولى. بعد ذلك نغلف قاموس `Resources` الخاص بها بـ `DictionaryEditor` لتسهيل عملية التعديل.

```csharp
// Get a reference to the first page (pages are 1‑based)
var firstPage = pdfDocument.Pages[1];

// Access the page's resource dictionary
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*نصيحة احترافية*: إذا كنت بحاجة لتعديل صفحة أخرى، فقط غير الفهرس (`Pages[2]`, `Pages[3]`, …). باقي المنطق يبقى كما هو.

## الخطوة 3 – تحديد (أو إنشاء) القاموس الفرعي ExtGState

مدخل `ExtGState` يحتوي على كائنات حالة الرسومات، والتي تشمل التعتيم (`CA` / `ca`) ووضع الدمج (`BM`). إذا لم يكن القاموس موجودًا، سيقوم Aspose بإنشائه لنا عند إضافة مدخل جديد.

```csharp
// Retrieve the ExtGState dictionary; create if missing
var extGStateDict = resourcesEditor["ExtGState"]
    .ToCosPdfDictionary(); // throws if missing, so ensure it exists
```

*ما الذي يحدث*: `ExtGState` هو المكان الذي يخزن فيه PDF حالات الرسومات القابلة لإعادة الاستخدام. بإضافة مدخل جديد (`GS0`) يمكننا لاحقًا الإشارة إليه من أي تدفق محتوى.

## الخطوة 4 – بناء حالة رسومية جديدة بالشفافية المطلوبة

الآن نحدد قيم الشفافية الفعلية:

- **CA** – تعتيم الخط (1 = معتم تمامًا).
- **ca** – تعتيم التعبئة (0.5 = شفاف بنسبة 50 %).
- **BM** – وضع الدمج (عادةً `"Normal"`).

```csharp
// Create a fresh graphics state dictionary
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define stroke opacity (CA), fill opacity (ca), and blend mode (BM)
newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity
newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // fill opacity (50% transparent)
newGraphicsState.Add("BM", new CosPdfName("Normal"));    // blend mode
```

*لماذا هذه المفاتيح*: يميز PDF بين الخط (`CA`) والتعبئة (`ca`) لأنك قد ترغب في حد صلب مع داخل شفاف. وضع الدمج يتحكم في كيفية خلط الكائن مع المحتوى الأساسي؛ `"Normal"` هو الخيار الأكثر أمانًا كإعداد افتراضي.

## الخطوة 5 – تسجيل حالة الرسومات والإشارة إليها

نضيف الحالة الجديدة إلى قاموس `ExtGState` تحت اسم فريد (`GS0`). لاحقًا يمكنك تطبيقها على أوامر رسم محددة، لكن مجرد إضافتها يكفي للعديد من الحالات التي يشير فيها PDF بالفعل إلى الحالة.

```csharp
// Register the new graphics state in the ExtGState dictionary
extGStateDict.Add("GS0", newGraphicsState);
```

*حالة حافة*: إذا كان `GS0` موجودًا مسبقًا، قد تحتاج إلى توليد مفتاح فريد (`GS1`, `GS2`, …) لتجنب الكتابة فوق الإعدادات الحالية.

## الخطوة 6 – حفظ PDF المعدل

أخيرًا، نكتب المستند المعدل إلى ملف جديد. هذه الخطوة **تحفظ PDF المعدل** مع ترك الأصلي دون تغيير.

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*النتيجة*: الآن يحتوي `output.pdf` على حالة رسومية تجعل أي كائنات مملوءة شفافة بنسبة 50 % (يبقى الخط معتمًا تمامًا). افتحه في Adobe Acrobat أو أي عارض للتحقق من التأثير.

## مثال كامل يعمل

بدمج كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.DataEditor;

using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// 1️⃣ Get first page and its resources
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);

// 2️⃣ Access (or create) ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]
    .ToCosPdfDictionary();

// 3️⃣ Define a new graphics state with transparency
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity
newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // fill opacity (50% transparent)
newGraphicsState.Add("BM", new CosPdfName("Normal"));    // blend mode

// 4️⃣ Register it as GS0
extGStateDict.Add("GS0", newGraphicsState);

// 5️⃣ Save the result
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

> **النتيجة المتوقعة** – عند فتح `output.pdf`، أي رسم يستخدم حالة الرسومات المضافة حديثًا سيظهر بتعبئة نصف شفافة بينما يبقى الحد واضحًا بالكامل. إذا لم تلاحظ أي تغيير، تحقق مرة أخرى من أن محتوى الصفحة يشير فعليًا إلى `GS0`؛ وإلا يمكنك إدراج مشغل `/GS0 gs` يدويًا في تدفق المحتوى.

## الأسئلة المتكررة (FAQs)

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تغيير التعتيم لكائن محدد فقط؟** | نعم. بعد إنشاء `GS0`، عدل تدفق محتوى الصفحة (مثلاً `firstPage.Contents[1]`) وأضف مسبقًا `/GS0 gs` قبل أوامر الرسم التي تريد أن تتأثر. |
| **ماذا لو كان PDF يحتوي بالفعل على مدخل ExtGState؟** | أضف مفتاحًا جديدًا (`GS1`, `GS2`, …) لتجنب التعارض. الشيفرة أعلاه تستخدم `GS0` للبساطة. |
| **هل يعمل هذا مع ملفات PDF المشفرة؟** | يجب توفير كلمة المرور عند التحميل: `new Document("file.pdf", new LoadOptions { Password = "secret" })`. باقي الخطوات تبقى كما هي. |
| **هل “Normal” هو وضع الدمج الوحيد؟** | لا. يدعم PDF وضعات مثل `"Multiply"`, `"Screen"`, `"Overlay"` وغيرها. ما عليك سوى استبدال السلسلة في مدخل `BM`. |
| **كيف أتحقق من التغيير برمجيًا؟** | بعد الحفظ، يمكنك قراءة قاموس `ExtGState` مرة أخرى والتأكد من أن `ca` يساوي `0.5`. |

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن عرفت كيفية **تحرير شفافية PDF** و**حفظ PDF المعدل**، قد ترغب في استكشاف:

- **تطبيق حالة الرسومات على النص** – استخدم نفس `GS0` قبل مشغل `Tf` للحصول على خطوط شبه شفافة.
- **معالجة دفعة متعددة للصفحات** – كرر الحلقة عبر `pdfDocument.Pages` وطبق الخطوات نفسها.
- **دمج مع طبقات الصور** – ضع PNG فوق المحتوى الموجود وتحكم في شفافيته عبر نفس حالة الرسومات.
- **ضغط PDF النهائي** – استدعِ `pdfDocument.Optimize()` قبل الحفظ لتقليل حجم الملف.

هذه المواضيع توسع التقنية الأساسية وتُحافظ على كفاءة سير عملك مع PDF.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، لا تتردد في ترك تعليق أدناه أو مراجعة مرجع Aspose.Pdf API للمزيد من التفاصيل.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}