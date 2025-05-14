---
"description": "Leer hoe u een PDF naar TIFF converteert met behulp van het Bradley-algoritme in Aspose.PDF voor .NET. Stapsgewijze handleiding, vereisten en veelgestelde vragen voor een naadloze conversie."
"linktitle": "Bradley-algoritme"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Bradley-algoritme"
"url": "/nl/net/programming-with-images/bradley-algorithm/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bradley-algoritme

## Invoering

Werken met PDF-bestanden kan soms meer vergen dan alleen het lezen of bewerken ervan – u moet ze mogelijk converteren naar afbeeldingen. Een krachtige manier om PDF's naar TIFF-afbeeldingen te converteren, is met behulp van het Bradley-algoritme via de Aspose.PDF voor .NET-bibliotheek. Deze methode garandeert binaire afbeeldingen van hoge kwaliteit, perfect voor documentarchivering en andere gespecialiseerde toepassingen.

Deze tutorial leidt je door een gedetailleerd en eenvoudig te volgen proces voor het converteren van een PDF-pagina naar een TIFF-afbeelding met het Bradley Binarization Algorithm. Aspose.PDF voor .NET vereenvoudigt deze taak en biedt je de mogelijkheid om je documentworkflows te automatiseren en te stroomlijnen.

## Vereisten

Voordat we in de code duiken, willen we ervoor zorgen dat je alles hebt wat je nodig hebt om de code te volgen:

- Aspose.PDF voor .NET: Je hebt de bibliotheek nodig. Download deze van [hier](https://releases.aspose.com/pdf/net/).
- Visual Studio (of een andere C# IDE).
- Basiskennis van C#.
- Een geldig rijbewijs of een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) van Aspose.

## Pakketten importeren

Zorg er allereerst voor dat u de benodigde naamruimten in uw project importeert. Deze bibliotheken bieden u de tools om PDF-documenten te bewerken, ze naar TIFF-formaat te converteren en het Bradley-binarisatiealgoritme toe te passen.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Laten we het proces opsplitsen in eenvoudige stappen, zodat u het soepel kunt volgen. Aan het einde van deze handleiding hebt u met succes een PDF-pagina omgezet naar een binaire TIFF-afbeelding met behulp van het Bradley-algoritme.

## Stap 1: Stel de documentmap in

De eerste stap is het opgeven van het pad naar de map waarin uw PDF-document zich bevindt. U definieert ook de uitvoerpaden voor de TIFF-afbeeldingen die worden gegenereerd.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Pad naar uw PDF-bestand
```

Hier sla je zowel de bron-PDF als de geconverteerde TIFF-bestanden op. Zorg ervoor dat de directory correct is ingesteld, zodat de code bestanden foutloos kan lezen en schrijven.

## Stap 2: Open het PDF-document

Nu het pad is ingesteld, is het tijd om het PDF-document te openen dat u wilt converteren. Aspose.PDF voor .NET maakt het eenvoudig om een document te laden voor verdere verwerking.

```csharp
Document pdfDocument = new Document(dataDir + "PageToTIFF.pdf");
```

Hier, `PageToTIFF.pdf` is het voorbeeldbestand. U kunt het vervangen door elk PDF-bestand naar keuze. Het documentobject bevat nu de PDF voor verdere bewerking.

## Stap 3: Uitvoerpaden voor afbeeldingen definiëren

Vervolgens geeft u de uitvoerpaden voor de gegenereerde TIFF-bestanden op, zowel de standaard TIFF als de gebinariseerde versie.

```csharp
string outputImageFile = dataDir + "resultant_out.tif";
string outputBinImageFile = dataDir + "37116-bin_out.tif";
```

Door deze paden te scheiden, ontstaat er één bestand voor de standaard TIFF-conversie en een ander bestand voor de gebinariseerde afbeelding nadat het Bradley-algoritme is toegepast.

## Stap 4: Een resolutieobject maken

Bij het converteren van PDF's naar TIFF speelt de resolutie een belangrijke rol bij het bepalen van de beeldkwaliteit. Voor ons doel stellen we deze in op 300 dpi om een uitvoer van hoge kwaliteit te garanderen.

```csharp
Resolution resolution = new Resolution(300);
```

Een hogere DPI betekent een helderder beeld, vooral bij documenten die moeten worden afgedrukt of gearchiveerd.

## Stap 5: TIFF-instellingen configureren

Vervolgens moet je de instellingen voor de TIFF-afbeelding configureren. We gebruiken LZW-compressie en stellen de kleurdiepte in op 1 bpp (1 bit per pixel) om een binaire afbeelding te verkrijgen.

```csharp
TiffSettings tiffSettings = new TiffSettings();
tiffSettings.Compression = CompressionType.LZW;
tiffSettings.Depth = Aspose.Pdf.Devices.ColorDepth.Format1bpp;
```

Door de diepte in te stellen op 1 bpp, bereiden we de afbeelding voor op binaire uitvoer. LZW-compressie is gekozen vanwege de efficiëntie bij het verkleinen van de bestandsgrootte zonder kwaliteitsverlies.

## Stap 6: Het TIFF-apparaat maken

Nu moet je een TIFF-apparaat aanmaken dat de conversie afhandelt. Dit apparaat gebruikt de eerder gedefinieerde resolutie en TIFF-instellingen.

```csharp
TiffDevice tiffDevice = new TiffDevice(resolution, tiffSettings);
```

Het TIFF-apparaat vormt de kern van deze bewerking. Het neemt het PDF-document en converteert elke pagina naar een TIFF-afbeelding, op basis van uw vooraf gedefinieerde instellingen.

## Stap 7: Converteer de PDF-pagina naar TIFF

Het is tijd om de PDF te verwerken en de eerste pagina om te zetten naar een TIFF-afbeelding. `Process` Met deze methode kunt u specifieke pagina's of het hele document converteren. In dit voorbeeld converteren we de eerste pagina.

```csharp
tiffDevice.Process(pdfDocument, outputImageFile);
```

Zodra de methode is voltooid, is er een TIFF-afbeelding opgeslagen op de eerder gedefinieerde locatie.

## Stap 8: Pas het Bradley-binarisatiealgoritme toe

Nu komt de magie: het Bradley-algoritme! Dit algoritme zet de grijswaarden TIFF-afbeelding om in een binaire afbeelding en optimaliseert deze voor documentherkenningssystemen.

```csharp
using (FileStream inStream = new FileStream(outputImageFile, FileMode.Open))
{
    using (FileStream outStream = new FileStream(outputBinImageFile, FileMode.Create))
    {
        tiffDevice.BinarizeBradley(inStream, outStream, 0.1);
    }
}
```

De BinarizeBradley-methode gebruikt twee bestandsstromen (invoer en uitvoer) en een drempelwaarde (hier `0.1`die het binarisatieniveau bepaalt. Na uitvoering heb je een perfect gebinariseerde afbeelding klaar voor gebruik.

## Stap 9: Bevestig succesvolle conversie

Tot slot is het een goede gewoonte om de gebruiker te laten weten dat het proces succesvol is verlopen. Dit kan met een eenvoudige console-uitvoer.

```csharp
System.Console.WriteLine("Conversion using Bradley algorithm performed successfully!");
```

Zodra dit is afgedrukt, weet u dat uw PDF-pagina succesvol is omgezet naar een binaire TIFF-afbeelding!

## Conclusie

Zo, dat is het! Je hebt net geleerd hoe je een PDF-pagina naar een TIFF-afbeelding converteert en het Bradley-binarisatiealgoritme toepast met Aspose.PDF voor .NET. Dit proces is essentieel voor documentarchivering, optische tekenherkenning (OCR) en andere professionele toepassingen. Dankzij de hoge resolutie en efficiënte compressie kun je ervoor zorgen dat je documentafbeeldingen zowel helder als hanteerbaar zijn.

## Veelgestelde vragen

### Wat is het Bradley-algoritme?
Het Bradley-algoritme is een binarisatietechniek waarmee grijstintenafbeeldingen worden omgezet in binaire (zwart-wit)afbeeldingen door voor elke pixel een adaptieve drempelwaarde te bepalen op basis van de omgeving.

### Kan ik met deze methode meerdere PDF-pagina's naar TIFF converteren?
Ja, u kunt de `Process` Methode om alle pagina's te converteren door door de pagina's in het document te lussen.

### Wat is de optimale resolutie voor het converteren van PDF's naar TIFF?
Voor afbeeldingen van hoge kwaliteit wordt over het algemeen 300 dpi aanbevolen. U kunt deze waarde echter naar wens aanpassen.

### Wat betekent 1bpp in kleurdiepte?
1 bpp (1 bit per pixel) betekent dat de afbeelding zwart-wit is, waarbij elke pixel volledig zwart of volledig wit is.

### Is het Bradley-algoritme geschikt voor OCR?
Ja, het Bradley-algoritme wordt vaak gebruikt bij OCR-voorverwerking omdat het het tekstcontrast in gescande documenten verbetert.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}