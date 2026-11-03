---
category: general
date: 2026-10-10
description: Aspose.PDF का उपयोग करके C# में PDF की पारदर्शिता कैसे बदलें, सीखें।
  यह चरण‑दर‑चरण गाइड PDF अपारदर्शिता, ग्राफ़िक्स स्टेट संपादन, और ExtGState शब्दकोश
  संशोधन को कवर करता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.PDF graphics state
- PDF opacity
- C# PDF manipulation
- ExtGState dictionary
language: hi
lastmod: 2026-10-10
og_description: Aspose.PDF के साथ C# में PDF की पारदर्शिता बदलें। PDF अपारदर्शिता,
  ग्राफ़िक्स स्टेट ऑब्जेक्ट्स और ExtGState डिक्शनरी को संपादित करने के लिए इस संक्षिप्त
  ट्यूटोरियल का पालन करें।
og_image_alt: Screenshot showing C# code that changes PDF transparency using Aspose.PDF
og_title: C# में PDF की पारदर्शिता बदलें – पूर्ण Aspose.PDF गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to change PDF transparency in C# using Aspose.PDF. This step‑by‑step
    guide covers PDF opacity, graphics state editing, and ExtGState dictionary manipulation.
  headline: How to change PDF transparency in C# with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF transparency
- Graphics state
title: C# में Aspose.PDF के साथ PDF की पारदर्शिता कैसे बदलें
url: /hi/net/programming-with-operators/how-to-change-pdf-transparency-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose.PDF के साथ PDF की पारदर्शिता कैसे बदलें

यदि आपको C# प्रोजेक्ट में **PDF की पारदर्शिता बदलनी** है, तो यह गाइड एक पूर्ण, तैयार‑चलाने योग्य समाधान दिखाता है। PDF की ग्राफ़िक्स स्टेट को संपादित करके आप स्ट्रोक अपारदर्शिता, फ़िल अपारदर्शिता और ब्लेंड मोड को नियंत्रित कर सकते हैं, बिना दस्तावेज़ को फिर से बनाने के।  

आप देखेंगे कि कैसे PDF लोड करें, **ExtGState डिक्शनरी** को संशोधित करें, इच्छित **PDF अपारदर्शिता** सेट करें, और परिणाम को सहेजें—सभी Aspose.PDF लाइब्रेरी का उपयोग करके। कोई बाहरी टूल आवश्यक नहीं है, और कोड .NET 6+ के साथ काम करता है।

## आवश्यकताएँ

- Visual Studio 2022 (या कोई भी C# IDE)  
- .NET 6 या बाद का रनटाइम  
- Aspose.PDF for .NET NuGet पैकेज (`Install-Package Aspose.PDF`)  
- एक PDF फ़ाइल जिसका नाम `input.pdf` है, किसी ऐसे फ़ोल्डर में जहाँ आपके पास पहुँच हो  

इन सबको तैयार रखने से ट्यूटोरियल बिना किसी निर्भरता की कमी के चल पाएगा।

## चरण 1: PDF दस्तावेज़ लोड करें

पहला कार्य मौजूदा PDF फ़ाइल को खोलना है। Aspose.PDF PDF को एक `Document` ऑब्जेक्ट के रूप में प्रस्तुत करता है, जो पेज, रिसोर्सेज़ और लो‑लेवल डिक्शनरीज़ तक पूरी पहुँच देता है।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Cosmos;

// Load the source PDF
var document = new Document("YOUR_DIRECTORY/input.pdf");
```

*क्यों महत्वपूर्ण है:* फ़ाइल को लोड करने से एक इन‑मेमोरी मॉडल बनता है जिसे आप संशोधित कर सकते हैं। `Document` क्लास PDF संरचना को एब्स्ट्रैक्ट करती है जबकि फिर भी लो‑लेवल ऑब्जेक्ट्स को उजागर करती है, जिनकी पारदर्शिता बदलने के लिए आवश्यकता होती है।

## चरण 2: पहला पेज और उसकी रिसोर्स डिक्शनरी प्राप्त करें

पारदर्शिता सेटिंग्स पेज की रिसोर्स डिक्शनरी में **ExtGState** एंट्री के तहत रहती हैं। आपको वह डिक्शनरी प्राप्त करनी होगी इससे पहले कि आप ग्राफ़िक्स स्टेट जोड़ या संपादित कर सकें।

```csharp
// Get the first page (pages are 1‑based)
var page = document.Pages[1];

// The DictionaryEditor simplifies access to resource entries
var resourcesEditor = new DictionaryEditor(page.Resources);
```

*क्यों महत्वपूर्ण है:* `Resources` कलेक्शन में फ़ॉन्ट्स, इमेजेज़ और ग्राफ़िक्स स्टेट्स होते हैं जो पेज द्वारा उपयोग किए जाते हैं। इसे संपादित करके आप केवल लक्षित पेज को प्रभावित करते हैं, जबकि दस्तावेज़ के बाकी हिस्से अपरिवर्तित रहते हैं।

## चरण 3: ExtGState डिक्शनरी तक पहुँचें (या बनाएं)

यदि PDF में पहले से एक `ExtGState` डिक्शनरी मौजूद है, तो आप उसे पुनः उपयोग कर सकते हैं; अन्यथा, पहला एंट्री जोड़ने पर Aspose.PDF एक खाली डिक्शनरी बना देगा।

```csharp
// Retrieve the ExtGState dictionary; create if missing
var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
               ?? new CosPdfDictionary(document);
```

*क्यों महत्वपूर्ण है:* `ExtGState` डिक्शनरी **ग्राफ़िक्स स्टेट ऑब्जेक्ट्स** रखती है। प्रत्येक ऑब्जेक्ट स्ट्रोक अपारदर्शिता (`CA`), फ़िल अपारदर्शिता (`ca`) और ब्लेंड मोड (`BM`) जैसे पैरामीटर परिभाषित करता है। इन मानों को बदलने से PDF के पारदर्शी तत्वों के रेंडरिंग पर सीधा असर पड़ता है।

## चरण 4: इच्छित पारदर्शिता के साथ नया ग्राफ़िक्स स्टेट परिभाषित करें

एक नया ग्राफ़िक्स स्टेट (`GS0`) बनाएँ और उसके पैरामीटर सेट करें। नीचे दिया गया उदाहरण 100 % स्ट्रोक अपारदर्शिता, 50 % फ़िल अपारदर्शिता और मानक “Normal” ब्लेंड मोड सेट करता है।

```csharp
// Name for the new graphics state
string graphicsStateName = "GS0";

// Create an empty dictionary for the graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

// Populate the dictionary with transparency parameters
var graphicsStateEntries = new[]
{
    // Stroke opacity (CA) – 1 = fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // Fill opacity (ca) – 0.5 = 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – "Normal" is the most common mode
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*क्यों महत्वपूर्ण है:* `CA` एंट्री स्ट्रोक (लाइन, बॉर्डर) के ब्लेंड को नियंत्रित करती है, जबकि `ca` फ़िल (शेप, टेक्स्ट) को प्रभावित करती है। इन मानों को समायोजित करना **PDF की पारदर्शिता बदलने** का मूल है। ब्लेंड मोड निर्धारित करता है कि पारदर्शी सामग्री नीचे की ग्राफ़िक्स के साथ कैसे इंटरैक्ट करती है।

## चरण 5: नया ग्राफ़िक्स स्टेट ExtGState डिक्शनरी में डालें

अब ग्राफ़िक्स स्टेट को पेज की `ExtGState` कलेक्शन में जोड़ें और सुनिश्चित करें कि पेज इसे रेफ़रेंस करता है।

```csharp
// Add the new graphics state to the ExtGState dictionary
extGState.Add(graphicsStateName, newGraphicsState);

// Update the Resources dictionary with the modified ExtGState
resourcesEditor["ExtGState"] = extGState;
```

*क्यों महत्वपूर्ण है:* एंट्री जोड़ने से ग्राफ़िक्स स्टेट PDF में रजिस्टर हो जाता है। कोई भी बाद का ड्रॉइंग ऑपरेशन जो `GS0` को चुनता है, वह आपके द्वारा परिभाषित अपारदर्शिता मानों का उपयोग करेगा।

## चरण 6: ग्राफ़िक्स स्टेट को पेज कंटेंट पर लागू करें (वैकल्पिक लेकिन सामान्य)

यदि आप चाहते हैं कि पेज की मौजूदा सामग्री नई पारदर्शिता अपनाए, तो आपको `gs` ऑपरेटर को प्रीपेंड करना होगा जो ग्राफ़िक्स स्टेट को चुनता है। नीचे पेज की कंटेंट्स में इस ऑपरेटर को प्रीपेंड करने का एक सरल तरीका दिया गया है।

```csharp
// Create a content stream that selects the new graphics state
var selectStateOperator = new GraphicsStateOperator(graphicsStateName);

// Insert the operator at the beginning of the page's content
page.Contents.Insert(0, selectStateOperator);
```

*क्यों महत्वपूर्ण है:* इस चरण के बिना, ग्राफ़िक्स स्टेट मौजूद रहेगा लेकिन कभी उपयोग नहीं होगा। `gs` ऑपरेटर (`GraphicsStateOperator`) PDF रेंडरर को बताता है कि परिभाषित अपारदर्शिता सेटिंग्स को उसके बाद आने वाली सभी चीज़ों पर लागू किया जाए।

## चरण 7: संशोधित PDF को सहेजें

अंत में, अपडेटेड दस्तावेज़ को डिस्क पर लिखें।

```csharp
document.Save("YOUR_DIRECTORY/output.pdf");
```

परिणामी `output.pdf` फ़ाइल आपके द्वारा निर्दिष्ट फ़िल अपारदर्शिता (50 % पारदर्शी) के साथ रेंडर होगी, जबकि स्ट्रोक पूरी तरह अपारदर्शी रहेंगे।

---

## पूर्ण स्रोत कोड (चलाने योग्य)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cosmos;
using System.Collections.Generic;

class ChangePdfTransparency
{
    static void Main()
    {
        // 1️⃣ Load the PDF
        var document = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Get first page and its resource dictionary
        var page = document.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3️⃣ Access (or create) the ExtGState dictionary
        var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                       ?? new CosPdfDictionary(document);

        // 4️⃣ Define a new graphics state (GS0) with desired opacity
        string gsName = "GS0";
        var newGs = CosPdfDictionary.CreateEmptyDictionary(document);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGs.Add(e);

        // 5️⃣ Add the graphics state to ExtGState and update resources
        extGState.Add(gsName, newGs);
        resourcesEditor["ExtGState"] = extGState;

        // 6️⃣ Apply the graphics state to existing content (optional)
        var gsOperator = new GraphicsStateOperator(gsName);
        page.Contents.Insert(0, gsOperator);

        // 7️⃣ Save the modified PDF
        document.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**अपेक्षित आउटपुट:** `output.pdf` को Adobe Acrobat या किसी भी PDF व्यूअर में खोलने पर पहले पेज पर सभी फ़िल्ड शेप्स 50 % अपारदर्शी दिखेंगे, जबकि स्ट्रोक पूरी तरह अपारदर्शी रहेंगे। यह दृश्य परिवर्तन पुष्टि करता है कि आपने सफलतापूर्वक **PDF की पारदर्शिता बदल दी** है।

---

## सामान्य प्रश्न और किनारे के मामलों

| प्रश्न | उत्तर |
|----------|--------|
| *क्या मैं पूरे पेज के बजाय किसी विशिष्ट ऑब्जेक्ट की पारदर्शिता बदल सकता हूँ?* | हाँ। पेज की शुरुआत में `gs` ऑपरेटर डालने के बजाय, उसे उस ड्रॉइंग कमांड से ठीक पहले रखें जो उस ऑब्जेक्ट को लक्षित करता है। `page.Contents.Insert(index, gsOperator)` का उपयोग करें जहाँ `index` इच्छित स्थान की ओर इशारा करता है। |
| *यदि PDF में पहले से “GS0” नाम का ExtGState एंट्री है तो क्या करें?* | एक अनोखा नाम चुनें (जैसे `GS1`) या मौजूदा एंट्री को ओवरराइट करें यदि आप उसे बदलना चाहते हैं। डिक्शनरी कुंजी पेज की रिसोर्सेज़ के भीतर अद्वितीय होनी चाहिए। |
| *क्या `ca` मान 0‑1 तक सीमित है?* | सही। `ca` (फ़िल अपारदर्शिता) और `CA` (स्ट्रोक अपारदर्शिता) का मान 0 (पूरी तरह पारदर्शी) से 1 (पूरी तरह अपारदर्शी) के बीच होना चाहिए। इस रेंज से बाहर के मान क्लैंप हो जाते हैं। |
| *क्या यह PDF/A या PDF/X अनुपालन वाले PDFs के साथ काम करता है?* | ग्राफ़िक्स स्टेट को संशोधित करने से सख्त अनुपालन टूट सकता है। यदि आपको अनुपालन बनाए रखना है, तो आउटपुट को PDF/A वैलिडेटर से सत्यापित करें और डिक्शनरी को तदनुसार समायोजित करें (जैसे `/PDFXConformance` एंट्री जोड़ें)। |
| *क्या मैं “Multiply” जैसे अलग ब्लेंड मोड सेट कर सकता हूँ?* | बिल्कुल। `new CosPdfName("Normal")` को `new CosPdfName("Multiply")` या PDF स्पेक में परिभाषित किसी भी ब्लेंड मोड से बदल दें। |

---

## टिप्स और सर्वोत्तम प्रथाएँ (E‑E‑A‑T)

- **प्रो टिप:** यदि आप कई पेजों को संशोधित करने वाले हैं तो पहली बार संशोधन के बाद `ExtGState` डिक्शनरी को कैश करें; इससे ऑब्जेक्ट निर्माण ओवरहेड घटेगा।  
- **ध्यान रखें:** विभिन्न पेजों में एक ही ग्राफ़िक्स स्टेट नाम को बिना रिसोर्स अपडेट किए पुनः उपयोग करने से अप्रत्याशित अपारदर्शिता मिश्रण हो सकता है। नाम को पेज‑विशिष्ट रखें या ग्लोबली यूनिक आइडेंटिफ़ायर उपयोग करें।  
- **प्रदर्शन:** बड़े PDFs के लिए पेजों को समानांतर (`Parallel.ForEach`) में प्रोसेस करने पर विचार करें, लेकिन `Document` ऑब्जेक्ट तक पहुँच को सिंक्रनाइज़ रखें ताकि थ्रेड‑सेफ़्टी समस्याएँ न आएँ।  
- **टेस्टिंग:** कम से कम दो व्यूअर्स (Adobe Acrobat Reader और ब्राउज़र PDF प्लगइन) में पारदर्शिता परिवर्तन की जाँच करें, क्योंकि कुछ व्यूअर्स ब्लेंड मोड को अलग‑अलग हैंडल कर सकते हैं।

---

## निष्कर्ष

अब आप Aspose.PDF के साथ **PDF की पारदर्शिता बदलना** C# में जानते हैं, `ExtGState` डिक्शनरी को संपादित करके। इस ट्यूटोरियल में PDF लोड करना, कस्टम ग्राफ़िक्स स्टेट बनाना, उसे पेज कंटेंट पर लागू करना, और अपडेटेड फ़ाइल सहेजना शामिल था।  

अब आप अधिक उन्नत **C# PDF मैनिपुलेशन** विषयों की खोज कर सकते हैं, जैसे कई ग्राफ़िक्स स्टेट्स को लेयर करना, विभिन्न **PDF अपारदर्शिता** मानों को ऑब्जेक्ट‑वाइज़ लागू करना, या Aspose.PDF के हाई‑लेवल API का उपयोग करके टेक्स्ट और इमेज इंसर्शन करना।

अन्य ब्लेंड मोड, अपारदर्शिता स्तर, या केवल चयनित पेजों पर ग्राफ़िक्स स्टेट लागू करने के साथ प्रयोग करने में संकोच न करें। यदि कोई समस्या आती है, तो Aspose.PDF दस्तावेज़ PDF ऑब्जेक्ट मॉडल और ग्राफ़िक्स स्टेट हैंडलिंग पर गहरी जानकारी प्रदान करता है।

हैप्पी कोडिंग!


## अगला आप क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच का पता लगा सकते हैं।

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Add Transparency to PDF with Aspose PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}