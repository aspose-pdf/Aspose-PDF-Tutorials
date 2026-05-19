---
category: general
date: 2026-03-24
description: Gyorsan és biztonságosan töltse be a PFX tanúsítványt C#‑ban, hogy fájlból
  PKCS7 detached aláírást hozzon létre. Lépésről‑lépésre útmutató teljes kóddal és
  buktatókkal.
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: hu
og_description: PFX tanúsítvány betöltése C#-ban és PKCS7 leválasztott aláírás generálása
  fájlból. Teljes példa magyarázatokkal és szélső esetek kezelésével.
og_title: PFX tanúsítvány betöltése C# – PKCS7 leválasztott aláírás létrehozása
tags:
- C#
- PKCS7
- X509
- Cryptography
title: PFX tanúsítvány betöltése C# – PKCS7 leválasztott aláírás létrehozása
url: /hu/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PFX tanúsítvány betöltése C#‑ban – PKCS7 leválasztott aláírás létrehozása

Volt már szükséged **PFX tanúsítvány betöltésére C#‑ban**, csak hogy aláírj néhány adatot, de nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő ütközik ugyanabba a falba, amikor először érintkezik az X.509 tanúsítványokkal és a PKCS#7‑tel.

A jó hír? Ebben az útmutatóban egy azonnal futtatható megoldást kapsz, amely **betölti a PFX tanúsítványt C#‑ban**, létrehozza a **PKCS7 leválasztott aláírást**, és még megmutatja, hogyan nyerheted ki az aláírást egy fájlból. Nincsenek homályos hivatkozások, csak konkrét kód és a sorok mögötti magyarázat.

> **Amit elsajátítasz**  
> * A tanúsítvány betöltési folyamatának tiszta megértése.  
> * Egy teljes, lefordítható példa, amely PKCS7 leválasztott aláírást hoz létre.  
> * Tippek a gyakori buktatók kezeléséhez (helytelen jelszó, hiányzó fájl, algoritmus eltérések).  

### Előkövetelmények

- .NET 6.0 vagy újabb (a használt API-k a báziskönyvtár részei).  
- Érvényes `.pfx` fájl és a hozzá tartozó jelszó.  
- Visual Studio 2022 vagy bármely kedvelt szerkesztő – a fő példához nincs szükség külön NuGet csomagokra.  

Ha ezek megvannak, merüljünk el benne.

---

## PFX tanúsítvány betöltése C#‑ban – Lépésről‑lépésre

Az alábbiakban a minimális `using` direktívákat találod, amelyekre szükséged lesz. Tartsd őket a fájlod tetején, hogy a fordító tudja, hol találja a típusokat.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ A tanúsítvány útvonalának és jelszavának megadása

Először is mondd meg a futtatókörnyezetnek, hol található a `.pfx` és mi a jelszava. Az útvonalak kódba írása rendben van egy demóhoz, de **soha** ne ágyazz jelszavakat a termelési kódba.

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **Pro tipp:** Tárold a jelszót Azure Key Vault‑ban, AWS Secrets Manager‑ben vagy környezeti változóban – soha ne commitold a forráskódba.

### 2️⃣ A tanúsítvány biztonságos betöltése

A betöltést egy `try / catch` blokkba helyezzük, hogy a gyakori hibákat, például a hiányzó fájlt vagy a helytelen jelszót, felszínre hozza.

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

### 3️⃣ **PKCS7 leválasztott aláírás** objektum létrehozása

Feltételezve, hogy egy harmadik fél könyvtárát használod, amely egy `PKCS7Detached` osztályt biztosít (számos kereskedelmi SDK ezt teszi), példányosítjuk azt a most betöltött tanúsítvánnyal.

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

> **Miért callback?** Néhány SDK lehetővé teszi hardveres biztonsági modulok (HSM-ek) vagy távoli aláíró szolgáltatások csatlakoztatását. A `CustomSignHash` kitettségével az aláírási logikát rugalmasan tarthatod.

### 4️⃣ A aláíró delegált megvalósítása

Itt egy egyszerű megvalósítás, amely a betöltött tanúsítvány privát kulcsát használja. Ha szükséges, cseréld le a `MySigner.Sign`-t a saját HSM hívásodra.

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

### 5️⃣ Tetszőleges adat aláírása és a leválasztott PKCS7 blob lekérése

Most ténylegesen aláírunk valamit. Az adat lehet egy fájl, egy JSON payload, vagy bármi, amit védeni szeretnél.

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**Várt kimenet**

```
Detached PKCS7 signature created successfully.
```

Most már rendelkezel egy **PKCS7 aláírással fájlból** (`sample.txt.sig`), amely az eredeti adat függetlenül ellenőrizhető.

---

## PKCS7 leválasztott aláírás létrehozása – Haladó beállítások

Miközben az alapfolyamat a legtöbb esetben működik, a termelési rendszerek gyakran igényelnek további beállításokat:

| Jellemző | Hogyan engedélyezhető | Mikor használjuk |
|----------|-----------------------|------------------|
| **Algoritmus kiválasztása** | Adja át a `HashAlgorithmName.SHA256`‑t (vagy SHA384/SHA512) a `SignHash`‑nek | Ha a megfelelőségi szabályzat egy adott hash‑t ír elő |
| **Időbélyegzés** | A aláírás után fűzzön hozzá egy RFC‑3161 időbélyeget | Hosszú távú ellenőrzéshez |
| **Több aláíró** | Hozzon létre további `PKCS7Detached` példányokat és egyesítse őket | Amikor a dokumentumok közös aláírást igényelnek |
| **Egyedi CMS attribútumok** | Használja a könyvtár `AddAttribute` metódusát a `Sign` előtt | Aláírási idő, aláíró azonosító stb. beágyazásához |

Az alábbi gyors kódrészlet a SHA‑256 kiválasztását mutatja:

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

---

## PKCS7 leválasztott aláírás ellenőrzése (opcionális)

Az ellenőrzés a történet másik fele. A legtöbb könyvtár egy `Verify` metódust biztosít, amely az eredeti adatot és a leválasztott aláírást veszi át.

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

Ha más SDK-t használsz, keresd a `CmsSignedData` vagy `SignedCms` osztályt a .NET `System.Security.Cryptography.Pkcs` névtérben – ezek is képesek a leválasztott aláírások kezelésére.

---

## Gyakori buktatók és hogyan kerüld el őket

1. **Helytelen jelszó** – A `CryptographicException` azt fogja mondani, hogy *„The specified network password is not correct.”* (azaz „A megadott hálózati jelszó nem helyes.”). Tárold a jelszavakat biztonságosan, és teszteld őket külön a tanúsítvány betöltése előtt.  
2. **Privát kulcs nélküli tanúsítvány** – Néhány `.pfx` fájlt a privát kulcs nélkül exportálnak. Ellenőrizd a CA vagy a Key Vault export beállításait.  
3. **Algoritmus eltérés** – Ha az aláíró SHA‑256‑ot vár, de SHA‑1‑et adsz meg, az ellenőrzés hibát fog eredményezni. Igazítsd az algoritmust az aláírási és ellenőrzési lépésekben.  
4. **Fájl útvonal problémák** – Relatív útvonalak fejlesztéskor működnek, de telepítéskor hibát okozhatnak. Inkább használd a `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` vagy konfiguráció‑alapú abszolút útvonalakat.  
5. **Platform különbségek** – A Windows és a Linux eltérően kezeli a privát kulcs tárolót. Az `X509KeyStorageFlags.Exportable` használata a legtöbb cross‑platform problémát enyhíti.

---

## Teljes működő példa (másolás‑beillesztés kész)

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