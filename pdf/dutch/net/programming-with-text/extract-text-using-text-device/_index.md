---
"description": "Leer hoe u tekst uit een PDF-document kunt extraheren met behulp van het tekstapparaat in Aspose.PDF voor .NET."
"linktitle": "Tekst extraheren met behulp van een tekstapparaat"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Tekst extraheren met behulp van een tekstapparaat"
"url": "/nl/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren met behulp van een tekstapparaat

## Invoering

Het extraheren van tekst uit een PDF kan lastig zijn, vooral wanneer u werkt met documenten met verschillende formaten, ingesloten lettertypen of complexe lay-outs. Maar met Aspose.PDF voor .NET wordt dit proces een fluitje van een cent! Of u nu pagina's van een PDF wilt converteren naar platte tekst voor verdere analyse of gewoon specifieke secties wilt extraheren, Aspose.PDF helpt u daarbij. In deze tutorial leggen we stap voor stap uit hoe u tekst uit een PDF kunt extraheren met behulp van de klasse TextDevice in Aspose.PDF. We geven ook duidelijke uitleg, zodat u dezelfde methoden eenvoudig op uw eigen projecten kunt toepassen.

## Vereisten

Voordat we aan de code beginnen, zorg ervoor dat je alles klaar hebt om te volgen. Dit heb je nodig:

1. Aspose.PDF voor .NET: Download de nieuwste versie van de [Aspose.PDF voor .NET downloadpagina](https://releases.aspose.com/pdf/net/).
2. Ontwikkelomgeving: Visual Studio of een andere C#-ontwikkelomgeving.
3. .NET Framework: zorg ervoor dat uw project gericht is op .NET Framework 4.x of hoger.
4. PDF-invoerbestand: een PDF-bestand dat u gebruikt voor tekstextractie. Plaats dit in een map op uw computer (we noemen dit `YOUR DOCUMENT DIRECTORY`).

## Pakketten importeren

Bovenaan uw code moet u de benodigde naamruimten importeren om met Aspose.PDF te kunnen werken:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## Stap 1: Laad uw PDF-document

Voordat we tekst kunnen extraheren, moeten we het PDF-document in het geheugen laden. In deze stap openen we uw PDF met Aspose.PDF. `Document` klasse. Hiermee krijgt u toegang tot alle pagina's en inhoud in het bestand.

```csharp
// Definieer het pad naar uw PDF-document
string dataDir = "YOUR DOCUMENT DIRECTORY";

// PDF-document laden
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Hier gebruiken we `Document pdfDocument = new Document(dataDir + "input.pdf");` om de PDF te laden. De `dataDir` De variabele bevat het directorypad van uw PDF-bestand. Dit geeft ons toegang tot het volledige document, waardoor we door pagina's kunnen bladeren en inhoud kunnen extraheren.

## Stap 2: Een stringbuilder instellen voor tekstopslag

Nu het document is geladen, hebben we een manier nodig om de geëxtraheerde tekst op te slaan. Hiervoor gebruiken we een `StringBuilder` waardoor efficiënte string-concatenatie mogelijk is.

```csharp
// StringBuilder om de geëxtraheerde tekst vast te houden
StringBuilder builder = new StringBuilder();
```

We initialiseren een `StringBuilder` Instantie, die tekst verzamelt die van elke pagina wordt geëxtraheerd. Dit is een efficiëntere manier om grote strings te verwerken in vergelijking met de reguliere stringaaneenschakeling in een lus.

## Stap 3: Door PDF-pagina's bladeren

Vervolgens doorlopen we elke pagina van het PDF-document om de tekst te extraheren. We verwerken elke pagina afzonderlijk met behulp van de `TextDevice` klasse, die verantwoordelijk is voor het converteren van de PDF-inhoud naar tekstformaat.

```csharp
// Doorloop alle pagina's in de PDF
foreach (Page pdfPage in pdfDocument.Pages)
{
    // Verwerk elke pagina voor tekst extractie
}
```

Deze lus gaat door elke pagina van de PDF (`pdfDocument.Pages`). Voor elke pagina zullen we de tekst extraheren en toevoegen aan onze `StringBuilder`.

## Stap 4: Tekst uit elke pagina halen

Nu stellen we het tekstextractieproces voor elke pagina in. Hier maken we een `TextDevice` object en gebruik het om de PDF-pagina's te verwerken. De `TextDevice` extraheert ruwe of opgemaakte tekst op basis van de extractieopties die we instellen.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // Maak een tekstapparaat voor tekstextractie
    TextDevice textDevice = new TextDevice();
    
    // Stel de tekstextractieopties in op de modus 'Puur'
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // Tekst van de huidige pagina extraheren en in de geheugenstroom opslaan
    textDevice.Process(pdfPage, textStream);

    // Converteer geheugenstroom naar tekst
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // Voeg de geëxtraheerde tekst toe aan de StringBuilder
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: De `TextDevice` klasse wordt gebruikt om tekst uit de PDF te extraheren.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: Met deze optie wordt de onbewerkte tekst geëxtraheerd zonder opmaak, zoals lettertypen of posities, te behouden. U kunt ook `TextFormattingMode.Raw` als u meer controle over de opmaak nodig hebt.
- `textDevice.Process(pdfPage, textStream);`:Hiermee wordt elke pagina van de PDF verwerkt en wordt de geëxtraheerde tekst in een bestand opgeslagen. `MemoryStream`.
- Ten slotte zetten we de tekst om van de `MemoryStream` aan een string toevoegen en deze aan de `StringBuilder`.

## Stap 5: Geëxtraheerde tekst opslaan in een bestand

Nadat alle pagina's zijn verwerkt, wordt de tekst opgeslagen in de `StringBuilder`De laatste stap is het opslaan van de geëxtraheerde tekst in een bestand.

```csharp
// Definieer het uitvoerpad voor het tekstbestand
dataDir = dataDir + "input_Text_Extracted_out.txt";

// Sla de geëxtraheerde tekst op in een bestand
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`:Hiermee wordt de volledige inhoud van de `StringBuilder` naar een tekstbestand.
- Het pad voor het uitvoerbestand wordt ingesteld door een bestandsnaam toe te voegen (`"input_Text_Extracted_out.txt"`) naar de `dataDir` pad.

## Conclusie

Het extraheren van tekst uit een PDF met Aspose.PDF voor .NET is een eenvoudig en efficiënt proces. Door de stappen in deze handleiding te volgen, kunt u eenvoudig PDF-documenten openen, door pagina's bladeren en tekst extraheren naar een tekstbestand. Dit is vooral handig voor het verwerken van grote hoeveelheden PDF-gegevens, het uitvoeren van tekstanalyses of het converteren van documenten voor verdere bewerking.

Met Aspose.PDF bent u niet beperkt tot tekstextractie: u kunt annotaties verwerken, afbeeldingen bewerken en zelfs PDF's converteren naar andere formaten zoals HTML of Word. De flexibiliteit en kracht van deze bibliotheek maken het een onmisbare tool voor PDF-beheer in .NET-applicaties.

## Veelgestelde vragen

### Kan Aspose.PDF tekst uit PDF-bestanden met afbeeldingen halen?
Nee, Aspose.PDF is ontworpen om tekst uit content-gebaseerde PDF's te extraheren. Voor afbeeldingen-gebaseerde PDF's is OCR-technologie vereist.

### Behoudt Aspose.PDF de opmaak bij het extraheren van tekst?
Standaard wordt de tekst zonder opmaak geëxtraheerd, maar u kunt de extractieopties aanpassen als u bepaalde opmaak wilt behouden.

### Kan ik tekst uit een specifiek paginabereik halen?
Ja, u kunt de code aanpassen, zodat deze over een specifiek paginabereik loopt in plaats van over alle pagina's.

### Wat zijn de tekstextractiemodi in Aspose.PDF?
Aspose.PDF biedt twee modi: Raw en Pure. De Raw-modus probeert de originele lay-out te behouden, terwijl de Pure-modus alleen de tekst zonder opmaak extraheert.

### Is Aspose.PDF voor .NET compatibel met .NET Core?
Ja, Aspose.PDF voor .NET is volledig compatibel met .NET Core en .NET Framework.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}