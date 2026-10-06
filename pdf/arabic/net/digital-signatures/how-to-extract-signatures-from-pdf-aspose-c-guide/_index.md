---
category: general
date: 2026-04-02
description: تعلم كيفية استخراج التوقيعات، إضافة حقل، إضافة صفحة فارغة إلى ملف PDF،
  كيفية إضافة عنصر واجهة (widget)، والحفاظ على شفافية PDF باستخدام Aspose.Pdf في C#.
draft: false
keywords:
- how to extract signatures
- how to add field
- add blank page pdf
- how to add widget
- preserve transparency pdf
language: ar
og_description: كيفية استخراج التوقيعات من ملف PDF وأداء المهام ذات الصلة مثل إضافة
  الحقول والصفحات الفارغة والأدوات والحفاظ على الشفافية باستخدام Aspose.Pdf.
og_title: كيفية استخراج التوقيعات من ملفات PDF – دليل Aspose C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: كيفية استخراج التوقيعات من ملفات PDF – دليل Aspose C#
url: /ar/net/digital-signatures/how-to-extract-signatures-from-pdf-aspose-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج التوقيعات من PDF – دليل Aspose C#

**كيفية استخراج التوقيعات من PDF** هو طلب شائع عندما تقوم بأتمتة معالجة العقود، أو الموافقات على الفواتير، أو أي سير عمل يعتمد على التوقيعات الرقمية.  
في هذا الدليل سنستعرض أيضًا **كيفية إضافة حقل**، **إضافة صفحة فارغة إلى PDF**، **كيفية إضافة عنصر واجهة (widget)**، و**الحفاظ على شفافية PDF** باستخدام مكتبة Aspose.Pdf لـ .NET.

تخيل أنك تستلم عشرات ملفات PDF موقعة كل ليلة؛ فتح كل ملف يدويًا للتحقق من التوقيعات سيكون كابوسًا. ببضع أسطر من كود C# يمكنك سحب أسماء التوقيعات برمجيًا، والحفاظ على الرسومات الأصلية، وحتى إغناء المستند بحقول نموذج جديدة—كل ذلك دون كسر الشفافية أو ملفات تعريف الألوان الموجودة.

> **ما ستحصل عليه:** مثال كامل قابل للتنفيذ يحول PDF إلى PDF/X‑4 (مع الحفاظ على الشفافية)، يستخرج كل اسم توقيع مضمّن، يضيف صفحة فارغة، وينشئ حقل نصي يظهر في مكانين على نفس الصفحة.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework)
- Aspose.Pdf for .NET **v25.2** أو أحدث (مطلوب لـ `GetSignatureNames()`)
- مشروع Visual Studio أو أي بيئة تطوير C#
- ثلاثة ملفات PDF تجريبية في مجلد تتحكم فيه:
  - `source.pdf` – أي PDF تريد تحويله مع الحفاظ على الشفافية
  - `signed.pdf` – PDF يحتوي بالفعل على توقيعات رقمية
  - (اختياري) مجلد فارغ لملفات الإخراج

> **نصيحة احترافية:** إذا لم يكن لديك نسخة مرخصة بعد، يمكنك طلب ترخيص مؤقت مجاني من موقع Aspose. الوضع المجاني يعمل للاختبار لكنه يضيف علامة مائية.

## الخطوة 1 – الحفاظ على شفافية PDF عبر التحويل إلى PDF/X‑4

غالبًا ما تُفقد الشفافية وملفات تعريف الألوان المضمّنة عند تسطيح PDF. التحويل إلى **PDF/X‑4** يحافظ على هذه العناصر البصرية، وهو أمر حاسم للمستندات الجاهزة للطباعة.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// 1️⃣ Convert source.pdf → PDF/X‑4 (preserves transparency & color profiles)
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,          // Target format
    ConvertErrorAction.Delete  // Remove pages that cause conversion errors
);

using (var sourceDoc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    sourceDoc.Convert(conversionOptions);
    sourceDoc.Save("YOUR_DIRECTORY/toPdfX4.pdf");
}
```

**لماذا هذا مهم:**  
PDF/X‑4 هو المعيار ISO لملفات PDF الخاصة بتبادل الرسومات التي تحتفظ بالشفافية الحية. باستخدام `PdfFormatConversionOptions`، تتجنب الفخ الشائع المتمثل في تحويل الكائنات الشفافة إلى نقطية، مما قد يزيد حجم الملف بشكل كبير ويقلل الجودة.

## الخطوة 2 – كيفية استخراج التوقيعات من PDF

قدمت Aspose الدالة `GetSignatureNames()` في الإصدار 25.2، مما يجعل استخراج التوقيعات عملية سطر واحد. تُعيد الدالة مصفوفة من الأسماء المنطقية المعيّنة لكل حقل توقيع رقمي.

```csharp
using Aspose.Pdf;

// 2️⃣ Pull out every signature name from signed.pdf
using (var signedDoc = new Document("YOUR_DIRECTORY/signed.pdf"))
{
    // Returns strings like "Signature1", "EmployeeSignature", etc.
    string[] signatureNames = signedDoc.GetSignatureNames();   // new method in 25.2

    // Show the names in the console – you could store them in a DB instead
    Console.WriteLine("Found signatures: " + string.Join(", ", signatureNames));
}
```

**ما المتوقع:** إذا كان `signed.pdf` يحتوي على توقيعين باسم *ManagerSig* و *ClientSig*، سيطبع الطرفية:

```
Found signatures: ManagerSig, ClientSig
```

**معالجة الحالات الطرفية:**  
- إذا لم يحتوي PDF على توقيعات، تُعيد `GetSignatureNames()` مصفوفة فارغة – لا يُرمى استثناء.  
- بالنسبة لملفات PDF التي تحتوي على حقول توقيع تالفة، يمكنك تغليف الاستدعاء داخل `try/catch` وتسجيل الخطأ دون إيقاف العملية بالكامل.

## الخطوة 3 – إضافة صفحة فارغة إلى PDF وإنشاء TextBox مع عدة Widgets

إضافة صفحة جديدة أمر بسيط، لكن **كيفية إضافة حقل** و**كيفية إضافة widget** معًا يتطلب بعض الدقة. الـ *widget* هو التمثيل البصري لحقل النموذج؛ يمكنك إرفاق عدة widgets لنفس الحقل المنطقي، مما يسمح بظهور نفس البيانات في مواقع متعددة.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// 3️⃣ Build a fresh document, add a blank page, then a textbox with two widgets
using (var newDoc = new Document())
{
    // ---- Add a blank page -------------------------------------------------
    var page = newDoc.Pages.Add();   // This is the "add blank page pdf" step

    // ---- Define the primary widget (the actual appearance) ---------------
    var textBox = new TextBoxField(page, new Rectangle(100, 600, 300, 650))
    {
        PartialName = "Comments",               // logical name of the field
        Value = "Enter your comment here"       // default value
    };

    // ---- Add a second widget at a different location ----------------------
    var secondWidget = new WidgetAnnotation(page, new Rectangle(100, 500, 300, 550));
    textBox.Widgets.Add(secondWidget); // This is the "how to add widget" part

    // ---- Register the field with the document's form collection -----------
    newDoc.Form.Add(textBox, "Comments");

    // ---- Save the result --------------------------------------------------
    newDoc.Save("YOUR_DIRECTORY/TextBoxMultipleWidgets.pdf");
}
```

**لماذا نستخدم عدة widgets؟**  
افترض أنك تريد أن يظهر نفس التعليق على الوجهين الأمامي والخلفي لعقد. بإرفاق widgetين لنفس الحقل، أي تعديل يجريه المستخدم في موقع سيُحدّث تلقائيًا الموقع الآخر.

**المخاطر الشائعة:**  
- نسيان إضافة الحقل إلى `newDoc.Form` سيجعل الـ widget غير مرئي في عارضات PDF.  
- استخدام إحداثيات مستطيل متطابقة لكلا الـ widgets سيؤدي إلى تراكبهما فوق بعضهما—تأكد من أن قيم `Rectangle` مختلفة.

## الخطوة 4 – تجميع كل شيء معًا: مثال كامل قابل للتنفيذ

فيما يلي برنامج واحد ينفّذ كل خطوة بالترتيب المذكور. انسخه إلى مشروع وحدة تحكم جديد، عدّل المسارات، وشغّله.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;

namespace AsposePdfDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Preserve transparency by converting to PDF/X‑4
            // -----------------------------------------------------------------
            var conversionOptions = new PdfFormatConversionOptions(
                PdfFormat.PDF_X_4,
                ConvertErrorAction.Delete);

            using (var sourceDoc = new Document("YOUR_DIRECTORY/source.pdf"))
            {
                sourceDoc.Convert(conversionOptions);
                sourceDoc.Save("YOUR_DIRECTORY/toPdfX4.pdf");
                Console.WriteLine("✅ PDF/X‑4 conversion complete (transparency preserved).");
            }

            // -----------------------------------------------------------------
            // 2️⃣ Extract signature names
            // -----------------------------------------------------------------
            using (var signedDoc = new Document("YOUR_DIRECTORY/signed.pdf"))
            {
                string[] signatureNames = signedDoc.GetSignatureNames(); // new in 25.2
                if (signatureNames.Length == 0)
                    Console.WriteLine("⚠️ No signatures found.");
                else
                    Console.WriteLine("🔍 Found signatures: " + string.Join(", ", signatureNames));
            }

            // -----------------------------------------------------------------
            // 3️⃣ Add a blank page and a textbox with two widgets
            // -----------------------------------------------------------------
            using (var newDoc = new Document())
            {
                // Add a blank page – “add blank page pdf”
                var page = newDoc.Pages.Add();

                // Primary widget for the textbox
                var textBox = new TextBoxField(page, new Rectangle(100, 600, 300, 650))
                {
                    PartialName = "Comments",
                    Value = "Enter your comment here"
                };

                // Second widget – “how to add widget”
                textBox.Widgets.Add(new WidgetAnnotation(page, new Rectangle(100, 500, 300, 550)));

                // Register the field – “how to add field”
                newDoc.Form.Add(textBox, "Comments");

                // Save the final document
                newDoc.Save("YOUR_DIRECTORY/TextBoxMultipleWidgets.pdf");
                Console.WriteLine("✅ Blank page added and textbox with two widgets created.");
            }

            Console.WriteLine("\nAll tasks completed successfully!");
        }
    }
}
```

### المخرجات المتوقعة

عند تشغيل البرنامج يجب أن ترى شيئًا مشابهًا لـ:

```
✅ PDF/X‑4 conversion complete (transparency preserved).
🔍 Found signatures: ManagerSig, ClientSig
✅ Blank page added and textbox with two widgets created.

All tasks completed successfully!
```

افتح `TextBoxMultipleWidgets.pdf` في Adobe Acrobat Reader؛ ستلاحظ وجود صندوقين نصيين متطابقين يحملان العنوان **Comments**—أحدهما قريب من الأعلى، والآخر أسفل قليلًا. الكتابة في أحدهما تُحدّث الآخر فورًا.

## الأسئلة المتكررة (FAQ)

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني استخراج بايتات التوقيع الفعلية؟** | `GetSignatureNames()` تُعيد فقط الأسماء المنطقية. لاستخراج الشهادة أو قيمة التوقيع تحتاج إلى كائنات `SignatureField` (`document.Form["fieldName"] as SignatureField`). |
| **هل يعمل تحويل PDF/X‑4 على ملفات PDF المشفّرة؟** | نعم، طالما تزود كلمة المرور عبر `Document.Open(file, password)`. |
| **ماذا لو احتجت إلى أكثر من widgetين؟** | ما عليك سوى استدعاء `textBox.Widgets.Add()` لكل `WidgetAnnotation` إضافي. |
| **هل ستورث الصفحة الفارغة حجم الصفحة من PDF الأصلي؟** | الصفحة الجديدة تستخدم الحجم الافتراضي (A4). يمكنك تمرير كائن `Page` بأبعاد مخصصة إذا لزم الأمر. |
| **هل الكود متوافق مع .NET Core؟** | بالتأكيد—Aspose.Pdf متعدد المنصات. فقط أضف حزمة NuGet إلى مشروع .NET Core الخاص بك. |

## الخلاصة

في هذا الدليل استعرضنا **كيفية استخراج التوقيعات من ملفات PDF**، مع تغطية **كيفية إضافة حقل**، **إضافة صفحة فارغة إلى PDF**، **كيفية إضافة widget**، و**الحفاظ على شفافية PDF** باستخدام Aspose.Pdf للغة C#. الآن لديك حل شامل من البداية إلى النهاية يمكنك دمجه في أي خط أنابيب لمعالجة المستندات.

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذه التقنيات مع وحدة OCR من Aspose لقراءة النص من المستندات الممسوحة ضوئيًا

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}