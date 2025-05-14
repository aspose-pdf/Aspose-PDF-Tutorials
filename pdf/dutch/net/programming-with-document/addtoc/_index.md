---
"description": "Leer hoe u een inhoudsopgave aan een PDF toevoegt met Aspose.PDF voor .NET. Deze stapsgewijze handleiding vereenvoudigt het proces en zorgt voor eenvoudige navigatie in uw documenten."
"linktitle": "Inhoudsopgave toevoegen aan PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Inhoudsopgave toevoegen aan PDF-bestand"
"url": "/nl/net/programming-with-document/addtoc/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Inhoudsopgave toevoegen aan PDF-bestand

## Invoering

Heb je ooit eindeloos door een lange PDF gescrold en gewenst dat er een overzichtelijke inhoudsopgave in zat? Nou, vandaag is je geluksdag! In deze tutorial leer je hoe je een inhoudsopgave aan je PDF-bestand toevoegt met Aspose.PDF voor .NET. Of je nu werkt aan een complex rapport, een e-book of een zakelijk voorstel, een inhoudsopgave kan je document omtoveren tot een professioneel, navigeerbaar meesterwerk.

## Vereisten

Voordat we in de code duiken, controleren we of je alles hebt wat je nodig hebt:

1. Aspose.PDF voor .NET: Zorg ervoor dat je de Aspose.PDF-bibliotheek hebt gedownload en geïnstalleerd. Je kunt deze downloaden van [hier](https://releases.aspose.com/pdf/net/).
   
2. Ontwikkelomgeving: Zorg ervoor dat u een .NET-ontwikkelomgeving zoals Visual Studio op uw computer hebt ingesteld.

3. Licentie: Als u geen licentie hebt, kunt u een gratis proefversie krijgen of een tijdelijke licentie aanvragen [hier](https://purchase.aspose.com/temporary-license/).

## Pakketten importeren

Om te beginnen, zorg ervoor dat u de benodigde naamruimten aan het begin van uw codebestand importeert. Zo doet u dat:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Met deze naamruimten krijgt u toegang tot PDF-specifieke functionaliteiten en kunt u tekstelementen in uw document bewerken.

Laten we deze taak opsplitsen in kleine stapjes. Elke stap begeleidt je door het proces van het maken en invoegen van een inhoudsopgave in je PDF-document.

## Stap 1: Het PDF-document laden

Het eerste dat we moeten doen, is het bestaande PDF-bestand laden waaraan we de inhoudsopgave willen toevoegen.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "AddTOC.pdf");
```

In deze stap geven we het pad naar de documentenmap op en laden we de PDF met behulp van de `Document` object. Zorg ervoor dat u het vervangt `"YOUR DOCUMENT DIRECTORY"` met het daadwerkelijke pad naar uw bestand.

## Stap 2: Een nieuwe pagina invoegen voor de inhoudsopgave

Vervolgens voegen we een nieuwe pagina toe aan het begin van het PDF-document. Deze pagina zal de inhoudsopgave bevatten.

```csharp
Page tocPage = doc.Pages.Insert(1);
```

Door de inhoudsopgavepagina aan het begin te plaatsen, zorgen we ervoor dat deze het allereerste is wat lezers in de PDF zien.

## Stap 3: Een TOC-informatieobject maken

Laten we nu een object maken dat de inhoudsopgave-informatie vertegenwoordigt. We voegen ook een titel toe aan de inhoudsopgave om deze te laten opvallen.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

Hier hebben we de titel van de inhoudsopgave ingesteld op 'Inhoudsopgave', het lettertype vergroot en de tekst vetgedrukt gemaakt om deze te benadrukken.

## Stap 4: Definieer TOC-elementen

In deze stap definiëren we de elementen (of koppen) die in de inhoudsopgave worden weergegeven. Deze elementen helpen lezers navigeren naar specifieke secties in het document.

```csharp
string[] titles = new string[4];
titles[0] = "First page";
titles[1] = "Second page";
titles[2] = "Third page";
titles[3] = "Fourth page";
```

We hebben een reeks strings gemaakt die als inhoudsopgave-items dienen en die overeenkomen met de verschillende pagina's in de PDF.

## Stap 5: Inhoudsopgavekoppen maken

Nu komt het cruciale onderdeel: het toevoegen van koppen aan de inhoudsopgave en het koppelen ervan aan de bijbehorende pagina's.

```csharp
for (int i = 0; i < 2; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);

    heading2.DestinationPage = doc.Pages[i + 2];
    heading2.Top = doc.Pages[i + 2].Rect.Height;
    segment2.Text = titles[i];

    tocPage.Paragraphs.Add(heading2);
}
```

Dit is wat er gebeurt:
- Kop: Wij creëren een `Heading` object en voeg een toe `TextSegment` ernaartoe.
- Bestemmingspagina: Wij stellen de pagina in waarnaar elke koptekst zal linken.
- Bovenste positie: Wij specificeren de positie op de pagina waar de koptekst naar zal verwijzen.
- Tekst: Elke kop krijgt een bijbehorende titel uit de matrix die we eerder hebben gemaakt.

Deze lus maakt koppen voor de eerste twee elementen in de inhoudsopgave en koppelt ze aan de bijbehorende pagina's.

## Stap 6: Sla de PDF op met de inhoudsopgave

Nadat we alle elementen van de inhoudsopgave hebben toegevoegd, is het tijd om de bijgewerkte PDF op te slaan.

```csharp
dataDir = dataDir + "TOC_out.pdf";
doc.Save(dataDir);
```

Het bestand is nu opgeslagen met de inhoudsopgave toegevoegd aan de PDF. Gefeliciteerd, je hebt met succes een inhoudsopgave toegevoegd!

## Stap 7: Bevestigingsbericht

Om de gebruiker te laten weten dat het proces voltooid is, tonen we een eenvoudig bericht in de console.

```csharp
Console.WriteLine("\nTOC added successfully to an existing PDF.\nFile saved at " + dataDir);
```

## Conclusie

En voilà! Met Aspose.PDF voor .NET is het toevoegen van een inhoudsopgave aan een PDF niet alleen eenvoudig, maar ook aanpasbaar. Of u nu eenvoudige navigatielinks of complexe structuren wilt maken, deze tool helpt u daarbij. Dus vergeet de volgende keer dat u aan een lange PDF werkt niet een inhoudsopgave toe te voegen voor een professionele touch!

## Veelgestelde vragen

### Kan ik het uiterlijk van de inhoudsopgave in Aspose.PDF aanpassen?  
Ja, u kunt het uiterlijk van de inhoudsopgave volledig aanpassen, inclusief het lettertype, de grootte en de uitlijning.

### Hoe voeg ik subkoppen toe aan de inhoudsopgave?  
U kunt subkoppen toevoegen door de `Heading` niveau (bijv. `Heading(2)`) om een hiërarchische inhoudsopgave te maken.

### Is het mogelijk om de inhoudsopgave automatisch bij te werken als het document verandert?  
Nee, de inhoudsopgave wordt niet automatisch bijgewerkt. U moet deze opnieuw maken als de documentstructuur verandert.

### Kan ik TOC-vermeldingen koppelen aan externe documenten?  
Ja, u kunt hyperlinks gebruiken om inhoudsopgave-items te koppelen aan externe PDF's of URL's.

### Ondersteunt Aspose.PDF inhoudsopgaven met meerdere niveaus?  
Ja, Aspose.PDF ondersteunt inhoudsopgaven op meerdere niveaus voor complexe documenten met subsecties.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}