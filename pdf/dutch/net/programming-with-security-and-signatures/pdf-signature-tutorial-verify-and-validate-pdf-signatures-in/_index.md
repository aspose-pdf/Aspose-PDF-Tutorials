---
category: general
date: 2026-04-10
description: Leer een complete pdf-handtekeninghandleiding met een voorbeeld van een
  digitale handtekening. Controleer de geldigheid van de handtekening, verifieer de
  pdf-handtekening en valideer de pdf-handtekening in slechts een paar stappen.
draft: false
keywords:
- pdf signature tutorial
- digital signature example
- check signature validity
- verify pdf signature
- validate pdf signature
language: nl
og_description: 'pdf-handtekening tutorial: stapsgewijze gids om pdf-handtekening
  te verifiëren, handtekeninggeldigheid te controleren en pdf-handtekening te valideren
  met C#.'
og_title: pdf-handtekening tutorial – Verifiëren en valideren van PDF‑handtekeningen
tags:
- C#
- PDF
- Digital Signature
title: PDF-handtekening tutorial – PDF-handtekeningen verifiëren en valideren in C#
url: /nl/net/programming-with-security-and-signatures/pdf-signature-tutorial-verify-and-validate-pdf-signatures-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# pdf signature tutorial – PDF‑handtekeningen verifiëren en valideren in C#

Heb je je ooit afgevraagd hoe je **handtekeninggeldigheid** van een PDF die je van een klant hebt ontvangen kunt **controleren**? Misschien heb je naar een ondertekend document gekeken en gedacht: “Is dit echt ondertekend door de juiste autoriteit?” Dat is een veelvoorkomend pijnpunt, vooral wanneer je compliance‑controles moet automatiseren. In deze **pdf signature tutorial** lopen we een **digital signature example** door die precies laat zien hoe je **pdf signature verifieert** en **pdf signature valideert** tegen een Certificate Authority (CA)‑server—geen giswerk meer.

Wat je uit deze gids haalt: een volledig, uitvoerbaar C#‑fragment, een uitleg waarom elke regel belangrijk is, tips voor het afhandelen van randgevallen, en een snelle manier om het CA‑validatieresultaat weer te geven. Geen externe documentatie nodig; alles wat je nodig hebt staat hier. Aan het einde kun je deze logica in elke .NET‑service embedden die ondertekende PDF’s verwerkt.

## Prerequisites

Voordat we beginnen, zorg dat je het volgende hebt:

- .NET 6.0 of later (de gebruikte API is compatibel met .NET Core en .NET Framework)
- Een PDF‑bibliotheek die de klassen `Document`, `PdfFileSignature` en `ValidationContext` levert (bijv. **Aspose.PDF**, **iText7**, of een propriëtaire SDK)
- Toegang tot de CA‑server die de handtekeningen heeft uitgegeven (je hebt de validatie‑endpoint nodig)
- Een ondertekend PDF‑bestand met de naam `signed.pdf` in een map die je beheert

Als je Aspose.PDF gebruikt, installeer dan het NuGet‑pakket:

```bash
dotnet add package Aspose.PDF
```

> **Pro tip:** Houd je CA‑URL in een configuratie‑bestand; hard‑coden is prima voor een demo, maar niet voor productie.

## Stap 1 – Open het ondertekende PDF‑document

Het eerste wat we doen is de PDF laden die je wilt inspecteren. Beschouw `Document` als de container die je lees‑/schrijftoegang geeft tot elk object in het bestand.

```csharp
using Aspose.Pdf;               // Core PDF classes
using Aspose.Pdf.Facades;       // Signature‑related facades
using System;

// Step 1: Open the signed PDF document
using (var signedDocument = new Document("YOUR_DIRECTORY/signed.pdf"))
{
    // subsequent steps go here...
}
```

> **Waarom dit belangrijk is:** Het openen van het bestand binnen een `using`‑block zorgt ervoor dat de bestands‑handle direct wordt vrijgegeven, waardoor lock‑problemen worden voorkomen wanneer dezelfde PDF later opnieuw wordt verwerkt.

## Stap 2 – Maak een handtekening‑handler voor het document

Vervolgens instantieren we een `PdfFileSignature`‑object. Deze handler weet hoe hij digitale handtekeningen in de PDF moet vinden en ermee moet werken.

```csharp
// Step 2: Create a signature handler for the document
var fileSignature = new PdfFileSignature(signedDocument);
```

> **Uitleg:** `PdfFileSignature` verbergt de low‑level PDF‑structuur, zodat je handtekeningen kunt opvragen op naam of index. Het vormt de brug tussen de ruwe PDF‑bytes en de hogere‑niveau validatielogica.

## Stap 3 – Bereid een Validation Context voor met de CA‑server‑URL

Om daadwerkelijk **handtekeninggeldigheid** te **controleren**, moeten we de bibliotheek vertellen waar hij revocatie‑informatie kan opvragen. Daar komt `ValidationContext` om de hoek kijken.

```csharp
// Step 3: Prepare a validation context with the CA server URL
var validationContext = new ValidationContext
{
    CaServerUrl = "https://ca.example.com/validate"
};
```

> **Wat er gebeurt:** De `CaServerUrl` wijst naar een REST‑endpoint dat OCSP/CRL‑data retourneert. De SDK belt deze service op de achtergrond, zodat je certificaten niet handmatig hoeft te parsen.

## Stap 4 – Verifieer de gewenste handtekening met de context

Nu **verifiëren we de pdf‑handtekening**. Je kunt de naam van de handtekening doorgeven (bijv. “Signature1”) of de index. De methode retourneert een Boolean die aangeeft of de handtekening alle controles doorstaat.

```csharp
// Step 4: Verify the desired signature using the context
bool isValid = fileSignature.VerifySignature("Signature1", validationContext);
```

> **Waarom dit cruciaal is:** `VerifySignature` doet drie dingen onder de motorkap:
> 1️⃣ Bevestigt dat de cryptografische hash overeenkomt met de ondertekende data.  
> 2️⃣ Controleert de certificaatketen tot een vertrouwde root.  
> 3️⃣ Neemt contact op met de CA‑server voor de revocatiestatus.  

Als een van deze stappen faalt, wordt `isValid` `false`.

## Stap 5 – Geef het CA‑validatieresultaat weer

Tot slot geven we het resultaat weer. In een echte service zou je dit waarschijnlijk loggen of in een database opslaan, maar voor een snelle demo volstaat een console‑output.

```csharp
// Step 5: Display the CA validation result
Console.WriteLine("CA validation: " + isValid);
```

> **Verwachte output:**  
> ```
> CA validation: True
> ```
> Als de handtekening is gemanipuleerd of het certificaat is ingetrokken, zie je `False`.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is de **complete code** die je kunt copy‑pasten in een console‑applicatie:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;

class Program
{
    static void Main()
    {
        // Open the signed PDF document
        using (var signedDocument = new Document("YOUR_DIRECTORY/signed.pdf"))
        {
            // Create a signature handler for the document
            var fileSignature = new PdfFileSignature(signedDocument);

            // Prepare a validation context with the CA server URL
            var validationContext = new ValidationContext
            {
                CaServerUrl = "https://ca.example.com/validate"
            };

            // Verify the desired signature using the context
            bool isValid = fileSignature.VerifySignature("Signature1", validationContext);

            // Display the CA validation result
            Console.WriteLine("CA validation: " + isValid);
        }
    }
}
```

> **Tip:** Vervang `"YOUR_DIRECTORY/signed.pdf"` door een absoluut pad als je de app vanuit een andere werkmap start.

## Veelvoorkomende variaties & randgevallen

### Meerdere handtekeningen in één PDF

Bevat een document meer dan één handtekening, iterate dan over de handtekeningen:

```csharp
var signatures = fileSignature.GetSignatures(); // returns collection
foreach (var sigInfo in signatures)
{
    bool valid = fileSignature.VerifySignature(sigInfo.Name, validationContext);
    Console.WriteLine($"{sigInfo.Name} valid: {valid}");
}
```

### Netwerkfouten afhandelen

Wanneer de CA‑server onbereikbaar is, gooit `VerifySignature` een uitzondering. Plaats de aanroep in een try‑catch en beslis of je de handtekening als *unknown* of *invalid* wilt behandelen.

```csharp
bool isValid;
try
{
    isValid = fileSignature.VerifySignature("Signature1", validationContext);
}
catch (Exception ex)
{
    Console.WriteLine($"Validation error: {ex.Message}");
    isValid = false; // or decide based on policy
}
```

### Offline validatie (CRL‑bestanden)

Kan je omgeving de CA‑server niet bereiken, laad dan een lokale Certificate Revocation List (CRL) in de `ValidationContext`:

```csharp
validationContext.CrlFilePath = "path/to/crl.pem";
```

### Een andere PDF‑bibliotheek gebruiken

De concepten blijven hetzelfde, zelfs als je Aspose vervangt door iText7:

- Laad de PDF met `PdfReader`.
- Toegang tot handtekeningen via `PdfSignatureUtil`.
- Stel een `OcspClient` of `CrlClient` in die naar jouw CA wijst.

De syntaxis verandert, maar het **digital signature example** volgt nog steeds dezelfde vijf‑stappen‑flow.

## Praktische tips uit de praktijk

- **Cache CA‑reacties**: Het herhaaldelijk opvragen van hetzelfde certificaat binnen een kort tijdsbestek verspilt bandbreedte. Sla OCSP‑reacties op met een configureerbare TTL.
- **Valideer timestamps**: Sommige handtekeningen bevatten een vertrouwde timestamp. Controleren of de timestamp binnen de geldigheidsperiode van het certificaat valt, voegt een extra zekerheid toe.
- **Log de volledige certificaatketen**: Als er iets misgaat, versnelt het hebben van de keten in je logs de foutopsporing enorm.
- **Vertrouw nooit op door gebruikers geleverde bestands‑paden**: Sanitize altijd het pad of gebruik een sandbox‑map om pad‑traversal‑aanvallen te voorkomen.

## Visueel overzicht

![pdf signature tutorial diagram showing the flow from opening a PDF to CA validation and result output](/images/pdf-signature-tutorial.png)

*Afbeeldings‑alt‑tekst: pdf signature tutorial diagram dat de stroom van het openen van een PDF naar CA‑validatie en resultaatoutput toont*

## Samenvatting

In deze **pdf signature tutorial** hebben we:

1. Een ondertekende PDF geopend (`Document`).
2. Een `PdfFileSignature`‑handler aangemaakt.
3. Een `ValidationContext` opgebouwd die naar de CA‑server wijst.
4. `VerifySignature` aangeroepen om **handtekeninggeldigheid** te **controleren**.
5. Het **CA‑validatieresultaat** uitgeprint.

Je hebt nu een solide basis om **pdf signature te verifiëren** en **pdf signature te valideren** in elke .NET‑applicatie, of je nu facturen, contracten of overheidsformulieren verwerkt.

## Wat is het vervolg?

- **Batchverwerking**: Breid het voorbeeld uit om een map met PDF’s te scannen en een CSV‑rapport te genereren.
- **Integratie met ASP.NET Core**: Exposeer een API‑endpoint dat een PDF‑stream accepteert en een JSON‑payload met validatieresultaten teruggeeft.
- **Timestamp‑validatie verkennen**: Voeg ondersteuning toe voor `PdfTimestamp`‑objecten om te verzekeren dat de handtekening niet is gemaakt nadat het certificaat is verlopen.
- **Beveilig de CA‑URL**: Verplaats deze naar `appsettings.json` en bescherm hem met Azure Key Vault of AWS Secrets Manager.

Voel je vrij om te experimenteren—vervang de CA‑URL, probeer verschillende handtekeningnamen, of onderteken zelfs je eigen PDF’s om de volledige cyclus in actie te zien. Als je ergens vastloopt, wijzen de opmerkingen in de code je de juiste kant op, en de community is altijd een zoekopdracht verwijderd.

Happy coding, en moge al je PDF’s tamper‑proof blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}