---
"description": "Créez des PDF avec du texte et des images avec Aspose.PDF pour .NET. Apprenez à ajouter du texte et des images en ligne étape par étape."
"linktitle": "Texte et image sous forme de paragraphe dans un fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Texte et image sous forme de paragraphe dans un fichier PDF"
"url": "/fr/net/programming-with-text/text-and-image-as-paragraph/"
"weight": 530
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Texte et image sous forme de paragraphe dans un fichier PDF

## Introduction

Dans le monde numérique d'aujourd'hui, le PDF est un format de document universel que la plupart d'entre nous utilisons quotidiennement. Qu'il s'agisse d'un rapport, d'un livre numérique ou d'une facture commerciale, le PDF facilite le partage d'informations sur différentes plateformes. Mais comment personnaliser un PDF par programmation ? C'est là qu'Aspose.PDF pour .NET entre en jeu. Dans ce tutoriel, nous vous guiderons dans l'insertion de texte et d'images sous forme de paragraphes dans un fichier PDF avec Aspose.PDF pour .NET.

## Prérequis

Avant de plonger dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin pour suivre en douceur :

- Bibliothèque Aspose.PDF pour .NET : vous devez installer Aspose.PDF pour .NET. Vous pouvez la télécharger. [ici](https://releases.aspose.com/pdf/net/).
- Visual Studio : toute version prenant en charge .NET fonctionnera parfaitement.
- Compréhension de base de C# : une certaine familiarité avec C# sera utile, mais ne vous inquiétez pas, je vous guiderai à chaque étape !
- Document PDF prêt : si vous souhaitez ajouter une image personnalisée, préparez-la.

Vous pouvez également obtenir un essai gratuit de la bibliothèque [ici](https://releases.aspose.com/), ou si vous travaillez sur un projet à grande échelle, envisagez de l'acheter [ici](https://purchase.aspose.com/buy)Besoin de plus de détails ? Consultez la documentation. [ici](https://reference.aspose.com/pdf/net/).

## Importer des packages

Pour démarrer avec Aspose.PDF pour .NET, vous devez importer les espaces de noms requis. Ces espaces de noms permettent à votre code C# d'interagir avec les fonctionnalités d'Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

Simple, non ? Passons maintenant à la partie amusante : créer votre propre fichier PDF.

## Guide étape par étape : création d'un PDF avec texte et image intégrée

Décomposons cela en étapes simples et faciles à suivre. Imaginez que vous assemblez un puzzle ; chaque étape consiste à trouver et à placer la bonne pièce.

## Étape 1 : Initialiser le document PDF

La première étape consiste à initialiser un nouveau document PDF avec Aspose.PDF. Ce document servira de base pour l'ajout de texte et d'images.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Instancier une instance de document
Document doc = new Document();
```

Que se passe-t-il ici ? Nous créons simplement un nouveau document en utilisant `Document` et définissez le répertoire où enregistrer le PDF. C'est comme ouvrir une nouvelle toile pour votre chef-d'œuvre !

## Étape 2 : ajouter une page à votre PDF

Un document ne sert à rien sans pages, n'est-ce pas ? Ajoutons une page vierge à votre document.

```csharp
// Ajouter une page à la collection de pages de l'instance de document
Page page = doc.Pages.Add();
```

Cet extrait de code ajoute une nouvelle page à la collection de pages de votre document. Imaginez-le comme ouvrir une page blanche dans un cahier.

## Étape 3 : Ajouter du texte sous forme de paragraphe

Ensuite, nous allons ajouter un paragraphe de texte. C'est ici que vous pourrez insérer votre message ou votre titre.

```csharp
// Créer un fragment de texte
TextFragment text = new TextFragment("Hello World.. ");
// Ajouter un fragment de texte à la collection de paragraphes de l'objet Page
page.Paragraphs.Add(text);
```

Ici, nous créons un `TextFragment` Objet contenant le texte « Hello World… », qui est ensuite ajouté à la page sous forme de paragraphe. C'est comme écrire la première phrase d'un document PDF.

## Étape 4 : ajouter une image en tant que paragraphe en ligne

Maintenant que nous avons le texte, pimentons le tout en ajoutant une image sous forme de paragraphe. Un paragraphe en ligne signifie simplement que l'image apparaîtra juste après le texte, un peu comme les images dans les documents Word.

```csharp
// Créer une instance d'image
Aspose.Pdf.Image image = new Aspose.Pdf.Image();
// Définir l'image comme paragraphe en ligne afin qu'elle apparaisse juste après 
// L'objet paragraphe précédent (TextFragment)
image.IsInLineParagraph = true;
// Spécifier le chemin du fichier image 
image.File = dataDir + "aspose-logo.jpg";
```

Dans cet extrait, nous créons un `Image` objet, indiquez-lui de s'aligner sur le texte et spécifiez le chemin d'accès au fichier image. Cela revient à coller une image juste après une phrase dans un document. Vous pouvez remplacer « aspose-logo.jpg » par l'image de votre choix.

## Étape 5 : Définir la taille de l’image (facultatif)

Vous souhaitez redimensionner l'image ? Aucun problème. Aspose.PDF vous permet d'ajuster la hauteur et la largeur de l'image avant de l'ajouter à votre document.

```csharp
// Définir la hauteur de l'image (facultatif)
image.FixHeight = 30;
// Définir la largeur de l'image (facultatif)
image.FixWidth = 100;
```

Cette partie est facultative, mais elle vous permet de contrôler la taille de l'image dans votre PDF. C'est comme redimensionner une photo avant de l'imprimer.

## Étape 6 : Ajouter une image à la collection de paragraphes

Nous avons préparé l'image. Insérons-la maintenant dans le document sous forme de paragraphe en ligne.

```csharp
// Ajouter une image à la collection de paragraphes de l'objet de page
page.Paragraphs.Add(image);
```

Cette ligne ajoute l'image juste après le texte dans la collection de paragraphes. C'est comme cliquer sur le bouton « Insérer une image » dans un éditeur de texte.

## Étape 7 : ajouter un autre paragraphe de texte en ligne

Et si vous souhaitez ajouter du texte juste après l'image ? Insérons un autre fragment de texte en ligne.

```csharp
// Réinitialiser l'objet TextFragment avec un contenu différent
text = new TextFragment(" Hello Again..");
// Définir TextFragment comme paragraphe en ligne
text.IsInLineParagraph = true;
// Ajouter le TextFragment nouvellement créé à la collection de paragraphes de la page
page.Paragraphs.Add(text);
```

Nous réutilisons le `TextFragment` Ajoutez ici un objet avec le nouveau texte (« Bonjour ») et insérez-le directement, juste après l'image. Cela donne à votre PDF un aspect fluide et cohérent.

## Étape 8 : Enregistrer le document PDF

Nous avons presque terminé ! Maintenant, enregistrons le document dans le répertoire spécifié.

```csharp
dataDir = dataDir + "TextAndImageAsParagraph_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nText and image added successfully as inline paragraphs.\nFile saved at " + dataDir);
```

Cette dernière étape enregistre le fichier dans votre répertoire sous le nom « TextAndImageAsParagraph_out.pdf ». Félicitations ! Vous avez créé un PDF contenant du texte et des images intégrées !

## Conclusion

Et voilà : créer un PDF avec du texte et des images sous forme de paragraphes intégrés avec Aspose.PDF pour .NET est aussi simple que de suivre ces étapes. En quelques lignes de code, vous pouvez ajouter du contenu dynamique à vos fichiers PDF, les rendant ainsi plus attrayants et professionnels. Qu'il s'agisse d'un rapport d'activité ou d'un livre numérique, maîtriser la mise en page de vos PDF peut faire toute la différence.

## FAQ

### Puis-je ajouter plusieurs images sous forme de paragraphes en ligne ?  
Oui, vous pouvez ajouter plusieurs images en créant des fichiers séparés. `Image` objets et les ajouter à la collection de paragraphes.

### Puis-je contrôler la position du texte et de l'image dans le PDF ?  
Oui, en utilisant des propriétés telles que les marges, vous pouvez contrôler le placement précis de votre texte et de vos images.

### Aspose.PDF pour .NET est-il gratuit ?  
Non, c'est un produit sous licence, mais vous pouvez en obtenir un [essai gratuit](https://releases.aspose.com/) ou acheter une licence [ici](https://purchase.aspose.com/buy).

### Puis-je ajouter des hyperliens au texte ?  
Oui, Aspose.PDF vous permet d'ajouter des hyperliens dans des fragments de texte. Vérifiez la [documentation](https://reference.aspose.com/pdf/net/) pour plus de détails.

### Puis-je personnaliser la police et le style du texte ?  
Absolument ! Vous pouvez facilement personnaliser les polices, les couleurs et autres caractéristiques de style des fragments de texte.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}