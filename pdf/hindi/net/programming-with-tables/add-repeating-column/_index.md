---
"description": ".NET के लिए Aspose.PDF का उपयोग करके PDF दस्तावेज़ों में दोहराए जाने वाले कॉलम जोड़ने का तरीका जानें। उदाहरणों और कोड के साथ चरण-दर-चरण मार्गदर्शिका। डेवलपर्स के लिए बिल्कुल सही।"
"linktitle": "पीडीएफ दस्तावेज़ में दोहराए जाने वाले कॉलम जोड़ें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "पीडीएफ दस्तावेज़ में दोहराए जाने वाले कॉलम जोड़ें"
"url": "/hi/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# पीडीएफ दस्तावेज़ में दोहराए जाने वाले कॉलम जोड़ें

## परिचय

यदि आप PDF दस्तावेज़ों के साथ काम कर रहे हैं और आपको दोहराए जाने वाले कॉलम जोड़ने की आवश्यकता है, तो आप सही जगह पर हैं! .NET के लिए Aspose.PDF का उपयोग करके, आप PDF में आसानी से तालिकाओं और सामग्री का प्रबंधन कर सकते हैं। चाहे आप गतिशील रिपोर्ट, चालान या कोई अन्य संरचित दस्तावेज़ बना रहे हों, दोहराए जाने वाले कॉलम डेटा को व्यवस्थित करने में गेम-चेंजर हो सकते हैं। आइए PDF दस्तावेज़ में दोहराए जाने वाले कॉलम जोड़ने के तरीके पर चरण-दर-चरण मार्गदर्शिका में गोता लगाएँ।

## आवश्यक शर्तें

कोड में जाने से पहले, आइए सुनिश्चित करें कि आपने सब कुछ सेट कर लिया है:

- .NET के लिए Aspose.PDF: आपको अपने प्रोजेक्ट में .NET के लिए Aspose.PDF लाइब्रेरी स्थापित करनी होगी।
- [.NET के लिए Aspose.PDF डाउनलोड करें](https://releases.aspose.com/pdf/net/)
- [मुफ्त परीक्षण](https://releases.aspose.com/)
- विकास वातावरण: सुनिश्चित करें कि आपके पास Visual Studio जैसा .NET संगत IDE स्थापित है।
- C# की बुनियादी समझ: यद्यपि हम सब कुछ विस्तार से समझाएंगे, लेकिन C# की बुनियादी समझ आपको इसे आसानी से समझने में मदद करेगी।
  
यदि आपके पास अभी तक .NET के लिए Aspose.PDF नहीं है, तो आप प्राप्त कर सकते हैं [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/) इसकी विशेषताओं का अन्वेषण शुरू करने के लिए।

## पैकेज आयात करें

आरंभ करने के लिए, आपको .NET के लिए Aspose.PDF से आवश्यक नामस्थान आयात करने होंगे। आप इसे इस प्रकार कर सकते हैं:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

ये पैकेज पीडीएफ दस्तावेजों के साथ काम करने और तालिकाओं में हेरफेर करने के लिए आवश्यक कक्षाएं और विधियां प्रदान करते हैं।

अब, आइए एक पीडीएफ दस्तावेज़ में दोहराए जाने वाले कॉलम जोड़ने के लिए प्रक्रिया को कई चरणों में विभाजित करें। आगे बढ़ते रहें!

## चरण 1: अपने दस्तावेज़ निर्देशिका का पथ सेट करें

किसी भी फ़ाइल को बनाने या उसमें बदलाव करने से पहले, हमें वह पथ निर्धारित करना होगा जहाँ जेनरेट की गई PDF को सहेजा जाएगा। अपने C# प्रोजेक्ट में, उस निर्देशिका पथ को सेट करें जहाँ आपकी फ़ाइलें स्थित होंगी:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

यह पथ उस निर्देशिका की ओर इंगित करता है जहाँ आउटपुट पीडीएफ़ सहेजा जाएगा। `"YOUR DOCUMENT DIRECTORY"` आपके मशीन पर वास्तविक पथ के साथ.

## चरण 2: एक नया पीडीएफ दस्तावेज़ बनाएँ

आरंभ करने के लिए, एक नया उदाहरण बनाएं `Document` यह पीडीएफ के सभी पृष्ठों और सामग्री के लिए कंटेनर के रूप में काम करेगा।

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

यहाँ, हमने एक नया पीडीएफ दस्तावेज़ बनाया है और इसमें एक खाली पृष्ठ जोड़ा है। `doc.Pages.Add()` विधि दस्तावेज़ में एक नया पृष्ठ सम्मिलित करती है।

## चरण 3: बाहरी तालिका को तत्कालित करें

इसके बाद, हम एक बाहरी तालिका बनाते हैं। यह तालिका पृष्ठ की पूरी चौड़ाई में फैलेगी और अन्य तालिकाओं के लिए एक कंटेनर के रूप में काम करेगी, जिसमें दोहराए जाने वाले कॉलम वाली तालिका भी शामिल होगी।

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

हमने निर्धारित किया है `ColumnWidths` प्रॉपर्टी को "100%" पर सेट करने का अर्थ है कि तालिका पूरे पृष्ठ की चौड़ाई में फैल जाएगी।

## चरण 4: आंतरिक तालिका बनाएं

अब, आइए आंतरिक तालिका बनाएं, जिसमें दोहराए जाने वाले कॉलम होंगे। यहाँ मुख्य गुण हैं `Broken`, जो तालिका को उसी पृष्ठ पर जारी रखने की अनुमति देता है, और `ColumnAdjustment`, जो सामग्री को फिट करने के लिए कॉलम की चौड़ाई को स्वचालित रूप से समायोजित करता है।

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

यह आंतरिक तालिका बाहरी तालिका के भीतर स्थित होगी।

## चरण 5: पेज पर तालिकाएँ जोड़ें

अब जब हमारे पास बाहरी और आंतरिक दोनों टेबल तैयार हैं, तो उन्हें पेज में जोड़ें। यह चरण सुनिश्चित करता है कि टेबल दस्तावेज़ की संरचना में शामिल हैं।

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

यहाँ, हमने जोड़ा `outerTable` पृष्ठ पर, और फिर बाहरी तालिका के भीतर, हमने नेस्ट किया `mytable`इसके अतिरिक्त, हमने सेट किया है `RepeatingColumnsCount` 5 पर सेट करें, यह निर्दिष्ट करते हुए कि डेटा जोड़ते समय कितने कॉलम दोहराए जाने चाहिए।

## चरण 6: हेडर पंक्ति जोड़ें

अब तालिका में हेडर जोड़ने का समय आ गया है। हेडर पंक्ति डेटा को संदर्भ देती है और कॉलम की संरचना में मदद करती है। 

```csharp
Aspose.Pdf.Row row = mytable.Rows.Add();
row.Cells.Add("header 1");
row.Cells.Add("header 2");
row.Cells.Add("header 3");
row.Cells.Add("header 4");
row.Cells.Add("header 5");
row.Cells.Add("header 6");
row.Cells.Add("header 7");
row.Cells.Add("header 11");
row.Cells.Add("header 12");
row.Cells.Add("header 13");
row.Cells.Add("header 14");
row.Cells.Add("header 15");
row.Cells.Add("header 16");
row.Cells.Add("header 17");
```

यह कोड स्निपेट पहली पंक्ति (जिसे हम हेडर के रूप में उपयोग करेंगे) जोड़ता है, और इसे “हेडर 1”, “हेडर 2”, इत्यादि जैसे पाठ वाले कक्षों से भर देता है।

## चरण 7: डेटा पंक्तियाँ जोड़ें

अंत में, हम तालिका में कुछ डेटा जोड़ सकते हैं। यह लूप गतिशील रूप से पंक्तियाँ बनाता है और कोशिकाओं को सामग्री से भरता है:

```csharp
for (int RowCounter = 0; RowCounter <= 5; RowCounter++)
{
    Aspose.Pdf.Row row1 = mytable.Rows.Add();
    row1.Cells.Add("col " + RowCounter.ToString() + ", 1");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 2");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 3");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 4");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 5");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 6");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 7");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 11");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 12");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 13");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 14");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 15");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 16");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 17");
}
```

लूप छह बार दोहराया जाता है, पंक्तियों को जोड़ता है और प्रत्येक सेल को संबंधित कॉलम डेटा (जैसे, "कॉलम 1, 1", "कॉलम 2, 2", आदि) से भरता है।

## चरण 8: दस्तावेज़ सहेजें

एक बार सभी पंक्तियाँ और कॉलम जोड़ दिए जाने के बाद, अंतिम चरण दस्तावेज़ को निर्दिष्ट फ़ाइल पथ पर सहेजना है।

```csharp
doc.Save(outFile);
```

आपका दस्तावेज़ अब दोहराए गए कॉलम के साथ सहेजा गया है!

## निष्कर्ष

बस, अब यह हो गया! इन सरल चरणों के साथ, आप .NET के लिए Aspose.PDF का उपयोग करके दोहराए जाने वाले कॉलम के साथ एक PDF दस्तावेज़ बना सकते हैं। नेस्टेड टेबल की लचीलेपन का लाभ उठाकर, आप जटिल लेआउट प्राप्त कर सकते हैं जो आपके PDF को पेशेवर और व्यवस्थित बनाते हैं। अपने अगले प्रोजेक्ट के लिए इसे आज़माएँ और अपनी PDF जनरेशन आवश्यकताओं को पूरा करने के लिए Aspose.PDF की पूरी क्षमता का पता लगाएँ।

## अक्सर पूछे जाने वाले प्रश्न

### .NET के लिए Aspose.PDF क्या है?
.NET के लिए Aspose.PDF एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को प्रोग्रामेटिक रूप से PDF दस्तावेज़ बनाने, संपादित करने और प्रबंधित करने की अनुमति देती है।

### क्या मैं दोहराए जाने वाले स्तंभों की संख्या को गतिशील रूप से समायोजित कर सकता हूँ?
हां, आप संशोधित करके दोहराए जाने वाले स्तंभों की संख्या बदल सकते हैं `RepeatingColumnsCount` संपत्ति।

### मैं .NET के लिए Aspose.PDF पर लाइसेंस कैसे लागू कर सकता हूं?
आप निम्नांकित तरीके से किसी फ़ाइल या स्ट्रीम से लाइसेंस लागू कर सकते हैं: [प्रलेखन](https://reference.aspose.com/pdf/net/).

### क्या तालिका कक्षों में छवियाँ जोड़ना संभव है?
हां, .NET के लिए Aspose.PDF तालिका कक्षों में छवियों सहित विभिन्न प्रकार की सामग्री जोड़ने का समर्थन करता है।

### क्या मैं टेबल लेआउट को और अधिक अनुकूलित कर सकता हूँ?
बिल्कुल! Aspose.PDF टेबल शैलियों को अनुकूलित करने के लिए व्यापक सुविधाएँ प्रदान करता है, जिसमें बॉर्डर, पैडिंग, संरेखण और बहुत कुछ शामिल है।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}