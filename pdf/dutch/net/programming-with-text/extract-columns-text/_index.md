---
"description": "Leer hoe u tekstkolommen uit PDF-bestanden kunt extraheren met Aspose.PDF voor .NET. Deze handleiding beschrijft elke stap met codevoorbeelden en uitleg."
"linktitle": "Kolommentekst uit PDF-bestand extraheren"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Kolommentekst uit PDF-bestand extraheren"
"url": "/nl/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kolommentekst uit PDF-bestand extraheren

## Invoering

Werkt u met PDF-bestanden en moet u tekst in een specifieke kolomindeling extraheren? Of u nu facturen, rapporten of gestructureerde documenten verwerkt, het nauwkeurig extraheren van tekst uit een PDF kan lastig zijn. Hier komt Aspose.PDF voor .NET om de hoek kijken om het proces te vereenvoudigen. In deze tutorial laten we u zien hoe u eenvoudig tekstkolommen uit een PDF-bestand kunt extraheren. 

## Vereisten

Voordat we in de code duiken, bespreken we eerst de essentiële zaken die je nodig hebt:

- Aspose.PDF voor .NET: Zorg ervoor dat u de nieuwste versie van Aspose.PDF voor .NET hebt geïnstalleerd. Zo niet, dan kunt u [download het hier](https://releases.aspose.com/pdf/net/).
- Ontwikkelomgeving: Om met de code te kunnen werken, hebt u Visual Studio of een andere .NET-ontwikkelomgeving nodig.
- PDF-document: Zorg dat u een voorbeeld-PDF-document bij de hand hebt, bij voorkeur een document met tekstkolommen, aangezien we er tekst uit gaan halen.

Als u Aspose.PDF voor .NET nog niet hebt geïnstalleerd, kunt u een [gratis proefperiode](https://releases.aspose.com/) of [een licentie kopen](https://purchase.aspose.com/buy) voor alle functies. U kunt ook een aanvraag indienen voor een [tijdelijke licentie](https://purchase.aspose.com/temporary-license) indien nodig.

## Naamruimten importeren

Om Aspose.PDF voor .NET in uw project te gebruiken, moet u de volgende naamruimten importeren:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## Stapsgewijze handleiding: tekstkolommen uit een PDF extraheren

Laten we nu elk onderdeel van de code uitsplitsen om beter te begrijpen hoe het werkt. Volg mee terwijl we stap voor stap elk onderdeel van het proces uitleggen.

## Stap 1: Het PDF-document laden

Het eerste dat u moet doen, is uw PDF-bestand in de `Document` object. Dit is hoe Aspose.PDF met uw document samenwerkt.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

In deze stap definiëren we eenvoudigweg de map waarin uw PDF-document is opgeslagen. Vervangen `"YOUR DOCUMENT DIRECTORY"` met het pad naar uw lokale PDF-bestand. De `Document` object laadt de PDF in het geheugen, waardoor deze toegankelijk is voor verdere verwerking.

## Stap 2: De tekstfragmentabsorber instellen

Vervolgens gebruiken we een `TextFragmentAbsorber` Om alle tekst uit het PDF-bestand te absorberen of vast te leggen. Deze absorberklasse is ontworpen om tekstfragmenten uit specifieke delen van uw PDF te extraheren, wat hem ideaal maakt voor het extraheren van tekstkolommen.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

Hier maken we een instantie van `TextFragmentAbsorber` en pas het toe op alle pagina's van de PDF met behulp van `Accept()`. De `TextFragmentCollection` slaat de geëxtraheerde tekst op, en uit deze verzameling kunnen we tekst naar behoefte manipuleren of extraheren.

## Stap 3: Pas de lettergrootte van de geëxtraheerde tekst aan

Nadat je de tekstfragmenten hebt vastgelegd, kun je de lettergrootte verkleinen, vooral als de oorspronkelijke tekst te groot is. In dit voorbeeld verkleinen we de lettergrootte met 70%.

```csharp
foreach (TextFragment tf in tfc)
{
    // Verklein het lettertype met 70%
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

Deze code loopt door elk `TextFragment` in de collectie en verkleint de lettergrootte met 70%. Door de lettergrootte aan te passen, kunt u de geëxtraheerde tekst gemakkelijker beheren, vooral als u deze voor verschillende doeleinden opmaakt.

## Stap 4: Sla het document op in een geheugenstroom

Nadat we de tekst hebben aangepast, slaan we de PDF op in een `MemoryStream`Hierdoor kunnen we het document in het geheugen bewaren voor verdere verwerking, zonder dat we het terug naar de schijf hoeven te schrijven.

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

Hier slaan we de PDF op in een geheugenstroom en laden we het document vervolgens opnieuw. Deze methode is handig wanneer u met grote bestanden werkt en onnodige schijfbewerkingen wilt vermijden.

## Stap 5: Alle tekst extraheren met Text Absorber

Nu we de PDF hebben voorbereid, is het tijd om de tekst te extraheren. We gebruiken `TextAbsorber` om alle tekst uit het document te halen.

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

In deze stap wordt de `TextAbsorber` absorbeert alle tekst uit de PDF en de geëxtraheerde tekst wordt opgeslagen in de `extractedText` string. Dit is waar de magie gebeurt: uw tekstkolommen staan nu in platte-tekstformaat!

## Stap 6: Sla de geëxtraheerde tekst op in een bestand

Ten slotte slaan we de geëxtraheerde tekst op in een `.txt` bestand voor eenvoudige toegang en verder gebruik.

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

Deze code schrijft de geëxtraheerde tekst naar een nieuw bestand. `.txt` bestand en slaat het op in de door u opgegeven directory. Er wordt een bericht in de console weergegeven ter bevestiging dat het proces succesvol is verlopen.

## Conclusie

Zo, dat is het! Het extraheren van tekstkolommen uit een PDF-bestand met Aspose.PDF voor .NET is eenvoudiger dan je zou denken. Met slechts een paar regels code kun je een PDF laden, specifieke tekst extraheren, de opmaak aanpassen en de resultaten opslaan in een tekstbestand.

Deze techniek is ongelooflijk handig voor het verwerken van gestructureerde documenten zoals tabellen, rapporten of in kolommen georganiseerde content. Of u nu de data-extractie wilt automatiseren of bulkdocumenten wilt verwerken, Aspose.PDF biedt de tools om dit efficiënt te doen.

## Veelgestelde vragen

### Kan ik tekst uit specifieke pagina's van een PDF halen?  
Ja! U kunt de `TextFragmentAbsorber` om specifieke pagina's te targeten met behulp van de `pdfDocument.Pages[pageIndex].Accept(tfa);` methode.

### Is het mogelijk om tekst uit slechts één kolom te halen in een PDF met meerdere kolommen?  
Ja, maar je moet met de coördinaten van de tekstfragmenten werken met behulp van `TextFragment.Rectangle` om specifieke delen van het document te targeten.

### Hoe kan ik de nauwkeurigheid van tekstextractie verbeteren?  
Voor een betere nauwkeurigheid zorgt u ervoor dat de structuur van de PDF goed gedefinieerd is en vermijdt u documenten met een complexe lay-out. U kunt de `TextFragmentAbsorber` om tekst te extraheren op basis van lettertypen, -grootten of -regio's.

### Ondersteunt Aspose.PDF tekst extractie uit gescande documenten?  
Ja, maar je hebt OCR-technologie (Optical Character Recognition) nodig. Aspose biedt hiervoor ook tools.

### Hoe ga ik om met grote PDF-bestanden met duizenden pagina's?  
Bij grote PDF-bestanden kunt u het document in delen verwerken door tekst uit een paar pagina's tegelijk te halen. Zo voorkomt u een hoog geheugengebruik.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}