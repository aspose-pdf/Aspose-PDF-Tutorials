---
category: general
date: 2026-08-14
description: Skapa signaturalternativ i C# för att tillämpa digital signatur. Lär
  dig hur du konfigurerar signaturen, implementerar en anpassad hashfunktion och signerar
  dokument programatiskt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: sv
lastmod: 2026-08-14
og_description: Skapa signaturalternativ i C# och tillämpa en digital signatur. Denna
  handledning guidar dig genom att konfigurera signaturen, lägga till en anpassad
  hash‑funktion och signera ett dokument.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Skapa signaturalternativ i C# – steg‑för‑steg guide för digital signering
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
title: Skapa signaturalternativ i C# – fullständig guide till digital signering
url: /sv/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa signaturalternativ i C# – fullständig guide till digital signering

Skapa signaturalternativ i C# för att konfigurera ett digitalt signaturflöde. Denna handledning visar hur du tillämpar digital signatur, implementerar en anpassad hash‑funktion och signerar ett dokument med hjälp av klassen `SignatureOptions`. Om du någonsin har behövt signera en PDF, XML eller någon binär payload från en .NET‑applikation, ger stegen nedan en färdig‑att‑köra‑lösning.

Du kommer att lära dig hur du:

* konfigurerar `SignatureOptions` med en anpassad hash‑algoritm,
* anropar signeringsmetoden korrekt,
* verifierar att signaturen har tillämpats,
* undviker vanliga fallgropar när du konfigurerar signaturen.

Det enda som krävs är ett modernt .NET SDK (≥ .NET 6) och ett signeringsbibliotek som exponerar `SignatureOptions` (t.ex. **GroupDocs.Signature**, **Aspose.Signature** eller ett liknande API). Inga externa verktyg behövs.

---

## Förutsättningar

| Krav | Varför det är viktigt |
|------|-----------------------|
| .NET 6 SDK eller senare | Tillhandahåller de moderna språkfunktionerna som används i exemplen. |
| Ett signerings‑bibliotek NuGet‑paket (t.ex. `GroupDocs.Signature`) | Tillhandahåller typen `SignatureOptions` och `Sign`‑utökningsmetoden. |
| Tillgång till en privat nyckel eller certifikat | Krävs för att generera en verifierbar digital signatur. |

Installera biblioteket med den vanliga CLI:n:

```bash
dotnet add package GroupDocs.Signature
```

---

## Steg 1: Skapa signaturalternativ

Det första steget är att instansiera `SignatureOptions` och sätta de egenskaper som styr signeringsprocessen. Detta objekt talar om för biblioteket *vad* som ska signeras och *hur* det ska signeras.

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

**Varför detta är viktigt:** `SignatureOptions` fungerar som ett avtal mellan din kod och signeringsmotorn. Genom att konfigurera det i förväg undviker du upprepad boilerplate när du signerar flera dokument.

---

## Steg 2: Implementera en anpassad hash‑funktion

En *anpassad hash‑funktion* ger dig full kontroll över digest‑värdet som signaturalgoritmen signerar. Detta är användbart när standard‑hashen (SHA‑256) inte uppfyller efterlevnadskrav eller när du behöver hash‑a en delmängd av dokumentet.

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

**Varför detta är viktigt:** Genom att tilldela `CustomSignHash` ersätter du bibliotekets interna hash‑steg med `MyHash`. Signeringsmotorn kommer nu att signera de byte som returneras av din funktion, vilket säkerställer efterlevnad av eventuella anpassade policyer.

---

## Steg 3: Ladda dokumentet och tillämpa digital signatur

När alternativen är förberedda kan du nu öppna målfilen och anropa signeringsmetoden. Metoden `Sign` tillhandahålls av biblioteket och använder de konfigurerade `SignatureOptions`.

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

**Varför detta är viktigt:** Anropet till `Sign` utför tre handlingar internt:

1. **Hash‑beräkning** – nu delegerad till din anpassade hash‑funktion.
2. **Signaturgenerering** – med den privata nyckel som levereras till bibliotekets konfiguration.
3. **Inbäddning** – den genererade signaturen bifogas till utdatafilen.

Om något steg misslyckas returnerar metoden `false`, vilket låter dig hantera felet på ett smidigt sätt.

---

## Steg 4: Verifiera att dokumentet är signerat

En snabb verifiering bekräftar att signaturen har tillämpats korrekt. De flesta bibliotek exponerar en `Verify`‑metod som kontrollerar integriteten hos den signerade filen.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Varför detta är viktigt:** Verifiering säkerställer att det signerade dokumentet inte har manipulerats efter signering och att den anpassade hashen producerade ett kompatibelt digest.

---

## Hur man konfigurerar signatur för olika filtyper

Samma `SignatureOptions`‑objekt kan återanvändas för PDF‑filer, Word‑dokument, bilder eller rena binärfiler. Den enda förändring som krävs är den specifika alternativklassen (t.ex. `PdfSignatureOptions`, `WordSignatureOptions`). Här är ett snabbt exempel för en JPEG‑bild:

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

**Varför detta är viktigt:** Att förstå hur man *konfigurerar signatur* för varje format låter dig utöka samma kodbas över flera dokumenttyper utan att skriva om hash‑logiken.

---

## Vanliga fallgropar och bästa praxis

| Fallgrop | Rekommenderad åtgärd |
|----------|----------------------|
| Glömmer att sätta `CustomSignHash` efter att ha skapat `SignatureOptions` | Tilldela delegaten omedelbart efter att ha konstruerat options‑objektet. |
| Använder en hash‑algoritm som signeringscertifikatet inte stödjer | Verifiera att certifikatets nyckelanvändning matchar hash‑längden (t.ex. RSA‑2048 med SHA‑512). |
| Förbiser behovet av att disponera `Signature`‑objekt | Omslut `Signature`‑instansen i ett `using`‑block för att frigöra filhandtag. |
| Spara den signerade filen över originalkällan | Skriv alltid till en ny filsökväg (`outputPath`) för att bevara originaldokumentet. |

---

## Fullt fungerande exempel

Nedan är ett självständigt program som sätter ihop alla delar. Kopiera det till ett nytt konsolprojekt och kör det; konsolen kommer att rapportera framgång eller misslyckande.

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

**Förväntad utdata**

```
Signature verified successfully.
```

Om konsolen skriver ut “Signing failed.” eller “Signature verification failed.”, dubbelkolla certifikatkonfigurationen och säkerställ att den anpassade hashen returnerar en byte‑array av förväntad storlek.

---

## Slutsats

Du vet nu hur du **skapar signaturalternativ** i C#, bifogar en **anpassad hash‑funktion** och **tillämpa digital signatur** på vilket stödjande dokument som helst. Handledningen täckte hela livscykeln: konfigurera alternativen, signera filen och verifiera resultatet. Genom att återanvända samma `SignatureOptions`‑instans kan du också **hur man konfigurerar signatur** för bilder, Word‑filer eller råa binärer.

---

## Vad blir nästa?

* Utforska ytterligare `SignatureOptions`‑egenskaper såsom visuella stämplar, tidsstämpelservrar och certifikatkedjor – dessa matchar nyckelordet **apply digital signature**.
* Experimentera med andra hash‑algoritmer (t.ex. Blake2b) genom att byta implementationen i `MyHash`.
* Integrera signeringsflödet i ett web‑API för att möjliggöra on‑the‑fly‑dokumentsignering – en naturlig utvidgning av **how to sign document** i en service‑orienterad arkitektur.

Känn dig fri att anpassa koden efter dina egna säkerhetspolicyer och dela dina erfarenheter i kommentarerna. Lycka till med signeringen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Change PDF Signature Language with Aspose.PDF for .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}