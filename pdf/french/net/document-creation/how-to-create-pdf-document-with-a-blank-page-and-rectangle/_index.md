---
category: general
date: 2026-09-05
description: Créer un document PDF en C# en ajoutant une page blanche, en dessinant
  un rectangle et en enregistrant le fichier PDF. Suivez un exemple Aspose.PDF pas
  à pas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: fr
lastmod: 2026-09-05
og_description: Créer un document PDF en C# en ajoutant une page blanche, en dessinant
  un rectangle et en enregistrant le fichier PDF. Suivez cet exemple complet avec
  Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Créer un document PDF avec une page blanche et un rectangle – Guide C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Comment créer un document PDF avec une page blanche et un rectangle
url: /fr/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un document PDF avec une page vierge et un rectangle

Si vous devez **créer un document PDF** de manière programmatique, ce guide présente une solution complète en C#. Vous apprendrez comment ajouter une page vierge, dessiner un rectangle sur cette page, puis enregistrer le fichier PDF. L'exemple utilise la bibliothèque Aspose.PDF, qui fonctionne avec .NET 6+ et .NET Framework 4.5+.

Ajouter une page vierge et dessiner des formes est une exigence courante pour les factures, les certificats ou les rapports personnalisés. À la fin de ce tutoriel, vous disposerez d'un projet exécutable qui produit un PDF contenant un seul rectangle positionné à (100, 100) avec une taille de 200 × 200 points.

## Prérequis

* Visual Studio 2022 (ou tout IDE C#)
* .NET 6 SDK ou .NET Framework 4.5+
* Package NuGet Aspose.PDF for .NET  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Permission d'écriture sur le répertoire de sortie

Aucune configuration supplémentaire n'est requise ; le code fonctionne immédiatement.

## Créer un document PDF – aperçu

Le processus complet se compose de quatre étapes logiques :

1. **Instantiate** un objet `Document` – cela représente le fichier PDF.
2. **Add a blank page** – la page fournit une toile pour le dessin.
3. **Draw a rectangle** – un objet `Path` définit la forme.
4. **Save the PDF file** – persiste le document sur le disque.

Chaque étape est isolée dans sa propre section afin que vous puissiez réutiliser ou remplacer des parties selon les besoins.

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="Capture d'écran montrant un document PDF avec un rectangle dessiné sur une page vierge"}

## Ajouter une page vierge pdf

Un PDF doit contenir au moins une page avant que des graphiques puissent être placés. La méthode `Pages.Add()` crée une page vide avec des dimensions par défaut (A4). Si vous avez besoin d'une taille différente, passez un argument `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Pourquoi cette étape est importante* – L'objet page contient des collections pour le texte, les images et les graphiques vectoriels. Sans page, toute tentative d'ajouter un rectangle déclencherait une exception.

### Cas particulier : taille de page personnalisée

Si votre mise en page nécessite une page de 6 × 9 pouces, remplacez l'appel par défaut par :

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Dessiner un rectangle pdf

Dessiner un rectangle consiste à créer une géométrie `Rectangle` et à l'envelopper dans un `Path`. L'appel `ValidateBounds()` garantit que la forme tient à l'intérieur des marges de la page, évitant ainsi le rognage.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Pourquoi cette étape est importante* – L'objet `Path` est la primitive vectorielle de bas niveau utilisée par Aspose.PDF. En validant les limites, vous évitez les erreurs d'exécution lorsque le rectangle dépasse les limites de la page.

### Astuce : style du rectangle

Vous pouvez modifier la couleur du trait et l'épaisseur de la ligne :

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Cela produit un contour rouge avec une épaisseur de 2 points.

## Enregistrer le fichier pdf

La persistance du document finalise le fichier sur le disque. La méthode `Save` accepte un chemin de fichier ou un flux. Fournir un chemin absolu rend l'emplacement explicite, ce qui est utile pour les scripts d'automatisation.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Pourquoi cette étape est importante* – L'enregistrement est le seul moment où la représentation en mémoire devient un fichier physique. Si vous devez renvoyer le PDF depuis une API web, remplacez le chemin de fichier par un `MemoryStream`.

### Cas particulier : écrasement de fichiers existants

Aspose.PDF écrase un fichier existant par défaut. Pour protéger les sorties précédentes, vérifiez d'abord l'existence du fichier :

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Comment ajouter un rectangle – bonnes pratiques

* **Conservez les coordonnées à l'intérieur des marges de la page** – utilisez `ValidateBounds()` ou calculez les marges manuellement.
* **Réutilisez les objets `GraphInfo`** lors du dessin de plusieurs formes ; cela réduit l'allocation mémoire.
* **Libérez l'objet `Document`** (comme montré avec `using var`) pour libérer rapidement les ressources natives.
* **Testez avec différents réglages DPI** si vous intégrez plus tard des images raster ; les formes vectorielles comme les rectangles restent nettes à n'importe quelle résolution.

## Exemple complet fonctionnel

Ci-dessous le programme complet que vous pouvez copier dans une application console. Il compile sans modification et produit `output.pdf` dans le dossier du projet.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Résultat attendu

L'exécution du programme crée un PDF d'une seule page. Lorsque vous ouvrez `output.pdf`, vous verrez une page blanche vierge avec un rectangle rouge positionné à 100 points du bord gauche et du bord inférieur, mesurant 200 × 200 points.

## Conclusion

Vous savez maintenant comment **créer un document PDF**, **ajouter une page vierge pdf**, **dessiner un rectangle pdf**, et **enregistrer le fichier pdf** en utilisant Aspose.PDF en C#. L'exemple couvre les appels d'API essentiels, explique pourquoi chaque appel est nécessaire, et fournit des astuces pour les variations courantes telles que les tailles de page personnalisées ou le style du rectangle.

Ensuite, explorez des sujets connexes comme **ajouter du texte**, **intégrer des images**, ou **créer des rapports multi‑pages**. Le même schéma—instancier un `Document`, manipuler les pages, ajouter du contenu vectoriel ou raster, puis `Save`—s'applique à tous ces scénarios. N'hésitez pas à expérimenter avec différentes formes, couleurs et mises en page pour répondre aux besoins de votre projet.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un document PDF C# – Ajouter une page, dessiner un rectangle et enregistrer](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Créer un document PDF avec Aspose.PDF – Guide étape par étape](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Créer un document PDF avec Aspose – Ajouter une page, zone de texte et formulaire](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}