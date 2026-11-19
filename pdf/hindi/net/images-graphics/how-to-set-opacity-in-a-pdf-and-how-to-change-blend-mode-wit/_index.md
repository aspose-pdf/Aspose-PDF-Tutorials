---
category: general
date: 2026-11-19
description: Aspose.Pdf का उपयोग करके PDF में अपारदर्शिता सेट करना और ब्लेंड मोड बदलना
  सीखें। पारदर्शी ग्राफिक्स के लिए चरण‑दर‑चरण C# गाइड।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set opacity
- how to change blend
- Aspose.Pdf graphics state
- PDF transparency C#
- modify PDF resources
language: hi
lastmod: 2026-11-19
og_description: Aspose.Pdf का उपयोग करके PDF में अपारदर्शिता कैसे सेट करें और ब्लेंड
  मोड कैसे बदलें। ग्राफिक्स को पारदर्शी बनाने के लिए इस पूर्ण C# ट्यूटोरियल का पालन
  करें।
og_image_alt: Code editor showing C# example that sets PDF opacity and blend mode
og_title: Aspose.Pdf के साथ PDF में अपारदर्शिता सेट करने और ब्लेंड मोड बदलने का तरीका
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to set opacity and how to change blend mode in a PDF using
    Aspose.Pdf. Step‑by‑step C# guide for transparent graphics.
  headline: How to set opacity in a PDF and how to change blend mode with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: PDF में अपारदर्शिता कैसे सेट करें और Aspose.Pdf के साथ ब्लेंड मोड कैसे बदलें
url: /hi/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF में Aspose.Pdf के साथ अपारदर्शिता कैसे सेट करें और ब्लेंड मोड कैसे बदलें

यदि आपको PDF के भीतर ऑब्जेक्ट्स के लिए **how to set opacity** सेट करने की आवश्यकता है, तो यह गाइड सटीक चरण दिखाता है। यह **how to change blend** मोड को भी कवर करता है ताकि नया ग्राफ़िक्स स्टेट पेज कंटेंट के साथ सही ढंग से मिश्रित हो।

इस ट्यूटोरियल में आप करेंगे:

* Aspose.Pdf के साथ मौजूदा PDF लोड करें।
* पेज के रिसोर्स डिक्शनरी तक पहुंचें।
* एक नया ग्राफ़िक्स स्टेट डिक्शनरी बनाएं जो स्ट्रोक अपारदर्शिता, फ़िल अपारदर्शिता, और ब्लेंड मोड को परिभाषित करता है।
* `ExtGState` कलेक्शन में ग्राफ़िक्स स्टेट जोड़ें।
* अपडेटेड PDF सहेजें।

कोई बाहरी टूल आवश्यक नहीं है—केवल Aspose.Pdf for .NET लाइब्रेरी और एक .NET विकास वातावरण।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.6+ के साथ भी काम करता है)।
* Aspose.Pdf for .NET NuGet पैकेज (`Install-Package Aspose.Pdf`)।
* `input.pdf` नामक PDF फ़ाइल जो लिखने योग्य फ़ोल्डर में स्थित हो ( `YOUR_DIRECTORY` को अपने वास्तविक पथ से बदलें)।

## चरण 1: Aspose.Pdf स्थापित करें और प्रोजेक्ट सेट अप करें

एक नया कंसोल प्रोजेक्ट बनाएं और Aspose.Pdf रेफ़रेंस जोड़ें:

```bash
dotnet new console -n PdfOpacityDemo
cd PdfOpacityDemo
dotnet add package Aspose.Pdf
```

प्रोजेक्ट फ़ाइल में अब Aspose.Pdf असेंबली शामिल है, जो बाद में उपयोग किए जाने वाले `Document`, `DictionaryEditor`, और `CosPdfDictionary` क्लासेज़ प्रदान करती है।

## चरण 2: PDF दस्तावेज़ लोड करें

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

// Load the existing PDF
Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

**क्यों यह महत्वपूर्ण है:** दस्तावेज़ को लोड करने से एक इन‑मेमोरी प्रतिनिधित्व बनता है जिसे आप संशोधित कर सकते हैं। इस चरण के बिना रिसोर्स डिक्शनरीज़ तक पहुंच नहीं हो पाएगी।

## चरण 3: पहला पेज और उसकी रिसोर्स डिक्शनरी प्राप्त करें

```csharp
// Retrieve the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Open the page’s resource dictionary for editing
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

**व्याख्या:** `Resources` डिक्शनरी में फ़ॉन्ट्स, इमेजेज़, और `ExtGState` कलेक्शन जैसे ऑब्जेक्ट्स होते हैं। इसे संपादित करने से आप नई ग्राफ़िक्स स्टेट्स जोड़ सकते हैं जो अपारदर्शिता और ब्लेंडिंग को नियंत्रित करती हैं।

## चरण 4: ExtGState डिक्शनरी तक पहुंचें (या बनाएं)

```csharp
// Try to get the existing ExtGState dictionary; create it if missing
CosPdfDictionary extGStateDict = null;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and add it to resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor["ExtGState"] = extGStateDict;
}
```

**यह चरण क्यों आवश्यक है:** `ExtGState` एंट्री ग्राफ़िक्स स्टेट ऑब्जेक्ट्स रखती है। यदि यह मौजूद नहीं है, तो नई एंट्रीज़ जोड़ने से पहले इसे बनाना होगा।

## चरण 5: अपारदर्शिता और ब्लेंड मोड के साथ नई ग्राफ़िक्स स्टेट बनाएं

```csharp
// Create a new empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Set stroke opacity (CA) – 1 = fully opaque, 0 = fully transparent
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Set fill opacity (ca) – 0.5 = 50 % transparent fill
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Set blend mode (BM) – "Normal" is the default; other options: Multiply, Screen, Overlay, etc.
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**यह समस्या कैसे हल करता है:**  
* `CA` स्ट्रोक किए गए पाथ्स (जैसे, लाइन्स) की अपारदर्शिता नियंत्रित करता है।  
* `ca` भरे हुए आकारों (जैसे, रेक्टेंगल्स) की अपारदर्शिता नियंत्रित करता है।  
* `BM` निर्धारित करता है कि नई ग्राफ़िक्स मौजूदा पेज कंटेंट के साथ कैसे संयोजित होती हैं। ब्लेंड मोड बदलना ठीक वही **how to change blend** है जो PDF के लिए आवश्यक है।

## चरण 6: ExtGState कलेक्शन में ग्राफ़िक्स स्टेट रजिस्टर करें

```csharp
// Use a unique key for the new graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

अब पेज इस ग्राफ़िक्स स्टेट को नाम `/GS0` के माध्यम से रेफ़र कर सकता है। कोई भी कंटेंट स्ट्रीम जो `/GS0 gs` सेट करता है, वह परिभाषित अपारदर्शिता और ब्लेंड मोड का उपयोग करेगा।

## चरण 7: मौजूदा कंटेंट पर ग्राफ़िक्स स्टेट लागू करें (वैकल्पिक)

यदि आप मौजूदा ड्रॉइंग कमांड्स को संशोधित करना चाहते हैं, तो आप ग्राफ़िक्स स्टेट ऑपरेटर को पेज की कंटेंट स्ट्रीम की शुरुआत में जोड़ सकते हैं:

```csharp
// Retrieve the content stream as a string
string pageContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string modifiedContent = "GS0 gs\n" + pageContent;

// Replace the original content
firstPage.Contents[1].Replace(modifiedContent);
```

**नोट:** यह चरण वैकल्पिक है। यदि आप बाद में नई ड्रॉइंग कमांड्स जोड़ते हैं, तो बस स्ट्रीम को `GS0 gs` से शुरू करें।

## चरण 8: संशोधित PDF सहेजें

```csharp
pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");
```

परिणामी `out.pdf` में एक ग्राफ़िक्स स्टेट है जहाँ फ़िल अपारदर्शिता 50 % है और ब्लेंड मोड `Normal` है। कोई भी कंटेंट जो `/GS0 gs` का उपयोग करता है, वह निर्दिष्ट ट्रांसपेरेंसी के साथ रेंडर होगा।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप `Program.cs` में कॉपी‑पेस्ट करके चला सकते हैं:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

class Program
{
    static void Main()
    {
        // 1. Load the PDF document
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get the first page and its resource dictionary
        Page firstPage = pdfDocument.Pages[1];
        DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

        // 3. Access or create the ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourceEditor["ExtGState"] = extGStateDict;
        }

        // 4. Define a new graphics state with opacity and blend mode
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity (fully opaque)
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity (50 % transparent)
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode (Normal)

        // 5. Add the graphics state to ExtGState collection
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Apply the graphics state to existing page content
        if (firstPage.Contents.Count > 0)
        {
            string original = firstPage.Contents[1].ToString();
            string withGs = "GS0 gs\n" + original;
            firstPage.Contents[1].Replace(withGs);
        }

        // 7. Save the updated PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");

        Console.WriteLine("PDF updated successfully – opacity set and blend mode changed.");
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर यह प्रिंट करता है:

```
PDF updated successfully – opacity set and blend mode changed.
```

जब आप `out.pdf` को PDF व्यूअर में खोलते हैं, तो कोई भी आकार जो नई परिभाषित ग्राफ़िक्स स्टेट का उपयोग करता है, 50 % फ़िल ट्रांसपेरेंसी के साथ दिखेगा जबकि स्ट्रोक पूरी तरह अपारदर्शी रहेगा। ब्लेंड मोड `Normal` सुनिश्चित करता है कि ग्राफ़िक्स बिना विशेष प्रभावों के संयोजित हों। आप `"Normal"` को `"Multiply"` या `"Screen"` में बदल सकते हैं ताकि विभिन्न दृश्य परिणामों के लिए **how to change blend** देख सकें।

## सामान्य प्रश्न और किनारे के मामले

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मैं कई ऑब्जेक्ट्स के लिए अलग-अलग अपारदर्शिता मान सेट कर सकता हूँ?** | हां। अतिरिक्त ग्राफ़िक्स स्टेट्स (जैसे, `GS1`, `GS2`) अलग-अलग `ca`/`CA` मानों के साथ बनाएं और प्रत्येक ऑब्जेक्ट को ड्रॉ करने से पहले उपयुक्त नाम का रेफ़रेंस दें। |
| **यदि PDF में पहले से ही `GS0` नाम का `ExtGState` एंट्री मौजूद है तो क्या करें?** | एक अद्वितीय कुंजी (`GS1`, `MyOpacityState`, आदि) चुनें या यदि पुराना परिभाषा अब आवश्यक नहीं है तो मौजूदा एंट्री को ओवरराइट करें। |
| **क्या ब्लेंड मोड केवल `Normal` तक सीमित है?** | नहीं। वैध नामों में `Multiply`, `Screen`, `Overlay`, `Darken`, `Lighten`, `ColorDodge`, `ColorBurn`, `HardLight`, `SoftLight`, `Difference`, `Exclusion`, तथा `Hue`, `Saturation`, `Color`, `Luminosity` शामिल हैं। |
| **क्या यह एन्क्रिप्टेड PDFs के साथ काम करता है?** | Aspose.Pdf एन्क्रिप्टेड PDFs को खोल सकता है यदि आप पासवर्ड `Document(string, LoadOptions)` के माध्यम से प्रदान करते हैं। डिक्रिप्शन के बाद ग्राफ़िक्स‑स्टेट में परिवर्तन वही रहता है। |
| **क्या परिवर्तन सभी पेजों को प्रभावित करेंगे?** | उदाहरण केवल पहले पेज को संशोधित करता है। सभी पेजों को प्रभावित करने के लिए, `pdfDocument.Pages` पर लूप करें और प्रत्येक पेज के लिए चरण 2‑6 दोहराएँ। |

## प्रो टिप्स

* **ग्राफ़िक्स स्टेट्स को पुन: उपयोग करें:** एक बार ग्राफ़िक्स स्टेट जोड़ने और इसे कई पेजों पर रेफ़र करने से फ़ाइल आकार कम होता है।
* **परफ़ॉर्मेंस:** बड़े PDFs को मेमोरी में संशोधित करना मेमोरी‑गहन हो सकता है। यदि आपको केवल छोटे परिवर्तन चाहिए तो `pdfDocument.Save(..., SaveOptions)` को इन्क्रिमेंटल अपडेट के साथ उपयोग करें।
* **ब्लेंड मोड्स का परीक्षण:** सभी PDF व्यूअर्स हर ब्लेंड मोड को समान रूप से रेंडर नहीं करते। विज़ुअल कंसिस्टेंसी सत्यापित करने के लिए आउटपुट को Adobe Acrobat Reader और किसी वैकल्पिक व्यूअर (जैसे, Foxit) में टेस्ट करें।

## निष्कर्ष

अब आप Aspose.Pdf for .NET का उपयोग करके PDF में **how to set opacity** और **how to change blend** मोड कैसे सेट करें, यह जानते हैं। `ExtGState` डिक्शनरी को संपादित करके आप ट्रांसपेरेंसी और कॉम्पोज़िटिंग पर सूक्ष्म नियंत्रण प्राप्त करते हैं, जिससे बाहरी टूल्स के बिना प्रोफेशनल‑ग्रेड PDF ग्राफ़िक्स संभव होते हैं।

अगला, आप निम्नलिखित का अन्वेषण कर सकते हैं:

* पारदर्शी बैकग्राउंड वाली इमेजेज़ जोड़ना (`how to set opacity` इमेजेज़ पर)।
* पुन: उपयोग योग्य कंटेंट स्ट्रीम बनाना जो नई ग्राफ़िक्स स्टेट को रेफ़र करता है।
* अन्य ब्लेंड मोड्स का उपयोग करना (`how to change blend` को `Multiply` या `Screen` में बदलना) रचनात्मक प्रभावों के लिए।

कोडिंग का आनंद लें, और अपने PDFs को अधिक दृश्य रूप से गतिशील बनाते हुए मज़ा लें!

## आगे आप क्या सीखें

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच का अन्वेषण करने में मदद करती हैं।

- [Aspose.PDF के साथ PDF में अपारदर्शिता कैसे बदलें – पूर्ण गाइड](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/)
- [Aspose.Pdf for .NET के साथ PDF में अपारदर्शिता कैसे बदलें](/pdf/english/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/)
- [C# में Aspose.Pdf का उपयोग करके PDF ट्रांसपेरेंसी कैसे बदलें](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}