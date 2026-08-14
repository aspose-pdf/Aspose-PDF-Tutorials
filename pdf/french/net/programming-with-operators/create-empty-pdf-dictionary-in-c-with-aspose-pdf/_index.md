---
category: general
date: 2026-08-14
description: Créer un dictionnaire PDF vide en C# avec Aspose.Pdf – apprenez à ajouter
  un état graphique à la collection ExtGState et à modifier les PDF de façon programmatique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: fr
lastmod: 2026-08-14
og_description: Créer un dictionnaire PDF vide en C# avec Aspose.Pdf. Suivez ce guide
  complet pour ajouter un état graphique personnalisé à la collection ExtGState d’un
  PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Créer un dictionnaire PDF vide en C# – Guide pas à pas Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Créer un dictionnaire PDF vide en C# avec Aspose.Pdf
url: /fr/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un dictionnaire PDF vide en C# avec Aspose.Pdf

Si vous devez **créer des dictionnaires PDF vides** lors de la manipulation de fichiers PDF, ce guide vous montre exactement comment le faire en C# en utilisant la bibliothèque Aspose.Pdf. Que vous construisiez un état graphique personnalisé, ajoutiez une nouvelle ressource ou prépariez un modèle pour une utilisation ultérieure, les étapes ci‑dessous vous offrent une solution complète et exécutable.

Vous apprendrez comment charger un PDF, accéder au dictionnaire des ressources de la première page, créer un tout nouveau `CosPdfDictionary` et l’insérer dans la collection `ExtGState`. À la fin du tutoriel, vous disposerez d’un fichier `output.pdf` fonctionnel contenant le dictionnaire nouvellement créé.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.6+)
- Visual Studio 2022 ou tout autre IDE C# de votre choix
- Une licence Aspose.Pdf for .NET (ou une clé d’évaluation temporaire)
- Un PDF d’exemple nommé **input.pdf** placé dans un dossier que vous contrôlez (le chemin du dossier sera utilisé comme `dataDir`)

Aucun package NuGet supplémentaire n’est requis au‑delà de `Aspose.Pdf`.

## Étape 1 : Configurer le projet et référencer Aspose.Pdf

1. Créez un nouveau projet **Console App** dans Visual Studio.  
2. Ouvrez le **Gestionnaire de packages NuGet** et installez `Aspose.Pdf` :

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Ajoutez les directives `using` suivantes en haut de `Program.cs` :

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Pourquoi ces espaces de noms ?* `Aspose.Pdf` contient la classe principale `Document`, tandis que `Aspose.Pdf.Operators.Gfx` fournit `CosPdfDictionary`, `CosPdfNumber` et d’autres objets PDF de bas niveau nécessaires pour **créer des dictionnaires PDF vides**.

## Étape 2 : Charger le PDF source

La première opération consiste à charger le fichier PDF existant dans une instance `Document`. Cela vous donne accès à toutes les pages, ressources et dictionnaires de bas niveau.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Explication* : `Document` lit le fichier en mémoire et prépare les structures internes. L’instruction `using` garantit que le handle du fichier est libéré après le traitement.

## Étape 3 : Accéder au dictionnaire des ressources de la première page

Chaque page PDF possède un dictionnaire **Resources** qui regroupe polices, images, objets ExtGState et autres ressources partagées. Pour insérer un nouvel état graphique, nous devons modifier ce dictionnaire.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` est une classe d’aide qui vous permet de traiter un dictionnaire PDF comme un `Dictionary<string, object>` en C#.

## Étape 4 : Récupérer (ou créer) la collection ExtGState

`ExtGState` contient les objets d’état graphique tels que l’opacité, le mode de fusion et l’épaisseur de trait. Si le PDF source possède déjà une entrée `ExtGState`, nous la réutilisons ; sinon nous créons un nouveau dictionnaire vide.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Pourquoi cette vérification ?* Certains PDF omettent complètement l’entrée `ExtGState`. En gérant les deux cas, le tutoriel reste robuste quel que soit le fichier d’entrée.

## Étape 5 : **Créer un dictionnaire PDF vide** pour un nouvel état graphique

Nous allons maintenant **créer des dictionnaires PDF vides** qui définissent les paramètres de l’état graphique. Le dictionnaire commence vide, puis nous y ajoutons les clés requises :

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Ce que fait chaque entrée

| Clé | Type | Signification |
|-----|------|----------------|
| **CA** | `CosPdfNumber` | Opacité du trait (plage 0‑1). |
| **ca** | `CosPdfNumber` | Opacité du remplissage (plage 0‑1). |
| **BM** | `CosPdfName`   | Mode de fusion ; `"Normal"` est le plus courant. |

Comme nous avons commencé avec un **dictionnaire PDF vide**, nous contrôlons entièrement les entrées ajoutées. Vous pouvez étendre ce dictionnaire avec d’autres paramètres d’état graphique tels que `LW` (épaisseur de trait) ou `LC` (extrémité de trait) selon vos besoins.

## Étape 6 : Insérer le nouvel état graphique dans ExtGState

Le dictionnaire `ExtGState` fonctionne comme une table de correspondance où chaque entrée est identifiée par un nom (par ex., `GS0`, `GS1`). Nous ajoutons notre dictionnaire fraîchement construit sous une clé unique.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Si vous prévoyez d’ajouter plusieurs états, incrémentez le suffixe (`GS1`, `GS2`, …) afin d’éviter les collisions de noms.

## Étape 7 : Enregistrer le PDF modifié

Enfin, écrivez les modifications sur le disque. La méthode `Save` sérialise automatiquement les dictionnaires mis à jour.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Ouvrez `output.pdf` dans n’importe quel lecteur PDF et inspectez l’entrée **Resources → ExtGState** (la plupart des lecteurs la masquent, mais des outils comme Adobe Acrobat Preflight ou PDF‑Tron peuvent la révéler). Vous devriez voir une entrée `GS0` contenant les valeurs d’opacité et de mode de fusion que vous avez définies.

## Exemple complet fonctionnel

En rassemblant tous les éléments, voici le programme complet que vous pouvez copier‑coller dans `Program.cs` et exécuter :

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Résultat attendu** – La console affiche une ligne de confirmation, et `output.pdf` contient la nouvelle entrée `GS0` sous `ExtGState`. Lorsque vous rendez une page qui référence `GS0` (par ex., via l’opérateur de flux de contenu `gs`), les traits seront totalement opaques tandis que les remplissages seront à 50 % de transparence.

## Questions fréquentes et gestion des cas limites

| Question | Réponse |
|----------|---------|
| *Et si le PDF comporte plusieurs pages ?* | L’exemple cible la première page (`Pages[1]`). Pour affecter toutes les pages, parcourez `pdfDocument.Pages` et répétez les étapes 3‑5 pour les ressources de chaque page. |
| *Puis‑je ajouter le dictionnaire à une page qui possède déjà une entrée ExtGState nommée « GS0 » ?* | Oui, mais vous devez utiliser une clé différente (`GS1`, `GS2`, …) afin de ne pas écraser l’entrée existante. |
| *Est‑il sûr de modifier le dictionnaire après l’enregistrement ?* | Une fois que vous appelez `Save`, la représentation en mémoire est détachée du fichier. Vous pouvez continuer à modifier l’objet `Document` et appeler à nouveau `Save` si nécessaire. |
| *Ai‑je besoin d’une licence pour Aspose.Pdf afin d’utiliser ` |  |

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment créer des lignes pointillées dans les PDF avec Aspose.PDF pour .NET : guide étape par étape](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Comment supprimer des graphiques des PDF avec Aspose.PDF .NET : guide complet](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Comment créer des PDF multi‑couches avec Aspose.PDF pour .NET : guide complet](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}