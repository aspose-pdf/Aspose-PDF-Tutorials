---
"description": "Leer hoe u een datum- en tijdstempel aan uw PDF-bestanden toevoegt met Aspose.PDF voor .NET met deze stapsgewijze handleiding. Perfect om de authenticiteit van uw document te verbeteren."
"linktitle": "Datum- en tijdstempel toevoegen aan PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Datum- en tijdstempel toevoegen aan PDF-bestand"
"url": "/nl/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Datum- en tijdstempel toevoegen aan PDF-bestand

## Invoering

Bij het beheren van documenten, met name PDF's, kan het toevoegen van een datum- en tijdstempel een echte doorbraak betekenen. Of u nu werkt aan juridische documenten, projectrapporten of facturen, een tijdstempel zorgt niet alleen voor authenticiteit, maar biedt ook een duidelijk overzicht van wanneer het document is gemaakt of gewijzigd. In deze handleiding leiden we u door het proces van het toevoegen van een datum- en tijdstempel aan een PDF-bestand met behulp van de Aspose.PDF-bibliotheek voor .NET. 

Dit artikel is zo opgesteld dat het eenvoudig en gemakkelijk te volgen is, zodat je deze functie met vertrouwen kunt implementeren, zelfs als je nog niet bekend bent met programmeren of de Aspose.PDF-bibliotheek. Laten we beginnen!

## Vereisten

Voordat we beginnen, zijn er een paar voorwaarden die u moet vervullen:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. Hier schrijft en voert u uw code uit.
2. Aspose.PDF voor .NET: U moet de Aspose.PDF-bibliotheek downloaden en installeren. U kunt de nieuwste versie vinden [hier](https://releases.aspose.com/pdf/net/).
3. Basiskennis van C#: Als u bekend bent met C#-programmering, begrijpt u de voorbeelden beter. Maar maak u geen zorgen als u nog maar net begint: we leggen alles stap voor stap uit.
4. Een PDF-bestand: Zorg dat u een voorbeeld-PDF-bestand bij de hand hebt. Voor ons voorbeeld gebruiken we een bestand met de naam `AddTextStamp.pdf`.

Zodra u aan deze vereisten voldoet, kunt u datum- en tijdstempels aan uw PDF-bestanden toevoegen!

## Pakketten importeren

Om te beginnen moet je de benodigde naamruimten in je C#-project importeren. Zo doe je dat:

### Een nieuw project maken

1. Open Visual Studio: start uw Visual Studio-toepassing.
2. Een nieuw project maken: Selecteer ‘Een nieuw project maken’ op het startscherm.
3. Kies Console App: Selecteer “Console App (.NET Framework)” uit de lijst met projectsjablonen.
4. Geef uw project een naam: Geef uw project een naam, bijvoorbeeld: `PDFDateTimeStamp`.

### Voeg Aspose.PDF-referentie toe

1. Klik met de rechtermuisknop op Verwijzingen: Klik in Solution Explorer met de rechtermuisknop op de map 'Verwijzingen' van uw project.
2. Selecteer “Referentie toevoegen”: Kies “Referentie toevoegen” uit het contextmenu.
3. Blader naar Aspose.PDF: Navigeer naar de locatie waar u Aspose.PDF hebt gedownload en selecteer het. Klik op "OK" om het aan uw project toe te voegen.

### Vereiste naamruimten importeren

Bovenaan je `Program.cs` bestand, moet u de volgende naamruimten importeren:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

Nu we alles hebben ingesteld, kunnen we het proces voor het toevoegen van een datum- en tijdstempel aan een PDF-bestand opsplitsen in duidelijke, beheersbare stappen.

## Stap 1: Stel de documentmap in

Eerst moet je de map opgeven waar je PDF-bestand zich bevindt. Dit is cruciaal, omdat de code in deze map naar de PDF zoekt.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Vervang door uw werkelijke pad
```

Zorg ervoor dat u vervangt `YOUR DOCUMENT DIRECTORY` met het daadwerkelijke pad naar uw PDF-bestand.

## Stap 2: Open het PDF-document

Vervolgens opent u het PDF-document waaraan u het tijdstempel wilt toevoegen. 

```csharp
// Document openen
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

Deze regel code initialiseert de `Document` klasse en laadt uw PDF-bestand in de `pdfDocument` voorwerp.

## Stap 3: Maak de datum-tijdstempel

Nu is het tijd om de datum- en tijdstempel te genereren. Je formatteert deze zodat deze op een specifieke manier wordt weergegeven. 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

Hier, `DateTime.Now` haalt de huidige datum en tijd op, en `ToString` formatteert het naar het door u gewenste formaat.

## Stap 4: Een tekststempel maken

Nu u de datum en tijd hebt ingevoerd, kunt u een tekststempel maken die aan uw PDF wordt toegevoegd.

```csharp
// Tekststempel maken
TextStamp textStamp = new TextStamp(annotationText);
```

Deze regel creëert een nieuw exemplaar van `TextStamp` met behulp van de geformatteerde datum- en tijdreeks.

## Stap 5: Eigenschappen van de stempel instellen

U kunt het uiterlijk en de positie van de stempel aanpassen. Zo stelt u de eigenschappen in:

```csharp
// Eigenschappen van de postzegel instellen
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

In deze stap stellen we de marges in en lijnen we de postzegel uit met de rechteronderhoek van de PDF-pagina.

## Stap 6: Voeg de stempel toe aan de PDF

Nu is het tijd om de tekststempel aan uw PDF-document toe te voegen. 

```csharp
// Postzegel toevoegen aan postzegelverzameling
pdfDocument.Pages[1].AddStamp(textStamp);
```

Deze regel voegt de stempel toe aan de eerste pagina van de PDF. U kunt het paginanummer wijzigen als u deze op een andere pagina wilt plaatsen.

## Stap 7: Maak een vrije tekstannotatie (optioneel)

Als u een aantekening aan de postzegel wilt toevoegen, kunt u een `FreeTextAnnotation` als volgt:

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

Met deze optionele stap wordt een vrije tekstuele aantekening gemaakt die aanvullende context of informatie over de postzegel kan geven.

## Stap 8: De annotatierand configureren

Als u de rand van uw aantekening wilt aanpassen, kunt u dat ook doen:

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

Met dit codefragment wordt de randbreedte ingesteld op 0, waardoor deze onzichtbaar wordt, en wordt de annotatie aan de PDF toegevoegd.

## Stap 9: Sla het PDF-document op

Ten slotte moet u het gewijzigde PDF-document opslaan. 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // Geef de naam van het uitvoerbestand op
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

Deze regel slaat de PDF met het toegevoegde tijdstempel op in een nieuw bestand. U kunt de opgegeven directory raadplegen om de uitvoer te bekijken.

## Conclusie

Gefeliciteerd! U hebt met succes een datum- en tijdstempel aan een PDF-bestand toegevoegd met Aspose.PDF voor .NET. Deze eenvoudige maar effectieve functie kan uw documenten verbeteren, ze professioneler maken en een duidelijk overzicht bieden van wanneer ze zijn gemaakt of gewijzigd. 

## Veelgestelde vragen

### Kan ik de datumnotatie in het tijdstempel aanpassen?
Ja, u kunt de `ToString` Methode om de datumnotatie naar uw voorkeur te wijzigen.

### Is Aspose.PDF gratis te gebruiken?
Aspose.PDF biedt een gratis proefperiode, maar voor alle functies moet u een licentie aanschaffen. U kunt een tijdelijke licentie krijgen. [hier](https://purchase.aspose.com/temporary-license/).

### Kan ik meerdere tijdstempels aan een PDF toevoegen?
Absoluut! Je kunt er meerdere maken `TextStamp` instanties en voeg ze toe aan verschillende pagina's of posities in de PDF.

### Wat als ik Visual Studio niet heb?
U kunt elke C# IDE of teksteditor gebruiken, maar voor het uitvoeren en debuggen van uw project wordt Visual Studio aanbevolen.

### Waar kan ik meer voorbeelden vinden van het gebruik van Aspose.PDF?
kunt meer voorbeelden en tutorials bekijken in de [Aspose.PDF-documentatie](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}