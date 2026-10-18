---
category: general
date: 2026-08-04
description: Aspose.Pdf का उपयोग करके ग्राफ़िक्स स्टेट PDF जोड़ें ताकि अपारदर्शिता
  और ब्लेंड मोड को नियंत्रित किया जा सके। PDF संसाधनों को सुरक्षित रूप से संशोधित
  करने के लिए इस पूर्ण ट्यूटोरियल का पालन करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose.Pdf
- PDF opacity
- PDF blend mode
- ExtGState dictionary
language: hi
lastmod: 2026-08-04
og_description: Aspose.Pdf के साथ ग्राफ़िक्स स्टेट PDF जोड़ें ताकि अपारदर्शिता और
  ब्लेंड मोड सेट किया जा सके। यह गाइड पूर्ण कोड दिखाता है, प्रत्येक चरण की व्याख्या
  करता है, और सामान्य समस्याओं को कवर करता है।
og_image_alt: Screenshot of a PDF page showing modified graphics state after using
  add graphics state pdf
og_title: Aspose.Pdf के साथ ग्राफ़िक्स स्टेट PDF जोड़ें – पूर्ण प्रोग्रामिंग गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  headline: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  name: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Locate (or create) the `ExtGState` dictionary.
    text: Locate (or create) the `ExtGState` dictionary.
  - name: Build a new graphics‑state dictionary with the desired entries.
    text: Build a new graphics‑state dictionary with the desired entries.
  - name: Reference the new state from drawing commands (outside the scope of this
      tutorial).
    text: Reference the new state from drawing commands (outside the scope of this
      tutorial).
  type: HowTo
tags:
- PDF
- Aspose
- C#
- Graphics state
title: Aspose.Pdf के साथ ग्राफ़िक्स स्टेट PDF जोड़ें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf के साथ ग्राफ़िक्स स्टेट PDF जोड़ें – चरण‑दर‑चरण गाइड

यदि आपको **add graphics state pdf** को अपारदर्शिता या ब्लेंड मोड को नियंत्रित करने के लिए जोड़ने की आवश्यकता है, तो यह ट्यूटोरियल आपको एक पूर्ण, प्रोडक्शन‑रेडी समाधान दिखाता है। आप सीखेंगे कि Aspose.Pdf का उपयोग करके PDF पेज की ExtGState डिक्शनरी को कैसे संपादित किया जाता है, और आप वह सटीक कोड देखेंगे जिसे आप अपने प्रोजेक्ट में कॉपी कर सकते हैं।

यह गाइड प्रोजेक्ट सेटअप से लेकर मिसिंग ExtGState एंट्रीज़ जैसे एज केस को हैंडल करने तक सब कुछ कवर करता है। अंत तक आपके पास एक PDF होगा जिसकी पहली पेज आपके द्वारा परिभाषित ग्राफ़िक्स स्टेट के साथ रेंडर होगी।

## पूर्वापेक्षाएँ

* .NET 6.0 SDK या बाद का संस्करण स्थापित हो।
* एक हालिया संस्करण का **Aspose.Pdf** NuGet पैकेज (उदाहरण के लिए, 23.12 या नया)।
* कोड से रेफ़रेंस करने योग्य फ़ोल्डर में स्थित एक इनपुट PDF फ़ाइल।
* एक डेवलपमेंट एनवायरनमेंट जैसे Visual Studio 2022 या VS Code।

## ग्राफ़िक्स स्टेट वर्कफ़्लो का अवलोकन

PDF ग्राफ़िक्स स्टेट यह नियंत्रित करता है कि ड्राइंग ऑपरेशन्स कैसे रेंडर होते हैं। दो प्रॉपर्टीज़ विज़ुअल इफ़ेक्ट्स के लिए सबसे सामान्य हैं:

* **Opacity** – `ca` (fill) और `CA` (stroke) एंट्रीज़।
* **Blend mode** – `BM` एंट्री।

ये मान एक **ExtGState dictionary** में रहते हैं जो पेज के रिसोर्स डिक्शनरी से जुड़ा होता है। नया ग्राफ़िक्स स्टेट जोड़ना तीन कार्यों से बना होता है:

1. `ExtGState` डिक्शनरी को खोजें (या बनाएं)।
2. इच्छित एंट्रीज़ के साथ एक नया graphics‑state डिक्शनरी बनाएं।
3. ड्राइंग कमांड्स से नए स्टेट को रेफ़रेंस करें (इस ट्यूटोरियल के दायरे से बाहर)।

## चरण 1: नया .NET कंसोल प्रोजेक्ट बनाएं

```bash
dotnet new console -n PdfGraphicsStateDemo
cd PdfGraphicsStateDemo
dotnet add package Aspose.Pdf
```

`dotnet add package` कमांड **Aspose.Pdf** लाइब्रेरी को लाता है, जो गाइड में पूरे उपयोग की गई API प्रदान करती है।

## चरण 2: PDF लोड करें और पहली पेज तक पहुंचें

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

// Load the source PDF
using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

// PDF pages are 1‑based; page 1 is the first page
Page firstPage = pdfDoc.Pages[1];
```

*क्यों यह महत्वपूर्ण है*: PDF ऑब्जेक्ट मॉडल 1‑आधारित इंडेक्सिंग का उपयोग करता है, इसलिए `Pages[0]` अनुरोध करने पर एक्सेप्शन फेंकेगा। `using` ब्लॉक के भीतर दस्तावेज़ लोड करने से फ़ाइल हैंडल स्वतः रिलीज़ हो जाता है।

## चरण 3: सुनिश्चित करें कि ExtGState डिक्शनरी मौजूद है

```csharp
// The page’s Resources dictionary holds many sub‑dictionaries (Font, XObject, etc.)
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

// Try to get the existing ExtGState dictionary; create one if it is missing
CosCosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and attach it to the page resources
    extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**Pro tip**: हमेशा `ExtGState` की उपस्थिति की जाँच करें। कुछ PDFs बिना इसे जनरेट होते हैं, और गैर‑मौजूद एंट्री को एडिट करने का प्रयास `KeyNotFoundException` उत्पन्न करेगा।

## चरण 4: नया ग्राफ़िक्स स्टेट बनाएं

```csharp
// Create a fresh dictionary for the new graphics state
CosCosPdfDictionary newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Stroke opacity (CA) – 1.0 means fully opaque
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes the fill 50 % transparent
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing operation
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

*इन एंट्रीज़ का कारण*:  
- `CA` लाइनों और बॉर्डर्स (stroke) को प्रभावित करता है।  
- `ca` भरे हुए आकारों और टेक्स्ट को प्रभावित करता है।  
- `BM` निर्धारित करता है कि स्रोत रंग गंतव्य के साथ कैसे ब्लेंड होता है; `"Normal"` मूल रूप को बनाए रखता है जबकि अपारदर्शिता का सम्मान करता है।

## चरण 5: ग्राफ़िक्स स्टेट को ExtGState डिक्शनरी में डालें

```csharp
// Choose a unique name for the graphics state; "GS0" is common for the first entry
extGStateDict.Add("GS0", newGraphicsState);
```

यदि आपको कई स्टेट्स चाहिए, तो सफ़िक्स (`GS1`, `GS2`, …) को बढ़ाएँ और बाद में अपने कंटेंट स्ट्रीम्स में सही नाम को रेफ़रेंस करें।

## चरण 6: संशोधित PDF को सेव करें

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
Console.WriteLine("PDF saved with new graphics state.");
```

परिणामी फ़ाइल (`output.pdf`) स्रोत के समान विज़ुअल कंटेंट रखती है, लेकिन कोई भी ड्राइंग कमांड जो बाद में `/GS0` को रेफ़रेंस करेगा, **PDF opacity** 0.5 और **PDF blend mode** `Normal` के साथ रेंडर होगा।

## पूर्ण चलाने योग्य उदाहरण

`Program.cs` में नीचे दिया गया प्रोग्राम कॉपी करें, जो चरण 1 में बनाए गए प्रोजेक्ट में है। अपने वातावरण से मेल खाने के लिए `YOUR_DIRECTORY` प्लेसहोल्डर्स को समायोजित करें।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

namespace PdfGraphicsStateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the PDF document
            using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Access the first page's resources
            Page firstPage = pdfDoc.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // 3️⃣ Retrieve or create ExtGState dictionary
            CosCosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
            {
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            }
            else
            {
                extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // 4️⃣ Define a new graphics state (opacity & blend mode)
            var newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            newGraphicsState.Add("CA", new CosPdfNumber(1));           // stroke opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));         // fill opacity
            newGraphicsState.Add("BM", new CosPdfName("Normal"));     // blend mode

            // 5️⃣ Add the graphics state to the ExtGState dictionary
            extGStateDict.Add("GS0", newGraphicsState);

            // 6️⃣ Save the modified PDF
            pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("PDF saved with new graphics state.");
        }
    }
}
```

### अपेक्षित परिणाम

`output.pdf` को किसी भी व्यूअर में खोलें। यदि आप बाद में ड्राइंग कमांड्स जोड़ते हैं जो `/GS0` को रेफ़रेंस करते हैं (उदाहरण के लिए, कंटेंट स्ट्रीम या किसी अन्य Aspose.Pdf API कॉल के माध्यम से), तो फ़िल 50 % अपारदर्शिता के साथ दिखेगा जबकि स्ट्रोक पूरी तरह अपारदर्शी रहेंगे। ब्लेंड मोड `"Normal"` बना रहेगा, जो अधिकांश कॉम्पोज़िटिंग परिदृश्यों के लिए उपयुक्त है।

## सामान्य विविधताओं को संभालना

| स्थिति | क्या बदलें | कारण |
|-----------|----------------|--------|
| **एकाधिक पृष्ठों को समान स्टेट चाहिए** | `pdfDoc.Pages` पर लूप चलाएँ और प्रत्येक पेज के लिए चरण 3‑5 दोहराएँ, या दस्तावेज़ के ग्लोबल रिसोर्सेज़ में एक ही ExtGState डिक्शनरी बनाकर उसे हर पेज से रेफ़रेंस करें। | डुप्लिकेट डिक्शनरी से बचता है और फ़ाइल आकार छोटा रखता है। |
| **प्रति पृष्ठ अलग अपारदर्शिता मान** | अलग-अलग नाम (`GS0`, `GS1`, …) उपयोग करें और प्रत्येक पेज की ExtGState में जोड़ने से पहले `ca`/`CA` को तदनुसार समायोजित करें। | रेंडरिंग पर सूक्ष्म नियंत्रण देता है। |
| **ExtGState में पहले से “GS0” नाम की कुंजी मौजूद है** | एक अलग कुंजी नाम (`GS1`, `MyState`, …) चुनें और उसे रेफ़रेंस करने वाले किसी भी कंटेंट स्ट्रीम को अपडेट करें। | मौजूदा ग्राफ़िक्स स्टेट्स के आकस्मिक ओवरराइट को रोकता है। |
| **ExtGState डिक्शनरी के बिना PDF जेनरेट हुआ** | चरण 3 में कोड पहले से ही एक बनाता है, इसलिए अतिरिक्त कार्य की आवश्यकता नहीं है। | किसी भी इनपुट PDF के लिए ऑपरेशन सफल होने की गारंटी देता है। |

## टिप्स और सर्वोत्तम प्रैक्टिसेज

* **Validate the PDF after modification** – `pdfDoc.Validate()` का उपयोग करें (नए Aspose.Pdf रिलीज़ में उपलब्ध) ताकि संरचनात्मक समस्याओं को जल्दी पकड़ा जा सके।
* **Keep the graphics‑state dictionary small** – केवल आवश्यक एंट्रीज़ शामिल करें; अतिरिक्त कुंजियाँ फ़ाइल आकार बढ़ाती हैं बिना किसी लाभ के।
* **When adding content streams that use the new state**, ड्राइंग ऑपरेटर्स से पहले `/GS0 gs` प्रीपेंड करें। उदाहरण के लिए: `contentStream.Append("/GS0 gs 100 100 m 200 200 l S");`
* **Dispose of large PDFs promptly** – उदाहरण में `using` स्टेटमेंट फ़ाइल हैंडल को रिलीज़ कर देता है, जो वेब‑सर्विस परिदृश्यों में आवश्यक है।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Pdf का उपयोग करके **add graphics state pdf** कैसे किया जाता है, **PDF opacity** को कैसे बदलें, **PDF blend mode** सेट करें, और **ExtGState dictionary** के साथ सुरक्षित रूप से काम करें। पूर्ण कोड सैंपल किसी भी .NET प्रोजेक्ट में डालने के लिए तैयार है, और साथ में दिए गए टिप्स आपको सामान्य समस्याओं से बचने में मदद करेंगे।

अगले चरण में, नए बनाए गए ग्राफ़िक्स स्टेट को टेक्स्ट, इमेज या वेक्टर शेप्स पर लागू करने का पता लगाएँ। आप अन्य ExtGState एंट्रीज़ जैसे `SM` (stroke‑adjustment) या `CA` मान जो 1 से बड़े हैं, को भी देख सकते हैं विशेष प्रभावों के लिए। हैप्पी PDF हैकिंग!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Aspose.PDF for .NET का उपयोग करके PDFs में पेज स्टैम्प कैसे जोड़ें: एक पूर्ण गाइड](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Aspose.PDF for .NET का उपयोग करके PDFs में इमेज स्टैम्प कैसे जोड़ें: चरण‑दर‑चरण गाइड](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)
- [Aspose.PDF .NET का उपयोग करके PDFs से ग्राफ़िक्स कैसे हटाएँ: एक पूर्ण गाइड](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}