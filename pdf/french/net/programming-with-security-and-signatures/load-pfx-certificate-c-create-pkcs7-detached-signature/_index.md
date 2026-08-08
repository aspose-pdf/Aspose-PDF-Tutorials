---
category: general
date: 2026-03-24
description: Chargez rapidement et en toute sécurité le certificat PFX en C# pour
  créer une signature détachée PKCS7 à partir d’un fichier. Guide pas à pas avec le
  code complet et les pièges.
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: fr
og_description: Charger un certificat PFX en C# et générer une signature détachée
  PKCS7 à partir d’un fichier. Exemple complet avec explications et gestion des cas
  limites.
og_title: Charger le certificat PFX C# – Créer une signature PKCS7 détachée
tags:
- C#
- PKCS7
- X509
- Cryptography
title: Charger le certificat PFX C# – Créer une signature détachée PKCS7
url: /fr/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Charger un certificat PFX C# – Créer une signature détachée PKCS7

Vous avez déjà eu besoin de **charger un certificat PFX en C#** simplement pour signer des données, mais vous ne saviez pas par où commencer ? Vous n'êtes pas le seul—de nombreux développeurs rencontrent le même obstacle lorsqu'ils manipulent pour la première fois des certificats X.509 et PKCS#7.  

Bonne nouvelle ? Dans ce tutoriel, vous obtiendrez une solution prête à l'emploi qui **charge un certificat PFX C#**, crée une **signature détachée PKCS7**, et vous montre même comment extraire la signature d'un fichier. Pas de références vagues, seulement du code concret et le raisonnement derrière chaque ligne.

> **Ce que vous en retirerez**  
> * Une compréhension claire du processus de chargement du certificat.  
> * Un exemple complet et compilable qui génère une signature détachée PKCS7.  
> * Des conseils pour gérer les problèmes courants (mot de passe incorrect, fichier manquant, incompatibilités d'algorithmes).  

### Prérequis

- .NET 6.0 ou version ultérieure (les API utilisées font partie de la bibliothèque de classes de base).  
- Un fichier `.pfx` valide et son mot de passe.  
- Visual Studio 2022 ou tout éditeur de votre choix—aucun package NuGet spécial requis pour l'exemple de base.  

Si vous avez tout cela, plongeons‑nous dedans.

---

## Charger un certificat PFX C# – Étape par étape

Voici l'ensemble minimal de directives `using` dont vous aurez besoin. Conservez‑les en haut de votre fichier afin que le compilateur sache où trouver les types.

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ Spécifier le chemin du certificat et le mot de passe

Tout d'abord, indiquez à l'exécution où se trouve le `.pfx` et quel est son mot de passe. Codifier les chemins en dur est acceptable pour une démonstration, mais **jamais** n'intégrez les mots de passe dans le code de production.

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **Astuce pro :** Stockez le mot de passe dans Azure Key Vault, AWS Secrets Manager ou une variable d'environnement—ne le validez jamais dans le contrôle de source.

### 2️⃣ Charger le certificat en toute sécurité

Nous encapsulons le chargement dans un bloc `try / catch` afin de faire remonter les erreurs courantes comme un fichier manquant ou un mot de passe incorrect.

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

### 3️⃣ Créer un objet de **signature détachée PKCS7**

En supposant que vous utilisez une bibliothèque tierce qui expose une classe `PKCS7Detached` (de nombreux SDK commerciaux le font), nous l'instancions avec le certificat que nous venons de charger.

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

> **Pourquoi un rappel ?** Certains SDK vous permettent d'intégrer des modules de sécurité matérielle (HSM) ou des services de signature à distance. En exposant `CustomSignHash`, vous gardez la logique de signature flexible.

### 4️⃣ Implémenter le délégué de signature

Voici une implémentation simple qui utilise la clé privée du certificat chargé. Remplacez `MySigner.Sign` par votre propre appel HSM si nécessaire.

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

### 5️⃣ Signer des données arbitraires et récupérer le blob PKCS7 détaché

Nous signons maintenant réellement quelque chose. Les données peuvent être un fichier, une charge JSON, ou tout ce que vous devez protéger.

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**Sortie attendue**

```
Detached PKCS7 signature created successfully.
```

Vous avez maintenant une **signature PKCS7 depuis un fichier** (`sample.txt.sig`) qui peut être vérifiée indépendamment des données originales.

---

## Créer une signature détachée PKCS7 – Options avancées

Bien que le flux de base fonctionne pour la plupart des scénarios, les systèmes de production ont souvent besoin de réglages supplémentaires :

| Fonctionnalité | Comment activer | Quand l’utiliser |
|----------------|-----------------|-------------------|
| **Sélection d'algorithme** | Passer `HashAlgorithmName.SHA256` (ou SHA384/SHA512) à `SignHash` | Si votre régime de conformité impose un hash spécifique |
| **Horodatage** | Ajouter un horodatage RFC‑3161 après la signature | Pour une validation à long terme |
| **Signataires multiples** | Créer des instances supplémentaires de `PKCS7Detached` et les fusionner | Lorsque les documents nécessitent une co‑signature |
| **Attributs CMS personnalisés** | Utiliser la méthode `AddAttribute` de la bibliothèque avant `Sign` | Pour intégrer l'heure de signature, l'ID du signataire, etc. |

Voici un extrait rapide montrant la sélection SHA‑256 :

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

---

## Vérifier la signature détachée PKCS7 (Optionnel)

La vérification est l'autre moitié de l'histoire. La plupart des bibliothèques exposent une méthode `Verify` qui prend les données originales et la signature détachée.

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

Si vous utilisez un SDK différent, cherchez une classe `CmsSignedData` ou `SignedCms` dans l'espace de noms .NET `System.Security.Cryptography.Pkcs` — elles peuvent également gérer les signatures détachées.

---

## Pièges courants & comment les éviter

1. **Mot de passe incorrect** – L'`CryptographicException` indiquera *« The specified network password is not correct. »* Stockez les mots de passe de façon sécurisée et testez‑les indépendamment avant de charger le certificat.  
2. **Certificat sans clé privée** – Certains fichiers `.pfx` sont exportés sans la clé privée. Vérifiez les paramètres d'exportation dans votre CA ou Key Vault.  
3. **Incompatibilité d'algorithme** – Si le signataire attend SHA‑256 mais que vous fournissez SHA‑1, la vérification échouera. Alignez l'algorithme entre les étapes de signature et de vérification.  
4. **Problèmes de chemin de fichier** – Les chemins relatifs fonctionnent en développement mais échouent en production. Privilégiez `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` ou des chemins absolus définis par la configuration.  
5. **Différences de plateforme** – Windows et Linux gèrent le magasin de clés privées différemment. Utiliser `X509KeyStorageFlags.Exportable` atténue la plupart des maux de tête multiplateformes.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

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