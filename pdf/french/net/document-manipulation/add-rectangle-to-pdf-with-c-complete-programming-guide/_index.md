---
category: general
date: 2026-06-05
description: Ajouter un rectangle à un PDF avec Aspose.Pdf en C#. Apprenez à charger
  un PDF existant, modifier une page PDF et insérer une forme dans le PDF en quelques
  minutes.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: fr
og_description: Ajoutez rapidement un rectangle à un PDF. Ce tutoriel montre comment
  charger un PDF existant, modifier une page PDF et dessiner un rectangle sur le PDF
  à l'aide d'Aspose.Pdf.
og_title: Ajouter un rectangle à un PDF avec C# – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: Ajouter un rectangle à un PDF avec C# – Guide complet de programmation
url: /fr/net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un rectangle à un PDF avec C# – Guide complet de programmation

Vous avez déjà eu besoin d'**ajouter un rectangle à un pdf** sans savoir quel appel d'API utiliser ? Vous n'êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu'ils essaient pour la première fois de modifier un PDF de façon programmatique. Bonne nouvelle ? En quelques lignes de C# et avec la puissante bibliothèque Aspose.Pdf, vous pouvez dessiner un rectangle sur n'importe quelle page d'un document existant en un clin d'œil.

Dans ce guide, nous allons parcourir le chargement d'un PDF existant, la sélection de la bonne page, la définition d'un rectangle adapté, puis l'insertion de la forme dans le PDF. À la fin, vous disposerez d'un extrait réutilisable que vous pourrez intégrer dans n'importe quel projet .NET. Oh, et nous aborderons également les subtilités du **draw rectangle on pdf** que vous n'avez peut‑être pas envisagées.

## Ce que vous allez acquérir

- Une solution claire, étape par étape, qui fonctionne immédiatement.
- Une compréhension de la façon de **load existing pdf** en toute sécurité.
- Des astuces pour **edit pdf page** sans corrompre le document.
- Des stratégies pour **insert shape into pdf** au‑delà des simples rectangles.
- Du code C# prêt à l'emploi que vous pouvez copier‑coller immédiatement.

### Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.6+).
- Package NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`).
- Une connaissance de base de la syntaxe C# (pas besoin de connaissances approfondies sur les PDF).

Si vous avez tout cela, plongeons‑y.

![Add rectangle to PDF example](add-rectangle-to-pdf.png "Screenshot showing a rectangle added to a PDF page – add rectangle to pdf")

## Ajouter un rectangle à un PDF – Vue d'ensemble étape par étape

Voici l'exemple complet et exécutable qui suit exactement l'ordre que nous allons détailler :

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Décomposons maintenant chaque ligne afin que vous compreniez **pourquoi** nous faisons ce que nous faisons, et pas seulement **quoi**.

## Charger un document PDF existant

### Pourquoi le chargement est important

Avant de pouvoir dessiner quoi que ce soit, le PDF doit être chargé en mémoire. Le constructeur `Document` lit le fichier, analyse sa structure interne et vous fournit un modèle d'objet avec lequel travailler. Si le fichier est verrouillé ou corrompu, Aspose lèvera une exception descriptive — vous saurez exactement ce qui a échoué.

### Code

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- Remplacez `YOUR_DIRECTORY` par le chemin absolu ou relatif de votre fichier source.
- Le chemin peut être une URL si vous activez le chargement distant d'Aspose (scénario avancé).
- **Astuce :** Enveloppez cela dans un bloc `try/catch` pour gérer `FileNotFoundException` ou `PdfException` de façon élégante.

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## Sélectionner et préparer la page

### Pourquoi la sélection de la page est cruciale

Les PDF sont orientés page ; chaque page possède son propre système de coordonnées. Aspose utilise un index **basé sur 1**, ce qui surprend les développeurs habitués aux collections basées sur 0. Sélectionner la mauvaise page lève soit une `ArgumentOutOfRangeException`, soit modifie une page non désirée.

### Code

```csharp
Page page = doc.Pages[1]; // First page
```

Si vous devez travailler sur la page 3, changez simplement l'index en `3`. Pour des scénarios dynamiques, vous pouvez boucler :

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## Définir et dessiner le rectangle sur le PDF

### Comprendre les coordonnées du rectangle

Un rectangle dans Aspose.Pdf est défini par ses coins inférieur‑gauche (`xLL`, `yLL`) et supérieur‑droit (`xUR`, `yUR`). Le système de coordonnées commence au **coin inférieur‑gauche** de la page, X augmentant vers la droite et Y augmentant vers le haut. C’est l’inverse de nombreux frameworks UI, donc surveillez bien les axes.

- `0,0` correspond au coin inférieur‑gauche de la page.
- Largeur = `xUR - xLL` ; Hauteur = `yUR - yLL`.

Si vous définissez accidentellement un rectangle plus grand que la page, `AddRectangle` lèvera une exception. Pour éviter cela, vous pouvez interroger la taille de la page :

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

Puis contraindre votre rectangle :

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### Code pour ajouter la forme

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- `AddRectangle` dessine automatiquement une fine bordure noire.
- Vous voulez un rectangle rempli ? Utilisez `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });`.
- Besoin d’une épaisseur de ligne différente ? Définissez `rect.LineWidth = 2;` avant l’ajout.

#### Cas particulier : plusieurs rectangles

Si vous appelez `AddRectangle` à plusieurs reprises, chaque appel ajoute une nouvelle forme. Pour éviter le chevauchement, décalez les rectangles suivants :

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## Enregistrer le PDF modifié

### Pourquoi l’enregistrement est l’étape finale

Toutes les manipulations restent en mémoire jusqu’à ce que vous les persistiez. `Document.Save` écrit le nouveau contenu sur le disque (ou dans un flux). Il est possible d’écraser le fichier original, mais garder une sauvegarde (`output.pdf`) est plus sûr.

### Code

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- Vous pouvez également enregistrer dans un `MemoryStream` si vous devez envoyer le PDF via HTTP :

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## Exemple complet fonctionnel (prêt à copier‑coller)

En réunissant tous les morceaux, voici le programme final que vous pouvez exécuter dès maintenant :

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**Résultat attendu :** Ouvrez `output.pdf` et vous verrez un rectangle à bordure bleue ancré au coin inférieur‑gauche de la première page, dimensionné jusqu’à 500 × 700 points (ou plus petit si la page est petite).

## Questions fréquentes & astuces avancées

- **Puis‑je ajouter le rectangle à chaque page automatiquement ?**  
  Oui — parcourez `doc.Pages` et répétez l’appel `AddRectangle` pour chaque objet `Page`.

- **Et si je dois dessiner un cercle ou un polygone ?**  
  Aspose propose les méthodes `AddCircle`, `AddPolygon` et `AddPolyline`. La même logique de rectangle s’applique pour les boîtes englobantes.

- **Existe‑t‑il un moyen de positionner le rectangle par rapport au centre de la page ?**  
  Calculez les coordonnées du centre :  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **Des problèmes de performance avec de gros PDF ?**  
  Aspose charge les pages de façon paresseuse, mais si vous traitez des milliers de pages, envisagez d’utiliser `PdfExtractor` pour travailler sur des sous‑ensembles ou de diffuser le fichier afin de réduire l’empreinte mémoire.

## Conclusion

Vous savez maintenant **comment ajouter un rectangle** à un PDF avec C# en utilisant Aspose.Pdf.

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Add Images & Page Numbers to PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}