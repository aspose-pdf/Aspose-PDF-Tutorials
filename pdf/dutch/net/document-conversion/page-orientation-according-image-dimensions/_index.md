---
"description": "Leer in deze stapsgewijze handleiding hoe u PDF's maakt met Aspose.PDF voor .NET en hoe u de pagina-oriëntatie instelt op basis van de afmetingen van afbeeldingen."
"linktitle": "Pagina-oriëntatie volgens afbeeldingsafmetingen"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Pagina-oriëntatie volgens afbeeldingsafmetingen"
"url": "/nl/net/document-conversion/page-orientation-according-image-dimensions/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Pagina-oriëntatie volgens afbeeldingsafmetingen

## Invoering

Welkom in de wereld van Aspose.PDF voor .NET! Als je programmatisch PDF-documenten wilt maken, bewerken of converteren, ben je hier aan het juiste adres. Aspose.PDF is een krachtige bibliotheek waarmee ontwikkelaars naadloos met PDF-bestanden kunnen werken. In deze handleiding leiden we je door het proces van het instellen van pagina-oriëntaties op basis van afbeeldingsafmetingen. Of je nu een ervaren ontwikkelaar bent of net begint, deze tutorial geeft je de kennis die je nodig hebt om aan de slag te gaan met Aspose.PDF.

## Vereisten

Voordat we in de code duiken, willen we ervoor zorgen dat je alles hebt wat je nodig hebt om dit te kunnen volgen:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. Dit is de beste IDE voor .NET-ontwikkeling.
2. .NET Framework: In deze handleiding wordt ervan uitgegaan dat u .NET Framework gebruikt. Zorg ervoor dat u de juiste versie hebt geïnstalleerd.
3. Aspose.PDF voor .NET: U kunt de bibliotheek downloaden van de [Aspose-website](https://releases.aspose.com/pdf/net/)Als je het eerst wilt uitproberen, kun je een [gratis proefperiode](https://releases.aspose.com/).
4. Basiskennis van C#: Kennis van C#-programmering helpt u de voorbeelden beter te begrijpen.

## Pakketten importeren

Om te beginnen moet je de benodigde pakketten importeren. Zo doe je dat:

1. Open uw Visual Studio-project.
2. Klik met de rechtermuisknop op uw project in Solution Explorer en selecteer 'NuGet-pakketten beheren'.
3. Zoeken naar `Aspose.PDF` en installeer het.

Nu we alles hebben ingesteld, gaan we het voorbeeld stap voor stap bekijken.

## Stap 1: Stel uw documentenmap in

Allereerst moet u het pad opgeven naar de documentenmap waar uw afbeeldingen zijn opgeslagen. Dit is waar Aspose de JPG-bestanden zal zoeken.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Vervangen `"YOUR DOCUMENT DIRECTORY"` met het daadwerkelijke pad waar uw afbeeldingen zich bevinden. Dit is cruciaal, want als Aspose uw afbeeldingen niet kan vinden, kan het de PDF niet aanmaken.

## Stap 2: Een nieuw PDF-document maken

Vervolgens maak je een nieuw PDF-documentobject aan. Hier worden al je afbeeldingen aan toegevoegd.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Deze regel initialiseert een nieuw exemplaar van de `Document` klasse, die uw PDF-bestand vertegenwoordigt.

## Stap 3: Afbeeldingsbestanden ophalen

Laten we nu alle JPG-bestanden uit de opgegeven map ophalen. Dit doen we met behulp van de `Directory.GetFiles` methode.

```csharp
string[] fileEntries = Directory.GetFiles(dataDir, "*.JPG");
```

Deze regel geeft je een reeks bestandsnamen die overeenkomen met het JPG-formaat. Zorg ervoor dat je map JPG-afbeeldingen bevat om dit te laten werken!

## Stap 4: Loop door elke afbeelding

Je moet elk afbeeldingsbestand doorlopen en aan het PDF-document toevoegen. Zo doe je dat:

```csharp
int counter;
for (counter = 0; counter < fileEntries.Length - 1; counter++)
{
    // Een paginaobject maken
    Aspose.Pdf.Page page = doc.Pages.Add();
```

In deze lus maak je voor elke afbeelding een nieuwe pagina aan. `doc.Pages.Add()` Met deze methode wordt een nieuwe pagina aan uw PDF-document toegevoegd.

## Stap 5: Een afbeeldingobject maken

Voor elke afbeelding moet u een `Image` object dat de beeldgegevens zal bevatten.

```csharp
    Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
    image1.File = fileEntries[counter];
```

Hier wijst u het huidige afbeeldingsbestand toe aan de `Image` object. Dit is essentieel voor het toevoegen van de afbeelding aan de PDF.

## Stap 6: Controleer de afmetingen van de afbeelding

Voordat u de afbeelding aan het PDF-bestand toevoegt, moet u de afmetingen controleren om de pagina-indeling te bepalen.

```csharp
    Bitmap myimage = new Bitmap(fileEntries[counter]);
    if (myimage.Width > page.PageInfo.Width)
        page.PageInfo.IsLandscape = true;
    else
        page.PageInfo.IsLandscape = false;
```

Dit codefragment controleert of de breedte van de afbeelding groter is dan de paginabreedte. Zo ja, dan wordt de pagina-oriëntatie ingesteld op liggend; anders blijft de pagina in staande modus.

## Stap 7: Voeg de afbeelding toe aan de PDF

Nu u de oriëntatie hebt ingesteld, is het tijd om de afbeelding aan het PDF-document toe te voegen.

```csharp
    page.Paragraphs.Add(image1);
}
```

Deze regel voegt de afbeelding toe aan de alineaverzameling van de huidige pagina. Het is alsof je een afbeelding in een kader plaatst!

## Stap 8: Sla het PDF-document op

Ten slotte moet u het PDF-document opslaan in de door u opgegeven directory.

```csharp
doc.Save(dataDir + "SetPageOrientation_out.pdf");
```

Deze regel slaat het document op met de naam `SetPageOrientation_out.pdf`Controleer uw documentenmap voor de nieuw aangemaakte PDF!

## Conclusie

En voilà! Je hebt met succes een PDF-document gemaakt met Aspose.PDF voor .NET, waarbij je de pagina-oriëntatie hebt ingesteld op basis van de afmetingen van de afbeeldingen. Deze krachtige bibliotheek opent een wereld aan mogelijkheden voor het werken met PDF-bestanden in je applicaties. Of je nu rapporten, facturen of andere documenten genereert, Aspose.PDF staat voor je klaar.

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een bibliotheek waarmee ontwikkelaars programmatisch PDF-documenten kunnen maken, bewerken en converteren.

### Hoe installeer ik Aspose.PDF?
U kunt Aspose.PDF installeren via NuGet Package Manager in Visual Studio of het downloaden van de [Aspose-website](https://releases.aspose.com/pdf/net/).

### Kan ik Aspose.PDF gratis gebruiken?
Ja, Aspose biedt een [gratis proefperiode](https://releases.aspose.com/) zodat u de bibliotheek kunt testen voordat u tot aankoop overgaat.

### Waar kan ik ondersteuning vinden voor Aspose.PDF?
U kunt ondersteuning vinden op de [Aspose-forum](https://forum.aspose.com/c/pdf/10).

### Welke bestandstypen kan ik met Aspose naar PDF converteren?
Aspose.PDF ondersteunt een breed scala aan bestandsindelingen, waaronder afbeeldingen, Word-documenten, Excel-spreadsheets en meer.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}