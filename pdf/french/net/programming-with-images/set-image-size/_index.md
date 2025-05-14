---
"description": "Apprenez à définir la taille d'une image dans un PDF avec Aspose.PDF pour .NET. Ce guide étape par étape vous aidera à redimensionner les images, à ajuster les propriétés des pages et à enregistrer vos PDF."
"linktitle": "Définir la taille de l'image dans le fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Définir la taille de l'image dans le fichier PDF"
"url": "/fr/net/programming-with-images/set-image-size/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Définir la taille de l'image dans le fichier PDF

## Introduction

Travailler avec des PDF est une exigence courante pour de nombreuses applications, et la possibilité de manipuler les éléments d'un fichier PDF peut être cruciale. Que vous créiez un générateur de rapports ou que vous ajoutiez du contenu dynamique à votre PDF, contrôler la taille des images est essentiel. Dans ce tutoriel, nous vous expliquerons comment définir la taille des images dans un fichier PDF avec Aspose.PDF pour .NET. Cette puissante bibliothèque offre un contrôle complet du contenu PDF, et nous vous expliquerons étape par étape sa simplicité. À la fin, vous serez capable de redimensionner les images en toute confiance et comprendrez comment cette fonctionnalité peut améliorer vos flux de travail PDF.


## Prérequis

Avant de plonger dans le code, vous devrez mettre en place quelques éléments pour suivre ce tutoriel.

1. Aspose.PDF pour .NET : assurez-vous d'avoir installé la dernière version de la bibliothèque Aspose.PDF. Vous pouvez [téléchargez-le ici](https://releases.aspose.com/pdf/net/).
2. .NET Framework ou .NET Core : assurez-vous que vous disposez d’un environnement de travail avec .NET Framework ou .NET Core configuré.
3. Connaissances de base de C# : nous utiliserons C# comme langage de programmation, il est donc essentiel de le connaître.
4. Exemple d'image : Vous aurez besoin d'un exemple d'image à intégrer au PDF. Vous pouvez utiliser l'image de votre choix, mais assurez-vous qu'elle soit accessible dans le répertoire de votre projet.

## Importer des packages

Pour utiliser Aspose.PDF pour .NET, vous devez d'abord importer les espaces de noms nécessaires. Voici une configuration simple :

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Maintenant que nous avons couvert les bases, passons à la création et à la modification d'un document PDF.

## Étape 1 : Initialisez votre document PDF

La première chose à faire est de créer un nouveau document PDF. Nous utiliserons `Document` classe d'Aspose.PDF pour y parvenir.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Instancier l'objet Document
Document doc = new Document();
```
 
Ici, nous instancions un `Document` qui représentera notre fichier PDF. Nous spécifions également le répertoire où se trouvent nos fichiers à l'aide de l'option `dataDir` variable. C'est le point de départ pour créer n'importe quel PDF avec Aspose.PDF.

## Étape 2 : ajouter une nouvelle page à votre PDF

Une fois notre document prêt, nous devons y ajouter une page. Chaque PDF doit comporter au moins une page ; ajoutons-en une.

```csharp
// Ajouter une page à la collection de pages du fichier PDF
Aspose.Pdf.Page page = doc.Pages.Add();
```
 
Nous ajoutons une nouvelle page au document en utilisant le `Pages.Add()` Méthode. Cette page servira de toile de fond pour notre image. Chaque page d'un PDF est une page blanche sur laquelle vous pouvez ajouter du texte, des images ou d'autres contenus.

## Étape 3 : Créer une instance d’image

Il est maintenant temps de préparer l'image à insérer dans le PDF. Aspose.PDF fournit un `Image` classe pour gérer les images.

```csharp
// Créer une instance d'image
Aspose.Pdf.Image img = new Aspose.Pdf.Image();
```
 
Nous créons une nouvelle instance du `Image` classe. Cet objet contiendra les propriétés de l'image à ajouter au PDF. Nous configurerons la taille et le type de l'image dans les étapes suivantes.

## Étape 4 : Définir la taille de l’image (largeur et hauteur)

C'est ici que nous entrons dans le vif du sujet : définir la taille de l'image. Aspose.PDF vous permet de spécifier la largeur et la hauteur de l'image en points.

```csharp
// Définir la largeur et la hauteur de l'image en points
img.FixWidth = 100;
img.FixHeight = 100;
```
 
Le `FixWidth` et `FixHeight` Les propriétés vous permettent de définir les dimensions exactes de l'image en points. Dans cet exemple, nous redimensionnons l'image à 100x100 points. Vous pouvez ajuster ces valeurs selon vos besoins.

## Étape 5 : Spécifiez le type d’image

Selon le format d'image utilisé, vous devrez peut-être définir le type d'image. Aspose.PDF prend en charge différents formats d'image ; nous définissons ici le type de fichier.

```csharp
// Définir le type d'image comme SVG
img.FileType = Aspose.Pdf.ImageFileType.Unknown;
```
 
Dans ce cas, nous laissons le type de fichier tel que `Unknown`qui permet à la bibliothèque de détecter automatiquement le type d'image. Si vous connaissez le type de fichier spécifique, vous pouvez le définir (par exemple, `ImageFileType.Jpeg` (pour les images JPEG). Cette étape permet à Aspose de gérer correctement l'image.

## Étape 6 : définissez le chemin d’accès à votre fichier image

Nous devons maintenant indiquer à Aspose où trouver le fichier image. Assurez-vous que votre image est accessible dans le répertoire spécifié.

```csharp
// Chemin d'accès au fichier source
img.File = dataDir + "aspose-logo.jpg";
```
 
Ici, nous définissons le chemin d'accès à l'image. Dans ce cas, l'image se trouve dans le dossier `dataDir` dossier et est nommé `aspose-logo.jpg`Assurez-vous de remplacer ceci par le nom et l'emplacement réels de votre fichier image.

## Étape 7 : Ajouter l’image à la page

Une fois l’image configurée et le chemin du fichier défini, nous pouvons maintenant ajouter l’image à notre page.

```csharp
// Ajouter l'image à la collection de paragraphes
page.Paragraphs.Add(img);
```
 
Le `Paragraphs.Add()` Cette méthode nous permet d'ajouter l'image à la page. Pensez à `Paragraphs` Collection sous forme de liste d'éléments qui seront affichés sur la page PDF. Nous pouvons ajouter plusieurs éléments à cette collection, tels que des images, du texte et des formes.

## Étape 8 : Ajuster les propriétés de la page

Pour que notre image s'adapte parfaitement, nous allons ajuster la taille de la page. Cela garantira que les dimensions de la page correspondent au contenu que nous ajoutons.

```csharp
// Définir les propriétés de la page
page.PageInfo.Width = 800;
page.PageInfo.Height = 800;
```
 
Ici, nous définissons la largeur et la hauteur de la page à 800 points. Cette étape est facultative, mais elle garantit que la page s'adapte à l'image redimensionnée. Vous pouvez ajuster ces valeurs selon vos besoins.

## Étape 9 : Enregistrer le PDF

Enfin, après avoir configuré les propriétés de l'image et de la page, nous pouvons enregistrer le PDF.

```csharp
// Enregistrez le fichier PDF résultant
dataDir = dataDir + "SetImageSize_out.pdf";
doc.Save(dataDir);
```
 
Nous enregistrons le document modifié sous `SetImageSize_out.pdf` dans le même répertoire. Ce fichier contiendra désormais l'image redimensionnée que vous avez ajoutée.

## Conclusion

Dans ce tutoriel, nous avons expliqué comment définir la taille d'une image dans un PDF avec Aspose.PDF pour .NET. Nous avons expliqué la création d'un document, l'ajout d'une page, la configuration d'une image et l'enregistrement du résultat. Ce guide étape par étape n'est qu'un aperçu des possibilités offertes par Aspose.PDF pour .NET. Maintenant que vous savez redimensionner les images, n'hésitez pas à explorer d'autres fonctionnalités comme la mise en forme du texte, la création de tableaux et même l'ajout d'annotations à votre PDF.

## FAQ

### Puis-je utiliser différents formats d'image avec Aspose.PDF pour .NET ?  
Oui, Aspose.PDF prend en charge divers formats d'image tels que JPEG, PNG, BMP et SVG.

### Comment conserver le rapport hauteur/largeur de l’image ?  
Vous pouvez conserver le rapport hauteur/largeur en définissant soit le `FixWidth` ou `FixHeight` tout en laissant l’autre dimension non définie.

### Puis-je ajouter plusieurs images à une seule page PDF ?  
Absolument ! Répétez simplement le processus d'ajout d'une instance d'image et ajoutez chaque instance à la `Paragraphs` collection.

### Est-il possible de définir la taille de l'image dans des unités autres que des points ?  
Aspose.PDF fonctionne principalement avec des points, mais vous pouvez convertir d'autres unités comme les pouces ou les millimètres en points (1 pouce = 72 points).

### Comment positionner une image à un endroit précis de la page ?  
Vous pouvez définir le `Image.LowerLeftX` et `Image.LowerLeftY` propriétés pour positionner l'image sur la page.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}