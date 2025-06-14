---
"description": "Leer hoe u bijschriften voor keuzerondjes in PDF's instelt met Aspose.PDF voor .NET. Deze stapsgewijze handleiding begeleidt u bij het laden, wijzigen en opslaan van uw PDF-formulieren."
"linktitle": "Bijschrift voor keuzerondje instellen"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Bijschrift voor keuzerondje instellen"
"url": "/nl/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bijschrift voor keuzerondje instellen

## Invoering

Als je je verdiept in PDF-bewerking met Aspose.PDF voor .NET, staat je een verrassing te wachten! Vandaag richten we ons op een praktische functie: het instellen van bijschriften voor keuzerondjes in je PDF-formulieren. Keuzerondjes zijn essentieel voor gebruikersformulieren waarbij je moet kunnen kiezen uit een reeks opties. Stel je ze voor als meerkeuzevragen waarbij slechts één antwoord is toegestaan. Deze tutorial leidt je door het proces van het bijwerken van bijschriften voor keuzerondjes in een PDF-formulier, zodat je documenten zowel interactief als gebruiksvriendelijk zijn. 

## Vereisten

Voordat u in de code duikt, moet u het volgende controleren:

1. Aspose.PDF voor .NET: Zorg ervoor dat de Aspose.PDF-bibliotheek geïnstalleerd is. Deze bibliotheek helpt u bij het programmatisch bewerken van PDF-bestanden.
2. Ontwikkelomgeving: U dient een .NET-ontwikkelomgeving in te stellen, zoals Visual Studio.
3. Voorbeeld PDF-formulier: Voor deze tutorial heb je een voorbeeld PDF-formulier met keuzerondjes nodig. Je kunt elk bestaand PDF-formulier gebruiken of een nieuw formulier met keuzerondjes maken.
4. Basiskennis van C#: in deze handleiding wordt ervan uitgegaan dat u een basiskennis hebt van de programmeerconcepten van C# en .NET.

Als u Aspose.PDF voor .NET nog niet hebt geïnstalleerd of als u een tijdelijke licentie nodig hebt, kunt u: [download het hier](https://releases.aspose.com/pdf/net/) of [een tijdelijke licentie krijgen](https://purchase.aspose.com/temporary-license/).

## Pakketten importeren

Om te beginnen moet je de benodigde pakketten in je C#-project importeren. Zo voeg je de Aspose.PDF-bibliotheek toe:

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

Zorg ervoor dat u deze pakketten via NuGet of uw favoriete methode aan uw project toevoegt.

## Stap 1: Het PDF-formulier laden

Eerst moet u het PDF-formulier laden dat de keuzerondjes bevat. `Aspose.Pdf.Facades.Form` klasse wordt hiervoor gebruikt. Zo doe je dat:

```csharp
// Definieer het pad naar uw documentenmap
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Laad het bron-PDF-formulier
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

In dit codefragment:
- `dataDir` geeft het pad aan waar uw PDF zich bevindt.
- `Form` klasse wordt gebruikt om te communiceren met de formuliervelden in de PDF.
- `Document` klasse biedt toegang tot de pagina's van het PDF-document.

## Stap 2: Door de keuzerondjevelden itereren

Vervolgens moet u door de velden in uw formulier itereren om de keuzerondjesvelden te identificeren en te bewerken:

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

In deze lus:
- `FieldNames` Geeft een lijst weer met alle veldnamen in de PDF.
- `GetButtonOptionValues(item)` haalt de opties op die beschikbaar zijn voor elk keuzerondje.

## Stap 3: Wijzig de opties voor keuzerondjes

Zodra u de keuzerondjesvelden hebt geïdentificeerd, kunt u hun opties wijzigen. Hiervoor moet u het veld omzetten naar `RadioButtonField` en de opties bijwerken:

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

Hier:
- We controleren of de veldnaam "radio1" bevat om het specifieke keuzerondjeveld te identificeren dat we willen wijzigen.
- `RadioButtonField` wordt vanuit de formuliervelden omgezet om specifieke wijzigingen aan te brengen.

## Stap 4: Stel het bijschrift voor de keuzerondje in

Om het bijschrift voor de keuzerondje in te stellen of bij te werken, moet u een `TextFragment` en gebruik `TextBuilder` om het op de gewenste locatie te plaatsen:

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // Maak een TextParagraph-object
        TextParagraph par = new TextParagraph();
        // Alineapositie instellen
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // Geef de woordomloopmodus op
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // Nieuw TextFragment toevoegen aan alinea
        par.AppendLine(updatedFragment);
        // Voeg de TextParagraph toe met behulp van TextBuilder
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

In dit deel:
- `TextFragment` wordt gebruikt om de tekst en het uiterlijk ervan te definiëren.
- `TextParagraph` helpt bij het positioneren en opmaken van de tekst.
- `TextBuilder` voegt de tekst toe aan de opgegeven pagina van de PDF.

## Stap 5: Sla de bijgewerkte PDF op

Sla ten slotte het bijgewerkte PDF-bestand op in een nieuw bestand:

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

Hiermee wordt gegarandeerd dat:
- De wijzigingen worden toegepast op de PDF.
- De oorspronkelijke keuzerondjeoptie is verwijderd zoals aangegeven.

## Conclusie

Het aanpassen van bijschriften van keuzerondjes in een PDF-formulier met Aspose.PDF voor .NET kan de interactiviteit en bruikbaarheid van uw documenten aanzienlijk verbeteren. Met de stappen in deze tutorial kunt u eenvoudig een PDF laden, de opties van keuzerondjes bijwerken en uw wijzigingen opslaan. Deze aanpak is handig voor formulierbeheer en zorgt ervoor dat uw PDF's voldoen aan de exacte behoeften van uw gebruikers. Duik in Aspose.PDF en ontdek de mogelijkheden voor andere PDF-bewerkingen!

## Veelgestelde vragen

### Kan ik meerdere keuzerondjevelden tegelijk bijwerken?
Ja, u kunt door alle keuzerondjevelden heen itereren en indien nodig wijzigingen doorvoeren.

### Heb ik een licentie nodig om Aspose.PDF te gebruiken?
U kunt beginnen met een gratis proefperiode, maar voor uitgebreid gebruik is een licentie vereist. [Hier een licentie verkrijgen](https://purchase.aspose.com/buy).

### Hoe kan ik de wijzigingen testen voordat ik de PDF opsla?
U kunt een voorbeeld van het PDF-bestand bekijken in uw ontwikkelomgeving of een PDF-viewer gebruiken om de wijzigingen te controleren.

### Is Aspose.PDF compatibel met alle versies van .NET?
Aspose.PDF ondersteunt verschillende versies van .NET. Controleer de compatibiliteit met uw specifieke .NET-versie.

### Kan ik andere formuliervelden op dezelfde manier bewerken?
Ja, vergelijkbare technieken kunnen worden toegepast op andere typen formuliervelden in PDF-documenten.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}