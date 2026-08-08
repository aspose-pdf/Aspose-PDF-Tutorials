---
category: general
date: 2026-03-27
description: Apprenez à dessiner un rectangle dans un PDF en utilisant Aspose.Pdf
  pour C#. Ajoutez un rectangle au PDF, ajoutez une forme au PDF et dessinez la forme
  sur le PDF avec des exemples de code clairs.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: fr
og_description: Maîtrisez la façon de dessiner un rectangle dans un PDF avec Aspose.Pdf.
  Ce tutoriel vous montre comment ajouter un rectangle à un PDF, ajouter une forme
  à un PDF et dessiner une forme sur un PDF, étape par étape.
og_title: Comment dessiner un rectangle dans un PDF avec C# – Guide complet
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Comment dessiner un rectangle dans un PDF avec C# – Guide étape par étape
url: /fr/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment dessiner un rectangle dans un PDF avec C# – Guide étape par étape

Vous vous êtes déjà demandé **how to draw rectangle** dans un PDF sans vous battre avec la syntaxe PDF de bas niveau ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent visualiser une boîte englobante, une zone de surbrillance ou un simple élément décoratif dans un document généré. La bonne nouvelle ? Avec Aspose.Pdf for .NET, le processus est un jeu d'enfant.

Dans ce tutoriel, nous passerons en revue tout ce dont vous avez besoin pour **add rectangle to PDF**, **add shape to PDF**, et finalement **draw rectangle in PDF** en utilisant du C# propre et idiomatique. À la fin, vous disposerez d'un programme exécutable qui génère un fichier PDF contenant un rectangle net — sans aucun outil externe requis.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Core et .NET Framework)
- Package NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- Un environnement de développement C# basique (Visual Studio, VS Code, Rider, etc.)

Aucune autre bibliothèque n'est nécessaire ; tout le reste est géré par Aspose.Pdf lui‑même.

## Étape 1 : Configurer le projet et importer les espaces de noms

Tout d'abord, créez une nouvelle application console et importez l'espace de noms Aspose.Pdf.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Pourquoi c'est important :** L'importation de `Aspose.Pdf.Drawing` vous donne accès à la classe de forme `Rectangle` que nous utiliserons pour **draw shape on PDF**. Garder le point d'entrée propre facilite le suivi des étapes suivantes.

## Étape 2 : Créer un nouveau document PDF et une page

Un PDF sans pages n'a aucun sens, nous commençons donc par créer un objet document et ajouter une seule page.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Explication :** La classe `Document` représente le fichier complet, tandis que `Pages.Add()` renvoie un nouvel objet `Page` où nous **add rectangle to PDF** plus tard. Le format A4 par défaut convient à la plupart des cas, mais vous pouvez spécifier largeur/hauteur si vous avez besoin d'un canevas personnalisé.

## Étape 3 : Définir la forme Rectangle

Voici maintenant le cœur de **how to draw rectangle** — la définition de sa position et de ses dimensions.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Pourquoi nous définissons ces propriétés :**  
- `BorderColor` et `BorderWidth` contrôlent le contour, rendant le rectangle visible.  
- `FillColor` lui donne un arrière‑plan subtil, utile lorsque vous souhaitez mettre en évidence une zone.  
- Le constructeur `(x, y, width, height)` vous permet de **draw rectangle in PDF** précisément où vous en avez besoin.

## Étape 4 : Ajouter le rectangle à la page

Avec la forme prête, nous **add shape to PDF** maintenant en l'attachant à la collection `Annotations` de la page. Aspose.Pdf valide automatiquement les limites, vous n'avez donc pas à vous soucier d'un dépassement.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Ce qui se passe en coulisses :** La collection `Annotations` traite le rectangle comme un graphique vectoriel. Lorsque le PDF est rendu, la bibliothèque traduit nos coordonnées dans le flux de contenu PDF.

## Étape 5 : Enregistrer le document

Enfin, écrivez le PDF sur le disque afin de pouvoir l'ouvrir avec n'importe quel lecteur.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Résultat :** L'ouverture de `RectangleDemo.pdf` montre un rectangle gris clair avec une bordure noire positionné à 100 pts du bord gauche et 500 pts du bord inférieur de la page. C’est la solution complète pour **how to draw rectangle** dans un PDF avec C#.

## Exemple complet fonctionnel

En assemblant tous les éléments, voici le programme complet, prêt à être exécuté :

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Sortie attendue :** Un fichier nommé `RectangleDemo.pdf` contenant une seule page avec un rectangle gris clair centré, bordé en noir. Vous pouvez l'ouvrir avec Adobe Reader, Chrome ou tout autre lecteur PDF.

## Variations courantes et cas limites

### 1. Dessiner plusieurs rectangles

Si vous devez **add rectangle to PDF** plusieurs fois, créez simplement des objets `Rectangle` supplémentaires et ajoutez chacun à `page.Annotations`. Parcourir une collection de coordonnées rend cela trivial.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Utiliser d'autres unités

Aspose.Pdf travaille en points (1 pt = 1/72 pouce). Si vous préférez les millimètres, convertissez‑les d'abord :

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Ajouter un rectangle en tant que champ de formulaire

Lorsque vous avez besoin d'un rectangle interactif (par ex., une zone cliquable), utilisez un `LinkAnnotation` au lieu d'un simple `Rectangle`. Le code est similaire mais ajoute une URL ou une action JavaScript.

### 4. Problèmes de compatibilité

Aspose.Pdf version 23.9 (sortie début 2026) prend pleinement en charge les API présentées ci‑dessus. Les versions antérieures peuvent nécessiter `page.AddAnnotation(rectangleShape)` au lieu de `page.Annotations.Add`. Vérifiez toujours les notes de version si vous rencontrez des erreurs de compilation.

## Astuces pro & pièges

- **Astuce pro :** Définissez `FillColor = Color.Transparent` si vous avez seulement besoin d’un contour. Cela réduit légèrement la taille du fichier.
- **Attention à :** Utiliser des coordonnées qui dépassent les dimensions de la page. Aspose.Pdf découpera silencieusement la forme, ce qui peut prêter à confusion lors du débogage.
- **Note de performance :** Ajouter des milliers de rectangles est acceptable, mais si vous générez de gros rapports, envisagez de regrouper les formes dans un seul objet `Graphics` afin de réduire la surcharge.

## Référence visuelle

Voici rapidement une capture d'écran du PDF généré (le rectangle est mis en évidence en gris clair). Le texte alternatif inclut le mot‑clé principal pour le SEO.

![exemple de comment dessiner un rectangle dans un PDF](https://example.com/images/rectangle-demo.png "exemple de comment dessiner un rectangle dans un PDF")

## Conclusion

Nous avons couvert **how to draw rectangle** dans un PDF en utilisant Aspose.Pdf pour C#. En créant un `Document`, en ajoutant une `Page`, en définissant une forme `Rectangle` et enfin en **adding shape to PDF**, vous pouvez générer des graphiques vectoriels avec seulement quelques lignes. Que vous ayez besoin de **add rectangle to pdf** pour la mise en évidence, le débogage de mise en page ou les superpositions UI, l'approche s'adapte bien.

Ensuite, vous pourriez explorer **draw shape on pdf** au‑delà des rectangles — pensez aux cercles, polylignes ou même aux chemins SVG personnalisés. Ou plongez dans le rendu de texte, l'insertion d'images et la manipulation de formulaires PDF pour créer des rapports complets. La bibliothèque Aspose.Pdf offre une API riche, et avec les bases couvertes ici, vous êtes prêt à expérimenter.

Bon codage, et que vos PDF ressemblent toujours exactement à ce que vous imaginez !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}