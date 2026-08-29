---
category: general
date: 2026-08-17
description: C# और Aspose.Pdf का उपयोग करके PDF में खाली ग्राफ़िक्स स्टेट बनाएं। ExtGState
  संसाधनों को सुरक्षित रूप से संपादित करने के लिए इस चरण‑दर‑चरण मार्गदर्शिका का पालन
  करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: hi
lastmod: 2026-08-17
og_description: C# का उपयोग करके PDF में खाली ग्राफ़िक्स स्टेट बनाएं। यह ट्यूटोरियल
  दिखाता है कि Aspose.Pdf के साथ ExtGState संसाधनों को कैसे संपादित किया जाए, ताकि
  विश्वसनीय PDF संशोधन किया जा सके।
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: C# के साथ PDF में खाली ग्राफ़िक्स स्टेट बनाएं – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C# के साथ PDF में खाली ग्राफ़िक्स स्टेट कैसे बनाएं
url: /hi/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ PDF में खाली ग्राफ़िक्स स्टेट कैसे बनाएं

यदि आपको PDF में **खाली ग्राफ़िक्स स्टेट बनाएं** है, तो यह गाइड आपको C# और Aspose.Pdf के साथ इसे कैसे करें दिखाता है। आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जो पृष्ठ के ExtGState डिक्शनरी में एक नया एंट्री जोड़ता है बिना मौजूदा सामग्री को प्रभावित किए।

PDF ग्राफ़िक्स स्टेट्स के साथ काम करना एक सामान्य आवश्यकता है जब आप ट्रांसपेरेंसी, ब्लेंड मोड्स, या अन्य रेंडरिंग पैरामीटर्स को प्रति‑ऑब्जेक्ट आधार पर नियंत्रित करना चाहते हैं। नीचे दिया गया कोड अनुशंसित दृष्टिकोण को दर्शाता है, प्रत्येक चरण के महत्व को समझाता है, और आप जिन सामान्य विविधताओं का सामना कर सकते हैं उन्हें कवर करता है।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण (सैंपल .NET Core के साथ भी संकलित होता है)।
* Aspose.Pdf for .NET लाइसेंस (या एक अस्थायी मूल्यांकन कुंजी)।
* एक फ़ोल्डर जिसमें वह `input.pdf` फ़ाइल हो जिसे आप संशोधित करना चाहते हैं।
* C# सिंटैक्स और PDF अवधारणाओं जैसे resources dictionaries की बुनियादी जानकारी।

## चरण 1: प्रोजेक्ट सेट अप करें और नेमस्पेस इम्पोर्ट करें

एक नया कंसोल एप्लिकेशन बनाएं या कोड को मौजूदा प्रोजेक्ट में इंटीग्रेट करें। Aspose.Pdf NuGet पैकेज जोड़ें:

```bash
dotnet add package Aspose.Pdf
```

फिर आवश्यक नेमस्पेस इम्पोर्ट करें:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

ये इम्पोर्ट आपको `Document`, `DictionaryEditor`, और PDF प्रिमिटिव क्लासेज़ तक पहुँच देते हैं जो **खाली ग्राफ़िक्स स्टेट बनाएं** एंट्रीज़ के लिए आवश्यक हैं।

## चरण 2: PDF फ़ाइलों को रखने वाले फ़ोल्डर को परिभाषित करें

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

पथ को अपने PDF फ़ाइलों के स्थान से बदलें। डायरेक्टरी को एक वेरिएबल में रखना कोड को पुन: उपयोग योग्य और परीक्षण में आसान बनाता है।

## चरण 3: स्रोत PDF दस्तावेज़ लोड करें

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

`using` स्टेटमेंट के भीतर दस्तावेज़ खोलने से फ़ाइल हैंडल स्वचालित रूप से रिलीज़ हो जाता है जब आप परिवर्तन सहेजते हैं।

## चरण 4: पहले पृष्ठ और उसके Resources डिक्शनरी तक पहुँचें

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` पहला पृष्ठ प्राप्त करता है (PDF पेज नंबर 1 से शुरू होते हैं)।
* `DictionaryEditor` PDF डिक्शनरी को पढ़ने और संशोधित करने का सुविधाजनक तरीका प्रदान करता है।
* `ExtGState` एंट्री पृष्ठ के सभी graphics‑state ऑब्जेक्ट्स रखती है। यदि कुंजी मौजूद नहीं है, तो Aspose.Pdf स्वचालित रूप से एक खाली डिक्शनरी बनाता है।

## चरण 5: नया खाली graphics‑state डिक्शनरी बनाएं

आप जो graphics state जोड़ते हैं वह खाली या opacity (`CA`, `ca`) या blend mode (`BM`) जैसे पैरामीटर्स के साथ पूर्व‑भरा हो सकता है। इस ट्यूटोरियल में हम **खाली ग्राफ़िक्स स्टेट** बनाते हैं और फिर कुछ सामान्य मान सेट करके दिखाते हैं कि डिक्शनरी कैसे काम करती है।

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` एक साफ कंटेनर बनाता है जिसे आप किसी भी graphics‑state कुंजियों से भर सकते हैं।
* `CA`, `ca`, और `BM` जोड़ना वैकल्पिक है; यदि आपको वास्तव में एक खाली स्टेट चाहिए तो आप इन्हें छोड़ सकते हैं। कोड दिखाता है कि बाद में रेंडरिंग को नियंत्रित करने के लिए एंट्री कैसे जोड़ें।

## चरण 6: नया graphics state ExtGState डिक्शनरी में डालें

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

एंट्री का नाम `"GS0"` रखने से ग्राफ़िक्स‑state नामों को “GS” से प्रीफ़िक्स करने की सामान्य प्रथा का पालन होता है। आप कोई भी वैध PDF नाम चुन सकते हैं जो मौजूदा कुंजियों से टकराता न हो।

## चरण 7: संशोधित PDF दस्तावेज़ सहेजें

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

`Save` कॉल अपडेटेड फ़ाइल को `output.pdf` में लिखता है। इस फ़ाइल को PDF व्यूअर में खोलने से पुष्टि होती है कि नया graphics state मौजूद है; आप बाद में इसे कंटेंट स्ट्रीम में `gs` ऑपरेटर के साथ रेफ़र कर सकते हैं।

### पूर्ण स्रोत सूची

सब कुछ मिलाकर, पूरा प्रोग्राम इस प्रकार दिखता है:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

प्रोग्राम चलाने से एक पुष्टि पंक्ति प्रिंट होती है और `output.pdf` बनता है जिसमें नया graphics state जोड़ा गया है।

## क्यों यह दृष्टिकोण सबसे अच्छा काम करता है

* **Direct dictionary editing** – `DictionaryEditor` का उपयोग करने से पूरे कंटेंट स्ट्रीम को पार्स करने की आवश्यकता नहीं रहती। आप केवल उन रिसोर्सेज़ को संशोधित करते हैं जिनकी आपको ज़रूरत है।
* **Typed PDF primitives** – `CosPdfNumber`, `CosPdfName`, और `CosPdfDictionary` यह सुनिश्चित करते हैं कि उत्पन्न PDF PDF 1.7 स्पेसिफिकेशन के अनुरूप हो।
* **Safety** – `using` ब्लॉक `Document` ऑब्जेक्ट को डिस्पोज़ कर देता है, जिससे फ़ाइल लॉक नहीं होते जो बाद के बिल्ड को भ्रष्ट कर सकते हैं।
* **Extensibility** – एक बार खाली graphics state बन जाने पर, आप इसे किसी भी कंटेंट ऑपरेटर (`gs`) से रेफ़र कर सकते हैं ताकि चयनित ड्रॉइंग कमांड्स के लिए opacity, blend mode, या अन्य पैरामीटर बदल सकें।

## सामान्य विविधताएँ और किनारे के मामले

| स्थिति | अनुशंसित संशोधन |
|-----------|-------------------|
| **Multiple pages** | `pdfDocument.Pages` पर लूप करें और प्रत्येक पृष्ठ के लिए डिक्शनरी इन्सर्शन दोहराएँ जिसे आप संशोधित करना चाहते हैं। |
| **No existing ExtGState entry** | `resourcesEditor["ExtGState"]` स्वचालित रूप से एक खाली डिक्शनरी बनाता है यदि वह मौजूद नहीं है। अतिरिक्त कोड की आवश्यकता नहीं है। |
| **Different graphics‑state name** | `"GS0"` को ऐसे नाम से बदलें जो आपके नामकरण मानक से मेल खाता हो, उदाहरण के लिए `"MyTransparentState"`। |
| **Adding only an empty state** | `parameters` एरे और `foreach` लूप को छोड़ दें; डिक्शनरी खाली ही रहेगी। |
| **Working with encrypted PDFs** | रिसोर्सेज़ को एडिट करने से पहले `new Document(path, password)` बनाते समय पासवर्ड प्रदान करें। |

## परिणाम की पुष्टि करना

आप PDF को एक लो‑लेवल व्यूअर जैसे **PDF‑Tron** या **iText Sharp** से निरीक्षण करके पुष्टि कर सकते हैं कि graphics state जोड़ा गया है। इस तरह की एंट्री देखें:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

यदि एंट्री दिखाई देती है, तो **खाली ग्राफ़िक्स स्टेट बनाएं** ऑपरेशन सफल रहा।

## निष्कर्ष

अब आप जानते हैं कि C# और Aspose.Pdf का उपयोग करके PDF में **खाली ग्राफ़िक्स स्टेट बनाएं**। ट्यूटोरियल ने हर चरण को कवर किया—दस्तावेज़ लोड करने से लेकर `ExtGState` डिक्शनरी को एडिट करने और परिणाम सहेजने तक—और प्रत्येक कार्रवाई के पीछे का तर्क समझाया।

* नए graphics state को कंटेंट स्ट्रीम्स (`gs /GS0`) में उपयोग करें।
* अतिरिक्त कुंजियों जैसे `/SM` (stroke adjustment) या `/OPM` (overprint mode) के साथ प्रयोग करें।
* इसी तकनीक को अन्य रिसोर्स टाइप्स जैसे `/XObject` या `/ColorSpace` पर लागू करें।

हैप्पी PDF हैकिंग, और स्वतंत्र रूप से अन्य **Aspose PDF graphics state** परिदृश्यों जैसे डायनामिक opacity परिवर्तन या कस्टम ब्लेंड मोड्स का अन्वेषण करें!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं ताकि आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Aspose.PDF for .NET के साथ PDFs में डैश्ड लाइन्स कैसे बनाएं: एक चरण‑दर‑चरण गाइड](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Aspose.PDF .NET के साथ PDFs से ग्राफ़िक्स कैसे हटाएं: एक पूर्ण गाइड](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Aspose.PDF for .NET के साथ PDFs में रेक्टैंगल्स कैसे बनाएं और भरें: एक चरण‑दर‑चरण गाइड](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}