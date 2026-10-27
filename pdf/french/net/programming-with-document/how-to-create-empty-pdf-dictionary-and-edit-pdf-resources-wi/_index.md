---
category: general
date: 2026-10-26
description: Apprenez à créer un dictionnaire PDF vide et à modifier les ressources
  PDF en utilisant Aspose.PDF pour C#. Guide étape par étape avec un exemple complet
  de code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: fr
lastmod: 2026-10-26
og_description: Créez un dictionnaire PDF vide et modifiez les ressources PDF avec
  Aspose.PDF pour C#. Suivez ce tutoriel complet pour modifier les états graphiques
  dans les PDF.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Créer un dictionnaire PDF vide et modifier les ressources PDF en C# – Guide
  Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Comment créer un dictionnaire PDF vide et modifier les ressources PDF avec
  Aspose.PDF en C#
url: /fr/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un dictionnaire PDF vide et modifier les ressources PDF avec Aspose.PDF en C#

Si vous devez **créer un dictionnaire PDF vide** puis **modifier les ressources PDF** dans une application C#, ce guide vous montre les étapes exactes. Vous verrez un exemple complet et exécutable qui ajoute un état graphique personnalisé à la première page d'un PDF existant.

Travailler avec des objets PDF de bas niveau peut sembler intimidant, mais Aspose.PDF fournit une API claire pour la manipulation des dictionnaires. À la fin de ce tutoriel, vous comprendrez pourquoi chaque opération est importante et comment adapter le code à d'autres types de ressources.

## Prérequis

* .NET 6.0 (ou ultérieur) installé.
* Une copie sous licence de **Aspose.PDF for .NET** – l'essai gratuit fonctionne pour les tests.
* Un IDE tel que Visual Studio 2022.
* Un fichier PDF nommé `input.pdf` placé dans un dossier que vous pouvez référencer depuis le code.

Aucun package NuGet supplémentaire n'est requis au-delà de `Aspose.Pdf`.

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez un nouveau projet console et ajoutez le package Aspose.PDF :

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

Dans `Program.cs`, importez les espaces de noms que vous utiliserez :

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Ces importations exposent les classes `Document`, `DictionaryEditor` et COS (Canonical Object Structure) qui vous permettent de **créer des dictionnaires PDF vides** et de modifier les dictionnaires de ressources existants.

## Étape 2 : Définir le dossier contenant les fichiers PDF

Spécifiez le répertoire qui contient `input.pdf`. Utiliser un chemin absolu évite les ambiguïtés lorsque le programme s'exécute depuis un répertoire de travail différent.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Remplacez `C:\PdfDemo\` par le chemin sur votre machine. Conserver le chemin dans une variable facilite la réutilisation pour les fichiers d'entrée et de sortie.

## Étape 3 : Ouvrir le document PDF source

Chargez le PDF que vous souhaitez modifier à l'intérieur d'un bloc `using` afin que le handle du fichier soit libéré automatiquement.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

L'ouverture du document vous donne accès à sa collection de pages, aux dictionnaires de ressources et aux objets COS de bas niveau.

## Étape 4 : Accéder à la première page et à son dictionnaire de ressources

La première page est indexée avec `1` (les pages PDF sont indexées à partir de 1). Récupérez le dictionnaire `Resources` de la page et encapsulez-le dans un `DictionaryEditor` pour permettre une édition sécurisée.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` abstrait la structure COS sous-jacente, vous permettant de lire ou de créer des entrées sans corrompre le PDF.

## Étape 5 : **Créer un dictionnaire PDF vide** pour un nouvel état graphique

Un état graphique contrôle la transparence, le mode de fusion et d'autres paramètres de dessin. Pour ajouter un état personnalisé, vous avez d'abord besoin d'un dictionnaire vide, puis le remplir avec les entrées requises.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

L'appel à `CreateEmptyDictionary` constitue le cœur de la **création de dictionnaires PDF vides**. Il renvoie un dictionnaire COS qui appartient au même document, garantissant l'intégrité des références croisées.

### Remplir les entrées de l'état graphique

Ajoutez les clés standard :

* `CA` – constante alpha de tracé (plage 0 – 1).
* `ca` – constante alpha de remplissage.
* `BM` – nom du mode de fusion.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Chaque entrée est ajoutée au dictionnaire vide que vous venez de créer. En séparant la définition de la boucle d'insertion, vous maintenez le code lisible et facilitez son extension avec des clés supplémentaires ultérieurement.

### Enregistrer le nouvel état graphique dans le dictionnaire de ressources

Attribuez un nom à l'état (`GS0`) et ajoutez-le au dictionnaire `ExtGState` qui se trouve dans les ressources de la page.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Le dictionnaire de ressources de la page contient désormais une référence à l'état graphique personnalisé, que vous pourrez appliquer ultérieurement aux flux de contenu.

## Étape 6 : Enregistrer le PDF mis à jour

Enfin, écrivez le document modifié dans un nouveau fichier. Conserver l'original intact vous aide à vérifier les modifications.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

Lorsque vous ouvrez `output.pdf` dans un visualiseur qui prend en charge l'inspection des états graphiques (par ex., Adobe Acrobat Pro), vous verrez que le dictionnaire `ExtGState` contient une entrée nommée `GS0` avec les valeurs que vous avez définies.

## Code source complet

Assembler toutes les pièces donne un programme autonome :

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Sortie attendue

L'exécution du programme affiche :

```
PDF updated successfully.
```

et crée `output.pdf` dans le même dossier. L'ouverture du fichier révèle une nouvelle entrée sous **Resources → ExtGState → GS0** avec les paramètres que vous avez définis.

## Variations courantes et cas limites

| Situation | Comment adapter le code |
|-----------|--------------------------|
| **Multiple pages** need the same graphics state | Créez le dictionnaire une fois, puis ajoutez la même référence `GS0` à chaque dictionnaire `ExtGState` de chaque page. |
| **Different blend mode** (e.g., `Multiply`) | Changez la valeur `CosPdfName("Normal")` en `CosPdfName("Multiply")`. |
| **No existing ExtGState dictionary** | Avant d'accéder à `resourcesEditor["ExtGState"]`, vérifiez `resourcesEditor.ContainsKey("ExtGState")`. Si elle est absente, créez un nouveau dictionnaire vide et ajoutez-le à `firstPage.Resources`. |
| **Large PDFs** cause memory pressure | Utilisez la surcharge de `PdfDocument.Load` qui diffuse les pages, ou traitez les pages une par une à l'intérieur du bloc `using`. |
| **Need to edit other resources** (fonts, XObjects) | Remplacez `"ExtGState"` par `"Font"` ou `"XObject"` dans la recherche `resourcesEditor`, puis suivez le même modèle de création d'un dictionnaire vide et de le remplir. |

Ces variations montrent comment le même modèle de **création d'un dictionnaire PDF vide** s'applique à tout type de ressource que vous souhaitez **modifier les ressources PDF**.

## Astuces professionnelles

* **Valider le résultat** – après l'enregistrement, ouvrez le PDF dans un outil capable d'afficher le dictionnaire de ressources brut (par ex., le `PDFDebugger` de PDF‑Box) pour vous assurer que l'entrée existe.
* **Réutiliser les dictionnaires** – si vous ajoutez le même état graphique à de nombreuses pages, stockez le dictionnaire dans une variable et référencez‑le plutôt que de le recréer à chaque fois.
* **Compatibilité des versions** – le code fonctionne avec Aspose.PDF 23.12 et versions ultérieures. Les versions antérieures peuvent nécessiter `CosDictionary` au lieu de `CosPdfDictionary`.

## Conclusion

Vous savez maintenant comment **créer des objets dictionnaire PDF vides** et **modifier les ressources PDF** en utilisant Aspose.PDF pour C#. Le tutoriel a couvert l'ouverture d'un document, l'accès au dictionnaire de ressources de la page, la création d'un état graphique personnalisé, son enregistrement et la sauvegarde du résultat. À partir de là, vous pouvez expérimenter avec d'autres types de ressources, combiner plusieurs états graphiques, ou intégrer la technique dans un pipeline de traitement PDF plus vaste.

---

*Prêt à explorer davantage ? Essayez d'ajouter un **ExtGState** personnalisé à un flux de contenu, ou de manipuler le dictionnaire **Font** pour incorporer de nouvelles polices. Les deux suivent le même modèle de création d'un dictionnaire vide et de modification des ressources PDF.*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Modifier le dictionnaire de ressources PDF avec Aspose.PDF – Guide C#](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Créer un état graphique personnalisé dans un PDF avec Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Comment créer un état graphique vide dans un PDF avec C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}