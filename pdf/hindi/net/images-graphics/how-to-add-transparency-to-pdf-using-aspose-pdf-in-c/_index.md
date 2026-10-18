---
category: general
date: 2026-10-17
description: Aspose.PDF for .NET का उपयोग करके PDF में पारदर्शिता जोड़ें, PDF संसाधनों
  को संपादित करें, और एक ही चलाने योग्य उदाहरण में संशोधित PDF फ़ाइलें सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- save modified pdf
- edit pdf resources
- Aspose.PDF transparency
- C# PDF manipulation
language: hi
lastmod: 2026-10-17
og_description: Aspose.PDF for .NET का उपयोग करके PDF में पारदर्शिता जोड़ें, PDF संसाधनों
  को संपादित करें, और पूर्ण C# उदाहरण के साथ संशोधित PDF फ़ाइलें सहेजें।
og_image_alt: Screenshot showing a PDF with added transparency using Aspose.PDF in
  C#
og_title: Aspose.PDF के साथ PDF में पारदर्शिता जोड़ें – गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Add transparency to PDF with Aspose.PDF for .NET, edit PDF resources,
    and save modified PDF files in a single, runnable example.
  headline: How to add transparency to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
title: Aspose.PDF का उपयोग करके C# में PDF में पारदर्शिता कैसे जोड़ें
url: /hi/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF में Aspose.PDF का उपयोग करके C# में ट्रांसपेरेंसी कैसे जोड़ें

यदि आपको प्रोग्रामेटिक रूप से **PDF में ट्रांसपेरेंसी जोड़ें** फ़ाइलें जोड़नी है, तो यह गाइड Aspose.PDF for .NET के साथ एक स्पष्ट, एंड‑टू‑एंड समाधान दिखाता है। आप सीखेंगे कि **PDF संसाधनों को संपादित करें**, एक कस्टम ग्राफ़िक्स स्टेट बनाएं, और **संशोधित PDF सहेजें** आउटपुट को बिना अपने C# प्रोजेक्ट से बाहर निकले कैसे सहेजें।

PDF ट्रांसपेरेंसी के साथ काम करना अक्सर लो‑लेवल PDF ऑपरेटरों के पीछे छिपा हुआ लगता है। इस ट्यूटोरियल के अंत तक आपके पास एक पूरी तरह कार्यात्मक उदाहरण होगा जिसे आप कॉपी‑पेस्ट कर सकते हैं, चला सकते हैं, और कई पृष्ठों या विभिन्न ब्लेंड मोड्स के लिए अनुकूलित कर सकते हैं।

## आवश्यकताएँ

- .NET 6.0 (या कोई भी नवीनतम .NET संस्करण)  
- Aspose.PDF for .NET NuGet पैकेज (`Aspose.Pdf`)  
- बेसिक C# ज्ञान  
- एक इनपुट PDF फ़ाइल (`input.pdf`) जो आप किसी फ़ोल्डर में रख सकते हैं

> **Pro tip:** शुरू करने से पहले `dotnet add package Aspose.Pdf` कमांड से पैकेज इंस्टॉल करें।

## चरण 1: PDF दस्तावेज़ लोड करें

पहला ऑपरेशन स्रोत PDF को खोलना है। Aspose.PDF PDF को एक `Document` ऑब्जेक्ट के रूप में दर्शाता है, जो आपको पृष्ठों, संसाधनों और लो‑लेवल डिक्शनरीज़ तक पहुंच प्रदान करता है।

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;   // for graphics‑state objects

// Path to the original PDF
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document in a using block so it disposes automatically
using (var document = new Document(pdfPath))
{
    // The rest of the steps are inside this block
```

*यह क्यों महत्वपूर्ण है:* इस तरह दस्तावेज़ खोलने से फ़ाइल हैंडल संपादन समाप्त होने के बाद रिलीज़ हो जाता है, जिससे बाद में **संशोधित PDF सहेजें** पर फ़ाइल‑लॉक समस्याओं से बचा जा सके।

## चरण 2: पहले पृष्ठ और उसकी रिसोर्स डिक्शनरी तक पहुंचें

PDF पृष्ठ ग्राफ़िक्स ऑब्जेक्ट्स (फ़ॉन्ट, इमेज, ExtGState एंट्रीज़) को *रिसोर्स डिक्शनरी* में संग्रहित करते हैं। अपारदर्शिता बदलने के लिए हमें `ExtGState` सब‑डिक्शनरी के साथ काम करना होगा।

```csharp
    // Get the first page (pages are 1‑based in Aspose.PDF)
    Page page = document.Pages[1];

    // Obtain a mutable editor for the page's resources
    var resourcesEditor = new DictionaryEditor(page.Resources);

    // Retrieve the ExtGState dictionary; create it if missing
    var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                         ?? new CosPdfDictionary(document);
```

*यह क्यों महत्वपूर्ण है:* यदि मूल PDF में पहले से ही `ExtGState` डिक्शनरी मौजूद है, तो हम उसे विस्तारित करेंगे; अन्यथा हम एक नई बनाते हैं ताकि हम सुरक्षित रूप से **PDF संसाधनों को संपादित** कर सकें।

## चरण 3: ट्रांसपेरेंसी के साथ नया ग्राफ़िक्स स्टेट बनाएं

एक ग्राफ़िक्स स्टेट (`ExtGState`) में पैरामीटर जैसे स्ट्रोक अपारदर्शिता (`CA`), फ़िल अपारदर्शिता (`ca`), और ब्लेंड मोड (`BM`) होते हैं। हम एक खाली डिक्शनरी बनाते हैं और उसमें वांछित मान भरते हैं।

```csharp
    // Create an empty ExtGState dictionary for the new entry
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Define the transparency entries
    var entries = new[]
    {
        // CA – stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA",
            new CosPdfNumber(1)),

        // ca – fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca",
            new CosPdfNumber(0.5)),

        // BM – blend mode (Normal is the default)
        new KeyValuePair<string, ICosPdfPrimitive>("BM",
            new CosPdfName("Normal"))
    };

    // Add each entry to the new ExtGState dictionary
    foreach (var entry in entries)
        newGraphicsState.Add(entry);
```

*यह क्यों महत्वपूर्ण है:* `ca` एंट्री इस ग्राफ़िक्स स्टेट का उपयोग करने वाली **PDF में ट्रांसपेरेंसी जोड़ने** की कुंजी है। आप संख्यात्मक मान (0 – 1) को समायोजित करके वस्तु की पारदर्शिता को नियंत्रित कर सकते हैं।

## चरण 4: ग्राफ़िक्स स्टेट को पृष्ठ संसाधनों में डालें

हमें नए ग्राफ़िक्स स्टेट को एक नाम देना होगा (जैसे, `"GS0"`). यह नाम बाद में कंटेंट स्ट्रीम द्वारा ट्रांसपेरेंसी लागू करने के लिए संदर्भित किया जा सकता है।

```csharp
    // Add the new ExtGState under the name "GS0"
    extGStateDict.Add("GS0", newGraphicsState);

    // Ensure the modified ExtGState dictionary is written back to the page
    resourcesEditor["ExtGState"] = extGStateDict;
```

*यह क्यों महत्वपूर्ण है:* `"GS0"` को `ExtGState` डिक्शनरी में जोड़ने से, कोई भी ड्रॉइंग ऑपरेशन जो इस स्टेट को चुनता है, निर्धारित अपारदर्शिता के साथ रेंडर होगा। यह ट्रांसपेरेंसी के लिए **PDF संसाधनों को संपादित** करने का मूल है।

## चरण 5: पृष्ठ सामग्री पर ग्राफ़िक्स स्टेट लागू करें (वैकल्पिक)

यदि आप चाहते हैं कि मौजूदा पृष्ठ सामग्री स्वचालित रूप से नई ट्रांसपेरेंसी का उपयोग करे, तो आपको पृष्ठ की कंटेंट स्ट्रीम की शुरुआत में एक ग्राफ़िक्स‑स्टेट ऑपरेटर जोड़ना होगा। नीचे दिया गया स्निपेट दिखाता है कि कैसे मौजूदा सामग्री को `gs` (ग्राफ़िक्स स्टेट सेट) और `Q` (ग्राफ़िक्स स्टेट पुनर्स्थापित) के साथ रैप किया जाए।

```csharp
    // Get the current content stream
    var content = page.Contents[1]; // assume a single content stream

    // Build a new stream that sets the graphics state, draws the original content, then restores
    string gsOperator = "/GS0 gs\n"; // select the graphics state we created
    string restoreOperator = "Q\n";   // restore graphics state after drawing

    // Prepend the gs operator and append the restore operator
    string newStream = gsOperator + content.Stream.ToString() + restoreOperator;

    // Replace the original stream with the modified one
    content.Stream = new CosPdfStream(document);
    content.Stream.SetData(newStream);
```

*यह क्यों महत्वपूर्ण है:* इस चरण के बिना, ग्राफ़िक्स स्टेट मौजूद है लेकिन उपयोग नहीं किया जाता। `gs` ऑपरेटर जोड़ने से PDF रेंडरर को बताता है कि उसके बाद आने वाली सभी चीज़ों पर ट्रांसपेरेंसी लागू हो।

## चरण 6: डिस्क पर **संशोधित PDF सहेजें**

अंत में, संशोधित दस्तावेज़ को नई फ़ाइल में लिखें। `Save` मेथड सभी लो‑लेवल अपडेट्स को स्वचालित रूप से संभालता है।

```csharp
    // Path for the output PDF
    string outputPath = @"YOUR_DIRECTORY\output.pdf";

    // Persist the changes
    document.Save(outputPath);
}
```

*यह क्यों महत्वपूर्ण है:* `document.Save` कॉल यह सुनिश्चित करता है कि अपडेटेड **संशोधित PDF सहेजें** में नया `ExtGState` एंट्री और उसे संदर्भित करने वाली कंटेंट स्ट्रीम शामिल हो। परिणामी फ़ाइल पहले पृष्ठ पर अर्ध‑पारदर्शी फ़िल दिखाएगी।

## अपेक्षित परिणाम

`output.pdf` को किसी भी PDF व्यूअर (Adobe Reader, Chrome, आदि) में खोलें और आपको पहले पृष्ठ की ग्राफ़िक्स 50 % फ़िल अपारदर्शिता के साथ रेंडर होते दिखेंगे। यदि आप PDF को **PDF‑Tron** या **iText** जैसे टूल से जांचते हैं, तो आपको `GS0` नाम की `ExtGState` डिक्शनरी एंट्री मिलेगी जिसमें `ca` मान `0.5` पर सेट होगा।

## किनारे के मामलों और विविधताएँ

| स्थिति | क्या बदलें |
|-----------|----------------|
| **Multiple pages** | `document.Pages` पर लूप करें और प्रत्येक पृष्ठ के लिए चरण 2‑5 दोहराएँ, `GS1`, `GS2`, … जैसे अद्वितीय नाम का उपयोग करके। |
| **Existing ExtGState name conflict** | जोड़ने से पहले `extGStateDict.ContainsKey("GS0")` जांचें; यदि यह मौजूद है, तो नया कुंजी उत्पन्न करें (`"GS" + Guid.NewGuid().ToString("N")`)। |
| **Different blend modes** | `BM` एंट्री बदलकर `"Normal"` को `"Multiply"`, `"Screen"` आदि से प्रतिस्थापित करें। |
| **Only stroke opacity needed** | `ca` एंट्री को छोड़ दें या इसे `1` सेट करें और इसके बजाय `CA` को समायोजित करें। |

## पूर्ण, चलाने योग्य उदाहरण



## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स इस गाइड में प्रदर्शित तकनीकों पर आधारित निकट संबंधी विषयों को कवर करते हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का पता लगाने में मदद करती हैं।

- [Aspose.PDF के साथ PDF में ट्रांसपेरेंसी जोड़ें – पूर्ण C# गाइड](/pdf/english/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/)
- [Aspose.PDF for .NET का उपयोग करके PDFs में पेज स्टैम्प कैसे जोड़ें: एक पूर्ण गाइड](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Aspose.PDF for .NET का उपयोग करके PDFs में इमेजेज कैसे जोड़ें: एक पूर्ण गाइड](/pdf/english/net/images-graphics/add-images-to-pdfs-using-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}