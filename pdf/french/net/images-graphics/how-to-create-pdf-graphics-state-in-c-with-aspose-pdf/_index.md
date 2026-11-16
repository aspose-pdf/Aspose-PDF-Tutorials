---
category: general
date: 2026-11-16
description: Apprenez à créer un état graphique PDF en C# avec Aspose.Pdf. Ce guide
  couvre l’opacité, le mode de fusion et un exemple complet de code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: fr
lastmod: 2026-11-16
og_description: Créez l’état graphique PDF en C# avec Aspose.Pdf. Suivez ce tutoriel
  complet pour définir l’opacité et le mode de fusion par programmation.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Créer l'état graphique PDF en C# – guide pas à pas Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Comment créer un état graphique PDF en C# avec Aspose.Pdf
url: /fr/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un état graphique PDF en C# avec Aspose.Pdf

Si vous devez **créer un état graphique PDF** dans un projet .NET, ce tutoriel vous montre exactement comment le faire avec Aspose.Pdf. Que vous souhaitiez contrôler l'opacité, changer le mode de fusion, ou réutiliser un état graphique personnalisé sur plusieurs pages, les étapes ci‑dessous vous offrent une solution complète, prête à l'emploi.

Dans ce guide, vous apprendrez comment accéder aux ressources de la page, ajouter une entrée **ExtGState**, et enregistrer les modifications dans un nouveau fichier. L'exemple fonctionne avec Aspose.Pdf 23.12 (ou ultérieur) et cible .NET 6+, mais les concepts s'appliquent également aux versions antérieures.

## Prérequis

* Visual Studio 2022 (ou tout IDE C#) avec le SDK .NET 6 installé.  
* Une licence Aspose.Pdf pour .NET ou une clé d'évaluation temporaire.  
* Un fichier PDF nommé `input.pdf` placé dans un dossier que vous pouvez référencer depuis le code.  

Aucun paquet NuGet supplémentaire n'est requis au-delà de `Aspose.Pdf`.

## Ce que couvre le tutoriel

* Chargement d'un document PDF existant.  
* Navigation vers le dictionnaire des ressources de la première page.  
* Création d'un nouveau dictionnaire d'état graphique qui définit l'opacité du trait (`CA`), l'opacité du remplissage (`ca`) et le mode de fusion (`BM`).  
* Ajout du nouvel état graphique à la collection **ExtGState** avec un nom personnalisé (`GS0`).  
* Enregistrement du PDF mis à jour afin que les commandes de dessin ultérieures puissent référencer le nouvel état.

À la fin du tutoriel, vous serez capable de **créer des objets d'état graphique PDF** programmétiquement et de les réutiliser dans toute opération de dessin.

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez une nouvelle application console (ou intégrez le code dans un projet existant). Ajoutez la référence Aspose.Pdf et incluez les espaces de noms requis :

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Astuce :** Si vous utilisez la version d'évaluation gratuite, ajoutez `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` avant de charger le document afin d'éviter les messages de filigrane.

## Étape 2 : Charger le document PDF

L'ouverture du fichier est simple. La classe `Document` représente l'ensemble du PDF et vous donne accès à ses pages et à ses ressources.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Placer le code à l'intérieur d'un bloc `using` garantit que le handle du fichier est libéré après l'opération, ce qui est essentiel pour la **manipulation PDF en C#** dans les services de production.

## Étape 3 : Récupérer le dictionnaire des ressources de la première page

Chaque page PDF possède un dictionnaire *Resources* qui stocke les polices, les images et les états graphiques. Nous avons besoin d'un `DictionaryEditor` pour modifier cette structure.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Si le PDF contient déjà une entrée `ExtGState`, `resourcesEditor["ExtGState"]` la renverra ; sinon, Aspose.Pdf crée un dictionnaire vide pour nous lorsque nous ajoutons la première entrée.

## Étape 4 : Accéder ou créer le dictionnaire ExtGState

Le dictionnaire **ExtGState** contient des objets d'état graphique nommés. Nous récupérons soit un existant, soit créons un nouveau conteneur.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Lorsque `ExtGState` n'existe pas, `resourcesEditor["ExtGState"]` renvoie automatiquement un nouveau dictionnaire vide, garantissant que le code fonctionne pour tout PDF.

## Étape 5 : Construire le nouveau dictionnaire d'état graphique

Un état graphique est un `CosPdfDictionary` avec des clés spécifiques :

* `CA` – opacité du trait (0‑1)  
* `ca` – opacité du remplissage (0‑1)  
* `BM` – mode de fusion (`Normal`, `Multiply`, etc.)

Nous créons un dictionnaire vide, le remplissons, puis l'ajoutons à `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Vous pouvez changer `0.5` à n'importe quelle valeur entre `0` et `1` pour ajuster l'opacité du remplissage, ou remplacer `"Normal"` par `"Multiply"` pour un **mode de fusion PDF** différent. Cette flexibilité explique pourquoi créer un état graphique personnalisé est une technique puissante dans la gestion des **états graphiques Aspose.Pdf**.

## Étape 6 : Enregistrer l'état graphique avec un nom

Les flux de contenu PDF font référence aux états graphiques par leur nom. Ici nous utilisons `GS0`, mais tout nom unique fonctionne.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Si vous avez besoin de plusieurs états, répétez l'étape de création avec des paramètres différents et ajoutez-les sous les noms `GS1`, `GS2`, etc. Ce schéma s'adapte bien aux documents complexes qui nécessitent des réglages d'opacité ou de fusion variés sur différentes couches.

## Étape 7 : Enregistrer le PDF modifié

Enfin, écrivez le document mis à jour dans un nouveau fichier. Conserver l'original intact facilite le débogage.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Après exécution, `output.pdf` contient une entrée `ExtGState` nommée `GS0`. Tout opérateur de dessin ultérieur peut la référencer en utilisant l'opérateur `gs` (par ex., `GS0 gs` dans un flux de contenu).  

> **Pourquoi c'est important :** En créant un état graphique réutilisable, vous évitez de répéter les réglages d'opacité et de fusion pour chaque commande de dessin, ce qui améliore à la fois les performances et la maintenabilité.

## Utiliser le nouvel état graphique dans un flux de contenu (optionnel)

Si vous souhaitez voir l'effet immédiatement, vous pouvez ajouter un simple rectangle qui utilise l'état que nous venons de créer :

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Le rectangle sera dessiné avec 50 % d'opacité de remplissage tandis que le trait restera entièrement opaque, exactement comme défini dans le dictionnaire **create PDF graphics state**.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Entrée `ExtGState` non trouvée | Certains PDF omettent complètement le dictionnaire. | Le `DictionaryEditor` le crée automatiquement lorsqu'on ajoute la première entrée, donc aucune vérification supplémentaire n'est nécessaire. |
| Valeurs d'opacité > 1 ou < 0 | La spécification PDF limite l'opacité à la plage `[0,1]`. | Limitez les valeurs avant de créer `CosPdfNumber`. |
| Erreur de frappe du mode de fusion | Les noms de mode de fusion PDF sont sensibles à la casse. | Utilisez les noms exacts comme `"Normal"`, `"Multiply"`, `"Screen"`. |
| Filigrane de licence | La version d'évaluation ajoute un filigrane sur la première page. | Appliquez un fichier de licence valide avant d'ouvrir le document. |

Traiter ces cas limites garantit que votre implémentation **create PDF graphics state** fonctionne de manière fiable sur différentes sources PDF.

## Exemple complet, exécutable

Voici un programme autonome que vous pouvez copier, coller et exécuter. Remplacez `YOUR_DIRECTORY` par le chemin réel d'un dossier sur votre machine.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un état graphique personnalisé dans un PDF avec Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Ajouter un état graphique à un PDF en utilisant Aspose.PDF pour .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [Comment créer un état graphique vide dans un PDF avec C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}