---
category: general
date: 2026-11-16
description: Aspose.Pdf का उपयोग करके PDF में पारदर्शिता सेट करने के लिए PDF संसाधनों
  को संपादित करके और PDF को कुशलतापूर्वक लोड करके। इस पूर्ण C# गाइड का पालन करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- edit pdf resources
- load pdf aspose
language: hi
lastmod: 2026-11-16
og_description: Aspose.Pdf का उपयोग करके PDF में पारदर्शिता कैसे सेट करें, जिससे ग्राफ़िक्स
  की सटीक अपारदर्शिता नियंत्रण सीधे C# से संभव हो।
og_image_alt: C# code snippet that sets PDF transparency via Aspose.Pdf
og_title: Aspose.Pdf के साथ PDF पारदर्शिता सेट करें – चरण‑दर‑चरण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to set transparency in a PDF with Aspose.Pdf by editing PDF resources
    and loading the PDF efficiently. Follow this complete C# guide.
  headline: How to set transparency in a PDF using Aspose.Pdf
  type: TechArticle
- description: How to set transparency in a PDF with Aspose.Pdf by editing PDF resources
    and loading the PDF efficiently. Follow this complete C# guide.
  name: How to set transparency in a PDF using Aspose.Pdf
  steps:
  - name: '**Load the PDF** with Aspose.Pdf (`load pdf aspose`).'
    text: '**Load the PDF** with Aspose.Pdf (`load pdf aspose`).'
  - name: '**Access the first page’s resources** dictionary (`edit pdf resources`).'
    text: '**Access the first page’s resources** dictionary (`edit pdf resources`).'
  - name: '**Create a custom ExtGState** that contains the desired transparency values.'
    text: '**Create a custom ExtGState** that contains the desired transparency values.'
  - name: '**Insert the ExtGState** back into the page resources.'
    text: '**Insert the ExtGState** back into the page resources.'
  - name: '**Save the modified PDF**.'
    text: '**Save the modified PDF**.'
  type: HowTo
tags:
- PDF
- Aspose.Pdf
- C#
title: Aspose.Pdf का उपयोग करके PDF में पारदर्शिता कैसे सेट करें
url: /hi/net/images-graphics/how-to-set-transparency-in-a-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf का उपयोग करके PDF में ट्रांसपेरेंसी कैसे सेट करें

यदि आपको PDF दस्तावेज़ में **how to set transparency** सेट करने की आवश्यकता है, तो यह ट्यूटोरियल Aspose.Pdf for .NET के साथ सटीक कदम दिखाता है। चाहे आप रिपोर्टिंग इंजन बना रहे हों या वॉटरमार्क जोड़ रहे हों, अपारदर्शिता को नियंत्रित करना एक सामान्य आवश्यकता है। गाइड के अंत तक आपके पास एक चलाने योग्य C# प्रोग्राम होगा जो PDF लोड करता है, उसके संसाधनों को संपादित करता है, और परिणाम को डिस्क पर वापस लिखता है।

PDF के साथ काम करते समय अक्सर आपको **edit PDF resources** जैसी चीज़ें करनी पड़ती हैं, जैसे ExtGState डिक्शनरी, और आपको **load PDF Aspose** को सही तरीके से लोड करना भी आवश्यक है ताकि खराब आउटपुट न हो। यह गाइड दोनों पहलुओं को कवर करता है और समझाता है कि प्रत्येक ऑपरेशन क्यों महत्वपूर्ण है, ताकि आप इस पैटर्न को मल्टी‑पेज दस्तावेज़ों या कस्टम ग्राफ़िक्स स्टेट्स में अनुकूलित कर सकें।

## PDF में ट्रांसपेरेंसी सेट करने का अवलोकन

PDF में ट्रांसपेरेंसी को *ExtGState* (external graphics state) ऑब्जेक्ट द्वारा परिभाषित किया जाता है। यह ऑब्जेक्ट पैरामीटर जैसे स्ट्रोक अपारदर्शिता (`CA`), फ़िल अपारदर्शिता (`ca`), और ब्लेंड मोड (`BM`) को संग्रहीत करता है। Aspose.Pdf आपको इन डिक्शनरीज़ को सीधे बदलने की अनुमति देता है, जिससे आप उच्च‑स्तरीय APIs पर निर्भर हुए बिना सूक्ष्म नियंत्रण प्राप्त कर सकते हैं।

समग्र प्रवाह इस प्रकार है:

1. **Load the PDF** with Aspose.Pdf (`load pdf aspose`).
2. **Access the first page’s resources** dictionary (`edit pdf resources`).
3. **Create a custom ExtGState** that contains the desired transparency values.
4. **Insert the ExtGState** back into the page resources.
5. **Save the modified PDF**.

प्रत्येक चरण को एक संक्षिप्त C# मेथड में लागू किया गया है, और पूर्ण स्रोत कोड लेख के अंत में दिखाया गया है।

## चरण 1: Aspose.Pdf के साथ PDF लोड करें (`load pdf aspose`)

किसी भी चीज़ को संपादित करने से पहले, आपको Aspose की `Document` क्लास का उपयोग करके फ़ाइल खोलनी होगी। `using` स्टेटमेंट यह सुनिश्चित करता है कि अपवाद होने पर भी फ़ाइल हैंडल रिलीज़ हो जाए।

```csharp
// Step 1: Load the PDF document
using (var pdfDocument = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf"))
{
    // All subsequent operations happen inside this block.
}
```

**यह क्यों महत्वपूर्ण है:**  
Aspose.Pdf PDF संरचना को एक ऑब्जेक्ट मॉडल में पार्स करता है। दस्तावेज़ को एक बार लोड करके मेमोरी में रखने से दोहराए गए I/O से बचा जा सकता है और यह सुनिश्चित होता है कि आपके द्वारा किए गए सभी परिवर्तन उसी इंस्टेंस पर लागू हों।

**सलाह:** यदि स्रोत PDF पासवर्ड‑सुरक्षित है, तो `Document` कन्स्ट्रक्टर में पासवर्ड पास करें:

```csharp
var pdfDocument = new Aspose.Pdf.Document("input.pdf", new LoadOptions { Password = "mySecret" });
```

## चरण 2: पेज रिसोर्सेज डिक्शनरी तक पहुँचें (`edit pdf resources`)

हर PDF पेज में एक *Resources* डिक्शनरी होती है जो फ़ॉन्ट्स, इमेजेज और ग्राफ़िक्स स्टेट्स को रखती है। नया ExtGState जोड़ने के लिए, इस डिक्शनरी को प्राप्त करें और मौजूदा `ExtGState` सब‑डिक्शनरी को लें (या यदि नहीं है तो एक नई बनाएं)।

```csharp
// Step 2: Access the first page's resources dictionary
var firstPage = pdfDocument.Pages[1];                     // Aspose uses 1‑based indexing
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

// Ensure the ExtGState entry exists; if not, create an empty dictionary.
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    resourcesEditor["ExtGState"] = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
}
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

**यह क्यों महत्वपूर्ण है:**  
`Resources` डिक्शनरी वह एकमात्र स्थान है जहाँ PDF रेंडरर ग्राफ़िक्स स्टेट डिफ़िनिशन देखता है। यदि `ExtGState` एंट्री मौजूद नहीं है, तो पेज बाद में आप द्वारा संदर्भित किसी भी अपारदर्शिता सेटिंग को नजरअंदाज कर देगा।

**विशेष मामला:** कुछ PDFs में पहले से ही कई एंट्रीज़ वाला `ExtGState` डिक्शनरी मौजूद होता है। ऐसे में आप ऊपर दिखाए अनुसार मौजूदा को पुनः उपयोग कर सकते हैं, ताकि अनावश्यक स्टेट्स को ओवरराइट न करना पड़े।

## चरण 3: ट्रांसपेरेंसी पैरामीटर निर्धारित करें

ट्रांसपेरेंसी को तीन कुंजियों द्वारा नियंत्रित किया जाता है:

| कुंजी | अर्थ | सामान्य सीमा |
|-----|---------|---------------|
| `CA` | Stroke opacity | 0 (transparent) … 1 (opaque) |
| `ca` | Fill opacity | 0 … 1 |
| `BM` | Blend mode | `"Normal"`, `"Multiply"`, etc. |

एक नया `CosPdfDictionary` बनाएं और इच्छित मानों से इसे भरें।

```csharp
// Step 3: Create a new ExtGState dictionary with desired entries
var customExtGState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var graphicsStateParameters = new[]
{
    // Stroke opacity = 1 (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA",
        new Aspose.Pdf.CosPdfNumber(1)),
    // Fill opacity = 0.5 (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca",
        new Aspose.Pdf.CosPdfNumber(0.5)),
    // Blend mode = Normal (standard source‑over composition)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM",
        new Aspose.Pdf.CosPdfName("Normal"))
};

foreach (var param in graphicsStateParameters)
    customExtGState.Add(param);
```

**यह क्यों महत्वपूर्ण है:**  
`ca` को `0.5` सेट करने से कोई भी भरी हुई आकृति (जैसे, आयत या टेक्स्ट) अर्ध‑पारदर्शी दिखेगी। आप इन संख्याओं को समायोजित करके वांछित दृश्य प्रभाव प्राप्त कर सकते हैं। ब्लेंड मोड यह निर्धारित करता है कि पारदर्शी कंटेंट नीचे की ग्राफ़िक्स के साथ कैसे मिलती है; `"Normal"` सबसे सामान्य विकल्प है।

**प्रो टिप:** यदि आपको अलग ब्लेंड मोड चाहिए, तो `"Normal"` को `"Multiply"` या `"Screen"` से बदलें ताकि नीचे की सामग्री को गहरा या हल्का करने जैसे कलात्मक प्रभाव प्राप्त हो सकें।

## चरण 4: कस्टम ExtGState को पेज रिसोर्सेज में डालें

अब डिक्शनरी को एक नाम (जैसे, `GS0`) से बाइंड करें और इसे पेज के `ExtGState` कलेक्शन में जोड़ें।

```csharp
// Step 4: Add the custom ExtGState entry to the page resources
extGStateDict.Add("GS0", customExtGState);
```

**यह क्यों महत्वपूर्ण है:**  
नाम (`GS0`) बाद में कंटेंट स्ट्रीम में ग्राफ़िक ऑपरेटर्स द्वारा संदर्भित किया जाता है। यदि आप इस स्टेट को कई पेजों पर उपयोग करने की योजना बनाते हैं, तो आप वही नाम पुनः उपयोग कर सकते हैं या पेज‑विशिष्ट नाम (`GS1`, `GS2`, …) बना सकते हैं।

**उन्नत विविधता:** मौजूदा कंटेंट स्ट्रीम पर स्टेट लागू करने के लिए, आप ड्राइंग कमांड्स से पहले PDF ऑपरेटर `q /GS0 gs` को प्रीपेंड कर सकते हैं। Aspose.Pdf इस उद्देश्य के लिए `PdfContentEditor` प्रदान करता है, लेकिन यह बुनियादी ट्यूटोरियल के दायरे से बाहर है।

## चरण 5: संशोधित PDF को सहेजें

अंत में, बदलावों को एक नई फ़ाइल में सहेजें। मूल फ़ाइल को अपरिवर्तित रखकर आप पहले/बाद के परिणामों की आसानी से तुलना कर सकते हैं।

```csharp
// Step 5: Save the modified PDF
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

**सत्यापन:** किसी भी PDF व्यूअर में `output.pdf` खोलें। कोई भी भरी हुई आकृति जो कस्टम ग्राफ़िक्स स्टेट का उपयोग करती है (जैसे, `GS0` से खींचा गया आयत) 50 % अपारदर्शिता पर दिखेगी। यदि परिवर्तन नहीं दिखता, तो दोबारा जांचें कि कंटेंट स्ट्रीम वास्तव में `GS0` को संदर्भित करता है। आप वैकल्पिक रूप से `PdfContentEditor` का उपयोग करके एक टेस्ट आयत भी डाल सकते हैं।

## पूर्ण कार्यशील उदाहरण

सभी चरणों को मिलाकर एक स्व-निहित प्रोग्राम बनता है जिसे आप कॉपी‑पेस्ट करके कंसोल एप्लिकेशन में उपयोग कर सकते हैं।

```csharp
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Load the PDF (load pdf aspose)
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources (edit pdf resources)
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            if (!resourcesEditor.ContainsKey("ExtGState"))
                resourcesEditor["ExtGState"] = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create custom ExtGState with transparency
            var customExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) customExtGState.Add(p);
            extGStateDict.Add("GS0", customExtGState);

            // OPTIONAL: Apply the graphics state to a sample rectangle
            // This demonstrates that the transparency works.
            var canvas = new Aspose.Pdf.PageEditor(firstPage);
            canvas.AddRectangle(100, 500, 200, 600); // left, bottom, right, top
            // Set the graphics state before drawing
            canvas.ContentStream.Operators.Insert(0, new SetGraphicsState("GS0"));
            canvas.Save();

            // Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        System.Console.WriteLine("Transparency applied successfully.");
    }
}
```

**वैकल्पिक ब्लॉक की व्याख्या:**  
`PageEditor` पेज में एक साधारण आयत जोड़ता है और ग्राफ़िक्स स्टेट को स्पष्ट रूप से `GS0` सेट करता है। यह चरण परीक्षण के लिए उपयोगी है; वास्तविक परिदृश्य में आपके पास पहले से ही ऐसी सामग्री होगी जो इस स्टेट को संदर्भित करती हो।

## सामान्य

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन तरीकों का अन्वेषण करने में मदद करती हैं।

- [Aspose.PDF के साथ ग्राफ़िक्स स्टेट PDF जोड़ना और ट्रांसपेरेंसी नियंत्रित करना कैसे करें](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [C# में Aspose.PDF का उपयोग करके PDF में ट्रांसपेरेंसी कैसे जोड़ें](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [C# में Aspose.Pdf का उपयोग करके PDF ट्रांसपेरेंसी कैसे बदलें](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}