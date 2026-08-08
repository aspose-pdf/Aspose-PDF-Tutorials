---
date: '2026-07-03'
description: जानिए कैसे जोड़ें Aspose PDF Maven dependency और Aspose.PDF for Java
  का उपयोग करके चयन योग्य टेक्स्ट के साथ PDF को XPS में बदलें। पूर्वापेक्षाएँ और अक्सर
  पूछे जाने वाले प्रश्नों (FAQs) के साथ चरण-दर-चरण मार्गदर्शिका।
keywords:
- aspose pdf maven dependency
- how to convert pdf to xps
- java convert pdf xps
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  headline: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  type: TechArticle
- description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  name: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  steps:
  - name: Load the PDF Document
    text: 'First, load your PDF document from its directory:'
  - name: Configure Save Options
    text: 'Create an instance of `XpsSaveOptions` to set up the XPS conversion options:'
  - name: Save as XPS File
    text: 'Finally, save the document in XPS format to your desired output directory:'
  type: HowTo
- questions:
  - answer: Yes—pass the password to the `Document` constructor or use `Document.open(String
      path, String password)` before conversion.
    question: Can I convert password‑protected PDFs?
  - answer: Absolutely. All vector shapes, images, and text are preserved, and the
      text remains selectable.
    question: Does the XPS retain vector graphics?
  - answer: The trial works without a license but adds a watermark to the output;
      a permanent license removes all restrictions.
    question: Is a license mandatory for the trial version?
  - answer: It processes files in a streaming manner, allowing conversion of PDFs
      with hundreds of pages without loading the entire document into memory.
    question: How does Aspose.PDF handle large files?
  - answer: The library runs on any OS with a compatible JDK, including Windows, Linux,
      and macOS.
    question: Which platforms are supported?
  type: FAQPage
title: Aspose PDF Maven Dependency – PDF को XPS में बदलें (Java)
url: /hi/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven निर्भरता – PDF को XPS में परिवर्तित करें (Java)

## परिचय

यदि आपको **add the Aspose PDF Maven dependency** जोड़ने की आवश्यकता है और फिर PDF दस्तावेज़ों को XPS में परिवर्तित करना है जबकि टेक्स्ट चयन योग्य बना रहे, तो आप सही जगह पर हैं। यह ट्यूटोरियल आपको हर कदम से गुज़राता है—Maven या Gradle को कॉन्फ़िगर करने से लेकर, PDF लोड करने, XPS विकल्प सेट करने, और अंत में चयन योग्य‑टेक्स्ट XPS फ़ाइल सहेजने तक। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी Java प्रोजेक्ट में डाल सकते हैं।

## त्वरित उत्तर
- **मुझे कौन सी निर्भरता चाहिए?** `com.aspose:aspose-pdf` (Maven) or the equivalent Gradle artifact.  
- **क्या XPS चयन योग्य टेक्स्ट रख सकता है?** Yes—Aspose.PDF preserves text layers automatically.  
- **कौन सा Java संस्करण आवश्यक है?** JDK 8 or newer.  
- **क्या मुझे उत्पादन के लिए लाइसेंस चाहिए?** A valid Aspose.PDF license is required for unlimited use.  
- **परिवर्तन में कितना समय लगता है?** Typically under a second for files under 100 pages on standard hardware.

## Aspose PDF Maven निर्भरता क्या है?
`aspose-pdf` Maven आर्टिफैक्ट पूर्ण Aspose.PDF for Java API प्रदान करता है, जिससे आप बाहरी सॉफ़्टवेयर के बिना PDF निर्माण, हेरफेर और रूपांतरण कर सकते हैं। इस निर्भरता को अपने `pom.xml` या `build.gradle` में जोड़ने से सभी आवश्यक बाइनरी शामिल हो जाते हैं, ताकि आप मैन्युअल JAR प्रबंधन के बिना तुरंत कोडिंग शुरू कर सकें।

## PDF को XPS में चयन योग्य टेक्स्ट के साथ क्यों परिवर्तित करें?
Aspose.PDF **50+ इनपुट और आउटपुट फ़ॉर्मेट** का समर्थन करता है और XPS फ़ाइलें बना सकता है जो खोज योग्य, चयन योग्य टेक्स्ट लेयर को बनाए रखती हैं। यह उन कार्यप्रवाहों के लिए महत्वपूर्ण है जिन्हें अभिलेखीय‑ग्रेड दस्तावेज़, सटीक लेआउट फ़िडेलिटी, या XPS‑सजग टूल्स में डाउनस्ट्रीम संपादन की आवश्यकता होती है। रूपांतरण आमतौर पर आधुनिक CPU पर 20‑पृष्ठ PDF के लिए एक सेकंड से कम समय में पूरा हो जाता है।

## पूर्वापेक्षाएँ
- **Java Development Kit (JDK) 8+** स्थापित है और `JAVA_HOME` कॉन्फ़िगर किया गया है।  
- **Maven 3.6+** या **Gradle 6+** निर्भरता प्रबंधन के लिए।  
- Java फ़ाइल I/O और अपवाद हैंडलिंग की बुनियादी परिचितता।

### आवश्यक लाइब्रेरी और निर्भरताएँ
आपको Aspose.PDF for Java लाइब्रेरी संस्करण 25.3 या बाद का चाहिए। इसे निम्नलिखित बिल्ड टूल्स में से किसी एक का उपयोग करके शामिल करें:

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle:**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```  

### पर्यावरण सेटअप
सुनिश्चित करें कि आपका IDE या बिल्ड पर्यावरण सही JDK की ओर इशारा कर रहा है और नेटवर्क Maven Central या आपके निजी रिपॉज़िटरी तक पहुँच सकता है।

## Aspose PDF Maven निर्भरता कैसे जोड़ें?
`aspose-pdf` वह आर्टिफैक्ट है जिसे आप अपने प्रोजेक्ट की बिल्ड फ़ाइल में जोड़ते हैं, फिर निर्भरताओं को रीफ़्रेश करते हैं ताकि JAR स्वचालित रूप से डाउनलोड हो जाएँ। Maven के लिए, `<dependencies>` के अंदर `<dependency>` ब्लॉक डालें; Gradle के लिए, `dependencies` ब्लॉक के अंदर `implementation` लाइन रखें। रीफ़्रेश के बाद, Aspose क्लासेस क्लासपाथ पर उपलब्ध हो जाती हैं, और आप मैन्युअल JAR हैंडलिंग के बिना कोडिंग शुरू कर सकते हैं।

## Aspose.PDF for Java सेटअप
### इंस्टॉलेशन चरण
1. **Maven/Gradle सेटअप:** ऊपर दिखाए अनुसार निर्भरता जोड़ें और लाइब्रेरी को पुल करने के लिए `mvn clean install` या `gradle build` चलाएँ।  
2. **लाइसेंस प्राप्ति:**  
   - एक [free trial](https://releases.aspose.com/pdf/java/) डाउनलोड करें या एक [temporary license](https://purchase.aspose.com/temporary-license/) प्राप्त करें।  
   - लाइसेंस फ़ाइल (`Aspose.Pdf.lic`) को अपने एप्लिकेशन द्वारा पहुँच योग्य फ़ोल्डर में रखें और स्टार्टअप पर लोड करें।

### बुनियादी इनिशियलाइज़ेशन
`License` एक Aspose लाइसेंस फ़ाइल लागू करता है जिससे पूरी कार्यक्षमता अनलॉक हो जाती है।  
लाइसेंस लोड करें (यदि आपके पास है) और PDF के साथ काम करने के लिए एक `Document` ऑब्जेक्ट बनाएँ।  
`Document` एक PDF फ़ाइल का प्रतिनिधित्व करता है और इसकी सामग्री को हेरफेर करने के लिए मेथड्स प्रदान करता है।

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## चयन योग्य टेक्स्ट के साथ PDF को XPS में कैसे परिवर्तित करें?
`XpsSaveOptions` PDF को XPS दस्तावेज़ के रूप में सहेजने की सेटिंग्स को कॉन्फ़िगर करता है, जिसमें टेक्स्ट संरक्षण शामिल है।  
स्रोत PDF लोड करें, टेक्स्ट को संरक्षित करने के लिए `XpsSaveOptions` को कॉन्फ़िगर करें, और `.xps` एक्सटेंशन के साथ `save` को कॉल करें। API स्वचालित रूप से एक टेक्स्ट लेयर एम्बेड करता है, इसलिए परिणामी XPS मूल PDF की तरह खोजा और कॉपी किया जा सकता है। यह पूरी प्रक्रिया आमतौर पर लाइब्रेरी सेटअप के बाद केवल तीन लाइनों के कोड की आवश्यकता होती है।

## कार्यान्वयन गाइड
### PDF को XPS में परिवर्तित करें
यह सुविधा आपको Aspose.PDF for Java का उपयोग करके PDF दस्तावेज़ को XPS फ़ाइल में परिवर्तित करने की अनुमति देती है।

#### चरण 1: PDF दस्तावेज़ लोड करें
पहले, अपने PDF दस्तावेज़ को उसकी डायरेक्टरी से लोड करें:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### चरण 2: सहेजने के विकल्प कॉन्फ़िगर करें
`XpsSaveOptions` का एक इंस्टेंस बनाकर XPS रूपांतरण विकल्प सेट करें:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### चरण 3: XPS फ़ाइल के रूप में सहेजें
अंत में, दस्तावेज़ को XPS फ़ॉर्मेट में अपने इच्छित आउटपुट डायरेक्टरी में सहेजें:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## सामान्य समस्याएँ और समाधान
- **XPS आउटपुट में खाली पृष्ठ:** सुनिश्चित करें कि PDF एन्क्रिप्टेड स्ट्रीम्स का उपयोग नहीं करता; यदि करता है, तो `Document` लोड करते समय पासवर्ड प्रदान करें।  
- **बड़े PDFs पर मेमोरी त्रुटियाँ:** सहेजने से पहले मेमोरी फुटप्रिंट कम करने के लिए `Document.optimizeResources()` का उपयोग करें।  
- **फ़ॉन्ट गायब हैं:** सर्वर पर आवश्यक फ़ॉन्ट स्थापित करें या रूपांतरण से पहले PDF में एम्बेड करें।

## अक्सर पूछे जाने वाले प्रश्न
**Q: क्या मैं पासवर्ड‑सुरक्षित PDFs को परिवर्तित कर सकता हूँ?**  
A: हाँ—परिवर्तन से पहले `Document` कंस्ट्रक्टर में पासवर्ड पास करें या `Document.open(String path, String password)` का उपयोग करें।

**Q: क्या XPS वेक्टर ग्राफ़िक्स को बनाए रखता है?**  
A: बिल्कुल। सभी वेक्टर आकार, छवियाँ, और टेक्स्ट संरक्षित रहते हैं, और टेक्स्ट चयन योग्य बना रहता है।

**Q: क्या ट्रायल संस्करण के लिए लाइसेंस अनिवार्य है?**  
A: ट्रायल लाइसेंस के बिना काम करता है लेकिन आउटपुट में वॉटरमार्क जोड़ता है; एक स्थायी लाइसेंस सभी प्रतिबंधों को हटा देता है।

**Q: Aspose.PDF बड़े फ़ाइलों को कैसे संभालता है?**  
A: यह फ़ाइलों को स्ट्रीमिंग तरीके से प्रोसेस करता है, जिससे सैकड़ों पृष्ठों वाले PDFs को पूरी दस्तावेज़ को मेमोरी में लोड किए बिना रूपांतरित किया जा सकता है।

**Q: कौन से प्लेटफ़ॉर्म समर्थित हैं?**  
A: लाइब्रेरी किसी भी OS पर चलती है जिसमें संगत JDK हो, जैसे Windows, Linux, और macOS।

---

**अंतिम अपडेट:** 2026-07-03  
**परीक्षण किया गया:** Aspose.PDF for Java 25.3  
**लेखक:** Aspose  

{{< blocks/products/products-backtop-button >}}

## संबंधित ट्यूटोरियल्स
- [Aspose.PDF for Java का उपयोग करके PDF को JPEG में परिवर्तित करें: चरण‑दर‑चरण गाइड](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [Aspose.PDF for Java का उपयोग करके PDF को Excel में कैसे परिवर्तित करें | चरण‑दर‑चरण गाइड](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [Java में Aspose.PDF का उपयोग करके XPS फ़ाइलों को PDF में कैसे परिवर्तित करें: पूर्ण गाइड](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}