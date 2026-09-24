---
category: general
date: 2026-03-22
description: كيفية تشغيل OCR على ملفات PDF باستخدام Aspose.Pdf في C#. تعلم تحويل ملفات
  PDF الممسوحة ضوئياً، وجعل PDF قابلاً للبحث، وتحميل مستند PDF بسهولة.
draft: false
keywords:
- how to run OCR
- run OCR on pdf
- convert scanned pdf
- make pdf searchable
- load pdf document
language: ar
og_description: كيفية تشغيل OCR على ملفات PDF باستخدام Aspose.Pdf. يوضح لك هذا البرنامج
  التعليمي كيفية تحويل ملفات PDF الممسوحة ضوئياً، وجعل PDF قابلًا للبحث، وتحميل مستند
  PDF في C#.
og_title: كيفية تشغيل OCR على PDF – دليل C# الكامل
tags:
- OCR
- Aspose.Pdf
- C#
- PDF processing
title: كيفية تشغيل OCR على ملفات PDF باستخدام Aspose.Pdf – دليل C# الكامل
url: /ar/net/advanced-features/how-to-run-ocr-on-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR على PDF – دليل C# الكامل

كيفية تشغيل OCR على ملفات PDF هي عقبة شائعة عندما تتعامل مع الأوراق الممسوحة ضوئياً. هل حاولت البحث في فاتورة ممسوحة ضوئياً وصادفت صعوبة؟ لست وحدك. في هذا الدرس سنستعرض الخطوات الدقيقة **run OCR on PDF** باستخدام Aspose.Pdf، لتحويل مسح ضبابي إلى مستند قابل للبحث بالكامل. في النهاية ستعرف أيضاً كيفية **convert scanned PDF**، **make PDF searchable**، وبالطبع **load PDF document** دون عناء.

سنغطي كل شيء من إعداد المشروع إلى التحقق من النتيجة. لا إيماءات غير ضرورية، ولا اختصارات “انظر الوثائق”—فقط مثال كامل وقابل للتنفيذ يمكنك لصقه في Visual Studio اليوم. إذا كنت تتساءل ما إذا كان هذا يعمل مع .NET 6 أو .NET Framework 4.8، فالجواب نعم؛ Aspose.Pdf يدعم كلاهما، والكود أدناه يتكيف تلقائياً.

## المتطلبات المسبقة

- **Aspose.Pdf for .NET** (أحدث نسخة حتى مارس 2026). يمكنك الحصول عليها من NuGet: `Install-Package Aspose.Pdf`.
- **scanned PDF** تريد معالجته (ضعه في مجلد يمكنك الإشارة إليه، مثلاً `YOUR_DIRECTORY/input.pdf`).
- .NET 6 SDK أو أحدث (الصياغة تستخدم `using var` المدعومة منذ C# 8 فصاعداً).
- بيئة تطوير من اختيارك—Visual Studio أو Rider أو VS Code كلها تعمل بشكل جيد.

هذا كل شيء. لا محركات OCR إضافية، ولا خدمات خارجية. مكوّن `OcrPlugin` المدمج في Aspose يقوم بالعمل الشاق.

## كيفية تشغيل OCR – الخطوات الأساسية

فيما يلي البرنامج الكامل المستقل. احفظه كـ `Program.cs` وشغّله؛ سيتوقف الطرفية بصمت، وستجد ملف PDF قابل للبحث بجوار ملف الإدخال.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Plugins;

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document you want to OCR
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Step 2: Create a PluginManager – this is the hub for all PDF plugins
        var pluginManager = new PluginManager();

        // Step 3: Register the built‑in OCR plugin (the one that actually reads the image)
        pluginManager.RegisterPlugin(new OcrPlugin());

        // Step 4: Prepare execution options – here we set English as the language.
        // You can add more languages by comma‑separating them, e.g., "eng,spa".
        var ocrOptions = new PluginExecutionOptions
        {
            Parameters = { ["Language"] = "eng" }
        };

        // Step 5: Execute the OCR plugin on the loaded document.
        // This mutates pdfDocument in‑place, turning each scanned page into searchable text.
        pluginManager.Execute(pdfDocument, ocrOptions);

        // Step 6: Save the OCR‑processed PDF to a new file.
        pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");

        Console.WriteLine("OCR complete! Output saved to ocr-output.pdf");
    }
}
```

### ما يفعله الكود خطوة بخطوة

1. **Load PDF Document** – يقوم مُنشئ `Document` بقراءة الملف إلى الذاكرة. هذا يلبي متطلب “load pdf document” ويمنحنا كائنًا قابلًا للتعديل للعمل معه.
2. **Plugin Manager** – تقوم Aspose بعزل الميزات الاختيارية (مثل OCR) خلف مدير. فكر فيه كصندوق أدوات تختار منه المطرقة المناسبة.
3. **Register OCR Plugin** – باستدعاء `RegisterPlugin(new OcrPlugin())` نخبر Aspose بأننا نعتزم تنفيذ التعرف الضوئي على الأحرف.
4. **Execution Options** – يتيح لك `PluginExecutionOptions` ضبط العملية بدقة. ضبط `Language` إلى `"eng"` يخبر المحرك بالبحث عن الأحرف الإنجليزية. يمكنك أيضًا إضافة `"spa"` للإسبانية أو `"deu"` للألمانية.
5. **Run the OCR** – يقوم `pluginManager.Execute` بالتنقل عبر كل صفحة، استخراج صورة الراستر، تشغيل محرك OCR، وإضافة طبقة نصية غير مرئية. هذا هو جوهر **run OCR on pdf**.
6. **Save the Result** – الآن يحتوي ملف PDF النهائي على طبقة نص مخفية، مما يجعله **make PDF searchable**. فتحه في Adobe Reader واستخدام أداة البحث يجب أن يجد أي كلمة كتبتها.

## الخطوة 1: تحميل مستند PDF

قد تتساءل لماذا نستخدم `using var` بدلاً من `new Document()` العادي. يضمن بيان `using` تحرير مقبض الملف فور الانتهاء، وهو أمر حاسم عندما تحاول لاحقًا استبدال نفس الملف على Windows.

```csharp
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

إذا كان المسار غير صحيح، تقوم Aspose برمي استثناء `FileNotFoundException`. تحقق مرة أخرى من أذونات المجلد—خاصة على Linux حيث يمكن أن تسبب حساسية الحالة مشكلة.

## الخطوة 2: تسجيل وتكوين مكوّن OCR

مكوّن OCR لا يتم تحميله افتراضيًا للحفاظ على خفة المكتبة الأساسية. تسجيله سطر واحد، لكن يمكنك أيضًا ربط عدة مكوّنات (مثل مزيل العلامات المائية) إذا تطلب سير العمل ذلك.

```csharp
var pluginManager = new PluginManager();
pluginManager.RegisterPlugin(new OcrPlugin());
```

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة مئات ملفات PDF دفعة واحدة، أنشئ `PluginManager` مرة واحدة وأعد استخدامه. إنشاءه لكل ملف يضيف عبئًا غير ضروري.

## الخطوة 3: تنفيذ عملية OCR (Convert Scanned PDF)

الآن يأتي الجزء الثقيل. طريقة `Execute` تفحص كل صفحة، تشغل OCR، وتكتب النص مرة أخرى في PDF. إنها فعّالة—Aspose يبث بيانات الصورة، لذا لن تنفد الذاكرة حتى مع مسح 200 صفحة.

```csharp
var ocrOptions = new PluginExecutionOptions
{
    Parameters = { ["Language"] = "eng" }
};

pluginManager.Execute(pdfDocument, ocrOptions);
```

**لماذا ضبط اللغة؟** تعتمد دقة OCR بشكل كبير على نموذج اللغة. توفير `"eng"` يخبر المحرك بإعطاء أولوية لأشكال الأحرف الإنجليزية، مما يقلل الإيجابيات الزائفة.

## الخطوة 4: حفظ والتحقق من PDF قابل للبحث

الحفظ بسيط، لكن التحقق هو ما يعرقل العديد من المطورين. بعد التنفيذ، افتح الناتج في أي عارض PDF وجرب اختصار **Ctrl + F**. إذا تمكنت من العثور على كلمات كانت في الأصل مجرد صور، فقد نجحت في **make PDF searchable**.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");
```

![PDF قابل للبحث بعد OCR – كيفية تشغيل OCR على PDF](/images/ocr-searchable.png "PDF قابل للبحث الناتج بعد كيفية تشغيل OCR على PDF")

*تظهر اللقطة أعلاه طبقة النص المخفي وهي مميزة عندما تبحث عن مصطلح.*

## المشكلات الشائعة & نصائح احترافية

| المشكلة | سبب حدوثه | الحل |
|-------|----------------|-----|
| **Blank output** | معامل اللغة مفقود أو تم تعيينه إلى رمز غير مدعوم. | تأكد من `["Language"] = "eng"` (أو أي رمز ISO‑639‑2 آخر). |
| **Slow processing** | صور كبيرة بدون تقليل الدقة. | أضف `["Resolution"] = "300"` إلى `Parameters` للسماح لـ OCR بالعمل بدقة DPI أقل. |
| **Missing fonts** | يقوم OCR بإنشاء نص لكن العارض لا يستطيع عرض الخط. | ضمّن الخطوط بتعيين `pdfDocument.FontEmbeddingMode = FontEmbeddingMode.Always`. |
| **Memory leaks** | عدم التخلص من كائن `Document`. | استخدم `using var` كما هو موضح، أو استدعِ `pdfDocument.Dispose()` يدوياً. |

### حالات حافة

- **Multi‑language PDFs:** مرّر قائمة مفصولة بفواصل مثل `"eng,spa,fra"` للتعامل مع محتوى مختلط.
- **Password‑protected files:** حمّل باستخدام `new Document("file.pdf", new LoadOptions { Password = "secret" })`.
- **Selective OCR:** إذا كنت تحتاج فقط إلى OCR لصفحات معينة، أنشئ كائن `PageRange` ومرره عبر `Parameters["Pages"] = "1-3,5"`.

## ملخص: ما أنجزناه

- **How to run OCR on PDF** باستخدام المكوّن المدمج في Aspose.Pdf.
- **Convert scanned PDF** إلى نسخة قابلة للبحث دون خدمات خارجية.
- **Make PDF searchable** بحيث يمكن للمستخدمين النهائيين العثور على النص فوراً.
- **Load PDF document** بأمان وإطلاق الموارد بسرعة.

كل ذلك في أقل من 30 سطرًا من C# النظيف.

## ما الذي يمكن تجربته لاحقًا

- جرّب لغات مختلفة لتطبيق OCR على عقود متعددة اللغات.
- اجمع OCR مع **text extraction** (`pdfDocument.Pages[i].ExtractText()`) لإدخال بيانات تلقائي.
- استخدم **Redaction plugin** لإزالة المعلومات الحساسة قبل OCR، لضمان الامتثال.
- نشر الكود كخدمة مصغرة خلف نقطة API حتى يتمكن غير المطورين من رفع المسحات والحصول على ملفات PDF قابلة للبحث فورًا.

هل لديك أسئلة حول توسيع هذا إلى السحابة أو دمجه مع Azure Functions؟ اترك تعليقًا، وسنستكشف تلك السيناريوهات معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}