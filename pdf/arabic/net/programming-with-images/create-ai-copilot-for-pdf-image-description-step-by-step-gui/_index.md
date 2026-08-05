---
category: general
date: 2026-08-04
description: إنشاء AI Copilot لتوليد وصف الصور لملفات PDF. تعلم كيفية تكوين خيارات
  الصور في OpenAI واستخراج وصف الصورة بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: ar
lastmod: 2026-08-04
og_description: إنشاء مساعد AI لتوليد وصف الصور لملفات PDF. يوضح لك هذا البرنامج التعليمي
  كيفية تكوين خيارات صورة OpenAI، تشغيل المساعد، واستخراج وصف الصورة باستخدام C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: إنشاء مساعد ذكي للذكاء الاصطناعي لوصف صور PDF – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: إنشاء مساعد AI لوصف صور PDF – دليل خطوة بخطوة
url: /ar/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مساعد AI لوصف صور PDF – دليل كامل

إذا كنت بحاجة إلى **إنشاء مساعد AI** يكتب أوتوماتيكياً أوصافاً للصور المدمجة في ملف PDF، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. ستتعلم كيفية تكوين خيارات صورة OpenAI، تشغيل المساعد، و **استخراج وصف الصورة** دون مغادرة مشروع C# الخاص بك.

إنشاء محتوى نصي لصور PDF هو طلب شائع من أجل تحسين إمكانية الوصول، فهرسة المحتوى، والتقارير الآلية. في نهاية هذا الشرح ستحصل على مكوّن قابل لإعادة الاستخدام **ينتج وصف الصورة** لأي مستند PDF تشير إليه.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث مثبت  
* رخصة Aspose.Pdf.AI (أو نسخة تجريبية مجانية)  
* مفتاح API الخاص بـ OpenAI يمكن لعميل Aspose استخدامه  
* Visual Studio 2022 (أو أي بيئة تطوير تدعم C#)  

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Pdf.AI`.

## الخطوة 1: إعداد عميل Aspose.Pdf.AI

الخطوة الأولى هي إنشاء عميل AI باستخدام تفاصيل المصادقة الخاصة بك. يتولى العميل التعامل مع خدمة OpenAI في الخلفية.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**لماذا هذا مهم:** الـ `AiClient` يضم جميع إعدادات مستوى الطلب (مفتاح API، مهلة الاتصال، سياسة إعادة المحاولة). إن إنشائه مرة واحدة وإعادة استخدامه عبر عدة نسخ من المساعد يقلل من الحمل ويضمن مصادقة متسقة.

## الخطوة 2: إنشاء مساعد وصف الصورة

الآن تقوم بإنشاء **مساعد AI** سيقرأ ملف PDF وينتج وصفًا لكل صورة. طريقة المصنع `CreateImageDescriptionCopilot` تقبل العميل ومجموعة من الخيارات التي تحدد كيفية توليد الوصف.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**لماذا هذا مهم:**  
* `OpenAIImageDescriptionOptions` (وهي **خيارات صورة OpenAI**) تتيح لك ضبط نموذج اللغة. تعديل درجة الحرارة أو النموذج يمكن أن يحسّن الصلة للرسوم التقنية مقارنةً بالصور الطبيعية.  
* تحديد مسار المستند يخبر المساعد أي ملف PDF يجب فحصه. المساعد يستخرج كل صورة نقطية، يرسلها إلى النموذج، ويعيد وصفًا مقروءًا للإنسان.

## الخطوة 3: استرجاع الوصف المُولد بشكل غير متزامن

يعمل المساعد بشكل غير متزامن لأنه قد يحتاج إلى رفع عدة ميغابايت من بيانات الصورة وانتظار استجابة النموذج. استخدم `await` لضمان إكمال الاستدعاء قبل الوصول إلى النتيجة.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**لماذا هذا مهم:** تُعيد الطريقة `Dictionary<int, string>` التي تربط كل صفحة (أو فهرس صورة) بوصفها. معالجة `AiException` تسمح لك بإظهار أخطاء الشبكة أو الحصص بدلاً من تعطل التطبيق.

## الخطوة 4: عرض أو تخزين الوصف

يمكنك كتابة الأوصاف إلى وحدة التحكم، ملف سجل، أو تضمينها مرة أخرى في PDF كنص بديل لتحسين إمكانية الوصول. أدناه مثال سريع يكتب النتيجة إلى ملف JSON للاستخدام لاحقًا.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**لماذا هذا مهم:** حفظ الناتج كملف JSON يحافظ على الربط بين كل صفحة ووصفها، مما يجعل من السهل على العمليات اللاحقة (فهرسة البحث، عرض الواجهة، إلخ) استهلاك البيانات.

## التعامل مع عدة صور في صفحة واحدة

إذا احتوت الصفحة على عدة صور، يُعيد المساعد وصفًا موحدًا مفصولًا بفواصل أسطر. لتقسيمها، افحص النتيجة الخام وقسّمها على `\n\n` (سطرين متتاليين). إليك طريقة مساعدة:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

يمكنك بعد ذلك التكرار على كل وصف صورة منفصل وتخزينه بشكل مستقل إذا لزم الأمر.

## حالة حافة: ملفات PDF الكبيرة وإدارة مهلة الاتصال

معالجة ملف PDF أكبر من 100 ميغابايت قد تتجاوز مهلات HTTP الافتراضية. عدّل إعداد مهلة العميل عند إنشاء `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

زيادة المهلة تمنع الإنهاء المبكر بينما تقوم الخدمة بمعالجة العديد من الصور عالية الدقة.

## نصيحة احترافية: تخزين النتائج مؤقتًا لتقليل التكلفة

تفرض OpenAI تكلفة لكل توكن، ويمكن أن تكون أوصاف الصور متكررة عبر إصدارات التقرير نفسه. احفظ ناتج JSON واستخدمه مرة أخرى عندما يتطابق تجزئة PDF مع ملف تم معالجته مسبقًا. هذه الممارسة توفر المال وتسرّع عمليات التشغيل اللاحقة.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

احفظ التجزئة جنبًا إلى جنب مع ملف JSON؛ إذا تطابقت التجزئة في تشغيل لاحق، تخطّ استدعاء AI.

## مثال كامل قابل للتنفيذ

بدمج كل ما سبق، إليك تطبيق وحدة تحكم مستقل يمكنك لصقه في مشروع .NET جديد.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**الناتج المتوقع (مقتطع)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

يقوم البرنامج بقراءة `AnnualReport.pdf`، ينشئ **مساعد AI**، ويكتب ملف JSON يربط كل صفحة بالوصف المُولد لها.

## أسئلة شائعة

* **هل يعمل هذا مع ملفات PDF المشفرة؟**  
  نعم، ولكن عليك توفير كلمة المرور عند إنشاء المساعد:  
  `imageOptions.WithPassword("mySecret")`.

* **هل يمكنني تحديد معالجة صفحات معينة فقط؟**  
  استخدم `imageOptions.WithPageRange(1, 10)` لتقييد المساعد على الصفحات 1‑10.

* **ماذا لو احتوت الصورة على نص؟**  
  يحاول النموذج وصف المحتوى البصري؛ لاستخراج النص بنمط OCR يجب عليك استخدام `CreateTextExtractionCopilot` بدلاً من ذلك.

## الخلاصة

أنت الآن تعرف كيف **تنشئ مساعد AI** الذي **ينتج وصف الصورة** لملفات PDF، وتُكوّن **خيارات صورة OpenAI**، وتُستخرج **وصف الصورة** برمجيًا في C#. يوضح المثال الكامل أفضل الممارسات مثل التعامل غير المتزامن، إدارة الأخطاء، وتخزين النتائج مؤقتًا.

بعد ذلك، قد ترغب في استكشاف:

* إضافة الأوصاف المُولدة مرة أخرى إلى PDF كنص بديل لتحسين إمكانية الوصول (`PdfDocument` → `PdfImage.AlternativeText`).  
* استخدام نمط المساعد نفسه **لإنشاء تقارير وصف الصور PDF** للمعالجة الدفعية.  
* تجربة نماذج OpenAI مختلفة أو إعدادات درجة الحرارة لضبط أسلوب الوصف.

لا تتردد في تعديل الكود، تجربة مستندات أكبر، ودمج الناتج في خط أنابيب الفهرسة الخاص بك. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}