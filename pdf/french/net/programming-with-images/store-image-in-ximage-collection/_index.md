---
"description": "Découvrez comment stocker des images dans la collection XImage à l'aide d'Aspose.PDF pour .NET dans ce guide complet étape par étape."
"linktitle": "Stocker l'image dans la collection XImage"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Stocker l'image dans la collection XImage"
"url": "/fr/net/programming-with-images/store-image-in-ximage-collection/"
"weight": 290
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stocker l'image dans la collection XImage

## Introduction

À l'ère du numérique, la gestion et la manipulation de documents par programmation sont essentielles pour de nombreuses applications. Aspose.PDF pour .NET permet aux développeurs de travailler facilement avec des fichiers PDF, améliorant ainsi les flux de travail et permettant la création de contenu dynamique. Dans ce guide, nous explorerons le processus de stockage d'une image dans la collection XImage, une fonctionnalité essentielle qui vous permet d'intégrer des visuels directement dans vos PDF. Prêt à vous lancer dans la création de contenu exceptionnel ?

## Prérequis

Avant de plonger dans le code et les processus, vous devez vous assurer que vous disposez de quelques éléments :

- Environnement .NET : .NET Framework doit être installé sur votre ordinateur. Choisissez la version adaptée aux besoins de votre projet.
- Aspose.PDF pour .NET : Assurez-vous de disposer de la bibliothèque Aspose.PDF. Vous pouvez la télécharger depuis [ici](https://releases.aspose.com/pdf/net/) ou commencez par un essai gratuit [ici](https://releases.aspose.com/).
- Fichier image : Vous aurez également besoin d'un fichier image (JPG ou PNG) à intégrer au PDF. Pour cet exemple, nous utiliserons un fichier nommé « aspose-logo.jpg ».
- Compréhension de base de C# : la familiarité avec la programmation C# vous aidera à suivre en douceur.

## Importer des packages

Pour commencer à utiliser Aspose.PDF pour .NET, vous devez importer les espaces de noms requis. Cette étape pose les bases de l'utilisation de toutes les fonctionnalités offertes par la bibliothèque.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Operators;
```

En important ces espaces de noms, vous activez diverses fonctionnalités dans Aspose.PDF, notamment la création de documents, le traitement d'images, etc.

Décomposons cela en étapes faciles à gérer, ce qui vous permettra de suivre plus facilement.

## Étape 1 : Configurez votre répertoire de documents

Quelle est la première chose à faire ? Définissez l'emplacement de stockage de vos documents. Vous devrez configurer une variable contenant le chemin d'accès à votre répertoire de documents. C'est là que votre PDF sera enregistré.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Remplacez par votre répertoire de documents réel.
```

## Étape 2 : Initialiser le document

Il est maintenant temps de créer un nouveau document PDF. C'est à cette étape que votre PDF prend vie. 

```csharp
Aspose.Pdf.Document document = new Document();
```

Ici, nous instancions un nouvel objet Document qui servira de canevas.

## Étape 3 : Ajouter une nouvelle page

Tout chef-d'œuvre a besoin d'une toile, n'est-ce pas ? Dans notre cas, il nous faut une page sur laquelle travailler dans le document.

```csharp
document.Pages.Add();
Page page = document.Pages[1]; // Obtenez la première page.
```

Nous ajoutons une nouvelle page à notre document. Nous allons maintenant opérer sur cette page.

## Étape 4 : Charger le fichier image

Ensuite, vous devrez charger l'image dans votre programme. Cette étape est similaire à l'ouverture d'un livre : vous devez accéder au contenu avant de pouvoir l'utiliser.

```csharp
using (FileStream imageStream = new FileStream(dataDir + "aspose-logo.jpg", FileMode.Open))
{
```

Cette ligne ouvre le fichier image sous forme de flux, ce qui nous permet de le manipuler et de l'intégrer dans le PDF.

## Étape 5 : Ajouter l'image aux ressources de la page

Maintenant que l'image est prête à être utilisée, il est temps de l'ajouter aux ressources de la page, en indiquant essentiellement au PDF : « Hé, j'ai une image sympa dont je veux que tu te souviennes ! »

```csharp
page.Resources.Images.Add(imageStream, ImageFilterType.Flate);
XImage ximage = page.Resources.Images[page.Resources.Images.Count];
```

Ce code effectue le gros du travail en ajoutant l'image au PDF et en l'attribuant à un `XImage` variable à laquelle nous pourrons faire référence plus tard.

## Étape 6 : Préparez-vous à dessiner l'image

Voici la partie amusante : le positionnement de l'image sur la page. Il vous faudra définir les coordonnées pour que l'image soit placée exactement là où vous le souhaitez.

```csharp
page.Contents.Add(new GSave());
```

Cette ligne enregistre l'état graphique pour une restauration ultérieure. C'est comme prendre un instantané de la configuration avant toute modification.

## Étape 7 : Définir la position et la taille de l’image

Maintenant, définissez la taille et l'endroit où vous souhaitez placer votre image :

```csharp
int lowerLeftX = 0;
int lowerLeftY = 0;
int upperRightX = 600;
int upperRightY = 600;
Aspose.Pdf.Rectangle rectangle = new Aspose.Pdf.Rectangle(lowerLeftX, lowerLeftY, upperRightX, upperRightY);
```

Ce bloc de code définit les dimensions du rectangle dans lequel votre image s'adaptera, lui donnant ainsi essentiellement une place sur votre page.

## Étape 8 : Créer une matrice de transformation 

Pour contrôler le positionnement de l'image, nous allons définir une matrice de transformation. Celle-ci détermine l'apparence de l'image aux coordonnées de destination.

```csharp
Matrix matrix = new Matrix(new double[] { rectangle.URX - rectangle.LLX, 0, 0, rectangle.URY - rectangle.LLY, rectangle.LLX, rectangle.LLY });
```

Considérez cela comme le tracé d'une carte avant de partir en voyage. Cela permet de déterminer l'apparence de l'image sur la page.

## Étape 9 : Placez l'image sur la page

Maintenant, il est temps d'indiquer réellement au PDF où placer cette image.

```csharp
page.Contents.Add(new ConcatenateMatrix(matrix));
page.Contents.Add(new Do(ximage.Name));
page.Contents.Add(new GRestore());
```

Ici, nous ajoutons des commandes au flux de contenu du PDF qui dessineront réellement l'image en fonction de la matrice que nous venons d'établir.

## Étape 10 : Enregistrer le document

Enfin, nous pouvons sauver notre chef-d'œuvre ! C'est le moment où tout votre travail acharné se concrétise en un résultat tangible.

```csharp
document.Save(dataDir + "FlateDecodeCompression.pdf");
```

Vous avez demandé à Aspose.PDF d'enregistrer le document sous le nom de fichier fourni. En exécutant ce code, vous trouverez le fichier PDF nouvellement créé dans le répertoire spécifié, avec votre image intégrée.

## Conclusion

Et voilà ! Vous avez appris à utiliser Aspose.PDF pour .NET pour stocker une image dans la collection XImage point par point. N'est-il pas gratifiant de voir votre code prendre forme et générer quelque chose d'utile ? Que vous développiez des applications ou que vous cherchiez simplement à automatiser des rapports, ce guide constitue une excellente base. N'oubliez pas que la puissance d'Aspose.PDF peut vous aider dans une multitude de tâches, alors continuez à explorer !

## FAQ

### Quels formats de fichiers sont pris en charge pour les images dans Aspose.PDF ?
Aspose.PDF prend en charge divers formats d'image, notamment JPG, PNG, BMP et GIF.

### Puis-je modifier la taille de l'image lors de son ajout au PDF ?
Oui, en ajustant les coordonnées définies dans le rectangle, vous pouvez modifier la taille de l'image affichée dans le PDF.

### Ai-je besoin d'une licence pour utiliser Aspose.PDF ?
Aspose propose un essai gratuit et diverses options d'achat. Vous pouvez les trouver [ici](https://purchase.aspose.com/buy).

### Comment puis-je obtenir de l’aide si je rencontre des problèmes ?
Vous pouvez demander de l'aide à la communauté Aspose [ici](https://forum.aspose.com/c/pdf/10).

### Existe-t-il un moyen d’appliquer une compression aux images ajoutées au PDF ?
Oui, lors de l'ajout d'images au PDF, vous pouvez spécifier le type de filtre d'image pour utiliser des méthodes de compression comme Flate.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}