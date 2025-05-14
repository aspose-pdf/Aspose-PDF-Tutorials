---
"description": "Voeg eenvoudig paginanummers toe aan de kop- en voettekst van uw PDF met behulp van een zwevend vak met Aspose.PDF voor .NET in deze stapsgewijze zelfstudie."
"linktitle": "Paginanummer in koptekst/voettekst met behulp van zwevende box"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Paginanummer in koptekst/voettekst met behulp van zwevende box"
"url": "/nl/net/programming-with-stamps-and-watermarks/page-number-in-header-footer-using-floating-box/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Paginanummer in koptekst/voettekst met behulp van zwevende box

## Invoering

Aspose.PDF voor .NET is een uitstekende tool voor programmatisch PDF-documentbeheer. Het vereenvoudigt de manier waarop we PDF-bestanden in .NET-applicaties maken, bewerken en manipuleren. Of u nu facturen, rapporten of andere documenttypen genereert, het elegant toevoegen van paginanummers kan de professionaliteit en organisatie van uw PDF's verbeteren. In deze tutorial duiken we in hoe u paginanummers toevoegt aan de kop- en voettekst van uw PDF met behulp van een zwevend kader. Klaar om te beginnen? Aan de slag!

## Vereisten

Voordat we aan deze spannende reis in de wereld van PDF-manipulatie beginnen, zijn er een paar dingen die u nodig hebt:

### .NET-omgeving instellen
Zorg ervoor dat je een .NET-ontwikkelomgeving hebt. Je kunt Visual Studio gebruiken, een populaire keuze onder ontwikkelaars voor .NET-applicaties.

### Aspose.PDF-bibliotheek
Installeer de Aspose.PDF-bibliotheek. U kunt deze eenvoudig downloaden van de website:

- [Download Aspose.PDF voor .NET](https://releases.aspose.com/pdf/net/)

### Basiskennis van C#-programmering
Een basiskennis van C# helpt u de concepten en codefragmenten te begrijpen die in deze tutorial worden behandeld.

### Toegang tot de documentatie
Het is altijd nuttig om de [Aspose.PDF-documentatie](https://reference.aspose.com/pdf/net/) Handig als referentiemateriaal en om eventuele aanvullende functionaliteiten verder te verkennen.

## Pakketten importeren

Om te beginnen moet je de benodigde pakketten in je project importeren. Dit zorgt ervoor dat de Aspose.PDF-assembly toegankelijk is voor gebruik in je code. Zo doe je dat:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Laten we het proces van het toevoegen van paginanummers met behulp van een zwevende box nu opsplitsen in hanteerbare stappen. Volg mee terwijl we het proces doorlopen.

## Stap 1: Stel uw documentomgeving in

Laten we beginnen met het specificeren van de map waar uw PDF-document wordt opgeslagen. Dit is cruciaal, omdat het bepaalt waar uw uitvoerbestand wordt opgeslagen.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Vervangen `YOUR DOCUMENT DIRECTORY` met het pad naar keuze waar u het PDF-uitvoerbestand wilt opslaan.

## Stap 2: Het document instantiëren

De volgende stap is het maken van een nieuw PDF-document. Dit omvat het gebruik van de `Document` klas uit de Aspose.PDF bibliotheek.

```csharp
// Instantieer documentinstantie
Aspose.Pdf.Document pdf = new Aspose.Pdf.Document();
```
Hier maken we een nieuw exemplaar van de `Document` klasse, die als canvas voor manipulatie dient.

## Stap 3: Een nieuwe pagina toevoegen

Laten we nu een pagina aan ons PDF-document toevoegen. Elke PDF heeft toch minstens één pagina nodig?

```csharp
// Een pagina toevoegen aan het PDF-document
Aspose.Pdf.Page page = pdf.Pages.Add();
```
Met dit codefragment wordt een nieuwe pagina aan ons document toegevoegd, zodat het document klaar is om inhoud te ontvangen, inclusief ons zwevende vak met paginanummers.

## Stap 4: Maak een zwevende doos

Vervolgens is het tijd om onze zwevende doos te maken die het paginanummer zal bevatten. `FloatingBox` klasse stelt ons in staat om inhoud vrij op de pagina te positioneren.

```csharp
// Initialiseert een nieuw exemplaar van de FloatingBox-klasse
Aspose.Pdf.FloatingBox box1 = new Aspose.Pdf.FloatingBox(140, 80);
```
Hier de parameters `(140, 80)` Geef de breedte en hoogte van de zwevende box op. U kunt deze waarden aanpassen aan uw lay-outvoorkeuren.

## Stap 5: De zwevende doos positioneren

Positionering is essentieel! Je wilt bepalen waar het paginanummer op de pagina komt te staan. Je werkt met de `Left` En `Top` Eigenschappen om de positie te specificeren.

```csharp
// Vlotterwaarde die de linkerpositie van de alinea aangeeft
box1.Left = 2;
// Vlotterwaarde die de bovenste positie van de alinea aangeeft
box1.Top = 10;
```
Deze waarden bepalen de plaatsing van het zwevende kader op de pagina. Experimenteer er gerust mee om te zien wat het beste bij uw document past.

## Stap 6: Tekst toevoegen met de paginanummermacro

Nu voegen we een string toe die dynamisch het paginanummer weergeeft. Dit is waar de magie gebeurt!

```csharp
// Voeg de macro's toe aan de alineaverzameling van de FloatingBox
box1.Paragraphs.Add(new Aspose.Pdf.Text.TextFragment("Page: ($p/ $P )"));
```
In dit geval, `($p/ $P)` is een macro die het huidige paginanummer weergeeft (`$p`) en het totale aantal pagina's (`$P`). Hierdoor wordt de tekst zo geformatteerd dat deze bijvoorbeeld lijkt op "Pagina: 1/5".

## Stap 7: Voeg het zwevende vak toe aan de pagina

Het is tijd om de zwevende box en de paginanummertekst toe te voegen aan de nieuw aangemaakte pagina.

```csharp
// Voeg een floatingBox toe aan de pagina
page.Paragraphs.Add(box1);
```
Met deze regel wordt uw zwevende vak als het ware in de pagina geïntegreerd, waardoor het onderdeel wordt van de lay-out van het document. 

## Stap 8: Sla uw document op

Vergeet ten slotte niet je werk op te slaan! De laatste stap is het opslaan van je PDF-document met een correcte bestandsnaam.

```csharp
// Sla het document op
pdf.Save(dataDir + "PageNumberinHeaderFooterUsingFloatingBox_out.pdf");
```
Zorg ervoor dat het opgegeven pad de gewenste bestandsnaam bevat. Je fantastische PDF met paginanummers is nu aangemaakt! 

## Conclusie

En voilà, mensen! Paginanummers toevoegen aan de kop- en voettekst van je PDF met Aspose.PDF voor .NET is zo simpel als wat. Met slechts een paar regels code ben je al begonnen aan een reis om documentverwerking in je applicaties onder de knie te krijgen. Aarzel niet om te experimenteren met verschillende lay-outs en opmaak – creativiteit kent immers geen grenzen! Klaar om dat professionele document te genereren? Pak je programmeerhoed en ga experimenteren.

## Veelgestelde vragen

### Kan ik het uiterlijk van de paginanummertekst aanpassen?  
Ja, u kunt teksteigenschappen, zoals lettergrootte, kleur en stijl, aanpassen door de `TextFragment` eigenschappen.

### Is Aspose.PDF gratis te gebruiken?  
Hoewel Aspose.PDF een gratis proefperiode biedt, is het een betaald product voor productiegebruik. U kunt [koop het hier](https://purchase.aspose.com/buy).

### Waar kan ik meer gedetailleerde documentatie vinden?  
Uitgebreide documentatie vindt u op de [Aspose.PDF Documentatiesite](https://reference.aspose.com/pdf/net/).

### Hoe pas ik kop- en voetteksten toe op meerdere pagina's?  
kunt door alle pagina's van uw document bladeren en de zwevende box op dezelfde manier op elke pagina toepassen.

### Wat als ik ondersteuning nodig heb voor extra functies?  
Voor eventuele aanvullende vragen of ondersteuning kunt u terecht op de [Aspose Forum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}