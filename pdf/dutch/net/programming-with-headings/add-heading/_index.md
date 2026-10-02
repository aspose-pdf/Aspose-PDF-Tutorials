---
title: Kop, taal en titel toevoegen aan een PDF met Aspose.PDF for .NET
weight: 110
limit:
description: Maak een PDF, stel de taal en titel in, en voeg een niveau‑1‑kop toe met Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Maak een PDF, stel de taal en titel in, en voeg een niveau‑1‑kop toe
    met Aspose.PDF for .NET.
  headline: Kop, taal en titel toevoegen aan een PDF met Aspose.PDF for .NET
  type: TechArticle
- description: Maak een PDF, stel de taal en titel in, en voeg een niveau‑1‑kop toe
    met Aspose.PDF for .NET.
  name: Kop, taal en titel toevoegen aan een PDF met Aspose.PDF for .NET
  steps:
  - name: Definieer de bestandsnaam voor de gegenereerde PDF.
    text: Definieer de bestandsnaam voor de gegenereerde PDF.
  - name: Maak een nieuwe lege PDF‑documentinstantie (`pdfDoc`) aan binnen een `using`‑blok.
    text: Maak een nieuwe lege PDF‑documentinstantie (`pdfDoc`) aan binnen een `using`‑blok.
  - name: Verkrijg de `ITaggedContent`‑interface om met getagde PDF‑structuren te
      werken.
    text: Verkrijg de `ITaggedContent`‑interface om met getagde PDF‑structuren te
      werken.
  - name: Stel de standaardtaal van het document in op Engels (VS) en wijs een titel‑metadata
      toe.
    text: Stel de standaardtaal van het document in op Engels (VS) en wijs een titel‑metadata
      toe.
  - name: Haal het root‑element van de logische structuurboom op.
    text: Haal het root‑element van de logische structuurboom op.
  - name: Bouw een niveau‑1‑kop‑element, stel de weergegeven tekst in en geef de taal
      op.
    text: Bouw een niveau‑1‑kop‑element, stel de weergegeven tekst in en geef de taal
      op.
  - name: Voeg het kop‑element toe aan de root, waardoor de kop in de PDF verschijnt.
    text: Voeg het kop‑element toe aan de root, waardoor de kop in de PDF verschijnt.
  - name: Sla de PDF op naar het opgegeven bestand en sluit de document‑scope.
    text: Sla de PDF op naar het opgegeven bestand en sluit de document‑scope.
  - name: Geef een bevestigingsbericht weer op de console.
    text: Geef een bevestigingsbericht weer op de console.
  type: HowTo
- questions:
  - answer: '`SetLanguage` definieert de standaardtaal voor de volledige logische
      structuur van het document; elk element dat geen eigen taal heeft ingesteld,
      erft "en-US".'
    question: Wat is het effect van het aanroepen van `tagContent.SetLanguage(\"en-US\")`
      op de PDF?
  - answer: Het instellen van `header.Language` is optioneel; de kop erft de standaardtaal
      van het document tenzij je een andere waarde toewijst, zoals getoond in het
      voorbeeld.
    question: Moet ik `header.Language` instellen als ik al `SetLanguage` op het document
      heb aangeroepen?
  - answer: Gebruik `tagContent.CreateHeaderElement(2)` om een niveau‑2‑kop te maken;
      het numerieke argument geeft het kopniveau aan dat in de structuurboom van de
      PDF wordt weergegeven.
    question: Hoe kan ik een niveau‑2‑kop maken in plaats van een niveau‑1‑kop?
  - answer: '`SetTitle` schrijft de opgegeven tekenreeks naar het titel‑metadata‑veld
      van het PDF‑document, dat kan worden bekeken in PDF‑readers en gebruikt kan
      worden voor zoeken of indexeren.'
    question: Wat doet `tagContent.SetTitle(\"PDF Example with Header\")`?
  - answer: Het kop‑element wordt niet toegevoegd aan de logische structuurboom, waardoor
      het niet in de PDF‑output verschijnt en niet wordt herkend als een kop voor
      toegankelijkheidstools.
    question: Wat gebeurt er als ik `rootElement.AppendChild(header)` weglaten?
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: Een kop invoegen en de taal instellen in een PDF
og_description: Leer hoe je een PDF maakt, de taal en titel instelt, en vervolgens een niveau‑1‑kop toevoegt met een paar regels .NET‑code.
og_image_alt: Gids die laat zien hoe je een kop, taal en titel toevoegt aan een PDF met Aspose.PDF for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kop, taal en titel toevoegen aan een PDF met Aspose.PDF
Deze tutorial leidt je stap voor stap door het maken van een nieuw PDF‑document met Aspose.PDF for .NET, het toewijzen van een standaardtaal en documenttitel, en het invoegen van een niveau‑1‑kop. Je ziet hoe je met de Document-, ITaggedContent-, StructureElement- en HeaderElement‑klassen werkt om een correct getagde PDF te produceren die geschikt is voor toegankelijkheidstools.

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

**Q: Wat is het effect van het aanroepen van `tagContent.SetLanguage(\"en-US\")` op de PDF?**  
A: `SetLanguage` definieert de standaardtaal voor de volledige logische structuur van het document; elk element dat geen eigen taal heeft ingesteld, erft "en-US".

**Q: Moet ik `header.Language` instellen als ik al `SetLanguage` op het document heb aangeroepen?**  
A: Het instellen van `header.Language` is optioneel; de kop erft de standaardtaal van het document tenzij je een andere waarde toewijst, zoals getoond in het voorbeeld.

**Q: Hoe kan ik een niveau‑2‑kop maken in plaats van een niveau‑1‑kop?**  
A: Gebruik `tagContent.CreateHeaderElement(2)` om een niveau‑2‑kop te maken; het numerieke argument geeft het kopniveau aan dat in de structuurboom van de PDF wordt weergegeven.

**Q: Wat doet `tagContent.SetTitle(\"PDF Example with Header\")`?**  
A: `SetTitle` schrijft de opgegeven tekenreeks naar het titel‑metadata‑veld van het PDF‑document, dat kan worden bekeken in PDF‑readers en gebruikt kan worden voor zoeken of indexeren.

**Q: Wat gebeurt er als ik `rootElement.AppendChild(header)` weglaten?**  
A: Het kop‑element wordt niet toegevoegd aan de logische structuurboom, waardoor het niet in de PDF‑output verschijnt en niet wordt herkend als een kop voor toegankelijkheidstools.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}