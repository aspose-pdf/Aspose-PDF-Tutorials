---
"description": "Découvrez comment faire pivoter du texte à l’aide d’un fragment de texte et d’un paragraphe dans un document PDF à l’aide d’Aspose.PDF pour .NET."
"linktitle": "Faire pivoter le texte à l'aide d'un fragment de texte et d'un paragraphe"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Faire pivoter le texte à l'aide d'un fragment de texte et d'un paragraphe"
"url": "/fr/net/programming-with-text/rotate-text-using-text-fragment-and-paragraph/"
"weight": 400
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Faire pivoter le texte à l'aide d'un fragment de texte et d'un paragraphe

## Introduction

Pour générer des documents dynamiques, le format PDF est la référence. Grâce à son attrait universel et à son professionnalisme attendu, il est couramment utilisé dans différents secteurs, notamment le droit, l'éducation et les entreprises. Dans cet article, nous allons examiner de plus près comment exploiter Aspose.PDF pour .NET pour créer un document PDF avec des fragments de texte pivotés, idéal pour donner du style à vos documents ou mettre en valeur des informations importantes. C'est parti !

## Prérequis

Avant de plonger dans les détails techniques, assurez-vous d’avoir quelques éléments en place :

1. Compréhension de base de .NET Framework : une connaissance de C# ou de VB.NET sera bénéfique car Aspose.PDF fonctionne parfaitement avec les applications .NET.
  
2. Bibliothèque Aspose.PDF pour .NET : Vous aurez besoin de la bibliothèque Aspose.PDF. Pas d'inquiétude, elle est facile à télécharger ! Vous pouvez l'obtenir ici : [Télécharger Aspose.PDF pour .NET](https://releases.aspose.com/pdf/net/).

3. Environnement de développement : vous pouvez utiliser n'importe quel IDE prenant en charge le développement .NET, comme Visual Studio. Assurez-vous que votre IDE peut accéder à la bibliothèque Aspose.PDF téléchargée.

4. Une licence temporaire (facultative) : Bien que vous puissiez commencer avec l'essai gratuit, si vous devez créer une application de production, envisagez d'acquérir une [permis temporaire](https://purchase.aspose.com/temporary-license/) pour une fonctionnalité complète.

5. Connexion Internet : cela peut sembler évident, mais vous en aurez besoin pour accéder à la documentation en ligne pour obtenir des conseils supplémentaires et un dépannage.

Une fois vos prérequis réglés, il est temps de passer à l'action !

## Importer des packages

Avant de lancer la partie codage, nous devons nous assurer que nous importons les packages nécessaires dans notre projet .NET. 

Pour commencer, assurez-vous d’utiliser les espaces de noms suivants en haut de votre fichier C# :

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
```

Cela vous permettra d'accéder aux fonctionnalités de manipulation de documents PDF et aux fonctionnalités de texte fournies par la bibliothèque Aspose.PDF.

Et maintenant, place au fun ! Nous allons créer une application simple pour générer un document PDF contenant des fragments de texte standard et pivotés. Prenez une grande inspiration et découvrons-la étape par étape.

## Étape 1 : Initialiser l'objet Document

Dans cette étape, nous allons créer un nouveau document PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Initialiser l'objet document
Document pdfDocument = new Document();
```

Cette ligne de code crée une nouvelle toile pour créer notre contenu. Imaginez-la comme verser une nouvelle couche de peinture sur votre toile. C'est passionnant !

## Étape 2 : Ajouter une page

Ensuite, nous devons ajouter une page à notre document. C'est là que la magie opère.

```csharp
// Obtenir une page particulière
Page pdfPage = (Page)pdfDocument.Pages.Add();
```

Imaginez cette étape comme la pose des fondations de votre chef-d'œuvre. Sans page, rien ne peut être peint ou écrit !

## Étape 3 : Créez votre premier fragment de texte

Nous allons maintenant ajouter du texte à notre PDF. Commençons par un extrait de texte standard.

```csharp
// Créer un fragment de texte
TextFragment textFragment1 = new TextFragment("main text");
// Définir les propriétés du texte
textFragment1.TextState.FontSize = 12;
textFragment1.TextState.Font = FontRepository.FindFont("TimesNewRoman");
```

Ici, nous avons créé notre premier fragment de texte nommé `textFragment1`Nous définissons également ses propriétés de police, vous savez, pour lui donner une belle apparence !

## Étape 4 : ajouter le premier fragment de texte à la page

Notre fragment de texte étant prêt, il est temps de le mettre sur la page.

```csharp
pdfPage.Paragraphs.Add(textFragment1);
```

Ce code place votre texte standard sur la toile. C'est comme poser votre pinceau sur la toile pour créer la première ligne de votre œuvre !

## Étape 5 : Créer des fragments de texte pivotés

Ensuite, nous allons ajouter du texte pivoté pour attirer le regard. C'est parti !

### Création du premier fragment de texte pivoté

```csharp
// Créer un fragment de texte
TextFragment textFragment2 = new TextFragment("rotated text");
// Définir les propriétés du texte
textFragment2.TextState.FontSize = 12;
textFragment2.TextState.Font = FontRepository.FindFont("TimesNewRoman");
// Définir la rotation
textFragment2.TextState.Rotation = 315;
```

Dans cet extrait, nous avons créé un fragment de texte nommé `textFragment2`Nous avons réglé sa rotation à 315 degrés, ce qui est bien incliné, mais pas complètement à l'envers. Cela pourrait représenter un texte nécessitant un peu de style !

### Ajout du fragment de texte pivoté à la page

Il est temps d’ajouter également ce texte accrocheur à la page !

```csharp
pdfPage.Paragraphs.Add(textFragment2);
```

Génial, non ? C'est comme ajouter une touche de couleur à votre toile pour la faire ressortir !

### Création d'un autre fragment de texte pivoté

Ajoutons un autre fragment de texte pivoté pour faire bonne mesure.

```csharp
// Créer un fragment de texte
TextFragment textFragment3 = new TextFragment("another rotated text");
// Définir les propriétés du texte
textFragment3.TextState.FontSize = 12;
textFragment3.TextState.Font = FontRepository.FindFont("TimesNewRoman");
// Définir la rotation
textFragment3.TextState.Rotation = 270;
```

Comme précédemment, nous ajoutons un autre texte pivoté. Cette fois, il est tourné à 270 degrés, presque à l'envers !

## Étape 6 : ajouter le deuxième fragment de texte pivoté à la page

Maintenant, ajoutons cette touche finale.

```csharp
pdfPage.Paragraphs.Add(textFragment3);
```

De cette façon, vous avez plusieurs fragments de texte pivotés fonctionnant ensemble sur la toile !

## Étape 7 : Enregistrer le document

Maintenant que nous avons un document rempli d'éléments fantastiques, terminons les choses en le sauvegardant.

```csharp
// Enregistrer le document
pdfDocument.Save(dataDir + "TextFragmentTests_Rotated3_out.pdf");
```

Et voilà ! Votre chef-d'œuvre créatif est enregistré au format PDF. Imaginez-le comme une exposition dans une galerie : il est prêt à être découvert !

## Conclusion

Félicitations ! Vous venez de créer un document PDF dynamique avec des fragments de texte standard et pivotés à l'aide d'Aspose.PDF pour .NET. Cela ouvre un monde de possibilités pour présenter vos informations. Que vous souhaitiez mettre en valeur les points clés d'un rapport ou simplement ajouter une touche visuelle à vos documents, ces techniques vous aideront à atteindre vos objectifs.

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?

Aspose.PDF pour .NET est une bibliothèque robuste qui permet aux développeurs de créer, manipuler et convertir des fichiers PDF à l'aide d'applications .NET.

### Puis-je utiliser Aspose.PDF dans une application Web ?

Absolument ! Aspose.PDF peut être intégré à n'importe quelle application .NET, y compris les applications web, les applications de bureau et les services.

### Existe-t-il un essai gratuit disponible pour Aspose.PDF ?

Oui, vous pouvez bénéficier d'un essai gratuit pour découvrir ses fonctionnalités avant de l'acheter. Découvrez-le sur [Essai gratuit d'Aspose](https://releases.aspose.com/).

### Comment puis-je faire pivoter du texte dans un PDF à l'aide d'Aspose.PDF ?

Vous pouvez faire pivoter le texte en définissant le `Rotation` propriété d'un `TextFragment` objet, comme démontré dans ce tutoriel.

### Où puis-je trouver de l'aide pour Aspose.PDF ?

Pour toute assistance ou question, vous pouvez visiter le [Forum d'assistance Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}