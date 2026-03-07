---
category: general
date: 2026-03-06
description: Créez un document PDF en C# et ajoutez facilement un numéro de Bates.
  Apprenez comment ajouter une page blanche au PDF, placer un tampon sur la page et
  mettre en œuvre la numérotation Bates.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: fr
og_description: Créer un document PDF en C# et ajouter un numéro de Bates. Ce guide
  montre comment ajouter une page blanche au PDF, placer un tampon sur la page et
  appliquer la numérotation Bates.
og_title: Créer un document PDF avec numérotation Bates – Tutoriel C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Créer un document PDF avec numérotation Bates en C# – Guide complet
url: /fr/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un document PDF avec numérotation Bates en C#

Vous avez déjà eu besoin de **créer un document PDF** en C# et vous vous êtes demandé comment ajouter un numéro Bates sans perdre patience ? Vous n'êtes pas seul — les cabinets d’avocats, les tribunaux et même certaines équipes de conformité d’entreprise rencontrent ce même problème chaque jour. La bonne nouvelle ? En quelques lignes de code Aspose.Pdf, vous pouvez générer un tout nouveau PDF, y ajouter une page blanche et apposer un numéro Bates correctement, le tout en un seul flux fluide.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : de la configuration du projet, à l’ajout d’une page blanche, à la façon **d’ajouter la numérotation Bates**, puis **placer le tampon sur la page** et enregistrer le résultat. À la fin, vous disposerez d’un extrait prêt à l’emploi que vous pourrez intégrer dans n’importe quelle application .NET. Pas de références vagues, juste un exemple complet et exécutable.

## Ce dont vous avez besoin

- **.NET 6+** (ou .NET Framework 4.6+ – Aspose.Pdf fonctionne avec les deux)
- **Aspose.Pdf for .NET** package NuGet (`Install-Package Aspose.Pdf`)
- Un IDE correct (Visual Studio, Rider ou VS Code avec l’extension C#)

C’est tout. Aucun DLL supplémentaire, aucun service externe. Plongeons‑y.

## Étape 1 : Créer le document PDF – Configuration initiale

Tout d’abord, nous avons besoin d’un nouvel objet `Document`. Considérez‑le comme la toile vierge où tout le reste prendra forme.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Pourquoi c’est important :** La classe `Document` est le point d’entrée de chaque opération Aspose. L’instancier vous donne accès à la collection `Pages`, aux métadonnées et aux paramètres de sécurité — tous les éléments de base pour un PDF professionnel.

## Étape 2 : Ajouter une page blanche au PDF

Un PDF sans pages, c’est comme un livre sans feuilles — pratiquement inutile. Ajouter une page blanche est simple, et cela nous fournit une surface sur laquelle apposer le numéro Bates.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Astuce pro :** Si vous avez besoin de plusieurs pages, appelez simplement `pdfDocument.Pages.Add()` dans une boucle. Chaque appel renvoie un nouvel objet `Page` que vous pouvez personnaliser indépendamment.

## Étape 3 : Comment ajouter la numérotation Bates – Créer le TextStamp

Voici le cœur du sujet : le **numéro Bates**. Dans Aspose.Pdf, il s’agit simplement d’un `TextStamp` avec un drapeau d’artefact spécial.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Pourquoi nous définissons `Artifact` :** Certains lecteurs PDF exposent les numéros Bates comme métadonnées recherchables. Marquer le tampon comme un artefact `BatesNumbering` garantit que les outils en aval le reconnaissent automatiquement.

## Étape 4 : Placer le tampon sur la page

Le tampon étant prêt, nous **plaçons le tampon sur la page**. C’est à cette étape que le numéro apparaît visuellement dans le PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Cas limite :** Si vous devez incrémenter le numéro sur chaque page, parcourez `pdfDocument.Pages` et mettez à jour `batesStamp.Value` avant d’appeler `AddStamp`. L’exemple ici reste simple avec un « Bates‑001 » statique.

## Étape 5 : Enregistrer et vérifier le résultat

Enfin, nous persistons le PDF sur le disque. Choisissez un dossier où vous avez les droits d’écriture ; sinon, vous rencontrerez une `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Lorsque vous ouvrirez `BatesStamped.pdf` dans n’importe quel visualiseur, vous devriez voir un petit « Bates‑001 » discrètement placé dans le coin inférieur droit de la page blanche.

> **Résultat attendu :**  
> ![PDF avec tampon de numéro Bates](image-placeholder.png "PDF avec tampon de numéro Bates")  
> *Texte alternatif : PDF avec tampon de numéro Bates dans le coin inférieur droit.*

Si le numéro n’apparaît pas, revérifiez les valeurs de marge et assurez‑vous que la taille de la page n’est pas trop petite (le format A4 par défaut fonctionne bien). Vérifiez également que le drapeau `Artifact` n’est pas supprimé par un outil de post‑traitement.

## Exemple complet fonctionnel

Voici le programme complet, prêt à copier‑coller. Il inclut toutes les directives `using` et les commentaires pour vous guider.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Exécutez le programme, ouvrez le PDF, et vous verrez le numéro Bates exactement à l’endroit indiqué. 🎉

## Variantes courantes & pièges

| Scénario | Ce qu’il faut modifier | Pourquoi |
|----------|------------------------|----------|
| **Pages multiples, numéros incrémentiels** | Boucler sur `pdfDocument.Pages`, définir `batesStamp.Value = $"Bates-{i:D3}"` avant `AddStamp` | Attribue à chaque page un identifiant unique, typique pour les dossiers juridiques |
| **Placement différent (en haut à gauche)** | Modifier `HorizontalAlignment = HorizontalAlignment.Left` et `VerticalAlignment = VerticalAlignment.Top` | Certaines organisations préfèrent le numéro dans l’en‑tête plutôt qu’en bas |
| **Police ou couleur personnalisée** | Définir `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Améliore la lisibilité ou répond aux exigences de la charte graphique |
| **Ajouter un PDF existant comme arrière‑plan** | Charger le PDF source avec `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Utile lorsqu’il faut tamponner un formulaire déjà généré |

## Conclusion

Nous venons de montrer comment **créer un document PDF**, **ajouter une page blanche**, et **ajouter un numéro Bates** avec Aspose.Pdf for .NET, puis **placer le tampon sur la page** et enregistrer le fichier. Le code est volontairement compact afin que vous puissiez l’adapter à des flux de travail plus importants — que vous traitiez des dizaines de fichiers ou que vous l’intégriez à un service web.

Si vous êtes prêt à aller plus loin, pensez à :

- Automatiser la logique d’incrémentation pour de gros dossiers.
- Intégrer la génération de PDF dans une API ASP.NET Core.
- Ajouter de la sécurité (protection par mot de passe) avec `pdfDocument.Encrypt(...)`.

N’hésitez pas à expérimenter, à casser des choses et à poser des questions dans les commentaires. Bon codage, et que vos PDFs soient toujours parfaitement tamponnés !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}