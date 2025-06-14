---
"description": "इस व्यापक ट्यूटोरियल में .NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइलों से बुकमार्क पृष्ठ संख्या निकालने का तरीका जानें।"
"linktitle": "बुकमार्क पेज नंबर को पीडीएफ फाइल में प्राप्त करें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "बुकमार्क पेज नंबर को पीडीएफ फाइल में प्राप्त करें"
"url": "/hi/net/programming-with-bookmarks/get-bookmark-page-number/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# बुकमार्क पेज नंबर को पीडीएफ फाइल में प्राप्त करें

## परिचय

डिजिटल युग में, पीडीएफ दस्तावेजों को कुशलतापूर्वक प्रबंधित करना व्यक्तिगत और व्यावसायिक उपयोग दोनों के लिए महत्वपूर्ण है। चाहे आप अपने एप्लिकेशन को बेहतर बनाने के इच्छुक डेवलपर हों या अपने दस्तावेज़ों को व्यवस्थित करने की आवश्यकता वाले व्यावसायिक पेशेवर हों, पीडीएफ में हेरफेर करने का तरीका समझना आपका समय और प्रयास बचा सकता है। पीडीएफ प्रबंधन की आवश्यक विशेषताओं में से एक बुकमार्क और उनके संबंधित पृष्ठ संख्याओं को निकालने की क्षमता है। इस ट्यूटोरियल में, हम .NET के लिए Aspose.PDF का उपयोग करके इसे प्राप्त करने का तरीका जानेंगे, एक शक्तिशाली लाइब्रेरी जो पीडीएफ हेरफेर को सरल बनाती है।

## आवश्यक शर्तें

कोड में आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

1. विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके मशीन पर विज़ुअल स्टूडियो स्थापित है। यह आपका विकास वातावरण होगा।
2. .NET के लिए Aspose.PDF: आपके पास Aspose.PDF लाइब्रेरी होनी चाहिए। आप इसे यहाँ से डाउनलोड कर सकते हैं। [वेबसाइट](https://releases.aspose.com/pdf/net/).
3. C# का बुनियादी ज्ञान: C# प्रोग्रामिंग से परिचित होने से आपको कोड स्निपेट को बेहतर ढंग से समझने में मदद मिलेगी।

## पैकेज आयात करें

आरंभ करने के लिए, आपको अपने C# प्रोजेक्ट में आवश्यक पैकेज आयात करने होंगे। आप यह कैसे कर सकते हैं, यहाँ बताया गया है:

1. अपना विज़ुअल स्टूडियो प्रोजेक्ट खोलें.
2. सॉल्यूशन एक्सप्लोरर में अपने प्रोजेक्ट पर राइट-क्लिक करें और "मैनेज नुगेट पैकेजेस" चुनें।
3. निम्न को खोजें `Aspose.PDF` और नवीनतम संस्करण स्थापित करें.

अब जब आपने सब कुछ सेट कर लिया है, तो आइए बुकमार्क पृष्ठ संख्या निकालने की प्रक्रिया को चरण दर चरण समझें।

## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें

बुकमार्क निकालने से पहले, आपको अपने PDF दस्तावेज़ का पथ निर्दिष्ट करना होगा। यह वह जगह है जहाँ आपकी PDF फ़ाइल स्थित है।

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

इस चरण में, प्रतिस्थापित करें `"YOUR DOCUMENT DIRECTORY"` वास्तविक पथ के साथ जहाँ आपकी PDF फ़ाइल संग्रहीत है। यह पथ महत्वपूर्ण है क्योंकि यह प्रोग्राम को बताता है कि जिस PDF फ़ाइल के साथ आप काम करना चाहते हैं उसे कहाँ देखना है।

## चरण 2: PdfBookmarkEditor इंस्टेंस बनाएं

इसके बाद, आपको इसका एक उदाहरण बनाना होगा `PdfBookmarkEditor` क्लास. यह क्लास पीडीएफ फाइलों में बुकमार्क्स में हेरफेर करने के तरीके प्रदान करता है।

```csharp
// Pdfबुकमार्कएडिटर बनाएं
PdfBookmarkEditor bookmarkEditor = new PdfBookmarkEditor();
```

यहाँ, हम उदाहरण दे रहे हैं `PdfBookmarkEditor`यह ऑब्जेक्ट हमें अपनी पीडीएफ फाइल को बांधने और उसमें से बुकमार्क निकालने की अनुमति देगा।

## चरण 3: पीडीएफ फाइल खोलें

अब, पीडीएफ फाइल को बाइंड करने का समय आ गया है `PdfBookmarkEditor` आपके द्वारा अभी बनाया गया उदाहरण.

```csharp
// पीडीएफ फाइल खोलें
bookmarkEditor.BindPdf(dataDir + "GetBookmarks.pdf");
```

इस पंक्ति में, हम प्रयोग कर रहे हैं `BindPdf` नामक पीडीएफ फाइल को खोलने की विधि `GetBookmarks.pdf`सुनिश्चित करें कि यह फ़ाइल निर्दिष्ट निर्देशिका में मौजूद है; अन्यथा, आपको एक त्रुटि का सामना करना पड़ेगा।

## चरण 4: बुकमार्क निकालें

पीडीएफ फाइल खुलने के बाद, आप अब इसका उपयोग करके बुकमार्क निकाल सकते हैं `ExtractBookmarks` तरीका।

```csharp
// बुकमार्क निकालें
Aspose.Pdf.Facades.Bookmarks bookmarks = bookmarkEditor.ExtractBookmarks();
```

यह चरण पीडीएफ फ़ाइल से सभी बुकमार्क्स को पुनर्प्राप्त करता है और उन्हें नामक एक चर में संग्रहीत करता है `bookmarks`यह वेरिएबल सभी बुकमार्क जानकारी रखेगा जिसे हम अगले चरण में संसाधित करेंगे।

## चरण 5: बुकमार्क के माध्यम से पुनरावृति करें

अब जब आपके पास बुकमार्क्स हैं, तो आप उनके शीर्षक और पृष्ठ संख्या प्रदर्शित करने के लिए उनमें लूप कर सकते हैं।

```csharp
foreach (Aspose.Pdf.Facades.Bookmark bookmark in bookmarks)
{
    string strLevelSeprator = string.Empty;
    for (int i = 1; i < bookmark.Level; i++)
    {
        strLevelSeprator += "----";
    }
    Console.WriteLine("{0}Title: {1}", strLevelSeprator, bookmark.Title);
    Console.WriteLine("{0}Page Number: {1}", strLevelSeprator, bookmark.PageNumber);
    Console.WriteLine("{0}Page Action: {1}", strLevelSeprator, bookmark.Action);
}
```

इस लूप में, हम प्रत्येक बुकमार्क के माध्यम से पुनरावृत्ति कर रहे हैं। प्रत्येक बुकमार्क के लिए, हम उसके स्तर के आधार पर एक स्ट्रिंग विभाजक बनाते हैं (बुकमार्क के पदानुक्रम को दृष्टिगत रूप से दर्शाने के लिए)। फिर, हम कंसोल पर प्रत्येक बुकमार्क से जुड़े शीर्षक, पृष्ठ संख्या और क्रिया को प्रिंट करते हैं।

## निष्कर्ष

.NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइल से बुकमार्क पेज नंबर निकालना एक सीधी प्रक्रिया है। इस ट्यूटोरियल में बताए गए चरणों का पालन करके, आप अपने PDF दस्तावेज़ों में बुकमार्क को कुशलतापूर्वक प्रबंधित कर सकते हैं। चाहे आप कोई एप्लिकेशन विकसित कर रहे हों या बस अपने PDF को व्यवस्थित करने की आवश्यकता हो, यह ज्ञान निस्संदेह काम आएगा।

## अक्सर पूछे जाने वाले प्रश्न

### .NET के लिए Aspose.PDF क्या है?
.NET के लिए Aspose.PDF एक लाइब्रेरी है जो डेवलपर्स को प्रोग्रामेटिक रूप से PDF दस्तावेज़ बनाने, हेरफेर करने और परिवर्तित करने की अनुमति देती है।

### क्या मैं Aspose.PDF का निःशुल्क उपयोग कर सकता हूँ?
हां, Aspose एक निःशुल्क परीक्षण संस्करण प्रदान करता है जिसका उपयोग आप लाइब्रेरी का मूल्यांकन करने के लिए कर सकते हैं। आप इसे डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/).

### मैं Aspose.PDF के लिए दस्तावेज़ कहां पा सकता हूं?
दस्तावेज़ उपलब्ध है [यहाँ](https://reference.aspose.com/pdf/net/).

### मैं Aspose.PDF के लिए लाइसेंस कैसे खरीदूं?
आप यहां से लाइसेंस खरीद सकते हैं [खरीद पृष्ठ](https://purchase.aspose.com/buy).

### यदि मुझे कोई समस्या आए तो मुझे क्या करना चाहिए?
यदि आपको कोई समस्या आती है तो आप सहायता ले सकते हैं [Aspose समर्थन मंच](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}