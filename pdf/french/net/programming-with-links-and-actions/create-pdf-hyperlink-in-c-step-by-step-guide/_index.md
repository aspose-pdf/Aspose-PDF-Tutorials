---
category: general
date: 2026-02-20
description: Créez rapidement un hyperlien PDF et intégrez un lien PDF avec C#. Apprenez
  à lier une page PDF spécifique et à convertir un DOCX en lien PDF en quelques minutes.
draft: false
keywords:
- create pdf hyperlink
- link specific pdf page
- embed link pdf
- create clickable pdf link
- convert docx pdf link
language: fr
og_description: Créez un hyperlien PDF instantanément. Ce guide montre comment lier
  une page PDF spécifique, intégrer un lien PDF et convertir un DOCX en lien PDF avec
  C#.
og_title: Créer un lien hypertexte PDF en C# – Tutoriel complet
tags:
- C#
- PDF
- Aspose
title: Créer un hyperlien PDF en C# – Guide étape par étape
url: /fr/net/programming-with-links-and-actions/create-pdf-hyperlink-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un hyperlien PDF en C# – Guide étape par étape

Vous avez déjà eu besoin de **créer un hyperlien PDF** mais vous ne saviez pas quel appel d'API rend réellement le lien fonctionnel ? Vous n'êtes pas seul — la plupart des développeurs rencontrent le même obstacle lorsqu'ils transforment un DOCX en PDF qui saute directement à une page particulière. La bonne nouvelle ? En quelques lignes de C# vous pouvez intégrer un lien, le pointer vers n'importe quelle page, et livrer un PDF soigné en un rien de temps.

Dans ce tutoriel, nous allons parcourir la conversion d'un document Word en PDF **et** l'ajout d'une zone cliquable qui renvoie à une page PDF spécifique. En chemin, nous aborderons également comment **intégrer un lien PDF** dans d'autres flux de travail et pourquoi vous pourriez vouloir **lier une page PDF spécifique** plutôt que de simplement joindre un fichier. À la fin, vous disposerez d'un extrait prêt à l'emploi que vous pourrez insérer dans n'importe quel projet .NET.

## Ce que vous allez apprendre

- Charger un fichier DOCX et le transformer en PDF avec Aspose.Words (ou toute bibliothèque compatible).  
- Créer une annotation **créer un lien PDF cliquable** qui pointe vers une page cible.  
- Définir la zone rectangulaire sur laquelle les utilisateurs cliquent réellement.  
- Enregistrer le PDF final et vérifier que l'hyperlien fonctionne.  
- Pièges courants lors de la **conversion docx pdf lien** et comment les éviter.

### Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+).  
- Packages NuGet Aspose.Words et Aspose.Pdf installés (`dotnet add package Aspose.Words` et `dotnet add package Aspose.Pdf`).  
- Un fichier DOCX simple nommé `input.docx` placé dans un dossier que vous contrôlez.  

Aucune configuration sophistiquée requise — juste quelques déclarations `using` et vous êtes prêt.

![Exemple de création d'hyperlien PDF](image.png "Création d'hyperlien PDF")

## Créer un hyperlien PDF – Vue d'ensemble

L'idée centrale d'une opération **créer un hyperlien PDF** est double :

1. **Annotation** – Le PDF utilise des *annotations de lien* pour décrire une région cliquable.  
2. **Destination** – L'annotation pointe vers un objet *destination*, qui peut être un numéro de page, une vue nommée ou une URL externe.

Lorsque vous combinez ces deux éléments, vous obtenez un lien pleinement fonctionnel qui se comporte comme ceux que vous voyez dans Adobe Reader. Le code ci‑dessous suit exactement ce schéma.

## Étape 1 : Charger le DOCX source

Première chose à faire, nous devons charger le document Word en mémoire. Aspose.Words se charge de la conversion lourde du DOCX en PDF en coulisses.

```csharp
using Aspose.Words;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source DOCX file
Document docx = new Document("YOUR_DIRECTORY/input.docx");

// Convert the Word document to a PDF object (in memory)
using var pdfStream = new MemoryStream();
docx.Save(pdfStream, SaveFormat.Pdf);
pdfStream.Position = 0;

// Create an Aspose.Pdf Document from the memory stream
Document pdfDoc = new Document(pdfStream);
```

*Pourquoi cette étape ?*  
Charger le DOCX avec `Aspose.Words.Document` garantit que tous les styles, images et sauts de page survivent à la conversion. En enregistrant dans un `MemoryStream`, nous évitons de créer un fichier intermédiaire sur le disque — un petit gain de performance et un flux de travail plus propre lorsque vous **intégrez un lien pdf** dans d'autres services plus tard.

## Étape 2 : Créer une annotation de lien

Maintenant que nous disposons d'un objet PDF, nous pouvons ajouter une annotation de lien. Pensez‑y comme à un post‑it qui indique au lecteur « cliquez ici ».

```csharp
// Create a new link annotation object
LinkAnnotation link = pdfDoc.Pages[1].Annotations.AddLink(
    new Rectangle(0, 0, 0, 0)); // Temporary rectangle; we'll set proper coordinates next
```

*Pourquoi utiliser `AddLink` ?*  
`AddLink` enregistre automatiquement l'annotation dans la collection d'annotations de la page, ce qui est essentiel pour que le visualiseur PDF reconnaisse la zone cliquable. Vous pourriez également instancier `LinkAnnotation` manuellement, mais la méthode d'aide garde le code concis.

## Étape 3 : Définir le rectangle cliquable

Le rectangle détermine où sur la page l'utilisateur peut cliquer. Les coordonnées PDF sont mesurées en points (1/72 de pouce), avec l'origine en bas‑à‑gauche.

```csharp
// Define the rectangle (left, bottom, right, top) in points
// Here we place the link near the top of the page, spanning 150 points wide
link.Rect = new Rectangle(50, 700, 200, 720);
```

*Pourquoi ces nombres ?*  
Les valeurs `50, 700, 200, 720` créent une boîte de 150 points de largeur et 20 points de hauteur, positionnée à environ 1 pouce du bord gauche et près du haut d'une page Letter standard. Ajustez les coordonnées selon votre mise en page — si vous placez le lien sous un titre, vous devrez probablement diminuer la valeur `bottom`.

## Étape 4 : Définir la page de destination (Lier une page PDF spécifique)

Nous voulons que le lien saute à la page 2 (indice zéro‑based 1) dans le même PDF. C’est le scénario classique de **lier une page PDF spécifique**.

```csharp
// Destination page index is zero‑based; 1 points to the second page
Destination dest = new Destination(1);

// Assign the destination to the annotation
link.Destination = dest;

// Optional: Change the appearance to look like a typical hyperlink (blue, underlined)
link.Color = Color.Blue;
link.Border = new Border(link) { Width = 0 };
```

*Pourquoi un objet `Destination` ?*  
Le PDF prend en charge de nombreux types de destination (ajustement de page, zoom, etc.). En utilisant le constructeur simple avec un indice de page, nous obtenons le comportement par défaut « fit page », ce que la plupart des utilisateurs attendent lorsqu'ils cliquent sur un lien.

## Étape 5 : Enregistrer le PDF modifié

Enfin, nous écrivons le PDF mis à jour sur le disque. Le fichier de sortie contient maintenant un **créer un lien PDF cliquable** qui saute à la deuxième page.

```csharp
// Save the PDF with the new hyperlink
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

C’est tout — votre PDF est prêt, et le lien fonctionne dans n'importe quel visualiseur standard.

## Tester l'hyperlien

Ouvrez `output.pdf` dans Adobe Reader ou tout visualiseur PDF moderne. Survolez le rectangle bleu ; le curseur doit se transformer en main. Un clic le fera basculer instantanément vers la page 2. Si rien ne se passe, revérifiez les coordonnées du rectangle et assurez‑vous que l’indice de destination correspond à une page existante.

## Pièges courants & comment les éviter

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Le lien ne fait rien | Index de page de destination hors limites | Vérifiez `pdfDoc.Pages.Count` et utilisez un indice valide (zéro‑based). |
| Le rectangle apparaît au mauvais endroit | Confusion du système de coordonnées PDF (origine en bas‑gauche) | Rappelez‑vous que Y = 0 est le bas de la page ; augmentez Y pour monter. |
| Couleur du lien invisible | Couleur de l'annotation non définie ou le visualiseur l'ignore | Définissez explicitement `link.Color = Color.Blue` et `link.Border.Width = 0`. |
| Taille du PDF qui explose | Enregistrement du PDF intermédiaire sur disque avant d’ajouter l’annotation | Utilisez un `MemoryStream` comme montré pour garder le pipeline en mémoire. |

## Cas limites et variantes

### Lier à une URL externe

Si vous devez **intégrer un lien PDF** qui pointe en dehors du document, remplacez l’affectation `Destination` par une `LinkAction` :

```csharp
link.Action = new LinkAction("https://example.com");
```

### Ajouter plusieurs liens sur différentes pages

Il suffit de boucler sur les pages et de créer une nouvelle `LinkAnnotation` pour chacune. N'oubliez pas d’ajuster les coordonnées du rectangle pour la mise en page de chaque page.

```csharp
for (int i = 1; i <= pdfDoc.Pages.Count; i++)
{
    var page = pdfDoc.Pages[i];
    var link = page.Annotations.AddLink(new Rectangle(50, 50, 150, 70));
    link.Destination = new Destination(i - 1); // Jump to the same page (self‑link)
}
```

### Utiliser des destinations nommées

Au lieu d’un indice numérique, vous pouvez créer une destination nommée, pratique lorsque l’ordre des pages peut changer ultérieurement.

```csharp
pdfDoc.NamedDestinations.Add("ChapterTwo", new Destination(1));
link.Destination = new Destination("ChapterTwo");
```

## Prochaines étapes – Intégrer le lien PDF dans des flux de travail plus larges

Maintenant que vous pouvez **créer un hyperlien PDF** programmatique, envisagez ces idées de suivi :

- **Traitement par lots** : Parcourez un dossier de fichiers DOCX, convertissez chacun et ajoutez un lien vers une page de table des matières.  
- **Rapports PDF dynamiques** : Générez une page de résumé avec des liens vers des sections détaillées—idéal pour les journaux d’audit.  
- **Services web** : Exposez un point d'API qui reçoit un DOCX, ajoute un **créer un lien PDF cliquable**, et renvoie les octets du PDF.  

Tous ces scénarios s’appuient sur les mêmes concepts de base que nous avons couverts : charger, annoter et enregistrer.

---

### TL;DR

Nous avons montré comment **créer un hyperlien PDF** en C# en chargeant un DOCX, en ajoutant une annotation de lien, en définissant un rectangle cliquable, en définissant une destination pour **lier une page PDF spécifique**, puis en enregistrant le résultat. Le même schéma vous permet de **intégrer un lien PDF**, **créer un lien PDF cliquable**, ou même **convertir docx pdf lien** pour des pipelines d'automatisation plus complexes.

N’hésitez pas à expérimenter—modifiez la taille du rectangle, pointez vers d’autres pages, ou remplacez‑le par une URL externe. Si vous rencontrez des difficultés, consultez le tableau « Pièges courants » ou laissez un commentaire ci‑dessous. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}