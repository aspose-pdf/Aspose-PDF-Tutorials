---
category: general
date: 2026-06-21
description: C# के साथ PDF टेक्स्टबॉक्स फ़ील्ड बनाएं और सीखें कि कैसे कुछ ही कोड लाइनों
  में PDF फ़ॉर्म फ़ील्ड को डुप्लिकेट करें या PDF फ़ॉर्म में टेक्स्टबॉक्स जोड़ें।
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: hi
og_description: PDF टेक्स्टबॉक्स फ़ील्ड जल्दी बनाएं। यह गाइड दिखाता है कि कैसे PDF
  फ़ॉर्म फ़ील्ड को डुप्लिकेट करें और आधुनिक C# PDF लाइब्रेरी का उपयोग करके PDF फ़ॉर्म
  में टेक्स्टबॉक्स जोड़ें।
og_title: PDF टेक्स्टबॉक्स फ़ील्ड बनाएं – पूर्ण C# ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: PDF टेक्स्टबॉक्स फ़ील्ड बनाएं – चरण-दर-चरण गाइड
url: /hi/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF टेक्स्टबॉक्स फ़ील्ड बनाएं – पूर्ण C# ट्यूटोरियल

क्या आपको कभी **PDF टेक्स्टबॉक्स फ़ील्ड बनाना** पड़ा है लेकिन आप नहीं जानते थे कि कौन से API कॉल्स इस्तेमाल करें? आप अकेले नहीं हैं। चाहे आप एक कॉन्ट्रैक्ट‑साइनिंग पोर्टल बना रहे हों या एक साधारण डेटा‑कैप्चर शीट, PDF में इंटरैक्टिव टेक्स्ट बॉक्स जोड़ना किसी भी फॉर्म‑ऑटोमेशन डेवलपर के लिए एक मूल कौशल है।  

इस गाइड में हम एक व्यावहारिक उदाहरण के माध्यम से चलेंगे जो न केवल **PDF फ़ॉर्म में टेक्स्टबॉक्स जोड़ता** है, बल्कि यह भी दिखाता है कि **PDF फ़ॉर्म फ़ील्ड को डुप्लिकेट** कैसे किया जाए ताकि वही इनपुट कई पृष्ठों पर दिखाई दे। अंत तक आपके पास एक रन करने योग्य प्रोग्राम होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं।

## आपको क्या चाहिए

- .NET 6.0 या बाद का संस्करण (कोड .NET Core के साथ भी काम करता है)  
- एक आधुनिक C# PDF लाइब्रेरी – नीचे दिया गया स्निपेट **PDFTron SDK** का उपयोग करता है, लेकिन अवधारणाएँ iText 7, PdfSharp, या अन्य लाइब्रेरीज़ में भी लागू होती हैं।  
- Visual Studio 2022 (या कोई भी IDE जो आपको पसंद हो)  

बस इतना ही – कोई अतिरिक्त सर्विस नहीं, कोई अजीब निर्भरताएँ नहीं। यदि आपके पास पहले से ही एक PDF है जिसे आप बढ़ाना चाहते हैं, तो बस कोड को उस पर पॉइंट करें।

---

## चरण 1: प्रोजेक्ट सेट अप करें और SDK इम्पोर्ट करें

First, create a console app:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Add the PDFTron NuGet package:

```bash
dotnet add package PDFTron.NET
```

Now open `Program.cs` and pull in the namespaces we’ll need:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** यदि आप कोई अलग लाइब्रेरी उपयोग कर रहे हैं, तो `using` स्टेटमेंट्स को समकक्ष (जैसे iText 7 के लिए `iText.Kernel.Pdf`) से बदल दें।

## चरण 2: PDF डॉक्यूमेंट और फ़ॉर्म को इनिशियलाइज़ करें

हम एक नई PDF से शुरू करेंगे जिसमें दो पृष्ठ होंगे – मूल टेक्स्टबॉक्स के लिए स्रोत पृष्ठ और डुप्लिकेट के लिए लक्ष्य पृष्ठ।

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

`Form` ऑब्जेक्ट वह जगह है जहाँ सभी इंटरैक्टिव फ़ील्ड रहते हैं। यदि डॉक्यूमेंट में पहले से फ़ॉर्म नहीं था, तो `GetForm()` हमारे लिए एक बनाता है।

## चरण 3: पहले पृष्ठ पर **PDF टेक्स्टबॉक्स फ़ील्ड बनाएं**

अब हमारे ट्यूटोरियल का मुख्य भाग – टेक्स्टबॉक्स फ़ील्ड बनाना। आयत के निर्देशांक पॉइंट्स में व्यक्त किए जाते हैं (1 इंच = 72 पॉइंट)। उदाहरण बॉक्स को पहले पृष्ठ के शीर्ष‑केन्द्र के पास रखता है।

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

हम `Value` को तुरंत सेट क्यों करते हैं? फ़ील्ड को प्री‑पॉप्युलेट करने से उपयोगकर्ताओं को अपेक्षित इनपुट का संकेत मिलता है, और यह भी दर्शाता है कि फ़ील्ड पूरी तरह कार्यात्मक है।

## चरण 4: फ़ील्ड को फ़ॉर्म में जोड़ें – **PDF फ़ॉर्म में टेक्स्टबॉक्स जोड़ें**

अब हम फ़ॉर्म में फ़ील्ड को एक लॉजिकल नाम के साथ रजिस्टर करते हैं। यह नाम वह है जिसे आप बाद में प्रोग्रामेटिकली फ़ील्ड का डेटा पढ़ने या संशोधित करने के लिए रेफ़र करेंगे।

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

एक स्पष्ट नाम (जैसे `"multiBox"`) चुनने से बाद का कोड समझने में आसान हो जाता है, विशेषकर जब आपके पास दर्जनों फ़ील्ड हों।

## चरण 5: दूसरे पृष्ठ पर **PDF फ़ॉर्म फ़ील्ड डुप्लिकेट करें**

एक सामान्य आवश्यकता यह है कि एक ही फ़ील्ड कई पृष्ठों पर दिखे – जैसे “Customer Name” बॉक्स जो हर इनवॉइस पृष्ठ पर आता है। PDFTron हमें विजेट एनोटेशन को क्लोन करने देता है, जो फ़ील्ड का विज़ुअल प्रतिनिधित्व है।

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

क्लोन किया गया विजेट मूल टेक्स्टबॉक्स के समान अंतर्निहित डेटा साझा करता है। जब उपयोगकर्ता एक इंस्टेंस में टाइप करता है, तो दूसरा स्वचालित रूप से अपडेट हो जाता है – यही **डुप्लिकेट PDF फ़ॉर्म फ़ील्ड** का जादू है।

## चरण 6: दस्तावेज़ को सहेजें और साफ़ करें

अंत में, PDF को डिस्क पर लिखें और PDFNet रनटाइम को बंद करें।

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

प्रोग्राम चलाने से दो‑पृष्ठीय PDF (`output.pdf`) बनता है। इसे Adobe Acrobat Reader में खोलें, पृष्ठ 1 पर टेक्स्टबॉक्स पर क्लिक करें, कुछ टाइप करें, फिर पृष्ठ 2 पर स्विच करें – वही टेक्स्ट तुरंत दिखाई देगा। यह एक पूरी तरह कार्यात्मक **create pdf textbox field** उदाहरण है जिसमें डुप्लिकेट फ़ील्ड शामिल है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Expected output:** `output.pdf` नाम की फ़ाइल जिसमें दो पृष्ठ हैं। दोनों पृष्ठ एक ही एडिटेबल टेक्स्टबॉक्स “Sample” लेबल के साथ दिखाते हैं। एक को एडिट करने से दूसरा तुरंत अपडेट हो जाता है।

---

## सामान्य प्रश्न और किनारे के मामलों

### यदि मुझे फ़ील्ड दो पृष्ठों से *अधिक* चाहिए तो क्या करें?

बस प्रत्येक अतिरिक्त पृष्ठ के लिए क्लोन‑एंड‑ऐड स्टेप्स दोहराएँ। अंतर्निहित डेटा ऑब्जेक्ट वही रहता है, इसलिए सभी विजेट्स सिंक्रनाइज़ रहते हैं।

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### मैं उपस्थिति (फ़ॉन्ट, बॉर्डर, बैकग्राउंड) कैसे बदलूँ?

प्रत्येक `Widget` में `SetBorderColor`, `SetBorderWidth`, और `SetBackgroundColor` मेथड होते हैं। आप फ़ॉन्ट और आकार को नियंत्रित करने के लिए डिफ़ॉल्ट अपीयरेंस स्ट्रिंग (`DA`) भी असाइन कर सकते हैं।

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### क्या मैं उपयोगकर्ता द्वारा भरने के बाद फ़ील्ड को रीड‑ओनली बना सकता हूँ?

हाँ। डेटा एकत्र करने के बाद फ़ील्ड पर `ReadOnly` फ़्लैग सेट करें, या अपने वर्कफ़्लो के आधार पर इसे टॉगल करें।

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### उन PDFs के बारे में क्या जो पहले से ही फ़ॉर्म रखते हैं?

यदि डॉक्यूमेंट में पहले से AcroForm है, तो `doc.GetForm()` बस उसे रिटर्न करता है। आप फिर नए फ़ील्ड जोड़ सकते हैं बिना मौजूदा फ़ील्ड को प्रभावित किए। केवल यह ध्यान रखें कि फ़ील्ड नाम यूनिक हों।

---

## वास्तविक‑विश्व प्रोजेक्ट्स के लिए टिप्स

- **Naming convention:** फ़ील्ड नामों के पहले पृष्ठ या सेक्शन का प्रीफ़िक्स रखें (जैसे `invoice_customer_name`) ताकि टकराव न हो।  
- **Validation:** यदि आपको क्लाइंट‑साइड वैलिडेशन चाहिए तो JavaScript एक्शन (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) उपयोग करें।  
- **Performance:** बड़े PDFs के साथ काम करते समय, बैच ऑपरेशन्स से पहले `doc.Lock()` कॉल करें ताकि I/O ओवरहेड कम हो।  
- **Accessibility:** `AlternateName` प्रॉपर्टी सेट करें ताकि स्क्रीन रीडर फ़ील्ड का वर्णन कर सके।

---

## निष्कर्ष

हमने अभी **PDF टेक्स्टबॉक्स फ़ील्ड बनाया**, दिखाया कि **PDF फ़ॉर्म फ़ील्ड को डुप्लिकेट** कैसे किया जाता है, और C# का उपयोग करके **PDF फ़ॉर्म में टेक्स्टबॉक्स जोड़ने** का सबसे सरल तरीका प्रदर्शित किया। पूरा, रन करने योग्य कोड ऊपर दिया गया है, और आप इसे स्टाइलिंग, वैलिडेशन, या अतिरिक्त पृष्ठों के साथ विस्तारित कर सकते हैं।

अगले कदम के लिए तैयार हैं? एक ड्रॉपडाउन (`ChoiceField`) या सिग्नेचर विजेट एम्बेड करने की कोशिश करें, या डेटा एंट्री के बाद फ़ॉर्म को आर्काइविंग के लिए फ्लैटन करने का पता लगाएँ। PDFTron SDK (या कोई भी तुलनीय लाइब्रेरी) आपको बिल्डिंग ब्लॉक्स देती है—आपकी कल्पना अंतिम रूप तय करती है।

यदि आपको कोई समस्या आती है, तो नीचे टिप्पणी छोड़ें या लाइब्रेरी की आधिकारिक डॉक्यूमेंटेशन देखें; वहाँ कई उदाहरण हैं जो यहाँ कवर किए गए विषयों को पूरक करते हैं। हैप्पी कोडिंग, और आपके फ़ॉर्म हमेशा सिंक में रहें!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}