---
category: general
date: 2026-10-04
description: Aspose.Pdf का उपयोग करके C# में PDF की पारदर्शिता कैसे बदलें, सीखें।
  यह चरण‑दर‑चरण गाइड opacity और blend mode को समायोजित करने के लिए एक कस्टम ग्राफ़िक्स
  स्टेट जोड़ता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: hi
lastmod: 2026-10-04
og_description: Aspose.Pdf का उपयोग करके C# में PDF की पारदर्शिता बदलें। अपने PDFs
  में अपारदर्शिता, ब्लेंड मोड और ग्राफ़िक्स स्टेट को संशोधित करने के लिए इस संक्षिप्त
  ट्यूटोरियल का पालन करें।
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: Aspose.Pdf के साथ PDF की पारदर्शिता बदलें – पूर्ण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: Aspose.Pdf का उपयोग करके C# में PDF की पारदर्शिता कैसे बदलें
url: /hi/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf का उपयोग करके C# में PDF ट्रांसपेरेंसी कैसे बदलें

यदि आपको .NET प्रोजेक्ट में **PDF ट्रांसपेरेंसी बदलनी** है, तो यह गाइड Aspose.Pdf के साथ इसे करने का सटीक तरीका दिखाता है। ट्यूटोरियल के अंत तक आपके पास एक PDF होगा जहाँ चयनित ऑब्जेक्ट्स कस्टम अपासिटी और ब्लेंड मोड का उपयोग करेंगे, बिना किसी बाहरी टूल की आवश्यकता के।

PDF अपासिटी के साथ काम करना वॉटरमार्क, ओवरले ग्राफ़िक्स, या सूक्ष्म दृश्य प्रभावों के लिए आम आवश्यकता है। नीचे दिए गए चरण सभी आवश्यक चीज़ों को कवर करते हैं—डॉक्यूमेंट लोड करने से लेकर **ExtGState डिक्शनरी** को एडिट करने, नया ग्राफ़िक्स स्टेट बनाने, और परिणाम सहेजने तक।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* **Aspose.Pdf for .NET** (संस्करण 23.12 या बाद का)। आप इसे NuGet के माध्यम से इंस्टॉल कर सकते हैं:

```bash
dotnet add package Aspose.Pdf
```

* एक .NET विकास वातावरण (Visual Studio, VS Code, या `dotnet` CLI)।
* एक इनपुट PDF फ़ाइल जो ज्ञात डायरेक्टरी में स्थित हो (उदाहरण में `input.pdf` उपयोग किया गया है)।

कोई अतिरिक्त लाइब्रेरी आवश्यक नहीं है।

## चरण 1: PDF डॉक्यूमेंट लोड करें

पहला ऑपरेशन मौजूदा PDF को खोलना है। `using` ब्लॉक का उपयोग करने से फ़ाइल हैंडल स्वचालित रूप से रिलीज़ हो जाता है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*क्यों महत्वपूर्ण है*: डॉक्यूमेंट लोड करने से मेमोरी में एक प्रतिनिधित्व बनता है जिसे आप संशोधित कर सकते हैं। `Document` क्लास आपको लो‑लेवल COS ऑब्जेक्ट्स तक पहुँच भी देती है, जो PDF ट्रांसपेरेंसी बदलने के लिए आवश्यक है।

## चरण 2: पहले पेज के रिसोर्सेज़ तक पहुँचें

ग्राफ़िक्स स्टेट्स पेज की रिसोर्स डिक्शनरी में संग्रहीत होते हैं। हम पहले पेज को प्राप्त करते हैं और उसके रिसोर्सेज़ को `DictionaryEditor` के साथ रैप करते हैं ताकि हम उन्हें आसानी से एडिट कर सकें।

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*व्याख्या*: `DictionaryEditor` COS डिक्शनरी हैंडलिंग को एब्स्ट्रैक्ट करता है, जिससे आप `ExtGState` जैसी एंट्रीज़ को पढ़ और लिख सकते हैं बिना रॉ PDF सिंटैक्स से निपटे।

## चरण 3: ExtGState डिक्शनरी प्राप्त (या बनाएं)

**ExtGState डिक्शनरी** नामित ग्राफ़िक्स स्टेट ऑब्जेक्ट्स को रखती है। यदि यह पहले से मौजूद है तो हम इसे पुनः उपयोग करते हैं; अन्यथा हम एक नई बनाते हैं।

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*इस चरण का कारण*: बिना `ExtGState` एंट्री के PDF इंजन को कस्टम अपासिटी सेटिंग्स के लिए कहीं नहीं मिलेगा। डिक्शनरी जोड़ने से पेज को आपके द्वारा परिभाषित नए ग्राफ़िक्स स्टेट्स का पता चलता है।

## चरण 4: अपासिटी और ब्लेंड मोड के साथ नया ग्राफ़िक्स स्टेट परिभाषित करें

एक ग्राफ़िक्स स्टेट PDF रेंडरिंग पैरामीटर्स का संग्रह है। यहाँ हम सेट करते हैं:

* **CA** – स्ट्रोक अपासिटी (1 = पूरी तरह अपारदर्शी)
* **ca** – फ़िल अपासिटी (0.5 = 50 % ट्रांसपेरेंट)
* **BM** – ब्लेंड मोड (`Normal` डिफ़ॉल्ट है, लेकिन आप `Multiply`, `Screen` आदि के साथ प्रयोग कर सकते हैं)

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*इनसाइट*: `CosPdfNumber` मान 0 और 1 के बीच के फ्लोटिंग‑पॉइंट नंबर होते हैं। इन्हें बदलने से आप स्ट्रोक और फ़िल की ट्रांसपेरेंसी को सूक्ष्म रूप से ट्यून कर सकते हैं। ब्लेंड मोड निर्धारित करता है कि ट्रांसपेरेंट कंटेंट नीचे के ग्राफ़िक्स के साथ कैसे इंटरैक्ट करता है।

## चरण 5: ExtGState में ग्राफ़िक्स स्टेट रजिस्टर करें

हम नए स्टेट को एक नाम (`GS0`) देते हैं। बाद में, जब आप ऑब्जेक्ट्स ड्रॉ करेंगे, तो आप इस नाम को कंटेंट स्ट्रीम में रेफ़र करेंगे।

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*बेस्ट प्रैक्टिस*: स्पष्ट नामकरण कन्वेंशन (`GS0`, `GS_Watermark` आदि) का उपयोग करें ताकि आप कई स्टेट्स को बिना भ्रम के मैनेज कर सकें।

## चरण 6: (वैकल्पिक) पेज कंटेंट पर ग्राफ़िक्स स्टेट लागू करें

यदि आप नए अपासिटी को मौजूदा पेज एलिमेंट्स पर लागू करना चाहते हैं, तो आपको पेज की कंटेंट स्ट्रीम को संशोधित करना होगा। नीचे एक सरल उदाहरण है जो पेज के ऊपर एक अर्ध‑ट्रांसपेरेंट रेक्टैंगल जोड़ता है।

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*क्यों काम करता है*: `SetGraphicsState` ऑपरेटर PDF इंटरप्रेटर को बताता है कि सभी बाद के ड्रॉइंग कमांड्स के लिए `GS0` में परिभाषित पैरामीटर्स का उपयोग करना है। इसलिए रेक्टैंगल 50 % फ़िल अपासिटी के साथ दिखेगा जबकि उसका स्ट्रोक पूरी तरह अपारदर्शी रहेगा।

## चरण 7: संशोधित PDF को सहेजें

अंत में, बदलावों को डिस्क पर लिखें।

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

परिणामी `output.pdf` में नया ग्राफ़िक्स स्टेट होगा, और कोई भी कंटेंट जो `GS0` को रेफ़र करता है, वह परिभाषित ट्रांसपेरेंसी के साथ रेंडर होगा।

---

![Diagram showing PDF transparency change](/images/pdf-transparency-before-after.png "PDF page before and after applying custom graphics state")
*Image alt text (for SEO and accessibility):* **PDF ट्रांसपेरेंसी बदलने का उदाहरण – मूल बनाम संशोधित पेज**

## पूर्ण कार्यशील उदाहरण

सब कुछ मिलाकर, यहाँ एक एकल, रन करने योग्य प्रोग्राम है जो PDF ट्रांसपेरेंसी बदलता है और एक अर्ध‑ट्रांसपेरेंट रेक्टैंगल जोड़ता है।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### अपेक्षित आउटपुट

* फ़ाइल `output.pdf` निर्दिष्ट फ़ोल्डर में बनाई जाती है।
* यदि आप PDF खोलते हैं, तो आपको एक लाल रेक्टैंगल दिखेगा जिसकी फ़िल 50 % ट्रांसपेरेंट है जबकि बॉर्डर पूरी तरह अपारदर्शी रहता है।
* कोई भी अन्य ऑब्जेक्ट जो `GS0` को रेफ़र करता है (जैसे वॉटरमार्क) वही अपासिटी और ब्लेंड मोड अपनाएगा।

## सामान्य प्रश्न एवं एज‑केस हैंडलिंग

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मैं केवल स्ट्रोक अपासिटी बदल सकता हूँ?** | `CA` को इच्छित मान पर सेट करें और `ca` को `1` पर रखें। |
| **कौन से ब्लेंड मोड सपोर्टेड हैं?** | सभी मानक PDF ब्लेंड मोड (`Normal`, `Multiply`, `Screen`, `Overlay`, आदि) `BM` एंट्री के माध्यम से स्वीकार किए जाते हैं। |
| **क्या मुझे उपयोग के बाद डिक्शनरी को क्लीन अप करना पड़ता है?** | नहीं। `CosPdfDictionary` ऑब्जेक्ट्स Aspose.Pdf द्वारा मैनेज होते हैं और `Save` कॉल करने पर फ़ाइल में लिखे जाते हैं। |
| **एन्क्रिप्टेड PDFs के साथ यह कैसे काम करता है?** | डॉक्यूमेंट को सही पासवर्ड के साथ लोड करें (`new Document(path, password)`)। एक बार मेमोरी में डिक्रिप्ट हो जाने पर ग्राफ़िक्स‑स्टेट मैनिपुलेशन समान रूप से काम करता है। |
| **क्या एक ही ग्राफ़िक्स स्टेट को कई पेजों पर लागू किया जा सकता है?** | हाँ। `GS0` एंट्री को प्रत्येक पेज की `ExtGState` डिक्शनरी में जोड़ें, या डॉक्यूमेंट की ग्लोबल रिसोर्सेज़ में एक साझा डिक्शनरी बनाकर प्रत्येक पेज से रेफ़र करें। |

## टिप्स और बेस्ट प्रैक्टिसेज

* **प्रो टिप:** ग्राफ़िक्स‑स्टेट नाम छोटे लेकिन वर्णनात्मक रखें (`GS_Watermark`, `GS_Overlay`)। इससे नाम टकराव नहीं होते और डिबगिंग आसान होती है।
* **ध्यान रखें:** मौजूदा `ExtGState` एंट्री को अनजाने में ओवरराइट न करें। नया डिक्शनरी बनाने से पहले हमेशा `resourcesEditor.ContainsKey("ExtGState")` चेक करें।
* **परफ़ॉर्मेंस नोट:** लो‑लेवल COS ऑब्जेक्ट्स को मॉडिफ़ाई करना तेज़ है, लेकिन यदि आपको हजारों पेज प्रोसेस करने हैं तो मेमोरी प्रेशर कम करने के लिए बदलावों को बैच में करने पर विचार करें।

## अगले कदम

अब जब आप **PDF ट्रांसपेरेंसी बदलना** जानते हैं, तो आप संबंधित विषयों का अन्वेषण कर सकते हैं, जैसे:

* कस्टम अपासिटी के साथ **वॉटरमार्क** जोड़ना (`PDF opacity C#`)।
* कलात्मक प्रभावों के लिए **विभिन्न ब्लेंड मोड** का उपयोग (`blend mode PDF`)।
* बड़े‑पैमाने पर डॉक्यूमेंट जनरेशन के लिए पुन: उपयोग योग्य **ग्राफ़िक्स स्टेट लाइब्रेरी** बनाना (`Aspose.Pdf graphics state`)।

`ca` और `CA` मानों को बदलकर प्रयोग करें, या लाल रेक्टैंगल को इमेज या टेक्स्ट ओवरले से बदलें। वही सिद्धांत लागू होते हैं—नए कंटेंट को ड्रॉ करने से पहले `GS0` ग्राफ़िक्स स्टेट को रेफ़र करें।

---

*आपने Aspose.Pdf का उपयोग करके C# में PDF ट्रांसपेरेंसी बदलना सीख लिया है। इन तकनीकों को रिपोर्ट, इनवॉइस, या किसी भी PDF‑आधारित आउटपुट में दृश्य सूक्ष्मता जोड़ने के लिए लागू करें।*


## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकते हैं।

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change PDF Opacity in C# – Complete Aspose Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}