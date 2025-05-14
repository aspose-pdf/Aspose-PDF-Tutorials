---
"description": "Leer hoe u horizontaal en verticaal uitgelijnde keuzerondjes in PDF kunt maken met Aspose.PDF voor .NET met deze stapsgewijze zelfstudie."
"linktitle": "Horizontaal en verticaal keuzerondjes"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Horizontaal en verticaal keuzerondjes"
"url": "/nl/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Horizontaal en verticaal keuzerondjes

## Invoering

Het maken van interactieve PDF-formulieren kan de gebruikerservaring aanzienlijk verbeteren, vooral als het gaat om het verzamelen van informatie. Een van de meest voorkomende formulierelementen is de keuzerondje, waarmee gebruikers één optie uit een set kunnen selecteren. In deze tutorial laten we zien hoe je horizontaal en verticaal uitgelijnde keuzerondjes kunt maken met Aspose.PDF voor .NET. Of je nu een ervaren ontwikkelaar bent of net begint, deze handleiding leidt je stap voor stap door het proces, zodat je elk onderdeel goed begrijpt.

## Vereisten

Voordat u aan de slag gaat met de code, moet u aan een paar voorwaarden voldoen:

1. Aspose.PDF voor .NET: Zorg ervoor dat de Aspose.PDF-bibliotheek geïnstalleerd is. U kunt deze downloaden van de [site](https://releases.aspose.com/pdf/net/).
2. Visual Studio: een ontwikkelomgeving waarin u uw code kunt schrijven en testen.
3. Basiskennis van C#: Kennis van C#-programmering helpt u de codefragmenten beter te begrijpen.

## Pakketten importeren

Om te beginnen moet je de benodigde pakketten in je C#-project importeren. Zo doe je dat:

### Een nieuw project maken

Open Visual Studio en maak een nieuw C#-project. Voor de eenvoud kunt u een consoletoepassing kiezen.

### Voeg Aspose.PDF-referentie toe

1. Klik met de rechtermuisknop op uw project in Solution Explorer.
2. Selecteer 'NuGet-pakketten beheren'.
3. Zoek naar "Aspose.PDF" en installeer de nieuwste versie.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

Nu u alles hebt ingesteld, gaan we de code opsplitsen om horizontaal en verticaal uitgelijnde keuzerondjes te maken.

## Stap 1: De documentenmap instellen

In deze stap definiëren we het pad naar de map waar uw PDF-documenten worden opgeslagen.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Vervangen `"YOUR DOCUMENT DIRECTORY"` met het daadwerkelijke pad waar u uw PDF-bestand wilt opslaan. Dit is cruciaal, omdat het het programma vertelt waar het moet zoeken naar invoerbestanden en waar het de uitvoer moet opslaan.

## Stap 2: Het bestaande PDF-document laden

Vervolgens moeten we het PDF-document laden waarmee we gaan werken. Dit doen we met behulp van de `FormEditor` klas.

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

Hier maken we een instantie van `FormEditor` en bind het aan een bestaand PDF-bestand met de naam `input.pdf`Zorg ervoor dat dit bestand in de opgegeven directory staat.

## Stap 3: Configureer de eigenschappen van keuzerondjes

Laten we nu een aantal eigenschappen voor onze keuzerondjes instellen. Denk hierbij aan de ruimte tussen de knoppen, hun positie en hun grootte.

```csharp
formEditor.RadioGap = 4; // Afstand tussen keuzerondjes
formEditor.RadioHoriz = true; // Instellen op waar voor horizontale uitlijning
formEditor.RadioButtonItemSize = 20; // Grootte van de keuzerondje
formEditor.Facade.BorderWidth = 1; // Randbreedte
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // Randkleur
```

Deze eigenschappen helpen bepalen hoe de keuzerondjes in de PDF worden weergegeven. `RadioGap` eigenschap regelt de ruimte tussen de knoppen, terwijl `RadioHoriz` bepaalt hun indeling.

## Stap 4: Horizontale keuzerondjes toevoegen

Laten we nu de horizontale keuzerondjes aan de PDF toevoegen.

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

In deze code definiëren we de items voor de keuzerondjes en voegen we ze toe aan de PDF. `AddField` methode heeft meerdere parameters nodig, waaronder het veldtype, de veldnaam en de coördinaten voor plaatsing.

## Stap 5: Verticale keuzerondjes toevoegen

Vervolgens voegen we de verticale keuzerondjes toe. Hiervoor moeten we de oriëntatie weer naar verticaal veranderen.

```csharp
formEditor.RadioHoriz = false; // Instellen op onwaar voor verticale uitlijning
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

Net als voorheen definiëren we de items en voegen we ze toe aan de PDF, maar deze keer worden ze verticaal uitgelijnd.

## Stap 6: Sla het PDF-document op

Ten slotte moeten we het gewijzigde PDF-document opslaan.

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

Deze code slaat de PDF op met de nieuw toegevoegde keuzerondjes. Controleer de opgegeven map voor het uitvoerbestand.

## Conclusie

Het maken van keuzerondjes in een PDF met Aspose.PDF voor .NET is een eenvoudig proces. Door de stappen in deze tutorial te volgen, kunt u eenvoudig zowel horizontaal als verticaal uitgelijnde keuzerondjes toevoegen aan uw PDF-formulieren. Dit verbetert niet alleen de interactiviteit van uw documenten, maar ook de algehele gebruikerservaring. Dus, ga aan de slag en probeer het eens!

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een krachtige bibliotheek waarmee ontwikkelaars programmatisch PDF-documenten kunnen maken, bewerken en converteren.

### Kan ik Aspose.PDF gratis gebruiken?
Ja, Aspose biedt een gratis proefversie aan waarmee u de bibliotheek kunt evalueren. U kunt deze downloaden. [hier](https://releases.aspose.com/).

### Hoe krijg ik ondersteuning voor Aspose.PDF?
U kunt ondersteuning krijgen door de [Aspose-forum](https://forum.aspose.com/c/pdf/10).

### Is het mogelijk om andere formulierelementen te maken met Aspose.PDF?
Absoluut! Aspose.PDF ondersteunt verschillende formulierelementen, waaronder tekstvelden, selectievakjes en dropdownmenu's.

### Waar kan ik Aspose.PDF voor .NET kopen?
U kunt Aspose.PDF voor .NET kopen bij de [aankooppagina](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}