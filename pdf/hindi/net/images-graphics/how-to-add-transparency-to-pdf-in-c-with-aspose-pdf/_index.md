---
category: general
date: 2026-11-22
description: Aspose.PDF for C# का उपयोग करके PDF में पारदर्शिता जोड़ें। स्पष्ट, चरण‑दर‑चरण
  उदाहरण के साथ PDF की अपारदर्शिता कैसे बदलें, सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- how to change pdf opacity
- Aspose.PDF opacity
- PDF graphics state C#
- PDF blend mode example
language: hi
lastmod: 2026-11-22
og_description: Aspose.PDF for C# के साथ PDF में पारदर्शिता जोड़ें। यह ट्यूटोरियल
  दिखाता है कि PDF की अपारदर्शिता को जल्दी और विश्वसनीय रूप से कैसे बदलें।
og_image_alt: Screenshot of a PDF page showing translucent graphics after adding transparency
og_title: C# में PDF में पारदर्शिता जोड़ें – पूर्ण Aspose.PDF गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Add transparency to PDF using Aspose.PDF for C#. Learn how to change
    PDF opacity with a clear, step‑by‑step example.
  headline: How to add transparency to PDF in C# with Aspose.PDF
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: C# में Aspose.PDF के साथ PDF में पारदर्शिता कैसे जोड़ें
url: /hi/net/images-graphics/how-to-add-transparency-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose.PDF के साथ PDF में ट्रांसपेरेंसी कैसे जोड़ें

यदि आपको **PDF फ़ाइलों में ट्रांसपेरेंसी जोड़नी** है, तो यह गाइड Aspose.PDF for .NET का उपयोग करके एक पूर्ण समाधान दिखाता है। आप देखेंगे कि **PDF की अपारदर्शिता** को वेक्टर ग्राफ़िक्स, टेक्स्ट या इमेज के लिए C# वातावरण से बाहर निकले बिना कैसे बदलें।

यह ट्यूटोरियल हर चरण को कवर करता है—डॉक्यूमेंट लोड करने से लेकर पेज की ग्राफ़िक्स स्टेट को एडिट करने और परिणाम को सेव करने तक। अंत तक, आप ऐसे PDF बना सकते हैं जहाँ चयनित तत्व अर्ध‑पारदर्शी दिखें, जो वॉटरमार्क, ओवरले इफ़ेक्ट या डिज़ाइन मॉक‑अप के लिए उपयोगी है।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.8 के साथ भी काम करता है)
* एक वैध Aspose.PDF for .NET लाइसेंस या अस्थायी इवैल्यूएशन की
* Visual Studio 2022 (या कोई भी IDE जो C# सपोर्ट करता हो)
* `input.pdf` नाम की इनपुट PDF, जो किसी ज्ञात फ़ोल्डर में रखी हो

इन वस्तुओं से यह सुनिश्चित होता है कि कोड अतिरिक्त कॉन्फ़िगरेशन के बिना चल सके।

## चरण 1: PDF दस्तावेज़ लोड करें

पहला ऑपरेशन मौजूदा PDF फ़ाइल को खोलना है। Aspose.PDF पूरे फ़ाइल को `Document` क्लास से दर्शाता है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;

// Load the source PDF
var inputPath = @"C:\MyFiles\input.pdf";
var doc = new Document(inputPath);
```

*इस चरण का महत्व*: दस्तावेज़ को लोड करने से एक इन‑मेमोरी मॉडल बनता है जो आपको पेज, रिसोर्सेज़ और कंटेंट स्ट्रीम्स को निरीक्षण करने देता है। इस ऑब्जेक्ट के बिना आप ग्राफ़िक्स स्टेट को संशोधित नहीं कर सकते।

## चरण 2: पहले पेज के रिसोर्स डिक्शनरी तक पहुंचें

ट्रांसपेरेंसी **ग्राफ़िक्स स्टेट** के माध्यम से लागू की जाती है, जो पेज की रिसोर्स डिक्शनरी में संग्रहीत होती है। इस डिक्शनरी को एडिट करने के लिए आपको `DictionaryEditor` की आवश्यकता होगी।

```csharp
// Get the first page (pages are 1‑based)
var page = doc.Pages[1];

// Open the resource dictionary for editing
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

यदि पेज में अभी तक `ExtGState` एंट्री नहीं है, तो Aspose.PDF जब आप इसे अनुरोध करते हैं तो स्वचालित रूप से एक खाली डिक्शनरी बना देता है। यह लचीलापन मतलब है कि वही कोड उन PDF के लिए भी काम करता है जो पहले से ट्रांसपेरेंसी उपयोग करते हैं या कभी नहीं करते।

## चरण 3: अपारदर्शिता मानों के साथ नया ग्राफ़िक्स स्टेट बनाएं

एक ग्राफ़िक्स स्टेट में पैरामीटर होते हैं जैसे फ़िल अपारदर्शिता (`ca`), स्ट्रोक अपारदर्शिता (`CA`), और ब्लेंड मोड (`BM`)। नीचे दिया गया ब्लॉक 50 % फ़िल अपारदर्शिता सेट करता है जबकि स्ट्रोक को पूरी तरह अपारदर्शी रखता है।

```csharp
// Build a new graphics state dictionary
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);

// Stroke opacity – fully opaque (value between 0 and 1)
graphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity – 50 % transparent
graphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode – Normal (other modes: Multiply, Screen, etc.)
graphicsState.Add("BM", new CosPdfName("Normal"));
```

*इन कुंजियों का कारण*:  
* `CA` स्ट्रोक्ड पाथ्स (लाइन, बॉर्डर) की अपारदर्शिता नियंत्रित करता है।  
* `ca` फ़िल्ड ऑब्जेक्ट्स (टेक्स्ट फ़िल, इमेज फ़िल) की अपारदर्शिता नियंत्रित करता है।  
* `BM` यह तय करता है कि पारदर्शी ऑब्जेक्ट नीचे की सामग्री के साथ कैसे मिश्रित होता है; `Normal` सबसे सामान्य विकल्प है।

## चरण 4: ग्राफ़िक्स स्टेट को पेज रिसोर्सेज़ में रजिस्टर करें

ग्राफ़िक्स स्टेट बनाने के बाद, आपको इसे पेज की `ExtGState` डिक्शनरी में एक अनूठे नाम (जैसे `GS0`) के तहत जोड़ना होगा। कंटेंट स्ट्रीम्स फिर इस नाम को संदर्भित करके अपारदर्शिता सेटिंग लागू कर सकते हैं।

```csharp
// Add the new graphics state to the resource dictionary
extGState.Add("GS0", graphicsState);
```

इस बिंदु पर PDF फ़ाइल में `GS0` नाम का पुन: उपयोग योग्य ग्राफ़िक्स स्टेट मौजूद है। कोई भी ड्राइंग कमांड जो `/GS0 gs` को संदर्भित करता है, निर्दिष्ट अपारदर्शिता के साथ रेंडर होगा।

## चरण 5: ग्राफ़िक्स स्टेट को पेज कंटेंट पर लागू करें (वैकल्पिक)

यदि आप मौजूदा कंटेंट को प्रभावित करना चाहते हैं, तो आपको पेज की कंटेंट स्ट्रीम की शुरुआत में एक कमांड डालना होगा। नीचे दिया गया स्निपेट ग्राफ़िक्स स्टेट ऑपरेटर को प्रीपेंड करने का तरीका दिखाता है।

```csharp
// Retrieve the original content stream
var content = page.Contents[1];

// Insert the graphics state operator at the start of the stream
content.Contents.Insert(0, new CosPdfLiteral("GS0 gs"));
```

*इस चरण का उपयोग कब करें*: यदि PDF में पहले से ड्राइंग कमांड्स हैं और आप उन्हें अर्ध‑पारदर्शी बनाना चाहते हैं, तो ऑपरेटर को प्रीपेंड करें। यदि आप बाद में नए ऑब्जेक्ट्स जोड़ने वाले हैं, तो उन ऑब्जेक्ट्स को बनाते समय सीधे `GS0` को संदर्भित कर सकते हैं।

## चरण 6: संशोधित PDF को सेव करें

अंत में, अपडेटेड डॉक्यूमेंट को डिस्क पर लिखें।

```csharp
var outputPath = @"C:\MyFiles\output.pdf";
doc.Save(outputPath);
```

परिणामी `output.pdf` पहली पेज के फ़िल एलिमेंट्स को 50 % अपारदर्शिता पर दिखाता है जबकि स्ट्रोक पूरी तरह दिखाई देते हैं। प्रभाव की पुष्टि के लिए फ़ाइल को किसी भी PDF व्यूअर में खोलें।

## कई पेजों के लिए PDF अपारदर्शिता बदलना

उसी विधि को किसी भी पेज नंबर के लिए लागू किया जा सकता है। `doc.Pages` पर लूप चलाएँ और चरण 2‑5 दोहराएँ, प्रत्येक पेज के लिए अलग ग्राफ़िक्स स्टेट नाम असाइन करें (जैसे `GS1`, `GS2`)। यहाँ एक संक्षिप्त संस्करण है:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    var pg = doc.Pages[i];
    var editor = new DictionaryEditor(pg.Resources);
    var ext = editor["ExtGState"].ToCosPdfDictionary();

    var gs = CosPdfDictionary.CreateEmptyDictionary(doc);
    gs.Add("CA", new CosPdfNumber(1));
    gs.Add("ca", new CosPdfNumber(0.75)); // 75% fill opacity
    gs.Add("BM", new CosPdfName("Normal"));

    var gsName = $"GS{i - 1}";
    ext.Add(gsName, gs);

    var cnt = pg.Contents[1];
    cnt.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
}
```

यह लूप दोहराव को कम करता है और **PDF अपारदर्शिता बदलने** का पूरा दस्तावेज़ दर्शाता है।

## सामान्य समस्याएँ और सर्वोत्तम‑प्रैक्टिस टिप्स

| समस्या | क्यों होता है | सुझाया गया समाधान |
|-------|----------------|-----------------|
| `ExtGState` एंट्री गायब | कुछ PDF कभी ग्राफ़िक्स‑स्टेट डिक्शनरी नहीं बनाते | `DictionaryEditor` स्वचालित रूप से एक बनाता है; अतिरिक्त कोड की जरूरत नहीं |
| अपारदर्शिता दिखाई नहीं देती | व्यूअर मूल पेज को कैश कर रहा है | व्यूअर कैश साफ़ करें या फ़ाइल को पुनः खोलें |
| ब्लेंड मोड मेल नहीं खाता | डार्क बैकग्राउंड पर `Multiply` उपयोग करने से ऑब्जेक्ट गायब हो सकते हैं | विभिन्न `BM` मान (`Normal`, `Screen`, `Overlay`) आज़माएँ ताकि वांछित विज़ुअल इफ़ेक्ट मिले |
| कई ग्राफ़िक्स स्टेट्स में टकराव | अलग पेजों पर एक ही नाम (`GS0`) पुनः उपयोग करने से पहले की परिभाषा ओवरराइट हो जाती है | प्रत्येक पेज के लिए अनूठा नाम उपयोग करें (`GS0`, `GS1`, …) |

## पूर्ण कार्यशील उदाहरण

नीचे एक स्वतंत्र प्रोग्राम दिया गया है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं। इसमें सभी `using` स्टेटमेंट्स, एरर हैंडलिंग और टिप्पणी शामिल हैं।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class AddTransparencyDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"C:\MyFiles\input.pdf";
        const string outputPath = @"C:\MyFiles\output.pdf";

        // Load the PDF
        var doc = new Document(inputPath);

        // Process each page
        for (int pageIndex = 1; pageIndex <= doc.Pages.Count; pageIndex++)
        {
            var page = doc.Pages[pageIndex];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Create a graphics state with 60% fill opacity
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);
            graphicsState.Add("CA", new CosPdfNumber(1));               // stroke opacity
            graphicsState.Add("ca", new CosPdfNumber(0.6));             // fill opacity
            graphicsState.Add("BM", new CosPdfName("Normal"));         // blend mode

            // Unique name for this page
            string gsName = $"GS{pageIndex - 1}";
            extGState.Add(gsName, graphicsState);

            // Prepend the graphics state operator to the page content
            var content = page.Contents[1];
            content.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
        }

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"PDF saved with transparency at: {outputPath}");
    }
}
```

**अपेक्षित आउटपुट**: जब आप `output.pdf` खोलेंगे, तो प्रत्येक पेज पर किसी भी फ़िल्ड शैप, टेक्स्ट या इमेज 60 % अपारदर्शिता के साथ दिखेगी, जबकि बॉर्डर पूरी तरह अपारदर्शी रहेंगे। यह विज़ुअल परिवर्तन तुरंत दिखता है और Adobe Acrobat, Edge, Chrome या किसी भी PDF व्यूअर में काम करता है जो PDF ग्राफ़िक्स स्टेट को सपोर्ट करता है।

## निष्कर्ष

अब आप Aspose.PDF for C# का उपयोग करके **PDF में ट्रांसपेरेंसी जोड़ना** जानते हैं। ट्यूटोरियल ने डॉक्यूमेंट लोड करना, पेज की रिसोर्स डिक्शनरी को एडिट करना, कस्टम ग्राफ़िक्स स्टेट बनाना, और संशोधित फ़ाइल को सेव करना कवर किया। आपने **PDF अपारदर्शिता बदलना** एकल या कई पेजों के लिए सीखा, साथ ही सामान्य गलतियों से बचने के व्यावहारिक टिप्स भी प्राप्त किए।

आगे, संबंधित विषयों का अन्वेषण करें जैसे:

* वैरिएबल अपारदर्शिता के साथ इमेज वॉटरमार्क जोड़ना
* रचनात्मक इफ़ेक्ट्स के लिए विभिन्न ब्लेंड मोड (`Multiply`, `Screen`) का उपयोग
* PDF एनोटेशन के साथ ट्रांसपेरेंसी को संयोजित करना

इन विविधताओं के साथ प्रयोग करें ताकि आप अपने प्रोजेक्ट की विज़ुअल आवश्यकताओं के अनुसार PDF आउटपुट को कस्टमाइज़ कर सकें। कोडिंग का आनंद लें!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में माहिर हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [How to add graphics state pdf and control transparency with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [How to set opacity in a PDF and how to change blend mode with Aspose.Pdf](/pdf/hongkong/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/)
- [How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}