---
category: general
date: 2026-11-16
description: تحويل PDF إلى PDF/X‑1A وإضافة ملف تعريف ICC مخصص في C# باستخدام Aspose.PDF.
  اتبع هذا الدليل خطوة بخطوة للحصول على مخرجات طباعة موثوقة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert pdf to pdf/x-1a
- add icc profile
- set custom icc profile
language: ar
lastmod: 2026-11-16
og_description: تحويل PDF إلى PDF/X‑1A وتضمين ملف تعريف ICC مخصص في C#. يوضح هذا الدليل
  شفرة Aspose.PDF الكاملة ونصائح الممارسات المثلى.
og_image_alt: Screenshot of C# code that converts a PDF to PDF/X‑1A while attaching
  an ICC profile
og_title: تحويل PDF إلى PDF/X‑1A وإدراج ملف تعريف ICC مخصص في C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Convert PDF to PDF/X‑1A and add a custom ICC profile in C# using Aspose.PDF.
    Follow this step‑by‑step guide for reliable printing output.
  headline: Convert PDF to PDF/X‑1A and add a custom ICC profile in C#
  type: TechArticle
- description: Convert PDF to PDF/X‑1A and add a custom ICC profile in C# using Aspose.PDF.
    Follow this step‑by‑step guide for reliable printing output.
  name: Convert PDF to PDF/X‑1A and add a custom ICC profile in C#
  steps:
  - name: '**Set PDF/X‑1A conformance** – required for print‑ready files.'
    text: '**Set PDF/X‑1A conformance** – required for print‑ready files.'
  - name: '**Attach the custom ICC profile** – guarantees color fidelity.'
    text: '**Attach the custom ICC profile** – guarantees color fidelity.'
  - name: '**Choose how to reference the profile** – either by file name or via an
      `OutputIntent`.'
    text: '**Choose how to reference the profile** – either by file name or via an
      `OutputIntent`.'
  type: HowTo
tags:
- PDF conversion
- C#
- Aspose.PDF
title: تحويل PDF إلى PDF/X‑1A وإضافة ملف تعريف ICC مخصص في C#
url: /ar/net/printing-rendering/convert-pdf-to-pdf-x-1a-and-add-a-custom-icc-profile-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل PDF إلى PDF/X‑1A وإضافة ملف تعريف ICC مخصص في C#

إذا كنت بحاجة إلى **تحويل PDF إلى PDF/X‑1A**، يوضح لك هذا الدليل كيفية تضمين ملف تعريف ICC مخصص في الوقت نفسه. غالبًا ما تتطلب دور الطباعة التوافق مع PDF/X‑1A لأنه يضمن تعريف جميع الألوان بواسطة ملف تعريف ICC، مما يزيل المفاجآت أثناء الطباعة. ستتعلم الشيفرة الدقيقة **لإضافة ملف تعريف ICC** و **لتعيين ملف تعريف ICC مخصص** باستخدام Aspose.PDF for .NET، بالإضافة إلى نصائح لتجنب الأخطاء الشائعة.

يغطي الدرس كل شيء من تثبيت المكتبة إلى التحقق من صحة ملف PDF الناتج. لا تحتاج إلى أي وثائق خارجية—فقط انسخ البرنامج النهائي، عدل مسارات الملفات، وشغّله.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث (تعمل الشيفرة أيضًا مع .NET Framework 4.7+)
* Visual Studio 2022 (أو أي بيئة تطوير C#)
* ترخيص Aspose.PDF for .NET أو مفتاح تقييم مؤقت
* ملف PDF المصدر الذي تريد تحويله
* ملف تعريف ICC (مثال: `FOGRA39.icc`) يتوافق مع سير عمل الطباعة الخاص بك

يمكنك تثبيت Aspose.PDF عبر NuGet:

```bash
dotnet add package Aspose.Pdf
```

## الخطوة 1: تثبيت Aspose.PDF for .NET

توفر حزمة NuGet مساحة الاسم `Aspose.Pdf` والفئة `PdfFormatConversionOptions` التي سنستخدمها **لتحويل PDF إلى PDF/X‑1A**. بعد انتهاء الأمر، تظهر الحزمة في مراجع مشروعك.

> **نصيحة احترافية:** إذا كنت تستخدم ترخيص تجريبي، استدعِ `License license = new License(); license.SetLicense("Aspose.Pdf.lic");` في بداية `Main` لتجنب علامات مائية التقييم.

## الخطوة 2: تحميل PDF المصدر

حمّل ملف PDF الذي تريد تحويله. تقوم فئة `Document` بقراءة الملف إلى الذاكرة، جاهزة للتحويل.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class PdfX1AConverter
{
    static void Main()
    {
        // Path to the original PDF
        string sourcePdfPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

        // Load the PDF document
        Document pdfDocument = new Document(sourcePdfPath);
```

كائن `Document` يمثل ملف PDF بالكامل، بما في ذلك صفحاته، خطوطه، وموارده. الاحتفاظ بالمستند في الذاكرة يضمن تشغيل التحويل بسرعة.

## الخطوة 3: تكوين خيارات التحويل لتحويل PDF إلى PDF/X‑1A وإضافة ملف تعريف ICC

تقوم هذه الخطوة بثلاثة أشياء:

1. **تعيين توافق PDF/X‑1A** – مطلوب للملفات الجاهزة للطباعة.
2. **إرفاق ملف تعريف ICC المخصص** – يضمن دقة الألوان.
3. **اختيار طريقة الإشارة إلى الملف التعريفي** – إما بالاسم أو عبر كائن `OutputIntent`.

```csharp
        // -----------------------------------------------------------------
        // 3.1 Create conversion options and request PDF/X‑1A conformance
        // -----------------------------------------------------------------
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions
        {
            // Enforce PDF/X‑1A:2001 compliance
            PdfXConformance = PdfXConformance.PdfX1A2001
        };

        // -----------------------------------------------------------------
        // 3.2 Path to the ICC profile you want to embed
        // -----------------------------------------------------------------
        string iccProfilePath = Path.Combine("YOUR_DIRECTORY", "FOGRA39.icc");

        // -----------------------------------------------------------------
        // 3.3 Option A – set the profile file name directly (simplest)
        // -----------------------------------------------------------------
        conversionOptions.IccProfileFileName = iccProfilePath;

        // -----------------------------------------------------------------
        // 3.4 Option B – set the profile via an OutputIntent (more control)
        // -----------------------------------------------------------------
        OutputIntent outputIntent = new OutputIntent
        {
            DestinationOutputProfile = new FileStreamSource(iccProfilePath)
        };
        conversionOptions.OutputIntents = new[] { outputIntent };

        // You can use either Option A or Option B. Both effectively
        // **set custom ICC profile** for the PDF/X‑1A output.
```

**لماذا نحدد ملف تعريف ICC:** يتطلب PDF/X‑1A وجود نية إخراج واحدة تحدد مساحة اللون. من خلال إرفاق `FOGRA39.icc`، تخبر الأجهزة اللاحقة بالضبط كيفية تفسير الألوان.

**الاختيار بين الخيار A و B:**  
*الخيار A* مختصر ويعمل في معظم السيناريوهات.  
*الخيار B* يمنحك الوصول إلى كائن `OutputIntent` الكامل، مما يسمح لك بإضافة بيانات وصفية إضافية (مثل قاموس `Info`) إذا لزم الأمر.

## الخطوة 4: تنفيذ التحويل والتحقق من النتيجة

الآن شغّل التحويل واكتب ملف PDF/X‑1A إلى القرص.

```csharp
        // -----------------------------------------------------------------
        // 4.1 Destination path for the PDF/X‑1A file
        // -----------------------------------------------------------------
        string outputPdfPath = Path.Combine("YOUR_DIRECTORY", "output_pdfx1.pdf");

        // -----------------------------------------------------------------
        // 4.2 Convert and save
        // -----------------------------------------------------------------
        pdfDocument.Convert(conversionOptions, outputPdfPath);

        Console.WriteLine($"PDF/X‑1A file saved to: {outputPdfPath}");
    }
}
```

عند انتهاء `Convert`، يكون `output_pdfx1.pdf` متوافقًا مع معيار PDF/X‑1A:2001 ويحتوي على ملف تعريف ICC المدمج. يمكنك التحقق من التوافق باستخدام أدوات مثل **veraPDF** أو **Adobe Acrobat Preflight**.

> **نصيحة احترافية:** شغّل `veraPDF` من سطر الأوامر بعد التحويل:  
> `verapdf --format text output_pdfx1.pdf` – سيعرض أي انتهاكات للتوافق.

## الأخطاء الشائعة وأفضل الممارسات

| المشكلة | لماذا يحدث | كيفية تجنبه |
|-------|----------------|-----------------|
| **ملف ICC مفقود** | `FileNotFoundException` عندما يكون المسار غير صحيح | استخدم `Path.Combine` وتحقق من وجود الملف بـ `File.Exists` قبل الإسناد |
| **مساحة لون غير صحيحة** | يستخدم PDF المصدر CMYK بينما ملف ICC هو RGB | اختر ملف تعريف ICC يتطابق مع مساحة لون المصدر، أو حوّل الألوان قبل الإرفاق |
| **عدم توافق إصدار PDF** | يتطلب PDF/X‑1A PDF 1.3؛ قد تحتوي ملفات PDF الأحدث على ميزات غير مدعومة | Aspose.PDF يقوم بخفض الإصدار تلقائيًا، لكن يمكنك تعيين `PdfVersion` في `PdfFormatConversionOptions` إذا لزم الأمر |
| **عدم تطبيق الترخيص** | تظهر علامات مائية تقييمية في الناتج | حمّل ملف الترخيص في بداية `Main` |

### حالة خاصة: تحويل PDF يحتوي بالفعل على ملف تعريف ICC

إذا كان PDF المصدر يحتوي بالفعل على نية إخراج، فإن Aspose.PDF يستبدلها بالتي تقدمها. هذا عادةً ما يكون مرغوبًا في إنتاج الطباعة، ولكن إذا كنت بحاجة للحفاظ على النية الأصلية، اقرأ مجموعة `Document.OutputIntents` أولاً وادمج حسب الحاجة.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك لصقه في مشروع وحدة تحكم جديد. استبدل `YOUR_DIRECTORY` بالمجلد الفعلي الذي يحتوي على `input.pdf` و `FOGRA39.icc`.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إدراج ملف تعريف ICC وتحويل PDF إلى PDF/X-1 باستخدام Aspose.Pdf](/pdf/english/net/document-conversion/how-to-embed-icc-profile-and-convert-pdf-to-pdf-x-1-with-asp/)
- [تعيين ملف تعريف ICC في تحويل PDF/X‑1A – دليل C# كامل](/pdf/english/net/document-conversion/set-icc-profile-in-pdf-x-1a-conversion-complete-c-guide/)
- [إضافة ملف تعريف ICC وتحويل PDF إلى PDF/X‑4 – دليل C#](/pdf/english/net/document-conversion/add-icc-profile-and-convert-pdf-to-pdf-x-4-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}