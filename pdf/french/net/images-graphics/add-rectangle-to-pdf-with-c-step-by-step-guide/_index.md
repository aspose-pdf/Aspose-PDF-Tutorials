---
category: general
date: 2026-08-04
description: Ajouter un rectangle à un PDF avec C#. Apprenez à dessiner une forme
  dans un PDF C# avec Aspose.Pdf dans un exemple clair et complet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: fr
lastmod: 2026-08-04
og_description: Ajouter un rectangle à un PDF avec C#. Ce tutoriel montre comment
  dessiner une forme dans un PDF en C# rapidement et de manière fiable.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Ajouter un rectangle à un PDF avec C# – guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Ajouter un rectangle à un PDF avec C# – guide étape par étape
url: /fr/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un rectangle à un PDF avec C# – guide étape par étape

Si vous devez **ajouter un rectangle à un PDF** depuis une application C#, ce guide vous montre exactement comment le faire. Vous verrez un exemple complet et exécutable qui dessine une forme dans un PDF C# en utilisant la bibliothèque Aspose.Pdf, et vous comprendrez pourquoi chaque ligne de code est importante.

Dessiner des formes dans les PDF est une exigence courante pour les générateurs de rapports, les modèles de factures et le marquage personnalisé de documents. À la fin de ce tutoriel, vous pourrez insérer n’importe quelle annotation rectangulaire, modifier sa taille, sa couleur ou sa position, et enregistrer le document modifié sans perdre le contenu existant.

**Ce que vous allez apprendre**

* Comment charger un PDF existant avec Aspose.Pdf.
* Comment définir les limites du rectangle et créer une forme rectangulaire.
* Comment ajouter le rectangle à la collection de paragraphes d’une page.
* Comment enregistrer le PDF mis à jour et vérifier le résultat.
* Variantes pour plusieurs pages, transparence et styles de ligne personnalisés.

**Prérequis**

* .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+).
* Visual Studio 2022 ou tout IDE C#.
* Une référence NuGet à `Aspose.Pdf` (version d’essai gratuite ou version sous licence).
* Un fichier PDF d’entrée nommé `input.pdf` placé dans un dossier que vous contrôlez.

---

## Comment dessiner une forme dans un PDF C# – configuration du projet

1. **Créer un nouveau projet console**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Ajouter le package Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Placer `input.pdf`** dans le répertoire du projet (ou tout dossier que vous référencerez plus tard).

Le projet est maintenant prêt à compiler du code qui **ajoutera un rectangle à un PDF**.

---

## Étape 1 : Charger le document PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*La classe `Document` analyse le fichier et expose une collection `Pages`. Le chargement est la première opération requise avant de pouvoir dessiner quoi que ce soit.*

---

## Étape 2 : Choisir la page cible

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Si vous devez ajouter le rectangle à une autre page, remplacez l’indice par le numéro de page souhaité. La bibliothèque lève une exception lorsque l’indice est hors limites, assurez‑vous donc que le PDF contient suffisamment de pages.*

---

## Étape 3 : Définir les limites du rectangle

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Le système de coordonnées utilise des points (1 pt = 1/72 pouce). L’exemple crée un rectangle de 250 pt de large sur 100 pt de haut près du haut de la page. Ajustez les valeurs pour correspondre à votre mise en page.*

---

## Étape 4 : Créer la forme rectangle

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*La classe `Rectangle` hérite de `GraphicalObject`. Définir `FillColor` et `Border` est optionnel, mais cela montre comment contrôler l’apparence lorsque vous **dessinez une forme dans un PDF C#** au-delà d’un simple contour.*

---

## Étape 5 : Ajouter le rectangle à la page

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Les paragraphes sont le conteneur de tout objet dessinable. En insérant la forme dans `Paragraphs`, Aspose.Pdf la rend lors de l’enregistrement du document.*

---

## Étape 6 : Enregistrer le PDF modifié

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*L’enregistrement crée un nouveau fichier afin que le `input.pdf` d’origine reste inchangé. Vous pouvez écraser le fichier source en passant le même chemin, mais conserver une sauvegarde est une bonne pratique.*

---

## Code complet (exécutable)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Résultat attendu** – Ouvrez `output.pdf` avec n’importe quel lecteur PDF. Vous devriez voir un rectangle rempli de bleu près du coin supérieur droit de la première page, bordé d’un trait gris foncé.

---

## Comment dessiner une forme dans un PDF C# sur plusieurs pages

Si vous devez **ajouter un rectangle à un PDF** sur chaque page, parcourez la collection `Pages` :

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Ce modèle réutilise les mêmes limites sur chaque page. Ajustez les coordonnées par page si vous avez besoin de positions différentes.*

---

## Pièges courants et conseils de bonnes pratiques

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Le rectangle apparaît hors de la page | Les coordonnées sont mesurées depuis le coin inférieur gauche ; l’utilisation d’un système de coordonnées orienté vers le haut peut prêter à confusion. | Rappelez‑vous que l’axe Y croît vers le haut. Utilisez des valeurs qui tiennent dans la taille de la page (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| La forme est invisible | Opacité du remplissage définie à `0` ou largeur du bord définie à `0`. | Assurez‑vous que `FillOpacity` est supérieur à `0` et que `Border.Width` est au moins `0.5`. |
| L’enregistrement lève `AccessDeniedException` | Le fichier de sortie est ouvert dans un autre programme. | Fermez les visionneurs avant d’exécuter le code, ou enregistrez vers un chemin différent. |
| Le rectangle chevauche le contenu existant | Aucun contrôle de superposition n’a été défini. | Utilisez la propriété `ZIndex` (des valeurs plus élevées se dessinent au-dessus) si vous devez gérer la superposition. |

---

## Étendre le rectangle – dégradés, rotation et transparence

Aspose.Pdf prend en charge les graphiques avancés. Pour créer un rectangle tourné avec un dégradé linéaire :

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Le même modèle de code montre **comment dessiner une forme dans un PDF C#** avec des effets visuels plus riches.*

---

## Vérifier le résultat par programme

Vous pouvez confirmer que le rectangle a été ajouté en vérifiant le nombre de paragraphes de la page :

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Si le nombre a augmenté de un après l’insertion, l’opération a réussi.

---

## Conclusion

Vous savez maintenant comment **ajouter un rectangle à un PDF** à l’aide de C#. Le tutoriel a couvert le chargement d’un document, la définition des limites, la création d’une forme rectangle, son insertion dans une page et l’enregistrement du résultat. Vous avez également vu comment gérer plusieurs pages, éviter les erreurs courantes et appliquer un style avancé.

Ensuite, explorez des sujets connexes tels que **comment dessiner une forme dans un PDF C#** pour des cercles, des polygones ou des tracés libres, et apprenez à combiner formes, texte et images pour créer des rapports PDF pleinement fonctionnels.

Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}