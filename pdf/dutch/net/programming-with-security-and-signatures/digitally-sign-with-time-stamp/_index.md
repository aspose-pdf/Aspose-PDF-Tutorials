---
"description": "Leer hoe u een PDF digitaal ondertekent met een tijdstempel met Aspose.PDF voor .NET. Deze stapsgewijze handleiding behandelt de vereisten, certificaatinstellingen, tijdstempels en meer."
"linktitle": "Digitaal ondertekenen met tijdstempel in PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Digitaal ondertekenen met tijdstempel in PDF-bestand"
"url": "/nl/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Digitaal ondertekenen met tijdstempel in PDF-bestand

## Invoering

Heb je ooit een PDF digitaal moeten ondertekenen en een tijdstempel moeten toevoegen voor extra beveiliging? Of je nu werkt aan juridische documenten, contracten of iets anders waarvoor veilige authenticatie vereist is, een digitale handtekening met een tijdstempel voegt een extra laag geloofwaardigheid toe. In deze tutorial leggen we uit hoe je Aspose.PDF voor .NET kunt gebruiken om een digitale handtekening met tijdstempel aan je PDF-documenten toe te voegen. Maak je geen zorgen, we leggen het stap voor stap uit!

## Vereisten

Voordat we de code induiken, zijn er een paar dingen die je moet instellen om te kunnen volgen. Hier is een korte checklist met de vereisten om je op weg te helpen:

- Aspose.PDF voor .NET-bibliotheek: U hebt de Aspose.PDF voor .NET-bibliotheek nodig die in uw project is geïnstalleerd. U kunt [Download hier de nieuwste versie](https://releases.aspose.com/pdf/net/) of voeg het toe aan uw project via NuGet.
- Een PDF-document: Je hebt een voorbeeld-PDF-bestand nodig om mee te werken. Zorg ervoor dat er een bestand in de map van je project staat dat je wilt ondertekenen.
- Digitaal certificaat (PFX-bestand): Zorg ervoor dat u een digitaal certificaat (een `.pfx` bestand) om het document digitaal te ondertekenen.
- Tijdstempel-URL: Dit is een online tijdstempelservice die wordt gebruikt om een tijdstempel aan de digitale handtekening te koppelen. 
- Basiskennis van C#: u hoeft geen expert te zijn, maar als u de basisbeginselen van C# kent, kunt u de code beter begrijpen en aanpassen.

Zodra je al deze vakjes hebt aangevinkt, ben je klaar om te beginnen met coderen!

## Pakketten importeren

Om te beginnen moet u de volgende naamruimten importeren in uw C#-project. Dit zorgt ervoor dat u toegang hebt tot de relevante Aspose.PDF-klassen en -functies.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## Stap 1: Het PDF-document laden

Het eerste wat we moeten doen, is het PDF-document laden dat we willen ondertekenen. Zo doe je dat:

```csharp
// Definieer het pad naar uw documentenmap
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// PDF-document laden
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

Deze stap is vrij eenvoudig. We definiëren simpelweg het pad naar het document dat we willen ondertekenen. `Document` klasse van Aspose.PDF zorgt voor het laden van het bestand.

## Stap 2: De digitale handtekening instellen

Vervolgens maken we de digitale handtekening aan met behulp van de PKCS7-klasse en laden we het PFX-bestand. Dit PFX-bestand bevat uw certificaat en persoonlijke sleutel, die nodig zijn om het document te ondertekenen.

```csharp
// Pad naar uw .pfx-bestand
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// Initialiseer het handtekeningobject
PdfFileSignature signature = new PdfFileSignature(document);

// Laad het PFX-bestand met een wachtwoord
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

Op dit punt vertelt u Aspose om uw digitale certificaat te gebruiken voor het ondertekenen van het document. `PKCS7` object regelt al het cryptografische werk voor u, zodat u zich geen zorgen hoeft te maken over de kleine details.

## Stap 3: Voeg de tijdstempelinstellingen toe

Een van de belangrijkste onderdelen van een robuuste digitale handtekening is de tijdstempel. Deze zorgt ervoor dat de handtekening van het document geverifieerd kan worden, zelfs nadat het certificaat is verlopen. Laten we de tijdstempel instellen met behulp van een online tijdstempelautoriteit.

```csharp
// Tijdstempelinstellingen definiëren
TimestampSettings timestampSettings = new TimestampSettings("https://uw_tijdstempel_url", "gebruiker:wachtwoord");

// Tijdstempelinstellingen toevoegen aan het PKCS7-object
pkcs.TimestampSettings = timestampSettings;
```

Hier geeft u de URL op voor de tijdstempelservice, die automatisch een tijd en datum aan uw handtekening toevoegt. Dit kan met of zonder authenticatie.

## Stap 4: Definieer de locatie en het uiterlijk van de handtekening

Nu gaan we bepalen waar de handtekening in de PDF komt te staan en wat de afmetingen ervan zijn. Je kunt de positie van het handtekeningvak op de pagina aanpassen, evenals de grootte.

```csharp
// Definieer het uiterlijk en de locatie van de handtekening (pagina 1, met opgegeven rechthoek)
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

Hier definiëren we een rechthoek die de handtekening op de coördinaten (100, 100) op de eerste pagina van de PDF plaatst, met een breedte van 200 en een hoogte van 100. U kunt deze waarden aanpassen aan uw ontwerp.

## Stap 5: Onderteken het PDF-document

Nu alles is ingesteld, is het tijd om de digitale handtekening daadwerkelijk op de PDF toe te passen. Deze stap combineert het certificaat, de tijdstempel en de positionering in één eenvoudige opdracht.

```csharp
// Onderteken het document op de eerste pagina
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

Dit is wat er gebeurt:
- 1: Dit geeft aan dat de handtekening op de eerste pagina moet worden aangebracht.
- 'Reden voor handtekening': Hier kunt u aangeven waarom u het document ondertekent.
- "Contact": Voer de contactgegevens van de ondertekenaar in.
- "Locatie": Geef de locatie van de ondertekenaar op.
- true: Deze Booleaanse waarde geeft aan of de handtekening zichtbaar is in het document.
- rect: De rechthoek die we eerder hebben gedefinieerd, specificeert de grootte en positie van de handtekening.
- pkcs: Het PKCS7-object bevat de instellingen voor het digitale certificaat en de tijdstempel.

## Stap 6: Sla de ondertekende PDF op

Zodra het document is ondertekend, hoeft u het alleen nog maar op te slaan. U kunt een nieuwe bestandsnaam kiezen om zowel de originele als de ondertekende versie te behouden.

```csharp
// Sla het ondertekende PDF-document op
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

Uw nieuw ondertekende en van een tijdstempel voorziene PDF is nu opgeslagen in de opgegeven map!

## Conclusie

En voilà! Je hebt met succes een PDF digitaal ondertekend met een tijdstempel met Aspose.PDF voor .NET. Dit proces garandeert de authenticiteit en integriteit van je documenten, waardoor zowel jij als de ontvanger gemoedsrust hebben. Digitale handtekeningen worden steeds belangrijker in de digitale wereld van vandaag, dus het beheersen van dit proces is zeker een vaardigheid die de moeite waard is.

## Veelgestelde vragen

### Kan ik een ander bestandsformaat gebruiken voor het certificaat?  
Ja, maar de tutorial richt zich op het gebruik van een PFX-bestand, het meestgebruikte formaat voor digitale certificaten.

### Heb ik een internetverbinding nodig om het tijdstempel toe te passen?  
Ja, aangezien het tijdstempel wordt opgehaald bij een online tijdstempelautoriteit, hebt u toegang tot internet nodig.

### Kan ik meerdere pagina's in een PDF ondertekenen?  
Absoluut! Je kunt de `signature.Sign()` Methode om meerdere pagina's te targeten of om door alle pagina's te loopen.

### Wat gebeurt er als het wachtwoord van het PFX-bestand onjuist is?  
Als het wachtwoord onjuist is, ontvangt u een uitzondering. Zorg er dus voor dat u het juiste wachtwoord invoert.

### Kan ik de handtekening onzichtbaar maken?  
Ja, je mag passeren `false` naar de `Sign` zichtbaarheidsparameter van de methode om de handtekening onzichtbaar te maken.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}