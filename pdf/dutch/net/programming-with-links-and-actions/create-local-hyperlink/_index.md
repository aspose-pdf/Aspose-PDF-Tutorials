---
"description": "Leer hoe u met Aspose.PDF voor .NET moeiteloos lokale hyperlinks in PDF-bestanden kunt maken met behulp van onze stapsgewijze handleiding."
"linktitle": "Lokale hyperlink maken in PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Lokale hyperlink maken in PDF-bestand"
"url": "/nl/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lokale hyperlink maken in PDF-bestand

## Invoering

In deze handleiding leiden we je door het proces van het maken van lokale hyperlinks in een PDF-bestand met Aspose.PDF voor .NET. We leggen elke stap duidelijk uit, zodat je het moeiteloos kunt volgen, zelfs als je nieuw bent in de wereld van PDF-bewerking.

## Vereisten

Voordat we ons in de code verdiepen, controleren we eerst of je alles hebt wat je nodig hebt:

1. Visual Studio: Dit heb je nodig om je .NET-applicaties te ontwikkelen. Download het van de [website](https://visualstudio.microsoft.com/).
2. Aspose.PDF voor .NET: U kunt deze bibliotheek downloaden via de [downloadlink hier](https://releases.aspose.com/pdf/net/)Het wordt geleverd met een uitgebreide reeks functies voor PDF-manipulatie.
3. Basiskennis van C#: Een beetje kennis van C#-programmering is handig, maar maak je geen zorgen: we gaan de code regel voor regel doornemen.
4. .NET Framework: Zorg ervoor dat .NET Framework op uw computer is geïnstalleerd. U kunt de vereisten bekijken in Aspose.PDF. [documentatie](https://reference.aspose.com/pdf/net/).

Nu u aan deze vereisten hebt voldaan, kunt u leren hoe u lokale hyperlinks in uw PDF-documenten kunt maken!

## Pakketten importeren

Nu je helemaal klaar bent, is het tijd om de benodigde pakketten in je C#-project te importeren. De Aspose.PDF-bibliotheek bevat alle klassen die we nodig hebben. Zo doe je dat:

### Open uw project

Open je bestaande .NET-project of maak een nieuw project in Visual Studio. Als je helemaal opnieuw begint, selecteer je 'Een nieuw project maken' in het opstartscherm.

### Referentie toevoegen aan Aspose.PDF

Klik met de rechtermuisknop op 'Afhankelijkheden' in uw projectmap in Solution Explorer. Selecteer 'NuGet-pakketten beheren' en zoek naar `Aspose.PDF`Installeer de nieuwste versie. Hiermee krijgt u alle tools die u nodig hebt voor het maken en bewerken van PDF's.

### Naamruimten importeren

Voeg bovenaan uw .cs-bestand using -richtlijnen toe voor de Aspose.PDF-bibliotheek, zoals deze:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Op deze manier krijgt u toegang tot de functies van de bibliotheek.

Laten we het proces van het maken van lokale hyperlinks opsplitsen in eenvoudige stappen. Elke stap wordt uitgebreid uitgelegd, zodat u de logica erachter begrijpt.

## Stap 1: Documentinstantie instellen

In deze stap maakt u een nieuw exemplaar van de klasse Document. Dit exemplaar vertegenwoordigt het PDF-bestand waarmee u gaat werken.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Stel uw documentmap in
Document doc = new Document(); // Documentinstantie maken
```
De `dataDir` variabele is waar uw nieuw aangemaakte PDF zal worden opgeslagen. U moet `"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad op uw systeem. De `Document` klasse maakt een nieuw PDF-document waar we pagina's en links aan kunnen toevoegen.

## Stap 2: Een pagina toevoegen aan het document

Vervolgens voegt u een pagina toe aan uw PDF-document. 

```csharp
Page page = doc.Pages.Add(); // Pagina toevoegen aan paginaverzameling
```
De `Pages.Add()` De methode voegt een nieuwe pagina toe aan het document. Hier komt al je content te staan.

## Stap 3: Een tekstfragment maken

Laten we nu een stuk tekst maken dat als klikbare link fungeert.

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
De `TextFragment` vertegenwoordigt een tekstfragment in de PDF. Hier maken we een link die gebruikers naar pagina 7 brengt.

## Stap 4: Lokale hyperlink maken

Hier gebeurt de magie! Je moet een lokale hyperlink maken die het tekstfragment vertelt waar het naartoe moet verwijzen.

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // Lokale hyperlink maken
link.TargetPageNumber = 7; // Doelpagina instellen voor linkinstantie
text.Hyperlink = link; // Hyperlink TextFragment instellen
```
De `LocalHyperlink` klasse is wat ons in staat stelt om naar andere pagina's in hetzelfde document te verwijzen. Door `TargetPageNumber` tot en met 7, vertelt u de hyperlink dat deze naar de specifieke pagina moet springen als erop wordt geklikt.

## Stap 5: Voeg het tekstfragment toe aan de pagina

Nadat u de hyperlink hebt ingesteld, is het tijd om ons tekstfragment toe te voegen aan de pagina die u hebt gemaakt.

```csharp
page.Paragraphs.Add(text); // Tekst toevoegen aan alineaverzameling van pagina
```
Met deze regel voegt u uw klikbare tekst toe aan de verzameling alinea's van de pagina.

## Stap 6: Maak een ander tekstfragment (optioneel)

Laten we een extra hyperlink toevoegen om terug te navigeren naar pagina 1.

```csharp
text = new TextFragment("link page number test to page 1"); // Nieuw tekstfragment maken
text.IsInNewPage = true; // Voeg het toe aan een nieuwe pagina
```
Een nieuwe maken `TextFragment` voor de tweede link hebben we ingesteld `IsInNewPage` naar true, wat aangeeft dat deze tekst op een nieuwe pagina wordt geplaatst.

## Stap 7: De tweede lokale hyperlink instellen

Net als voorheen maak je nog een lokale hyperlink voor pagina 1.

```csharp
link = new LocalHyperlink(); // Een ander lokaal hyperlinkexemplaar maken
link.TargetPageNumber = 1; // Doelpagina instellen voor tweede hyperlink
text.Hyperlink = link; // Link instellen voor tweede TextFragment
```
Deze hyperlink verwijst naar pagina 1, zodat gebruikers terug kunnen gaan naar de tweede pagina.

## Stap 8: Voeg het tweede tekstfragment toe aan de nieuwe pagina

Laten we deze tekst nu aan de pagina toevoegen.

```csharp
page.Paragraphs.Add(text); // Tekst toevoegen aan alineaverzameling van pagina-object
```
Op dezelfde manier als bij stap 5 voegt deze regel de nieuwe hyperlinktekst toe aan de nieuw aangemaakte pagina.

## Stap 9: Sla het document op

Eindelijk is het tijd om je harde werk op te slaan! 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // Geef de naam van het uitvoerbestand op
doc.Save(dataDir); // Bijgewerkt document opslaan
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
Dit combineert uw directorypad met de bestandsnaam. De `Save()` Met deze methode wordt uw document opgeslagen en ontvangt u een bevestigingsbericht dat alles goed is verlopen!

## Conclusie

Het maken van lokale hyperlinks in PDF-bestanden met Aspose.PDF voor .NET is niet zomaar een handige truc; het is een praktische functie die de navigatie en gebruikerservaring verbetert. U beschikt nu over de kennis om uw lezers direct naar de informatie te leiden die ze nodig hebben. Denk maar eens terug aan onze eerste vergelijking: geen verloren zielen meer die door eindeloze pagina's dwalen.

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een bibliotheek waarmee ontwikkelaars programmatisch PDF-documenten kunnen maken, bewerken en converteren met behulp van het .NET Framework.

### Kan ik hyperlinks maken naar externe webpagina's?
Ja, Aspose.PDF ondersteunt ook het maken van hyperlinks naar externe URL's, naast lokale hyperlinks binnen de PDF.

### Is er een gratis proefversie voor Aspose.PDF?
Absoluut! Je kunt de gratis proefperiode bekijken via de [site](https://releases.aspose.com/).

### Welke programmeertalen ondersteunt Aspose?
Aspose biedt bibliotheken voor verschillende programmeertalen, waaronder Java, C++ en Python.

### Hoe krijg ik ondersteuning voor Aspose-producten?
U kunt ondersteuning zoeken via de [Aspose Forum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}