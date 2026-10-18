---
category: general
date: 2026-04-25
description: Aspose.Pdf का उपयोग करके PDFs में बेट्स नंबरिंग जल्दी से जोड़ें। जानें
  कि PDF में पेज नंबर कैसे जोड़ें, फ़ॉन्ट आकार को स्वतः समायोजित करें, और C# में टेक्स्ट
  वॉटरमार्क कैसे जोड़ें।
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: hi
og_description: Aspose.Pdf के साथ PDFs में बेट्स नंबरिंग जोड़ें। यह गाइड दिखाता है
  कि कैसे एक ही चलाने योग्य उदाहरण में PDF में पृष्ठ संख्याएँ जोड़ें, फ़ॉन्ट आकार
  को स्वचालित रूप से समायोजित करें, और टेक्स्ट वॉटरमार्क जोड़ें।
og_title: PDF में Bates नंबरिंग जोड़ें – पूर्ण Aspose.C# ट्यूटोरियल
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose के साथ PDFs में बेट्स नंबरिंग जोड़ें – पूर्ण गाइड
url: /hi/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose के साथ PDFs में Bates नंबरिंग जोड़ें – पूर्ण गाइड

क्या आपको कभी **PDF में bates numbering** जोड़नी पड़ी लेकिन शुरुआत नहीं पता थी? आप अकेले नहीं हैं—कानूनी टीमें, ऑडिटर्स और डेवलपर्स रोज़ इस समस्या का सामना करते हैं। अच्छी खबर? Aspose.Pdf for .NET के साथ आप एक Bates नंबर स्टैम्प कर सकते हैं, फ़ॉन्ट आकार को ऑटो‑एडजस्ट कर सकते हैं, और यहाँ तक कि स्टैम्प को एक सूक्ष्म टेक्स्ट वॉटरमार्क के रूप में भी उपयोग कर सकते हैं—सिर्फ कुछ ही C# लाइनों में।

इस ट्यूटोरियल में हम **add page numbers pdf** करने के सटीक चरणों को देखेंगे, फ़ॉन्ट को इस तरह ट्यून करेंगे कि वह कभी ओवरफ़्लो न हो, और “how to add bates” सवाल का हमेशा के लिए जवाब देंगे। अंत तक आपके पास एक तैयार‑चलाने‑योग्य कंसोल ऐप होगा जो प्रोफ़ेशनली नंबर किया हुआ PDF बनाता है, और आप देखेंगे कि इसे कैसे एक पूर्ण‑वॉटरमार्क समाधान में विस्तारित किया जा सकता है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* **Aspose.Pdf for .NET** (अप्रैल 2026 तक का नवीनतम NuGet पैकेज)।  
* .NET 6.0 SDK या नया – API .NET Framework पर भी समान रूप से काम करता है, लेकिन .NET 6 बेहतर प्रदर्शन देता है।  
* एक सैंपल PDF जिसका नाम `input.pdf` है और जिसे आप रेफ़रेंस कर सकें (जैसे, `C:\Docs\`)।  

कोई अतिरिक्त कॉन्फ़िगरेशन आवश्यक नहीं; लाइब्रेरी स्वयं‑समाहित है।

---

## Step 1 – Load the Source PDF Document

सबसे पहले हम उस फ़ाइल को खोलते हैं जिसे हम नंबर करना चाहते हैं। Aspose की `Document` क्लास पूरे PDF का प्रतिनिधित्व करती है, और इसे लोड करना इतना सरल है कि कंस्ट्रक्टर में पाथ पास कर दें।

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Why this matters*: डॉक्यूमेंट लोड करने से आपको `Pages` कलेक्शन तक पहुंच मिलती है, जहाँ हम बाद में Bates स्टैम्प जोड़ेंगे। यदि फ़ाइल नहीं मिलती, तो Aspose स्पष्ट `FileNotFoundException` फेंकेगा, जिससे आपको तुरंत पता चल जाएगा कि क्या गड़बड़ है।

---

## Step 2 – Create a Text Stamp for Bates Numbers

अब हम वह विज़ुअल एलिमेंट बनाते हैं जो हर पेज पर दिखेगा। `TextStamp` क्लास आपको कोई भी स्ट्रिंग एम्बेड करने देती है, और हम प्लेसहोल्डर `{page}-{total}` का उपयोग करेंगे ताकि Aspose उन टोकन को स्वचालित रूप से बदल दे।

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Key points*:

* **auto adjust font size** – `AutoAdjustFontSizeToFitStampRectangle` को `true` सेट करने से टेक्स्ट कभी भी रेक्टैंगल के बाहर नहीं निकलता, जो वैरिएबल‑लेन्थ पेज नंबरों के लिए एकदम सही है।  
* **add text watermark** – `Opacity` को कम करके हम Bates नंबर को एक हल्के वॉटरमार्क में बदल देते हैं, जिससे “add text watermark” की आवश्यकता बिना अतिरिक्त कदम के पूरी होती है।  
* **how to add bates** – `{page}` और `{total}` टोकन ही गुप्त मसाला हैं; Aspose रनटाइम पर इन्हें बदल देता है, इसलिए आपको खुद कुछ भी गणना करने की ज़रूरत नहीं।  

---

## Step 3 – Apply the Stamp to Every Page

एक आम गलती यह है कि केवल पहले पेज पर ही स्टैम्प लगाया जाए। वास्तव में **add page numbers pdf** करने के लिए हमें पूरे `Pages` कलेक्शन पर लूप करना होगा।

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

क्लोन क्यों? `AddStamp` मेथड अंदरूनी तौर पर एक कॉपी बनाता है, लेकिन प्रत्येक इटरेशन में एक नया इंस्टेंस स्पष्ट रूप से उपयोग करने से अनजाने साइड‑इफ़ेक्ट्स से बचा जा सकता है, जैसे कि बाद में स्टैम्प प्रॉपर्टीज़ (जैसे रंग बदलना) बदलना।

---

## Step 4 – Save the Updated PDF

स्टैम्प लग जाने के बाद, बदलावों को सहेजना सीधा‑सरल है। आप मूल फ़ाइल को ओवरराइट कर सकते हैं या नई लोकेशन पर लिख सकते हैं—यहाँ हम `output.pdf` नाम की नई फ़ाइल सहेजेंगे।

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

यदि आप `output.pdf` खोलेंगे तो प्रत्येक पेज पर “Bates: 1‑10”, “Bates: 2‑10”, … नीचे‑दाएँ कोने में दिखेगा, हल्की अपारदर्शिता के साथ जो **add text watermark** भी बन जाता है।

---

## Full Working Example

सब कुछ मिलाकर, यहाँ एक एकल, स्वयं‑समाहित कंसोल प्रोग्राम है जिसे आप Visual Studio में कॉपी‑पेस्ट कर सकते हैं।

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Expected result**: किसी भी व्यूअर में `output.pdf` खोलें; प्रत्येक पेज पर निचले‑दाएँ कोने में “Bates: 3‑12” जैसी लाइन दिखेगी, रेक्टैंगल के लिए बिल्कुल सही आकार की, और 40 % अपारदर्शिता के साथ रेंडर होगी। यह कानूनी‑ट्रैकिंग आवश्यकता और विज़ुअल वॉटरमार्क दोनों को पूरा करता है।

---

## Common Variations & Edge Cases

| Situation | What to change | Why |
|-----------|----------------|-----|
| **Different placement** | `HorizontalAlignment` / `VerticalAlignment` को समायोजित करें या `XIndent`/`YIndent` सेट करें | कुछ फर्में टॉप‑लेफ़्ट या सेंटर प्लेसमेंट पसंद करती हैं। |
| **Custom prefix** | `"Bates: "` को `"Doc‑ID: "` या किसी भी स्ट्रिंग से बदलें | आप अलग नामकरण नियम उपयोग कर रहे हो सकते हैं। |
| **Multiple stamps** | दूसरा `TextStamp` बनाएं (जैसे, गोपनीयता नोटिस) और पहले के बाद जोड़ें | **add bates numbering** को अन्य **add text watermark** आवश्यकताओं के साथ मिलाना आसान है। |
| **Large page counts** | प्रारंभिक फ़ॉन्ट आकार बढ़ाएँ (जैसे, `14`) – ऑटो‑एडजस्ट आवश्यकता पड़ने पर इसे छोटा कर देगा | जब आपके पास > 999 पेज हों तो स्ट्रिंग लंबी हो जाती है; ऑटो‑एडजस्ट क्लिपिंग रोकता है। |
| **Encrypted PDFs** | स्टैम्प लगाने से पहले `pdfDocument.Decrypt("password")` कॉल करें | पासवर्ड के बिना सुरक्षित फ़ाइल को मॉडिफ़ाई नहीं किया जा सकता। |

---

## Pro Tips & Pitfalls

* **Pro tip:** यदि टेक्स्ट पेज के किनारे से चिपका हुआ दिखे तो `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` सेट करें।  
* **Watch out for:** बहुत छोटे रेक्टैंगल (डिफ़ॉल्ट आकार 100 × 30 pt)। यदि आपको बड़ा एरिया चाहिए तो `batesStamp.Width` और `batesStamp.Height` मैन्युअली सेट करें।  
* **Performance note:** हजारों पेजों पर स्टैम्प लगाना कुछ सेकंड ले सकता है, लेकिन Aspose पेजों को प्रभावी रूप से स्ट्रीम करता है—पूरे डॉक्यूमेंट को मेमोरी में लोड करने की ज़रूरत नहीं।  

---

## Conclusion

हमने दिखाया कि कैसे Aspose.Pdf का उपयोग करके **add bates numbering** को PDF में लागू किया जाए, साथ ही **add page numbers pdf**, **auto adjust font size**, और **add text watermark** को एक ही प्रवाह में किया जाए। ऊपर दिया गया पूर्ण, चलाने योग्य उदाहरण आपको किसी भी कानूनी‑डॉक्यूमेंट वर्कफ़्लो या आंतरिक रिपोर्टिंग सिस्टम के लिए एक ठोस आधार देता है।

अगला कदम? इस एप्रोच को Aspose की PDF मर्जिंग API के साथ जोड़ें ताकि कई फ़ाइलों को बैच‑प्रोसेस किया जा सके, या `TextFragment` क्लास को एक्सप्लोर करें अधिक समृद्ध वॉटरमार्क (रंगीन, घुमाया हुआ, या मल्टी‑लाइन) के लिए। संभावनाएँ अनंत हैं, और अब आपके पास जो कोड है वह एक भरोसेमंद बेसलाइन है।

यदि यह गाइड आपके काम आया, तो टिप्पणी छोड़ें, रिपॉज़िटरी को स्टार दें, या अपनी खुद की वैरिएशन शेयर करें। Happy coding, और आपके PDFs हमेशा परफेक्टली नंबर किए रहें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}