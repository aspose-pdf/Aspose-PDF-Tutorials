---
category: general
date: 2026-03-22
description: Ajoutez rapidement une numérotation Bates à un PDF avec Aspose.Pdf. Apprenez
  comment ajouter une numérotation Bates, des numéros de page séquentiels, un pied
  de page personnalisé au PDF, et un artefact au PDF en quelques minutes.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: fr
og_description: Ajouter une numérotation Bates à un PDF avec Aspose.Pdf. Ce guide
  montre comment ajouter la numérotation Bates, ajouter des numéros de page séquentiels,
  ajouter un pied de page personnalisé au PDF et ajouter un artefact au PDF.
og_title: Ajouter la numérotation Bates à un PDF – Tutoriel C# étape par étape
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Ajouter la numérotation Bates PDF – Guide complet C#
url: /fr/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une numérotation Bates PDF – Guide complet C#  

Vous avez déjà eu besoin d'**add bates numbering pdf** à un lot de documents juridiques mais vous ne saviez pas par où commencer ? Vous n'êtes pas le premier—de nombreux développeurs rencontrent ce problème lorsqu'ils construisent des outils de gestion de dossiers. La bonne nouvelle ? Avec Aspose.Pdf vous pouvez **add bates**, **add sequential page numbers**, et même **add custom footer pdf** personnalisés en quelques lignes de code.  

Dans ce tutoriel, nous parcourrons l'ensemble du processus, de l'installation de la bibliothèque à l'enregistrement du fichier final, en ajoutant des astuces sur la façon d'**add artifact to pdf** sans casser le contenu existant. À la fin, vous disposerez d'un extrait prêt à l'emploi que vous pourrez insérer dans n'importe quel projet .NET.

## Ce dont vous avez besoin

- .NET 6+ (le code fonctionne aussi bien sur .NET Core que sur .NET Framework)  
- Une licence valide d'Aspose.Pdf pour .NET (vous pouvez commencer avec une évaluation gratuite)  
- Un PDF d'entrée (`input.pdf`) placé dans un dossier que vous pouvez référencer  
- Visual Studio, Rider ou tout éditeur C# de votre choix  

C’est tout—aucun paquet NuGet supplémentaire en dehors d'Aspose.Pdf.

## Étape 1 : Installer Aspose.Pdf via NuGet

Tout d'abord, installons la bibliothèque sur votre machine. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.Pdf
```

Ou, si vous utilisez la console du gestionnaire de packages de Visual Studio :

```powershell
Install-Package Aspose.Pdf
```

*Astuce :* Après l'installation, vérifiez que le dossier `Aspose.Pdf` apparaît sous `Dependencies → Packages` dans l'explorateur de solution.

## Étape 2 : Charger le document PDF source

Nous créons maintenant un objet `Document` qui représente le PDF que nous voulons marquer. L'utilisation de l'instruction `using` garantit que le handle du fichier est libéré automatiquement.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Pourquoi utiliser `using var` ? Cela garantit la libération même en cas d'exception, évitant les problèmes de verrouillage du fichier lorsque vous essayez d'écraser le même fichier plus tard.

## Étape 3 : Créer et configurer un artefact de numérotation Bates

Un numéro Bates est essentiellement un artefact texte qui vit dans la structure logique du PDF. Vous pouvez le considérer comme un **custom footer pdf** car il apparaît sur chaque page sans faire partie du flux de contenu de la page.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Pourquoi ces paramètres sont importants

- **Prefix** : Utile pour distinguer les types de documents (par ex., “INV‑” pour les factures).  
- **Start** : Définit le premier numéro ; vous pouvez le récupérer depuis une base de données si vous avez besoin de continuité entre les fichiers.  
- **Format** : `"0000"` force un affichage à quatre chiffres, assurant l'alignement lorsque les nombres augmentent.  
- **X/Y** : Les coordonnées sont mesurées depuis le coin inférieur gauche, donc `Y = 20` place le texte juste au-dessus de la marge de la page. Ajustez `X` si vous voulez que le numéro soit aligné à gauche ou centré.

Si vous devez **add sequential page numbers** au lieu de numéros Bates, il suffit d'omettre `Prefix` et d'ajuster `Format` à `"###"` ou tout autre modèle que vous préférez.

## Étape 4 : Appliquer l'artefact à toutes les pages

Aspose.Pdf vous permet d'attacher un artefact à l'ensemble du document en un seul appel. C'est la façon la plus efficace d'**add artifact to pdf** sans parcourir chaque page manuellement.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

En coulisses, Aspose ajoute l'artefact au dictionnaire de chaque page, ce qui signifie que la numérotation fait partie de la structure logique du PDF—parfait pour une extraction ou une recherche ultérieure.

## Étape 5 : Enregistrer le PDF mis à jour

Enfin, écrivez les modifications sur le disque. Vous pouvez écraser le fichier original ou enregistrer dans un nouveau fichier ; ce dernier est plus sûr pendant le développement.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Lorsque vous ouvrez `output.pdf` dans un visualiseur, vous verrez “INV‑1000”, “INV‑1001”, … en bas à droite de chaque page.

### Vérifier le résultat

Ouvrez le PDF dans Adobe Acrobat ou tout autre visualiseur et cherchez les numéros. Si vous devez confirmer programmétiquement, vous pouvez relire l'artefact :

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Ce fragment affiche l'étiquette Bates de chaque page—pratique pour les tests automatisés.

## Cas limites & Questions fréquentes

### Que faire si mon PDF possède déjà un pied de page ?

L'ajout d'un artefact n'écrasera pas les pieds de page existants car les artefacts résident dans une couche séparée. Cependant, si le chevauchement visuel pose problème, ajustez la coordonnée `Y` ou augmentez le décalage `X` pour déplacer le numéro Bates.

### Puis-je utiliser une police ou une couleur différente ?

Absolument. Le `BatesNumberingArtifact` hérite de `Artifact`, vous pouvez donc définir `Font`, `FontColor` et même `Opacity`. Exemple :

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Comment réinitialiser le compteur pour un nouveau document ?

Il suffit de modifier `Start` avant d'appeler `AddArtifact`. Si vous générez de nombreux PDF dans une boucle, conservez un compteur dans votre logique d'application.

### Cette approche est‑elle compatible avec les PDF chiffrés ?

Aspose.Pdf peut ouvrir des PDF chiffrés si vous fournissez le mot de passe :

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Après déchiffrement, les mêmes étapes d'ajout d'artefact fonctionnent parfaitement.

## Exemple complet fonctionnel

Voici le programme complet, prêt à l'exécution. Copiez‑le dans une application console, ajustez les chemins, et appuyez sur **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Sortie attendue :** La console affiche “Bates numbering added successfully!” et `output.pdf` contient des libellés séquentiels comme `INV‑1000`, `INV‑1001`, etc., positionnés en bas à droite de chaque page.

## Récapitulatif rapide

- **Objectif principal :** **add bates numbering pdf** avec Aspose.Pdf.  
- Nous avons couvert **how to add bates**, **add sequential page numbers**, et **add custom footer pdf** via un seul artefact.  
- Le tutoriel a montré comment **add artifact to pdf**, gérer les cas limites et vérifier le résultat.  

## Et après ?

- **Préfixes dynamiques :** Récupérez les valeurs depuis une base de données pour générer “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Placement conditionnel :** Utilisez la détection de la taille de page (`page.MediaBox`) pour centrer les numéros sur les pages en mode paysage.  
- **Combiner avec des filigranes :** Ajoutez un logo semi‑transparent à côté du numéro Bates pour le branding.  

Amusez‑vous à expérimenter—peut‑être découvrirez‑vous une façon plus intelligente de traiter par lots des milliers de fichiers. Si vous rencontrez des problèmes, laissez un commentaire ou consultez la documentation officielle d'Aspose (elle est étonnamment claire). Bon codage !  

![exemple d'ajout de numérotation bates pdf](https://example.com/bates-numbering-screenshot.png "Capture d'écran montrant l'ajout de numérotation bates pdf dans un visualiseur PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}