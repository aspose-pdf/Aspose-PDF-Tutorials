---
category: general
date: 2026-08-20
description: Aspose.Pdf के साथ PDF में कस्टम ग्राफ़िक्स स्टेट बनाएं। सीखें कि PDF
  संसाधनों को कैसे संपादित करें और कुछ ही चरणों में PDF में ट्रांसपेरेंसी कैसे जोड़ें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: hi
lastmod: 2026-08-20
og_description: Aspose.Pdf के साथ PDF में कस्टम ग्राफ़िक्स स्टेट बनाएं। यह ट्यूटोरियल
  दिखाता है कि कैसे PDF संसाधनों को संपादित करें और जल्दी से ट्रांसपैरेंसी PDF जोड़ें।
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: PDF में कस्टम ग्राफ़िक्स स्टेट बनाएं – Aspose.Pdf गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Aspose.Pdf का उपयोग करके PDF में कस्टम ग्राफ़िक्स स्टेट बनाएं
url: /hi/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf का उपयोग करके PDF में कस्टम ग्राफ़िक्स स्टेट बनाएं

यदि आपको PDF में **कस्टम ग्राफ़िक्स स्टेट** बनाना है, तो यह गाइड आपको Aspose.Pdf for .NET के साथ इसे कैसे करना है, बिल्कुल दिखाता है। ट्यूटोरियल के अंत तक आप **PDF संसाधनों को संपादित** कर सकेंगे, एक नया ग्राफ़िक्स‑स्टेट डिक्शनरी इंजेक्ट कर सकेंगे, और **ट्रांसपेरेंसी PDF** कंटेंट जोड़ सकेंगे बिना अपने C# प्रोजेक्ट से बाहर निकले।

आप एक पूर्ण, चलाने योग्य उदाहरण, प्रत्येक पंक्ति के महत्व की व्याख्या, और मल्टी‑पेज दस्तावेज़ या विभिन्न ब्लेंड मोड को संभालने के टिप्स देखेंगे। कोई बाहरी टूल आवश्यक नहीं—सिर्फ Aspose.Pdf लाइब्रेरी और एक बेसिक .NET डेवलपमेंट एनवायरनमेंट।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)
* **Aspose.Pdf for .NET** की लाइसेंस प्राप्त कॉपी (टेस्टिंग के लिए फ्री ट्रायल काम करता है)
* `input.pdf` नाम की एक इनपुट PDF फ़ाइल, जिसे आप कोड से रेफ़रेंस कर सकें ऐसे फ़ोल्डर में रखें
* Visual Studio 2022 या कोई भी IDE जो C# डेवलपमेंट को सपोर्ट करता हो

ट्यूटोरियल मानता है कि आप बुनियादी C# सिंटैक्स और PDF पेजों की अवधारणा से परिचित हैं।

## चरण 1: स्रोत PDF लोड करें और पहला पृष्ठ एक्सेस करें

पहला ऑपरेशन PDF फ़ाइल को खोलना और उस पेज को प्राप्त करना है जिसके संसाधनों को आप संशोधित करना चाहते हैं। Aspose.Pdf प्रत्येक पेज को एक `Page` ऑब्जेक्ट के रूप में दर्शाता है, और हर पेज में एक **resource dictionary** होती है जो ग्राफ़िक्स स्टेट्स, फ़ॉन्ट्स, XObjects, आदि संग्रहीत करती है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*यह क्यों महत्वपूर्ण है:* `Document` क्लास फ़ाइल को मेमोरी में लोड करती है, और `Pages[1]` आपको सीधे पहले पेज की रिसोर्स डिक्शनरी तक पहुँच देती है, जहाँ ग्राफ़िक्स स्टेट स्थित होता है।

## चरण 2: रिसोर्स डिक्शनरी को एडिटिंग के लिए खोलें

Aspose.Pdf एक `DictionaryEditor` हेल्पर प्रदान करता है जो आपको रिसोर्स डिक्शनरी को सामान्य .NET `Dictionary` की तरह ट्रीट करने देता है। यह `ExtGState` जैसे एंट्रीज़ को पढ़ने, जोड़ने या बदलने को सीधा बनाता है।

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*यह क्यों महत्वपूर्ण है:* `DictionaryEditor` लो‑लेवल COS ऑब्जेक्ट्स को एब्स्ट्रैक्ट करता है, जिससे आप परिचित की/वैल्यू पेयर्स के साथ काम कर सकते हैं जबकि PDF अनुपालन बना रहता है।

## चरण 3: ExtGState डिक्शनरी को प्राप्त (या बनाएं)

**ExtGState** एंट्री पेज के सभी एक्सटर्नल ग्राफ़िक्स‑स्टेट ऑब्जेक्ट्स को रखती है। यदि डिक्शनरी मौजूद नहीं है, तो Aspose.Pdf आपके लिए एक खाली डिक्शनरी बना देगा।

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*यह क्यों महत्वपूर्ण है:* यदि `ExtGState` एंट्री गायब होगी तो बाद में `KeyNotFoundException` आएगा। यह गार्ड कोड को उन PDFs पर काम करने देता है जिन्होंने पहले कभी कस्टम ग्राफ़िक्स स्टेट परिभाषित नहीं किया था—जो **PDF संसाधनों को संपादित** करने की मजबूती का एक आवश्यक हिस्सा है।

## चरण 4: कस्टम ग्राफ़िक्स स्टेट डिक्शनरी बनाएं

एक ग्राफ़िक्स स्टेट यह वर्णन करता है कि ड्रॉइंग ऑपरेशन्स कैसे रेंडर होते हैं। **ट्रांसपेरेंसी PDF** जोड़ने के लिए आपको `ca` (फिल अपारदर्शिता) और `CA` (स्ट्रोक अपारदर्शिता) एंट्रीज़ सेट करनी होंगी, और वैकल्पिक रूप से एक ब्लेंड मोड (`BM`) भी। नीचे दिया गया कोड इन पैरामीटर्स के साथ एक नई डिक्शनरी बनाता है।

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*यह क्यों महत्वपूर्ण है:* `ca` और `CA` एंट्रीज़ क्रमशः फिल और स्ट्रोक ऑपरेशन्स की ट्रांसपेरेंसी को नियंत्रित करती हैं। `BM` सेट करने से आप विभिन्न कॉम्पोज़िटिंग इफ़ेक्ट्स के साथ प्रयोग कर सकते हैं, जो बाद में **ट्रांसपेरेंसी PDF** कंटेंट जैसे अर्ध‑पारदर्शी शैप्स या इमेजेज जोड़ते समय उपयोगी होता है।

## चरण 5: नई ग्राफ़िक्स स्टेट को एक यूनिक नाम के तहत रजिस्टर करें

`ExtGState` डिक्शनरी में हर ग्राफ़िक्स स्टेट का एक यूनिक नाम होना चाहिए (जैसे `GS0`, `GS1`)। आप कोई भी ऐसा नाम चुन सकते हैं जो मौजूदा एंट्रीज़ से टकराए नहीं।

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*यह क्यों महत्वपूर्ण है:* नई डिक्शनरी को `GS0` के तहत डालकर आप स्टेट को पेज कंटेंट स्ट्रीम से एड्रेसेबल बनाते हैं। कंडीशनल ब्लॉक यह सुनिश्चित करता है कि `ExtGState` एंट्री मौजूद हो, भले ही PDF शुरू में बिना इस एंट्री के बना हो—एक और **PDF संसाधनों को संपादित** करने का सुरक्षा उपाय।

## चरण 6: पेज कंटेंट में कस्टम ग्राफ़िक्स स्टेट का उपयोग करें (वैकल्पिक)

पिछले चरण केवल ग्राफ़िक्स स्टेट को *परिभाषित* करते हैं। वास्तविक प्रभाव देखने के लिए आपको इसे पेज की कंटेंट स्ट्रीम में रेफ़रेंस करना होगा। नीचे एक त्वरित उदाहरण है जो हमने अभी बनाया हुआ स्टेट उपयोग करके अर्ध‑पारदर्शी आयत बनाता है।

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*यह क्यों महत्वपूर्ण है:* `SetExtGState` ऑपरेटर (`gs`) PDF रेंडरर को बताता है कि `GS0` में परिभाषित पैरामीटर्स लागू करें। आयत 50 % फिल अपारदर्शिता के साथ दिखाई देगा जबकि उसका स्ट्रोक पूरी तरह अपारदर्शी रहेगा।

## चरण 7: संशोधित PDF को सेव करें

अंत में, बदलावों को डिस्क पर लिखें। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई फ़ाइल बना सकते हैं।

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

जब आप `output_with_custom_gs.pdf` को PDF व्यूअर में खोलेंगे, तो आपको पहले पेज पर एक अर्ध‑पारदर्शी आयत दिखनी चाहिए। यह पुष्टि करता है कि आपने सफलतापूर्वक **कस्टम ग्राफ़िक्स स्टेट बनाया**, **PDF संसाधनों को संपादित किया**, और **ट्रांसपेरेंसी PDF** कंटेंट जोड़ा।

## सामान्य विविधताएँ और किनारी मामलों

| स्थिति | क्या समायोजित करें |
|-----------|----------------|
| **एकाधिक पृष्ठों को समान स्टेट चाहिए** | ग्राफ़िक्स स्टेट को एक बार (चरण 1‑5) रजिस्टर करें और किसी भी पृष्ठ की कंटेंट स्ट्रीम में `GS0` को रेफ़रेंस करें। |
| **प्रत्येक तत्व के लिए अलग अपारदर्शिता** | विभिन्न `ca`/`CA` मानों के साथ अतिरिक्त स्टेट्स (`GS1`, `GS2`, …) परिभाषित करें और `SetExtGState` का उपयोग करके उनके बीच स्विच करें। |
| **Normal के अलावा अन्य ब्लेंड मोड** | `BM` एंट्री में `"Normal"` को `"Multiply"`, `"Screen"` या किसी भी PDF‑स्टैंडर्ड ब्लेंड मोड से बदलें। |
| **नाम टकराव** | जोड़ने से पहले, `extGStateDict.ContainsKey(yourName)` जांचें और आवश्यकता होने पर एक अद्वितीय सफ़िक्स चुनें। |
| **PDF में पहले से ही ExtGState डिक्शनरी मौजूद है** | चरण 3 का कोड पहले से मौजूद डिक्शनरी को पुनः उपयोग करता है, इसलिए अतिरिक्त हैंडलिंग की आवश्यकता नहीं है। |

**Pro tip:** बड़े PDFs के साथ काम करते समय, `Document` उपयोग को `using` ब्लॉक में रैप करें (जैसा कि दिखाया गया है) ताकि नेटिव रिसोर्सेज तुरंत रिलीज़ हों। साथ ही, यदि आप संसाधनों को संपादित करने के बाद PDF/A या PDF/X कंफ़ॉर्मेंस की गारंटी देना चाहते हैं, तो Aspose.Pdf की `PdfCompliance` प्रॉपर्टी को सक्षम करने पर विचार करें।

## पूर्ण कार्यशील उदाहरण

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## आगे क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स निकटतम संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण करने में मदद करेंगे।

- [Aspose के साथ PDF बनाना – फ़ॉर्म फ़ील्ड और पेज जोड़ें](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Aspose.PDF .NET का उपयोग करके PDFs में कस्टम टेबल बनाना](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Aspose Pdf Net में कस्टम PDF स्टैम्प बनाएं](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}