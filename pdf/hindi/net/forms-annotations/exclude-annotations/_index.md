---
title: Aspose.Pdf for .NET के साथ एनोटेशनों को बाहर रखते हुए साइड‑बाय‑साइड PDF तुलना
weight: 101
limit:
description: Aspose.Pdf for .NET का उपयोग करके PDFs की तुलना करने और एनोटेशन क्षेत्रों को बाहर रखने के लिए चरण‑दर‑चरण मार्गदर्शिका।
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET का उपयोग करके PDFs की तुलना करने और एनोटेशन क्षेत्रों
    को बाहर रखने के लिए चरण‑दर‑चरण मार्गदर्शिका।
  headline: Aspose.Pdf for .NET के साथ एनोटेशनों को बाहर रखते हुए साइड‑बाय‑साइड PDF
    तुलना
  type: TechArticle
- description: Aspose.Pdf for .NET का उपयोग करके PDFs की तुलना करने और एनोटेशन क्षेत्रों
    को बाहर रखने के लिए चरण‑दर‑चरण मार्गदर्शिका।
  name: Aspose.Pdf for .NET के साथ एनोटेशनों को बाहर रखते हुए साइड‑बाय‑साइड PDF तुलना
  steps:
  - name: प्राथमिक PDF, द्वितीयक PDF, और आउटपुट डिफ़ PDF के फ़ाइल पाथ को परिभाषित
      करें।
    text: प्राथमिक PDF, द्वितीयक PDF, और आउटपुट डिफ़ PDF के फ़ाइल पाथ को परिभाषित
      करें।
  - name: जाँचें कि दोनों इनपुट PDF फ़ाइलें मौजूद हैं और यदि कोई भी गायब हो तो त्रुटि
      संदेश के साथ प्रक्रिया को रोक दें।
    text: जाँचें कि दोनों इनपुट PDF फ़ाइलें मौजूद हैं और यदि कोई भी गायब हो तो त्रुटि
      संदेश के साथ प्रक्रिया को रोक दें।
  - name: दोनों PDF फ़ाइलों को Document ऑब्जेक्ट्स (pdfA और pdfB) के रूप में एक using
      ब्लॉक के भीतर खोलें ताकि वे स्वचालित रूप से डिस्पोज़ हो जाएँ।
    text: दोनों PDF फ़ाइलों को Document ऑब्जेक्ट्स (pdfA और pdfB) के रूप में एक using
      ब्लॉक के भीतर खोलें ताकि वे स्वचालित रूप से डिस्पोज़ हो जाएँ।
  - name: pdfA में प्रत्येक एनोटेशन के बाउंडिंग रेक्टेंगल एकत्र करें और उन्हें ignoredRectsA
      में संग्रहित करें।
    text: pdfA में प्रत्येक एनोटेशन के बाउंडिंग रेक्टेंगल एकत्र करें और उन्हें ignoredRectsA
      में संग्रहित करें।
  - name: pdfB में प्रत्येक एनोटेशन के बाउंडिंग रेक्टेंगल एकत्र करें और उन्हें ignoredRectsB
      में संग्रहित करें।
    text: pdfB में प्रत्येक एनोटेशन के बाउंडिंग रेक्टेंगल एकत्र करें और उन्हें ignoredRectsB
      में संग्रहित करें।
  - name: एक SideBySideComparisonOptions ऑब्जेक्ट बनाएं और पहले एकत्र किए गए एनोटेशन
      रेक्टेंगल को ExcludeAreas1 और ExcludeAreas2 को असाइन करें ताकि तुलना के दौरान
      उन क्षेत्रों को अनदेखा किया जाए।
    text: एक SideBySideComparisonOptions ऑब्जेक्ट बनाएं और पहले एकत्र किए गए एनोटेशन
      रेक्टेंगल को ExcludeAreas1 और ExcludeAreas2 को असाइन करें ताकि तुलना के दौरान
      उन क्षेत्रों को अनदेखा किया जाए।
  - name: दो Document ऑब्जेक्ट्स और कॉन्फ़िगर किए गए विकल्पों का उपयोग करके साइड‑बाय‑साइड
      PDF तुलना चलाएँ, और परिणाम को outputPdf में लिखें।
    text: दो Document ऑब्जेक्ट्स और कॉन्फ़िगर किए गए विकल्पों का उपयोग करके साइड‑बाय‑साइड
      PDF तुलना चलाएँ, और परिणाम को outputPdf में लिखें।
  - name: Document ऑब्जेक्ट्स को डिस्पोज़ करें और using ब्लॉक से बाहर निकलें।
    text: Document ऑब्जेक्ट्स को डिस्पोज़ करें और using ब्लॉक से बाहर निकलें।
  - name: एक पुष्टि संदेश प्रिंट करें जो दर्शाता है कि तुलना पूरी हो गई है और डिफ़
      PDF कहाँ सहेजा गया था।
    text: एक पुष्टि संदेश प्रिंट करें जो दर्शाता है कि तुलना पूरी हो गई है और डिफ़
      PDF कहाँ सहेजा गया था।
  type: HowTo
- questions:
  - answer: हां। कोड बस संबंधित `ignoredRects` सूची में कोई रेक्टेंगल नहीं जोड़ता,
      इसलिए `ExcludeAreas1`/`ExcludeAreas2` को एक खाली एरे मिलता है और तुलना करने
      वाला पूरी पेज को प्रोसेस करता है।
    question: यदि किसी PDF पेज में कोई एनोटेशन नहीं है तो क्या होता है – क्या तुलना
      अभी भी काम करेगी?
  - answer: '`ExcludeAreas1` (या `ExcludeAreas2`) को एकत्र किए गए रेक्टेंगल सेट करें
      और दूसरी प्रॉपर्टी को खाली एरे रखें; तुलना करने वाला केवल निर्दिष्ट दस्तावेज़
      में क्षेत्रों को अनदेखा करेगा।'
    question: क्या मैं एक दस्तावेज़ से केवल एनोटेशन को बाहर रख सकता हूँ जबकि डिफ़
      में दूसरे के एनोटेशन को रख सकूँ?
  - answer: ओवरलैपिंग रेक्टेंगल को तुलना करने वाला आंतरिक रूप से मर्ज कर देता है,
      इसलिए ओवरलैपिंग एनोटेशन सीमाओं को दोबारा गिनती किए बिना सुरक्षित रूप से बाहर
      रखा जाता है।
    question: क्या ओवरलैपिंग एनोटेशन रेक्टेंगल `ExcludeAreas` के साथ कोई समस्या पैदा
      करते हैं?
  - answer: हां, `compareOpts.ExcludeTables = true;` सेट करें – यह फ़्लैग `ExcludeAreas1`/`ExcludeAreas2`
      के साथ मिलकर तालिका क्षेत्रों को भी अनदेखा करता है।
    question: क्या समान विकल्प ऑब्जेक्ट का उपयोग करके एनोटेशनों के साथ तालिकाओं को
      भी बाहर रखने का कोई तरीका है?
  - answer: कोड सूची में जोड़ने से पहले `if (a != null && a.Rect != null)` जांचता
      है, इसलिए null रेक्टेंगल को बस छोड़ दिया जाता है और कोई अपवाद नहीं फेंका जाता।
    question: यदि किसी एनोटेशन की `Rect` प्रॉपर्टी null है – क्या कोड अपवाद फेंकेगा?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: एनोटेशनों के बिना PDFs की तुलना करें
og_description: एक साइड‑बाय‑साइड PDF डिफ़ चलाएँ जो सभी एनोटेशन मार्क्स को छोड़ देता है।
og_image_alt: Aspose.Pdf for .NET का उपयोग करके एनोटेशन क्षेत्रों को बाहर रखने वाली साइड‑बाय‑साइड PDF तुलना दर्शाने वाला मार्गदर्शिका
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET के साथ एनोटेशनों को बाहर रखते हुए साइड‑बाय‑साइड PDF तुलना
यह ट्यूटोरियल दिखाता है कि Aspose.Pdf for .NET का उपयोग करके दो PDF फ़ाइलों की तुलना कैसे करें, जबकि किसी भी एनोटेशन सामग्री को अनदेखा किया जाए। यह प्रत्येक दस्तावेज़ से सभी एनोटेशन के बाउंडिंग बॉक्स निकालता है, उन क्षेत्रों को SideBySideComparisonOptions में पास करता है, और फिर साइड‑बाय‑साइड तुलना चलाता है। परिणाम एक डिफ़ PDF है जो केवल गैर‑एनोटेशन परिवर्तन को हाइलाइट करता है।

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: यदि किसी PDF पेज में कोई एनोटेशन नहीं है तो क्या होता है – क्या तुलना अभी भी काम करेगी?**  
A: हां। कोड बस संबंधित `ignoredRects` सूची में कोई रेक्टेंगल नहीं जोड़ता, इसलिए `ExcludeAreas1`/`ExcludeAreas2` को एक खाली एरे मिलता है और तुलना करने वाला पूरी पेज को प्रोसेस करता है।

**Q: क्या मैं एक दस्तावेज़ से केवल एनोटेशन को बाहर रख सकता हूँ जबकि डिफ़ में दूसरे के एनोटेशन को रख सकूँ?**  
A: `ExcludeAreas1` (या `ExcludeAreas2`) को एकत्र किए गए रेक्टेंगल सेट करें और दूसरी प्रॉपर्टी को खाली एरे रखें; तुलना करने वाला केवल निर्दिष्ट दस्तावेज़ में क्षेत्रों को अनदेखा करेगा।

**Q: क्या ओवरलैपिंग एनोटेशन रेक्टेंगल `ExcludeAreas` के साथ कोई समस्या पैदा करते हैं?**  
A: ओवरलैपिंग रेक्टेंगल को तुलना करने वाला आंतरिक रूप से मर्ज कर देता है, इसलिए ओवरलैपिंग एनोटेशन सीमाओं को दोबारा गिनती किए बिना सुरक्षित रूप से बाहर रखा जाता है।

**Q: क्या समान विकल्प ऑब्जेक्ट का उपयोग करके एनोटेशनों के साथ तालिकाओं को भी बाहर रखने का कोई तरीका है?**  
A: हां, `compareOpts.ExcludeTables = true;` सेट करें – यह फ़्लैग `ExcludeAreas1`/`ExcludeAreas2` के साथ मिलकर तालिका क्षेत्रों को भी अनदेखा करता है।

**Q: यदि किसी एनोटेशन की `Rect` प्रॉपर्टी null है – क्या कोड अपवाद फेंकेगा?**  
A: कोड सूची में जोड़ने से पहले `if (a != null && a.Rect != null)` जांचता है, इसलिए null रेक्टेंगल को बस छोड़ दिया जाता है और कोई अपवाद नहीं फेंका जाता।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}