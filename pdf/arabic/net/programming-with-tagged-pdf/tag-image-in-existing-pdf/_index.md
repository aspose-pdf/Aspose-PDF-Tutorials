---
"description": "تعرّف على كيفية وضع علامات على الصور في ملفات PDF الحالية باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة لتحسين إمكانية الوصول مع التوافق مع PDF/UA."
"linktitle": "وضع علامة على الصورة في ملف PDF الموجود"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "وضع علامة على الصورة في ملف PDF الموجود"
"url": "/ar/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# وضع علامة على الصورة في ملف PDF الموجود

## مقدمة

في هذا البرنامج التعليمي، سنشرح لك كيفية إضافة وسم إلى صورة في ملف PDF موجود باستخدام Aspose.PDF لـ .NET. بنهاية هذا الدليل، ستتمكن من تعيين نص بديل للصور، وتعديل سمات التخطيط، وضمان توافق ملف PDF مع معايير إمكانية الوصول.

## المتطلبات الأساسية

قبل أن نبدأ، دعنا نستعرض ما ستحتاجه للبدء:

- Aspose.PDF لـ .NET: تأكد من تنزيل أحدث إصدار من Aspose.PDF لـ .NET وتثبيته. [التحميل هنا](https://releases.aspose.com/pdf/net/).
- .NET Framework: تأكد من أن لديك بيئة تطوير .NET مثل Visual Studio.
- الفهم الأساسي لبنية PDF: الإلمام بعناصر بنية PDF مثل الفقرات والامتدادات والجداول والصور.
- ترخيص صالح: يمكنك شراء ترخيص [هنا](https://purchase.aspose.com/buy) أو استخدم واحدة مؤقتة [هنا](https://purchase.aspose.com/temporary-license/).

## استيراد الحزم

لبدء البرمجة، عليك استيراد مساحات الأسماء الأساسية من Aspose.PDF لـ .NET. سيُتيح لك هذا الوصول إلى الفئات والأساليب اللازمة للتعامل مع مستند PDF.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

الآن بعد أن هيأنا المسرح، دعنا نقسم عملية وضع العلامات على الصورة إلى خطوات متعددة.

## الخطوة 1: تحميل مستند PDF الموجود

الخطوة الأولى هي تحميل ملف PDF الذي ترغب بالعمل عليه. يمكن أن يكون هذا أي ملف PDF يحتوي على صورة ترغب في وسمها.

```csharp
// المسار إلى دليل المستندات.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// افتح المستند
Document document = new Document(inFile);
```

- يستبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي لملفك.
- ال `Document` تسمح لك هذه الفئة بتحميل ملف PDF موجود. ستُعدِّل هذا الملف لإضافة علامة إلى الصورة.

## الخطوة 2: الوصول إلى المحتوى المُوسوم وعنصر البنية الجذرية

بعد فتح ملف PDF، الخطوة التالية هي الوصول إلى المحتوى المُعلَّم وتحديد عنصر البنية الجذرية. هذا أمر بالغ الأهمية لأنه يسمح لك بالتنقل بين عناصر ملف PDF وإجراء التعديلات اللازمة.

```csharp
// احصل على محتوى مُعَلَّم وعنصر هيكل الجذر
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` يتيح الوصول إلى العناصر المنظمة في ملف PDF.
- ال `RootElement` هو العنصر الهيكلي الأعلى، والذي يمكنك من خلاله الانتقال إلى عناصر أخرى مثل الفقرات والجداول والصور.

## الخطوة 3: تعيين عنوان مستند PDF المُعَلَّم

إن إضافة عنوان إلى مستند PDF المُعَلَّم يضمن تصنيف مستندك بشكل صحيح، وهو أمر مفيد لإمكانية الوصول إليه والامتثال لمعايير PDF/UA.

```csharp
// تعيين عنوان لمستند PDF المُوسوم
taggedContent.SetTitle("Document with images");
```

- يؤدي تعيين عنوان لملف PDF المُوسوم إلى تحسين إمكانية الوصول إليه وتحسين وضوح المستند بالنسبة لقارئات الشاشة وتقنيات المساعدة.

## الخطوة 4: البحث عن الصورة ووضع علامة عليها

الآن، دعنا نجد عنصر الصورة (المشار إليه باسم `FigureElement` في Aspose.PDF، قم بتعيين نص بديل له، وقم بتكوين سمات التخطيط الخاصة به.

```csharp
// التنقل عبر جميع عناصر الشكل (الصور) وتعيين النص البديل وسمات التخطيط
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // تعيين نص بديل للشكل
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // إنشاء وتعيين سمة BBox (الصندوق المحيط)
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // تعيين سمات التخطيط للشكل
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- هذا الكود يتكرر خلال كل `FigureElement` الأشياء الموجودة في البنية الجذرية، والتي تمثل الصور.
- يحدد النص البديل لإمكانية الوصول (سيستخدم قارئو الشاشة هذا لوصف الصورة).
- المربع المحدد (`BBox`) تحدد إحداثيات تخطيط الصورة، مما يضمن عرضها بشكل صحيح في المستند.

## الخطوة 5: تعديل عناصر النطاق داخل الجدول

في بعض الحالات، قد تحتاج إلى تعديل عناصر النطاق داخل جدول. سنوضح هنا كيفية العثور على `SpanElement` ونقلها إلى فقرة.

```csharp
// العثور على عناصر الجدول والنطاق والفقرة
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// نقل عنصر الامتداد إلى الفقرة
spanElement.ChangeParentElement(paragraph);
```

- هنا، نجد `TableElement`، `SpanElement`، و `ParagraphElement` داخل ملف PDF.
- باستخدام `ChangeParentElement` في هذه الطريقة، نقوم بنقل الامتداد إلى الفقرة لضمان وضع العلامات والبنية المناسبة.

## الخطوة 6: حفظ المستند والتحقق من توافقه مع PDF/UA

بمجرد إجراء كافة التغييرات، تكون الخطوة الأخيرة هي حفظ ملف PDF المحدث والتحقق مما إذا كان يتوافق مع معايير PDF/UA.

```csharp
// احفظ مستند PDF المحدث
document.Save(outFile);

// التحقق من صحة توافق PDF/UA
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- ال `Validate` تتحقق الطريقة من مستند PDF وفقًا لمعايير PDF/UA وتسجل النتائج.
- يساعد ضمان الامتثال على تحسين إمكانية الوصول وتلبية المتطلبات التنظيمية لنشر المستندات.

## خاتمة

في هذا البرنامج التعليمي، شرحنا لك كيفية وضع علامات على الصور في ملف PDF موجود باستخدام Aspose.PDF لـ .NET. من خلال تحديد نص بديل، وتعديل سمات التخطيط، والتحقق من توافق المستند مع PDF/UA، يمكنك ضمان سهولة الوصول إلى ملفات PDF الخاصة بك وتوافقها مع المعايير الحديثة. يُسهّل Aspose.PDF العمل مع العناصر المنظمة، مما يمنحك التحكم في تخطيط مستندك وسهولة الوصول إليه.

## الأسئلة الشائعة

### ما هو استخدام Aspose.PDF لـ .NET؟
Aspose.PDF for .NET هي مكتبة قوية تستخدم لإنشاء وتحرير ومعالجة مستندات PDF برمجيًا في بيئة .NET.

### كيف يمكنني التأكد من توافق PDF/UA؟
يمكنك استخدام Aspose.PDF `Validate` طريقة للتحقق من توافق PDF/UA بعد إجراء تعديلات على المستند.

### ما هو النص البديل في ملفات PDF؟
النص البديل هو وصف يضاف إلى الصور في ملفات PDF لتحسين إمكانية الوصول إليها، وخاصة للمستخدمين الذين يعتمدون على برامج قراءة الشاشة.

### هل يمكنني التعامل مع الجداول والامتدادات في ملف PDF باستخدام Aspose.PDF؟
نعم، يسمح لك Aspose.PDF بالتعامل مع الجداول والامتدادات والعناصر المنظمة الأخرى داخل مستند PDF.

### أين يمكنني تنزيل Aspose.PDF لـ .NET؟
يمكنك تنزيل أحدث إصدار من Aspose.PDF لـ .NET [هنا](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}