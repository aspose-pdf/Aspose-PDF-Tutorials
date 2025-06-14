---
"description": "इस चरण-दर-चरण मार्गदर्शिका के साथ .NET के लिए Aspose.PDF का उपयोग करके PDF दस्तावेज़ों में फ़ाइल जानकारी सेट करना सीखें। मेटाडेटा के साथ अपने PDF को आसानी से बेहतर बनाएँ।"
"linktitle": "पीडीएफ फाइल में फाइल जानकारी सेट करें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "पीडीएफ फाइल में फाइल जानकारी सेट करें"
"url": "/hi/net/programming-with-document/setfileinfo/"
"weight": 310
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# पीडीएफ फाइल में फाइल जानकारी सेट करें

## परिचय

जब PDF फ़ाइलों को प्रबंधित करने की बात आती है, तो दस्तावेज़ मेटाडेटा पर नियंत्रण रखना महत्वपूर्ण होता है। चाहे आप लेखक की जानकारी, कीवर्ड या यहाँ तक कि विषय पंक्ति जोड़ना चाह रहे हों, .NET के लिए Aspose.PDF आपके PDF दस्तावेज़ों में फ़ाइल जानकारी सेट करने का एक सहज तरीका प्रदान करता है। यह ट्यूटोरियल आपको प्रक्रिया के माध्यम से चरण-दर-चरण मार्गदर्शन करेगा, यह सुनिश्चित करते हुए कि आप कोड के प्रत्येक भाग को समझते हैं। तो, अपनी कोडिंग टोपी पकड़ो, और चलो PDF हेरफेर की दुनिया में गोता लगाएँ!

## आवश्यक शर्तें

इससे पहले कि हम शुरू करें, कुछ चीजें हैं जिन्हें आपको तैयार रखना होगा:

1. विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके मशीन पर विज़ुअल स्टूडियो स्थापित है। यहीं पर आप अपना .NET कोड लिखेंगे और निष्पादित करेंगे।
   
2. .NET के लिए Aspose.PDF: आपको Aspose.PDF लाइब्रेरी डाउनलोड और इंस्टॉल करनी होगी। आप इसे यहाँ से प्राप्त कर सकते हैं [Aspose डाउनलोड पृष्ठ](https://releases.aspose.com/pdf/net/).

3. C# का बुनियादी ज्ञान: C# प्रोग्रामिंग से परिचित होने से आपको हमारे द्वारा उपयोग किए जाने वाले कोड स्निपेट को समझने में मदद मिलेगी।

4. एक पीडीएफ फाइल: एक नमूना पीडीएफ फाइल तैयार रखें जिसे आप संशोधित करना चाहते हैं। इस ट्यूटोरियल के लिए, हम इसे इस प्रकार संदर्भित करेंगे `SetFileInfo.pdf`.

एक बार जब आप यह सब सेट कर लेंगे, तो हम कोड में कूदने के लिए तैयार हैं!

## पैकेज आयात करें

आरंभ करने के लिए, आपको आवश्यक पैकेज आयात करने होंगे जो आपको PDF फ़ाइलों के साथ काम करने की अनुमति देंगे। अपने C# प्रोजेक्ट में, अपनी कोड फ़ाइल के शीर्ष पर निम्नलिखित using निर्देश जोड़ें:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
```

ये नामस्थान पीडीएफ दस्तावेजों को प्रभावी ढंग से संचालित करने के लिए आवश्यक वर्गों और विधियों तक पहुंच प्रदान करते हैं।

## चरण 1: दस्तावेज़ निर्देशिका निर्धारित करें

सबसे पहले, आपको वह डायरेक्टरी निर्दिष्ट करनी होगी जहाँ आपकी PDF फ़ाइल स्थित है। यह महत्वपूर्ण है क्योंकि आप फ़ाइल को इसी पथ से खोलेंगे।

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

स्पष्टीकरण: प्रतिस्थापित करें `"YOUR DOCUMENT DIRECTORY"` आपके फ़ोल्डर वाले वास्तविक पथ के साथ `SetFileInfo.pdf`यह आपके प्रोग्राम को बताता है कि पीडीएफ फाइल को कहां देखना है।

## चरण 2: पीडीएफ दस्तावेज़ खोलें

इसके बाद, उस PDF दस्तावेज़ को खोलें जिसे आप संशोधित करना चाहते हैं। `Document` Aspose.PDF लाइब्रेरी से क्लास.

```csharp
// दस्तावेज़ खोलें
Document pdfDocument = new Document(dataDir + "SetFileInfo.pdf");
```

स्पष्टीकरण: यहाँ, हम एक नया उदाहरण बनाते हैं `Document` क्लास में जाकर पीडीएफ फाइल का पथ पास करें। इससे दस्तावेज़ मेमोरी में लोड हो जाता है, संपादन के लिए तैयार।

## चरण 3: दस्तावेज़ जानकारी ऑब्जेक्ट बनाएँ

अब जब हमने दस्तावेज़ खोल लिया है, तो हमें एक ऑब्जेक्ट बनाने की आवश्यकता है जो दस्तावेज़ की जानकारी रखेगा।

```csharp
// दस्तावेज़ जानकारी निर्दिष्ट करें
DocumentInfo docInfo = new DocumentInfo(pdfDocument);
```

स्पष्टीकरण: `DocumentInfo` क्लास हमें पीडीएफ के लिए विभिन्न मेटाडेटा गुण सेट करने की अनुमति देता है। इस ऑब्जेक्ट का उपयोग लेखक, निर्माण तिथि और अधिक जैसी जानकारी संग्रहीत करने के लिए किया जाएगा।

## चरण 4: दस्तावेज़ मेटाडेटा सेट करें

साथ `DocumentInfo` ऑब्जेक्ट तैयार होने के बाद, इसे प्रासंगिक मेटाडेटा से भरने का समय आ गया है। यह वह जगह है जहाँ आप लेखक, निर्माण तिथि, कीवर्ड, संशोधन तिथि, विषय और दस्तावेज़ का शीर्षक निर्दिष्ट कर सकते हैं।

```csharp
docInfo.Author = "Aspose";
docInfo.CreationDate = DateTime.Now;
docInfo.Keywords = "Aspose.Pdf, DOM, API";
docInfo.ModDate = DateTime.Now;
docInfo.Subject = "PDF Information";
docInfo.Title = "Setting PDF Document Information";
```

स्पष्टीकरण: प्रत्येक पंक्ति दस्तावेज़ की एक विशिष्ट विशेषता निर्धारित करती है। उदाहरण के लिए, `docInfo.Author` लेखक का नाम निर्धारित करता है, जबकि `docInfo.CreationDate` दस्तावेज़ बनाए जाने की तिथि निर्धारित करता है। आप इन मानों को आवश्यकतानुसार अनुकूलित कर सकते हैं।

## चरण 5: दस्तावेज़ सहेजें

वांछित मेटाडेटा सेट करने के बाद, अगला चरण संशोधित पीडीएफ को सहेजना है। आपको आउटपुट फ़ाइल के लिए एक नया पथ निर्दिष्ट करना होगा।

```csharp
dataDir = dataDir + "SetFileInfo_out.pdf";
// आउटपुट दस्तावेज़ सहेजें
pdfDocument.Save(dataDir);
```

स्पष्टीकरण: यहाँ, हम जोड़ते हैं `_out.pdf` संशोधित दस्तावेज़ के लिए एक नई फ़ाइल बनाने के लिए मूल फ़ाइल नाम में परिवर्तन करें। `Save` विधि तब इस नई फ़ाइल में परिवर्तन लिखती है।

## चरण 6: परिवर्तनों की पुष्टि करें

अंत में, यह पुष्टि करना हमेशा अच्छा विचार है कि जानकारी सही ढंग से सेट की गई है। आप कंसोल पर एक सफ़लता संदेश प्रिंट करके ऐसा कर सकते हैं।

```csharp
Console.WriteLine("\nFile informations setup successfully.\nFile saved at " + dataDir);
```

स्पष्टीकरण: यह लाइन एक संदेश आउटपुट करती है जो यह संकेत देती है कि फ़ाइल सफलतापूर्वक सहेज ली गई है, साथ ही नई फ़ाइल का पथ भी बताती है। यह सुनिश्चित करने का एक सरल तरीका है कि सब कुछ योजना के अनुसार हुआ।

## निष्कर्ष

.NET के लिए Aspose.PDF का उपयोग करके PDF दस्तावेज़ों में फ़ाइल जानकारी सेट करना एक सीधी प्रक्रिया है जो आपके PDF की उपयोगिता को बहुत बढ़ा सकती है। इन चरणों का पालन करके, आप आसानी से लेखक, निर्माण तिथि और अधिक जैसे मेटाडेटा जोड़ सकते हैं, जिससे आपके दस्तावेज़ अधिक जानकारीपूर्ण और पेशेवर बन सकते हैं। चाहे आप ऐसे एप्लिकेशन विकसित कर रहे हों जो PDF उत्पन्न करते हैं या बस अपने दस्तावेज़ों को बेहतर ढंग से प्रबंधित करने की आवश्यकता है, Aspose.PDF आपको काम को कुशलतापूर्वक पूरा करने के लिए आवश्यक उपकरण प्रदान करता है।

## अक्सर पूछे जाने वाले प्रश्न

### .NET के लिए Aspose.PDF क्या है?
.NET के लिए Aspose.PDF एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को प्रोग्रामेटिक रूप से PDF दस्तावेज़ बनाने, हेरफेर करने और परिवर्तित करने की अनुमति देती है।

### क्या मैं Aspose.PDF का निःशुल्क उपयोग कर सकता हूँ?
हां, Aspose एक निःशुल्क परीक्षण संस्करण प्रदान करता है जिसका उपयोग आप लाइब्रेरी का मूल्यांकन करने के लिए कर सकते हैं। [निःशुल्क परीक्षण पृष्ठ](https://releases.aspose.com/) अधिक जानकारी के लिए.

### मैं दस्तावेज कहां पा सकता हूं?
Aspose.PDF का पूरा दस्तावेज़ यहां पाया जा सकता है [यहाँ](https://reference.aspose.com/pdf/net/).

### मैं Aspose.PDF कैसे खरीदूं?
आप Aspose.PDF के लिए लाइसेंस खरीद सकते हैं [खरीद पृष्ठ](https://purchase.aspose.com/buy).

### यदि मुझे सहायता की आवश्यकता हो तो क्या होगा?
यदि आपके कोई प्रश्न हों या आपको सहायता की आवश्यकता हो, तो आप यहां जा सकते हैं [Aspose समर्थन मंच](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}