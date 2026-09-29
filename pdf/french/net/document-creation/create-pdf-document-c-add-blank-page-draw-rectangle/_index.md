---
category: general
date: 2026-02-12
description: Créez rapidement un document PDF en C# en ajoutant une page vierge, en
  vérifiant la taille de la page, en dessinant un rectangle et en enregistrant le
  fichier. Guide étape par étape avec Aspose.Pdf.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- save pdf file c#
- check pdf page size
language: fr
og_description: Créez rapidement un document PDF en C# en ajoutant une page blanche,
  en vérifiant la taille de la page, en dessinant un rectangle et en enregistrant
  le fichier. Tutoriel complet avec code.
og_title: Créer un document PDF C# – Ajouter une page blanche et dessiner un rectangle
tags:
- PDF
- C#
- Aspose.Pdf
- Document Generation
title: Créer un document PDF C# – Ajouter une page vierge et dessiner un rectangle
url: /fr/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/
---

final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document PDF C# – Ajouter une page vierge et dessiner un rectangle

Vous avez déjà eu besoin de **créer un document PDF C#** à partir de zéro et vous vous êtes demandé comment ajouter une page vierge, vérifier les dimensions de la page, dessiner une forme, puis enfin l’enregistrer ? Vous n’êtes pas seul. De nombreux développeurs rencontrent exactement ce blocage lorsqu’ils automatisent des rapports, factures ou tout type de sortie imprimable.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre exactement comment **ajouter une page vierge PDF**, **vérifier la taille d’une page PDF**, **dessiner un rectangle PDF**, et **enregistrer un fichier PDF C#** en utilisant la bibliothèque Aspose.Pdf. À la fin, vous disposerez d’un fichier PDF prêt à l’emploi avec un rectangle à bordure bleue parfaitement placé sur une page au format A4.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- **.NET 6.0** ou version ultérieure (le code fonctionne également avec le .NET Framework 4.6+).  
- **Aspose.Pdf for .NET** installé via NuGet (`Install-Package Aspose.Pdf`).  
- Une compréhension de base de la syntaxe C# — rien de compliqué.  
- Un IDE de votre choix (Visual Studio, Rider, VS Code, etc.).

> **Astuce :** Si vous utilisez Visual Studio, le gestionnaire de packages NuGet rend l’ajout d’Aspose.Pdf très simple — il suffit de rechercher “Aspose.Pdf” et de cliquer sur Installer.

## Étape 1 : Créer un document PDF C# – Initialiser le Document

La première chose dont vous avez besoin est un nouvel objet `Document`. Considérez‑le comme une toile vierge où chaque opération ultérieure peindra son contenu.

```csharp
using Aspose.Pdf;
using System;

// Step 1: Create a new PDF document
var pdfDocument = new Document();
```

> **Pourquoi c’est important :** La classe `Document` est le point d’entrée pour chaque opération PDF. L’instancier alloue les structures internes nécessaires pour gérer les pages, les ressources et les métadonnées.

## Étape 2 : Ajouter une page vierge PDF – Ajouter une nouvelle page

Un PDF sans pages est comme un livre sans feuilles — inutile. Ajouter une page vierge nous donne quelque chose sur lequel dessiner.

```csharp
// Step 2: Add a blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Que se passe‑t‑il en coulisses ?** `Pages.Add()` crée une page qui hérite de la taille par défaut (A4 pour la plupart des paramètres). Vous pourrez modifier ses dimensions plus tard si vous avez besoin d’une taille personnalisée.

## Étape 3 : Définir le rectangle et vérifier la taille de la page PDF

Avant de dessiner, nous devons définir où le rectangle sera placé et nous assurer qu’il tient dans la page. C’est ici que le mot‑clé **check PDF page size** entre en jeu.

```csharp
// Step 3: Define rectangle position and size (fits within a standard A4 page)
var rectangle = new Rectangle(50, 50, 550, 750);

// Step 3b: Verify that the rectangle fits inside the page boundaries
bool fitsWidth = page.PageInfo.Width >= rectangle.Width;
bool fitsHeight = page.PageInfo.Height >= rectangle.Height;

if (!fitsWidth || !fitsHeight)
{
    throw new InvalidOperationException(
        $"Rectangle (W:{rectangle.Width}, H:{rectangle.Height}) exceeds page size (W:{page.PageInfo.Width}, H:{page.PageInfo.Height}).");
}
```

> **Pourquoi vérifier :** Certains PDF utilisent des tailles de page personnalisées (Letter, Legal, etc.). Si le rectangle est plus grand que la page, l’opération de dessin sera rognée ou générera une erreur. Cette vérification rend le code robuste face à d’éventuels changements de taille de page.

## Étape 4 : Dessiner un rectangle PDF – Rendre la forme

Place maintenant la partie amusante : dessiner réellement un rectangle avec une bordure bleue et un remplissage transparent. Cela illustre la capacité **draw rectangle PDF**.

```csharp
// Step 4: Draw the rectangle with a blue border and a transparent fill
page.AddRectangle(
    rectangle,
    Color.Blue,          // Border color
    Color.Transparent    // Fill color (transparent)
);
```

> **Comment ça fonctionne :** `AddRectangle` prend trois arguments — la géométrie du rectangle, la couleur du trait (bordure) et la couleur de remplissage. Utiliser `Color.Transparent` garantit que l’intérieur reste vide, laissant le contenu sous‑jacent visible.

## Étape 5 : Enregistrer le fichier PDF C# – Persister le Document sur le disque

Enfin, nous écrivons le document dans un fichier. C’est l’étape **save pdf file c#** qui finalise le tout.

```csharp
// Step 5: Save the PDF to a file
string outputPath = @"C:\Temp\shape.pdf"; // Adjust the path as needed
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved successfully to {outputPath}");
```

> **Conseil :** Enveloppez tout le processus dans un bloc `using` (ou appelez `pdfDocument.Dispose()`) pour libérer rapidement les ressources natives, surtout si vous générez de nombreux PDF dans une boucle.

## Exemple complet et exécutable

En assemblant toutes les pièces, voici le programme complet que vous pouvez copier‑coller dans une application console :

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // Add a blank page
            Page page = pdfDocument.Pages.Add();

            // Define rectangle (fits within a standard A4 page)
            var rectangle = new Rectangle(50, 50, 550, 750);

            // Ensure the rectangle fits inside the page boundaries
            if (page.PageInfo.Width >= rectangle.Width && page.PageInfo.Height >= rectangle.Height)
            {
                // Draw the rectangle with a blue border and a transparent fill
                page.AddRectangle(rectangle, Color.Blue, Color.Transparent);
            }
            else
            {
                Console.WriteLine("Rectangle does not fit on the page. Adjust dimensions.");
                return;
            }

            // Save the PDF to a file
            string outputPath = @"C:\Temp\shape.pdf"; // Change to your desired folder
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF created at: {outputPath}");
        }
    }
}
```

### Résultat attendu

Ouvrez `shape.pdf` et vous verrez une seule page au format A4 avec un rectangle à bordure bleue positionné à 50 pts du bord gauche et du bord inférieur. L’intérieur du rectangle est transparent, de sorte que le fond de la page reste visible.

![exemple de création de document pdf c# montrant le rectangle](https://example.com/placeholder.png "exemple de création de document pdf c#")

*(Texte alternatif de l’image : **exemple de création de document pdf c# montrant le rectangle**)  

Si vous remplacez `Color.Blue` par `Color.Red` ou ajustez les coordonnées, le rectangle reflétera ces modifications — n’hésitez pas à expérimenter.

## Questions fréquentes & cas particuliers

### Et si j’ai besoin d’une taille de page différente ?

Vous pouvez définir les dimensions de la page avant d’ajouter du contenu :

```csharp
Page customPage = pdfDocument.Pages.Add();
customPage.SetPageSize(PageSize.Letter.Width, PageSize.Letter.Height);
```

N’oubliez pas de réexécuter la logique **check PDF page size** après avoir modifié les dimensions.

### Puis‑je dessiner d’autres formes ?

Absolument. Aspose.Pdf propose `AddCircle`, `AddEllipse`, `AddLine` et même des objets `Path` libres. Le même schéma—définir la géométrie, vérifier les limites, puis appeler la méthode `Add*` appropriée—s’applique.

### Comment remplir le rectangle avec une couleur ?

Remplacez `Color.Transparent` par n’importe quelle couleur opaque :

```csharp
page.AddRectangle(rectangle, Color.Blue, Color.LightGray);
```

### Existe‑t‑il un moyen d’ajouter du texte à l’intérieur du rectangle ?

Bien sûr. Après avoir dessiné le rectangle, ajoutez un `TextFragment` positionné à l’intérieur des coordonnées du rectangle :

```csharp
var tf = new TextFragment("Hello, world!");
tf.Rect = new Rectangle(60, 60, 540, 730); // Slightly inset
page.Paragraphs.Add(tf);
```

## Conclusion

Nous venons de vous montrer comment **créer un document PDF C#**, **ajouter une page vierge PDF**, **vérifier la taille d’une page PDF**, **dessiner un rectangle PDF**, et enfin **enregistrer un fichier PDF C#**—le tout dans un exemple concis, de bout en bout. Le code est prêt à être exécuté, les explications couvrent le *pourquoi* de chaque étape, et vous disposez maintenant d’une base solide pour des tâches de génération PDF plus sophistiquées.

Prêt pour le prochain défi ? Essayez de superposer plusieurs formes, d’insérer des images ou de générer des tableaux—tout suit le même modèle que nous avons utilisé ici. Et si vous devez un jour ajuster les dimensions de page ou passer à une autre bibliothèque PDF, les concepts restent les mêmes.

Bon codage, et que vos PDF se rendent toujours exactement comme vous le souhaitez !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}