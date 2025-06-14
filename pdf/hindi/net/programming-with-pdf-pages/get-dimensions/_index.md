---
"description": "इस ट्यूटोरियल में, हम बताते हैं कि .NET के लिए Aspose.PDF का उपयोग करके PDF पेज आयाम कैसे प्राप्त करें और हेरफेर कैसे करें। प्रक्रिया के माध्यम से आपका मार्गदर्शन करने के लिए विस्तृत चरण प्रदान किए गए हैं।"
"linktitle": "पीडीएफ पेज आयाम प्राप्त करें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "पीडीएफ पेज आयाम प्राप्त करें"
"url": "/hi/net/programming-with-pdf-pages/get-dimensions/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# पीडीएफ पेज आयाम प्राप्त करें

## परिचय

क्या आपको कभी किसी PDF दस्तावेज़ के पेज आयामों में फेरबदल करने की ज़रूरत पड़ी है? हो सकता है कि आप किसी पेज का आकार बदलना चाहते हों या उसे अपनी ज़रूरतों के हिसाब से घुमाना चाहते हों? अगर ऐसा है, तो आप सही जगह पर हैं! इस ट्यूटोरियल में, हम आपको .NET के लिए Aspose.PDF का उपयोग करके PDF पेज आयामों को पुनः प्राप्त करने और संशोधित करने के बारे में बताएँगे। चाहे आप शुरुआती हों या अनुभवी डेवलपर, आपको यह गाइड सरल और अनुसरण करने में आसान लगेगी।

.NET के लिए Aspose.PDF एक शक्तिशाली लाइब्रेरी है जो आपको PDF फ़ाइलों को आसानी से बनाने, उनमें हेरफेर करने और उन्हें बदलने की सुविधा देती है। यह PDF के लिए स्विस आर्मी चाकू की तरह है - आप अपनी सटीक आवश्यकताओं के अनुसार हर छोटी-छोटी जानकारी को बदल सकते हैं। तो, चलिए सीधे शुरू करते हैं और सीखते हैं कि इस शानदार टूल का उपयोग करके PDF पेज के आयामों को कैसे प्राप्त और अपडेट किया जाए!

## आवश्यक शर्तें

आरंभ करने से पहले, आपको इस ट्यूटोरियल को सुचारू रूप से समझने के लिए कुछ चीजों की आवश्यकता होगी:

1. .NET के लिए Aspose.PDF: आप कर सकते हैं [डाउनलोड का नवीनतम संस्करण यहां](https://releases.aspose.com/pdf/net/)यदि आपके पास लाइसेंस नहीं है, तो चिंता न करें! आप अनुरोध कर सकते हैं [मुफ्त परीक्षण](https://releases.aspose.com/), या चुनें [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/).
2. विज़ुअल स्टूडियो: वह विकास वातावरण जिसका उपयोग आप कोड लिखने और निष्पादित करने के लिए करेंगे।
3. C# का बुनियादी ज्ञान: यद्यपि हम चीजों को सरल रखेंगे, C# से थोड़ी परिचितता प्रक्रिया को आसान बना देगी।
4. कार्य करने के लिए पीडीएफ फाइल: परीक्षण के लिए कोई भी नमूना पीडीएफ फाइल लें या नई फाइल बनाएं।

## पैकेज आयात करें

.NET के लिए Aspose.PDF के साथ काम करने के लिए, आपको कुछ आवश्यक नामस्थान आयात करने होंगे। यह PDF दस्तावेज़ों के साथ बातचीत करने के लिए मंच तैयार करता है। इसे करने का तरीका यहां बताया गया है:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

ये आयात यह सुनिश्चित करते हैं कि आपके पास पीडीएफ फाइलों में हेरफेर करने के लिए आवश्यक कोर क्लासों तक पहुंच है, विशेष रूप से पृष्ठों को प्रबंधित करने और उनके आयामों को पुनः प्राप्त करने के लिए।

अब जब सब कुछ तैयार हो गया है, तो आइए इस प्रक्रिया को आसान चरणों में विभाजित करें।

## चरण 1: फ़ाइल पथ निर्धारित करें और दस्तावेज़ लोड करें

पहला कदम अपने PDF दस्तावेज़ का पथ निर्दिष्ट करना और Aspose.PDF का उपयोग करके इसे लोड करना है। यह आपको PDF फ़ाइल में पृष्ठों के साथ इंटरैक्ट करने की अनुमति देगा।

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// दस्तावेज़ खोलें
Document pdfDocument = new Document(dataDir + "UpdateDimensions.pdf");
```

इस चरण में, आप अनिवार्य रूप से उस पीडीएफ फाइल को खोल रहे हैं जिस पर आप काम करना चाहते हैं। यदि आपने कभी किसी पुस्तक को किसी विशेष पृष्ठ पर खोला है, तो यह काफी हद तक समान है - लेकिन इसके बजाय, आप इसके पृष्ठों तक पहुँचने के लिए एक पीडीएफ दस्तावेज़ खोल रहे हैं।

## चरण 2: यदि कोई पृष्ठ मौजूद न हो तो रिक्त पृष्ठ जोड़ें

अगर आपके दस्तावेज़ में कोई पेज नहीं है तो क्या होगा? चिंता न करें! हम दस्तावेज़ में एक खाली पेज जोड़ सकते हैं और उसके साथ काम कर सकते हैं। यहाँ बताया गया है कि कैसे जाँचें कि कोई पेज मौजूद है या नहीं और अगर ज़रूरी हो तो नया पेज जोड़ें:

```csharp
// पीडीएफ दस्तावेज़ में एक रिक्त पृष्ठ जोड़ता है
Page page = pdfDocument.Pages.Count > 0 ? pdfDocument.Pages[1] : pdfDocument.Pages.Add();
```

कोड की यह पंक्ति जाँचती है कि दस्तावेज़ में पहले से कोई पेज है या नहीं। यदि हाँ, तो यह पहला पेज चुनता है (`Pages[1]`) अन्यथा, यह एक रिक्त पृष्ठ बनाता है और उसे पीडीएफ में जोड़ देता है।

इसे ऐसे समझें जैसे कि एक खाली नोटबुक खोलें और यदि उसमें कुछ भी न हो तो पहले पृष्ठ पर लिखें - आसान है, है ना?

## चरण 3: पृष्ठ की ऊंचाई और चौड़ाई की जानकारी प्राप्त करें

अब जबकि हमारे पास काम करने के लिए एक पेज है, तो चलिए पेज के आयाम प्राप्त करते हैं। हम इसका उपयोग करेंगे `GetPageRect()` ऊंचाई और चौड़ाई प्राप्त करने की विधि.

```csharp
// पृष्ठ की ऊंचाई और चौड़ाई की जानकारी प्राप्त करें
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

यहाँ, `GetPageRect(true)` एक आयत लौटाता है जिसमें पृष्ठ की ऊंचाई और चौड़ाई शामिल होती है। यह एक रूलर से कागज़ के टुकड़े को मापने जैसा है। आउटपुट कंसोल में प्रदर्शित किया जाएगा, जो आपको वर्तमान पृष्ठ आयाम देगा।

## चरण 4: पृष्ठ को 90 डिग्री घुमाएँ

क्या आप पेज को घुमाना चाहते हैं? कोई समस्या नहीं! एक साधारण गुण के साथ, आप पेज को 90 डिग्री तक घुमा सकते हैं।

```csharp
// पृष्ठ को 90 डिग्री कोण पर घुमाएँ
page.Rotate = Rotation.on90;
```

यह चरण पृष्ठ को 90 डिग्री तक दक्षिणावर्त घुमाता है। कल्पना करें कि आप अपने डेस्क पर एक मुद्रित शीट को घुमा रहे हैं - अब यह लैंडस्केप मोड में है!

## चरण 5: रोटेशन के बाद पृष्ठ के आयामों की पुनः जाँच करें

पेज को घुमाने के बाद, आयामों को फिर से जांचना एक अच्छा विचार है। क्यों? क्योंकि घुमाव इस बात को प्रभावित कर सकता है कि आप ऊंचाई और चौड़ाई की व्याख्या कैसे करते हैं।

```csharp
// पृष्ठ की ऊंचाई और चौड़ाई की जानकारी प्राप्त करें
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

अब, पेज के आयाम नए ओरिएंटेशन के आधार पर अपडेट किए जाएँगे। यह आपके फ़ोन पर फ़ोटो को घुमाने जैसा है - अचानक, चौड़ाई ऊँचाई बन जाती है, और इसके विपरीत।


## निष्कर्ष

बधाई हो! आपने सफलतापूर्वक सीख लिया है कि .NET के लिए Aspose.PDF का उपयोग करके PDF पृष्ठ के आयामों को कैसे प्राप्त और संशोधित किया जाए। अब तक, आपको PDF लोड करने, उसके पृष्ठ आयामों की जाँच करने और ज़रूरत पड़ने पर पृष्ठ को घुमाने में भी सक्षम होना चाहिए।

PDF में हेरफेर करना जटिल नहीं है। Aspose.PDF के साथ, यह कुछ चरणों का पालन करने और सहज तरीकों का उपयोग करने जितना आसान है। तो अगली बार जब आपको PDF पेज आयामों को संभालने की आवश्यकता होगी, तो आपको पता होगा कि क्या करना है!

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं पृष्ठ को 90 डिग्री के अतिरिक्त अन्य कोणों से भी घुमा सकता हूँ?
हां, Aspose.PDF आपको 0, 90, 180, या 270 डिग्री तक पृष्ठों को घुमाने की अनुमति देता है `Rotation` संपत्ति।

### यदि मेरे PDF में कोई पृष्ठ नहीं है तो क्या होगा?
यदि आपके पीडीएफ में कोई पृष्ठ नहीं है, तो आप इसका उपयोग करके एक रिक्त पृष्ठ जोड़ सकते हैं `Pages.Add()` विधि, जैसा कि इस ट्यूटोरियल में दिखाया गया है।

### क्या मैं एक साथ कई पृष्ठों में हेरफेर कर सकता हूँ?
हां, आप एकाधिक पृष्ठों पर जा सकते हैं और उन सभी पर आकार बदलने या घुमाने जैसे परिवर्तन लागू कर सकते हैं।

### क्या पृष्ठ आयाम पीडीएफ के अंदर की सामग्री को प्रभावित करते हैं?
पेज के आयाम केवल कैनवास के आकार को बदलते हैं, सामग्री को नहीं। हालाँकि, आकार बदलने से पेज पर सामग्री के दिखने का तरीका बदल सकता है।

### मैं .NET के लिए Aspose.PDF के बारे में अधिक जानकारी कहां पा सकता हूं?
आप यहां जा सकते हैं [दस्तावेज़ यहाँ](https://reference.aspose.com/pdf/net/) अधिक विस्तृत जानकारी और उन्नत उपयोग मामलों के लिए.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}