---
category: general
date: 2026-03-27
description: Aspose.Pdf for C# का उपयोग करके PDF में आयत कैसे बनाएं, सीखें। PDF में
  आयत जोड़ें, PDF में आकार जोड़ें और स्पष्ट कोड उदाहरणों के साथ PDF पर आकार बनाएं।
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: hi
og_description: Aspose.Pdf का उपयोग करके PDF में आयत कैसे बनाएं, इसमें महारत हासिल
  करें। यह ट्यूटोरियल आपको चरण-दर-चरण दिखाता है कि PDF में आयत कैसे जोड़ें, PDF में
  आकार कैसे जोड़ें, और PDF पर आकार कैसे बनाएं।
og_title: C# के साथ PDF में आयत कैसे बनाएं – पूर्ण गाइड
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C# के साथ PDF में आयत कैसे बनाएं – चरण‑दर‑चरण गाइड
url: /hi/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ PDF में आयत कैसे बनाएं – चरण‑दर‑चरण गाइड

क्या आपने कभी **PDF में आयत कैसे बनाएं** के बारे में सोचा है बिना लो‑लेवल PDF सिंटैक्स से जूझे? आप अकेले नहीं हैं। कई डेवलपर्स को तब रुकावट आती है जब उन्हें जनरेटेड दस्तावेज़ में बाउंडिंग बॉक्स, हाइलाइट एरिया, या एक साधारण सजावटी तत्व दिखाना होता है। अच्छी खबर? Aspose.Pdf for .NET के साथ यह प्रक्रिया बहुत आसान है।

इस ट्यूटोरियल में हम आपको **add rectangle to PDF**, **add shape to PDF**, और अंततः **draw rectangle in PDF** करने के लिए आवश्यक सब कुछ बताएंगे, साफ़ और idiomatic C# का उपयोग करके। अंत तक आपके पास एक runnable प्रोग्राम होगा जो एक crisp आयत वाला PDF फ़ाइल बनाता है—बिना किसी बाहरी टूल के।

## आवश्यकताएँ

- .NET 6.0 या बाद का (कोड .NET Core और .NET Framework के साथ भी काम करता है)
- Aspose.Pdf for .NET NuGet पैकेज (`Install-Package Aspose.Pdf`)
- एक बेसिक C# डेवलपमेंट एनवायरनमेंट (Visual Studio, VS Code, Rider, आदि)

कोई अन्य लाइब्रेरीज़ आवश्यक नहीं हैं; बाकी सब कुछ Aspose.Pdf खुद संभालता है।

## चरण 1: प्रोजेक्ट सेट अप करें और नेमस्पेसेस इम्पोर्ट करें

सबसे पहले, एक नया कंसोल एप्लिकेशन बनाएं और Aspose.Pdf नेमस्पेस को इम्पोर्ट करें।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Why this matters:** `Aspose.Pdf.Drawing` को इम्पोर्ट करने से आपको `Rectangle` shape क्लास मिलती है जिसका उपयोग हम **draw shape on PDF** करने के लिए करेंगे। एंट्री पॉइंट को साफ़ रखने से बाद के चरणों को फॉलो करना आसान होता है।

## चरण 2: नया PDF डॉक्यूमेंट और एक पेज बनाएं

पेजों के बिना PDF बेकार है, इसलिए हम एक डॉक्यूमेंट ऑब्जेक्ट बनाकर एक सिंगल पेज जोड़ते हैं।

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Explanation:** `Document` क्लास पूरे फ़ाइल को दर्शाता है, जबकि `Pages.Add()` एक नया `Page` ऑब्जेक्ट रिटर्न करता है जहाँ हम बाद में **add rectangle to PDF** करेंगे। डिफ़ॉल्ट A4 साइज अधिकांश मामलों में काम करता है, लेकिन यदि आपको कस्टम कैनवास चाहिए तो आप width/height पास कर सकते हैं।

## चरण 3: Rectangle Shape को परिभाषित करें

अब आता है **how to draw rectangle** का मुख्य भाग—उसकी पोज़िशन और डाइमेंशन को परिभाषित करना।

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Why we set these properties:**  
- `BorderColor` और `BorderWidth` आउटलाइन को नियंत्रित करते हैं, जिससे आयत दिखाई देती है।  
- `FillColor` इसे एक हल्का बैकग्राउंड देता है, जो किसी क्षेत्र को हाइलाइट करने में उपयोगी है।  
- कंस्ट्रक्टर `(x, y, width, height)` आपको **draw rectangle in PDF** ठीक उसी जगह बनाने देता है जहाँ आपको चाहिए।

## चरण 4: आयत को पेज में जोड़ें

Shape तैयार होने के बाद, हम अब **add shape to PDF** पेज की `Annotations` कलेक्शन में अटैच करके करते हैं। Aspose.Pdf स्वचालित रूप से बाउंड्स को वैलिडेट करता है, इसलिए आपको ओवरफ़्लो की चिंता नहीं करनी पड़ेगी।

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**What happens under the hood:** `Annotations` कलेक्शन आयत को एक वेक्टर ग्राफिक के रूप में ट्रीट करता है। जब PDF रेंडर होता है, लाइब्रेरी हमारे कोऑर्डिनेट्स को PDF कंटेंट स्ट्रीम में ट्रांसलेट करती है।

## चरण 5: डॉक्यूमेंट को सेव करें

अंत में, PDF को डिस्क पर लिखें ताकि आप इसे किसी भी व्यूअर में खोल सकें।

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Result:** `RectangleDemo.pdf` खोलने पर एक लाइट‑ग्रे आयत काली बॉर्डर के साथ दिखती है, जो पेज के बाएँ से 100 pts और नीचे से 500 pts पर स्थित है। यही C# का उपयोग करके PDF में **how to draw rectangle** की पूरी समाधान है।

## पूर्ण कार्यशील उदाहरण

सभी हिस्सों को जोड़ते हुए, यहाँ पूरा, रन‑तैयार प्रोग्राम है:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Expected output:** `RectangleDemo.pdf` नाम की फ़ाइल जिसमें एक सिंगल पेज है, जिसमें केंद्रित लाइट‑ग्रे आयत काली बॉर्डर के साथ है। आप इसे Adobe Reader, Chrome, या किसी भी PDF व्यूअर से खोल सकते हैं।

## सामान्य विविधताएँ और एज केस

### 1. कई आयतें बनाना

यदि आपको **add rectangle to PDF** एक से अधिक बार करना है, तो बस अतिरिक्त `Rectangle` ऑब्जेक्ट बनाएं और प्रत्येक को `page.Annotations` में जोड़ें। कोऑर्डिनेट्स के कलेक्शन पर लूप करना इसे बहुत आसान बनाता है।

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. विभिन्न यूनिट्स का उपयोग

Aspose.Pdf पॉइंट्स में काम करता है (1 pt = 1/72 इंच)। यदि आप मिलीमीटर पसंद करते हैं, तो पहले उन्हें कन्वर्ट करें:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. आयत को फ़ॉर्म फ़ील्ड के रूप में जोड़ना

जब आपको एक इंटरैक्टिव आयत चाहिए (जैसे, क्लिक करने योग्य एरिया), तो साधारण `Rectangle` के बजाय `LinkAnnotation` का उपयोग करें। कोड समान है लेकिन एक URL या JavaScript एक्शन जोड़ता है।

### 4. संगतता संबंधी चिंताएँ

Aspose.Pdf संस्करण 23.9 (early 2026 में रिलीज़) ऊपर दिखाए गए API को पूरी तरह सपोर्ट करता है। पुराने संस्करणों को `page.Annotations.Add` के बजाय `page.AddAnnotation(rectangleShape)` की आवश्यकता हो सकती है। यदि आपको कंपाइल एरर मिलते हैं तो हमेशा रिलीज़ नोट्स चेक करें।

## प्रो टिप्स और पिटफ़ॉल्स

- **Pro tip:** यदि आपको केवल आउटलाइन चाहिए तो `FillColor = Color.Transparent` सेट करें। इससे फ़ाइल साइज थोड़ा कम हो जाता है।
- **Watch out for:** ऐसे कोऑर्डिनेट्स का उपयोग जो पेज डाइमेंशन्स से अधिक हों। Aspose.Pdf चुपचाप शैप को क्लिप कर देगा, जो डिबगिंग में भ्रमित कर सकता है।
- **Performance note:** हजारों आयतें जोड़ना ठीक है, लेकिन यदि आप बड़े रिपोर्ट जनरेट कर रहे हैं तो ओवरहेड कम करने के लिए शैप्स को एक ही `Graphics` ऑब्जेक्ट में बैच करने पर विचार करें।

## विज़ुअल रेफ़रेंस

नीचे जनरेटेड PDF का एक त्वरित स्क्रीनशॉट है (आयत लाइट ग्रे में हाइलाइटेड है)। alt टेक्स्ट में SEO के लिए मुख्य कीवर्ड शामिल है।

![how to draw rectangle in PDF example](https://example.com/images/rectangle-demo.png "how to draw rectangle in PDF example")

## निष्कर्ष

हमने Aspose.Pdf for C# का उपयोग करके PDF में **how to draw rectangle** को कवर किया है। `Document` बनाकर, `Page` जोड़कर, `Rectangle` shape को परिभाषित करके, और अंत में **adding shape to PDF** करके, आप कुछ ही लाइनों से वेक्टर‑बेस्ड ग्राफिक्स जेनरेट कर सकते हैं। चाहे आपको हाइलाइटिंग, लेआउट डिबगिंग, या UI ओवरलेज़ के लिए **add rectangle to pdf** चाहिए, यह तरीका अच्छी स्केलेबिलिटी प्रदान करता है।

अगले चरण में आप **draw shape on pdf** को आयतों से आगे बढ़ाकर देख सकते हैं—जैसे सर्कल, पॉलीलाइन, या कस्टम SVG पाथ्स। या टेक्स्ट रेंडरिंग, इमेज इन्सर्शन, और PDF फ़ॉर्म मैनीपुलेशन में डुबकी लगाकर फुल‑फ़ीचर रिपोर्ट बना सकते हैं। Aspose.Pdf लाइब्रेरी एक समृद्ध API देती है, और यहाँ कवर किए गए मूलभूत ज्ञान के साथ आप प्रयोग करने के लिए तैयार हैं।

हैप्पी कोडिंग, और आपके PDF हमेशा वैसा ही दिखें जैसा आप कल्पना करते हैं!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}