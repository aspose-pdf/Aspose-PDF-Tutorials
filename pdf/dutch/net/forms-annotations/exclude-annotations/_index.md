---
title: Side‑by‑Side PDF‑vergelijking met uitsluiting van annotaties met Aspose.Pdf for .NET
weight: 101
limit:
description: Stapsgewijze handleiding om PDF‑bestanden te vergelijken en annotatie‑gebieden uit te sluiten met Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Stapsgewijze handleiding om PDF‑bestanden te vergelijken en annotatie‑gebieden
    uit te sluiten met Aspose.Pdf for .NET.
  headline: Side‑by‑Side PDF‑vergelijking met uitsluiting van annotaties met Aspose.Pdf
    for .NET
  type: TechArticle
- description: Stapsgewijze handleiding om PDF‑bestanden te vergelijken en annotatie‑gebieden
    uit te sluiten met Aspose.Pdf for .NET.
  name: Side‑by‑Side PDF‑vergelijking met uitsluiting van annotaties met Aspose.Pdf
    for .NET
  steps:
  - name: Definieer de bestands‑paden voor de primaire PDF, de secundaire PDF en de
      uitvoer‑diff‑PDF.
    text: Definieer de bestands‑paden voor de primaire PDF, de secundaire PDF en de
      uitvoer‑diff‑PDF.
  - name: Controleer of beide invoer‑PDF‑bestanden bestaan en annuleer met een foutmelding
      als een van beide ontbreekt.
    text: Controleer of beide invoer‑PDF‑bestanden bestaan en annuleer met een foutmelding
      als een van beide ontbreekt.
  - name: Open de twee PDF‑bestanden als Document‑objecten (pdfA en pdfB) binnen een
      using‑blok zodat ze automatisch worden vrijgegeven.
    text: Open de twee PDF‑bestanden als Document‑objecten (pdfA en pdfB) binnen een
      using‑blok zodat ze automatisch worden vrijgegeven.
  - name: Verzamel de begrenzingsrechthoeken van elke annotatie in pdfA en sla ze
      op in ignoredRectsA.
    text: Verzamel de begrenzingsrechthoeken van elke annotatie in pdfA en sla ze
      op in ignoredRectsA.
  - name: Verzamel de begrenzingsrechthoeken van elke annotatie in pdfB en sla ze
      op in ignoredRectsB.
    text: Verzamel de begrenzingsrechthoeken van elke annotatie in pdfB en sla ze
      op in ignoredRectsB.
  - name: Maak een SideBySideComparisonOptions‑object aan en wijs de eerder verzamelde
      annotatie‑rechthoeken toe aan ExcludeAreas1 en ExcludeAreas2 zodat die regio's
      tijdens de vergelijking worden genegeerd.
    text: Maak een SideBySideComparisonOptions‑object aan en wijs de eerder verzamelde
      annotatie‑rechthoeken toe aan ExcludeAreas1 en ExcludeAreas2 zodat die regio's
      tijdens de vergelijking worden genegeerd.
  - name: Voer de side‑by‑side PDF‑vergelijking uit met de twee Document‑objecten
      en de geconfigureerde opties, en schrijf het resultaat naar outputPdf.
    text: Voer de side‑by‑side PDF‑vergelijking uit met de twee Document‑objecten
      en de geconfigureerde opties, en schrijf het resultaat naar outputPdf.
  - name: Maak de Document‑objecten vrij en verlaat het using‑blok.
    text: Maak de Document‑objecten vrij en verlaat het using‑blok.
  - name: Print een bevestigingsbericht dat aangeeft dat de vergelijking voltooid
      is en waar de diff‑PDF is opgeslagen.
    text: Print een bevestigingsbericht dat aangeeft dat de vergelijking voltooid
      is en waar de diff‑PDF is opgeslagen.
  type: HowTo
- questions:
  - answer: Ja. De code voegt simpelweg geen rechthoeken toe aan de overeenkomstige
      `ignoredRects`‑lijst, zodat `ExcludeAreas1`/`ExcludeAreas2` een lege array ontvangen
      en de comparer de hele pagina verwerkt.
    question: Wat gebeurt er als een PDF‑pagina geen annotaties heeft – werkt de vergelijking
      dan nog steeds?
  - answer: Stel `ExcludeAreas1` (of `ExcludeAreas2`) in op de verzamelde rechthoeken
      en laat de andere eigenschap een lege array; de comparer negeert alleen regio's
      in het opgegeven document.
    question: Kan ik alleen annotaties van één document uitsluiten terwijl ik de annotaties
      van het andere document in de diff behoud?
  - answer: Overlappende rechthoeken worden intern door de comparer samengevoegd,
      zodat overlappende annotatie‑grenzen veilig worden uitgesloten zonder dubbel
      te tellen.
    question: Veroorzaken overlappende annotatie‑rechthoeken problemen met `ExcludeAreas`?
  - answer: Ja, stel `compareOpts.ExcludeTables = true;` in – deze vlag werkt samen
      met `ExcludeAreas1`/`ExcludeAreas2` om ook tabel‑regio's uit te sluiten.
    question: Is er een manier om naast annotaties ook tabellen uit te sluiten met
      hetzelfde options‑object?
  - answer: De code controleert `if (a != null && a.Rect != null)` voordat deze aan
      de lijst wordt toegevoegd, dus null‑rechthoeken worden simpelweg overgeslagen
      en er wordt geen uitzondering gegooid.
    question: Wat als de `Rect`‑eigenschap van een annotatie null is – zal de code
      een uitzondering veroorzaken?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: PDF's vergelijken zonder annotaties
og_description: Voer een side‑by‑side PDF‑diff uit die alle annotatiemarkeringen overslaat.
og_image_alt: Handleiding die een side‑by‑side PDF‑vergelijking toont waarbij annotatie‑regio's worden uitgesloten met Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Side‑by‑Side PDF‑vergelijking met uitsluiting van annotaties met Aspose.Pdf
Deze tutorial laat zien hoe je twee PDF‑bestanden kunt vergelijken met Aspose.Pdf for .NET terwijl je alle annotatie‑inhoud negeert. Het extraheert de begrenzingsvakken van alle annotaties uit elk document, voert die regio's in SideBySideComparisonOptions in, en voert vervolgens een side‑by‑side‑vergelijking uit. Het resultaat is een diff‑PDF die alleen de niet‑annotatie‑wijzigingen markeert.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Wat gebeurt er als een PDF‑pagina geen annotaties heeft – werkt de vergelijking dan nog steeds?**  
A: Ja. De code voegt simpelweg geen rechthoeken toe aan de overeenkomstige `ignoredRects`‑lijst, zodat `ExcludeAreas1`/`ExcludeAreas2` een lege array ontvangen en de comparer de hele pagina verwerkt.

**Q: Kan ik alleen annotaties van één document uitsluiten terwijl ik de annotaties van het andere document in de diff behoud?**  
A: Stel `ExcludeAreas1` (of `ExcludeAreas2`) in op de verzamelde rechthoeken en laat de andere eigenschap een lege array; de comparer negeert alleen regio's in het opgegeven document.

**Q: Veroorzaken overlappende annotatie‑rechthoeken problemen met `ExcludeAreas`?**  
A: Overlappende rechthoeken worden intern door de comparer samengevoegd, zodat overlappende annotatie‑grenzen veilig worden uitgesloten zonder dubbel te tellen.

**Q: Is er een manier om naast annotaties ook tabellen uit te sluiten met hetzelfde options‑object?**  
A: Ja, stel `compareOpts.ExcludeTables = true;` in – deze vlag werkt samen met `ExcludeAreas1`/`ExcludeAreas2` om ook tabel‑regio's uit te sluiten.

**Q: Wat als de `Rect`‑eigenschap van een annotatie null is – zal de code een uitzondering veroorzaken?**  
A: De code controleert `if (a != null && a.Rect != null)` voordat deze aan de lijst wordt toegevoegd, dus null‑rechthoeken worden simpelweg overgeslagen en er wordt geen uitzondering gegooid.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}