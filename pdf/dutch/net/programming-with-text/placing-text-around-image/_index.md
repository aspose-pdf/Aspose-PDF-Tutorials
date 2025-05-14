---
"description": "Leer hoe u tekst rond afbeeldingen in PDF's plaatst met Aspose.PDF voor .NET. Volg onze stapsgewijze handleiding om professionele PDF's te maken met afbeeldingen en tekst naast elkaar."
"linktitle": "Tekst rond een afbeelding in een PDF-bestand plaatsen"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Tekst rond een afbeelding in een PDF-bestand plaatsen"
"url": "/nl/net/programming-with-text/placing-text-around-image/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tekst rond een afbeelding in een PDF-bestand plaatsen

## Invoering

Heb je ooit geprobeerd tekst rond een afbeelding in een PDF-bestand te plaatsen, maar vond je het lastig? Zo ja, dan ben je hier aan het juiste adres! Aspose.PDF voor .NET maakt dit proces eenvoudig, waardoor je met slechts een paar regels code tekst naast afbeeldingen kunt plaatsen. Of je nu rapporten, documenten of presentaties maakt, deze functie is een fantastische manier om de lay-out van je content te verbeteren en visueel aantrekkelijker te maken. Vandaag laten we zien hoe je Aspose.PDF voor .NET kunt gebruiken om tekst rond afbeeldingen in een PDF-document te plaatsen.

## Vereisten

Voordat we de code induiken, zorgen we ervoor dat alles klaar staat. Dit heb je nodig:

- Aspose.PDF voor .NET: U kunt het downloaden van [hier](https://releases.aspose.com/pdf/net/).
- Visual Studio: Zorg ervoor dat u de nieuwste versie hebt geïnstalleerd, zodat u soepel kunt werken.
- .NET Framework: In dit voorbeeld wordt .NET gebruikt. Zorg er dus voor dat uw omgeving is ingesteld voor .NET-ontwikkeling.
- Een tijdelijke licentie: U kunt een tijdelijke licentie aanvragen [hier](https://purchase.aspose.com/temporary-license/) als u het product evalueert.

Als u Aspose.PDF voor .NET nog niet hebt ingesteld, volgt u de installatie-instructies in de [documentatie](https://reference.aspose.com/pdf/net/).

## Naamruimten importeren

Voordat we beginnen met coderen, moeten we de benodigde naamruimten importeren. Hier is het codefragment dat daarvoor nodig is:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Deze naamruimten zijn essentieel omdat ze toegang bieden tot klassen zoals `Document`, `Page`, `Image`, En `HtmlFragment`, waarmee we de PDF gaan maken en bewerken.

Nu we de basis hebben gelegd, laten we eens kijken hoe je tekst rond een afbeelding in je PDF-bestand plaatst met Aspose.PDF voor .NET. We leiden je hier stap voor stap doorheen.

## Stap 1: Instantieer het documentobject

Eerst moet je een PDF-document maken. In Aspose.PDF doe je dit door een `Document` object. Dit object vormt de basis voor alle content die we toevoegen.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

We hebben hier een leeg PDF-document gemaakt. Het bevat nog geen pagina's, maar maak je geen zorgen, we voegen er in de volgende stap een toe.

## Stap 2: Een pagina toevoegen aan het document

Nu we ons document hebben, is het tijd om een pagina toe te voegen. Zie dit als het creëren van een leeg vel papier waar je je content op plaatst.

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

Deze code voegt een nieuwe pagina toe aan het document. Standaard is de pagina leeg, maar dat gaan we veranderen.

## Stap 3: Maak een tabel om inhoud te organiseren

Om de afbeelding en tekst goed uitgelijnd te houden, gebruiken we een tabel. Tabellen in pdf's kunnen je helpen bij het structureren van je lay-out, net als in Word-documenten of HTML.

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
page.Paragraphs.Add(table1);
```

Dit fragment maakt een tabel en voegt deze toe aan de pagina. Beschouw de tabel als het kader voor het uitlijnen van je afbeelding en tekst.

## Stap 4: Kolombreedtes voor de tabel instellen

Nu we een tabel hebben toegevoegd, moeten we bepalen hoe breed de kolommen moeten zijn. Dit zorgt ervoor dat de afbeelding en tekst de juiste afmetingen op de pagina hebben.

```csharp
table1.ColumnWidths = "120 270";
```

Deze lijn stelt de breedte van twee kolommen in: één voor de afbeelding en één voor de tekst. Pas deze waarden aan als uw afbeelding of tekst meer of minder ruimte nodig heeft.

## Stap 5: Marges en opvulling definiëren

Om er zeker van te zijn dat alles er netjes uitziet, voegen we wat marges en opvulling toe aan de tabel.

```csharp
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;
table1.DefaultCellPadding = margin;
```

Met deze instellingen weet u zeker dat de tabel een consistente regelafstand heeft, waardoor de inhoud visueel aantrekkelijk wordt.

## Stap 6: Een afbeelding in de tabel invoegen

Laten we nu naar het leukste gedeelte gaan: een afbeelding toevoegen. In dit geval voegen we het Aspose-logo toe, maar je kunt gerust elke gewenste afbeelding gebruiken.

```csharp
Aspose.Pdf.Row row1 = table1.Rows.Add();
Aspose.Pdf.Image logo = new Aspose.Pdf.Image();
logo.File = dataDir + "aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;
row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```

Dit is wat er gebeurt:
- Wij laden de afbeelding uit de door u opgegeven directory.
- Wij stellen de hoogte en breedte van de afbeelding in.
- Ten slotte voegen we de afbeelding toe aan de eerste cel in de tabel.

## Stap 7: Voeg tekst toe naast de afbeelding

Nu de afbeelding op zijn plaats staat, voegen we er wat tekst aan toe. In dit voorbeeld gebruiken we HTML-tekst om de inhoud vorm te geven.

```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component that enables .NET applications to <b>create PDF documents from scratch</b> without utilizing Adobe Acrobat.</font>";

Aspose.Pdf.HtmlFragment TitleText = new Aspose.Pdf.HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);
```

Dit blok voegt een gestileerde titel en beschrijving toe aan de cel naast de afbeelding. Je kunt de tekst opmaken met HTML-tags voor meer personalisatie.

## Stap 8: Verticale uitlijning aanpassen

Standaard wordt de inhoud van tabelcellen mogelijk niet uitgelijnd zoals u wilt. In dit geval willen we ervoor zorgen dat de tekst bovenaan de cel wordt uitgelijnd.

```csharp
row1.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
```

Hierdoor staat de tekst bovenaan de cel en blijft de lay-out netjes en professioneel.

## Stap 9: Voeg meer tekst toe onder de afbeelding en beschrijving

Mogelijk wilt u meer inhoud onder de afbeelding en tekst plaatsen. Laten we hiervoor een extra rij aan de tabel toevoegen.

```csharp
Aspose.Pdf.Row SecondRow = table1.Rows.Add();
SecondRow.Cells.Add();
SecondRow.Cells[0].ColSpan = 2;
SecondRow.Cells[0].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;

string SecondRowString = "<font face=\"Arial\" size=2>Aspose.Pdf for .NET supports the creation of PDF files through API and XML or XSL-FO templates.</font>";
Aspose.Pdf.HtmlFragment SecondRowText = new Aspose.Pdf.HtmlFragment(SecondRowString);
SecondRow.Cells[0].Paragraphs.Add(SecondRowText);
```

Hier hebben we nog een rij met extra tekst toegevoegd, verdeeld over beide kolommen, om een evenwicht in de lay-out te behouden.

## Stap 10: Sla het PDF-document op

Ten slotte moeten we het document opslaan, zodat u de wijzigingen kunt bekijken.

```csharp
doc.Save(dataDir + "PlacingTextAroundImage_out.pdf");
```

Hiermee wordt het PDF-bestand opgeslagen met de afbeelding en tekst in de opmaak die u wenst.

## Conclusie

Het plaatsen van tekst rond afbeeldingen in een PDF lijkt misschien een lastige klus, maar Aspose.PDF voor .NET vereenvoudigt het proces. Door gebruik te maken van tabellen, afbeeldingen en opgemaakte tekst, kunt u met minimale inspanning professioneel ogende PDF's maken. Met slechts een paar regels code kunt u de inhoud precies daar plaatsen waar u wilt, waardoor uw documenten er verzorgd en overzichtelijk uitzien.

## Veelgestelde vragen

### Kan ik deze methode gebruiken om meerdere afbeeldingen met tekst te plaatsen?
Ja, u kunt eenvoudig meer rijen en cellen aan uw tabel toevoegen om extra afbeeldingen en tekst toe te voegen.

### Kan ik de uitlijning van de afbeelding wijzigen?
Absoluut! U kunt de uitlijning van de afbeelding wijzigen door de uitlijningseigenschappen van de cel aan te passen.

### Hoe kan ik de tekst verder opmaken?
U kunt HTML-tags gebruiken binnen de `HtmlFragment` object om verschillende stijlen toe te passen, zoals vet, cursief of verschillende lettertypen.

### Kan ik de afstand tussen de tekst en de afbeelding bepalen?
Ja, met behulp van de `MarginInfo` Met object kunt u de opvulling en marges tussen elementen bepalen.

### Is het mogelijk om links aan de tekst toe te voegen?
Zeker! U kunt hyperlinks in de HTML-tekst insluiten met behulp van de `<a>` label.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}