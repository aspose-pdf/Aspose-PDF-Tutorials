---
category: general
date: 2026-01-15
description: Ajoutez rapidement des numéros Bates à votre PDF avec Aspose.Pdf. Apprenez
  comment ajouter un pied de page au PDF, ajouter des numéros de page au PDF et créer
  une numérotation de pages personnalisée.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: fr
og_description: Ajoutez rapidement des numéros Bates à votre PDF avec Aspose.Pdf.
  Apprenez comment ajouter un pied de page au PDF, ajouter des numéros de page au
  PDF et ajouter une numérotation de page personnalisée.
og_title: Ajouter des numéros Bates au PDF – numérotation Bates PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Ajouter des numéros Bates au PDF – numérotation Bates PDF
url: /fr/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter des numéros Bates à un PDF – Guide complet

Vous avez déjà eu besoin d'**add bates numbers** à un PDF mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul — les équipes juridiques, les auditeurs et toute personne manipulant d'énormes ensembles de documents rencontrent ce problème quotidiennement. La bonne nouvelle ? Avec Aspose.Pdf for .NET, vous pouvez parsemer ces numéros sur chaque page en quelques lignes seulement.

Dans ce tutoriel, nous parcourrons l'ensemble du processus : depuis l'importation de la bibliothèque Aspose.Pdf, le chargement de votre fichier source, la configuration d'un *BatesNumberingArtifact*, son attachement en tant que pied de page, et enfin l'enregistrement du résultat. À la fin, vous saurez également comment **add footer to pdf**, **add page numbers pdf**, et même **add custom page numbering** pour ces cas limites difficiles.

## Ce dont vous avez besoin

- .NET 6+ (ou .NET Framework 4.8 si vous êtes encore sur la pile classique)  
- Une référence au package NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- Un fichier PDF que vous souhaitez tamponner (nous l'appellerons `source.pdf`)  

C’est tout — aucun outil supplémentaire, aucun éditeur PDF lourd. Plongeons‑y.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Étape 1 : Ajouter des numéros Bates – Charger le document PDF

Tout d'abord, nous avons besoin d'un objet `Document` qui représente le PDF que nous allons modifier. Considérez cela comme l'ouverture d'un document Word avant de commencer à taper.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Pourquoi c'est important :** Le chargement du fichier vous donne accès à sa collection `Pages`, où nous attacherons plus tard l'artifact de numérotation Bates. Si le fichier est introuvable, Aspose lèvera une `FileNotFoundException` claire, alors vérifiez à nouveau le chemin.

## Étape 2 : Configurer les paramètres de bates numbering pdf

Nous définissons maintenant *comment* les numéros doivent apparaître. Le `BatesNumberingArtifact` vous permet de définir un préfixe, le numéro de départ, le remplissage de chiffres, le suffixe et le placement. C'est le cœur de **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Astuce pro :** Si vous avez besoin que les numéros apparaissent dans l'en‑tête à la place, remplacez `BottomCenter` par `TopCenter`. L'énumération de placement prend également en charge `BottomLeft`, `BottomRight`, etc., vous offrant une flexibilité pour différents styles **add footer to pdf**.

## Étape 3 : Ajouter des numéros de page pdf – Attacher l'Artifact à chaque page

Avec l'artifact prêt, nous parcourons chaque page et l'ajoutons à la collection `Artifacts`. C'est l'étape qui **adds page numbers pdf** réellement.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Que se passe-t-il en coulisses ?** La collection `Artifacts` est rendue après le contenu principal de la page, garantissant que le numéro Bates se situe au-dessus de tout texte existant mais en dessous des annotations. Si vous avez besoin que le numéro soit derrière le contenu (rare), vous utiliseriez `page.Artifacts.Insert(0, batesArtifact)`.

## Étape 4 : Ajouter une numérotation de page personnalisée – Enregistrer le PDF mis à jour

Enfin, nous écrivons le document modifié sur le disque. Le fichier de sortie contiendra les numéros Bates comme une partie permanente de chaque page.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Conseil de vérification :** Ouvrez `bates_out.pdf` dans n'importe quel visualiseur. Vous devriez voir quelque chose comme `CASE-01000-A` centré en bas de chaque page. Si les numéros sont absents, revérifiez que la propriété `Placement` correspond à l'emplacement souhaité.

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet, prêt à être exécuté :

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Résultat attendu

- **Fichier :** `bates_out.pdf` dans le même dossier que `source.pdf`
- **Visuel :** Texte centré en bas `CASE-01000-A`, `CASE-01001-A`, … pour chaque page suivante
- **Comportement :** Les numéros sont intégrés de façon permanente ; ils survivent à l'impression, à l'aplatissement et à d'autres modifications.

## Variations courantes & cas limites

| Situation | Comment ajuster |
|-----------|-----------------|
| **Numéro de départ différent** | Modifiez `StartNumber` à n'importe quel entier (par ex., `StartNumber = 500`). |
| **Suffixes de lettres par volume** | Utilisez une boucle pour modifier `Suffix` par page, ou créez plusieurs artifacts avec des suffixes différents. |
| **Numérotation alignée à droite** | Définissez `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Documents volumineux (10k+ pages)** | Envisagez de traiter les pages par lots ou d'augmenter `NumberDigits` pour éviter le dépassement. |
| **Masquer les numéros sur certaines pages** | Ignorez ces pages dans la boucle `foreach` (par ex., `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Attention :** Utiliser un `Prefix` ou `Suffix` contenant des caractères illégaux pour les noms de fichiers (par ex., `*` ou `?`). Aspose les incorporera toujours, mais ils peuvent poser problème lors de l'extraction du texte ultérieurement.

## Astuces pro pour l'utilisation en production

- **Mettez en cache l'artifact** si vous traitez de nombreux PDF consécutivement ; le créer une fois économise quelques millisecondes par fichier.  
- **Sécurité des threads :** L'instance `BatesNumberingArtifact` n'est pas thread‑safe, donc donnez à chaque thread sa propre copie.  
- **Performance :** Pour des lots massifs, désactivez la compression PDF (`pdfDocument.Compress = false`) avant l'enregistrement, puis réactivez‑la si nécessaire.  
- **Tests :** Effectuez toujours une vérification visuelle rapide du premier PDF généré pour vous assurer que le placement correspond aux normes de votre équipe juridique.

## Conclusion

Vous disposez maintenant d'une recette solide, de bout en bout, pour **add bates numbers** à n'importe quel PDF en utilisant Aspose.Pdf, avec des options pour **add footer to pdf**, **add page numbers pdf**, et **add custom page numbering**. Le code est entièrement autonome, fonctionne avec .NET 6 et versions ultérieures, et peut être intégré à n'importe quel pipeline d'automatisation existant.

Et ensuite ? Essayez de remplacer le placement `BottomCenter` par un style d'en‑tête, expérimentez des préfixes dynamiques (par ex., des identifiants de dossiers provenant d'une base de données), ou combinez cela avec les fonctionnalités d'extraction de texte d'Aspose pour générer un index consultable de vos documents nouvellement numérotés. Le ciel est la limite, et vous venez d'acquérir un outil puissant pour le contrôle des documents.

Bon codage, et que vos PDF restent toujours parfaitement numérotés !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}