---
category: general
date: 2026-02-20
description: Aspose.Pdf के साथ C# में PDF हस्ताक्षर को मान्य करना और PDF में बेट्स
  नंबरिंग जोड़ना सीखें – चरण‑दर‑चरण कोड, व्याख्याएँ और सर्वोत्तम‑प्रैक्टिस टिप्स।
draft: false
keywords:
- how to validate pdf signature
- add bates numbering to pdf
- pdf signature validation c#
- bates numbering aspaspdf
- pdf conversion pdf/x‑4
language: hi
og_description: Aspose.Pdf का उपयोग करके C# में PDF सिग्नेचर को वैध करने और PDF में
  बेट्स नंबरिंग जोड़ने का तरीका। कोड और टिप्स के साथ पूर्ण ट्यूटोरियल।
og_title: PDF हस्ताक्षर को कैसे मान्य करें और PDF में बेट्स नंबरिंग जोड़ें
tags:
- Aspose.Pdf
- C#
- PDF processing
title: PDF हस्ताक्षर को कैसे सत्यापित करें और PDF में बेट्स नंबरिंग जोड़ें
url: /hi/net/digital-signatures/how-to-validate-pdf-signature-and-add-bates-numbering-to-pdf/
---

दस्तावेज़ लेआउट के अनुसार निर्देशांक समायोजित करें।"

Heading "## Full Working Example" => "## पूर्ण कार्यशील उदाहरण"

Paragraph: "Below is the complete program, ready to copy‑paste into a console app. Replace the placeholder paths and passwords with your own values."

Translate: "नीचे पूर्ण प्रोग्राम दिया गया है, जिसे कॉपी‑पेस्ट करके एक कंसोल ऐप में उपयोग किया जा सकता है। प्लेसहोल्डर पाथ और पासवर्ड को अपने मानों से बदलें।"

Then code block unchanged.

After code block, there is an incomplete code snippet; we keep as is.

Then closing shortcodes.

Also there is a backtop button shortcode at end.

Make sure to keep all shortcodes unchanged.

Now produce final output with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF हस्ताक्षर को मान्य कैसे करें और PDF में Bates नंबरिंग जोड़ें

क्या आपने कभी **PDF हस्ताक्षर को मान्य करने** के बारे में सोचा है, इससे पहले कि आप क्लाइंट को अनुबंध भेजें? शायद आप केस फाइलों को संभाल रहे हैं और आसान ट्रैकिंग के लिए **PDF में Bates नंबरिंग जोड़ने** का भरोसेमंद तरीका चाहिए। जो भी हो, आप सही जगह पर आए हैं। इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे दोनों किया जाए – मौजूदा डिजिटल हस्ताक्षर को मान्य किया जाए, फिर Aspose.Pdf for .NET का उपयोग करके आपके दस्तावेज़ पर क्रमिक Bates नंबर स्टैम्प किए जाएँ।

हम कुछ अतिरिक्त ट्रिक्स भी जोड़ेंगे: PDF/X‑4 में रूपांतरण, पेज रिसोर्सेज़ को समायोजित करना, इमेज को रास्टर किए बिना HTML में निर्यात करना, और अंत में SHA‑3 आधारित डिजिटल हस्ताक्षर लागू करना। अंत तक आपके पास एक एकल C# प्रोग्राम होगा जो पूरे वर्कफ़्लो को संभालता है, उत्पादन के लिए तैयार या तेज़ प्रूफ़‑ऑफ़‑कॉन्सेप्ट के रूप में।

## आपको क्या चाहिए

- **.NET 6+** (या .NET Framework 4.7.2 – API समान रूप से काम करता है)
- **Aspose.Pdf for .NET** NuGet पैकेज (लेखन के समय नवीनतम संस्करण, 23.12)
- एक **PDF फ़ाइल** जिसमें मौजूदा हस्ताक्षर हो (`input.pdf`)
- एक **PKCS#7 प्रमाणपत्र** (`cert.pfx`) और उसका पासवर्ड
- थोड़ा बहुत C# अनुभव – हम कोड को स्पष्ट और विस्तृत टिप्पणी के साथ रखेंगे।

यदि इनमें से कोई भी परिचित नहीं लग रहा है, तो रुकें और आवश्यक भाग प्राप्त करें; बाकी गाइड मानता है कि ये पहले से मौजूद हैं।

---

## चरण 1: PDF दस्तावेज़ लोड करें  

सबसे पहले आपको एक `Document` ऑब्जेक्ट बनाना होता है जो पूरे PDF फ़ाइल का प्रतिनिधित्व करता है। इसे Excel में वर्कबुक लोड करने के समान समझें – आपको ऑब्जेक्ट चाहिए ताकि आप किसी भी चीज़ को निरीक्षण या संशोधित कर सकें।

```csharp
using System;
using Aspose.Pdf;

static void Main()
{
    // Load the source PDF that may already contain a digital signature
    Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **यह क्यों महत्वपूर्ण है:** दस्तावेज़ को लोड किए बिना आप हस्ताक्षर फ़ील्ड या पेज कलेक्शन तक पहुँच नहीं सकते। Aspose.Pdf लो‑लेवल PDF संरचना को एब्स्ट्रैक्ट करता है, जिससे आप `Pages` और `Resources` जैसे हाई‑लेवल ऑब्जेक्ट्स के साथ काम कर सकते हैं।

---

## चरण 2: मौजूदा PDF हस्ताक्षर को मान्य करें  

अब हम मुख्य प्रश्न का उत्तर देते हैं: **PDF हस्ताक्षर को कैसे मान्य करें**? `PdfFileSignature` क्लास एक `ValidateSignature` मेथड प्रदान करती है जो एक `SignatureValidationResult` लौटाती है। यह बताती है कि हस्ताक्षर सही है, रद्द किया गया है, या समझौता हुआ है।

```csharp
    // Detect if the existing signature is compromised
    PdfFileSignature signatureValidator = new PdfFileSignature(pdfDocument);
    var validationResult = signatureValidator.ValidateSignature();

    Console.WriteLine($"Compromised? {validationResult.IsCompromised}");
```

> **प्रो टिप:** `IsCompromised` `true` लौटाता है यदि दस्तावेज़ पर हस्ताक्षर के बाद बदलाव किया गया हो, या यदि प्रमाणपत्र श्रृंखला को सत्यापित नहीं किया जा सकता। फॉरेंसिक उद्देश्यों के लिए, विस्तृत संदेशों के लिए `validationResult.ValidationErrors` को भी जांचें।

---

## चरण 3: PDF/X‑4 में रूपांतरण (वैकल्पिक लेकिन उपयोगी)  

कानूनी और अभिलेखीय वर्कफ़्लो अक्सर PDF/X अनुपालन की मांग करते हैं। PDF/X‑4 में रूपांतरण करने से किसी भी बचे हुए रूपांतरण त्रुटियों को हटाया जाता है जो डाउनस्ट्रीम सिस्टम को प्रभावित कर सकती हैं।

```csharp
    // Convert the PDF to PDF/X‑4, deleting any conversion errors automatically
    PdfFormatConversionOptions conversionOptions =
        new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);
    pdfDocument.Convert(conversionOptions);
```

> **क्यों रूपांतरण करें?** PDF/X‑4 यह सुनिश्चित करता है कि सभी रंग प्रोफ़ाइल और फ़ॉन्ट एम्बेडेड हों, जिससे फ़ाइल को विभिन्न प्लेटफ़ॉर्म पर खोलने पर रेंडरिंग समस्याओं का जोखिम कम हो जाता है।

---

## चरण 4: PDF में Bates नंबरिंग जोड़ें  

यहाँ हम **PDF में Bates नंबरिंग जोड़ते** हैं – मुकदमेबाज़ी, ऑडिट या किसी भी बड़े दस्तावेज़ सेट के लिए आवश्यक। `BatesNumberingOptions` आपको प्रीफ़िक्स, प्रारंभिक संख्या और यहां तक कि फ़ॉर्मेटिंग सेट करने की अनुमति देता है।

```csharp
    // Add Bates numbering for case management
    BatesNumberingOptions batesOptions = new BatesNumberingOptions
    {
        Prefix = "CASE",   // You can change this to any identifier you need
        Start = 5000       // Starting number – adjust as required
    };
    pdfDocument.Pages.AddBatesNumbering(batesOptions);
```

> **वास्तविक‑दुनिया टिप:** प्रीफ़िक्स को छोटा रखें (3‑5 अक्षर) ताकि संकरी पृष्ठों पर लाइन‑रैपिंग न हो। यदि आपको सेक्शन‑वार नंबरिंग चाहिए, तो पूरे दस्तावेज़ के बजाय पृष्ठों के एक उपसमुच्चय पर `AddBatesNumbering` चलाएँ।

---

## चरण 5: ExtGState डिक्शनरी डालें (रेडैक्शन अपारदर्शिता उदाहरण)  

कभी‑कभी आपको ग्राफ़िक्स स्टेट को नियंत्रित करने की आवश्यकता होती है – उदाहरण के लिए, अर्ध‑पारदर्शी रेडैक्शन ओवरले सेट करना। यह चरण दिखाता है कि कैसे कस्टम ExtGState डिक्शनरी को पहले पृष्ठ के रिसोर्सेज़ में इंजेक्ट किया जाए।

```csharp
    // Insert an ExtGState dictionary on the first page (example: redaction opacity)
    Page firstPage = pdfDocument.Pages[1];
    DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
    CosPdfDictionary extGStateDictionary = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    extGStateDictionary.Add("CA", new CosPdfNumber(1));   // stroke opacity
    extGStateDictionary.Add("ca", new CosPdfNumber(0.5)); // fill opacity
    resourcesEditor["ExtGState"] = extGStateDictionary;
```

> **कब उपयोग करें:** यदि आप एक रेडैक्शन टूल बना रहे हैं, तो आप बाद में संवेदनशील टेक्स्ट को कवर करने वाले आकारों को ड्रॉ करते समय इस ExtGState को रेफ़र करेंगे।

---

## चरण 6: इमेज को रास्टर किए बिना HTML के रूप में सहेजें  

HTML में निर्यात करना वेब प्रीव्यू के लिए उपयोगी हो सकता है। डिफ़ॉल्ट रूप से Aspose.Pdf इमेज को रास्टर करता है, जिससे फ़ाइल आकार बढ़ जाता है। `SkipRasterImages` सेट करने से मूल वेक्टर संरक्षित रहते हैं।

```csharp
    // Save the document as HTML without rasterizing images
    HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions { SkipRasterImages = true };
    pdfDocument.Save("YOUR_DIRECTORY/output.html", htmlSaveOptions);
```

> **परिणाम:** परिणामी `output.html` में हल्के `<img>` टैग होते हैं जो मूल इमेज स्ट्रीम की ओर इशारा करते हैं, जिससे पृष्ठ साफ़ और तेज़ लोड होता है।

---

## चरण 7: SHA‑3 हैश के साथ PDF पर हस्ताक्षर करें  

अंत में, हम (अब नंबरित) PDF को SHA‑3‑512 हैश का उपयोग करके साइन करते हैं। SHA‑3 पारंपरिक SHA‑256 से नया है और एक अलग क्रिप्टोग्राफ़िक निर्माण प्रदान करता है, जिसे कुछ अनुपालन मानकों ने अब आवश्यक बना दिया है।

```csharp
    // Sign the PDF using a SHA‑3 hash and save the signed version
    PKCS7Detached pkcs7Signature = new PKCS7Detached(
        "YOUR_DIRECTORY/cert.pfx",
        "YOUR_PASSWORD",
        DigestHashAlgorithm.Sha3_512);

    PdfFileSignature pdfSigner = new PdfFileSignature(pdfDocument);
    // Sign on page 1, visible rectangle (x, y, width, height)
    pdfSigner.Sign(1, true, new Rectangle(100, 100, 200, 150), pkcs7Signature);
    pdfSigner.Save("YOUR_DIRECTORY/signed.pdf");
}
```

> **महत्वपूर्ण:** आयत निर्धारित करती है कि दृश्य हस्ताक्षर उपस्थिति कहाँ रखी जाएगी। अपने दस्तावेज़ लेआउट के अनुसार निर्देशांक समायोजित करें।

---

## पूर्ण कार्यशील उदाहरण  

नीचे पूर्ण प्रोग्राम दिया गया है, जिसे कॉपी‑पेस्ट करके एक कंसोल ऐप में उपयोग किया जा सकता है। प्लेसहोल्डर पाथ और पासवर्ड को अपने मानों से बदलें।

```csharp
using System;
using Aspose.Pdf;

static void Main()
{
    // 1️⃣ Load the PDF
    Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

    // 2️⃣ Validate existing signature
    PdfFileSignature signatureValidator = new PdfFileSignature(pdfDocument);
    var validationResult = signatureValidator.ValidateSignature();
    Console.WriteLine($"Compromised? {validationResult.IsCompromised}");

    // 3️⃣ Convert to PDF/X‑4
    PdfFormatConversionOptions conversionOptions =
        new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);
    pdfDocument.Convert(conversionOptions);

    // 4️⃣ Add Bates numbering (add bates numbering to pdf)
    BatesNumberingOptions batesOptions = new BatesNumberingOptions
    {
        Prefix = "CASE",
        Start = 5000
    };
    pdfDocument.Pages.AddBatesNumbering(batesOptions);

    // 5️⃣ Insert ExtGState (redaction opacity)
    Page firstPage = pdfDocument.Pages[1];
    DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
    CosPdfDictionary extGStateDictionary = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    extGStateDictionary.Add("CA", new CosPdfNumber(1));
    extGStateDictionary.Add("ca", new CosPdfNumber(0.5));
    resourcesEditor["ExtGState"] = extGStateDictionary;

    // 6️⃣ Save as HTML (no raster images)
    HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions { SkipRasterImages = true };
    pdfDocument.Save("YOUR_DIRECTORY/output.html", htmlSaveOptions);

    // 7️⃣ Sign with SHA‑3
    PKCS7Detached pkcs7Signature = new PKCS7Detached(
        "YOUR_DIRECTORY/cert.pfx",
        "YOUR_PASSWORD",
        Digest

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}