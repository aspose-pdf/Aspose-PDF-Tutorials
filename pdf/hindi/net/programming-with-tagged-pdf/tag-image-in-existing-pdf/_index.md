---
"description": ".NET के लिए Aspose.PDF का उपयोग करके मौजूदा PDF में छवियों को टैग करना सीखें। PDF/UA अनुपालन के साथ पहुँच क्षमता बढ़ाने के लिए चरण-दर-चरण मार्गदर्शिका।"
"linktitle": "मौजूदा PDF में छवि टैग करें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "मौजूदा PDF में छवि टैग करें"
"url": "/hi/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# मौजूदा PDF में छवि टैग करें

## परिचय

इस ट्यूटोरियल में, हम आपको बताएंगे कि .NET के लिए Aspose.PDF का उपयोग करके किसी मौजूदा PDF में किसी छवि को कैसे टैग किया जाए। इस गाइड के अंत तक, आप छवियों के लिए वैकल्पिक टेक्स्ट सेट करने, लेआउट विशेषताओं को समायोजित करने और यह सुनिश्चित करने में सक्षम होंगे कि आपका PDF पहुँच मानकों का अनुपालन करता है।

## आवश्यक शर्तें

इससे पहले कि हम आगे बढ़ें, आइए जानें कि शुरुआत करने के लिए आपको क्या चाहिए:

- .NET के लिए Aspose.PDF: सुनिश्चित करें कि आपने .NET के लिए Aspose.PDF का नवीनतम संस्करण डाउनलोड और इंस्टॉल किया है। [यहां से डाउनलोड करें](https://releases.aspose.com/pdf/net/).
- .NET फ्रेमवर्क: सुनिश्चित करें कि आपके पास Visual Studio जैसा .NET विकास वातावरण स्थापित है।
- पीडीएफ संरचना की बुनियादी समझ: पैराग्राफ, स्पैन, टेबल और छवियों जैसे पीडीएफ संरचना तत्वों से परिचित होना।
- वैध लाइसेंस: आप या तो लाइसेंस खरीद सकते हैं [यहाँ](https://purchase.aspose.com/buy) या अस्थायी का उपयोग करें [यहाँ](https://purchase.aspose.com/temporary-license/).

## पैकेज आयात करें

कोडिंग शुरू करने के लिए, आपको .NET के लिए Aspose.PDF से आवश्यक नेमस्पेस आयात करने की आवश्यकता है। ये आपको PDF दस्तावेज़ में हेरफेर करने के लिए आवश्यक क्लास और विधियों तक पहुँच प्रदान करेंगे।

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

अब जबकि हमने मंच तैयार कर लिया है, आइए एक छवि को टैग करने की प्रक्रिया को कई चरणों में विभाजित करें।

## चरण 1: मौजूदा PDF दस्तावेज़ लोड करें

पहला कदम उस पीडीएफ फाइल को लोड करना है जिसके साथ आप काम करना चाहते हैं। यह कोई भी पीडीएफ फाइल हो सकती है जिसमें वह छवि हो जिसे आप टैग करना चाहते हैं।

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// दस्तावेज़ खोलें
Document document = new Document(inFile);
```

- प्रतिस्थापित करें `"YOUR DOCUMENT DIRECTORY"` आपकी फ़ाइल का वास्तविक पथ सहित.
- The `Document` क्लास आपको मौजूदा पीडीएफ लोड करने की अनुमति देता है। आप छवि को टैग करने के लिए इस पीडीएफ को संशोधित करेंगे।

## चरण 2: टैग की गई सामग्री और मूल संरचना तत्व तक पहुंचें

एक बार जब आप पीडीएफ खोल लेते हैं, तो अगला चरण टैग की गई सामग्री तक पहुंचना और मूल संरचना तत्व की पहचान करना है। यह महत्वपूर्ण है क्योंकि यह आपको पीडीएफ में तत्वों के माध्यम से नेविगेट करने और संशोधन करने की अनुमति देता है।

```csharp
// टैग की गई सामग्री और मूल संरचना तत्व प्राप्त करें
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` पीडीएफ में संरचित तत्वों तक पहुंच प्रदान करता है।
- The `RootElement` यह सबसे ऊपरी संरचना तत्व है, जहां से आप पैराग्राफ, तालिकाओं और छवियों जैसे अन्य तत्वों तक जा सकते हैं।

## चरण 3: टैग किए गए PDF दस्तावेज़ के लिए शीर्षक सेट करें

टैग किए गए PDF दस्तावेज़ में शीर्षक जोड़ने से यह सुनिश्चित होता है कि आपके दस्तावेज़ को उचित रूप से लेबल किया गया है, जो पहुंच और PDF/UA अनुपालन के लिए उपयोगी है।

```csharp
// टैग किए गए PDF दस्तावेज़ के लिए शीर्षक सेट करें
taggedContent.SetTitle("Document with images");
```

- अपने टैग किए गए पीडीएफ के लिए शीर्षक सेट करने से पहुंच में वृद्धि होती है और स्क्रीन रीडर्स और सहायक प्रौद्योगिकियों के लिए दस्तावेज़ की स्पष्टता में सुधार होता है।

## चरण 4: छवि ढूंढें और टैग करें

अब, आइए छवि तत्व (जिसे a . कहा जाता है) ढूंढें `FigureElement` Aspose.PDF में), इसके लिए एक वैकल्पिक पाठ सेट करें, और इसके लेआउट विशेषताओं को कॉन्फ़िगर करें।

```csharp
// सभी चित्र तत्वों (छवियों) के माध्यम से लूप करें और वैकल्पिक पाठ और लेआउट विशेषताएँ सेट करें
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // चित्र के लिए वैकल्पिक पाठ सेट करें
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // BBox विशेषता (बाउंडिंग बॉक्स) बनाएं और सेट करें
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // आकृति के लिए लेआउट विशेषताएँ सेट करें
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- यह कोड सभी लूपों से होकर गुजरता है `FigureElement` मूल संरचना में ऑब्जेक्ट, जो छवियों का प्रतिनिधित्व करते हैं।
- यह सुलभता के लिए वैकल्पिक पाठ निर्धारित करता है (स्क्रीन रीडर इसका उपयोग छवि का वर्णन करने के लिए करेंगे)।
- बाउंडिंग बॉक्स (`BBox`) छवि के लेआउट के लिए निर्देशांक निर्दिष्ट करता है, यह सुनिश्चित करता है कि यह दस्तावेज़ में सही ढंग से प्रदर्शित हो।

## चरण 5: तालिका के भीतर स्पैन तत्वों को संशोधित करें

कुछ मामलों में, आपको टेबल के अंदर स्पैन एलिमेंट को संशोधित करने की आवश्यकता हो सकती है। यहाँ, हम दिखाएंगे कि कैसे स्पैन एलिमेंट को ढूँढ़ा जाए। `SpanElement` और इसे एक पैराग्राफ में ले जाएं.

```csharp
// तालिका, अवधि और पैराग्राफ़ तत्व खोजें
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// स्पैन तत्व को पैराग्राफ़ में ले जाएँ
spanElement.ChangeParentElement(paragraph);
```

- यहाँ, हम पाते हैं `TableElement`, `SpanElement`, और `ParagraphElement` पीडीएफ के भीतर.
- का उपयोग `ChangeParentElement` विधि में, हम उचित टैगिंग और संरचना सुनिश्चित करने के लिए स्पैन को पैराग्राफ में ले जाते हैं।

## चरण 6: दस्तावेज़ सहेजें और PDF/UA अनुपालन को मान्य करें

एक बार सभी परिवर्तन हो जाने के बाद, अंतिम चरण अद्यतन पीडीएफ को सहेजना और यह जांचना है कि क्या यह पीडीएफ/यूए मानकों का अनुपालन करता है।

```csharp
// अपडेट किया गया PDF दस्तावेज़ सहेजें
document.Save(outFile);

// PDF/UA अनुपालन को सत्यापित करें
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- The `Validate` विधि पीडीएफ दस्तावेज़ को पीडीएफ/यूए मानकों के विरुद्ध जांचती है और परिणामों को लॉग करती है।
- अनुपालन सुनिश्चित करने से पहुंच में सुधार करने और दस्तावेज़ प्रकाशन के लिए नियामक आवश्यकताओं को पूरा करने में मदद मिलती है।

## निष्कर्ष

इस ट्यूटोरियल में, हमने आपको .NET के लिए Aspose.PDF का उपयोग करके किसी मौजूदा PDF में छवियों को टैग करने का तरीका दिखाया है। वैकल्पिक टेक्स्ट सेट करके, लेआउट विशेषताओं को समायोजित करके, और PDF/UA अनुपालन के लिए दस्तावेज़ को मान्य करके, आप यह सुनिश्चित कर सकते हैं कि आपके PDF सुलभ हैं और आधुनिक मानकों को पूरा करते हैं। Aspose.PDF संरचित तत्वों के साथ काम करना आसान बनाता है, जिससे आपको अपने दस्तावेज़ के लेआउट और पहुँच पर नियंत्रण मिलता है।

## अक्सर पूछे जाने वाले प्रश्न

### .NET के लिए Aspose.PDF का उपयोग किस लिए किया जाता है?
.NET के लिए Aspose.PDF एक शक्तिशाली लाइब्रेरी है जिसका उपयोग .NET वातावरण में प्रोग्रामेटिक रूप से PDF दस्तावेज़ों को बनाने, संपादित करने और हेरफेर करने के लिए किया जाता है।

### मैं PDF/UA अनुपालन कैसे सुनिश्चित करूँ?
आप Aspose.PDF का उपयोग कर सकते हैं `Validate` दस्तावेज़ में संशोधन करने के बाद पीडीएफ/यूए अनुपालन की जांच करने की विधि।

### पीडीएफ में वैकल्पिक पाठ क्या है?
वैकल्पिक पाठ एक विवरण है जो पीडीएफ फाइलों में छवियों के साथ जोड़ा जाता है, ताकि पहुंच में सुधार हो सके, खासकर उन उपयोगकर्ताओं के लिए जो स्क्रीन रीडर पर निर्भर रहते हैं।

### क्या मैं Aspose.PDF के साथ PDF में तालिकाओं और स्पैन में हेरफेर कर सकता हूं?
हां, Aspose.PDF आपको PDF दस्तावेज़ के भीतर तालिकाओं, स्पैन और अन्य संरचित तत्वों में हेरफेर करने की अनुमति देता है।

### मैं .NET के लिए Aspose.PDF कहां से डाउनलोड कर सकता हूं?
आप .NET के लिए Aspose.PDF का नवीनतम संस्करण डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}