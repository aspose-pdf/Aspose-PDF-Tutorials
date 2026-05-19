---
category: general
date: 2026-03-24
description: Laad een PFX‑certificaat in C# snel en veilig om een PKCS7‑detached‑handtekening
  van een bestand te maken. Stapsgewijze handleiding met volledige code en valkuilen.
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: nl
og_description: Laad PFX‑certificaat C# en genereer een PKCS7‑gedetacheerde handtekening
  vanuit een bestand. Volledig voorbeeld met uitleg en afhandeling van randgevallen.
og_title: PFX-certificaat laden C# – PKCS7 losgekoppelde handtekening maken
tags:
- C#
- PKCS7
- X509
- Cryptography
title: PFX‑certificaat laden in C# – Maak een PKCS7‑ontkoppelde handtekening
url: /nl/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PFX-certificaat laden in C# – PKCS7 Detached-handtekening maken

Heb je ooit **een PFX-certificaat in C# moeten laden** alleen om wat gegevens te ondertekenen, maar wist je niet waar je moest beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen dezelfde muur aan wanneer ze voor het eerst X.509-certificaten en PKCS#7 aanraken.  

Het goede nieuws? In deze tutorial krijg je een kant‑klaar werkende oplossing die **een PFX-certificaat laadt in C#**, een **PKCS7 detached-handtekening** maakt, en zelfs laat zien hoe je de handtekening uit een bestand haalt. Geen vage verwijzingen, alleen concrete code en de redenering achter elke regel.

> **Wat je zult meenemen**  
> * Een duidelijk begrip van het certificaat‑laadproces.  
> * Een volledig, compileerbaar voorbeeld dat een PKCS7 detached-handtekening maakt.  
> * Tips voor het omgaan met veelvoorkomende valkuilen (verkeerd wachtwoord, ontbrekend bestand, algoritme‑mismatch).  

### Vereisten

- .NET 6.0 of later (de gebruikte API's maken deel uit van de basis‑class library).  
- Een geldig `.pfx`‑bestand en het bijbehorende wachtwoord.  
- Visual Studio 2022 of een andere editor naar keuze—geen speciale NuGet‑pakketten nodig voor het kernvoorbeeld.  

Als je die hebt, laten we erin duiken.

---

## PFX-certificaat laden in C# – Stap‑voor‑stap

Hieronder staat de minimale set `using`‑directieven die je nodig hebt. Houd ze bovenaan je bestand zodat de compiler weet waar de types te vinden zijn.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ Specificeer het certificaatpad en wachtwoord

Eerst, geef de runtime aan waar het `.pfx`‑bestand zich bevindt en wat het wachtwoord is. Paden hard‑coderen is acceptabel voor een demo, maar **nooit** wachtwoorden in productcode opnemen.

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **Pro tip:** Sla het wachtwoord op in Azure Key Vault, AWS Secrets Manager, of een omgevingsvariabele—commit het nooit naar source control.

### 2️⃣ Laad het certificaat veilig

We omhullen het laden in een `try / catch`‑blok om veelvoorkomende fouten, zoals een ontbrekend bestand of een onjuist wachtwoord, zichtbaar te maken.

```csharp
X509Certificate2 LoadCertificate(string path, string password)
{
    try
    {
        // The X509KeyStorageFlags ensure the private key is exportable for signing
        var cert = new X509Certificate2(path, password,
            X509KeyStorageFlags.MachineKeySet |
            X509KeyStorageFlags.PersistKeySet |
            X509KeyStorageFlags.Exportable);

        if (!cert.HasPrivateKey)
            throw new InvalidOperationException("The certificate does not contain a private key.");

        return cert;
    }
    catch (Exception ex) when (ex is CryptographicException || ex is IOException)
    {
        Console.Error.WriteLine($"Failed to load certificate: {ex.Message}");
        throw;
    }
}
```

### 3️⃣ Maak een **PKCS7 detached-handtekening**‑object

Aangenomen dat je een third‑party‑bibliotheek gebruikt die een `PKCS7Detached`‑klasse blootlegt (veel commerciële SDK's doen dat), maken we een instantie aan met het certificaat dat we zojuist hebben geladen.

```csharp
// Step 3: Build the signer
var certificate = LoadCertificate(certificatePath, certificatePassword);

var pkcs7Signer = new PKCS7Detached(certificate)
{
    // Provide a custom hash‑signing callback.
    // The library will invoke this delegate for each hash it needs to sign.
    CustomSignHash = (hash, algorithm) => MySigner.Sign(hash, algorithm)
};
```

> **Waarom een callback?** Sommige SDK's laten je hardware security modules (HSM's) of externe ondertekeningsdiensten aansluiten. Door `CustomSignHash` bloot te stellen, houd je de ondertekeningslogica flexibel.

### 4️⃣ Implementeer de ondertekenings‑delegate

Hier is een eenvoudige implementatie die de privésleutel van het geladen certificaat gebruikt. Vervang `MySigner.Sign` door je eigen HSM‑aanroep indien nodig.

```csharp
static class MySigner
{
    public static byte[] Sign(byte[] hash, HashAlgorithmName algorithm)
    {
        // The certificate's private key is an RSA key in most cases.
        using RSA rsa = certificate.GetRSAPrivateKey()
            ?? throw new InvalidOperationException("RSA private key not available.");

        // RSA-PKCS#1 v1.5 signing – adjust if your policy requires PSS.
        return rsa.SignHash(hash, algorithm, RSASignaturePadding.Pkcs1);
    }
}
```

### 5️⃣ Onderteken willekeurige data en haal de detached PKCS7‑blob op

Nu ondertekenen we daadwerkelijk iets. De data kan een bestand, een JSON‑payload of wat je ook moet beschermen zijn.

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**Verwachte output**

```
Detached PKCS7 signature created successfully.
```

Je hebt nu een **PKCS7‑handtekening uit bestand** (`sample.txt.sig`) die onafhankelijk van de oorspronkelijke data kan worden geverifieerd.

---

## PKCS7 Detached-handtekening maken – Geavanceerde opties

Hoewel de basisstroom voor de meeste scenario's werkt, hebben productiesystemen vaak extra instellingen nodig:

| Functie | Hoe in te schakelen | Wanneer te gebruiken |
|---------|---------------------|----------------------|
| **Algoritme‑selectie** | Geef `HashAlgorithmName.SHA256` (of SHA384/SHA512) door aan `SignHash` | Als je compliance‑regime een specifiek hash vereist |
| **Tijdstempeling** | Voeg een RFC‑3161 tijdstempel toe na de handtekening | Voor langdurige validatie |
| **Meerdere ondertekenaars** | Maak extra `PKCS7Detached`‑instanties aan en voeg ze samen | Wanneer documenten co‑ondertekening nodig hebben |
| **Aangepaste CMS‑attributen** | Gebruik de `AddAttribute`‑methode van de bibliotheek vóór `Sign` | Om ondertekeningtijd, ondertekenaar‑ID, enz. in te sluiten |

Hieronder staat een snel fragment dat SHA‑256‑selectie laat zien:

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

---

## PKCS7 Detached-handtekening verifiëren (optioneel)

Verificatie is de andere helft van het verhaal. De meeste bibliotheken bieden een `Verify`‑methode die de oorspronkelijke data en de detached‑handtekening neemt.

```csharp
bool VerifySignature(byte[] originalData, byte[] signature, X509Certificate2 cert)
{
    var verifier = new PKCS7Detached(cert);
    return verifier.Verify(originalData, signature);
}

// Usage
bool isValid = VerifySignature(dataToSign, detachedSignature, certificate);
Console.WriteLine(isValid ? "Signature valid!" : "Signature invalid!");
```

Als je een andere SDK gebruikt, zoek dan naar een `CmsSignedData`‑ of `SignedCms`‑klasse in .NET’s `System.Security.Cryptography.Pkcs`‑namespace—die kunnen ook detached‑handtekeningen verwerken.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

1. **Verkeerd wachtwoord** – De `CryptographicException` zal melden *“The specified network password is not correct.”* Bewaar wachtwoorden veilig en test ze onafhankelijk voordat je het certificaat laadt.  
2. **Certificaat zonder privésleutel** – Sommige `.pfx`‑bestanden worden geëxporteerd zonder de privésleutel. Controleer de exportinstellingen in je CA of Key Vault.  
3. **Algoritme‑mismatch** – Als de ondertekenaar SHA‑256 verwacht maar jij SHA‑1 levert, zal verificatie falen. Zorg dat het algoritme consistent is tussen onderteken‑ en verificatiestappen.  
4. **Bestandspad‑problemen** – Relatieve paden werken tijdens ontwikkeling maar breken bij deployment. Geef de voorkeur aan `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` of configuratie‑gedreven absolute paden.  
5. **Platformverschillen** – Windows en Linux behandelen de privésleutel‑opslag anders. Het gebruik van `X509KeyStorageFlags.Exportable` vermindert de meeste cross‑platform problemen.

---

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;

// ------------------------------------------------------------
// Helper class that encapsulates signing logic
// ------------------------------------------------------------
static class MySigner
{
    private static X509Certificate2 _cert;

    public static void Init(X509Certificate2 cert) => _cert = cert;

    public static byte[] Sign(byte[] hash, HashAlgorithmName algorithm)
    {
        using RSA rsa = _cert.GetRSAPrivateKey()
            ?? throw new InvalidOperationException("RSA private key not available.");

        return rsa.SignHash(hash, algorithm, RSASignaturePadding.Pkcs1);
    }
}

// ------------------------------------------------------------
// Main program
// ------------------------------------------------------------
class Program
{
    static X509Certificate2 LoadCertificate(string path, string password)
    {
        try
        {
            var cert = new X509Certificate2(path, password,
                X509KeyStorageFlags.MachineKeySet |
                X509KeyStorageFlags.PersistKeySet |
                X509KeyStorageFlags.Exportable);

            if (!cert.HasPrivateKey)
                throw new InvalidOperationException("Certificate lacks a private key.");

            return cert;
        }
        catch (Exception ex) when (ex is CryptographicException || ex is IOException)
        {
            Console.Error.WriteLine($"Failed to load certificate: {ex.Message}");
            throw;
        }
    }

    static void Main()
    {
        // 1️⃣ Path & password
        string certPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
        string certPassword = "yourPassword";

        // 2️⃣ Load the cert
        X509Certificate2 cert = LoadCertificate(certPath, certPassword);
        MySigner.Init(cert);

        // 3️⃣ Create PKCS7 signer (replace with your library's class)
        var pkcs7Signer = new PKCS7Detached(cert)
        {
            CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
        };

        // 4️⃣ Data to sign
        string dataFile = "sample.txt";
        byte[] data = File.ReadAllBytes(dataFile);

        // 5️⃣ Generate detached signature
        byte[] signature = pkcs7Signer.Sign(data);
        File.WriteAllBytes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}