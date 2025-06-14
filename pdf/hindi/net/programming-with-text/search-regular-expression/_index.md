---
"description": "इस चरण-दर-चरण ट्यूटोरियल में जानें कि .NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइलों में रेगुलर एक्सप्रेशन कैसे खोजें। रेगेक्स के साथ अपनी उत्पादकता बढ़ाएँ।"
"linktitle": "पीडीएफ फाइल में रेगुलर एक्सप्रेशन खोजें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "पीडीएफ फाइल में रेगुलर एक्सप्रेशन खोजें"
"url": "/hi/net/programming-with-text/search-regular-expression/"
"weight": 440
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# पीडीएफ फाइल में रेगुलर एक्सप्रेशन खोजें

## परिचय

बड़े PDF दस्तावेज़ों से निपटते समय, आप खुद को दिनांक, फ़ोन नंबर या अन्य संरचित डेटा जैसे विशिष्ट पैटर्न या फ़ॉर्मेट की खोज करते हुए पा सकते हैं। मैन्युअल रूप से PDF को देखना थकाऊ हो सकता है, है न? यहीं पर रेगुलर एक्सप्रेशन (regex) का उपयोग करना काम आता है। इस ट्यूटोरियल में, हम .NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइल में रेगुलर एक्सप्रेशन पैटर्न की खोज करने का तरीका जानेंगे। यह गाइड आपको प्रत्येक चरण से गुजारेगी ताकि आप इसे अपने .NET एप्लिकेशन में आसानी से लागू कर सकें।

## आवश्यक शर्तें

इससे पहले कि हम चरण-दर-चरण ट्यूटोरियल में उतरें, आइए देखें कि आपको क्या करने की आवश्यकता है:

- .NET के लिए Aspose.PDF: आपको यह लाइब्रेरी इंस्टॉल करनी होगी। अगर आपने इसे अभी तक इंस्टॉल नहीं किया है, तो आप इसे इंस्टॉल कर सकते हैं। [यहाँ पर डाउनलोड करो](https://releases.aspose.com/pdf/net/).
- IDE: विजुअल स्टूडियो या कोई अन्य C# संगत IDE.
- .NET फ्रेमवर्क: सुनिश्चित करें कि आपका प्रोजेक्ट .NET फ्रेमवर्क के उपयुक्त संस्करण के साथ सेटअप किया गया है।
- C# का बुनियादी ज्ञान: यद्यपि यह मार्गदर्शिका विस्तृत है, फिर भी C# की बुनियादी समझ उपयोगी होगी।

### पैकेज आयात करें

आरंभ करने के लिए, आपको अपने प्रोजेक्ट में Aspose.PDF for .NET से आवश्यक नेमस्पेस आयात करने होंगे। ये पैकेज PDF के साथ काम करने और regex का उपयोग करके खोज ऑपरेशन करने के लिए आवश्यक हैं।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

आइए Aspose.PDF का उपयोग करके PDF फ़ाइल में नियमित अभिव्यक्तियों की खोज करने की प्रक्रिया को कई चरणों में विभाजित करें।

## चरण 1: दस्तावेज़ निर्देशिका सेट करें

हर PDF ऑपरेशन यह निर्दिष्ट करने से शुरू होता है कि आपका दस्तावेज़ कहाँ स्थित है। आपको अपनी PDF फ़ाइल का पथ परिभाषित करना होगा, जो कि इसमें संग्रहीत है `dataDir` चर।

### चरण 1.1: अपना दस्तावेज़ पथ परिभाषित करें

```csharp
// अपने PDF दस्तावेज़ का पथ निर्धारित करें
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

प्रतिस्थापित करें `"YOUR DOCUMENT DIRECTORY"` अपनी PDF फ़ाइल के वास्तविक पथ के साथ। यह चरण महत्वपूर्ण है क्योंकि यह आपके कोड को उस फ़ाइल की ओर इंगित करता है जिसके साथ आप काम करना चाहते हैं।

### चरण 1.2: पीडीएफ दस्तावेज़ खोलें

इसके बाद, आपको पीडीएफ दस्तावेज़ को खोलना होगा `Document` Aspose.PDF से क्लास.

```csharp
// दस्तावेज़ खोलें
Document pdfDocument = new Document(dataDir + "SearchRegularExpressionAll.pdf");
```

यहाँ, `"SearchRegularExpressionAll.pdf"` यह नमूना पीडीएफ फाइल है जहां हम रेगेक्स खोज करेंगे।

## चरण 2: TextFragmentAbsorber सेट अप करें

यहीं पर जादू घटित होता है! `TextFragmentAbsorber` क्लास उन पाठ के टुकड़ों को कैप्चर करने में मदद करता है जो किसी विशिष्ट पैटर्न या नियमित अभिव्यक्ति से मेल खाते हैं।

आइए रेगेक्स का उपयोग करके पैटर्न खोजने के लिए अवशोषक को सेट करें। इस मामले में, हम "1999-2000" जैसे वर्षों के पैटर्न की खोज कर रहे हैं।

```csharp
// नियमित अभिव्यक्ति से मेल खाने वाले सभी वाक्यांशों को खोजने के लिए TextAbsorber ऑब्जेक्ट बनाएं
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("\\d{4}-\\d{4}"); // 1999-2000 की तरह
```

नियमित अभिव्यक्ति `\\d{4}-\\d{4}` चार अंकों के पैटर्न को देखता है, जिसके बाद एक हाइफ़न और चार अन्य अंक होते हैं, जो वर्ष श्रेणियों के लिए विशिष्ट है।

## चरण 3: नियमित अभिव्यक्ति खोज सक्षम करें

यह सुनिश्चित करने के लिए कि खोज ऑपरेशन पैटर्न को एक नियमित अभिव्यक्ति के रूप में व्याख्या करता है, आपको खोज विकल्पों को कॉन्फ़िगर करने की आवश्यकता है `TextSearchOptions` कक्षा।

```csharp
// नियमित अभिव्यक्ति उपयोग निर्दिष्ट करने के लिए पाठ खोज विकल्प सेट करें
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textFragmentAbsorber.TextSearchOptions = textSearchOptions;
```

सेटिंग `TextSearchOptions` को `true` यह सुनिश्चित करता है कि अवशोषक सादे पाठ के बजाय नियमित अभिव्यक्ति-आधारित खोज का उपयोग करता है।

## चरण 4: टेक्स्ट अवशोषक को स्वीकार करें

इस चरण पर, आप पीडीएफ दस्तावेज़ पर टेक्स्ट अवशोषक लागू करते हैं ताकि यह खोज ऑपरेशन कर सके। यह कॉल करके किया जाता है `Accept` विधि पर `Pages` पीडीएफ दस्तावेज़ का ऑब्जेक्ट.

```csharp
// सभी पृष्ठों के लिए अवशोषक स्वीकार करें
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

यह कमांड पीडीएफ के सभी पृष्ठों को प्रोसेस करता है, तथा नियमित अभिव्यक्ति से मेल खाने वाले किसी भी पाठ की तलाश करता है।

## चरण 5: परिणाम निकालें और प्रदर्शित करें

खोज पूरी होने के बाद, आपको परिणाम निकालने की आवश्यकता है। `TextFragmentAbsorber` इन परिणामों को एक में संग्रहीत करता है `TextFragmentCollection`आप प्रत्येक मेल खाते पाठ खंड तक पहुंचने और उसे प्रदर्शित करने के लिए इस संग्रह के माध्यम से लूप कर सकते हैं।

### चरण 5.1: निकाले गए पाठ अंशों को पुनः प्राप्त करें

```csharp
// निकाले गए पाठ अंश प्राप्त करें
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

अब जब आपने टुकड़े एकत्र कर लिए हैं, तो अब समय है कि आप उन पर नजर डालें और प्रासंगिक विवरण जैसे पाठ, स्थिति, फ़ॉन्ट विवरण आदि प्रदर्शित करें।

### चरण 5.2: टुकड़ों के माध्यम से लूप करें

```csharp
// टुकड़ों के माध्यम से लूप
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

प्रत्येक के लिए `TextFragment`, फ़ॉन्ट आकार, फ़ॉन्ट नाम और स्थिति जैसे विवरण प्रिंट किए जाते हैं। यह न केवल पाठ खोजने में मदद करता है बल्कि आपको इसकी सटीक स्वरूपण और स्थान भी बताता है।

## निष्कर्ष

बस, अब यह हो गया! रेगुलर एक्सप्रेशन का उपयोग करके PDF फ़ाइल में पैटर्न खोजना अविश्वसनीय रूप से शक्तिशाली है, खासकर संरचित टेक्स्ट जैसे दिनांक, फ़ोन नंबर और इसी तरह के पैटर्न के लिए। .NET के लिए Aspose.PDF ऐसे ऑपरेशन को आसानी से करने का एक सहज तरीका प्रदान करता है। अब आप PDF टेक्स्ट सर्चिंग को स्वचालित करने के लिए रेगुलर एक्सप्रेशन की शक्ति का लाभ उठा सकते हैं, जिससे आपका वर्कफ़्लो और अधिक कुशल बन जाएगा।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं एक पीडीएफ में एकाधिक पैटर्न खोज सकता हूँ?
हां, आप कई चला सकते हैं `TextFragmentAbsorber` एक ही पीडीएफ में विभिन्न रेगेक्स पैटर्न वाली कई ऑब्जेक्ट्स।

### क्या Aspose.PDF केस-असंवेदनशील पैटर्न की खोज का समर्थन करता है?
बिल्कुल! आप कॉन्फ़िगर कर सकते हैं `TextSearchOptions` खोज को केस-असंवेदनशील बनाने के लिए.

### क्या पीडीएफ के आकार की कोई सीमा है जिसके माध्यम से मैं खोज कर सकता हूं?
इसमें कोई सख्त सीमा नहीं है, लेकिन पीडीएफ के आकार और रेगेक्स पैटर्न की जटिलता के आधार पर प्रदर्शन भिन्न हो सकता है।

### क्या मैं पीडीएफ में पाए गए पाठ को हाइलाइट कर सकता हूं?
हां, Aspose.PDF आपको अवशोषक का उपयोग करके पाठ मिलने पर उसे हाइलाइट करने या यहां तक कि बदलने की अनुमति देता है।

### यदि पैटर्न नहीं मिलता तो मैं त्रुटियों को कैसे संभालूँ?
यदि कोई मिलान नहीं मिलता है, तो `TextFragmentCollection` खाली हो जाएगा। आप परिणामों के माध्यम से लूपिंग से पहले एक सरल जाँच के साथ इस परिदृश्य को संभाल सकते हैं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}