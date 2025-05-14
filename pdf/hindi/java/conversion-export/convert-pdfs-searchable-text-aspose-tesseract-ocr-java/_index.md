---
"date": "2025-04-14"
"description": "Aspose.PDF और Tesseract OCR का उपयोग करके Java के साथ इमेज-आधारित PDF दस्तावेज़ों को खोज योग्य टेक्स्ट में कैसे परिवर्तित करें, यह जानें। यह मार्गदर्शिका सेटअप, कार्यान्वयन और व्यावहारिक अनुप्रयोगों को कवर करती है।"
"title": "जावा में Aspose.PDF और Tesseract OCR का उपयोग करके PDF को खोज योग्य टेक्स्ट में कैसे बदलें"
"url": "/hi/java/conversion-export/convert-pdfs-searchable-text-aspose-tesseract-ocr-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# जावा में Aspose.PDF और Tesseract OCR का उपयोग करके PDF को खोज योग्य टेक्स्ट में कैसे बदलें

## परिचय

क्या आप स्कैन किए गए या छवि-आधारित PDF दस्तावेज़ों से टेक्स्ट निकालने में चुनौतियों का सामना कर रहे हैं? इन गैर-खोज योग्य फ़ाइलों को खोज योग्य प्रारूपों में बदलना डेटा निष्कर्षण, संग्रह और पहुँच में क्रांतिकारी बदलाव ला सकता है। यह ट्यूटोरियल आपको इस परिवर्तन को कुशलतापूर्वक प्राप्त करने के लिए Tesseract OCR के साथ-साथ Java के लिए Aspose.PDF का उपयोग करने के बारे में मार्गदर्शन करेगा।

**आप क्या सीखेंगे:**
- जावा में टेसेरैक्ट ओसीआर का उपयोग करके पीडीएफ छवियों को पाठ में परिवर्तित करें
- दस्तावेज़ प्रसंस्करण के लिए Aspose.PDF की शक्तिशाली सुविधाओं को लागू करें
- संसाधित दस्तावेज़ को खोज योग्य PDF के रूप में सहेजें

इन कौशलों के साथ, आप अपने दस्तावेज़ों की पूरी क्षमता को अनलॉक कर सकते हैं। कार्यान्वयन में उतरने से पहले, सुनिश्चित करें कि आपके पास सब कुछ तैयार है।

## आवश्यक शर्तें

इस ट्यूटोरियल का प्रभावी ढंग से पालन करने के लिए, सुनिश्चित करें कि आपके पास ये हैं:
- जावा प्रोग्रामिंग की बुनियादी समझ.
- निर्भरता प्रबंधन के लिए मावेन या ग्रेडेल से परिचित होना।
- टेसेरैक्ट ओसीआर सॉफ्टवेयर का स्थापित संस्करण (गूगल से निःशुल्क उपलब्ध)।

इसके अतिरिक्त, जावा परियोजनाओं को संभालने के लिए अपने विकास वातावरण को सेट करें और Aspose.PDF लाइब्रेरी तक पहुंच सुनिश्चित करें।

## Java के लिए Aspose.PDF सेट अप करना

अपने जावा प्रोजेक्ट में Aspose.PDF का उपयोग शुरू करने के लिए, इसे Maven या Gradle के माध्यम से निर्भरता के रूप में जोड़ें:

**मावेन:**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**ग्रेडेल:**

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### लाइसेंस अधिग्रहण

आप Aspose.PDF की क्षमताओं का परीक्षण करने के लिए एक निःशुल्क परीक्षण लाइसेंस प्राप्त कर सकते हैं या विस्तारित परीक्षण के लिए एक अस्थायी लाइसेंस खरीद सकते हैं। [Aspose का लाइसेंसिंग पृष्ठ](https://purchase.aspose.com/temporary-license/) अधिक जानकारी के लिए.

Aspose.PDF को आरंभीकृत और सेट अप करने के लिए, सुनिश्चित करें कि आपकी लाइसेंस फ़ाइल तैयार है और इसे दिखाए अनुसार लागू करें:

```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file.lic");
```

## कार्यान्वयन मार्गदर्शिका

### फ़ीचर 1: टेसेरैक्ट का उपयोग करके OCR रूपांतरण

यह सुविधा दर्शाती है कि कैसे Tesseract OCR का उपयोग करके PDF में छवियों को पाठ में परिवर्तित किया जाए।

#### चरण 1: OCR प्रोसेसिंग के लिए कॉलबैक बनाएं

कॉलबैक फ़ंक्शन `CallBackGetHocr` पीडीएफ से प्रत्येक छवि को संसाधित करता है:

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.Document.CallBackGetHocr;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Scanner;

CallBackGetHocr cbgh = new CallBackGetHocr() {
    @Override
    public String invoke(BufferedImage img) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        File outputfile = new File(dataDir + "/test.jpg");
        try {
            // बफर की गई छवि को JPEG फ़ाइल के रूप में लिखें
            ImageIO.write(img, "jpg", outputfile);
        } catch (IOException e1) {
            e1.printStackTrace();
        }
        
        try {
            // छवि को टेक्स्ट में बदलने और HOCR प्रारूप में संग्रहीत करने के लिए Tesseract OCR निष्पादित करें
            java.lang.Process process = Runtime.getRuntime().exec(
                "tesseract " + dataDir + "/test.jpg " + outputDir + "/out hocr"
            );
            process.waitFor();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }

        // उत्पन्न HOCR HTML फ़ाइल को स्ट्रिंग में पढ़ें
        File file = new File(outputDir + "/out.html");
        StringBuilder fileContents = new StringBuilder((int) file.length());
        Scanner scanner = null;
        try {
            scanner = new Scanner(file);
            String lineSeparator = System.getProperty("line.separator");
            while (scanner.hasNextLine()) {
                fileContents.append(scanner.nextLine() + lineSeparator);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (scanner != null)
                scanner.close();
        }

        // अस्थायी फ़ाइलें हटाएँ
        File fileOut = new File(outputDir + "/out.html");
        if (fileOut.exists()) {
            fileOut.delete();
        }
        File fileTest = new File(dataDir + "/test.jpg");
        if (fileTest.exists()) {
            fileTest.delete();
        }
        return fileContents.toString();
    }
};
```

#### चरण 2: पीडीएफ को खोज योग्य टेक्स्ट में बदलें

मौजूदा गैर-खोज योग्य पीडीएफ को लोड करें और कॉलबैक का उपयोग करके इसे परिवर्तित करें:

```java
// प्लेसहोल्डर निर्देशिका पथ परिभाषित करें
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
String outputDir = "YOUR_OUTPUT_DIRECTORY";

// मौजूदा PDF दस्तावेज़ लोड करें
Document doc = new Document(dataDir + "/outFile.pdf");

// OCR प्रसंस्करण के लिए कॉलबैक का उपयोग करके दस्तावेज़ को परिवर्तित करें
doc.convert(cbgh);

// परिवर्तित दस्तावेज़ को खोज योग्य PDF के रूप में सहेजें
doc.save(outputDir + "/output971.pdf");
```

### फ़ीचर 2: पीडीएफ दस्तावेज़ रूपांतरण और सहेजना

OCR लागू करने के बाद, अपने PDF को खोजने योग्य प्रारूप में सेव करें।

## व्यावहारिक अनुप्रयोगों

1. **संग्रहण:** पुराने स्कैन किए गए दस्तावेज़ों को आसानी से प्राप्त करने के लिए खोजने योग्य प्रारूपों में परिवर्तित करें।
2. **पहुंच:** स्क्रीन रीडर्स के लिए पाठ उपलब्ध कराकर पहुंच में सुधार करें।
3. **डेटा खनन:** विश्लेषण के लिए छवि-आधारित रिपोर्ट या पुस्तकों से पाठ्य डेटा निकालें।
4. **कानूनी दस्तावेज:** बेहतर खोज क्षमता के लिए न्यायालय के अभिलेखों और कानूनी दस्तावेजों को रूपांतरित करें।
5. **एकीकरण:** वेब अनुप्रयोगों या दस्तावेज़ प्रबंधन प्रणालियों में रूपांतरण प्रक्रिया का उपयोग करें।

## प्रदर्शन संबंधी विचार

- **छवि गुणवत्ता अनुकूलित करें:** उच्च रिज़ॉल्यूशन वाली छवियां अधिक सटीक OCR परिणाम प्रदान करती हैं, लेकिन इसके लिए अधिक प्रसंस्करण शक्ति की आवश्यकता होती है।
- **प्रचय संसाधन:** कार्यकुशलता में सुधार के लिए कई फाइलों को बैचों में संभालें।
- **स्मृति प्रबंधन:** जावा मेमोरी उपयोग की निगरानी करें और बड़े दस्तावेज़ों के लिए हीप आकार को उचित रूप से कॉन्फ़िगर करें।

## निष्कर्ष

Aspose.PDF और Tesseract OCR का उपयोग करके PDF को खोज योग्य टेक्स्ट में बदलना छवि-आधारित दस्तावेज़ों से मूल्यवान जानकारी अनलॉक करने का एक शक्तिशाली तरीका है। इस गाइड का पालन करके, आप इस कार्यक्षमता को अपने अनुप्रयोगों में आसानी से एकीकृत कर सकते हैं। विशिष्ट उपयोग मामलों के अनुरूप कोड को अनुकूलित करके या अन्य प्रणालियों के साथ एकीकृत करके आगे की खोज करें।

क्या आप इसे आजमाने के लिए तैयार हैं? आज ही अपनी परियोजनाओं में इन तकनीकों को लागू करना शुरू करें!

## अक्सर पूछे जाने वाले प्रश्न अनुभाग

**प्रश्न 1: क्या मैं बिना लाइसेंस के Java के लिए Aspose.PDF का उपयोग कर सकता हूँ?**
- A1: हाँ, आप Aspose.PDF को इसके निःशुल्क परीक्षण संस्करण के साथ आज़मा सकते हैं, जिसमें कुछ सीमाएँ हैं। पूर्ण कार्यक्षमता के लिए, अस्थायी या स्थायी लाइसेंस प्राप्त करने पर विचार करें।

**प्रश्न 2: टेसेरैक्ट ओसीआर द्वारा कौन से छवि प्रारूप समर्थित हैं?**
- A2: Tesseract JPEG, PNG, TIFF और BMP सहित विभिन्न छवि प्रारूपों का समर्थन करता है। सुनिश्चित करें कि आपकी छवियाँ इष्टतम परिणामों के लिए इन प्रारूपों में हैं।

**प्रश्न 3: मैं ओसीआर प्रक्रिया के दौरान त्रुटियों को कैसे संभालूँ?**
- A3: अपवादों को प्रभावी ढंग से प्रबंधित करने के लिए OCR निष्पादन कोड के आसपास try-catch ब्लॉक का उपयोग करके मजबूत त्रुटि प्रबंधन को लागू करें।

**प्रश्न 4: क्या इस समाधान को वेब अनुप्रयोग में एकीकृत करना संभव है?**
- A4: बिल्कुल! आप Aspose.PDF और Tesseract को सर्वर वातावरण में तैनात कर सकते हैं, जिससे आप API के माध्यम से या अपने बैकएंड सिस्टम के साथ सीधे एकीकरण के माध्यम से दस्तावेज़ों को संसाधित कर सकते हैं।

**प्रश्न 5: टेसेरैक्ट ओसीआर चलाने के लिए सिस्टम आवश्यकताएँ क्या हैं?**
- A5: Tesseract को बुनियादी ऑपरेटिंग सिस्टम समर्थन की आवश्यकता होती है। सुनिश्चित करें कि आपके मशीन पर जावा इंस्टॉल है और साथ ही Tesseract जैसी बाहरी प्रक्रियाओं को निष्पादित करने के लिए सभी आवश्यक अनुमतियाँ हैं।

## संसाधन

- **दस्तावेज़ीकरण:** विस्तृत मार्गदर्शिकाएँ और API संदर्भ देखें [Aspose.PDF दस्तावेज़ीकरण](https://reference.aspose.com/pdf/java/).
- **डाउनलोड करना:** Aspose.PDF के नवीनतम संस्करण तक पहुंचें [डाउनलोड पृष्ठ](https://releases.aspose.com/pdf/java/).
- **खरीदना:** सीधे लाइसेंस प्राप्त करें [Aspose खरीद पृष्ठ](https://purchase.aspose.com/buy).
- **मुफ्त परीक्षण:** निःशुल्क परीक्षण के साथ सुविधाओं का लाभ उठाएँ [Aspose निःशुल्क परीक्षण](https://releases.aspose.com/pdf/java/#downloads).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}