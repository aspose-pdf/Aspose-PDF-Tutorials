---
category: general
date: 2026-11-16
description: Aspose.Pdf का उपयोग करके C# में PDF ग्राफ़िक्स स्टेट कैसे बनाएं, सीखें।
  यह गाइड अपारदर्शिता, ब्लेंड मोड और पूर्ण कोड उदाहरण को कवर करता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: hi
lastmod: 2026-11-16
og_description: Aspose.Pdf के साथ C# में PDF ग्राफ़िक्स स्टेट बनाएं। अपारदर्शिता और
  ब्लेंड मोड को प्रोग्रामेटिकली सेट करने के लिए इस पूर्ण ट्यूटोरियल का पालन करें।
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: C# में PDF ग्राफ़िक्स स्टेट बनाएं – चरण‑दर‑चरण Aspose.Pdf गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: C# में Aspose.Pdf के साथ PDF ग्राफ़िक्स स्टेट कैसे बनाएं
url: /hi/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create PDF graphics state in C# with Aspose.Pdf

यदि आपको **PDF ग्राफ़िक्स स्टेट** बनाना है किसी .NET प्रोजेक्ट में, तो यह ट्यूटोरियल आपको Aspose.Pdf के साथ इसे करने का सटीक तरीका दिखाता है। चाहे आप अपारदर्शिता (opacity) को नियंत्रित करना चाहते हों, ब्लेंड मोड बदलना चाहते हों, या कस्टम ग्राफ़िक्स स्टेट को कई पेज़ों में पुन: उपयोग करना चाहते हों, नीचे दिए गए चरण एक पूर्ण, तैयार‑चलाने‑योग्य समाधान प्रदान करते हैं।

इस गाइड में आप सीखेंगे कि पेज रिसोर्सेज़ तक कैसे पहुँचें, **ExtGState** एंट्री कैसे जोड़ें, और बदलावों को नई फ़ाइल में कैसे सहेजें। उदाहरण Aspose.Pdf 23.12 (या बाद के संस्करण) के साथ काम करता है और .NET 6+ को टार्गेट करता है, लेकिन अवधारणाएँ पहले के संस्करणों पर भी लागू होती हैं।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

* Visual Studio 2022 (या कोई भी C# IDE) जिसमें .NET 6 SDK स्थापित हो।  
* Aspose.Pdf for .NET लाइसेंस या एक अस्थायी इवैल्यूएशन की।  
* `input.pdf` नामक एक PDF फ़ाइल जो आप कोड से रेफ़र कर सकें ऐसी फ़ोल्डर में रखी हो।  

`Aspose.Pdf` के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है।

## What the tutorial covers

* मौजूदा PDF दस्तावेज़ को लोड करना।  
* पहले पेज के रिसोर्सेज़ डिक्शनरी तक नेविगेट करना।  
* एक नया ग्राफ़िक्स स्टेट डिक्शनरी बनाना जो स्ट्रोक अपारदर्शिता (`CA`), फ़िल अपारदर्शिता (`ca`), और ब्लेंड मोड (`BM`) को परिभाषित करता है।  
* नए ग्राफ़िक्स स्टेट को **ExtGState** कलेक्शन में कस्टम नाम (`GS0`) के साथ जोड़ना।  
* अपडेटेड PDF को सहेजना ताकि बाद के ड्रॉइंग कमांड नए स्टेट को रेफ़र कर सकें।

ट्यूटोरियल के अंत तक आप प्रोग्रामेटिक रूप से **PDF ग्राफ़िक्स स्टेट** ऑब्जेक्ट बना सकेंगे और उन्हें किसी भी ड्रॉइंग ऑपरेशन में पुन: उपयोग कर सकेंगे।

## Step 1: Set up the project and import namespaces

एक नया कंसोल एप्लिकेशन बनाएं (या कोड को मौजूदा प्रोजेक्ट में इंटीग्रेट करें)। Aspose.Pdf रेफ़रेंस जोड़ें और आवश्यक नेमस्पेसेज़ को इम्पोर्ट करें:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **प्रो टिप:** यदि आप फ्री इवैल्यूएशन वर्ज़न उपयोग कर रहे हैं, तो दस्तावेज़ लोड करने से पहले  
> `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");`  
> जोड़ें ताकि वॉटरमार्क संदेश न दिखें।

## Step 2: Load the PDF document

फ़ाइल खोलना सीधा है। `Document` क्लास पूरे PDF को दर्शाता है और आपको उसके पेज़ और रिसोर्सेज़ तक पहुँच देता है।

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

कोड को `using` ब्लॉक में रखने से फ़ाइल हैंडल ऑपरेशन के बाद रिलीज़ हो जाता है, जो प्रोडक्शन सर्विसेज़ में **C# PDF manipulation** के लिए आवश्यक है।

## Step 3: Retrieve the first page’s resources dictionary

हर PDF पेज में एक *Resources* डिक्शनरी होती है जो फ़ॉन्ट्स, इमेजेज़ और ग्राफ़िक्स स्टेट्स को स्टोर करती है। हमें इस संरचना को एडिट करने के लिए `DictionaryEditor` चाहिए।

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

यदि PDF में पहले से `ExtGState` एंट्री मौजूद है, तो `resourcesEditor["ExtGState"]` उसे रिटर्न करेगा; अन्यथा, Aspose.Pdf पहला एंट्री जोड़ते समय हमारे लिए एक खाली डिक्शनरी बना देगा।

## Step 4: Access or create the ExtGState dictionary

**ExtGState** डिक्शनरी में नामित ग्राफ़िक्स स्टेट ऑब्जेक्ट्स रखे जाते हैं। हम या तो मौजूदा को फ़ेच करेंगे या नया कंटेनर बनाएँगे।

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

जब `ExtGState` मौजूद नहीं होता, तो `resourcesEditor["ExtGState"]` स्वचालित रूप से एक नई खाली डिक्शनरी रिटर्न करता है, जिससे कोड किसी भी PDF पर काम करता है।

## Step 5: Build the new graphics state dictionary

एक ग्राफ़िक्स स्टेट `CosPdfDictionary` होता है जिसमें विशिष्ट कुंजियाँ होती हैं:

* `CA` – स्ट्रोक अपारदर्शिता (0‑1)  
* `ca` – फ़िल अपारदर्शिता (0‑1)  
* `BM` – ब्लेंड मोड (`Normal`, `Multiply`, आदि)

हम एक खाली डिक्शनरी बनाते हैं, उसे भरते हैं, और फिर `ExtGState` में जोड़ते हैं।

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

आप `0.5` को `0` से `1` के बीच किसी भी मान में बदल सकते हैं फ़िल अपारदर्शिता को समायोजित करने के लिए, या `"Normal"` को `"Multiply"` से बदल सकते हैं अलग **PDF blend mode** के लिए। यह लचीलापन ही कारण है कि कस्टम ग्राफ़िक्स स्टेट बनाना **Aspose.Pdf graphics state** हैंडलिंग में एक शक्तिशाली तकनीक है।

## Step 6: Register the graphics state with a name

PDF कंटेंट स्ट्रीम्स ग्राफ़िक्स स्टेट को नाम से रेफ़र करती हैं। यहाँ हम `GS0` उपयोग कर रहे हैं, लेकिन कोई भी यूनिक नाम काम करेगा।

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

यदि आपको कई स्टेट्स चाहिए, तो अलग-अलग पैरामीटर के साथ निर्माण चरण दोहराएँ और उन्हें `GS1`, `GS2`, आदि के रूप में जोड़ें। यह पैटर्न जटिल दस्तावेज़ों में विभिन्न लेयरों पर अलग‑अलग अपारदर्शिता या ब्लेंड सेटिंग्स की आवश्यकता होने पर अच्छी तरह स्केल करता है।

## Step 7: Save the modified PDF

अंत में, अपडेटेड दस्तावेज़ को नई फ़ाइल में लिखें। मूल फ़ाइल को अपरिवर्तित रखना डिबगिंग को आसान बनाता है।

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

चलाने के बाद, `output.pdf` में `GS0` नाम की `ExtGState` एंट्री होगी। कोई भी बाद का ड्रॉइंग ऑपरेटर इसे `gs` ऑपरेटर (जैसे, कंटेंट स्ट्रीम में `GS0 gs`) के माध्यम से रेफ़र कर सकता है।  

> **क्यों महत्वपूर्ण है:** एक पुन: उपयोग योग्य ग्राफ़िक्स स्टेट बनाकर आप प्रत्येक ड्रॉइंग कमांड के लिए अपारदर्शिता और ब्लेंड सेटिंग्स दोहराने से बचते हैं, जिससे प्रदर्शन और मेंटेनबिलिटी दोनों में सुधार होता है।

## Using the new graphics state in a content stream (optional)

यदि आप तुरंत प्रभाव देखना चाहते हैं, तो एक साधा रेक्टैंगल जोड़ें जो अभी बनाए गए स्टेट को उपयोग करता हो:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

यह रेक्टैंगल 50 % फ़िल अपारदर्शिता के साथ ड्रॉ होगा जबकि स्ट्रोक पूरी तरह अपारदर्शी रहेगा, ठीक उसी तरह जैसा **create PDF graphics state** डिक्शनरी में परिभाषित है।

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| `ExtGState` entry not found | कुछ PDFs पूरी तरह से डिक्शनरी को छोड़ देते हैं। | `DictionaryEditor` पहली एंट्री जोड़ते समय इसे स्वचालित रूप से बनाता है, इसलिए अतिरिक्त चेक की आवश्यकता नहीं। |
| Opacity values > 1 or < 0 | PDF स्पेसिफ़िकेशन अपारदर्शिता को `[0,1]` रेंज तक सीमित करता है। | `CosPdfNumber` बनाने से पहले मान को क्लैंप (सीमित) करें। |
| Blend mode typo | PDF ब्लेंड मोड नाम केस‑सेंसिटिव होते हैं। | ठीक‑ठीक नाम जैसे `"Normal"`, `"Multiply"`, `"Screen"` उपयोग करें। |
| License watermark | इवैल्यूएशन वर्ज़न पहली पेज़ पर वॉटरमार्क जोड़ता है। | दस्तावेज़ खोलने से पहले वैध लाइसेंस फ़ाइल लागू करें। |

इन एज केसों को संभालने से आपका **create PDF graphics state** इम्प्लीमेंटेशन विभिन्न PDF स्रोतों पर भरोसेमंद रूप से काम करता है।

## Full, runnable example

नीचे एक स्व-समाहित प्रोग्राम दिया गया है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं। `YOUR_DIRECTORY` को अपने मशीन पर वास्तविक फ़ोल्डर पाथ से बदलें।

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}