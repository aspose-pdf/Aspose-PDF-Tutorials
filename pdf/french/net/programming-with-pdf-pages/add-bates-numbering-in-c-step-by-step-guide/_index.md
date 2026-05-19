---
category: general
date: 2026-03-27
description: Ajoutez rapidement la numérotation Bates en C#. Apprenez comment ajouter
  des numéros de page personnalisés, des numéros de page séquentiels et des numéros
  personnalisés aux documents Word.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: fr
og_description: Ajoutez la numérotation Bates en C# avec un exemple clair. Ce guide
  montre comment ajouter des numéros de page personnalisés, des numéros de page séquentiels,
  et plus encore.
og_title: Ajouter la numérotation Bates en C# – Tutoriel complet
tags:
- C#
- Document Processing
- Bates Numbering
title: Ajouter la numérotation Bates en C# – Guide étape par étape
url: /fr/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter la numérotation Bates en C# – Guide étape par étape

Vous êtes-vous déjà demandé comment **ajouter une numérotation Bates** à un document Word sans perdre la tête ? Vous n'êtes pas le seul. Dans de nombreux projets juridiques ou de conformité, chaque page doit disposer d’un identifiant unique, et le faire manuellement est un cauchemar.  

Dans ce tutoriel, nous passerons en revue un exemple complet et exécutable qui **ajoute la numérotation Bates**, vous montre **comment ajouter des Bates** en quelques lignes, et couvre même comment **ajouter des numéros de page personnalisés** et **ajouter des numéros de page séquentiels** lorsque vous en avez besoin. À la fin, vous disposerez d’un fichier .docx estampillé avec les numéros de votre choix—sans aucun outil tiers.

## Ce que vous allez apprendre

- Charger un fichier DOCX avec l’API Aspose.Words for .NET (ou toute bibliothèque compatible).  
- Configurer **add custom numbers** tels qu’un préfixe, une valeur de départ et une taille de police.  
- Appliquer la numérotation à chaque page en un seul appel.  
- Enregistrer le résultat et vérifier que les numéros apparaissent comme prévu.  

Aucune expérience préalable de la numérotation Bates n’est requise ; il suffit d’une configuration C# de base et d’une copie du document source. Plongeons‑y.

## Prérequis

- .NET 6+ (le code fonctionne aussi bien sur .NET Core que sur .NET Framework).  
- Aspose.Words for .NET installé via NuGet (`Install-Package Aspose.Words`).  
- Un document Word nommé `input.docx` placé dans un dossier que vous pouvez référencer (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code ou tout IDE C# de votre choix.

> **Astuce :** Si vous utilisez une autre bibliothèque (par ex. Open XML SDK), les concepts restent les mêmes—il suffit d’échanger les appels d’API.

## Étape 1 : Charger le document source

Tout d’abord, nous devons charger le fichier Word en mémoire.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Pourquoi c’est important :* Le chargement du fichier crée un objet `Document` qui vous donne accès aux pages, sections et à l’arbre de nœuds de bas niveau. Sans cela, vous ne pouvez pas attacher de numérotation.

## Étape 2 : Configurer les options de numérotation Bates

Nous définissons maintenant exactement comment les numéros doivent apparaître. C’est ici que vous **add custom page numbers** ou **add sequential page numbers**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Pourquoi c’est important :* Le `Prefix` vous permet **add custom numbers** comme un identifiant de dossier, tandis que `Start` détermine le compteur initial. Modifier `FontSize` garantit que les numéros ne débordent pas des marges de la page.

## Étape 3 : Appliquer la numérotation Bates à chaque page

Avec les options prêtes, nous demandons à la bibliothèque d’estamper chaque page.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Pourquoi c’est important :* La méthode `AddBatesNumbering` parcourt la collection interne des pages et insère une zone de texte dans le coin inférieur droit (emplacement par défaut). C’est le cœur de **how to add bates** sans écrire vous‑même une boucle.

## Étape 4 : Enregistrer le document mis à jour

Enfin, nous écrivons le fichier modifié sur le disque.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Pourquoi c’est important :* L’enregistrement crée un nouveau `output.docx` que vous pouvez ouvrir avec Word, LibreOffice ou tout autre visualiseur pour confirmer que les numéros apparaissent.

## Résultat attendu

Ouvrez `output.docx`. Chaque page doit afficher quelque chose comme :

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Si vous ouvrez l’aperçu avant impression du document, vous verrez les numéros dans le coin inférieur droit, avec la taille de police que vous avez définie.

## Cas particuliers & variantes

| Situation | Ce qu’il faut modifier | Pourquoi |
|-----------|------------------------|----------|
| **Pas de préfixe nécessaire** | `Prefix = string.Empty` | Supprime la partie « ABC‑ », ne laissant que la séquence numérique. |
| **Commencer à 1** | `Start = 1` | Utile pour **add sequential page numbers** simples sans préfixe personnalisé. |
| **Documents volumineux (>10 000 pages)** | Augmenter `FontSize` ou ajuster `Location` (utiliser les surcharges de `AddBatesNumbering`) | Évite le chevauchement avec les pieds‑de‑page ou en‑têtes. |
| **Fichier source en lecture‑seule** | Ouvrir avec `LoadOptions` qui autorisent l’écriture, ou copier le fichier d’abord | Sinon `document.Save` lèvera une exception. |
| **Placement différent** | `batesOptions.Position = BatesNumberingPosition.TopLeft` (ou autre enum) | Certaines entreprises exigent les numéros en haut de page. |

> **Remarque :** Toutes les bibliothèques n’exposent pas une classe `BatesNumberingOptions`. Avec Open XML SDK, vous inséreriez manuellement une `TextBox`—même principe, plus de code.

## Exemple complet fonctionnel

Voici le programme complet en un seul bloc. Copiez‑collez‑le dans une application console et exécutez‑le.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Exécutez le programme, ouvrez `output.docx`, et vous verrez la numérotation exactement où vous l’attendiez. 🎉

## FAQ

**Q : Puis‑je changer la couleur des numéros ?**  
R : Oui. Après l’appel à `AddBatesNumbering`, vous pouvez récupérer les objets `Shape` générés et définir leur propriété `FillColor`.

**Q : Et si je veux les numéros à gauche au lieu de droite ?**  
R : Utilisez `batesOptions.Position = BatesNumberingPosition.BottomLeft` (ou `TopLeft`, `TopRight`). L’API supporte les quatre coins.

**Q : Cela fonctionne‑t‑il avec une sortie PDF ?**  
R : Absolument. Après avoir ajouté la numérotation, appelez `document.Save("output.pdf")`. Les numéros sont rendus dans le PDF comme dans Word.

## Conclusion

Vous savez maintenant **how to add bates numbering** à un fichier Word avec C#. Le tutoriel a couvert le chargement d’un document, la configuration de **add custom numbers**, l’application de **add sequential page numbers**, et l’enregistrement du résultat final. Avec le code complet, vous pouvez l’intégrer à n’importe quel projet et commencer à estampiller des documents immédiatement.

Prêt pour le prochain défi ? Essayez de combiner cela avec un processeur batch qui parcourt un dossier de fichiers, ou explorez **add custom page numbers** dans l’en‑tête/pied‑de‑page pour un rendu plus soigné. Dans tous les cas, vous disposez d’une base solide pour toute tâche d’automatisation juridique ou de conformité.

Des questions ou un cas d’usage intéressant ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}