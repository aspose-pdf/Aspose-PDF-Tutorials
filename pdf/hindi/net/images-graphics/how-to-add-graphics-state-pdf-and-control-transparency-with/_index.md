---
category: general
date: 2026-09-05
description: Aspose.PDF का उपयोग करके ग्राफ़िक्स स्टेट PDF में ट्रांसपेरेंसी सेट करना
  सीखें। यह चरण‑दर‑चरण गाइड यह भी दिखाता है कि कैसे ट्रांसपेरेंसी PDF जोड़ें और PDF
  की ट्रांसपेरेंसी को प्रभावी ढंग से संशोधित करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- how to add transparency pdf
- modify pdf transparency
language: hi
lastmod: 2026-09-05
og_description: Aspose.PDF का उपयोग करके ग्राफ़िक्स स्टेट PDF जोड़ें। इस गाइड का पालन
  करके जानें कि कैसे PDF में ट्रांसपेरेंसी जोड़ें और कुछ ही C# कोड लाइनों में PDF
  की ट्रांसपेरेंसी को संशोधित करें।
og_image_alt: Screenshot of C# code that adds graphics state pdf to a PDF document
og_title: Aspose.PDF के साथ ग्राफ़िक्स स्टेट PDF जोड़ें – C# में पारदर्शिता नियंत्रित
  करें
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to add graphics state pdf using Aspose.PDF to set transparency.
    This step‑by‑step guide also shows how to add transparency pdf and modify pdf
    transparency efficiently.
  headline: How to add graphics state pdf and control transparency with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- PDF graphics state
- PDF transparency
- C# PDF manipulation
title: Aspose.PDF के साथ ग्राफ़िक्स स्टेट PDF कैसे जोड़ें और पारदर्शिता को नियंत्रित
  करें
url: /hi/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF के साथ ग्राफ़िक्स स्टेट PDF जोड़ना और ट्रांसपेरेंसी नियंत्रित करना

यदि आपको मौजूदा दस्तावेज़ में **add graphics state pdf** जोड़ने की आवश्यकता है, तो यह गाइड आपको सटीक चरण दिखाता है। आप Aspose.PDF for .NET का उपयोग करके ट्रांसपेरेंसी PDF कैसे जोड़ें, और मूल लेआउट को बिगाड़े बिना PDF ट्रांसपेरेंसी को कैसे संशोधित करें, यह देखेंगे।

आगे के अनुभागों में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे, प्रत्येक पंक्ति का महत्व समझाएंगे, और सामान्य समस्याओं पर चर्चा करेंगे। अंत तक आप किसी भी PDF पेज में कस्टम ग्राफ़िक्स स्टेट्स—जैसे स्ट्रोक और फ़िल अल्फा वैल्यूज़—एंबेड कर सकेंगे।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)
* एक वैध Aspose.PDF for .NET लाइसेंस या अस्थायी इवैल्यूएशन कुंजी
* Visual Studio 2022 (या कोई भी C# एडिटर जो आप पसंद करते हैं)
* एक इनपुट PDF फ़ाइल (`input.pdf`) जिसके संशोधित करने के अधिकार आपके पास हैं

`Aspose.Pdf` के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है।

## चरण 1: PDF दस्तावेज़ लोड करें

पहला कार्य स्रोत PDF को खोलना है। Aspose.PDF फ़ाइल को एक `Document` ऑब्जेक्ट में लपेटता है, जो आपको पृष्ठों, संसाधनों और लो‑लेवल PDF संरचनाओं तक पहुँच प्रदान करता है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.Xmp;

string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document inside a using block so resources are released automatically.
using (var doc = new Document(inputPath))
{
    // The rest of the code lives inside this block.
}
```

**क्यों यह महत्वपूर्ण है:** `using` स्टेटमेंट के साथ फ़ाइल खोलने से यह सुनिश्चित होता है कि अपवाद होने पर भी फ़ाइल हैंडल बंद हो जाता है। `Document` ऑब्जेक्ट क्रॉस‑रेफ़रेंस टेबल भी लोड करता है, जिससे बाद में लो‑लेवल डिक्शनरीज़ को संपादित किया जा सकता है।

## चरण 2: पहले पृष्ठ के रिसोर्स डिक्शनरी तक पहुँचें

प्रत्येक PDF पृष्ठ में एक *Resources* डिक्शनरी होती है जो फ़ॉन्ट्स, XObjects, और ग्राफ़िक्स स्टेट्स (`ExtGState`) को संग्रहीत करती है। नया ग्राफ़िक्स स्टेट इंजेक्ट करने के लिए, हमें पहले इस डिक्शनरी को प्राप्त करना होगा।

```csharp
// Inside the using block
Page page = doc.Pages[1];                     // Get the first page (pages are 1‑based)
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

**क्यों यह महत्वपूर्ण है:** `ExtGState` वह कुंजी है जिसके तहत ग्राफ़िक्स स्टेट ऑब्जेक्ट्स संग्रहीत होते हैं। यदि पृष्ठ में अभी तक `ExtGState` एंट्री नहीं है, तो Aspose.PDF स्वचालित रूप से एक खाली डिक्शनरी बना देता है, इसलिए कोड दोनों मामलों में काम करता है।

## चरण 3: नया ग्राफ़िक्स स्टेट डिक्शनरी बनाएं

ग्राफ़िक्स स्टेट डिक्शनरी यह निर्धारित करती है कि ड्राइंग ऑपरेशन्स कैसे व्यवहार करेंगे। ट्रांसपेरेंसी के लिए हमें `CA` (stroke alpha), `ca` (fill alpha), और वैकल्पिक रूप से ब्लेंड मोड (`BM`) की आवश्यकता होती है। नीचे दिया गया कोड उस डिक्शनरी को बनाता है।

```csharp
// Create an empty COS dictionary that will become our new graphics state.
CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);

// Define the entries we want: 1.0 stroke opacity, 0.5 fill opacity, Normal blend mode.
var entries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke alpha (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill alpha (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

foreach (var entry in entries)
{
    newGs.Add(entry);
}
```

**क्यों यह महत्वपूर्ण है:**  
* `CA` स्ट्रोक किए गए पाथ्स (लाइन, बॉर्डर) की अपारदर्शिता नियंत्रित करता है।  
* `ca` भरे हुए ऑब्जेक्ट्स (शेप्स, टेक्स्ट) की अपारदर्शिता नियंत्रित करता है।  
* `BM` ब्लेंड मोड चुनता है; “Normal” सबसे सामान्य है और सभी PDF व्यूअर्स के साथ काम करता है।

### किनारा मामला: `ExtGState` एंट्री अनुपलब्ध

यदि `page.Resources` में `ExtGState` डिक्शनरी नहीं है, तो `dictEditor["ExtGState"]` `null` लौटाता है। ऐसी स्थिति में आप इसे मैन्युअली बना सकते हैं:

```csharp
if (extGState == null)
{
    extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
    dictEditor["ExtGState"] = extGState;
}
```

इस गार्ड को शामिल करने से ट्यूटोरियल उन PDFs के लिए मजबूत बन जाता है जिन्होंने पहले कभी कस्टम ग्राफ़िक्स स्टेट का उपयोग नहीं किया था।

## चरण 4: नया ग्राफ़िक्स स्टेट रिसोर्स डिक्शनरी में जोड़ें

अब हम नई बनाई गई डिक्शनरी को एक नाम (जैसे `GS0`) से बाइंड करते हैं। कंटेंट स्ट्रीम्स इस नाम को संदर्भित करके परिभाषित ट्रांसपेरेंसी लागू कर सकते हैं।

```csharp
// Register the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);
```

**क्यों यह महत्वपूर्ण है:** PDF कंटेंट ऑपरेटर्स जैसे `gs` एक नामित ग्राफ़िक्स स्टेट पर स्विच करते हैं। `GS0` जोड़ने से आप बाद की कंटेंट स्ट्रीम्स को ` /GS0 gs ` का उपयोग करके ट्रांसपेरेंसी सेटिंग्स सक्रिय करने में सक्षम बनाते हैं।

## चरण 5: (वैकल्पिक) मौजूदा कंटेंट पर ग्राफ़िक्स स्टेट लागू करें

यदि आप चाहते हैं कि वर्तमान पृष्ठ के मौजूदा तत्व ट्रांसपेरेंट हो जाएँ, तो आप पृष्ठ की कंटेंट स्ट्रीम की शुरुआत में एक `gs` ऑपरेटर जोड़ सकते हैं। यह चरण वैकल्पिक है क्योंकि कई उपयोग‑केस केवल नए जोड़े गए ऑब्जेक्ट्स के लिए ग्राफ़िक्स स्टेट की आवश्यकता रखते हैं।

```csharp
// Prepend "GS0" graphics state to the page’s content
page.Contents.Insert(0, new OperatorGraphicsState("GS0"));
```

**क्यों यह महत्वपूर्ण है:** इस पंक्ति के बिना पृष्ठ अपनी मूल उपस्थिति बनाए रखेगा। ऑपरेटर जोड़ने से यह सुनिश्चित होता है कि ऑपरेटर के बाद ड्रॉ किया गया सब कुछ नई अपारदर्शिता मानों को विरासत में लेता है।

## चरण 6: संशोधित PDF को सहेजें

अंत में, अपडेटेड दस्तावेज़ को डिस्क पर लिखें। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई जगह पर लिख सकते हैं।

```csharp
string outputPath = @"YOUR_DIRECTORY\output.pdf";
doc.Save(outputPath);
```

**क्यों यह महत्वपूर्ण है:** `doc.Save` संशोधित क्रॉस‑रेफ़रेंस टेबल, रिसोर्स डिक्शनरीज़, और किसी भी नई कंटेंट स्ट्रीम को सीरियलाइज़ करता है, जिससे एक वैध PDF बनता है जिसे कोई भी व्यूअर खोल सकता है।

## पूर्ण कार्यशील उदाहरण

सभी भागों को मिलाकर, यहाँ एक स्व-निहित प्रोग्राम है जिसे आप कॉपी, पेस्ट और चलाने के लिए उपयोग कर सकते हैं।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Xmp;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Cos;

class AddGraphicsStateExample
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        using (var doc = new Document(inputPath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Access the first page's resource dictionary
            // -----------------------------------------------------------------
            Page page = doc.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary();

            // Ensure ExtGState exists
            if (extGState == null)
            {
                extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
                dictEditor["ExtGState"] = extGState;
            }

            // -----------------------------------------------------------------
            // 3️⃣ Create a new graphics state (transparency settings)
            // -----------------------------------------------------------------
            CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries) newGs.Add(entry);

            // -----------------------------------------------------------------
            // 4️⃣ Register the graphics state as "GS0"
            // -----------------------------------------------------------------
            extGState.Add("GS0", newGs);

            // -----------------------------------------------------------------
            // 5️⃣ (Optional) Apply the graphics state to existing content
            // -----------------------------------------------------------------
            page.Contents.Insert(0, new OperatorGraphicsState("GS0"));

            // -----------------------------------------------------------------
            // 6️⃣ Save the modified PDF
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved with new graphics state at: {outputPath}");
        }
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने के बाद, `output.pdf` को Adobe Acrobat Reader या किसी भी PDF व्यूअर में खोलें। पहले पृष्ठ पर कोई भी भरे हुए आकार (जैसे, रंगीन आयत) **50 % अपारदर्शिता** के साथ दिखना चाहिए, जबकि स्ट्रोक पूरी तरह अपारदर्शी रहेंगे। यदि आपने वैकल्पिक `gs` ऑपरेटर जोड़ा है, तो उस पृष्ठ की *सभी* मौजूदा सामग्री समान ट्रांसपेरेंसी विरासत में लेती है।

## सामान्य प्रश्न और समस्या निवारण

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मैं एक से अधिक ग्राफ़िक्स स्टेट जोड़ सकता हूँ?** | हां। अतिरिक्त डिक्शनरीज़ बनाएं (जैसे, `GS1`, `GS2`) और विभिन्न `gs` ऑपरेटर्स के साथ उनका संदर्भ दें। |
| **यदि PDF पहले से `GS0` जैसा नाम उपयोग कर रहा है तो क्या करें?** | एक अद्वितीय नाम चुनें (जैसे, `MyGS`) या `extGState.Keys` के साथ मौजूदा कुंजियों की जाँच करें। |
| **क्या यह एन्क्रिप्टेड PDFs के साथ काम करता है?** | दस्तावेज़ को सही पासवर्ड के साथ खोलना आवश्यक है। उपयोग करें `new Document(inputPath, new LoadOptions { Password = "pwd" })`। |
| **क्या ये परिवर्तन अन्य पृष्ठों को प्रभावित करेंगे?** | नहीं। ग्राफ़िक्स स्टेट केवल उस पृष्ठ के रिसोर्सेज़ में जोड़ी जाती है जिसे आप संपादित करते हैं। सभी पृष्ठों को प्रभावित करने के लिए, प्रत्येक पृष्ठ के लिए प्रक्रिया दोहराएँ या डिक्शनरी को *डॉक्यूमेंट‑लेवल* रिसोर्सेज़ में जोड़ें। |
| **क्या इसका प्रदर्शन पर कोई असर पड़ता है?** | एकल ग्राफ़िक्स स्टेट जोड़ना नगण्य है। कई पृष्ठों वाले बड़े PDFs को लूप की आवश्यकता हो सकती है, लेकिन ऑपरेशन अभी भी O(number of pages) रहता है। |

## प्रो टिप्स

* **ग्राफ़िक्स स्टेट्स को पुन: उपयोग करें:** यदि आपको कई पृष्ठों पर समान ट्रांसपेरेंसी चाहिए, तो डिक्शनरी को *डॉक्यूमेंट* रिसोर्सेज़ (`doc.Resources`) में जोड़ें और प्रत्येक पृष्ठ से उसका संदर्भ दें। इससे फ़ाइल आकार कम होता है।
* **ब्लेंड मोड्स:** रचनात्मक प्रभावों के लिए अन्य `BM` मानों जैसे `Multiply`, `Screen`, या `Overlay` के साथ प्रयोग करें। सभी व्यूअर्स हर ब्लेंड मोड को सपोर्ट नहीं करते, इसलिए अपने लक्षित दर्शकों के साथ परीक्षण करें।
* **टेस्टिंग:** हमेशा मूल और संशोधित PDFs को साइड‑बाय‑साइड तुलना करें। ऐसे डिफ़ टूल का उपयोग करें जो PDFs को रेंडर कर सके (जैसे, `DiffPDF`) यह सुनिश्चित करने के लिए कि केवल इच्छित परिवर्तन हुए हैं।

## अगले कदम

अब जब आप जानते हैं **how to add transparency pdf** और **modify pdf transparency**, आप संबंधित विषयों का अन्वेषण कर सकते हैं:

* **Add graphics state pdf** ओवरप्रिंट और हाफटोन इफ़ेक्ट्स के लिए
* **Embedding images with custom opacity** `ImageFragment` और ग्राफ़िक्स स्टेट का उपयोग करके
* **Batch processing** फ़ोल्डर में कई PDFs को समानांतरता के साथ प्रोसेस करना ताकि थ्रूपुट बढ़े
* **Using Aspose.PDF’s high‑level API** (`PdfSaveOptions`, `PdfPageEditor`) अधिक जटिल वर्कफ़्लो के लिए

विभिन्न अल्फा वैल्यूज़ के साथ प्रयोग करने में संकोच न करें

## अब आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [Aspose का उपयोग करके PDF में ट्रांसपेरेंसी जोड़ें – पूर्ण C# गाइड](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Aspose.PDF .NET का उपयोग करके PDF में टेक्स्ट स्टैम्प कैसे जोड़ें: व्यापक गाइड](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Aspose.PDF for .NET का उपयोग करके PDFs में इमेजेज़ कैसे जोड़ें: चरण‑दर‑चरण गाइड](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}