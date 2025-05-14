---
"description": "Leer hoe u eenvoudig tekst toevoegt aan de voettekst van een PDF-bestand met Aspose.PDF voor .NET. Inclusief stapsgewijze handleiding voor naadloze integratie."
"linktitle": "Tekst in voettekst van PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Tekst in voettekst van PDF-bestand"
"url": "/nl/net/programming-with-stamps-and-watermarks/text-in-footer/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tekst in voettekst van PDF-bestand

## Invoering

Wilt u aangepaste tekst toevoegen aan de voettekst van een PDF-bestand met Aspose.PDF voor .NET? Dan bent u hier aan het juiste adres! Of u nu paginanummers, datums of andere aangepaste tekst wilt toevoegen, deze tutorial leidt u door het hele proces. Met Aspose.PDF, een robuuste bibliotheek voor PDF-bewerking, is het toevoegen van een voettekst ongelooflijk eenvoudig. In dit artikel bekijken we het stapsgewijze proces om tekst toe te voegen aan de voettekst van elke pagina in uw PDF-bestand. Het is snel, eenvoudig en perfect voor iedereen die PDF-aanpassingen in hun .NET-applicaties wil automatiseren.


## Vereisten

Voordat we met coderen beginnen, willen we ervoor zorgen dat je alles klaar hebt:

- Aspose.PDF voor .NET: Zorg ervoor dat Aspose.PDF voor .NET geïnstalleerd is. Zo niet, dan kunt u [download het hier](https://releases.aspose.com/pdf/net/).
- IDE: Je hebt een ontwikkelomgeving nodig zoals Visual Studio.
- Basiskennis van C#: Basiskennis van C# en .NET is vereist.
- Licentie: Hoewel u Aspose.PDF in de evaluatiemodus kunt gebruiken, kunt u voor volledige functionaliteit overwegen een [gratis proefperiode](https://releases.aspose.com/) of een aanvraag indienen voor een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/).

## Pakketten importeren

Voordat we beginnen met coderen, moet u ervoor zorgen dat u de benodigde naamruimten importeert. Dit zorgt ervoor dat de klassen en methoden uit de Aspose.PDF-bibliotheek beschikbaar zijn in uw project.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Nu u klaar bent, gaan we het proces voor het toevoegen van tekst aan de voettekst van een PDF-bestand opsplitsen in eenvoudig te volgen stappen.

## Stap 1: Initialiseer uw project en stel de documentmap in

Voordat u met uw PDF-bestanden kunt werken, moet u het pad naar uw documentenmap opgeven. Dit is waar uw PDF-bestand zich bevindt en waar het gewijzigde bestand wordt opgeslagen.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Hier vervangen `"YOUR DOCUMENT DIRECTORY"` met het daadwerkelijke pad naar uw map. Deze map bevat het originele PDF-bestand en dient tevens als uitvoerlocatie voor het gewijzigde bestand.

## Stap 2: Het PDF-document laden

De volgende stap is het laden van het PDF-bestand in uw project. `Document` klasse van Aspose.PDF kunt u bestaande PDF-documenten openen en bewerken.

```csharp
// Document openen
Document pdfDocument = new Document(dataDir + "TextinFooter.pdf");
```

Hier, `TextinFooter.pdf` is het bestand waarmee we werken. U kunt dit vervangen door uw eigen bestandsnaam.

## Stap 3: De voettekst maken

Laten we nu de voettekst maken die op elke pagina wordt gestempeld. Dit doen we met behulp van de `TextStamp` klasse. De tekst die u definieert, wordt gebruikt als voettekst voor alle pagina's.

```csharp
// Voettekst maken
TextStamp textStamp = new TextStamp("Footer Text");
```

In dit geval hebben we een eenvoudige voettekst gemaakt met de tekst "Voettekst". U kunt deze gerust aanpassen met uw eigen tekst. Bijvoorbeeld "Vertrouwelijk" of een paginanummer, als u dat wilt.

## Stap 4: Voetteksteigenschappen instellen

Om de voettekst correct te positioneren, moeten we enkele eigenschappen aanpassen, zoals marges, uitlijning en positionering. `TextStamp` Met de klasse hebt u volledige controle over waar en hoe de voettekst wordt weergegeven.

```csharp
// Eigenschappen van de postzegel instellen
textStamp.BottomMargin = 10;
textStamp.HorizontalAlignment = HorizontalAlignment.Center;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

Hier hebben we de ondermarge ingesteld op 10 eenheden, de tekst horizontaal gecentreerd en verticaal onderaan de pagina geplaatst. U kunt deze waarden aanpassen aan uw specifieke lay-outbehoeften.

## Stap 5: Voettekst op alle pagina's toepassen

Nu komt het leukste gedeelte: de voettekst op elke pagina in de PDF toepassen. Door over alle pagina's in het document te itereren, kunnen we de voettekst aan elke pagina toevoegen.

```csharp
// Voettekst toevoegen op alle pagina's
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(textStamp);
}
```

Deze lus zorgt ervoor dat de voettekst op alle pagina's van het document wordt gestempeld, ongeacht het aantal pagina's van het PDF-bestand.

## Stap 6: Sla het bijgewerkte PDF-bestand op

Nadat u de voettekst aan alle pagina's hebt toegevoegd, slaat u als laatste het gewijzigde PDF-bestand op in de opgegeven map.

```csharp
dataDir = dataDir + "TextinFooter_out.pdf";
// Bijgewerkt PDF-bestand opslaan
pdfDocument.Save(dataDir);
```

We slaan het bestand op met een nieuwe naam, `TextinFooter_out.pdf`, in dezelfde map. U kunt de naam ervan naar wens wijzigen.

## Stap 7: Bevestig succes

Ten slotte kunt u een succesbericht op de console afdrukken, zodat de gebruiker weet dat de PDF succesvol is bijgewerkt.

```csharp
Console.WriteLine("\nText in footer added successfully.\nFile saved at " + dataDir);
```

En dat is alles! Je hebt succesvol tekst toegevoegd aan de voettekst van elke pagina in je PDF.

## Conclusie

Het toevoegen van een voettekst aan een PDF-document met Aspose.PDF voor .NET is een eenvoudige en krachtige manier om uw PDF-bestanden te personaliseren. Met slechts een paar regels code kunt u gepersonaliseerde tekst, zoals datums, titels of paginanummers, aan elke pagina in het document toevoegen. Door deze handleiding te volgen, beschikt u nu over de kennis om deze functionaliteit in uw .NET-applicaties te implementeren.

## Veelgestelde vragen

### Kan ik aan elke pagina in het PDF-bestand een andere voettekst toevoegen?  
Ja, u kunt unieke voetteksten aan elke pagina toevoegen door verschillende voetteksten op te geven `TextStamp` objecten voor elke pagina.

### Hoe verander ik het lettertype van de voettekst?  
U kunt de tekst aanpassen met behulp van de `TextStamp.TextState` Eigenschap om lettertype, grootte en kleur in te stellen.

### Kan ik afbeeldingen in de voettekst toevoegen in plaats van tekst?  
Ja, je kunt gebruiken `ImageStamp` om afbeeldingen toe te voegen aan de voettekst van een PDF-bestand.

### Is het mogelijk om een voettekst alleen aan specifieke pagina's toe te voegen?  
Absoluut! U kunt de paginanummers specificeren waar u de voettekst wilt hebben door specifieke `Page` objecten.

### Hoe kan ik een bestaande voettekst uit een PDF verwijderen?  
U kunt bestaande postzegels wissen met behulp van de `Page.DeleteStampById` methode of door gebruik te maken van `RemoveStamp` om alle postzegels te verwijderen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}