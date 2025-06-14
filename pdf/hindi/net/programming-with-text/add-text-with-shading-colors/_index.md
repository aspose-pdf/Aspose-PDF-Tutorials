---
"description": "इस चरण-दर-चरण ट्यूटोरियल के साथ .NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइलों में टेक्स्ट शेडिंग जोड़ना सीखें। रंगीन ग्रेडिएंट के साथ अपने दस्तावेज़ों को कस्टमाइज़ करें।"
"linktitle": "पीडीएफ फाइल में शेडिंग रंगों के साथ टेक्स्ट जोड़ें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "पीडीएफ फाइल में शेडिंग रंगों के साथ टेक्स्ट जोड़ें"
"url": "/hi/net/programming-with-text/add-text-with-shading-colors/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# पीडीएफ फाइल में शेडिंग रंगों के साथ टेक्स्ट जोड़ें

## परिचय

क्या आपको कभी ऐसा लगा है कि PDF दस्तावेज़ों को थोड़े रंग से आकर्षक बनाने की ज़रूरत है? हो सकता है कि आपने PDF के साथ काम किया हो और सोचा हो, “इसे अलग दिखाने के लिए कुछ अतिरिक्त की ज़रूरत है।” खैर, अब और न देखें! .NET के लिए Aspose.PDF के साथ, आप आसानी से अपनी PDF फ़ाइलों में शेडिंग रंगों के साथ टेक्स्ट जोड़ सकते हैं। चाहे आप प्रस्तुति के लिए कोई दस्तावेज़ तैयार कर रहे हों या बस टेक्स्ट के किसी हिस्से को चमकाना चाहते हों, टेक्स्ट को शेडिंग करना वास्तव में आपके दस्तावेज़ के डिज़ाइन को बेहतर बना सकता है।

## आवश्यक शर्तें

कोड में गोता लगाने से पहले, इस ट्यूटोरियल का पालन करने के लिए आपको कुछ चीजें सेट अप करने की आवश्यकता है। यहाँ बताया गया है कि आपको क्या चाहिए:

1. .NET के लिए Aspose.PDF: सुनिश्चित करें कि आपने Aspose.PDF का नवीनतम संस्करण डाउनलोड और इंस्टॉल किया है। आप ऐसा कर सकते हैं [यहाँ पर डाउनलोड करो](https://releases.aspose.com/pdf/net/).
2. IDE (एकीकृत विकास वातावरण): आप किसी भी .NET-संगत IDE का उपयोग कर सकते हैं, लेकिन Visual Studio अत्यधिक अनुशंसित है।
3. C# का मूलभूत ज्ञान: आपको C# सिंटैक्स और .NET वातावरण से परिचित होना चाहिए।
4. एक नमूना पीडीएफ फाइल: आपको काम करने के लिए एक नमूना पीडीएफ फाइल की आवश्यकता होगी। यदि आपके पास एक नहीं है, तो आप एक साधारण टेक्स्ट पीडीएफ बना सकते हैं, या प्रदर्शन के लिए किसी भी मौजूदा फ़ाइल का उपयोग कर सकते हैं।
5. Aspose.PDF लाइसेंस: जबकि आप Aspose.PDF को एक के साथ आज़मा सकते हैं [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/)इसके अलावा, आप निःशुल्क परीक्षण का उपयोग करके भी सुविधाओं का पता लगा सकते हैं।

## पैकेज आयात करें

कोड में जाने से पहले, आपको आवश्यक नेमस्पेस आयात करने की आवश्यकता होगी। ये आपको Aspose.PDF ऑब्जेक्ट के साथ काम करने और अपने PDF दस्तावेज़ों में टेक्स्ट और रंग सेटिंग में हेरफेर करने की अनुमति देंगे।

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

आइए Aspose.PDF for .NET का उपयोग करके PDF फ़ाइल में टेक्स्ट में शेडिंग जोड़ने की प्रक्रिया को प्रबंधनीय चरणों में विभाजित करें। चिंता न करें, यह सुनने में जितना आसान लगता है, उससे कहीं ज़्यादा आसान है!

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

सबसे पहले, आपको अपने दस्तावेज़ों का स्थान निर्धारित करना होगा। इसे उस फ़ोल्डर के रूप में सोचें जहाँ आपकी सभी PDF फ़ाइलें रहेंगी और जहाँ आप अपनी नई संपादित फ़ाइल को सहेजेंगे।

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

प्रतिस्थापित करें `"YOUR DOCUMENT DIRECTORY"` आपकी PDF फ़ाइलों के वास्तविक पथ के साथ। यह सुनिश्चित करता है कि आपका कोड जानता है कि कहाँ देखना है और संपादित दस्तावेज़ को कहाँ सहेजना है।

## चरण 2: मौजूदा PDF दस्तावेज़ लोड करें

एक बार जब आप अपनी डॉक्यूमेंट डायरेक्टरी सेट कर लेते हैं, तो उस पीडीएफ फाइल को लोड करने का समय आ जाता है जिसे आप संपादित करना चाहते हैं। इस उदाहरण में, हम नाम की एक फाइल का उपयोग कर रहे हैं `"text_sample4.pdf"`.

```csharp
using (Document pdfDocument = new Document(dataDir + "text_sample4.pdf"))
{
    // अगले कदम के लिए आगे बढ़ें...
}
```

The `Document` Aspose.PDF से ऑब्जेक्ट हमें पीडीएफ खोलने और उसके साथ काम करने में मदद करेगा।

## चरण 3: TextFragmentAbsorber का उपयोग करके विशिष्ट टेक्स्ट की खोज करें

टेक्स्ट के किसी खास हिस्से पर शेडिंग लगाने के लिए हमें पीडीएफ में उस टेक्स्ट को ढूंढना होगा। यहीं पर TextFragmentAbsorber काम आता है। यह एक स्कैनर की तरह है जो उस टेक्स्ट को सोख लेता है जिसे आप संशोधित करना चाहते हैं।

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber("Lorem ipsum");
pdfDocument.Pages.Accept(absorber);
```

इस उदाहरण में, हम पीडीएफ में "लोरेम इप्सुम" वाक्यांश की तलाश कर रहे हैं। `Accept` यह विधि पृष्ठों को संसाधित करती है और अवशोषक को पाठ अंशों की पहचान करने की अनुमति देती है।

## चरण 4: उस टेक्स्ट फ़्रैगमेंट तक पहुँचें जिसे आप संशोधित करना चाहते हैं

अब जब पाठ अवशोषित हो गया है, तो आप विशिष्ट TextFragment तक पहुँच सकते हैं। हम मान रहे हैं कि "Lorem ipsum" पाठ की पहली घटना वही है जिसे हम संशोधित करना चाहते हैं।

```csharp
TextFragment textFragment = absorber.TextFragments[1];
```

यह पंक्ति TextFragments संग्रह से “Lorem ipsum” वाक्यांश का पहला उदाहरण प्राप्त करती है। यदि आप किसी भिन्न उदाहरण को संशोधित करना चाहते हैं, तो आप इंडेक्स बदल सकते हैं।

## चरण 5: पाठ पर छायांकन लागू करें

अब मज़ेदार हिस्सा आता है! चलिए टेक्स्ट में कुछ शेडिंग रंग जोड़ते हैं। आप GradientAxialShading का उपयोग करके ग्रेडिएंट प्रभाव के साथ एक नया रंग बना सकते हैं। इस उदाहरण में, हम एक शेडिंग लागू करेंगे जो लाल से नीले रंग में परिवर्तित होती है।

```csharp
textFragment.TextState.ForegroundColor = new Aspose.Pdf.Color()
{
    PatternColorSpace = new Aspose.Pdf.Drawing.GradientAxialShading(Color.Red, Color.Blue)
};
```

इससे चयनित पाठ में लाल से नीले रंग तक एक चिकनी ढाल बनती है। `PatternColorSpace` इस विशेष रंग प्रभाव को परिभाषित करने के लिए उपयोग किया जाता है।

## चरण 6: पाठ को रेखांकित करें (वैकल्पिक)

यदि आप अतिरिक्त जोर देने के लिए पाठ में रेखांकन जोड़ना चाहते हैं, तो आप इसे सेट करके ऐसा कर सकते हैं `Underline` संपत्ति को `true`.

```csharp
textFragment.TextState.Underline = true;
```

रेखांकन जोड़ने से आपका छायांकित पाठ और भी अधिक ध्यान देने योग्य हो सकता है।

## चरण 7: अपडेट किए गए PDF दस्तावेज़ को सहेजें

अंत में, जब छायांकन और अन्य वांछित संशोधन लागू हो जाएं, तो पीडीएफ को निर्देशिका में सेव कर दें।

```csharp
pdfDocument.Save(dataDir + "text_out.pdf");
```

संशोधित पीडीएफ को इस नाम से सहेजा जाएगा `"text_out.pdf"` आपके द्वारा पहले निर्दिष्ट निर्देशिका में। अब, आप फ़ाइल खोल सकते हैं और अपने सुंदर छायांकित पाठ को देख सकते हैं!

## निष्कर्ष

और अब यह हो गया! बस कुछ आसान चरणों में, आपने .NET के लिए Aspose.PDF का उपयोग करके PDF में टेक्स्ट पर सफलतापूर्वक शेडिंग लागू कर दी है। यह सुविधा न केवल विशिष्ट टेक्स्ट को हाइलाइट करने में मदद करती है, बल्कि यह आपके दस्तावेज़ों में एक पॉलिश, पेशेवर स्पर्श भी जोड़ती है। चाहे आप विज़ुअली आकर्षक रिपोर्ट बना रहे हों या बस अपने टेक्स्ट के कुछ हिस्सों को अलग दिखाना चाहते हों, यह तकनीक गेम-चेंजर है।


## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं एक साथ कई पाठ अंशों पर छायांकन लागू कर सकता हूँ?
हाँ! TextFragments संग्रह के माध्यम से पुनरावृत्ति करके, आप प्रत्येक खंड पर व्यक्तिगत रूप से छायांकन लागू कर सकते हैं।

### क्या ग्रेडिएंट रंगों को अनुकूलित करना संभव है?
बिल्कुल! आप GradientAxialShading का उपयोग करके ग्रेडिएंट के लिए कोई भी रंग परिभाषित कर सकते हैं।

### क्या मुझे इस सुविधा का उपयोग करने के लिए सशुल्क लाइसेंस की आवश्यकता है?
आप इस सुविधा को एक का उपयोग करके आज़मा सकते हैं [मुफ्त परीक्षण](https://releases.aspose.com/) या एक [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/), लेकिन पूर्ण कार्यक्षमता के लिए, सशुल्क लाइसेंस की सिफारिश की जाती है।

### मैं पाठ की फ़ॉन्ट शैली कैसे बदल सकता हूँ?
आप TextState ऑब्जेक्ट के माध्यम से फ़ॉन्ट आकार, शैली और वज़न जैसे गुणों को संशोधित कर सकते हैं जैसे कि गुण सेट करके `FontSize` और `FontStyle`.

### क्या मैं नये जोड़े गए पाठ में छायांकन जोड़ सकता हूँ?
हां, आप इस गाइड में बताई गई विधि का उपयोग करके पीडीएफ में नया टेक्स्ट जोड़ सकते हैं और शेडिंग लागू कर सकते हैं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}