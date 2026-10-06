---
category: general
date: 2026-03-29
description: Comment signer un PDF avec une signature numérique et ajouter une image
  recadrée en C#. Apprenez à ajouter une signature numérique à un PDF, recadrer une
  image pour le PDF et ajouter une image au PDF facilement.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: fr
og_description: Comment signer un PDF avec une signature numérique et intégrer une
  image recadrée en utilisant Aspose.Pdf en C#. Suivez ce guide pour une solution
  complète.
og_title: Comment signer un PDF et ajouter des images – Tutoriel C# étape par étape
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Comment signer un PDF et ajouter des images – Guide complet en C#
url: /fr/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment signer un PDF et ajouter des images – Guide complet C#

Vous vous êtes déjà demandé **comment signer un PDF** de façon programmatique tout en insérant une image personnalisée ? Peut-être que vous construisez un flux d'approbation et avez besoin d'une signature juridiquement contraignante *et* d'une vignette de la photo du signataire sur la même page. En bref, vous voulez **ajouter une signature numérique pdf** du contenu, recadrer cette image, puis **ajouter une image au pdf** sans effort.  

Ce tutoriel vous guide à travers chaque étape — du chargement d’un certificat ECDSA PKCS#7 au recadrage d’un JPEG et à son apposition sur la page signée. À la fin, vous disposerez d’un seul fichier C# exécutable qui signe la page 1, recadre une photo à 400 × 400 px et la place à un emplacement précis. Aucun script externe, aucune magie, juste du code clair et des explications.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+)
- **Aspose.Pdf for .NET** package NuGet (version 23.9 ou plus récente)
- Un certificat ECDSA P‑256 au format PKCS#7 (`.pfx`) et son mot de passe
- Une image JPEG que vous souhaitez intégrer (par ex. `photo.jpg`)

> **Astuce :** Gardez votre fichier de certificat hors du contrôle de version et protégez le mot de passe avec un gestionnaire de secrets.

---

## Étape 1 : Configurer le projet et les importations

Tout d’abord, créez une application console (ou intégrez cela dans un service existant). Ajoutez la référence Aspose.Pdf :

```bash
dotnet add package Aspose.Pdf
```

Puis incluez les espaces de noms requis :

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Ces instructions `using` vous donnent accès aux classes `Document`, `Signature` et `Rectangle` dont nous aurons besoin plus tard.

## Étape 2 : Charger le PDF et préparer la signature

Nous ouvrirons un PDF existant (`source.pdf`) et créerons un objet **digital signature pdf** qui utilise une signature PKCS#7 détachée. Le certificat est une clé ECDSA P‑256, largement acceptée pour la conformité.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Pourquoi c’est important :** Utiliser une signature PKCS#7 détachée conserve le contenu original du PDF intact tout en y intégrant un hachage cryptographique. C’est l’approche standard de l’industrie pour les PDF juridiquement contraignants.

## Étape 3 : Appliquer la signature numérique à une page spécifique

Nous placerons maintenant le champ de signature visible sur **page 1**. Le rectangle définit où apparaît la boîte de signature (les coordonnées sont en points, où 1 inch = 72 points).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Si vous n’avez pas besoin d’une boîte visible, définissez `isVisible` sur `false`. Le `signatureRect` peut être ajusté pour correspondre à la mise en page de votre document.

## Étape 4 : Ouvrir le flux d'image et définir les zones de recadrage

Nous lirons le fichier JPEG dans un flux et spécifierons un **source rectangle** qui sélectionne les 400 × 400 pixels en haut à gauche. Il s’agit de l’opération **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Cas limite :** Si votre image est plus petite que 400 × 400, le recadrage sera automatiquement limité aux dimensions réelles de l’image — aucune exception n’est levée.

## Étape 5 : Définir l'emplacement de l'image recadrée

Ensuite, définissez le **destination rectangle** sur la page PDF. Dans cet exemple, nous plaçons l’image à (50, 50) avec une taille de 200 × 200 points (≈ 2,78 pouces carrés).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

N’hésitez pas à expérimenter : modifiez les coordonnées X/Y pour déplacer l’image, ou ajustez la largeur/hauteur pour la mise à l’échelle.

## Étape 6 : Insérer l'image recadrée sur la page signée

Enfin, nous ajoutons l’image à **page 1** (la même page qui porte maintenant la signature). La surcharge `AddImage` que nous utilisons accepte les rectangles source et destination, effectuant ainsi le recadrage et le placement en un seul appel.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

En coulisses, Aspose.Pdf extrait la région de 400 × 400 pixels, la redimensionne à 200 × 200 points et l’écrit dans le flux de contenu du PDF.

## Étape 7 : Enregistrer le PDF signé et enrichi d'image

Après toutes les modifications, persistez le document. Vous pouvez écraser le fichier original ou écrire dans un nouveau fichier.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

Lorsque vous ouvrez `output_signed.pdf` dans Adobe Acrobat ou tout autre lecteur PDF, vous verrez :

- Un champ de signature visible aux coordonnées que vous avez spécifiées.
- La photo recadrée placée à (50, 50) sur la page 1.
- La signature numérique validée (à condition que le lecteur fasse confiance à votre certificat).

---

## Questions fréquentes (FAQ)

| Question | Réponse |
|----------|---------|
| **Puis‑je signer une autre page ?** | Changez l’argument `pageNumber` dans `signature.Sign` pour n’importe quel indice de page valide (commençant à 1). |
| **Et si j’ai besoin de plusieurs signatures ?** | Créez une nouvelle instance `Signature` pour chaque page ou emplacement, en réutilisant le même `pkcsSignature` si le même certificat s’applique. |
| **Le recadrage d’image est‑il limité aux rectangles ?** | Oui, `AddImage` d’Aspose.Pdf fonctionne avec des régions rectangulaires. Pour des formes complexes, vous devrez pré‑traiter l’image (par ex. avec System.Drawing) avant l’insertion. |
| **Comment rendre la signature invisible ?** | Définissez `isVisible` sur `false` et omettez le `signatureRect`. La signature restera cryptographiquement valide. |
| **Quels formats puis‑je intégrer en plus du JPEG ?** | PNG, BMP, GIF et TIFF sont tous pris en charge. Il suffit de changer le chemin du fichier et de s’assurer que le flux lit les bons octets. |

## Exemple complet fonctionnel

Voici le programme complet, autonome. Copiez‑collez‑le dans `Program.cs`, ajustez les chemins, puis exécutez.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Résultat attendu :** L’ouverture de `output_signed.pdf` montre un champ de signature (100 × 100 → 300 × 300 points) et une image de 200 × 200 points dérivée du coin supérieur gauche de `photo.jpg`. La signature est validée avec le certificat ECDSA fourni.

## Conclusion

Nous avons couvert **comment signer un PDF**, comment **ajouter une signature numérique pdf** à une page spécifique, comment **recadrer une image pour pdf**, et enfin comment **ajouter une image au pdf** en utilisant Aspose.Pdf en C#. L’ensemble du flux — du chargement du certificat à l’enregistrement du document final — tient dans un seul fichier source lisible.

Si vous êtes prêt pour le prochain défi, envisagez :

- D’ajouter **plusieurs signatures** sur différentes pages (utilisez le concept de « digital signature pdf page »).
- D’intégrer des **codes QR** qui renvoient à des services de vérification.
- D’automatiser le processus dans une API ASP.NET Core pour une génération de PDF à la volée.

Rappelez‑vous, la clé d’une automatisation PDF robuste est une séparation claire des responsabilités : gestion des signatures, traitement des images et assemblage final du document. Jouez avec les coordonnées, changez le format de l’image, ou expérimentez la datation — votre flux de travail est désormais pleinement extensible.

Des questions, des scénarios limites, ou un cas d’usage intéressant à partager ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}