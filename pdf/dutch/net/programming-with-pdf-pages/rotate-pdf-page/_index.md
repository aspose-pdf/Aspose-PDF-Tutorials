---
title: Roteer een enkele PDF‑pagina 180 graden met Aspose.PDF for .NET
weight: 260
limit:
description: Leer hoe je de derde pagina van een PDF 180° kunt roteren met Aspose.PDF for .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Leer hoe je de derde pagina van een PDF 180° kunt roteren met Aspose.PDF
    for .NET.
  headline: Roteer een enkele PDF‑pagina 180 graden met Aspose.PDF for .NET
  type: TechArticle
- description: Leer hoe je de derde pagina van een PDF 180° kunt roteren met Aspose.PDF
    for .NET.
  name: Roteer een enkele PDF‑pagina 180 graden met Aspose.PDF for .NET
  steps:
  - name: Het bestand bevat alleen verklarende opmerkingen en geen uitvoerbare code,
      en dient als een tijdelijke aanduiding voor het oorspronkelijke voorbeeld.
    text: Het bestand bevat alleen verklarende opmerkingen en geen uitvoerbare code,
      en dient als een tijdelijke aanduiding voor het oorspronkelijke voorbeeld.
  type: HowTo
- questions:
  - answer: Gebruik de paginaverzameling van de SDK met nul‑gebaseerde indexering,
      bijv. `pdfDocument.Pages[2]`, omdat index 2 overeenkomt met de derde pagina.
    question: Hoe richt ik me op de derde pagina van de PDF voor rotatie?
  - answer: De rotatie‑eigenschap accepteert alleen de vier standaardwaarden 0, 90,
      180 en 270 graden; elke andere waarde wordt afgerond naar de dichtstbijzijnde
      toegestane hoek.
    question: Kan ik een pagina roteren met een andere hoek dan 180 graden?
  - answer: De rotatie wordt alleen toegepast op het in‑memory `PdfDocument`; je moet
      `pdfDocument.Save(\"output.pdf\")` (of een vergelijkbare opslaand methode) aanroepen
      om de wijzigingen naar een nieuw bestand te schrijven, zodat de bron ongewijzigd
      blijft.
    question: Wijzigt het roteren van de pagina automatisch het originele bestand?
  - answer: De SDK berekent automatisch de posities van annotaties en formuliervelden
      opnieuw zodat ze correct uitgelijnd blijven met de nieuwe oriëntatie.
    question: Wat gebeurt er met annotaties of formuliervelden nadat de pagina is
      geroteerd?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Roteer een PDF‑pagina 180° met Aspose.PDF
og_description: Draai de derde pagina van je PDF snel ondersteboven met een paar regels Aspose.PDF for .NET‑code.
og_image_alt: Gids die code toont die de derde pagina van een PDF 180 graden roteert met Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Roteer een enkele PDF‑pagina 180 graden met Aspose.PDF
In deze tutorial leer je hoe je de derde pagina van een PDF‑document met 180 graden kunt roteren met Aspose.PDF for .NET. Het voorbeeld laat zien hoe je een PDF laadt, pagina 3 selecteert, de rotatie toepast en het bijgewerkte bestand opslaat. Deze aanpak stelt je in staat een specifieke pagina om te draaien zonder de oriëntatie van de overige pagina's te wijzigen.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: Hoe richt ik me op de derde pagina van de PDF voor rotatie?**  
A: Gebruik de paginaverzameling van de SDK met nul‑gebaseerde indexering, bijv. `pdfDocument.Pages[2]`, omdat index 2 overeenkomt met de derde pagina.

**Q: Kan ik een pagina roteren met een andere hoek dan 180 graden?**  
A: De rotatie‑eigenschap accepteert alleen de vier standaardwaarden 0, 90, 180 en 270 graden; elke andere waarde wordt afgerond naar de dichtstbijzijnde toegestane hoek.

**Q: Wijzigt het roteren van de pagina automatisch het originele bestand?**  
A: De rotatie wordt alleen toegepast op het in‑memory `PdfDocument`; je moet `pdfDocument.Save(\"output.pdf\")` (of een vergelijkbare opslaand methode) aanroepen om de wijzigingen naar een nieuw bestand te schrijven, zodat de bron ongewijzigd blijft.

**Q: Wat gebeurt er met annotaties of formuliervelden nadat de pagina is geroteerd?**  
A: De SDK berekent automatisch de posities van annotaties en formuliervelden opnieuw zodat ze correct uitgelijnd blijven met de nieuwe oriëntatie.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}