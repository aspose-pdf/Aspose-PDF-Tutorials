---
"description": "تعرّف على كيفية التوقيع الرقمي على ملفات PDF باستخدام Aspose.PDF لـ .NET. دليل خطوة بخطوة لضمان أمان مستنداتك وصحتها."
"linktitle": "تسجيل الدخول رقميًا إلى ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تسجيل الدخول رقميًا إلى ملف PDF"
"url": "/ar/net/programming-with-security-and-signatures/digitally-sign/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تسجيل الدخول رقميًا إلى ملف PDF

## مقدمة

في عالمنا الرقمي، لا شك أن تأمين المستندات أمرٌ بالغ الأهمية. سواءً كنتَ عاملًا مستقلًا تُرسِل عقودًا، أو صاحب مشروع صغير يُدير الفواتير، أو جزءًا من شركة كبيرة، فإن ضمان بقاء مستنداتك أصليةً ومنع التلاعب بها أمرٌ بالغ الأهمية. ومن الطرق الفعّالة لتحقيق هذا الأمان استخدام التوقيعات الرقمية. في هذه المقالة، سنستكشف كيفية توقيع ملف PDF رقميًا باستخدام مكتبة Aspose.PDF لـ .NET. سنشرح لك كل شيء خطوة بخطوة.

## المتطلبات الأساسية

قبل الخوض في التفاصيل، لنتأكد من توفر كل ما تحتاجه لبدء التوقيع الرقمي على ملفات PDF. إليك قائمة بالمتطلبات الأساسية:

1. إطار عمل .NET: تأكد من تثبيت إطار عمل .NET على جهازك. يدعم Aspose.PDF لـ .NET إصدارات متعددة من إطار العمل.
2. مكتبة Aspose.PDF: ستحتاج إلى تنزيل مكتبة Aspose.PDF وتثبيتها. يمكنك الحصول عليها من [رابط الإصدار](https://releases.aspose.com/pdf/net/).
3. الشهادة الرقمية: لتوقيع ملفات PDF، ستحتاج إلى شهادة رقمية — `.pfx` الملف عادة.
4. بيئة التطوير: استخدم Visual Studio أو أي بيئة تطوير متكاملة من اختيارك تدعم C#.

بمجرد توفر هذه المتطلبات الأساسية لديك، ستكون جاهزًا للبدء في توقيع مستندات PDF الخاصة بك!

## استيراد الحزم

بعد أن انتهيت من إعداد كل شيء، لنستورد الحزم اللازمة لتشغيل مشروعنا. في أعلى فئة C#، أضف مساحات الأسماء ذات الصلة:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Collections;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
```

توفر هذه المساحات الأسماء الفئات والطرق الأساسية التي ستستخدمها لمعالجة ملفات PDF باستخدام Aspose.PDF.

## الخطوة 1: إعداد مسارات المستندات الخاصة بك

الخطوة الأولى هي تحديد مسارات ملفات PDF المدخلة والمخرجة وشهادتك الرقمية. استبدل `YOUR DOCUMENTS DIRECTORY` مع المسار الفعلي على نظامك حيث توجد ملفاتك.

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
string pbxFile = ""; // المسار إلى الشهادة الرقمية الخاصة بك (.pfx)
string inFile = dataDir + @"DigitallySign.pdf";
string outFile = dataDir + @"DigitallySign_out.pdf";
```
في هذه المقتطفة، `inFile` هو ملف PDF الأصلي الذي تريد التوقيع عليه، و `outFile` هو المكان الذي سيتم فيه حفظ ملف PDF الموقع.

## الخطوة 2: تحميل مستند PDF

بعد ذلك، نحتاج إلى تحميل مستند PDF الذي نريد توقيعه. `Document` يتم استخدام الفئة الموجودة في Aspose.PDF هنا:

```csharp
using (Document document = new Document(inFile))
{
    // متابعة مع منطق التوقيع هنا...
}
```

يفتح هذا الرمز ملف PDF الخاص بك ويجهزه للعمليات الإضافية.

## الخطوة 3: تهيئة فئة PdfFileSignature

بمجرد تحميل المستند، نقوم بإنشاء مثيل لـ `PdfFileSignature` الفئة التي ستسمح لنا بالعمل بالتوقيعات الرقمية على مستند PDF المحمل لدينا.

```csharp
using (PdfFileSignature signature = new PdfFileSignature(document))
{
    // إعداد عملية التوقيع
}
```

هذه الفئة هي وجهتك لكل الأشياء المتعلقة بتوقيعات PDF!

## الخطوة 4: إنشاء نسخة شهادة رقمية

هنا يمكنك إعداد شهادتك التي ستُستخدم لتوقيع ملف PDF. ستحتاج إلى توفير مسار شهادتك. `.pfx` الملف مع كلمة المرور المرتبطة به.

```csharp
PKCS7 pkcs = new PKCS7(pbxFile, "WebSales");
```

تأكد من الاستبدال `"WebSales"` مع كلمة المرور الفعلية للشهادة الخاصة بك.

## الخطوة 5: تكوين مظهر التوقيع

بعد ذلك، نحدد كيفية ظهور التوقيع في ملف PDF. يمكنك تخصيص موقع ومظهر التوقيع باستخدام مستطيل. 

```csharp
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
signature.SignatureAppearance = dataDir + @"aspose-logo.jpg";
```

هنا، نقوم بوضع التوقيع عند الإحداثيات (100، 100) بعرض 200 وارتفاع 100.

## الخطوة 6: إنشاء التوقيع وحفظه

الآن حان وقت إنشاء التوقيع وحفظ ملف PDF المُوقّع. يمكنك توضيح سبب التوقيع، وبيانات الاتصال بك، وموقعك. سيساعدك هذا في عملية التحقق لاحقًا.

```csharp
DocMDPSignature docMdpSignature = new DocMDPSignature(pkcs, DocMDPAccessPermissions.FillingInForms);
signature.Certify(1, "Signature Reason", "Contact", "Location", true, rect, docMdpSignature);
signature.Save(outFile);
```

## الخطوة 7: التحقق من التوقيع

بعد حفظ ملف PDF المُوقّع، يُنصح دائمًا بالتأكد من صحة إضافة التوقيع. يمكننا استرجاع أسماء التوقيعات والتحقق من صحتها. 

```csharp
using (Document document = new Document(outFile))
{
    using (PdfFileSignature signature = new PdfFileSignature(document))
    {
        IList<string> sigNames = signature.GetSignNames();
        if (sigNames.Count > 0) 
        {
            if (signature.VerifySigned(sigNames[0] as string)) 
            {
                if (signature.IsCertified) 
                {
                    if (signature.GetAccessPermissions() == DocMDPAccessPermissions.FillingInForms) 
                    {
                        // التوقيع صحيح ومصدق
                    }
                }
            }
        }
    }
}
```

يضمن هذا الجزء التحقق من صحة عملك؛ ففي نهاية المطاف، لن ترغب في إرسال مستند غير موقع!

## الخطوة 8: التعامل مع الاستثناءات

من الحكمة دائمًا تغليف الكود الخاص بك في كتلة try-catch للتعامل مع أي استثناءات بسلاسة. 

```csharp
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

بهذه الطريقة، إذا حدث شيء غير متوقع، ستعرف بالضبط ما الذي حدث خطأ دون تعطل تطبيقك.

## خاتمة

تُوفر التوقيعات الرقمية حمايةً أساسيةً للمستندات، إذ تُثبت صحتها وسلامتها. مع Aspose.PDF لـ .NET، يُصبح توقيع ملف PDF عمليةً سهلةً تُحسّن سير عمل إدارة مستنداتك بشكل كبير. الآن، وبعد أن تعلمتَ كيفية رقمنة توقيعاتك، يُمكنك ضمان احترافيتك وتعاملك الآمن مع مستنداتك لعملائك وشركائك.

## الأسئلة الشائعة

### ما هو التوقيع الرقمي؟
التوقيع الرقمي هو المعادل التشفيري للتوقيع اليدوي، ويضمن صحة البيانات وسلامتها.

### هل يمكنني استخدام Aspose.PDF لتوقيع ملفات PDF في أي تطبيق .NET؟
نعم! Aspose.PDF لـ .NET متوافق مع مختلف تطبيقات .NET، بما في ذلك سطح المكتب والويب والخدمات.

### ما هي أنواع الشهادات الرقمية التي يمكنني استخدامها؟
يمكنك استخدام أي شهادة PKCS#12، والتي يتم حفظها عادةً في `.pfx` أو `.p12` ملف.

### هل هناك نسخة تجريبية من Aspose.PDF متاحة؟
نعم! يمكنك تنزيل نسخة تجريبية مجانية من [صفحة إصدارات Aspose](https://releases.aspose.com/).

### كيف يمكنني الحصول على الدعم إذا واجهت مشاكل؟
للحصول على الدعم، يمكنك زيارة [منتدى Aspose PDF](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}