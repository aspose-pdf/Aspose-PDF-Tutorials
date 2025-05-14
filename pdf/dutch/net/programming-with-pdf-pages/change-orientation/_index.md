---
"description": "Stapsgewijze handleiding voor het wijzigen van de pagina-oriëntatie van een PDF met Aspose.PDF voor .NET. Eenvoudig te volgen en te implementeren in uw projecten."
"linktitle": "Verander oriëntatie"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Verander oriëntatie"
"url": "/nl/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Verander oriëntatie

## Invoering

Heb je ooit problemen gehad met een PDF-bestand waarvan de pagina-oriëntatie gewoon... niet klopte? Misschien heb je te maken met een document dat verkeerd is gescand of aangemaakt, en de pagina's moeten worden gedraaid om ze te laten kloppen. Gelukkig voor ons biedt Aspose.PDF voor .NET een eenvoudige en krachtige manier om PDF-bestanden op vrijwel elke denkbare manier te bewerken, inclusief het wijzigen van de pagina-oriëntatie. Of je nu wilt overschakelen van staand naar liggend of andersom, deze handleiding leidt je stap voor stap door het proces.

Dus, als u er klaar voor bent om aan de slag te gaan en die PDF-pagina's eenvoudig te roteren, laten we dan beginnen!

## Vereisten

Voordat we dieper ingaan op het wijzigen van de pagina-oriëntatie in uw PDF, leggen we u kort uit wat u hiervoor nodig hebt:

- Aspose.PDF voor .NET: Zorg ervoor dat je de Aspose.PDF-bibliotheek voor .NET hebt geïnstalleerd. Zo niet, dan kun je... [download het hier](https://releases.aspose.com/pdf/net/).
- Een .NET-ontwikkelomgeving: u kunt Visual Studio, JetBrains Rider of een andere gewenste IDE gebruiken om met .NET te werken.
- Basiskennis van C#: Hoewel deze gids eenvoudig is, is hij met enige basiskennis van C# nog makkelijker te volgen.
- Een PDF-bestand: In het onderstaande voorbeeld wordt ervan uitgegaan dat u een PDF-bestand met meerdere pagina's hebt. Als u er geen bij de hand hebt, kunt u een voorbeeld-PDF maken of downloaden om mee te werken.

Als u net begint, kunt u Aspose.PDF ook proberen met een [gratis tijdelijke licentie](https://purchase.aspose.com/temporary-license/) voordat u besluit om [koop de volledige versie](https://purchase.aspose.com/buy).

## Naamruimten importeren

Voordat u de pagina-oriëntatie in uw PDF kunt aanpassen, moet u de benodigde naamruimten in uw C#-project importeren. Zorg ervoor dat u over het volgende beschikt:

```csharp
using System.IO;
using Aspose.Pdf;
```

Nu we dit hebben geïmporteerd, kunnen we naar het hoofdonderdeel van de tutorial gaan.

## Stap 1: Het PDF-document laden

Het eerste wat we moeten doen is het PDF-bestand laden dat u wilt wijzigen. U kunt hiervoor de `Document` klasse uit de Aspose.PDF-naamruimte om uw PDF te openen.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Deze regel laadt de PDF vanuit de opgegeven map. Zorg ervoor dat u `"YOUR DOCUMENT DIRECTORY"` met het daadwerkelijke pad naar uw bestand. De `"input.pdf"` is de PDF waarvan u de oriëntatie wilt wijzigen.

## Stap 2: Door elke pagina bladeren

Nu we het document hebben geladen, gaan we elke pagina in de PDF doorlopen. We gebruiken een `foreach` doorloop elke pagina, zodat we de gewijzigde oriëntatie op alle pagina's kunnen toepassen.

```csharp
foreach (Page page in doc.Pages)
{
    // Manipuleer elke pagina
}
```

Deze lus doorloopt alle pagina's in het document.

## Stap 3: Haal de MediaBox van de pagina op

Elke pagina in een PDF heeft een `MediaBox` die de grenzen van de pagina definieert. We hebben hier toegang toe nodig om de huidige oriëntatie te bepalen en aan te passen.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

De `MediaBox` geeft ons de afmetingen van de pagina, zoals de breedte, hoogte en positie.

## Stap 4: De breedte en hoogte omwisselen

Om de pagina-oriëntatie te wijzigen van staand naar liggend of van liggend naar staand, wisselen we eenvoudig de breedte- en hoogtewaarden om. Met deze stap passen we de afmetingen van de pagina aan.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

Deze code verwisselt de hoogte en breedte en verplaatst de linkerbenedenhoek (`LLY`) zodat de inhoud na rotatie netjes past.

## Stap 5: MediaBox en CropBox bijwerken

Nu we de nieuwe hoogte en breedte hebben, kunnen we de wijzigingen toepassen op de pagina. `MediaBox` En `CropBox`. De `CropBox` is essentieel als het originele document één set had, zodat de hele pagina correct wordt weergegeven.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

Met deze stap wordt de pagina aangepast op basis van de nieuwe afmetingen die we zojuist hebben berekend.

## Stap 6: Draai de pagina

Tot slot stellen we de rotatiehoek van de pagina in. Aspose.PDF maakt dit supersimpel. We kunnen de pagina 90 graden draaien om van staand naar liggend te gaan of andersom.

```csharp
page.Rotate = Rotation.on90;
```

Met deze code draait u de pagina 90 graden, waardoor deze in de gewenste stand komt.

## Stap 7: Sla de uitvoer-PDF op

Nadat de gewijzigde oriëntatie op alle pagina's is toegepast, slaan we het gewijzigde document op in een nieuw bestand. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

Zorg ervoor dat u een nieuwe bestandsnaam opgeeft (in dit geval `ChangeOrientation_out.pdf`) om de uitvoer op te slaan. Zo overschrijf je het originele bestand niet.

### Conclusie

En voilà! Het wijzigen van de pagina-oriëntatie van een PDF-bestand met Aspose.PDF voor .NET is net zo eenvoudig als het laden van het document, het doorlopen van de pagina's, het aanpassen van de MediaBox en het opslaan van het bijgewerkte bestand. Of u nu te maken hebt met een slecht gescand document of pagina's moet roteren om aan uw opmaakbehoeften te voldoen, deze stapsgewijze handleiding helpt u op weg.

## Veelgestelde vragen

### Kan ik specifieke pagina's roteren in plaats van alle pagina's in het PDF-bestand?  
Ja, u kunt de lus aanpassen zodat deze op specifieke pagina's wordt gericht met behulp van hun index, in plaats van door alle pagina's te lussen.

### Wat is de `MediaBox`?  
De `MediaBox` Definieert de grootte en vorm van de pagina in een PDF-bestand. Het is de plek waar de inhoud van de pagina wordt geplaatst.

### Werkt Aspose.PDF voor .NET met andere bestandsformaten?  
Ja, Aspose.PDF kan verschillende bestandsformaten verwerken, zoals HTML, XML, XPS en meer.

### Is er een gratis versie van Aspose.PDF voor .NET?  
Ja, je kunt beginnen met een [gratis proefperiode](https://releases.aspose.com/) of vraag een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/).

### Kan ik de wijzigingen ongedaan maken nadat ik ze heb opgeslagen?  
Zodra u het document opslaat, zijn de wijzigingen permanent. Zorg ervoor dat u aan een kopie werkt of een back-up van het originele bestand bewaart.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}