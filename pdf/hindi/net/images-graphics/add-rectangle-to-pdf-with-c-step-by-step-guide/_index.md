---
category: general
date: 2026-08-04
description: C# का उपयोग करके PDF में आयत जोड़ें। Aspose.Pdf के साथ PDF में आकृति
  कैसे बनाएं, यह स्पष्ट और पूर्ण उदाहरण में सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: hi
lastmod: 2026-08-04
og_description: C# का उपयोग करके PDF में आयत जोड़ें। यह ट्यूटोरियल दिखाता है कि कैसे
  PDF में C# से आकार को तेज़ और भरोसेमंद तरीके से बनाया जाए।
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: C# के साथ PDF में आयत जोड़ें – पूर्ण प्रोग्रामिंग गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C# के साथ PDF में आयत जोड़ें – चरण-दर-चरण मार्गदर्शिका
url: /hi/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ PDF में आयत जोड़ें – चरण‑दर‑चरण गाइड

यदि आपको C# एप्लिकेशन से **PDF में आयत जोड़नी** है, तो यह गाइड आपको बिल्कुल वही दिखाएगा जो करना है। आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जो Aspose.Pdf लाइब्रेरी का उपयोग करके PDF C# में एक आकार बनाता है, और आप समझेंगे कि कोड की प्रत्येक पंक्ति क्यों महत्वपूर्ण है।

PDF में आकार बनाना रिपोर्ट जेनरेटर, इनवॉइस टेम्पलेट और कस्टम दस्तावेज़ ब्रांडिंग के लिए आम आवश्यकता है। इस ट्यूटोरियल के अंत तक आप किसी भी आयताकार एनोटेशन को सम्मिलित कर सकते हैं, उसका आकार, रंग या स्थिति बदल सकते हैं, और मौजूदा सामग्री को खोए बिना संशोधित दस्तावेज़ को सहेज सकते हैं।

**आप क्या सीखेंगे**

* Aspose.Pdf के साथ मौजूदा PDF कैसे लोड करें।
* आयत की सीमाएँ निर्धारित करें और आयत आकार बनाएं।
* आयत को पृष्ठ के पैराग्राफ संग्रह में कैसे जोड़ें।
* अपडेटेड PDF को कैसे सहेजें और परिणाम की पुष्टि करें।
* कई पृष्ठों, पारदर्शिता और कस्टम लाइन स्टाइल्स के लिए विविधताएँ।

**पूर्वापेक्षाएँ**

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)।
* Visual Studio 2022 या कोई भी C# IDE।
* `Aspose.Pdf` का NuGet रेफ़रेंस (फ़्री ट्रायल या लाइसेंस्ड संस्करण)।
* `input.pdf` नामक इनपुट PDF फ़ाइल जिसे आप नियंत्रित फ़ोल्डर में रखें।

---

## PDF C# में आकार कैसे बनाएं – प्रोजेक्ट सेटअप

1. **एक नया कंसोल प्रोजेक्ट बनाएं**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Aspose.Pdf पैकेज जोड़ें**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **`input.pdf`** को प्रोजेक्ट डायरेक्टरी (या किसी भी फ़ोल्डर) में रखें जिसे आप बाद में रेफ़र करेंगे।

अब प्रोजेक्ट तैयार है कोड को कंपाइल करने के लिए जो **PDF में आयत जोड़ता** है।

---

## चरण 1: PDF दस्तावेज़ लोड करें

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*`Document` क्लास फ़ाइल को पार्स करता है और एक `Pages` कलेक्शन प्रदान करता है। ड्रॉइंग शुरू करने से पहले लोड करना पहला आवश्यक ऑपरेशन है।*

---

## चरण 2: लक्ष्य पृष्ठ चुनें

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*यदि आपको आयत किसी अन्य पृष्ठ पर जोड़नी है, तो इंडेक्स को इच्छित पृष्ठ संख्या से बदलें। लाइब्रेरी तब अपवाद फेंकती है जब इंडेक्स रेंज से बाहर हो, इसलिए सुनिश्चित करें कि PDF में पर्याप्त पृष्ठ हों।*

---

## चरण 3: आयत की सीमाएँ निर्धारित करें

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*कोऑर्डिनेट सिस्टम पॉइंट्स (1 pt = 1/72 इंच) का उपयोग करता है। यह उदाहरण पृष्ठ के शीर्ष के पास 250 pt चौड़ी और 100 pt ऊँची आयत बनाता है। अपने लेआउट के अनुसार संख्याएँ समायोजित करें।*

---

## चरण 4: आयत आकार बनाएं

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*`Rectangle` क्लास `GraphicalObject` से विरासत में मिलती है। `FillColor` और `Border` सेट करना वैकल्पिक है, लेकिन यह दिखाता है कि **PDF C# में आकार कैसे बनाएं** के दौरान उपस्थिति को कैसे नियंत्रित किया जाए, सिर्फ साधारण रूपरेखा से आगे।*

---

## चरण 5: आयत को पृष्ठ में जोड़ें

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*पैराग्राफ किसी भी ड्रॉएबल ऑब्जेक्ट के कंटेनर होते हैं। `Paragraphs` में आकार डालने से Aspose.Pdf दस्तावेज़ सहेजे जाने पर इसे रेंडर करता है।*

---

## चरण 6: संशोधित PDF सहेजें

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*सेव करने से एक नई फ़ाइल बनती है जिससे मूल `input.pdf` अपरिवर्तित रहता है। आप वही पाथ पास करके स्रोत फ़ाइल को ओवरराइट भी कर सकते हैं, लेकिन बैकअप रखना सर्वोत्तम अभ्यास है।*

---

## पूर्ण स्रोत कोड (चलाने योग्य)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**अपेक्षित आउटपुट** – किसी भी PDF व्यूअर में `output.pdf` खोलें। आपको पहले पृष्ठ के ऊपर‑दाएँ कोने के पास एक नीले‑रंग से भरी हुई आयत दिखनी चाहिए, जिसके चारों ओर गहरा ग्रे बॉर्डर हो।

---

## PDF C# में कई पृष्ठों पर आकार कैसे बनाएं

यदि आपको हर पृष्ठ पर **PDF में आयत जोड़नी** है, तो `Pages` कलेक्शन पर लूप करें:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*यह पैटर्न प्रत्येक पृष्ठ पर समान सीमाएँ पुन: उपयोग करता है। यदि आपको अलग‑अलग स्थितियों की आवश्यकता है तो प्रत्येक पृष्ठ के लिए कोऑर्डिनेट समायोजित करें।*

---

## सामान्य समस्याएँ और सर्वोत्तम‑प्रैक्टिस टिप्स

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| आयत पृष्ठ से बाहर दिखती है | कोऑर्डिनेट नीचे‑बाएँ से मापे जाते हैं; शीर्ष‑उन्मुख कोऑर्डिनेट सिस्टम भ्रम पैदा कर सकता है। | याद रखें कि Y‑अक्ष ऊपर की ओर बढ़ता है। ऐसे मान उपयोग करें जो पृष्ठ आकार (`page.PageInfo.Width`, `page.PageInfo.Height`) के भीतर हों। |
| आकार दिखाई नहीं देता | `FillOpacity` को `0` सेट किया गया है या बॉर्डर चौड़ाई `0` है। | सुनिश्चित करें कि `FillOpacity` `0` से बड़ा हो और `Border.Width` कम से कम `0.5` हो। |
| सहेजते समय `AccessDeniedException` आता है | आउटपुट फ़ाइल किसी अन्य प्रोग्राम में खुली है। | कोड चलाने से पहले सभी व्यूअर बंद करें, या अलग पाथ पर सहेजें। |
| आयत मौजूदा सामग्री के ऊपर ओवरलैप करती है | लेयरिंग कंट्रोल सेट नहीं किया गया था। | यदि लेयरिंग नियंत्रित करनी हो तो `ZIndex` प्रॉपर्टी (उच्च मान ऊपर रेंडर होते हैं) का उपयोग करें। |

---

## आयत का विस्तार – ग्रेडिएंट, रोटेशन, और पारदर्शिता

Aspose.Pdf उन्नत ग्राफ़िक्स का समर्थन करता है। घुमाई हुई आयत के साथ रैखिक ग्रेडिएंट बनाने के लिए:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*यह वही कोड पैटर्न **PDF C# में आकार कैसे बनाएं** को अधिक समृद्ध दृश्य प्रभावों के साथ दर्शाता है।*

---

## प्रोग्रामेटिक रूप से परिणाम की पुष्टि करें

आप पृष्ठ के पैराग्राफ काउंट की जाँच करके पुष्टि कर सकते हैं कि आयत जोड़ी गई है या नहीं:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

यदि सम्मिलन के बाद काउंट एक से बढ़ गया, तो ऑपरेशन सफल रहा।

---

## निष्कर्ष

अब आप C# का उपयोग करके **PDF में आयत जोड़ना** जानते हैं। इस ट्यूटोरियल में दस्तावेज़ लोड करना, सीमाएँ निर्धारित करना, आयत आकार बनाना, उसे पृष्ठ में डालना, और परिणाम सहेजना शामिल था। आपने कई पृष्ठों को संभालना, सामान्य त्रुटियों से बचना, और उन्नत स्टाइलिंग लागू करना भी देखा।

अगला, **PDF C# में आकार कैसे बनाएं** जैसे कि वृत्त, बहुभुज, या फ्री‑फ़ॉर्म पाथ के लिए संबंधित विषयों का अन्वेषण करें, और आकारों को टेक्स्ट व इमेज़ के साथ मिलाकर पूर्ण‑फ़ीचर PDF रिपोर्ट बनाना सीखें।

कोडिंग का आनंद लें!

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का पता लगा सकें।

- [Aspose.PDF for .NET के साथ PDFs में पेज स्टैम्प कैसे जोड़ें | वॉटरमार्क्स & बैकग्राउंड गाइड](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [Aspose.PDF for .NET का उपयोग करके PDF में इमेज़ स्टैम्प कैसे जोड़ें: एक व्यापक गाइड](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Aspose.PDF for .NET के साथ PDFs में घूर्णनशील इमेज़ वॉटरमार्क कैसे जोड़ें](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}