---
title: Voeg een getagde externe link met tooltip toe aan PDF met Aspose.Pdf for .NET
weight: 440
limit:
description: Leer hoe je een getagde externe hyperlink met weergavetekst en tooltip toevoegt aan een PDF met Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Leer hoe je een getagde externe hyperlink met weergavetekst en tooltip
    toevoegt aan een PDF met Aspose.Pdf for .NET.
  headline: Voeg een getagde externe link met tooltip toe aan PDF met Aspose.Pdf for
    .NET
  type: TechArticle
- description: Leer hoe je een getagde externe hyperlink met weergavetekst en tooltip
    toevoegt aan een PDF met Aspose.Pdf for .NET.
  name: Voeg een getagde externe link met tooltip toe aan PDF met Aspose.Pdf for .NET
  steps:
  - name: Definieer de paden voor de bron‑PDF en het resultaatbestand.
    text: Definieer de paden voor de bron‑PDF en het resultaatbestand.
  - name: Controleer of de bron‑PDF bestaat en annuleer als deze niet gevonden kan
      worden.
    text: Controleer of de bron‑PDF bestaat en annuleer als deze niet gevonden kan
      worden.
  - name: Open het PDF‑document binnen een using‑blok om correcte vrijgave te garanderen.
    text: Open het PDF‑document binnen een using‑blok om correcte vrijgave te garanderen.
  - name: Verkrijg de tagged‑content manager voor het geopende document.
    text: Verkrijg de tagged‑content manager voor het geopende document.
  - name: Stel de documenttaal in op Engels (VS) en geef de PDF een titel afgeleid
      van de bestandsnaam.
    text: Stel de documenttaal in op Engels (VS) en geef de PDF een titel afgeleid
      van de bestandsnaam.
  - name: Haal het root‑element op van de boom van de logische structuur waaraan nieuwe
      elementen worden toegevoegd.
    text: Haal het root‑element op van de boom van de logische structuur waaraan nieuwe
      elementen worden toegevoegd.
  - name: Maak een link‑element, stel de weergavetekst, doel‑URL en tooltip‑titel
      in, en voeg het vervolgens toe aan de structuur van het document.
    text: Maak een link‑element, stel de weergavetekst, doel‑URL en tooltip‑titel
      in, en voeg het vervolgens toe aan de structuur van het document.
  - name: Sla de bijgewerkte PDF op naar het opgegeven resultaatbestand.
    text: Sla de bijgewerkte PDF op naar het opgegeven resultaatbestand.
  - name: Geef een bevestigingsbericht weer dat aangeeft waar de gewijzigde PDF is
      opgeslagen.
    text: Geef een bevestigingsbericht weer dat aangeeft waar de gewijzigde PDF is
      opgeslagen.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` retourneert de bestaande getagde inhoud als het
      document al getagd is; het maakt geen dubbele boom aan.'
    question: Wat als de bron‑PDF al getagd is – zal het aanroepen van `pdfDoc.TaggedContent`
      een nieuwe tag‑boom creëren of de bestaande hergebruiken?
  - answer: Ja – zoek het gewenste `StructureElement` (bijv. een `Div` of `Paragraph`
      op een pagina) via de logische structuurboom en roep `AppendChild(externalLink)`
      aan op dat element.
    question: Kan ik de hyperlink op een specifieke pagina plaatsen in plaats van
      deze aan het root‑element toe te voegen?
  - answer: De tooltip wordt alleen weergegeven als `externalLink.Title` is ingesteld
      vóór `pdfDoc.Save`; het later instellen heeft geen effect op de al geschreven
      PDF.
    question: Is de `Title`‑eigenschap van `LinkElement` vereist om de tooltip te
      laten verschijnen, en kan deze worden ingesteld na het aanroepen van `Save`?
  - answer: Wijs een `FileSpecification` (bijv. `new FileSpecification("file:///C:/Docs/manual.pdf")`)
      toe aan `externalLink.Hyperlink` in plaats van `WebHyperlink` te gebruiken.
    question: Hoe maak ik een link naar een lokaal bestand in plaats van een web‑URL?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Voeg een getagde externe link met tooltip in een PDF in
og_description: Integreer een toegankelijke hyperlink met zichtbare tekst en een tooltip in je PDF met Aspose.Pdf for .NET.
og_image_alt: Gids die laat zien hoe je een getagde externe hyperlink met tooltip toevoegt aan een PDF met Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Voeg een getagde externe link met tooltip toe aan PDF met Aspose.Pdf
Deze tutorial laat zien hoe je een bestaande PDF opent met Aspose.Pdf for .NET, een getagde externe hyperlink maakt die zichtbare weergavetekst en een tooltip‑titel bevat, de link in de logische structuur van het document invoegt en het bijgewerkte bestand opslaat. Door de stappen te volgen maak je een toegankelijke PDF waarin de link deel uitmaakt van de tag‑hiërarchie en extra context biedt aan lezers.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: Wat als de bron‑PDF al getagd is – zal het aanroepen van `pdfDoc.TaggedContent` een nieuwe tag‑boom creëren of de bestaande hergebruiken?**  
A: `pdfDoc.TaggedContent` retourneert de bestaande getagde inhoud als het document al getagd is; het maakt geen dubbele boom aan.

**Q: Kan ik de hyperlink op een specifieke pagina plaatsen in plaats van deze aan het root‑element toe te voegen?**  
A: Ja – zoek het gewenste `StructureElement` (bijv. een `Div` of `Paragraph` op een pagina) via de logische structuurboom en roep `AppendChild(externalLink)` aan op dat element.

**Q: Is de `Title`‑eigenschap van `LinkElement` vereist om de tooltip te laten verschijnen, en kan deze worden ingesteld na het aanroepen van `Save`?**  
A: De tooltip wordt alleen weergegeven als `externalLink.Title` is ingesteld vóór `pdfDoc.Save`; het later instellen heeft geen effect op de al geschreven PDF.

**Q: Hoe maak ik een link naar een lokaal bestand in plaats van een web‑URL?**  
A: Wijs een `FileSpecification` (bijv. `new FileSpecification("file:///C:/Docs/manual.pdf")`) toe aan `externalLink.Hyperlink` in plaats van `WebHyperlink` te gebruiken.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}