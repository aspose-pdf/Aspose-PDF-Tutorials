---
"date": "2025-04-11"
"description": "Leer hoe u efficiënt datum- en tijdstempels of annotaties aan uw PDF-documenten toevoegt met Aspose.PDF voor .NET. Verbeter uw documentbeheer met deze eenvoudig te volgen stappen."
"title": "Datum- en tijdstempels toevoegen aan PDF's met Aspose.PDF voor .NET"
"url": "/nl/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Datum- en tijdstempels toevoegen aan PDF's met Aspose.PDF voor .NET

## Invoering

In het huidige digitale tijdperk is effectief documentbeheer cruciaal voor bedrijven en particulieren. Het toevoegen van datum- en tijdstempels of annotaties aan uw PDF's kan de gegevensintegriteit en -organisatie verbeteren. Deze tutorial laat zien hoe u deze functies kunt integreren met Aspose.PDF voor .NET.

**Belangrijkste punten:**
- Voeg de huidige datum en tijd toe als tekststempels op een bepaalde PDF-pagina.
- Maak vrije tekstaantekeningen op de gewenste locaties in het document.
- Volg de aanbevolen procedures voor optimale prestaties met Aspose.PDF voor .NET.

## Vereisten
Voordat u begint, zorg ervoor dat u het volgende heeft:

### Vereiste bibliotheken en versies
- **Aspose.PDF voor .NET**: Een robuuste bibliotheek voor PDF-bewerking zonder Adobe Acrobat. Gebruik versie 21.x of hoger.

### Vereisten voor omgevingsinstellingen
- Ontwikkelomgeving met .NET Framework 4.5+ of .NET Core 2.0+
- Visual Studio of een andere IDE die C#-programmering ondersteunt

### Kennisvereisten
- Basiskennis van C#- en .NET-projectstructuren
- Kennis van het verwerken van bestanden in een directorystructuur

## Aspose.PDF instellen voor .NET
Installeer Aspose.PDF met behulp van een van de volgende methoden:

**Met behulp van .NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**Pakketbeheer gebruiken:**
```powershell
Install-Package Aspose.PDF
```

**Via de NuGet Package Manager-gebruikersinterface:**
- Open de NuGet Package Manager in uw IDE.
- Zoek naar "Aspose.PDF" en installeer de nieuwste versie.

### Stappen voor het verkrijgen van een licentie
Om Aspose.PDF volledig te benutten:
1. **Gratis proefperiode:** Download een tijdelijke licentie om alle functies te ontdekken.
2. **Tijdelijke licentie:** Vraag indien nodig een uitgebreide evaluatielicentie aan.
3. **Aankoop:** Koop een licentie voor langdurig gebruik via de Aspose-website.

Initialiseer uw licentie in code:
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## Implementatiegids
Laten we datum- en tijdstempels toevoegen aan PDF's.

### Functie 1: Datum/tijdstempel toevoegen aan PDF
Met deze functie worden de huidige datum en tijd als tekststempel toegevoegd aan de eerste pagina van een opgegeven PDF-document.

#### Stapsgewijze implementatie

##### 1. Open bestaand PDF-document
Laad uw doeldocument:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. Huidige datum en tijd als tekenreeks ophalen
De huidige datum en tijd noteren:
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. Maak een tekststempel met de huidige datum en tijd
Maak een `TextStamp` instantie die de geformatteerde tekenreeks gebruikt:
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. Tekststempel toevoegen aan de eerste pagina
Voeg de stempel toe aan de eerste pagina van uw document:
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5. Maak en voeg een vrije tekstannotatie toe (optioneel)
Voor complexere annotaties maakt u een `FreeTextAnnotation`:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6. Sla het gewijzigde document op
Sla uw wijzigingen op:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### Functie 2: Vrije tekstannotatie toevoegen aan PDF
Voeg op elke gewenste locatie in een PDF-document gratis tekstuele aantekeningen toe.

#### Stapsgewijze implementatie

##### 1. Open een bestaand PDF-document
Laad uw doeldocument:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. Definieer het rechthoekgebied voor annotatie
Geef aan waar de aantekening op de pagina moet worden geplaatst:
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. Maak een vrije tekstannotatie met een opgegeven uiterlijk en locatie
Initialiseer uw annotatie met de gewenste tekst- en weergave-instellingen:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. Stel de randstijl in en voeg de annotatie toe
Zorg ervoor dat de randstijl aan uw wensen voldoet (in dit geval onzichtbaar):
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5. Sla het gewijzigde document op
Sla uw document op met de nieuw toegevoegde annotatie:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## Praktische toepassingen
Het toevoegen van datumstempels en aantekeningen aan PDF's is nuttig in verschillende sectoren:
- **Juridische documenten**: Zorgt voor naleving door wijzigingen van een tijdstempel te voorzien.
- **Academische artikelen**: Maakt samenwerkend bewerken met annotaties mogelijk.
- **Financiële gegevens**: Zorgt voor nauwkeurige controletrajecten met tijdstempelrapporten.
- **Technische documentatie**: Markeert updates of belangrijke opmerkingen in handleidingen.

## Prestatieoverwegingen
Voor optimale prestaties bij gebruik van Aspose.PDF voor .NET:
- **Batchverwerking**: Verwerk meerdere PDF's in batches om overheadkosten te verlagen.
- **Geheugenbeheer**: Gebruik `Dispose` Methoden om geheugenbronnen vrij te maken na het verwerken van elk document.
- **Geoptimaliseerde lettertypen en afbeeldingen**: Beperk lettertypen en afbeeldingsresoluties om de bestandsgrootte te verkleinen.

## Conclusie
Door Aspose.PDF voor .NET te integreren, kunt u datumstempels en annotatiefuncties toevoegen aan PDF-documenten, wat de functionaliteit verbetert. Deze tools verbeteren de gegevensintegriteit en stroomlijnen het documentbeheer.

Experimenteer met verschillende configuraties en ontdek de extra functies die Aspose.PDF biedt om aan uw specifieke behoeften te voldoen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}