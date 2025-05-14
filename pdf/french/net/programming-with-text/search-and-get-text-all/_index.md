---
"description": "Découvrez comment rechercher et obtenir du texte à partir de toutes les pages d’un document PDF à l’aide d’Aspose.PDF pour .NET."
"linktitle": "Rechercher et obtenir tout le texte"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Rechercher et obtenir tout le texte"
"url": "/fr/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rechercher et obtenir tout le texte

## Introduction

Avez-vous déjà eu besoin d'extraire du texte d'un PDF, mais avez-vous trouvé la tâche difficile ? Les PDF peuvent parfois ressembler à des conteneurs verrouillés, ce qui complique l'accès aux informations nécessaires. Mais voici la bonne nouvelle : avec Aspose.PDF pour .NET, vous pouvez facilement rechercher et récupérer du texte dans n'importe quel PDF. Cette puissante bibliothèque fournit tout ce dont vous avez besoin pour travailler avec des PDF dans vos applications .NET, simplifiant ainsi l'extraction de texte. Dans ce tutoriel, nous vous expliquerons comment rechercher et extraire du texte d'un fichier PDF avec Aspose.PDF pour .NET. Que vous développiez un outil d'analyse de texte ou que vous souhaitiez simplement automatiser l'extraction de données à partir de rapports PDF, vous êtes au bon endroit !

## Prérequis

Avant de passer au code, assurons-nous que tout est configuré :

1. Aspose.PDF pour .NET : Vous devez télécharger et installer Aspose.PDF pour .NET. Vous pouvez l'obtenir depuis la page de téléchargement. [ici](https://releases.aspose.com/pdf/net/).
2. Environnement .NET : assurez-vous que .NET Framework ou .NET Core est configuré sur votre machine de développement.
3. Connaissances de base en C## : une certaine familiarité avec C# et le travail avec des projets .NET sont recommandés.
4. Document PDF : Exemple de fichier PDF à partir duquel nous allons extraire du texte. Dans cet exemple, nous utiliserons `SearchAndGetTextFromAll.pdf`.

## Importer des packages

Avant d'écrire du code, vous devez importer les espaces de noms nécessaires dans votre projet pour travailler avec Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Ces espaces de noms donnent accès au modèle d'objet de document du PDF et nous permettent de manipuler le texte dans le fichier.

Décomposons le processus en étapes simples afin que vous puissiez le suivre facilement.

## Étape 1 : Définir le répertoire du document

Tout d'abord, vous devez spécifier le chemin d'accès au répertoire où se trouve votre PDF. Cela permet à l'application de localiser le fichier dont vous extrairez le texte.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- Le `dataDir` la variable doit pointer vers le répertoire où se trouve votre `SearchAndGetTextFromAll.pdf` le fichier est stocké.
- Remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin réel sur votre machine.

## Étape 2 : ouvrez le document PDF

Ensuite, nous allons ouvrir le document PDF en utilisant Aspose.PDF `Document` objet.

```csharp
// Ouvrir le document
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- Nous créons une nouvelle instance du `Document` classe en passant le chemin complet du fichier PDF.
- Cela chargera le PDF en mémoire, le rendant prêt à être traité.

## Étape 3 : Créer un absorbeur de texte

Le `TextFragmentAbsorber` L'objet permet de rechercher un texte spécifique dans le PDF. Dans ce cas, nous rechercherons le mot « texte ».

```csharp
// Créez un objet TextAbsorber pour rechercher toutes les instances de la phrase de recherche d'entrée
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- Le `TextFragmentAbsorber` est initialisé avec la chaîne `"text"`Cela signifie qu'il recherchera toutes les occurrences du mot « texte » dans le document PDF.

## Étape 4 : Accepter l'absorbeur pour toutes les pages

Nous allons maintenant demander au document PDF d’accepter l’absorbeur et de rechercher le texte sur toutes ses pages.

```csharp
// Accepter l'absorbeur pour toutes les pages
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Le `Accept` La méthode est appliquée aux pages du document. Elle recherchera le texte spécifié dans toutes les pages.

## Étape 5 : Extraire des fragments de texte

Une fois que l'absorbeur a scanné le document, nous pouvons récupérer les fragments de texte extraits.

```csharp
// Obtenir les fragments de texte extraits
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- Le `TextFragments` propriété de la `TextFragmentAbsorber` renvoie une collection de tous les fragments de texte qui correspondent au terme de recherche.

## Étape 6 : Parcourir les fragments de texte

Maintenant que nous avons la collection de fragments de texte, nous allons les parcourir et en extraire les détails.

```csharp
// Boucle à travers les fragments
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- Le `foreach` la boucle parcourt chaque `TextFragment` dans la collection.
- Nous imprimons diverses propriétés de chaque fragment, telles que le texte réel, sa position sur la page, les détails de la police et la taille de la police.
- Le `XIndent` et `YIndent` les propriétés donnent les coordonnées exactes du fragment de texte dans le PDF.

## Conclusion

Et voilà ! En quelques lignes de code, nous avons réussi à rechercher et extraire du texte d'un PDF avec Aspose.PDF pour .NET. La flexibilité d'Aspose.PDF permet de manipuler les PDF de multiples façons, ce qui en fait un excellent choix pour les développeurs à la recherche de solutions PDF robustes dans les environnements .NET. Vous pouvez facilement étendre cet exemple pour rechercher d'autres mots, extraire plus de détails ou même manipuler le contenu du PDF selon vos besoins. Nous espérons que ce guide vous a donné une approche claire et simple de l'utilisation des PDF. N'hésitez pas à l'essayer avec vos propres PDF !

## FAQ

### Puis-je rechercher plusieurs mots à la fois ?  
Oui, vous pouvez modifier le `TextFragmentAbsorber` pour rechercher plusieurs phrases en ajustant la chaîne de recherche en conséquence.

### Que se passe-t-il si le texte s’étend sur plusieurs lignes ?  
Aspose.PDF reconnaîtra et extraira le texte même s'il s'étend sur plusieurs lignes. Vous pouvez gérer ces fragments individuellement.

### Comment enregistrer le texte extrait dans un fichier ?  
Vous pouvez écrire le texte extrait dans un fichier à l'aide d'opérations d'E/S de fichier C# standard, telles que `StreamWriter`.

### Aspose.PDF prend-il en charge l'extraction de texte à partir de fichiers PDF numérisés ?  
Aspose.PDF ne prend pas en charge l'OCR. Pour les PDF numérisés, un outil OCR est nécessaire pour reconnaître le texte.

### Comment gérer les PDF cryptés ?  
Si votre PDF est protégé par mot de passe, vous pouvez le déverrouiller à l'aide d'Aspose.PDF en fournissant le mot de passe lors du chargement du document.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}