---
category: general
date: 2026-04-06
description: C# का उपयोग करके PDF में जल्दी से आयत जोड़ें। इस चरण‑दर‑चरण ट्यूटोरियल
  में PDF पर आयत बनाना, C# में PDF दस्तावेज़ लोड करना, और Aspose PDF से आयत बनाना
  सीखें।
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- draw shape in pdf
- load pdf document c#
- aspose pdf draw rectangle
language: hi
og_description: PDF में तुरंत आयत जोड़ें। यह गाइड दिखाता है कि PDF पर आयत कैसे बनाएं,
  C# में PDF दस्तावेज़ कैसे लोड करें, और स्पष्ट कोड उदाहरणों के साथ Aspose PDF का
  उपयोग करके आयत कैसे बनाएं।
og_title: C# के साथ PDF में आयत जोड़ें – पूर्ण Aspose PDF ट्यूटोरियल
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: C# के साथ PDF में आयत जोड़ें – पूर्ण Aspose PDF गाइड
url: /hi/net/images-graphics/add-rectangle-to-pdf-with-c-full-aspose-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF में आयत जोड़ें – पूर्ण Aspose PDF ट्यूटोरियल

क्या आपको कभी **PDF में आयत जोड़ने** की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि कौन सा API कॉल काम करेगा? आप अकेले नहीं हैं; कई डेवलपर्स को रिपोर्ट ऑटोमेट करने या दस्तावेज़ में सेक्शन को हाइलाइट करने के दौरान यही समस्या आती है। इस गाइड में हम Aspose.PDF for .NET का उपयोग करके **PDF पर आयत खींचने** के सटीक चरणों को दिखाएंगे, और आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जिसे आप अपने प्रोजेक्ट में जोड़ सकते हैं।

हम यह भी बताएंगे कि **C# में PDF दस्तावेज़ लोड करना** कैसे किया जाता है, यह सत्यापित करें कि आकार पृष्ठ में फिट बैठता है, और जब आप **PDF में आकार खींचने** की कोशिश करते हैं तो कुछ सामान्य समस्याओं पर चर्चा करेंगे। अंत तक आपके पास एक कार्यशील प्रोग्राम होगा जो किसी भी PDF की पहली पृष्ठ पर एक चमकीला पीला आयत जोड़ देगा।

## आप को क्या चाहिए

- .NET 6.0 या बाद का (कोड .NET Framework 4.6+ के साथ भी काम करता है)
- Aspose.PDF for .NET NuGet पैकेज (संस्करण 23.11 या नया)
- एक सैंपल PDF फ़ाइल (`input.pdf`) जिसे आप किसी फ़ोल्डर में रख सकते हैं
- Visual Studio, VS Code, या कोई भी C# IDE जो आप पसंद करते हैं

कोई अतिरिक्त कॉन्फ़िगरेशन फ़ाइलें नहीं, कोई COM इंटरऑप नहीं, बस कुछ `using` स्टेटमेंट्स और कुछ लाइनों का लॉजिक।

## चरण 1: C# में PDF दस्तावेज़ लोड करें – फ़ाइल तैयार करना

सबसे पहले आपको मौजूदा PDF खोलना होगा ताकि आपके पास उस पर ड्रॉ करने के लिए कुछ हो। Aspose.PDF इसे एक लाइन में कर देता है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color

// Step 1: Load the PDF document
var inputPath = @"C:\MyPdfs\input.pdf";
using var pdfDocument = new Document(inputPath);
```

**Why this matters:**  
`Document` पूरे PDF फ़ाइल का प्रतिनिधित्व करता है। इसे `using` ब्लॉक में लपेटने से फ़ाइल हैंडल तुरंत रिलीज़ हो जाता है, जिससे Windows पर फ़ाइल‑लॉक समस्याएँ नहीं आतीं। यदि आप `using` भूल जाते हैं, तो सहेजने की कोशिश पर आपको “cannot access the file because it is being used by another process” जैसा संदेश मिल सकता है।

## चरण 2: लक्ष्य पृष्ठ तक पहुँचें और सीमाओं की जाँच करें – PDF में आकार सुरक्षित रूप से खींचें

पृष्ठ पर आयत लगाने से पहले, आपको पृष्ठ ऑब्जेक्ट चाहिए और यह पुष्टि करनी चाहिए कि आयत पृष्ठ के आयामों के भीतर फिट बैठती है। यह रन‑टाइम एक्सेप्शन से बचाता है और आपका PDF साफ़-सुथरा रहता है।

```csharp
// Step 2: Get the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define rectangle bounds: lower‑left X/Y and upper‑right X/Y
var rectangleBounds = new Rectangle(50, 700, 200, 800);

// Verify the rectangle is inside the page limits
bool fits = rectangleBounds.LLX >= 0 &&
            rectangleBounds.URX <= firstPage.PageInfo.Width &&
            rectangleBounds.LLY >= 0 &&
            rectangleBounds.URY <= firstPage.PageInfo.Height;

if (!fits)
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

**Explanation:**  
`Rectangle` कंस्ट्रक्टर चार संख्याएँ अपेक्षित करता है: बायें‑नीचे X, बायें‑नीचे Y, दायें‑ऊपर X, दायें‑ऊपर Y। ये मान पॉइंट्स में मापे जाते हैं (1 pt ≈ 1/72 in)। सत्यापन चरण एक छोटा सुरक्षा जाल है—विशेषकर उपयोगी जब आप निर्देशांक गतिशील रूप से गणना करते हैं (जैसे, इमेज साइज या टेक्स्ट की लंबाई के आधार पर)।

## चरण 3: PDF में आयत जोड़ें – “PDF में आयत जोड़ें” का मुख्य भाग

अब मज़ेदार भाग: वास्तव में आकार को डालना। Aspose.PDF एक `RectangleShape` क्लास प्रदान करता है जिसे आप पृष्ठ के `Paragraphs` संग्रह में डाल सकते हैं।

```csharp
// Step 3: Add a yellow rectangle shape
var rectangleShape = new RectangleShape(rectangleBounds)
{
    FillColor = Color.Yellow,
    Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black) // Optional: thin black border
};

firstPage.Paragraphs.Add(rectangleShape);
```

**Why use `RectangleShape`?**  
यह एक वेक्टर ग्राफ़िक है, इसलिए आयत किसी भी डिवाइस पर साफ़-सुथरे ढंग से स्केल होती है। इसे `Paragraphs` में जोड़ने से यह किसी भी अन्य कंटेंट एलिमेंट की तरह व्यवहार करता है—पृष्ठ के सापेक्ष स्थित, न कि मौजूदा टेक्स्ट के सापेक्ष। यदि आपको पारदर्शी भराव चाहिए, तो बस `FillColor = Color.Transparent` सेट करें।

> **Pro tip:** `FillColor` को `Color.FromArgb(128, 255, 255, 0)` में बदलें ताकि एक अर्ध‑पारदर्शी पीला रंग मिले जो नीचे का टेक्स्ट दिखा सके।

## चरण 4: अपडेटेड PDF सहेजें – “PDF में आयत जोड़ें” चक्र समाप्त करें

एक बार आकार जगह पर हो जाने पर, आप बस दस्तावेज़ को नई फ़ाइल में सहेजते हैं (या यदि आप चाहें तो मूल फ़ाइल को ओवरराइट कर सकते हैं)।

```csharp
// Step 4: Save the updated PDF
var outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

बस इतना ही! `output.pdf` खोलें और आप देखेंगे कि एक चमकीला पीला आयत ठीक उन निर्देशांक के बीच बैठा है जो आपने निर्दिष्ट किए थे।

## पूर्ण कार्यशील उदाहरण – सभी चरण एक फ़ाइल में

नीचे पूरा, स्वतंत्र प्रोग्राम दिया गया है जिसे आप जैसा है वैसा कंपाइल और चलाकर उपयोग कर सकते हैं। इसमें त्रुटि संभालना और टिप्पणियाँ शामिल हैं जो प्रत्येक पंक्ति को समझाती हैं।

```csharp
// ---------------------------------------------------------------
// AddRectangleToPdf.cs
// Demonstrates how to add rectangle to PDF using Aspose.PDF for .NET
// ---------------------------------------------------------------
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddRectangleToPdf
{
    static void Main()
    {
        // ----- 1. Load the PDF document -----
        string inputPath = @"C:\MyPdfs\input.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        using var pdfDoc = new Document(inputPath);

        // ----- 2. Access first page and define rectangle bounds -----
        Page page = pdfDoc.Pages[1];
        var rect = new Rectangle(50, 700, 200, 800);

        // Verify rectangle fits the page
        bool fits = rect.LLX >= 0 && rect.URX <= page.PageInfo.Width &&
                    rect.LLY >= 0 && rect.URY <= page.PageInfo.Height;
        if (!fits)
        {
            Console.WriteLine("Rectangle exceeds page dimensions. Adjust coordinates.");
            return;
        }

        // ----- 3. Create and add rectangle shape -----
        var shape = new RectangleShape(rect)
        {
            FillColor = Color.Yellow,
            Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black)
        };
        page.Paragraphs.Add(shape);

        // ----- 4. Save the modified PDF -----
        string outputPath = @"C:\MyPdfs\output.pdf";
        pdfDoc.Save(outputPath);
        Console.WriteLine($"Rectangle added successfully. Saved to {outputPath}");
    }
}
```

**Expected result:**  
जब आप `output.pdf` खोलेंगे, तो पहली पृष्ठ पर एक पीला आयत दिखेगा जिसकी निचला‑बायाँ कोना (50 pt, 700 pt) पर शुरू होता है और ऊपर‑दायाँ कोना (200 pt, 800 pt) पर समाप्त होता है। आयत में एक पतली काली बॉर्डर होगी, जिससे यह अधिकांश बैकग्राउंड पर स्पष्ट रूप से दिखाई देगा।

## सामान्य प्रश्न और किनारे के मामलों

### यदि मुझे आयत किसी अलग पृष्ठ पर खींचनी हो तो क्या करें?

सिर्फ `pdfDoc.Pages[1]` को इच्छित पृष्ठ संख्या में बदलें (`pdfDoc.Pages[3]` तीसरे पृष्ठ के लिए)। याद रखें कि Aspose 1‑आधारित इंडेक्सिंग उपयोग करता है, शून्य‑आधारित नहीं।

### क्या मैं लूप में कई आयतें खींच सकता हूँ?

बिल्कुल। आयत‑निर्माण लॉजिक को एक `foreach` में रखें जो निर्देशांक के संग्रह पर इटररेट करता है। केवल प्रदर्शन का ध्यान रखें; हजारों आकार जोड़ने से फ़ाइल आकार में उल्लेखनीय वृद्धि हो सकती है।

### यह `Graphics` या `System.Drawing` का उपयोग करने से कैसे अलग है?

`System.Drawing` रास्टर इमेज के साथ काम करता है; आउटपुट एक बिटमैप में बेक हो जाता है, जो ज़ूम करने पर धुंधला हो सकता है। `RectangleShape` वेक्टर‑आधारित है, यानी यह किसी भी ज़ूम लेवल पर स्पष्ट रहता है—पेशेवर PDFs के लिए आदर्श।

### यदि PDF पासवर्ड‑सुरक्षित हो तो क्या करें?

दस्तावेज़ को `PdfLoadOptions` ऑब्जेक्ट के साथ लोड करें जिसमें पासवर्ड शामिल हो:

```csharp
var loadOpts = new PdfLoadOptions { Password = "mySecret" };
using var pdfDoc = new Document(inputPath, loadOpts);
```

फिर सामान्य रूप से आगे बढ़ें। जब दस्तावेज़ मेमोरी में डिक्रिप्ट हो जाएगा तो आयत जोड़ दी जाएगी।

## दृश्य संदर्भ

![पहले पृष्ठ पर पीले आयत के साथ PDF में आयत जोड़ने का उदाहरण](/images/add-rectangle-to-pdf-example.png)

*Alt text: “पहले पृष्ठ पर पीले आयत के साथ PDF में आयत जोड़ने का उदाहरण”*

## सारांश और अगले कदम

हमने अभी-अभी Aspose.PDF for .NET का उपयोग करके **PDF में आयत जोड़ने** के बारे में कवर किया है, दस्तावेज़ लोड करने से लेकर संशोधित फ़ाइल सहेजने तक। मुख्य बिंदु:

1. सही डिस्पोज़ल के साथ PDF लोड करें (`load pdf document c#`)।
2. आयत की सीमाएँ निर्धारित करें और पुष्टि करें कि वे पृष्ठ में फिट होते हैं।
3. `RectangleShape` का उपयोग करके **PDF पर आयत खींचें** (या कोई अन्य **PDF में आकार खींचें** जिसकी आपको आवश्यकता हो)।
4. परिणाम सहेजें और वेक्टर‑शार्प आयत का आनंद लें।

और अधिक करने के लिए तैयार हैं? `RectangleShape` को `EllipseShape` या `PolygonShape` से बदलें ताकि कस्टम हाइलाइट बन सकें। या Aspose की टेक्स्ट‑एक्सट्रैक्शन क्षमताओं का अन्वेषण करें ताकि कीवर्ड लोकेशन के आधार पर आकारों को गतिशील रूप से स्थित किया जा सके। लाइब्रेरी इतनी समृद्ध है कि आप C# से बाहर निकले बिना पूर्ण‑फ़ीचर एनोटेशन टूल बना सकते हैं।

यदि आपको कोई समस्या आती है, तो नीचे टिप्पणी छोड़ें—हम मदद करने के लिए तैयार हैं। और यदि आपको यह उपयोगी लगे तो Aspose.PDF NuGet पैकेज को स्टार देना न भूलें। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}