---
category: general
date: 2026-10-10
description: Aspose.PDF का उपयोग करके PDF में आयत जोड़ना, PDF पर आकार बनाना, और संशोधित
  PDF को सहेजना सीखें। इसमें विशिष्ट PDF पृष्ठ तक पहुँचने के लिए चरण‑दर‑चरण मार्गदर्शिका
  शामिल है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: hi
lastmod: 2026-10-10
og_description: C# में Aspose.PDF का उपयोग करके PDF में आयत जोड़ें। यह ट्यूटोरियल
  दिखाता है कि PDF पर आकृति कैसे बनाएं, किसी विशिष्ट PDF पृष्ठ तक कैसे पहुंचें, और
  संशोधित PDF को कैसे सहेजें।
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Aspose.PDF के साथ PDF में आयत जोड़ें – पूर्ण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: C# में Aspose.PDF के साथ PDF में आयत कैसे जोड़ें
url: /hi/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF में Aspose.PDF के साथ C# में आयत कैसे जोड़ें

यदि आपको प्रोग्रामेटिक रूप से **PDF में आयत जोड़नी** है, तो यह गाइड आपको बिल्कुल बताता है कि कैसे करना है। आप सीखेंगे **PDF पर आकार (shape) बनाना**, किसी विशेष पृष्ठ को लक्षित करना, और **संशोधित PDF को सहेजना** बिना त्रुटियों के।

PDF दस्तावेज़ों के साथ काम करना रिपोर्टिंग, इनवॉइसिंग, या दस्तावेज़ एनोटेशन के लिए एक सामान्य आवश्यकता है। इस ट्यूटोरियल के अंत तक आप आत्मविश्वास से **PDF में आकार जोड़** सकते हैं, out‑of‑bounds त्रुटियों को संभाल सकते हैं, और समाधान को किसी भी .NET प्रोजेक्ट में एकीकृत कर सकते हैं।

## आवश्यकताएँ

* .NET 6.0 SDK या बाद का संस्करण स्थापित हो  
* Visual Studio 2022 (या कोई भी C# IDE)  
* Aspose.PDF for .NET लाइसेंस या एक मुफ्त इवैल्यूएशन की – API दोनों मोड में समान रूप से काम करता है  
* `input.pdf` नाम की एक PDF फ़ाइल जिसे आप अपने कोड से रेफ़रेंस कर सकें  

ये आइटम उदाहरण के लिए एकमात्र बाहरी निर्भरताएँ हैं।

## चरण 1: Aspose.PDF NuGet पैकेज स्थापित करें

Aspose.PDF लाइब्रेरी वह `Document`, `Rectangle`, और अन्य ड्रॉइंग क्लासेज़ प्रदान करती है जिसकी आपको आवश्यकता है।

```bash
dotnet add package Aspose.PDF
```

इस कमांड को चलाने से Aspose.PDF का नवीनतम स्थिर संस्करण आपके प्रोजेक्ट में जोड़ दिया जाता है, जिससे PDF क्लासेज़ कंपाइलेशन के लिए उपलब्ध हो जाती हैं।

## चरण 2: PDF दस्तावेज़ लोड करें

पहला कार्य स्रोत फ़ाइल को लोड करना है। यह एक इन‑मेमोरी प्रतिनिधित्व बनाता है जिसे आप संशोधित कर सकते हैं।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*यह क्यों महत्वपूर्ण है*: दस्तावेज़ को लोड करने से आपको उसके पेज़ कलेक्शन तक पहुँच मिलती है, जो बाद में **विशिष्ट PDF पृष्ठ तक पहुँचने** के लिए आवश्यक है।

## चरण 3: दूसरे पृष्ठ (शून्य‑आधारित सूचकांक) तक पहुँचें

PDF पृष्ठों को `0` से इंडेक्स किया जाता है। दूसरे पृष्ठ पर आयत रखने के लिए, इंडेक्स `1` पर पृष्ठ को प्राप्त करें।

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

यदि दस्तावेज़ में दो से कम पृष्ठ हैं, तो `ArgumentOutOfRangeException` फेंका जाएगा, जो उत्पादन कोड में गार्ड क्लॉज़ की आवश्यकता को संकेत करता है।

## चरण 4: आयत आकार बनाएं

`Rectangle` स्ट्रक्चर का उपयोग करके आयत की स्थिति और आकार निर्धारित करें, फिर इसे Aspose ड्रॉइंग ऑब्जेक्ट में रैप करें।

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*यह क्यों महत्वपूर्ण है*: `BorderInfo` और `FillColor` प्रॉपर्टीज़ आपको **PDF पर आकार (shape) बनाना** एक स्पष्ट आउटलाइन और वैकल्पिक फ़िल के साथ देती हैं, जिससे आयत पाठकों के लिए स्पष्ट रूप से दिखे।

## चरण 5: आयत को पृष्ठ के पैराग्राफ संग्रह में जोड़ें

Aspose.PDF ड्रॉइंग ऑब्जेक्ट्स को पैराग्राफ एलिमेंट्स के रूप में मानता है। आयत को पृष्ठ के `Paragraphs` कलेक्शन में जोड़ने से वह पृष्ठ पर रेंडर हो जाता है।

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

इस बिंदु पर मेमोरी में PDF दस्तावेज़ में नया आकार मौजूद है, लेकिन डिस्क पर फ़ाइल तब तक अपरिवर्तित रहती है जब तक आप इसे सहेज नहीं लेते।

## चरण 6: संशोधित PDF को सहेजें और out‑of‑bounds त्रुटियों को संभालें

`Save` को कॉल करने से अपडेटेड दस्तावेज़ एक नई फ़ाइल में लिखा जाता है। यदि आयत पृष्ठ के आयामों से बाहर निकलती है, तो Aspose `PdfException` फेंकेगा। इस अपवाद को पकड़ने से आप समस्या को साफ़ तौर पर रिपोर्ट कर सकते हैं।

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*यह क्यों महत्वपूर्ण है*: `try/catch` ब्लॉक सुनिश्चित करता है कि आपका एप्लिकेशन **संशोधित PDF को सुरक्षित रूप से सहेज** सके, और त्रुटि संदेश आपको आवश्यक होने पर आयत के निर्देशांक समायोजित करने में मदद करता है।

## पूर्ण कार्यशील उदाहरण

सभी चरणों को मिलाकर, यहाँ पूरा, तैयार‑चलाने‑योग्य प्रोग्राम है:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर यह प्रिंट करता है:

```
PDF saved successfully with rectangle added.
```

और `output.pdf` बनाता है जिसमें मूल सामग्री के साथ दूसरे पृष्ठ पर निर्दिष्ट निर्देशांक पर एक नीली आयत दिखाई देती है।

यदि आयत पृष्ठ से बड़ी होती, तो आप देखते:

```
Shape out of bounds: The shape exceeds page margins.
```

## सामान्य प्रश्न और किनारे के मामले

### यदि PDF में केवल एक पृष्ठ है तो क्या करें?

`pdfDocument.Pages[1]` तक पहुँचने का प्रयास करने पर `ArgumentOutOfRangeException` फेंका जाएगा। इंडेक्स करने से पहले `pdfDocument.Pages.Count` की जाँच करके इस स्थिति से बचें।

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### विभिन्न पृष्ठों पर कई आयतें कैसे जोड़ें?

प्रत्येक लक्ष्य पृष्ठ के लिए चरण 2‑4 दोहराएँ, आवश्यकतानुसार आयत के निर्देशांक समायोजित करें। आप इस लॉजिक को एक लूप में रख सकते हैं जो `pdfDocument.Pages` पर इटररेट करता है।

### क्या मैं वृत्त या बहुभुज जैसी अन्य आकृतियों का उपयोग कर सकता हूँ?

हाँ। Aspose.PDF `Ellipse`, `Polygon`, और `Polyline` क्लासेज़ प्रदान करता है जो `Rectangle` के समान पैटर्न का पालन करती हैं। `new Aspose.Pdf.Drawing.Rectangle` कॉल को इच्छित आकार क्लास से बदल दें।

### क्या लाइब्रेरी घुमाए गए पृष्ठों वाले PDFs का समर्थन करती है?

Aspose.PDF आकार रेंडर करते समय पृष्ठ घुमाव को स्वचालित रूप से सम्मानित करता है। आयत के निर्देशांक पृष्ठ के मूल कोऑर्डिनेट सिस्टम में व्याख्यायित होते हैं, इसलिए अतिरिक्त ट्रांसफ़ॉर्मेशन की आवश्यकता नहीं होती।

## प्रदर्शन संबंधी विचार

* **Memory usage** – बड़े PDF (सैकड़ों मेगाबाइट) को लोड करने से अनुपातिक मेमोरी खर्च होती है। यदि आपको केवल एक पृष्ठ संशोधित करना है, तो `PdfFileInfo` का उपयोग करके उस पृष्ठ को निकालें, संशोधित करें, और फिर उसे वापस मर्ज करें।  
* **Batch processing** – कई दस्तावेज़ों में आकार जोड़ते समय, एक ही `License` इंस्टेंस को पुन: उपयोग करें ताकि बार‑बार लाइसेंस वैधता ओवरहेड से बचा जा सके।

## अगले कदम

अब जब आप **PDF में आयत जोड़** सकते हैं, तो इन संबंधित विषयों का अन्वेषण करें:

* **draw shape on PDF** – टेक्स्ट, इमेज और वॉटरमार्क ओवरले करना सीखें  
* **add shape to PDF** – कई आकारों को एक ही एनोटेशन लेयर में संयोजित करें  
* **save modified PDF** – स्ट्रीम (`MemoryStream`) का उपयोग करके PDFs को सीधे वेब API से रिटर्न करें  
* **access specific PDF page** – कस्टम रिपोर्ट के लिए पेज‑रेंज एक्सट्रैक्शन लागू करें  

विभिन्न रंगों, लाइन स्टाइल्स और ट्रांसपैरेंसी लेवल के साथ प्रयोग करें ताकि आपके ब्रांडिंग गाइडलाइन के अनुरूप हो सके।

---

*हैप्पी कोडिंग! यदि इस ट्यूटोरियल ने आपको **PDF में आयत जोड़ने** में मदद की, तो इसे टीम के साथ साझा करने या समुदाय में सुधार योगदान करने पर विचार करें।*

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [C# में Aspose.PDF के साथ PDF में आकार जोड़ने की चरण‑दर‑चरण गाइड](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Aspose.PDF for .NET का उपयोग करके PDF में लाइन ऑब्जेक्ट कैसे जोड़ें: चरण‑दर‑चरण गाइड](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [C# में PDF कैसे बनाएं – पृष्ठ जोड़ें, आयत बनाएं और सहेजें](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}