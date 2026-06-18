---
category: general
date: 2026-04-25
description: C# में संग्रह को तेज़ी से इटरेट करें, स्पष्ट foreach लूप उदाहरण के साथ।
  कुछ ही चरणों में ऑब्जेक्ट नाम प्राप्त करना और स्ट्रिंग सूची प्रदर्शित करना सीखें।
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: hi
og_description: C# में foreach लूप का उपयोग करके कलेक्शन को इटररेट करने का उदाहरण।
  जानिए कैसे ऑब्जेक्ट नाम प्राप्त करें और स्ट्रिंग सूची को कुशलतापूर्वक प्रदर्शित
  करें।
og_title: C# में संग्रह को दोहराएँ – चरण‑दर‑चरण वस्तुओं पर लूप
tags:
- C#
- collections
- loops
title: C# में कलेक्शन को इटरेट करें – आइटम्स पर लूप करने के लिए सरल गाइड
url: /hi/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इटेरेट कलेक्शन C# – फ़ोरइच लूप उदाहरण के साथ आइटम्स पर कैसे लूप करें

क्या आपको कभी **iterate collection C#** करने की ज़रूरत पड़ी है लेकिन आप सुनिश्चित नहीं थे कि कौन सा निर्माण सबसे साफ़ कोड देता है? आप अकेले नहीं हैं। कई प्रोजेक्ट्स में हम केवल कुछ स्ट्रिंग्स प्रिंट करने के लिए लंबी `for` लूप लिखते हैं—समय और पठनीयता बर्बाद होती है। अच्छी खबर? एक ही `foreach` लूप एक ऑब्जेक्ट से हर नाम निकाल सकता है और **display string list** को सेकंडों में दिखा सकता है।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे जो दिखाता है कि कैसे **get object names** प्राप्त करें, आइटम्स पर लूप करें, और उन्हें कंसोल में आउटपुट करें। अंत तक आपके पास एक स्वयं‑समाहित स्निपेट होगा जिसे आप किसी भी .NET 6+ कंसोल ऐप में डाल सकते हैं, साथ ही किनारे के मामलों और प्रदर्शन के लिए कुछ टिप्स भी।

> **Pro tip:** यदि आप बड़े कलेक्शन्स के साथ काम कर रहे हैं, तो `Parallel.ForEach` का उपयोग करने पर विचार करें—लेकिन यह एक अलग दिन का विषय है।

---

## आप क्या सीखेंगे

- एक ऑब्जेक्ट से नामों का कलेक्शन कैसे प्राप्त करें (`GetSignatureNames` हमारे उदाहरण में)
- **foreach loop example** की सिंटैक्स और बारीकियों को C# में
- कंसोल में **display string list** दिखाने के तरीके, फ़ॉर्मेटिंग ट्रिक्स सहित
- आइटम्स पर लूप करते समय सामान्य pitfalls (null कलेक्शन, खाली परिणाम)
- एक पूर्ण, कॉपी‑पेस्ट तैयार प्रोग्राम जिसे आप तुरंत चला सकते हैं

कोई बाहरी लाइब्रेरी आवश्यक नहीं है; केवल .NET के साथ आने वाली बेस क्लास लाइब्रेरी। यदि आपके पास .NET SDK इंस्टॉल है, तो आप तैयार हैं।

![Iterate collection C# diagram showing a list flowing into a foreach loop and then to the console](/images/iterate-collection-csharp.png "iterate collection c# diagram")

---

## चरण 1: सैंपल ऑब्जेक्ट सेट अप करें

सबसे पहले—हमें एक ऐसा ऑब्जेक्ट चाहिए जो नामों का कलेक्शन रिटर्न कर सके। कल्पना करें कि आपके पास एक `Signature` क्लास है जो कई सिग्नेचर रखता है; प्रत्येक सिग्नेचर की एक `Name` प्रॉपर्टी होती है। मेथड `GetSignatureNames` बस उन नामों को `IEnumerable<string>` में निकालता है।

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Why this matters:** `IEnumerable<string>` रिटर्न करके हम मेथड को लचीला रखते हैं—कॉलर्स बिना मूल सूची को कॉपी किए एने्यूमरेट, क्वेरी या परिणाम को कन्वर्ट कर सकते हैं। यह बाद में **loop over items** को आसान बनाता है।

---

## चरण 2: स्ट्रिंग लिस्ट दिखाने के लिए फ़ोरइच लूप लिखें

अब जब हमारे पास नामों का स्रोत है, चलिए वास्तव में **iterate collection C#** करते हैं। `foreach` कंस्ट्रक्ट स्वचालित रूप से एने्यूमेरेबल से प्रत्येक एलिमेंट निकालता है, इसलिए हमें इंडेक्स वेरिएबल मैनेज करने की जरूरत नहीं है।

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**कोड की व्याख्या:**

1. **Instantiate** `Signature` – अब आपके पास एक ऑब्जेक्ट है जो अपने नामों को जानता है।
2. **Retrieve** कलेक्शन `GetSignatureNames()` के माध्यम से – यह **get object names** चरण है।
3. **Foreach loop example** – `foreach (var name in signatureNames)` स्वचालित रूप से प्रत्येक स्ट्रिंग पर इटररेट करता है।
4. **Display** प्रत्येक `name` को `Console.WriteLine` से – कंसोल ऐप में **display string list** करने का क्लासिक तरीका।

क्योंकि `signatureNames` `IEnumerable<string>` को इम्प्लीमेंट करता है, `foreach` लूप बॉक्स से बाहर काम करता है, एने्यूरेटर को पीछे से संभालता है। ऑफ‑बाय‑वन एरर या मैन्युअल बाउंड्स चेकिंग की चिंता नहीं करनी पड़ती।

---

## चरण 3: प्रोग्राम चलाएँ और आउटपुट सत्यापित करें

प्रोग्राम को कंपाइल और एक्सीक्यूट करें (उदा., प्रोजेक्ट फ़ोल्डर से `dotnet run`)। आपको यह दिखना चाहिए:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

यदि कुछ भी प्रिंट नहीं होता, तो दोबारा जांचें कि `GetSignatureNames` `null` तो नहीं रिटर्न कर रहा। एक त्वरित डिफेन्सिव गार्ड आपके सिरदर्द को बचा सकता है:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

अब लूप एक गायब कलेक्शन को सुगमता से संभालेगा और `NullReferenceException` फेंके बिना बस कुछ नहीं आउटपुट करेगा।

---

## चरण 4: सामान्य वैरिएशन और एज केस

### 4.1 जटिल ऑब्जेक्ट्स की सूची पर लूपिंग

अक्सर आप साधारण स्ट्रिंग्स के साथ नहीं, बल्कि कई प्रॉपर्टीज़ वाले ऑब्जेक्ट्स के साथ काम करेंगे। ऐसे में आप अभी भी **loop over items** कर सकते हैं और तय कर सकते हैं कि क्या दिखाना है:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

यहाँ हम स्ट्रिंग इंटरपोलेशन का उपयोग करके फ़ील्ड्स को जोड़ते हैं—यह अभी भी `foreach` लूप है, बस अधिक समृद्ध आउटपुट के साथ।

### 4.2 `break` के साथ जल्दी बाहर निकलना

यदि आपको केवल पहला मिलता-जुलता नाम चाहिए, तो लूप से `break` कर दें:

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 पैरेलल एने्यूमरेशन (एडवांस्ड)

जब कलेक्शन बहुत बड़ा हो और प्रत्येक इटरेशन CPU‑इंटेंसिव हो, तो `Parallel.ForEach` चीज़ों को तेज़ कर सकता है:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

याद रखें, `Console.WriteLine` स्वयं थ्रेड‑सेफ़ है लेकिन आउटपुट क्रम अनिश्चित रहेगा।

---

## चरण 5: साफ़ और मेंटेनेबल लूप्स के टिप्स

- जब आपको इंडेक्स की ज़रूरत नहीं होती, तो **`foreach` को `for` पर प्राथमिकता दें**; यह ऑफ‑बाय‑वन बग्स को कम करता है।
- मेथड सिग्नेचर में **`IEnumerable<T>` का उपयोग करें** ताकि API लचीला रहे।
- नल कलेक्शन्स के खिलाफ **null‑कोएलिसिंग ऑपरेटर (`??`)** से गार्ड रखें।
- लूप बॉडी को छोटा रखें—यदि आप कई लाइन्स लिख रहे हैं, तो एक मेथड निकालें।
- इटररेट करते समय कलेक्शन को संशोधित करने से **बचें**; यह `InvalidOperationException` फेंकेगा।

---

## निष्कर्ष

हमने अभी-अभी दिखाया कि कैसे **iterate collection C#** को एक साफ़ **foreach loop example** का उपयोग करके किया जाए, **object names** प्राप्त करें, और कंसोल में **display string list** करें। पूरा प्रोग्राम—ऑब्जेक्ट डिफिनिशन, रिट्रीवल, और इटरेशन—जैसा है वैसा चलाता है, जिससे आपको किसी भी स्थिति में जहाँ आपको आइटम्स पर लूप करना हो, एक ठोस आधार मिलता है।

अब आप आगे खोज सकते हैं:

- लूपिंग से पहले LINQ के साथ फ़िल्टरिंग (`signatureNames.Where(n => n.Contains("a"))`)
- कंसोल की बजाय आउटपुट को फ़ाइल में लिखना
- असिंक्रोनस स्ट्रीम्स के लिए `IAsyncEnumerable<T>` का उपयोग

इनको आज़माएँ, और आप देखेंगे कि `foreach` कंस्ट्रक्ट कितना बहुमुखी है। एज केस या प्रदर्शन के बारे में सवाल हैं? नीचे टिप्पणी छोड़ें, और खुशहाल कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}