---
category: general
date: 2026-09-08
description: Aspose.PDF for .NET के साथ PDF में पारदर्शिता जोड़ें – स्ट्रोक और फ़िल
  अपारदर्शिता, ब्लेंड मोड सेट करना सीखें, और मिनटों में परिणाम सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- aspose.pdf transparency
- pdf graphics state
- extgstate dictionary
- pdf opacity settings
language: hi
lastmod: 2026-09-08
og_description: Aspose.PDF for .NET का उपयोग करके PDF में पारदर्शिता जोड़ें। यह ट्यूटोरियल
  दिखाता है कि ExtGState डिक्शनरी को कैसे संशोधित करें, अपारदर्शिता और ब्लेंड मोड
  सेट करें, और अपडेटेड फ़ाइल को सहेजें।
og_image_alt: Screenshot of a PDF page showing semi‑transparent shapes created with
  Aspose.PDF
og_title: Aspose.PDF के साथ PDF में ट्रांसपेरेंसी जोड़ें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Add transparency to PDF with Aspose.PDF for .NET – learn to set stroke
    and fill opacity, blend mode, and save the result in minutes.
  headline: How to add transparency to PDF files using Aspose.PDF for .NET
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Aspose.PDF for .NET का उपयोग करके PDF फ़ाइलों में पारदर्शिता कैसे जोड़ें
url: /hi/net/images-graphics/how-to-add-transparency-to-pdf-files-using-aspose-pdf-for-ne/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF for .NET का उपयोग करके PDF फ़ाइलों में पारदर्शिता कैसे जोड़ें

यदि आपको **PDF में पारदर्शिता जोड़नी** है, यह गाइड आपको बिल्कुल दिखाएगा कि Aspose.PDF for .NET के साथ ग्राफ़िक्स स्टेट को कैसे संशोधित किया जाए। आप एक पृष्ठ पर स्ट्रोक अपारदर्शिता, फ़िल अपारदर्शिता, और ब्लेंड मोड सेट करना सीखेंगे, फिर परिणाम को नई फ़ाइल के रूप में सहेजेंगे।

पारदर्शिता वॉटरमार्क, ओवरले ग्राफ़िक्स, या रिपोर्ट में दृश्य प्रभावों के लिए एक सामान्य आवश्यकता है। इस ट्यूटोरियल में आप पूरा, चलाने योग्य कोड देखेंगे, प्रत्येक API कॉल क्यों महत्वपूर्ण है समझेंगे, और गुम संसाधन प्रविष्टियों जैसी किनारी मामलों को संभालने के टिप्स प्राप्त करेंगे।

## आपको क्या चाहिए

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.6+ के साथ भी काम करता है)
* एक वैध Aspose.PDF for .NET लाइसेंस (टेस्टिंग के लिए मुफ्त ट्रायल काम करता है)
* `input.pdf` नामक इनपुट PDF, जिसे आप कोड से संदर्भित कर सकें ऐसे फ़ोल्डर में रखें
* एक C# विकास वातावरण (Visual Studio, Rider, या VS Code)

`Aspose.Pdf` के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है।

## PDF ग्राफ़िक्स स्टेट का अवलोकन

PDF ग्राफ़िक्स स्टेट एक पृष्ठ के रिसोर्स डिक्शनरी के भीतर **ExtGState डिक्शनरी** में संग्रहीत होती है। प्रत्येक प्रविष्टि रेंडरिंग पैरामीटर जैसे लाइन चौड़ाई, अपारदर्शिता, और ब्लेंड मोड को परिभाषित करती है। एक नया ग्राफ़िक्स स्टेट ऑब्जेक्ट बनाकर और उसे `ExtGState` डिक्शनरी में जोड़कर आप कई ड्रॉइंग कमांड्स में समान पारदर्शिता सेटिंग्स को पुन: उपयोग कर सकते हैं।

इस संरचना को समझने से आप सामान्य समस्याओं से बच सकते हैं, जैसे `Page` ऑब्जेक्ट पर सीधे अपारदर्शिता सेट करने की कोशिश (जिसका समर्थन API नहीं करता)। इसके बजाय, आप निम्न‑स्तरीय COS ऑब्जेक्ट्स के साथ काम करते हैं जो PDF विशिष्टीकरण के साथ एक‑से‑एक मैप होते हैं।

## चरण 1: PDF दस्तावेज़ लोड करें

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Cos;

// Load the source PDF
var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");
```

*इस चरण का उद्देश्य क्या है?*  
`Document` किसी भी PDF हेरफेर का प्रवेश बिंदु है। फ़ाइल को लोड करने से एक इन‑मेमोरी प्रतिनिधित्व बनता है जिसे आप डिस्क पर मूल फ़ाइल को छुए बिना संपादित कर सकते हैं।

## चरण 2: पहला पृष्ठ और उसका रिसोर्स डिक्शनरी एडिटर प्राप्त करें

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor provides convenient access to the page’s resources
var resourceEditor = new DictionaryEditor(page.Resources);
```

*इस चरण का उद्देश्य क्या है?*  
सभी ग्राफ़िक्स‑स्टेट प्रविष्टियां पृष्ठ के रिसोर्सेज के अंदर रहती हैं। `DictionaryEditor` निम्न‑स्तरीय COS डिक्शनरी हैंडलिंग को एब्स्ट्रैक्ट करता है, जिससे आप `ExtGState` जैसी प्रविष्टियों को पढ़ या बना सकते हैं।

## चरण 3: पृष्ठ संसाधनों से ExtGState डिक्शनरी प्राप्त करें

```csharp
// The ExtGState entry may already exist; if not, create it
CosPdfDictionary extGStateDict;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a new ExtGState dictionary and attach it to the page resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourceEditor.Add("ExtGState", extGStateDict);
}
```

*इस चरण का उद्देश्य क्या है?*  
PDF पूरी तरह से `ExtGState` डिक्शनरी को छोड़ सकता है। ऊपर दिया गया कोड दोनों मौजूदा और अनुपस्थित मामलों को सुरक्षित रूप से संभालता है, जिससे ट्यूटोरियल किसी भी इनपुट PDF के साथ काम करता है।

## चरण 4: एक नया ग्राफ़िक्स स्टेट डिक्शनरी बनाएं और उसकी प्रविष्टियों को परिभाषित करें

```csharp
// Create an empty dictionary that will hold our transparency settings
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Define the entries:
//   CA – stroke opacity (0 = fully transparent, 1 = opaque)
//   ca – fill opacity
//   BM – blend mode (Normal, Multiply, etc.)
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity = 100%
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity = 50%
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Standard blend mode
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*इस चरण का उद्देश्य क्या है?*  
`CA` और `ca` PDF ऑपरेटर हैं जो स्ट्रोकिंग और नॉन‑स्ट्रोकिंग (फ़िल) ऑपरेशनों के लिए अपारदर्शिता को नियंत्रित करते हैं। `BM` को `Normal` सेट करने से डिफ़ॉल्ट कॉम्पोज़िटिंग व्यवहार बना रहता है, लेकिन आप कलात्मक प्रभावों के लिए `Multiply` या `Screen` के साथ प्रयोग कर सकते हैं।

## चरण 5: नया ग्राफ़िक्स स्टेट ExtGState डिक्शनरी में जोड़ें

```csharp
// Choose a unique name for the graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

*इस चरण का उद्देश्य क्या है?*  
नाम `GS0` एक संदर्भ बन जाता है जिसे आप बाद में कंटेंट स्ट्रीम (`/GS0 gs`) में उपयोग कर सकते हैं। इसे `ExtGState` में जोड़ने से PDF नई पारदर्शिता पैरामीटर को पहचानता है।

## चरण 6: कंटेंट स्ट्रीम में ग्राफ़िक्स स्टेट लागू करें (वैकल्पिक)

यदि आप प्रभाव को तुरंत देखना चाहते हैं, तो आप एक सरल ड्रॉइंग कमांड को प्रीपेंड कर सकते हैं जो नई स्टेट का उपयोग करता है:

```csharp
// Build a content stream that draws a semi‑transparent rectangle
var content = new PageContent();
content.Operators.Add(new Operator("q"));                     // Save graphics state
content.Operators.Add(new Operator("GS0", "gs"));            // Set our custom graphics state
content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg")); // Set fill color (light blue)
content.Operators.Add(new Operator("100", "500", "200", "100", "re")); // Rectangle
content.Operators.Add(new Operator("f"));                    // Fill
content.Operators.Add(new Operator("Q"));                     // Restore graphics state

// Insert the new content at the beginning of the page
page.Contents.Insert(0, content);
```

*इस चरण का उद्देश्य क्या है?*  
वैकल्पिक स्निपेट दर्शाता है कि आपने जो ग्राफ़िक्स स्टेट (`GS0`) जोड़ी है, वह वास्तव में कैसे उपयोग होती है। आयत 50 % फ़िल अपारदर्शिता के साथ दिखाई देगा जबकि उसका स्ट्रोक पूरी तरह अपारदर्शी रहेगा।

## चरण 7: संशोधित PDF दस्तावेज़ सहेजें

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

परिणामी फ़ाइल, `output.pdf`, नई `ExtGState` प्रविष्टि रखती है और यदि आपने वैकल्पिक कंटेंट जोड़ा है तो एक अर्ध‑पारदर्शी आयत ओवरले भी शामिल करता है।

### अपेक्षित आउटपुट

जब आप `output.pdf` को Adobe Acrobat Reader या किसी भी PDF व्यूअर में खोलते हैं, तो आपको दिखना चाहिए:

* मूल पृष्ठ सामग्री अपरिवर्तित रहती है।
* यदि आपने वैकल्पिक ड्रॉइंग कोड चलाया है, तो एक हल्का‑नीला आयत जिसका फ़िल 50 % पारदर्शी है, जिससे नीचे का पृष्ठ दिखता है।

## पूरा स्रोत सूची

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class AddTransparencyExample
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2. Get the first page and its resources
        var page = pdfDoc.Pages[1];
        var resourceEditor = new DictionaryEditor(page.Resources);

        // 3. Retrieve or create ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
            extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            resourceEditor.Add("ExtGState", extGStateDict);
        }

        // 4. Create new graphics state with transparency settings
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // 5. Add the graphics state to ExtGState with a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Draw a rectangle using the new state
        var content = new PageContent();
        content.Operators.Add(new Operator("q"));
        content.Operators.Add(new Operator("GS0", "gs"));
        content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg"));
        content.Operators.Add(new Operator("100", "500", "200", "100", "re"));
        content.Operators.Add(new Operator("f"));
        content.Operators.Add(new Operator("Q"));
        page.Contents.Insert(0, content);

        // 7. Save the updated PDF
        pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

कोड को एक कंसोल एप्लिकेशन में कॉपी करें, `YOUR_DIRECTORY` को वास्तविक फ़ोल्डर पथ से बदलें, और चलाएँ। प्रोग्राम `output.pdf` उत्पन्न करेगा जिसमें जोड़ी गई पारदर्शिता सेटिंग्स होंगी।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| लक्षण | कारण | समाधान |
|---------|-------|-----|
| `KeyNotFoundException` on `"ExtGState"` | पृष्ठ में `ExtGState` प्रविष्टि नहीं है। | ट्यूटोरियल पहले से ही गायब होने पर डिक्शनरी बनाता है; सुनिश्चित करें कि आप प्रदान किए गए शर्तीय ब्लॉक का उपयोग करें। |
| Viewer में पारदर्शिता दिखाई नहीं देती | ड्रॉइंग कमांड्स कभी भी `GS0` को संदर्भित नहीं करते। | `gs` ऑपरेटर (`"GS0 gs"`) को किसी भी स्ट्रोकिंग/फ़िलिंग ऑपरेशन से पहले जोड़ें, जैसा कि वैकल्पिक स्निपेट में दिखाया गया है। |
| सेव करने के बाद PDF भ्रष्ट हो जाता है | उच्च‑स्तरीय `Page` API को निम्न‑स्तरीय COS ऑब्जेक्ट्स के साथ गलत तरीके से मिलाना। | `DictionaryEditor` के माध्यम से `CosPdfDictionary` प्राप्त करने के पैटर्न का पालन करें और एक ही डिक्शनरी को दो बार संशोधित करने से बचें। |
| ब्लेंड मोड का कोई प्रभाव नहीं है | व्यूअर चयनित ब्लेंड मोड का समर्थन नहीं करता। | व्यापक संगतता के लिए `Normal` का उपयोग करें; केवल उन व्यूअर्स में `Multiply` के साथ प्रयोग करें जो समर्थन की रिपोर्ट करते हैं। |

## अगले कदम

अब जब आप **PDF में पारदर्शिता जोड़ना** जानते हैं, तो आप:

* `pdfDoc.Pages` पर इटररेट करके कई पृष्ठों पर समान ग्राफ़िक्स स्टेट लागू करें।
* जटिल वॉटरमार्किंग के लिए क्लिपिंग पाथ्स के साथ पारदर्शिता को संयोजित करें।
* `SM` (स्ट्रोक समायोजन) या `CA` जैसी अन्य ExtGState प्रविष्टियों का अन्वेषण करें।

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकट संबंधी विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.PDF for .NET का उपयोग करके PDFs में टेक्स्ट स्टैम्प जोड़ना और संरेखित करना | वॉटरमार्क्स और बैकग्राउंड्स](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [Aspose.PDF for .NET का उपयोग करके PDFs में घूर्णन इमेज वॉटरमार्क जोड़ना](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [Aspose.PDF for .NET का उपयोग करके PDFs में पेज स्टैम्प जोड़ना: एक पूर्ण गाइड](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}