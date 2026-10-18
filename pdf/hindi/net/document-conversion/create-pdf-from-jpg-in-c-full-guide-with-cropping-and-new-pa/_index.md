---
category: general
date: 2026-04-06
description: JPG से जल्दी PDF बनाएं और सीखें कि PDF में छवि को कैसे क्रॉप करें, नया
  PDF पेज जोड़ें, और C# का उपयोग करके क्रॉप के साथ JPG को PDF में बदलें।
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: hi
og_description: C# के साथ JPG से PDF बनाएं और PDF में छवि को क्रॉप करें। नई PDF पेज
  जोड़ना और JPG को क्रॉप के साथ PDF में बदलना सीखें।
og_title: C# में JPG से PDF बनाएं – चरण-दर-चरण गाइड
tags:
- Aspose.Pdf
- C#
- PDF generation
title: C# में JPG से PDF बनाएं – क्रॉपिंग और नई पृष्ठों के साथ पूर्ण गाइड
url: /hi/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में JPG से PDF बनाएं – क्रॉपिंग और नई पेजेस के साथ पूर्ण गाइड

क्या आपको कभी **create PDF from JPG** करने की ज़रूरत पड़ी है लेकिन आप नहीं जानते थे कि केवल वही भाग कैसे रखें जो आप वास्तव में चाहते हैं? आप अकेले नहीं हैं। कई ऐप्स में—जैसे इनवॉइस, रसीदें, या फोटो‑बुक्स—डेवलपर्स को एक तस्वीर को PDF में बदलना पड़ता है जबकि अनचाहे किनारों को हटाना पड़ता है।  

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने योग्य समाधान के माध्यम से चलेंगे जो **creates PDF from JPG** करता है, आपको दिखाएगा कि **crop image in PDF** कैसे करें, और यह दर्शाएगा कि **how to add new pdf page** कैसे किया जाता है जब आपको एक से अधिक तस्वीरों की आवश्यकता हो। अंत तक आप यह भी जान जाएंगे कि **convert JPG to PDF with crop** और **insert image into PDF C#** कैसे किया जाता है Aspose.Pdf लाइब्रेरी का उपयोग करके।

## आप क्या सीखेंगे

- .NET प्रोजेक्ट में Aspose.Pdf सेट अप करें (कोई भारी कॉन्फ़िगरेशन आवश्यक नहीं)।
- एक JPEG लोड करें, वह क्षेत्र निर्धारित करें जिसे आप रखना चाहते हैं, और उसे PDF पेज में सम्मिलित करते हुए क्रॉप करें।
- एक ही दस्तावेज़ में अतिरिक्त पेज जोड़ें, जिससे आप कई छवियों से मल्टी‑पेज PDF बना सकें।
- अंतिम फ़ाइल को सहेजें और आउटपुट को सत्यापित करें।  

**Prerequisites:** .NET 6+ (या .NET Framework 4.6+), Visual Studio 2022 या कोई भी एडिटर जो आपको पसंद हो, और `Aspose.Pdf` का NuGet रेफ़रेंस। अन्य कोई बाहरी सेवाएँ आवश्यक नहीं हैं।

![Create PDF from JPG example](image.jpg){: .align-center alt="क्रॉप की गई छवि को PDF पेज पर रखे हुए Create PDF from JPG उदाहरण"}

---

## चरण 1: Aspose.Pdf स्थापित करें और अपने प्रोजेक्ट को तैयार करें

सबसे पहले—Aspose.Pdf पैकेज जोड़ें। अपने सॉल्यूशन फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package Aspose.Pdf
```

यह एकल लाइन वह सब कुछ लाती है जिसकी आपको आवश्यकता है: `Document`, `Rectangle`, और `Page` क्लासेज़ जिन्हें हम बाद में उपयोग करेंगे। मेरे अनुभव में, NuGet तरीका सबसे साफ़ है ताकि आप DLLs के साथ झंझट किए बिना अपडेटेड रह सकें।

> **Pro tip:** यदि आप .NET Framework को टार्गेट कर रहे हैं, तो `Aspose.Pdf.NET` पैकेज का उपयोग करें; API सतह समान है।

## चरण 2: JPEG लोड करें और पेज आकार निर्धारित करें

हमें एक कैनवास चाहिए जो अंतिम PDF पेज के लिए हम चाहते हैं उन आयामों से मेल खाता हो। नीचे दिया गया कोड एक नया `Document` बनाता है और स्रोत छवि को स्ट्रीम के रूप में खोलता है।

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Rectangle क्यों? Aspose.Pdf में `Rectangle` पेज के आयाम और वह छवि क्षेत्र दोनों को दर्शाता है जिसे आप प्रदर्शित करना चाहते हैं। *पेज* को *क्रॉप एरिया* से अलग करके आप PDF में क्या दिखेगा, उस पर सूक्ष्म नियंत्रण प्राप्त करते हैं।

## चरण 3: क्रॉप एरिया चुनें (ऊपरी‑बाएँ क्वार्टर)

मान लीजिए आपको फोटो का केवल ऊपर‑बाएँ क्वार्टर चाहिए। हम उस क्षेत्र की गणना पेज आकार के सापेक्ष करते हैं:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

`Rectangle` कंस्ट्रक्टर **lower‑left X/Y** और **upper‑right X/Y** मान लेता है। `LLY` में आधी ऊँचाई जोड़ने से हम क्रॉप के नीचे को ऊपर की ओर शिफ्ट करते हैं, जिससे प्रभावी रूप से छवि का निचला आधा हट जाता है। यदि आपको अलग भाग चाहिए तो इन गणनाओं को समायोजित करें।

> **Why crop before adding?**  
> PDF पक्ष पर क्रॉप करने से डिस्क पर अस्थायी बिटमैप बनाने से बचा जाता है, जिससे I/O और मेमोरी दोनों बचते हैं। Aspose आपके लिए गणना संभालता है, और परिणाम एक साफ़, वेक्टर‑फ्रेंडली PDF होता है।

## चरण 4: नया पेज जोड़ें और क्रॉप की गई छवि सम्मिलित करें

अब हम वास्तव में छवि को PDF पेज पर रखते हैं। यहीं पर **how to add new pdf page** कीवर्ड चमकता है।

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` तीन आर्ग्यूमेंट लेता है:

1. **Stream** – स्रोत JPEG।  
2. **Page rectangle** – पेज का आकार निर्धारित करता है (हमारा `pageBounds`)।  
3. **Crop rectangle** – Aspose को बताता है कि छवि का कौन सा भाग रेंडर करना है।

यदि आपको अधिक पेज चाहिए, तो बस प्रत्येक बार एक नया `imageStream` के साथ `Add` + `AddImage` पैटर्न दोहराएँ। यह **how to add new pdf page** की आवश्यकता को पूरा करता है जबकि कोड को साफ़ रखता है।

## चरण 5: PDF सहेजें और परिणाम सत्यापित करें

अंतिम चरण एक लाइनर है, लेकिन इसे कम मत आँकिए—सही पाथ पर सहेजने से फ़ाइल किसी भी PDF व्यूअर द्वारा खोली जा सकती है।

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

जब आप `cropped_image.pdf` खोलेंगे, तो आपको एक ही पेज दिखेगा जिसमें मूल JPEG का केवल ऊपर‑बाएँ क्वार्टर होगा, जो 600 × 800 पेज के भीतर पूरी तरह केंद्रित होगा।

## पूर्ण कार्यशील उदाहरण (सभी चरण एक साथ)

नीचे पूरा प्रोग्राम है जिसे आप कॉपी‑पेस्ट करके एक कंसोल ऐप में उपयोग कर सकते हैं। यह जैसा है वैसा ही कंपाइल हो जाएगा, बशर्ते आपने Aspose.Pdf स्थापित किया हो और निर्दिष्ट स्थान पर JPEG रखी हो।

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### अपेक्षित आउटपुट

- **File:** `cropped_image.pdf` (≈ 30 KB)।
- **Content:** एक पेज, 600 × 800 पॉइंट्स, जो `photo.jpg` का ऊपर‑बाएँ क्वार्टर दिखाता है।
- **Behavior:** कोई विकृति नहीं; छवि अपने मूल रिज़ॉल्यूशन को क्रॉप बाउंड्स के भीतर बनाए रखती है।

## अक्सर पूछे जाने वाले प्रश्न और किनारे के मामलों

### अगर मुझे पूरी छवि रखनी हो, न कि केवल एक क्वार्टर?

सिर्फ `cropArea` को `pageBounds` के बराबर सेट करें:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### क्या मैं अलग पेज आकार (जैसे A4) उपयोग कर सकता हूँ?

बिल्कुल। `pageBounds` मानों को A4 पेज के पॉइंट्स में आयाम (595 × 842) से बदलें:

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

क्रॉप रेक्टेंगल वही रह सकता है या नए आस्पेक्ट रेशियो से मेल खाने के लिए पुनः गणना किया जा सकता है।

### मैं कई छवियों को कैसे जोड़ूँ, प्रत्येक अपने पेज पर?

फ़ाइल पाथों के संग्रह पर लूप करें:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### ट्रांसपैरेंसी या PNG छवियों के बारे में क्या?

Aspose.Pdf PNG को JPEG की तरह ही संभालता है। यदि स्रोत में अल्फा चैनल है, तो PDF इसे संरक्षित करेगा, बशर्ते PDF संस्करण ट्रांसपैरेंसी का समर्थन करता हो (डिफ़ॉल्ट ठीक है)।

### क्या यह .NET Core पर Linux में काम करता है?

हां। Aspose.Pdf क्रॉस‑प्लेटफ़ॉर्म है; बस यह सुनिश्चित करें कि `imageStream` लक्ष्य OS पर एक वैध फ़ाइल पाथ की ओर इशारा करता हो। कोई Windows‑विशिष्ट API उपयोग नहीं किया गया है।

## टिप्स और सर्वोत्तम प्रथाएँ

- **Memory Management:** हमेशा `using` स्टेटमेंट्स में स्ट्रीम्स को रैप करें (जैसा दिखाया गया है) ताकि फ़ाइल लॉक न हों।  
- **Performance:** यदि आप दर्जनों छवियों को प्रोसेस कर रहे हैं, तो एक ही `Document` इंस्टेंस को पुन: उपयोग करने और प्रत्येक छवि के लिए `pdfDocument.Pages.Add()` कॉल करने पर विचार करें।  
- **Error Handling:** पूरी रूटीन को `try/catch` ब्लॉक में रैप करें और ट्रबलशूटिंग के लिए `PdfException` को लॉग करें।  
- **Quality Control:** Aspose.Pdf आपको `ImageFragment` के माध्यम से इमेज रिज़ॉल्यूशन सेट करने देता है। हाई‑dpi स्कैन के लिए `ImageFragment.Resolution = 300;` सेट करें।  
- **Security:** यदि PDF को बाहरी रूप से साझा किया जाएगा, तो आप `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);` के साथ एन्क्रिप्शन जोड़ सकते हैं।

## निष्कर्ष

हमने अभी बताया कि C# में **create PDF from JPG** कैसे किया जाता है, **crop image in PDF** कैसे किया जाता है, और मल्टी‑पेज दस्तावेज़ बनाने के लिए **add new PDF page** कैसे जोड़ा जाता है। वही पैटर्न आपको किसी भी स्थिति में **convert JPG to PDF with crop** और **insert image into PDF C#** करने देता है—साधारण रसीदों से लेकर जटिल फोटो‑बुक्स तक।  

इसे आज़माएँ: क्रॉप लॉजिक बदलें, A4 पेजों के साथ प्रयोग करें, या कई छवियों को श्रृंखला में जोड़ें। Aspose.Pdf लाइब्रेरी इन कार्यों को आसान बनाती है, और ऊपर दिया गया कोड एक ठोस, उद्धरण‑योग्य रेफ़रेंस है जिसे आप किसी भी प्रोजेक्ट में पेस्ट कर सकते हैं।  

### आगे क्या?

- **Add text annotations** PDF में जोड़ें (जैसे, प्रत्येक छवि के नीचे कैप्शन)।
- **Create a table of contents** स्वचालित रूप से मल्टी‑पेज PDFs के लिए बनाएँ।
- **Merge multiple PDFs** `pdfDocument.Pages.AddRange(otherDoc.Pages);` का उपयोग करके।

इनमें से प्रत्येक विषय उन मूलभूत बातों पर आधारित है जो आपने अभी सीखी हैं, इसलिए आप इन्हें खोजने के लिए अच्छी तरह तैयार हैं।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}