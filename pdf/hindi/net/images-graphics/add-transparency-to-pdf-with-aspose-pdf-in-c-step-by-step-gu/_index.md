---
category: general
date: 2026-03-19
description: Aspose.PDF for C# का उपयोग करके PDF में पारदर्शिता जोड़ें। कुछ ही कोड
  लाइनों में अपारदर्शिता, ब्लेंड मोड और ExtGState सेट करना सीखें।
draft: false
keywords:
- add transparency to pdf
- Aspose PDF transparency
- C# PDF graphics state
- PDF blend mode
- set PDF opacity
language: hi
og_description: PDF में शीघ्रता से पारदर्शिता जोड़ें। यह गाइड Aspose.PDF का उपयोग
  करके C# में अपारदर्शिता और ब्लेंड मोड को नियंत्रित करने का तरीका दिखाता है।
og_title: Aspose PDF के साथ PDF में ट्रांसपेरेंसी जोड़ें – पूर्ण C# ट्यूटोरियल
tags:
- Aspose.PDF
- C#
title: C# में Aspose PDF के साथ PDF में पारदर्शिता जोड़ें – चरण‑दर‑चरण गाइड
url: /hi/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Transparency to PDF with Aspose PDF in C# – Complete Tutorial

क्या आपने कभी **PDF फ़ाइलों में पारदर्शिता जोड़ने** के बारे में सोचा है बिना लो‑लेवल PDF सिंटैक्स से जूझे? आप अकेले नहीं हैं। कई डेवलपर्स को शीप्स या टेक्स्ट को अर्ध‑पारदर्शी बनाने का तेज़ तरीका चाहिए—जैसे वॉटरमार्क, ओवरले ग्राफ़िक्स, या दस्तावेज़ के अंदर सूक्ष्म UI संकेत।  

इस गाइड में हम एक **पूरा, चलाने योग्य उदाहरण** देखेंगे जो दिखाता है कि Aspose.PDF for .NET का उपयोग करके फ़िल ओपेसिटी, स्ट्रोक ओपेसिटी, और ब्लेंड मोड कैसे सेट करें। अंत तक आपके पास एक PDF होगा जिसमें एक आयत 50 % ओपेसिटी के साथ दिखाई देगा, और आप समझेंगे कि ExtGState डिक्शनरी इस प्रभाव को हासिल करने की कुंजी क्यों है।

हम वह सब कवर करेंगे जिसकी आपको ज़रूरत है: आवश्यक NuGet पैकेज, कोड स्वयं, प्रत्येक लाइन की व्याख्या, और कुछ टिप्स पुराने PDF व्यूअर्स जैसे एज केस के लिए। कोई बाहरी रेफ़रेंस नहीं—सिर्फ एक स्व‑समाहित समाधान जिसे आप आज़ ही कॉपी‑पेस्ट करके चला सकते हैं।

## What You’ll Need

- **Aspose.PDF for .NET** (v23.12 या बाद का)। NuGet के ज़रिए इंस्टॉल करें: `Install-Package Aspose.PDF`।
- एक .NET डेवलपमेंट एनवायरनमेंट (Visual Studio, Rider, या `dotnet` CLI)।
- एक सैंपल PDF जिसका नाम `input.pdf` हो और जो किसी फ़ोल्डर में हो जिसे आप नियंत्रित करते हैं (ट्यूटोरियल में `YOUR_DIRECTORY/` को प्लेसहोल्डर के रूप में इस्तेमाल किया गया है)।

बस इतना ही। अगर आपके पास ये सब है, तो चलिए शुरू करते हैं।

## Add Transparency to PDF – Overview

PDF में कुछ पारदर्शी बनाने का मूलभूत हिस्सा **ग्राफ़िक्स स्टेट** (`ExtGState`) है। पेज के रिसोर्स डिक्शनरी में एक कस्टम ग्राफ़िक्स स्टेट ऑब्जेक्ट जोड़कर आप निम्नलिखित परिभाषित कर सकते हैं:

| Property | Meaning |
|----------|---------|
| `ca` | Fill opacity (0 = पूरी तरह पारदर्शी, 1 = अपारदर्शी)। |
| `CA` | Stroke opacity (उसी स्केल पर)। |
| `BM` | Blend mode (जैसे `Normal`, `Multiply`)। |

हम एक नया ग्राफ़िक्स स्टेट बनाएँगे, उसे पेज के `ExtGState` डिक्शनरी में डालेंगे, और बाद में ड्रॉ करते समय उसका रेफ़रेंस करेंगे। नीचे दिया गया कोड स्निपेट ठीक यही करता है।

![add transparency to pdf diagram](add_transparency_to_pdf.png){alt="PDF में पारदर्शिता जोड़ें"}

## Step 1: Set Up the Project and Load the PDF

पहले हम एक साधारण कंसोल ऐप (या कोई भी C# प्रोजेक्ट) बनाते हैं और स्रोत PDF को लोड करते हैं।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;          // For low‑level PDF operators
using Aspose.Pdf.Text;               // Optional, if you want to add text later
using Aspose.Pdf.XObjects;          // For image handling, not needed here

// Define the folder that contains the PDF file
string inputDir = @"YOUR_DIRECTORY/";

// Load the PDF document
using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
{
    // All subsequent steps go inside this using block
```

**Why this matters:**  
`Document` Aspose के साथ किसी भी PDF मैनिपुलेशन का एंट्री पॉइंट है। इसे `using` स्टेटमेंट में रैप करने से यह सुनिश्चित होता है कि फ़ाइल को बाद में सेव करने पर सभी रिसोर्स सही ढंग से फ्लश हो जाएँ।

## Step 2: Access the First Page and Its Resources

हमें पहले पेज की रिसोर्स डिक्शनरी चाहिए क्योंकि `ExtGState` कलेक्शन वहीं रहता है।

```csharp
    // Grab the first page (pages are 1‑based in Aspose)
    Page firstPage = pdfDocument.Pages[1];

    // Helper to edit dictionaries (resources, etc.)
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);

    // Retrieve the existing ExtGState dictionary, or create a new one if missing
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

**Explanation:**  
यदि पेज में पहले से `ExtGState` एंट्री है तो हम उसे री‑यूज़ करते हैं; अन्यथा हम एक नई डिक्शनरी बनाते हैं। यह डिफेन्सिव अप्रोच उन PDFs में नल‑रेफ़रेंस एरर से बचाता है जिनमें कोई ग्राफ़िक्स स्टेट नहीं होता।

## Step 3: Create a New Graphics State with Desired Opacity

अब हम वास्तविक पारदर्शिता मान निर्धारित करते हैं।

```csharp
    // Create an empty dictionary that will represent our new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Stroke opacity – fully opaque (1.0)
    newGraphicsState.Add("CA", new CosPdfNumber(1));

    // Fill opacity – 50 % transparent (0.5)
    newGraphicsState.Add("ca", new CosPdfNumber(0.5));

    // Blend mode – Normal is the default, but you can experiment with Multiply, Screen, etc.
    newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**Why these keys?**  
- `CA` स्ट्रोक (लाइन, बॉर्डर) की ओपेसिटी नियंत्रित करता है।  
- `ca` फ़िल (सॉलिड शेप, टेक्स्ट) की ओपेसिटी नियंत्रित करता है।  
- `BM` तय करता है कि पारदर्शी ऑब्जेक्ट नीचे की सामग्री के साथ कैसे ब्लेंड होता है। `"Normal"` का उपयोग करने से विज़ुअल रिज़ल्ट अधिकांश व्यूअर्स में पूर्वानुमेय रहता है।

## Step 4: Register the Graphics State in the Page Resources

हम अपने ग्राफ़िक्स स्टेट को एक नाम (`GS0`) देते हैं और उसे `ExtGState` डिक्शनरी में जोड़ते हैं।

```csharp
    // Add the graphics state to the ExtGState dictionary with a unique name
    extGStateDict.Add("GS0", newGraphicsState);
```

**Tip:**  
यदि आपको विभिन्न ओपेसिटी वाले कई पारदर्शी ऑब्जेक्ट चाहिए, तो अतिरिक्त एंट्रीज़ (`GS1`, `GS2`, …) बनाएँ और `ca`/`CA` मानों को उसी अनुसार समायोजित करें।

## Step 5: Draw a Transparent Rectangle Using the New Graphics State

ग्राफ़िक्स स्टेट सेट होने के बाद, अब हम कुछ ऐसा ड्रॉ कर सकते हैं जो वास्तव में उसका उपयोग करे। नीचे हम पेज पर एक अर्ध‑पारदर्शी नीला आयत जोड़ते हैं।

```csharp
    // Prepare a content stream for the page (adds to existing content)
    var canvas = new Aspose.Pdf.Drawing.Graphic(firstPage);

    // Set the graphics state we just created
    canvas.SetGraphicsState("GS0");

    // Choose a fill color (blue) and draw the rectangle
    canvas.SetColor(new Aspose.Pdf.Drawing.Color(0, 0, 255)); // RGB blue
    canvas.Rectangle(100, 500, 200, 100); // x, y, width, height

    // Close the canvas to flush commands
    canvas.Close();
```

**What you’ll see:**  
जब आप परिणामी PDF खोलेंगे, तो निर्दिष्ट स्थान पर एक नीला आयत दिखाई देगा, लेकिन नीचे की पेज सामग्री अभी भी उसके माध्यम से दिखेगी क्योंकि फ़िल ओपेसिटी 0.5 है। यदि आप Adobe Acrobat के “Edit PDF” फ़ीचर जैसे टूल से PDF को इंस्पेक्ट करेंगे, तो आपको `ExtGState` ऑब्जेक्ट (`GS0`) उस आयत से जुड़ा हुआ दिखेगा।

## Step 6: Save the Updated PDF

अंत में, संशोधित डॉक्यूमेंट को डिस्क पर लिखें।

```csharp
    // Save the document with a new name so the original stays untouched
    pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
}
```

यही पूरा वर्कफ़्लो है। कंसोल ऐप चलाएँ, `ExtGStateAdded.pdf` खोलें, और पारदर्शी ओवरले की जाँच करें।

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddTransparencyDemo
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF file
        string inputDir = @"YOUR_DIRECTORY/";

        // Step 2: Load the PDF document
        using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
        {
            // Step 3: Get the first page and its resource dictionary
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

            // Step 4: Create a new graphics state with opacity and blend mode settings
            CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity (fully opaque)
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));       // fill opacity (50% transparent)
            newGraphicsState.Add("BM", new CosPdfName("Normal"));   // blend mode

            // Step 5: Add the new graphics state to the page resources
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 6: Draw a rectangle using the new graphics state
            var canvas = new Graphic(firstPage);
            canvas.SetGraphicsState("GS0");
            canvas.SetColor(new Color(0, 0, 255)); // blue fill
            canvas.Rectangle(100, 500, 200, 100);
            canvas.Close();

            // Step 7: Save the updated PDF document
            pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
        }

        Console.WriteLine("PDF with transparency created successfully.");
    }
}
```

**Expected result:**  
`ExtGStateAdded.pdf` खोलने पर (100, 500) पर एक नीला आयत 50 % फ़िल ओपेसिटी के साथ दिखेगा। आयत के नीचे मौजूद कोई भी टेक्स्ट या इमेज अभी भी दिखाई देगा।

---

## Frequently Asked Questions & Edge Cases

### Does this work with older PDF viewers?
अधिकांश आधुनिक व्यूअर्स (Adobe Reader, Foxit, Chrome) बेसिक `ca`/`CA` ओपेसिटी कीज़ को सपोर्ट करते हैं। बहुत पुराने रीडर्स इन्हें अनदेखा कर सकते हैं और शेप को पूरी तरह अपारदर्शी रेंडर कर सकते हैं।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}