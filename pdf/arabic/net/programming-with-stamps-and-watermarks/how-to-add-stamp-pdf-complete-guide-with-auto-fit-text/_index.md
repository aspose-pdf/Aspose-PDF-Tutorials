---
category: general
date: 2026-06-30
description: كيفية إضافة ختم PDF باستخدام Aspose.PDF وتعديل النص تلقائيًا ليتناسب
  مع PDF. دليل خطوة بخطوة مع الكود الكامل، الشروحات، والنصائح.
draft: false
keywords:
- how to add stamp pdf
- adjust font size to fit
- auto‑fit text in pdf
language: ar
og_description: كيفية إضافة ختم PDF بسهولة. تعلم تعديل حجم الخط ليتناسب وضبط النص
  تلقائيًا في PDF باستخدام Aspose.PDF في دقائق.
og_title: كيفية إضافة ختم PDF – دليل النص المتناسب تلقائيًا
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to add stamp pdf using Aspose.PDF and auto‑fit text in pdf. Step‑by‑step
    tutorial with full code, explanations, and tips.
  headline: How to add stamp pdf – Complete guide with auto‑fit text
  type: TechArticle
- description: How to add stamp pdf using Aspose.PDF and auto‑fit text in pdf. Step‑by‑step
    tutorial with full code, explanations, and tips.
  name: How to add stamp pdf – Complete guide with auto‑fit text
  steps:
  - name: Expected Output
    text: Open `autoFontStamp.pdf` in any PDF viewer. You should see a rectangular
      label on the first page, **exactly 300 × 100 points**, containing the phrase
      “Long text that must fit”. If the original string is longer than the rectangle
      can accommodate at the default font size, you’ll notice the text has sh
  - name: 1. Multiple Stamps on One Page
    text: If you need several annotations, simply repeat the `AddStamp` call with
      different `TextStamp` instances. Remember to adjust `XIndent` and `YIndent`
      to position each stamp.
  - name: 2. Changing Font Family or Color
    text: 'You can customize the appearance via the `TextState` property:'
  - name: 3. Using Images Instead of Text
    text: Aspose also supports `ImageStamp`. The same auto‑fit logic doesn’t apply,
      but you can manually size the image to the stamp rectangle.
  type: HowTo
tags:
- pdf
- aspnet
- stamp
- font-size
title: كيفية إضافة ختم PDF – دليل كامل مع ضبط النص تلقائيًا
url: /ar/net/programming-with-stamps-and-watermarks/how-to-add-stamp-pdf-complete-guide-with-auto-fit-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة ختم PDF – دليل كامل مع النص المتكيف تلقائيًا

إن سؤال "كيفية إضافة ختم PDF" يتكرر كثيرًا كلما احتجت إلى توضيح مستند دون فتح محرر رسومي. هل جربت وضع تسمية طويلة على صفحة PDF ولاحظت أنها تمتد خارج الحدود؟ في هذا الدرس سنحل هذه المشكلة باستخدام **Aspose.PDF for .NET** وسنوضح لك كيفية **ضبط حجم الخط ليتناسب** تلقائيًا.

سنستعرض كل سطر من الشيفرة، نشرح لماذا كل إعداد مهم، وسننتهي بملف PDF يعمل بالكامل يثبت أن الختم يتقلص (أو يتوسع) للبقاء داخل مستطيله. لا إشارات غامضة—حل عملي يمكنك نسخه ولصقه وتشغيله اليوم.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

* **.NET 6.0** أو أحدث (تعمل الشيفرة أيضًا على .NET Framework 4.7+).  
* حزمة **Aspose.Pdf** من NuGet (`Install-Package Aspose.Pdf`).  
* ملف PDF اسمه `input.pdf` موجود في مجلد يمكنك الإشارة إليه (سنسميه `YOUR_DIRECTORY`).  
* أي بيئة تطوير تفضلها—Visual Studio، Rider، أو حتى VS Code.

هذا كل شيء. لا خدمات خارجية، ولا حيل ترخيص (Aspose يقدم مفتاح تجربة مجاني يمكنك تضمينه للاختبار). جاهز؟ لنبدأ.

## كيفية إضافة ختم PDF – الخطوة 1: تحميل المستند المصدر

أول شيء يجب فعله هو فتح ملف PDF الذي تريد تعديلّه. تتعامل Aspose.PDF مع الملف ككائن `Document`، مما يمنحك الوصول إلى الصفحات، التعليقات، وبالطبع الختم.

```csharp
using Aspose.Pdf;

// Step 1: Open the source PDF document
using (var document = new Document(@"YOUR_DIRECTORY\input.pdf"))
{
    // The using‑statement ensures the file is closed properly.
```

> **لماذا هذا مهم:**  
> فتح المستند داخل كتلة `using` يضمن تحرير جميع مقبضات الملفات، مما يمنع أخطاء “الملف مقفل” عندما تحاول حفظ أو حذف الـ PDF لاحقًا.

## ضبط حجم الخط ليتناسب – تكوين TextStamp

الآن ننشئ كائن `TextStamp`. هذا هو العنصر الذي سيظهر فعليًا على الصفحة. يحدث السحر عندما نفعّل **AutoAdjustFontSizeToFitStampRectangle** ونحدد قيمة الدقة.

```csharp
    // Step 2: Create a text stamp and enable automatic font size adjustment
    var stamp = new TextStamp("Long text that must fit")
    {
        // Shrink or expand text to fit the stamp area automatically
        AutoAdjustFontSizeToFitStampRectangle = true,

        // Precision for the size calculation (0.01 = 1% tolerance)
        AutoAdjustFontSizePrecision = 0.01f,

        // Define the rectangle that the stamp must stay inside
        Width = 300,   // points (approx 4.2 inches)
        Height = 100,  // points (approx 1.4 inches)

        // Keep the original text scaling; we only want font size to change
        Scale = false
    };
```

> **نصيحة محترف:** إذا كنت تتعامل مع نص متعدد اللغات، اضبط أيضًا `stamp.TextState.Font = FontRepository.FindFont("Arial Unicode MS");` لتجنب مشاكل الأحرف المفقودة.

> **لماذا يعمل هذا:**  
> `AutoAdjustFontSizeToFitStampRectangle` يخبر Aspose بحساب أكبر حجم خط ممكن لا يزال يتناسب داخل المستطيل المحدد بـ `Width` و `Height`. تتحكم `AutoAdjustFontSizePrecision` في دقة هذا الحساب—الأرقام الأصغر تعني توافق أكثر إحكامًا لكن مع زمن معالجة أطول قليلًا.

## النص المتكيف تلقائيًا في PDF – إضافة الختم إلى صفحة

بعد تكوين الختم، الخطوة التالية هي وضعه على صفحة محددة. في هذا المثال سنستخدم الصفحة الأولى، لكن يمكنك استهداف أي فهرس (`document.Pages[3]` للصفحة الثالثة، على سبيل المثال).

```csharp
    // Step 3: Add the stamp to the first page of the PDF
    document.Pages[1].AddStamp(stamp);
```

> **سؤال شائع:** *ماذا لو كان الـ PDF لا يحتوي على صفحات؟*  
> ستطرح Aspose استثناء `ArgumentOutOfRangeException`. إضافة شرط حماية سريع (`if (document.Pages.Count == 0) throw new InvalidOperationException("PDF is empty.");`) يجعل الشيفرة أكثر صلابة.

## حفظ PDF – التحقق من النتيجة

أخيرًا، نكتب التغييرات إلى القرص. اسم ملف الإخراج يوضح أن حجم خط الختم تم ضبطه تلقائيًا.

```csharp
    // Step 4: Save the modified PDF with the auto‑adjusted stamp
    document.Save(@"YOUR_DIRECTORY\autoFontStamp.pdf");
} // End of using block – document is disposed here
```

### النتيجة المتوقعة

افتح `autoFontStamp.pdf` في أي عارض PDF. يجب أن ترى تسمية مستطيلة على الصفحة الأولى، **بأبعاد 300 × 100 نقطة** بالضبط، تحتوي على العبارة “Long text that must fit”. إذا كان النص الأصلي أطول من المستطيل عند حجم الخط الافتراضي، ستلاحظ أن النص قد تقلص بما يكفي للبقاء داخل المستطيل—بدون قطع، بدون تجاوز.

![Screenshot of PDF with auto‑fit stamp](https://example.com/auto-fit-stamp.png "auto‑fit text in pdf example")  
*نص بديل: لقطة شاشة لملف PDF مع ختم متكيف تلقائيًا يظهر حجم الخط المعدل.*

## الحالات الخاصة والاختلافات

### 1. عدة أختام على صفحة واحدة

إذا كنت بحاجة إلى عدة تعليقات، ببساطة كرّر استدعاء `AddStamp` مع كائنات `TextStamp` مختلفة. تذكّر تعديل `XIndent` و `YIndent` لتحديد موضع كل ختم.

```csharp
stamp.XIndent = 50;   // horizontal offset from the left edge
stamp.YIndent = 150;  // vertical offset from the bottom edge
document.Pages[1].AddStamp(stamp);
```

### 2. تغيير عائلة الخط أو اللون

يمكنك تخصيص المظهر عبر خاصية `TextState`:

```csharp
stamp.TextState.Font = FontRepository.FindFont("Times New Roman");
stamp.TextState.FontSize = 12; // base size; auto‑adjust will override if needed
stamp.TextState.ForegroundColor = Color.FromRgb(255, 0, 0); // red text
```

### 3. استخدام صور بدلاً من النص

تدعم Aspose أيضًا `ImageStamp`. لا ينطبق منطق التكيف التلقائي هنا، لكن يمكنك ضبط حجم الصورة يدويًا لتتناسب مع مستطيل الختم.

```csharp
var imgStamp = new ImageStamp(@"YOUR_DIRECTORY\logo.png")
{
    Width = 200,
    Height = 80,
    XIndent = 20,
    YIndent = 20
};
document.Pages[1].AddStamp(imgStamp);
```

## نصائح عملية من الميدان

* **لا تُثبّت المسارات صراحةً** – استخدم `Path.Combine(Environment.CurrentDirectory, "input.pdf")` للقدرة على النقل.  
* **المعالجة الدفعية** – غلف الروتين بالكامل داخل حلقة `foreach (var file in Directory.GetFiles(...))` لختم عشرات ملفات PDF تلقائيًا.  
* **الأداء** – إذا كنت تعالج ملفات PDF كبيرة، فكر في تعطيل `AutoAdjustFontSizePrecision` (اجعلها `0.05f`) لتسريع الحساب مع فرق بصري ضئيل.  
* **الاختبار** – دائمًا افتح ملف PDF الناتج بعد أول تشغيل لتتأكد من أن أبعاد المستطيل هي ما تتوقعه. فحص بصري سريع يوفر ساعات من التصحيح لاحقًا.

## الخلاصة

أصبح لديك الآن حل كامل، قابل للنسخ واللصق، لـ **كيفية إضافة ختم PDF** مع **ضبط حجم الخط تلقائيًا ليتناسب** وتحقيق **النص المتكيف تلقائيًا في PDF** باستخدام Aspose.PDF. من خلال تحميل المستند، تكوين `TextStamp` مع تمكين الضبط التلقائي، وضعه على الصفحة المطلوبة، وحفظ الملف، يمكنك توضيح ملفات PDF برمجيًا دون القلق بشأن تجاوز النص.

ما الخطوة التالية؟ جرّب دمج هذه التقنية مع سير عمل يعتمد على البيانات—اسحب أسماء العملاء من قاعدة بيانات وضع ختمًا على كل فاتورة داخل حلقة. أو جرّب أحجام مستطيلات مختلفة لترى كيف يتصرف خوارزمية التكيف مع سلاسل نصية قصيرة جدًا أو طويلة جدًا.

هل لديك تعديل ترغب في مشاركته؟ اترك تعليقًا، أو أنشئ مشروعًا جديدًا ودع سحر التكيف التلقائي يقوم بعمله. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Add a Text Stamp to PDFs Using Aspose.PDF for .NET](/pdf/english/net/document-manipulation/add-text-stamp-pdf-aspose-dotnet/)
- [How to Add and Align Text Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}