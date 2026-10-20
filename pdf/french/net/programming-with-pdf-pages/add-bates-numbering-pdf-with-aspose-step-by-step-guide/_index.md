---
category: general
date: 2026-08-08
description: Ajouter une numérotation Bates à un PDF avec Aspose.Pdf en C#. Ce tutoriel
  montre également comment ajouter une page blanche à un PDF et générer un PDF de
  façon programmatique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: fr
lastmod: 2026-08-08
og_description: Ajoutez une numérotation Bates à un PDF avec Aspose.Pdf en C#. Apprenez
  à ajouter une page blanche à un PDF, à générer un PDF par programmation et à enregistrer
  le document final en quelques minutes.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Ajouter une numérotation Bates à un PDF avec Aspose – guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Ajouter une numérotation Bates à un PDF avec Aspose – guide étape par étape
url: /fr/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une numérotation Bates PDF avec Aspose – guide étape par étape

Ajouter une numérotation bates pdf avec Aspose.Pdf est simple une fois que vous comprenez les étapes principales. Si vous devez également ajouter une page vierge pdf ou générer un pdf de manière programmatique, ce guide couvre tout ce dont vous avez besoin.

Dans ce tutoriel vous allez :

* Créer un nouveau document PDF à partir de zéro.  
* Ajouter une page vierge pdf qui accueillera les numéros Bates.  
* Configurer l'artifact de numérotation Bates avec un préfixe personnalisé.  
* Enregistrer le PDF afin que les numéros apparaissent dans le fichier généré.  

À la fin, vous disposerez d'une application console C# entièrement fonctionnelle qui produit un PDF contenant des numéros Bates tels que **CASE‑1000**, **CASE‑1001**, … – une exigence courante pour les flux de travail juridiques et d'e‑discovery.

## Prérequis

* .NET 6.0 SDK ou version ultérieure (le code fonctionne également avec .NET Framework 4.8).  
* Visual Studio 2022 ou tout IDE compatible C#.  
* Une licence valide d'Aspose.Pdf for .NET (ou une clé d'évaluation gratuite).  
* Une connaissance de base de la syntaxe C#.

> **Astuce :** Si vous exécutez le code sans licence, Aspose ajoutera un petit filigrane au PDF de sortie.

## Étape 1 : Configurer le projet et importer Aspose.Pdf

Créer un nouveau projet console et ajouter le package NuGet Aspose.Pdf :

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Les directives `using` requises pour l'exemple sont :

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Ces espaces de noms vous donnent accès aux classes `Document`, `Page` et `BatesNumberingArtifact` utilisées plus tard.

## Étape 2 : Ajouter une page vierge pdf

Un numéro Bates doit être attaché à une page, nous créons donc d'abord une page vierge qui recevra l'artifact de numérotation.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

La classe `Document` représente le fichier PDF complet, tandis que `Pages.Add()` insère une nouvelle page vide à la fin de la collection de pages du document. Comme le document commence vide, cet appel crée également la première page.

## Étape 3 : Configurer l'artifact de numérotation Bates

Nous définissons maintenant l'apparence des numéros Bates. Le `BatesNumberingArtifact` vous permet de définir le numéro de départ, le préfixe, le suffixe et les options de formatage.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Pourquoi c'est important :**  
Définir `StartNumber` à **1000** correspond aux conventions typiques des dossiers juridiques. Le `Prefix` garantit que chaque numéro apparaît sous la forme **CASE‑1000**, **CASE‑1001**, … ce qui facilite la recherche et le tri.

## Étape 4 : Attacher l'artifact à la page

L'artifact doit être ajouté à la collection `Artifacts` de la page afin qu'Aspose le rende sur chaque page lors de l'enregistrement.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Lorsque le document est enregistré, Aspose répète automatiquement l'artifact sur toutes les pages, en incrémentant le numéro pour chaque page suivante.

## Étape 5 : (Facultatif) Ajouter des pages supplémentaires

Si vous avez besoin de plus de pages, répétez simplement `pdfDocument.Pages.Add()`. L'artifact de numérotation Bates que vous avez attaché à l'étape précédente apparaîtra automatiquement sur chaque nouvelle page.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Étape 6 : Enregistrer le PDF – générer un pdf de manière programmatique

Enfin, persistez le document sur le disque. C'est à ce moment que les numéros Bates sont rendus sur les pages.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Résultat attendu :**  
Ouvrez *BatesNumberedDocument.pdf* et vous verrez un PDF de trois pages. Chaque page affiche un numéro Bates dans le coin inférieur droit :

* Page 1 → **CASE‑1000**  
* Page 2 → **CASE‑1001**  
* Page 3 → **CASE‑1002**

Les numéros sont automatiquement incrémentés parce que l'artifact est attaché à la collection de pages.

## Exemple complet, exécutable

En réunissant tous les éléments, voici un programme console complet que vous pouvez copier, coller et exécuter :

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Exécutez le programme avec `dotnet run`. Après l'exécution, localisez le fichier sur votre bureau et vérifiez les numéros Bates.

![Exemple d'ajout de numérotation bates pdf](/images/bates-numbering.png "Exemple d'ajout de numérotation bates pdf")

## Questions fréquentes et cas particuliers

### Que faire si j'ai besoin d'une police ou d'une position différente ?

Le `BatesNumberingArtifact` expose des propriétés telles que `FontSize`, `FontColor`, `HorizontalAlignment` et `VerticalAlignment`. Par exemple :

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Comment exclure une page spécifique de la numérotation ?

Créez un `BatesNumberingArtifact` séparé pour les pages que vous souhaitez numéroter et ajoutez‑le uniquement à ces pages. Les pages sans artifact attaché resteront non numérotées.

### Cela fonctionne-t-il avec des PDF existants ?

Oui. Au lieu de `new Document()`, chargez un fichier existant :

```csharp
Document pdfDocument = new Document("input.pdf");
```

Puis attachez l'artifact aux pages souhaitées et enregistrez.

## Conclusion

Vous savez maintenant comment **ajouter une numérotation bates pdf** avec Aspose.Pdf, comment **ajouter une page vierge pdf**, et comment **générer un pdf de manière programmatique** dans une solution C# propre et réutilisable. L'approche fonctionne avec n'importe quel nombre de pages, des préfixes personnalisés et des options de style, vous donnant un contrôle total sur le document final.

Les prochaines étapes que vous pourriez explorer :

* Utiliser **create pdf as

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment ajouter et personnaliser les numéros de page dans les PDF avec Aspose.PDF pour .NET | Guide de manipulation de documents](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Comment ajouter une page vide à la fin d'un PDF avec Aspose.PDF pour .NET | Guide étape par étape](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Créer un document PDF avec Aspose.PDF – Ajouter une page, une forme & Enregistrer](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}