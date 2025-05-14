---
"description": "Maak eenvoudig professionele PDF's door tabellen te renderen met Aspose.PDF voor .NET. Volg onze stapsgewijze handleiding om het genereren van documenten onder de knie te krijgen."
"linktitle": "Tabel weergeven in PDF-document"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Tabel weergeven in PDF-document"
"url": "/nl/net/programming-with-tables/render-table/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tabel weergeven in PDF-document

## Invoering

Het maken van professioneel ogende PDF's via een programma lijkt misschien een lastige klus, maar met Aspose.PDF voor .NET wordt het een fluitje van een cent. Of u nu rapporten, facturen of andere documenttypen genereert die tabelgegevens vereisen, Aspose.PDF biedt de tools die u nodig hebt. In deze tutorial laten we stap voor stap zien hoe u tabellen in een PDF-document kunt weergeven. Aan het einde hebt u een gedegen begrip van hoe u tabellen kunt bewerken, pagina-eigenschappen kunt beheren en PDF-bestanden eenvoudig kunt opslaan.

## Vereisten

Voordat we in de code duiken, heb je het volgende nodig:

- Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. U kunt het downloaden. [hier](https://visualstudio.microsoft.com/downloads/).
- Aspose.PDF voor .NET: U kunt de Aspose.PDF-bibliotheek eenvoudig downloaden van de [Aspose-releasepagina](https://releases.aspose.com/pdf/net/).
- Basiskennis van C#: Als u de basisprincipes van C# begrijpt, kunt u de cursus beter volgen.
- .NET Framework: Zorg er idealiter voor dat u in een compatibele .NET-omgeving werkt.

Zodra u aan deze vereisten hebt voldaan, kunt u beginnen met het maken van PDF-documenten!

## Pakketten importeren

Aan het begin van je C#-bestand moet je de benodigde Aspose.PDF-naamruimten importeren. Zo kun je de bibliotheekfunctionaliteiten in ons project gebruiken.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Zorg ervoor dat je de nodige verwijzingen naar de Aspose.PDF-bibliotheek in je project hebt toegevoegd. Als je NuGet gebruikt, kun je deze eenvoudig toevoegen door te zoeken naar `Aspose.PDF`.

Nu we alles hebben ingesteld, gaan we het proces opsplitsen in hanteerbare stappen voor het renderen van een tabel in een PDF-document. Maak je geen zorgen; ik begeleid je door elke stap met duidelijke instructies!

## Stap 1: Document- en pagina-info instellen

Allereerst moeten we een nieuw document aanmaken en de pagina-instellingen configureren. Zo gaat dat:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document();
PageInfo pageInfo = doc.PageInfo;
Aspose.Pdf.MarginInfo marginInfo = pageInfo.Margin;

marginInfo.Left = 37;
marginInfo.Right = 37;
marginInfo.Top = 37;
marginInfo.Bottom = 37;

pageInfo.IsLandscape = true;
```

Uitleg: 
- We beginnen met het definiëren waar ons document wordt opgeslagen (`dataDir`). 
- Vervolgens maken we een nieuw exemplaar van de `Document` klas. 
- We configureren de paginamarges om wat ruimte rond onze tabel te creëren.
- Tot slot stellen we het document in op de liggende weergave, wat handig is bij het weergeven van bredere tabellen.

## Stap 2: Maak de eerste tabel

Laten we nu onze eerste tabel maken en deze vullen met wat voorbeeldgegevens:

```csharp
Aspose.Pdf.Table table = new Aspose.Pdf.Table();
table.ColumnWidths = "50 100"; // Kolombreedtes definiëren
```

Uitleg: Hier instantiëren we de `Table` klasse en stel de kolombreedtes in. De eerste kolom is 50 eenheden breed en de tweede kolom is 100 eenheden breed.

## Stap 3: Vul de tabel met rijen

Laten we nu rijen in een lus aan onze tabel toevoegen:

```csharp
Page curPage = doc.Pages.Add(); // Een nieuwe pagina toevoegen
for (int i = 1; i <= 120; i++)
{
    Aspose.Pdf.Row row = table.Rows.Add();
    row.FixedRowHeight = 15; // Stel een vaste hoogte in voor rijen
    
    Aspose.Pdf.Cell cell1 = row.Cells.Add();
    cell1.Paragraphs.Add(new TextFragment("Content 1"));
    
    Aspose.Pdf.Cell cell2 = row.Cells.Add();
    cell2.Paragraphs.Add(new TextFragment("HHHHH"));
}
```

Uitleg: 
- Hier maken we een nieuwe pagina om onze tabel toe te voegen.
- Wij gebruiken een `for` Loop om 120 rijen aan onze tabel toe te voegen. Elke rij heeft een vaste hoogte van 15 eenheden.
- Binnen elke rij voegen we twee cellen toe en vullen deze met tekst.

## Stap 4: Voeg de eerste tabel toe aan de pagina

Zodra we de tabel hebben gevuld, voegen we deze toe aan de huidige pagina:

```csharp
Aspose.Pdf.Paragraphs paragraphs = curPage.Paragraphs;
paragraphs.Add(table);
```

Uitleg: Met deze stap voegt u de tabel die u hebt gemaakt eenvoudigweg toe aan de alinea's van de huidige pagina. Hierdoor wordt de tabel zichtbaar in het PDF-document.

## Stap 5: Een tweede tabel maken

Laten we nu een tweede tabel met andere inhoud maken en deze aan een nieuwe pagina toevoegen:

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
table1.ColumnWidths = "100 100";
for (int i = 1; i <= 10; i++)
{
    Aspose.Pdf.Row row = table1.Rows.Add();
    Aspose.Pdf.Cell cell1 = row.Cells.Add();
    cell1.Paragraphs.Add(new TextFragment("LAAAAAAA"));
    
    Aspose.Pdf.Cell cell2 = row.Cells.Add();
    cell2.Paragraphs.Add(new TextFragment("LAAGGGGGG"));
}
table1.IsInNewPage = true; // Tweede tabel instellen om op een nieuwe pagina te verschijnen
paragraphs.Add(table1);
```

Uitleg: 
- Met dit codefragment wordt een nieuwe tabel gemaakt met twee kolommen, beide 100 eenheden breed.
- A `for` lus voegt 10 rijen met voorbeeldinhoud toe.
- Door het instellen `table1.IsInNewPage` Als dat waar is, zorgen we ervoor dat deze tabel op een nieuwe pagina verschijnt, zodat alles georganiseerd en overzichtelijk blijft.

## Stap 6: Sla het document op

Nu onze tabellen klaar zijn, slaan we ons document op:

```csharp
dataDir = dataDir + "IsNewPageProperty_Test_out.pdf";
doc.Save(dataDir);
```

Uitleg: We geven de bestandsnaam op en slaan het document op in de opgegeven map. Wanneer u deze code uitvoert, verschijnt er een PDF-bestand met de titel `IsNewPageProperty_Test_out.pdf` wordt op de door u opgegeven locatie aangemaakt.

## Stap 7: Bevestigingsbericht

Om de gebruiker te laten weten dat alles soepel is verlopen, kunnen we tot slot een vriendelijk bericht op de console toevoegen:

```csharp
Console.WriteLine("\nTable rendered successfully on a page.\nFile saved at " + dataDir);
```

Uitleg: Dit is een eenvoudige manier om te bevestigen dat de bewerking succesvol is verlopen en waar de gebruiker het nieuwe PDF-bestand kan vinden.

## Conclusie

En voilà! Je hebt succesvol tabellen in een PDF-document weergegeven met Aspose.PDF voor .NET. Met slechts een paar regels code kun je grote hoeveelheden gegevens verwerken en presenteren in een overzichtelijke indeling, waardoor je documenten zowel informatief als visueel aantrekkelijk worden. Of je nu werkt aan inventarislijsten, financiële rapporten of educatieve documenten, tabellen zijn een uitstekende manier om complexe informatie in één oogopslag over te brengen.

## Veelgestelde vragen

### Kan ik het uiterlijk van de tabellen in Aspose.PDF aanpassen?  
Absoluut! Je kunt kleuren, randen, lettertypen en andere eigenschappen aanpassen om het uiterlijk van je tabellen te verbeteren.

### Is Aspose.PDF gratis te gebruiken?  
Aspose.PDF biedt een gratis proefversie aan, maar voor commercieel gebruik is een aankoop vereist. U kunt de prijzen bekijken. [hier](https://purchase.aspose.com/buy).

### Hoe kan ik ondersteuning krijgen voor problemen met Aspose.PDF?  
kunt hulp krijgen via het Aspose-ondersteuningsforum [hier](https://forum.aspose.com/c/pdf/10).

### Zijn er beperkingen voor de gratis proefversie?  
Ja, de proefversie kan bepaalde beperkingen hebben, zoals watermerken op gegenereerde documenten. Voor volledige functionaliteit kunt u een tijdelijke licentie overwegen. [hier](https://purchase.aspose.com/temporary-license/).

### Waar kan ik meer informatie vinden over de functies van Aspose.PDF?  
U kunt de uitgebreide documentatie die beschikbaar is, bekijken [hier](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}