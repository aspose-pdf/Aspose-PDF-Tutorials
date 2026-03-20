---
category: general
date: 2026-03-19
description: Aspose.Pdf का उपयोग करके C# में PDF के पहले पृष्ठ पर स्टैम्प जोड़ें और
  PDF पर वॉटरमार्क लागू करें। PDF में नोट जोड़ना सीखें और एक पूर्ण कार्यशील उदाहरण
  देखें।
draft: false
keywords:
- add stamp to pdf
- apply watermark pdf
- add note to pdf
- how to add stamp
- add stamp first page
language: hi
og_description: Aspose.Pdf का उपयोग करके C# में PDF के पहले पृष्ठ पर स्टैम्प जोड़ें
  और वॉटरमार्क लागू करें। पूर्ण चरण‑दर‑चरण गाइड।
og_title: PDF में स्टैम्प जोड़ें – पहले पृष्ठ पर वॉटरमार्क लागू करें
tags:
- aspnet
- csharp
- pdf
- aspose
title: PDF में स्टैम्प जोड़ें – पहले पृष्ठ पर PDF वॉटरमार्क लागू करें
url: /hi/net/programming-with-stamps-and-watermarks/add-stamp-to-pdf-apply-watermark-pdf-on-first-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF में स्टैम्प जोड़ें – पहले पृष्ठ पर वॉटरमार्क लागू करें

क्या आपको कभी **PDF में स्टैम्प जोड़ने** की ज़रूरत पड़ी है लेकिन आप नहीं जानते थे कि कहाँ से शुरू करें? शायद आप उसी पृष्ठ पर **PDF में वॉटरमार्क लागू करना** चाहते हैं, या समीक्षकों के लिए जल्दी से **PDF में नोट जोड़ना** चाहते हैं। इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने योग्य C# उदाहरण के माध्यम से आपको दिखाएंगे कि यह कैसे किया जाता है, और हम प्रत्येक लाइन के “क्यों” को समझाएंगे ताकि आप इसे किसी भी स्थिति में अनुकूलित कर सकें।

हम स्रोत दस्तावेज़ को लोड करने से लेकर स्टैम्प किया हुआ संस्करण सहेजने तक सब कुछ कवर करेंगे, साथ ही मल्टी‑पेज PDFs को संभालने, स्केलिंग समस्याओं, और स्टैम्प की उपस्थिति को अनुकूलित करने के कुछ टिप्स भी देंगे। अंत तक आप आत्मविश्वास के साथ “**स्टैम्प कैसे जोड़ें**?” का उत्तर दे पाएँगे और **पहले पृष्ठ पर स्टैम्प जोड़ना** बिना किसी परेशानी के जान पाएँगे।

---

## आपको क्या चाहिए

- **Aspose.Pdf for .NET** (कोई भी नवीनतम संस्करण, जैसे 23.10) – वह लाइब्रेरी जो PDF हेरफेर को आसान बनाती है।  
- .NET विकास वातावरण (Visual Studio, VS Code, Rider – जैसा भी आपको पसंद हो)।  
- एक इनपुट PDF फ़ाइल (हम इसे `input.pdf` कहेंगे) जिसे आप किसी फ़ोल्डर में रख सकते हैं।  

Aspose.Pdf के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है, और कोड .NET 6+ तथा .NET Framework 4.7.2 दोनों पर काम करता है।

![PDF में स्टैम्प जोड़ने का उदाहरण](/images/add-stamp-to-pdf.png "एक PDF की स्क्रीनशॉट जिसमें टेक्स्ट स्टैम्प है – PDF में स्टैम्प जोड़ें")

*Alt text: PDF में स्टैम्प जोड़ें – PDF के पहले पृष्ठ पर लागू टेक्स्ट स्टैम्प का दृश्य उदाहरण.*

## चरण 1 – स्रोत PDF दस्तावेज़ लोड करें

PDF में **स्टैम्प जोड़ने** के लिए, हमें पहले फ़ाइल का इन‑मेमोरी प्रतिनिधित्व चाहिए। `Aspose.Pdf.Document` क्लास यह काम करती है।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class PdfStampDemo
{
    static void Main()
    {
        // Load the original PDF (replace YOUR_DIRECTORY with your actual path)
        var pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);
```

**यह क्यों महत्वपूर्ण है:**  
`Document` फ़ाइल संरचना को पार्स करता है, जिससे आपको पृष्ठों, एनोटेशन और संसाधनों तक पहुँच मिलती है। `using` ब्लॉक का उपयोग करने से फ़ाइल हैंडल तुरंत रिलीज़ हो जाता है—जब आप बाद में उसी फ़ाइल को ओवरराइट करने की कोशिश करते हैं तो यह महत्वपूर्ण है।

## चरण 2 – टेक्स्ट स्टैम्प बनाएं और कॉन्फ़िगर करें

अब हम `TextStamp` बनाकर PDF में **नोट जोड़ेंगे**। यह ऑब्जेक्ट वॉटरमार्क की तरह व्यवहार करता है, लेकिन आप आकार, फ़ॉन्ट और शब्द‑रैप को नियंत्रित कर सकते हैं।

```csharp
        // Step 2: Create a text stamp that will serve as a note/watermark
        var textStamp = new TextStamp("Important note")
        {
            // Auto‑adjust font size so the text fits inside the stamp rectangle
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,

            // Wrap words rather than breaking them mid‑word
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

            // Define the stamp rectangle (you can tweak these values)
            Width = 400,
            Height = 200,

            // Turn off scaling – we want the stamp to keep its exact size
            Scale = false
        };
```

**ध्यान रखने योग्य मुख्य बिंदु:**

- `AutoAdjustFontSizeToFitStampRectangle` स्टैम्प को छोटा या बड़ा करने देता है ताकि टेक्स्ट कभी ओवरफ़्लो न हो – विभिन्न पृष्ठ आकारों पर **PDF में वॉटरमार्क लागू करने** के समय उपयोगी।  
- `WordWrapMode.ByWords` सुनिश्चित करता है कि टेक्स्ट शब्द सीमाओं पर रैप हो, जिससे नोट पढ़ने योग्य बनता है।  
- `Scale = false` सेट करने से पृष्ठ DPI बदलने पर स्टैम्प खिंचा नहीं जाता।

## चरण 3 – स्टैम्प को पहले पृष्ठ से जोड़ें

यदि आप सोच रहे हैं कि **स्टैम्प कैसे जोड़ें** विशेष रूप से पहले पृष्ठ पर, तो यही जगह है। `Pages` संग्रह 1‑आधारित है, इसलिए `Pages[1]` पहला पृष्ठ है।

```csharp
        // Step 3: Add the configured stamp to the first page
        pdfDocument.Pages[1].AddStamp(textStamp);
```

**पहले पृष्ठ का कारण क्या है?**  
कई कानूनी या ब्रांडिंग आवश्यकताएँ केवल कवर पृष्ठ पर एक दृश्यमान वॉटरमार्क मांगती हैं। `Pages[1]` को लक्षित करके हम **पहले पृष्ठ पर स्टैम्प जोड़ने** की स्थिति को पूरे दस्तावेज़ को लूप किए बिना पूरा करते हैं।

## चरण 4 – संशोधित PDF सहेजें

अंत में, बदलावों को डिस्क पर लिखें। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई फ़ाइल बना सकते हैं; यहाँ हम `Stamped.pdf` बनाएँगे।

```csharp
        // Step 4: Save the stamped PDF
        var outputPath = @"YOUR_DIRECTORY\Stamped.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Stamp added successfully! Output saved to {outputPath}");
    }
}
```

प्रोग्राम चलाने पर एक PDF बनेगा जहाँ पहले पृष्ठ पर “Important note” स्टैम्प दिखेगा, जिससे प्रभावी रूप से **PDF में स्टैम्प जोड़ना** और साथ ही **PDF में वॉटरमार्क लागू करना** एक ही बार में हो जाएगा।

## वैकल्पिक: विभिन्न परिदृश्यों के लिए स्टैम्प को ट्यून करना

### कई पृष्ठ

यदि आप बाद में तय करते हैं कि आपको *हर* पृष्ठ पर वही नोट चाहिए, तो एकल‑पृष्ठ लाइन को लूप से बदलें:

```csharp
foreach (var page in pdfDocument.Pages)
{
    page.AddStamp(textStamp);
}
```

### इमेज स्टैम्प

यदि आप टेक्स्ट के बजाय लोगो पसंद करते हैं तो Aspose `ImageStamp` भी सपोर्ट करता है। वही प्रॉपर्टीज़ (आकार, स्थिति, स्केलिंग) लागू होती हैं।

### स्टैम्प की पोजिशनिंग

डिफ़ॉल्ट रूप से स्टैम्प आयत के टॉप‑लेफ़्ट कोने में दिखाई देता है। इसे स्थानांतरित करने के लिए, `HorizontalAlignment` और `VerticalAlignment` सेट करें:

```csharp
textStamp.HorizontalAlignment = HorizontalAlignment.Center;
textStamp.VerticalAlignment = VerticalAlignment.Middle;
```

## सामान्य समस्याएँ और प्रो टिप्स

- **फ़ाइल लॉक:** यदि आपको `IOException` मिलता है जिसमें कहा गया है कि फ़ाइल उपयोग में है, तो सुनिश्चित करें कि कोई अन्य प्रक्रिया (एक्सप्लोरर सहित) PDF को नहीं खोल रही है। `using` ब्लॉक मदद करता है, लेकिन दोबारा जाँचें।  
- **फ़ॉन्ट समस्याएँ:** Aspose डिफ़ॉल्ट रूप से सिस्टम फ़ॉन्ट्स का उपयोग करता है। गैर‑लैटिन स्क्रिप्ट्स के लिए, आवश्यक फ़ॉन्ट एम्बेड करें या `textStamp.Font` स्पष्ट रूप से सेट करें।  
- **बड़ी PDFs:** 100 MB से बड़ी PDFs के लिए, सहेजने से पहले `pdfDocument.Optimize()` उपयोग करने पर विचार करें ताकि फ़ाइल आकार कम हो सके।  
- **टेस्टिंग:** उत्पन्न `Stamped.pdf` को कई व्यूअर्स (Adobe Reader, Edge, Chrome) में खोलें ताकि स्टैम्प लगातार रेंडर हो रहा हो, यह पुष्टि हो सके।  

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class PdfStampDemo
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Create a configurable text stamp (our note/watermark)
        var textStamp = new TextStamp("Important note")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 400,
            Height = 200,
            Scale = false,
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Middle
        };

        // 3️⃣ Add the stamp to the first page (add stamp first page)
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 4️⃣ Save the stamped PDF
        var outputPath = @"YOUR_DIRECTORY\Stamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"Stamp added successfully! Output saved to {outputPath}");
    }
}
```

**अपेक्षित परिणाम:** `Stamped.pdf` खोलें; पहला पृष्ठ 400 × 200 पॉइंट आकार का केंद्रित “Important note” बॉक्स दिखाएगा, जिसमें टेक्स्ट स्वचालित रूप से फिट होने के लिए री‑साइज़ हो जाता है। अन्य सभी पृष्ठ अपरिवर्तित रहते हैं।

## निष्कर्ष

हमने अभी दिखाया कि कैसे **PDF में स्टैम्प जोड़ें** और **PDF में वॉटरमार्क लागू करें** एक साफ़, पुन: उपयोग योग्य तरीके से किया जाता है। दस्तावेज़ को लोड करके, `TextStamp` को कॉन्फ़िगर करके, इसे **पहले पृष्ठ पर स्टैम्प जोड़ने** के लिए अटैच करके, और सहेजकर, आप बिना लो‑लेवल PDF स्ट्रीम्स के साथ छेड़छाड़ किए एक पेशेवर‑दिखावट वाला नोट प्राप्त करते हैं।

अब आप हर पृष्ठ पर स्टैम्प जोड़ने, इमेज बदलने, या जटिल ब्रांडिंग के लिए कई स्टैम्प स्टैक करने का अन्वेषण कर सकते हैं। वही पैटर्न—बनाएँ, कॉन्फ़िगर करें, अटैच करें, सहेजें—अधिकांश Aspose.Pdf कार्यों में लागू होता है, इसलिए इसे विस्तारित करना आसान होगा।

यदि आपका कोई अलग उपयोग मामला है, जैसे बैच जॉब में दर्जनों PDFs पर गोपनीय लेबल स्टैम्प करना? ऊपर की लॉजिक को `foreach` में लपेटें जो फ़ाइलों के फ़ोल्डर पर इटररेट करता है। या, यदि आपको पृष्ठ सामग्री के आधार पर शर्तीय रूप से **PDF में नोट जोड़ना** है, तो स्टैम्प करने से पहले टेक्स्ट खोजने के लिए Aspose के `TextFragmentAbsorber` को देखें।

कोडिंग का आनंद लें, और आपके PDFs हमेशा बिल्कुल उसी तरह स्टैम्प हों जैसा आपको चाहिए! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}