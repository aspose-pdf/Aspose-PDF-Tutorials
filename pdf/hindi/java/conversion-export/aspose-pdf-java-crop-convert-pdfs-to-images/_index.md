---
date: '2026-06-07'
description: Aspose.PDF for Java का उपयोग करके PDF पृष्ठ को इमेज में बदलना और उसे
  क्रॉप करना सीखें, जिससे उच्च रिज़ॉल्यूशन PDF इमेजेज बनती हैं।
keywords:
- pdf page to image
- high resolution pdf image
- convert pdf to bmp
- java pdf to png
- aspose pdf license free
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Learn how to convert a PDF page to image and crop it using Aspose.PDF
    for Java, producing high resolution PDF images.
  headline: Convert PDF Page to Image and Crop with Aspose.PDF Java
  type: TechArticle
- description: Learn how to convert a PDF page to image and crop it using Aspose.PDF
    for Java, producing high resolution PDF images.
  name: Convert PDF Page to Image and Crop with Aspose.PDF Java
  steps:
  - name: Define the Crop Region (set crop box pdf)
    text: '- *Parameters*: left, bottom, right, top coordinates (in points).'
  - name: Save the Cropped Document
    text: '> **Pro tip:** Verify the rectangle dimensions against the page size to
      avoid “out of bounds” errors.'
  - name: Load from Byte Stream and Convert
    text: '- The `Resolution` object controls DPI; 300 dpi yields a crisp BMP suitable
      for printing or further analysis. > **Common pitfall:** Forgetting to close
      streams can lead to memory leaks. Always dispose of `ByteArrayOutputStream`
      and `ByteArrayInputStream` when finished.'
  type: HowTo
- questions:
  - answer: Iterate through `document.getPages()` and apply `setCropBox` to each page
      as needed.
    question: How do I crop multiple pages at once?
  - answer: Yes, Aspose.PDF supports `JpegDevice`, `PngDevice`, `TiffDevice`, and
      more for **pdf to image java** conversions.
    question: Can I convert PDF pages to other image formats?
  - answer: Adjust the rectangle coordinates so they stay within the page dimensions;
      otherwise an exception is thrown.
    question: What if my crop rectangle exceeds page bounds?
  - answer: Process pages in batches, reuse streams, and call `document.optimizeResources()`
      to free unused objects.
    question: How can I handle very large PDFs efficiently?
  - answer: Render the page to an image first, display it in a UI component, and confirm
      the crop box visually.
    question: Is there a way to preview the cropped area before saving?
  type: FAQPage
title: Aspose.PDF Java के साथ PDF पृष्ठ को इमेज में बदलें और क्रॉप करें
url: /hi/java/conversion-export/aspose-pdf-java-crop-convert-pdfs-to-images/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# PDF पृष्ठ को छवि में बदलें और Aspose.PDF Java के साथ क्रॉप करें

यदि आपको **PDF पृष्ठ को छवि में बदलना** है और साथ ही एक विशिष्ट क्षेत्र को क्रॉप करना है, तो आप सही जगह पर हैं। यह गाइड आपको PDF पृष्ठ से एक आयत को क्रॉप करने और फिर उस क्षेत्र को Aspose.PDF for Java का उपयोग करके उच्च‑रिज़ॉल्यूशन BMP छवि के रूप में रेंडर करने की प्रक्रिया दिखाता है। अंत तक, आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी दस्तावेज़‑प्रोसेसिंग पाइपलाइन में शामिल कर सकते हैं।

## त्वरित उत्तर
- **यह ट्यूटोरियल कौन सी लाइब्रेरी उपयोग करता है?** Aspose.PDF for Java.
- **क्या मैं कस्टम क्रॉप बॉक्स सेट कर सकता हूँ?** हाँ – पेज ऑब्जेक्ट पर `setCropBox` कॉल करें.
- **कौन सा इमेज फ़ॉर्मेट सबसे बेहतर गुणवत्ता देता है?** 300 dpi पर BMP सबसे तेज़ परिणाम देता है.
- **परीक्षण के लिए क्या लाइसेंस चाहिए?** एक अस्थायी मुफ्त लाइसेंस सभी मूल्यांकन सीमाओं को हटा देता है.
- **क्या मैं अन्य फ़ॉर्मेट आउटपुट कर सकता हूँ?** बिल्कुल – `JpegDevice`, `PngDevice`, `TiffDevice` आदि समर्थित हैं.

## Aspose.PDF के साथ **PDF को कैसे क्रॉप करें** क्या है?
Aspose.PDF के साथ PDF को क्रॉप करना मतलब एक आयताकार क्रॉप बॉक्स को परिभाषित करना है जो पृष्ठ के उस भाग को निर्दिष्ट करता है जिसे रखना है और बाकी को हटाना है। लाइब्रेरी पृष्ठ के MediaBox, CropBox और अन्य सीमाओं को समायोजित करती है ताकि केवल चयनित क्षेत्र ही रेंडर या सहेजा जाए।

## PDF को छवि में बदलने के लिए Java में Aspose.PDF का उपयोग क्यों करें?
Aspose.PDF for Java उच्च‑रिज़ॉल्यूशन रास्टराइज़ेशन प्रदान करता है, जिससे आप PDF पृष्ठों को 1200 dpi तक रेंडर कर सकते हैं, जो प्रिंटिंग और विश्लेषण के लिए स्पष्ट छवियां देता है। यह नेटिव डिपेंडेंसीज़ के बिना काम करता है, BMP, JPEG, PNG, और TIFF जैसे कई आउटपुट फ़ॉर्मेट का समर्थन करता है, और DPI, कलर डेप्थ, और कॉम्प्रेशन को नियंत्रित करने के लिए एक सरल API प्रदान करता है।

## पूर्वापेक्षाएँ
- **JDK** (संस्करण 8 या नया) स्थापित और कॉन्फ़िगर किया हुआ.
- **IDE** जैसे IntelliJ IDEA या Eclipse.
- **Aspose.PDF for Java** – संस्करण 25.3 या बाद का, Maven/Gradle के माध्यम से जोड़ा गया.
- Java और बिल्ड टूल्स की बुनियादी जानकारी.

## Aspose.PDF for Java सेटअप करना
सबसे पहले, लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें।

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

विकास के दौरान पूर्ण कार्यक्षमता अनलॉक करने के लिए एक अस्थायी मुफ्त लाइसेंस प्राप्त करें।

### बेसिक इनिशियलाइज़ेशन
```java
import com.aspose.pdf.Document;

public class SetupAsposePDF {
    public static void main(String[] args) {
        // Initialize the library with a license if you have one.
        // License license = new License();
        // license.setLicense("path_to_your_license.lic");
        
        System.out.println("Setup complete!");
    }
}
```  

पर्यावरण तैयार होने के बाद, चलिए क्रॉपिंग की ओर बढ़ते हैं।

## Aspose.PDF का उपयोग करके PDF पृष्ठों को कैसे क्रॉप करें
`Rectangle` क्लास एक आयताकार क्षेत्र को दर्शाती है जिसे बाएँ, नीचे, दाएँ और ऊपर के निर्देशांक (पॉइंट्स में) द्वारा परिभाषित किया जाता है।  
PDF पृष्ठ को क्रॉप करने के लिए, दस्तावेज़ लोड करें, एक `Rectangle` बनाएं जो इच्छित बाएँ, नीचे, दाएँ और ऊपर के किनारे पॉइंट्स में परिभाषित करे, और इसे पृष्ठ के क्रॉप बॉक्स पर `setCropBox` के साथ असाइन करें। बॉक्स सेट करने के बाद, दस्तावेज़ को सहेजने से प्रत्येक प्रोसेस्ड पृष्ठ पर केवल निर्दिष्ट क्षेत्र वाली फ़ाइल बनती है।

### सीधा उत्तर
आप एक `Rectangle` बनाकर बाएँ, नीचे, दाएँ और ऊपर के किनारे पॉइंट्स में परिभाषित करते हैं, फिर `page.setCropBox(rectangle)` कॉल करते हैं। बॉक्स सेट करने के बाद दस्तावेज़ सहेजें – अनचाहे मार्जिन तुरंत हट जाते हैं।

### चरण 1: आवश्यक लाइब्रेरी इम्पोर्ट करें
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.Rectangle;
```  

### चरण 2: PDF दस्तावेज़ लोड करें
```java
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document document = new Document(dataDir + "/Input.pdf");
```  

### चरण 3: क्रॉप क्षेत्र निर्धारित करें (crop box सेट करें pdf)
```java
Rectangle pageRect = new Rectangle(20, 671, 693, 1125);
document.getPages().get_Item(1).setCropBox(pageRect);
```  
- *पैरामीटर*: बाएँ, नीचे, दाएँ, ऊपर के निर्देशांक (पॉइंट्स में).

### चरण 4: क्रॉप किया गया दस्तावेज़ सहेजें
```java
document.save(dataDir + "/CroppedOutput.pdf");
```  

> **Pro tip:** आयत के आयामों को पृष्ठ आकार के खिलाफ जाँचें ताकि “out of bounds” त्रुटियों से बचा जा सके.

## क्रॉप किए गए PDF क्षेत्र को छवि में बदलना (pdf to bmp conversion)
`BmpDevice` क्लास PDF पृष्ठों को BMP इमेज फ़ॉर्मेट में रेंडर करती है।  
`Resolution` क्लास आउटपुट इमेज DPI को निर्दिष्ट करती है।  
क्रॉप करने के बाद, आप एक `BmpDevice` बनाकर, उसकी रिज़ॉल्यूशन सेट करके, और पृष्ठ को प्रोसेस करके चयनित क्षेत्र को छवि में रेंडर कर सकते हैं। डिवाइस रास्टराइज़्ड आउटपुट को एक स्ट्रीम में लिखता है, जिसे आप फिर BMP फ़ाइल के रूप में सहेज सकते हैं या आवश्यकतानुसार अन्य फ़ॉर्मेट में बदल सकते हैं।

### सीधा उत्तर
एक `BmpDevice` (या कोई अन्य इमेज डिवाइस) बनाएं, उसकी `Resolution` को 300 dpi पर सेट करें, और क्रॉप किए गए पृष्ठ पर `process` कॉल करें। डिवाइस छवि को एक स्ट्रीम में लिखता है, जिसे आप फिर `.bmp` फ़ाइल के रूप में सहेज सकते हैं.

### चरण 5: अतिरिक्त लाइब्रेरी इम्पोर्ट करें
```java
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import com.aspose.pdf.devices.BmpDevice;
import com.aspose.pdf.devices.Resolution;
```  

### चरण 6: क्रॉप किया गया PDF बाइट स्ट्रीम में सहेजें
```java
ByteArrayOutputStream outStream = new ByteArrayOutputStream();
document.save(outStream);
```  

### चरण 7: बाइट स्ट्रीम से लोड करें और कनवर्ट करें
```java
document = new Document(new ByteArrayInputStream(outStream.toByteArray()));
Resolution resolution = new Resolution(300); // High‑quality image
BmpDevice bmpDevice = new BmpDevice(resolution);
bmpDevice.process(document.getPages().get_Item(1), "YOUR_OUTPUT_DIRECTORY/Output.bmp");
```  
- `Resolution` ऑब्जेक्ट DPI को नियंत्रित करता है; 300 dpi एक स्पष्ट BMP देता है जो प्रिंटिंग या आगे के विश्लेषण के लिए उपयुक्त है.

> **Common pitfall:** स्ट्रीम को बंद करना न भूलें, अन्यथा मेमोरी लीक हो सकता है. उपयोग समाप्त होने पर `ByteArrayOutputStream` और `ByteArrayInputStream` को हमेशा डिस्पोज़ करें.

## व्यावहारिक उपयोग
- **दस्तावेज़ अभिलेख:** संग्रहण से पहले हेडर/फ़ूटर हटाकर जगह बचाएँ.
- **डिजिटल सिग्नेचर:** सत्यापन के लिए केवल सिग्नेचर क्षेत्र निकालें.
- **डेटा एक्सट्रैक्शन:** विश्लेषण पाइपलाइन के लिए टेबल या चार्ट अलग करें.
- **ग्राफिक डिज़ाइन:** वेक्टर PDF सेक्शन को UI मॉक‑अप्स के लिए रास्टर एसेट्स में बदलें.

## प्रदर्शन संबंधी विचार
- **रिज़ॉल्यूशन बनाम गति:** उच्च DPI प्रोसेसिंग समय और मेमोरी उपयोग बढ़ाता है.
- **बैच प्रोसेसिंग:** मेमोरी फुटप्रिंट कम रखने के लिए बड़े PDF को पृष्ठ‑दर‑पृष्ठ प्रोसेस करें.
- **रिसोर्स क्लीनअप:** उपयोग के बाद `document.dispose()` कॉल करें या JVM गार्बेज कलेक्टर को ऑब्जेक्ट्स पुनः प्राप्त करने दें.

## अक्सर पूछे जाने वाले प्रश्न

**Q: मैं एक साथ कई पृष्ठों को कैसे क्रॉप करूँ?**  
A: `document.getPages()` पर इटरेट करें और प्रत्येक पृष्ठ पर आवश्यकतानुसार `setCropBox` लागू करें.

**Q: क्या मैं PDF पृष्ठों को अन्य इमेज फ़ॉर्मेट में बदल सकता हूँ?**  
A: हाँ, Aspose.PDF `JpegDevice`, `PngDevice`, `TiffDevice` आदि को **pdf to image java** कन्वर्ज़न के लिए समर्थन देता है.

**Q: यदि मेरा क्रॉप आयत पृष्ठ की सीमाओं से बाहर है तो क्या होगा?**  
A: आयत के निर्देशांक को पृष्ठ के आयामों के भीतर रखें; अन्यथा एक एक्सेप्शन फेंका जाएगा.

**Q: बहुत बड़े PDF को कुशलतापूर्वक कैसे हैंडल करूँ?**  
A: पृष्ठों को बैच में प्रोसेस करें, स्ट्रीम को पुन: उपयोग करें, और उपयोग न किए गए ऑब्जेक्ट्स को मुक्त करने के लिए `document.optimizeResources()` कॉल करें.

**Q: क्या सहेजने से पहले क्रॉप किए गए क्षेत्र का प्रीव्यू देख सकते हैं?**  
A: पहले पृष्ठ को इमेज में रेंडर करें, UI कॉम्पोनेंट में दिखाएँ, और विज़ुअली क्रॉप बॉक्स की पुष्टि करें.

## संसाधन
- **डॉक्यूमेंटेशन:** [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **डाउनलोड:** [Aspose.PDF Releases](https://releases.aspose.com/pdf/java/)
- **खरीदें:** [Buy Aspose.PDF](https://purchase.aspose.com/buy)
- **फ्री ट्रायल:** [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **अस्थायी लाइसेंस:** [Get a Temporary License](https://purchase.aspose.com/temporary-license/)
- **सपोर्ट:** [Aspose Forum](https://forum.aspose.com/c/pdf/10)

इस गाइड को फॉलो करके, अब आपके पास Aspose.PDF for Java का उपयोग करके **pdf पृष्ठ को छवि** में बदलने और क्रॉप करने की ठोस नींव है। विभिन्न DPI सेटिंग्स, आउटपुट फ़ॉर्मेट, और बैच वर्कफ़्लो के साथ प्रयोग करें ताकि समाधान को अपने प्रोजेक्ट की जरूरतों के अनुसार अनुकूलित किया जा सके.

---

**Last Updated:** 2026-06-07  
**Tested With:** Aspose.PDF for Java 25.3  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## संबंधित ट्यूटोरियल

- [Extract PDF Page Image to BMP with Aspose.PDF for Java](/pdf/java/conversion-export/convert-pdf-pages-to-bmp-aspose-java/)
- [Convert PDF to HTML in Java with Embedded PNG Images using Aspose.PDF](/pdf/java/conversion-export/convert-pdf-to-html-with-png-images-java/)
- [Convert PDF to PNG Using Aspose.PDF for Java – A Comprehensive Guide](/pdf/java/conversion-export/convert-pdf-pages-to-png-aspose-pdf-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}