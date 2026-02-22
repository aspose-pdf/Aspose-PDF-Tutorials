---
category: general
date: 2026-02-22
description: Aspose.Pdf का उपयोग करके गोपनीय वॉटरमार्क PDF ट्यूटोरियल – सीखें कि कैसे
  किसी भी PDF के पहले पृष्ठ पर गोपनीय लेबल को टेक्स्ट स्टैम्प के रूप में जोड़ा जाए।
draft: false
keywords:
- confidential watermark pdf
- add confidential label
- aspose pdf watermark
- add stamp first page
- add text stamp pdf
language: hi
og_description: 'गोपनीय वॉटरमार्क PDF गाइड: Aspose.Pdf for .NET का उपयोग करके पहले
  पृष्ठ पर टेक्स्ट स्टैम्प के रूप में गोपनीय लेबल जोड़ने के चरण‑दर‑चरण निर्देश।'
og_title: Aspose के साथ गोपनीय वॉटरमार्क PDF – टेक्स्ट स्टैम्प जोड़ें
tags:
- aspose
- pdf
- watermark
- csharp
title: 'Aspose के साथ गोपनीय वॉटरमार्क PDF: पहले पृष्ठ पर टेक्स्ट स्टैम्प जोड़ें'
url: /hi/net/programming-with-stamps-and-watermarks/confidential-watermark-pdf-with-aspose-add-a-text-stamp-to-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# गोपनीय वॉटरमार्क PDF – पहले पृष्ठ पर टेक्स्ट स्टैम्प कैसे जोड़ें

क्या आपको कभी **confidential watermark PDF** की ज़रूरत पड़ी, लेकिन सिर्फ पहले पृष्ठ पर लेबल कैसे लगाएँ, यह नहीं पता था? आप अकेले नहीं हैं—कई डेवलपर्स इस सवाल से जूझते हैं “लेआउट बिगड़े बिना गोपनीय लेबल कैसे जोड़ूँ?”  

अच्छी खबर? Aspose.Pdf for .NET के साथ आप इसे कुछ ही लाइनों में कर सकते हैं, और मैं आपको अभी पूरी प्रक्रिया दिखाऊँगा। कोई अस्पष्ट संदर्भ नहीं, सिर्फ एक पूर्ण, कॉपी‑एंड‑पेस्ट समाधान जो आज काम करता है।

## आप क्या सीखेंगे

इस ट्यूटोरियल में हम कवर करेंगे:

* Aspose.Pdf NuGet पैकेज को इंस्टॉल करना (एकमात्र पूर्वापेक्षा)।
* मौजूदा PDF को लोड करना।
* `TextStamp` का उपयोग करके **confidential watermark PDF** बनाना।
* उस स्टैम्प को **सिर्फ पहले पृष्ठ** पर जोड़ना ( “add stamp first page” आवश्यकता)।
* परिणाम को सेव करना और आउटपुट की जाँच करना।

अंत तक आपके पास एक तैयार‑से‑उपयोग स्निपेट होगा जिसे आप किसी भी C# प्रोजेक्ट में डाल सकते हैं, साथ ही कई पृष्ठों या विभिन्न स्टैम्प शैलियों के लिए स्केल करने के टिप्स भी मिलेंगे।

## पूर्वापेक्षाएँ

* .NET 6+ (कोड .NET Core और .NET Framework दोनों पर काम करता है)।
* Visual Studio 2022 या आपका पसंदीदा IDE।
* Aspose.Pdf for .NET – संस्करण 23.10 या नया, नवीनतम बग फिक्स के लिए अनुशंसित।

यदि आपने अभी तक अपने प्रोजेक्ट में Aspose.Pdf नहीं जोड़ा है, तो चलाएँ:

```bash
dotnet add package Aspose.Pdf
```

बस इतना ही—कोई अतिरिक्त DLLs नहीं, ट्रायल के लिए लाइसेंस हेडेक्स नहीं (शिप करने से पहले अपना लाइसेंस की लागू करना याद रखें)।

## चरण 1: स्रोत PDF दस्तावेज़ लोड करें

सबसे पहले हमें उस फ़ाइल को खोलना है जिसे हम सुरक्षित करना चाहते हैं। `Document` क्लास पूरे PDF का प्रतिनिधित्व करता है, और इसे लोड करना बस पाथ पास करने जितना आसान है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the PDF you want to watermark
string inputPdfPath = @"C:\MyDocs\input.pdf";

// Load the PDF into memory
using var pdfDocument = new Document(inputPdfPath);
```

*क्यों महत्वपूर्ण है*: दस्तावेज़ को लोड करने से आपको `Pages` कलेक्शन तक पहुँच मिलती है, जहाँ हम स्टैम्प जोड़ेंगे। `using var` का उपयोग फ़ाइल हैंडल को तुरंत रिलीज़ कर देता है—बड़े बैचों के लिए यह महत्वपूर्ण है।

## चरण 2: गोपनीय टेक्स्ट स्टैम्प बनाएं

अब हम विज़ुअल लेबल तैयार करते हैं। `TextStamp` हमें आकार, रैपिंग और स्केलिंग को नियंत्रित करने देता है। नीचे दिए गए सेटिंग्स यह सुनिश्चित करती हैं कि शब्द *Confidential* बिना ओवरफ़्लो हुए ठीक से फिट हो।

```csharp
// Build a text stamp that says "Confidential"
var confidentialStamp = new TextStamp("Confidential")
{
    // Auto‑adjust the font so it never exceeds the rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,

    // Wrap by whole words—no broken words in the middle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

    // Define the stamp rectangle (you can tweak width/height)
    Width = 300,
    Height = 100,

    // Keep the stamp size constant even if the page is resized
    Scale = false
};
```

**प्रो टिप**: यदि आपको अलग फ़ॉन्ट या रंग चाहिए, तो `confidentialStamp.TextState.Font` और `confidentialStamp.TextState.ForegroundColor` सेट करें। उदाहरण के लिए, `confidentialStamp.TextState.Font = FontRepository.FindFont("Arial")` और `confidentialStamp.TextState.ForegroundColor = Color.Red`।

## चरण 3: स्टैम्प केवल पहले पृष्ठ पर जोड़ें

Aspose पेज इंडेक्सिंग 1‑आधारित करता है, इसलिए `Pages[1]` पहला पृष्ठ है। यहाँ स्टैम्प जोड़ने से **add stamp first page** आवश्यकता पूरी होती है।

```csharp
// Attach the stamp to the very first page
pdfDocument.Pages[1].AddStamp(confidentialStamp);
```

यदि आपको हर पृष्ठ पर वॉटरमार्क लगाना हो, तो `pdfDocument.Pages` पर लूप करें। लेकिन एक‑पृष्ठ लेबल के लिए यह एक‑लाइनर काम कर देता है।

## चरण 4: वॉटरमार्क्ड PDF को सेव करें

अंत में, संशोधित दस्तावेज़ को डिस्क पर लिखें। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई फ़ाइल बना सकते हैं—आपकी पसंद।

```csharp
// Destination path for the watermarked PDF
string outputPdfPath = @"C:\MyDocs\Stamped.pdf";

// Persist the changes
pdfDocument.Save(outputPdfPath);
```

जब आप `Stamped.pdf` खोलेंगे, तो आपको *Confidential* पृष्ठ 1 के ऊपर‑बाएँ कोने में (या जहाँ आपने स्टैम्प रखा है) दिखेगा। दस्तावेज़ का बाकी हिस्सा अपरिवर्तित रहेगा।

## अपेक्षित परिणाम

| पहले | बाद (पहला पृष्ठ) |
|--------|-------------------|
| ![मूल PDF पृष्ठ](/images/original.png "मूल PDF पृष्ठ") | ![गोपनीय वॉटरमार्क PDF उदाहरण](/images/confidential-watermark.png "गोपनीय वॉटरमार्क PDF उदाहरण") |

*Image alt text*: **गोपनीय वॉटरमार्क PDF उदाहरण** (मुख्य कीवर्ड शामिल है)।

## किनारे के मामलों और सामान्य प्रश्न

### यदि PDF में कोई पृष्ठ नहीं है तो क्या होगा?

`Pages[1]` तक पहुँचने की कोशिश करने पर `ArgumentOutOfRangeException` फेंका जाएगा। इसे रोकने के लिए:

```csharp
if (pdfDocument.Pages.Count == 0)
    throw new InvalidOperationException("The PDF is empty.");
```

### कई पृष्ठों पर वॉटरमार्क कैसे लगाएँ?

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(confidentialStamp);
}
```

यदि आप प्रत्येक पृष्ठ पर अलग‑कोने में स्टैम्प चाहते हैं, तो `confidentialStamp` की पोजीशन रीसेट करना न भूलें।

### क्या मैं स्टैम्प की पोजीशन बदल सकता हूँ?

हाँ—`confidentialStamp.HorizontalAlignment` और `confidentialStamp.VerticalAlignment` सेट करें, या पिक्सेल‑परफ़ेक्ट प्लेसमेंट के लिए `confidentialStamp.XIndent` / `YIndent` उपयोग करें।

### क्या यह पासवर्ड‑प्रोटेक्टेड PDFs के साथ काम करता है?

Aspose पासवर्ड प्रदान करने पर एन्क्रिप्टेड फ़ाइलें खोल सकता है:

```csharp
var pdfDocument = new Document(inputPdfPath, new LoadOptions { Password = "mySecret" });
```

### बड़े बैचों पर प्रदर्शन कैसा रहेगा?

प्रत्येक दस्तावेज़ को अलग‑अलग लोड और सेव करना I/O‑हेवी हो सकता है। एक ही `Document` इंस्टेंस को इन‑मेमोरी ऑपरेशन्स के लिए पुन: उपयोग करें और बैच के अंत में केवल एक बार persist करें।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम है जिसे आप कॉन्सोल ऐप में कॉपी‑पेस्ट कर सकते हैं। इसमें सभी चरण, एरर हैंडलिंग, और एक सरल वेरिफिकेशन मैसेज शामिल है।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        string inputPdfPath = @"C:\MyDocs\input.pdf";
        if (!System.IO.File.Exists(inputPdfPath))
        {
            Console.WriteLine("Input file not found.");
            return;
        }

        using var pdfDocument = new Document(inputPdfPath);

        if (pdfDocument.Pages.Count == 0)
        {
            Console.WriteLine("The PDF contains no pages.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Create the confidential text stamp
        // -------------------------------------------------
        var confidentialStamp = new TextStamp("Confidential")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 300,
            Height = 100,
            Scale = false,
            // Optional styling
            TextState = { FontSize = 24, Font = FontRepository.FindFont("Arial"), ForegroundColor = Color.Red }
        };

        // -------------------------------------------------
        // 3️⃣ Add the stamp to the first page only
        // -------------------------------------------------
        pdfDocument.Pages[1].AddStamp(confidentialStamp);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        string outputPdfPath = @"C:\MyDocs\Stamped.pdf";
        pdfDocument.Save(outputPdfPath);

        Console.WriteLine($"Successfully added a confidential watermark PDF. Saved to: {outputPdfPath}");
    }
}
```

प्रोग्राम चलाएँ, `Stamped.pdf` खोलें, और आपको **confidential watermark PDF** ठीक उसी जगह पर दिखाई देगा जहाँ हमने इरादा किया था।

## निष्कर्ष

अब आपके पास Aspose.Pdf का उपयोग करके किसी भी PDF के **पहले पृष्ठ** पर **टेक्स्ट स्टैम्प** के रूप में **गोपनीय लेबल** जोड़ने का एक ठोस, प्रोडक्शन‑रेडी तरीका है। समाधान पूरी तरह से स्व-निहित है, नवीनतम .NET संस्करणों के साथ काम करता है, और इसे कई पृष्ठों, कस्टम फ़ॉन्ट्स या विभिन्न रंगों के लिए विस्तारित किया जा सकता है।

**अगले कदम** जिन्हें आप एक्सप्लोर कर सकते हैं:

* टेक्स्ट स्टैम्प को इमेज स्टैम्प (`ImageStamp`) से बदलें ताकि लोगो एम्बेड हो सके।
* इस दृष्टिकोण को लूप के साथ मिलाकर पूरे दस्तावेज़ में **aspose pdf watermark** बनाएं।
* कोड को ASP.NET Core API में इंटीग्रेट करें ताकि उपयोगकर्ता PDFs अपलोड कर सकें और तुरंत वॉटरमार्क्ड संस्करण प्राप्त कर सकें।

इसे आज़माएँ, आयामों को समायोजित करें, और **add text stamp pdf** तकनीक को अपने दस्तावेज़‑सुरक्षा टूलबॉक्स में एक मुख्य उपकरण बनाएं। हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}