---
category: general
date: 2026-03-29
description: एक ही प्रक्रिया में PDF को PDF/X‑1a में बदलें और PDF पृष्ठ को PNG के
  रूप में निर्यात करें – साथ ही Aspose.Pdf (C#) का उपयोग करके PDF में टेक्स्ट स्टैंप
  कैसे जोड़ें, सीखें।
draft: false
keywords:
- convert pdf to pdf/x-1a
- export pdf page png
- add text stamp pdf
- Aspose.Pdf conversion
- PDF/X‑1a workflow
language: hi
og_description: PDF को PDF/X‑1a में बदलें और PDF पेज को PNG में निर्यात करें, साथ
  ही टेक्स्ट स्टैम्प PDF जोड़ें – Aspose.Pdf के साथ पूर्ण C# गाइड।
og_title: PDF को PDF/X‑1A में बदलें, पृष्ठ को PNG के रूप में निर्यात करें और टेक्स्ट
  स्टैम्प जोड़ें
tags:
- Aspose.Pdf
- C#
- PDF processing
title: पीडीएफ को पीडीएफ/एक्स‑1ए में बदलें, पेज को पीएनजी के रूप में निर्यात करें और
  टेक्स्ट स्टैम्प जोड़ें
url: /hi/net/conversion-export/convert-pdf-to-pdf-x-1a-export-page-png-add-text-stamp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF को PDF/X‑1a में बदलें, पेज PNG निर्यात करें और टेक्स्ट स्टैम्प जोड़ें – पूर्ण C# गाइड

क्या आपको कभी **PDF को PDF/X‑1a में बदलने** की जरूरत पड़ी, लेकिन साथ ही पहले पेज का त्वरित PNG प्रीव्यू और उसी दस्तावेज़ पर एक कस्टम टेक्स्ट स्टैम्प चाहिए था? आप अकेले नहीं हैं। कई प्रोडक्शन पाइपलाइनों में—जैसे प्रिंट‑रेडी प्री‑फ़्लाइटिंग या ऑटोमेटेड रिपोर्ट जेनरेशन—आप अक्सर इस सटीक संयोजन की माँग का सामना करते हैं।

इस ट्यूटोरियल में हम एक ही, सुसंगत वर्कफ़्लो को चरण‑दर‑चरण देखेंगे जो क्रमशः तीन काम करता है: **PDF को PDF/X‑1a में बदलना**, **PDF पेज को PNG में निर्यात करना**, और **PDF में टेक्स्ट स्टैम्प जोड़ना**। कोड .NET के लिए Aspose.Pdf लाइब्रेरी का उपयोग करता है, इसलिए आप लो‑लेवल PDF इंटर्नल्स से जूझे बिना एक प्रोफेशनल‑ग्रेड समाधान प्राप्त करते हैं। अंत तक आपके पास एक रन‑एबल C# प्रोग्राम होगा जिसे आप किसी भी कंसोल ऐप, Azure Function, या CI स्टेप में डाल सकते हैं।

> **आपको क्या मिलेगा** – एक पूर्ण सोर्स फ़ाइल, चरण‑बद्ध व्याख्याएँ, सामान्य pitfalls के लिए टिप्स, और आउटपुट को जल्दी से वेरिफ़ाई करने का तरीका।

## Prerequisites

- .NET 6.0 या बाद का (API .NET Framework 4.x के साथ भी काम करता है)।  
- Aspose.Pdf for .NET NuGet पैकेज (`Aspose.Pdf`) – लेखन के समय संस्करण 23.10 नवीनतम है।  
- एक इनपुट PDF (`input.pdf`) और एक ICC प्रोफ़ाइल फ़ाइल (`Coated_Fogra39L_VIGC_300.icc`) जिसे आप नियंत्रित फ़ोल्डर में रखें।  
- C# और Visual Studio (या आपका पसंदीदा IDE) की बुनियादी जानकारी।

यदि इनमें से कोई भी चीज़ अपरिचित लग रही है, तो बस NuGet पैकेज इस प्रकार इंस्टॉल करें:

```bash
dotnet add package Aspose.Pdf --version 23.10.0
```

अब चलिए शुरू करते हैं।

## Step 1: Load the source PDF document

सबसे पहले हम उस PDF को खोलते हैं जिसपर काम करना है। Aspose.Pdf की `Document` क्लास पूरी फ़ाइल को दर्शाती है, और यह लेज़ीली कंटेंट लोड करती है, इसलिए जब तक आप पेजेस को एक्सेस नहीं करते तब तक कोई परफ़ॉर्मेंस पेनाल्टी नहीं लगती।

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using Aspose.Pdf.Conversion;

// Adjust these paths to match your environment
string baseDir = @"C:\MyProjects\PdfDemo\";
string inputPath = Path.Combine(baseDir, "input.pdf");

// Load the PDF – this is where any file‑not‑found errors will surface
Document pdfDoc = new Document(inputPath);
```

*यह क्यों महत्वपूर्ण है*: दस्तावेज़ को पहले लोड करने से हमें एक ही ऑब्जेक्ट मिलता है जिसे हम कन्वर्ज़न, रेंडरिंग और स्टैम्पिंग के लिए पास कर सकते हैं। यदि आप स्पष्ट लोड को स्किप करके गैर‑मौजूद फ़ाइल पर काम करने की कोशिश करेंगे, तो बाद में आपको एक cryptic `FileNotFoundException` मिलेगा।

## Step 2: Convert the document to PDF/X‑1a using a custom ICC profile

PDF/X‑1a प्रिंट‑रेडी PDFs के लिए de‑facto मानक है। इस कन्वर्ज़न स्टेप में आप **Output Intent** (ICC प्रोफ़ाइल) भी एम्बेड कर सकते हैं ताकि डाउनस्ट्रीम RIPs को ठीक‑ठीक पता हो कि रंग कैसे इंटरप्रेट किए जाने चाहिए।

```csharp
// Prepare conversion options – we ask Aspose to delete any objects that would break PDF/X‑1a compliance
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // Drop non‑compliant objects automatically
{
    IccProfileFileName = Path.Combine(baseDir, "Coated_Fogra39L_VIGC_300.icc"),
    OutputIntent = new OutputIntent("FOGRA39") // Human‑readable name for the intent
};

// Perform the conversion in‑place
pdfDoc.Convert(conversionOptions);
```

*Pro tip*: यदि आपको कड़ी एरर हैंडलिंग चाहिए, तो `ConvertErrorAction.Delete` को `ConvertErrorAction.Throw` से बदल दें। इस तरह पहला compliance issue मिलने पर कन्वर्ज़न तुरंत abort हो जाएगा, जो ऑटोमेटेड QA पाइपलाइनों के लिए उपयोगी है।

## Step 3: Export the first page as a PNG while analyzing fonts

PNG प्रीव्यू अक्सर तेज़ विज़ुअल चेक या थंबनेल जेनरेशन के लिए आवश्यक होता है। `AnalyzeFonts` को सक्षम करके Aspose सुनिश्चित करता है कि एम्बेडेड फ़ॉन्ट्स सही‑से‑रास्टराइज़ हों, जिससे missing‑glyph समस्याएँ नहीं आतीं।

```csharp
// Configure the PNG device – you can tweak resolution, color depth, etc.
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions
    {
        AnalyzeFonts = true,          // Guarantees faithful text rendering
        Resolution = 300              // 300 DPI is a good trade‑off for quality vs. size
    }
};

// Export the first page (index is 1‑based)
string pngPath = Path.Combine(baseDir, "page1.png");
pngDevice.Process(pdfDoc.Pages[1], pngPath);
```

इस प्रक्रिया के बाद आपको `page1.png` स्रोत फ़ाइलों के बगल में मिल जाएगा। इसे किसी भी इमेज व्यूअर में खोलें और पुष्टि करें कि कन्वर्ज़न सही दिख रहा है।

## Step 4: Add a text stamp that automatically adjusts its font size

एक **टेक्स्ट स्टैम्प** PDF पर वॉटरमार्क या एनोटेशन जोड़ने का सुविधाजनक तरीका है, बिना मूल कंटेंट स्ट्रीम को बदले। `AutoAdjustFontSizeToFitStampRectangle` सेट करने से लाइब्रेरी टेक्स्ट को स्वचालित रूप से छोटा या बड़ा कर देती है ताकि वह आपके द्वारा परिभाषित रेक्टेंगल के बाहर न जाए।

```csharp
// Create a stamp with the desired text
TextStamp autoSizeStamp = new TextStamp("Auto‑size")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    Width = 400,        // Width of the stamp rectangle (points)
    Height = 200,       // Height of the stamp rectangle (points)
    // Optional: position the stamp – here we center it on the page
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Center,
    // Optional: give it a semi‑transparent background for readability
    Background = new BackgroundInfo(Color.FromRgb(255, 255, 0), 0.3f)
};

// Attach the stamp to the first page (you could loop over all pages if needed)
pdfDoc.Pages[1].AddStamp(autoSizeStamp);
```

*ऑटो‑साइज़ क्यों?* यदि बाद में आप स्टैम्प टेक्स्ट को लंबा (जैसे डायनामिक टाइमस्टैम्प) बदलते हैं, तो आपको मैन्युअली फ़ॉन्ट साइज री‑कैल्कुलेट नहीं करना पड़ेगा—स्टैम्प फ़्लाई पर एडजस्ट हो जाएगा।

## Step 5: Save the updated PDF document

अंत में सब कुछ डिस्क पर लिखें। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या एक नई फ़ाइल बना सकते हैं; नीचे दिया गया उदाहरण `output.pdf` बनाता है।

```csharp
string outputPath = Path.Combine(baseDir, "output.pdf");
pdfDoc.Save(outputPath);
```

सेव पूरा होने पर आपके पास होगा:

1. एक **PDF/X‑1a** कंप्लायंट फ़ाइल (`output.pdf`)।  
2. पहले पेज का **PNG प्रीव्यू** (`page1.png`)।  
3. एक **टेक्स्ट स्टैम्प** जो अपने रेक्टेंगल में पूरी तरह फिट बैठता है।

### Quick verification checklist

| ✅ जाँच | कैसे सत्यापित करें |
|--------|-------------------|
| PDF/X‑1a अनुपालन | Adobe Acrobat में `output.pdf` खोलें → *Print Production* → *Preflight* और “PDF/X‑1a:2001” चुनें। |
| PNG सही दिख रहा है | `page1.png` को Windows Photo Viewer या किसी भी इमेज एडिटर में खोलें। |
| स्टैम्प दिखाई दे | `output.pdf` को स्क्रॉल करें – टेक्स्ट “Auto‑size” पेज 1 पर केंद्रित होना चाहिए। |

![PDF को PDF/X‑1a में बदलने का पूर्वावलोकन](image.png "स्टैम्प वाला पेज दिखाते हुए PDF को PDF/X‑1a में बदलने का पूर्वावलोकन")

*Image alt text*: **ऑटो‑साइज़ टेक्स्ट स्टैम्प के साथ PDF को PDF/X‑1a में बदलने का पूर्वावलोकन** – सभी चरणों के बाद अंतिम PDF को दर्शाता है।

## Common Variations & Edge Cases

- **एकाधिक पेजेस** – यदि आपको हर पेज पर स्टैम्प लगाना है, तो `pdfDoc.Pages` पर लूप लगाएँ और लूप के अंदर `AddStamp` कॉल करें।  
- **विभिन्न आउटपुट फ़ॉर्मेट** – आर्काइवल PDFs के लिए `PdfFormat.PDF_X_1A` को `PdfFormat.PDF_A_1B` में बदलें।  
- **हाई‑रेज़ोल्यूशन PNG** – प्रिंट‑क्वालिटी थंबनेल के लिए `RenderingOptions` में `Resolution = 600` सेट करें।  
- **स्टैम्प के लिए कस्टम फ़ॉन्ट** – स्टैम्प जोड़ने से पहले `autoSizeStamp.Font = FontRepository.FindFont("Arial")` असाइन करें।  
- **एरर हैंडलिंग** – प्रत्येक प्रमुख स्टेप को `try/catch` में रैप करें और डिबगिंग आसान बनाने के लिए `ConversionException` या `FileNotFoundException` को लॉग करें।

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using Aspose.Pdf.Conversion;
using Aspose.Pdf.Color; // For BackgroundInfo color

class PdfX1aWorkflow
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Setup paths
        // -----------------------------------------------------------------
        string baseDir = @"C:\MyProjects\PdfDemo\";
        string inputPdf = Path.Combine(baseDir, "input.pdf");
        string iccProfile = Path.Combine(baseDir, "Coated_Fogra39L_VIGC_300.icc");
        string pngOutput = Path.Combine(baseDir, "page1.png");
        string finalPdf = Path.Combine(baseDir, "output.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Load the source document
        // -----------------------------------------------------------------
        Document pdfDoc = new Document(inputPdf);

        // -----------------------------------------------------------------
        // 3️⃣ Convert to PDF/X‑1a (print‑ready)
        // -----------------------------------------------------------------
        PdfFormatConversionOptions convOpts = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = iccProfile,
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDoc.Convert(convOpts);

        // -----------------------------------------------------------------
        // 4️⃣ Export first page as PNG (export pdf page png)
        // -----------------------------------------------------------------
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions
            {
                AnalyzeFonts = true,
                Resolution = 300
            }
        };
        pngDevice.Process(pdfDoc.Pages[1], pngOutput);

        // -----------------------------------------------------------------
        // 5️⃣ Add auto‑sizing text stamp (add text stamp pdf)
        // -----------------------------------------------------------------
        TextStamp stamp = new TextStamp("Auto‑size")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Width = 400,
            Height = 200,
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Center,
            Background = new BackgroundInfo(Color.From

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}