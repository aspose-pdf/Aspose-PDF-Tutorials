---
title: PDF's vergelijken terwijl specifieke gebieden worden genegeerd met Aspose.Pdf for .NET
weight: 201
limit:
description: Leer PDF's naast elkaar te vergelijken en geselecteerde gebieden te negeren met Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Leer PDF's naast elkaar te vergelijken en geselecteerde gebieden te
    negeren met Aspose.Pdf for .NET.
  headline: PDF's vergelijken terwijl specifieke gebieden worden genegeerd met Aspose.Pdf
    for .NET
  type: TechArticle
- description: Leer PDF's naast elkaar te vergelijken en geselecteerde gebieden te
    negeren met Aspose.Pdf for .NET.
  name: PDF's vergelijken terwijl specifieke gebieden worden genegeerd met Aspose.Pdf
    for .NET
  steps:
  - name: Definieer de bestands‑paden voor de twee bron‑PDF‑bestanden en de uitvoer‑diff‑PDF.
    text: Definieer de bestands‑paden voor de twee bron‑PDF‑bestanden en de uitvoer‑diff‑PDF.
  - name: Controleer of beide bron‑PDF‑bestanden bestaan en stop met een foutmelding
      als één van hen ontbreekt.
    text: Controleer of beide bron‑PDF‑bestanden bestaan en stop met een foutmelding
      als één van hen ontbreekt.
  - name: Maak een array aan die het rechthoekige gebied bevat dat in de eerste PDF
      moet worden genegeerd.
    text: Maak een array aan die het rechthoekige gebied bevat dat in de eerste PDF
      moet worden genegeerd.
  - name: Maak een array aan die het rechthoekige gebied bevat dat in de tweede PDF
      moet worden genegeerd.
    text: Maak een array aan die het rechthoekige gebied bevat dat in de tweede PDF
      moet worden genegeerd.
  - name: Configureer de naast‑elkaar vergelijking door de ignore‑area‑arrays toe
      te wijzen aan de juiste eigenschappen.
    text: Configureer de naast‑elkaar vergelijking door de ignore‑area‑arrays toe
      te wijzen aan de juiste eigenschappen.
  - name: Laad beide PDF‑bestanden en voer de naast‑elkaar vergelijking uit, waarbij
      het diff‑bestand wordt gegenereerd op het opgegeven pad.
    text: Laad beide PDF‑bestanden en voer de naast‑elkaar vergelijking uit, waarbij
      het diff‑bestand wordt gegenereerd op het opgegeven pad.
  - name: Print een bevestigingsbericht dat aangeeft dat de vergelijking is voltooid
      en waar de diff‑PDF is opgeslagen.
    text: Print een bevestigingsbericht dat aangeeft dat de vergelijking is voltooid
      en waar de diff‑PDF is opgeslagen.
  type: HowTo
- questions:
  - answer: De coördinaten zijn in points (1/72 inch) met de oorsprong in de linker‑onderhoek
      van de pagina, dus de eerste twee getallen zijn de linker‑onder X/Y en de laatste
      twee de rechter‑boven X/Y.
    question: Welk coördinatensysteem gebruiken de `Rectangle`‑waarden bij het definiëren
      van negeer‑zones?
  - answer: Ja – lever meerdere `Aspose.Pdf.Rectangle`‑objecten in de `ExcludeAreas1`
      (of `ExcludeAreas2`) array; elk rechthoek wordt onafhankelijk uitgesloten tijdens
      de vergelijking.
    question: Kan ik meer dan één rechthoekig gebied in hetzelfde document negeren?
  - answer: Nee. `ExcludeAreas1` geldt voor de eerste PDF en `ExcludeAreas2` voor
      de tweede, zodat je verschillende coördinaten voor elk document kunt opgeven.
    question: Moeten de negeer‑rechthoeken identiek zijn in beide PDF's?
  - answer: Aspose.Pdf negeert stilzwijgend rechthoeken die volledig buiten de pagina
      vallen; ze hebben geen effect op het vergelijkingsresultaat.
    question: Wat gebeurt er als een rechthoek buiten de paginagrenzen wordt gedefinieerd?
  - answer: De `ExcludeAreas`‑arrays gelden per pagina, dus je moet dezelfde `Rectangle`
      aan de collectie van elke pagina toevoegen (bijv. door door `pdf.Pages` te itereren
      en de array toe te wijzen) voordat je `SideBySidePdfComparer.Compare` aanroept.
    question: Hoe kan ik hetzelfde gebied op elke pagina van een PDF uitsluiten?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Regio's negeren bij het vergelijken van PDF's
og_description: Zie hoe je geselecteerde gebieden kunt overslaan in een naast‑elkaar PDF‑vergelijking en een schone diff‑PDF krijgt.
og_image_alt: Gids die naast‑elkaar PDF‑vergelijking toont met uitgesloten rechthoekige gebieden met Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF's vergelijken terwijl specifieke gebieden worden genegeerd met Aspose.Pdf
Deze tutorial toont hoe je twee PDF‑documenten naast elkaar kunt vergelijken met Aspose.Pdf for .NET terwijl je aangewezen rechthoekige gebieden uitsluit van de analyse. Door uitsluitingsgebieden in elk bestand te definiëren, markeert de gegenereerde diff‑PDF alleen de wijzigingen die van belang zijn, waardoor het makkelijker wordt om je te concentreren op relevante verschillen.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Welk coördinatensysteem gebruiken de `Rectangle`‑waarden bij het definiëren van negeer‑zones?**  
A: De coördinaten zijn in points (1/72 inch) met de oorsprong in de linker‑onderhoek van de pagina, dus de eerste twee getallen zijn de linker‑onder X/Y en de laatste twee de rechter‑boven X/Y.

**Q: Kan ik meer dan één rechthoekig gebied in hetzelfde document negeren?**  
A: Ja – lever meerdere `Aspose.Pdf.Rectangle`‑objecten in de `ExcludeAreas1` (of `ExcludeAreas2`) array; elk rechthoek wordt onafhankelijk uitgesloten tijdens de vergelijking.

**Q: Moeten de negeer‑rechthoeken identiek zijn in beide PDF's?**  
A: Nee. `ExcludeAreas1` geldt voor de eerste PDF en `ExcludeAreas2` voor de tweede, zodat je verschillende coördinaten voor elk document kunt opgeven.

**Q: Wat gebeurt er als een rechthoek buiten de paginagrenzen wordt gedefinieerd?**  
A: Aspose.Pdf negeert stilzwijgend rechthoeken die volledig buiten de pagina vallen; ze hebben geen effect op het vergelijkingsresultaat.

**Q: Hoe kan ik hetzelfde gebied op elke pagina van een PDF uitsluiten?**  
A: De `ExcludeAreas`‑arrays gelden per pagina, dus je moet dezelfde `Rectangle` aan de collectie van elke pagina toevoegen (bijv. door door `pdf.Pages` te itereren en de array toe te wijzen) voordat je `SideBySidePdfComparer.Compare` aanroept.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}