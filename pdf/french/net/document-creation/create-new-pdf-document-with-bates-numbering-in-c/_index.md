---
category: general
date: 2026-08-04
description: Créer un nouveau document PDF en C# et ajouter rapidement une numérotation
  Bates au PDF à l’aide d’Aspose.Pdf – apprendre à ajouter une page blanche au PDF
  et des numéros de page personnalisés.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: fr
lastmod: 2026-08-04
og_description: Créer un nouveau document PDF en C# et ajouter automatiquement une
  numérotation Bates au PDF pour la gestion de dossiers juridiques – exemple complet
  de code inclus.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Créer un nouveau document PDF avec une numérotation Bates en C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Créer un nouveau document PDF avec numérotation Bates en C#
url: /fr/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau document PDF avec numérotation Bates en C#

Si vous devez **créer un nouveau document PDF** en C#, ce guide vous montre comment **ajouter une numérotation Bates pdf** à l’aide d’Aspose.Pdf. Vous apprendrez à **ajouter une page blanche pdf**, à configurer **l’ajout de numéros de page personnalisés**, et à enregistrer le fichier final.

Le tutoriel couvre chaque étape, de l’installation de la bibliothèque à la génération d’un PDF conforme aux normes des dossiers juridiques. À la fin, vous pourrez générer un PDF, insérer une page blanche, appliquer des numéros Bates et personnaliser le format de numérotation — le tout avec un seul programme exécutable.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 SDK ou version ultérieure installé  
* Visual Studio 2022 (ou tout IDE C#)  
* Une licence active d’Aspose.Pdf pour .NET ou une clé d’évaluation gratuite  

Vous n’avez besoin d’aucun package NuGet supplémentaire ; le tutoriel installe tout automatiquement.

## Étape 1 : Installer Aspose.Pdf via NuGet

Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.Pdf
```

Cette commande ajoute la dernière version stable d’Aspose.Pdf à votre projet, qui fournit les classes `Document`, `BatesNumbering` et autres classes de manipulation PDF que vous utiliserez.

## Étape 2 : Créer un nouveau document PDF – configuration initiale

Créer le fichier PDF est la base de toutes les opérations ultérieures. La classe `Document` représente l’ensemble du conteneur PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Pourquoi c’est important* : l’instanciation de `Document` alloue les structures internes requises pour les pages, les polices et les graphiques. Utiliser `using var` garantit que le fichier est correctement libéré après l’enregistrement.

## Étape 3 : Ajouter une page blanche pdf

Un PDF doit contenir au moins une page avant de pouvoir y placer du contenu. Ajouter une page blanche vous donne une toile vierge pour les numéros Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

La méthode `Pages.Add()` ajoute une nouvelle page vide à la fin de la collection de pages du document. Vous pouvez répéter cet appel pour ajouter d’autres pages si vous devez plus tard **ajouter des numéros de page personnalisés** sur plusieurs pages.

## Étape 4 : Configurer la numérotation Bates – comment ajouter des Bates

La numérotation Bates est un identifiant séquentiel couramment utilisé dans les documents juridiques. Vous la configurez via la classe `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Pourquoi c’est important* : `StartNumber` définit le premier numéro, `Prefix` ajoute une étiquette lisible, et `Increment` contrôle le pas. Vous pouvez également ajuster `HorizontalAlignment`, `VerticalAlignment`, `FontSize` et `Margins` pour contrôler l’apparence du numéro sur chaque page.

## Étape 5 : Appliquer la numérotation Bates pdf à la page

Une fois les options de numérotation prêtes, appliquez‑les à la page (ou à l’ensemble du document).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

L’appel à `Apply` insère le numéro formaté dans le pied de page de la page par défaut. Si vous avez besoin du numéro ailleurs, définissez `bates.Position` avant d’appeler `Apply`.

## Étape 6 : Enregistrer le PDF avec les numéros Bates appliqués

Enfin, écrivez le document en mémoire sur le disque.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Le fichier enregistré contient maintenant une seule page avec le numéro Bates **CaseA-1000** affiché en bas. Ouvrez le PDF dans n’importe quel visualiseur pour vérifier la numérotation.

## Résultat attendu

Lorsque vous ouvrez `BatesNumbered.pdf`, vous devez voir :

* Une page blanche (ou plus si vous avez ajouté des pages supplémentaires)  
* Le texte **CaseA-1000** positionné en bas de la page (emplacement par défaut)  

Si vous ajoutez d’autres pages et réutilisez la même instance `BatesNumbering`, les numéros s’incrémenteront automatiquement (CaseA-1001, CaseA-1002, …).

## Astuce pro : Ajouter des numéros de page personnalisés en plus des numéros Bates

Parfois, vous avez besoin à la fois des numéros Bates et des numéros de page traditionnels. Vous pouvez les combiner en ajoutant un `TextFragment` après avoir appliqué la numérotation Bates :

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Cet extrait montre **ajouter des numéros de page personnalisés** tout en conservant l’étiquette Bates.

## Cas particulier : Appliquer la numérotation Bates à plusieurs pages

Si votre document contient plusieurs pages, vous pouvez appliquer la même instance `BatesNumbering` à chaque page dans une boucle :

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

La boucle garantit que chaque page reçoit un numéro séquentiel basé sur le `StartNumber` et l’`Increment` que vous avez définis.

## Problèmes courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Les numéros apparaissent décentrés | L’alignement par défaut ne correspond pas à votre mise en page | Définissez explicitement `bates.HorizontalAlignment` et `bates.VerticalAlignment` |
| Les numéros chevauchent le contenu existant | Aucun marge n’est définie | Ajustez `bates.Margin` ou utilisez `bates.Position` pour déplacer le numéro |
| Exception de licence à l’exécution | La version d’évaluation limite la sortie | Appliquez une licence Aspose.Pdf valide avant de créer le document (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Exemple complet fonctionnel

Voici un programme autonome que vous pouvez copier, coller et exécuter.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment ajouter et personnaliser les numéros de page dans les PDF avec Aspose.PDF pour .NET | Guide de manipulation de documents](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET : ajouter des numéros de page aux PDF à l’aide de FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Créer un document PDF avec Aspose.PDF – Ajouter une page, une forme et enregistrer](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}