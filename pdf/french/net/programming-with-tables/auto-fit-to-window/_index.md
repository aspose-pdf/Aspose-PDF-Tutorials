---
"description": "Découvrez comment ajuster automatiquement un tableau à la fenêtre avec Aspose.PDF pour .NET grâce à ce guide détaillé, étape par étape. Idéal pour créer des tableaux soignés et bien ajustés dans vos PDF."
"linktitle": "Ajuster automatiquement à la fenêtre"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Ajuster automatiquement à la fenêtre"
"url": "/fr/net/programming-with-tables/auto-fit-to-window/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajuster automatiquement à la fenêtre

## Introduction

Lorsqu'on travaille avec des PDF, on utilise souvent des tableaux, et il arrive que l'on ait besoin qu'ils s'adaptent parfaitement à la largeur d'une page. Dans ce tutoriel, nous allons découvrir comment ajuster automatiquement un tableau à une fenêtre avec Aspose.PDF pour .NET. Cela permet d'obtenir des tableaux soignés et organisés, évitant ainsi les problèmes de débordement ou de colonnes irrégulières. Prêt à apprendre ? C'est parti !

## Prérequis

Avant de passer au guide étape par étape, vous aurez besoin de quelques éléments :

1. Aspose.PDF pour .NET doit être installé dans votre projet. Si ce n'est pas encore le cas, vous pouvez [téléchargez-le ici](https://releases.aspose.com/pdf/net/) ou explorer leur [version d'essai gratuite](https://releases.aspose.com/).
2. Une compréhension de base de la programmation .NET.
3. Visual Studio ou tout autre IDE pris en charge par .NET installé sur votre système.

> PS : N’oubliez pas que vous aurez besoin d’une licence pour utiliser Aspose.PDF sans limitations. Vous pouvez en acheter une. [ici](https://purchase.aspose.com/buy) ou obtenir un [permis temporaire](https://purchase.aspose.com/temporary-license/) pour tester toutes les fonctionnalités.

## Importer des packages

Avant de plonger dans le code, vous devrez importer les espaces de noms nécessaires :

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Maintenant que nous sommes tous prêts, décomposons cela en étapes simples et digestes pour comprendre comment vous pouvez ajuster automatiquement un tableau à une fenêtre à l'aide d'Aspose.PDF pour .NET.

## Étape 1 : Initialiser l'objet Document

Tout d'abord, vous devez créer un document PDF. Considérez ce document comme une feuille vierge sur laquelle vous ajouterez des pages et des tableaux.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Instanciez l'objet Pdf en appelant son constructeur vide
Document doc = new Document();
```
  
Ici, nous créons un nouveau document en utilisant le `Document` classe d'Aspose.PDF. Le `dataDir` est l'emplacement où votre PDF sera enregistré une fois que vous avez terminé.

## Étape 2 : ajouter une page au document

Un document PDF a besoin de pages, n'est-ce pas ? Ajoutons-en une.

```csharp
// Créer une section (page) dans l'objet Pdf
Page sec1 = doc.Pages.Add();
```
  
Nous avons ajouté une nouvelle page au document en utilisant le `Pages.Add()` méthode. Vous pouvez considérer cela comme l'ajout d'une nouvelle feuille à votre document où vous placerez le tableau.

## Étape 3 : Créer et configurer une table

Il est maintenant temps de créer un tableau et de l'ajuster pour qu'il s'adapte à la fenêtre.

```csharp
// Instancier un objet table
Aspose.Pdf.Table tab1 = new Aspose.Pdf.Table();
// Ajoutez le tableau dans la collection de paragraphes de la section souhaitée
sec1.Paragraphs.Add(tab1);
```
  
Nous avons initialisé un nouveau `Table` et l'a ajouté à la collection de paragraphes de la page. Chaque page PDF peut contenir différents paragraphes, et ici, nous traitons le tableau comme un paragraphe.

## Étape 4 : Définir la largeur des colonnes et l'ajuster automatiquement à la fenêtre

Ensuite, nous définissons la largeur des colonnes et nous assurons que le tableau s’ajuste pour s’adapter à la fenêtre.

```csharp
// Définir la largeur des colonnes du tableau
tab1.ColumnWidths = "50 50 50";
tab1.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```
  
Nous avons défini des largeurs de colonnes fixes pour le tableau, mais nous avons également ajouté `ColumnAdjustment.AutoFitToWindow`, ce qui garantit que le tableau ajuste sa taille pour s'adapter à la fenêtre disponible.

## Étape 5 : Définir les bordures et les marges du tableau et des cellules

Les tableaux sans bordures sont souvent illisibles. Définissons des bordures et des marges pour un rendu plus net.

```csharp
// Définir la bordure de cellule par défaut à l'aide de l'objet BorderInfo
tab1.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);

// Définir la bordure du tableau à l'aide d'un autre objet BorderInfo personnalisé
tab1.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 1F);

// Créez un objet MarginInfo et définissez ses marges gauche, inférieure, droite et supérieure
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;

// Définir le remplissage de cellule par défaut sur l'objet MarginInfo
tab1.DefaultCellPadding = margin;
```
  
Les bordures sont ajoutées au tableau et aux cellules à l'aide de `BorderInfo` classe, où vous définissez l'épaisseur. Les marges sont définies pour donner aux cellules un espace de remplissage.

## Étape 6 : Ajouter des lignes et des cellules au tableau

Un tableau sans contenu ? Ce n'est pas bon ! Ajoutons des lignes et des cellules.

```csharp
// Créez des lignes dans le tableau, puis des cellules dans les lignes
Aspose.Pdf.Row row1 = tab1.Rows.Add();
row1.Cells.Add("col1");
row1.Cells.Add("col2");
row1.Cells.Add("col3");

Aspose.Pdf.Row row2 = tab1.Rows.Add();
row2.Cells.Add("item1");
row2.Cells.Add("item2");
row2.Cells.Add("item3");
```
  
Nous créons deux lignes et ajoutons trois cellules à chaque ligne. C'est ici que vous saisirez vos données (qui peuvent être des chaînes de caractères ou des éléments plus complexes).

## Étape 7 : Enregistrer le document

Une fois que tout est configuré, vous souhaiterez enregistrer votre document PDF nouvellement créé.

```csharp
dataDir = dataDir + "AutoFitToWindow_out.pdf";
// Enregistrer le document mis à jour contenant l'objet tableau
doc.Save(dataDir);
```
  
Le `doc.Save()` La méthode enregistre le PDF dans le répertoire spécifié. Dans ce cas, le document sera enregistré sous `AutoFitToWindow_out.pdf` dans votre répertoire défini.

## Conclusion

Et voilà ! Vous venez de créer un tableau qui s'adapte automatiquement à la fenêtre avec Aspose.PDF pour .NET. Cela garantit non seulement un aspect professionnel et un ajustement parfait, mais vous offre également une grande flexibilité pour travailler avec des tailles de données variables. Que vous créiez des rapports, des factures ou tout autre document nécessitant des tableaux, cette méthode est idéale pour conserver des mises en page claires et lisibles.

## FAQ

### Puis-je ajouter plus de lignes de manière dynamique ?  
Oui, vous pouvez continuer à ajouter des lignes en utilisant le `tab1.Rows.Add()` méthode, basée dynamiquement sur le contenu.

### Comment ajuster la table si je ne veux pas qu'elle s'ajuste automatiquement ?  
Vous pouvez définir manuellement le `ColumnWidths` sans utiliser `ColumnAdjustment.AutoFitToWindow` pour maintenir une largeur de table fixe.

### Puis-je ajouter des images ou d’autres contenus à l’intérieur des cellules ?  
Oui, Aspose.PDF vous permet d'ajouter des images, du texte et même d'autres tableaux à l'intérieur des cellules !

### Que faire si j’ai besoin de styles de tableau plus complexes ?  
Vous pouvez personnaliser davantage les styles de tableau et de cellule en utilisant des propriétés telles que la couleur d'arrière-plan, l'alignement du texte et les paramètres de police.

### Est-il possible d'exporter ce tableau vers d'autres formats que PDF ?  
Absolument ! Aspose.PDF prend en charge l'exportation vers différents formats tels que HTML, DOCX, etc.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}