---
category: general
date: 2026-10-01
description: Aspose.PDF का उपयोग करके कस्टम ExtGState PDF जोड़ें और शीघ्रता से ट्रांसपैरेंसी
  सेट करें। इस गाइड का पालन करके जानें कि कस्टम ग्राफ़िक्स स्टेट के साथ ट्रांसपैरेंसी
  PDF कैसे सेट करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom extgstate pdf
- how to set transparency pdf
- Aspose.PDF graphics state
- PDF opacity settings
- PDF blend mode tutorial
language: hi
lastmod: 2026-10-01
og_description: कस्टम ExtGState PDF जोड़ें और कुछ ही C# लाइनों में ट्रांसपेरेंसी PDF
  सेट करना सीखें। यह गाइड फ़ाइल लोड करने से लेकर परिणाम सहेजने तक हर कदम को कवर करता
  है।
og_image_alt: Screenshot of a PDF page showing transparent graphics after adding a
  custom ExtGState
og_title: कस्टम ExtGState PDF जोड़ें – पूर्ण Aspose.PDF ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add custom ExtGState PDF using Aspose.PDF to set transparency PDF quickly.
    Follow this guide to learn how to set transparency PDF with a custom graphics
    state.
  headline: Add custom ExtGState PDF with Aspose.PDF – step‑by‑step guide
  type: TechArticle
tags:
- PDF
- Aspose.PDF
- C#
- GraphicsState
title: Aspose.PDF के साथ कस्टम ExtGState PDF जोड़ें – चरण‑दर‑चरण गाइड
url: /hi/net/images-graphics/add-custom-extgstate-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF के साथ कस्टम ExtGState PDF जोड़ें – चरण‑दर‑चरण गाइड

यदि आपको अपारदर्शिता और ब्लेंड मोड को नियंत्रित करने के लिए **कस्टम ExtGState PDF** जोड़ने की आवश्यकता है, तो यह ट्यूटोरियल आपको ठीक‑ठीक दिखाता है। आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जो Aspose.PDF for .NET का उपयोग करके **PDF में पारदर्शिता कैसे सेट करें** दर्शाता है।

आगे के अनुभागों में हम आवश्यक NuGet पैकेज, कोड‑बाय‑कोड विवरण, और कई पृष्ठों या कस्टम ब्लेंड मोड जैसे किनारे के मामलों को संभालने के टिप्स को कवर करेंगे। अंत तक आप किसी भी मौजूदा PDF को संशोधित करके बिना IDE छोड़े एक पारदर्शी ग्राफ़िक्स स्टेट लागू कर पाएँगे।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)
- Visual Studio 2022 (या कोई भी पसंदीदा C# एडिटर)
- **Aspose.PDF for .NET** NuGet पैकेज (संस्करण 23.12 या नया)
- एक सैंपल PDF फ़ाइल जिसका नाम `input.pdf` है, जिसे आप प्रोजेक्ट से रेफ़रेंस कर सकें

> **Pro tip:** अपने सॉल्यूशन में एक समर्पित “Resources” फ़ोल्डर रखें ताकि इनपुट और आउटपुट PDFs एक साथ रखे जा सकें। इससे कोड चलाते समय पाथ‑संबंधी त्रुटियों से बचा जा सकता है।

## Install Aspose.PDF

NuGet Package Manager कंसोल खोलें और चलाएँ:

```bash
dotnet add package Aspose.PDF
```

यह पैकेज `Aspose.Pdf.Document`, `CosPdfDictionary`, और कोड नमूने में उपयोग की गई संबंधित क्लासेस प्रदान करता है।

## Step 1 – Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;

// Load the source PDF
using var pdfDocument = new Document("Resources/input.pdf");
```

**Why this step matters:**  
`Document` पूरी PDF फ़ाइल को मेमोरी में दर्शाता है। इसे `using` ब्लॉक के साथ खोलने से सभी अनमैनेज्ड रिसोर्सेज़ प्रोसेसिंग समाप्त होने के बाद रिलीज़ हो जाते हैं।

## Step 2 – Access the first page’s resource dictionary

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// The resource dictionary holds objects like fonts, XObjects, and ExtGState entries
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**Explanation:**  
हर PDF पेज का एक *Resources* डिक्शनरी होता है जो पुन: उपयोग योग्य ऑब्जेक्ट्स को समूहित करता है। इस डिक्शनरी को एडिट करके हम एक नया ग्राफ़िक्स स्टेट इंजेक्ट कर सकते हैं जिसे पेज बाद में रेफ़र कर सके।

## Step 3 – Retrieve (or create) the ExtGState dictionary

```csharp
// Try to get the existing ExtGState dictionary; create one if it does not exist
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

**Why we check first:**  
कुछ PDFs पहले से ही एक `ExtGState` एंट्री परिभाषित कर चुके होते हैं। डुप्लिकेट जोड़ने से मौजूदा स्टेट्स ओवरराइट हो सकते हैं और अन्य कंटेंट टूट सकता है। यह डिफेन्सिव कोड मूल एंट्रीज़ को बरकरार रखता है।

## Step 4 – Build a custom graphics state

```csharp
// Create an empty dictionary that will become our custom graphics state
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // CA – stroke opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // ca – fill opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // BM – blend mode (Normal, Multiply, Screen, etc.)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Add each entry to the dictionary
foreach (var entry in graphicsStateEntries)
{
    newGraphicsState.Add(entry);
}
```

**What each key does:**

| Key | Meaning | Typical values |
|-----|---------|----------------|
| `CA` | Stroke opacity | `0.0` (पूरी तरह पारदर्शी) → `1.0` (अपारदर्शी) |
| `ca` | Fill opacity | `CA` के समान रेंज |
| `BM` | Blend mode | `Normal`, `Multiply`, `Screen`, `Overlay`, आदि |

`ca` को `0.5` सेट करने से भराव वाले आकार 50 % पारदर्शी हो जाते हैं, जबकि `CA` स्ट्रोक के लिए पूरी तरह अपारदर्शी रहता है। `BM` बदलने से आप Photoshop‑जैसे ब्लेंड इफ़ेक्ट्स का प्रयोग कर सकते हैं।

## Step 5 – Register the custom graphics state under a unique name

```csharp
// Choose a unique name for the new state, e.g., "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

**Naming convention:**  
PDF स्पेसिफिकेशन छोटे, अपरकेस पहचानकर्ताओं की सलाह देता है। `GS0` (Graphics State 0) का उपयोग करने से नाम को कंटेंट स्ट्रीम से रेफ़र करना आसान हो जाता है।

## Step 6 – Apply the custom graphics state in a content stream (optional)

यदि आप पहले पेज पर एक पारदर्शी आयत बनाना चाहते हैं, तो नीचे दिए गए ऑपरेटर्स को प्रीपेंड कर सकते हैं:

```csharp
// Build the content stream that uses the new graphics state
var content = new Operator[]
{
    new Operator("q"),                 // Save graphics state
    new Operator("GS0", "gs"),         // Set our custom ExtGState
    new Operator("0.5 0.5 1 rg"),      // Set fill color (light blue)
    new Operator("100 500 200 100 re"),// Rectangle (x, y, width, height)
    new Operator("f"),                 // Fill the rectangle using the fill opacity
    new Operator("Q")                  // Restore graphics state
};

// Add the operators to the page's content
firstPage.Contents.Add(content);
```

**Why this step is optional:**  
पिछले चरण केवल ग्राफ़िक्स स्टेट *परिभाषित* करते हैं। प्रभाव देखने के लिए इसे पेज की कंटेंट स्ट्रीम से रेफ़र करना आवश्यक है। ऊपर दिया गया स्निपेट एक व्यावहारिक उपयोग केस दर्शाता है, लेकिन आप इस स्टेट को अपने PDF के मौजूदा ड्रॉइंग कमांड्स पर भी लागू कर सकते हैं।

## Step 7 – Save the modified PDF

```csharp
// Persist the changes to a new file
pdfDocument.Save("Resources/output.pdf");
```

जब आप `output.pdf` खोलेंगे तो आपको आयत 50 % फ़िल अपारदर्शिता के साथ रेंडर होती दिखेगी जबकि उसकी बॉर्डर पूरी तरह अपारदर्शी रहेगी—बिल्कुल वही परिणाम जो **PDF में पारदर्शिता कैसे सेट करें** का उपयोग करके कस्टम ExtGState से प्राप्त हुआ है।

## Handling Multiple Pages

यदि आपको हर पेज पर समान पारदर्शिता प्रभाव चाहिए, तो `pdfDocument.Pages` पर लूप करें और प्रत्येक पेज के रिसोर्सेज़ के लिए **Step 2**‑**Step 5** दोहराएँ। ध्यान रखें कि ग्राफ़िक्स स्टेट केवल एक बार प्रति पेज जोड़ा जाए; एक ही डिक्शनरी को कई पेजों में पुन: उपयोग करना PDF स्पेसिफिकेशन द्वारा अनुमति नहीं है।

```csharp
foreach (Page page in pdfDocument.Pages)
{
    var editor = new DictionaryEditor(page.Resources);
    // Ensure ExtGState exists, then add GS0 as shown earlier
    // (code omitted for brevity)
}
```

## Common pitfalls and how to avoid them

| Symptom | Cause | Fix |
|---------|-------|-----|
| Opacity में कोई बदलाव नहीं | `ca` या `CA` मान 0‑1 रेंज के बाहर | `0.0` से `1.0` के बीच दशमलव मान उपयोग करें। |
| कंटेंट गायब हो जाता है | ग्राफ़िक्स स्टेट लागू नहीं हुआ (`gs` ऑपरेटर गायब) | ड्रॉइंग कमांड्स से पहले `GS0 gs` डालें। |
| PDF नहीं खुल रहा | `ExtGState` डिक्शनरी में डुप्लिकेट की | जोड़ने से पहले `extGStateDict.ContainsKey("GS0")` जांचें। |
| Blend mode अनदेखा हो रहा है | व्यूअर निर्दिष्ट मोड को सपोर्ट नहीं करता | `Normal`, `Multiply` जैसे मानक मोड्स का उपयोग करें। |

## Full runnable example

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF
        using var pdfDocument = new Document("Resources/input.pdf");

        // Work with the first page
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = new CosPdfDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create custom graphics state
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGraphicsState.Add(e);

        // Register under a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a transparent rectangle
        var ops = new Operator[]
        {
            new Operator("q"),
            new Operator("GS0", "gs"),
            new Operator("0.5 0.5 1 rg"),
            new Operator("100 500 200 100 re"),
            new Operator("f"),
            new Operator("Q")
        };
        firstPage.Contents.Add(ops);

        // Save result
        pdfDocument.Save("Resources/output.pdf");
    }
}
```

**Expected output:**  
`output.pdf` खोलने पर (100, 500) निर्देशांक पर एक हल्का‑नीला आयत 50 % फ़िल अपारदर्शिता के साथ दिखेगा। आयत की बॉर्डर पूरी तरह अपारदर्शी रहेगी क्योंकि `CA` को `1.0` सेट किया गया है।

## Conclusion

अब आप Aspose.PDF के साथ **कस्टम ExtGState PDF** ऑब्जेक्ट्स जोड़ना और अपारदर्शिता तथा ब्लेंड मोड को सटीक रूप से नियंत्रित करना जानते हैं—जिससे आम सवाल **PDF में पारदर्शिता कैसे सेट करें** का उत्तर मिलता है। ट्यूटोरियल ने दस्तावेज़ लोड करना, रिसोर्स डिक्शनरी एडिट करना, ग्राफ़िक्स स्टेट परिभाषित करना, उसे लागू करना और परिणाम सहेजना कवर किया।

अगले चरण में आप खोज सकते हैं:

- विभिन्न ब्लेंड मोड्स (`Multiply`, `Screen`) का उपयोग करके रचनात्मक इफ़ेक्ट्स बनाना।
- इमेज XObjects पर वही ExtGState लागू करके अर्ध‑पारदर्शी लोगो जोड़ना।
- बैकग्राउंड सर्विस में बड़े पैमाने पर PDF संशोधनों को ऑटोमेट करना।

मूल्य, ग्राफ़िक्स स्टेट का नाम बदलना, या


## What Should You Learn Next?


निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add a Page Stamp to PDFs Using Aspose.PDF for Java (2023 Guide)](/pdf/english/java/watermarks-backgrounds/add-page-stamp-aspose-pdf-java/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF for Java: A Comprehensive Guide](/pdf/english/java/document-manipulation/aspose-pdf-java-add-text-stamp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}