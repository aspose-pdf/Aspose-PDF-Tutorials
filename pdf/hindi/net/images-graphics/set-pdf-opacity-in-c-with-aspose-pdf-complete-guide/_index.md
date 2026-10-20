---
category: general
date: 2026-08-08
description: Aspose.PDF का उपयोग करके C# में PDF की अपारदर्शिता सेट करें – कुछ लाइनों
  के कोड से स्ट्रोक और फ़िल की पारदर्शिता को कैसे समायोजित करें, जानें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set pdf opacity
- Aspose.PDF for .NET
- C# graphics state
- PDF resource dictionary
- blend mode
- PDF transparency
language: hi
lastmod: 2026-08-08
og_description: C# में PDF अपारदर्शिता जल्दी सेट करें। यह गाइड आपको Aspose.PDF के
  ग्राफ़िक्स स्टेट API का उपयोग करके स्ट्रोक और फ़िल ट्रांसपेरेंसी को संशोधित करने
  का तरीका दिखाता है।
og_image_alt: Screenshot of C# code that sets PDF opacity with Aspose.PDF
og_title: Aspose.PDF के साथ C# में PDF अपारदर्शिता सेट करें – चरण‑दर‑चरण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Set PDF opacity in C# using Aspose.PDF – learn how to adjust stroke
    and fill transparency with a few lines of code.
  headline: Set PDF opacity in C# with Aspose.PDF – complete guide
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Aspose.PDF के साथ C# में PDF की अपारदर्शिता सेट करें – पूर्ण मार्गदर्शिका
url: /hi/net/images-graphics/set-pdf-opacity-in-c-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set PDF opacity in C# with Aspose.PDF – complete guide

यदि आपको **PDF की अपारदर्शिता (opacity)** को विशिष्ट ड्रॉइंग ऑपरेशन्स के लिए सेट करना है, तो यह ट्यूटोरियल Aspose.PDF for .NET के साथ इसे कैसे किया जाए, यह बिल्कुल दिखाता है। चाहे आप वॉटरमार्क, अर्द्ध‑पारदर्शी ओवरले, या कस्टम ग्राफ़िक्स बना रहे हों, आप एक संक्षिप्त, प्रोडक्शन‑रेडी तरीका सीखेंगे।

आगे के सेक्शन में हम PDF को लोड करने से लेकर उसके ग्राफ़िक्स स्टेट को एडिट करने, नई अपारदर्शिता परिभाषा जोड़ने, और परिणाम को सेव करने तक सब कुछ कवर करेंगे। कोई बाहरी दस्तावेज़ आवश्यक नहीं—सिर्फ नीचे दिया गया कोड और प्रत्येक चरण की संक्षिप्त व्याख्या।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ पर भी काम करता है)
* एक वैध Aspose.PDF for .NET लाइसेंस (मुफ़्त ट्रायल मूल्यांकन के लिए पर्याप्त है)
* एक इनपुट PDF फ़ाइल (`input.pdf`) जो किसी ऐसे फ़ोल्डर में हो जहाँ आप पढ़‑और‑लिख सकें
* Visual Studio 2022 या कोई भी C# IDE जो आप पसंद करते हैं

## Step 1 – Load the PDF document (Aspose.PDF for .NET)

पहला काम मौजूदा PDF को खोलना है। Aspose.PDF PDF फ़ाइल को `Document` क्लास से दर्शाता है, जो आपको पेजेज़, रिसोर्सेज़ और लो‑लेवल ऑब्जेक्ट्स तक पूरी पहुँच देता है।

```csharp
// Load the PDF document from disk
string inputPath = @"C:\MyFolder\input.pdf";
using var doc = new Aspose.Pdf.Document(inputPath);
```

*Why this matters*: डॉक्यूमेंट को लोड करने से एक इन‑मेमोरी मॉडल बनता है जिसे आप सुरक्षित रूप से संशोधित कर सकते हैं। `using` स्टेटमेंट फ़ाइल हैंडल को स्वचालित रूप से रिलीज़ कर देता है जब हम काम समाप्त कर लेते हैं।

## Step 2 – Get the first page you want to edit

अपारदर्शिता प्रत्येक पेज के रिसोर्स डिक्शनरी के माध्यम से परिभाषित होती है। यहाँ हम पहले पेज को टारगेट कर रहे हैं, लेकिन आप `doc.Pages` पर लूप करके बैच ऑपरेशन भी कर सकते हैं।

```csharp
// Access the first page (pages are 1‑based in Aspose.PDF)
var page = doc.Pages[1];
```

*Why this matters*: हर पेज की अपनी `Resources` कलेक्शन होती है, जिसमें ग्राफ़िक्स स्टेट्स, फ़ॉन्ट्स, इमेजेज़ आदि संग्रहीत होते हैं। सही पेज को संशोधित करने से अपारदर्शिता इफ़ेक्ट वहीँ दिखेगा जहाँ आप चाहते हैं।

## Step 3 – Open the page’s resource dictionary for editing

Aspose.PDF एक `DictionaryEditor` हेल्पर प्रदान करता है जिससे आप लो‑लेवल PDF डिक्शनरी को फ़ाइल संरचना को बिगाड़े बिना बदल सकते हैं।

```csharp
// Prepare a dictionary editor for the page's resources
var dictEditor = new Aspose.Pdf.DictionaryEditor(page.Resources);
```

*Why this matters*: PDF की COS (Content Object System) डिक्शनरी को सीधे एडिट करना ही कस्टम ग्राफ़िक्स स्टेट इन्जेक्ट करने का एकमात्र तरीका है। एडिटर लो‑लेवल सिंटैक्स को एब्स्ट्रैक्ट करता है जबकि PDF वैध रहता है।

## Step 4 – Retrieve the existing ExtGState dictionary

**ExtGState** (external graphics state) डिक्शनरी में अपारदर्शिता, ब्लेंड मोड, लाइन विड्थ आदि होते हैं। यदि यह मौजूद नहीं है, तो आप नया एंट्री जोड़ते समय Aspose.PDF इसे स्वचालित रूप से बना देता है।

```csharp
// Get the ExtGState dictionary; create it if missing
var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary()
                ?? new Aspose.Pdf.Cos.CosPdfDictionary(doc);
```

*Why this matters*: `ExtGState` एंट्री के बिना आप बाद में पेज कंटेंट स्ट्रीम में कस्टम अपारदर्शिता को रेफ़र नहीं कर पाएंगे। यह चरण सुनिश्चित करता है कि कंटेनर मौजूद है।

## Step 5 – Create a new graphics state with the desired opacity

एक ग्राफ़िक्स स्टेट पैरामीटर्स का संग्रह होता है। अपारदर्शिता के लिए हम `CA` (stroke opacity) और `ca` (fill opacity) सेट करते हैं। हम ब्लेंड मोड (`BM`) भी सेट करते हैं ताकि ट्रांसपेरेंट पिक्सेल नीचे की सामग्री के साथ कैसे इंटरैक्ट करें, यह नियंत्रित हो।

```csharp
// Build a new graphics state dictionary
var newGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(doc);
newGs.Add("CA", new Aspose.Pdf.Cos.CosPdfNumber(0.8)); // 80 % stroke opacity
newGs.Add("ca", new Aspose.Pdf.Cos.CosPdfNumber(0.4)); // 40 % fill opacity
newGs.Add("BM", new Aspose.Pdf.Cos.CosPdfName("Normal")); // standard blend mode
```

*Why this matters*: `CA` और `ca` का मान 0 (पूरी तरह से पारदर्शी) से 1 (पूरी तरह से अपारदर्शी) तक हो सकता है। इन संख्याओं को समायोजित करके आप वांछित विज़ुअल इफ़ेक्ट प्राप्त कर सकते हैं। ब्लेंड मोड `"Normal"` सबसे आम है, लेकिन आप कलात्मक प्रभावों के लिए `"Multiply"` या `"Screen"` आज़मा सकते हैं।

## Step 6 – Register the new graphics state in the ExtGState collection

हर ग्राफ़िक्स स्टेट का एक यूनिक नाम होना चाहिए (जैसे `GS0`)। हम अपनी डिक्शनरी को `ExtGState` कलेक्शन में जोड़ते हैं, फिर पेज की रिसोर्सेज़ को अपडेट करते हैं।

```csharp
// Add the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);

// Ensure the ExtGState entry is stored back in the page resources
dictEditor["ExtGState"] = extGState;
```

*Why this matters*: स्टेट को नाम (`GS0`) देने से आप बाद में पेज कंटेंट स्ट्रीम में `gs` ऑपरेटर के ज़रिए इसे रेफ़र कर सकते हैं। यदि आपको कई अपारदर्शिता लेवल चाहिए, तो अतिरिक्त एंट्रीज़ (`GS1`, `GS2`, …) बनाएँ।

## Step 7 – Apply the graphics state to drawing commands (optional)

यदि आप मौजूदा कंटेंट पर तुरंत अपारदर्शिता लागू करना चाहते हैं, तो आपको पेज की कंटेंट स्ट्रीम को एडिट करना होगा। नीचे एक सरल उदाहरण है जो नई बनाई गई स्टेट का उपयोग करके अर्द्ध‑पारदर्शी आयत बनाता है।

```csharp
// Build a content stream that uses the graphics state GS0
var content = new Aspose.Pdf.Operator.GSave();
content.Operators.Add(new Aspose.Pdf.Operator.SetGraphicsState("GS0"));
content.Operators.Add(new Aspose.Pdf.Operator.SetFillColorRgb(1, 0, 0)); // red fill
content.Operators.Add(new Aspose.Pdf.Operator.Rectangle(100, 500, 200, 100));
content.Operators.Add(new Aspose.Pdf.Operator.FillPath());
content.Operators.Add(new Aspose.Pdf.Operator.GRestore());

page.Contents.Add(content);
```

*Why this matters*: `gs` ऑपरेटर (`SetGraphicsState`) PDF रेंडरर को बताता है कि आगे के सभी ड्रॉइंग कमांड्स में `GS0` में परिभाषित अपारदर्शिता मानों का उपयोग करना है। `grestore`/`gsave` जोड़ी यह सुनिश्चित करती है कि पेज के अन्य तत्व अप्रभावित रहें।

## Step 8 – Save the modified PDF

अंत में, अपडेटेड डॉक्यूमेंट को डिस्क पर लिखें।

```csharp
// Save the PDF with the new opacity settings
string outputPath = @"C:\MyFolder\output.pdf";
doc.Save(outputPath);
```

*Why this matters*: सेव करने से सभी बदलाव फाइनल हो जाते हैं, नई ग्राफ़िक्स स्टेट एम्बेड हो जाती है, और एक ऐसा PDF बनता है जिसे कोई भी व्यूअर (Adobe Acrobat, Chrome, आदि) इच्छित ट्रांसपेरेंसी के साथ दिखा सके।

### Expected result

`output.pdf` को किसी PDF व्यूअर में खोलें। आपको एक लाल आयत दिखेगी जिसकी आउटलाइन 80 % अपारदर्शी और फ़िल 40 % अपारदर्शी होगी, जो बैकग्राउंड कंटेंट के साथ स्मूदली ब्लेंड होगी। पेज का बाकी हिस्सा अपरिवर्तित रहेगा।

## Common variations and edge cases

| Situation | What to change | Reason |
|-----------|----------------|--------|
| **Multiple opacity levels** | Create additional graphics states (`GS1`, `GS2`, …) with different `CA`/`ca` values and reference them where needed | Allows fine‑grained control over different elements |
| **Different blend modes** | Use `"Multiply"`, `"Screen"`, `"Overlay"` etc., instead of `"Normal"` in the `BM` entry | Produces artistic blending effects |
| **Applying to an existing content stream** | Insert `SetGraphicsState` before the specific drawing operators you want to affect | Prevents unwanted opacity on unrelated objects |
| **Large PDFs** | Process pages in a `foreach (Page p in doc.Pages)` loop to avoid loading the entire file into memory at once | Improves performance and reduces memory pressure |
| **No existing ExtGState** | The code in Step 4 already creates one if missing, so no extra handling is required | Guarantees the dictionary is present |

### Pro tip

जब आप कई कस्टम ग्राफ़िक्स स्टेट्स जोड़ते हैं, तो नामकरण को सुसंगत रखें (`GS0`, `GS1`, …) और प्रत्येक का उद्देश्य एक टिप्पणी ब्लॉक में दस्तावेज़ करें। इससे भविष्य में मेंटेनेंस आसान हो जाता है, विशेषकर सहयोगी प्रोजेक्ट्स में।

## Full, runnable example

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं। इसमें सभी चरण, आवश्यक `using` निर्देश, और टिप्पणी शामिल हैं।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

namespace PdfOpacityDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the PDF
            string inputPath = @"C:\MyFolder\input.pdf";
            using var doc = new Document(inputPath);

            // 2. Get the first page (adjust index for other pages)
            var page = doc.Pages[1];

            // 3. Open the page's resource dictionary
            var dictEditor = new DictionaryEditor(page.Resources);

            // 4. Retrieve or create the ExtGState dictionary
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary()
                            ?? new CosPdfDictionary(doc);

            // 5. Create a new graphics state with desired opacity
            var newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            newGs.Add("CA", new CosPdfNumber(0.8));          // stroke opacity (80%)
            newGs.Add("ca", new CosPdfNumber(0.4));          // fill opacity (40%)
            newGs.Add("BM", new CosPdfName("Normal"));      // blend mode

            // 6. Register the graphics state as "GS0"
            extGState.Add("GS0", newGs);
            dictEditor["ExtGState"] = extGState; // write back to resources

            // 7. (Optional) Draw a rectangle using the new opacity
            var content = new Operator.GSave();
            content.Operators.Add(new Operator.SetGraphicsState("GS0"));
            content.Operators.Add(new Operator.SetFillColorRgb(1, 0, 0)); // red
            content.Operators.Add(new Operator.Rectangle(100, 500, 200, 100));
            content.Operators.Add(new Operator.FillPath());
            content.Operators.Add(new Operator.GRestore());

            page.Contents.Add(content);

            // 8. Save the modified PDF
            string outputPath = @"C:\MyFolder\output.pdf";
            doc.Save(outputPath);

            Console.WriteLine("PDF saved with new opacity settings at: " + outputPath);
        }
    }
}
```

Run the program,

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर कर सकें।

- [Set Image Backgrounds in PDFs Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/aspose-pdf-net-set-image-backgrounds/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Customize PDFs with Aspose.PDF for .NET: Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}