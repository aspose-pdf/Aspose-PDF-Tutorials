---
category: general
date: 2026-08-14
description: Créer des options de signature en C# pour appliquer une signature numérique.
  Apprenez comment configurer la signature, implémenter une fonction de hachage personnalisée
  et signer des documents de façon programmatique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: fr
lastmod: 2026-08-14
og_description: Créez des options de signature en C# et appliquez une signature numérique.
  Ce tutoriel vous guide à travers la configuration de la signature, l’ajout d’une
  fonction de hachage personnalisée et la signature d’un document.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Créer des options de signature en C# – guide de signature numérique étape
  par étape
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
title: Créer des options de signature en C# – guide complet de la signature numérique
url: /fr/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer des options de signature en C# – guide complet de la signature numérique

Créer des options de signature en C# pour configurer un flux de travail de signature numérique. Ce tutoriel montre comment appliquer une signature numérique, implémenter une fonction de hachage personnalisée et signer un document en utilisant la classe `SignatureOptions`. Si vous avez déjà eu besoin de signer un PDF, un XML ou toute charge binaire depuis une application .NET, les étapes ci‑dessous vous offrent une solution prête à l’emploi.

Vous apprendrez à :

* configurer `SignatureOptions` avec un algorithme de hachage personnalisé,
* appeler correctement la méthode de signature,
* vérifier que la signature a été appliquée,
* éviter les pièges courants lors de la configuration de la signature.

Les seules prérequis sont un SDK .NET récent (≥ .NET 6) et une bibliothèque de signature qui expose `SignatureOptions` (par exemple, **GroupDocs.Signature**, **Aspose.Signature**, ou une API similaire). Aucun outil externe n’est requis.

---

## Prérequis

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| .NET 6 SDK ou version ultérieure | Fournit les fonctionnalités modernes du langage utilisées dans les exemples. |
| Un package NuGet de bibliothèque de signature (p. ex., `GroupDocs.Signature`) | Fournit le type `SignatureOptions` et la méthode d’extension `Sign`. |
| Accès à une clé privée ou à un certificat | Nécessaire pour générer une signature numérique vérifiable. |

Installez la bibliothèque avec la CLI standard :

```bash
dotnet add package GroupDocs.Signature
```

---

## Étape 1 : Créer des options de signature

La première étape consiste à instancier `SignatureOptions` et à définir les propriétés qui contrôlent le processus de signature. Cet objet indique à la bibliothèque *quoi* signer et *comment* le signer.

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

**Pourquoi c’est important :** `SignatureOptions` agit comme un contrat entre votre code et le moteur de signature. En le configurant dès le départ, vous évitez de répéter du code boilerplate lors de la signature de plusieurs documents.

---

## Étape 2 : Implémenter une fonction de hachage personnalisée

Une *fonction de hachage personnalisée* vous donne un contrôle total sur le condensat que l’algorithme de signature signe. Cela est utile lorsque le hachage par défaut (SHA‑256) ne répond pas aux exigences de conformité ou lorsque vous devez hacher une sous‑partie du document.

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

**Pourquoi c’est important :** En assignant `CustomSignHash`, vous remplacez l’étape de hachage interne de la bibliothèque par `MyHash`. Le moteur de signature signera désormais les octets retournés par votre fonction, garantissant la conformité à toute politique personnalisée.

---

## Étape 3 : Charger le document et appliquer la signature numérique

Avec les options prêtes, vous pouvez maintenant ouvrir le fichier cible et appeler la méthode de signature. La méthode `Sign` est fournie par la bibliothèque et utilise les `SignatureOptions` configurées.

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

**Pourquoi c’est important :** L’appel à `Sign` effectue trois actions en interne :

1. **Calcul du hachage** – désormais délégué à votre fonction de hachage personnalisée.  
2. **Génération de la signature** – en utilisant la clé privée fournie à la configuration de la bibliothèque.  
3. **Intégration** – la signature générée est attachée au fichier de sortie.

Si une étape échoue, la méthode renvoie `false`, vous permettant de gérer l’erreur de manière élégante.

---

## Étape 4 : Vérifier que le document est signé

Une vérification rapide confirme que la signature a été correctement appliquée. La plupart des bibliothèques exposent une méthode `Verify` qui contrôle l’intégrité du fichier signé.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Pourquoi c’est important :** La vérification garantit que le document signé n’a pas été altéré après la signature et que le hachage personnalisé a produit un condensat compatible.

---

## Comment configurer la signature pour différents types de fichiers

Le même objet `SignatureOptions` peut être réutilisé pour les PDF, les documents Word, les images ou les binaires simples. Le seul changement requis est la classe d’options spécifique (p. ex., `PdfSignatureOptions`, `WordSignatureOptions`). Voici un exemple rapide pour une image JPEG :

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

**Pourquoi c’est important :** Comprendre comment *configurer la signature* pour chaque format vous permet d’étendre la même base de code à plusieurs types de documents sans réécrire la logique de hachage.

---

## Pièges courants et bonnes pratiques

| Piège | Solution recommandée |
|-------|----------------------|
| Oublier de définir `CustomSignHash` après la création de `SignatureOptions` | Assignez le délégué immédiatement après la construction de l’objet d’options. |
| Utiliser un algorithme de hachage que le certificat de signature ne supporte pas | Vérifiez que l’usage de la clé du certificat correspond à la longueur du hachage (p. ex., RSA‑2048 avec SHA‑512). |
| Négliger la nécessité de libérer les objets `Signature` | Encapsulez l’instance `Signature` dans un bloc `using` pour libérer les poignées de fichiers. |
| Sauvegarder le fichier signé en écrasant la source originale | Écrivez toujours vers un nouveau chemin de fichier (`outputPath`) pour préserver le document d’origine. |

---

## Exemple complet fonctionnel

Voici un programme autonome qui assemble toutes les pièces. Copiez‑le dans un nouveau projet console et exécutez‑le ; la console indiquera le succès ou l’échec.

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

**Sortie attendue**

```
Signature verified successfully.
```

Si la console affiche « Signing failed. » ou « Signature verification failed. », revérifiez la configuration du certificat et assurez‑vous que le hachage personnalisé renvoie un tableau d’octets de la taille attendue.

---

## Conclusion

Vous savez maintenant comment **créer des options de signature** en C#, attacher une **fonction de hachage personnalisée**, et **appliquer une signature numérique** à tout document pris en charge. Le tutoriel a couvert le cycle complet : configuration des options, signature du fichier, et vérification du résultat. En réutilisant la même instance `SignatureOptions`, vous pouvez également **configurer la signature** pour des images, des fichiers Word ou des binaires bruts.

---

## Prochaines étapes

* Explorer les propriétés supplémentaires de `SignatureOptions` telles que les tampons visuels, les serveurs d’horodatage et les chaînes de certificats – elles correspondent au mot‑clé **apply digital signature**.  
* Expérimenter d’autres algorithmes de hachage (par ex., Blake2b) en remplaçant l’implémentation dans `MyHash`.  
* Intégrer le flux de signature dans une API web pour permettre la signature de documents à la volée – une extension naturelle de **how to sign document** dans une architecture orientée services.

N’hésitez pas à adapter le code à vos propres politiques de sécurité, et partagez votre expérience dans les commentaires. Bonne signature !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment changer la langue de la signature PDF avec Aspose.PDF pour .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Tutoriel de signature numérique Aspose Pdf Net](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Tutoriel de signature numérique Aspose Pdf Net](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}