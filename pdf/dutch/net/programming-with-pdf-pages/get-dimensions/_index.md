---
"description": "In deze tutorial leggen we uit hoe je PDF-pagina-afmetingen kunt bepalen en bewerken met Aspose.PDF voor .NET. Gedetailleerde stappen leiden je door het proces."
"linktitle": "PDF-pagina-afmetingen ophalen"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "PDF-pagina-afmetingen ophalen"
"url": "/nl/net/programming-with-pdf-pages/get-dimensions/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF-pagina-afmetingen ophalen

## Invoering

Heb je ooit de pagina-afmetingen van een PDF-document moeten aanpassen? Misschien wilde je een pagina aanpassen of roteren naar wens? Zo ja, dan ben je hier aan het juiste adres! In deze tutorial laten we je zien hoe je de pagina-afmetingen van een PDF kunt ophalen en aanpassen met Aspose.PDF voor .NET. Of je nu een beginner of een ervaren ontwikkelaar bent, je zult deze handleiding eenvoudig en gemakkelijk te volgen vinden.

Aspose.PDF voor .NET is een krachtige bibliotheek waarmee je moeiteloos PDF-bestanden kunt maken, bewerken en transformeren. Het is alsof je een Zwitsers zakmes voor PDF's hebt: je kunt elk detail aanpassen aan jouw specifieke wensen. Laten we er meteen mee aan de slag gaan en leren hoe je PDF-pagina-afmetingen kunt ophalen en bijwerken met deze fantastische tool!

## Vereisten

Voordat u begint, moet u een aantal zaken regelen om deze tutorial soepel te kunnen volgen:

1. Aspose.PDF voor .NET: U kunt [Download hier de nieuwste versie](https://releases.aspose.com/pdf/net/). Als u geen vergunning heeft, maak u dan geen zorgen! U kunt een [gratis proefperiode](https://releases.aspose.com/), of kies voor een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
2. Visual Studio: de ontwikkelomgeving waarin u de code schrijft en uitvoert.
3. Basiskennis van C#: Hoewel we het simpel willen houden, zal enige vertrouwdheid met C# het proces soepeler laten verlopen.
4. PDF-bestand om mee te werken: download een voorbeeld-PDF-bestand of maak een nieuw bestand om te testen.

## Pakketten importeren

Om met Aspose.PDF voor .NET te werken, moet u een aantal essentiële naamruimten importeren. Dit maakt de weg vrij voor interactie met PDF-documenten. Zo doet u dat:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Met deze imports hebt u toegang tot de kernklassen die nodig zijn om PDF-bestanden te bewerken, met name voor het beheren van pagina's en het ophalen van hun afmetingen.

Nu we alles op zijn plaats hebben, kunnen we het proces opdelen in eenvoudig te volgen stappen.

## Stap 1: Definieer het bestandspad en laad het document

De eerste stap is het opgeven van het pad naar uw PDF-document en het laden ervan met Aspose.PDF. Dit stelt u in staat om met de pagina's in het PDF-bestand te werken.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Document openen
Document pdfDocument = new Document(dataDir + "UpdateDimensions.pdf");
```

In deze stap open je in feite het PDF-bestand waaraan je wilt werken. Als je ooit een boek op een bepaalde pagina hebt geopend, is dit vrijwel hetzelfde – maar in plaats daarvan open je een PDF-document om toegang te krijgen tot de pagina's.

## Stap 2: Voeg een lege pagina toe als er geen pagina's bestaan

Wat als uw document geen pagina's heeft? Geen zorgen! We kunnen een lege pagina aan het document toevoegen en ermee werken. Zo controleert u of er een pagina bestaat en voegt u indien nodig een nieuwe toe:

```csharp
// Voegt een lege pagina toe aan een pdf-document
Page page = pdfDocument.Pages.Count > 0 ? pdfDocument.Pages[1] : pdfDocument.Pages.Add();
```

Deze regel code controleert of er al een pagina in het document staat. Zo ja, dan wordt de eerste pagina gekozen (`Pages[1]`Anders wordt er een lege pagina gemaakt en aan de PDF toegevoegd.

Stel je voor dat je een leeg notitieboekje opent en op de eerste pagina schrijft, terwijl er niets staat. Makkelijk toch?

## Stap 3: Informatie over paginahoogte en -breedte ophalen

Nu we een pagina hebben om mee te werken, gaan we de afmetingen van de pagina ophalen. We gebruiken de `GetPageRect()` Methode om de hoogte en breedte te verkrijgen.

```csharp
// Informatie over paginahoogte en -breedte ophalen
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

Hier, `GetPageRect(true)` Retourneert een rechthoek die de hoogte en breedte van de pagina bevat. Het is vergelijkbaar met het meten van een stuk papier met een liniaal. De uitvoer wordt weergegeven in de console en geeft u de huidige pagina-afmetingen.

## Stap 4: Draai de pagina 90 graden

Wil je de pagina draaien? Geen probleem! Met een eenvoudige eigenschap kun je de pagina 90 graden draaien.

```csharp
// Pagina 90 graden draaien
page.Rotate = Rotation.on90;
```

Met deze stap draait u de pagina 90 graden met de klok mee. Stelt u zich voor dat u een afgedrukt vel papier op uw bureau omdraait – nu staat het in de liggende stand!

## Stap 5: Controleer de pagina-afmetingen opnieuw na rotatie

Nadat u de pagina hebt gedraaid, is het een goed idee om de afmetingen opnieuw te controleren. Waarom? Omdat rotatie van invloed kan zijn op hoe u de hoogte en breedte interpreteert.

```csharp
// Informatie over paginahoogte en -breedte ophalen
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

De pagina-afmetingen worden nu aangepast aan de nieuwe stand. Het is alsof je een foto op je telefoon draait: de breedte wordt ineens de hoogte, en andersom.


## Conclusie

Gefeliciteerd! Je hebt succesvol geleerd hoe je de afmetingen van een PDF-pagina kunt ophalen en wijzigen met Aspose.PDF voor .NET. Je zou nu een PDF moeten kunnen laden, de pagina-afmetingen moeten kunnen controleren en de pagina zelfs kunnen roteren indien nodig.

Het bewerken van PDF's hoeft niet ingewikkeld te zijn. Met Aspose.PDF is het zo eenvoudig als het volgen van een paar stappen en het gebruiken van intuïtieve methoden. Dus de volgende keer dat u PDF-pagina-afmetingen moet verwerken, weet u precies wat u moet doen!

## Veelgestelde vragen

### Kan ik de pagina ook in andere hoeken dan 90 graden draaien?
Ja, met Aspose.PDF kunt u pagina's 0, 90, 180 of 270 graden draaien met behulp van de `Rotation` eigendom.

### Wat gebeurt er als mijn PDF geen pagina's heeft?
Als uw PDF geen pagina's heeft, kunt u een lege pagina toevoegen met behulp van de `Pages.Add()` methode, zoals getoond in deze tutorial.

### Kan ik meerdere pagina's tegelijk bewerken?
Ja, u kunt door meerdere pagina's bladeren en transformaties, zoals het formaat wijzigen of roteren, op alle pagina's toepassen.

### Hebben de pagina-afmetingen invloed op de inhoud van het PDF-bestand?
Pagina-afmetingen veranderen alleen de grootte van het canvas, niet de inhoud. Het wijzigen van de grootte kan echter wel van invloed zijn op de weergave van de inhoud op de pagina.

### Waar kan ik meer informatie vinden over Aspose.PDF voor .NET?
U kunt de [documentatie hier](https://reference.aspose.com/pdf/net/) voor meer gedetailleerde informatie en geavanceerde use cases.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}