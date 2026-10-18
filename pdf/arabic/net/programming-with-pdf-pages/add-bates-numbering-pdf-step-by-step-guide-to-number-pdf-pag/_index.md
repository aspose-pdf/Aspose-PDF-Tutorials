---
category: general
date: 2026-03-03
description: أضف ترقيم بيتس إلى ملفات PDF بسرعة وتعلم كيفية ترقيم صفحات PDF أو إضافة
  أرقام PDF متسلسلة باستخدام Aspose.Pdf في C#.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: ar
og_description: إضافة ترقيم بايتس لملف PDF باستخدام C# لترقيم صفحات PDF وإضافة أرقام
  PDF متسلسلة. الكود الكامل، الشروحات، وأفضل الممارسات.
og_title: إضافة ترقيم بايتس إلى PDF – دورة شاملة في C#
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: إضافة ترقيم بايتس إلى PDF – دليل خطوة بخطوة لترقيم صفحات PDF
url: /ar/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة ترقيم Bates إلى PDF – دليل C# الكامل

هل احتجت يوماً إلى **add bates numbering pdf** للملفات لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—ففرق القانونية، المدققون، والأرشيفيون يواجهون نفس المشكلة. الخبر السار؟ ببضع أسطر من C# ومكتبة Aspose.Pdf يمكنك **number pdf pages** تلقائيًا، وستحصل أيضًا على مرونة **add sequential pdf numbers** مع بادئات، لاحقات، ومواقع مخصصة.

في هذا الدليل سنستعرض مثالًا واقعيًا، نشرح لماذا كل إعداد مهم، ونظهر لك كيفية تعديل الكود لحالات خاصة مثل أحجام الصفحات المختلفة أو عدد الأرقام المخصص. في النهاية ستحصل على مقطع جاهز للتنفيذ يضيف أرقام Bates إلى أي PDF تستخدمه، وستفهم “السبب” وراء كل خيار.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- ترخيص صالح لـ Aspose.Pdf for .NET (أو مفتاح تقييم مجاني)
- Visual Studio 2022 (أو أي محرر C# تفضله)
- ملف PDF مصدر اسمه `source.pdf` في مجلد يمكنك الإشارة إليه

هذا كل شيء—لا تحتاج إلى حزم NuGet إضافية بخلاف Aspose.Pdf.

## الخطوة 1 – فتح مستند PDF المصدر

أول شيء تحتاج إلى القيام به هو تحميل ملف PDF الذي تريد وضع العلامة عليه. استخدام كتلة `using` يضمن تحرير مقبض الملف بشكل صحيح، مما يمنع مشاكل القفل لاحقًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Why this matters:** فتح المستند داخل جملة `using` يضمن التخلص الحتمي. إذا تخطيت ذلك، قد يبقى الملف مقفلاً، وستفشل المحاولات اللاحقة لحفظ أو حذف PDF—شيء رأيت أنه يسبب صداعًا في خطوط الإنتاج.

## الخطوة 2 – تكوين خيارات ترقيم Bates

الآن نخبر Aspose كيف نريد أن يظهر ترقيم Bates. كل خاصية ترتبط مباشرةً بعنصر بصري على الصفحة.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### نصائح سريعة للخيارات

| الخاصية | ما تقوم به | متى يجب تغييره |
|----------|--------------|-------------------|
| **Prefix / Suffix** | يضيف نصًا ثابتًا قبل/بعد الجزء الرقمي. | استخدم معرف القضية، رمز المشروع، أو “CONF‑” للوثائق السرية. |
| **Start** | الرقم الأول في السلسلة. | إذا كنت تواصل نظام ترقيم من دفعة سابقة، اضبطه وفقًا لذلك. |
| **NumberOfDigits** | يتحكم في إضافة أصفار بادئة. | في الملفات القانونية غالبًا ما تحتاج إلى 6 أرقام بالضبط؛ اضبطه إلى `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | اختر بناءً على تخطيط المستند؛ BottomRight هو الأكثر شيوعًا لأرقام Bates. |

> **Pro tip:** إذا كنت بحاجة إلى **number pdf pages** في أعمدة متعددة، يمكنك استدعاء `pdfDocument.AddBatesNumbering` مرتين بقيم `Placement` مختلفة وسلاسل `Prefix` مميزة.

## الخطوة 3 – تطبيق ترقيم Bates على المستند

مع إعداد الخيارات، يصبح الختم الفعلي استدعاء طريقة واحدة. Aspose يتعامل داخليًا مع ترقيم الصفحات، الدوران، وحسابات الهوامش.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Why a single call works:** في الخلفية، Aspose يتكرر على `pdfDocument.Pages`، ينشئ `TextFragment` لكل صفحة، ويضعه بناءً على `Placement` التي اخترتها. هذه التجريدية توفر عليك كتابة حلقة يدوية والتعامل مع تحويلات الإحداثيات.

## الخطوة 4 – حفظ PDF المحدث

أخيرًا، اكتب الملف المعدل إلى القرص. يمكنك استبدال الأصلي أو إنشاء ملف جديد؛ المثال أدناه ينشئ نسخة جديدة.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

إذا كنت بحاجة إلى **add sequential pdf numbers** إلى تدفق (مثلاً عند إرسال الملف عبر API)، استبدل مسار الملف بـ `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## مثال عملي كامل

بجمع كل ذلك معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### النتيجة المتوقعة

- ملف جديد `bates_numbered.pdf` يظهر في `C:\MyDocs`.
- كل صفحة تظهر شيئًا مثل `2025-05000-A`، `2025-05001-A`، … في الزاوية السفلية اليمنى.
- الأرقام مملوءة بأصفار لتصبح خمسة أرقام، وفقًا لإعداد `NumberOfDigits`.

## معالجة التغييرات الشائعة

### 1. أحجام صفحات مختلفة

إذا كان PDF الخاص بك يحتوي على صفحات عمودية وأفقية مختلطة، قد تلاحظ أن الرقم يُقَصّ على الجانب الأوسع. لإصلاح ذلك، فعّل خاصية `AutoFit`:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. خط أو لون مخصص

أرقام Bates الافتراضية هي باللون الأسود، حجم 12‑pt من Times New Roman. غيّر المظهر عبر الوصول إلى `TextState`:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. تخطي صفحات

افترض أنك تريد **number pdf pages** لكن تخطي صفحة العنوان. استخدم نطاق صفحات:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. إضافة مخططات ترقيم متعددة

أحيانًا تتطلب الفرق القانونية كلًا من رقم Bates وعلامة مائية سرية. نفّذ استدعائين منفصلين لـ `AddBatesNumbering` بقيم `Placement` مختلفة:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات PDF التي تحتوي بالفعل على نص موجود؟**  
ج: نعم. Aspose يضيف رقم Bates كطبقة منفصلة، لذا يبقى المحتوى الموجود دون تعديل. إذا كنت تحتاج الأرقام لتظهر *خلف* النص الموجود (نادرًا)، سيتعين عليك تعديل تدفقات محتوى الصفحة يدويًا.

**س: ماذا لو كان PDF محميًا بكلمة مرور؟**  
ج: قم بتحميله باستخدام كلمة المرور أولاً: `new Document(path, new LoadOptions { Password = "secret" })`. بعد الختم، يمكنك إعادة تطبيق التشفير عبر `pdfDocument.Encrypt(...)`.

**س: هل يمكنني استخدام هذا في تطبيق .NET Core console؟**  
ج: بالتأكيد. نفس الكود يعمل في .NET Core، .NET 5+، و .NET Framework. فقط قم بالإشارة إلى حزمة Aspose.Pdf NuGet المناسبة.

## الخلاصة

لقد غطينا للتو كيفية **add bates numbering pdf** للملفات، وكيفية **number pdf pages**، وكيفية **add sequential pdf numbers** مع تحكم كامل في التنسيق، الموقع، ومعالجة الحالات الخاصة. المقتطف القصير أعلاه يقوم بالعمل الشاق، بينما الخيارات الإضافية تتيح لك تعديل الحل لأي تدفق عمل قانوني، أرشيفي، أو امتثالي.

هل أنت مستعد للخطوة التالية؟ جرّب دمج هذا النهج مع:

- **Batch processing** – تكرار عبر مجلد من ملفات PDF وتطبيق نفس مخطط الترقيم.
- **Dynamic prefixes** – سحب معرفات القضايا من قاعدة بيانات وإدراجها لكل مستند.
- **PDF/A compliance** – بعد الترقيم، استدعِ `pdfDocument.Convert(..., PdfFormat.PdfA2b)` لضمان الحفظ على المدى الطويل.

لا تتردد في التجربة، مشاركة ما توصلت إليه، أو طرح أسئلة في التعليقات. برمجة سعيدة، ولتظل ملفات PDF الخاصة بك دائمًا مفهرسة بشكل مثالي! 

![Screenshot of a PDF page with Bates numbers in the bottom‑right corner](https://example.com/images/bates-numbered.png "add bates numbering pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}