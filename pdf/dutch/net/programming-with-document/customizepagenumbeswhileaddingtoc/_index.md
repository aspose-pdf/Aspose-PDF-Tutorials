---
"description": "Leer in deze uitgebreide tutorial hoe u paginanummers kunt aanpassen terwijl u een inhoudsopgave toevoegt aan uw PDF-documenten met Aspose.PDF voor .NET."
"linktitle": "Paginanummers aanpassen tijdens het toevoegen van de inhoudsopgave"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Paginanummers aanpassen tijdens het toevoegen van de inhoudsopgave"
"url": "/nl/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Paginanummers aanpassen tijdens het toevoegen van de inhoudsopgave

## Invoering

PDF's zijn de absolute top in documentbeheer. Ze zijn hét formaat voor het delen en bewaren van documenten op verschillende platforms. Maar wat gebeurt er als u uw PDF-documenten wilt uitbreiden met functies zoals een inhoudsopgave? Dan komt Aspose.PDF voor .NET in beeld! Deze krachtige bibliotheek stelt ontwikkelaars in staat om PDF-bestanden eenvoudig te bewerken, waardoor ze moeiteloos inhoud kunnen toevoegen, wijzigen en aanpassen. In deze tutorial duiken we in hoe u paginanummers kunt aanpassen terwijl u een inhoudsopgave aan uw PDF-documenten toevoegt met Aspose.PDF voor .NET. Dus, pak je programmeerhoed en laten we aan de slag gaan!

## Vereisten

Voordat we met de code aan de slag gaan, zijn er een paar dingen die je moet regelen:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. Dit wordt onze ontwikkelomgeving.
2. Aspose.PDF voor .NET: U moet de Aspose.PDF-bibliotheek downloaden en installeren. U kunt deze vinden [hier](https://releases.aspose.com/pdf/net/).
3. Basiskennis van C#: Kennis van C#-programmering helpt u de codefragmenten beter te begrijpen.
4. Een voorbeeld-PDF-bestand: Zorg dat je een voorbeeld-PDF-bestand bij de hand hebt waarmee we aan de slag kunnen. Je kunt een eenvoudig PDF-bestand maken of een bestaand PDF-bestand downloaden.

## Pakketten importeren

Om te beginnen moeten we de benodigde pakketten importeren. Open je Visual Studio-project en voeg een verwijzing toe naar de Aspose.PDF-bibliotheek. Je kunt dit doen met NuGet Package Manager:

1. Klik met de rechtermuisknop op uw project in Solution Explorer.
2. Selecteer 'NuGet-pakketten beheren'.
3. Zoek naar "Aspose.PDF" en installeer het.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Zodra je de bibliotheek hebt geïnstalleerd, kun je beginnen met coderen!

## Stap 1: Stel uw documentenmap in

Allereerst moeten we onze documentenmap instellen. Dit is waar we onze PDF-invoer- en uitvoerbestanden opslaan. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

Vervang in dit fragment `YOUR DOCUMENT DIRECTORY` met het daadwerkelijke pad waar uw PDF-bestanden zich bevinden. Dit helpt ons om de bestaande PDF te laden en de gewijzigde versie op te slaan.

## Stap 2: Het bestaande PDF-bestand laden

Nu we onze documentenmap hebben ingesteld, kunnen we het bestaande PDF-bestand laden. 

```csharp
Document doc = new Document(inFile);
```

Hier creëren we een nieuwe `Document` object door het invoerbestandspad door te geven. Dit stelt ons in staat om de PDF-inhoud programmatisch te bewerken.

## Stap 3: Een nieuwe pagina voor de inhoudsopgave invoegen

Vervolgens moeten we een nieuwe pagina in ons PDF-bestand maken waar de inhoudsopgave komt te staan.

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

Deze regel voegt een nieuwe pagina aan het begin van het document in. De inhoudsopgave wordt op deze pagina weergegeven.

## Stap 4: Inhoudsopgave-informatie maken

Laten we nu een object maken om de inhoudsopgave-informatie weer te geven.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

In deze stap maken we een `TocInfo` object en geef het de titel "Inhoudsopgave". We passen ook de lettergrootte en -stijl aan. `PageNumbersPrefix` wordt ingesteld op "P", wat het voorvoegsel wordt van de paginanummers in de inhoudsopgave.

## Stap 5: Voeg koppen toe aan de inhoudsopgave

Nu komt het leuke gedeelte! We bladeren door de pagina's van het document en voegen koppen toe aan onze inhoudsopgave.

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

In deze lus maken we een nieuwe `Heading` object voor elke pagina. We stellen de bestemmingspagina voor elke kop in en specificeren de weer te geven tekst, namelijk "Pagina X", waarbij X het paginanummer is. Ten slotte voegen we de kop toe aan de inhoudsopgave.

## Stap 6: Sla het bijgewerkte document op

Nadat u alle benodigde koppen hebt toegevoegd, is het tijd om ons bijgewerkte document op te slaan.

```csharp
doc.Save(outFile);
```

Deze regel slaat de aangepaste PDF op, inclusief de inhoudsopgave. Je kunt nu het uitvoerbestand openen en je aangepaste inhoudsopgave bekijken!

## Conclusie

En voilà! Je hebt met succes paginanummers aangepast terwijl je een inhoudsopgave aan je PDF-document toevoegde met Aspose.PDF voor .NET. Deze krachtige bibliotheek maakt het eenvoudig om PDF-bestanden te bewerken en met slechts een paar regels code kun je je documenten aanzienlijk verbeteren. Of je nu rapporten, e-books of andere PDF-bestanden maakt, een inhoudsopgave kan de navigatie voor je lezers aanzienlijk verbeteren. Dus waar wacht je nog op? Duik in Aspose.PDF en begin vandaag nog met het maken van fantastische PDF's!

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een bibliotheek waarmee ontwikkelaars programmatisch PDF-documenten kunnen maken, bewerken en converteren.

### Kan ik Aspose.PDF gratis gebruiken?
Ja, Aspose biedt een gratis proefversie aan waarmee u de functies van de bibliotheek kunt verkennen. U kunt deze downloaden. [hier](https://releases.aspose.com/).

### Hoe krijg ik ondersteuning voor Aspose.PDF?
kunt ondersteuning krijgen door het Aspose-forum te bezoeken [hier](https://forum.aspose.com/c/pdf/10).

### Is er een tijdelijke licentie beschikbaar?
Ja, u kunt een tijdelijke licentie voor Aspose.PDF aanvragen [hier](https://purchase.aspose.com/temporary-license/).

### Waar kan ik Aspose.PDF voor .NET kopen?
U kunt Aspose.PDF voor .NET kopen [hier](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}