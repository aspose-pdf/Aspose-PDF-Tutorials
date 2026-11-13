---
category: general
date: 2026-11-12
description: Apprenez à modifier l'opacité d'un PDF avec Aspose.Pdf, ajouter de la
  transparence, définir le mode de fusion et enregistrer le PDF modifié en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: fr
lastmod: 2026-11-12
og_description: Modifiez l'opacité d’un PDF avec Aspose.Pdf, apprenez à ajouter de
  la transparence, définir le mode de fusion et enregistrer les fichiers PDF modifiés
  en C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Modifier l'opacité d’un PDF avec Aspose.Pdf – ajouter de la transparence
  et enregistrer
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Modifier l'opacité du PDF avec Aspose.Pdf et enregistrer le fichier
url: /fr/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifier l'opacité d'un PDF avec Aspose.Pdf et enregistrer le fichier

Si vous devez **modifier l'opacité d'un PDF** dans un document, Aspose.Pdf fournit une API simple pour ajuster à la fois la transparence du trait et du remplissage. Ce tutoriel montre exactement **comment ajouter de la transparence**, **comment définir le mode de fusion**, et **enregistrer les fichiers PDF modifiés** avec seulement quelques lignes de code C#.

Vous parcourrez chaque étape — du chargement d'un PDF existant à la définition d'un nouvel état graphique et à la persistance des modifications. À la fin de ce guide, vous pourrez :

* Réduire la visibilité des graphiques vectoriels ou des images.
* Appliquer un mode de fusion personnalisé tel que *Normal* ou *Multiply*.
* Exporter le fichier mis à jour sans perdre aucun autre contenu.

La seule condition préalable est un environnement de développement .NET fonctionnel et une référence à la bibliothèque Aspose.Pdf (version 23.9 ou ultérieure). Aucun outil externe n'est requis.

## Prérequis

| Exigence | Pourquoi c'est important |
|-------------|----------------|
| .NET 6.0 SDK or later | Garantit la compatibilité avec les dernières API Aspose.Pdf. |
| Aspose.Pdf for .NET NuGet package | Fournit les classes `Document`, `CosPdfDictionary` et autres utilisées dans le code. |
| A PDF file to edit (e.g., `input.pdf`) | Sert de source pour les modifications d'opacité. |

Installez le package NuGet avec :

```bash
dotnet add package Aspose.Pdf
```

## Modifier l'opacité d'un PDF avec Aspose.Pdf

### Étape 1 : Charger le document PDF

Commencez par créer une instance `Document` qui pointe vers votre fichier source. Le constructeur lit l'intégralité du PDF en mémoire, vous permettant de manipuler ses objets internes.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Pourquoi cette étape ?** Le chargement du fichier crée un modèle d'objet manipulable. Toutes les modifications suivantes opèrent sur cette représentation en mémoire, garantissant que le fichier original reste intact jusqu'à ce que vous l'enregistriez explicitement.

### Étape 2 : Accéder aux ressources de la première page

Chaque page PDF possède un *dictionnaire de ressources* qui contient des objets tels que les polices, les images et les états graphiques. Vous devez modifier ce dictionnaire pour y injecter une nouvelle entrée `ExtGState`.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Astuce :** Si votre PDF contient plusieurs pages nécessitant la même opacité, répétez cette étape pour chaque page ou partagez un seul `ExtGState` entre les pages.

### Étape 3 : S'assurer qu'un dictionnaire ExtGState existe

Le dictionnaire `ExtGState` contient des états graphiques personnalisés. S'il n'existe pas, le code en crée automatiquement un.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Pourquoi cette étape ?** Sans un conteneur `ExtGState`, toute tentative de référencer un nouvel état graphique échouerait, entraînant un PDF qui ignore vos paramètres d'opacité.

### Étape 4 : Définir un nouvel état graphique (ExtGState)

Un état graphique définit le comportement des opérations de dessin. Le dictionnaire suivant définit l'opacité du trait (`CA`), l'opacité du remplissage (`ca`) et le mode de fusion (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Comment définir l'opacité du remplissage :** L'entrée `ca` contrôle l'opacité des formes remplies (texte, tracés). Ajustez la valeur numérique entre `0` (complètement transparent) et `1` (complètement opaque) selon vos besoins de conception.  
> **Comment définir le mode de fusion :** L'entrée `BM` sélectionne l'algorithme de composition. Les valeurs courantes incluent `Normal`, `Multiply`, `Screen` et `Overlay`. Choisissez celle qui correspond à votre intention visuelle.

### Étape 5 : Enregistrer l'état graphique dans le dictionnaire de ressources

Attribuez un nom au nouvel état (par ex. `GS0`) et ajoutez-le au dictionnaire `ExtGState`. Ce nom sera référencé plus tard dans le flux de contenu de la page.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Conseil pro :** Utilisez une convention de nommage comme `GS0`, `GS1`, … lorsque vous créez plusieurs états. Cela évite les collisions de noms et facilite le débogage.

### Étape 6 : Appliquer l'état graphique au contenu de la page

Pour voir réellement l'effet d'opacité, insérez l'opérateur `/GS0 gs` avant les commandes de dessin que vous souhaitez affecter. L'exemple ci-dessous dessine un rectangle semi‑transparent.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Pourquoi les opérateurs `q` et `Q` ?** Ils poussent et retirent la pile d'états graphiques, garantissant que le changement d'opacité n'affecte que le rectangle et non le reste de la page.

### Étape 7 : Enregistrer le PDF modifié

Enfin, écrivez le document mis à jour sur le disque. La méthode `Save` écrase le fichier cible ou en crée un nouveau s'il n'existe pas.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Comment enregistrer le PDF modifié :** L'appel `Save` écrit toutes les modifications en mémoire, y compris le nouveau `ExtGState`, vers le chemin spécifié. Vous pouvez également diffuser le résultat vers un `MemoryStream` pour les réponses web.

## Exemple complet fonctionnel

Ci-dessous se trouve un programme unique et autonome qui intègre chaque étape décrite ci‑dessus. Copiez‑le dans une application console et exécutez‑le pour vérifier le changement d'opacité.



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment enregistrer un PDF modifié avec Aspose.Pdf et ajouter de la transparence](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Comment ajouter de la transparence à un PDF en utilisant Aspose.PDF en C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Comment ajouter un état graphique PDF et contrôler la transparence avec Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}