---
"description": "Leer met behulp van onze stapsgewijze handleiding hoe u een tekststempel toevoegt aan een PDF-bestand met Aspose.PDF voor .NET en verbeter de presentatie van uw documenten."
"linktitle": "Tekststempel toevoegen in PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Tekststempel toevoegen in PDF-bestand"
"url": "/nl/net/programming-with-stamps-and-watermarks/add-text-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tekststempel toevoegen in PDF-bestand

## Invoering

In het digitale tijdperk van vandaag zijn pdf's een veelgebruikt formaat voor het delen en verspreiden van documenten. Of je nu een ontwikkelaar, content creator of gewoon iemand bent die zijn pdf-bestanden wil verbeteren, kennis van het programmatisch bewerken van pdf's kan een enorme vooruitgang betekenen. Een handige functie die je misschien wilt gebruiken, is de mogelijkheid om tekststempels toe te voegen aan je pdf-bestanden. Het toevoegen van een tekststempel kan je documenten een professionele uitstraling geven of belangrijke informatie overbrengen, zoals 'Voorbeeld', 'Vertrouwelijk' of zelfs een watermerk.

## Vereisten

Voordat we de code induiken, zijn er een paar vereisten om ervoor te zorgen dat alles correct is ingesteld. Dit is wat je nodig hebt:

1. Aspose.PDF voor .NET: Zorg ervoor dat de Aspose.PDF-bibliotheek in uw project is geïnstalleerd. Als u dit nog niet hebt gedaan, kunt u deze downloaden van de website. [Aspose-website](https://releases.aspose.com/pdf/net/).
2. Visual Studio of compatibele IDE: U hebt een ontwikkelomgeving nodig om uw .NET-code te schrijven en uit te voeren. Visual Studio is de meest voorkomende keuze onder ontwikkelaars.
3. Basiskennis van C#: Kennis van C# en de principes van objectgeoriënteerd programmeren helpt u de voorbeelden beter te begrijpen.
4. Voorbeeld PDF-bestand: U dient een PDF-bestand bij de hand te hebben. U kunt een eenvoudige PDF maken of een bestaande PDF gebruiken om de functionaliteit te testen.

Zodra je aan deze voorwaarden hebt voldaan, kunnen we verder met coderen!

## Pakketten importeren

Laten we nu de benodigde pakketten importeren. Deze stap is cruciaal omdat het de klassen en methoden uit de Aspose-bibliotheek beschikbaar maakt in je project.

### Aspose.PDF-assemblage importeren

Om te beginnen moet je de Aspose.PDF-naamruimte importeren. Voeg bovenaan je C#-bestand de volgende using-richtlijn toe:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Hiermee krijgt u toegang tot klassen die essentieel zijn voor het maken en bewerken van PDF-documenten.

Laten we nu naar de kern van de tutorial gaan. We zullen het proces opsplitsen in duidelijke en beknopte stappen. Elke stap leidt je door de code om een tekststempel aan een PDF-bestand toe te voegen.

## Stap 1: De documentenmap instellen

Eerst moet je de map bepalen waar je PDF-document is opgeslagen. Dit betekent dat je code moet weten waar het PDF-bestand dat je wilt bewerken zich bevindt.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Uitleg: Vervangen `"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad waar uw PDF-bestand (`AddTextStamp.pdf`) wordt opgeslagen. Dit pad wordt later gebruikt om de gewijzigde PDF te openen en op te slaan.

## Stap 2: Open het PDF-document

Vervolgens openen we het PDF-document met behulp van de `Document` klasse uit de Aspose.PDF-naamruimte.

```csharp
// Document openen
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

Uitleg: Hier maken we een instantie van de `Document` klasse en het pad naar ons PDF-bestand doorgeven. Dit laadt het PDF-bestand zodat we het kunnen bewerken.

## Stap 3: Een tekststempel maken

Nu gaan we een tekststempel maken die we later op ons PDF-document toepassen.

```csharp
// Tekststempel maken
TextStamp textStamp = new TextStamp("Sample Stamp");
```

Uitleg: De `TextStamp` Het object wordt gemaakt met de tekst die u wilt weergeven. In dit geval gebruiken we "Voorbeeldstempel" als tekst voor onze stempel.

## Stap 4: Stempeleigenschappen instellen

Om je stempel te personaliseren, kunnen we verschillende eigenschappen instellen, zoals achtergrondkleur, positie en rotatie. Laten we dat nu doen:

```csharp
// Instellen of stempel achtergrond is
textStamp.Background = true;

// Oorsprong instellen
textStamp.XIndent = 100;
textStamp.YIndent = 100;

// Draai stempel
textStamp.Rotate = Rotation.on90;
```

Uitleg:
- Achtergrond: Als u dit instelt op `true` betekent dat de stempel achter de inhoud van het PDF-bestand wordt weergegeven.
- XIndent & YIndent: Deze eigenschappen bepalen de positie van de postzegel op de pagina. In dit voorbeeld wordt de postzegel 100 eenheden vanaf de linker- en bovenrand van de pagina geplaatst.
- Roteren: Hiermee roteert u de stempel 90 graden. U kunt verschillende rotatieopties kiezen op basis van uw ontwerpvereisten.

## Stap 5: Teksteigenschappen aanpassen

Laten we nu creatief aan de slag gaan en het uiterlijk van de tekst op onze stempel aanpassen:

```csharp
// Teksteigenschappen instellen
textStamp.TextState.Font = FontRepository.FindFont("Arial");
textStamp.TextState.FontSize = 14.0F;
textStamp.TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
textStamp.TextState.ForegroundColor = Aspose.Pdf.Color.FromRgb(Color.Aqua);
```

Uitleg:
- Lettertype: We gebruiken het Arial-lettertype en maken het vet en cursief.
- Lettergrootte: Deze is ingesteld op 14 punten.
- Voorgrondkleur: Gebruik RGB om de tekstkleur in te stellen op Aqua. U kunt de kleur gerust aanpassen aan uw merk- of ontwerpbehoeften!

## Stap 6: Voeg een stempel toe aan de PDF-pagina

Nu is het tijd om de stempel aan een specifieke pagina van het PDF-document toe te voegen.

```csharp
// Voeg een stempel toe aan een bepaalde pagina
pdfDocument.Pages[1].AddStamp(textStamp);
```

Uitleg: In dit voorbeeld wordt de stempel toegevoegd aan de eerste pagina van de PDF (pagina's zijn 1-geïndexeerd). Pas het paginanummer indien nodig aan voor uw document.

## Stap 7: Sla de gewijzigde PDF op

Ten slotte slaan we het document op met het nieuw toegevoegde tekststempel.

```csharp
dataDir = dataDir + "AddTextStamp_out.pdf";

// Uitvoerdocument opslaan
pdfDocument.Save(dataDir);
Console.WriteLine("\nText stamp added successfully.\nFile saved at " + dataDir);
```

Uitleg: We definiëren een nieuw pad voor het uitvoerbestand en slaan vervolgens het gewijzigde document op. Na het opslaan wordt het pad weergegeven op de console, wat de succesvolle bewerking bevestigt.

## Conclusie

Gefeliciteerd! U hebt met succes een tekststempel aan een PDF-bestand toegevoegd met Aspose.PDF voor .NET. Met deze methode kunt u uw documenten efficiënt annoteren, wat zowel de professionaliteit als de bruikbaarheid ervan verbetert. Of u nu watermerken, handtekeningen of eenvoudige notities toevoegt, de Aspose-bibliotheek biedt krachtige tools om uw PDF's eenvoudig te bewerken.

## Veelgestelde vragen

### Wat is een tekststempel in een PDF?
Een tekststempel is een grafische overlay met tekst die op een PDF-document kan worden geplaatst. Deze overlay wordt vaak gebruikt voor aantekeningen of watermerken.

### Kan ik de postzegel personaliseren met afbeeldingen?
Ja, Aspose.PDF ondersteunt ook het toevoegen van afbeeldingsstempels, wat zorgt voor meer flexibiliteit in het ontwerp.

### Welke programmeertalen kan ik gebruiken met Aspose.PDF?
Aspose.PDF is primair gericht op .NET, maar er zijn versies beschikbaar voor andere talen, zoals Java en Python.

### Hoe krijg ik een tijdelijke licentie voor Aspose.PDF?
U kunt een tijdelijke vergunning aanvragen door naar de website te gaan [aankooplink](https://purchase.aspose.com/temporary-license/) op hun website.

### Waar kan ik ondersteuning vinden voor Aspose.PDF?
Ondersteuning voor Aspose.PDF is beschikbaar op hun [ondersteuningsforum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}