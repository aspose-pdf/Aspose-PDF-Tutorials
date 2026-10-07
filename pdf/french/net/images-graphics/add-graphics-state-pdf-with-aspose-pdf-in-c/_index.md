---
category: general
date: 2026-10-07
description: Ajoutez un état graphique PDF en utilisant Aspose.Pdf en C# pour modifier
  la transparence du PDF. Suivez ce guide étape par étape pour intégrer des états
  graphiques personnalisés et contrôler l'opacité.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: fr
lastmod: 2026-10-07
og_description: Ajoutez un état graphique PDF avec Aspose.Pdf en C#. Apprenez à modifier
  la transparence d’un PDF en créant un dictionnaire d’état graphique personnalisé.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Ajouter un état graphique PDF avec Aspose.Pdf – contrôler la transparence
  du PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Ajouter l'état graphique PDF avec Aspose.Pdf en C#
url: /fr/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un état graphique PDF avec Aspose.Pdf en C#

Si vous devez **ajouter un état graphique PDF** à un document, ce tutoriel vous montre exactement comment le faire avec Aspose.Pdf pour .NET. À la fin du guide, vous saurez également comment **modifier la transparence d'un PDF**, ce qui vous permet de définir des valeurs d'opacité personnalisées pour toute opération de dessin.

Travailler avec les états graphiques PDF vous permet de contrôler des paramètres tels que la largeur de ligne, le mode de fusion, et surtout pour cet article, la transparence du contenu. Les étapes ci‑dessous sont rédigées pour les développeurs à l’aise avec C# et qui souhaitent une solution prête à l’emploi sans fouiller dans la documentation officielle du SDK.

## Ce que vous allez apprendre

* Comment créer un nouveau dictionnaire d’état graphique et le remplir avec les entrées `CA`, `ca` et `BM`.  
* Comment insérer ce dictionnaire dans la ressource `ExtGState` de la page afin que le PDF le reconnaisse.  
* Comment les valeurs `ca` (trait) et `CA` (remplissage) affectent **la modification de la transparence PDF** pour les commandes de dessin suivantes.  
* Les pièges courants tels que les collisions de noms et la compatibilité des versions, ainsi que des astuces professionnelles pour étendre l’état graphique ultérieurement.

**Prérequis**

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7+).  
* Une licence valide d’Aspose.Pdf pour .NET (l’évaluation gratuite fonctionne pour les tests).  
* Visual Studio 2022 ou tout IDE C# de votre choix.  

---

## Étape 1 : Installer Aspose.Pdf pour .NET

Ajoutez le package NuGet à votre projet :

```bash
dotnet add package Aspose.Pdf
```

Le package inclut l’espace de noms `Aspose.Pdf` qui fournit les classes `Document`, `DictionaryEditor` et `CosPdfDictionary` utilisées plus tard.

> **Astuce :** Si vous prévoyez de traiter de nombreux PDF en lot, activez la **License** tôt dans `Program.cs` pour éviter le filigrane d’évaluation.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Étape 2 : Définir les chemins d’entrée et de sortie

Vous devez indiquer au SDK le PDF existant (`input.pdf`) et spécifier où le fichier modifié sera enregistré (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Pourquoi c’est important :** Utiliser des chemins absolus empêche le SDK de chercher dans le mauvais répertoire de travail, ce qui est une source fréquente de `FileNotFoundException`.

## Étape 3 : Ouvrir le PDF et localiser les ressources de la première page

Le dictionnaire `ExtGState` se trouve à l’intérieur du dictionnaire de ressources de chaque page. Nous modifierons la première page pour simplifier, mais la même approche fonctionne pour n’importe quel indice de page.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Cas particulier :** Si la page n’a aucune entrée `ExtGState`, vous devez la créer :

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Étape 4 : Construire un nouveau dictionnaire d’état graphique

Un état graphique est une collection de paires clé/valeur qui décrivent le comportement des opérations de dessin. Pour la transparence, nous avons besoin de trois clés :

| Clé | Signification | Valeur typique |
|-----|----------------|----------------|
| `CA` | Opacité du remplissage (0 = transparent, 1 = opaque) | `1` (pleinement opaque) |
| `ca` | Opacité du trait (même échelle) | `0.5` (50 % transparent) |
| `BM` | Mode de fusion (ex., `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Pourquoi ces valeurs ?**  
`ca = 0.5` rend tout tracé (lignes, bordures) à 50 % d’opacité, tandis que `CA = 1` laisse les formes remplies totalement opaques. Ajustez les deux nombres pour obtenir l’effet exact de **modification de la transparence PDF** dont vous avez besoin.

## Étape 5 : Insérer l’état graphique dans le dictionnaire ExtGState

Vous devez donner au nouvel état un nom unique (par ex., `GS0`). Si le nom existe déjà, Aspose.Pdf écrasera l’entrée existante, ce qui pourrait casser d’autres contenus qui en dépendent.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Maintenant, les ressources de la page connaissent `GS0`. Pour l’utiliser réellement, vous référenceriez l’état graphique dans un flux de contenu via l’opérateur `gs` (par ex., `GS0 gs`). Aspose.Pdf vous permet d’injecter des opérateurs PDF bruts si vous devez dessiner des formes personnalisées.

## Étape 6 : Enregistrer le PDF modifié

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

Le `output.pdf` résultant contient le même contenu visuel que l’original, mais toute commande de dessin ultérieure qui sélectionne `GS0` respectera les paramètres de transparence que vous avez définis.

### Résultat attendu

Ouvrez `output.pdf` dans Adobe Acrobat ou tout visualiseur PDF. Si vous ajoutez une nouvelle ligne tracée en utilisant l’état graphique `GS0` (par ex., via `pdfDocument.Pages[1].Contents.Add(...)`), la ligne apparaîtra semi‑transparente tandis que les remplissages resteront opaques. Cela démontre que vous avez réussi à **ajouter un état graphique PDF** et à **modifier la transparence du PDF**.

---

## Exemple complet exécutable

Voici le programme complet que vous pouvez copier‑coller dans une application console. Il inclut le chargement de la licence, la gestion des erreurs et des commentaires expliquant chaque étape non évidente.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Add Transparency to PDF with Aspose PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}