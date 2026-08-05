---
category: general
date: 2026-08-04
description: كيفية استخدام Aspose لاستخراج نص PDF الممسوح ضوئياً وتحويل PDF إلى نص
  باستخدام C#. تعلم قراءة ملفات PDF الممسوحة ضوئياً والحصول على نتائج OCR موثوقة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: ar
lastmod: 2026-08-04
og_description: كيفية استخدام Aspose لقراءة ملفات PDF الممسوحة ضوئياً، واستخراج نص
  PDF الممسوح، وتحويل PDF إلى نص مع مثال كامل قابل للتنفيذ.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: كيفية استخدام Aspose – استخراج النص من ملفات PDF الممسوحة ضوئياً باستخدام
  C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: كيفية استخدام Aspose لاستخراج النص من ملف PDF ممسوح ضوئياً – دليل خطوة بخطوة
url: /ar/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose لاستخراج النص من ملف PDF ممسوح ضوئياً – دليل خطوة بخطوة

إذا كنت بحاجة إلى **how to use Aspose** للتعرف الضوئي على الأحرف (OCR)، يوضح لك هذا الدليل كيفية استخراج نص PDF الممسوح ضوئياً في بضع أسطر من C#. سواء كنت تبني خدمة أرشفة مستندات أو فهرس بحث للوثائق القديمة، فإن الحل يعمل مع أي ملف PDF ممسوح تضخه إلى خدمة Aspose.Pdf.AI.

في هذا البرنامج التعليمي ستقوم بـ:

* إنشاء مساعد OCR يقرأ ملف PDF ممسوح ضوئياً.
* استخراج النص المعترف به بشكل غير متزامن.
* عرض النص المستخرج أو معالجته بشكل إضافي.

المتطلب الوحيد هو اشتراك نشط في Aspose.Pdf.AI وبيئة تطوير .NET 6 (أو أحدث).

## المتطلبات المسبقة

| المتطلبات | لماذا يهم |
|-------------|----------------|
| .NET 6 SDK أو أحدث | يوفر `async Main` وميزات لغة حديثة. |
| حزمة NuGet Aspose.Pdf.AI (`Aspose.Pdf.AI`) | تحتوي على `AICopilotFactory` وخيارات OCR. |
| مثيل `client` صالح لـ Aspose.Pdf.AI (مفتاح API) | يُصادق على طلباتك إلى خدمة السحابة. |
| ملف PDF ممسوح ضوئياً (مثال: `Scanned.pdf`) | المستند المصدر الذي سيُستخرج منه النص. |

ثبت الحزمة باستخدام .NET CLI:

```bash
dotnet add package Aspose.Pdf.AI
```

## الخطوة 1: إعداد عميل Aspose.Pdf.AI

قبل أن تتمكن من استدعاء أي نقطة نهاية OCR يجب عليك إنشاء عميل يحمل بيانات اعتماد API الخاصة بك. العميل آمن للاستخدام عبر الخيوط ويمكن إعادة استخدامه لعدة مستندات.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**لماذا هذه الخطوة مطلوبة** – يتحقق خدمة Aspose من كل طلب مقابل اشتراكك. إنشاء العميل مرة واحدة يجنب عمليات المصافحة المتكررة ويحافظ على نظافة الكود.

## الخطوة 2: إنشاء مساعد OCR لملف PDF الممسوح ضوئياً

`AICopilotFactory` يبني مساعد OCR متخصص يعرف كيفية معالجة الملف الذي تحدده. تمرّر `client` وكائن `OpenAIOcrOptions` الذي يشير إلى مسار PDF.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Explanation** – `CreateOcrCopilot` يغلف جميع استدعاءات HTTP منخفضة المستوى. طريقة `WithDocument` تخبر الخدمة أي ملف يجب تحليله؛ يمكنك أيضاً تزويد `Stream` إذا كان PDF موجوداً في الذاكرة.

## الخطوة 3: استخراج النص المعترف به بشكل غير متزامن

استدعاء `GetTextAsync` يشغّل عملية OCR في السحابة ويعيد النتيجة كنص عادي. لأن العملية قد تستغرق بضع ثوانٍ، فإن الطريقة غير متزامنة.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Why asynchronous?** – زمن استجابة الشبكة ووقت معالجة OCR غير متوقعين. استخدام `await` يمنع تطبيقك من حجز الخيط الرئيسي، وهو أمر مهم خاصةً في سيناريوهات واجهة المستخدم أو خدمات الويب.

## الخطوة 4: استخدام النص المستخرج

في هذه المرحلة لديك `string` عادي من .NET يحتوي على النسخة الكاملة للـ PDF الممسوح. يمكنك كتابته إلى وحدة التحكم، تخزينه في قاعدة بيانات، أو إرساله إلى محرك بحث.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### النتيجة المتوقعة

إذا كان `Scanned.pdf` يحتوي على صفحة واحدة بالجملة “Hello, world!”، سيظهر في وحدة التحكم:

```
=== OCR Result ===
Hello, world!
```

بالنسبة للمستندات متعددة الصفحات، يتم دمج نص كل صفحة مع الحفاظ على فواصل الأسطر.

## مثال كامل قابل للتنفيذ

فيما يلي برنامج كامل يمكنك لصقه في مشروع وحدة تحكم جديد (`dotnet new console`). يوضح **how to use Aspose** من البداية إلى النهاية، بما في ذلك معالجة الأخطاء للمشكلات الشائعة.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**نقاط رئيسية في المثال**

* `await` يضمن تنفيذ غير محجوب.
* كتلة `try/catch` تُظهر أخطاء الشبكة أو الخدمة، وهو أمر أساسي عند **reading scanned PDF** على نطاق واسع.
* استبدل `YOUR_API_KEY` و `YOUR_DIRECTORY/Scanned.pdf` بالقيم الحقيقية قبل التشغيل.

## معالجة الحالات الخاصة ونصائح الممارسات المثلى

| الحالة | النهج الموصى به |
|-----------|----------------------|
| **ملفات PDF الكبيرة ( > 50 MB )** | قسّم المستند إلى أجزاء أصغر على جانب العميل وعالج كل جزء باستخدام copilot منفصل. هذا يقلل من ضغط الذاكرة ويحسن الاعتمادية. |
| **مسحات منخفضة الجودة** | قم بضبط جودة OCR بإضافة `.WithLanguage("eng")` أو `.WithEnhanceImage(true)` إلى `OpenAIOcrOptions`. الخدمة تدعم تلميحات اللغة التي تحسن الدقة. |
| **لغات متعددة** | قدّم قائمة مفصولة بفواصل، مثال `.WithLanguage("eng,spa")`. محرك OCR سيكتشف ويكتب كلا اللغتين. |
| **ملفات صور غير PDF** | حوّل الصورة إلى PDF أولاً (مكتبة `Aspose.Pdf`) أو استخدم `OpenAIOcrOptions.WithImage` لإرسال الصورة مباشرة. |
| **تجاوز حد المعدل** | نفّذ تأخيرًا أُسِيًا وإعادة المحاولة؛ API Aspose يُعيد HTTP 429 عندما تتجاوز الحصة. |

### نصيحة احترافية

قم بتخزين نتيجة `ocrText` مؤقتًا إذا كنت تخطط لإعادة استخدامها لاحقًا. عملية OCR هي الجزء الأكثر تكلفة في سير العمل، وإعادة استخدام السلسلة يتجنب استدعاءات API مكررة ويوفر الاعتمادات.

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات PDF المحمية بكلمة مرور؟**  
نعم. أضف `.WithPassword("yourPassword")` إلى مُنشئ الخيارات قبل إنشاء الـ copilot.

**س: هل يمكنني استخراج النص بتنسيق منظم (مثل JSON مع أرقام الصفحات)؟**  
استخدم `GetTextStructureAsync()` بدلاً من `GetTextAsync()`. تُعيد الطريقة حمولة JSON تشمل فهارس الصفحات، صناديق الحدود، ودرجات الثقة.

**س: ماذا لو كان PDF يحتوي على جداول؟**  
استخراج النص العادي يُسطّح الجداول إلى صفوف مفصولة بفواصل سطرية. للحصول على بيانات أغنى، اطلب تحويل PDF إلى HTML (`GetHtmlAsync`) وحلل عناصر جدول HTML.

## الخلاصة

أنت الآن تعرف **how to use Aspose** لقراءة PDF ممسوح، استخراج نص PDF الممسوح، و**convert PDF to text** ببرنامج C# بسيط. تتكون العملية من إنشاء مساعد OCR، استدعاء `GetTextAsync`، ومعالجة السلسلة الناتجة. باتباع توصيات الحالات الخاصة يمكنك توسيع الحل لتعامل مع دفعات مستندات كبيرة، محتوى متعدد اللغات، وملفات PDF مؤمنة.

بعد ذلك، قد ترغب في استكشاف:

* **كيفية استخراج النص** مع الحفاظ على التخطيط (`GetHtmlAsync`).
* استخدام Aspose.Pdf.AI **لاستخراج الجداول** وتصديرها إلى CSV.
* دمج مخرجات OCR مع Azure Cognitive Search لأرشفة مستندات قابلة للبحث.

برمجة سعيدة، واستمتع بالدقة التي يجلبها OCR المدعوم بالذكاء الاصطناعي من Aspose إلى سير عمل PDF الممسوح!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من ملفات PDF باستخدام Aspose.PDF لـ .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [كيفية استخراج النص من مناطق محددة في ملفات PDF باستخدام Aspose.PDF لـ .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [كيفية استخراج النص المميز من ملفات PDF باستخدام Aspose.PDF لـ .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}