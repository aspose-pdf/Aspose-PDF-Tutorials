---
category: general
date: 2026-08-14
description: C# का उपयोग करके PDF पर जल्दी से आयत बनाएं। केवल कुछ पंक्तियों में आयत
  के आयाम निर्धारित करना और PDF पृष्ठ में आकार जोड़ना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: hi
lastmod: 2026-08-14
og_description: C# के साथ सेकंडों में PDF पर आयत बनाएं। यह गाइड दिखाता है कि आयत के
  आयाम कैसे निर्धारित करें, एक आकार जोड़ें, और विश्वसनीय PDF ग्राफिक्स के लिए पृष्ठ
  सीमाओं की पुष्टि करें।
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: PDF पर आयत बनाएं – पूर्ण C# ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: PDF पर आयत बनाएं – चरण‑दर‑चरण C# गाइड
url: /hi/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF पर आयत बनाएं – पूर्ण C# ट्यूटोरियल

यदि आपको C# का उपयोग करके **PDF पर आयत बनानी** है, तो यह गाइड आपको एक संक्षिप्त, प्रोडक्शन‑रेडी समाधान दिखाता है। आप बिल्कुल **आयत के आयाम कैसे निर्धारित करें** देखेंगे, यह सत्यापित करेंगे कि आकार पेज में फिट बैठता है, और एक ही मेथड कॉल से इसे पेज में जोड़ेंगे।

यह ट्यूटोरियल PDF दस्तावेज़ बनाने से लेकर आयत को रेंडर करने तक सब कुछ कवर करता है, ताकि आप कोड को अपने प्रोजेक्ट में कॉपी‑पेस्ट करके तुरंत परिणाम देख सकें। कोई बाहरी दस्तावेज़ीकरण आवश्यक नहीं—नीचे दिए गए चरणों का पालन करें।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ पर भी काम करता है)
* **Aspose.PDF for .NET** NuGet पैकेज (`Install-Package Aspose.PDF`)
* C# सिंटैक्स की बुनियादी समझ
* Visual Studio या VS Code जैसा IDE

> **Pro tip:** तेज़ प्रयोगों के लिए Aspose.PDF का फ्री इवैल्यूएशन लाइसेंस उपयोग करें; यह एक छोटा वॉटरमार्क जोड़ता है लेकिन सभी फीचर टेस्ट करने देता है।

## C# के साथ PDF पर आयत कैसे बनाएं

कार्य का मूल भाग `RectangleShape` बनाना, उसका आकार और स्ट्रोक सेट करना, और उसे `Page` से जोड़ना है। नीचे दिया गया H2 हेडर मुख्य कीवर्ड रखता है, जिससे SEO आवश्यकताएँ पूरी होती हैं।

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### प्रत्येक चरण की व्याख्या

| चरण | क्यों महत्वपूर्ण है |
|------|-------------------|
| **1️⃣ नया PDF दस्तावेज़ बनाएं** | वह कंटेनर इनिशियलाइज़ करता है जो पेज और ग्राफ़िक्स रखेगा। |
| **2️⃣ एक खाली पेज जोड़ें** | आपको `Page` ऑब्जेक्ट चाहिए क्योंकि शैप्स पेज से जुड़ते हैं, सीधे दस्तावेज़ से नहीं। |
| **3️⃣ आयत की सीमाएँ निर्धारित करें** | यहाँ **आयत के आयाम कैसे निर्धारित करें** दिखाया गया है। `Rectangle` कंस्ट्रक्टर `x`, `y`, `width`, और `height` को पॉइंट्स में लेता है (1 pt = 1/72 in)। |
| **4️⃣ आयत शैप बनाएं** | `RectangleShape` Aspose क्लास है जो आयत रेंडर करती है। `StrokeColor` सेट करने से आउटलाइन बनती है; आप `FillColor` सेट करके भराव भी कर सकते हैं। |
| **5️⃣ पेज सीमाओं की जाँच करें** | `CheckShapeBoundary` अपवाद फेंकता है यदि आयत पेज आकार से बाहर हो, जिससे खराब PDF बनना रोका जाता है। |
| **6️⃣ शैप को पेज में जोड़ें** | शैप पेज की कंटेंट स्ट्रीम का हिस्सा बन जाता है। |
| **7️⃣ PDF सहेजें** | दस्तावेज़ को ऐसी फ़ाइल में लिखता है जिसे आप किसी भी PDF व्यूअर से खोल सकते हैं। |

परिणामी `RectangleDemo.pdf` में एक काली आयत पेज के ऊपर‑बाएँ कोने में स्थित होगी, जिसकी चौड़ाई 500 pt और ऊँचाई 700 pt है।

![draw rectangle on pdf example](https://example.com/rectangle-demo.png "draw rectangle on pdf example")

*Image alt text: draw rectangle on pdf example showing a black rectangle in the upper left corner of a PDF page.*

## विभिन्न पेज आकारों के लिए आयत के आयाम कैसे निर्धारित करें

ऊपर दिया गया स्निपेट स्थिर मान (`500 x 700`) उपयोग करता है। वास्तविक अनुप्रयोगों में अक्सर आयत को पेज की चौड़ाई और ऊँचाई के अनुसार अनुकूलित करना पड़ता है।

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**मुख्य बिंदु:**

* वास्तविक पेज आकार पढ़ने के लिए `page.PageInfo.Width` और `Height` का उपयोग करें।
* किसी फ़ैक्टर (जैसे `0.8f`) से गुणा करने से आयाम पेज का प्रतिशत बन जाता है।
* केंद्रित करने के लिए आयत के आकार को पेज आकार से घटाएँ और शेष को आधा करें।

## सामान्य समस्याएँ और उनका समाधान

| समस्या | क्यों होता है | समाधान |
|---------|--------------|--------|
| आयत पेज से बाहर निकलती है | हार्ड‑कोडेड आयाम पेज आकार से बड़े होते हैं। | शैप जोड़ने **से पहले** `page.CheckShapeBoundary` कॉल करें; यदि अपवाद आए तो आयाम समायोजित करें। |
| स्ट्रोक दिखाई नहीं देता | `StrokeColor` डिफ़ॉल्ट (`Color.Empty`) पर रहता है। | स्पष्ट रूप से `StrokeColor` सेट करें (उदा., `Color.Black`)। |
| आयत स्क्रीन से बाहर दिखती है | PDF स्पेस में निर्देशांक नीचे‑बाएँ से शुरू होते हैं; स्क्रीन‑स्टाइल ऊपर‑बाएँ निर्देशांक उपयोग करने से उलटाव होता है। | याद रखें कि मूल बिंदु `(0,0)` नीचे‑बाएँ कोना है। `y` को उसी अनुसार समायोजित करें या `pageHeight - desiredY` उपयोग करें। |
| लाइन की मोटाई अनपेक्षित | डिफ़ॉल्ट लाइन चौड़ाई प्रिंटिंग के लिए बहुत पतली हो सकती है। | `rectangleShape.LineWidth = 2;` सेट करके मोटाई बढ़ाएँ। |

## उदाहरण का विस्तार

एक बार जब आप **PDF पर आयत बना** सकते हैं, तो आप आसानी से अन्य शैप्स भी जोड़ सकते हैं:

* **EllipseShape** – वृत्त या अंडाकार के लिए।
* **PolygonShape** – कस्टम बहुभुजों के लिए।
* **TextFragment** – अपनी आयतों को लेबल करने के लिए।

सभी शैप्स का वर्कफ़्लो समान है: सीमाएँ निर्धारित करें, दिखावट कॉन्फ़िगर करें, सीमाओं की जाँच करें, फिर पेज में जोड़ें।

## पूर्ण, चलाने योग्य प्रोग्राम

नीचे पूरा प्रोग्राम दिया गया है जो बेसिक आयत और डायनामिक साइजिंग उदाहरण को मिलाता है। इसे नए कंसोल प्रोजेक्ट में कॉपी करें, `Aspose.PDF` NuGet पैकेज रिस्टोर करें, और चलाएँ।

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**अपेक्षित आउटपुट:**  
`CombinedRectangles.pdf` खोलें। आपको नीचे‑बाएँ कोने में एक काली आयत और केंद्रित डार्क‑ब्लू आयत लाइट‑येलो फ़िल के साथ दिखेगी। दोनों आयतें पेज मार्जिन का सम्मान करती हैं।

## निष्कर्ष

अब आप जानते हैं कि C# के साथ **PDF पर आयत कैसे बनाएं** और दोनों स्थिर तथा रिस्पॉन्सिव लेआउट के लिए **आयत के आयाम कैसे निर्धारित करें**। यह तरीका Aspose.PDF के `RectangleShape`, बाउंडरी चेकिंग, और सरल गणित का उपयोग करके किसी भी पेज आकार के अनुसार अनुकूलित करता है।

आगे आप खोज सकते हैं:

* **फ़िल रंग** और **लाइन स्टाइल** (डैश्ड, डॉटेड) जोड़ना – द्वितीयक कीवर्ड: how to define rectangle dimensions with style.
* कई शैप्स को एक ही `Page` में मिलाकर चार्ट या फॉर्म बनाना।
* PDF को स्ट्रीम में एक्सपोर्ट करना ताकि वेब API में डिस्क पर सहेजे बिना उपयोग किया जा सके।

विभिन्न आकार, रंग, और स्थितियों के साथ प्रयोग करें और अपने .NET एप्लिकेशन में PDF ग्राफ़िक्स में महारत हासिल करें। Happy coding!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर मास्टर कर सकें और अपने प्रोजेक्ट में वैकल्पिक इम्प्लीमेंटेशन एप्रोच खोज सकें।

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}