---
category: general
date: 2026-09-15
description: Aspose.Pdf for .NET का उपयोग करके PDF में अपारदर्शिता कैसे बदलें और संशोधित
  PDF फ़ाइलों को सहेजते समय ट्रांसपेरेंसी कैसे जोड़ें, यह सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change opacity
- how to add transparency
- save modified pdf
language: hi
lastmod: 2026-09-15
og_description: Aspose.Pdf for .NET का उपयोग करके PDF में अपारदर्शिता कैसे बदलें,
  जिसमें ट्रांसपेरेंसी जोड़ना और संशोधित PDF फ़ाइलों को मिनटों में सहेजना शामिल है।
og_image_alt: Screenshot showing a PDF page before and after opacity changes
og_title: Aspose.Pdf के साथ PDF में अपारदर्शिता कैसे बदलें – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: How to change opacity in a PDF using Aspose.Pdf for .NET and learn
    how to add transparency while you save modified PDF files.
  headline: How to change opacity in a PDF with Aspose.Pdf for .NET
  type: TechArticle
tags:
- Aspose.Pdf
- .NET
- PDF manipulation
title: Aspose.Pdf for .NET के साथ PDF में अपारदर्शिता कैसे बदलें
url: /hi/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET के साथ PDF में अपारदर्शिता (opacity) कैसे बदलें

यदि आपको PDF के भीतर ऑब्जेक्ट्स की **अपारदर्शिता बदलने** की आवश्यकता है, तो यह गाइड Aspose.Pdf for .NET का उपयोग करके सटीक चरण दिखाता है। आप **ग्राफ़िक्स स्टेट्स में ट्रांसपेरेंसी जोड़ना** भी देखेंगे और सही तरीके से **संशोधित PDF** फ़ाइलें बिना गुणवत्ता खोए कैसे सहेजें, यह सीखेंगे।

अपारदर्शिता बदलना आम आवश्यकता है जब आप वॉटरमार्क ओवरले करना चाहते हैं, फेडेड बैकग्राउंड बनाना चाहते हैं, या दस्तावेज़ के भीतर UI‑जैसे इफ़ेक्ट्स बनाना चाहते हैं। नीचे दिया गया कोड सैंपल किसी भी PDF के साथ काम करता है जिसे Aspose.Pdf खोल सकता है, और ट्यूटोरियल प्रत्येक लाइन को समझाता है ताकि आप जान सकें *क्यों* यह महत्वपूर्ण है।

## आप क्या सीखेंगे

- Aspose.Pdf के साथ PDF दस्तावेज़ लोड करना।
- पेज के रिसोर्स डिक्शनरी को संपादित करके नया ग्राफ़िक्स स्टेट बनाना।
- स्ट्रोक अपारदर्शिता (`CA`), फ़िल अपारदर्शिता (`ca`) और ब्लेंड मोड (`BM`) को परिभाषित करना।
- `ExtGState` डिक्शनरी में ग्राफ़िक्स स्टेट डालना।
- **संशोधित PDF** फ़ाइलें सहेजना जो नई ट्रांसपेरेंसी सेटिंग्स को बनाए रखें।
- `ExtGState` एंट्रीज़ की कमी या मल्टी‑पेज दस्तावेज़ जैसी किनारी स्थितियों को संभालना।

### पूर्वापेक्षाएँ

| आवश्यकता | कारण |
|-------------|--------|
| .NET 6.0 या बाद का संस्करण | C# कोड के लिए रनटाइम प्रदान करता है। |
| Aspose.Pdf for .NET (NuGet पैकेज `Aspose.Pdf`) | उदाहरण में उपयोग किए गए PDF मैनिपुलेशन API को सप्लाई करता है। |
| बेसिक C# ज्ञान | सिंटैक्स और प्रोजेक्ट स्ट्रक्चर को समझने के लिए आवश्यक है। |
| इनपुट PDF (`input.pdf`) | वह फ़ाइल जिसे आप संशोधित करेंगे। |

> **Pro tip:** शुरू करने से पहले `dotnet add package Aspose.Pdf` कमांड से पैकेज इंस्टॉल करें।

## चरण 1: PDF दस्तावेज़ लोड करें

पहला ऑपरेशन स्रोत फ़ाइल को खोलना है। `using` ब्लॉक का उपयोग करने से दस्तावेज़ सही तरीके से डिस्पोज़ हो जाता है, जिससे Windows पर फ़ाइल लॉक होने से बचा जा सकता है।

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

> **यह क्यों महत्वपूर्ण है:** दस्तावेज़ को खोलने से एक इन‑मेमोरी प्रतिनिधित्व बनता है जिसे आप संपादित कर सकते हैं। `using` स्टेटमेंट सुनिश्चित करता है कि रिसोर्सेज़ रिलीज़ हों, जो बाद में **संशोधित PDF** फ़ाइलें उसी फ़ोल्डर में सहेजते समय आवश्यक है।

## चरण 2: पहला पेज और उसकी रिसोर्स डिक्शनरी प्राप्त करें

ट्रांसपेरेंसी सेटिंग्स पेज की रिसोर्स डिक्शनरी में रहती हैं। सरलता के लिए हम पहले पेज पर फोकस करेंगे, लेकिन यही लॉजिक किसी भी पेज इंडेक्स पर लागू होता है।

```csharp
// Step 2: Retrieve the first page and its resources
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

> **यह क्यों महत्वपूर्ण है:** `Resources` में फ़ॉन्ट्स, इमेजेज़ और `ExtGState` डिक्शनरी जैसी ऑब्जेक्ट्स होते हैं जहाँ ग्राफ़िक्स स्टेट्स संग्रहीत होते हैं। इस डिक्शनरी को एडिट करना ही वह एकमात्र तरीका है जिससे आप ड्रॉइंग कमांड्स की अपारदर्शिता को प्रभावित कर सकते हैं।

## चरण 3: सुनिश्चित करें कि ExtGState डिक्शनरी मौजूद है

यदि PDF में पहले से ही `ExtGState` एंट्री है, तो हम उसे पुन: उपयोग कर सकते हैं। अन्यथा हमें `KeyNotFoundException` से बचने के लिए नई डिक्शनरी बनानी होगी।

```csharp
// Step 3: Get or create the ExtGState dictionary
Aspose.Pdf.CosCosPdfDictionary extGStateDict;

if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and attach it
    extGStateDict = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

> **यह क्यों महत्वपूर्ण है:** PDFs लचीले होते हैं; कुछ फ़ाइलें कभी `ExtGState` परिभाषित नहीं करतीं। एक बनाकर सुनिश्चित किया जाता है कि आगे के अपारदर्शिता पैरामीटर रखने के लिए एक जगह उपलब्ध हो।

## चरण 4: अपारदर्शिता मानों के साथ नया ग्राफ़िक्स स्टेट बनाएं

एक ग्राफ़िक्स स्टेट (`GS`) रेंडरिंग पैरामीटर्स रखता है। `CA` (स्ट्रोक अपारदर्शिता) और `ca` (फ़िल अपारदर्शिता) के मान `0` (पूरी तरह से पारदर्शी) से `1` (पूरी तरह से अपारदर्शी) तक होते हैं। `BM` की मदद से ब्लेंड मोड चुना जाता है; `"Normal"` सबसे आम विकल्प है।

```csharp
// Step 4: Create a graphics state dictionary and set opacity parameters
var graphicsState = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA", new Aspose.Pdf.CosPdfNumber(1.0)),   // stroke opacity (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca", new Aspose.Pdf.CosPdfNumber(0.5)), // fill opacity (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM", new Aspose.Pdf.CosPdfName("Normal")) // blend mode
};

foreach (var p in parameters)
{
    graphicsState.Add(p);
}
```

> **यह क्यों महत्वपूर्ण है:** `ca` को `0.5` सेट करने से PDF रेंडरर को बताया जाता है कि भराव वाले आकार आधी अपारदर्शिता के साथ ड्रॉ किए जाएँ। अपने डिज़ाइन आवश्यकताओं के अनुसार संख्यात्मक मान बदलें। `BM` एंट्री वैकल्पिक है लेकिन यह स्पष्ट करती है कि पारदर्शी कंटेंट नीचे के ऑब्जेक्ट्स के साथ कैसे मिश्रित होगा।

## चरण 5: नया ग्राफ़िक्स स्टेट ExtGState डिक्शनरी में रजिस्टर करें

प्रत्येक ग्राफ़िक्स स्टेट का एक यूनिक नाम होना चाहिए (जैसे, `"GS0"`). यदि आप मौजूदा स्टेट को ओवरराइट करना चाहते हैं तो नाम पुन: उपयोग कर सकते हैं, लेकिन नया पहचानकर्ता उपयोग करने से अनजाने साइड‑इफ़ेक्ट्स से बचा जा सकता है।

```csharp
// Step 5: Add the graphics state to ExtGState with a unique name
extGStateDict.Add("GS0", graphicsState);
```

> **यह क्यों महत्वपूर्ण है:** एक बार स्टेट स्टोर हो जाने पर, आप इसे पेज कंटेंट स्ट्रीम में `/GS0` ऑपरेटर के साथ रेफ़र कर सकते हैं। यही वह मैकेनिज़्म है जिससे **ड्रॉइंग कमांड्स में ट्रांसपेरेंसी जोड़ना** संभव होता है।

## चरण 6: संशोधित PDF सहेजें

रिसोर्स डिक्शनरी को अपडेट करने के बाद, परिवर्तन को डिस्क पर लिखें। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई फ़ाइल बना सकते हैं; उदाहरण में स्रोत को सुरक्षित रखने के लिए `output.pdf` बनाया गया है।

```csharp
// Step 6: Save the modified PDF
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **यह क्यों महत्वपूर्ण है:** `Save` मेथड इन‑मेमोरी ऑब्जेक्ट्स, जिसमें नया ग्राफ़िक्स स्टेट भी शामिल है, को वैध PDF फ़ाइल में सीरियलाइज़ करता है। यह **अपारदर्शिता बदलने** और **संशोधित PDF** दस्तावेज़ सहेजने** का अंतिम चरण है।

## पूर्ण, चलाने योग्य उदाहरण

सभी हिस्सों को मिलाकर आपको एक स्व-निहित प्रोग्राम मिलता है जिसे आप कंसोल एप्लिकेशन में कॉपी कर सकते हैं।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Collections;

class Program
{
    static void Main()
    {
        // Path to the source PDF
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";

        // Load the document
        using var pdfDocument = new Document(pdfPath);

        // Work with the first page
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState exists
        CosCosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create a new graphics state with opacity settings
        var graphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
        };
        foreach (var p in parameters)
            graphicsState.Add(p);

        // Add the state to ExtGState under the name "GS0"
        extGStateDict.Add("GS0", graphicsState);

        // Save the result
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        Console.WriteLine("Opacity changed and PDF saved successfully.");
    }
}
```

### अपेक्षित परिणाम

`output.pdf` को किसी भी PDF व्यूअर में खोलें। कोई भी कंटेंट जो बाद में ग्राफ़िक्स स्टेट `GS0` को रेफ़र करता है (उदाहरण के लिए, `/GS0 gs` के साथ ड्रॉ किया गया आयत) **50 % फ़िल अपारदर्शिता** के साथ दिखेगा जबकि स्ट्रोक पूरी तरह अपारदर्शी रहेगा। यदि आप Aspose.Pdf के `Page.Contents.Add` API के माध्यम से ऐसे ड्रॉइंग कमांड्स जोड़ते हैं, तो आप तुरंत ट्रांसपेरेंसी इफ़ेक्ट देखेंगे।

## कई पेज और कई ग्राफ़िक्स स्टेट्स को संभालना

- **कई पेज:** `pdfDocument.Pages` पर लूप करें और प्रत्येक पेज के लिए चरण 2‑5 दोहराएँ। यदि पेजों को अलग‑अलग अपारदर्शिता स्तर चाहिए तो अलग स्टेट नाम (`GS1`, `GS2`, …) उपयोग करें।
- **मौजूदा स्टेट का पुन: उपयोग:** यदि PDF में पहले से `"GS0"` नाम का स्टेट मौजूद है और आप केवल उसकी अपारदर्शिता बदलना चाहते हैं, तो नई एंट्री बनाने के बजाय `extGStateDict["GS0"]` से उसे प्राप्त करें।
- **परफ़ॉर्मेंस टिप:** बहुत सारे ग्राफ़िक्स स्टेट्स जोड़ने से फ़ाइल साइज बढ़ सकता है। समान अपारदर्शिता सेटिंग्स को एक ही स्टेट में कंसॉलिडेट करें और कई पेजों से रेफ़र करें।

## सामान्य समस्याएँ और उनका समाधान

| समस्या | कारण | समाधान |
|-------|-------|-----|
| `"ExtGState"` पर `KeyNotFoundException` | PDF में डिक्शनरी नहीं है। | चरण 3 में दिखाए अनुसार नई बनाएं। |
| ट्रांसपेरेंसी दिखाई नहीं दे रही | कंटेंट स्ट्रीम नया स्टेट रेफ़र नहीं कर रहा। | ड्रॉइंग कमांड्स से पहले `/GS0 gs` डालें या `Graphics` API के साथ `GraphicsState` पैरामीटर उपयोग करें। |
| आउटपुट PDF भ्रष्ट है | रीड‑ओनली फ़ोल्डर में सहेजने की कोशिश। | सुनिश्चित करें कि गंतव्य पाथ लिखने योग्य है और वही फ़ाइल अभी भी खुली नहीं है। |
| अपारदर्शिता मान 1 से बड़ा या 0 से छोटा | प्रतिशत के बजाय अंश पास कर दिया। | मानों को `0.0` से `1.0` के बीच रखें। |

## अगले कदम

अब जब आप **अपारदर्शिता बदलना** और **ट्रांसपेरेंसी जोड़ना** जानते हैं, तो आप संबंधित विषयों का अन्वेषण कर सकते हैं:

- `Image` ऑब्जेक्ट्स और `Transparency` प्रॉपर्टी का उपयोग करके **इमेजेज़ में ट्रांसपेरेंसी जोड़ना**।
- कई PDFs को मर्ज करना जबकि ग्राफ़िक्स स्टेट्स को संरक्षित रखना।
- `PdfSaveOptions` जैसे **संशोधित PDF** विकल्पों का उपयोग करके परिणाम को कंप्रेस या एन्क्रिप्ट करना।

विभिन्न `ca` और `CA` मान, `"Multiply"` या `"Screen"` जैसे ब्लेंड मोड आज़माएँ, और देखें कि वे विज़ुअल आउटपुट को कैसे प्रभावित करते हैं। यहाँ कवर की गई तकनीकें उन्नत PDF स्टाइलिंग के लिए एक ठोस आधार बनाती हैं।

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}