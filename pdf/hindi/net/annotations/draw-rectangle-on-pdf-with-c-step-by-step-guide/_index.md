---
category: general
date: 2026-06-21
description: C# का उपयोग करके PDF पर आयत बनाएं। जानें कि PDF दस्तावेज़ को कैसे लोड
  करें, काली आयत एनोटेशन बनाएं, और संशोधित PDF को कुशलतापूर्वक सहेजें।
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: hi
og_description: 'C# में PDF पर आयत बनाएं: PDF दस्तावेज़ लोड करके, काली आयत एनोटेशन
  बनाकर, और संशोधित PDF को सहेजें। पूर्ण कोड शामिल है।'
og_title: C# के साथ PDF पर आयत बनाएं – पूर्ण प्रोग्रामिंग ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: C# के साथ PDF पर आयत बनाएं – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Draw Rectangle on PDF with C# – Complete Programming Tutorial

क्या आपको कभी **PDF पर आयत (rectangle) बनानी** पड़ी है लेकिन नहीं पता था कहाँ से शुरू करें? आप अकेले नहीं हैं। चाहे वह किसी सेक्शन को हाइलाइट करना हो, संवेदनशील डेटा को ब्लैक‑आउट करना हो, या बस एक विज़ुअल संकेत जोड़ना हो, प्रोग्रामेटिकली *PDF पर आयत बनाना* सीखना मैन्युअल एडिटिंग में घंटों बचा सकता है।

इस गाइड में हम एक व्यावहारिक उदाहरण देखेंगे जिसमें **PDF दस्तावेज़ लोड** किया जाता है, **एक काली आयत बनाई** जाती है, और फिर **संशोधित PDF को सेव** किया जाता है। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी C# प्रोजेक्ट में डाल सकते हैं—कोई रहस्य नहीं, सिर्फ स्पष्ट कोड और व्याख्याएँ।

## What This Tutorial Covers

- **Aspose.PDF for .NET** लाइब्रेरी का उपयोग करके **pdf दस्तावेज़ लोड** करना  
- आयत के कोऑर्डिनेट्स निर्धारित करना और सुनिश्चित करना कि वह पेज की सीमा के भीतर रहे  
- **add black rectangle** मेथड से पेज पर एनोटेशन जोड़ना  
- **save modified pdf** को नई फ़ाइल लोकेशन पर सहेजना  
- एज‑केस हैंडलिंग (एकाधिक पृष्ठ, आउट‑ऑफ़‑बाउंड्स आयत, कस्टम रंग)  

कोई बाहरी टूल नहीं, कोई अस्पष्ट रेफ़रेंस नहीं—बस एक पूर्ण, चलाने योग्य उदाहरण जिसे आप कॉपी‑पेस्ट कर सकते हैं।

---

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हैं:

1. .NET 6.0 SDK (या कोई भी हालिया .NET संस्करण) स्थापित हो  
2. **Aspose.PDF for .NET** का रेफ़रेंस (NuGet से उपलब्ध: `Install-Package Aspose.PDF`)  
3. एक मौजूदा PDF फ़ाइल (`input.pdf`) जो आप पढ़/लिख सकते हैं  

बस इतना ही। अगर आप बुनियादी C# सिंटैक्स से परिचित हैं, तो आप तैयार हैं।

---

## Step 1: Load PDF Document

सबसे पहले हमें **load pdf document** कॉल चाहिए। Aspose.PDF की `Document` क्लास फ़ाइल पाथ लेती है और पूरी फ़ाइल को मेमोरी में पढ़ लेती है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*क्यों महत्वपूर्ण है*: PDF को लोड करने से आपको उसके पेज, मेटाडेटा और ड्रॉइंग सतह तक पहुंच मिलती है। इस चरण के बिना आप कोई भी आकार नहीं रख सकते।

---

## Step 2: Pick the Target Page

Aspose में PDF पेज 1‑आधारित होते हैं, इसलिए पहला पेज इंडेक्स 1 है। वह पेज चुनें जिसे आप एनोटेट करना चाहते हैं—आमतौर पर डेमो के लिए पहला पेज।

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

अगर आपको किसी अलग पेज पर काम करना है, तो बस इंडेक्स बदल दें। सुनिश्चित करें कि वह इंडेक्स मौजूद है, ताकि `ArgumentOutOfRangeException` न आए।

---

## Step 3: Define the Rectangle Geometry

एक आयत को उसके लोअर‑लेफ़्ट (X,Y) और अपर‑राइट (X,Y) कोऑर्डिनेट्स से परिभाषित किया जाता है। `Rectangle` स्ट्रक्ट इनको `LLX`, `LLY`, `URX`, `URY` के रूप में स्टोर करता है।

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

इन संख्याओं को अपनी ज़रूरत के अनुसार बदलें—`100,100` लोअर‑लेफ़्ट कोरिडिनेट को बाएँ और नीचे की किनारों से 100 पॉइंट्स पर रखता है, जबकि `300,300` अपर‑राइट को किनारों से 300 पॉइंट्स पर सेट करता है।

---

## Step 4: Verify the Rectangle Fits Inside the Page

पेज की सीमा के बाहर ड्रॉ करने की कोशिश या तो अनदेखी हो जाएगी या लाइब्रेरी संस्करण के आधार पर एक्सेप्शन फेंकेगी। एक त्वरित चेक आपके कोड को मजबूत बनाता है।

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Pro tip*: अगर आप विभिन्न आकार के PDF को सपोर्ट करना चाहते हैं, तो आयत को पेज की चौड़ाई/ऊँचाई के प्रतिशत के आधार पर गणना करें, न कि निरपेक्ष पॉइंट्स पर।

---

## Step 5: Add Black Rectangle Annotation

अब मज़ेदार हिस्सा—**add black rectangle** को पेज पर जोड़ना। Aspose `AddRectangle` प्रदान करता है जो जियोमेट्री और एक `Color` लेता है। हम `Color.Black` का उपयोग करके **create black rectangle** बनाएँगे।

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

यह एक ही लाइन भारी काम कर देती है: यह एक एनोटेशन ऑब्जेक्ट बनाती है, उसकी बॉर्डर रंग को काला सेट करती है, और उसे पेज की एनोटेशन कलेक्शन में डाल देती है।

अगर आपको कोई अलग फ़िल या बॉर्डर स्टाइल चाहिए, तो `Annotation` ऑब्जेक्ट को स्वीकार करने वाले ओवरलोड को देखें जहाँ आप लाइन विड्थ, डैश पैटर्न, या यहाँ तक कि अपासिटी भी बदल सकते हैं।

---

## Step 6: Save Modified PDF

अंत में **save modified pdf** के साथ बदलावों को स्थायी बनाएँ। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई फ़ाइल में लिख सकते हैं—यहाँ हम एक आउटपुट फ़ाइल बनाएँगे।

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

यही पूरा वर्कफ़्लो है। प्रोग्राम चलाएँ और `output.pdf` खोलें; आपको वही काली आयत दिखेगी जो आपने परिभाषित की थी।

---

## Full Working Example

नीचे एक स्व-समाहित कंसोल एप्लिकेशन है जो सभी चरणों को एक साथ जोड़ता है। इसे नई `.csproj` में कॉपी करें और **Run** दबाएँ।

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**Expected output** in the console:

```
Successfully drew rectangle on PDF and saved the file.
```

`output.pdf` खोलें और आप देखेंगे कि काली आयत आपके निर्दिष्ट कोऑर्डिनेट्स पर स्थित है।

---

## Handling Common Variations

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Multiple pages** | `pdfDocument.Pages` पर लूप चलाएँ और प्रत्येक `Page` ऑब्जेक्ट पर वही लॉजिक लागू करें। | पूरे दस्तावेज़ में बैच एनोटेशन की अनुमति देता है। |
| **Different colors** | `Color.Black` को `Color.Red` या किसी भी `System.Drawing.Color` से बदलें। | हाइलाइट करने के लिए काली के बजाय रंगीन उपयोगी रहता है। |
| **Transparent fill** | `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }` का उपयोग करें। | ठोस ब्लॉक की बजाय अर्ध‑पारदर्शी ओवरले देता है। |
| **Dynamic rectangle size** | `URX` और `URY` को `PageInfo.Width * 0.5` आदि के आधार पर गणना करें। | आयत विभिन्न पेज आकारों के अनुसार अनुकूल बनती है। |
| **Error handling** | पूरे ब्लॉक को `try…catch` में रखें और `Aspose.Pdf.IOException` को लॉग करें। | स्रोत फ़ाइल गायब या लॉक होने पर क्रैश से बचाता है। |

इन बदलावों से आप **create black rectangle** एनोटेशन को कई संदर्भों में बिना कोर लॉजिक बदले उपयोग कर सकते हैं।

---

## Pro Tips & Pitfalls

- **Document को Dispose करें**: यद्यपि Aspose.PDF `IDisposable` को इम्प्लीमेंट करता है, `using` पैटर्न छोटे‑समय वाले कंसोल ऐप्स के लिए अनिवार्य नहीं है। लेकिन लंबे‑समय वाले सर्विसेज़ में `Document` को `using` ब्लॉक में रैप करना नेटीव रिसोर्सेज़ को तुरंत मुक्त करने में मदद करता है।  
- **Coordinate System**: PDF कोऑर्डिनेट्स लोअर‑लेफ़्ट कोर्नर से शुरू होते हैं। अगर आप WinForms जैसी टॉप‑लेफ़्ट ओरिजिन के आदी हैं, तो Y‑अक्ष को उलटना पड़ेगा: `pageHeight - y`।  
- **Performance**: बहुत बड़े PDF में एनोटेशन जोड़ना मेमोरी‑इंटेन्सिव हो सकता है। पेज को चंक्स में प्रोसेस करने या हल्के एडिट्स के लिए `PdfFileEditor` का उपयोग करने पर विचार करें।  
- **Legal**: स्रोत PDF को संशोधित करने के अधिकार सुनिश्चित करें—कुछ दस्तावेज़ संपादन से संरक्षित होते हैं।

---

## Conclusion

हमने दिखाया कि कैसे **draw rectangle on PDF** को C# के साथ किया जाता है—**load pdf document** से शुरू करके जियोमेट्री परिभाषित करना, **add black rectangle**, और अंत में **save modified pdf**। उदाहरण पूर्ण, चलाने योग्य, और वास्तविक‑दुनिया के परिदृश्यों जैसे बैच प्रोसेसिंग या कस्टम स्टाइलिंग के लिए अनुकूल है।

आगे आप अन्य एनोटेशन प्रकार (टेक्स्ट, हाईलाइट) जोड़ने या एनोटेशन के बाद कई PDF को मर्ज करने का अन्वेषण कर सकते हैं। **load pdf document** और **save modified pdf** चरण वही रहते हैं, इसलिए आप इस पैटर्न को आत्मविश्वास के साथ विस्तारित कर सकते हैं।

क्या आपने कोई ट्विस्ट आज़माया? कमेंट में शेयर करें, और कोडिंग का आनंद लें!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स को मास्टर कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [जावा का उपयोग करके PDF में भरी हुई आयत ऑब्जेक्ट बनाएं](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [जावा का उपयोग करके PDF में भरी हुई आयत ऑब्जेक्ट बनाएं](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [जावा का उपयोग करके PDF में भरी हुई आयत ऑब्जेक्ट बनाएं](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}