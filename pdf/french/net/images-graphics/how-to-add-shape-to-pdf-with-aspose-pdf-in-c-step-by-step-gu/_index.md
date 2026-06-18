---
category: general
date: 2026-06-18
description: Comment ajouter une forme à un PDF avec Aspose.PDF en C# – charger un
  PDF, dessiner un rectangle et l’enregistrer.
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: fr
og_description: Comment ajouter une forme à un PDF avec Aspose.PDF en C#. Apprenez
  à charger un document PDF, dessiner un rectangle et enregistrer le fichier mis à
  jour.
og_title: Comment ajouter une forme à un PDF avec Aspose.PDF en C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Comment ajouter une forme à un PDF avec Aspose.PDF en C# – Guide étape par
  étape
url: /fr/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter une forme à un PDF avec Aspose.PDF en C# – Tutoriel complet

Vous vous êtes déjà demandé **comment ajouter une forme à un PDF** sans vous battre avec des flux d'octets de bas niveau ? Dans de nombreuses applications réelles, vous devez mettre en évidence une région, souligner une clause, ou simplement tracer une boîte englobante pour un champ de signature. La bonne nouvelle, c’est qu’Aspose.PDF rend cela très simple. Dans ce guide, nous chargerons un document PDF en C#, dessinerons un rectangle et enregistrerons le résultat — rien de plus, rien de moins.

Nous passerons en revue chaque ligne de code, expliquerons *pourquoi* chaque élément est important, et même vous montrerons une façon rapide de vérifier que la forme se trouve exactement où vous l’attendez. À la fin, vous serez à l’aise avec **comment dessiner des formes dans des fichiers PDF**, et vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet .NET.

## Prérequis

- **.NET 6.0** (ou toute version .NET récente) installé sur votre machine.  
- Une **licence valide Aspose.PDF for .NET** (ou une clé d’évaluation gratuite).  
- Visual Studio 2022, Rider, ou tout éditeur de votre choix.  
- Un fichier PDF existant (`input.pdf`) placé dans un dossier que vous pouvez référencer.

> **Astuce :** Si vous ne faites que tester, la version d’évaluation gratuite suffit parfaitement — elle ajoute un petit filigrane mais se comporte autrement comme le produit complet.

## Étape 1 : Configurer le projet et importer les espaces de noms

Tout d’abord, créez un nouveau projet console (ou ajoutez‑le à un projet existant) et importez les espaces de noms nécessaires.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

**Pourquoi c’est important :** `Aspose.Pdf` vous fournit le modèle de document principal, tandis que `Aspose.Pdf.Drawing` contient la classe de forme `Rectangle` que nous utiliserons plus tard. Sans ce dernier, le compilateur signalera que `Rectangle` n’est pas défini.

## Étape 2 : Charger le document PDF en C#

Maintenant, nous **chargeons réellement le document PDF en C#**. C’est la première opération que vous effectuez toujours lorsque vous avez l’intention de modifier un fichier existant.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*Explication* :  
- `Document` représente le fichier complet dans Aspose.  
- Passer le chemin complet au constructeur lit le fichier en mémoire.  
- La ligne `Console.WriteLine` est optionnelle mais pratique pour le débogage — si le nombre de pages est zéro, vous savez immédiatement qu’il y a eu un problème.

## Étape 3 : Définir la forme Rectangle

Voici le cœur de **comment ajouter une forme à un PDF**. Nous créons un objet `Rectangle` qui spécifie sa position et sa taille en utilisant le système de coordonnées où (0,0) correspond au coin inférieur gauche de la page.

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

Pourquoi nous définissons `FillColor` sur transparent : la plupart des cas d’utilisation ne veulent qu’une bordure (pensez à une boîte de surlignage). La propriété `Border` vous permet de contrôler l’épaisseur et la couleur ; le rouge fait ressortir le rectangle sur une page blanche typique.

## Étape 4 : Vérifier que la forme tient à l'intérieur des limites de la page

Avant d’**ajouter le rectangle**, il est judicieux de s’assurer que la forme ne déborde pas des bords de la page. Aspose fournit `ValidateShapeBounds` exactement pour cela.

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*Pourquoi* : Dessiner en dehors de la page peut provoquer des artefacts d’affichage ou même lever une exception. Cette vérification rend le tutoriel robuste pour les PDF de toute taille.

## Étape 5 : Ajouter le rectangle à la page souhaitée

Nous **ajoutons enfin la forme au PDF**. La méthode `AddRectangle` attache la forme à la collection d’annotations de la page, ce qui signifie que les visionneuses PDF la rendront comme n’importe quel autre dessin.

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

Si vous devez cibler une page différente, remplacez simplement l’indice `1` par le numéro de page approprié (Aspose utilise un indexation à partir de 1).

## Étape 6 : Enregistrer le PDF modifié

La dernière étape consiste à écrire les modifications sur le disque. Vous pouvez écraser le fichier original ou en créer un nouveau — ici nous générerons `output.pdf`.

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*Ce à quoi vous devez vous attendre* : Ouvrez `output.pdf` dans Adobe Reader ou tout autre lecteur et vous devriez voir un rectangle rouge net ancré au coin inférieur gauche de la première page.

![Diagramme montrant le rectangle ajouté au PDF](https://example.com/rectangle-diagram.png "exemple d'ajout de forme à un PDF")

*Texte alternatif* : "comment ajouter une forme à un PDF – rectangle dessiné sur la première page d'un fichier PDF"

## Étape 7 : Exemple complet fonctionnel (prêt à copier‑coller)

Ci‑dessous se trouve le programme complet que vous pouvez compiler et exécuter immédiatement. N’oubliez pas de remplacer `YOUR_DIRECTORY` par le chemin réel de votre dossier.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

Exécutez le programme, ouvrez `output.pdf`, et vous verrez le rectangle rouge exactement où nous l’avons placé. Si vous avez besoin d’une forme différente — ellipse, ligne ou polygone — remplacez simplement `Rectangle` par `Ellipse`, `Line` ou `Polygon` tout en conservant le même flux de travail. C’est essentiellement **comment dessiner des formes dans un PDF** avec Aspose.

## Questions fréquentes et cas particuliers

### Et si je dois dessiner sur plusieurs pages ?

Il suffit de parcourir `pdfDoc.Pages` et d’appeler `AddRectangle` (ou toute autre forme) pour chaque page. N’oubliez pas d’ajuster les coordonnées si les pages ont des tailles différentes.

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### Puis-je remplir le rectangle avec une couleur ?

Absolument. Changez `FillColor` de `Transparent` à n’importe quelle `Color` que vous désirez, par exemple `Color.Yellow`. La forme apparaîtra alors comme un bloc plein.

### Cela fonctionne-t-il avec des PDF protégés par mot de passe ?

Aspose.PDF peut ouvrir les fichiers chiffrés si vous fournissez le mot de passe :

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### Comment ajouter un rectangle avec des coins arrondis ?

Utilisez la classe `RoundedRectangle` à la place de `Rectangle`. Le reste des étapes reste identique.

## Récapitulatif

Nous avons couvert **comment ajouter une forme à un PDF** en utilisant Aspose.PDF en C#. Le processus se résume à :

1. **Charger le document PDF en C#** – créer un objet `Document`.  
2. **Définir un rectangle** (ou toute autre forme).  
3. **Valider les limites** pour éviter les débordements.  
4. **Ajouter le rectangle** à la page cible.  
5. **Enregistrer** le fichier modifié.

C’est l’ensemble du flux de travail pour **aspose pdf add rectangle**, et vous disposez maintenant d’un modèle que vous pouvez adapter pour des cercles, des lignes ou des polygones personnalisés.

## Et ensuite ?

- **Explorer d’autres primitives de dessin** : `Ellipse`, `Line`, `Polygon`.  
- **Ajouter des annotations de texte** à côté de vos formes pour plus d’interactivité.  
- **Combiner avec des champs de formulaire PDF** si vous créez un contrat remplissable.  
- **Découvrir les fonctionnalités de conversion PDF d’Aspose** pour transformer vos PDF annotés en images pour des miniatures de prévisualisation.

N’hésitez pas à expérimenter — peut‑être dessiner un filigrane, mettre en évidence une cellule de tableau, ou délimiter un champ de signature. L’API est flexible, et vous connaissez maintenant les bases.

Bon codage, et que vos PDF ressemblent toujours exactement à ce que vous avez prévu !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un document PDF avec Aspose.PDF – Ajouter une page, une forme et enregistrer](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Comment ajouter et personnaliser les numéros de page dans les PDF avec Aspose.PDF pour .NET | Guide de manipulation de documents](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Comment ajouter des hyperliens dans les PDF avec Aspose.PDF pour .NET&#58; Guide complet](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}