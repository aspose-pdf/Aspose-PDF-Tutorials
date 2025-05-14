---
"description": "Apprenez à créer un rectangle rempli dans un PDF avec Aspose.PDF pour .NET grâce à ce tutoriel étape par étape. Idéal pour les développeurs de tous niveaux."
"linktitle": "Créer un rectangle rempli"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Créer un rectangle rempli"
"url": "/fr/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer un rectangle rempli

## Introduction

Avez-vous déjà rêvé de créer des PDF visuellement attrayants par programmation ? Si oui, vous êtes au bon endroit ! Dans ce tutoriel, nous allons plonger dans l'univers d'Aspose.PDF pour .NET, une bibliothèque puissante qui vous permet de manipuler facilement des documents PDF. Aujourd'hui, nous allons nous concentrer sur la création d'un rectangle rempli dans un fichier PDF. Que vous soyez un développeur expérimenté ou débutant, ce guide vous guidera pas à pas de manière conviviale et engageante. Alors, à vos codes et c'est parti !

## Prérequis

Avant de passer au code, vous devez mettre en place quelques éléments :

1. Visual Studio : assurez-vous d'avoir installé Visual Studio sur votre ordinateur. C'est un IDE fantastique pour le développement .NET.
2. Aspose.PDF pour .NET : vous devrez télécharger et installer la bibliothèque Aspose.PDF. Vous pouvez la trouver. [ici](https://releases.aspose.com/pdf/net/).
3. Connaissances de base de C# : une petite familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.

## Importer des packages

Pour commencer, vous devez importer les packages nécessaires dans votre projet C#. Voici comment procéder :

### Créer un nouveau projet

Ouvrez Visual Studio et créez un projet C#. Vous pouvez choisir une application console pour plus de simplicité.

### Ajouter une référence Aspose.PDF

1. Cliquez avec le bouton droit sur votre projet dans l’Explorateur de solutions.
2. Sélectionnez « Gérer les packages NuGet ».
3. Recherchez « Aspose.PDF » et installez la dernière version.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Maintenant que tout est configuré, plongeons dans le code !

## Étape 1 : Configurez votre répertoire de documents

Tout d'abord, vous devez spécifier le chemin d'accès où votre PDF sera enregistré. C'est essentiel car cela indique au programme où créer le fichier.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin réel sur votre machine où vous souhaitez enregistrer le PDF.

## Étape 2 : Créer une instance de document

Ensuite, nous allons créer une instance du `Document` classe. Cette classe représente le document PDF avec lequel vous travaillerez.

```csharp
// Créer une instance de document
Document doc = new Document();
```

Cette ligne initialise un nouveau document PDF que nous pouvons manipuler.

## Étape 3 : Ajouter une page au document

Maintenant, ajoutons une page à notre document. Chaque PDF nécessite au moins une page, n'est-ce pas ?

```csharp
// Ajouter une page à la collection de pages du fichier PDF
Page page = doc.Pages.Add();
```

Ce code ajoute une nouvelle page au document, nous permettant de dessiner des formes dessus.

## Étape 4 : Créer une instance de graphique

Pour dessiner des formes, nous devons créer un `Graph` exemple. Considérez un graphique comme une toile sur laquelle vous pouvez dessiner diverses formes.

```csharp
// Créer une instance de graphique
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

Ici, nous créons un graphique avec une largeur de 100 et une hauteur de 400.

## Étape 5 : Ajouter le graphique à la page

Maintenant que nous avons notre graphique, ajoutons-le à la page que nous avons créée précédemment.

```csharp
// Ajouter un objet graphique à la collection de paragraphes de l'instance de page
page.Paragraphs.Add(graph);
```

Cette ligne attache le graphique à la page, le rendant prêt à être dessiné.

## Étape 6 : Créer une instance de rectangle

Ensuite, nous allons créer un rectangle que nous voulons remplir de couleur.

```csharp
// Créer une instance de rectangle
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

Dans ce code, nous définissons la position et la taille du rectangle. Les paramètres représentent les coordonnées x et y, la largeur et la hauteur.

## Étape 7 : Spécifiez la couleur de remplissage

Choisissons maintenant une couleur pour notre rectangle. Dans cet exemple, nous le remplirons de rouge.

```csharp
// Spécifier la couleur de remplissage pour l'objet graphique
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

Cette ligne définit la couleur de remplissage du rectangle sur rouge. Vous pouvez choisir la couleur de votre choix !

## Étape 8 : Ajouter le rectangle au graphique

Notre rectangle étant prêt, il est temps de l'ajouter au graphique.

```csharp
// Ajouter un objet rectangle à la collection de formes de l'objet graphique
graph.Shapes.Add(rect);
```

Ce code ajoute le rectangle au graphique, le faisant ainsi partie de notre dessin.

## Étape 9 : Enregistrer le document PDF

Enfin, nous devons enregistrer notre document dans le répertoire spécifié.

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// Enregistrer le fichier PDF
doc.Save(dataDir);
```

Ce code enregistre le fichier PDF avec le nom `CreateFilledRectangle_out.pdf` dans le répertoire que vous avez spécifié précédemment.

## Étape 10 : Message de confirmation

Pour nous faire savoir que tout s'est bien passé, nous pouvons imprimer un message de confirmation.

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

Cette ligne affichera un message dans la console, confirmant que le rectangle rempli a été créé avec succès.

## Conclusion

Et voilà ! Vous avez réussi à créer un rectangle rempli dans un document PDF avec Aspose.PDF pour .NET. Cette puissante bibliothèque ouvre un monde de possibilités pour la manipulation des PDF, vous permettant de créer de superbes documents par programmation. Que vous génériez des rapports, des factures ou tout autre type de PDF, Aspose.PDF est là pour vous.

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque qui permet aux développeurs de créer, manipuler et convertir des documents PDF par programmation.

### Puis-je utiliser Aspose.PDF gratuitement ?
Oui, Aspose propose une version d'essai gratuite pour explorer les fonctionnalités de la bibliothèque. Vous pouvez la télécharger. [ici](https://releases.aspose.com/).

### Existe-t-il un moyen d'obtenir de l'aide pour Aspose.PDF ?
Absolument ! Vous pouvez obtenir de l'aide via le forum Aspose. [ici](https://forum.aspose.com/c/pdf/10).

### Comment puis-je acheter Aspose.PDF ?
Vous pouvez acheter Aspose.PDF en visitant la page d'achat [ici](https://purchase.aspose.com/buy).

### Quels types de formes puis-je créer avec Aspose.PDF ?
Vous pouvez créer diverses formes, notamment des rectangles, des cercles, des lignes, etc., à l'aide de la bibliothèque Aspose.PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}