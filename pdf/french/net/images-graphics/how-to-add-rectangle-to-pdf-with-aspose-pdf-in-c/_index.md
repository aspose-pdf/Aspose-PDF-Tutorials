---
category: general
date: 2026-10-10
description: Apprenez comment ajouter un rectangle à un PDF, dessiner une forme sur
  un PDF et enregistrer le PDF modifié à l'aide d'Aspose.PDF. Comprend un guide étape
  par étape pour accéder à une page PDF spécifique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: fr
lastmod: 2026-10-10
og_description: Ajouter un rectangle à un PDF avec Aspose.PDF en C#. Ce tutoriel montre
  comment dessiner une forme sur un PDF, accéder à une page PDF spécifique et enregistrer
  le PDF modifié.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Ajouter un rectangle à un PDF avec Aspose.PDF – guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Comment ajouter un rectangle à un PDF avec Aspose.PDF en C#
url: /fr/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter un rectangle à un PDF avec Aspose.PDF en C#

Si vous devez **ajouter un rectangle à un PDF** de façon programmatique, ce guide vous montre exactement comment faire. Vous apprendrez à **dessiner une forme sur un PDF**, cibler une page particulière, et **enregistrer le PDF modifié** sans erreurs.

Travailler avec des documents PDF est une exigence courante pour les rapports, la facturation ou l'annotation de documents. À la fin de ce tutoriel, vous pourrez **ajouter une forme à un PDF** en toute confiance, gérer les erreurs hors limites, et intégrer la solution dans n'importe quel projet .NET.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

* SDK .NET 6.0 ou version ultérieure installé  
* Visual Studio 2022 (ou tout IDE C#)  
* Une licence Aspose.PDF pour .NET ou une clé d'évaluation gratuite – l'API fonctionne de la même manière dans les deux modes  
* Un fichier PDF nommé `input.pdf` placé dans un dossier que vous pouvez référencer depuis votre code  

Ces éléments sont les seules dépendances externes pour l'exemple.

## Étape 1 : Installer le package NuGet Aspose.PDF

La bibliothèque Aspose.PDF fournit les classes `Document`, `Rectangle` et d'autres classes de dessin dont vous avez besoin.

```bash
dotnet add package Aspose.PDF
```

L'exécution de cette commande ajoute la dernière version stable d'Aspose.PDF à votre projet, rendant les classes PDF disponibles pour la compilation.

## Étape 2 : Charger le document PDF

La première opération consiste à charger le fichier source. Cela crée une représentation en mémoire que vous pouvez modifier.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Pourquoi c'est important* : le chargement du document vous donne accès à sa collection de pages, ce qui est nécessaire pour **accéder à une page PDF spécifique** plus tard.

## Étape 3 : Accéder à la deuxième page (index zéro‑based)

Les pages PDF sont indexées à partir de `0`. Pour placer un rectangle sur la deuxième page, récupérez la page à l'index `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Si le document comporte moins de deux pages, une `ArgumentOutOfRangeException` sera levée, vous indiquant la nécessité d’une clause de protection dans le code de production.

## Étape 4 : Créer la forme rectangle

Définissez la position et la taille du rectangle à l'aide de la structure `Rectangle`, puis encapsulez‑le dans un objet de dessin Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Pourquoi c'est important* : les propriétés `BorderInfo` et `FillColor` vous permettent de **dessiner une forme sur un PDF** avec un contour visible et un remplissage optionnel, faisant ressortir le rectangle pour les lecteurs.

## Étape 5 : Ajouter le rectangle à la collection de paragraphes de la page

Aspose.PDF traite les objets de dessin comme des éléments de paragraphe. Ajouter le rectangle à la collection `Paragraphs` de la page le rend visible sur celle‑ci.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

À ce stade, le document PDF en mémoire contient la nouvelle forme, mais le fichier sur le disque reste inchangé jusqu'à ce que vous l'enregistriez.

## Étape 6 : Enregistrer le PDF modifié et gérer les erreurs hors limites

Appeler `Save` écrit le document mis à jour dans un nouveau fichier. Si le rectangle dépasse les dimensions de la page, Aspose lève une `PdfException`. Capturer cette exception vous permet de signaler proprement le problème.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Pourquoi c'est important* : le bloc `try/catch` garantit que votre application **enregistre le PDF modifié** en toute sécurité, et le message d’erreur vous aide à ajuster les coordonnées du rectangle si nécessaire.

## Exemple complet fonctionnel

En réunissant toutes les étapes, voici le programme complet, prêt à être exécuté :

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Résultat attendu

L'exécution du programme affiche :

```
PDF saved successfully with rectangle added.
```

et crée `output.pdf` qui montre le contenu original plus un rectangle bleu aux coordonnées spécifiées sur la deuxième page.

Si le rectangle était plus grand que la page, vous verriez :

```
Shape out of bounds: The shape exceeds page margins.
```

## Questions fréquentes et cas limites

### Que faire si le PDF ne comporte qu’une seule page ?

Tenter d'accéder à `pdfDocument.Pages[1]` lève une `ArgumentOutOfRangeException`. Protégez‑vous en vérifiant `pdfDocument.Pages.Count` avant d’indexer.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Comment ajouter plusieurs rectangles sur différentes pages ?

Répétez les Étapes 2‑4 pour chaque page cible, en ajustant les coordonnées du rectangle selon les besoins. Vous pouvez placer la logique dans une boucle qui parcourt `pdfDocument.Pages`.

### Puis‑je utiliser d’autres formes comme des cercles ou des polygones ?

Oui. Aspose.PDF fournit les classes `Ellipse`, `Polygon` et `Polyline` qui suivent le même schéma que `Rectangle`. Remplacez l’appel `new Aspose.Pdf.Drawing.Rectangle` par la classe de forme souhaitée.

### La bibliothèque prend‑elle en charge les PDF avec des pages pivotées ?

Aspose.PDF respecte automatiquement la rotation de la page lors du rendu des formes. Les coordonnées du rectangle sont interprétées dans le système de coordonnées natif de la page, aucune transformation supplémentaire n’est requise.

## Considérations de performance

* **Utilisation mémoire** – Charger un PDF volumineux (des centaines de mégaoctets) consomme une mémoire proportionnelle. Si vous n’avez besoin de modifier qu’une seule page, envisagez d’utiliser `PdfFileInfo` pour extraire cette page, la modifier, puis la réintégrer.
* **Traitement par lots** – Lors de l’ajout de formes à de nombreux documents, réutilisez une seule instance `License` afin d’éviter le surcoût de validation répétée de la licence.

## Prochaines étapes

Maintenant que vous pouvez **add rectangle to PDF**, explorez ces sujets connexes :

* **draw shape on PDF** – apprenez à superposer du texte, des images et des filigranes  
* **add shape to PDF** – combinez plusieurs formes en une seule couche d’annotation  
* **save modified PDF** – utilisez des flux (`MemoryStream`) pour renvoyer les PDF directement depuis des API web  
* **access specific PDF page** – implémentez l’extraction de plages de pages pour des rapports personnalisés  

Expérimentez avec différentes couleurs, styles de ligne et niveaux de transparence pour correspondre aux directives de votre identité visuelle.

---

*Bon codage ! Si ce tutoriel vous a aidé à **add rectangle to PDF**, pensez à le partager avec vos collègues ou à contribuer des améliorations à la communauté.*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment ajouter une forme à un PDF avec Aspose.PDF en C# – Guide étape par étape](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Comment ajouter un objet ligne dans un PDF en utilisant Aspose.PDF pour .NET : guide étape par étape](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Comment créer un PDF en C# – Ajouter une page, dessiner un rectangle et enregistrer](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}