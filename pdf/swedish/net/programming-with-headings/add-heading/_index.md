---
title: Lägg till rubrik, språk och titel i en PDF med Aspose.PDF for .NET
weight: 110
limit:
description: Skapa en PDF, ange dess språk och titel samt lägg till en rubrik på nivå 1 med Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Skapa en PDF, ange dess språk och titel samt lägg till en rubrik på
    nivå 1 med Aspose.PDF for .NET.
  headline: Lägg till rubrik, språk och titel i en PDF med Aspose.PDF for .NET
  type: TechArticle
- description: Skapa en PDF, ange dess språk och titel samt lägg till en rubrik på
    nivå 1 med Aspose.PDF for .NET.
  name: Lägg till rubrik, språk och titel i en PDF med Aspose.PDF for .NET
  steps:
  - name: Ange filnamnet för den genererade PDF‑filen.
    text: Ange filnamnet för den genererade PDF‑filen.
  - name: Skapa en ny tom PDF‑dokumentinstans (`pdfDoc`) inom ett `using`‑block.
    text: Skapa en ny tom PDF‑dokumentinstans (`pdfDoc`) inom ett `using`‑block.
  - name: Hämta `ITaggedContent`‑gränssnittet för att arbeta med taggade PDF‑strukturer.
    text: Hämta `ITaggedContent`‑gränssnittet för att arbeta med taggade PDF‑strukturer.
  - name: Ställ in dokumentets standardspråk till English (US) och tilldela en titelmetadata.
    text: Ställ in dokumentets standardspråk till English (US) och tilldela en titelmetadata.
  - name: Hämta rot‑elementet i det logiska strukturträdet.
    text: Hämta rot‑elementet i det logiska strukturträdet.
  - name: Skapa ett rubrik‑element på nivå 1, ange dess visade text och specificera
      dess språk.
    text: Skapa ett rubrik‑element på nivå 1, ange dess visade text och specificera
      dess språk.
  - name: Lägg till rubrik‑elementet i roten, vilket får rubriken att visas i PDF‑filen.
    text: Lägg till rubrik‑elementet i roten, vilket får rubriken att visas i PDF‑filen.
  - name: Spara PDF‑filen till den angivna filen och stäng dokumentets omfattning.
    text: Spara PDF‑filen till den angivna filen och stäng dokumentets omfattning.
  - name: Skriv ut ett bekräftelsemeddelande till konsolen.
    text: Skriv ut ett bekräftelsemeddelande till konsolen.
  type: HowTo
- questions:
  - answer: '`SetLanguage` definierar standardspråket för hela dokumentets logiska
      struktur; alla element som inte har ett eget språk angivet kommer att ärva "en-US".'
    question: Vilken effekt har anropet `tagContent.SetLanguage("en-US")` på PDF‑filen?
  - answer: Att sätta `header.Language` är valfritt; rubriken kommer att ärva dokumentets
      standardspråk om du inte tilldelar ett annat värde, som visas i exemplet.
    question: Behöver jag sätta `header.Language` om jag redan har anropat `SetLanguage`
      på dokumentet?
  - answer: Använd `tagContent.CreateHeaderElement(2)` för att skapa en rubrik på
      nivå 2; det numeriska argumentet anger rubriknivån som kommer att återspeglas
      i PDF‑filens strukturträd.
    question: Hur kan jag skapa en rubrik på nivå 2 istället för en rubrik på nivå 1?
  - answer: '`SetTitle` skriver den angivna strängen till PDF‑filens dokumentmetadata‑titelfält,
      vilket kan visas i PDF‑läsare och användas för sökning eller indexering.'
    question: Vad gör `tagContent.SetTitle("PDF Example with Header")`?
  - answer: Rubrik‑elementet kommer inte att läggas till i det logiska strukturträdet,
      så det visas inte i PDF‑utdata och känns inte igen som en rubrik av tillgänglighetsverktyg.
    question: Vad händer om jag utelämnar `rootElement.AppendChild(header)`?
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: Infoga en rubrik och ange språk i en PDF
og_description: Lär dig att skapa en PDF, ange dess språk och titel och sedan lägga till en rubrik på nivå 1 med några rader .NET‑kod.
og_image_alt: Guide som visar hur man lägger till en rubrik, anger språk och titel i en PDF med Aspose.PDF for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till rubrik, språk och titel i en PDF med Aspose.PDF
Den här handledningen guidar dig genom att skapa ett nytt PDF‑dokument med Aspose.PDF for .NET, tilldela ett standardspråk och en dokumenttitel samt infoga en rubrik på nivå 1. Du får se hur du arbetar med klasserna Document, ITaggedContent, StructureElement och HeaderElement för att producera en korrekt taggad PDF som är lämplig för tillgänglighetsverktyg.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Vilken effekt har anropet `tagContent.SetLanguage("en-US")` på PDF‑filen?**  
A: `SetLanguage` definierar standardspråket för hela dokumentets logiska struktur; alla element som inte har ett eget språk angivet kommer att ärva "en-US".

**Q: Behöver jag sätta `header.Language` om jag redan har anropat `SetLanguage` på dokumentet?**  
A: Att sätta `header.Language` är valfritt; rubriken kommer att ärva dokumentets standardspråk om du inte tilldelar ett annat värde, som visas i exemplet.

**Q: Hur kan jag skapa en rubrik på nivå 2 istället för en rubrik på nivå 1?**  
A: Använd `tagContent.CreateHeaderElement(2)` för att skapa en rubrik på nivå 2; det numeriska argumentet anger rubriknivån som kommer att återspeglas i PDF‑filens strukturträd.

**Q: Vad gör `tagContent.SetTitle("PDF Example with Header")`?**  
A: `SetTitle` skriver den angivna strängen till PDF‑filens dokumentmetadata‑titelfält, vilket kan visas i PDF‑läsare och användas för sökning eller indexering.

**Q: Vad händer om jag utelämnar `rootElement.AppendChild(header)`?**  
A: Rubrik‑elementet kommer inte att läggas till i det logiska strukturträdet, så det visas inte i PDF‑utdata och känns inte igen som en rubrik av tillgänglighetsverktyg.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}