---
category: general
date: 2026-11-12
description: Aspose.Pdf का उपयोग करके PDF की अपारदर्शिता कैसे बदलें, पारदर्शिता जोड़ें,
  ब्लेंड मोड सेट करें, और C# में संशोधित PDF को सहेजें, यह सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: hi
lastmod: 2026-11-12
og_description: Aspose.Pdf के साथ PDF की अपारदर्शिता बदलें, ट्रांसपेरेंसी कैसे जोड़ें,
  ब्लेंड मोड सेट करें, और C# में संशोधित PDF फ़ाइलें सहेजें।
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Aspose.Pdf के साथ PDF की अपारदर्शिता बदलें – पारदर्शिता जोड़ें और सहेजें
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose.Pdf के साथ PDF की अपारदर्शिता बदलें और फ़ाइल सहेजें
url: /hi/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf के साथ PDF अपारदर्शिता बदलें और फ़ाइल सहेजें

यदि आपको दस्तावेज़ में **PDF अपारदर्शिता बदलनी** है, तो Aspose.Pdf एक सरल API प्रदान करता है जिससे स्ट्रोक और फ़िल ट्रांसपेरेंसी दोनों को समायोजित किया जा सकता है। यह ट्यूटोरियल बिल्कुल दिखाता है **कैसे ट्रांसपेरेंसी जोड़ें**, **कैसे ब्लेंड मोड सेट करें**, और **संशोधित PDF** फ़ाइलों को केवल कुछ पंक्तियों के C# कोड से सहेजें।

आप प्रत्येक चरण से गुजरेंगे—एक मौजूदा PDF लोड करने से लेकर नया ग्राफ़िक्स स्टेट परिभाषित करने और बदलावों को स्थायी बनाने तक। इस गाइड के अंत तक आप कर सकेंगे:

* वेक्टर ग्राफ़िक्स या छवियों की दृश्यता कम करना।
* *Normal* या *Multiply* जैसे कस्टम ब्लेंड मोड लागू करना।
* अन्य किसी भी सामग्री को खोए बिना अपडेटेड फ़ाइल निर्यात करना।

केवल पूर्वापेक्षा यह है कि आपके पास एक कार्यशील .NET विकास वातावरण और Aspose.Pdf लाइब्रेरी (संस्करण 23.9 या बाद का) का संदर्भ हो। कोई बाहरी टूल आवश्यक नहीं है।

## Prerequisites

| आवश्यकता | क्यों महत्वपूर्ण है |
|-------------|----------------|
| .NET 6.0 SDK or later | नवीनतम Aspose.Pdf APIs के साथ संगतता सुनिश्चित करता है। |
| Aspose.Pdf for .NET NuGet package | कोड में उपयोग किए गए `Document`, `CosPdfDictionary` और संबंधित क्लासेस प्रदान करता है। |
| A PDF file to edit (e.g., `input.pdf`) | अपारदर्शिता परिवर्तन के लिए स्रोत के रूप में कार्य करता है। |

NuGet पैकेज को इस प्रकार इंस्टॉल करें:

```bash
dotnet add package Aspose.Pdf
```

## Aspose.Pdf के साथ PDF अपारदर्शिता बदलें

### Step 1: PDF दस्तावेज़ लोड करें

सबसे पहले एक `Document` इंस्टेंस बनाएं जो आपके स्रोत फ़ाइल की ओर इशारा करता है। कंस्ट्रक्टर पूरे PDF को मेमोरी में पढ़ता है, जिससे आप उसके आंतरिक ऑब्जेक्ट्स को बदल सकते हैं।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **इस चरण का कारण?** फ़ाइल को लोड करने से एक ऐसा ऑब्जेक्ट मॉडल बनता है जिसे आप बदल सकते हैं। सभी बाद के परिवर्तन इस इन‑मेमोरी प्रतिनिधित्व पर लागू होते हैं, जिससे मूल फ़ाइल तब तक अप्रभावित रहती है जब तक आप स्पष्ट रूप से सहेज नहीं लेते।

### Step 2: पहले पृष्ठ के संसाधनों तक पहुँचें

प्रत्येक PDF पृष्ठ एक *resource dictionary* रखता है जिसमें फ़ॉन्ट, छवियां और ग्राफ़िक्स स्टेट जैसी वस्तुएं होती हैं। आपको इस शब्दकोश को संपादित करके नया `ExtGState` एंट्री जोड़ना होगा।

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **टिप:** यदि आपके PDF में कई पृष्ठ हैं जिन्हें समान अपारदर्शिता चाहिए, तो इस चरण को प्रत्येक पृष्ठ के लिए दोहराएँ या सभी पृष्ठों में एक ही `ExtGState` साझा करें।

### Step 3: सुनिश्चित करें कि ExtGState शब्दकोश मौजूद है

`ExtGState` शब्दकोश कस्टम ग्राफ़िक्स स्टेट को रखता है। यदि यह मौजूद नहीं है, तो कोड इसे स्वचालित रूप से बनाता है।

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **इस चरण का कारण?** बिना `ExtGState` कंटेनर के, नया ग्राफ़िक्स स्टेट रेफ़र करने का कोई तरीका नहीं होगा, और PDF आपके अपारदर्शिता सेटिंग को नजरअंदाज़ कर देगा।

### Step 4: एक नया ग्राफ़िक्स स्टेट (ExtGState) परिभाषित करें

ग्राफ़िक्स स्टेट यह निर्धारित करता है कि ड्रॉइंग ऑपरेशन कैसे व्यवहार करेंगे। नीचे दिया गया शब्दकोश स्ट्रोक अपारदर्शिता (`CA`), फ़िल अपारदर्शिता (`ca`) और ब्लेंड मोड (`BM`) सेट करता है।

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **फ़िल अपारदर्शिता कैसे सेट करें:** `ca` एंट्री भरे हुए आकारों (टेक्स्ट, पाथ) की अपारदर्शिता को नियंत्रित करती है। `0` (पूरी तरह से पारदर्शी) से `1` (पूरी तरह से अपारदर्शी) के बीच मान को अपनी डिज़ाइन आवश्यकता के अनुसार समायोजित करें।  
> **ब्लेंड मोड कैसे सेट करें:** `BM` एंट्री कॉम्पोज़िटिंग एल्गोरिदम चुनती है। सामान्य मानों में `Normal`, `Multiply`, `Screen`, और `Overlay` शामिल हैं। वह चुनें जो आपके दृश्य उद्देश्य से मेल खाता हो।

### Step 5: संसाधन शब्दकोश में ग्राफ़िक्स स्टेट को रजिस्टर करें

नए स्टेट को एक नाम दें (जैसे `GS0`) और इसे `ExtGState` शब्दकोश में जोड़ें। यह नाम बाद में पृष्ठ कंटेंट स्ट्रीम में रेफ़र किया जाएगा।

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **प्रो टिप:** जब आप कई स्टेट बनाते हैं, तो `GS0`, `GS1`, … जैसी नामकरण पद्धति अपनाएँ। यह नाम टकराव से बचाता है और डिबगिंग को आसान बनाता है।

### Step 6: पृष्ठ सामग्री पर ग्राफ़िक्स स्टेट लागू करें

अपारदर्शिता प्रभाव देखने के लिए, उस ड्रॉइंग कमांड से पहले `/GS0 gs` ऑपरेटर डालें जिसे आप प्रभावित करना चाहते हैं। नीचे का उदाहरण एक अर्ध‑पारदर्शी आयत बनाता है।

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **`q` और `Q` ऑपरेटर क्यों?** वे ग्राफ़िक्स स्टेट स्टैक को पुश और पॉप करते हैं, जिससे अपारदर्शिता परिवर्तन केवल आयत पर लागू होता है और पृष्ठ के बाकी हिस्से पर नहीं।

### Step 7: संशोधित PDF सहेजें

अंत में, अपडेटेड दस्तावेज़ को डिस्क पर लिखें। `Save` मेथड लक्ष्य फ़ाइल को ओवरराइट कर देता है या यदि फ़ाइल मौजूद नहीं है तो नई फ़ाइल बनाता है।

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **संशोधित PDF कैसे सहेजें:** `Save` कॉल सभी इन‑मेमोरी बदलावों को, जिसमें नया `ExtGState` भी शामिल है, निर्दिष्ट पथ पर लिखता है। आप वेब रेस्पॉन्स के लिए परिणाम को `MemoryStream` में भी स्ट्रीम कर सकते हैं।

## पूर्ण कार्यशील उदाहरण

नीचे एक एकल, स्व-समाहित प्रोग्राम है जो ऊपर वर्णित सभी चरणों को सम्मिलित करता है। इसे एक कंसोल एप्लिकेशन में कॉपी करें और चलाएँ ताकि अपारदर्शिता परिवर्तन की पुष्टि हो सके।

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट से संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Aspose.Pdf के साथ संशोधित PDF कैसे सहेजें और ट्रांसपेरेंसी जोड़ें](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [C# में Aspose.PDF का उपयोग करके PDF में ट्रांसपेरेंसी कैसे जोड़ें](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Aspose.PDF के साथ ग्राफ़िक्स स्टेट PDF जोड़ें और ट्रांसपेरेंसी नियंत्रित करें](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}