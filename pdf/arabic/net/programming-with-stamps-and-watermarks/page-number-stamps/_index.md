---
"description": "تعرف على كيفية إضافة طوابع أرقام الصفحات إلى ملفات PDF باستخدام Aspose.PDF لـ .NET من خلال دليلنا السهل المتابعة، والذي يتضمن مثالاً للكود."
"linktitle": "طوابع أرقام الصفحات في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "طوابع أرقام الصفحات في ملف PDF"
"url": "/ar/net/programming-with-stamps-and-watermarks/page-number-stamps/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# طوابع أرقام الصفحات في ملف PDF

## مقدمة

هل سبق لك أن وجدت نفسك تواجه صعوبة في التعامل مع مستند PDF، متمنيًا لو كان يحتوي على أرقام صفحات لتسهيل التنقل؟ سواء كنت طالبًا تُشارك ملاحظاتك، أو محترفًا تُقدم تقاريرك، أو أي شخص يُدير مستندات متعددة الصفحات، فإن إضافة أرقام الصفحات تُحسّن وضوح ملفات PDF. لحسن الحظ، مع مكتبة Aspose.PDF for .NET القوية، يُمكنك إضافة علامات أرقام الصفحات إلى مستندات PDF بسهولة. في هذا الدليل، سنشرح لك العملية خطوة بخطوة، ونضمن لك امتلاك جميع المعلومات اللازمة. هيا بنا!

## المتطلبات الأساسية

قبل أن نبدأ في إضافة طوابع أرقام الصفحات إلى مستندات PDF الخاصة بك، تأكد من توفر المتطلبات الأساسية التالية:

1. Visual Studio: تأكد من تثبيت Visual Studio على نظامك. ستكتب وتنفذ شفرتك البرمجية هنا.
2. .NET Framework: تعتبر المعرفة ببرمجة C# وإطار عمل .NET أمرًا ضروريًا نظرًا لأن Aspose.PDF مصمم لتطبيقات .NET.
3. مكتبة Aspose.PDF: يمكنك تنزيل مكتبة Aspose.PDF من [إصدارات Aspose PDF](https://releases.aspose.com/pdf/net/). 
4. الفهم الأساسي لملفات PDF: على الرغم من أنك لست بحاجة إلى أن تكون خبيرًا، فإن الفهم الأساسي لكيفية عمل ملفات PDF سيساعدك على فهم البرنامج التعليمي بشكل أفضل.

بمجرد إعداد هذه المتطلبات الأساسية، ستكون جاهزًا لبدء ختم أرقام الصفحات تلك!

## استيراد الحزم

قبل البدء بالبرمجة، تأكد من استيراد حزم Aspose.PDF اللازمة إلى مشروعك. هذا ضروري للاستفادة من وظائف المكتبة بسلاسة. إليك كيفية القيام بذلك:

### إنشاء مشروع جديد

1. افتح Visual Studio.
2. انقر على `File` > `New` > `Project`.
3. حدد قالبًا مناسبًا لـ C# (على سبيل المثال، تطبيق وحدة التحكم)، وقم بتسميته، ثم انقر فوق `Create`.

### إضافة مرجع Aspose.PDF

1. انقر بزر الماوس الأيمن على اسم المشروع في مستكشف الحلول.
2. انقر على `Manage NuGet Packages`.
3. بحث عن `Aspose.PDF` وتثبيت الإصدار الأحدث.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

مع المكتبة جاهزة للانطلاق، دعنا ننتقل إلى الترميز!

بعد إعداد بيئتنا، حان وقت إضافة علامات ترقيم الصفحات إلى ملف PDF. سنُقسّم هذه العملية إلى خطوات واضحة لتسهيل الفهم.

## الخطوة 1: تحديد دليل المستندات

للبدء، عليك تحديد المجلد الذي يحتوي على ملف PDF. هذه هي نقطة انطلاق مشروعك.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // تحديث هذا المسار
```

شرح: استبدال `"YOUR DOCUMENT DIRECTORY"` مع المسار المؤدي إلى المجلد الذي يحتوي على ملف PDF. هذا مهم لأنه يُرشد الكود الخاص بك إلى مكان الملف الذي تريد تعديله.

## الخطوة 2: افتح المستند

بعد ذلك، سنفتح مستند PDF الموجود الذي نريد إضافة طوابع أرقام الصفحات إليه.

```csharp
Document pdfDocument = new Document(dataDir + "PageNumberStamp.pdf");
```

التوضيح: هنا، نحن نستخدم `Document` الفئة التي يوفرها Aspose.PDF لفتح ملف PDF الخاص بنا. تأكد من تطابق اسم الملف مع اسم الملف الموجود في مجلدك.

## الخطوة 3: إنشاء ختم رقم الصفحة

الآن يأتي الجزء الممتع! لنُنشئ ختمًا لرقم الصفحة لإضافته إلى ملف PDF.

```csharp
PageNumberStamp pageNumberStamp = new PageNumberStamp();
```

الشرح: `PageNumberStamp` ستسمح لنا الفئة بإنشاء طابع يعرض رقم الصفحة الحالية بالنسبة إلى العدد الإجمالي للصفحات في المستند.

## الخطوة 4: تكوين الختم

الآن، ستحتاج إلى ضبط إعدادات طابعك. هنا يمكنك تصميم شكل وسلوك الطابع.

```csharp
pageNumberStamp.Background = false;
pageNumberStamp.Format = "Page # of " + pdfDocument.Pages.Count;
pageNumberStamp.BottomMargin = 10;
pageNumberStamp.HorizontalAlignment = HorizontalAlignment.Center;
pageNumberStamp.StartingNumber = 1;
```

توضيح:
- `Background = false`:هذا يعني أن الختم سيظهر في المقدمة.
- `Format`:هنا، يمكنك تعيين التنسيق لإظهار "الصفحة X من Y"، حيث يمكنك جلب إجمالي الصفحات في المستند بشكل ديناميكي.
- `BottomMargin`:ضبط المسافة من أسفل الصفحة.
- `HorizontalAlignment`:مركز الختم أفقيًا.
- `StartingNumber`:يحدد رقم الصفحة الأولية، عادةً من 1.

## الخطوة 5: تعيين خصائص النص

بعد ذلك، يمكنك تخصيص كيفية ظهور النص في الختم.

```csharp
pageNumberStamp.TextState.Font = FontRepository.FindFont("Arial");
pageNumberStamp.TextState.FontSize = 14.0F;
pageNumberStamp.TextState.FontStyle = FontStyles.Bold;
pageNumberStamp.TextState.FontStyle = FontStyles.Italic;
pageNumberStamp.TextState.ForegroundColor = Color.Aqua;
```

التوضيح: تعمل هذه السمات على تكوين نوع الخط وحجمه ونمطه (غامق ومائل) ولون النص داخل الختم لجعله جذابًا بصريًا.

## الخطوة 6: إضافة الختم إلى صفحة محددة

بعد تكوين طابعتك، حان الوقت لإضافتها إلى صفحة معينة في مستندك.

```csharp
pdfDocument.Pages[1].AddStamp(pageNumberStamp);
```

شرح: يُضيف هذا السطر الطابع إلى الصفحة الأولى من ملف PDF. يمكنك تعديل `Pages[1]` فهرس للصفحات الأخرى حسب الضرورة.

## الخطوة 7: حفظ المستند الناتج

وأخيرًا، احفظ مستند PDF المعدّل حتى تصبح التغييرات دائمة.

```csharp
dataDir = dataDir + "PageNumberStamp_out.pdf";
pdfDocument.Save(dataDir);
Console.WriteLine("\nPage number stamp added successfully.\nFile saved at " + dataDir);
```

توضيح: أنت تُحدِّد مسار ملف الإخراج وتحفظ المستند. ستُعلِمك وحدة التحكم بإضافة الطابع بنجاح ومكان حفظ الملف.

## خاتمة

إضافة علامات ترقيم الصفحات إلى ملفات PDF باستخدام Aspose.PDF لـ .NET ليست سهلة فحسب، بل قابلة للتخصيص بدرجة كبيرة. لقد شرحنا لك عملية إنشاء علامة ترقيم الصفحات خطوة بخطوة، لضمان حصولك على إرشادات واضحة طوال العملية. أنت الآن تمتلك المعرفة اللازمة لتحسين مستندات PDF الخاصة بك، وجعلها أكثر سهولة في الاستخدام واحترافية. 

## الأسئلة الشائعة

### هل يمكنني تخصيص مظهر أرقام الصفحات؟  
نعم! يمكنك تغيير الخط والحجم واللون وتنسيق أرقام الصفحات كما هو موضح في الدليل.

### هل استخدام Aspose.PDF مجاني؟  
يقدم Aspose.PDF نسخة تجريبية مجانية، ولكنك ستحتاج إلى ترخيص للاستخدام المكثف. اطلع على [صفحة الشراء](https://purchase.aspose.com/buy) لمزيد من المعلومات.

### ماذا لو واجهت مشاكل أثناء التنفيذ؟  
يمكنك زيارة [منتدى دعم Aspose](https://forum.aspose.com/c/pdf/10) للحصول على المساعدة.

### كيف يمكنني إنشاء أرقام الصفحات تلقائيًا لصفحات متعددة؟  
يقوم كود الدليل تلقائيًا بحساب العدد الإجمالي للصفحات، مما يجعل التخصيص للصفحات المتعددة أمرًا سهلاً.

### هل يمكنني استخدام Aspose.PDF في لغات برمجة أخرى؟  
في حين يركز هذا الدليل على .NET، فإن Aspose لديه مكتبات لـ Java وPython والمزيد.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}