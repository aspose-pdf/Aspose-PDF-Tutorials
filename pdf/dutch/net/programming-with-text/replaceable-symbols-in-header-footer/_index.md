---
"description": "Leer hoe u vervangbare symbolen in de kop- en voettekst van een PDF-document gebruikt met Aspose.PDF voor .NET."
"linktitle": "Vervangbare symbolen in koptekst en voettekst"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Vervangbare symbolen in koptekst en voettekst"
"url": "/nl/net/programming-with-text/replaceable-symbols-in-header-footer/"
"weight": 320
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vervangbare symbolen in koptekst en voettekst

## Invoering

Bij het werken met PDF-bestanden moet u soms kop- en voetteksten aanpassen met dynamische inhoud, zoals paginanummers, rapportnamen of gegenereerde datums. Gelukkig vereenvoudigt Aspose.PDF voor .NET dit proces, waardoor u PDF's kunt maken met automatisch bijgewerkte symbolen in kop- en voetteksten, zoals paginanummers of details over de rapportgeneratie. Dit artikel begeleidt u stapsgewijs bij het vervangen van symbolen in kop- en voetteksten met Aspose.PDF voor .NET, op een manier die niet alleen eenvoudig maar ook ongelooflijk efficiënt is.

## Vereisten

Voordat u met de stapsgewijze handleiding aan de slag gaat, moet u ervoor zorgen dat u het volgende bij de hand hebt:

- Aspose.PDF voor .NET-bibliotheek – [Download](https://releases.aspose.com/pdf/net/) of krijg een [gratis proefperiode](https://releases.aspose.com/).
- Visual Studio of een andere C# IDE op uw systeem geïnstalleerd.
- Basiskennis van C#- en .NET-ontwikkeling.
- Een geldig [licentie](https://purchase.aspose.com/temporary-license/) voor Aspose.PDF, of u kunt de proefversie gebruiken.

## Pakketten importeren

Om te beginnen moet u de benodigde naamruimten importeren die de functionaliteit van Aspose.PDF voor .NET mogelijk maken. Hieronder ziet u de benodigde import:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Deze zijn essentieel voor het maken van PDF's, het bewerken van tekst en het beheren van kop- en voetteksten.

Laten we de voorbeeldcode opsplitsen in eenvoudig te begrijpen stappen.

## Stap 1: Het document en de pagina instellen

Eerst moeten we het document initialiseren en er een pagina aan toevoegen. Dit vormt de basis voor het toevoegen van kop- en voetteksten.

```csharp
// Documentmap instellen
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Initialiseer het documentobject
Document doc = new Document();

// Een pagina toevoegen aan het document
Page page = doc.Pages.Add();
```

Hier stellen we een PDF-document op met behulp van de `Document` klasse en een pagina toevoegen met `doc.Pages.Add()`Deze pagina bevat de koptekst, voettekst en andere inhoud.

## Stap 2: Paginamarges configureren

Vervolgens definiëren we de marges voor de pagina om ervoor te zorgen dat de inhoud niet helemaal tot aan de rand reikt.

```csharp
// Marges configureren
MarginInfo marginInfo = new MarginInfo();
marginInfo.Top = 90;
marginInfo.Bottom = 50;
marginInfo.Left = 50;
marginInfo.Right = 50;
page.PageInfo.Margin = marginInfo;
```

Hier hebben we de boven-, onder-, linker- en rechtermarges gedefinieerd met behulp van de `MarginInfo` klasse en paste het toe op de pagina met behulp van `page.PageInfo.Margin`.

## Stap 3: De header maken en configureren

Laten we nu een koptekst maken en deze aan de pagina toevoegen. De koptekst bevat de titel en naam van het rapport.

```csharp
// Koptekst maken
HeaderFooter hfFirst = new HeaderFooter();
page.Header = hfFirst;

// Koptekstmarges instellen
hfFirst.Margin.Left = 50;
hfFirst.Margin.Right = 50;

// Titel toevoegen aan koptekst
TextFragment t1 = new TextFragment("report title");
t1.TextState.Font = FontRepository.FindFont("Arial");
t1.TextState.FontSize = 16;
t1.TextState.ForegroundColor = Aspose.Pdf.Color.Black;
t1.TextState.FontStyle = FontStyles.Bold;
t1.TextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
hfFirst.Paragraphs.Add(t1);

// Rapportnaam toevoegen aan koptekst
TextFragment t2 = new TextFragment("Report_Name");
t2.TextState.Font = FontRepository.FindFont("Arial");
t2.TextState.FontSize = 12;
t2.TextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
hfFirst.Paragraphs.Add(t2);
```

We hebben er twee toegevoegd `TextFragment` objecten naar de koptekst: één voor de rapporttitel en één voor de rapportnaam. De tekst wordt opgemaakt met `TextState` eigenschappen zoals lettertype, grootte en uitlijning.

## Stap 4: De voettekst maken en configureren

Nu is het tijd om de voettekst in te stellen. Hierin worden dynamische inhoud, zoals paginanummers en de generatiedatum, geplaatst.

```csharp
// Voettekst maken
HeaderFooter hfFoot = new HeaderFooter();
page.Footer = hfFoot;

// Voettekstmarges instellen
hfFoot.Margin.Left = 50;
hfFoot.Margin.Right = 50;

// Voettekstinhoud toevoegen
TextFragment t3 = new TextFragment("Generated on test date");
TextFragment t4 = new TextFragment("Report Name");
TextFragment t5 = new TextFragment("Page $p of $P");
```

In de voettekst nemen we fragmenten op voor de generatiedatum, rapportnaam en dynamische paginanummers (`$p` En `$P` geven respectievelijk het huidige paginanummer en het totale aantal pagina's weer.

## Stap 5: Maak een tabel in de voettekst

U kunt ook complexere elementen, zoals tabellen, in de voettekst toevoegen om uw gegevens beter te organiseren.

```csharp
// Tabel voor voettekst maken
Table tab2 = new Table();
hfFoot.Paragraphs.Add(tab2);
tab2.ColumnWidths = "165 172 165";

// Rijen en cellen voor de tabel maken
Row row3 = tab2.Rows.Add();
row3.Cells.Add();
row3.Cells.Add();
row3.Cells.Add();

// Uitlijning voor elke cel instellen
row3.Cells[0].Alignment = Aspose.Pdf.HorizontalAlignment.Left;
row3.Cells[1].Alignment = Aspose.Pdf.HorizontalAlignment.Center;
row3.Cells[2].Alignment = Aspose.Pdf.HorizontalAlignment.Right;

// Inhoud toevoegen aan tabelcellen
row3.Cells[0].Paragraphs.Add(t3);
row3.Cells[1].Paragraphs.Add(t4);
row3.Cells[2].Paragraphs.Add(t5);
```

Met dit codeblok wordt een tabel met drie kolommen in de voettekst gemaakt, waarbij elke kolom verschillende stukjes informatie bevat, zoals de generatiedatum, de rapportnaam en paginanummers.

## Stap 6: Inhoud toevoegen aan de pagina

Naast kop- en voetteksten kunt u ook inhoud toevoegen aan de hoofdtekst van de PDF-pagina. Hier voegen we een tabel met wat tijdelijke tekst toe.

```csharp
Table table = new Table();
table.ColumnWidths = "33% 33% 34%";
page.Paragraphs.Add(table);

// Tabelinhoud toevoegen
for (int i = 0; i <= 10; i++)
{
    Row row = table.Rows.Add();
    for (int c = 0; c <= 2; c++)
    {
        Cell cell = row.Cells.Add("Content " + c);
        cell.Margin = new MarginInfo { Left = 30, Top = 10, Bottom = 10 };
    }
}
```

Deze code voegt een eenvoudige tabel met drie kolommen toe aan de pagina. U kunt deze aanpassen aan uw specifieke behoeften.

## Stap 7: Sla de PDF op

Zodra alles is ingesteld, slaat u als laatste stap het PDF-document op de gewenste locatie op.

```csharp
dataDir = dataDir + "ReplaceableSymbolsInHeaderFooter_out.pdf";
doc.Save(dataDir);
Console.WriteLine("Symbols replaced successfully in header and footer. File saved at " + dataDir);
```

U geeft het bestandspad op en slaat het document op met `doc.Save()`Dat is alles! Je hebt met succes een PDF gemaakt met aangepaste kop- en voetteksten.

## Conclusie

Het vervangen van symbolen in kop- en voetteksten met Aspose.PDF voor .NET is niet alleen eenvoudig, maar ook krachtig. Door de bovenstaande stapsgewijze handleiding te volgen, kunt u uw PDF's eenvoudig aanpassen met dynamische inhoud, zoals paginanummers, rapportnamen en datums. Deze methode is zeer flexibel, waardoor u tabellen kunt invoegen, de opmaak kunt aanpassen en de lay-out kunt aanpassen aan uw specifieke wensen.

## Veelgestelde vragen

### Kan ik lettertypen voor kopteksten en voetteksten aanpassen?  
Ja, u kunt de lettertypen, grootten, kleuren en stijlen voor tekst in kop- en voetteksten volledig aanpassen.

### Hoe voeg ik afbeeldingen toe aan kop- en voetteksten?  
Je kunt gebruiken `ImageStamp` om afbeeldingen in uw kop- en voetteksten in te voegen.

### Is het mogelijk om hyperlinks in kop- of voetteksten toe te voegen?  
Ja, je kunt gebruiken `TextFragment` met een hyperlink door de `Hyperlink` eigendom.

### Kan ik verschillende kopteksten gebruiken voor even en oneven pagina's?  
Ja, met Aspose.PDF kunt u verschillende kop- en voetteksten opgeven voor even en oneven pagina's.

### Hoe pas ik de positie van de kop- en voetteksten aan?  
U kunt de marges en uitlijningseigenschappen aanpassen om de positie van uw kopteksten en voetteksten te bepalen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}