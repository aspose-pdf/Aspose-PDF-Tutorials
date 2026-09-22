---
category: general
date: 2026-02-09
description: Vérifiez la signature PDF avec Aspose.PDF en C#. Apprenez comment ajouter
  un rectangle au PDF, enregistrer le PDF mis à jour et utiliser les fonctionnalités
  de signature d'Aspose PDF.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: fr
og_description: Vérifiez rapidement la signature PDF en C#. Ce guide montre comment
  ajouter des graphiques PDF, enregistrer le PDF mis à jour et utiliser les API de
  signature PDF d’Aspose.
og_title: Vérifier la signature PDF et ajouter un rectangle PDF – Guide complet Aspose
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: Vérifier la signature PDF et ajouter un rectangle PDF avec Aspose
url: /fr/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# vérifier la signature PDF et ajouter un rectangle PDF avec Aspose

Vous avez déjà eu besoin de **vérifier la signature PDF** dans un projet C# mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul—les signatures numériques sont indispensables pour la conformité, pourtant de nombreux développeurs rencontrent des difficultés lorsqu'ils doivent également modifier le document par la suite.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui **vérifie la signature PDF**, ajoute un **rectangle** à la première page, vérifie que la forme reste à l'intérieur des limites de la page, et enfin **enregistre le PDF mis à jour**—le tout en utilisant l'API moderne Aspose.PDF. À la fin, vous disposerez d'un programme autonome que vous pourrez intégrer à n'importe quelle solution .NET.

## Ce que vous allez apprendre

- Charger un PDF signé avec Aspose.PDF.
- Utiliser les classes **aspose pdf signature** pour vérifier chaque signature et détecter les compromissions.
- Ajouter des graphiques **add rectangle pdf** en toute sécurité, en veillant à ce qu'ils s'adaptent à la page.
- **Save updated pdf** tout en préservant les signatures existantes.
- Astuces, gestion des cas limites et pièges courants.

Aucun document externe n'est requis—tout ce dont vous avez besoin se trouve ici.

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7+).
- Le package NuGet Aspose.PDF for .NET (≥ 23.10). Installez-le avec :

```bash
dotnet add package Aspose.Pdf
```

- Un fichier PDF signé nommé `signed.pdf` placé dans un répertoire que vous contrôlez (remplacez `YOUR_DIRECTORY` dans le code).
- Une connaissance de base de C# et de Visual Studio ou VS Code.

> **Conseil pro :** Si vous n'avez pas de PDF signé sous la main, Aspose propose un fichier de démonstration gratuit sur son site que vous pouvez télécharger pour les tests.

---

## vérifier la signature PDF – Étape par étape

La première chose à faire est d'ouvrir le document et de parcourir chaque signature numérique. Aspose.PDF nous fournit deux méthodes pratiques : `VerifySignature` indique si la vérification cryptographique réussit, tandis que la méthode plus récente `IsSignatureCompromised` signale toute falsification pouvant être survenue après la signature.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Pourquoi c'est important :**  
- `VerifySignature` seul ne confirme que le certificat du signataire est toujours de confiance.  
- `IsSignatureCompromised` détecte les changements subtils—comme l'ajout d'un objet caché—vous permettant de savoir si le contenu visuel du PDF a été modifié après la signature.

**Sortie attendue** (exemple avec deux signatures) :

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

Si une signature indique `compromised=True`, vous devez interrompre le traitement ultérieur ou alerter l'utilisateur, car l'intégrité du document ne peut pas être garantie.

---

## ajouter un rectangle PDF à une page

Maintenant que nous avons confirmé que les signatures sont intactes (ou du moins conscients de toute compromission), ajoutons un simple graphique rectangle. Cela est utile pour apposer des marques « Reviewed », mettre en évidence des sections, ou simplement attirer l'attention sur une zone.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**Ce que signifient les nombres :**  
- Le système de coordonnées du PDF commence au coin inférieur gauche.  
- Dans l'exemple, le rectangle s'étend sur 100 points horizontalement et 100 points verticalement, placé approximativement au centre d'une page A4 typique.

> **Note :** Aspose prend également en charge `AddEllipse`, `AddPolygon`, etc., si vous avez besoin de formes plus complexes.

---

## vérifier les limites graphiques – s'assurer que le rectangle tient

Avant d'appliquer les modifications, il est judicieux de vérifier que nos graphiques restent à l'intérieur de la zone imprimable de la page. La nouvelle méthode `CheckGraphicsBounds` fait exactement cela.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

Si `shapeFits` renvoie `false`, vous devrez ajuster les coordonnées du rectangle—peut-être le réduire ou le déplacer plus bas sur la page. Cela évite les découpes accidentelles qui peuvent paraître non professionnelles, surtout lorsque le PDF est imprimé ultérieurement.

---

## enregistrer le PDF mis à jour – préserver les signatures et les nouveaux graphiques

Enfin, nous écrivons le document modifié sur le disque. La méthode `Save` respecte les signatures existantes ; elle ne les invalide pas à moins que le contenu n'ait réellement changé (ce que nous avons déjà vérifié avec `IsSignatureCompromised`).

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Pourquoi utiliser un nouveau fichier ?**  
Écraser l'original pourrait supprimer les signatures d'origine, rendant impossible la comparaison avant/après. En écrivant dans `output.pdf`, vous conservez la source à des fins d'audit.

---

## Exemple complet, exécutable

Voici le programme complet que vous pouvez copier‑coller dans une application console. Toutes les étapes sont combinées, les commentaires expliquent chaque bloc, et vous verrez la sortie console attendue à la fin.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Sortie console attendue** (en supposant une signature valide et non compromise) :

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

Si une signature est compromise, vous verrez `compromised=True` et pourrez décider de continuer ou non.

---

## Questions fréquentes & gestion des cas limites

| Question | Réponse |
|----------|--------|
| **Que se passe-t-il si le PDF n'a aucune signature ?** | `GetSignNames()` renvoie une collection vide ; la boucle saute simplement, et vous pouvez toujours ajouter des graphiques. |
| **Puis-je ajouter plusieurs rectangles ?** | Oui—appelez simplement `AddRectangle` à plusieurs reprises avec différents objets `Rectangle`. |
| **Que faire avec les PDF protégés par mot de passe ?** | Chargez-les avec `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` avant la vérification. |
| **L'ajout de graphiques invalidera-t-il une signature valide ?** | Seulement si la signature couvre la page où vous insérez les graphiques. Utilisez `IsSignatureCompromised` pour détecter cela ; sinon la signature reste intacte. |
| **Dois-je fermer les ressources ?** | Les objets Aspose.PDF sont gérés ; la libération est optionnelle mais vous pouvez envelopper le code dans un bloc `using` pour plus de sécurité. |

---

## Conseils pro pour la production

- **Traitement par lots :** Enveloppez toute la routine dans une méthode qui accepte les chemins d'entrée/sortie ; puis alimentez une liste de fichiers à un `Parallel.ForEach` pour gagner en vitesse.
- **Journalisation :** Remplacez `Console.WriteLine` par un logger approprié (par ex., Serilog) afin de capturer les résultats de vérification dans les traces d’audit.
- **Politique de signature :** Combinez `VerifySignature` avec une vérification de révocation de certificat (OCSP/CRL) pour une conformité plus stricte.
- **Style des graphiques :** Utilisez `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });` pour faire ressortir le rectangle.
- **Verrouillage de version :** Fixez la version du package NuGet Aspose.PDF afin d'éviter les changements incompatibles lors des mises à jour de la bibliothèque.

---

## Conclusion

Vous disposez maintenant d'un exemple complet, de bout en bout, qui **vérifie la signature PDF**, **ajoute un rectangle PDF**, et **enregistre le PDF mis à jour** en utilisant les dernières API Aspose.PDF. Le code vérifie les signatures compromises, s'assure que les graphiques restent dans les limites de la page, et préserve les signatures numériques d'origine—exactement ce qu'exige un flux de travail de conformité réel.

Ensuite, vous pourriez explorer :

- Ajouter des **add graphics pdf** comme des filigranes ou des codes QR.
- Utiliser l'API **aspose pdf signature** pour créer de nouvelles signatures programmatiquement.
- Automatiser le processus dans un service web ASP.NET Core pour la validation de documents à la volée.

Essayez-le, modifiez les coordonnées du rectangle, et observez comment la bibliothèque réagit à différentes structures PDF. Bon codage, et que vos PDFs restent à la fois signés et élégants ! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}