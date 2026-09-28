---
category: general
date: 2026-02-12
description: أضف أرقام بايتس إلى ملفات PDF بسرعة. تعلّم كيفية إضافة حقل نص إلى PDF،
  وإضافة حقل نموذج إلى PDF، وإضافة أرقام الصفحات إلى PDF باستخدام Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: ar
og_description: إضافة أرقام بيتس إلى مستندات PDF باستخدام C#. يوضح هذا الدليل كيفية
  إضافة حقل نص إلى PDF، وإضافة حقل نموذج إلى PDF، وإضافة أرقام الصفحات إلى PDF باستخدام
  Aspose.PDF.
og_title: إضافة أرقام بايتس إلى ملفات PDF – دليل كامل بلغة C#
tags:
- PDF
- C#
- Aspose.PDF
title: إضافة أرقام بايتس إلى ملفات PDF – دليل C# خطوة بخطوة
url: /ar/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة أرقام Bates إلى ملفات PDF – دليل C# الكامل

هل احتجت يوماً إلى **add bates numbers** إلى مجموعة من ملفات PDF القانونية لكنك لم تعرف من أين تبدأ؟ لست وحدك. في العديد من مكاتب المحاماة ومشاريع e‑discovery، طباعة كل صفحة بمعرف فريد هي مهمة يومية، والقيام بذلك يدوياً كابوس.

الخبر السار؟ ببضع أسطر من C# و Aspose.PDF يمكنك أتمتة العملية بالكامل. في هذا الدرس سنستعرض **how to add bates** numbers، نضيف حقل نصي إلى كل صفحة، ونحفظ ملف PDF نظيف وقابل للبحث—كل ذلك دون عناء.

> **ما ستحصل عليه:** عينة كود جاهزة للتنفيذ، شرح لأهمية كل سطر، نصائح للحالات الخاصة، وقائمة تحقق سريعة للتحقق من النتيجة.  
> سنتطرق أيضاً إلى مهام ذات صلة مثل **add text field pdf**، **add form field pdf**، و **add page numbers pdf**، لتكون لديك مجموعة أدوات جاهزة لأي تحدٍ في أتمتة المستندات.

---

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.6+).  
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها).  
- رخصة صالحة لـ Aspose.PDF for .NET (الإصدار التجريبي المجاني يكفي للاختبار).  
- ملف PDF مصدر يُدعى `source.pdf` موجود في مجلد يمكنك الإشارة إليه.

إذا كان أي من هذه غير مألوف لك، توقف وقم بتثبيت العنصر المفقود قبل المتابعة. الخطوات أدناه تفترض أنك قد أضفت حزمة NuGet الخاصة بـ Aspose.PDF:

```bash
dotnet add package Aspose.Pdf
```

---

## كيفية إضافة أرقام Bates إلى ملف PDF باستخدام Aspose.PDF

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. يقوم بتحميل PDF، إنشاء **حقل صندوق نص** على كل صفحة، كتابة رقم Bates بصيغة معينة، وأخيراً حفظ الملف المعدل.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### لماذا يعمل هذا

- **`Document`** هو نقطة الدخول؛ يمثل ملف PDF بالكامل.  
- **`Rectangle`** يحدد موقع الحقل على الصفحة. الأرقام بوحدة النقاط (1 pt ≈ 1/72 in). عدّل الإحداثيات إذا أردت وضع الرقم في زاوية مختلفة.  
- **`TextBoxField`** هو *حقل نموذج* يمكنه احتواء أي سلسلة نصية. عبر تعيين `Value` نضيف فعلياً **add page numbers pdf** مع بادئة مخصصة.  
- **`pdfDocument.Form.Add`** يسجل الحقل في AcroForm الخاص بالـ PDF، مما يجعله مرئياً في عارضات مثل Adobe Acrobat.  

إذا احتجت لتغيير المظهر (الخط، اللون، الحجم) يمكنك تعديل خصائص `TextBoxField`—اطلع على وثائق Aspose لـ `DefaultAppearance` و `Border`.

---

## إضافة حقل نص إلى كل صفحة PDF (خطوة “add text field pdf”)

أحياناً تريد فقط تسمية مرئية، لا حقل نموذج تفاعلي. في هذه الحالة يمكنك استبدال `TextBoxField` بـ `TextFragment` وإضافته مباشرة إلى مجموعة `Paragraphs` الخاصة بالصفحة. إليك بديل سريع:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

نهج **add text field pdf** مفيد عندما يكون المستند النهائي للقراءة فقط، بينما طريقة **add form field pdf** تبقي الأرقام قابلة للتحرير لاحقاً.

---

## حفظ PDF بأرقام Bates (لحظة “add page numbers pdf”)

بعد انتهاء الحلقة، استدعاء `pdfDocument.Save` يكتب كل شيء إلى القرص. إذا أردت الحفاظ على الملف الأصلي، ببساطة غيّر مسار الإخراج أو استخدم التحميل الزائد لـ `pdfDocument.Save` لتوجيه النتيجة مباشرة إلى استجابة في Web API.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

هذا هو الجزء الأنيق—بدون ملفات مؤقتة، بدون مكتبات إضافية، فقط Aspose يتولى الجزء الثقيل.

---

## النتيجة المتوقعة والتحقق السريع

افتح `bates.pdf` في أي عارض PDF. يجب أن ترى صندوقاً صغيراً في الزاوية السفلية اليسرى من كل صفحة يحتوي على:

```
BATES-00001
BATES-00002
…
```

إذا فحصت خصائص المستند، ستلاحظ وجود AcroForm يحتوي على حقول مسماة `Bates_1`, `Bates_2`, إلخ. هذا يؤكد نجاح خطوة **add form field pdf**.

---

## المشكلات الشائعة ونصائح الخبراء

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| الأرقام تظهر غير مركزة | إحداثيات الـ Rectangle نسبية إلى الزاوية السفلية اليسرى للصفحة. | عكس قيمة Y (`pageHeight - marginTop`) أو استخدم `page.PageInfo.Height` لحساب موضع أعلى. |
| الحقول غير مرئية في Adobe Reader | الحد الافتراضي مضبوط على “No”. | عيّن `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| ملفات PDF الكبيرة تستهلك الذاكرة | `using` يُفرغ المستند فقط بعد انتهاء الحلقة. | عالج الصفحات على دفعات أو استخدم `pdfDocument.Save` مع `SaveOptions` التي تدعم البث. |
| الرخصة غير مفعلة | Aspose يضيف علامة مائية على الصفحة الأولى. | سجّل رخصتك مبكراً: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## توسيع الحل

- **بادئات مخصصة:** استبدل `"BATES-"` بأي سلسلة (`"DOC-"`, `"CASE-"`, …).  
- **طول الصفر المسبق:** غيّر `{pageNumber:D5}` إلى `{pageNumber:D3}` للحصول على ثلاثة أرقام.  
- **وضعية ديناميكية:** استخدم `pdfDocument.Pages[pageNumber].PageInfo.Width` لتحديد موقع الحقل على الجانب الأيمن.  
- **الترقيم الشرطي:** تخطى الصفحات الفارغة بفحص `pdfDocument.Pages[pageNumber].IsBlank`.

كل هذه التغييرات تحافظ على النمط الأساسي لـ **add bates numbers**, **add text field pdf**, و **add form field pdf**.

---

## مثال كامل يعمل (الكل في واحد)

فيما يلي البرنامج النهائي الجاهز للتنفيذ والذي يدمج النصائح السابقة. انسخه إلى تطبيق Console جديد واضغط F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

شغّله، افتح النتيجة، وسترى معرفاً احترافياً على كل صفحة—بالضبط ما يتوقعه أخصائي دعم التقاضي.

---

## الخلاصة

لقد شرحنا **how to add bates numbers** إلى أي PDF باستخدام C# و Aspose.PDF. بإنشاء **text box field** على كل صفحة نضيف في آن واحد **add text field pdf**, **add form field pdf**, و **add page numbers pdf** في مرور واحد. النهج سريع، قابل للتوسع، وسهل التخصيص للبادئات المخصصة، التخطيطات المختلفة، أو المنطق الشرطي.

مستعد للتحدي التالي؟ جرّب تضمين رمز QR يربط بملف القضية الأصلي، أو أنشئ صفحة فهرس منفصلة تسرد جميع أرقام Bates مع عناوين الصفحات المقابلة. نفس الـ API يتيح لك دمج ملفات PDF، استخراج صفحات، وحتى طمس البيانات الحساسة—الحدود لا توجد.

إذا واجهت أي صعوبة، اترك تعليقاً أدناه أو راجع الوثائق الرسمية لـ Aspose لمزيد من التفاصيل. Happy coding، ونتمنى أن تظل ملفات PDF لديك مرقمة بدقة دائمًا!  

---  

![لقطة شاشة لإضافة أرقام bates](https://example.com/images/add-bates-numbers.png "مثال على إضافة أرقام bates")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}