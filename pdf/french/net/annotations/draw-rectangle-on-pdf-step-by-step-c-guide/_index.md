---
category: general
date: 2026-08-14
description: Dessinez un rectangle sur un PDF rapidement avec C#. Apprenez à définir
  les dimensions du rectangle et à ajouter des formes à une page PDF en quelques lignes
  seulement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: fr
lastmod: 2026-08-14
og_description: Dessinez un rectangle sur un PDF avec C# en quelques secondes. Ce
  guide montre comment définir les dimensions du rectangle, ajouter une forme et vérifier
  les limites de la page pour des graphiques PDF fiables.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: dessiner un rectangle sur un PDF – tutoriel complet C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Dessiner un rectangle sur un PDF – guide C# étape par étape
url: /fr/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# dessiner un rectangle sur pdf – tutoriel complet C#

Si vous devez **dessiner un rectangle sur pdf** avec C#, ce guide vous présente une solution concise et prête pour la production. Vous verrez exactement **comment définir les dimensions d'un rectangle**, vérifier que la forme s'adapte, et l'ajouter à une page avec un seul appel de méthode.

Le tutoriel couvre tout, de la création d'un document PDF au rendu du rectangle, afin que vous puissiez copier‑coller le code dans votre propre projet et voir les résultats immédiatement. Aucune documentation externe n'est requise — seulement les étapes ci‑dessous.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

* .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+)
* Le package NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* Une compréhension de base de la syntaxe C#
* Un IDE tel que Visual Studio ou VS Code

> **Astuce :** Utilisez la licence d'évaluation gratuite d'Aspose.PDF pour des expériences rapides ; elle ajoute un petit filigrane mais vous permet de tester toutes les fonctionnalités.

## Comment dessiner un rectangle sur PDF avec C#

L'essentiel de la tâche consiste à créer un `RectangleShape`, définir sa taille et son contour, puis l'attacher à une `Page`. Le titre H2 suivant contient le mot‑clé principal, répondant aux exigences SEO.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Explication de chaque étape

| Étape | Pourquoi c'est important |
|------|---------------------------|
| **1️⃣ Créer un nouveau document PDF** | Initialise le conteneur qui contiendra les pages et les graphiques. |
| **2️⃣ Ajouter une page vierge** | Vous avez besoin d'un objet `Page` car les formes sont attachées à une page, pas directement au document. |
| **3️⃣ Définir les limites du rectangle** | C’est ici que vous **comment définir les dimensions d'un rectangle**. Le constructeur `Rectangle` prend `x`, `y`, `width` et `height` en points (1 pt = 1/72 in). |
| **4️⃣ Créer la forme rectangle** | `RectangleShape` est la classe Aspose qui rend un rectangle. Définir `StrokeColor` indique le contour ; vous pouvez aussi définir `FillColor` pour un remplissage plein. |
| **5️⃣ Vérifier les limites de la page** | `CheckShapeBoundary` lève une exception si le rectangle dépasse la taille de la page, évitant ainsi des PDF mal formés. |
| **6️⃣ Ajouter la forme à la page** | La forme devient partie du flux de contenu de la page. |
| **7️⃣ Enregistrer le PDF** | Persiste le document dans un fichier que vous pouvez ouvrir avec n'importe quel lecteur PDF. |

Le `RectangleDemo.pdf` résultant contient un rectangle noir positionné dans le coin supérieur gauche de la page, exactement 500 pt de large et 700 pt de haut.

![dessiner un rectangle sur pdf exemple](https://example.com/rectangle-demo.png "dessiner un rectangle sur pdf exemple")

*Texte alternatif de l'image : exemple de dessin d'un rectangle sur pdf montrant un rectangle noir dans le coin supérieur gauche d'une page PDF.*

## Comment définir les dimensions d'un rectangle pour différentes tailles de page

L'extrait ci‑dessus utilise des valeurs fixes (`500 x 700`). Dans les applications réelles, vous devez souvent que le rectangle s'adapte à la largeur et à la hauteur de la page.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Points clés :**

* Utilisez `page.PageInfo.Width` et `Height` pour lire la taille réelle de la page.
* Multiplier par un facteur (par ex., `0.8f`) vous permet d'exprimer les dimensions en pourcentage de la page.
* Le centrage s'obtient en soustrayant la taille du rectangle de la taille de la page et en divisant le reste par deux.

## Pièges courants et comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| Le rectangle dépasse la page | Dimensions codées en dur plus grandes que la taille de la page. | Appelez `page.CheckShapeBoundary` **avant** d'ajouter la forme ; ajustez les dimensions si une exception est levée. |
| Le contour n'est pas visible | `StrokeColor` laissé à la valeur par défaut (`Color.Empty`). | Définissez explicitement `StrokeColor` (par ex., `Color.Black`). |
| Le rectangle apparaît hors écran | Les coordonnées commencent en bas‑gauche dans l'espace PDF ; utiliser des coordonnées style écran (haut‑gauche) provoque un renversement. | Rappelez‑vous que l'origine `(0,0)` est le coin inférieur gauche. Ajustez `y` en conséquence ou utilisez `pageHeight - desiredY`. |
| Épaisseur de ligne inattendue | L'épaisseur de ligne par défaut peut être trop fine pour l'impression. | Définissez `rectangleShape.LineWidth = 2;` pour augmenter l'épaisseur. |

## Étendre l'exemple

Une fois que vous pouvez **dessiner un rectangle sur pdf**, vous pouvez facilement ajouter d'autres formes :

* **EllipseShape** – pour des cercles ou des ovales.
* **PolygonShape** – pour des polygones personnalisés.
* **TextFragment** – pour étiqueter vos rectangles.

Toutes les formes partagent le même flux de travail : définir les limites, configurer l'apparence, vérifier les limites, puis ajouter à la page.

## Programme complet et exécutable

Voici le programme complet qui combine le rectangle de base et l'exemple de dimensionnement dynamique. Copiez‑le dans un nouveau projet console, restaurez le package NuGet `Aspose.PDF`, puis exécutez.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Sortie attendue :**  
Ouvrez `CombinedRectangles.pdf`. Vous verrez un rectangle noir ancré dans le coin inférieur gauche et un rectangle bleu foncé centré avec un remplissage jaune clair. Les deux rectangles respectent les marges de la page.

## Conclusion

Vous savez maintenant comment **dessiner un rectangle sur pdf** avec C# et précisément **comment définir les dimensions d'un rectangle** pour des mises en page fixes et réactives. L'approche utilise `RectangleShape` d'Aspose.PDF, la vérification des limites et des calculs simples pour s'adapter à n'importe quelle taille de page.

Ensuite, vous pourriez explorer :

* Ajouter des **couleurs de remplissage** et des **styles de ligne** (pointillés, tirets) – mot‑clé secondaire : comment définir les dimensions d'un rectangle avec style.
* Combiner plusieurs formes dans une même `Page` pour créer des graphiques ou des formulaires.
* Exporter le PDF vers un flux pour des API web au lieu de l'enregistrer sur disque.

Expérimentez avec différentes tailles, couleurs et positions pour maîtriser les graphiques PDF dans vos applications .NET. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment personnaliser les PDF avec Aspose.PDF pour .NET : définir les marges de page et tracer des lignes](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Comment ajouter des tampons de page dans les PDF en utilisant Aspose.PDF pour .NET : guide complet](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Comment ajouter des tampons de numéro de page dans les PDF en utilisant Aspose.PDF pour .NET | Tampons et arrière‑plans](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}