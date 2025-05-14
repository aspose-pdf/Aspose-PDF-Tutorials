---
"description": "Leer hoe u een tekstrand toevoegt aan een PDF-bestand met Aspose.PDF voor .NET met deze stapsgewijze handleiding. Verbeter uw PDF-documenten."
"linktitle": "Tekstrand toevoegen in PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Tekstrand toevoegen in PDF-bestand"
"url": "/nl/net/programming-with-text/add-text-border/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tekstrand toevoegen in PDF-bestand

## Invoering

Het maken en bewerken van PDF-documenten is een essentiële vaardigheid geworden in de digitale wereld van vandaag. Of u nu rapporten, facturen of andere documentatie genereert, controle hebben over hoe uw tekst eruitziet, kan een aanzienlijk verschil maken. Een dergelijke verbetering die u wellicht wilt implementeren, is het toevoegen van een rand rond uw tekst in een PDF-bestand. In deze handleiding leiden we u door de stappen om een tekstrand toe te voegen aan een PDF-bestand met behulp van de Aspose.PDF-bibliotheek voor .NET. Laten we er meteen mee aan de slag gaan!

## Vereisten

Voordat we beginnen, zijn er een paar dingen die je moet regelen. Maak je geen zorgen, het is vrij eenvoudig!

1. Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. Dit wordt uw ontwikkelomgeving waar u uw code schrijft en uitvoert.
2. Aspose.PDF voor .NET: Je moet de Aspose.PDF-bibliotheek downloaden en installeren. Je kunt deze vinden op de [Aspose PDF voor .NET downloadpagina](https://releases.aspose.com/pdf/net/)Als je het eerst wilt uitproberen, kun je ook een [gratis proefperiode hier](https://releases.aspose.com/).
3. Basiskennis van C#: Een fundamenteel begrip van de programmeertaal C# helpt u de voorbeelden gemakkelijk te volgen.
4. .NET Framework: Zorg ervoor dat u .NET Framework hebt geïnstalleerd en ingesteld in uw project.

Zodra je aan deze vereisten voldoet, kun je beginnen met coderen!

## Pakketten importeren

Nu we alles hebben ingesteld, importeren we de benodigde pakketten om Aspose.PDF in ons project te gebruiken. Dit kunt u doen door de volgende using-richtlijnen bovenaan uw C#-bestand toe te voegen:

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

```

Dankzij deze naamruimten kunt u effectief met PDF-documenten en tekstfragmenten werken. 

Laten we het proces van het toevoegen van een tekstrand nu in gedetailleerde stappen opsplitsen. We nemen elke stap door, zodat je precies begrijpt wat er onder de motorkap gebeurt.

## Stap 1: Het document instellen

Allereerst moeten we een nieuw PDF-document maken. Dit is waar al onze magie gebeurt.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Nieuw documentobject maken 
Document pdfDocument = new Document();
```

In deze stap specificeren we de map waar we ons PDF-bestand willen opslaan. Vervolgens maken we een nieuw exemplaar van de `Document` klasse, die ons PDF-document vertegenwoordigt.

## Stap 2: Een nieuwe pagina toevoegen

Vervolgens moeten we een pagina aan ons document toevoegen. Zie dit als een leeg canvas waar we onze tekst op plaatsen.

```csharp
// Specifieke pagina ophalen
Page pdfPage = (Page)pdfDocument.Pages.Add();
```

Hier noemen we de `Add()` methode op de `Pages` verzameling van onze `pdfDocument` object. Dit voegt een nieuwe pagina toe aan het document en we slaan een verwijzing ernaar op in de `pdfPage` variabel.

## Stap 3: Een tekstfragment maken

Laten we nu de tekst maken die we in onze PDF willen weergeven. Hier definiëren we de inhoud van ons tekstfragment.

```csharp
// Tekstfragment maken
TextFragment textFragment = new TextFragment("main text");
textFragment.Position = new Position(100, 600);
```

In deze code maken we een nieuwe `TextFragment` object met de tekst "hoofdtekst". We stellen ook de positie ervan op de pagina in met behulp van de `Position` klasse. De coördinaten (100, 600) geven aan waar de tekst op de pagina wordt geplaatst.

## Stap 4: Teksteigenschappen instellen

Vervolgens passen we ons tekstfragment aan om het visueel aantrekkelijk te maken. Dit omvat het instellen van de lettergrootte, het lettertype, de achtergrondkleur en de voorgrondkleur.

```csharp
// Teksteigenschappen instellen
textFragment.TextState.FontSize = 12;
textFragment.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment.TextState.BackgroundColor = Aspose.Pdf.Color.LightGray;
textFragment.TextState.ForegroundColor = Aspose.Pdf.Color.Red;
```

Hier stellen we de lettergrootte in op 12, gebruiken we "Times New Roman" als lettertype en passen we een lichtgrijze achtergrondkleur toe op rode tekst. Deze eigenschappen verbeteren de zichtbaarheid van de tekst.

## Stap 5: Stel de omlijningskleur voor de rand in

Nu komen we bij het spannende gedeelte: een rand om onze tekst toevoegen!

```csharp
// Stel de eigenschap StrokingColor in voor het tekenen van een rand (lijning) rond een tekstrechthoek
textFragment.TextState.StrokingColor = Aspose.Pdf.Color.DarkRed;
```

In deze stap specificeren we de kleur van de rand die we rond onze tekst willen tekenen. Hier hebben we gekozen voor een donkerrode kleur.

## Stap 6: De rand van de tekstrechthoek inschakelen

Om daadwerkelijk de rand rond onze tekst te tekenen, moeten we de `DrawTextRectangleBorder` eigendom.

```csharp
// Stel de eigenschapswaarde DrawTextRectangleBorder in op true
textFragment.TextState.DrawTextRectangleBorder = true;
```

Door deze eigenschap in te stellen op `true`, vertellen we Aspose.PDF om de rand rond het tekstvak te tekenen op basis van de opgegeven streekkleur.

## Stap 7: Voeg het tekstfragment toe aan de pagina

Nu het tekstfragment klaar is en alle eigenschappen zijn ingesteld, is het tijd om het aan de pagina toe te voegen.

```csharp
TextBuilder tb = new TextBuilder(pdfPage);
tb.AppendText(textFragment);
```

Hier creëren we een `TextBuilder` object dat geassocieerd is met onze `pdfPage`. Vervolgens gebruiken we de `AppendText` methode om onze toe te voegen `textFragment` naar de pagina. 

## Stap 8: Sla het document op

Ten slotte moeten we ons PDF-document opslaan in de opgegeven map. Dit is het moment van de waarheid!

```csharp
// Sla het document op
pdfDocument.Save(dataDir + "PDFWithTextBorder_out.pdf");
```

In deze stap noemen we de `Save` methode op onze `pdfDocument` object, waarbij u het pad opgeeft waar we het bestand willen opslaan. Zodra u de code uitvoert, zou u uw nieuwe PDF met de tekstrand in de opgegeven map moeten vinden!

## Conclusie

En voilà! Je hebt met succes een tekstrand toegevoegd aan een PDF-bestand met Aspose.PDF voor .NET. Deze eenvoudige maar krachtige functie kan de leesbaarheid en esthetiek van je PDF-documenten aanzienlijk verbeteren. Of je nu rapporten, brochures of andere soorten documentatie maakt, het is handig om te weten hoe je tekstopmaak kunt aanpassen.

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een krachtige bibliotheek waarmee ontwikkelaars programmatisch PDF-documenten kunnen maken, bewerken en verwerken met behulp van het .NET Framework.

### Kan ik Aspose.PDF gratis uitproberen?
Ja! Aspose biedt een [gratis proefperiode](https://releases.aspose.com/) van hun PDF-bibliotheek, zodat u de functies ervan kunt testen voordat u tot aankoop overgaat.

### Hoe kan ik Aspose.PDF voor .NET kopen?
U kunt Aspose.PDF voor .NET rechtstreeks bij hen kopen [aankooppagina](https://purchase.aspose.com/buy).

### Is er ondersteuning beschikbaar voor Aspose.PDF?
Absoluut! Je kunt ondersteuning krijgen door de [Aspose-ondersteuningsforum](https://forum.aspose.com/c/pdf/10).

### Wat als ik een tijdelijk rijbewijs nodig heb?
Aspose biedt een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) Optie voor ontwikkelaars die de bibliotheek gedurende een beperkte tijd moeten evalueren.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}