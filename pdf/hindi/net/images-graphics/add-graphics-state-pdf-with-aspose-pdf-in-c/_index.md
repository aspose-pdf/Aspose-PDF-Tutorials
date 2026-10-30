---
category: general
date: 2026-10-07
description: Aspose.Pdf का उपयोग करके C# में ग्राफ़िक्स स्टेट PDF जोड़ें ताकि PDF
  की पारदर्शिता को संशोधित किया जा सके। कस्टम ग्राफ़िक्स स्टेट्स को एम्बेड करने और
  अपारदर्शिता को नियंत्रित करने के लिए इस चरण‑दर‑चरण गाइड का पालन करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: hi
lastmod: 2026-10-07
og_description: C# में Aspose.Pdf के साथ ग्राफ़िक्स स्टेट PDF जोड़ें। कस्टम ग्राफ़िक्स
  स्टेट डिक्शनरी बनाकर PDF की पारदर्शिता को कैसे संशोधित करें, सीखें।
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Aspose.Pdf के साथ ग्राफ़िक्स स्टेट PDF जोड़ें – PDF पारदर्शिता नियंत्रित
  करें
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C# में Aspose.Pdf के साथ ग्राफ़िक्स स्टेट PDF जोड़ें
url: /hi/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add graphics state pdf with Aspose.Pdf in C#

यदि आपको दस्तावेज़ में **add graphics state pdf** जोड़ना है, तो यह ट्यूटोरियल आपको Aspose.Pdf for .NET के साथ इसे करने का सटीक तरीका दिखाता है। गाइड के अंत तक आप **modify PDF transparency** को भी समझ जाएंगे, जिससे आप किसी भी ड्रॉइंग ऑपरेशन पर कस्टम अपारदर्शिता मान सेट कर सकते हैं।

PDF ग्राफ़िक्स स्टेट्स के साथ काम करने से आप लाइन की चौड़ाई, ब्लेंड मोड, और इस लेख के लिए सबसे महत्वपूर्ण—कंटेंट की पारदर्शिता—जैसे पैरामीटर नियंत्रित कर सकते हैं। नीचे दिए गए चरण उन डेवलपर्स के लिए लिखे गए हैं जो C# में सहज हैं और आधिकारिक SDK दस्तावेज़ों को गहराई से पढ़े बिना तैयार‑से‑चलाने वाला समाधान चाहते हैं।

## What you’ll learn

* नई ग्राफ़िक्स स्टेट डिक्शनरी बनाना और उसमें `CA`, `ca`, और `BM` एंट्रीज़ जोड़ना।  
* उस डिक्शनरी को पेज के `ExtGState` रिसोर्स में डालना ताकि PDF उसे पहचान ले।  
* `ca` (stroke) और `CA` (fill) मानों का **modify PDF transparency** पर प्रभाव समझना, जिससे बाद के ड्रॉइंग कमांड्स पर असर पड़े।  
* नामकरण टकराव और संस्करण संगतता जैसी सामान्य समस्याएँ, साथ ही ग्राफ़िक्स स्टेट को बाद में विस्तारित करने के प्रो टिप्स।

**Prerequisites**

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)।  
* एक वैध Aspose.Pdf for .NET लाइसेंस (टेस्टिंग के लिए फ्री इवैल्यूएशन चलती है)।  
* Visual Studio 2022 या आपका पसंदीदा कोई भी C# IDE।  

---

## Step 1: Install Aspose.Pdf for .NET

अपने प्रोजेक्ट में NuGet पैकेज जोड़ें:

```bash
dotnet add package Aspose.Pdf
```

यह पैकेज `Aspose.Pdf` नेमस्पेस प्रदान करता है, जिसमें `Document`, `DictionaryEditor`, और `CosPdfDictionary` क्लासेज़ शामिल हैं, जो बाद में उपयोग होंगी।

> **Pro tip:** यदि आप बैच में कई PDFs प्रोसेस करने वाले हैं, तो `Program.cs` में **License** को जल्दी लोड करें ताकि इवैल्यूएशन वॉटरमार्क न आए।

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Step 2: Define input and output paths

आपको SDK को मौजूदा PDF (`input.pdf`) की ओर इशारा करना है और यह बताना है कि संशोधित फ़ाइल (`output.pdf`) कहाँ सेव होगी।

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Why this matters:** एब्सोल्यूट पाथ्स का उपयोग करने से SDK गलत वर्किंग डायरेक्टरी में खोज नहीं करेगा, जो `FileNotFoundException` का आम कारण है।

## Step 3: Open the PDF and locate the first page’s resources

`ExtGState` डिक्शनरी प्रत्येक पेज के रिसोर्स डिक्शनरी के अंदर रहती है। हम सरलता के लिए पहले पेज को एडिट करेंगे, लेकिन यही तरीका किसी भी पेज इंडेक्स के लिए काम करता है।

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Edge case:** यदि पेज में `ExtGState` एंट्री नहीं है, तो आपको इसे बनाना पड़ेगा:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Step 4: Build a new graphics state dictionary

ग्राफ़िक्स स्टेट एक की/वैल्यू पेयर का संग्रह है जो ड्रॉइंग ऑपरेशन्स के व्यवहार को परिभाषित करता है। पारदर्शिता के लिए हमें तीन कुंजियों की जरूरत है:

| कुंजी | अर्थ | सामान्य मान |
|------|------|-------------|
| `CA` | Fill opacity (0 = transparent, 1 = opaque) | `1` (पूरी तरह अपारदर्शी) |
| `ca` | Stroke opacity (same scale) | `0.5` (50 % transparent) |
| `BM` | Blend mode (e.g., `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Why these values?**  
`ca = 0.5` किसी भी स्ट्रोक्ड पाथ (लाइन, बॉर्डर) को 50 % अपारदर्शी बनाता है, जबकि `CA = 1` भराव वाले आकारों को पूरी तरह अपारदर्शी रखता है। अपनी इच्छित **modify PDF transparency** प्रभाव के अनुसार दोनों मानों को समायोजित करें।

## Step 5: Insert the graphics state into the ExtGState dictionary

आपको नई स्टेट को एक यूनिक नाम देना होगा (जैसे `GS0`)। यदि वही नाम पहले से मौजूद है, तो Aspose.Pdf मौजूदा एंट्री को ओवरराइट कर देगा, जिससे अन्य कंटेंट टूट सकता है।

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

अब पेज के रिसोर्सेज़ को `GS0` के बारे में पता चल गया है। इसे वास्तविक रूप से उपयोग करने के लिए, आप कंटेंट स्ट्रीम में `gs` ऑपरेटर (जैसे `GS0 gs`) के माध्यम से ग्राफ़िक्स स्टेट को रेफ़र करेंगे। Aspose.Pdf आपको कस्टम शैप्स ड्रॉ करने के लिए रॉ PDF ऑपरेटर्स इंजेक्ट करने की सुविधा देता है।

## Step 6: Save the modified PDF

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

परिणामी `output.pdf` मूल फ़ाइल के समान दृश्य कंटेंट रखता है, लेकिन कोई भी बाद का ड्रॉइंग कमांड जो `GS0` को चुनता है, वह आपके द्वारा परिभाषित पारदर्शिता सेटिंग्स को मानता है।

### Expected result

`output.pdf` को Adobe Acrobat या किसी भी PDF व्यूअर में खोलें। यदि आप `GS0` ग्राफ़िक्स स्टेट का उपयोग करके (जैसे `pdfDocument.Pages[1].Contents.Add(...)` द्वारा) एक नई स्ट्रोक्ड लाइन जोड़ते हैं, तो वह अर्ध‑पारदर्शी दिखेगी जबकि भराव अपारदर्शी रहेगा। यह दर्शाता है कि आपने सफलतापूर्वक **add graphics state pdf** और **modify PDF transparency** को लागू किया है।

---

## Full runnable example

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉन्सोल एप्लिकेशन में कॉपी‑पेस्ट कर सकते हैं। इसमें लाइसेंस लोड करना, एरर हैंडलिंग, और प्रत्येक गैर‑स्पष्ट चरण की व्याख्या करने वाले कमेंट्स शामिल हैं।

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Add Transparency to PDF with Aspose PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}