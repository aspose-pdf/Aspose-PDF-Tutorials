---
"description": "जानें कि .NET के लिए Aspose.PDF का उपयोग करके PDF में रेडियो बटन कैप्शन कैसे सेट करें। यह चरण-दर-चरण मार्गदर्शिका आपको अपने PDF फ़ॉर्म को लोड करने, संशोधित करने और सहेजने के बारे में बताती है।"
"linktitle": "रेडियो बटन कैप्शन सेट करें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "रेडियो बटन कैप्शन सेट करें"
"url": "/hi/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# रेडियो बटन कैप्शन सेट करें

## परिचय

यदि आप .NET के लिए Aspose.PDF के साथ PDF में हेरफेर करना चाहते हैं, तो आपके लिए यह एक बेहतरीन अनुभव है! आज, हम एक व्यावहारिक सुविधा पर ध्यान केंद्रित कर रहे हैं: अपने PDF फ़ॉर्म में रेडियो बटन कैप्शन सेट करना। रेडियो बटन उपयोगकर्ता फ़ॉर्म के लिए आवश्यक हैं जहाँ आपको विकल्पों के एक सेट से चुनने की आवश्यकता होती है। उन्हें बहुविकल्पीय प्रश्नों के रूप में कल्पना करें जहाँ केवल एक उत्तर की अनुमति है। यह ट्यूटोरियल आपको PDF फ़ॉर्म में रेडियो बटन कैप्शन अपडेट करने की प्रक्रिया से गुजारेगा, ताकि आपके दस्तावेज़ इंटरैक्टिव और उपयोगकर्ता के अनुकूल दोनों हों। 

## आवश्यक शर्तें

कोड में गोता लगाने से पहले, आपको कुछ चीजें सुनिश्चित करनी होंगी:

1. .NET के लिए Aspose.PDF: सुनिश्चित करें कि आपके पास Aspose.PDF लाइब्रेरी स्थापित है। यह लाइब्रेरी आपको प्रोग्रामेटिक रूप से PDF फ़ाइलों में हेरफेर करने में मदद करेगी।
2. विकास परिवेश: आपके पास .NET विकास परिवेश स्थापित होना चाहिए, जैसे कि Visual Studio.
3. नमूना पीडीएफ फॉर्म: इस ट्यूटोरियल के लिए, आपको रेडियो बटन के साथ एक नमूना पीडीएफ फॉर्म की आवश्यकता होगी। आप किसी भी मौजूदा पीडीएफ फॉर्म का उपयोग कर सकते हैं या रेडियो बटन के साथ एक नया बना सकते हैं।
4. C# का बुनियादी ज्ञान: यह मार्गदर्शिका मानती है कि आपको C# और .NET प्रोग्रामिंग अवधारणाओं की बुनियादी समझ है।

यदि आपने अभी तक .NET के लिए Aspose.PDF स्थापित नहीं किया है या आपको एक अस्थायी लाइसेंस की आवश्यकता है, तो आप कर सकते हैं [यहाँ पर डाउनलोड करो](https://releases.aspose.com/pdf/net/) या [अस्थायी लाइसेंस प्राप्त करें](https://purchase.aspose.com/temporary-license/).

## पैकेज आयात करें

आरंभ करने के लिए, आपको अपने C# प्रोजेक्ट में आवश्यक पैकेज आयात करने होंगे। Aspose.PDF लाइब्रेरी को शामिल करने का तरीका इस प्रकार है:

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

सुनिश्चित करें कि आपने इन पैकेजों को NuGet या अपनी पसंदीदा विधि के माध्यम से अपने प्रोजेक्ट में जोड़ा है।

## चरण 1: पीडीएफ फॉर्म लोड करें

सबसे पहले, आपको पीडीएफ फॉर्म लोड करना होगा जिसमें रेडियो बटन शामिल हैं। `Aspose.Pdf.Facades.Form` इस उद्देश्य के लिए class का उपयोग किया जाता है। आप इसे इस प्रकार कर सकते हैं:

```csharp
// अपने दस्तावेज़ निर्देशिका का पथ निर्धारित करें
string dataDir = "YOUR DOCUMENT DIRECTORY";

// स्रोत पीडीएफ फॉर्म लोड करें
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

इस कोड स्निपेट में:
- `dataDir` वह पथ निर्दिष्ट करता है जहां आपका PDF स्थित है.
- `Form` क्लास का उपयोग पीडीएफ के भीतर फॉर्म फ़ील्ड के साथ इंटरैक्ट करने के लिए किया जाता है।
- `Document` क्लास पीडीएफ दस्तावेज़ के पृष्ठों तक पहुंच प्रदान करता है।

## चरण 2: रेडियो बटन फ़ील्ड के माध्यम से पुनरावृति करें

इसके बाद, आपको रेडियो बटन फ़ील्ड को पहचानने और उनमें बदलाव करने के लिए अपने फ़ॉर्म में फ़ील्ड को दोहराना होगा:

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

इस लूप में:
- `FieldNames` पीडीएफ में सभी फ़ील्ड नामों की सूची प्रदान करता है।
- `GetButtonOptionValues(item)` प्रत्येक रेडियो बटन के लिए उपलब्ध विकल्पों को पुनः प्राप्त करता है।

## चरण 3: रेडियो बटन विकल्प संशोधित करें

एक बार जब आप रेडियो बटन फ़ील्ड की पहचान कर लेते हैं, तो आप उनके विकल्पों को संशोधित कर सकते हैं। इसके लिए, आपको फ़ील्ड को कास्ट करना होगा `RadioButtonField` और इसके विकल्पों को अपडेट करें:

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

यहाँ:
- हम यह जांचते हैं कि फ़ील्ड नाम में "रेडियो1" है या नहीं, ताकि हम उस विशिष्ट रेडियो बटन फ़ील्ड की पहचान कर सकें जिसे हम संशोधित करना चाहते हैं।
- `RadioButtonField` विशिष्ट संशोधन करने के लिए फॉर्म फ़ील्ड से कास्ट किया जाता है।

## चरण 4: रेडियो बटन के लिए कैप्शन सेट करें

रेडियो बटन के लिए कैप्शन सेट या अपडेट करने के लिए, आपको एक बनाना होगा `TextFragment` और उपयोग करें `TextBuilder` इसे इच्छित स्थान पर रखने के लिए:

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // टेक्स्टपैराग्राफ ऑब्जेक्ट बनाएँ
        TextParagraph par = new TextParagraph();
        // पैराग्राफ़ स्थिति सेट करें
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // शब्द रैपिंग मोड निर्दिष्ट करें
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // पैराग्राफ़ में नया टेक्स्टफ़्रेगमेंट जोड़ें
        par.AppendLine(updatedFragment);
        // TextBuilder का उपयोग करके TextParagraph जोड़ें
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

इस हिस्से में:
- `TextFragment` इसका उपयोग पाठ और उसके स्वरूप को परिभाषित करने के लिए किया जाता है।
- `TextParagraph` पाठ को स्थान देने और प्रारूपित करने में मदद करता है.
- `TextBuilder` पीडीएफ के निर्दिष्ट पृष्ठ पर पाठ जोड़ता है।

## चरण 5: अपडेट की गई पीडीएफ को सेव करें

अंत में, अपडेट की गई पीडीएफ को एक नई फाइल में सेव करें:

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

इससे यह सुनिश्चित होगा कि:
- परिवर्तन पीडीएफ पर लागू किये जाते हैं।
- मूल रेडियो बटन विकल्प को निर्दिष्ट अनुसार हटा दिया गया है।

## निष्कर्ष

.NET के लिए Aspose.PDF का उपयोग करके PDF फ़ॉर्म में रेडियो बटन कैप्शन को संशोधित करने से आपके दस्तावेज़ों की अन्तरक्रियाशीलता और उपयोगिता में काफ़ी वृद्धि हो सकती है। इस ट्यूटोरियल में बताए गए चरणों के साथ, आप आसानी से PDF लोड कर सकते हैं, रेडियो बटन विकल्पों को अपडेट कर सकते हैं और अपने परिवर्तनों को सहेज सकते हैं। यह दृष्टिकोण फ़ॉर्म प्रबंधन के लिए आसान है और यह सुनिश्चित करता है कि आपके PDF आपके उपयोगकर्ताओं की सटीक ज़रूरतों को पूरा करें। Aspose.PDF में गोता लगाएँ और अन्य PDF हेरफेर के लिए इसकी क्षमताओं का पता लगाएँ!

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं एक साथ कई रेडियो बटन फ़ील्ड अपडेट कर सकता हूँ?
हां, आप सभी रेडियो बटन फ़ील्डों को पुनरावृत्त कर सकते हैं और आवश्यकतानुसार परिवर्तन लागू कर सकते हैं।

### क्या मुझे Aspose.PDF का उपयोग करने के लिए लाइसेंस की आवश्यकता है?
आप निःशुल्क परीक्षण के साथ शुरुआत कर सकते हैं, लेकिन विस्तारित उपयोग के लिए लाइसेंस की आवश्यकता होगी। [यहां से लाइसेंस प्राप्त करें](https://purchase.aspose.com/buy).

### मैं पीडीएफ को सेव करने से पहले परिवर्तनों का परीक्षण कैसे कर सकता हूँ?
आप अपने विकास परिवेश में पीडीएफ का पूर्वावलोकन कर सकते हैं या संशोधनों की जांच करने के लिए पीडीएफ व्यूअर का उपयोग कर सकते हैं।

### क्या Aspose.PDF .NET के सभी संस्करणों के साथ संगत है?
Aspose.PDF .NET के विभिन्न संस्करणों का समर्थन करता है। सुनिश्चित करें कि आप अपने विशिष्ट .NET संस्करण के साथ संगतता की जांच करें।

### क्या मैं इसी प्रकार अन्य फॉर्म फ़ील्ड में भी परिवर्तन कर सकता हूँ?
हां, इसी प्रकार की तकनीकों को पीडीएफ दस्तावेजों में अन्य प्रकार के फॉर्म फ़ील्ड पर भी लागू किया जा सकता है।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}