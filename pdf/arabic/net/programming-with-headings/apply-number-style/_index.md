---
"description": "تعرف على كيفية تطبيق أنماط الأرقام المختلفة (الأرقام الرومانية والأبجدية) على العناوين في ملف PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل خطوة بخطوة."
"linktitle": "تطبيق نمط الأرقام في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تطبيق نمط الأرقام في ملف PDF"
"url": "/ar/net/programming-with-headings/apply-number-style/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق نمط الأرقام في ملف PDF

## مقدمة

هل سبق لك أن وجدت نفسك بحاجة إلى إضافة قوائم مرقمة بشكل جميل إلى مستندات PDF الخاصة بك؟ سواء كنت تُنسّق مستندات قانونية أو تقارير أو عروضًا تقديمية، فإن أنماط الترقيم الصحيحة ضرورية لتنظيم المعلومات. مع Aspose.PDF لـ .NET، يمكنك تطبيق أنماط ترقيم متنوعة على عناوين ملفات PDF، مما يُنشئ مستندات منظمة واحترافية. 

## المتطلبات الأساسية

قبل الغوص في البرمجة، دعنا نستعرض ما ستحتاج إليه:

1. Aspose.PDF لـ .NET: قم بتنزيل أحدث إصدار من Aspose.PDF من [هنا](https://releases.aspose.com/pdf/net/).
2. بيئة التطوير: تأكد من أن لديك Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة مع .NET.
3. .NET Framework: تأكد من تثبيت .NET Framework 4.0 أو أعلى.
4. الترخيص: يمكنك استخدام ترخيص مؤقت من [هنا](https://purchase.aspose.com/temporary-license/) أو استكشاف [نسخة تجريبية مجانية](https://releases.aspose.com/) خيارات.

## استيراد الحزم

للبدء، تأكد من استيراد مساحات الأسماء التالية في مشروعك:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## الخطوة 1: إعداد المستند

لنبدأ بإنشاء مستند PDF جديد وضبط إعدادات صفحاته. سنضبط حجم الصفحة والهوامش للتحكم في تصميم محتوانا.

التوضيح: في هذه الخطوة، نقوم بإعداد البنية الأساسية لملف PDF، والتي تتضمن تحديد حجم الصفحة والارتفاع والهوامش للحصول على تنسيق متسق.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDoc = new Document();

// تعيين أبعاد الصفحة والهوامش
pdfDoc.PageInfo.Width = 612.0;
pdfDoc.PageInfo.Height = 792.0;
pdfDoc.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfDoc.PageInfo.Margin.Left = 72;
pdfDoc.PageInfo.Margin.Right = 72;
pdfDoc.PageInfo.Margin.Top = 72;
pdfDoc.PageInfo.Margin.Bottom = 72;
```

من خلال القيام بذلك، سيكون مستندك له حجم صفحة قياسي، يعادل صفحة بحجم 8.5 × 11 بوصة، وهامش 72 نقطة (أو 1 بوصة) على جميع الجوانب.

## الخطوة 2: إضافة صفحة إلى ملف PDF

بعد ذلك، سنضيف صفحة جديدة إلى مستند PDF حيث سنطبق أنماط الترقيم لاحقًا.

شرح: كل ملف PDF يتطلب صفحات! هذه الخطوة تُضيف صفحة فارغة إلى ملف PDF وتُضبط هوامشها لتتوافق مع إعدادات مستوى المستند.

```csharp
// إضافة صفحة جديدة إلى مستند PDF
Aspose.Pdf.Page pdfPage = pdfDoc.Pages.Add();
pdfPage.PageInfo.Width = 612.0;
pdfPage.PageInfo.Height = 792.0;
pdfPage.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfPage.PageInfo.Margin.Left = 72;
pdfPage.PageInfo.Margin.Right = 72;
pdfPage.PageInfo.Margin.Top = 72;
pdfPage.PageInfo.Margin.Bottom = 72;
```

## الخطوة 3: إنشاء صندوق عائم

يتيح لك الصندوق العائم وضع محتوى (مثل النصوص أو العناوين) داخل مربع يعمل بشكل مستقل عن تدفق الصفحة. يُعد هذا مفيدًا عندما ترغب في التحكم الكامل في تصميم محتواك.

التوضيح: هنا، نقوم بإعداد FloatingBox ليحتوي على العناوين التي سيتم تطبيق أنماط الأرقام عليها.

```csharp
// إنشاء FloatingBox للمحتوى المنظم
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox();
floatBox.Margin = pdfPage.PageInfo.Margin;
pdfPage.Paragraphs.Add(floatBox);
```

## الخطوة 4: أضف العنوان الأول بالأرقام الرومانية

والآن يأتي الجزء المثير! لنُضِف العنوان الأول بترقيم رومانيّ صغير.

التوضيح: نقوم بتطبيق نمط NumberingStyle.NumeralsRomanLowercase على العنوان، والذي سيعرض الترقيم بالأرقام الرومانية (i، ii، iii، إلخ).

```csharp
// إنشاء العنوان الأول بالأرقام الرومانية
Aspose.Pdf.Heading heading = new Aspose.Pdf.Heading(1);
heading.IsInList = true;
heading.StartNumber = 1;
heading.Text = "List 1";
heading.Style = NumberingStyle.NumeralsRomanLowercase;
heading.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading);
```

## الخطوة 5: إضافة عنوان رقمي روماني ثانٍ

ولأغراض العرض التوضيحي، دعونا نضيف عنوانًا ثانيًا للأرقام الرومانية، ولكن هذه المرة سنبدأ من الرقم 13.

التوضيح: تسمح لك خاصية StartNumber ببدء الترقيم من رقم مخصص—في هذه الحالة، نبدأ من 13.

```csharp
// إنشاء عنوان ثانٍ يبدأ بالرقم الروماني 13
Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
heading2.IsInList = true;
heading2.StartNumber = 13;
heading2.Text = "List 2";
heading2.Style = NumberingStyle.NumeralsRomanLowercase;
heading2.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading2);
```

## الخطوة 6: إضافة عنوان مع ترقيم أبجدي

من أجل التنوع، دعونا نضيف عنوانًا ثالثًا، ولكن هذه المرة سنستخدم الترقيم الأبجدي بأحرف صغيرة (a، b، c، إلخ).

التوضيح: إن تغيير نمط الترقيم إلى أحرف صغيرة يسمح لنا بتطبيق الترقيم الأبجدي على عناويننا.

```csharp
// إنشاء عنوان بترقيم أبجدي
Aspose.Pdf.Heading heading3 = new Aspose.Pdf.Heading(2);
heading3.IsInList = true;
heading3.StartNumber = 1;
heading3.Text = "the value, as of the effective date of the plan, of property to be distributed under the plan on account of each allowed";
heading3.Style = NumberingStyle.LettersLowercase;
heading3.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading3);
```

## الخطوة 7: حفظ ملف PDF

أخيرًا، بعد تطبيق كافة العناوين وأنماط الأرقام، دعنا نحفظ ملف PDF في الدليل المطلوب.

التوضيح: هذه الخطوة تحفظ ملف PDF الذي يحتوي على كافة العناوين المنسقة مع أنماط الترقيم المطبقة.

```csharp
// حفظ مستند PDF
dataDir = dataDir + "ApplyNumberStyle_out.pdf";
pdfDoc.Save(dataDir);
Console.WriteLine("\nNumber style applied successfully in headings.\nFile saved at " + dataDir);
```

## خاتمة

ها قد انتهيت! لقد نجحت في تطبيق أنماط الترقيم - الأرقام الرومانية والأبجدية - على العناوين في ملف PDF باستخدام Aspose.PDF لـ .NET. تمنحك المرونة التي يوفرها Aspose.PDF للتحكم في تخطيط الصفحة وأنماط الترقيم وموضع المحتوى مجموعة أدوات فعّالة لإنشاء مستندات PDF منظمة واحترافية.

## الأسئلة الشائعة

### هل يمكنني تطبيق أنماط أرقام مختلفة على نفس مستند PDF؟  
نعم، يسمح لك Aspose.PDF لـ .NET بخلط أنماط الترقيم المختلفة مثل الأرقام الرومانية والأرقام العربية والترقيم الأبجدي داخل نفس المستند.

### كيف يمكنني تخصيص الرقم الأولي للعناوين؟  
يمكنك تعيين رقم البداية لأي عنوان باستخدام `StartNumber` ملكية.

### هل هناك طريقة لإعادة تعيين تسلسل الترقيم؟  
نعم، يمكنك إعادة تعيين الترقيم عن طريق ضبط `StartNumber` الخاصية لكل عنوان.

### هل يمكنني تطبيق تنسيق غامق أو مائل على العناوين بالإضافة إلى الترقيم؟  
بالتأكيد! يمكنك تخصيص أنماط العناوين بتعديل خصائص مثل الخط والحجم والخط العريض والمائل باستخدام `TextState` هدف.

### كيف أحصل على ترخيص مؤقت لـ Aspose.PDF؟  
يمكنك الحصول على ترخيص مؤقت من [هنا](https://purchase.aspose.com/temporary-license/) لاختبار Aspose.PDF دون قيود.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}