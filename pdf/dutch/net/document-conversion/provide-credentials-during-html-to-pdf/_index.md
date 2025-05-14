---
"description": "Leer hoe je HTML naar PDF converteert met Aspose.PDF voor .NET met deze stapsgewijze handleiding. Perfect voor ontwikkelaars die de documentgeneratie willen stroomlijnen."
"linktitle": "Geef referenties op tijdens HTML naar PDF"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Geef referenties op tijdens HTML naar PDF"
"url": "/nl/net/document-conversion/provide-credentials-during-html-to-pdf/"
"weight": 240
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Geef referenties op tijdens HTML naar PDF

## Invoering

In de wereld van softwareontwikkeling is het converteren van HTML naar PDF een veelvoorkomende vereiste. Of u nu rapporten, facturen of andere documenten genereert, een betrouwbare bibliotheek die deze taak afhandelt, kan u veel tijd en moeite besparen. Maak kennis met Aspose.PDF voor .NET, een krachtige bibliotheek waarmee ontwikkelaars eenvoudig PDF-documenten kunnen maken, bewerken en converteren. In deze tutorial leiden we u door het proces van het gebruik van Aspose.PDF om HTML naar PDF te converteren en bieden we u inloggegevens voor beveiligde toegang. Dus, pak uw programmeerhoed en laten we beginnen!

## Vereisten

Voordat we beginnen, zijn er een paar dingen die u moet regelen:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. Dit wordt onze ontwikkelomgeving.
2. Aspose.PDF voor .NET: U kunt de bibliotheek downloaden van de [website](https://releases.aspose.com/pdf/net/)Als je het eerst wilt uitproberen, kun je ook een [gratis proefperiode](https://releases.aspose.com/).
3. Basiskennis van C#: Kennis van C#-programmering helpt u de voorbeelden beter te begrijpen.
4. Internettoegang: Omdat we HTML-inhoud van een URL ophalen, moet u ervoor zorgen dat u een actieve internetverbinding hebt.

## Pakketten importeren

Om aan de slag te gaan met Aspose.PDF, moet je de benodigde pakketten in je project importeren. Zo doe je dat:

1. Open uw Visual Studio-project.
2. Klik met de rechtermuisknop op uw project in Solution Explorer en selecteer 'NuGet-pakketten beheren'.
3. Zoek naar "Aspose.PDF" en installeer de nieuwste versie.

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Net;
```
Nu we alles hebben ingesteld, kunnen we het proces van het converteren van HTML naar PDF met inloggegevens opsplitsen in beheersbare stappen.

## Stap 1: Stel uw documentenmap in

Voordat we HTML naar PDF kunnen converteren, moeten we opgeven waar onze PDF-uitvoer moet worden opgeslagen. Dit doen we door een pad naar de documentenmap te definiëren.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Vervangen `"YOUR DOCUMENT DIRECTORY"` met het daadwerkelijke pad waar u uw PDF-bestand wilt opslaan. Dit kan een map op uw bureaublad zijn of een andere locatie op uw systeem.

## Stap 2: Een webverzoek maken

Vervolgens moeten we een verzoek aanmaken om de HTML-inhoud van een specifieke URL op te halen. Hiervoor gebruiken we de `WebRequest` klas.

```csharp
WebRequest request = WebRequest.Create("http://My.signchart.com/Report/PrintBook.asp?ProjectGuid=6FB9DBB0-");
```

Hier maken we een verzoek aan voor de URL die de HTML bevat die we willen converteren. Zorg ervoor dat je de URL vervangt door de URL die je wilt gebruiken.

## Stap 3: Stel inloggegevens in (indien vereist)

Als de server inloggegevens nodig heeft om toegang te krijgen tot de inhoud, moeten we deze instellen. Dit doen we met behulp van de `CredentialCache.DefaultCredentials`.

```csharp
request.Credentials = CredentialCache.DefaultCredentials;
```

Deze regel zorgt ervoor dat de aanvraag de standaardreferenties van de huidige gebruiker gebruikt. Als u specifieke referenties moet opgeven, kunt u een nieuwe maken. `NetworkCredential` voorwerp.

## Stap 4: Ontvang het antwoord

Nu we ons verzoek hebben ingesteld, is het tijd om het antwoord van de server te ontvangen.

```csharp
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
```

Deze regel verstuurt het verzoek en wacht op een reactie van de server. Als alles goed gaat, ontvangen we de HTML-inhoud die we nodig hebben.

## Stap 5: Lees de responsstroom

Zodra we het antwoord hebben, moeten we de inhoud die door de server is geretourneerd, lezen. Dit doen we met behulp van een `StreamReader`.

```csharp
Stream dataStream = response.GetResponseStream();
StreamReader reader = new StreamReader(dataStream);
string responseFromServer = reader.ReadToEnd();
reader.Close();
dataStream.Close();
response.Close();
```

Hier lezen we de volledige inhoud van de responsstroom in een tekenreeksvariabele met de naam `responseFromServer`Vergeet niet de reader en de stream te sluiten om bronnen vrij te maken.

## Stap 6: HTML naar PDF converteren

Nu komt het spannende gedeelte! We zetten de HTML-inhoud om in een PDF-document met Aspose.PDF.

```csharp
MemoryStream stream = new MemoryStream(System.Text.Encoding.UTF8.GetBytes(responseFromServer));
HtmlLoadOptions options = new HtmlLoadOptions("http://Mijn.signchart.com/");
options.ExternalResourcesCredentials = CredentialCache.DefaultCredentials;

Document pdfDocument = new Document(stream, options);
```

In deze stap maken we een `MemoryStream` van de HTML-inhoud en het instellen `HtmlLoadOptions`Hiermee kunnen we de basis-URL voor externe bronnen (zoals afbeeldingen of stijlbladen) opgeven waarnaar de HTML mogelijk verwijst.

## Stap 7: Sla het PDF-document op

Ten slotte moeten we het gegenereerde PDF-document opslaan in de opgegeven map.

```csharp
pdfDocument.Save(dataDir + "ProvideCredentialsDuringHTMLToPDF_out.pdf");
```

Deze regel slaat het PDF-bestand op met de naam `ProvideCredentialsDuringHTMLToPDF_out.pdf` in de directory die we eerder hebben opgegeven.

## Conclusie

En voilà! Je hebt HTML succesvol naar PDF geconverteerd met Aspose.PDF voor .NET en hebt inloggegevens voor veilige toegang verstrekt. Deze krachtige bibliotheek maakt het werken met PDF-documenten eenvoudig en met slechts een paar regels code kun je professioneel ogende PDF's genereren van HTML-inhoud. 

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een bibliotheek waarmee ontwikkelaars PDF-documenten in .NET-toepassingen kunnen maken, bewerken en converteren.

### Hoe installeer ik Aspose.PDF?
U kunt Aspose.PDF installeren via NuGet Package Manager in Visual Studio of het downloaden van de [website](https://releases.aspose.com/pdf/net/).

### Kan ik Aspose.PDF gratis gebruiken?
Ja, Aspose biedt een gratis proefversie aan waarmee u de bibliotheek kunt uitproberen voordat u tot aankoop overgaat.

### Welke soorten documenten kan ik maken met Aspose.PDF?
Met Aspose.PDF kunt u een breed scala aan documenten maken, waaronder rapporten, facturen en formulieren.

### Waar kan ik ondersteuning vinden voor Aspose.PDF?
U kunt ondersteuning vinden en vragen stellen op de [Aspose-ondersteuningsforum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}