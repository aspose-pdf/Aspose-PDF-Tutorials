---
category: general
date: 2026-07-29
description: Aspose.Pdf for .NET का उपयोग करके PDF में पारदर्शिता जोड़ें। चरण‑दर‑चरण
  ट्यूटोरियल में PDF की अपारदर्शिता, ब्लेंड मोड और ग्राफ़िक्स स्टेट सेट करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- Aspose.Pdf for .NET
- ExtGState dictionary
- PDF opacity
- graphics state
- Blend mode
language: hi
lastmod: 2026-07-29
og_description: PDF में शीघ्रता से पारदर्शिता जोड़ें। यह गाइड Aspose.Pdf for .NET
  का उपयोग करके PDF की अपारदर्शिता और ब्लेंड मोड सेट करने का तरीका दिखाता है।
og_image_alt: Screenshot of a PDF page showing transparent overlay created with Aspose.Pdf
og_title: Aspose.Pdf के साथ PDF में पारदर्शिता जोड़ें – पूर्ण .NET मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Add transparency to PDF using Aspose.Pdf for .NET. Learn to set PDF
    opacity, blend mode, and graphics state in a step‑by‑step tutorial.
  headline: Add Transparency to PDF with Aspose.Pdf – Complete .NET Guide
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- .NET
title: Aspose.Pdf के साथ PDF में पारदर्शिता जोड़ें – पूर्ण .NET गाइड
url: /hi/net/advanced-features/add-transparency-to-pdf-with-aspose-pdf-complete-net-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Transparency to PDF with Aspose.Pdf – Complete .NET Guide

क्या आपको कभी **PDF फ़ाइलों में ट्रांसपेरेंसी जोड़नी** पड़ी है लेकिन यह नहीं पता था कि कौन से API प्रॉपर्टीज़ बदलें? आप अकेले नहीं हैं। इस ट्यूटोरियल में हम एक व्यावहारिक, एंड‑टू‑एंड उदाहरण के माध्यम से दिखाएंगे कि PDF की अपारदर्शिता कैसे सेट करें, ब्लेंड मोड कैसे परिभाषित करें, और **Aspose.Pdf for .NET** का उपयोग करके नया ग्राफ़िक्स स्टेट कैसे इंजेक्ट करें।

हम एक खाली PDF से शुरू करेंगे, उसमें एक अर्ध‑पारदर्शी आयत जोड़ेंगे, और परिणाम को सहेजेंगे—सिर्फ कुछ ही लाइनों में। अंत तक आप समझेंगे कि **ExtGState डिक्शनरी** क्यों महत्वपूर्ण है, **ग्राफ़िक्स स्टेट** कैसे स्ट्रोक और फ़िल अपारदर्शिता दोनों को नियंत्रित करता है, और **ब्लेंड मोड** पर्दे के नीचे क्या करता है।

## What You’ll Learn

- Aspose.Pdf के साथ मौजूदा PDF को कैसे लोड करें।
- पेज पर **ExtGState** डिक्शनरी को कैसे एक्सेस और मॉडिफ़ाई करें।
- नया **ग्राफ़िक्स स्टेट** कैसे बनाएं जो `CA`, `ca`, और `BM` एंट्रीज़ को परिभाषित करता है।
- बदले हुए डॉक्यूमेंट को कैसे सेव करें ताकि ट्रांसपेरेंसी इफ़ेक्ट किसी भी PDF व्यूअर में दिखे।
- सामान्य pitfalls (जैसे, नया स्टेट रिसोर्स डिक्शनरी में जोड़ना भूल जाना) और उनके त्वरित समाधान।

> **Prerequisites:** Visual Studio 2022 (या कोई भी IDE जो आप पसंद करते हैं), .NET 6 या बाद का संस्करण, और Aspose.Pdf for .NET लाइसेंस (डेमो के लिए फ्री ट्रायल काम करता है)।  

---

## Step 1: Load the PDF Document

सबसे पहले—उस फ़ाइल को खोलें जिसे आप एडिट करना चाहते हैं। `Aspose.Pdf.Document` क्लास पार्सिंग से लेकर राइटिंग तक सब संभालती है।

```csharp
// Step 1: Load the PDF document
string pdfPath = @"C:\Temp\input.pdf";   // replace with your actual path
using var document = new Aspose.Pdf.Document(pdfPath);
```

*Why this matters:* डॉक्यूमेंट को लोड करने से आपको अंदरूनी COS (Concrete Object Structure) ऑब्जेक्ट्स तक पहुंच मिलती है, जहाँ **ग्राफ़िक्स स्टेट** रहता है। वैध `Document` इंस्टेंस के बिना आप **ExtGState डिक्शनरी** तक नहीं पहुंच सकते।

---

## Step 2: Grab the First Page and Its Resource Dictionary

ट्रांसपेरेंसी पेज‑लेवल रिसोर्स स्कोप पर लागू होती है, इसलिए हमें पेज की रिसोर्स कलेक्शन चाहिए।

```csharp
// Step 2: Access the first page and its resource dictionary
var page = document.Pages[1];                     // pages are 1‑based in Aspose
var resourcesEditor = new Aspose.Pdf.Text.DictionaryEditor(page.Resources);
```

> **Tip:** यदि आप मल्टी‑पेज PDFs के साथ काम कर रहे हैं, तो बस `document.Pages` पर लूप लगाएँ और प्रत्येक पेज के लिए ये स्टेप्स दोहराएँ जिसे आप प्रभावित करना चाहते हैं।

---

## Step 3: Locate (or Create) the ExtGState Dictionary

**ExtGState** एंट्री पेज के सभी एक्सटेंडेड ग्राफ़िक्स स्टेट्स को स्टोर करती है। यदि यह अभी तक मौजूद नहीं है, तो Aspose हमारे लिए एक खाली डिक्शनरी बना देगा।

```csharp
// Step 3: Retrieve the ExtGState dictionary where graphics states are stored
var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                ?? new Aspose.Pdf.Cos.CosPdfDictionary(document);
```

*Explanation:*  
- `resourcesEditor["ExtGState"]` मौजूदा डिक्शनरी को फ़ेच करता है।  
- नल‑कोएलसिंग ऑपरेटर (`??`) सुनिश्चित करता है कि हमारे पास हमेशा काम करने के लिए एक डिक्शनरी हो, जिससे `NullReferenceException` से बचा जा सके।

---

## Step 4: Build a New Graphics State with PDF Opacity

अब हम वास्तविक ट्रांसपेरेंसी पैरामीटर्स परिभाषित करेंगे। `CA` स्ट्रोक अपारदर्शिता को नियंत्रित करता है, `ca` फ़िल अपारदर्शिता को, और `BM` ब्लेंड मोड सेट करता है (जैसे “Normal”, “Multiply” आदि)।

```csharp
// Step 4: Create a new graphics state dictionary and define its parameters
var newGraphicsState = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(document);

var parameters = new (string Name, Aspose.Pdf.Cos.ICosPdfPrimitive Value)[]
{
    ("CA", new Aspose.Pdf.Cos.CosPdfNumber(1.0)),      // Stroke opacity = 100%
    ("ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),      // Fill opacity = 50%
    ("BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))   // Blend mode = Normal
};

foreach (var (name, value) in parameters)
{
    newGraphicsState.Add(name, value);
}
```

*Why these keys?*  
- `CA` (`Stroke opacity`) और `ca` (`Fill opacity`) PDF स्पेसिफिकेशन द्वारा ट्रांसपेरेंसी व्यक्त करने के लिए दो न्यूमेरिक एंट्रीज़ हैं।  
- `BM` (`Blend mode`) रेंडरर को बताता है कि ट्रांसपेरेंट ऑब्जेक्ट को बैकग्राउंड के साथ कैसे मिलाया जाए; “Normal” सबसे आम विकल्प है।

---

## Step 5: Register the New State in the ExtGState Dictionary

हम अपने ग्राफ़िक्स स्टेट को एक नाम देते हैं (`GS0` इस उदाहरण में) और इसे पेज की **ExtGState** कलेक्शन में डालते हैं।

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a name
extGState.Add("GS0", newGraphicsState);

// Ensure the page's Resources point to the updated ExtGState
resourcesEditor["ExtGState"] = extGState;
```

> **Pro tip:** यदि आप कई स्टेट्स जोड़ने की योजना बना रहे हैं तो एक यूनिक नाम (`GS1`, `GS2`, …) चुनें। नाम दोहराने से पहले वाला एंट्री ओवरराइट हो जाएगा।

---

## Step 6: Apply the Graphics State to Content (Optional but Recommended)

यदि आप तुरंत ट्रांसपेरेंसी इफ़ेक्ट देखना चाहते हैं, तो आप नए बनाए गए स्टेट का उपयोग करके एक आयत ड्रॉ कर सकते हैं। यह स्टेप *PDF में ट्रांसपेरेंसी जोड़ने* के लिए अनिवार्य नहीं है—स्टेट अब किसी भी भविष्य के कंटेंट स्ट्रीम के लिए उपलब्ध है—पर यह सब कुछ सही काम कर रहा है, यह वेरिफ़ाई करने में मदद करता है।

```csharp
// Optional: Draw a semi‑transparent rectangle using the new graphics state
var canvas = new Aspose.Pdf.Drawing.Graphic(page);
canvas.SetExtGState("GS0");                     // reference the state we just added
canvas.Rectangle(100, 500, 200, 100);          // x, y, width, height
canvas.FillColor = Aspose.Pdf.Drawing.Color.FromRgba(255, 0, 0, 128); // red with 50% alpha
canvas.StrokeColor = Aspose.Pdf.Drawing.Color.Black;
canvas.Draw();
```

*Explanation:*  
- `SetExtGState("GS0")` कंटेंट स्ट्रीम को बताता है कि वह हमारे परिभाषित ग्राफ़िक्स स्टेट का उपयोग करे।  
- आयत 50 % फ़िल अपारदर्शिता के साथ दिखाई देगी, जिससे यह पुष्टि होगी कि **PDF अपारदर्शिता** सेटिंग्स सक्रिय हैं।

---

## Step 7: Save the Modified PDF

अंत में, बदलावों को डिस्क पर लिखें।

```csharp
// Step 7: Save the modified PDF
string outputPath = @"C:\Temp\output.pdf";
document.Save(outputPath);
```

`output.pdf` को Adobe Acrobat, Foxit, या यहाँ तक कि अपने ब्राउज़र में खोलें—आपको पेज कंटेंट के ऊपर अर्ध‑पारदर्शी आयत दिखनी चाहिए।

---

## Full Working Example

सब कुछ एक साथ मिलाकर, यहाँ पूरा, कॉपी‑पेस्ट‑रेडी प्रोग्राम है:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        string pdfPath = @"C:\Temp\input.pdf";
        using var document = new Document(pdfPath);

        // Access first page and its resources
        var page = document.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // Retrieve or create ExtGState dictionary
        var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                        ?? new CosPdfDictionary(document);

        // Build new graphics state (stroke opacity 1, fill opacity 0.5, normal blend)
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
        var parameters = new (string, ICosPdfPrimitive)[]
        {
            ("CA", new CosPdfNumber(1.0)),
            ("ca", new CosPdfNumber(0.5)),
            ("BM", new CosPdfName("Normal"))
        };
        foreach (var (name, value) in parameters)
            newGraphicsState.Add(name, value);

        // Add graphics state to ExtGState with a unique name
        extGState.Add("GS0", newGraphicsState);
        resourcesEditor["ExtGState"] = extGState;   // update page resources

        // OPTIONAL: draw a rectangle using the new state to verify
        var canvas = new Graphic(page);
        canvas.SetExtGState("GS0");
        canvas.Rectangle(100, 500, 200, 100);
        canvas.FillColor = Color.FromRgba(255, 0, 0, 128); // 50% transparent red
        canvas.StrokeColor = Color.Black;
        canvas.Draw();

        // Save the output PDF
        string outputPath = @"C:\Temp\output.pdf";
        document.Save(outputPath);
    }
}
```

### Expected Output

- `output.pdf` में मूल पेज **के साथ** एक लाल आयत होगी जो 50 % ट्रांसपेरेंट है।  
- **ExtGState** एंट्री `GS0` अब पेज की रिसोर्स डिक्शनरी का हिस्सा है, पुनः उपयोग के लिए तैयार।

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Do I need a license to run this?** | एक ट्रायल लाइसेंस विकास और टेस्टिंग के लिए काम करता है। प्रोडक्शन के लिए आपको पेड लाइसेंस चाहिए, अन्यथा आउटपुट में वॉटरमार्क रहेगा। |
| **What if the PDF already has an ExtGState entry?** | कोड मौजूदा डिक्शनरी की जाँच करता है और उसे री‑यूज़ करता है, इसलिए पहले से परिभाषित स्टेट्स नहीं खोएँगे। |
| **Can I set a different blend mode?** | बिल्कुल। `"Normal"` को `"Multiply"`, `"Screen"` या किसी भी PDF‑डिफाइंड ब्लेंड मोड से बदल दें। |
| **Is `CA` mandatory?** | नहीं। यदि आप `CA` छोड़ देते हैं, तो स्ट्रोक अपारदर्शिता डिफॉल्ट रूप से 1 (पूरी तरह अपारदर्शी) रहती है। आप केवल `ca` सेट करके फ़िल ट्रांसपेरेंसी भी कर सकते हैं। |
| **How do I apply the state to text?** | `canvas.SetExtGState("GS0")` को `canvas.ShowText(...)` से पहले कॉल करें। वही ग्राफ़िक्स स्टेट टेक्स्ट, पाथ और इमेजेज़ सभी पर लागू होता है। |

---

## Next Steps

Now


## What Should You Learn Next?


निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूरी तरह कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Add Image Stamps to PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET&#58; Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}