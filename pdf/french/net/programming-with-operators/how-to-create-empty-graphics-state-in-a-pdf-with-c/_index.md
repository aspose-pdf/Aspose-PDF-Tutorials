---
category: general
date: 2026-08-17
description: Créez un état graphique vide dans un PDF en utilisant C# et Aspose.Pdf.
  Suivez ce guide étape par étape pour modifier les ressources ExtGState en toute
  sécurité.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: fr
lastmod: 2026-08-17
og_description: Créer un état graphique vide dans un PDF en C#. Ce tutoriel montre
  comment modifier les ressources ExtGState avec Aspose.Pdf pour des modifications
  fiables de PDF.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Créer un état graphique vide dans un PDF avec C# – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Comment créer un état graphique vide dans un PDF avec C#
url: /fr/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un état graphique vide dans un PDF avec C#

Si vous devez **créer un état graphique vide** dans un PDF, ce guide vous montre exactement comment le faire avec C# et Aspose.Pdf. Vous verrez un exemple complet et exécutable qui ajoute une nouvelle entrée au dictionnaire ExtGState de la page sans affecter le contenu existant.

Travailler avec les états graphiques PDF est une exigence courante lorsque vous voulez contrôler la transparence, les modes de fusion ou d’autres paramètres de rendu objet par objet. Le code ci‑dessous démontre l’approche recommandée, explique pourquoi chaque étape est importante et couvre les variations typiques que vous pourriez rencontrer.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou ultérieur (l’exemple se compile également avec .NET Core).
* Une licence Aspose.Pdf for .NET (ou une clé d’évaluation temporaire).
* Un dossier contenant un fichier `input.pdf` que vous souhaitez modifier.
* Une connaissance de base de la syntaxe C# et des concepts PDF tels que les dictionnaires de ressources.

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez une nouvelle application console ou intégrez le code dans un projet existant. Ajoutez le package NuGet Aspose.Pdf :

```bash
dotnet add package Aspose.Pdf
```

Puis importez les espaces de noms requis :

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Ces imports vous donnent accès aux classes `Document`, `DictionaryEditor` et aux primitives PDF nécessaires pour **créer des entrées d’état graphique vides**.

## Étape 2 : Définir le dossier contenant les fichiers PDF

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Remplacez le chemin par l’emplacement de vos propres fichiers PDF. Conserver le répertoire dans une variable rend le code réutilisable et plus facile à tester.

## Étape 3 : Charger le document PDF source

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Ouvrir le document à l’intérieur d’une instruction `using` garantit que le handle du fichier est libéré automatiquement après l’enregistrement des modifications.

## Étape 4 : Accéder à la première page et à son dictionnaire Resources

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` récupère la première page (les numéros de page PDF commencent à 1).
* `DictionaryEditor` offre un moyen pratique de lire et de modifier les dictionnaires PDF.
* L’entrée `ExtGState` contient tous les objets d’état graphique de la page. Si la clé n’existe pas, Aspose.Pdf crée automatiquement un dictionnaire vide.

## Étape 5 : Construire un nouveau dictionnaire d’état graphique vide

L’état graphique que vous ajoutez peut être vide ou pré‑rempli avec des paramètres tels que l’opacité (`CA`, `ca`) ou le mode de fusion (`BM`). Dans ce tutoriel nous créons un **état graphique vide** puis définissons quelques valeurs typiques pour illustrer le fonctionnement du dictionnaire.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` crée un conteneur vierge que vous pouvez remplir avec n’importe quelles clés d’état graphique.
* Ajouter `CA`, `ca` et `BM` est optionnel ; vous pouvez les omettre si vous avez réellement besoin d’un état vide. Le code montre comment ajouter des entrées lorsque vous décidez plus tard de contrôler le rendu.

## Étape 6 : Insérer le nouvel état graphique dans le dictionnaire ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Nommer l’entrée `"GS0"` suit la convention courante de préfixer les noms d’états graphiques par « GS ». Vous pouvez choisir n’importe quel nom PDF valide qui ne rentre pas en conflit avec des clés existantes.

## Étape 7 : Enregistrer le document PDF modifié

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

L’appel `Save` écrit le fichier mis à jour sous `output.pdf`. Ouvrir ce fichier dans un visualiseur PDF confirme que le nouvel état graphique existe ; vous pourrez le référencer plus tard avec l’opérateur `gs` dans les flux de contenu.

### Listing complet du code source

En rassemblant le tout, le programme complet ressemble à ceci :

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

L’exécution du programme affiche une ligne de confirmation et produit `output.pdf` contenant le nouvel état graphique ajouté.

## Pourquoi cette approche est la meilleure

* **Édition directe du dictionnaire** – L’utilisation de `DictionaryEditor` évite d’analyser tout le flux de contenu. Vous ne modifiez que les ressources qui vous intéressent.
* **Primitives PDF typées** – `CosPdfNumber`, `CosPdfName` et `CosPdfDictionary` garantissent que le PDF généré respecte la spécification PDF 1.7.
* **Sécurité** – Le bloc `using` libère l’objet `Document`, prévenant les verrous de fichier qui pourraient corrompre des builds ultérieurs.
* **Extensibilité** – Une fois l’état graphique vide créé, vous pouvez le référencer depuis n’importe quel opérateur de contenu (`gs`) pour modifier l’opacité, le mode de fusion ou d’autres paramètres pour des commandes de dessin sélectionnées.

## Variations courantes et cas limites

| Situation | Ajustement recommandé |
|-----------|-----------------------|
| **Pages multiples** | Parcourez `pdfDocument.Pages` et répétez l’insertion du dictionnaire pour chaque page que vous devez modifier. |
| **Pas d’entrée ExtGState existante** | `resourcesEditor["ExtGState"]` crée automatiquement un dictionnaire vide s’il n’existe pas. Aucun code supplémentaire n’est nécessaire. |
| **Nom d’état graphique différent** | Remplacez `"GS0"` par un nom qui correspond à votre convention, par ex. `"MyTransparentState"`. |
| **Ajout d’un seul état vide** | Omettez le tableau `parameters` et la boucle `foreach` ; le dictionnaire restera vide. |
| **Travail avec des PDF chiffrés** | Fournissez le mot de passe lors de la construction `new Document(path, password)` avant de modifier les ressources. |

## Vérification du résultat

Vous pouvez vérifier que l’état graphique a été ajouté en inspectant le PDF avec un visualiseur bas‑niveau tel que **PDF‑Tron** ou **iText Sharp**. Recherchez une entrée similaire à :

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Si l’entrée apparaît, l’opération **create empty graphics state** a réussi.

## Conclusion

Vous savez maintenant comment **créer un état graphique vide** dans un PDF en utilisant C# et Aspose.Pdf. Le tutoriel a couvert chaque étape — du chargement du document à la modification du dictionnaire `ExtGState` et à l’enregistrement du résultat — tout en expliquant la logique derrière chaque action.  

À partir d’ici, vous pouvez :

* Utiliser le nouvel état graphique dans les flux de contenu (`gs /GS0`).
* Expérimenter avec des clés supplémentaires comme `/SM` (ajustement du trait) ou `/OPM` (mode surimpression).
* Appliquer la même technique à d’autres types de ressources comme `/XObject` ou `/ColorSpace`.

Bonne manipulation de PDF, et n’hésitez pas à explorer d’autres scénarios **Aspose PDF graphics state** tels que les changements d’opacité dynamiques ou les modes de fusion personnalisés !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}