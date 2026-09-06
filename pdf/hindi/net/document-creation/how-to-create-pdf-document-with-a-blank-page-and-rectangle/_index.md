---
category: general
date: 2026-09-05
description: C# में एक खाली पृष्ठ जोड़कर, एक आयत बनाकर, और PDF फ़ाइल को सहेजकर PDF
  दस्तावेज़ बनाएं। चरण‑दर‑चरण Aspose.PDF उदाहरण का पालन करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: hi
lastmod: 2026-09-05
og_description: C# में एक खाली पृष्ठ जोड़कर, आयत बनाकर और PDF फ़ाइल को सहेजकर PDF
  दस्तावेज़ बनाएं। Aspose.PDF के साथ इस पूर्ण उदाहरण का पालन करें।
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: खाली पृष्ठ और आयत के साथ PDF दस्तावेज़ बनाएं – C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: खाली पृष्ठ और आयत के साथ PDF दस्तावेज़ कैसे बनाएं
url: /hi/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ब्लैंक पेज और आयत के साथ PDF दस्तावेज़ कैसे बनाएं

यदि आपको प्रोग्रामेटिक रूप से **PDF दस्तावेज़ बनाना** है, तो यह गाइड C# में एक पूर्ण समाधान दिखाता है। आप सीखेंगे कि कैसे एक ब्लैंक पेज जोड़ें, उस पेज पर एक आयत बनाएं, और अंत में PDF फ़ाइल को सहेजें। यह उदाहरण Aspose.PDF लाइब्रेरी का उपयोग करता है, जो .NET 6+ और .NET Framework 4.5+ के साथ काम करती है।

ब्लैंक पेज जोड़ना और आकार बनाना इनवॉइस, प्रमाणपत्र, या कस्टम रिपोर्ट के लिए एक सामान्य आवश्यकता है। इस ट्यूटोरियल के अंत तक आपके पास एक चलाने योग्य प्रोजेक्ट होगा जो (100, 100) पर स्थित एक आयत के साथ PDF उत्पन्न करता है, जिसका आकार 200 × 200 पॉइंट्स है।

## पूर्वापेक्षाएँ

* Visual Studio 2022 (या कोई भी C# IDE)
* .NET 6 SDK या .NET Framework 4.5+
* Aspose.PDF for .NET NuGet पैकेज  
  ```bash
  dotnet add package Aspose.PDF
  ```
* आउटपुट डायरेक्टरी में लिखने की अनुमति

कोई अतिरिक्त कॉन्फ़िगरेशन आवश्यक नहीं है; कोड तुरंत चल जाता है।

## PDF दस्तावेज़ बनाना – अवलोकन

पूरा प्रक्रिया चार तार्किक चरणों में विभाजित है:

1. **Instantiate** एक `Document` ऑब्जेक्ट – यह PDF फ़ाइल का प्रतिनिधित्व करता है।
2. **Add a blank page** – पेज ड्रॉइंग के लिए एक कैनवास प्रदान करता है।
3. **Draw a rectangle** – एक `Path` ऑब्जेक्ट आकार को परिभाषित करता है।
4. **Save the PDF file** – दस्तावेज़ को डिस्क पर सहेजता है।

प्रत्येक चरण को अपने स्वयं के सेक्शन में अलग किया गया है ताकि आप आवश्यकता अनुसार भागों को पुन: उपयोग या बदल सकें।

![ब्लैंक पेज पर आयत के साथ PDF का आरेख](https://example.com/placeholder-image.png){.img-fluid alt="स्क्रीनशॉट जो ब्लैंक पेज पर खींची गई आयत के साथ PDF दस्तावेज़ दिखाता है"}

## ब्लैंक पेज PDF जोड़ें

किसी भी ग्राफ़िक को रखने से पहले PDF में कम से कम एक पेज होना आवश्यक है। `Pages.Add()` मेथड डिफ़ॉल्ट आयाम (A4) के साथ एक खाली पेज बनाता है। यदि आपको अलग आकार चाहिए, तो `PageSize` आर्ग्यूमेंट पास करें।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Why this step matters* – पेज ऑब्जेक्ट टेक्स्ट, इमेज और वेक्टर ग्राफ़िक्स के संग्रह रखता है। पेज के बिना, आयत जोड़ने का कोई भी प्रयास एक अपवाद उत्पन्न करेगा।

### किनारा मामला: कस्टम पेज आकार

यदि आपके लेआउट को 6 × 9 इंच पेज चाहिए, तो डिफ़ॉल्ट कॉल को इस तरह बदलें:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## PDF में आयत बनाएं

आयत बनाना `Rectangle` ज्योमेट्री बनाने और उसे `Path` में रैप करने का काम है। `ValidateBounds()` कॉल सुनिश्चित करता है कि आकार पेज मार्जिन के भीतर फिट हो, जिससे क्लिपिंग नहीं होती।

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Why this step matters* – `Path` ऑब्जेक्ट Aspose.PDF द्वारा उपयोग किया गया लो‑लेवल वेक्टर प्रिमिटिव है। बाउंड्स को वैलिडेट करके आप रन‑टाइम त्रुटियों से बचते हैं जब आयत पेज सीमाओं से बाहर हो जाती है।

### प्रो टिप: आयत का स्टाइलिंग

आप स्ट्रोक रंग और लाइन की चौड़ाई बदल सकते हैं:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

यह 2‑पॉइंट मोटाई के साथ एक लाल रूपरेखा बनाता है।

## PDF फ़ाइल सहेजें

दस्तावेज़ को स्थायी बनाना डिस्क पर फ़ाइल को अंतिम रूप देता है। `Save` मेथड फ़ाइल पाथ या स्ट्रीम स्वीकार करता है। एक पूर्ण पाथ प्रदान करने से स्थान स्पष्ट हो जाता है, जो ऑटोमेशन स्क्रिप्ट्स के लिए उपयोगी है।

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Why this step matters* – सहेजना वह एकमात्र बिंदु है जहाँ इन‑मेमोरी प्रतिनिधित्व एक भौतिक फ़ाइल बन जाता है। यदि आपको वेब API से PDF लौटाना है, तो फ़ाइल पाथ को `MemoryStream` से बदलें।

### किनारा मामला: मौजूदा फ़ाइलों को ओवरराइट करना

Aspose.PDF डिफ़ॉल्ट रूप से मौजूदा फ़ाइल को ओवरराइट कर देता है। पिछले आउटपुट को सुरक्षित रखने के लिए, पहले फ़ाइल की मौजूदगी जांचें:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## आयत जोड़ने के सर्वोत्तम अभ्यास

* **Keep coordinates within the page margins** – `ValidateBounds()` का उपयोग करें या मार्जिन मैन्युअली गणना करें।
* **Reuse `GraphInfo` objects** जब कई आकार बनाते हैं; यह मेमोरी आवंटन को कम करता है।
* **Dispose of the `Document` object** (जैसे `using var` में दिखाया गया है) ताकि नेटिव रिसोर्सेज़ तुरंत मुक्त हो जाएँ।
* **Test with different DPI settings** यदि आप बाद में रास्टर इमेज एम्बेड करते हैं; वेक्टर आकार जैसे आयत किसी भी रिज़ॉल्यूशन पर स्पष्ट रहते हैं।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कंसोल एप्लिकेशन में कॉपी कर सकते हैं। यह बिना संशोधन के कंपाइल होता है और प्रोजेक्ट फ़ोल्डर में `output.pdf` बनाता है।

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने से एक सिंगल‑पेज PDF बनता है। जब आप `output.pdf` खोलेंगे तो आपको एक ब्लैंक सफ़ेद पेज पर एक लाल आयत दिखाई देगी, जो बाएँ और नीचे के किनारों से 100 पॉइंट्स पर स्थित है, और जिसका आकार 200 × 200 पॉइंट्स है।

## निष्कर्ष

अब आप जानते हैं कि Aspose.PDF का उपयोग करके C# में **PDF दस्तावेज़ बनाना**, **ब्लैंक पेज PDF जोड़ना**, **PDF में आयत बनाना**, और **PDF फ़ाइल सहेजना** कैसे किया जाता है। यह उदाहरण आवश्यक API कॉल्स को कवर करता है, बताता है कि प्रत्येक कॉल क्यों आवश्यक है, और कस्टम पेज साइज या आयत स्टाइलिंग जैसी सामान्य विविधताओं के लिए टिप्स प्रदान करता है।

अगला, **टेक्स्ट जोड़ना**, **इमेज एम्बेड करना**, या **मल्टी‑पेज रिपोर्ट बनाना** जैसे संबंधित विषयों का अन्वेषण करें। वही पैटर्न—`Document` को instantiate करना, पेजेज़ को मैनीपुलेट करना, वेक्टर या रास्टर कंटेंट जोड़ना, फिर `Save`—इन सभी परिदृश्यों पर लागू होता है। विभिन्न आकार, रंग, और पेज लेआउट के साथ प्रयोग करने में संकोच न करें ताकि आपके प्रोजेक्ट की जरूरतों को पूरा किया जा सके।

## आगे आप क्या सीखें

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को खोजने में मदद करती हैं।

- [PDF दस्तावेज़ C# बनाएं – पेज जोड़ें, आयत बनाएं और सहेजें](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Aspose.PDF के साथ PDF दस्तावेज़ बनाएं – चरण‑दर‑चरण गाइड](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Aspose के साथ PDF दस्तावेज़ बनाएं – पेज जोड़ें, टेक्स्ट बॉक्स, और फ़ॉर्म](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}