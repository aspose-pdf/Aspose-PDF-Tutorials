---
title: Aspose.Pdf for .NET का उपयोग करके पृष्ठ दस के बाद PDF विभाजित करें
weight: 360
limit:
description: Aspose.Pdf for .NET के साथ PDF दस्तावेज़ को दसवें पृष्ठ के तुरंत बाद विभाजित करने के लिए चरण‑दर‑चरण कोड।
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET के साथ PDF दस्तावेज़ को दसवें पृष्ठ के तुरंत बाद
    विभाजित करने के लिए चरण‑दर‑चरण कोड।
  headline: Aspose.Pdf for .NET का उपयोग करके पृष्ठ दस के बाद PDF विभाजित करें
  type: TechArticle
- description: Aspose.Pdf for .NET के साथ PDF दस्तावेज़ को दसवें पृष्ठ के तुरंत बाद
    विभाजित करने के लिए चरण‑दर‑चरण कोड।
  name: Aspose.Pdf for .NET का उपयोग करके पृष्ठ दस के बाद PDF विभाजित करें
  steps:
  - name: हेडर टिप्पणी उदाहरण का उद्देश्य समझाती हैं, यह बताती हैं कि पूरा कोड स्थानांतरित
      कर दिया गया है, और अद्यतन स्रोत का लिंक प्रदान करती हैं।
    text: हेडर टिप्पणी उदाहरण का उद्देश्य समझाती हैं, यह बताती हैं कि पूरा कोड स्थानांतरित
      कर दिया गया है, और अद्यतन स्रोत का लिंक प्रदान करती हैं।
  - name: स्टब लाइन कोई कार्रवाई नहीं करती और केवल मूल URL को कार्यशील रखने के लिए
      मौजूद है।
    text: स्टब लाइन कोई कार्रवाई नहीं करती और केवल मूल URL को कार्यशील रखने के लिए
      मौजूद है।
  type: HowTo
- questions:
  - answer: Aspose.Pdf कोई त्रुटि नहीं फेंकेगा; `Split` मेथड केवल मूल दस्तावेज़ को
      अपरिवर्तित वापस करेगा क्योंकि दसवें पृष्ठ के बाद नया भाग शुरू करने के लिए कोई
      पृष्ठ नहीं है।
    question: यदि स्रोत PDF में दस से कम पृष्ठ हों तो क्या होता है?
  - answer: आप `PdfDocument` इंस्टेंस पर `PdfDocument.Split(pageNumber)` को कॉल करते
      हैं, `pageNumber` के रूप में `10` पास करके दो अलग-अलग दस्तावेज़ बनाते हैं।
    question: PDF को पृष्ठ दस पर विभाजित करने के लिए कौन सी क्लास और मेथड उपयोग की
      जाती हैं?
  - answer: हाँ, Aspose.Pdf परिणामस्वरूप विभाजित दस्तावेज़ों में सभी पृष्ठ‑स्तर की
      वस्तुओं (बुकमार्क, एनोटेशन, फ़ॉर्म फ़ील्ड आदि) को संरक्षित रखता है, जिससे वे
      अपने मूल पृष्ठों से जुड़े रहते हैं।
    question: क्या बुकमार्क, एनोटेशन और फ़ॉर्म फ़ील्ड विभाजन के बाद अपनी मूल पृष्ठों
      के साथ ही रहते हैं?
  - answer: '`Split` कॉल करने के बाद, आपको दो `PdfDocument` ऑब्जेक्ट मिलते हैं; आपको
      पहले पर `Save("FirstPart.pdf")` और दूसरे पर `Save("SecondPart.pdf")` कॉल करना
      होगा, तथा स्वयं अलग-अलग फ़ाइल नाम प्रदान करने होंगे।'
    question: विभाजन द्वारा निर्मित दो भागों के आउटपुट फ़ाइलों के नाम कैसे रखें?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: पृष्ठ 10 के बाद PDF विभाजित करें
og_description: Aspose.Pdf for .NET का उपयोग करके पृष्ठ 10 पर PDF विभाजित करने के लिए त्वरित ट्यूटोरियल।
og_image_alt: Aspose.Pdf for .NET का उपयोग करके दसवें पृष्ठ के बाद PDF विभाजित करने का तरीका दिखाने वाला गाइड
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET का उपयोग करके पृष्ठ दस के बाद PDF विभाजित करें
PDF को अलग-अलग दस्तावेज़ों में विभाजित करने से वितरण और प्रोसेसिंग सरल हो सकती है। यह ट्यूटोरियल आपको Aspose.Pdf for .NET का उपयोग करके PDF को ठीक दसवें पृष्ठ के बाद विभाजित करने, दो अलग-अलग फ़ाइलें बनाने के माध्यम से ले जाता है। केवल कुछ C# लाइनों के साथ चरण‑दर‑चरण कोड का पालन करके पहले दस पृष्ठ और शेष पृष्ठ निकालें।

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/split-pdf" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: यदि स्रोत PDF में दस से कम पृष्ठ हों तो क्या होता है?**  
A: Aspose.Pdf कोई त्रुटि नहीं फेंकेगा; `Split` मेथड केवल मूल दस्तावेज़ को अपरिवर्तित वापस करेगा क्योंकि दसवें पृष्ठ के बाद नया भाग शुरू करने के लिए कोई पृष्ठ नहीं है।

**Q: PDF को पृष्ठ दस पर विभाजित करने के लिए कौन सी क्लास और मेथड उपयोग की जाती हैं?**  
A: आप `PdfDocument` इंस्टेंस पर `PdfDocument.Split(pageNumber)` को कॉल करते हैं, `pageNumber` के रूप में `10` पास करके दो अलग-अलग दस्तावेज़ बनाते हैं।

**Q: क्या बुकमार्क, एनोटेशन और फ़ॉर्म फ़ील्ड विभाजन के बाद अपनी मूल पृष्ठों के साथ ही रहते हैं?**  
A: हाँ, Aspose.Pdf परिणामस्वरूप विभाजित दस्तावेज़ों में सभी पृष्ठ‑स्तर की वस्तुओं (बुकमार्क, एनोटेशन, फ़ॉर्म फ़ील्ड आदि) को संरक्षित रखता है, जिससे वे अपने मूल पृष्ठों से जुड़े रहते हैं।

**Q: विभाजन द्वारा निर्मित दो भागों के आउटपुट फ़ाइलों के नाम कैसे रखें?**  
A: `Split` कॉल करने के बाद, आपको दो `PdfDocument` ऑब्जेक्ट मिलते हैं; आपको पहले पर `Save("FirstPart.pdf")` और दूसरे पर `Save("SecondPart.pdf")` कॉल करना होगा, तथा स्वयं अलग-अलग फ़ाइल नाम प्रदान करने होंगे।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}