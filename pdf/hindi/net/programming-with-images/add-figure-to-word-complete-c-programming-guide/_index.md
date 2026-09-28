---
category: general
date: 2026-04-12
description: C# के साथ Word में जल्दी से चित्र जोड़ें। जानें कि Word में चित्र को
  कैसे स्थित करें, docx में चित्र कैसे डालें, और उन्नत लेआउट के लिए कस्टम XML कैसे
  जोड़ें।
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: hi
og_description: C# के साथ Word में जल्दी से फ़िगर जोड़ें। जानें कि Word में फ़िगर
  को कैसे पोज़िशन करें, docx में फ़िगर डालें, और उन्नत लेआउट के लिए कस्टम XML जोड़ें।
og_title: वर्ड में चित्र जोड़ें – पूर्ण C# प्रोग्रामिंग गाइड
tags:
- C#
- Word Automation
- Document Generation
title: वर्ड में चित्र जोड़ें – पूर्ण C# प्रोग्रामिंग गाइड
url: /hi/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Figure to Word – Complete C# Programming Guide

क्या आपको कभी **add figure to Word** करने की ज़रूरत पड़ी, लेकिन शुरुआत कैसे करें, समझ नहीं आया? आप अकेले नहीं हैं। कई ऑफिस‑ऑटोमेशन प्रोजेक्ट्स में वह गायब टुकड़ा एक अच्छी तरह से रखी गई तस्वीर या डायग्राम होता है जो एक कस्टम XML पार्ट के अंदर रहता है। यह गाइड आपको दिखाता है कि **position figure in Word** कैसे किया जाता है, फ़िगर को *.docx* फ़ाइल में कैसे डाला जाता है, और यहाँ तक कि अंतर्निहित कस्टम XML को कैसे ट्यून किया जाए ताकि शैप किसी भी नेटिव Word ऑब्जेक्ट की तरह व्यवहार करे।

हम GemBox.Document लाइब्रेरी (छोटी फ़ाइलों के लिए मुफ्त, बड़े वर्कलोड के लिए कमर्शियल) का उपयोग करके एक वास्तविक उदाहरण से गुजरेंगे। अंत तक आपके पास एक स्व-निहित, चलाने योग्य प्रोग्राम होगा जो टैग‑कंटेंट कंटेनर के अंदर X = 50, Y = 200 निर्देशांक पर फ़िगर डालता है। कोई अस्पष्ट “see the docs” शॉर्टकट नहीं—सिर्फ स्पष्ट कोड, क्यों काम करता है, और टिप्स जो आप सीधे अपने प्रोजेक्ट में कॉपी कर सकते हैं।

## Prerequisites

- .NET 6.0 या बाद का (कोड .NET Core 3.1 के साथ भी कम्पाइल होता है)
- **GemBox.Document** NuGet पैकेज (`Install-Package GemBox.Document`)
- एक स्टार्टर Word फ़ाइल (`input.docx`) जिसमें पहले से ही वह कस्टम XML टैग हो जहाँ आप फ़िगर दिखाना चाहते हैं
- बेसिक C# ज्ञान (आप देखेंगे कि प्रत्येक लाइन क्यों महत्वपूर्ण है)

> **Pro tip:** यदि आपके पास प्री‑टैग्ड डॉक्यूमेंट नहीं है, तो आप Word में *Content Control* → *XML Mapping Pane* → कस्टम XML पार्ट मैप करके एक बना सकते हैं। लाइब्रेरी उस कंट्रोल को `TaggedContent` के रूप में ट्रीट करेगी।

## Step 1 – Load the Source Document

सबसे पहले हम मौजूदा *.docx* फ़ाइल को खोलते हैं। `Document` सभी GemBox ऑपरेशन्स का एंट्री पॉइंट है।

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Why?* फ़ाइल को लोड करने से हमें उसके आंतरिक पार्ट्स, जिसमें कस्टम XML कंटेनर भी शामिल हैं, तक पहुंच मिलती है। इसके बिना हम `TaggedContent` नोड को नहीं ढूंढ पाएंगे जो हमारी फ़िगर को रखेगा।

## Step 2 – Access the Tagged Content (Custom XML Container)

कस्टम XML Word में एक *content control* के अंदर स्टोर किया जाता है। GemBox इसे `TaggedContent` के रूप में एक्सपोज़ करता है।

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

यदि डॉक्यूमेंट में कई टैग्ड सेक्शन हैं, तो `TaggedContent` **पहला** वाला रिटर्न करता है। आप `doc.TaggedContents` को एने्यूमरेट करके नाम से किसी विशिष्ट टैग को भी चुन सकते हैं।

## Step 3 – Create the Figure Element

एक `FigureElement` एक तस्वीर, चार्ट, या कोई भी विज़ुअल ऑब्जेक्ट दर्शाता है जिसे Word *shape* के रूप में ट्रीट करता है। हम इसे टैग्ड कंटेनर के अंदर बनाएँगे।

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Why create a figure here?* कस्टम XML नोड से जुड़ाकर, Word जानता है कि फ़िगर उस लॉजिकल सेक्शन से संबंधित है, जो बाद में एडिटिंग या कंटेंट‑कंट्रोल‑आधारित वर्कफ़्लोज़ के लिए महत्वपूर्ण है।

## Step 4 – Position the Figure Precisely

Word पोजिशनिंग के लिए पॉइंट्स (1 pt ≈ 1/72 in) का उपयोग करता है। `PointF` स्ट्रक्ट हमें X/Y कोऑर्डिनेट्स आसानी से सेट करने देता है।

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** `Position` प्रॉपर्टी एक `PointF` लेती है जहाँ पहला वैल्यू हॉरिज़ॉन्टल ऑफ़सेट (बाएँ) और दूसरा वैल्यू वर्टिकल ऑफ़सेट (ऊपर) पेज मार्जिन के सापेक्ष होता है। इन नंबरों को समायोजित करके प्लेसमेंट को फाइन‑ट्यून करें।

## Step 5 – Insert the Figure into the Tagged Content Tree

अब हम फ़िगर को कस्टम XML ट्री के रूट एलिमेंट से जोड़ते हैं। इससे शैप वास्तविक रूप से Word डॉक्यूमेंट में जुड़ जाता है।

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

इस चरण पर फ़िगर डॉक्यूमेंट में मौजूद है, लेकिन अभी तक उसका इमेज सोर्स नहीं है। चलिए डिस्क से एक साधारण PNG जोड़ते हैं।

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Step 6 – Save the Modified Document

अंत में, हम बदलावों को एक नई *.docx* फ़ाइल में लिखते हैं।

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

जब आप `output.docx` को Word में खोलेंगे, तो आपको चित्र (50, 200) निर्देशांक पर ठीक उसी कस्टम‑XML ब्लॉक के अंदर दिखेगा जिसे आपने टार्गेट किया था।

### Full Working Example

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Expected result:** `output.docx` खोलने पर PNG बिल्कुल वही जगह पर रहेगा जहाँ आपने निर्दिष्ट किया था, और यह कस्टम XML पार्ट के अंदर नेस्टेड होगा। यदि आप डॉक्यूमेंट का XML (`.docx` → unzip → `word/document.xml`) देखेंगे, तो आपको `<w:pict>` एलिमेंट के साथ सही `<v:shape>` कोऑर्डिनेट्स मिलेंगे।

## Common Questions & Edge Cases

### What if the document has multiple tagged sections?

`doc.TaggedContents` का उपयोग करके एने्यूमरेट करें और टैग नाम से चुनें:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### How to add a caption to the figure?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Does this work with Word 2010 and later?

हाँ। GemBox.Document Open XML स्टैंडर्ड को टार्गेट करता है, जो Word 2007 + (2010, 2013, 2016, 2019, और Microsoft 365 सहित) के साथ कम्पैटिबल है।

### What if I need to rotate the shape?

```csharp
figure.Rotation = 45; // degrees
```

### How to add a vector graphic instead of a raster image?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro Tips & Pitfalls

- **File paths:** `Path.Combine` का उपयोग करके हार्ड‑कोडेड सेपरेटर से बचें, विशेषकर नॉन‑Windows प्लेटफ़ॉर्म पर।
- **License limits:** फ्री GemBox लाइसेंस डॉक्यूमेंट साइज को 20 KB तक सीमित करता है। बड़े फ़ाइलों के लिए कमर्शियल की खरीदें।
- **Performance:** बैच प्रोसेसिंग के लिए एक ही `Document` इंस्टेंस को री‑यूज़ करने से मेमोरी ओवरहेड काफी घटता है।
- **Shape overflow:** यदि फ़िगर के डायमेंशन पेज मार्जिन से बाहर हैं, तो Word उसे क्लिप कर देगा। `figure.Width` और `figure.Height` को तदनुसार एडजस्ट करें।

## Conclusion

अब आप **how to add figure to Word**, ठीक‑ठाक **position figure in Word**, और अंतर्निहित कस्टम XML को इस तरह मैनीपुलेट करना जानते हैं कि शैप किसी भी नेटिव एलिमेंट की तरह व्यवहार करे। पूरा, runnable उदाहरण हर चरण को दर्शाता है—डॉक्यूमेंट लोड करना, `FigureElement` बनाना, कोऑर्डिनेट्स सेट करना, इमेज अटैच करना, और अंत में अपडेटेड *.docx* को सेव करना।

अब **insert figure into docx** को कई फ़िगर्स जोड़कर, लूप्स का उपयोग करके, या ऑन‑द‑फ्लाई चार्ट जेनरेट करके एक्सप्लोर करें। आप **how to add custom xml** के साथ richer कंटेंट कंट्रोल्स भी बना सकते हैं या **how to position shape word** को टेबल्स और हेडर्स में आज़मा सकते हैं। संभावनाएँ अनंत हैं, और यहाँ कवर किए गए फंडामेंटल्स के साथ आप Word डॉक्यूमेंट्स को प्रो की तरह ऑटोमेट करने के लिए तैयार हैं।

Happy coding, and feel free to drop a comment if you hit any snags!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}