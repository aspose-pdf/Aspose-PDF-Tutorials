---
"description": "जानें कि .NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइल से हाइपरलिंक टेक्स्ट को आसानी से कैसे निकाला जाए। चरण-दर-चरण मार्गदर्शिका और कोड शामिल है।"
"linktitle": "हाइपरलिंक टेक्स्ट को PDF फ़ाइल में प्राप्त करें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "हाइपरलिंक टेक्स्ट को PDF फ़ाइल में प्राप्त करें"
"url": "/hi/net/programming-with-links-and-actions/get-hyperlink-text/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# हाइपरलिंक टेक्स्ट को PDF फ़ाइल में प्राप्त करें

## परिचय

जब पीडीएफ फाइलों के साथ काम करने की बात आती है, तो हाइपरलिंक निकालना एक कठिन काम हो सकता है। चाहे आप डेवलपर हों, डेटा विश्लेषक हों, या कोई ऐसा व्यक्ति जो अपने दस्तावेज़ प्रसंस्करण को सुव्यवस्थित करना चाहता हो, सही टूलकिट होने से बहुत फ़र्क पड़ सकता है। .NET के लिए Aspose.PDF दर्ज करें—PDF फ़ाइलों को आसानी से मैनिपुलेट करने के लिए आपकी पसंदीदा लाइब्रेरी। इस लेख में, हम चरण-दर-चरण यह पता लगाएंगे कि PDF फ़ाइल से हाइपरलिंक टेक्स्ट कैसे निकाला जाता है। तो, तैयार हो जाइए और PDF की जटिल दुनिया में गोता लगाएँ!

## आवश्यक शर्तें

इससे पहले कि हम पीडीएफ से हाइपरलिंक टेक्स्ट निकालने की अपनी यात्रा शुरू करें, कुछ आवश्यक चीजें हैं जिनकी आपको शुरुआत करने की आवश्यकता होगी:

1. C# का बुनियादी ज्ञान: C# प्रोग्रामिंग की समझ होना उपयोगी है क्योंकि हम कुछ कोड लिखेंगे।
2. Visual Studio स्थापित: सुनिश्चित करें कि आपके मशीन पर Visual Studio स्थापित है। यह कोड लिखने और परीक्षण करने के लिए हमारा खेल का मैदान होगा।
3. .NET के लिए Aspose.PDF: आपके पास Aspose.PDF लाइब्रेरी होनी चाहिए। आप इसे यहाँ से डाउनलोड कर सकते हैं। [साइट](https://releases.aspose.com/pdf/net/) या उपलब्ध निःशुल्क परीक्षण के साथ शुरू करें [यहाँ](https://releases.aspose.com/).

## पैकेज आयात करें

एक बार जब आप सब कुछ सेट कर लें, तो सबसे पहले हमें आवश्यक पैकेज आयात करने होंगे। यहाँ बताया गया है कि कैसे:

### एक नया प्रोजेक्ट बनाएं

विजुअल स्टूडियो खोलकर और एक नया C# कंसोल अनुप्रयोग प्रोजेक्ट बनाकर आरंभ करें।

### Aspose.PDF संदर्भ जोड़ें

1. समाधान एक्सप्लोरर में अपने प्रोजेक्ट पर राइट-क्लिक करें।
2. "NuGet पैकेज प्रबंधित करें" चुनें.
3. निम्न को खोजें `Aspose.PDF` और इसे स्थापित करें.
4. यह आपको Aspose.PDF द्वारा प्रदान की गई सभी अद्भुत कक्षाओं और विधियों तक पहुंचने की अनुमति देगा।

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections;
using Aspose.Pdf.Annotations;
```

ठीक है, चलिए रोमांचक भाग पर आते हैं - एक PDF दस्तावेज़ से हाइपरलिंक टेक्स्ट निकालना! यहाँ बताया गया है कि इसे चरण दर चरण कैसे किया जाता है।

## चरण 1: अपना दस्तावेज़ पथ सेट करें

हमारे कोड में, हमें सबसे पहले उस पथ को निर्दिष्ट करना होगा जहाँ हमारा PDF दस्तावेज़ स्थित है। यह एक स्ट्रिंग वैरिएबल का उपयोग करके किया जाता है। 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

प्रतिस्थापित करना सुनिश्चित करें `"YOUR DOCUMENT DIRECTORY"` आपकी PDF फ़ाइल के वास्तविक पथ के साथ। उदाहरण के लिए, यह कुछ इस तरह दिख सकता है `"C:\\Documents\\"`.

## चरण 2: पीडीएफ दस्तावेज़ लोड करें

अगले चरण में पीडीएफ फाइल को लोड करना शामिल है ताकि हम इसे प्रोसेस करना शुरू कर सकें। हम इसका एक उदाहरण बनाएंगे `Document` क्लास में जाएं और उसमें अपना फ़ाइल पथ पास करें।

```csharp
Document document = new Document(dataDir + "input.pdf");
```

इस बिंदु पर, यदि सब कुछ सही ढंग से सेट किया गया है, तो आपकी पीडीएफ फाइल लोड हो जाएगी और इंटरेक्शन के लिए तैयार हो जाएगी।

## चरण 3: प्रत्येक पृष्ठ पर पुनरावृत्ति करें

PDF में कई पेज हो सकते हैं, इसलिए हम लिंक एनोटेशन खोजने के लिए हर पेज पर जाएँगे। आप इसे इस तरह से कर सकते हैं:

```csharp
foreach (Page page in document.Pages)
{
    // लिंक एनोटेशन दिखाएं
    ShowLinkAnnotations(page);
}
```

इस लूप में, हम एक विधि परिभाषित करेंगे जिसे कहा जाता है `ShowLinkAnnotations` जो हाइपरलिंक्स के निष्कर्षण का काम संभालेगा। 

## चरण 4: ShowLinkAnnotations विधि को परिभाषित करें

यहीं पर जादू होता है! आप प्रत्येक पृष्ठ पर हाइपरलिंक टेक्स्ट निकालने के लिए एक विधि बनाएंगे। यहाँ इस विधि का एक सरलीकृत संस्करण दिया गया है:

```csharp
private static void ShowLinkAnnotations(Page page)
{
    foreach (Annotation annotation in page.Annotations)
    {
        if (annotation is LinkAnnotation link)
        {
            Console.WriteLine("Link Text: " + link.Title);
            Console.WriteLine("Link URI: " + link.Action.URI);
        }
    }
}
```

- जाँचें कि क्या एनोटेशन एक लिंक है: यहाँ, हम जाँचते हैं कि क्या पृष्ठ पर एनोटेशन एक लिंक है `LinkAnnotation`यदि ऐसा है, तो हम इसका शीर्षक और यूआरआई निकालने के लिए आगे बढ़ते हैं।
- हाइपरलिंक टेक्स्ट प्रदर्शित करें: `Console.WriteLine`, हम लिंक टेक्स्ट और संबंधित यूआरआई प्रिंट करते हैं।

## चरण 5: अपवाद प्रबंधन

अंत में, त्रुटि प्रबंधन को शामिल करना हमेशा एक अच्छा अभ्यास है। संभावित त्रुटियों को पकड़ने के लिए अपने कोड को try-catch ब्लॉक में लपेटें, जैसे:

```csharp
try
{
    // आपका कोड यहाँ
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

यदि कोई काम योजना के अनुसार नहीं होता है तो इससे आपको स्पष्ट परिणाम मिलेगा।

## निष्कर्ष 

बधाई हो! आपने सफलतापूर्वक सीख लिया है कि .NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइल से हाइपरलिंक टेक्स्ट कैसे निकाला जाता है! कोड की कुछ ही पंक्तियों के साथ, आप अपने PDF दस्तावेज़ों से पहले से कहीं ज़्यादा जानकारी प्राप्त कर सकते हैं। चाहे डेटा निष्कर्षण, लिंक सत्यापन या दस्तावेज़ ऑडिटिंग के लिए हो, यह मार्गदर्शिका आपको PDF हाइपरलिंक निष्कर्षण से निपटने के लिए तैयार करती है। Aspose.PDF के साथ प्रयोग करते रहें, और जल्द ही आप PDF में हेरफेर करने में माहिर हो जाएँगे!

## अक्सर पूछे जाने वाले प्रश्न

### .NET के लिए Aspose.PDF क्या है?
.NET के लिए Aspose.PDF एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को प्रोग्रामेटिक रूप से PDF दस्तावेज़ बनाने, हेरफेर करने और परिवर्तित करने की अनुमति देती है।

### क्या इसका कोई निःशुल्क संस्करण उपलब्ध है?
हां, आप यहां से निःशुल्क परीक्षण संस्करण डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/).

### मैं किस प्रकार के हाइपरलिंक निकाल सकता हूँ?
आप पीडीएफ में मौजूद किसी भी हाइपरलिंक को निकाल सकते हैं, चाहे वह एक सामान्य वेब यूआरएल हो या दस्तावेज़ के भीतर एक क्रॉस-रेफरेंस लिंक हो।

### क्या मैं हाइपरलिंक के साथ चित्र और पाठ निकाल सकता हूँ?
बिल्कुल! Aspose.PDF न केवल हाइपरलिंक्स बल्कि PDF से चित्र और टेक्स्ट निकालने की कार्यक्षमता भी प्रदान करता है।

### मैं और अधिक Aspose.PDF संसाधन कहां पा सकता हूं?
विस्तृत दस्तावेज़ीकरण के लिए, यहां जाएं [Aspose PDF दस्तावेज़ीकरण](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}