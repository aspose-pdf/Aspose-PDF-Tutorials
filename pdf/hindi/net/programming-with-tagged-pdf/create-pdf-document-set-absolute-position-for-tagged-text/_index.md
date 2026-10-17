---
category: general
date: 2026-03-24
description: PDF दस्तावेज़ बनाएं और टैग किए गए टेक्स्ट के लिए एब्सोल्यूट पोजीशन सेट
  करना सीखें। यह ट्यूटोरियल दिखाता है कि स्पैन एलिमेंट कैसे जोड़ें, टैग किया गया कंटेंट
  कैसे जोड़ें और पेज पर टेक्स्ट को कैसे पोजिशन करें।
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: hi
og_description: PDF दस्तावेज़ बनाएं और तुरंत देखें कि कैसे निरपेक्ष स्थिति सेट करें,
  स्पैन तत्व जोड़ें, और टैग किए गए PDF सामग्री के साथ पृष्ठ पर पाठ को स्थित करें।
og_title: PDF दस्तावेज़ बनाएं – टैग किए गए पाठ की पूर्ण स्थिति निर्धारण
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: PDF दस्तावेज़ बनाएं – टैग किए गए पाठ के लिए निरपेक्ष स्थिति निर्धारित करें
url: /hi/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF दस्तावेज़ बनाएं – टैग्ड टेक्स्ट के लिए एब्सोल्यूट पोजीशन सेट करें

क्या आपको कभी **create pdf document** की आवश्यकता पड़ी है जिसमें सुलभ, टैग्ड टेक्स्ट बिल्कुल वहीँ स्थित हो जहाँ आप चाहते हैं? शायद आप एक फ़ॉर्म‑जैसे PDF बना रहे हैं जहाँ लेबल को एक सटीक निर्देशांक पर बैठना चाहिए, या आप एक प्रमाणपत्र बना रहे हैं और नाम को बैकग्राउंड इमेज के साथ पूरी तरह संरेखित होना चाहिए।  

इस गाइड में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे जो दिखाता है **how to add tagged** कंटेंट, **set absolute position**, और **add span element** ताकि आप **position text on page** बिना अनुमान लगाए कर सकें। कोई बाहरी संदर्भ नहीं—सिर्फ वह कोड जिसे आप कॉपी‑पेस्ट कर सकते हैं, साथ ही प्रत्येक पंक्ति के “क्यों” की व्याख्याएँ।

## आवश्यकताएँ

- .NET 6+ (या .NET Framework 4.6+) के साथ C# कंपाइलर  
- NuGet के माध्यम से स्थापित Aspose.Pdf for .NET (लेखन के समय का नवीनतम संस्करण, 23.12)  
- C# सिंटैक्स की बुनियादी परिचितता  

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं।

---

## PDF दस्तावेज़ बनाना – एब्सोल्यूट पोजीशन सेट करना

पहला काम हम एक खाली `Document` को इंस्टैंशिएट करना है। यह ऑब्जेक्ट पूरे PDF फ़ाइल का प्रतिनिधित्व करता है और हमें टैग्ड‑कंटेंट ट्री तक पहुँच देता है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**यह क्यों महत्वपूर्ण है:**  
`Document` PDF संरचना की जड़ है। इसे पहले बनाकर हम सुनिश्चित करते हैं कि दृश्य तत्वों (पेज, ग्राफिक्स) और तार्किक संरचना (टैग) दोनों के लिए एक कैनवास मौजूद हो। `using` स्टेटमेंट फ़ाइल को सही ढंग से डिस्पोज़ करना सुनिश्चित करता है, जिससे Windows पर फ़ाइल‑हैंडल लीक नहीं होते।

## टैग्ड कंटेंट सक्षम करें (How to Add Tagged)

किसी भी टैग्ड एलिमेंट को डालने से पहले, दस्तावेज़ को *टैग्ड* के रूप में चिह्नित होना चाहिए। Aspose.Pdf स्वचालित रूप से एक `TaggedContent` ऑब्जेक्ट बनाता है, लेकिन आपको फ़्लैग को ऑन करना होगा।

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**आंतरिक रूप से क्या होता है?:**  
`TaggedContent` को `true` सेट करने से PDF रीडर्स को बताया जाता है कि फ़ाइल में एक लॉजिकल स्ट्रक्चर ट्री है। यह स्क्रीन रीडर्स और `SetPosition` मेथड को स्पैन एलिमेंट पर सही ढंग से काम करने के लिए महत्वपूर्ण है।

## टैग्ड‑कंटेंट ट्री का रूट एलिमेंट प्राप्त करें

रूट एलिमेंट सभी स्ट्रक्चरल टैग्स (जैसे `<Document>`, `<Section>`, `<Span>`) का प्रवेश बिंदु है। इसे PDF के अदृश्य “बॉडी” के रूप में सोचें।

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**रूट की आवश्यकता क्यों है:**  
सभी बाद के टैग्स को ट्री में कहीं न कहीं अटैच होना चाहिए; अन्यथा वे एक्सेसिबिलिटी हायरार्की में नहीं दिखेंगे।

## स्पैन एलिमेंट जोड़ें – इनलाइन टेक्स्ट का बिल्डिंग ब्लॉक

*स्पैन* HTML `<span>` का PDF समकक्ष है—छोटे टेक्स्ट भागों को सटीक रूप से पोजिशन करने के लिए उत्तम।

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**डिज़ाइन नोट:**  
यदि आपको अधिक समृद्ध फ़ॉर्मेटिंग (बोल्ड, इटैलिक, हाइपरलिंक्स) चाहिए, तो आप स्पैन को `<Paragraph>` में रैप कर सकते हैं या बाद में `TextFragment` ऑब्जेक्ट्स का उपयोग कर सकते हैं। एब्सोल्यूट पोजीशनिंग के लिए, एक साधा स्पैन सबसे हल्का विकल्प है।

## एब्सोल्यूट पोजीशन सेट करें – X=100, Y=200

अब मज़ेदार हिस्सा आता है: पेज पर स्पैन को एक सटीक स्थान पर रखना। कॉर्डिनेट सिस्टम बॉटम‑लेफ़्ट कोने (0,0) से शुरू होता है और पॉइंट्स (1 pt ≈ 1/72 in) का उपयोग करता है।

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**एब्सोल्यूट पोजीशनिंग क्यों?:**  
जब आपको पिक्सेल‑परफेक्ट लेआउट चाहिए—जैसे प्रमाणपत्र, इनवॉइस, या फ़ॉर्म—रिलेटिव फ्लो (जैसे लेफ़्ट‑टू‑राइट टेक्स्ट) पर्याप्त नहीं होता। `SetPosition` सामान्य टेक्स्ट फ्लो को बायपास करता है और एलिमेंट को आपके द्वारा निर्दिष्ट स्थान पर पिन कर देता है।

## स्पैन में टेक्स्ट जोड़ें

स्पैन को पोजिशन करने के बाद, हम अब वास्तविक स्ट्रिंग डालते हैं।

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**टिप:**  
यदि आपको यूनिकोड कैरेक्टर्स या राइट‑टू‑लेफ़्ट स्क्रिप्ट्स चाहिए, तो बस स्ट्रिंग पास करें; Aspose.Pdf स्वचालित रूप से एन्कोडिंग संभालता है।

## स्पैन को रूट एलिमेंट में जोड़ें

अंत में, हम स्पैन को दस्तावेज़ के लॉजिकल ट्री में अटैच करते हैं ताकि यह अंतिम PDF का हिस्सा बन जाए।

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**यदि आप इस चरण को भूल जाएँ तो क्या होगा?:**  
स्पैन मेमोरी में मौजूद रहेगा लेकिन फ़ाइल में कभी सीरियलाइज़ नहीं होगा, इसलिए आपको कोई टेक्स्ट नहीं दिखेगा और एक्सेसिबिलिटी ट्री अधूरा रहेगा।

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूरा प्रोग्राम है जिसे आप कंसोल ऐप में डाल सकते हैं। यह एक‑पेज PDF बनाता है, (100, 200) पर एक टैग्ड स्पैन जोड़ता है, और फ़ाइल को `TaggedPositioned.pdf` के रूप में सेव करता है।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**अपेक्षित आउटपुट:**  
`TaggedPositioned.pdf` को किसी भी व्यूअर (Adobe Acrobat, Foxit, आदि) में खोलें। आपको वाक्यांश **“Positioned tagged text”** पेज के बाएँ किनारे से ठीक 100 pt और नीचे के किनारे से 200 pt पर दिखाई देगा। यदि आप *Tags* पैनल की जाँच करें, तो दस्तावेज़ के रूट के तहत एक `<Span>` एलिमेंट सूचीबद्ध होगा, जो पुष्टि करता है कि कंटेंट सही ढंग से टैग्ड है।

## सामान्य प्रश्न और किनारे के मामलों

### यदि मुझे पहले पेज के अलावा किसी विशिष्ट पेज पर टेक्स्ट पोजिशन करना हो तो?

`SetPosition` कॉल करने से पहले वह पेज जोड़ें जिसे आप चाहते हैं (`var page = pdfDocument.Pages[3];`)। स्पैन स्वचालित रूप से सक्रिय पेज कॉन्टेक्स्ट से जुड़ जाएगा।

### क्या मैं पोजीशन इंच या सेंटीमीटर में सेट कर सकता हूँ?

`SetPosition` पॉइंट्स को स्वीकार करता है। नीचे दिए फ़ॉर्मूले से कन्वर्ट करें:  
- **इंच → पॉइंट्स:** `points = inches * 72`  
- **सेन्टीमीटर → पॉइंट्स:** `points = cm * 28.3465`

### मैं स्पैन का फ़ॉन्ट या रंग कैसे बदलूँ?

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### यदि दस्तावेज़ में पहले से टैग्स मौजूद हों तो क्या करें?

आप अभी भी एक नया स्पैन बना सकते हैं और इसे किसी भी मौजूदा एलिमेंट (`rootElement`, एक विशिष्ट `<Section>`, आदि) में जोड़ सकते हैं। बस यह सुनिश्चित करें कि आप एक लॉजिकल हायरार्की बनाए रखें—स्क्रीन रीडर्स एक अच्छी तरह संरचित ट्री की अपेक्षा करते हैं।

### क्या यह PDF/A या PDF/UA अनुपालन के साथ काम करता है?

हाँ। टैग्ड PDFs PDF/UA के लिए एक मुख्य आवश्यकता है। यदि आपको PDF/A चाहिए, तो कंटेंट बन जाने के बाद `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` सेट करें।

## प्रो टिप्स और पिटफ़ॉल्स

- **Pro tip:** कंटेंट को पोजिशन करने से पहले हमेशा एक पेज जोड़ें। पेज न होने पर, `SetPosition` चुपचाप फेल हो जाता है क्योंकि रेंडर करने की जगह नहीं होती।  
- **Watch out for units:** UI डिज़ाइन के पिक्सेल को PDF पॉइंट्स के साथ मिलाने से आपका टेक्स्ट गलत जगह पर जाएगा। अपने कन्वर्ज़न को दोबारा जाँचें।  
- **Performance hint:** यदि आप हजारों PDFs जेनरेट कर रहे हैं, तो एक ही `Document` इंस्टेंस को पुनः उपयोग करें और रन के बीच `pdfDocument.Pages.Clear()` कॉल करें ताकि अत्यधिक मेमोरी अलोकेशन से बचा जा सके।  
- **Accessibility reminder:** टैगिंग केवल एक अतिरिक्त सुविधा नहीं है; कई नियम (Section 508, EN 301 549) इसे अनिवार्य करते हैं। `CreateSpanElement` का उपयोग करने से टेक्स्ट सहायक तकनीकों द्वारा खोजा जा सकेगा।  

## निष्कर्ष

हमने अभी **created pdf document** को शून्य से बनाया, **एब्सोल्यूट पोजीशन सेट की**, **स्पैन एलिमेंट जोड़ा**, और **how to add tagged** कंटेंट दिखाया ताकि आप **position text on page** को पिक्सेल‑परफेक्ट सटीकता के साथ कर सकें। पूर्ण उदाहरण चलाने के लिए तैयार है, और व्याख्या ने *how* और *why* दोनों को कवर किया—वही जो डेवलपर्स (और AI असिस्टेंट) एक विश्वसनीय समाधान के लिए खोजते हैं।

अगले चरण में, आप खोज सकते हैं:

- पोजिशन किए गए टेक्स्ट के पीछे इमेजेज़ जोड़ना वॉटरमार्क्ड प्रमाणपत्रों के लिए।  
- `CreateParagraphElement` का उपयोग करके मल्टी‑लाइन ब्लॉक्स बनाना जो अभी भी एब्सोल्यूट प्लेसमेंट की आवश्यकता रखते हैं।  
- स्ट्रिक्ट एक्सेसिबिलिटी ऑडिट्स को पूरा करने के लिए PDF/UA में एक्सपोर्ट करना।  

कोऑर्डिनेट्स, फ़ॉन्ट्स, या रंगों को बदलने में संकोच न करें—प्रयोग ही टैग्ड PDF जेनरेशन में महारत हासिल करने का सबसे तेज़ तरीका है। यदि आपको कोई समस्या आती है, तो नीचे कमेंट छोड़ें; कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}