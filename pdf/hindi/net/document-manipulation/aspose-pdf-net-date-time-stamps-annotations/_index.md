---
"date": "2025-04-11"
"description": "जानें कि .NET के लिए Aspose.PDF का उपयोग करके अपने PDF दस्तावेज़ों में दिनांक और समय स्टैम्प या एनोटेशन को कुशलतापूर्वक कैसे जोड़ा जाए। इन आसान चरणों के साथ दस्तावेज़ प्रबंधन को बेहतर बनाएँ।"
"title": ".NET के लिए Aspose.PDF का उपयोग करके PDF में दिनांक और समय टिकट जोड़ें"
"url": "/hi/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# .NET के लिए Aspose.PDF का उपयोग करके PDF में दिनांक और समय टिकट जोड़ें

## परिचय

आज के डिजिटल युग में, व्यवसायों और व्यक्तियों के लिए प्रभावी दस्तावेज़ प्रबंधन महत्वपूर्ण है। अपने PDF में दिनांक और समय टिकट या एनोटेशन जोड़ने से डेटा अखंडता और संगठन को बढ़ाया जा सकता है। यह ट्यूटोरियल दर्शाता है कि .NET के लिए Aspose.PDF का उपयोग करके इन सुविधाओं को कैसे एकीकृत किया जाए।

**चाबी छीनना:**
- निर्दिष्ट PDF पृष्ठ पर वर्तमान दिनांक और समय को टेक्स्ट स्टैम्प के रूप में जोड़ें।
- दस्तावेज़ में इच्छित स्थानों पर मुक्त पाठ एनोटेशन बनाएँ।
- .NET के लिए Aspose.PDF के साथ इष्टतम प्रदर्शन के लिए सर्वोत्तम प्रथाओं का पालन करें।

## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास:

### आवश्यक लाइब्रेरी और संस्करण
- **.NET के लिए Aspose.PDF**: Adobe Acrobat के बिना PDF हेरफेर के लिए एक मजबूत लाइब्रेरी। संस्करण 21.x या बाद का उपयोग करें।

### पर्यावरण सेटअप आवश्यकताएँ
- .NET Framework 4.5+ या .NET Core 2.0+ के साथ विकास वातावरण
- विजुअल स्टूडियो या कोई अन्य IDE जो C# प्रोग्रामिंग का समर्थन करता है

### ज्ञान पूर्वापेक्षाएँ
- C# और .NET प्रोजेक्ट संरचनाओं की बुनियादी समझ
- निर्देशिका संरचना में फ़ाइलों को संभालने की जानकारी

## .NET के लिए Aspose.PDF सेट अप करना
निम्नलिखित में से किसी एक विधि का उपयोग करके Aspose.PDF स्थापित करें:

**.NET CLI का उपयोग करना:**
```bash
dotnet add package Aspose.PDF
```

**पैकेज मैनेजर का उपयोग करना:**
```powershell
Install-Package Aspose.PDF
```

**NuGet पैकेज मैनेजर UI के माध्यम से:**
- अपने IDE में NuGet पैकेज मैनेजर खोलें।
- "Aspose.PDF" खोजें और नवीनतम संस्करण स्थापित करें।

### लाइसेंस प्राप्ति चरण
Aspose.PDF का पूर्ण उपयोग करने के लिए:
1. **मुफ्त परीक्षण:** सभी सुविधाओं का पता लगाने के लिए एक अस्थायी लाइसेंस डाउनलोड करें.
2. **अस्थायी लाइसेंस:** यदि आवश्यक हो तो विस्तारित मूल्यांकन लाइसेंस का अनुरोध करें।
3. **खरीदना:** Aspose वेबसाइट से दीर्घकालिक उपयोग के लिए लाइसेंस खरीदें।

अपना लाइसेंस कोड में आरंभ करें:
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## कार्यान्वयन मार्गदर्शिका
आइए पीडीएफ में दिनांक और समय टिकट जोड़ें।

### फ़ीचर 1: PDF में दिनांक-समय स्टाम्प जोड़ें
यह सुविधा किसी निर्दिष्ट PDF दस्तावेज़ के प्रथम पृष्ठ पर वर्तमान दिनांक और समय को टेक्स्ट स्टैम्प के रूप में जोड़ देती है।

#### चरण-दर-चरण कार्यान्वयन

##### 1. मौजूदा पीडीएफ दस्तावेज़ खोलें
अपना लक्ष्य दस्तावेज़ लोड करें:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. वर्तमान दिनांक और समय को स्ट्रिंग के रूप में प्राप्त करें
वर्तमान दिनांक और समय को प्रारूपित करें:
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. वर्तमान दिनांक और समय के साथ टेक्स्ट स्टैम्प बनाएं
एक बनाने के `TextStamp` स्वरूपित स्ट्रिंग का उपयोग करके उदाहरण:
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. पहले पेज पर टेक्स्ट स्टैम्प जोड़ें
अपने दस्तावेज़ के पहले पृष्ठ पर स्टाम्प जोड़ें:
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5. FreeTextAnnotation बनाएं और जोड़ें (वैकल्पिक)
अधिक जटिल एनोटेशन के लिए, बनाएं `FreeTextAnnotation`:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6. संशोधित दस्तावेज़ सहेजें
अपने परिवर्तन सहेजें:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### फ़ीचर 2: पीडीएफ पर फ्रीटेक्स्ट एनोटेशन जोड़ें
किसी पीडीएफ दस्तावेज़ में किसी भी इच्छित स्थान पर निःशुल्क पाठ एनोटेशन जोड़ें।

#### चरण-दर-चरण कार्यान्वयन

##### 1. मौजूदा PDF दस्तावेज़ खोलें
अपना लक्ष्य दस्तावेज़ लोड करें:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. एनोटेशन के लिए आयत क्षेत्र को परिभाषित करें
पृष्ठ पर एनोटेशन को कहां रखना है, यह निर्दिष्ट करें:
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. निर्दिष्ट स्वरूप और स्थान के साथ FreeTextAnnotation बनाएँ
अपने एनोटेशन को इच्छित टेक्स्ट और उपस्थिति सेटिंग्स के साथ आरंभ करें:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. बॉर्डर स्टाइल सेट करें और एनोटेशन जोड़ें
सुनिश्चित करें कि बॉर्डर शैली आपकी आवश्यकताओं से मेल खाती है (इस मामले में अदृश्य):
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5. संशोधित दस्तावेज़ सहेजें
अपने दस्तावेज़ को नए जोड़े गए एनोटेशन के साथ सहेजें:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## व्यावहारिक अनुप्रयोगों
पीडीएफ में दिनांक स्टाम्प और एनोटेशन जोड़ना विभिन्न उद्योगों में उपयोगी है:
- **कानूनी दस्तावेजों**: परिवर्तनों को समयबद्ध करके अनुपालन सुनिश्चित करता है।
- **शैक्षणिक पत्र**: एनोटेशन के साथ सहयोगात्मक संपादन की सुविधा प्रदान करता है।
- **वित्तीय रिकॉर्ड**: टाइमस्टैम्प्ड रिपोर्ट के साथ सटीक ऑडिट ट्रेल्स बनाए रखता है।
- **तकनीकी दस्तावेज़ीकरण**: मैनुअल में अपडेट या महत्वपूर्ण नोट्स को हाइलाइट करता है।

## प्रदर्शन संबंधी विचार
.NET के लिए Aspose.PDF का उपयोग करते समय इष्टतम प्रदर्शन के लिए:
- **प्रचय संसाधन**: ओवरहेड को कम करने के लिए बैचों में कई पीडीएफ को संसाधित करें।
- **स्मृति प्रबंधन**: उपयोग `Dispose` प्रत्येक दस्तावेज़ को संसाधित करने के बाद मेमोरी संसाधनों को मुक्त करने की विधियाँ।
- **अनुकूलित फ़ॉन्ट और छवियाँ**: फ़ाइल आकार को कम करने के लिए फ़ॉन्ट प्रकार और छवि रिज़ॉल्यूशन को सीमित करें।

## निष्कर्ष
.NET के लिए Aspose.PDF को एकीकृत करने से आप PDF दस्तावेज़ों में दिनांक स्टैम्पिंग और एनोटेशन सुविधाएँ जोड़ सकते हैं, जिससे कार्यक्षमता में वृद्धि होती है। ये उपकरण डेटा अखंडता में सुधार करते हैं और दस्तावेज़ प्रबंधन को सुव्यवस्थित करते हैं।

विभिन्न कॉन्फ़िगरेशन के साथ प्रयोग करें और अपनी विशिष्ट आवश्यकताओं को पूरा करने के लिए Aspose.PDF द्वारा प्रदान की गई अतिरिक्त सुविधाओं का पता लगाएं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}