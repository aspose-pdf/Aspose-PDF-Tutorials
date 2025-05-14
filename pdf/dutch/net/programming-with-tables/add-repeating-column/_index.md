---
"description": "Leer hoe u herhalende kolommen toevoegt aan PDF-documenten met Aspose.PDF voor .NET. Stapsgewijze handleiding met voorbeelden en code. Perfect voor ontwikkelaars."
"linktitle": "Herhalende kolom toevoegen in PDF-document"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Herhalende kolom toevoegen in PDF-document"
"url": "/nl/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Herhalende kolom toevoegen in PDF-document

## Invoering

Werk je met PDF-documenten en wil je herhalende kolommen toevoegen? Dan ben je hier aan het juiste adres! Met Aspose.PDF voor .NET kun je eenvoudig tabellen en inhoud binnen een PDF beheren. Of je nu dynamische rapporten, facturen of andere gestructureerde documenten maakt, herhalende kolommen kunnen een revolutie teweegbrengen in het ordenen van gegevens. Laten we eens kijken naar een stapsgewijze handleiding voor het toevoegen van herhalende kolommen aan een PDF-document.

## Vereisten

Voordat we met de code aan de slag gaan, controleren we of alles klaar staat:

- Aspose.PDF voor .NET: De Aspose.PDF voor .NET-bibliotheek moet in uw project zijn geïnstalleerd.
- [Download Aspose.PDF voor .NET](https://releases.aspose.com/pdf/net/)
- [Gratis proefperiode](https://releases.aspose.com/)
- Ontwikkelomgeving: Zorg ervoor dat u een .NET-compatibele IDE zoals Visual Studio hebt geïnstalleerd.
- Basiskennis van C#: Hoewel we alles uitleggen, is een basiskennis van C# voldoende om de cursus soepel te kunnen volgen.
  
Als u Aspose.PDF voor .NET nog niet hebt, kunt u een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) om de functies ervan te gaan verkennen.

## Pakketten importeren

Om te beginnen moet u de benodigde naamruimten importeren uit Aspose.PDF voor .NET. Zo doet u dat:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Deze pakketten bieden de essentiële klassen en methoden die nodig zijn om met PDF-documenten te werken en tabellen te bewerken.

Laten we het proces nu opsplitsen in meerdere stappen om herhalende kolommen aan een PDF-document toe te voegen. Volg mee!

## Stap 1: Stel het pad naar uw documentenmap in

Voordat we bestanden aanmaken of bewerken, moeten we het pad definiëren waar de gegenereerde PDF wordt opgeslagen. Stel in je C#-project het pad in naar de map waar je bestanden zich bevinden:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

Dit pad verwijst naar de map waar de PDF-uitvoer wordt opgeslagen. Vervangen `"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad op uw machine.

## Stap 2: Een nieuw PDF-document maken

Om te beginnen, instantiëer een nieuwe `Document` object. Dit dient als container voor alle pagina's en inhoud in de PDF.

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

Hier hebben we een nieuw PDF-document gemaakt en er een lege pagina aan toegevoegd. De `doc.Pages.Add()` methode voegt een nieuwe pagina in het document in.

## Stap 3: Instantieer de buitenste tabel

Vervolgens maken we een buitenste tabel. Deze tabel beslaat de volledige breedte van de pagina en dient als container voor andere tabellen, waaronder de tabel met de herhalende kolommen.

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

We hebben de `ColumnWidths` eigenschap op "100%" in, wat betekent dat de tabel over de gehele paginabreedte wordt uitgerekt.

## Stap 4: De binnenste tabel maken

Laten we nu de interne tabel aanmaken, die herhalende kolommen zal bevatten. De belangrijkste eigenschappen hier zijn: `Broken`waardoor de tabel op dezelfde pagina kan worden voortgezet, en `ColumnAdjustment`, die automatisch de kolombreedtes aanpast aan de inhoud.

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

Deze binnenste tabel wordt genest in de buitenste tabel.

## Stap 5: Tabellen toevoegen aan de pagina

Nu we zowel de buitenste als de binnenste tabel klaar hebben, kunnen we ze aan de pagina toevoegen. Deze stap zorgt ervoor dat de tabellen in de documentstructuur worden opgenomen.

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

Hier hebben we de `outerTable` naar de pagina, en vervolgens hebben we binnen de buitenste tabel de `mytable`Daarnaast stellen we in `RepeatingColumnsCount` tot 5, om aan te geven hoeveel kolommen herhaald moeten worden als er gegevens worden toegevoegd.

## Stap 6: Koptekstrij toevoegen

Nu is het tijd om de kopteksten aan de tabel toe te voegen. De koptekstrij geeft context aan de gegevens en helpt bij het structureren van de kolommen. 

```csharp
Aspose.Pdf.Row row = mytable.Rows.Add();
row.Cells.Add("header 1");
row.Cells.Add("header 2");
row.Cells.Add("header 3");
row.Cells.Add("header 4");
row.Cells.Add("header 5");
row.Cells.Add("header 6");
row.Cells.Add("header 7");
row.Cells.Add("header 11");
row.Cells.Add("header 12");
row.Cells.Add("header 13");
row.Cells.Add("header 14");
row.Cells.Add("header 15");
row.Cells.Add("header 16");
row.Cells.Add("header 17");
```

Met dit codefragment wordt de eerste rij (die we als kopteksten gebruiken) toegevoegd en gevuld met cellen die tekst bevatten, zoals 'koptekst 1', 'koptekst 2', enzovoort.

## Stap 7: Gegevensrijen toevoegen

Ten slotte kunnen we wat gegevens aan de tabel toevoegen. Deze lus creëert dynamisch rijen en vult de cellen met inhoud:

```csharp
for (int RowCounter = 0; RowCounter <= 5; RowCounter++)
{
    Aspose.Pdf.Row row1 = mytable.Rows.Add();
    row1.Cells.Add("col " + RowCounter.ToString() + ", 1");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 2");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 3");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 4");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 5");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 6");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 7");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 11");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 12");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 13");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 14");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 15");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 16");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 17");
}
```

De lus wordt zes keer herhaald, waarbij rijen worden toegevoegd en elke cel wordt gevuld met bijbehorende kolomgegevens (bijvoorbeeld 'kolom 1, 1', 'kolom 2, 2', enz.).

## Stap 8: Sla het document op

Zodra alle rijen en kolommen zijn toegevoegd, slaat u het document als laatste op in het opgegeven bestandspad.

```csharp
doc.Save(outFile);
```

Uw document is nu opgeslagen met herhalende kolommen!

## Conclusie

Zo, dat is het! Met deze eenvoudige stappen kunt u een PDF-document met herhalende kolommen maken met Aspose.PDF voor .NET. Door de flexibiliteit van geneste tabellen te benutten, kunt u complexe lay-outs creëren die uw PDF's er professioneel en overzichtelijk uit laten zien. Probeer dit uit voor uw volgende project en ontdek alle mogelijkheden van Aspose.PDF voor uw PDF-generatiebehoeften.

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een krachtige bibliotheek waarmee ontwikkelaars programmatisch PDF-documenten kunnen maken, bewerken en beheren.

### Kan ik het aantal herhalende kolommen dynamisch aanpassen?
Ja, u kunt het aantal herhalende kolommen wijzigen door de `RepeatingColumnsCount` eigendom.

### Hoe kan ik een licentie aanvragen voor Aspose.PDF voor .NET?
kunt een licentie aanvragen vanuit een bestand of stream door de volgende stappen te volgen: [documentatie](https://reference.aspose.com/pdf/net/).

### Is het mogelijk om afbeeldingen aan de tabelcellen toe te voegen?
Ja, Aspose.PDF voor .NET ondersteunt het toevoegen van verschillende soorten inhoud, waaronder afbeeldingen, aan tabelcellen.

### Kan ik de tabelindeling verder aanpassen?
Absoluut! Aspose.PDF biedt uitgebreide functies voor het aanpassen van tabelstijlen, waaronder randen, opvulling, uitlijning en meer.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}