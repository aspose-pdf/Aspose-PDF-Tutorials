---
"description": "Leer hoe u een afbeelding en paginanummer inline in de headersectie van een PDF kunt toevoegen met Aspose.PDF voor .NET met behulp van deze stapsgewijze handleiding."
"linktitle": "Afbeelding en paginanummer in koptekst-voettekstsectie inline"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Afbeelding en paginanummer in koptekst-voettekstsectie inline"
"url": "/nl/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section-inline/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Afbeelding en paginanummer in koptekst-voettekstsectie inline

## Invoering

Aspose.PDF voor .NET is een krachtige tool met uitgebreide mogelijkheden voor het bewerken en genereren van PDF-bestanden. Of u nu afbeeldingen wilt toevoegen, kop- en voetteksten wilt aanpassen of tekst wilt beheren, Aspose.PDF helpt u daarbij. In deze tutorial laten we zien hoe u een afbeelding en een paginanummer inline in de kop- of voettekst van een PDF-document kunt toevoegen. Laten we meteen aan de slag gaan en het proces stap voor stap uitleggen.

## Vereisten

Voordat we met de code aan de slag gaan, willen we ervoor zorgen dat je alles paraat hebt om de stappen te kunnen volgen:

- Aspose.PDF voor .NET: Download de nieuwste versie van de [Aspose PDF-downloadpagina](https://releases.aspose.com/pdf/net/).
- Ontwikkelomgeving: U hebt een C# IDE nodig, zoals Visual Studio.
- Licentie: Als u nog geen licentie heeft, kunt u een [tijdelijke licentie hier](https://purchase.aspose.com/temporary-license/) of koop een volledige van de [Aspose-winkel](https://purchase.aspose.com/buy).

Nu u aan de vereisten voldoet, kunnen we beginnen.

## Pakketten importeren

Voordat u begint met coderen, moet u ervoor zorgen dat u de benodigde naamruimten importeert:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Met deze pakketten kunt u met PDF-bestanden werken en tekst bewerken.

## Stap 1: De documentenmap instellen

Het eerste wat we moeten doen, is het pad definiëren naar de map waar ons PDF-bestand wordt opgeslagen. Dit pad kan worden aangepast naar de map van uw project of naar een andere locatie op uw computer.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Deze variabele bevat de locatie waar uw document wordt opgeslagen. Vervangen `"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad.

## Stap 2: Het PDF-document instantiëren

In deze stap maken we een nieuw exemplaar van de `Aspose.Pdf.Document` object. Dit object vormt de ruggengraat van uw PDF-bestand.

```csharp
// Een Document-object instantiëren door de lege constructor aan te roepen
Aspose.Pdf.Document pdf1 = new Aspose.Pdf.Document();
```

Hier maken we een leeg PDF-bestand dat we later met inhoud kunnen vullen.

## Stap 3: Een pagina toevoegen aan de PDF

Je PDF moet minstens één pagina bevatten waar je kopteksten, voetteksten en inhoud kunt toevoegen. Laten we een lege pagina aan ons document toevoegen.

```csharp
// Een pagina maken in het PDF-object
Aspose.Pdf.Page page = pdf1.Pages.Add();
```

Door te bellen `pdf1.Pages.Add()`, er wordt een nieuwe pagina aan het document toegevoegd, klaar voor aanpassing van de kop- en voettekst.

## Stap 4: De koptekst maken en instellen

Nu is het tijd om de koptekst voor het document te maken. Hier voegen we de tekst, afbeelding en paginanummer toe.

```csharp
// Maak een koptekstsectie van het document
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
// Stel de koptekst voor het PDF-bestand in
page.Header = header;
```

Wij creëren een `HeaderFooter` object en wijs het toe aan de `Header` eigenschap van de pagina, zodat alles wat we aan de header toevoegen, bovenaan de pagina verschijnt.

## Stap 5: Inline-tekst toevoegen aan de koptekst

Het toevoegen van tekst is net zo eenvoudig als het maken van een `TextFragment` en de eigenschappen ervan specificeren. Laten we wat gekleurde tekst aan onze header toevoegen.

```csharp
// Een tekstobject maken
Aspose.Pdf.Text.TextFragment txt1 = new Aspose.Pdf.Text.TextFragment("Aspose.Pdf is a Robust component by");
// Geef de kleur op
txt1.TextState.ForegroundColor = Color.Blue;
txt1.IsInLineParagraph = true;
```

In deze stap maken we een `TextFragment` met de inhoud "Aspose.Pdf is een robuust onderdeel van" en stel de kleur in op blauw. `IsInLineParagraph` Deze eigenschap zorgt ervoor dat de tekst inline staat, wat betekent dat deze op dezelfde regel wordt weergegeven als de andere elementen (zoals de afbeelding en aanvullende tekst).

## Stap 6: Een inline-afbeelding in de koptekst invoegen

Om je header visueel aantrekkelijk te maken, kun je een afbeelding in de tekst plaatsen. Dit kan je bedrijfslogo of een andere afbeelding zijn.

```csharp
// Maak een afbeeldingobject in de sectie
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
// Stel het pad van het afbeeldingsbestand in
image1.File = dataDir + "aspose-logo.jpg";
// Stel de afbeeldingsbreedte in Informatie
image1.FixWidth = 50;
image1.FixHeight = 20;
// Geeft aan dat de InlineParagraph van seg1 een afbeelding is.
image1.IsInLineParagraph = true;
```

Hier voegen we een afbeelding toe aan de header door een `Image` object, het pad ervan instellen en de breedte en hoogte aanpassen. De `IsInLineParagraph` zorgt ervoor dat de afbeelding uitgelijnd is met de tekst.

## Stap 7: Voeg extra inline tekst toe om de koptekst te voltooien

Voeg nog wat tekst toe om de inline-header te voltooien.

```csharp
Aspose.Pdf.Text.TextFragment txt2 = new Aspose.Pdf.Text.TextFragment(" Pty Ltd.");
txt2.IsInLineParagraph = true;
txt2.TextState.ForegroundColor = Color.Maroon;
header.Paragraphs.Add(txt1);
header.Paragraphs.Add(image1);
header.Paragraphs.Add(txt2);
```

In dit onderdeel maken we nog een `TextFragment` met de inhoud "Pty Ltd." en stel de kleur in op kastanjebruin. Zowel tekstfragmenten als de afbeelding worden aan de koptekst toegevoegd.

## Stap 8: Sla de PDF op

Nadat u de koptekst hebt ingesteld, kunt u de PDF opslaan.

```csharp
// PDF opslaan
pdf1.Save(dataDir + "ImageAndPageNumberInHeaderFooter_UsingInlineParagraph_out.pdf");
```

De `Save` methode schrijft het uiteindelijke PDF-bestand naar de opgegeven locatie.

## Conclusie

Gefeliciteerd! U hebt met succes een afbeelding en tekst toegevoegd aan de koptekst van een PDF-document met Aspose.PDF voor .NET. Deze tutorial heeft u door de essentiële stappen geleid, waaronder het maken van een document, het toevoegen van pagina's, het invoegen van kopteksten en het plaatsen van inline content zoals tekst en afbeeldingen. Aspose.PDF biedt u ongelooflijke flexibiliteit bij het beheren van uw PDF's, of het nu gaat om het bewerken van kopteksten, voetteksten of complexe content. 

## Veelgestelde vragen

### Kan ik ook een paginanummer aan de koptekst toevoegen?
Ja! U kunt eenvoudig een paginanummer toevoegen met behulp van de `TextFragment` klasse en formatteer deze naar behoefte. Plaats hem gewoon in de headersectie als inline-inhoud.

### Hoe stel ik een achtergrondafbeelding in de header in?
Je kunt de `BackgroundImage` eigendom van de `HeaderFooter` klasse om een achtergrondafbeelding in te stellen. Dit is echter geen inline-inhoud en zal de volledige header bedekken.

### Is het mogelijk om andere afbeeldingformaten dan JPEG te gebruiken?
Absoluut! Aspose.PDF ondersteunt verschillende afbeeldingsformaten zoals PNG, BMP en GIF.

### Kan ik het lettertype van de tekst in de koptekst aanpassen?
Ja, u kunt de `TextState` object om het lettertype, de grootte en de stijl van de tekst te wijzigen.

### Heb ik een licentie nodig om Aspose.PDF voor .NET te gebruiken?
Ja, Aspose.PDF vereist een licentie voor productiegebruik, maar u kunt beginnen met een [gratis proefperiode hier](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}