---
"description": "Leer hoe u gegroepeerde selectievakjes (keuzerondjes) in een PDF-document kunt maken met Aspose.PDF voor .NET met deze stapsgewijze zelfstudie."
"linktitle": "Gegroepeerde selectievakjes in PDF-document"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Gegroepeerde selectievakjes in PDF-document"
"url": "/nl/net/programming-with-forms/grouped-check-boxes/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gegroepeerde selectievakjes in PDF-document

## Invoering

Het maken van interactieve PDF's is niet zo moeilijk als het lijkt, vooral niet als je krachtige tools zoals Aspose.PDF voor .NET tot je beschikking hebt. Een van de interactieve elementen die je mogelijk aan je PDF-documenten moet toevoegen, zijn gegroepeerde selectievakjes, of specifieker, keuzerondjes waarmee gebruikers één optie uit een set kunnen selecteren. Deze tutorial begeleidt je door het proces van het toevoegen van gegroepeerde selectievakjes (keuzerondjes) aan een PDF-document met Aspose.PDF voor .NET. Of je nu een beginner of een ervaren ontwikkelaar bent, je zult deze handleiding boeiend, gedetailleerd en gemakkelijk te volgen vinden.

## Vereisten

Voordat we in de stapsgewijze handleiding duiken, willen we eerst enkele essentiële vereisten doornemen:

1. Aspose.PDF voor .NET: Zorg ervoor dat de Aspose.PDF-bibliotheek geïnstalleerd is. Zo niet, dan kunt u [download het hier](https://releases.aspose.com/pdf/net/).
2. IDE: U moet een ontwikkelomgeving instellen, zoals Visual Studio.
3. .NET Framework: Het project moet gericht zijn op een versie van .NET Framework die compatibel is met Aspose.PDF.
4. Basiskennis van C#: Kennis van C# en PDF-bewerking is vereist om de cursus soepel te kunnen volgen.
5. Licentie: Aspose.PDF vereist een licentie voor volledige functionaliteit. U kunt [een tijdelijke vergunning verkrijgen](https://purchase.aspose.com/temporary-license/) indien nodig.

## Pakketten importeren

Voordat u begint, moet u ervoor zorgen dat u de benodigde naamruimten in uw project hebt geïmporteerd:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Met deze pakketten krijgt u toegang tot alle klassen en methoden die nodig zijn om PDF-documenten te bewerken, inclusief het maken van keuzerondjes en het definiëren van hun eigenschappen.

In dit gedeelte leggen we het proces voor het maken van gegroepeerde selectievakjes (keuzerondjes) uit in duidelijke, gemakkelijk te volgen stappen.

## Stap 1: Een nieuw PDF-document maken

De eerste stap is het maken van een exemplaar van de `Document` object, dat uw PDF-bestand zal vertegenwoordigen. Voeg vervolgens een lege pagina toe aan uw document waar u de gegroepeerde selectievakjes plaatst.

```csharp
// Instantieer Document-object
Document pdfDocument = new Document();

// Een pagina toevoegen aan het PDF-bestand
Page page = pdfDocument.Pages.Add();
```

Hiermee wordt de basis gelegd voor het toevoegen van elementen, zoals keuzerondjes, aan de PDF.

## Stap 2: Initialiseer het keuzerondjeveld

Vervolgens moeten we een `RadioButtonField` object, dat de gegroepeerde selectievakjes (keuzerondjes) bevat. Dit veld wordt toegevoegd aan de specifieke pagina waar de selectievakjes verschijnen.

```csharp
// Instantieer het RadioButtonField-object en wijs het toe aan de eerste pagina
RadioButtonField radio = new RadioButtonField(pdfDocument.Pages[1]);
```

U kunt dit zien als een container waarin de afzonderlijke keuzerondjes worden gegroepeerd.

## Stap 3: Opties voor keuzerondjes toevoegen

Laten we nu de individuele keuzerondjes aan het veld toevoegen. In dit voorbeeld voegen we twee keuzerondjes toe en specificeren we hun posities met behulp van de `Rectangle` voorwerp.

```csharp
// Voeg de eerste keuzerondje toe en geef de positie ervan op met behulp van Rechthoek
RadioButtonOptionField opt1 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(0, 0, 20, 20));
RadioButtonOptionField opt2 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(100, 0, 120, 20));

// Optienamen instellen voor identificatie
opt1.OptionName = "Option1";
opt2.OptionName = "Option2";
```

Hier, de `Rectangle` object definieert de coördinaten en de grootte van elk keuzerondje op de pagina.

## Stap 4: Pas de stijl van keuzerondjes aan

U kunt het uiterlijk van de keuzerondjes aanpassen door hun `Style` eigenschap. U kunt bijvoorbeeld vierkante of kruisvormige selectievakjes gebruiken.

```csharp
// De stijl van de keuzerondjes instellen
opt1.Style = BoxStyle.Square;
opt2.Style = BoxStyle.Cross;
```

Hiermee kunt u het uiterlijk van de selectievakjes bepalen, waardoor ze gebruiksvriendelijker en visueel aantrekkelijker worden.

## Stap 5: Randeigenschappen configureren

Randen spelen een cruciale rol bij het gemakkelijk herkenbaar maken van de selectievakjes. Hier voegen we ononderbroken randen toe rond elke keuzerondje en definiëren we de breedte en kleur ervan.

```csharp
// De rand van de eerste keuzerondje configureren
opt1.Border = new Border(opt1);
opt1.Border.Style = BorderStyle.Solid;
opt1.Border.Width = 1;
opt1.Characteristics.Border = Color.Black;

// Configureer de rand van de tweede keuzerondje
opt2.Border = new Border(opt2);
opt2.Border.Style = BorderStyle.Solid;
opt2.Border.Width = 1;
opt2.Characteristics.Border = Color.Black;
```

Met deze stap wordt ervoor gezorgd dat elk keuzerondje een duidelijk gedefinieerde rand heeft, waardoor de leesbaarheid van het document wordt verbeterd.

## Stap 6: Voeg keuzerondjes toe aan het formulier

Nu voegen we de keuzerondjes toe aan het formulier van het document. Dit is de laatste stap in het groeperen van de selectievakjes onder één veld.

```csharp
// Voeg een keuzerondje toe aan het formulierobject van het document
pdfDocument.Form.Add(radio);
```

Het formulierobject fungeert als een container voor alle interactieve elementen, inclusief onze gegroepeerde selectievakjes.

## Stap 7: Sla het PDF-document op

Als alles is ingesteld, kunt u het PDF-document opslaan op de gewenste locatie.

```csharp
// Definieer het pad van het uitvoerbestand
string dataDir = "YOUR DOCUMENT DIRECTORY" + "GroupedCheckBoxes_out.pdf";

// Sla het PDF-document op
pdfDocument.Save(dataDir);

// Bevestig succesvolle creatie
Console.WriteLine("Grouped checkboxes added successfully. File saved at " + dataDir);
```

En dat is alles! Je hebt met succes een PDF met gegroepeerde selectievakjes gemaakt met Aspose.PDF voor .NET.

## Conclusie

Het toevoegen van interactieve elementen zoals gegroepeerde selectievakjes aan PDF-documenten kan in eerste instantie lastig lijken, maar met Aspose.PDF voor .NET wordt het een fluitje van een cent. Door deze stapsgewijze handleiding te volgen, hebt u geleerd hoe u een eenvoudig PDF-document opzet, gegroepeerde keuzerondjes toevoegt, hun weergave aanpast en het eindresultaat opslaat. Of u nu formulieren, enquêtes of een ander type interactieve PDF maakt, deze handleiding geeft u een solide basis om mee te beginnen.

## Veelgestelde vragen

### Kan ik meer dan twee keuzerondjes aan een groep toevoegen?
Absoluut! Instantieer gewoon extra `RadioButtonOptionField` objecten en voeg ze toe aan de `RadioButtonField` zoals getoond in de tutorial.

### Hoe kan ik meerdere groepen selectievakjes in één document verwerken?
Om meerdere groepen te creëren, moet u afzonderlijke groepen instantiëren `RadioButtonField` objecten voor elke groep.

### Zit er een limiet aan het aantal selectievakjes dat ik kan toevoegen?
Nee, Aspose.PDF voor .NET stelt geen beperkingen aan het aantal selectievakjes dat u aan een PDF kunt toevoegen.

### Kan ik het uiterlijk van selectievakjes wijzigen nadat ik ze heb toegevoegd?
Ja, u kunt eigenschappen zoals randstijl, breedte en kleur wijzigen nadat u de selectievakjes hebt toegevoegd.

### Is het mogelijk om afbeeldingen als keuzerondjes te gebruiken?
Ja, met Aspose.PDF kunt u aangepaste afbeeldingen gebruiken als keuzerondjes door de volgende instellingen te kiezen: `Appearance` eigenschap van elke keuzerondjeoptie.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}