---
category: general
date: 2026-10-13
description: Aspose.Pdf for C# के साथ PDF में पारदर्शिता सेट करना सीखें। साथ ही देखें
  कि संशोधित PDF को कैसे सहेजें और फ़िल अल्फा को कैसे बदलें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: hi
lastmod: 2026-10-13
og_description: Aspose.Pdf for C# के साथ PDF में पारदर्शिता कैसे सेट करें। इस गाइड
  का पालन करके PDF संसाधनों को संपादित करें, फ़िल अल्फा बदलें, और संशोधित PDF फ़ाइलें
  सहेजें।
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Aspose.Pdf C# के साथ PDF में पारदर्शिता कैसे सेट करें – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Aspose.Pdf C# के साथ PDF में पारदर्शिता कैसे सेट करें
url: /hi/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf C# के साथ PDF में पारदर्शिता कैसे सेट करें

यदि आपको C# का उपयोग करके PDF में पारदर्शिता सेट करनी है, तो यह ट्यूटोरियल सटीक चरण दिखाता है। आप यह भी सीखेंगे कि संशोधित PDF फ़ाइलें कैसे सहेजें और Aspose.Pdf वातावरण से बाहर निकले बिना fill alpha कैसे बदलें।

यह गाइड दस्तावेज़ लोड करने, PDF संसाधनों को संपादित करने, fill opacity को परिभाषित करने वाला ग्राफ़िक्स स्टेट बनाने और बदलावों को स्थायी बनाने की प्रक्रिया को दर्शाता है। कोई बाहरी टूल आवश्यक नहीं है; सब कुछ एक मानक .NET प्रोजेक्ट के भीतर चलता है।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

* .NET 6.0 या बाद का संस्करण स्थापित हो  
* Aspose.Pdf for .NET का वैध लाइसेंस (या एक मुफ्त इवैल्यूएशन कुंजी)  
* ज्ञात डायरेक्टरी में स्थित इनपुट PDF फ़ाइल  

आप NuGet के माध्यम से Aspose.Pdf पैकेज जोड़ सकते हैं:

```bash
dotnet add package Aspose.Pdf
```

## PDF में पारदर्शिता कैसे सेट करें

यह सेक्शन मुख्य कार्यान्वयन को दर्शाता है। प्रत्येक चरण यह समझाता है **क्यों** कोड आवश्यक है, न कि केवल **क्या** करता है।

### चरण 1: PDF दस्तावेज़ लोड करें

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*इस चरण का कारण क्या है?*  
`Document` मेमोरी में संपूर्ण PDF फ़ाइल का प्रतिनिधित्व करता है। फ़ाइल खोलने से आपको पेज, संसाधन और लो‑लेवल ऑब्जेक्ट्स तक पहुंच मिलती है जिन्हें आप संशोधित करेंगे।

### चरण 2: ग्राफ़िक्स स्टेट जोड़ने के लिए PDF संसाधनों को संपादित करें

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*इस चरण का कारण क्या है?*  
PDF पेज पुन: उपयोग योग्य ऑब्जेक्ट्स—फ़ॉन्ट, इमेज और ग्राफ़िक्स स्टेट्स—को एक रिसोर्स डिक्शनरी में संग्रहीत करते हैं। `ExtGState` एंट्री में पारदर्शिता सेटिंग्स होती हैं। इस डिक्शनरी को संपादित करके आप एक नया स्टेट पेश कर सकते हैं जिसे पेज संदर्भित कर सके।

### चरण 3: fill alpha बदलें और fill opacity सेट करें

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*इस चरण का कारण क्या है?*  
`ca` **fill opacity** को नियंत्रित करता है, जबकि `CA` **stroke opacity** को। `ca` को `0.5` सेट करने से भरे हुए आकार 50 % पारदर्शी हो जाते हैं। `BM` एंट्री ब्लेंड मोड चुनती है; `"Normal"` मानक पारदर्शिता के लिए सबसे आम विकल्प है।

### चरण 4: नए ग्राफ़िक्स स्टेट को ExtGState डिक्शनरी में जोड़ें

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*इस चरण का कारण क्या है?*  
ग्राफ़िक्स स्टेट को `"GS0"` नाम देने से पेज की कंटेंट स्ट्रीम इसे `gs` ऑपरेटर के साथ संदर्भित कर सकती है। इस पंजीकरण के बाद पेज वह पारदर्शिता लागू कर सकता है जिसे आपने अभी परिभाषित किया है।

### चरण 5: (वैकल्पिक) कंटेंट स्ट्रीम में ग्राफ़िक्स स्टेट लागू करें

यदि आप नए fill opacity के साथ एक आयत बनाना चाहते हैं, तो पिछले चरणों के बाद निम्नलिखित जोड़ें:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*इस चरण का कारण क्या है?*  
`q`/`Q` ऑपरेटर्स ग्राफ़िक्स स्टेट को सहेजते और पुनर्स्थापित करते हैं, जिससे पारदर्शिता केवल इच्छित ड्रॉइंग कमांड्स पर प्रभाव डालती है। `gs` ऑपरेटर `"GS0"` नामक ग्राफ़िक्स स्टेट पर स्विच करता है।

### चरण 6: संशोधित PDF सहेजें

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*इस चरण का कारण क्या है?*  
सेव करने से अपडेटेड रिसोर्स डिक्शनरी और किसी भी नई कंटेंट स्ट्रीम को डिस्क पर लिखा जाता है। परिणामी फ़ाइल (`output.pdf`) में पिछले चरण में परिभाषित पारदर्शी आयत शामिल होगी।

## पूर्ण चलाने योग्य उदाहरण

सभी हिस्सों को मिलाकर, यहाँ एक पूरा प्रोग्राम है जिसे आप कंपाइल और रन कर सकते हैं:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**अपेक्षित परिणाम** – `output.pdf` एक आयत दिखाता है जो हल्के बैंगनी रंग से भरा है और 50 % पारदर्शी है, जिससे कोई भी पृष्ठभूमि सामग्री आंशिक रूप से दिखाई देती है।

## सामान्य प्रश्न और किनारे के मामले

* **क्या मैं fill opacity के बजाय stroke opacity बदल सकता हूँ?**  
  `CA` (बड़े अक्षर) का मान `0` (पूरी तरह से पारदर्शी) से `1` (पूरी तरह से अपारदर्शी) के बीच किसी संख्या पर सेट करें। उदाहरण में `CA` पहले से ही `1` पर सेट है, जिसका अर्थ है स्ट्रोक अपारदर्शी रहता है।

* **यदि पेज में पहले से ExtGState डिक्शनरी नहीं है तो क्या होगा?**  
  `resourceEditor["ExtGState"]` स्वचालित रूप से एक खाली डिक्शनरी बना देगा। `"GS0"` जोड़ना उसी तरह काम करता है।

* **क्या ग्राफ़िक्स स्टेट कई पेजों में पुन: उपयोग योग्य है?**  
  हाँ। एक बार जब आप एंट्री को दस्तावेज़ की रिसोर्स डिक्शनरी में जोड़ देते हैं, तो कोई भी पेज जो `"GS0"` को संदर्भित करता है, वही पारदर्शिता सेटिंग्स प्राप्त करेगा।

* **यह तरीका उच्च‑स्तरीय `Graphics` API का उपयोग करने से कैसे अलग है?**  
  लो‑लेवल रिसोर्स डिक्शनरी को संपादित करने से आपको PDF के आंतरिक भागों पर सटीक नियंत्रण मिलता है और अतिरिक्त ऑब्जेक्ट्स को एम्बेड न करने के कारण फ़ाइल आकार छोटा रहता है।

## निष्कर्ष

अब आप **Aspose.Pdf for C# के साथ PDF में पारदर्शिता कैसे सेट करें** जानते हैं। ट्यूटोरियल ने PDF संसाधनों को संपादित करना, fill alpha बदलना, fill opacity सेट करना और संशोधित PDF को सहेजना कवर किया। इस आधार के साथ आप विभिन्न ब्लेंड मोड्स के साथ प्रयोग कर सकते हैं, टेक्स्ट पर पारदर्शिता लागू कर सकते हैं, या जटिल दस्तावेज़ों के लिए पुन: उपयोग योग्य ग्राफ़िक्स स्टेट बना सकते हैं।

### अगले कदम

* `BM` एंट्री बदलकर अन्य ब्लेंड मोड्स (`Multiply`, `Screen`, आदि) का अन्वेषण करें।  
* स्ट्रोक अल्फा (`CA`) को समायोजित करके अर्ध‑पारदर्शी आउटलाइन बनाएं।  
* कई ग्राफ़िक्स स्टेट्स को मिलाकर पुन: उपयोग योग्य विज़ुअल इफ़ेक्ट्स की लाइब्रेरी बनाएं।  

अपना परिणाम साझा करने या टिप्पणी में प्रश्न पूछने में संकोच न करें। Happy coding!

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}