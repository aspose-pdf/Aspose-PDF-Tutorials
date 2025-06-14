---
"description": "Leer hoe u digitale handtekeningen en certificaatinformatie uit PDF-documenten kunt extraheren met Aspose.PDF voor .NET. Een complete stapsgewijze handleiding voor C#-ontwikkelaars."
"linktitle": "Handtekeninginfo extraheren"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Handtekeninginfo extraheren"
"url": "/nl/net/programming-with-security-and-signatures/extract-signature-info/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Handtekeninginfo extraheren

## Invoering

In de huidige digitale wereld is het cruciaal om de veiligheid en integriteit van documenten te waarborgen. Een van de meest gebruikte methoden om PDF's te beveiligen, is het toevoegen van een digitale handtekening. Het ophalen en verifiëren van de handtekeninggegevens kan echter soms een uitdaging zijn, vooral wanneer u met verschillende certificaten werkt. In deze handleiding leiden we u door het proces van het extraheren van handtekeninggegevens uit PDF-documenten met Aspose.PDF voor .NET, waardoor de taak een fluitje van een cent wordt. U leert hoe u toegang krijgt tot handtekeningvelden, certificaatgegevens extraheert en deze in een bestand opslaat.

## Vereisten

Voordat we beginnen, zorgen we ervoor dat alles klaar is om te beginnen.

- Aspose.PDF voor .NET-bibliotheek: Als u deze nog niet hebt, kunt u deze downloaden van de [Aspose.PDF voor .NET downloadpagina](https://releases.aspose.com/pdf/net/). 
- .NET-ontwikkelomgeving: u hebt een IDE zoals Visual Studio nodig.
- Basiskennis van C#: Kennis van C# is nuttig om de codefragmenten in deze tutorial te begrijpen.
- PDF-document met een digitale handtekening: zorg ervoor dat u voor testdoeleinden een PDF-bestand hebt dat minimaal één digitale handtekening bevat.

## Vereiste naamruimten importeren

Voordat u aan de slag gaat met de code, is het belangrijk om de benodigde naamruimten te importeren. Deze naamruimten geven u toegang tot de Aspose.PDF-functionaliteit en geven u toegang tot PDF-documenten.

```csharp
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
using System;
```

Nu u de basisfuncties hebt ingesteld, kunnen we verder met het daadwerkelijke proces van het extraheren van handtekeninggegevens uit een PDF.

## Stap 1: De documentenmap instellen

Voordat u aan een PDF-document gaat werken, moet u de locatie opgeven van het bestand dat u wilt gebruiken. U kunt `"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad van de map waarin uw PDF's zijn opgeslagen.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string input = dataDir + "ExtractSignatureInfo.pdf";
```

Hier specificeren we de map waarin het PDF-bestand zich bevindt en de bestandsnaam zelf. Zorg ervoor dat het bestand in die map staat!

## Stap 2: Het PDF-document laden

Nu u uw directory hebt ingesteld, is de volgende stap het laden van het PDF-document met behulp van de `Document` klasse van Aspose.PDF.

```csharp
using (Document pdfDocument = new Document(input))
{
    // Verwerk de PDF hier.
}
```

Deze regel code initialiseert een `Document` object dat het PDF-bestand vertegenwoordigt. De `using` Deze instructie zorgt ervoor dat de bronnen worden opgeruimd nadat het document is verwerkt.

## Stap 3: Toegang tot formuliervelden

In deze stap doorlopen we alle formuliervelden in het PDF-document. Omdat handtekeningen doorgaans als formuliervelden worden opgeslagen, helpt deze stap ons bij het identificeren van de handtekeningvelden.

```csharp
foreach (Field field in pdfDocument.Form)
{
    // Identificeer hier de handtekeningvelden.
}
```

Door te itereren door de `Form` eigendom van de `Document` object, kunnen we elk formulierveld onderzoeken om te controleren of het een handtekeningveld is.

## Stap 4: Handtekeningvelden identificeren

Zodra u toegang hebt tot de formuliervelden, is de volgende stap om te bepalen welke velden handtekeningvelden zijn. We kunnen dit doen door elk veld naar een `SignatureField` voorwerp.

```csharp
SignatureField sf = field as SignatureField;
if (sf != null)
{
    // Handtekeninginfo extraheren.
}
```

Hier gebruiken we de `as` sleutelwoord om te proberen elk formulierveld naar een `SignatureField`Als de cast succesvol is, weten we dat het veld een signatuur is.

## Stap 5: Het certificaat extraheren

Nu u het handtekeningveld hebt geïdentificeerd, is de volgende taak het extraheren van het certificaat uit de handtekening. Certificaten bevatten cruciale informatie over de ondertekenaar en de geldigheid van de handtekening.

```csharp
Stream cerStream = sf.ExtractCertificate();
```

De `ExtractCertificate` methode retourneert een `Stream` Object dat de certificaatgegevens bevat. Deze stroom kan worden gebruikt om het certificaat op te slaan voor verdere analyse of opslag.

## Stap 6: Het certificaat opslaan in een bestand

Nadat u het certificaat hebt uitgepakt, is de laatste stap het opslaan in een bestand. In dit geval slaan we het certificaat op als een `.cer` bestand.

```csharp
if (cerStream != null)
{
    using (cerStream)
    {
        byte[] bytes = new byte[cerStream.Length];
        using (FileStream fs = new FileStream(dataDir + @"input.cer", FileMode.CreateNew))
        {
            cerStream.Read(bytes, 0, bytes.Length);
            fs.Write(bytes, 0, bytes.Length);
        }
    }
}
```

In dit codeblok:

1. Controleer of de certificaatstroom niet nul is.
2. Lees de certificaatgegevens in een byte-array.
3. Schrijf de byte-array naar een `.cer` bestand in de documentmap.

## Conclusie

Het extraheren van digitale handtekeningen en bijbehorende certificaatinformatie uit PDF-documenten met Aspose.PDF voor .NET is vrij eenvoudig wanneer het in eenvoudige stappen wordt uitgelegd. Of u nu documenten controleert, handtekeningen verifieert of certificaten opslaat, deze tutorial geeft u de kennis om dit efficiënt te doen. Vergeet niet dat het beveiligen en verifiëren van documenten cruciaal is in de huidige digitale wereld, en tools zoals Aspose.PDF voor .NET maken dit veel eenvoudiger.

## Veelgestelde vragen

### Kan ik meerdere handtekeningen uit een PDF halen met Aspose.PDF voor .NET?
Ja, de code doorloopt alle formuliervelden in het document, waardoor u meerdere handtekeningen kunt extraheren als deze bestaan.

### Wat gebeurt er als er geen handtekening in het PDF-bestand wordt gevonden?
Als er geen handtekeningvelden aanwezig zijn, slaat de code deze gewoon over zonder een fout te genereren.

### Kan ik deze aanpak gebruiken om de geldigheid van een handtekening te verifiëren?
kunt het certificaat weliswaar extraheren, maar om de geldigheid van de handtekening te verifiëren, zijn extra stappen nodig, zoals het controleren van de vertrouwensketen van het certificaat.

### Is het mogelijk om andere formulierveldgegevens te extraheren met Aspose.PDF voor .NET?
Ja, met Aspose.PDF kunt u verschillende typen formuliervelden in een PDF openen en bewerken, niet alleen handtekeningvelden.

### Hoe kan ik de details van het geëxtraheerde certificaat bekijken?
Zodra het certificaat is opgeslagen als een `.cer` Als u een bestand hebt, kunt u het openen met een certificaatviewer of importeren in een certificaatarchief van het systeem voor nadere inspectie.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}