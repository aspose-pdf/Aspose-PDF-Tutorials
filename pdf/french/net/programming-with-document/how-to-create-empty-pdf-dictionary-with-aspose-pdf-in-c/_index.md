---
category: general
date: 2026-09-18
description: Apprenez à créer un dictionnaire PDF vide en C# avec Aspose.PDF. Ce guide
  étape par étape couvre ExtGState, l’état graphique et la manipulation de CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: fr
lastmod: 2026-09-18
og_description: Créer un dictionnaire PDF vide en C# avec Aspose.PDF. Suivez ce tutoriel
  complet pour modifier les dictionnaires ExtGState et d’état graphique.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Créer un dictionnaire PDF vide en C# – guide complet Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Comment créer un dictionnaire PDF vide avec Aspose.PDF en C#
url: /fr/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un dictionnaire PDF vide avec Aspose.PDF en C#

Si vous devez **créer un dictionnaire PDF vide** lors du traitement d'un fichier PDF, ce guide vous montre exactement comment le faire en utilisant Aspose.PDF pour .NET. Que vous ajustiez la transparence, les modes de fusion ou tout état graphique personnalisé, les étapes ci‑dessous vous permettent de modifier le dictionnaire `ExtGState` de manière sûre et efficace.

Dans ce tutoriel, vous apprendrez à :

* Charger un document PDF avec Aspose.PDF.
* Accéder aux ressources de la première page et au dictionnaire `ExtGState` existant.
* Construire un nouveau `CosPdfDictionary` vide et le remplir avec des entrées d’état graphique.
* Enregistrer le PDF modifié sans perdre le contenu original.

La solution fonctionne avec tout PDF contenant au moins une page et ne nécessite que la bibliothèque Aspose.PDF (version 23.10 ou ultérieure).

## Prérequis

* .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.8).
* Une référence au package NuGet **Aspose.PDF**.
* Un fichier PDF d’entrée situé à `YOUR_DIRECTORY/input.pdf`.
* Une connaissance de base du C# et des concepts PDF tels que les ressources et l’état graphique.

> **Astuce :** Lors du traitement de gros PDF, encapsulez l’objet `Document` dans un bloc `using` afin de garantir que toutes les poignées de fichiers soient libérées rapidement.

## Étape 1 : Charger le document PDF

La première opération ouvre le fichier source. Aspose.PDF lit l’ensemble du document en mémoire, vous permettant de modifier les objets internes.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Pourquoi c’est important* : Charger le document crée un modèle d’objets mutable. Sans cette étape, vous ne pouvez pas accéder aux ressources de la page nécessaires à la manipulation du dictionnaire.

## Étape 2 : Récupérer les ressources de la première page

Chaque page possède un dictionnaire `Resources` qui contient les polices, les images et les états graphiques. Y accéder vous fournit un `DictionaryEditor` qui simplifie les opérations de lecture/écriture.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Pourquoi c’est important* : Le dictionnaire `ExtGState` se trouve dans les ressources de la page. Modifier le mauvais dictionnaire n’aurait aucun effet sur le rendu.

## Étape 3 : Localiser le dictionnaire ExtGState existant

L’entrée `ExtGState` peut déjà contenir des objets d’état graphique. Nous la récupérons sous forme de `CosPdfDictionary` afin de pouvoir y ajouter de nouvelles entrées.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Si l’entrée `ExtGState` n’existe pas, Aspose.PDF crée automatiquement un dictionnaire vide lorsque vous en assignerez un nouveau plus tard.

## Étape 4 : **Créer un dictionnaire PDF vide** pour un nouvel état graphique

Ici nous construisons un tout nouveau `CosPdfDictionary`—le cœur de l’opération **create empty PDF dictionary**. Nous le remplissons ensuite avec les clés d’état graphique standard :

* `CA` – opacité du trait.
* `ca` – opacité du remplissage.
* `BM` – mode de fusion.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Pourquoi c’est important* : En définissant explicitement chaque entrée, vous contrôlez la façon dont les objets de la page se mélangent et se rendent. Le dictionnaire est **vide** jusqu’à ce que vous ajoutiez ces clés, ce qui satisfait l’exigence de **create empty PDF dictionary** avant de le remplir.

## Étape 5 : Ajouter le nouvel état graphique au dictionnaire ExtGState

Chaque état graphique doit avoir un nom unique (par ex., `GS0`). Nous insérons le dictionnaire fraîchement construit sous ce nom.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Si vous avez besoin de plusieurs états, continuez à ajouter des entrées comme `GS1`, `GS2`, etc., en vous assurant que chaque nom soit unique dans le dictionnaire `ExtGState`.

## Étape 6 : Enregistrer le document PDF mis à jour

Enfin, écrivez les modifications sur le disque. Le fichier original reste intact car nous enregistrons vers un nouveau chemin.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

Le `output.pdf` résultant contient désormais un état graphique supplémentaire (`GS0`) que vous pouvez référencer depuis n’importe quel flux de contenu de page à l’aide de l’opérateur `/GS0`.

## Exemple complet fonctionnel

Assembler toutes les étapes donne un programme autonome que vous pouvez exécuter immédiatement.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Sortie attendue** : Après l’exécution du programme, `output.pdf` contient le même contenu visuel que `input.pdf`. L’inspection du PDF avec un outil tel qu’Adobe Acrobat ou PDF‑Tron affichera une nouvelle entrée `GS0` sous le dictionnaire `ExtGState` de la première page.

## Variations courantes et cas particuliers

| Situation | Ce qu’il faut ajuster |
|-----------|-----------------------|
| **Pas d’entrée ExtGState existante** | Remplacez `resourcesEditor["ExtGState"]` par `new CosPdfDictionary(pdfDocument)` et réattribuez‑le à `firstPage.Resources["ExtGState"]`. |
| **Plusieurs pages nécessitent le même état** | Ajoutez la même entrée `GS0` au dictionnaire `ExtGState` de chaque page, ou référencez le dictionnaire depuis un objet de ressources partagé. |
| **Mode de fusion différent** | Modifiez la valeur `CosPdfName` de `"Normal"` à `"Multiply"`, `"Screen"`, etc., selon l’effet souhaité. |
| **Valeurs d’opacité plus élevées** | Utilisez `new CosPdfNumber(0.8)` pour `ca` ou `CA` afin d’augmenter l’opacité du remplissage ou du trait. |
| **Utilisation d’un opérateur de flux** | Dans le flux de contenu, écrivez `"/GS0 gs"` avant les opérations de dessin pour appliquer le nouvel état graphique. |

## Considérations de performance

* **Utilisation de la mémoire** – Charger un PDF très volumineux consomme de la mémoire proportionnelle au nombre de pages. Si vous n’avez besoin d’éditer que la première page, envisagez d’utiliser `pdfDocument.Pages.Delete(pageNumber)` après le traitement pour libérer les ressources.
* **Sécurité des threads** – Les objets Aspose.PDF ne sont pas thread‑safe. Effectuez les modifications de dictionnaire sur un seul thread ou créez des instances `Document` distinctes par thread.

## Conclusion

Vous savez maintenant comment **create empty PDF dictionary** avec Aspose.PDF, les remplir avec des entrées d’état graphique et les attacher au dictionnaire `ExtGState` d’une page. Cette technique permet un contrôle fin de l’opacité, du mode de fusion et d’autres paramètres de rendu directement depuis C#.

Ensuite, explorez des sujets connexes tels que **PDF manipulation C#**, l’ajout d’entrées personnalisées au **ExtGState dictionary** pour des effets de transparence avancés, ou l’utilisation de **CosPdfDictionary** pour modifier d’autres types de ressources comme les polices ou les XObjects. Expérimentez avec plusieurs états graphiques pour créer des effets visuels sophistiqués dans vos PDFs.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer et remplir des rectangles dans les PDF avec Aspose.PDF pour .NET : guide étape par étape](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [Comment créer des lignes pointillées dans les PDF avec Aspose.PDF pour .NET : guide étape par étape](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Comment ajouter une page vide à la fin d’un PDF avec Aspose.PDF pour .NET | guide étape par étape](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}