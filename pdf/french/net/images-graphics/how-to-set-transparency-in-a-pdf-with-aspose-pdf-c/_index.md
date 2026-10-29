---
category: general
date: 2026-10-13
description: Apprenez à définir la transparence dans un PDF avec Aspose.Pdf pour C#.
  Découvrez également comment enregistrer le PDF modifié et modifier l'alpha de remplissage.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: fr
lastmod: 2026-10-13
og_description: Comment définir la transparence dans un PDF avec Aspose.Pdf pour C#.
  Suivez ce guide pour modifier les ressources PDF, changer l'alpha de remplissage
  et enregistrer les fichiers PDF modifiés.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Comment définir la transparence dans un PDF avec Aspose.Pdf C# – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Comment définir la transparence dans un PDF avec Aspose.Pdf C#
url: /fr/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir la transparence dans un PDF avec Aspose.Pdf C#

Si vous devez définir la transparence dans un PDF en utilisant C#, ce tutoriel montre les étapes exactes. Vous apprendrez également comment enregistrer les fichiers PDF modifiés et modifier l’alpha de remplissage sans quitter l’environnement Aspose.Pdf.

Le guide parcourt le chargement d’un document, la modification des ressources PDF, la création d’un état graphique qui définit l’opacité de remplissage, et la persistance des modifications. Aucun outil externe n’est requis ; tout s’exécute à l’intérieur d’un projet .NET standard.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou version ultérieure installé  
* Une licence valide d’Aspose.Pdf pour .NET (ou une clé d’évaluation gratuite)  
* Un fichier PDF d’entrée situé dans un répertoire connu  

Vous pouvez ajouter le package Aspose.Pdf via NuGet :

```bash
dotnet add package Aspose.Pdf
```

## Comment définir la transparence dans un PDF

Cette section contient l’implémentation principale. Chaque étape explique **pourquoi** le code est nécessaire, pas seulement **ce que** fait le code.

### Étape 1 : Charger le document PDF

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Pourquoi cette étape ?*  
`Document` représente l’ensemble du fichier PDF en mémoire. L’ouverture du fichier vous donne accès aux pages, aux ressources et aux objets de bas niveau que vous allez modifier.

### Étape 2 : Modifier les ressources PDF pour ajouter un état graphique

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*Pourquoi cette étape ?*  
Les pages PDF stockent des objets réutilisables — polices, images et états graphiques—dans un dictionnaire de ressources. L’entrée `ExtGState` contient les paramètres de transparence. En modifiant ce dictionnaire, vous pouvez introduire un nouvel état que la page pourra référencer.

### Étape 3 : Modifier l’alpha de remplissage et définir l’opacité de remplissage

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Pourquoi cette étape ?*  
`ca` contrôle **l’opacité de remplissage**, tandis que `CA` contrôle **l’opacité du trait**. Définir `ca` à `0.5` rend les formes remplies à 50 % transparentes. L’entrée `BM` sélectionne le mode de fusion ; `"Normal"` est le choix le plus courant pour une transparence standard.

### Étape 4 : Ajouter le nouvel état graphique au dictionnaire ExtGState

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*Pourquoi cette étape ?*  
Nommer l’état graphique (`"GS0"`) permet aux flux de contenu de la page de le référencer avec l’opérateur `gs`. Après cet enregistrement, la page peut appliquer la transparence que vous venez de définir.

### Étape 5 : (Facultatif) Appliquer l’état graphique dans un flux de contenu

Si vous souhaitez dessiner un rectangle en utilisant la nouvelle opacité de remplissage, ajoutez ce qui suit après les étapes précédentes :

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*Pourquoi cette étape ?*  
Les opérateurs `q`/`Q` sauvegardent et restaurent l’état graphique, garantissant que la transparence n’affecte que les commandes de dessin prévues. L’opérateur `gs` passe à l’état graphique nommé `"GS0"`.

### Étape 6 : Enregistrer le PDF modifié

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Pourquoi cette étape ?*  
L’enregistrement écrit le dictionnaire de ressources mis à jour et les nouveaux flux de contenu sur le disque. Le fichier résultant (`output.pdf`) contient le rectangle transparent défini à l’étape précédente.

## Exemple complet exécutable

En assemblant les morceaux, voici un programme complet que vous pouvez compiler et exécuter :

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Résultat attendu** – `output.pdf` montre un rectangle rempli d’une couleur violet clair à 50 % de transparence, laissant le contenu d’arrière‑plan partiellement visible.

## Questions fréquentes et cas particuliers

* **Puis‑je modifier l’opacité du trait au lieu de l’opacité du remplissage ?**  
  Définissez la valeur de `CA` (lettres majuscules) à un nombre compris entre `0` (totalement transparent) et `1` (totalement opaque). L’exemple fixe déjà `CA` à `1`, ce qui signifie que les traits restent opaques.

* **Que se passe‑t‑il si la page ne possède pas encore de dictionnaire ExtGState ?**  
  `resourceEditor["ExtGState"]` créera automatiquement un dictionnaire vide. L’ajout de `"GS0"` fonctionne de la même manière.

* **L’état graphique est‑il réutilisable sur plusieurs pages ?**  
  Oui. Une fois l’entrée ajoutée au dictionnaire de ressources du document, toute page qui référence `"GS0"` héritera des mêmes paramètres de transparence.

* **En quoi cette approche diffère‑t‑elle de l’utilisation de l’API haut niveau `Graphics` ?**  
  Modifier le dictionnaire de ressources de bas niveau vous donne un contrôle précis sur les internes du PDF et produit des fichiers plus petits car cela évite l’insertion d’objets supplémentaires.

## Conclusion

Vous savez maintenant **comment définir la transparence dans un PDF** avec Aspose.Pdf pour C#. Le tutoriel a couvert la modification des ressources PDF, le changement de l’alpha de remplissage, la définition de l’opacité de remplissage et l’enregistrement du PDF modifié. Avec cette base, vous pouvez expérimenter différents modes de fusion, appliquer la transparence au texte, ou créer des états graphiques réutilisables pour des documents complexes.

### Prochaines étapes

* Explorez d’autres modes de fusion (`Multiply`, `Screen`, etc.) en modifiant l’entrée `BM`.  
* Ajustez l’alpha du trait (`CA`) pour créer des contours semi‑transparents.  
* Combinez plusieurs états graphiques pour constituer une bibliothèque d’effets visuels réutilisables.  

N’hésitez pas à partager vos résultats ou à poser des questions dans les commentaires. Bon codage !

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code fonctionnels complets avec des explications étape par étape pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}