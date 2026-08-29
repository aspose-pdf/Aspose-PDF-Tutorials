---
category: general
date: 2026-08-20
description: Créez un état graphique personnalisé dans un PDF avec Aspose.Pdf. Apprenez
  à modifier les ressources PDF et à ajouter de la transparence dans un PDF en quelques
  étapes seulement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: fr
lastmod: 2026-08-20
og_description: Créez un état graphique personnalisé dans un PDF avec Aspose.Pdf.
  Ce tutoriel montre comment modifier les ressources PDF et ajouter rapidement la
  transparence au PDF.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Créer un état graphique personnalisé dans le PDF – Guide Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Créer un état graphique personnalisé dans un PDF avec Aspose.Pdf
url: /fr/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un état graphique personnalisé dans un PDF avec Aspose.Pdf

Si vous devez **créer un état graphique personnalisé** dans un PDF, ce guide vous montre exactement comment le faire avec Aspose.Pdf pour .NET. À la fin du tutoriel, vous serez capable de **modifier les ressources PDF**, d’injecter un nouveau dictionnaire d’état graphique, et d’**ajouter du contenu PDF avec transparence** sans quitter votre projet C#.

Vous verrez un exemple complet et exécutable, une explication de l’importance de chaque ligne, ainsi que des conseils pour gérer les documents multi‑pages ou différents modes de fusion. Aucun outil externe n’est requis — il suffit de la bibliothèque Aspose.Pdf et d’un environnement de développement .NET de base.

## Prérequis

* .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+)
* Une copie sous licence de **Aspose.Pdf for .NET** (l’essai gratuit fonctionne pour les tests)
* Un fichier PDF d’entrée nommé `input.pdf` placé dans un dossier que vous pouvez référencer depuis le code
* Visual Studio 2022 ou tout IDE supportant le développement C#

Le tutoriel suppose que vous êtes familier avec la syntaxe de base du C# et le concept des pages PDF.

## Étape 1 : Charger le PDF source et accéder à la première page

La première opération consiste à ouvrir le fichier PDF et à récupérer la page dont vous souhaitez modifier les ressources. Aspose.Pdf représente chaque page comme un objet `Page`, et chaque page contient un **dictionnaire de ressources** qui stocke les états graphiques, les polices, les XObjects, etc.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Pourquoi c’est important :* La classe `Document` charge le fichier en mémoire, et `Pages[1]` vous donne un accès direct au dictionnaire de ressources de la première page, qui est l’endroit où vit un état graphique.

## Étape 2 : Ouvrir le dictionnaire de ressources pour le modifier

Aspose.Pdf fournit un assistant `DictionaryEditor` qui vous permet de traiter un dictionnaire de ressources comme un `Dictionary` .NET ordinaire. Cela rend simple la lecture, l’ajout ou le remplacement d’entrées comme `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Pourquoi c’est important :* `DictionaryEditor` abstrait les objets COS de bas niveau, vous permettant de travailler avec des paires clé/valeur familières tout en conservant la conformité PDF.

## Étape 3 : Récupérer (ou créer) le dictionnaire ExtGState

L’entrée **ExtGState** contient tous les objets d’état graphique externes pour la page. Si le dictionnaire n’existe pas, Aspose.Pdf en créera un vide pour vous.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Pourquoi c’est important :* Une entrée `ExtGState` manquante provoquerait une `KeyNotFoundException` plus tard. Cette protection permet au code de fonctionner sur des PDF qui n’ont jamais défini d’état graphique personnalisé auparavant—une partie essentielle de la robustesse de **modifier les ressources PDF**.

## Étape 4 : Construire le dictionnaire d’état graphique personnalisé

Un état graphique décrit comment les opérations de dessin sont rendues. Pour **ajouter du PDF avec transparence**, vous devez définir les entrées `ca` (opacité de remplissage) et `CA` (opacité du trait), et éventuellement un mode de fusion (`BM`). Le code suivant construit un nouveau dictionnaire avec ces paramètres.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Pourquoi c’est important :* Les entrées `ca` et `CA` contrôlent la transparence pour les opérations de remplissage et de trait, respectivement. Définir `BM` vous permet d’expérimenter différents effets de composition, ce qui est utile lorsque vous **ajoutez du PDF avec transparence** plus tard, comme des formes ou images semi‑transparentes.

## Étape 5 : Enregistrer le nouvel état graphique sous un nom unique

Chaque état graphique dans le dictionnaire `ExtGState` doit avoir un nom unique (par ex., `GS0`, `GS1`). Vous pouvez choisir n’importe quel nom qui ne entre pas en conflit avec les entrées existantes.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Pourquoi c’est important :* En insérant le nouveau dictionnaire sous `GS0`, vous rendez l’état adressable depuis les flux de contenu de la page. Le bloc conditionnel garantit que l’entrée `ExtGState` est présente même pour les PDF qui n’en avaient pas au départ—une autre protection de **modifier les ressources PDF**.

## Étape 6 : Utiliser l’état graphique personnalisé dans le contenu de la page (optionnel)

Les étapes précédentes ne font que *définir* l’état graphique. Pour voir réellement l’effet, vous devez le référencer dans le flux de contenu de la page. Voici un exemple rapide qui dessine un rectangle semi‑transparent en utilisant l’état que nous venons de créer.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Pourquoi c’est important :* L’opérateur `SetExtGState` (`gs`) indique au rendu PDF d’appliquer les paramètres définis dans `GS0`. Le rectangle apparaîtra avec une opacité de remplissage de 50 % tandis que son trait restera entièrement opaque.

## Étape 7 : Enregistrer le PDF modifié

Enfin, écrivez les modifications sur le disque. Vous pouvez écraser le fichier original ou en créer un nouveau.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Lorsque vous ouvrez `output_with_custom_gs.pdf` dans un visualiseur PDF, vous devriez voir un rectangle semi‑transparent sur la première page. Cela confirme que vous avez réussi à **créer un état graphique personnalisé**, **modifier les ressources PDF**, et **ajouter du contenu PDF avec transparence**.

## Variations courantes et cas limites

| Situation | Ce qu’il faut ajuster |
|-----------|-----------------------|
| **Plusieurs pages nécessitent le même état** | Enregistrez l’état graphique une fois (étapes 1‑5) et référencez `GS0` dans le flux de contenu de n’importe quelle page. |
| **Opacité différente par élément** | Définissez des états supplémentaires (`GS1`, `GS2`, …) avec des valeurs `ca`/`CA` différentes et basculez entre eux en utilisant `SetExtGState`. |
| **Mode de fusion autre que Normal** | Remplacez `"Normal"` par `"Multiply"`, `"Screen"` ou tout autre mode de fusion standard PDF dans l’entrée `BM`. |
| **Collision de nom** | Avant d’ajouter, vérifiez `extGStateDict.ContainsKey(yourName)` et choisissez un suffixe unique si nécessaire. |
| **Le PDF contient déjà un dictionnaire ExtGState** | Le code à l’étape 3 réutilise déjà le dictionnaire existant, donc aucune manipulation supplémentaire n’est requise. |

**Astuce :** Lors du travail avec de gros PDF, encapsulez l’utilisation de `Document` dans un bloc `using` (comme montré) pour libérer rapidement les ressources natives. En outre, envisagez d’activer la propriété `PdfCompliance` d’Aspose.Pdf si vous devez garantir la conformité PDF/A ou PDF/X après la modification des ressources.

## Exemple complet fonctionnel



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment créer un PDF avec Aspose – Ajouter un champ de formulaire et des pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Comment créer des tables personnalisées dans les PDF avec Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Créer des tampons PDF personnalisés Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}