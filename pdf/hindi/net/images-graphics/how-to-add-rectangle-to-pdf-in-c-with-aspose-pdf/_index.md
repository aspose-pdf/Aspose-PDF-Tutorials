---
category: general
date: 2026-09-27
description: C# में PDF में आयत जोड़ना सीखें, जब आप PDF दस्तावेज़ लोड करते हैं और
  Aspose.Pdf के साथ PDF के पहले पृष्ठ तक पहुँचते हैं।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- access first page pdf
- load pdf document c#
- add graphics pdf c#
language: hi
lastmod: 2026-09-27
og_description: C# में PDF दस्तावेज़ लोड करके और पहले पृष्ठ तक पहुंचकर PDF में आयत
  जोड़ें। विश्वसनीय परिणामों के लिए इस चरण‑दर‑चरण ट्यूटोरियल का पालन करें।
og_image_alt: Code editor showing how to add rectangle to PDF using C#
og_title: C# में PDF में आयत जोड़ें – पूर्ण Aspose.Pdf गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to add rectangle to PDF in C# while you load PDF document
    C# and access first page PDF with Aspose.Pdf.
  headline: How to add rectangle to PDF in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C# में Aspose.Pdf के साथ PDF में आयत कैसे जोड़ें
url: /hi/net/images-graphics/how-to-add-rectangle-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose.Pdf के साथ PDF में आयत कैसे जोड़ें

यदि आपको C# एप्लिकेशन में **PDF में आयत जोड़नी** है, तो यह गाइड सटीक चरण दिखाता है। आप एक PDF दस्तावेज़ लोड करेंगे, पहले पृष्ठ तक पहुँचेंगे, एक आयत आकार बनाएँगे, और परिवर्तन को डिस्क पर लिखेंगे। यह समाधान Aspose.Pdf .NET 2024‑R2 के साथ काम करता है और किसी बाहरी टूल की आवश्यकता नहीं है।

PDF फ़ाइलों में आयत जोड़ना अक्सर सेक्शन को हाइलाइट करने, फ़ॉर्म‑जैसे ओवरले बनाने, या सरल ग्राफ़िक्स बनाने के लिए आवश्यक होता है। नीचे दिया गया कोड एक पुन: उपयोग योग्य पैटर्न प्रदान करता है जिसे आप अन्य आकार, रंग या अपारदर्शिता सेटिंग्स के साथ विस्तारित कर सकते हैं।

## आप क्या सीखेंगे

* Aspose.Pdf का उपयोग करके **C# में PDF दस्तावेज़ लोड करना**।
* सुरक्षित रूप से **PDF का पहला पृष्ठ एक्सेस करना**।
* एक आयत बनाना और **PDF में आयत जोड़ना**।
* कैसे सत्यापित करें कि आयत पृष्ठ की सीमाओं के भीतर फिट होती है।
* मौजूदा सामग्री खोए बिना अपडेटेड फ़ाइल को कैसे सहेजें।

यह ट्यूटोरियल मानता है कि आपके पास एक बुनियादी C# विकास वातावरण (Visual Studio 2022 या बाद का) और एक वैध Aspose.Pdf लाइसेंस है। `Aspose.Pdf` के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है।

## चरण 1: C# में PDF दस्तावेज़ लोड करें  

स्रोत फ़ाइल को लोड करना पहला कार्य है। Aspose.Pdf पूरे PDF को मेमोरी में पढ़ता है, जिससे आप पृष्ठों, एनोटेशन और ग्राफ़िक्स को बदल सकते हैं।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // for Color

// Load the PDF document
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

*इस चरण का महत्व* – `Document` ऑब्जेक्ट पूरे PDF का प्रतिनिधित्व करता है। यदि फ़ाइल नहीं खुल पाती है, तो एक अपवाद फेंका जाता है, इसलिए प्रोडक्शन कोड में कंस्ट्रक्टर को कॉल करने से पहले पथ की जाँच करनी चाहिए।

## चरण 2: PDF का पहला पृष्ठ एक्सेस करें  

Aspose.Pdf में पृष्ठ 1‑आधारित होते हैं, इसलिए पहला पृष्ठ इंडेक्स 1 से प्राप्त किया जाता है। यह चरण ठीक‑ठीक वाक्यांश **access first page PDF** को दर्शाता है।

```csharp
// Access the first page (pages are 1‑based)
Page page = doc.Pages[1];
```

*इस चरण का महत्व* – सही पृष्ठ को बदलने से बाद के पृष्ठों पर अनजाने में संपादन से बचा जा सकता है। यदि PDF में कोई पृष्ठ नहीं है, तो `doc.Pages[1]` `ArgumentOutOfRangeException` उठाता है, जिसे आप एक मित्रवत त्रुटि संदेश देने के लिए पकड़ सकते हैं।

## चरण 3: आयत आकार बनाएं  

अब आप उस आयत की ज्यामिति परिभाषित करते हैं जिसे आप जोड़ना चाहते हैं। कंस्ट्रक्टर पैरामीटर `(x, y, width, height)` होते हैं जहाँ मूल बिंदु `(0,0)` पृष्ठ के निचले‑बाएँ कोने को दर्शाता है।

```csharp
// Define a rectangle shape (x, y, width, height)
Rectangle rect = new Rectangle(10, 10, 200, 200);

// Optional: customize the appearance
rect.GraphInfo = new GraphInfo
{
    Color = Color.Black,   // stroke color
    LineWidth = 2          // thickness in points
};
```

*इस चरण का महत्व* – `GraphInfo` सेट करने से आयत के रेंडरिंग को नियंत्रित किया जाता है। बिना इसे सेट किए, डिफ़ॉल्ट स्ट्रोक पारदर्शी होने के कारण आकार अदृश्य रहेगा।

## चरण 4: सत्यापित करें कि आयत पृष्ठ की सीमाओं के भीतर फिट होती है  

आकार जोड़ने से पहले आपको यह सुनिश्चित करना चाहिए कि वह पृष्ठ के आकार से अधिक न हो। यह रेंडरिंग आर्टिफैक्ट्स को रोकता है और PDF स्पेसिफिकेशन के अनुरूप रखता है।

```csharp
// Verify the rectangle fits within the page boundaries
if (page.Rect.Contains(rect))
{
    // Step 5 will run here
}
else
{
    // Adjust rectangle or log a warning
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*इस चरण का महत्व* – `Contains` जाँच यह गारंटी देती है कि आयत पूरी तरह से प्रिंटेबल एरिया के अंदर है। यदि आप इस चरण को छोड़ देते हैं और आयत बाहर निकलती है, तो कुछ व्यूअर आकार को क्लिप कर सकते हैं या त्रुटि रिपोर्ट कर सकते हैं।

## चरण 5: PDF में आयत जोड़ें  

जब बाउंड्स जाँच सफल हो जाती है, तो आप आयत को पृष्ठ में जोड़ते हैं। यह वह मुख्य कार्य है जो **add rectangle to PDF** आवश्यकता को पूरा करता है।

```csharp
// Add the rectangle to the page
page.Add(rect);
```

*इस चरण का महत्व* – `page.Add` आकार को पृष्ठ की कंटेंट स्ट्रीम में डालता है। आयत दृश्य लेयर का हिस्सा बन जाता है और किसी भी PDF व्यूअर में दिखाई देगा।

## चरण 6: अपडेटेड PDF सहेजें  

अंत में, संशोधित दस्तावेज़ को डिस्क पर वापस लिखें। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई फ़ाइल बना सकते हैं।

```csharp
// Save the updated PDF
doc.Save("YOUR_DIRECTORY/output.pdf");
```

*इस चरण का महत्व* – सहेजने से सभी परिवर्तन अंतिम रूप ले लेते हैं। यदि आपको मूल को संरक्षित रखना है, तो नीचे दिखाए अनुसार अलग आउटपुट पाथ चुनें।

## पूर्ण, चलाने योग्य उदाहरण

नीचे एक स्व-निहित कंसोल प्रोग्राम है जो प्रत्येक चरण को सम्मिलित करता है। कोड को नए C# प्रोजेक्ट में कॉपी करें, फ़ाइल पाथ समायोजित करें, और चलाएँ।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;

class AddRectangleExample
{
    static void Main()
    {
        // Load the PDF document (load pdf document c#)
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // Access first page PDF
        Page page = doc.Pages[1];

        // Create a rectangle shape
        Rectangle rect = new Rectangle(10, 10, 200, 200);
        rect.GraphInfo = new GraphInfo
        {
            Color = Color.Black,
            LineWidth = 2
        };

        // Verify bounds before adding
        if (page.Rect.Contains(rect))
        {
            // Add rectangle to PDF
            page.Add(rect);
        }
        else
        {
            System.Console.WriteLine("Rectangle does not fit on the page.");
            return;
        }

        // Save the result
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Rectangle added successfully.");
    }
}
```

**अपेक्षित आउटपुट** – निष्पादन के बाद, `output.pdf` में मूल सामग्री के साथ एक काली‑बॉर्डर वाली आयत होगी जो निचले‑बाएँ कोने से 10 pt की दूरी पर स्थित है। Adobe Acrobat या किसी भी PDF व्यूअर में फ़ाइल खोलने पर पहले पृष्ठ पर आयत ओवरले दिखेगा।

## सामान्य विविधताओं को संभालना

| स्थिति | सिफारिश किया गया परिवर्तन |
|-----------|--------------------|
| पृष्ठ आकार अलग है (जैसे, A4 बनाम Letter) | डायनामिक रूप से फिट होने वाली आयत की गणना के लिए `page.Rect.Width` और `page.Rect.Height` का उपयोग करें। |
| आपको भराव वाली आयत चाहिए | `rect.GraphInfo.FillColor = Color.LightGray;` सेट करें और वैकल्पिक रूप से `rect.GraphInfo.IsFilled = true;`। |
| कई पृष्ठों को समान आयत चाहिए | `doc.Pages` पर लूप करें और प्रत्येक पृष्ठ के लिए जोड़ने का कार्य दोहराएँ। |
| पारदर्शिता आवश्यक है | `rect.GraphInfo.Transparency = 0.5;` सेट करें (रेंज 0–1)। |

ये विविधताएँ दर्शाती हैं कि **add graphics pdf c#** दृष्टिकोण एकल आकार से परे कैसे स्केल करता है।

## प्रो टिप्स

* **प्रदर्शन टिप** – बड़े PDF प्रोसेस करते समय, एक ही `Document` इंस्टेंस को पुन: उपयोग करें और लूप के अंदर `Save` कॉल करने से बचें। सभी पृष्ठों को प्रोसेस करने के बाद एक बार सहेजें।
* **त्रुटि संभालना** – पूरी प्रक्रिया को `try/catch` ब्लॉक में रैप करें ताकि `FileNotFoundException`, `InvalidOperationException`, और Aspose‑विशिष्ट `PdfException` को पकड़ सकें।
* **लाइसेंस** – मूल्यांकन वॉटरमार्क से बचने के लिए `Document` बनाने से पहले अपना Aspose.Pdf लाइसेंस रजिस्टर करें।

## निष्कर्ष

अब आप जानते हैं कि C# में **PDF में आयत कैसे जोड़ें** लोड करके a

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [C# में PDF दस्तावेज़ बनाएं – PDF में पृष्ठ जोड़ें और आयत](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/)
- [C# में PDF दस्तावेज़ बनाएं – खाली पृष्ठ जोड़ें और आयत बनाएं](/pdf/english/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/)
- [C# में PDF दस्तावेज़ बनाएं – पृष्ठ जोड़ें, आयत बनाएं और सहेजें](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}