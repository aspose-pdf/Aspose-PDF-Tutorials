---
"description": "Apprenez à rechercher du texte dans des PDF et à le surligner avec des rectangles grâce à Aspose.PDF pour .NET ! Tutoriel simple et étape par étape pour améliorer vos compétences en manipulation de PDF."
"linktitle": "Rechercher du texte et dessiner un rectangle"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Rechercher du texte et dessiner un rectangle"
"url": "/fr/net/programming-with-text/search-text-and-draw-rectangle/"
"weight": 460
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rechercher du texte et dessiner un rectangle

## Introduction

Vous souhaitez améliorer vos compétences en manipulation de PDF ? Vous souhaitez apprendre à rechercher du texte spécifique dans vos fichiers PDF et à le surligner avec un rectangle ? Vous êtes tombé sur le guide idéal ! Aujourd'hui, je vous explique comment utiliser Aspose.PDF pour .NET pour rechercher du texte dans un document PDF et dessiner des rectangles autour. Cet article vous propose un tutoriel étape par étape, clair et pratique, pour vous permettre de suivre et d'appliquer ces techniques à vos projets. 

## Prérequis

Avant de plonger dans le tutoriel, préparons ce dont vous avez besoin pour assurer un flux de travail fluide :

1. Compréhension de base de .NET : vous devez être familiarisé avec la programmation C# et le framework .NET pour suivre efficacement ce didacticiel.
   
2. Visual Studio installé : vous aurez besoin d'un environnement de développement intégré (IDE) pour écrire et tester votre code. Visual Studio Community est une excellente option, et c'est gratuit.
   
3. Aspose.PDF pour .NET : la bibliothèque Aspose.PDF doit être installée dans votre projet. Vous pouvez la télécharger. [ici](https://releases.aspose.com/pdf/net/) ou envisager un [permis temporaire](https://purchase.aspose.com/temporary-license/) pour des fonctionnalités étendues.
   
4. Exemple de document PDF : pour ce tutoriel, vous aurez besoin d’un exemple de fichier PDF nommé `SearchAndGetTextFromAll.pdf` stocké dans votre répertoire de projet. 

## Importer des packages

Pour commencer, vous devez d'abord importer les packages nécessaires dans votre projet .NET. Suivez ces étapes :

### Ouvrez Visual Studio

Lancez Visual Studio et créez une nouvelle application console ou utilisez-en une existante dans laquelle vous souhaitez implémenter les fonctionnalités PDF.

### Ajoutez Aspose.PDF à votre projet

1. Cliquez avec le bouton droit sur votre projet dans l’Explorateur de solutions.
2. Sélectionnez « Gérer les packages NuGet ».
3. Rechercher `Aspose.PDF` et installez la dernière version.

En faisant cela, vous posez les bases de toutes les manipulations PDF étonnantes que vous êtes sur le point d’effectuer.

## Importer des espaces de noms

En haut de votre fichier programme, vous souhaiterez importer les espaces de noms pertinents de la bibliothèque Aspose :

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Facades;
```

Cela facilite l'accès aux classes et aux méthodes de la bibliothèque Aspose.PDF pour vos tâches.


Maintenant que tout est configuré, décomposons le processus de recherche de texte dans un PDF et de dessin d'un rectangle autour de celui-ci en étapes gérables.

## Étape 1 : Définissez le chemin d’accès de votre document

Tout d'abord, définissez le chemin d'accès à votre fichier PDF. Assurez-vous de remplacer `YOUR DOCUMENT DIRECTORY` avec le chemin réel où votre `SearchAndGetTextFromAll.pdf` est stocké.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## Étape 2 : ouvrez le document PDF

Ensuite, créez une instance du `Document` classe pour charger votre PDF :

```csharp
Document document = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

Cette ligne de code ouvre votre fichier PDF spécifié, vous permettant de le manipuler davantage.

## Étape 3 : Créer un absorbeur de texte

Il vous faut maintenant un moyen de rechercher du texte dans ce document. Pour cela, nous utilisons la fonction `TextFragmentAbsorber`:

```csharp
TextFragmentAbsorber textAbsorber = new TextFragmentAbsorber(@"[\S]+");
```

L'expression régulière `@"[\S]+"` est conçu pour correspondre à n'importe quelle chaîne non blanche dans le PDF. 

## Étape 4 : Configurer les options de recherche de texte

Ensuite, vous devez configurer les options de recherche de texte :

```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textAbsorber.TextSearchOptions = textSearchOptions;
```

Ici, le `true` Ce paramètre signifie que la recherche sera sensible à la casse. Vous pouvez le définir sur `false` si vous souhaitez une recherche insensible à la casse.

## Étape 5 : Accepter l'absorbeur de texte dans le document

Avec votre `TextFragmentAbsorber` et les options de recherche prêtes, il est temps d'absorber le texte du document :

```csharp
document.Pages.Accept(textAbsorber);
```

Cette méthode examine chaque page de votre PDF pour trouver des fragments de texte correspondant au modèle spécifié.

## Étape 6 : Créer un éditeur de contenu PDF

Pour dessiner des formes sur le document, vous aurez besoin de `PdfContentEditor`:

```csharp
var editor = new PdfContentEditor(document);
```

Cet éditeur vous permet de manipuler et d'éditer facilement le contenu PDF.

## Étape 7 : Parcourir les fragments de texte trouvés

Maintenant, vous voudrez parcourir les fragments de texte trouvés pour dessiner des rectangles autour d'eux :

```csharp
foreach (TextFragment textFragment in textAbsorber.TextFragments)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        DrawBox(editor, textFragment.Page.Number, textSegment, System.Drawing.Color.Red);
    }
}
```

Cette boucle parcourt chaque fragment de texte et ses segments, appelant un `DrawBox` méthode de dessin de rectangle.

## Étape 8 : Définir la méthode DrawBox

Vous devez définir le `DrawBox` Méthode qui gère la logique de dessin du rectangle. Voici une implémentation simple :

```csharp
private static void DrawBox(PdfContentEditor editor, int pageNumber, TextSegment textSegment, System.Drawing.Color color)
{
    // Calculer les dimensions du rectangle en fonction du segment de texte
    float x = textSegment.Rectangle.LLX;
    float y = textSegment.Rectangle.LLY;
    float width = textSegment.Rectangle.Width;
    float height = textSegment.Rectangle.Height;

    // Dessinez un rectangle en utilisant les valeurs calculées
    editor.DrawRectangle(pageNumber, x, y, width, height, color, 1);
}
```

Cette méthode détermine la position et la taille du rectangle en fonction du rectangle de délimitation du segment et utilise l'éditeur pour le dessiner.

## Étape 9 : Enregistrer le document modifié

Après avoir dessiné les rectangles autour du texte trouvé, vous pouvez enregistrer le document modifié :

```csharp
dataDir = dataDir + "SearchTextAndDrawRectangle_out.pdf";
document.Save(dataDir);
```

Assurez-vous que votre nouveau fichier est enregistré sous un nom distinct pour éviter d’écraser votre document d’origine.

## Étape 10 : Message de confirmation

Enfin, imprimez un message de confirmation sur la console pour vous faire savoir que l'opération a réussi :

```csharp
Console.WriteLine("\nRectangle drawn successfully on searched text.\nFile saved at " + dataDir);
```

Et voilà ! Vous avez réussi à créer un script pour rechercher du texte dans un PDF et le mettre en évidence avec des rectangles.

## Conclusion

Félicitations ! Vous venez de débloquer une compétence puissante qui peut grandement améliorer vos compétences en manipulation de PDF grâce à Aspose.PDF pour .NET. En quelques étapes simples, vous pouvez rechercher n'importe quel texte dans votre document et le surligner visuellement, rendant ainsi vos documents PDF plus interactifs et faciles à gérer. N'hésitez pas à tester différents modèles d'expressions régulières et options de couleurs pour personnaliser cet outil !

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque qui fournit un moyen complet de créer, manipuler et convertir des documents PDF par programmation.

### Puis-je utiliser Aspose.PDF gratuitement ?
Oui, Aspose propose un essai gratuit pour tester les fonctionnalités de la bibliothèque. Découvrez-le. [ici](https://releases.aspose.com/).

### Quel langage de programmation dois-je utiliser avec Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est conçu pour être utilisé avec C# et d'autres langages .NET.

### Comment obtenir de l'aide avec Aspose.PDF ?
Vous pouvez consulter le forum d'assistance Aspose pour obtenir de l'aide concernant tout problème ou toute question. [ici](https://forum.aspose.com/c/pdf/10).

### Où puis-je télécharger Aspose.PDF pour .NET ?
Vous pouvez télécharger la bibliothèque à partir du site Web d'Aspose, [ici](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}