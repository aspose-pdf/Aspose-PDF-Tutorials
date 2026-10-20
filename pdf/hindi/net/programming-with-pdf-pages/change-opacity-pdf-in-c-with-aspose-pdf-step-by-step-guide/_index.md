---
category: general
date: 2026-08-11
description: C# में Aspose.Pdf का उपयोग करके PDF की अपारदर्शिता बदलें। जानें कैसे
  PDF पृष्ठों में पारदर्शिता जोड़ें, ग्राफिक स्टेट सेट करें, और परिणाम को जल्दी सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change opacity PDF
- how to add transparency
- add pdf transparency
language: hi
lastmod: 2026-08-11
og_description: Aspose.Pdf के साथ C# में PDF की अपारदर्शिता बदलें। इस गाइड को फॉलो
  करें ताकि आप देख सकें कि किसी भी PDF दस्तावेज़ में पारदर्शिता कैसे जोड़ें, ग्राफ़िक्स
  स्टेट्स को कस्टमाइज़ करें, और परिणाम को एक्सपोर्ट करें।
og_image_alt: Screenshot illustrating change opacity PDF example in C# code
og_title: C# में PDF की अपारदर्शिता बदलें – पूर्ण Aspose.Pdf ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  headline: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  name: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
    text: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
  - name: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
    text: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
  - name: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
    text: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
  - name: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
    text: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Aspose.Pdf के साथ C# में PDF की अपारदर्शिता बदलें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose.Pdf के साथ PDF की अपारदर्शिता बदलें – चरण‑दर‑चरण गाइड

यदि आपको प्रोग्रामेटिकली **PDF की अपारदर्शिता बदलनी** है, तो यह ट्यूटोरियल आपको ठीक‑ठीक दिखाता है कि कैसे। Aspose.Pdf for .NET का उपयोग करके आप ग्राफ़िक्स ऑब्जेक्ट्स, टेक्स्ट और इमेजेज़ की ट्रांसपेरेंसी को अपने C# कोड से बाहर निकले बिना नियंत्रित कर सकते हैं।

आगे के सेक्शन में आप सीखेंगे **कैसे PDF पेज में ट्रांसपेरेंसी जोड़ें**, ग्राफ़िक्स स्टेट ऑब्जेक्ट्स का क्या मतलब है, और संशोधित दस्तावेज़ को कैसे सहेजें। गाइड में **PDF ट्रांसपेरेंसी जोड़ते** समय आम समस्याओं को भी कवर किया गया है और वास्तविक परिदृश्यों के लिए टिप्स दिए गए हैं।

## आप क्या हासिल करेंगे

* एक मौजूदा PDF दस्तावेज़ लोड करें।
* एक नया ग्राफ़िक्स स्टेट डिक्शनरी बनाएं जो अपारदर्शिता मान निर्धारित करता है।
* ग्राफ़िक्स स्टेट को पेज के रिसोर्स डिक्शनरी में डालें।
* दस्तावेज़ को अपडेटेड **PDF अपारदर्शिता परिवर्तन** प्रभाव के साथ सहेजें।

कोई बाहरी टूल आवश्यक नहीं—सिर्फ Aspose.Pdf for .NET लाइब्रेरी (वर्ज़न 23.10 या बाद का) और एक .NET डेवलपमेंट एनवायरनमेंट।

## पूर्वापेक्षाएँ

* .NET 6.0 (या .NET Framework 4.7.2+) स्थापित हो।
* Visual Studio 2022 या कोई भी C#‑संगत IDE।
* `Aspose.Pdf` NuGet पैकेज का रेफ़रेंस।
* एक इनपुट PDF फ़ाइल (`input.pdf`) जो लिखने योग्य डायरेक्टरी में स्थित हो।

> **प्रो टिप:** अपारदर्शिता परिवर्तन का परीक्षण करते समय, ऐसे PDF के साथ काम करें जिसमें पहले से वेक्टर ग्राफ़िक्स या टेक्स्ट हो; रास्टर इमेजेज़ `ca` और `CA` पैरामीटर को अनदेखा करती हैं जब तक कि वे ट्रांसपेरेंसी ग्रुप के अंदर न हों।

## Aspose.Pdf के साथ PDF की अपारदर्शिता बदलें

समाधान का मूल भाग पेज के **ExtGState** (external graphics state) डिक्शनरी को संशोधित करना है। यह डिक्शनरी **ca** (stroke opacity) और **CA** (fill opacity) जैसे पैरामीटर स्टोर करती है। नया एंट्री जोड़कर आप बाद में कंटेंट स्ट्रीम में इसका रेफ़रेंस दे सकते हैं।

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;

class ChangeOpacityPdfExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var document = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 2: Access the first page and its resource dictionary
            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Step 3: Create a new graphics state dictionary with desired opacity values
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                // Fill opacity (CA) – 1.0 means fully opaque
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                // Stroke opacity (ca) – 0.5 makes lines semi‑transparent
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                // Blend mode (BM) – Normal is the default blend mode
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // Step 4: Add the new graphics state to the ExtGState dictionary
            // “GS0” is the identifier you will reference later in the content stream
            extGState.Add("GS0", newGraphicsState);

            // Optional: Demonstrate usage by drawing a semi‑transparent rectangle
            // This part shows how the new graphics state affects drawing commands.
            var canvas = new Aspose.Pdf.Drawing.Graphic(page);
            canvas.SetGraphicsState("GS0"); // Apply the opacity settings
            canvas.Rectangle(100, 500, 200, 600);
            canvas.FillColor = Color.FromRgb(255, 0, 0); // Red fill
            canvas.StrokeColor = Color.FromRgb(0, 0, 255); // Blue border
            canvas.Draw();

            // Step 5: Save the modified PDF
            document.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF saved with changed opacity.");
    }
}
```

### क्यों यह काम करता है

* **ExtGState** एक PDF रिसोर्स है जो पुन: उपयोग योग्य ग्राफ़िक्स पैरामीटर स्टोर करता है। एक कस्टम एंट्री (`GS0`) जोड़ने से आप एक पुन: उपयोग योग्य अपारदर्शिता कॉन्फ़िगरेशन बनाते हैं।
* **ca** कुंजी स्ट्रोक ऑपरेशन्स (लाइन, बॉर्डर) की अपारदर्शिता नियंत्रित करती है। **CA** कुंजी फ़िल ऑपरेशन्स (रंगीन शैप, टेक्स्ट) की अपारदर्शिता नियंत्रित करती है। `ca = 0.5` सेट करने से स्ट्रोक 50 % ट्रांसपेरेंट हो जाता है, जबकि `CA = 1` फ़िल को पूरी तरह अपारदर्शी रखता है।
* `SetGraphicsState("GS0")` कॉल Aspose.Pdf को कंटेंट स्ट्रीम में `/GS0 gs` ऑपरेटर इमीट करने को कहता है, जिससे सभी बाद के ड्रॉइंग कमांड्स के लिए नई ट्रांसपेरेंसी सेटिंग सक्रिय हो जाती है।

## मौजूदा कंटेंट में ट्रांसपेरेंसी कैसे जोड़ें

यदि पेज पर पहले से टेक्स्ट या इमेजेज़ हैं और आप उन्हें फिर से ड्रॉ किए बिना अर्ध‑ट्रांसपेरेंट बनाना चाहते हैं, तो आप मौजूदा कंटेंट से पहले एक **gs** ऑपरेटर इंजेक्ट कर सकते हैं। नीचे दिया गया स्निपेट पेज की कंटेंट स्ट्रीम के पहले इस ऑपरेटर को प्रीपेंड करने का तरीका दिखाता है।

```csharp
// Retrieve the existing content stream
var content = page.Contents[1];
var originalBytes = content.ToByteArray();

// Build the new content with the graphics state applied
var gsOperator = System.Text.Encoding.ASCII.GetBytes("/GS0 gs\n");
var newBytes = new List<byte>(gsOperator);
newBytes.AddRange(originalBytes);

// Replace the page content
page.Contents[1].Replace(newBytes.ToArray());
```

### किनारे के केस और विचार

| स्थिति | सिफ़ारिश किया गया समाधान |
|-----------|----------------------|
| **Multiple pages** | `document.Pages` पर लूप करें और प्रत्येक पेज के लिए चरण 2‑4 दोहराएँ जिसे आप प्रभावित करना चाहते हैं। |
| **Different opacity per element** | अतिरिक्त ग्राफ़िक्स स्टेट्स (`GS1`, `GS2`, …) बनाएं जिनमें अलग‑अलग `ca`/`CA` मान हों और उन्हें चयनित रूप से लागू करें। |
| **PDFs with existing ExtGState entries** | `dictEditor["ExtGState"]` को सुरक्षित रूप से उपयोग करें; यदि कुंजी मौजूद नहीं है, तो एक नया `CosPdfDictionary` बनाकर `page.Resources` को असाइन करें। |
| **Transparency groups** | जटिल कंपोज़िटिंग (जैसे ओवरलैपिंग इमेजेज़) के लिए `/Group` डिक्शनरी को `S /Transparency` और `CS /DeviceRGB` के साथ सेट करें। यह बेसिक **PDF अपारदर्शिता परिवर्तन** से आगे है लेकिन उन्नत लेआउट्स के लिए आवश्यक हो सकता है। |

## वेक्टर ग्राफ़िक्स में PDF ट्रांसपेरेंसी जोड़ें

आयतों के अलावा, आप वही ग्राफ़िक्स स्टेट किसी भी वेक्टर ड्रॉइंग—लाइन, कर्व, या यहाँ तक कि टेक्स्ट—पर लागू कर सकते हैं। यहाँ एक त्वरित उदाहरण है जो अर्ध‑ट्रांसपेरेंट टेक्स्ट लिखता है:

```csharp
var textFragment = new TextFragment("Transparent text")
{
    Position = new Position(100, 400),
    TextState = { FontSize = 36, ForegroundColor = Color.Black }
};
page.Paragraphs.Add(textFragment);

// Apply the graphics state to the text fragment
textFragment.TextState.GraphicsState = "GS0";
```

`TextState` की `GraphicsState` प्रॉपर्टी PDF इंजन को बताती है कि टेक्स्ट को `GS0` में परिभाषित अपारदर्शिता के साथ रेंडर किया जाए। यह **PDF ट्रांसपेरेंसी जोड़ने** का सबसे सीधा तरीका है।

## PDF की अपारदर्शिता बदलते समय आम समस्याएँ

1. **Missing ExtGState dictionary** – कुछ PDFs में डिफ़ॉल्ट रूप से `ExtGState` एंट्री नहीं होती। ऐसे में इसे बनाएं:  
   ```csharp
   if (!dictEditor.ContainsKey("ExtGState"))
       dictEditor.Add("ExtGState", new CosPdfDictionary(document));
   ```
2. **Incorrect resource name** – `SetGraphicsState` में उपयोग किया गया नाम बिल्कुल वही कुंजी होना चाहिए जो आपने जोड़ी है (`GS0`)। टाइपो होने पर डिफ़ॉल्ट, पूरी तरह अपारदर्शी रेंडरिंग होगी।
3. **Overriding existing graphics states** – नया एंट्री जोड़ना मौजूदा एंट्री को रिप्लेस नहीं करता। यदि आप ऐसा नाम दोबारा उपयोग करते हैं जो पहले से मौजूद है, तो अनजाने में अन्य पेज एलिमेंट्स को प्रभावित कर सकते हैं जो उसी का रेफ़रेंस रखते हैं।
4. **Viewer compatibility** – पुराने PDF व्यूअर्स (pre‑1.4) ट्रांसपेरेंसी को अनदेखा कर सकते हैं। सुनिश्चित करें कि आपका लक्ष्य दर्शक आधुनिक व्यूअर जैसे Adobe Reader DC या Chrome के बिल्ट‑इन PDF व्यूअर का उपयोग करे।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, स्व-निहित प्रोग्राम दिया गया है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं। इसमें सभी आवश्यक `using` निर्देश, एरर हैंडलिंग और टिप्पणी शामिल हैं।

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Text;
using System.Drawing; // For Color

class ChangeOpacityPdfFull
{
    static void Main()
    {
        const string inputPath = "YOUR_DIRECTORY/input.pdf";
        const string outputPath = "YOUR_DIRECTORY/output.pdf";

        // Load the PDF
        using (var document = new Document(inputPath))
        {
            // Ensure the first page exists
            if (document.Pages.Count == 0)
                throw new InvalidOperationException("The PDF contains no pages.");

            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);

            // Create ExtGState dictionary if it does not exist
            if (!dictEditor.ContainsKey("ExtGState"))
                dictEditor.Add("ExtGState", new CosPdfDictionary(document));

            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Define a new graphics state with 50 % stroke opacity
            var opacityState = CosPdfDictionary.CreateEmptyDictionary(document);
            opacityState.Add("CA", new CosPdfNumber(1));   // Fill opacity = 100 %
            opacityState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity = 50 %
            opacityState.Add("BM", new CosPdfName("Normal"));

            // Add the state under the name "


## अब आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Aspose.PDF .NET का उपयोग करके PDF में टेक्स्ट स्टैम्प कैसे जोड़ें: व्यापक गाइड](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Aspose.PDF for .NET का उपयोग करके PDFs में पेज स्टैम्प कैसे जोड़ें: पूर्ण गाइड](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Aspose.PDF for .NET का उपयोग करके PDFs में पेज स्टैम्प कैसे जोड़ें | वॉटरमार्क्स और बैकग्राउंड गाइड](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}