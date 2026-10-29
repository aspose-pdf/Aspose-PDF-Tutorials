---
title: Draai elke PDF-pagina 180° met Aspose.Pdf voor .NET
weight: 260
limit:
description: Stapsgewijze gids om alle pagina's van een PDF 180 graden te draaien met Aspose.Pdf voor .NET.
keywords: [rotate pdf pages .net, Aspose.Pdf for .NET, rotate all pages 180 degrees, pdf page rotation, c# pdf manipulation]
url: /net/programming-with-pdf-pages/rotate-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Stapsgewijze gids om alle pagina's van een PDF 180 graden te draaien
    met Aspose.Pdf voor .NET.
  headline: Draai elke PDF-pagina 180° met Aspose.Pdf voor .NET
  type: TechArticle
- description: Stapsgewijze gids om alle pagina's van een PDF 180 graden te draaien
    met Aspose.Pdf voor .NET.
  name: Draai elke PDF-pagina 180° met Aspose.Pdf voor .NET
  steps:
  - name: Declareer de bron- en bestemmingsbestandspaden voor de PDF.
    text: Declareer de bron- en bestemmingsbestandspaden voor de PDF.
  - name: Controleer of het bronbestand bestaat en annuleer met een foutmelding als
      dat niet het geval is.
    text: Controleer of het bronbestand bestaat en annuleer met een foutmelding als
      dat niet het geval is.
  - name: Maak een Document-object voor de bron-PDF aan binnen een using-blok om resources
      te beheren.
    text: Maak een Document-object voor de bron-PDF aan binnen een using-blok om resources
      te beheren.
  - name: Itereer door elke Page in pdfDoc.Pages en stel de Rotate‑eigenschap in op
      Rotation.on180, waardoor elke pagina ondersteboven wordt gedraaid.
    text: Itereer door elke Page in pdfDoc.Pages en stel de Rotate‑eigenschap in op
      Rotation.on180, waardoor elke pagina ondersteboven wordt gedraaid.
  - name: Sla het gewijzigde Document op naar het bestemmingsbestand, waarbij de rotaties
      worden bewaard.
    text: Sla het gewijzigde Document op naar het bestemmingsbestand, waarbij de rotaties
      worden bewaard.
  - name: Schrijf een bevestigingsbericht naar de console dat aangeeft dat de bewerking
      is voltooid.
    text: Schrijf een bevestigingsbericht naar de console dat aangeeft dat de bewerking
      is voltooid.
  type: HowTo
- questions:
  - answer: De code controleert `File.Exists(sourceFile)` en schrijft een fout naar
      `Console.Error` voordat hij terugkeert, zodat er geen uitzondering wordt gegooid
      en het programma netjes afsluit.
    question: Wat gebeurt er als het bron‑PDF‑bestand niet bestaat?
  - answer: Ja, vervang `Rotation.on180` door een andere enum‑waarde zoals `Rotation.on90`
      (met de klok mee) of `Rotation.on270` (tegen de klok in) om een andere rotatie
      toe te passen.
    question: Kan ik de pagina's met een andere hoek draaien, bijv. 90° met de klok
      mee?
  - answer: De `Pages`‑collectie van Aspose.Pdf is 1‑gebaseerd, maar de `foreach`‑iterator
      verbergt dat, en itereert over elk `Page`‑object ongeacht de onderliggende index.
    question: Is de paginacollectie nul‑gebaseerd? Hoe werkt de `foreach`‑lus?
  - answer: Het aanroepen van `pdfDoc.Save(destinationFile)` zal elk bestaand bestand
      met die naam overschrijven, dus gebruik een andere bestandsnaam of maak een
      back‑up van het origineel als je het wilt behouden.
    question: Wordt de originele PDF overschreven als ik dezelfde bestandsnaam gebruik
      voor `destinationFile`?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pages/og-image.png
og_title: Draai elke PDF-pagina 180°
og_description: Leer hoe je alle pagina's van een PDF ondersteboven kunt draaien met slechts een paar regels C#‑code.
og_image_alt: Gids die laat zien hoe je elke pagina van een PDF met 180 graden draait met Aspose.Pdf voor .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Draai elke PDF-pagina 180° met Aspose.Pdf voor .NET
Deze tutorial laat zien hoe je elke pagina van een bestaande PDF‑document met 180 graden kunt roteren met de Aspose.Pdf Document-klasse. Door een volledige paginaverdraaiing toe te passen kun je snel ondersteboven scans corrigeren of documenten opnieuw oriënteren zonder ze opnieuw te maken. Het voorbeeld is geschreven in C# en werkt op het .NET‑platform.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pages" >}}


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

**Q: Wat gebeurt er als het bron‑PDF‑bestand niet bestaat?**  
A: De code controleert `File.Exists(sourceFile)` en schrijft een fout naar `Console.Error` voordat hij terugkeert, zodat er geen uitzondering wordt gegooid en het programma netjes afsluit.

**Q: Kan ik de pagina's met een andere hoek draaien, bijv. 90° met de klok mee?**  
A: Ja, vervang `Rotation.on180` door een andere enum‑waarde zoals `Rotation.on90` (met de klok mee) of `Rotation.on270` (tegen de klok in) om een andere rotatie toe te passen.

**Q: Is de paginacollectie nul‑gebaseerd? Hoe werkt de `foreach`‑lus?**  
A: De `Pages`‑collectie van Aspose.Pdf is 1‑gebaseerd, maar de `foreach`‑iterator verbergt dat, en itereert over elk `Page`‑object ongeacht de onderliggende index.

**Q: Wordt de originele PDF overschreven als ik dezelfde bestandsnaam gebruik voor `destinationFile`?**  
A: Het aanroepen van `pdfDoc.Save(destinationFile)` zal elk bestaand bestand met die naam overschrijven, dus gebruik een andere bestandsnaam of maak een back‑up van het origineel als je het wilt behouden.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}