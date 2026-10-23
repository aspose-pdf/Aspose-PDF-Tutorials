---
category: general
date: 2026-10-23
description: C# में Aspose.Pdf का उपयोग करके PDF की अपारदर्शिता कैसे बदलें। ExtGState
  को संपादित करना, स्ट्रोक/फ़िल अपारदर्शिता सेट करना, और कुछ ही कोड लाइनों में ब्लेंड
  मोड लागू करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change PDF opacity
- Aspose.Pdf opacity
- PDF graphics state
- ExtGState dictionary
- C# PDF manipulation
- PDF blend mode
language: hi
lastmod: 2026-10-23
og_description: C# में Aspose.Pdf का उपयोग करके PDF की अपारदर्शिता कैसे बदलें। स्ट्रोक
  और फ़िल अपारदर्शिता को संशोधित करने, ब्लेंड मोड सेट करने और अपडेटेड दस्तावेज़ को
  सहेजने के लिए इस संक्षिप्त गाइड का पालन करें।
og_image_alt: Screenshot of a PDF page with semi‑transparent graphics created by Aspose.Pdf
  in C#
og_title: C# में PDF की अपारदर्शिता कैसे बदलें – पूर्ण Aspose.Pdf ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  headline: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  name: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf;'
  - name: Get the first page and its resource dictionary
    text: '```csharp // Step 2: Get the first page and its resource dictionary var
      firstPage = pdfDocument.Pages[1]; var resourcesEditor = new DictionaryEditor(firstPage.Resources);
      ```'
  - name: Retrieve (or create) the ExtGState dictionary
    text: '```csharp // Step 3: Retrieve the ExtGState dictionary from the page resources
      // If ExtGState does not exist, create an empty one. CosPdfDictionary extGStateDict;
      if (resourcesEditor.ContainsKey("ExtGState")) { extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
      } else { extGStateDic'
  - name: Create a new graphics state dictionary and define opacity entries
    text: '```csharp // Step 4: Create a new graphics state dictionary and define
      its entries var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
      var graphicsStateEntries = new[] { new KeyValuePair<string, ICosPdfPrimitive>("CA",
      new CosPdfNumber(1.0)), // Stroke opacity (fully opaque)'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Step 5: Add the new graphics state to the ExtGState dictionary
      (named "GS0") extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: Save the updated PDF document
    text: '```csharp // Step 6: Save the updated PDF document pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      } ```'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Opacity
- GraphicsState
title: C# में Aspose.Pdf के साथ PDF की अपारदर्शिता कैसे बदलें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/programming-with-operators/how-to-change-pdf-opacity-in-c-with-aspose-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose.Pdf के साथ PDF अपारदर्शिता कैसे बदलें – चरण‑दर‑चरण गाइड

यदि आपको विशिष्ट तत्वों के लिए **PDF अपारदर्शिता कैसे बदलें** की आवश्यकता है, तो यह ट्यूटोरियल एक पूर्ण, चलाने योग्य समाधान दिखाता है। आप देखेंगे कि ExtGState डिक्शनरी को कैसे संपादित करें, स्ट्रोक और फ़िल अपारदर्शिता दोनों सेट करें, और ब्लेंड मोड चुनें—सभी कुछ स्पष्ट C# कोड लाइनों के साथ।

PDF अपारदर्शिता बदलना उपयोगी होता है जब आप वॉटरमार्क, ओवरले ग्राफ़िक्स, या सूक्ष्म दृश्य प्रभाव बनाना चाहते हैं बिना पूरे दस्तावेज़ को पुनः निर्मित किए। गाइड मानता है कि आपके पास एक बेसिक C# वातावरण और Aspose.Pdf for .NET लाइब्रेरी स्थापित है।

![how to change PDF opacity using Aspose.Pdf in C#](https://example.com/og-image.png)

## आवश्यकताएँ

* .NET 6.0 या बाद का (कोड .NET Framework 4.7+ के साथ भी काम करता है)
* **Aspose.Pdf for .NET** की लाइसेंस प्राप्त प्रति (नि:शुल्क ट्रायल परीक्षण के लिए काम करता है)
* एक इनपुट PDF फ़ाइल जो ऐसे फ़ोल्डर में स्थित हो जिसे आप कोड से संदर्भित कर सकें
* Visual Studio 2022 या कोई भी पसंदीदा C# एडिटर

कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है—Aspose.Pdf में इस ट्यूटोरियल में उपयोग किए गए सभी प्रकार शामिल हैं।

## PDF ग्राफ़िक्स स्टेट को समझना

एक PDF पेज ड्राइंग पैरामीटर को **graphics state** ऑब्जेक्ट में संग्रहीत करता है। **ExtGState** डिक्शनरी में निम्नलिखित एंट्रीज़ होती हैं:

* **CA** – स्ट्रोक अपारदर्शिता (0 = पारदर्शी, 1 = अपारदर्शी)
* **ca** – फ़िल अपारदर्शिता
* **BM** – ब्लेंड मोड (जैसे, *Normal*, *Multiply*, *Screen*)

एक नया ग्राफ़िक्स स्टेट डिक्शनरी बनाकर और उसे पेज के ExtGState संग्रह में जोड़कर, आप बाद में कंटेंट स्ट्रीम में इस स्टेट को संदर्भित कर सकते हैं। यह तरीका पूरे पेज कंटेंट को पुनः लिखने से बचाता है और किसी भी मौजूदा PDF के साथ काम करता है।

## Aspose.Pdf के साथ PDF अपारदर्शिता कैसे बदलें

निम्नलिखित छह चरण पूरे प्रक्रिया को कवर करते हैं—दस्तावेज़ लोड करने से लेकर संशोधित फ़ाइल सहेजने तक। प्रत्येक चरण में आपको आवश्यक सटीक कोड और यह समझाया गया है कि वह चरण क्यों महत्वपूर्ण है।

### चरण 1: PDF दस्तावेज़ लोड करें

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

**यह क्यों महत्वपूर्ण है** – `Aspose.Pdf.Document` से फ़ाइल खोलने से आपको PDF की आंतरिक संरचना तक पूर्ण पहुँच मिलती है, जिसमें पेज रिसोर्सेज शामिल हैं जहाँ **ExtGState** डिक्शनरी स्थित होती है।

### चरण 2: पहला पेज और उसका रिसोर्स डिक्शनरी प्राप्त करें

```csharp
// Step 2: Get the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**यह क्यों महत्वपूर्ण है** – प्रत्येक पेज में एक *Resources* डिक्शनरी होती है जो फ़ॉन्ट, इमेज और ग्राफ़िक्स स्टेट्स को समूहित करती है। `DictionaryEditor` उस संग्रह तक सुविधाजनक पढ़ने/लिखने की पहुँच प्रदान करता है।

### चरण 3: ExtGState डिक्शनरी प्राप्त करें (या बनाएं)

```csharp
// Step 3: Retrieve the ExtGState dictionary from the page resources
// If ExtGState does not exist, create an empty one.
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**यह क्यों महत्वपूर्ण है** – कुछ PDFs में पहले से ही **ExtGState** एंट्री होती है; अन्य में नहीं। शर्तीय लॉजिक सुनिश्चित करता है कि ट्यूटोरियल दोनों मामलों में काम करे, जिससे यह वास्तविक‑दुनिया की फ़ाइलों के लिए मजबूत बनता है।

### चरण 4: नया ग्राफ़िक्स स्टेट डिक्शनरी बनाएं और अपारदर्शिता एंट्रीज़ परिभाषित करें

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

**यह क्यों महत्वपूर्ण है** – ये तीन मुख्य एंट्रीज़ यह नियंत्रित करती हैं कि ड्राइंग कमांड कैसे रेंडर होते हैं:

* `CA = 1.0` स्ट्रोक लाइनों को पूरी तरह दृश्यमान रखता है।
* `ca = 0.5` भराव वाले आकारों को अर्द्ध‑पारदर्शी बनाता है।
* `BM = Normal` डिफ़ॉल्ट ब्लेंड मोड का उपयोग करता है; आप रचनात्मक प्रभावों के लिए `"Normal"` को `"Multiply"` या `"Screen"` से बदल सकते हैं।

### चरण 5: नया ग्राफ़िक्स स्टेट ExtGState डिक्शनरी में जोड़ें

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary (named "GS0")
extGStateDict.Add("GS0", graphicsStateDict);
```

**यह क्यों महत्वपूर्ण है** – एंट्री का नाम `"GS0"` रखने से एक रेफ़रेंस बनता है जिसे आप बाद में कंटेंट स्ट्रीम (`/GS0 gs`) में उपयोग कर सकते हैं। यदि आपको कई अपारदर्शिता वैरिएशन चाहिए, तो अलग-अलग `CA`/`ca` मानों के साथ अतिरिक्त एंट्रीज़ (`"GS1"`, `"GS2"`, …) जोड़ें।

### चरण 6: अपडेटेड PDF दस्तावेज़ सहेजें

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**यह क्यों महत्वपूर्ण है** – परिवर्तन को स्थायी बनाकर संशोधित **ExtGState** डिक्शनरी फ़ाइल में वापस लिखी जाती है। resulting PDF अब एक पुन: उपयोग योग्य ग्राफ़िक्स स्टेट रखता है जिसे कोई भी ड्राइंग कमांड उपयोग कर सकता है।

## पेज कंटेंट में नया ग्राफ़िक्स स्टेट लागू करना

ऊपर के चरण केवल ग्राफ़िक्स स्टेट बनाते हैं; आपको इसे पेज के कंटेंट स्ट्रीम में संदर्भित करना होगा। यहाँ एक त्वरित उदाहरण है जो हमने अभी जोड़ी गई स्टेट का उपयोग करके अर्द्ध‑पारदर्शी आयत बनाता है:

```csharp
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    var page = pdfDocument.Pages[1];
    var content = new PageContentEditor(page);
    // Begin the graphics state GS0
    content.InsertContent(0, "q /GS0 gs\n"); // Save graphics state and apply GS0
    // Draw a rectangle (100,100) to (300,300)
    content.InsertContent(0, "0.2 0.6 0.8 rg\n"); // Set fill color (light blue)
    content.InsertContent(0, "100 100 200 200 re\n");
    content.InsertContent(0, "f\n"); // Fill rectangle with current fill opacity
    // Restore graphics state
    content.InsertContent(0, "Q\n");
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**व्याख्या** – `q` ऑपरेटर वर्तमान ग्राफ़िक्स स्टेट को सहेजता है, `/GS0 gs` अपारदर्शिता सेटिंग्स लागू करता है, आयत खींची जाती है, और `Q` मूल स्टेट को पुनर्स्थापित करता है। आप इस स्निपेट को पेज पर कहीं भी रख सकते हैं, मौजूदा कंटेंट से पहले या बाद में, आपके वांछित विज़ुअल लेयरिंग के अनुसार।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| लक्षण | कारण | समाधान |
|---------|-------|-----|
| अपारदर्शिता अपरिवर्तित दिखती है | पेज में ExtGState एंट्री नहीं है या कंटेंट नई स्टेट को संदर्भित नहीं करता। | `ExtGState` मौजूद है और कंटेंट स्ट्रीम में `/GS0 gs` (या आपका चुना हुआ नाम) शामिल है, यह सत्यापित करें। |
| ब्लेंड मोड का कोई प्रभाव नहीं | असंगत रंग स्थान या PDF संस्करण का उपयोग। | PDF संस्करण कम से कम 1.4 हो (पारदर्शिता के लिए आवश्यक) और आप स्पॉट रंगों को ब्लेंड मोड्स के साथ मिलाते नहीं हैं, यह सुनिश्चित करें। |
| दस्तावेज़ पुराने व्यूअर्स में नहीं खुलता | PDF 1.3 या उससे पहले में पारदर्शिता समर्थित नहीं है। | सेव करने से पहले `pdfDocument.Version = 1.4;` सेट करें, या स्पष्ट रूप से PDF संस्करण को अपग्रेड करें। |

## परिणाम का परीक्षण

`output.pdf` को Adobe Acrobat Reader, Foxit, या किसी भी आधुनिक PDF व्यूअर में खोलें। आपको आयत 50 % फ़िल अपारदर्शिता के साथ रेंडर होती दिखनी चाहिए जबकि उसकी बॉर्डर पूरी तरह अपारदर्शी रहती है। *Edit → Preferences → Accessibility* विकल्पों का उपयोग करके “Use high‑contrast colors” को टॉगल करें और पुष्टि करें कि अर्द्ध‑पारदर्शी प्रभाव बना रहता है।

यदि आपको प्रोग्रामेटिक रूप से सत्यापित करना है, तो Aspose.Pdf आपको ग्राफ़िक्स स्टेट को वापस पढ़ने की सुविधा देता है:

```csharp
var gs = pdfDocument.Pages[1].Resources["ExtGState"]["GS0"].ToCosPdfDictionary();
var fillOpacity = ((CosPdfNumber)gs["ca"]).Value; // Should be 0.5
```

## तकनीक का विस्तार

* **एकाधिक अपारदर्शिता स्तर** – विभिन्न `ca` मानों के साथ अधिक एंट्रीज़ (`"GS1"`, `"GS2"`) जोड़ें और जहाँ आवश्यक हो वहाँ संदर्भित करें।
* **विभिन्न ब्लेंड मोड्स** – कलात्मक ओवरले के लिए `"Normal"` को `"Multiply"` या `"Screen"` से बदलें।
* **इमेजेज़ पर लागू करना** – `Do` ऑपरेटर जो XObject इमेज ड्रॉ करता है, उससे पहले वही ग्राफ़िक्स स्टेट उपयोग करें।

## निष्कर्ष

अब आप **C# में Aspose.Pdf का उपयोग करके PDF अपारदर्शिता कैसे बदलें** जानते हैं। एक कस्टम ग्राफ़िक्स स्टेट बनाकर, उसे पेज के ExtGState डिक्शनरी में जोड़कर, और कंटेंट स्ट्रीम में स्टेट को कॉल करके, आप स्ट्रोक और फ़िल ट्रांसपेरेंसी तथा ब्लेंड मोड्स पर सूक्ष्म नियंत्रण प्राप्त करते हैं। पूरा उदाहरण कॉपी, रन और किसी भी PDF मैनिपुलेशन परिदृश्य में अनुकूलित करने के लिए तैयार है।

अगली चुनौती के लिए तैयार हैं? इस तकनीक को इमेजेज़ पर **Aspose.Pdf opacity** के साथ मिलाएँ, या पेशेवर‑ग्रेड ओवरले बनाने के लिए **PDF blend mode** प्रभावों का अन्वेषण करें। कोडिंग का आनंद लें!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का पता लगाने में मदद करेंगे।

- [Aspose.PDF के साथ PDF अपारदर्शिता बदलें – पूर्ण C# गाइड](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [C# में Aspose.Pdf के साथ PDF अपारदर्शिता बदलें – चरण‑दर‑चरण गाइड](/pdf/english/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/)
- [C# में Aspose.Pdf का उपयोग करके PDF पारदर्शिता कैसे बदलें](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}