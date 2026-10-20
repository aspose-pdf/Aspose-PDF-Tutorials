---
title: Anpassa tabellcellers bakgrund, kantlinjer och utfyllnad i PDF‑filer med Aspose.Pdf för .NET
weight: 101
limit:
description: Lär dig hur du skapar en PDF med en tvåkolumnstabell och applicerar anpassade bakgrundsfärger, kantlinjer och utfyllnad på varje cell med Aspose.Pdf för .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Lär dig hur du skapar en PDF med en tvåkolumnstabell och applicerar
    anpassade bakgrundsfärger, kantlinjer och utfyllnad på varje cell med Aspose.Pdf
    för .NET.
  headline: Anpassa tabellcellers bakgrund, kantlinjer och utfyllnad i PDF‑filer med
    Aspose.Pdf för .NET
  type: TechArticle
- description: Lär dig hur du skapar en PDF med en tvåkolumnstabell och applicerar
    anpassade bakgrundsfärger, kantlinjer och utfyllnad på varje cell med Aspose.Pdf
    för .NET.
  name: Anpassa tabellcellers bakgrund, kantlinjer och utfyllnad i PDF‑filer med Aspose.Pdf
    för .NET
  steps:
  - name: Skapa ett nytt tomt PDF‑dokument inom ett using‑block.
    text: Skapa ett nytt tomt PDF‑dokument inom ett using‑block.
  - name: Lägg till en tom sida i PDF‑dokumentet.
    text: Lägg till en tom sida i PDF‑dokumentet.
  - name: Instansiera ett Table‑objekt med två 200‑punkts kolumner, en tunn svart
      yttre kantlinje och en standardcellutfyllnad på 5 punkter.
    text: Instansiera ett Table‑objekt med två 200‑punkts kolumner, en tunn svart
      yttre kantlinje och en standardcellutfyllnad på 5 punkter.
  - name: Lägg till den första raden i tabellen.
    text: Lägg till den första raden i tabellen.
  - name: Skapa den första cellen, infoga texten "First cell", sätt en ljusgul bakgrund,
      en röd 2‑punkts kantlinje och en 4‑punkts marginal.
    text: Skapa den första cellen, infoga texten "First cell", sätt en ljusgul bakgrund,
      en röd 2‑punkts kantlinje och en 4‑punkts marginal.
  - name: Skapa den andra cellen, lägg till texten "Second cell", ge den en ljusgrön
      bakgrund, en blå 2‑punkts kantlinje och en 4‑punkts marginal.
    text: Skapa den andra cellen, lägg till texten "Second cell", ge den en ljusgrön
      bakgrund, en blå 2‑punkts kantlinje och en 4‑punkts marginal.
  - name: Lägg till den andra raden i tabellen.
    text: Lägg till den andra raden i tabellen.
  - name: Skapa den tredje cellen, infoga "Third cell", sätt en ljuscyan bakgrund,
      en mörkgrå 2‑punkts kantlinje och en 4‑punkts marginal.
    text: Skapa den tredje cellen, infoga "Third cell", sätt en ljuscyan bakgrund,
      en mörkgrå 2‑punkts kantlinje och en 4‑punkts marginal.
  - name: Skapa den fjärde cellen, lägg till "Fourth cell", ge den en ljusrosa bakgrund,
      en lila 2‑punkts kantlinje och en 4‑punkts marginal.
    text: Skapa den fjärde cellen, lägg till "Fourth cell", ge den en ljusrosa bakgrund,
      en lila 2‑punkts kantlinje och en 4‑punkts marginal.
  - name: Lägg till den fullt stylade tabellen på sidan så att den blir synlig i PDF‑filen.
    text: Lägg till den fullt stylade tabellen på sidan så att den blir synlig i PDF‑filen.
  - name: Spara PDF‑dokumentet till en fil och stäng using‑blocket.
    text: Spara PDF‑dokumentet till en fil och stäng using‑blocket.
  - name: Skriv ut ett bekräftelsemeddelande till konsolen.
    text: Skriv ut ett bekräftelsemeddelande till konsolen.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` ger en grundläggande utfyllnad för varje cell, men
      om du tilldelar en `Margin` (t.ex. `cellA1.Margin = new MarginInfo(...)`) så
      åsidosätter marginalvärdena standardutfyllnaden för den specifika cellen.'
    question: Påverkar `DefaultCellPadding` som är satt på `Table` celler som också
      har en definierad `Margin`?
  - answer: Utan `Table.Border` utelämnas den yttre rektangeln runt hela tabellen;
      endast de enskilda cellkantlinjer du har satt (t.ex. `cellA2.Border`) kommer
      att vara synliga.
    question: Hur kommer PDF‑filen att se ut om jag tar bort `Border`‑egenskapen från
      `Table`‑objektet?
  - answer: Ja, skapa en `BorderInfo` med en specifik `BorderSide` (t.ex. `new BorderInfo(BorderSide.Left,
      3, Aspose.Pdf.Color.Black)`) och tilldela den till cellens `Border`‑egenskap.
    question: Kan jag ge en cell olika kantbredd på varje sida?
  - answer: Instansiera en ny `Row` med `Row newRow = dataTable.Rows.Add();` och lägg
      sedan till celler i `newRow.Cells` på samma sätt som i de tidigare raderna.
    question: Hur lägger jag till en tredje rad i tabellen efter den visade koden?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Formatera PDF‑tabellceller – bakgrund, kantlinje, utfyllnad
og_description: Formatera snabbt tabellceller i en PDF med anpassade färger, kantlinjer och avstånd med Aspose.Pdf för .NET.
og_image_alt: Guide som visar hur du formaterar bakgrundsfärg, kantlinje och utfyllnad för tabellceller i en PDF med Aspose.Pdf för .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Anpassa tabellcellers bakgrund, kantlinjer och utfyllnad i PDF‑filer med Aspose.Pdf för .NET
I den här handledningen får du se hur du genererar ett PDF‑dokument, lägger till en tvåkolumnstabell och exakt styr varje cells utseende. Genom att ange bakgrundsfärger, definiera kantlinjer och justera utfyllnad kan du få tabelldata att sticka ut och se professionella ut. Exemplet använder Aspose.Pdf Document‑ och Table‑klasserna för att demonstrera varje formateringsalternativ.

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

**Q: Påverkar `DefaultCellPadding` som är satt på `Table` celler som också har en definierad `Margin`?**  
A: `DefaultCellPadding` ger en grundläggande utfyllnad för varje cell, men om du tilldelar en `Margin` (t.ex. `cellA1.Margin = new MarginInfo(...)`) så åsidosätter marginalvärdena standardutfyllnaden för den specifika cellen.

**Q: Hur kommer PDF‑filen att se ut om jag tar bort `Border`‑egenskapen från `Table`‑objektet?**  
A: Utan `Table.Border` utelämnas den yttre rektangeln runt hela tabellen; endast de enskilda cellkantlinjer du har satt (t.ex. `cellA2.Border`) kommer att vara synliga.

**Q: Kan jag ge en cell olika kantbredd på varje sida?**  
A: Ja, skapa en `BorderInfo` med en specifik `BorderSide` (t.ex. `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) och tilldela den till cellens `Border`‑egenskap.

**Q: Hur lägger jag till en tredje rad i tabellen efter den visade koden?**  
A: Instansiera en ny `Row` med `Row newRow = dataTable.Rows.Add();` och lägg sedan till celler i `newRow.Cells` på samma sätt som i de tidigare raderna.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}