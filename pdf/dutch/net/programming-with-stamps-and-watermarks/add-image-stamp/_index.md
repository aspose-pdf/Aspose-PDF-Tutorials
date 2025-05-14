---
"description": "Leer hoe u een afbeeldingsstempel toevoegt aan PDF-bestanden met Aspose.PDF voor .NET, met stapsgewijze instructies en voorbeeldcode."
"linktitle": "Afbeeldingsstempel toevoegen aan PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Afbeeldingsstempel toevoegen aan PDF-bestand"
"url": "/nl/net/programming-with-stamps-and-watermarks/add-image-stamp/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Afbeeldingsstempel toevoegen aan PDF-bestand

## Invoering

Als het gaat om het bewerken van PDF-bestanden, zijn er maar weinig tools zo robuust en gebruiksvriendelijk als Aspose.PDF voor .NET. Of u nu aantekeningen wilt toevoegen, formulieren wilt maken of afbeeldingen wilt stempelen, deze bibliotheek biedt uitgebreide functionaliteit om aan diverse PDF-bewerkingsbehoeften te voldoen. In deze tutorial richten we ons op een specifieke taak: het toevoegen van een afbeeldingstempel aan een PDF-bestand. Dit gaat niet alleen over het plakken van een afbeelding op een pagina; het gaat erom uw documenten te verbeteren met branding en visuele aantrekkingskracht!

## Vereisten

Voordat we in de details van de code duiken, moeten we ervoor zorgen dat je alles hebt wat je nodig hebt. Dit heb je nodig:

1. Visual Studio of een .NET IDE: U hebt een .NET-ontwikkelomgeving nodig om de codefragmenten te implementeren.
2. Aspose.PDF voor .NET-bibliotheek: dit is de belangrijkste tool die we zullen gebruiken. U kunt de nieuwste versie van de bibliotheek downloaden van de [Aspose-releasepagina](https://releases.aspose.com/pdf/net/).
3. Basiskennis van C#: Een fundamenteel begrip van C#-programmering helpt u om soepel door de code te navigeren.
4. Een afbeeldingsbestand: Je hebt een afbeeldingsbestand nodig dat je als stempel wilt gebruiken. Zorg ervoor dat het een ondersteund formaat heeft (zoals JPEG, PNG, enz.).
5. Bestaand PDF-bestand: Een voorbeeld-PDF-bestand waar u de afbeeldingsstempel aan toevoegt.

Nu we alles klaar hebben, kunnen we met de code aan de slag!

## Pakketten importeren

Het allerbelangrijkste: voordat je iets doet, moet je de benodigde naamruimten importeren. In je C#-code kun je dit doen door de volgende using -richtlijn bovenaan je bestand toe te voegen:

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using Aspose.Pdf.Text;
```

Hiermee krijgt u toegang tot de verschillende klassen en methoden die de Aspose.PDF-bibliotheek biedt.

## Stap 1: Stel uw documentenmap in

De eerste stap is het specificeren van het pad naar uw documenten. U wilt uw document en de afbeeldingen opslaan in een goed gedefinieerde map. Voor de eenvoud declareert u een variabele `dataDir` zoals dit:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Zorg ervoor dat u vervangt `"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad op uw systeem.

## Stap 2: Open het PDF-document

Vervolgens moeten we het PDF-document openen dat we willen aanpassen. Dit is waar Aspose.PDF in uitblinkt! Je hebt slechts een paar regels code nodig:

```csharp
Document pdfDocument = new Document(dataDir + "AddImageStamp.pdf");
```

Deze regel creëert een nieuwe `Document` object door het opgegeven PDF-bestand te laden. Zorg ervoor dat het bestand in de opgegeven map staat, anders krijg je de foutmelding 'bestand niet gevonden'!

## Stap 3: Maak de afbeeldingenstempel

Nu komt het leuke gedeelte: het toevoegen van de afbeeldingstempel! Eerst moeten we een afbeeldingstempelobject maken met behulp van je afbeeldingsbestand:

```csharp
ImageStamp imageStamp = new ImageStamp(dataDir + "aspose-logo.jpg");
```

Deze regel initialiseert een `ImageStamp` object dat de afbeelding vertegenwoordigt die u wilt toevoegen. Het is cruciaal om te controleren of het pad naar uw afbeelding correct is.

## Stap 4: Configureer de eigenschappen van de afbeeldingstempel

Hier kun je creatief aan de slag gaan en je stempel personaliseren. Je kunt eigenschappen instellen zoals positie, grootte, rotatie en dekking. Hier is een voorbeeld van hoe je dit doet:

```csharp
imageStamp.Background = true; // Stel in op 'true' als u wilt dat de stempel op de achtergrond wordt weergegeven
imageStamp.XIndent = 100; // Positie van links
imageStamp.YIndent = 100; // Positie van bovenaf
imageStamp.Height = 300; // Hoogte van de postzegel instellen
imageStamp.Width = 300; // Breedte van de postzegel instellen
imageStamp.Rotate = Rotation.on270; // Draai indien nodig
imageStamp.Opacity = 0.5; // Dekking instellen
```

U kunt deze waarden naar eigen wens aanpassen! Met deze aanpassing kunt u uw stempel precies daar plaatsen waar u hem wilt.

## Stap 5: Voeg de stempel toe aan een bepaalde pagina

Nu we onze stempel hebben geconfigureerd, is de volgende stap het specificeren waar we hem in het PDF-document willen plaatsen. In dit voorbeeld voegen we hem toe aan de eerste pagina:

```csharp
pdfDocument.Pages[1].AddStamp(imageStamp);
```

Met dit codefragment krijgt Aspose de opdracht om de stempel toe te voegen aan de eerste pagina van het document.

## Stap 6: Sla het document op

Zodra de stempel is aangebracht, is het tijd om je wijzigingen op te slaan. Je moet een pad opgeven voor het PDF-bestand dat als uitvoer dient:

```csharp
dataDir = dataDir + "AddImageStamp_out.pdf";
pdfDocument.Save(dataDir);
```

Uw document is nu opgeslagen met de nieuwe afbeeldingsstempel!

## Stap 7: Bevestig de wijziging

Tot slot is het altijd goed om te bevestigen dat je bewerking succesvol is verlopen. Je kunt dit doen met een eenvoudig consolebericht:

```csharp
Console.WriteLine("\nImage stamp added successfully.\nFile saved at " + dataDir);
```

Met dit bericht krijgt u de melding dat de afbeeldingenstempel is toegevoegd en waar u uw nieuw gewijzigde PDF kunt vinden.

## Conclusie

Gefeliciteerd! Je hebt zojuist een afbeeldingstempel aan een PDF toegevoegd met Aspose.PDF voor .NET. Het lijkt in eerste instantie misschien ingewikkeld, maar met een beetje oefening kun je je PDF-documenten op talloze manieren aanpassen. De sleutel hierbij is experimenteren met de verschillende eigenschappen die Aspose biedt – je fantasie is de limiet.

## Veelgestelde vragen

### Is Aspose.PDF voor .NET gratis te gebruiken?  
Aspose.PDF biedt een gratis proefperiode, maar voor verder gebruik na de proefperiode is een licentie vereist. U kunt de [prijsopties hier](https://purchase.aspose.com/buy).

### Kan ik meerdere stempels aan één PDF toevoegen?  
Absoluut! Je kunt er meerdere maken `ImageStamp` objecten en voeg ze toe aan elke pagina in de PDF.

### Welke afbeeldingsformaten worden voor postzegels ondersteund?  
Aspose.PDF ondersteunt verschillende afbeeldingformaten, waaronder JPEG, PNG en BMP.

### Hoe kan ik een afbeeldingstempel roteren?  
U kunt de `Rotate` eigendom van de `ImageStamp` object om de afbeelding in de gewenste hoek te draaien. Opties zijn onder andere: `Rotation.on90`, `Rotation.on180`, enz.

### Waar kan ik meer documentatie over Aspose.PDF vinden?  
U kunt de volledige API-referentie en documentatie bekijken [hier](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}