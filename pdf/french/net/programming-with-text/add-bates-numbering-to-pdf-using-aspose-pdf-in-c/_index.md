---
category: general
date: 2026-09-27
description: Ajoutez une numérotation Bates à un PDF à l'aide d'Aspose.PDF en C#.
  Apprenez comment charger un document PDF, définir les options de numérotation Bates
  et enregistrer le fichier mis à jour.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: fr
lastmod: 2026-09-27
og_description: Ajoutez une numérotation Bates à un PDF avec Aspose.PDF en C#. Ce
  tutoriel vous montre comment charger un document PDF, configurer la numérotation
  Bates et enregistrer le résultat.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Ajouter une numérotation Bates aux PDF avec Aspose.PDF – Guide C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Ajouter une numérotation Bates à un PDF avec Aspose.PDF en C#
url: /fr/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une numérotation Bates à un PDF avec Aspose.PDF en C#

Si vous devez **ajouter une numérotation Bates** à un fichier PDF, ce guide vous présente une solution complète, prête à l’emploi. Vous verrez comment **charger un document PDF**, configurer les options de numérotation Bates, et écrire le fichier numéroté sur le disque — le tout avec Aspose.PDF pour .NET.

L’application de numéros Bates est courante dans les flux de travail juridiques, d’application de la loi et d’archivage. À la fin de ce tutoriel, vous pourrez intégrer un identifiant séquentiel sur chaque page, personnaliser le préfixe et démarrer le comptage à n’importe quel nombre choisi.

## Ce que vous apprendrez

* Comment **charger le contenu d’un document PDF** dans un objet `Aspose.Pdf.Document`.  
* Les étapes exactes **pour ajouter une numérotation Bates** avec `BatesNumberingOptions`.  
* Comment enregistrer le fichier modifié tout en préservant la mise en page et la qualité d’origine.  

Aucun outil externe n’est requis — seulement le package NuGet Aspose.PDF et un environnement de développement .NET (Visual Studio, VS Code ou Rider).  

---

## Étape 1 : Installer Aspose.PDF pour .NET

Ouvrez le dossier de votre projet dans un terminal et exécutez :

```bash
dotnet add package Aspose.PDF
```

Le package inclut l’espace de noms `Aspose.Pdf`, qui fournit toutes les classes utilisées dans ce tutoriel. Après l’installation, rechargez le projet afin que l’IDE prenne en compte la nouvelle référence.

## Étape 2 : Charger le document PDF

Le chargement du fichier source est la première opération car le moteur de numérotation Bates fonctionne sur une instance `Document` existante.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Pourquoi c’est important :** La classe `Document` analyse la structure du PDF, vous donnant accès aux pages, annotations et métadonnées. Sans charger le fichier au préalable, vous ne pouvez appliquer aucune numérotation.

## Étape 3 : Configurer les options de numérotation Bates

Créez un objet `BatesNumberingOptions` et définissez le préfixe souhaité, le numéro de départ et les paramètres de formatage optionnels.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Pourquoi c’est important :** `BatesNumberingOptions` indique à Aspose.PDF comment générer l’étiquette pour chaque page. Le `Prefix` vous aide à regrouper les dossiers liés, tandis que `StartNumber` vous permet de poursuivre une séquence à partir d’un lot précédent.

## Étape 4 : Enregistrer le PDF avec les numéros Bates appliqués

Passez l’objet d’options à la méthode `Save`. Aspose.PDF écrit les numéros directement sur chaque page.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Pourquoi c’est important :** La surcharge `Save(string, BatesNumberingOptions)` combine l’étape de rendu avec le processus de numérotation, garantissant que le fichier de sortie contient les identifiants visibles.

## Exemple complet – tout ensemble

Ci‑dessous se trouve un programme autonome que vous pouvez copier, coller et exécuter. Il montre **comment ajouter une numérotation Bates** du début à la fin.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Résultat attendu

L’exécution du programme produit `output.pdf` où chaque page affiche une étiquette similaire à :

```
CASE01-1
CASE01-2
CASE01-3
...
```

Les numéros apparaissent par défaut dans le pied de page, mais vous pouvez les déplacer en ajustant la propriété `Margin` dans `BatesNumberingOptions`.

## Cas limites et variations courantes

| Situation | Ce qu’il faut ajuster |
|-----------|-----------------------|
| **Préfixe différent par lot** | Modifiez `Prefix` avant d’appeler `Save`. Vous pouvez parcourir plusieurs documents avec des préfixes distincts. |
| **Continuer la numérotation à partir d’un fichier précédent** | Définissez `StartNumber` au dernier numéro utilisé + 1. |
| **Placer les numéros dans l’en-tête** | Utilisez `batesOptions.Margin = new Margin(20, 0, 0, 0);` (marge supérieure) ou personnalisez `batesOptions.Position`. |
| **Police ou couleur personnalisée** | Attribuez les propriétés `Font`, `FontSize` et `Color` comme indiqué dans la section commentée. |
| **PDF volumineux (1000 + pages)** | L’opération est efficace en mémoire ; cependant, vous pouvez activer `doc.OptimizeResources()` avant l’enregistrement pour réduire la taille du fichier. |

**Astuce :** Si votre flux de travail nécessite différents schémas de numérotation par document, encapsulez la logique dans une méthode d’assistance :

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Conclusion

Vous savez maintenant **comment ajouter une numérotation Bates** à n’importe quel PDF avec Aspose.PDF en C#. Le tutoriel a couvert le chargement du document PDF, la configuration des options de numérotation et l’enregistrement du fichier final — le tout dans un seul programme exécutable.  

À partir d’ici, vous pouvez explorer des sujets connexes tels que **l’ajout de filigranes**, **la fusion de plusieurs PDF**, ou **l’extraction de texte** avec Aspose.PDF. Expérimentez différentes polices, couleurs et positions pour correspondre aux normes de formatage de votre organisation.

Prêt à automatiser votre flux de travail de documents juridiques ? Ajoutez le code à votre pipeline de construction, exécutez‑le sur des lots de fichiers, et laissez Aspose.PDF gérer le travail lourd. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un document PDF C# – Ajouter une numérotation Bates](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Ajouter une numérotation Bates PDF – Guide étape par étape pour numéroter les pages PDF](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Tutoriel Aspose PDF – Insérer une page blanche et mettre à jour la numérotation Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}