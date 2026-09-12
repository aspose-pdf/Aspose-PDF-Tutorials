---
category: general
date: 2026-09-12
description: Aspose.PDF का उपयोग करके C# में PDF में पारदर्शिता कैसे जोड़ें, PDF पर
  आयत कैसे बनाएं, और पारदर्शिता के साथ PDF को कैसे सहेजें – चरण‑दर‑चरण गाइड।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: hi
lastmod: 2026-09-12
og_description: Aspose.PDF का उपयोग करके C# में PDF में पारदर्शिता जोड़ें, PDF पर
  एक आयत बनाएं, और पारदर्शिता के साथ PDF सहेजें। इस पूर्ण ट्यूटोरियल का पालन करें।
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: PDF में पारदर्शिता जोड़ें और PDF पर आयत बनाएं – पूर्ण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Aspose.PDF के साथ PDF में पारदर्शिता कैसे जोड़ें और PDF पर आयत कैसे बनाएं
url: /hi/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF के साथ PDF में ट्रांसपेरेंसी कैसे जोड़ें और PDF पर आयत (Rectangle) कैसे बनाएं

यदि आपको **PDF फ़ाइलों में ट्रांसपेरेंसी जोड़नी** है, तो यह गाइड आपको C# में इसे बिल्कुल कैसे करना है दिखाता है। आप यह भी सीखेंगे कि **PDF पर आयत कैसे बनाएं** और अंत में **ट्रांसपेरेंसी के साथ PDF कैसे सेव करें** ताकि परिणाम को रिपोर्ट, इनवॉइस या किसी भी दस्तावेज़‑ऑटोमेशन वर्कफ़्लो में पुनः उपयोग किया जा सके।

इस ट्यूटोरियल में आप करेंगे:

* मौजूदा PDF दस्तावेज़ को लोड करेंगे।
* स्ट्रोक और फ़िल ऑपेसिटी को परिभाषित करने वाला एक कस्टम ग्राफ़िक्स स्टेट बनाएँगे।
* उस ग्राफ़िक्स स्टेट को कैनवास पर लागू करके आयत ड्रॉ करेंगे।
* ट्रांसपेरेंसी सेटिंग्स को बरकरार रखते हुए संशोधित फ़ाइल को सेव करेंगे।

Aspose.PDF for .NET लाइब्रेरी के अलावा कोई बाहरी टूल आवश्यक नहीं है, और हर कोड लाइन की व्याख्या की गई है ताकि आप समझ सकें कि *क्यों* प्रत्येक कदम महत्वपूर्ण है।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)।
* **Aspose.PDF for .NET** की लाइसेंस्ड या इवैल्यूएशन कॉपी। इसे NuGet के माध्यम से इंस्टॉल करें:

```bash
dotnet add package Aspose.Pdf
```

* एक इनपुट PDF (`input.pdf`) जिसे आप अपने प्रोजेक्ट से रेफ़रेंस कर सकें।

## चरण 1: PDF दस्तावेज़ लोड करें

पहला ऑपरेशन स्रोत फ़ाइल को खोलना है। `using` स्टेटमेंट का उपयोग करने से दस्तावेज़ सही तरीके से डिस्पोज़ हो जाता है, जिससे बाद में फ़ाइल‑लॉकिंग समस्याओं से बचा जा सके।

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*यह क्यों महत्वपूर्ण है*: दस्तावेज़ लोड करने से आपको पेज कलेक्शन, रिसोर्स डिक्शनरी और ड्रॉइंग के लिए आवश्यक कैनवास ऑब्जेक्ट्स तक पहुँच मिलती है।

## चरण 2: पहले पेज की रिसोर्स डिक्शनरी तक पहुँचें

हर PDF पेज की एक **रिसोर्स डिक्शनरी** होती है जिसमें फ़ॉन्ट, इमेज और ग्राफ़िक्स स्टेट जैसी वस्तुएँ संग्रहीत रहती हैं। नई ट्रांसपेरेंसी सेटिंग जोड़ने के लिए हमें `ExtGState` एंट्री को एडिट करना होगा।

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*यह क्यों महत्वपूर्ण है*: `DictionaryEditor` हमें लो‑लेवल PDF ऑब्जेक्ट्स को पढ़ने और संशोधित करने की सुविधा देता है बिना दस्तावेज़ की संरचना को तोड़े।

## चरण 3: ट्रांसपेरेंसी मानों के साथ कस्टम ग्राफ़िक्स स्टेट बनाएं

एक ग्राफ़िक्स स्टेट (`ExtGState`) यह नियंत्रित करता है कि ड्रॉइंग ऑपरेशन्स कैसे रेंडर होते हैं। हम दो ऑपेसिटी पैरामीटर परिभाषित करते हैं:

* **CA** – स्ट्रोक ऑपेसिटी (आकार की बाहरी रेखा)।
* **ca** – फ़िल ऑपेसिटी (आकार का अंदरूनी भाग)।

हम ब्लेंड मोड (`BM`) को “Normal” भी सेट करते हैं, जो सबसे सामान्य कॉम्पोज़िट ऑपरेशन है।

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*यह क्यों महत्वपूर्ण है*: `ExtGState` डिक्शनरी में `GS0` जोड़ने से हम एक पुन: उपयोग योग्य रेफ़रेंस बनाते हैं जिसे कैनवास ड्रॉइंग से पहले एक्टिवेट कर सकता है। `0.5` फ़िल ऑपेसिटी आयत को अर्ध‑पारदर्शी बनाती है, जिससे **PDF में ट्रांसपेरेंसी जोड़ने** का लक्ष्य पूरा होता है।

## चरण 4: ग्राफ़िक्स स्टेट लागू करें और आयत बनाएं

अब हम पेज के कैनवास को अभी बनाए गए ग्राफ़िक्स स्टेट का उपयोग करने के लिए कहते हैं, फिर आयत ड्रॉ करते हैं। कोऑर्डिनेट्स PDF कोऑर्डिनेट सिस्टम (नीचे‑बाएँ कोना मूल बिंदु) का पालन करते हैं।

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*यह क्यों महत्वपूर्ण है*: `SetGraphicsState("GS0")` ड्रॉइंग कॉन्टेक्स्ट को पहले परिभाषित ट्रांसपेरेंसी सेटिंग्स पर स्विच कर देता है। `Rectangle` मेथड आकार को परिभाषित करता है, और `Stroke` निर्दिष्ट ऑपेसिटी के साथ आउटलाइन रेंडर करता है। यदि आप भराव (फ़िल) वाली आयत चाहते हैं, तो `Stroke()` को `FillAndStroke()` से बदलें।

## चरण 5: ट्रांसपेरेंसी बरकरार रखते हुए संशोधित PDF सेव करें

अंत में, दस्तावेज़ को डिस्क पर वापस लिखें। आउटपुट फ़ाइल में नया ग्राफ़िक्स स्टेट, ड्रॉ की गई आयत और ट्रांसपेरेंसी जानकारी होगी।

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*यह क्यों महत्वपूर्ण है*: दस्तावेज़ को सेव करने से सभी बदलाव अंतिम रूप ले लेते हैं। परिणामी फ़ाइल किसी भी PDF व्यूअर में खुल सकती है, और आयत 50 % फ़िल ऑपेसिटी के साथ दिखाई देगी।

### अपेक्षित परिणाम

जब आप `output_with_extgstate.pdf` खोलेंगे, तो आपको एक आयत दिखेगी जिसकी बॉर्डर पूरी तरह अपारदर्शी होगी और अंदरूनी भाग अर्ध‑पारदर्शी होगा, जिससे नीचे की पेज सामग्री दिखाई दे सकेगी।

## किनारे के मामलों और व्यावहारिक टिप्स

| स्थिति | सुझाया गया समायोजन |
|-----------|------------------------|
| **एकाधिक पेज** | `pdfDocument.Pages` पर लूप करें और प्रत्येक लक्ष्य पेज के लिए चरण 2‑4 दोहराएँ। |
| **विभिन्न ऑपेसिटी मान** | `CA` (स्ट्रोक) और `ca` (फ़िल) के लिए `CosPdfNumber` मान को `0` (पूरी तरह पारदर्शी) से `1` (पूरी तरह अपारदर्शी) के बीच किसी भी संख्या में बदलें। |
| **कस्टम ब्लेंड मोड** | `"Normal"` को `"Multiply"`, `"Screen"` या आपके व्यूअर द्वारा समर्थित किसी भी PDF‑स्टैंडर्ड ब्लेंड मोड से बदलें। |
| **फ़िल्ड आयत** | `canvas.Stroke()` के बजाय `canvas.FillAndStroke()` कॉल करें ताकि फ़िल और आउटलाइन दोनों लागू हों। |
| **एक ही ग्राफ़िक्स स्टेट का पुनः उपयोग** | आप एक ही पेज पर कई आकार ड्रॉ करने से पहले `canvas.SetGraphicsState("GS0")` कॉल कर सकते हैं। |

**प्रो टिप:** नया `ExtGState` जोड़ने के बाद हमेशा रिसोर्स डिक्शनरी की जाँच करें। यदि डिक्शनरी मौजूद नहीं है, तो पहले इसे बनाएँ:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## पूर्ण, चलाने योग्य उदाहरण

नीचे एक स्व-निहित प्रोग्राम दिया गया है जिसे आप कॉन्सोल एप्लिकेशन में कॉपी करके तुरंत चला सकते हैं (`YOUR_DIRECTORY` को वास्तविक पाथ से बदलें)।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

प्रोग्राम चलाने से `output_with_extgstate.pdf` बनता है, जो **PDF में ट्रांसपेरेंसी जोड़ना**, **PDF पर आयत बनाना**, और **ट्रांसपेरेंसी के साथ PDF सेव करना** को एक ही फ्लो में दर्शाता है।

## निष्कर्ष

आप अब जानते हैं कि Aspose.PDF for .NET का उपयोग करके **PDF में ट्रांसपेरेंसी कैसे जोड़ें**, **PDF पर आयत कैसे बनाएं**, और **ट्रांसपेरेंसी के साथ PDF कैसे सेव करें**। प्रक्रिया कस्टम `ExtGState` बनाने, उसे कैनवास पर लागू करने और बदलावों को स्थायी करने के इर्द‑गिर्द घूमती है। इन बिल्डिंग ब्लॉक्स के साथ आप तकनीक को अन्य आकारों, कई पेजों या डायनामिक ऑपेसिटी मानों तक विस्तारित कर सकते हैं।

**आगे के कदम**

* `canvas.Ellipse`, `canvas.Path` या `canvas.TextFragment` जैसे अन्य ड्रॉइंग प्रिमिटिव्स को समान ग्राफ़िक्स स्टेट के साथ एक्सप्लोर करें।
* इमेज ओवरले के साथ ट्रांसपेरेंसी को मिलाकर वॉटरमार्क बनाएं (`canvas.Image` + कस्टम `ExtGState`)।
* उन्नत कॉम्पोज़िट इफ़ेक्ट्स के लिए **ग्राफ़िक्स स्टेट पैरामीटर** पर Aspose.PDF दस्तावेज़ीकरण देखें।

हैप्पी कोडिंग, और अपने PDF वर्कफ़्लो में ट्रांसपेरेंसी द्वारा लाई गई दृश्य लचीलापन का आनंद लें!


## अगला क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}