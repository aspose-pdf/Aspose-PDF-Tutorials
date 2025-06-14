---
"description": "Leer hoe u verschillende nummerstijlen (Romeinse cijfers, alfabetisch) kunt toepassen op koppen in een PDF met Aspose.PDF voor .NET met behulp van deze stapsgewijze handleiding."
"linktitle": "Nummerstijl toepassen in PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Nummerstijl toepassen in PDF-bestand"
"url": "/nl/net/programming-with-headings/apply-number-style/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nummerstijl toepassen in PDF-bestand

## Invoering

Heb je ooit mooi genummerde lijsten aan je PDF-documenten moeten toevoegen? Of je nu juridische documenten, rapporten of presentaties opmaakt, correcte nummeringsstijlen zijn essentieel voor het ordenen van informatie. Met Aspose.PDF voor .NET kun je verschillende nummeringsstijlen toepassen op de koppen van je PDF-bestand, waardoor je goed gestructureerde en professionele documenten creëert. 

## Vereisten

Voordat we beginnen met coderen, leggen we eerst uit wat je nodig hebt:

1. Aspose.PDF voor .NET: Download de nieuwste versie van Aspose.PDF van [hier](https://releases.aspose.com/pdf/net/).
2. Ontwikkelomgeving: Zorg ervoor dat u Visual Studio of een andere .NET-compatibele IDE hebt.
3. .NET Framework: Zorg ervoor dat u .NET Framework 4.0 of hoger hebt geïnstalleerd.
4. Licentie: U kunt een tijdelijke licentie gebruiken van [hier](https://purchase.aspose.com/temporary-license/) of verken de [gratis proefperiode](https://releases.aspose.com/) opties.

## Pakketten importeren

Om te beginnen moet u ervoor zorgen dat de volgende naamruimten in uw project zijn geïmporteerd:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## Stap 1: Het document instellen

Laten we beginnen met het maken van een nieuw PDF-document en het configureren van de pagina-instellingen. We stellen de paginagrootte en marges in om de lay-out van onze content te bepalen.

Uitleg: In deze stap stellen we de basisstructuur van de PDF in. Dit houdt in dat we de paginagrootte, hoogte en marges definiëren voor een consistente opmaak.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDoc = new Document();

// Pagina-afmetingen en marges instellen
pdfDoc.PageInfo.Width = 612.0;
pdfDoc.PageInfo.Height = 792.0;
pdfDoc.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfDoc.PageInfo.Margin.Left = 72;
pdfDoc.PageInfo.Margin.Right = 72;
pdfDoc.PageInfo.Margin.Top = 72;
pdfDoc.PageInfo.Margin.Bottom = 72;
```

Als u dit doet, krijgt uw document een standaardpaginaformaat, gelijk aan een pagina van 8,5 x 11 inch, en een marge van 72 punten (of 1 inch) aan alle kanten.

## Stap 2: Een pagina toevoegen aan de PDF

Vervolgens voegen we een nieuwe pagina toe aan het PDF-document, waar we later de nummeringsstijlen op toepassen.

Uitleg: Elke PDF heeft pagina's nodig! Met deze stap wordt een lege pagina aan de PDF toegevoegd en worden de marges aangepast aan de instellingen op documentniveau.

```csharp
// Een nieuwe pagina toevoegen aan het PDF-document
Aspose.Pdf.Page pdfPage = pdfDoc.Pages.Add();
pdfPage.PageInfo.Width = 612.0;
pdfPage.PageInfo.Height = 792.0;
pdfPage.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfPage.PageInfo.Margin.Left = 72;
pdfPage.PageInfo.Margin.Right = 72;
pdfPage.PageInfo.Margin.Top = 72;
pdfPage.PageInfo.Margin.Bottom = 72;
```

## Stap 3: Maak een zwevende doos

Met een FloatingBox kun je content (zoals tekst of koppen) in een vak plaatsen dat zich onafhankelijk van de paginastroom gedraagt. Dit is handig wanneer je volledige controle wilt over de lay-out van je content.

Uitleg: Hier stellen we een FloatingBox in die de koppen bevat waarop de nummerstijlen worden toegepast.

```csharp
// Maak een FloatingBox voor gestructureerde inhoud
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox();
floatBox.Margin = pdfPage.PageInfo.Margin;
pdfPage.Paragraphs.Add(floatBox);
```

## Stap 4: Voeg de eerste kop met Romeinse cijfers toe

Nu komt het spannende gedeelte! Laten we de eerste kop met kleine Romeinse cijfers toevoegen.

Uitleg: We passen de stijl NumberingStyle.NumeralsRomanLowercase toe op de koptekst, waardoor de nummering in Romeinse cijfers wordt weergegeven (i, ii, iii, enz.).

```csharp
// Maak de eerste kop met Romeinse cijfers
Aspose.Pdf.Heading heading = new Aspose.Pdf.Heading(1);
heading.IsInList = true;
heading.StartNumber = 1;
heading.Text = "List 1";
heading.Style = NumberingStyle.NumeralsRomanLowercase;
heading.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading);
```

## Stap 5: Voeg een tweede Romeinse cijferkop toe

Ter illustratie voegen we een tweede Romeins cijfer toe, maar deze keer beginnen we bij 13.

Uitleg: Met de eigenschap StartNumber kunt u de nummering laten beginnen bij een aangepast nummer. In dit geval beginnen we bij 13.

```csharp
// Maak een tweede kop, beginnend bij het Romeinse cijfer 13
Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
heading2.IsInList = true;
heading2.StartNumber = 13;
heading2.Text = "List 2";
heading2.Style = NumberingStyle.NumeralsRomanLowercase;
heading2.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading2);
```

## Stap 6: Voeg een kop met alfabetische nummering toe

Voor de afwisseling voegen we een derde kopje toe, maar dit keer gebruiken we alfabetische nummering in kleine letters (a, b, c, etc.).

Uitleg: Door de nummeringsstijl te wijzigen naar LettersLowercase kunnen we alfabetische nummering op onze koppen toepassen.

```csharp
// Maak een kop met alfabetische nummering
Aspose.Pdf.Heading heading3 = new Aspose.Pdf.Heading(2);
heading3.IsInList = true;
heading3.StartNumber = 1;
heading3.Text = "the value, as of the effective date of the plan, of property to be distributed under the plan on account of each allowed";
heading3.Style = NumberingStyle.LettersLowercase;
heading3.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading3);
```

## Stap 7: De PDF opslaan

Nadat u alle koppen en nummerstijlen hebt toegepast, slaat u het PDF-bestand op in de gewenste map.

Uitleg: Met deze stap wordt het PDF-bestand met alle opgemaakte koppen met toegepaste nummeringsstijlen opgeslagen.

```csharp
// Sla het PDF-document op
dataDir = dataDir + "ApplyNumberStyle_out.pdf";
pdfDoc.Save(dataDir);
Console.WriteLine("\nNumber style applied successfully in headings.\nFile saved at " + dataDir);
```

## Conclusie

En voilà! Je hebt met succes nummeringsstijlen – Romeinse cijfers en alfabetische cijfers – toegepast op koppen in een PDF-bestand met Aspose.PDF voor .NET. De flexibiliteit die Aspose.PDF biedt voor het beheren van de pagina-indeling, nummeringsstijlen en de positionering van de inhoud, biedt je een krachtige toolset voor het maken van overzichtelijke, professionele PDF-documenten.

## Veelgestelde vragen

### Kan ik verschillende nummerstijlen op hetzelfde PDF-document toepassen?  
Ja, met Aspose.PDF voor .NET kunt u verschillende nummeringsstijlen, zoals Romeinse cijfers, Arabische cijfers en alfabetische nummering, in hetzelfde document gebruiken.

### Hoe kan ik het startnummer voor koppen aanpassen?  
U kunt het startnummer voor elke kop instellen met behulp van de `StartNumber` eigendom.

### Is er een manier om de nummering opnieuw in te stellen?  
Ja, u kunt de nummering opnieuw instellen door de `StartNumber` eigenschap voor elke kop.

### Kan ik naast nummering ook vetgedrukte of cursieve opmaak op koppen toepassen?  
Absoluut! U kunt koptekststijlen aanpassen door eigenschappen zoals lettertype, grootte, vet en cursief te wijzigen met behulp van de `TextState` voorwerp.

### Hoe krijg ik een tijdelijke licentie voor Aspose.PDF?  
U kunt een tijdelijke vergunning verkrijgen bij [hier](https://purchase.aspose.com/temporary-license/) om Aspose.PDF zonder beperkingen te testen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}