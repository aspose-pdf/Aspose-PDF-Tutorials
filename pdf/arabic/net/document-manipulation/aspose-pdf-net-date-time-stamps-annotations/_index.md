---
"date": "2025-04-11"
"description": "تعرّف على كيفية إضافة التاريخ والوقت أو التعليقات التوضيحية بكفاءة إلى مستندات PDF باستخدام Aspose.PDF لـ .NET. حسّن إدارة مستنداتك باتباع هذه الخطوات السهلة."
"title": "إضافة طوابع التاريخ والوقت إلى ملفات PDF باستخدام Aspose.PDF لـ .NET"
"url": "/ar/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# إضافة طوابع التاريخ والوقت إلى ملفات PDF باستخدام Aspose.PDF لـ .NET

## مقدمة

في عصرنا الرقمي، تُعدّ إدارة المستندات الفعّالة أمرًا بالغ الأهمية للشركات والأفراد. إضافة التاريخ والوقت أو التعليقات التوضيحية إلى ملفات PDF تُحسّن سلامة البيانات وتنظيمها. يوضح هذا البرنامج التعليمي كيفية دمج هذه الميزات باستخدام Aspose.PDF لـ .NET.

**النقاط الرئيسية:**
- أضف التاريخ والوقت الحاليين كطوابع نصية على صفحة PDF محددة.
- إنشاء تعليقات نصية مجانية في المواقع المطلوبة في المستند.
- اتبع أفضل الممارسات للحصول على الأداء الأمثل مع Aspose.PDF لـ .NET.

## المتطلبات الأساسية
قبل البدء، تأكد من أن لديك:

### المكتبات والإصدارات المطلوبة
- **Aspose.PDF لـ .NET**: مكتبة قوية لمعالجة ملفات PDF دون الحاجة إلى Adobe Acrobat. استخدم الإصدار 21.x أو أحدث.

### متطلبات إعداد البيئة
- بيئة تطوير مع .NET Framework 4.5+ أو .NET Core 2.0+
- Visual Studio أو أي بيئة تطوير متكاملة أخرى تدعم برمجة C#

### متطلبات المعرفة
- فهم أساسي لهياكل مشاريع C# و.NET
- المعرفة بكيفية التعامل مع الملفات في بنية الدليل

## إعداد Aspose.PDF لـ .NET
قم بتثبيت Aspose.PDF باستخدام إحدى الطرق التالية:

**استخدام .NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**استخدام مدير الحزم:**
```powershell
Install-Package Aspose.PDF
```

**عبر واجهة مستخدم NuGet Package Manager:**
- افتح مدير الحزم NuGet في IDE الخاص بك.
- ابحث عن "Aspose.PDF" وقم بتثبيت الإصدار الأحدث.

### خطوات الحصول على الترخيص
للاستفادة الكاملة من Aspose.PDF:
1. **نسخة تجريبية مجانية:** قم بتنزيل ترخيص مؤقت لاستكشاف كافة الميزات.
2. **رخصة مؤقتة:** اطلب ترخيص تقييم موسع إذا لزم الأمر.
3. **شراء:** قم بشراء ترخيص للاستخدام طويل الأمد من موقع Aspose.

قم بتهيئة الترخيص الخاص بك في الكود:
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## دليل التنفيذ
دعونا نضيف طوابع التاريخ والوقت إلى ملفات PDF.

### الميزة 1: إضافة ختم التاريخ والوقت إلى ملف PDF
تضيف هذه الميزة التاريخ والوقت الحاليين كختم نصي على الصفحة الأولى من مستند PDF محدد.

#### التنفيذ خطوة بخطوة

##### 1. افتح مستند PDF الموجود
قم بتحميل المستند المستهدف:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. الحصول على التاريخ والوقت الحاليين كسلسلة
تنسيق التاريخ والوقت الحاليين:
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. إنشاء ختم نصي بالتاريخ والوقت الحاليين
إنشاء `TextStamp` مثال باستخدام السلسلة المنسقة:
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. إضافة ختم النص إلى الصفحة الأولى
أضف الختم إلى الصفحة الأولى من مستندك:
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5. إنشاء وإضافة FreeTextAnnotation (اختياري)
للحصول على تعليقات توضيحية أكثر تعقيدًا، قم بإنشاء `FreeTextAnnotation`:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6. احفظ المستند المعدّل
احفظ التغييرات الخاصة بك:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### الميزة 2: إضافة تعليقات توضيحية مجانية إلى ملف PDF
أضف تعليقات نصية مجانية في أي مكان تريده داخل مستند PDF.

#### التنفيذ خطوة بخطوة

##### 1. افتح مستند PDF موجود
قم بتحميل المستند المستهدف:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. حدد منطقة المستطيل للتعليق التوضيحي
حدد مكان وضع التعليق التوضيحي على الصفحة:
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. إنشاء FreeTextAnnotation بمظهر وموقع محددين
قم بتهيئة التعليق التوضيحي الخاص بك باستخدام النص المطلوب وإعدادات المظهر:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. تعيين نمط الحدود وإضافة التعليقات التوضيحية
تأكد من أن نمط الحدود يطابق احتياجاتك (غير مرئي في هذه الحالة):
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5. احفظ المستند المعدّل
احفظ مستندك بالتعليق التوضيحي المضاف حديثًا:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## التطبيقات العملية
إن إضافة طوابع التاريخ والتعليقات التوضيحية إلى ملفات PDF أمر مفيد في مختلف الصناعات:
- **الوثائق القانونية**:يضمن الامتثال من خلال وضع علامة زمنية على التغييرات.
- **الأوراق الأكاديمية**:يسهل التحرير التعاوني باستخدام التعليقات التوضيحية.
- **السجلات المالية**:يحافظ على مسارات التدقيق الدقيقة مع التقارير المختومة بالوقت.
- **الوثائق الفنية**:يسلط الضوء على التحديثات أو الملاحظات المهمة في الأدلة.

## اعتبارات الأداء
للحصول على الأداء الأمثل عند استخدام Aspose.PDF لـ .NET:
- **معالجة الدفعات**:قم بمعالجة ملفات PDF متعددة على دفعات لتقليل التكلفة.
- **إدارة الذاكرة**: يستخدم `Dispose` طرق لتحرير موارد الذاكرة بعد معالجة كل مستند.
- **الخطوط والصور المُحسّنة**:قم بتحديد أنواع الخطوط ودقة الصور لتقليل حجم الملف.

## خاتمة
يتيح لك دمج Aspose.PDF لـ .NET إضافة ميزات ختم التاريخ والتعليق التوضيحي إلى مستندات PDF، مما يُحسّن وظائفها. تُحسّن هذه الأدوات سلامة البيانات وتُبسّط إدارة المستندات.

قم بتجربة تكوينات مختلفة واستكشف الميزات الإضافية التي يوفرها Aspose.PDF لتلبية احتياجاتك المحددة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}