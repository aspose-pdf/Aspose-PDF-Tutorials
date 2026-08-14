---
category: general
date: 2026-08-14
description: Maak handtekeningopties in C# om een digitale handtekening toe te passen.
  Leer hoe je de handtekening configureert, een aangepaste hash‑functie implementeert
  en documenten programmeermatig ondertekent.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: nl
lastmod: 2026-08-14
og_description: Maak handtekeningopties in C# en pas een digitale handtekening toe.
  Deze tutorial leidt je door het configureren van de handtekening, het toevoegen
  van een aangepaste hash‑functie en het ondertekenen van een document.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Maak handtekeningopties in C# – stapsgewijze gids voor digitale ondertekening
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  headline: Create signature options in C# – full guide to digital signing
  type: TechArticle
- description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  name: Create signature options in C# – full guide to digital signing
  steps:
  - name: '**Hash calculation** – now delegated to your custom hash function.'
    text: '**Hash calculation** – now delegated to your custom hash function.'
  - name: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
    text: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
  - name: '**Embedding** – the generated signature is attached to the output file.'
    text: '**Embedding** – the generated signature is attached to the output file.'
  type: HowTo
tags:
- digital signature
- C#
- security
title: Maak handtekeningopties in C# – volledige gids voor digitale ondertekening
url: /nl/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak handtekeningopties in C# – volledige gids voor digitale ondertekening

Maak handtekeningopties in C# om een digitale‑handtekening‑workflow te configureren. Deze tutorial laat zien hoe je een digitale handtekening toepast, een aangepaste hash‑functie implementeert en een document ondertekent met de `SignatureOptions`‑klasse. Als je ooit een PDF, XML of een willekeurige binaire payload vanuit een .NET‑applicatie moest ondertekenen, bieden de onderstaande stappen een kant‑en‑klaar werkende oplossing.

Je leert hoe je:

* `SignatureOptions` configureert met een aangepaste hash‑algoritme,
* de ondertekeningsmethode correct aanroept,
* verifieert dat de handtekening is toegepast,
* veelvoorkomende valkuilen bij het configureren van de handtekening vermijdt.

De enige vereisten zijn een recente .NET SDK (≥ .NET 6) en een ondertekeningsbibliotheek die `SignatureOptions` beschikbaar stelt (bijvoorbeeld **GroupDocs.Signature**, **Aspose.Signature**, of een vergelijkbare API). Er zijn geen externe tools nodig.

---

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| .NET 6 SDK of later | Biedt de moderne taalfeatures die in de voorbeelden worden gebruikt. |
| Een ondertekenings‑bibliotheek NuGet‑pakket (bijv. `GroupDocs.Signature`) | Levert het type `SignatureOptions` en de `Sign` extensiemethode. |
| Toegang tot een privésleutel of certificaat | Vereist om een verifieerbare digitale handtekening te genereren. |

Installeer de bibliotheek met de standaard CLI:

```bash
dotnet add package GroupDocs.Signature
```

---

## Stap 1: Maak handtekeningopties

De eerste stap is het instantieren van `SignatureOptions` en het instellen van de eigenschappen die het ondertekeningsproces regelen. Dit object vertelt de bibliotheek *wat* er moet worden ondertekend en *hoe*.

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

// Create a new SignatureOptions instance
var signatureOptions = new SignatureOptions
{
    // The signing algorithm (e.g., RSA‑SHA256) is defined by the library.
    // You can also set visual appearance, page number, etc., here.
    // For this tutorial we focus on the custom hash function.
};
```

**Waarom dit belangrijk is:** `SignatureOptions` fungeert als een contract tussen jouw code en de ondertekeningsengine. Door het vooraf te configureren vermijd je herhaaldelijke boilerplate bij het ondertekenen van meerdere documenten.

---

## Stap 2: Implementeer een aangepaste hash‑functie

Een *aangepaste hash‑functie* geeft je volledige controle over de digest die het handtekeningalgoritme ondertekent. Dit is nuttig wanneer de standaard hash (SHA‑256) niet voldoet aan compliance‑eisen of wanneer je slechts een deel van het document moet hashen.

```csharp
using System.Security.Cryptography;
using System.Text;

// Define a delegate that matches the library’s expected signature
Func<byte[], byte[]> MyHash = data =>
{
    // Example: compute SHA‑512 and then truncate to 256 bits
    using var sha512 = SHA512.Create();
    var fullHash = sha512.ComputeHash(data);

    // Truncate to the first 32 bytes (256 bits)
    var truncated = new byte[32];
    Buffer.BlockCopy(fullHash, 0, truncated, 0, truncated.Length);
    return truncated;
};

// Attach the custom hash to the options
signatureOptions.CustomSignHash = hash => MyHash(hash);
```

**Waarom dit belangrijk is:** Door `CustomSignHash` toe te wijzen, vervang je de interne hash‑stap van de bibliotheek door `MyHash`. De ondertekeningsengine ondertekent nu de bytes die jouw functie retourneert, waardoor je voldoet aan elke aangepaste beleidsregel.

---

## Stap 3: Laad het document en pas digitale handtekening toe

Met de opties klaar kun je nu het doelbestand openen en de ondertekeningsmethode aanroepen. De methode `Sign` wordt door de bibliotheek geleverd en maakt gebruik van de geconfigureerde `SignatureOptions`.

```csharp
using System.IO;

// Path to the file you want to sign
string inputPath = @"C:\Docs\contract.pdf";
string outputPath = @"C:\Docs\contract.signed.pdf";

// Load the document into the Signature object
using var signature = new Signature(inputPath);

// Sign the document using the previously created options
bool result = signature.Sign(outputPath, signatureOptions);

if (!result)
{
    throw new InvalidOperationException("The document could not be signed.");
}
```

**Waarom dit belangrijk is:** De aanroep van `Sign` voert intern drie acties uit:

1. **Hash‑berekening** – nu gedelegeerd aan jouw aangepaste hash‑functie.  
2. **Handtekeninggeneratie** – met de privésleutel die aan de configuratie van de bibliotheek is geleverd.  
3. **Invoeging** – de gegenereerde handtekening wordt aan het uitvoerbestand toegevoegd.

Als een stap faalt, retourneert de methode `false`, zodat je de fout op een nette manier kunt afhandelen.

---

## Stap 4: Verifieer dat het document is ondertekend

Een snelle verificatie bevestigt dat de handtekening correct is toegepast. De meeste bibliotheken bieden een `Verify`‑methode die de integriteit van het ondertekende bestand controleert.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Waarom dit belangrijk is:** Verificatie zorgt ervoor dat het ondertekende document niet is gemanipuleerd na ondertekening en dat de aangepaste hash een compatibele digest heeft opgeleverd.

---

## Hoe handtekening configureren voor verschillende bestandstypen

Hetzelfde `SignatureOptions`‑object kan opnieuw worden gebruikt voor PDF’s, Word‑documenten, afbeeldingen of ruwe binaire bestanden. Het enige wat je hoeft te wijzigen is de specifieke opties‑klasse (bijv. `PdfSignatureOptions`, `WordSignatureOptions`). Hieronder een kort voorbeeld voor een JPEG‑afbeelding:

```csharp
using GroupDocs.Signature.Options;

var imageOptions = new ImageSignatureOptions
{
    // Position the signature on the image
    Left = 100,
    Top = 50,
    Width = 150,
    Height = 50,
    CustomSignHash = hash => MyHash(hash)   // reuse the same custom hash
};

using var imgSignature = new Signature(@"C:\Images\photo.jpg");
imgSignature.Sign(@"C:\Images\photo.signed.jpg", imageOptions);
```

**Waarom dit belangrijk is:** Begrijpen hoe je *handtekening configureert* per formaat stelt je in staat om dezelfde codebasis over meerdere documenttypen uit te breiden zonder de hash‑logica opnieuw te schrijven.

---

## Veelvoorkomende valkuilen en best practices

| Valkuil | Aanbevolen oplossing |
|---------|----------------------|
| Vergeten `CustomSignHash` in te stellen na het maken van `SignatureOptions` | Wijs de delegate direct toe na het construeren van het opties‑object. |
| Een hash‑algoritme gebruiken dat het ondertekeningscertificaat niet ondersteunt | Controleer of het sleutelgebruik van het certificaat overeenkomt met de hash‑lengte (bijv. RSA‑2048 met SHA‑512). |
| Het niet vrijgeven van `Signature`‑objecten | Plaats de `Signature`‑instantie in een `using`‑blok om bestands‑handles vrij te geven. |
| Het ondertekende bestand overschrijven op de originele bron | Schrijf altijd naar een nieuw bestandspad (`outputPath`) om het originele document te behouden. |

---

## Volledig werkend voorbeeld

Hieronder vind je een zelfstandig programma dat alle onderdelen samenbrengt. Kopieer het naar een nieuw console‑project en voer het uit; de console geeft succes of falen weer.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

class Program
{
    // Custom hash implementation (SHA‑512 truncated to 256 bits)
    private static byte[] MyHash(byte[] data)
    {
        using var sha512 = SHA512.Create();
        var full = sha512.ComputeHash(data);
        var truncated = new byte[32];
        Buffer.BlockCopy(full, 0, truncated, 0, truncated.Length);
        return truncated;
    }

    static void Main()
    {
        // Paths
        string input = @"C:\Docs\contract.pdf";
        string output = @"C:\Docs\contract.signed.pdf";

        // Step 1: create signature options
        var signatureOptions = new SignatureOptions
        {
            CustomSignHash = hash => MyHash(hash)
        };

        // Step 2: sign the document
        using var signer = new Signature(input);
        bool signed = signer.Sign(output, signatureOptions);
        if (!signed)
        {
            Console.WriteLine("Signing failed.");
            return;
        }

        // Step 3: verify the signature
        using var verifier = new Signature(output);
        bool verified = verifier.Verify();
        Console.WriteLine(verified
            ? "Signature verified successfully."
            : "Signature verification failed.");
    }
}
```

**Verwachte uitvoer**

```
Signature verified successfully.
```

Als de console “Signing failed.” of “Signature verification failed.” afdrukt, controleer dan de certificaatconfiguratie en zorg ervoor dat de aangepaste hash een byte‑array van de verwachte grootte retourneert.

---

## Conclusie

Je weet nu hoe je **handtekeningopties maakt** in C#, een **aangepaste hash‑functie** toevoegt, en een **digitale handtekening toepast** op elk ondersteund document. De tutorial besloeg de volledige levenscyclus: configureren van de opties, ondertekenen van het bestand en verifiëren van het resultaat. Door dezelfde `SignatureOptions`‑instantie te hergebruiken kun je ook **handtekening configureren** voor afbeeldingen, Word‑bestanden of ruwe binaire data.

---

## Wat kun je hierna doen?

* Verken extra `SignatureOptions`‑eigenschappen zoals visuele stempels, timestamp‑servers en certificaat‑ketens – deze sluiten aan bij het **apply digital signature**‑keyword.  
* Experimenteer met andere hash‑algoritmen (bijv. Blake2b) door de implementatie binnen `MyHash` te vervangen.  
* Integreer de ondertekeningsstroom in een web‑API om on‑the‑fly documentondertekening mogelijk te maken – een natuurlijke uitbreiding van **how to sign document** in een service‑georiënteerde architectuur.

Voel je vrij om de code aan te passen aan je eigen beveiligingsbeleid, en deel je ervaringen in de reacties. Veel succes met ondertekenen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken uit deze gids. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Hoe PDF-handtekeningtaal wijzigen met Aspose.PDF voor .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}