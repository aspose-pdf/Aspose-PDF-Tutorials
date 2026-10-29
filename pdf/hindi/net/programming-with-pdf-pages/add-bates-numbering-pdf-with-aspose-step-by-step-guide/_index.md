---
category: general
date: 2026-08-08
description: C# में Aspose.Pdf का उपयोग करके PDF में बेट्स नंबरिंग जोड़ें। यह ट्यूटोरियल
  यह भी दिखाता है कि कैसे खाली पृष्ठ वाला PDF जोड़ें और प्रोग्रामेटिक रूप से PDF जनरेट
  करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: hi
lastmod: 2026-08-08
og_description: C# में Aspose.Pdf के साथ बेट्स नंबरिंग PDF जोड़ें। ब्लैंक पेज PDF
  जोड़ना सीखें, प्रोग्रामेटिकली PDF जेनरेट करें, और मिनटों में अंतिम दस्तावेज़ सहेजें।
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Aspose के साथ PDF में Bates नंबरिंग जोड़ें – पूर्ण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Aspose के साथ PDF में Bates नंबरिंग जोड़ें – चरण‑दर‑चरण गाइड
url: /hi/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose के साथ PDF में bates नंबरिंग जोड़ें – चरण‑दर‑चरण गाइड

Aspose.Pdf के साथ PDF में bates नंबरिंग जोड़ना सरल है जब आप मूल चरणों को समझ लेते हैं। यदि आपको खाली पृष्ठ PDF जोड़ने या प्रोग्रामेटिक रूप से PDF उत्पन्न करने की भी आवश्यकता है, तो यह गाइड आपकी सभी आवश्यकताओं को कवर करता है।

इस ट्यूटोरियल में आप करेंगे:

* शुरुआत से एक नया PDF दस्तावेज़ बनाएं।  
* एक खाली पृष्ठ PDF जोड़ें जो Bates नंबरों को होस्ट करेगा।  
* कस्टम प्रीफ़िक्स के साथ Bates नंबरिंग आर्टिफैक्ट को कॉन्फ़िगर करें।  
* PDF को सहेजें ताकि नंबर उत्पन्न फ़ाइल में दिखाई दें।  

अंत तक आपके पास एक पूर्ण कार्यात्मक C# कंसोल एप्लिकेशन होगा जो **CASE‑1000**, **CASE‑1001**, … जैसे Bates नंबरों वाला PDF उत्पन्न करता है – कानूनी और e‑discovery कार्यप्रवाहों के लिए एक सामान्य आवश्यकता।

## पूर्वापेक्षाएँ

* .NET 6.0 SDK या बाद का संस्करण (कोड .NET Framework 4.8 के साथ भी काम करता है)।  
* Visual Studio 2022 या कोई भी C#‑संगत IDE।  
* एक वैध Aspose.Pdf for .NET लाइसेंस (या एक मुफ्त मूल्यांकन कुंजी)।  
* C# सिंटैक्स की बुनियादी परिचितता।  

> **प्रो टिप:** यदि आप कोड को बिना लाइसेंस के चलाते हैं, तो Aspose आउटपुट PDF में एक छोटा वॉटरमार्क जोड़ देगा।

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose.Pdf इम्पोर्ट करें

एक नया कंसोल प्रोजेक्ट बनाएं और Aspose.Pdf NuGet पैकेज जोड़ें:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

उदाहरण के लिए आवश्यक `using` निर्देश इस प्रकार हैं:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

ये नेमस्पेस आपको बाद में उपयोग किए जाने वाले `Document`, `Page`, और `BatesNumberingArtifact` क्लासेज़ तक पहुँच प्रदान करते हैं।

## चरण 2: एक खाली पृष्ठ PDF जोड़ें

Bates नंबर को किसी पृष्ठ से संलग्न होना आवश्यक है, इसलिए हम पहले एक खाली पृष्ठ बनाते हैं जो नंबरिंग आर्टिफैक्ट प्राप्त करेगा।

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

`Document` क्लास पूरे PDF फ़ाइल का प्रतिनिधित्व करता है, जबकि `Pages.Add()` दस्तावेज़ के पृष्ठ संग्रह के अंत में एक नया, खाली पृष्ठ सम्मिलित करता है। क्योंकि दस्तावेज़ शुरू में खाली है, यह कॉल पहला पृष्ठ भी बनाता है।

## चरण 3: Bates नंबरिंग आर्टिफैक्ट को कॉन्फ़िगर करें

अब हम परिभाषित करते हैं कि Bates नंबर कैसे दिखने चाहिए। `BatesNumberingArtifact` आपको प्रारंभिक संख्या, प्रीफ़िक्स, सफ़िक्स, और फ़ॉर्मेटिंग विकल्प सेट करने की अनुमति देता है।

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**यह क्यों महत्वपूर्ण है:**  
`StartNumber` को **1000** पर सेट करने से सामान्य कानूनी केस फ़ाइल परम्पराओं से मेल खाता है। `Prefix` सुनिश्चित करता है कि प्रत्येक संख्या **CASE‑1000**, **CASE‑1001**, … के रूप में दिखाई दे, जिससे खोज और क्रमबद्ध करना आसान हो जाता है।

## चरण 4: आर्टिफैक्ट को पृष्ठ से संलग्न करें

आर्टिफैक्ट को पृष्ठ के `Artifacts` संग्रह में जोड़ना आवश्यक है ताकि Aspose सहेजते समय इसे प्रत्येक पृष्ठ पर रेंडर करे।

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

जब दस्तावेज़ सहेजा जाता है, तो Aspose स्वचालित रूप से सभी पृष्ठों पर आर्टिफैक्ट को दोहराता है, और प्रत्येक अगले पृष्ठ के लिए संख्या बढ़ाता है।

## चरण 5: (वैकल्पिक) अतिरिक्त पृष्ठ जोड़ें

यदि आपको अधिक पृष्ठों की आवश्यकता है, तो बस `pdfDocument.Pages.Add()` को दोहराएँ। पिछले चरण में संलग्न किया गया Bates नंबरिंग आर्टिफैक्ट प्रत्येक नए पृष्ठ पर स्वचालित रूप से दिखाई देगा।

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## चरण 6: PDF सहेजें – प्रोग्रामेटिक रूप से PDF उत्पन्न करें

अंत में, दस्तावेज़ को डिस्क पर सहेजें। यही वह बिंदु है जहाँ Bates नंबर पृष्ठों पर रेंडर होते हैं।

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**अपेक्षित परिणाम:**  
*BatesNumberedDocument.pdf* खोलें और आपको एक तीन‑पृष्ठीय PDF दिखाई देगा। प्रत्येक पृष्ठ नीचे‑दाएँ कोने में एक Bates नंबर दिखाता है:

* पृष्ठ 1 → **CASE‑1000**  
* पृष्ठ 2 → **CASE‑1001**  
* पृष्ठ 3 → **CASE‑1002**

संख्याएँ स्वचालित रूप से बढ़ती हैं क्योंकि आर्टिफैक्ट पृष्ठ संग्रह से जुड़ा हुआ है।

## पूर्ण, चलाने योग्य उदाहरण

सब कुछ मिलाकर, यहाँ एक पूर्ण कंसोल प्रोग्राम है जिसे आप कॉपी, पेस्ट और चलाकर उपयोग कर सकते हैं:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

`dotnet run` के साथ प्रोग्राम चलाएँ। निष्पादन के बाद, फ़ाइल को अपने डेस्कटॉप पर खोजें और Bates नंबरों की पुष्टि करें।

![bates नंबरिंग PDF उदाहरण](/images/bates-numbering.png "bates नंबरिंग PDF उदाहरण")

## सामान्य प्रश्न और किनारे के मामले

### यदि मुझे अलग फ़ॉन्ट या स्थिति चाहिए तो क्या करें?

`BatesNumberingArtifact` `FontSize`, `FontColor`, `HorizontalAlignment`, और `VerticalAlignment` जैसी प्रॉपर्टीज़ को उजागर करता है। उदाहरण के लिए:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### किसी विशिष्ट पृष्ठ को नंबरिंग से कैसे बाहर रखें?

उन पृष्ठों के लिए एक अलग `BatesNumberingArtifact` बनाएं जिन्हें आप नंबर करना चाहते हैं और इसे केवल उन पृष्ठों में जोड़ें। जिन पृष्ठों में कोई आर्टिफैक्ट संलग्न नहीं है, वे अननंबर रहेंगे।

### क्या यह मौजूदा PDFs के साथ काम करता है?

हां। `new Document()` के बजाय, मौजूदा फ़ाइल लोड करें:

```csharp
Document pdfDocument = new Document("input.pdf");
```

फिर इच्छित पृष्ठों पर आर्टिफैक्ट संलग्न करें और सहेजें।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Pdf का उपयोग करके **bates नंबरिंग PDF कैसे जोड़ें**, **खाली पृष्ठ PDF कैसे जोड़ें**, और **प्रोग्रामेटिक रूप से PDF कैसे उत्पन्न करें** एक साफ़, पुन: उपयोग योग्य C# समाधान में। यह तरीका किसी भी संख्या में पृष्ठों, कस्टम प्रीफ़िक्स, और स्टाइलिंग विकल्पों के साथ काम करता है, जिससे आपको अंतिम दस्तावेज़ पर पूर्ण नियंत्रण मिलता है।

अगले कदम जिन्हें आप देख सकते हैं:

* उपयोग करें **create pdf as

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.PDF for .NET का उपयोग करके PDFs में पृष्ठ संख्याएँ जोड़ना और अनुकूलित करना | दस्तावेज़ हेरफेर गाइड](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF for .NET का उपयोग करके PDF के अंत में एक खाली पृष्ठ जोड़ना | चरण‑दर‑चरण गाइड](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Aspose.PDF के साथ PDF दस्तावेज़ बनाएं – पृष्ठ, आकार जोड़ें और सहेजें](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}