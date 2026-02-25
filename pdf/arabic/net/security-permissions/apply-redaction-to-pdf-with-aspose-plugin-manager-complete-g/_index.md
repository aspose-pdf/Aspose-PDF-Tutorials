---
category: general
date: 2026-02-25
description: تعلم كيفية تطبيق الحجب على ملفات PDF باستخدام مدير الإضافات الخاص بـ
  Aspose. سنوضح لك كيفية استخدام مدير الإضافات، وتحميل إضافة PDF بالاسم، وأكثر من
  ذلك.
draft: false
keywords:
- apply redaction to pdf
- use plugin manager
- how to use plugin manager
- how to load pdf plugin
- load plugin by name
language: ar
og_description: قم بتطبيق التشويش على ملفات PDF بسرعة باستخدام مدير إضافات Aspose.
  اكتشف كيفية استخدام مدير الإضافات، وتحميل إضافة PDF بالاسم، وحماية البيانات الحساسة.
og_title: تطبيق الحجب على PDF باستخدام مدير إضافات Aspose – دليل كامل
tags:
- Aspose.Pdf
- C#
- PDF Redaction
title: تطبيق التعتيم على ملفات PDF باستخدام مدير إضافات Aspose – دليل كامل
url: /ar/net/security-permissions/apply-redaction-to-pdf-with-aspose-plugin-manager-complete-g/
---

shortcodes at top and bottom.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق الحجب على ملفات PDF باستخدام Aspose Plugin Manager – دليل شامل

هل احتجت يومًا إلى **تطبيق الحجب على ملفات PDF** لكن لم تكن متأكدًا أي استدعاء API سيؤدي المهمة؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند حماية المعلومات السرية. الخبر السار؟ باستخدام **Plugin Manager** الخاص بـ Aspose.Pdf، يمكنك تحميل إضافة Redaction في الوقت الفعلي والبدء في تنقية مستنداتك ببضع أسطر من الشيفرة فقط.

في هذا الدرس سنستعرض **كيفية استخدام Plugin Manager**، نوضح **كيفية تحميل إضافة PDF** بالاسم، ثم نطبق **الحجب على PDF** فعليًا. في النهاية ستحصل على مثال مكتمل، قابل للتنفيذ، يمكنك إدراجه في أي مشروع .NET.

## المتطلبات المسبقة — ما ستحتاجه

- .NET 6.0 أو أحدث (الشيفرة تعمل مع .NET Core و .NET Framework أيضًا)
- حزمة NuGet الخاصة بـ Aspose.Pdf for .NET (الإصدار 23.9 أو أحدث)
- ملف PDF يحتوي على نص تريد إخفائه (سنستخدم `sample.pdf` في المثال)
- Visual Studio 2022 أو أي محرر C# تفضله

لا توجد مراجع تجميعية إضافية مطلوبة لإضافة الحجب؛ **Plugin Manager** يتولى كل شيء نيابةً عنك.

## الخطوة 1: استيراد مساحة الأسماء Aspose.Pdf Plugins

قبل أن تتمكن من التفاعل مع نظام الإضافات، تحتاج إلى جلب مساحة الأسماء المناسبة إلى النطاق. هذا يمنحك الوصول إلى `PluginManager` والفئات المرتبطة.

```csharp
// Step 1: Import the Aspose.Pdf plugins namespace
using Aspose.Pdf.Plugins;
using Aspose.Pdf;          // Core PDF classes
using System.IO;          // For file handling
```

> **لماذا هذا مهم:** سطر `using Aspose.Pdf.Plugins;` هو البوابة **لاستخدام مدير الإضافات**. بدون هذا السطر ستحصل على أخطاء تجميع، حتى وإن كانت مساحة الأسماء الأساسية `Aspose.Pdf` مُشار إليها بالفعل.

## الخطوة 2: تحميل إضافة الحجب بالاسم

الآن يأتي السحر. بدلاً من إضافة مرجع DLL منفصل، ببساطة تخبر المدير بتحميل الإضافة التي تحتاجها. هذه هي الطريقة الأنظف **لتحميل الإضافة بالاسم**.

```csharp
// Step 2: Load the Redaction plugin (no explicit assembly reference needed)
PluginManager.LoadPlugin("Redaction");
```

> **نصيحة احترافية:** إذا أردت التحقق من الإضافات المتاحة، استدعِ `PluginManager.GetLoadedPlugins()`—ستحصل على قائمة يمكنك تسجيلها لأغراض التصحيح.

## الخطوة 3: فتح مستند PDF الذي تريد حجب محتوياته

مع تحميل الإضافة في الذاكرة، يمكننا فتح أي ملف PDF. فئة `Document` تمثل الملف بالكامل.

```csharp
// Step 3: Load the target PDF
string inputPath = Path.Combine("Resources", "sample.pdf");
Document pdfDoc = new Document(inputPath);
```

> **ماذا لو كان الملف مفقودًا؟** مُنشئ `Document` يرمي استثناء `FileNotFoundException`. احرص على تغليف الاستدعاء بكتلة try/catch إذا كنت تتوقع ملفات مفقودة في بيئة الإنتاج.

## الخطوة 4: تعريف مناطق الحجب

يتم الحجب عن طريق تحديد مناطق مستطيلة على الصفحة. يمكنك أيضًا استخدام البحث النصي للعثور على الكلمات الحساسة تلقائيًا، لكن في هذا الدليل سنحدد الإحداثيات يدويًا.

```csharp
// Step 4: Create a redaction annotation on page 1
var redaction = new RedactionAnnotation(pdfDoc.Pages[1], new Aspose.Pdf.Rectangle(100, 500, 300, 450))
{
    FillColor = Color.Black,
    OverlayText = "REDACTED",
    OverlayTextAlignment = HorizontalAlignment.Center,
    OverlayTextColor = Color.White,
    Repeat = true
};

// Add the annotation to the page
pdfDoc.Pages[1].Annotations.Add(redaction);
```

> **لماذا نضع `Repeat = true`؟** هذا يخبر المحرك بتكرار الحجب على كل ظهور لنفس المستطيل عند معالجة المستند—اختصار مفيد عندما يكون لديك حقول متطابقة متعددة.

## الخطوة 5: تطبيق الحجب وحفظ النتيجة

تضيف إضافة الحجب طريقة `Redact` إلى فئة `Document`. استدعاؤها يزيل فعليًا المحتوى خلف التعليق ويُسطّح الطبقة العلوية.

```csharp
// Step 5: Apply redaction and save the protected PDF
pdfDoc.Redact();   // <-- This method comes from the Redaction plugin
string outputPath = Path.Combine("Output", "sample_redacted.pdf");
pdfDoc.Save(outputPath);
```

> **الناتج المتوقع:** سيظهر `sample_redacted.pdf` مطابقًا للأصل، باستثناء أن المستطيل المحدد سيصبح صندوقًا أسود صلبًا مع كلمة “REDACTED” مركزة في الوسط. كل النص المخفي يُحذف نهائيًا من تدفق الملف.

## الخطوة 6: التحقق من الحجب (اختياري)

إذا أردت التأكد تمامًا من عدم إمكانية استعادة المحتوى المحجوب، افتح ملف PDF المحفوظ في محرر نصوص وابحث عن السلسلة الأصلية. لن تجدها—محرك Aspose يزيلها أثناء تنفيذ `Redact()`.

```csharp
// Quick verification (for demo purposes only)
bool containsSecret = File.ReadAllText(outputPath).Contains("SecretValue");
Console.WriteLine(containsSecret ? "Redaction failed!" : "Redaction successful.");
```

> **خطأ شائع:** نسيان استدعاء `Redact()` بعد إضافة التعليقات. التعليق وحده يخفي البيانات *بصريًا* فقط؛ النص الأساسي يظل قابلًا للبحث حتى تقوم بتنفيذ عملية الحجب.

## مثال كامل يعمل

بجمع كل ما سبق، إليك ملف واحد يمكنك نسخه‑ولصقه في مشروع Console وتشغيله فورًا.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Plugins;
using Aspose.Pdf.Annotations;
using System;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // Load the Redaction plugin – no extra DLL needed
        PluginManager.LoadPlugin("Redaction");

        // Open the PDF you want to protect
        string input = Path.Combine("Resources", "sample.pdf");
        Document doc = new Document(input);

        // Define a redaction area on the first page
        var redaction = new RedactionAnnotation(
            doc.Pages[1],
            new Rectangle(100, 500, 300, 450))
        {
            FillColor = Color.Black,
            OverlayText = "REDACTED",
            OverlayTextAlignment = HorizontalAlignment.Center,
            OverlayTextColor = Color.White,
            Repeat = true
        };
        doc.Pages[1].Annotations.Add(redaction);

        // Apply the redaction (this actually removes the data)
        doc.Redact();

        // Save the sanitized PDF
        string output = Path.Combine("Output", "sample_redacted.pdf");
        doc.Save(output);

        // Simple verification
        bool hidden = File.ReadAllText(output).Contains("SecretValue");
        Console.WriteLine(hidden ? "Redaction failed." : "Redaction succeeded!");
    }
}
```

شغّل البرنامج، افتح `Output/sample_redacted.pdf`، وسترى الصندوق الأسود حيث كان النص الحساس موجودًا. هذا هو **تطبيق الحجب على PDF** عمليًا.

![تطبيق الحجب على PDF باستخدام Aspose Plugin Manager](redaction-demo.png){alt="تطبيق الحجب على PDF باستخدام Aspose Plugin Manager"}

## الأسئلة المتكررة

### هل يعمل هذا مع ملفات PDF المشفرة؟
نعم—ما عليك سوى تمرير كلمة المرور عند إنشاء كائن `Document`: `new Document(inputPath, "password")`. سيُطبق الحجب بعد فك التشفير.

### هل يمكن حجب عدة صفحات مرة واحدة؟
بالطبع. يمكنك التكرار عبر `doc.Pages` وإضافة `RedactionAnnotation` إلى كل صفحة تحتاجها. علمة `Repeat` تعمل لكل تعليق على حدة، وليس لكل صفحة.

### ماذا لو احتجت **لتحميل إضافة pdf** ديناميكيًا بناءً على إدخال المستخدم؟
يمكنك استدعاء `PluginManager.LoadPlugin(userChosenName)` حيث `userChosenName` هو سلسلة مثل `"Redaction"` أو `"Watermark"`. تأكد فقط من وجود الإضافة في مجلد إضافات Aspose.

### هل هناك طريقة **لاستخدام مدير الإضافات** دون كتابة اسم الإضافة صراحةً؟
نعم—استخدم `PluginManager.GetAvailablePlugins()` لاستعراض الإضافات المتاحة ودع المستخدم يختار من قائمة واجهة المستخدم. هذا يجعل الكود مرنًا ومستقبليًا.

## الخلاصة

لقد أظهرنا لك كيفية **تطبيق الحجب على PDF** باستخدام **Plugin Manager** الخاص بـ Aspose. الخطوات—استيراد مساحة الأسماء، **تحميل الإضافة بالاسم**، إنشاء تعليقات الحجب، استدعاء `Redact()`، ثم الحفظ—تشكل سير العمل الكامل من البداية حتى النهاية.

الآن بعد أن عرفت **كيفية استخدام مدير الإضافات** و**كيفية تحميل إضافة PDF** دون إضافة مراجع إضافية، يمكنك حماية أي مستند يمر عبر تطبيقك. جرّب لاحقًا دمج الحجب مع استخراج النص أو OCR لتحديد العبارات الحساسة تلقائيًا—هذه توسعات طبيعية لما غطيناه.

هل لديك أسئلة إضافية حول Aspose أو معالجة PDF أو بنى الإضافات؟ اترك تعليقًا، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}