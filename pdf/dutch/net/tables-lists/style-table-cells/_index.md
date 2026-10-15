---
title: Aangepaste achtergrond, randen en opvulling van tabelcellen in PDF's met Aspose.Pdf for .NET
weight: 101
limit:
description: Leer hoe je een PDF maakt met een tabel van twee kolommen en aangepaste achtergrondkleuren, randen en opvulling op elke cel toepast met Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Leer hoe je een PDF maakt met een tabel van twee kolommen en aangepaste
    achtergrondkleuren, randen en opvulling op elke cel toepast met Aspose.Pdf for
    .NET.
  headline: Aangepaste achtergrond, randen en opvulling van tabelcellen in PDF's met
    Aspose.Pdf for .NET
  type: TechArticle
- description: Leer hoe je een PDF maakt met een tabel van twee kolommen en aangepaste
    achtergrondkleuren, randen en opvulling op elke cel toepast met Aspose.Pdf for
    .NET.
  name: Aangepaste achtergrond, randen en opvulling van tabelcellen in PDF's met Aspose.Pdf
    for .NET
  steps:
  - name: Doe een nieuw leeg PDF‑document aan binnen een using‑blok.
    text: Doe een nieuw leeg PDF‑document aan binnen een using‑blok.
  - name: Voeg een lege pagina toe aan het PDF‑document.
    text: Voeg een lege pagina toe aan het PDF‑document.
  - name: Instantieer een Table‑object met twee kolommen van 200 punten, een dunne
      zwarte buitenrand en een standaard celopvulling van 5 punten.
    text: Instantieer een Table‑object met twee kolommen van 200 punten, een dunne
      zwarte buitenrand en een standaard celopvulling van 5 punten.
  - name: Voeg de eerste rij toe aan de tabel.
    text: Voeg de eerste rij toe aan de tabel.
  - name: Maak de eerste cel, voeg de tekst "First cell" in, stel een lichtgele achtergrond
      in, een rode rand van 2 punten en een marge van 4 punten.
    text: Maak de eerste cel, voeg de tekst "First cell" in, stel een lichtgele achtergrond
      in, een rode rand van 2 punten en een marge van 4 punten.
  - name: Maak de tweede cel, voeg de tekst "Second cell" toe, geef het een lichtgroene
      achtergrond, een blauwe rand van 2 punten en een marge van 4 punten.
    text: Maak de tweede cel, voeg de tekst "Second cell" toe, geef het een lichtgroene
      achtergrond, een blauwe rand van 2 punten en een marge van 4 punten.
  - name: Voeg de tweede rij toe aan de tabel.
    text: Voeg de tweede rij toe aan de tabel.
  - name: Maak de derde cel, voeg "Third cell" in, stel een lichtcyaan achtergrond
      in, een donkergrijze rand van 2 punten en een marge van 4 punten.
    text: Maak de derde cel, voeg "Third cell" in, stel een lichtcyaan achtergrond
      in, een donkergrijze rand van 2 punten en een marge van 4 punten.
  - name: Maak de vierde cel, voeg "Fourth cell" toe, geef het een lichtroze achtergrond,
      een paarse rand van 2 punten en een marge van 4 punten.
    text: Maak de vierde cel, voeg "Fourth cell" toe, geef het een lichtroze achtergrond,
      een paarse rand van 2 punten en een marge van 4 punten.
  - name: Voeg de volledig gestylede tabel toe aan de pagina zodat deze zichtbaar
      wordt in de PDF.
    text: Voeg de volledig gestylede tabel toe aan de pagina zodat deze zichtbaar
      wordt in de PDF.
  - name: Sla het PDF‑document op naar een bestand en sluit het using‑blok.
    text: Sla het PDF‑document op naar een bestand en sluit het using‑blok.
  - name: Print een bevestigingsbericht naar de console.
    text: Print een bevestigingsbericht naar de console.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` biedt een basisopvulling voor elke cel, maar als
      je een `Margin` toewijst (bijv. `cellA1.Margin = new MarginInfo(...)`) dan overschrijven
      de marge‑waarden de standaardopvulling voor die specifieke cel.'
    question: Beïnvloedt de `DefaultCellPadding` die op de `Table` is ingesteld cellen
      die ook een `Margin` hebben gedefinieerd?
  - answer: Zonder `Table.Border` wordt de buitenste rechthoek rond de hele tabel
      weggelaten; alleen de individuele celranden die je instelt (bijv. `cellA2.Border`)
      zijn zichtbaar.
    question: Hoe ziet de PDF eruit als ik de `Border`‑eigenschap van het `Table`‑object
      verwijder?
  - answer: Ja, maak een `BorderInfo` met een specifieke `BorderSide` (bijv. `new
      BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) en wijs deze toe aan
      de `Border`‑eigenschap van de cel.
    question: Kan ik een cel een verschillende randdikte per zijde geven?
  - answer: Instantieer een nieuwe `Row` met `Row newRow = dataTable.Rows.Add();`
      en voeg vervolgens cellen toe aan `newRow.Cells` net als bij de eerdere rijen.
    question: Hoe voeg ik een derde rij toe aan de tabel na de getoonde code?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Stijl PDF‑tabelcellen – Achtergrond, Rand, Opvulling
og_description: Formatteer snel tabelcellen in een PDF met aangepaste kleuren, randen en afstanden met Aspose.Pdf for .NET.
og_image_alt: Gids die laat zien hoe je de achtergrondkleur, rand en opvulling van tabelcellen in een PDF stijlt met Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aangepaste achtergrond, randen en opvulling van tabelcellen in PDF's met Aspose.Pdf
In deze tutorial zie je hoe je een PDF‑document genereert, een tabel met twee kolommen toevoegt en het uiterlijk van elke cel nauwkeurig regelt. Door achtergrondkleuren in te stellen, randen te definiëren en de opvulling aan te passen, kun je tabelgegevens laten opvallen en er verzorgd uit laten zien. Het voorbeeld gebruikt de Aspose.Pdf Document- en Table‑klassen om elke stijloptie te demonstreren.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: Beïnvloedt de `DefaultCellPadding` die op de `Table` is ingesteld cellen die ook een `Margin` hebben gedefinieerd?**  
A: `DefaultCellPadding` biedt een basisopvulling voor elke cel, maar als je een `Margin` toewijst (bijv. `cellA1.Margin = new MarginInfo(...)`) dan overschrijven de marge‑waarden de standaardopvulling voor die specifieke cel.

**Q: Hoe ziet de PDF eruit als ik de `Border`‑eigenschap van het `Table`‑object verwijder?**  
A: Zonder `Table.Border` wordt de buitenste rechthoek rond de hele tabel weggelaten; alleen de individuele celranden die je instelt (bijv. `cellA2.Border`) zijn zichtbaar.

**Q: Kan ik een cel een verschillende randdikte per zijde geven?**  
A: Ja, maak een `BorderInfo` met een specifieke `BorderSide` (bijv. `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) en wijs deze toe aan de `Border`‑eigenschap van de cel.

**Q: Hoe voeg ik een derde rij toe aan de tabel na de getoonde code?**  
A: Instantieer een nieuwe `Row` met `Row newRow = dataTable.Rows.Add();` en voeg vervolgens cellen toe aan `newRow.Cells` net als bij de eerdere rijen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}