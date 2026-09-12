---
category: general
date: 2026-09-12
description: Apprenez à ajouter de la transparence à un PDF, dessiner un rectangle
  sur un PDF et enregistrer le PDF avec transparence en utilisant Aspose.PDF en C#
  – guide étape par étape.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: fr
lastmod: 2026-09-12
og_description: Ajoutez de la transparence à un PDF, dessinez un rectangle sur le
  PDF et enregistrez le PDF avec transparence en utilisant Aspose.PDF en C#. Suivez
  ce tutoriel complet.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Ajouter de la transparence à un PDF et dessiner un rectangle sur un PDF
  – guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Comment ajouter de la transparence à un PDF et dessiner un rectangle sur un
  PDF avec Aspose.PDF
url: /fr/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter de la transparence à un PDF et dessiner un rectangle sur un PDF avec Aspose.PDF

Si vous devez **ajouter de la transparence à un PDF**, ce guide vous montre exactement comment le faire en C#. Vous apprendrez également comment **dessiner un rectangle sur un PDF** et enfin **enregistrer le PDF avec transparence** afin que le résultat puisse être réutilisé dans des rapports, factures ou tout flux de travail d'automatisation de documents.

Dans ce tutoriel, vous allez :

* Charger un document PDF existant.  
* Créer un état graphique personnalisé qui définit l'opacité du trait et du remplissage.  
* Appliquer cet état graphique au canvas et dessiner un rectangle.  
* Enregistrer le fichier modifié tout en préservant les paramètres de transparence.

Aucun outil externe n'est requis au-delà de la bibliothèque Aspose.PDF for .NET, et chaque ligne de code est expliquée afin que vous compreniez *pourquoi* chaque étape est importante.

## Prérequis

* .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+).  
* Une copie sous licence ou d'évaluation de **Aspose.PDF for .NET**. Installez‑la via NuGet :

```bash
dotnet add package Aspose.Pdf
```

* Un PDF d’entrée (`input.pdf`) placé dans un dossier que vous pouvez référencer depuis votre projet.

## Étape 1 : Charger le document PDF

La première opération consiste à ouvrir le fichier source. L’utilisation de l’instruction `using` garantit que le document est correctement libéré, ce qui évite les problèmes de verrouillage de fichier lors de l’enregistrement ultérieur.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Pourquoi c’est important* : Charger le document vous donne accès à la collection de pages, aux dictionnaires de ressources et aux objets canvas nécessaires pour le dessin.

## Étape 2 : Accéder au dictionnaire de ressources de la première page

Chaque page PDF possède un **dictionnaire de ressources** qui stocke des objets tels que les polices, les images et les états graphiques. Pour introduire un nouveau paramètre de transparence, nous devons modifier l’entrée `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Pourquoi c’est important* : Le `DictionaryEditor` nous permet de lire et de modifier des objets PDF de bas niveau sans rompre la structure du document.

## Étape 3 : Créer un état graphique personnalisé avec des valeurs de transparence

Un état graphique (`ExtGState`) contrôle la façon dont les opérations de dessin sont rendues. Nous définissons deux paramètres d’opacité :

* **CA** – opacité du trait (le contour des formes).  
* **ca** – opacité du remplissage (l’intérieur des formes).

Nous définissons également le mode de fusion (`BM`) à « Normal », qui est l’opération de composition la plus courante.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Pourquoi c’est important* : En ajoutant `GS0` au dictionnaire `ExtGState`, nous créons une référence réutilisable que le canvas peut activer avant le dessin. L’opacité de remplissage de `0.5` rend le rectangle semi‑transparent, atteignant ainsi l’objectif **ajouter de la transparence à un PDF**.

## Étape 4 : Appliquer l’état graphique et dessiner un rectangle

Nous indiquons maintenant au canvas de la page d’utiliser l’état graphique que nous venons de créer, puis nous dessinons un rectangle. Les coordonnées suivent le système de coordonnées PDF (origine en bas‑à‑gauche).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Pourquoi c’est important* : `SetGraphicsState("GS0")` bascule le contexte de dessin vers les paramètres de transparence définis précédemment. La méthode `Rectangle` définit la forme, et `Stroke` rend le contour avec l’opacité spécifiée. Si vous souhaitez également un rectangle rempli, remplacez `Stroke()` par `FillAndStroke()`.

## Étape 5 : Enregistrer le PDF modifié tout en préservant la transparence

Enfin, écrivez le document sur le disque. Le fichier de sortie contient le nouvel état graphique, le rectangle dessiné et les informations de transparence.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Pourquoi c’est important* : L’enregistrement du document finalise toutes les modifications. Le fichier résultant peut être ouvert dans n’importe quel lecteur PDF, et le rectangle apparaîtra avec une opacité de remplissage de 50 %.

### Résultat attendu

Lorsque vous ouvrez `output_with_extgstate.pdf`, vous devez voir un rectangle dont le bord est totalement opaque et dont l’intérieur est semi‑transparent, laissant ainsi transparaître le contenu sous‑jacent de la page.

## Cas limites et conseils pratiques

| Situation | Ajustement recommandé |
|-----------|------------------------|
| **Multiple pages** | Parcourez `pdfDocument.Pages` et répétez les étapes 2‑4 pour chaque page cible. |
| **Different opacity values** | Modifiez les valeurs `CosPdfNumber` pour `CA` (trait) et `ca` (remplissage) avec n’importe quel nombre compris entre `0` (totalement transparent) et `1` (totalement opaque). |
| **Custom blend modes** | Remplacez `"Normal"` par `"Multiply"`, `"Screen"` ou tout autre mode de fusion PDF standard pris en charge par votre visionneur. |
| **Filled rectangle** | Appelez `canvas.FillAndStroke()` au lieu de `canvas.Stroke()` pour appliquer à la fois le remplissage et le contour. |
| **Re‑using the same graphics state** | Vous pouvez appeler `canvas.SetGraphicsState("GS0")` avant de dessiner un nombre quelconque de formes sur la même page. |

**Astuce :** Inspectez toujours le dictionnaire de ressources après avoir ajouté un nouveau `ExtGState`. Si le dictionnaire n’existe pas, créez‑le d’abord :

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Exemple complet et exécutable

Voici un programme autonome que vous pouvez copier dans une application console et exécuter immédiatement (remplacez `YOUR_DIRECTORY` par un chemin réel).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

L’exécution du programme génère `output_with_extgstate.pdf`, qui démontre **ajouter de la transparence à un PDF**, **dessiner un rectangle sur un PDF** et **enregistrer le PDF avec transparence** en un seul flux.

## Conclusion

Vous savez maintenant comment **ajouter de la transparence à un PDF**, **dessiner un rectangle sur un PDF** et **enregistrer le PDF avec transparence** en utilisant Aspose.PDF for .NET. Le processus repose sur la création d’un `ExtGState` personnalisé, son application au canvas et la persistance des modifications. Avec ces blocs de construction, vous pouvez étendre la technique à d’autres formes, plusieurs pages ou des valeurs d’opacité dynamiques.

**Prochaines étapes**

* Explorez d’autres primitives de dessin telles que `canvas.Ellipse`, `canvas.Path` ou `canvas.TextFragment` tout en réutilisant le même état graphique.  
* Combinez la transparence avec des superpositions d’images pour créer des filigranes (`canvas.Image` + `ExtGState` personnalisé).  
* Consultez la documentation Aspose.PDF sur les **paramètres d’état graphique** pour des effets de composition avancés.

Bon codage, et profitez de la flexibilité visuelle que la transparence apporte à vos flux de travail PDF !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment créer un PDF en C# – Ajouter une page, dessiner un rectangle et enregistrer](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Comment ajouter un objet ligne dans un PDF avec Aspose.PDF pour .NET : Guide étape par étape](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Ajouter des tampons d’image aux PDF avec Aspose.PDF pour .NET : Guide étape par étape](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}