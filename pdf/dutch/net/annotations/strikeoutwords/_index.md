---
"description": "Leer hoe je woorden in een PDF doorhaalt met Aspose.PDF voor .NET met deze uitgebreide stapsgewijze handleiding. Verbeter je vaardigheden in het bewerken van documenten."
"linktitle": "Woorden doorhalen"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Woorden doorhalen"
"url": "/nl/net/annotations/strikeoutwords/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Woorden doorhalen

## Invoering

Heb je ooit specifieke tekst in een PDF moeten benadrukken door deze door te strepen? Of je nu documenten controleert, tekst markeert of gewoon bepaalde secties wilt markeren, het doorhalen van woorden kan een waardevol hulpmiddel zijn. In deze tutorial laten we zien hoe je dat kunt doen met Aspose.PDF voor .NET. Deze uitgebreide handleiding begeleidt je bij elke stap, zodat je alle informatie hebt die je nodig hebt om deze functie effectief te implementeren in je .NET-applicaties. 

## Vereisten

Voordat we met de code aan de slag gaan, zijn er een paar vereisten waaraan je moet voldoen om deze tutorial te kunnen volgen:

1. Aspose.PDF voor .NET-bibliotheek: Zorg ervoor dat u de Aspose.PDF voor .NET-bibliotheek hebt geïnstalleerd. U kunt [download het hier](https://releases.aspose.com/pdf/net/).

2. .NET Framework: Zorg ervoor dat .NET Framework op uw computer is geïnstalleerd. Deze tutorial is bedoeld voor .NET-toepassingen.

3. Ontwikkelomgeving: Je hebt een IDE zoals Visual Studio nodig om je code te schrijven en uit te voeren.

4. PDF-document: Zorg dat u een voorbeeld-PDF-bestand bij de hand hebt waarmee u wilt werken. Dit is het document waarin we de tekst doorhalen.

5. Basiskennis van C#: Kennis van C#-programmering is noodzakelijk om de stappen in deze tutorial te begrijpen en te implementeren.

## Pakketten importeren

Voordat we kunnen beginnen met coderen, moeten we de benodigde naamruimten in ons .NET-project importeren. Dit geeft ons toegang tot de klassen en methoden die nodig zijn om PDF-bestanden te bewerken met Aspose.PDF.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Deze naamruimten zijn essentieel voor het werken met PDF-documenten, het verwerken van tekst en het toevoegen van aantekeningen, zoals doorhalingen.

In dit gedeelte leggen we het proces van het doorhalen van woorden in een PDF-document uit in eenvoudige, beheersbare stappen. Elke stap wordt vergezeld door een gedetailleerde uitleg, zodat u begrijpt hoe alles werkt.

## Stap 1: Het PDF-document laden

De eerste stap is het laden van het PDF-document dat u wilt bewerken. Dit is het document waarin u specifieke woorden of zinnen doorstreept.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Open het PDF-document
Document document = new Document(dataDir + "input.pdf");
```

- `dataDir`: Deze variabele bevat het pad naar uw documentmap. Vervangen `"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad waar uw PDF-bestand zich bevindt.
- `Document`: De `Document` De klasse vertegenwoordigt een PDF-document. Door het bestandspad naar de constructor door te geven, openen we het PDF-bestand voor verwerking.

## Stap 2: Maak een TextFragment Absorber om specifieke tekst te vinden

Vervolgens maken we een exemplaar van `TextFragmentAbsorber` Om te zoeken naar een specifiek tekstfragment in het PDF-document. Zo kunnen we de tekst vinden die we willen doorhalen.

```csharp
// Maak een TextFragment Absorber-instantie om naar een specifiek tekstfragment te zoeken
Aspose.Pdf.Text.TextFragmentAbsorber textFragmentAbsorber = new Aspose.Pdf.Text.TextFragmentAbsorber("Estoque");
```

- `TextFragmentAbsorber`Deze klasse wordt gebruikt om specifieke tekstfragmenten in het PDF-document te vinden en ermee te werken. In dit voorbeeld zoeken we naar het woord "Estoque". Vervang "Estoque" door het woord of de woordgroep die u in uw document wilt vinden.

## Stap 3: Door de pagina's van het PDF-document bladeren

Nu we onze `TextFragmentAbsorber`moeten we door elke pagina van het PDF-document itereren om de opgegeven tekst te vinden.

```csharp
// Door de pagina's van het PDF-document bladeren
for (int i = 1; i <= document.Pages.Count; i++)
{
    // De huidige pagina van het PDF-document ophalen
    Page page = document.Pages[i];
    page.Accept(textFragmentAbsorber);
}
```

- `for (int i = 1; i <= document.Pages.Count; i++)`:Deze lus doorloopt elke pagina van het PDF-document.
- `document.Pages[i]`: Haalt de huidige pagina op die wordt verwerkt.
- `page.Accept(textFragmentAbsorber)`:Deze methode past de `TextFragmentAbsorber` naar de huidige pagina, op zoek naar de opgegeven tekst.

## Stap 4: Verzamel en verwerk de tekstfragmenten

Nadat we de pagina's hebben doorgenomen, verzamelen we de gevonden tekstfragmenten en bereiden we deze voor op verdere verwerking.

```csharp
// Maak een verzameling opgenomen tekstfragmenten
Aspose.Pdf.Text.TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`Deze verzameling slaat alle tekstfragmenten op die in het document zijn gevonden. We gebruiken deze verzameling in de volgende stap om de tekst door te strepen.

## Stap 5: Loop door de tekstfragmenten en streep ze door

In deze stap doorlopen we elk tekstfragment in onze verzameling en passen we er een doorhalingsannotatie op toe.

```csharp
// Itereer over de verzameling tekstfragmenten
for (int j = 1; j <= textFragmentCollection.Count; j++)
{
	Aspose.Pdf.Text.TextFragment textFragment = textFragmentCollection[j];

    // De rechthoekige afmetingen van het TextFragment-object verkrijgen
    Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(
        (float)textFragment.Position.XIndent,
        (float)textFragment.Position.YIndent,
        (float)textFragment.Position.XIndent + (float)textFragment.Rectangle.Width,
        (float)textFragment.Position.YIndent + (float)textFragment.Rectangle.Height);

    // Instantieer StrikeOut Annotation-instantie
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.Page, rect);

    // Eigenschappen van de doorhalingsannotatie instellen
    strikeOut.Opacity = .80f;
    strikeOut.Border = new Border(strikeOut);
    strikeOut.Color = Aspose.Pdf.Color.Red;

    // Voeg de annotatie toe aan de annotatieverzameling van de pagina van het tekstfragment
    textFragment.Page.Annotations.Add(strikeOut);
}
```

- `TextFragment textFragment = textFragmentCollection[j]`: Deze regel haalt het huidige tekstfragment op.
- `Aspose.Pdf.Rectangle`:We berekenen de rechthoekige afmetingen van het tekstfragment om te bepalen waar we de doorhaling moeten toepassen.
- `StrikeOutAnnotation`: Deze klasse vertegenwoordigt de doorgestreepte annotatie. We instantiëren deze met de berekende rechthoek en de huidige pagina.
- `strikeOut.Opacity`: Met deze eigenschap bepaalt u de dekking van de doorhaling, waardoor deze 80% zichtbaar wordt.
- `strikeOut.Color`We hebben de kleur van de doorhaling ingesteld op rood. Je kunt dit naar elke gewenste kleur veranderen.
- `textFragment.Page.Annotations.Add(strikeOut)`: Hiermee wordt de doorgehaalde annotatie aan de pagina toegevoegd.

## Stap 6: Sla het gewijzigde PDF-document op

De laatste stap is het opslaan van het gewijzigde PDF-document met de doorhalingen.

```csharp
// Sla het bijgewerkte PDF-document op
dataDir = dataDir + "StrikeOutWords_out.pdf";
document.Save(dataDir);
```

- `dataDir + "StrikeOutWords_out.pdf"`: Hiermee wordt een nieuwe bestandsnaam voor het gewijzigde document aangemaakt. Het oorspronkelijke bestand blijft ongewijzigd.
- `document.Save(dataDir)`: Slaat het PDF-document met de doorhalingen op de opgegeven locatie op.

## Conclusie

Gefeliciteerd! Je hebt met succes specifieke woorden in een PDF-document doorgehaald met Aspose.PDF voor .NET. Door deze stapsgewijze handleiding te volgen, kun je nu PDF-documenten aanpassen door tekst te markeren of door te halen. Zo worden ze dynamischer en beter afgestemd op jouw behoeften. Of je nu juridische documenten annoteert, rapporten opstelt of tekst markeert ter controle, deze tutorial heeft je de vaardigheden bijgebracht om dit efficiënt te doen.

## Veelgestelde vragen

### Kan ik de kleur van de doorhaling veranderen?

Ja, u kunt de kleur veranderen door de `strikeOut.Color` eigenschap. U kunt het bijvoorbeeld instellen op `Aspose.Pdf.Color.Blue` voor een blauwe strikeout.

### Is het mogelijk om meerdere woorden tegelijk door te strepen?

Absoluut! De `TextFragmentAbsorber` Kan worden gebruikt om naar een woord of zin in het document te zoeken. U kunt de doorhaling op meerdere instanties toepassen door de `TextFragmentCollection`.

### Wat als ik alleen tekst op specifieke pagina's wil doorhalen?

U kunt de lus die door de pagina's itereert, aanpassen zodat deze alleen de pagina's bevat die u wilt wijzigen. Bijvoorbeeld: `for (int i = 1; i <= 3; i++)` zou de doorhaling alleen op de eerste drie pagina's toepassen.

### Hoe kan ik de dikte van de doorhaallijn aanpassen?

U kunt de dikte van de doorhaallijn aanpassen door de `Border` eigendom van de `StrikeOutAnnotation`Hierdoor is het mogelijk om het uiterlijk van de strikeout aan te passen.

### Is er een manier om het doorhalen ongedaan te maken nadat ik het document heb opgeslagen?

Zodra het document is opgeslagen, is de doorhaling permanent. Als u de originele tekst zonder doorhaling wilt behouden, kunt u overwegen een back-up van het originele document te maken voordat u wijzigingen aanbrengt.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}