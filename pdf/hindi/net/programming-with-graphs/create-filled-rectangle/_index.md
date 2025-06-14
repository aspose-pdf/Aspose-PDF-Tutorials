---
"description": "इस चरण-दर-चरण ट्यूटोरियल के साथ .NET के लिए Aspose.PDF का उपयोग करके PDF में भरा हुआ आयत बनाना सीखें। सभी स्तरों के डेवलपर्स के लिए बिल्कुल सही।"
"linktitle": "भरा हुआ आयत बनाएँ"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "भरा हुआ आयत बनाएँ"
"url": "/hi/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# भरा हुआ आयत बनाएँ

## परिचय

क्या आपने कभी प्रोग्रामेटिक रूप से आकर्षक PDF बनाना चाहा है? अगर हाँ, तो आप सही जगह पर हैं! इस ट्यूटोरियल में, हम .NET के लिए Aspose.PDF की दुनिया में गोता लगाएँगे, एक शक्तिशाली लाइब्रेरी जो आपको आसानी से PDF दस्तावेज़ों में हेरफेर करने की अनुमति देती है। आज, हम PDF फ़ाइल के भीतर एक भरा हुआ आयत बनाने पर ध्यान केंद्रित करेंगे। चाहे आप एक अनुभवी डेवलपर हों या अभी शुरुआत कर रहे हों, यह गाइड आपको प्रत्येक चरण को एक दोस्ताना और आकर्षक तरीके से पूरा करने में मदद करेगी। तो, अपनी कोडिंग टोपी पकड़ो, और चलो शुरू करते हैं!

## आवश्यक शर्तें

इससे पहले कि हम कोड में प्रवेश करें, कुछ चीजें हैं जिन्हें आपको ध्यान में रखना होगा:

1. विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके मशीन पर विज़ुअल स्टूडियो स्थापित है। यह .NET विकास के लिए एक शानदार IDE है।
2. .NET के लिए Aspose.PDF: आपको Aspose.PDF लाइब्रेरी डाउनलोड और इंस्टॉल करनी होगी। आप इसे पा सकते हैं [यहाँ](https://releases.aspose.com/pdf/net/).
3. C# का बुनियादी ज्ञान: C# प्रोग्रामिंग से थोड़ी परिचितता आपको कोड स्निपेट को बेहतर ढंग से समझने में मदद करेगी।

## पैकेज आयात करें

आरंभ करने के लिए, आपको अपने C# प्रोजेक्ट में आवश्यक पैकेज आयात करने होंगे। आप यह कैसे कर सकते हैं, यहाँ बताया गया है:

### एक नया प्रोजेक्ट बनाएं

Visual Studio खोलें और एक नया C# प्रोजेक्ट बनाएँ। आप सरलता के लिए कंसोल एप्लीकेशन चुन सकते हैं।

### Aspose.PDF संदर्भ जोड़ें

1. समाधान एक्सप्लोरर में अपने प्रोजेक्ट पर राइट-क्लिक करें।
2. "NuGet पैकेज प्रबंधित करें" चुनें.
3. "Aspose.PDF" खोजें और नवीनतम संस्करण स्थापित करें।

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

अब जब हमने सब कुछ सेट कर लिया है, तो चलिए कोड पर आते हैं!

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

सबसे पहले, आपको वह पथ निर्दिष्ट करना होगा जहाँ आपका PDF सहेजा जाएगा। यह महत्वपूर्ण है क्योंकि यह प्रोग्राम को बताता है कि फ़ाइल कहाँ बनानी है।

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

प्रतिस्थापित करें `"YOUR DOCUMENT DIRECTORY"` अपनी मशीन पर उस वास्तविक पथ के साथ जहां आप पीडीएफ को सहेजना चाहते हैं।

## चरण 2: दस्तावेज़ इंस्टेंस बनाएँ

इसके बाद, हम इसका एक उदाहरण बनाएंगे `Document` क्लास. यह क्लास उस पीडीएफ दस्तावेज़ का प्रतिनिधित्व करता है जिसके साथ आप काम करेंगे.

```csharp
// दस्तावेज़ उदाहरण बनाएँ
Document doc = new Document();
```

यह पंक्ति एक नया पीडीएफ दस्तावेज़ आरंभ करती है जिसे हम संशोधित कर सकते हैं।

## चरण 3: दस्तावेज़ में एक पृष्ठ जोड़ें

अब, चलिए अपने दस्तावेज़ में एक पेज जोड़ते हैं। हर PDF को कम से कम एक पेज की ज़रूरत होती है, है न?

```csharp
// पीडीएफ फाइल के पेज टू पेज संग्रह को जोड़ें
Page page = doc.Pages.Add();
```

यह कोड दस्तावेज़ में एक नया पृष्ठ जोड़ता है, जिससे हम उस पर आकृतियाँ बना सकते हैं।

## चरण 4: ग्राफ़ इंस्टेंस बनाएँ

आकृतियाँ बनाने के लिए, हमें एक आकृति बनाने की आवश्यकता है `Graph` उदाहरण के लिए, ग्राफ को एक कैनवास के रूप में सोचें, जिस पर आप विभिन्न आकृतियाँ बना सकते हैं।

```csharp
// ग्राफ़ इंस्टेंस बनाएँ
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

यहां, हम 100 की चौड़ाई और 400 की ऊंचाई वाला एक ग्राफ बना रहे हैं।

## चरण 5: पेज पर ग्राफ़ जोड़ें

अब जबकि हमारे पास ग्राफ है, तो आइए इसे उस पेज में जोड़ें जिसे हमने पहले बनाया था।

```csharp
// पेज इंस्टेंस के पैराग्राफ़ संग्रह में ग्राफ़ ऑब्जेक्ट जोड़ें
page.Paragraphs.Add(graph);
```

यह रेखा ग्राफ को पृष्ठ से जोड़ती है, तथा उसे आरेखण के लिए तैयार करती है।

## चरण 6: एक आयत उदाहरण बनाएँ

इसके बाद, हम एक आयत बनाएंगे जिसे हम रंग से भरना चाहते हैं।

```csharp
// आयत उदाहरण बनाएँ
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

इस कोड में, हम आयत की स्थिति और आकार को परिभाषित करते हैं। पैरामीटर x और y निर्देशांक, चौड़ाई और ऊँचाई को दर्शाते हैं।

## चरण 7: भरण रंग निर्दिष्ट करें

अब, आइए अपने आयत के लिए एक रंग चुनें। इस उदाहरण के लिए हम इसे लाल रंग से भरेंगे।

```csharp
// ग्राफ़ ऑब्जेक्ट के लिए भरण रंग निर्दिष्ट करें
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

यह रेखा आयत का रंग लाल रंग में सेट करती है। आप अपनी पसंद का कोई भी रंग चुन सकते हैं!

## चरण 8: ग्राफ़ में आयत जोड़ें

अब जब हमारा आयत तैयार हो गया है, तो उसे ग्राफ में जोड़ने का समय आ गया है।

```csharp
// ग्राफ़ ऑब्जेक्ट के आकार संग्रह में आयत ऑब्जेक्ट जोड़ें
graph.Shapes.Add(rect);
```

यह कोड आयत को ग्राफ में जोड़ता है, तथा उसे हमारे चित्र का हिस्सा बनाता है।

## चरण 9: पीडीएफ दस्तावेज़ सहेजें

अंत में, हमें अपने दस्तावेज़ को निर्दिष्ट निर्देशिका में सहेजना होगा।

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// पीडीएफ फाइल सहेजें
doc.Save(dataDir);
```

यह कोड पीडीएफ फाइल को इस नाम से सेव करता है `CreateFilledRectangle_out.pdf` आपके द्वारा पहले निर्दिष्ट निर्देशिका में.

## चरण 10: पुष्टिकरण संदेश

हमें यह बताने के लिए कि सब कुछ सुचारू रूप से हुआ, हम एक पुष्टिकरण संदेश प्रिंट कर सकते हैं।

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

यह पंक्ति कंसोल में एक संदेश आउटपुट करेगी, जो पुष्टि करेगी कि भरा हुआ आयत सफलतापूर्वक बनाया गया है।

## निष्कर्ष

और अब यह हो गया! आपने .NET के लिए Aspose.PDF का उपयोग करके PDF दस्तावेज़ में सफलतापूर्वक एक भरा हुआ आयत बनाया है। यह शक्तिशाली लाइब्रेरी PDF हेरफेर के लिए संभावनाओं की एक दुनिया खोलती है, जिससे आप प्रोग्रामेटिक रूप से शानदार दस्तावेज़ बना सकते हैं। चाहे आप रिपोर्ट, चालान या किसी अन्य प्रकार का PDF बना रहे हों, Aspose.PDF आपके लिए है।

## अक्सर पूछे जाने वाले प्रश्न

### .NET के लिए Aspose.PDF क्या है?
.NET के लिए Aspose.PDF एक लाइब्रेरी है जो डेवलपर्स को प्रोग्रामेटिक रूप से PDF दस्तावेज़ बनाने, हेरफेर करने और परिवर्तित करने की अनुमति देती है।

### क्या मैं Aspose.PDF का निःशुल्क उपयोग कर सकता हूँ?
हां, Aspose एक निःशुल्क परीक्षण संस्करण प्रदान करता है जिसका उपयोग आप लाइब्रेरी की विशेषताओं का पता लगाने के लिए कर सकते हैं। आप इसे डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/).

### क्या Aspose.PDF के लिए समर्थन पाने का कोई तरीका है?
बिल्कुल! आप Aspose फ़ोरम के ज़रिए सहायता प्राप्त कर सकते हैं [यहाँ](https://forum.aspose.com/c/pdf/10).

### मैं Aspose.PDF कैसे खरीद सकता हूँ?
आप खरीद पृष्ठ पर जाकर Aspose.PDF खरीद सकते हैं [यहाँ](https://purchase.aspose.com/buy).

### मैं Aspose.PDF के साथ किस प्रकार की आकृतियाँ बना सकता हूँ?
आप Aspose.PDF लाइब्रेरी का उपयोग करके आयत, वृत्त, रेखाएँ आदि सहित विभिन्न आकृतियाँ बना सकते हैं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}