---
"description": "Guide étape par étape pour modifier l'orientation d'un PDF avec Aspose.PDF pour .NET. Facile à suivre et à mettre en œuvre dans vos projets."
"linktitle": "Orientation du changement"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Orientation du changement"
"url": "/fr/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Orientation du changement

## Introduction

Avez-vous déjà rencontré des difficultés avec un fichier PDF dont l'orientation des pages est… erronée ? Il s'agit peut-être d'un document numérisé ou mal créé, et dont les pages doivent être pivotées pour être lisibles. Heureusement, Aspose.PDF pour .NET offre un moyen simple et puissant de manipuler les fichiers PDF de presque toutes les manières imaginables, y compris de modifier l'orientation de vos pages. Que vous souhaitiez passer du mode portrait au mode paysage ou inversement, ce guide vous guidera pas à pas.

Alors, si vous êtes prêt à vous lancer et à faire pivoter ces pages PDF en toute simplicité, commençons !

## Prérequis

Avant d'entrer dans les détails de la modification de l'orientation des pages dans votre PDF, examinons rapidement ce dont vous aurez besoin :

- Aspose.PDF pour .NET : Assurez-vous d'avoir installé la bibliothèque Aspose.PDF pour .NET. Si ce n'est pas le cas, vous pouvez [téléchargez-le ici](https://releases.aspose.com/pdf/net/).
- Un environnement de développement .NET : vous pouvez utiliser Visual Studio, JetBrains Rider ou tout autre IDE préféré pour travailler avec .NET.
- Connaissances de base de C# : bien que ce guide soit simple, une compréhension de base de C# le rendra encore plus facile à suivre.
- Un fichier PDF : L'exemple ci-dessous suppose que vous disposez d'un fichier PDF de plusieurs pages. Si vous n'en avez pas sous la main, créez ou téléchargez un exemple de PDF.

De plus, si vous débutez, vous pouvez essayer Aspose.PDF avec un [permis temporaire gratuit](https://purchase.aspose.com/temporary-license/) avant de décider de [acheter la version complète](https://purchase.aspose.com/buy).

## Importer des espaces de noms

Avant de pouvoir modifier l'orientation des pages de votre PDF, vous devez importer les espaces de noms nécessaires dans votre projet C#. Assurez-vous d'avoir les éléments suivants :

```csharp
using System.IO;
using Aspose.Pdf;
```

Une fois ceci importé, passons à la partie principale du tutoriel.

## Étape 1 : Charger le document PDF

La première chose à faire est de charger le fichier PDF à modifier. Vous pouvez utiliser l'outil `Document` classe de l'espace de noms Aspose.PDF pour ouvrir votre PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Cette ligne charge le PDF depuis le répertoire spécifié. Assurez-vous de remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin d'accès réel à votre fichier. `"input.pdf"` est-ce le PDF dont vous souhaitez modifier l'orientation.

## Étape 2 : Parcourir chaque page

Maintenant que le document est chargé, parcourons chaque page du PDF. Nous utiliserons un `foreach` boucle pour parcourir chaque page, nous permettant d'appliquer le changement d'orientation à toutes.

```csharp
foreach (Page page in doc.Pages)
{
    // Manipuler chaque page
}
```

Cette boucle parcourra toutes les pages du document.

## Étape 3 : Obtenir la MediaBox de la page

Chaque page d'un PDF a un `MediaBox` qui définit les limites de la page. Nous devons y accéder pour déterminer l'orientation actuelle et la modifier.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

Le `MediaBox` nous donne les dimensions de la page, telles que sa largeur, sa hauteur et son positionnement.

## Étape 4 : échangez la largeur et la hauteur

Pour modifier l'orientation de la page de portrait à paysage ou inversement, il suffit d'inverser les valeurs de largeur et de hauteur. Cette étape ajustera les dimensions de la page.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

Ce code échange la hauteur et la largeur et repositionne le coin inférieur gauche (`LLY`) afin que le contenu s'adapte parfaitement après la rotation.

## Étape 5 : Mettre à jour MediaBox et CropBox

Maintenant que nous avons la nouvelle hauteur et la nouvelle largeur, appliquons les modifications à la page. `MediaBox` et `CropBox`. Le `CropBox` est essentiel si le document original en avait un seul, garantissant que la page entière s'affiche correctement.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

Cette étape redimensionne la page en fonction des nouvelles dimensions que nous venons de calculer.

## Étape 6 : faire pivoter la page

Enfin, nous définissons l'angle de rotation de la page. Aspose.PDF simplifie grandement cette opération. Nous pouvons faire pivoter la page de 90 degrés pour passer du mode portrait au mode paysage, ou inversement.

```csharp
page.Rotate = Rotation.on90;
```

Ce code fait pivoter la page de 90 degrés, la retournant dans l'orientation souhaitée.

## Étape 7 : Enregistrer le PDF de sortie

Après avoir appliqué les modifications d’orientation à toutes les pages, nous enregistrons le document modifié dans un nouveau fichier. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

Assurez-vous de fournir un nouveau nom de fichier (dans ce cas, `ChangeOrientation_out.pdf`) pour enregistrer le résultat. De cette façon, vous n'écraserez pas votre fichier d'origine.

### Conclusion

Et voilà ! Pour modifier l'orientation d'un fichier PDF avec Aspose.PDF pour .NET, il suffit de charger le document, de parcourir les pages, d'ajuster la MediaBox et d'enregistrer le fichier mis à jour. Que vous ayez besoin d'un document mal numérisé ou de faire pivoter des pages pour les adapter à vos besoins de mise en forme, ce guide étape par étape devrait vous aider.

## FAQ

### Puis-je faire pivoter des pages spécifiques au lieu de toutes les pages du PDF ?  
Oui, vous pouvez modifier la boucle pour cibler des pages spécifiques en utilisant leur index au lieu de parcourir toutes les pages.

### Qu'est-ce que le `MediaBox`?  
Le `MediaBox` Définit la taille et la forme de la page dans un fichier PDF. C'est là que le contenu de la page est placé.

### Aspose.PDF pour .NET fonctionne-t-il avec d’autres formats de fichiers ?  
Oui, Aspose.PDF peut gérer une variété de formats de fichiers tels que HTML, XML, XPS, etc.

### Existe-t-il une version gratuite d'Aspose.PDF pour .NET ?  
Oui, vous pouvez commencer avec un [essai gratuit](https://releases.aspose.com/) ou demander un [permis temporaire](https://purchase.aspose.com/temporary-license/).

### Puis-je annuler les modifications une fois enregistrées ?  
Une fois le document enregistré, les modifications sont permanentes. Veillez à conserver une copie ou une sauvegarde du fichier original.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}