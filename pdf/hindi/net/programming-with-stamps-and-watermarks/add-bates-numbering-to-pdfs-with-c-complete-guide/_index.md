---
category: general
date: 2026-04-10
description: C# के साथ मिनटों में PDFs में Bates नंबरिंग जोड़ें। कस्टम पेज नंबर कैसे
  जोड़ें, PDF फ़ाइलों को कैसे नंबर करें, और Bates नंबरिंग को प्रभावी ढंग से लागू करना
  सीखें।
draft: false
keywords:
- add bates numbering
- add custom page numbers
- how to number pdf
- how to add bates
- apply bates numbering
language: hi
og_description: C# के साथ मिनटों में PDFs में Bates नंबरिंग जोड़ें। यह गाइड दिखाता
  है कि कैसे कस्टम पेज नंबर जोड़ें, PDF फ़ाइलों को नंबर करें, और चरण‑दर‑चरण Bates
  नंबरिंग लागू करें।
og_title: C# के साथ PDFs में बेट्स नंबरिंग जोड़ें – पूर्ण गाइड
tags:
- PDF
- C#
- Bates numbering
title: C# के साथ PDFs में बेट्स नंबरिंग जोड़ें – पूर्ण गाइड
url: /hi/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ PDFs में Bates नंबरिंग जोड़ें – पूर्ण गाइड

क्या आपको कभी PDF में **add bates numbering** जोड़ने की जरूरत पड़ी लेकिन शुरुआत नहीं पता थी? आप अकेले नहीं हैं—कानूनी टीमें, ऑडिटर, और बड़े दस्तावेज़ सेट संभालने वाले सभी को अक्सर यह समस्या आती है। अच्छी खबर? कुछ ही C# लाइनों से आप प्रत्येक पृष्ठ पर एक कस्टम पहचानकर्ता के साथ स्वचालित रूप से स्टैम्प लगा सकते हैं, और आप रास्ते में **how to add custom page numbers** भी सीखेंगे।

इस ट्यूटोरियल में हम आपको वह सब कुछ दिखाएंगे जिसकी आपको जरूरत है: आवश्यक NuGet पैकेज, नंबरिंग विकल्पों को कॉन्फ़िगर करना, नंबर लागू करना, और परिणाम की पुष्टि करना। अंत तक आप प्रोग्रामेटिक रूप से **how to number PDF** फ़ाइलों को नंबर करने के बारे में जान जाएंगे, और आप प्रीफ़िक्स, सफ़िक्स, फ़ॉन्ट साइज को बदलने या यहाँ तक कि विशिष्ट पृष्ठों को लक्षित करने के लिए तैयार होंगे।

## आवश्यकताएँ

- .NET 6.0 या बाद का (कोड .NET Framework 4.7+ के साथ भी काम करता है)
- Visual Studio 2022 (या कोई भी IDE जो आप पसंद करते हैं)
- **Aspose.PDF for .NET** लाइब्रेरी (शिक्षा के लिए फ्री ट्रायल काम करता है)
- `source.pdf` नामक एक सैंपल PDF जिसे आप नियंत्रित फ़ोल्डर में रखें

यदि आपने ये सभी बिंदु पूरे कर लिए हैं, तो चलिए शुरू करते हैं।

## चरण 1: Aspose.PDF स्थापित करें और रेफ़रेंस जोड़ें

पहले, अपने प्रोजेक्ट में Aspose.PDF पैकेज जोड़ें:

```bash
dotnet add package Aspose.PDF
```

या NuGet पैकेज मैनेजर UI का उपयोग करें। इंस्टॉल होने के बाद, अपने फ़ाइल के शीर्ष पर नेमस्पेस शामिल करें:

```csharp
using Aspose.Pdf;
```

> **Pro tip:** अपने पैकेजों को अद्यतित रखें; नवीनतम संस्करण (अप्रैल 2026 तक) बड़े दस्तावेज़ों के लिए कई प्रदर्शन सुधार जोड़ता है।

## चरण 2: स्रोत PDF दस्तावेज़ खोलें

फ़ाइल खोलना सरल है। हम एक `using` ब्लॉक का उपयोग करेंगे ताकि फ़ाइल हैंडल स्वचालित रूप से रिलीज़ हो जाए।

```csharp
// Step 2: Open the source PDF document
using (var sourceDocument = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

`Document` क्लास पूरे PDF का प्रतिनिधित्व करता है, जिससे हमें पृष्ठों, एनोटेशन, और बेशक Bates नंबरिंग तक पहुँच मिलती है।

## चरण 3: Bates नंबरिंग सेटिंग्स परिभाषित करें

अब बात का मुख्य भाग—**add bates numbering** विकल्पों को कॉन्फ़िगर करना। आप प्रारंभिक संख्या, प्रीफ़िक्स, सफ़िक्स, फ़ॉन्ट साइज, मार्जिन, और यहाँ तक कि कौन से पृष्ठ स्टैम्प प्राप्त करेंगे, को नियंत्रित कर सकते हैं।

```csharp
// Step 3: Define Bates numbering settings
var batesOptions = new BatesNumberingOptions
{
    StartNumber = 1,                 // First number in the sequence
    Prefix = "ABC-",                 // Text before the number
    Suffix = "-2024",                // Text after the number
    FontSize = 12,                   // Size of the numbering font
    Margin = 10,                     // Distance from the page edge (points)
    PageNumbers = new[] { 1, 2, 3 }  // Pages to which numbering is applied
};
```

### ये सेटिंग्स क्यों महत्वपूर्ण हैं

- **StartNumber** आपको पिछले बैच से क्रम जारी रखने देता है।
- **Prefix/Suffix** केस पहचानकर्ता या वर्ष स्टैम्प के लिए उपयोगी होते हैं।
- **FontSize** और **Margin** पठनीयता को प्रभावित करते हैं; बहुत छोटा फ़ॉन्ट प्रिंट में छूट सकता है।
- **PageNumbers** वह जगह है जहाँ आप **apply bates numbering** चयनात्मक रूप से करते हैं। इस एरे को छोड़ दें ताकि हर पृष्ठ को नंबर किया जाए।

यदि आपको क्रमिक नहीं होने वाले **add custom page numbers** की आवश्यकता है, तो आप `{5, 10, 15}` जैसी सूची बना सकते हैं और इसे यहाँ पास कर सकते हैं।

## चरण 4: चयनित पृष्ठों पर Bates नंबरिंग लागू करें

विकल्प तैयार होने के बाद, लाइब्रेरी भारी काम करती है। `AddBatesNumbering` मेथड प्रत्येक लक्ष्य पृष्ठ पर स्टैम्प डालता है।

```csharp
// Step 4: Apply the Bates numbering to the selected pages
sourceDocument.AddBatesNumbering(batesOptions);
```

पर्दे के पीछे, Aspose.PDF प्रत्येक पृष्ठ के लिए एक टेक्स्ट फ्रैगमेंट बनाता है, इसे मार्जिन के अनुसार स्थित करता है, और चुने हुए फ़ॉन्ट साइज का सम्मान करता है। यह सुनिश्चित करता है कि नंबर ठीक उसी जगह दिखें जहाँ आप उम्मीद करते हैं, चाहे आप PDF स्क्रीन पर देखें या प्रिंट करें।

## चरण 5: संशोधित दस्तावेज़ को सहेजें

अंत में, बदलावों को नई फ़ाइल में सहेजें ताकि आपका मूल फ़ाइल अपरिवर्तित रहे।

```csharp
// Step 5: Save the modified document with Bates numbers
sourceDocument.Save("YOUR_DIRECTORY/bates.pdf");
```

अब आपके पास `bates.pdf` है जिसमें स्टैम्प किए गए पृष्ठ हैं। इसे किसी भी PDF व्यूअर में खोलें और आपको कुछ इस तरह दिखेगा:

```
ABC-1-2024   (on page 1, top‑right)
ABC-2-2024   (on page 2, top‑right)
ABC-3-2024   (on page 3, top‑right)
```

### परिणाम की पुष्टि

एक त्वरित सत्यापन के लिए प्रोग्रामेटिक रूप से पहले पृष्ठ का टेक्स्ट पढ़ें:

```csharp
using (var doc = new Document("YOUR_DIRECTORY/bates.pdf"))
{
    var text = doc.Pages[1].ExtractText();
    Console.WriteLine(text.Contains("ABC-1-2024") ? "Bates number applied!" : "Oops, something went wrong.");
}
```

यदि कंसोल पर *Bates number applied!* प्रिंट होता है, तो आप सफल हैं।

## किनारे के मामलों और सामान्य विविधताएँ

| स्थिति | क्या बदलें | कारण |
|-----------|----------------|--------|
| **हर पृष्ठ को नंबर करें** | Omit `PageNumbers` or set it to `null` | The API defaults to all pages when the array isn’t supplied. |
| **प्रति पक्ष अलग मार्जिन** | Use `Margin = new MarginInfo { Top = 15, Right = 10 }` (requires Aspose > 23.3) | Gives you fine‑grained control over placement. |
| **बड़े दस्तावेज़ (> 500 पृष्ठ)** | Enable `batesOptions.StartNumber` at a higher value and consider `batesOptions.FontSize = 10` to avoid overlap | Keeps the stamp readable without crowding the page |
| **विभिन्न फ़ॉन्ट चाहिए** | Set `batesOptions.Font = FontRepository.FindFont("Arial")` | Some legal firms require a specific typeface. |

> **Watch out:** यदि आप कोई ऐसा पृष्ठ संख्या प्रदान करते हैं जो मौजूद नहीं है (उदाहरण के लिए, `PageNumbers = new[] { 999 }`), तो Aspose.PDF चुपचाप उसे छोड़ देता है। यदि आप सूची को गतिशील रूप से बनाते हैं तो हमेशा रेंज को वैध करें।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, तैयार‑चलाने वाला प्रोग्राम है। इसे एक कंसोल ऐप में पेस्ट करें, पाथ्स को समायोजित करें, और **F5** दबाएँ।

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        // Open the source PDF
        using (var sourceDocument = new Document(sourcePath))
        {
            // Configure Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1,
                Prefix = "ABC-",
                Suffix = "-2024",
                FontSize = 12,
                Margin = 10,
                PageNumbers = new[] { 1, 2, 3 } // Change or remove to number all pages
            };

            // Apply the numbering
            sourceDocument.AddBatesNumbering(batesOptions);

            // Save the new PDF
            sourceDocument.Save(outputPath);
        }

        // Verify the first page contains the expected stamp
        using (var doc = new Document(outputPath))
        {
            string extracted = doc.Pages[1].ExtractText();
            bool success = extracted.Contains("ABC-1-2024");
            Console.WriteLine(success
                ? "Bates numbering added successfully!"
                : "Numbering failed – check your options.");
        }
    }
}
```

इस कोड को चलाने से `bates.pdf` उत्पन्न होगा जिसमें पहले दिखाए गए तीन स्टैम्प किए गए पृष्ठ होंगे। फ़ाइल खोलें, और आपको नंबर दाएँ संरेखित, किनारे से 10 पॉइंट, 12‑पॉइंट फ़ॉन्ट में दिखेंगे।

## दृश्य पूर्वावलोकन

![add bates numbering preview](/images/bates-numbering-sample.png)

*ऊपर का स्क्रीनशॉट दिखाता है कि स्क्रिप्ट चलाने के बाद **add bates numbering** आउटपुट कैसे दिखता है।*

## निष्कर्ष

हमने अभी-अभी C# का उपयोग करके PDF में **add bates numbering** कैसे किया, यह कवर किया है। `BatesNumberingOptions` को कॉन्फ़िगर करके, स्टैम्प लागू करके, और दस्तावेज़ को सहेजकर, आपके पास एक दोहराने योग्य समाधान है जो **add custom page numbers**, **how to number pdf** फ़ाइलों, और किसी भी प्रोजेक्ट में **apply bates numbering** भी कर सकता है।

अगले कदम? इसे एक बैच प्रोसेसर के साथ मिलाएँ जो PDFs के फ़ोल्डर को पार करता है, या प्रत्येक केस प्रकार के लिए अलग-अलग प्रीफ़िक्स के साथ प्रयोग करें। आप नंबरिंग के बाद कई PDFs को मर्ज करने का भी पता लगा सकते हैं—सम्पूर्ण केस बंडल बनाने के लिए उपयोगी।

किनारे के मामलों के बारे में प्रश्न हैं, या हेडर के बजाय फुटर में नंबर एम्बेड करना चाहते हैं? टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}