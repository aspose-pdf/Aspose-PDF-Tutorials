---
"description": "जानें कि .NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइल से बॉर्डर कैसे निकालें और उन्हें इमेज के रूप में कैसे सेव करें। कोड सैंपल और सफलता के लिए टिप्स के साथ चरण-दर-चरण गाइड।"
"linktitle": "पीडीएफ फाइल में बॉर्डर निकालें"
"second_title": ".NET API संदर्भ के लिए Aspose.PDF"
"title": "पीडीएफ फाइल में बॉर्डर निकालें"
"url": "/hi/net/programming-with-tables/extract-border/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# पीडीएफ फाइल में बॉर्डर निकालें

## परिचय

PDF के साथ काम करते समय, बॉर्डर या ग्राफ़िकल पथ जैसे विशिष्ट तत्वों को निकालना एक कठिन काम लग सकता है। लेकिन .NET के लिए Aspose.PDF के साथ, आप आसानी से PDF फ़ाइल से बॉर्डर या आकृतियाँ निकाल सकते हैं और उन्हें एक छवि के रूप में सहेज सकते हैं। इस ट्यूटोरियल में, हम PDF से बॉर्डर निकालने और उसे PNG छवि के रूप में सहेजने की प्रक्रिया में गोता लगाएँगे। अपने PDF की ग्राफ़िकल सामग्री पर नियंत्रण रखने के लिए तैयार हो जाइए!

## आवश्यक शर्तें

इससे पहले कि हम कोड में उतरें, सुनिश्चित करें कि आपने सब कुछ सेट कर लिया है:

1. .NET के लिए Aspose.PDF: यदि आपने अभी तक Aspose.PDF लाइब्रेरी स्थापित नहीं की है, तो आप कर सकते हैं [यहाँ पर डाउनलोड करो](https://releases.aspose.com/pdf/net/)आपको लाइसेंस भी लागू करना होगा, या तो निःशुल्क परीक्षण के माध्यम से या खरीदे गए लाइसेंस के माध्यम से।
2. IDE सेटअप: Visual Studio या किसी अन्य .NET IDE में C# प्रोजेक्ट सेट अप करें। सुनिश्चित करें कि आपने Aspose.PDF लाइब्रेरी में आवश्यक संदर्भ जोड़ दिए हैं।
3. इनपुट पीडीएफ फाइल: एक पीडीएफ फाइल तैयार रखें जिससे आप बॉर्डर निकालेंगे। यह ट्यूटोरियल नाम की एक फाइल का संदर्भ देगा `input.pdf`.

## आवश्यक पैकेज आयात करना

आइए आवश्यक नेमस्पेस को आयात करके शुरू करें। ये पैकेज पीडीएफ सामग्री में हेरफेर करने के लिए आवश्यक उपकरण प्रदान करते हैं।

```csharp
using System.IO;
using System;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;
using System.Collections;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
```

अब जबकि हमने मूल बातें समझ ली हैं, तो चलिए चरण-दर-चरण मार्गदर्शिका की ओर बढ़ते हैं, जहां हम कोड के प्रत्येक भाग को विस्तृत रूप से समझाएंगे।


## चरण 1: पीडीएफ दस्तावेज़ लोड करना

पहला कदम पीडीएफ दस्तावेज़ को लोड करना है जिसमें वह बॉर्डर है जिसे आप निकालना चाहते हैं। इसे पढ़ने से पहले किताब खोलने जैसा समझें - आपको सामग्री तक पहुँच की आवश्यकता है!

हम उस निर्देशिका को निर्दिष्ट करके शुरू करेंगे जहां आपकी पीडीएफ फाइल संग्रहीत है और दस्तावेज़ को लोड करें `Aspose.Pdf.Document` कक्षा।

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

यह कोड लोड करता है `input.pdf` अपनी निर्दिष्ट निर्देशिका से फ़ाइल प्राप्त करें। सुनिश्चित करें कि फ़ाइल पथ सही है, अन्यथा आपको फ़ाइल नहीं मिली त्रुटि मिल सकती है।

## चरण 2: ग्राफ़िक्स और बिटमैप सेट अप करना

एक्सट्रेक्ट करना शुरू करने से पहले, हमें ड्रॉ करने के लिए एक कैनवास बनाना होगा। .NET की दुनिया में, इसका मतलब है बिटमैप और ग्राफ़िक्स ऑब्जेक्ट सेट करना। बिटमैप इमेज को दर्शाता है, और ग्राफ़िक्स ऑब्जेक्ट हमें पीडीएफ से निकाले गए बॉर्डर जैसे आकार बनाने की अनुमति देगा।

```csharp
System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap((int)doc.Pages[1].PageInfo.Width, (int)doc.Pages[1].PageInfo.Height);
System.Drawing.Drawing2D.GraphicsPath graphicsPath = new System.Drawing.Drawing2D.GraphicsPath();
System.Drawing.Drawing2D.Matrix lastCTM = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, 0);
System.Drawing.Drawing2D.Matrix inversionMatrix = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, (float)doc.Pages[1].PageInfo.Height);
System.Drawing.PointF lastPoint = new System.Drawing.PointF(0, 0);
System.Drawing.Color fillColor = System.Drawing.Color.FromArgb(0, 0, 0);
System.Drawing.Color strokeColor = System.Drawing.Color.FromArgb(0, 0, 0);
```

यहाँ इसका विवरण दिया गया है:
- हम पीडीएफ के प्रथम पृष्ठ के आकार का एक बिटमैप चित्र बनाते हैं।
- GraphicsPath का उपयोग आकृतियों (इस मामले में, बॉर्डर) को परिभाषित करने के लिए किया जाता है।
- मैट्रिक्स यह परिभाषित करता है कि ग्राफिक्स को कैसे रूपांतरित किया जाएगा; हमें व्युत्क्रम मैट्रिक्स की आवश्यकता है क्योंकि PDF और .NET में अलग-अलग निर्देशांक प्रणालियां हैं।

## चरण 3: पीडीएफ सामग्री का प्रसंस्करण


पीडीएफ फाइल ड्राइंग कमांडों की एक श्रृंखला है, और हमें सीमा संबंधी जानकारी की पहचान करने और उसे निकालने के लिए इनमें से प्रत्येक कमांड को संसाधित करने की आवश्यकता है।

```csharp
foreach (Operator op in doc.Pages[1].Contents)
{
    // प्रसंस्करण आदेश जैसे कि स्थिति को सहेजना/पुनर्स्थापित करना, रेखाएँ खींचना, आकृतियाँ भरना आदि।
}
```

कोड पीडीएफ की सामग्री स्ट्रीम में प्रत्येक ड्राइंग ऑपरेटर के माध्यम से लूप करता है। प्रत्येक ऑपरेटर एक रेखा, आयत या अन्य ग्राफ़िकल निर्देश का प्रतिनिधित्व कर सकता है।

## चरण 4: पीडीएफ ऑपरेटरों को संभालना

पीडीएफ फाइल में प्रत्येक ऑपरेटर एक क्रिया को नियंत्रित करता है। बॉर्डर निकालने के लिए, हमें "मूव टू", "लाइन टू", और "ड्रा रेक्टेंगल" जैसे कमांड की पहचान करने की आवश्यकता है। निम्नलिखित ऑपरेटर इन क्रियाओं को संभालते हैं:

- MoveTo: कर्सर को प्रारंभिक बिंदु पर ले जाता है।
- LineTo: वर्तमान बिंदु से नए बिंदु तक एक रेखा खींचता है।
- Re: एक आयत बनाएं (यह सीमा का हिस्सा हो सकता है)।

```csharp
Aspose.Pdf.Operators.MoveTo opMoveTo = op as Aspose.Pdf.Operators.MoveTo;
Aspose.Pdf.Operators.LineTo opLineTo = op as Aspose.Pdf.Operators.LineTo;
Aspose.Pdf.Operators.Re opRe = op as Aspose.Pdf.Operators.Re;

if (opMoveTo != null)
{
    lastPoint = new System.Drawing.PointF((float)opMoveTo.X, (float)opMoveTo.Y);
}
else if (opLineTo != null)
{
    System.Drawing.PointF linePoint = new System.Drawing.PointF((float)opLineTo.X, (float)opLineTo.Y);
    graphicsPath.AddLine(lastPoint, linePoint);
    lastPoint = linePoint;
}
else if (opRe != null)
{
    System.Drawing.RectangleF re = new System.Drawing.RectangleF((float)opRe.X, (float)opRe.Y, (float)opRe.Width, (float)opRe.Height);
    graphicsPath.AddRectangle(re);
}
```

इस चरण में:
- हम खींची गई प्रत्येक रेखा या आकृति के लिए बिंदु अंकित करते हैं।
- आयतों के लिए (`opRe`), हम उन्हें सीधे जोड़ते हैं `graphicsPath`, जिसका उपयोग हम बाद में सीमा रेखा खींचने के लिए करेंगे।

## चरण 5: बॉर्डर बनाना

एक बार जब हम उन रेखाओं और आयतों की पहचान कर लेते हैं जो बॉर्डर बनाती हैं, तो हमें उन्हें वास्तव में बिटमैप ऑब्जेक्ट पर खींचना होगा। यहीं पर ग्राफ़िक्स ऑब्जेक्ट काम आता है।

```csharp
using (System.Drawing.Graphics gr = System.Drawing.Graphics.FromImage(bitmap))
{
    gr.SmoothingMode = SmoothingMode.HighQuality;
    gr.DrawPath(new System.Drawing.Pen(strokeColor), graphicsPath);
}
```

- हम बिटमैप के आधार पर एक ग्राफ़िक्स ऑब्जेक्ट बनाते हैं।
- SmoothingMode.HighQuality सुनिश्चित करता है कि हमें एक अच्छी चिकनी छवि मिले।
- अंत में, हम बॉर्डर खींचने के लिए DrawPath का उपयोग करते हैं।

## चरण 6: निकाले गए बॉर्डर को सहेजना

अब जब हमने बॉर्डर निकाल लिया है, तो इसे इमेज फ़ाइल के रूप में सेव करने का समय आ गया है। इससे बॉर्डर PNG के रूप में सेव हो जाएगा।

```csharp
dataDir = dataDir + "ExtractBorder_out.png";
bitmap.Save(dataDir, ImageFormat.Png);
```

- बिटमैप को PNG छवि के रूप में सहेजा जाता है।
- अब आप निकाले गए बॉर्डर को देखने के लिए इस छवि को खोल सकते हैं।

## निष्कर्ष

.NET के लिए Aspose.PDF का उपयोग करके PDF फ़ाइल से बॉर्डर निकालना पहली बार में मुश्किल लग सकता है, लेकिन एक बार जब आप इसे समझ लेते हैं, तो यह आसान हो जाता है। PDF में ड्रॉइंग ऑपरेटर को समझकर और शक्तिशाली .NET लाइब्रेरी का उपयोग करके, आप ग्राफिकल कंटेंट को कुशलतापूर्वक मैनिपुलेट और एक्सट्रैक्ट कर सकते हैं। यह गाइड आपको PDF मैनिपुलेशन के साथ आरंभ करने के लिए एक मजबूत आधार प्रदान करता है!

## अक्सर पूछे जाने वाले प्रश्न

### मैं पीडीएफ में एकाधिक पृष्ठों को कैसे संभालूँ?  
आप दस्तावेज़ में प्रत्येक पृष्ठ पर पुनरावृत्ति करके लूप कर सकते हैं `doc.Pages` हार्डकोडिंग के बजाय `doc.Pages[1]`.

### क्या मैं उसी दृष्टिकोण का उपयोग करके पाठ जैसे अन्य तत्वों को निकाल सकता हूं?  
हां, Aspose.PDF पीडीएफ फाइलों से पाठ, चित्र और अन्य सामग्री निकालने के लिए समृद्ध API प्रदान करता है।

### सीमाओं से बचने के लिए मैं लाइसेंस कैसे लागू करूँ?  
तुम कर सकते हो [लाइसेंस लागू करें](https://purchase.aspose.com/temporary-license/) इसे के माध्यम से लोड करके `License` Aspose द्वारा प्रदान की गई क्लास.

### यदि मेरी PDF में कोई बॉर्डर नहीं है तो क्या होगा?  
यदि आपके PDF में कोई दृश्यमान बॉर्डर नहीं है, तो ग्राफ़िक्स निष्कर्षण प्रक्रिया कोई परिणाम नहीं दे सकती है। सुनिश्चित करें कि PDF सामग्री में ड्राएबल बॉर्डर शामिल हैं।

### क्या मैं आउटपुट को PNG के अलावा अन्य प्रारूपों में सहेज सकता हूँ?  
हाँ, बस बदलो `ImageFormat.Png` किसी अन्य समर्थित प्रारूप जैसे `ImageFormat.Jpeg`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}