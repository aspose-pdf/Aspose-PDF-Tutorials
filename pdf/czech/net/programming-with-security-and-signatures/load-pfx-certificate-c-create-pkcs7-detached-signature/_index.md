---
category: general
date: 2026-03-24
description: Rychlé a bezpečné načtení PFX certifikátu v C# pro vytvoření odděleného
  PKCS7 podpisu ze souboru. Krok za krokem průvodce s kompletním kódem a úskalími.
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: cs
og_description: Načíst PFX certifikát v C# a vygenerovat oddělený podpis PKCS7 ze
  souboru. Kompletní příklad s vysvětleními a ošetřením okrajových případů.
og_title: Načíst PFX certifikát C# – Vytvořit oddělený podpis PKCS7
tags:
- C#
- PKCS7
- X509
- Cryptography
title: Načíst PFX certifikát v C# – Vytvořit oddělený podpis PKCS7
url: /cs/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načtení certifikátu PFX v C# – Vytvoření odpojeného podpisu PKCS7

Už jste někdy potřebovali **načíst certifikát PFX v C#** jen pro podepsání nějakých dat, ale nevedeli jste, kde začít? Nejste jediní — mnoho vývojářů narazí na stejnou překážku, když poprvé pracují s certifikáty X.509 a PKCS#7.  

Dobrá zpráva? V tomto tutoriálu získáte připravené řešení, které **načte certifikát PFX v C#**, vytvoří **odpojený podpis PKCS7** a dokonce vám ukáže, jak získat podpis ze souboru. Žádné vágní odkazy, jen konkrétní kód a zdůvodnění každého řádku.

> **Co si z toho odnesete**  
> * Jasné pochopení procesu načítání certifikátu.  
> * Kompletní, kompilovatelný příklad, který vytváří odpojený podpis PKCS7.  
> * Tipy pro řešení běžných problémů (špatné heslo, chybějící soubor, nesoulad algoritmů).  

### Požadavky

- .NET 6.0 nebo novější (používaná API jsou součástí základní knihovny tříd).  
- Platný soubor `.pfx` a jeho heslo.  
- Visual Studio 2022 nebo jakýkoli editor dle libosti — pro základní příklad nejsou vyžadovány žádné speciální NuGet balíčky.

Pokud je máte, pojďme se ponořit.

---

## Načtení certifikátu PFX v C# – Krok za krokem

Níže je minimální sada `using` direktiv, které budete potřebovat. Umístěte je na začátek souboru, aby kompilátor věděl, kde najít typy.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ Zadejte cestu k certifikátu a heslo

Nejprve řekněte runtime, kde se nachází `.pfx` a jaké je jeho heslo. Hard‑codování cest je v ukázce v pořádku, ale **nikdy** nevestavujte hesla do produkčního kódu.

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **Tip:** Uložte heslo v Azure Key Vault, AWS Secrets Manager nebo jako proměnnou prostředí — nikdy jej neukládejte do verzovacího systému.

### 2️⃣ Bezpečné načtení certifikátu

Načítání zabalíme do bloku `try / catch`, abychom odhalili běžné chyby, jako chybějící soubor nebo nesprávné heslo.

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

### 3️⃣ Vytvořte objekt **PKCS7 detached signature**

Předpokládáme, že používáte knihovnu třetí strany, která poskytuje třídu `PKCS7Detached` (mnoho komerčních SDK to dělá), vytvoříme její instanci s certifikátem, který jsme právě načetli.

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

> **Proč callback?** Některá SDK umožňují připojit hardwarové bezpečnostní moduly (HSM) nebo vzdálené služby podepisování. Exponováním `CustomSignHash` udržujete logiku podepisování flexibilní.

### 4️⃣ Implementujte delegáta pro podepisování

Zde je jednoduchá implementace, která používá soukromý klíč načteného certifikátu. V případě potřeby nahraďte `MySigner.Sign` vlastním voláním HSM.

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

### 5️⃣ Podepište libovolná data a získejte odpojený PKCS7 blob

Nyní skutečně něco podepíšeme. Data mohou být soubor, JSON payload nebo cokoli, co potřebujete chránit.

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**Očekávaný výstup**

```
Detached PKCS7 signature created successfully.
```

Nyní máte **PKCS7 podpis ze souboru** (`sample.txt.sig`), který lze ověřit nezávisle na původních datech.

---

## Vytvoření odpojeného podpisu PKCS7 – Pokročilé možnosti

Zatímco základní tok funguje pro většinu scénářů, produkční systémy často potřebují další nastavení:

| Funkce | Jak povolit | Kdy použít |
|--------|-------------|------------|
| **Výběr algoritmu** | Předávejte `HashAlgorithmName.SHA256` (nebo SHA384/SHA512) do `SignHash` | Pokud vaše souladová politika vyžaduje konkrétní hash |
| **Časové razítkování** | Přidejte RFC‑3161 timestamp po podpisu | Pro dlouhodobou validaci |
| **Více podepisujících** | Vytvořte další instance `PKCS7Detached` a sloučte je | Když dokumenty vyžadují společné podepisování |
| **Vlastní CMS atributy** | Použijte metodu `AddAttribute` knihovny před `Sign` | Pro vložení času podpisu, ID podepisujícího atd. |

Níže je rychlý úryvek ukazující výběr SHA‑256:

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

## Ověření odpojeného podpisu PKCS7 (volitelné)

Ověření je druhou polovinou příběhu. Většina knihoven poskytuje metodu `Verify`, která přijímá původní data a odpojený podpis.

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

Pokud používáte jiné SDK, hledejte třídu `CmsSignedData` nebo `SignedCms` v .NET jmenném prostoru `System.Security.Cryptography.Pkcs` — ty také umí pracovat s odpojenými podpisy.

## Běžné úskalí a jak se jim vyhnout

1. **Špatné heslo** – `CryptographicException` bude hlásit *“The specified network password is not correct.”* Ukládejte hesla bezpečně a testujte je samostatně před načtením certifikátu.  
2. **Certifikát bez soukromého klíče** – Některé soubory `.pfx` jsou exportovány bez soukromého klíče. Zkontrolujte nastavení exportu ve vašem CA nebo Key Vault.  
3. **Nesoulad algoritmu** – Pokud podepisující očekává SHA‑256, ale vy použijete SHA‑1, ověření selže. Zarovnejte algoritmus mezi kroky podepisování a ověřování.  
4. **Problémy s cestou k souboru** – Relativní cesty fungují ve vývoji, ale selžou po nasazení. Upřednostněte `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` nebo absolutní cesty řízené konfigurací.  
5. **Rozdíly mezi platformami** – Windows a Linux zacházejí s úložištěm soukromých klíčů odlišně. Použití `X509KeyStorageFlags.Exportable` zmírňuje většinu problémů napříč platformami.

## Kompletní funkční příklad (připravený ke kopírování)

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