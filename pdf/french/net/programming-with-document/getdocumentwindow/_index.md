---
"description": "Découvrez comment utiliser la fonctionnalité GetDocumentWindow d'Aspose.PDF pour .NET pour récupérer des informations sur les propriétés de la fenêtre d'un document PDF."
"linktitle": "Fenêtre Obtenir un document"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Fenêtre Obtenir un document"
"url": "/fr/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Fenêtre Obtenir un document

# Introduction

Vous travaillez avec des PDF et souhaitez mieux contrôler leur affichage à l'ouverture ? Qu'il s'agisse de masquer la barre de menus ou de redimensionner la fenêtre pour l'adapter à la première page, Aspose.PDF pour .NET vous offre tous les outils nécessaires pour personnaliser le comportement d'un PDF à l'ouverture dans une visionneuse. Dans ce tutoriel, nous allons vous expliquer comment récupérer et manipuler les paramètres de la fenêtre d'un document dans Aspose.PDF pour .NET.


# Prérequis

Avant de plonger dans le didacticiel, assurez-vous que vous disposez des prérequis suivants :

- Aspose.PDF pour .NET installé sur votre environnement de développement.
  - [Télécharger Aspose.PDF pour .NET](https://releases.aspose.com/pdf/net/)
- Une licence valide pour Aspose.PDF, ou vous pouvez obtenir une [essai gratuit](https://releases.aspose.com/) ou [permis temporaire](https://purchase.aspose.com/temporary-license/).
- Compréhension de base de .NET et C#.
- Visual Studio ou un autre IDE approprié.

# Importer des packages

Avant de commencer à écrire du code, vous devez importer les packages nécessaires. Ouvrez votre projet et, en haut de votre fichier C#, ajoutez l'espace de noms suivant :

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Cela vous donnera accès à toutes les classes et méthodes nécessaires à la manipulation de documents PDF à l'aide d'Aspose.PDF pour .NET.

Décomposons maintenant le processus de récupération des différents paramètres de la fenêtre d'un document. Pour cet exemple, nous utiliserons un fichier PDF nommé `GetDocumentWindow.pdf`.

## Étape 1 : définir le chemin du répertoire du document

Tout d'abord, nous devons définir le chemin d'accès à notre fichier PDF. Il est essentiel que le chemin d'accès soit correct pour éviter toute erreur lors de l'exécution.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ici, remplacez `"YOUR DOCUMENT DIRECTORY"` avec le répertoire où se trouve votre fichier PDF. Il s'agit du répertoire de travail à partir duquel vous chargerez le document PDF.

## Étape 2 : ouvrez le document PDF

Une fois le chemin d'accès défini, l'étape suivante consiste à ouvrir le document PDF avec Aspose.PDF. Le document sera alors chargé en mémoire et vous pourrez récupérer ses propriétés.

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

Avec cette simple ligne de code, vous avez chargé avec succès votre fichier PDF dans le `pdfDocument` objet, qui vous permettra désormais d'accéder à toutes ses propriétés.

## Étape 3 : Récupérer l'état de centrage de la fenêtre

Vérifions ensuite si la fenêtre du document doit être centrée à l'ouverture. La valeur par défaut est : `false`.

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

Si la sortie est `true`, la fenêtre du document s'ouvrira au centre de l'écran. Sinon, elle s'ouvrira à sa position par défaut.

## Étape 4 : Vérifiez le sens du texte

Un autre aspect crucial de l'apparence d'un PDF est l'orientation du texte, qui détermine si le texte se lit de gauche à droite (G2D) ou de droite à gauche (D2G). Vous pouvez récupérer cette information avec le code suivant :

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

Le résultat sera `L2R` pour le texte de gauche à droite et `R2L` pour le texte de droite à gauche. Ce paramètre est particulièrement utile pour les documents en langues comme l'arabe ou l'hébreu.

## Étape 5 : Afficher le titre du document dans la fenêtre

La propriété suivante vous permet de contrôler si le titre du document ou le nom du fichier doit être affiché dans la barre de titre de la fenêtre. Par défaut, cette propriété est définie sur `false`, ce qui signifie que le nom du fichier sera affiché.

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

Si vous souhaitez que le titre du document soit affiché à la place du nom du fichier, ce paramètre doit être activé.

## Étape 6 : redimensionner la fenêtre pour l'adapter à la première page

Vous pouvez parfois souhaiter que la fenêtre du document se redimensionne automatiquement pour s'adapter à la première page du PDF à son ouverture. Voici comment vérifier si cette fonctionnalité est activée :

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

Par défaut, cette option est définie sur `false`, ce qui signifie que la taille de la fenêtre restera telle quelle quelle que soit la taille de la première page.

## Étape 7 : Masquer la barre de menus

Pour une expérience de lecture plus ciblée, vous pouvez masquer la barre de menus de l'application de visualisation. Vous pouvez récupérer ce paramètre en utilisant la ligne suivante :

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

Cela reviendra `true` si la barre de menu est masquée, et `false` sinon.

## Étape 8 : Masquer la barre d’outils

De même, vous pouvez masquer la barre d'outils dans la visionneuse PDF pour une interface utilisateur plus claire. Ce paramètre peut être récupéré comme suit :

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

Si ce paramètre est activé, la barre d’outils sera masquée lors de l’ouverture du PDF.

## Étape 9 : Masquer les barres de défilement et les éléments de l'interface utilisateur

Si vous souhaitez afficher uniquement le contenu de la page sans aucun élément d'interface utilisateur supplémentaire comme des barres de défilement, ce paramètre contrôle ce comportement :

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

Lorsqu'il est réglé sur `true`, la visionneuse PDF masquera les barres de défilement et autres éléments de l'interface utilisateur, ne laissant que le contenu du document.

## Étape 10 : Définir le mode de page non plein écran

Vous pouvez contrôler l'apparence du document lorsque vous quittez le mode plein écran à l'aide du `NonFullScreenPageMode` propriété. Ce paramètre est utile pour définir comment l'utilisateur doit interagir avec le document en mode non plein écran.

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

La sortie peut être définie sur différents modes tels que les vignettes, les contours ou le panneau de pièces jointes.

## Étape 11 : Définir la mise en page

Ce paramètre vous permet de contrôler la mise en page du document. Par exemple, vous pouvez opter pour une vue page par page ou en colonnes continues :

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

Cela donne aux utilisateurs une certaine flexibilité dans la façon dont ils lisent ou visualisent le contenu du document.

## Étape 12 : Spécifier le mode de page

Enfin, le `PageMode` La propriété définit l'affichage du document à l'ouverture. Les options incluent l'affichage des vignettes, le passage en mode plein écran ou l'affichage du panneau des pièces jointes.

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

En fonction de vos besoins, vous pouvez définir ce mode sur n'importe quel mode adapté à l'objectif de votre PDF.

## Conclusion

Comme vous pouvez le constater, Aspose.PDF pour .NET offre des outils complets pour manipuler l'affichage de vos documents PDF dans différents visualiseurs. Que vous souhaitiez masquer la barre d'outils, centrer la fenêtre ou contrôler l'orientation du texte, Aspose.PDF offre la flexibilité nécessaire pour améliorer l'expérience utilisateur.

# FAQ

### Puis-je personnaliser le niveau de zoom initial du PDF ?
Oui, Aspose.PDF vous permet de définir le niveau de zoom lors de l'ouverture du document.

### Comment puis-je verrouiller la taille de la fenêtre d'un PDF ?
Vous pouvez définir le `FitWindow` propriété pour empêcher le redimensionnement de la fenêtre.

### Aspose.PDF prend-il en charge différents modes de lecture ?
Oui, il prend en charge différents modes tels que le plein écran, les miniatures et les pièces jointes.

### Est-il possible de masquer les barres de défilement dans la visionneuse PDF ?
Absolument, vous pouvez masquer les barres de défilement en définissant le `HideWindowUI` propriété à `true`.

### Puis-je centrer la fenêtre du document lorsqu'elle est ouverte ?
Oui, vous pouvez contrôler cela en définissant le `CenterWindow` propriété.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}