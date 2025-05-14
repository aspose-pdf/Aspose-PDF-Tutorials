---
"description": "Apprenez à extraire efficacement le texte surligné d'un fichier PDF avec Aspose.PDF pour .NET grâce à ce tutoriel. Idéal pour l'analyse de données et la révision de contenu."
"linktitle": "Extraire le texte en surbrillance dans un fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Extraire le texte en surbrillance dans un fichier PDF"
"url": "/fr/net/annotations/extracthighlightedtext/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extraire le texte en surbrillance dans un fichier PDF

## Introduction

Lorsque vous travaillez avec des fichiers PDF, l'extraction du texte surligné peut être cruciale, que ce soit pour l'analyse de données, la révision de contenu ou simplement l'organisation de vos notes. Si vous utilisez Aspose.PDF pour .NET, ce processus est simple et efficace. Dans ce tutoriel, nous vous expliquerons comment extraire le texte surligné d'un document PDF avec Aspose.PDF pour .NET. Nous aborderons tous les aspects, des prérequis aux instructions étape par étape, pour une compréhension complète.

## Prérequis

Avant de plonger dans le code, vous devez mettre en place quelques éléments :

- Bibliothèque Aspose.PDF pour .NET : Assurez-vous d'avoir installé la bibliothèque Aspose.PDF. Sinon, vous pouvez la télécharger depuis le [page de sortie](https://releases.aspose.com/pdf/net/).
- Environnement de développement : vous devez disposer d’un environnement de développement fonctionnel configuré, tel que Visual Studio.
- Connaissances de base de C# : La familiarité avec le langage de programmation C# et la programmation orientée objet est essentielle.
- Une licence Aspose valide : Bien que vous puissiez commencer par un essai gratuit, envisagez d'en obtenir un [permis temporaire](https://purchase.aspose.com/temporary-license/) ou en acheter un auprès de [ici](https://purchase.aspose.com/buy) pour une utilisation sans restriction.

## Importer des packages

Pour commencer, vous devez importer les espaces de noms nécessaires dans votre projet C#. Ceci est essentiel pour accéder aux classes et méthodes fournies par Aspose.PDF pour .NET.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Décomposons maintenant le processus d'extraction du texte surligné d'un fichier PDF avec Aspose.PDF pour .NET. Chaque étape est expliquée en détail pour vous aider à comprendre les concepts sous-jacents et leur mise en œuvre.

## Étape 1 : Configurez votre répertoire de projet

Tout d'abord, vous devez configurer le répertoire de votre projet où se trouve votre fichier PDF. C'est là que la magie opère.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin d'accès au répertoire où se trouve le fichier PDF. C'est dans ce répertoire que l'application récupérera le PDF pour le traiter.

## Étape 2 : Charger le document PDF

Ensuite, chargez le document PDF dont vous souhaitez extraire le texte surligné. Pour ce faire, utilisez l'outil `Document` cours fourni par Aspose.PDF.

```csharp
Document doc = new Document(dataDir + "ExtractHighlightedText.pdf");
```

Le `Document` La classe est instanciée avec le chemin d'accès au fichier PDF. Ici, `"ExtractHighlightedText.pdf"` est le nom du fichier PDF contenant le texte surligné. Assurez-vous que ce fichier existe dans le répertoire spécifié.

## Étape 3 : Accéder à la collection d'annotations

Une fois le document PDF chargé, l'étape suivante consiste à accéder aux annotations sur la première page. Les annotations permettent d'ajouter des informations supplémentaires, comme des surlignages, des commentaires, etc.

```csharp
foreach (Annotation annotation in doc.Pages[1].Annotations)
{
```

Le `Annotations` propriété de la `Page` L'objet donne accès à toutes les annotations d'une page spécifique du PDF. Ici, nous parcourons chaque annotation de la première page.

## Étape 4 : Filtrer les annotations de texte en surbrillance

Maintenant que nous avons accès à toutes les annotations, nous devons filtrer uniquement les annotations textuelles en surbrillance. Pour ce faire, nous vérifions le type de chaque annotation.

```csharp
if (annotation is TextMarkupAnnotation)
{
    TextMarkupAnnotation highlightedAnnotation = annotation as TextMarkupAnnotation;
```

Le `TextMarkupAnnotation` La classe est utilisée pour représenter les annotations de balisage de texte, y compris les surlignages. `is` le mot-clé vérifie si l'annotation est de type `TextMarkupAnnotation`, et si c'est le cas, il convertit l'annotation en `TextMarkupAnnotation`.

## Étape 5 : Extraire le texte en surbrillance

Une fois l’annotation en surbrillance identifiée, l’étape suivante consiste à extraire le texte associé à la surbrillance.

```csharp
TextFragmentCollection collection = highlightedAnnotation.GetMarkedTextFragments();
foreach (TextFragment tf in collection)
{
    Console.WriteLine(tf.Text);
}
```

Le `GetMarkedTextFragments()` la méthode renvoie une collection de `TextFragment` objets, chacun représentant une portion du texte surligné. Nous parcourons cette collection et affichons le texte de chaque fragment dans la console.

## Conclusion

L'extraction du texte surligné d'un PDF avec Aspose.PDF pour .NET est une fonctionnalité puissante qui simplifie votre flux de travail, notamment pour les documents volumineux. En suivant les étapes décrites dans ce tutoriel, vous pourrez facilement implémenter cette fonctionnalité dans vos propres projets. Que vous organisiez vos notes, prépariez des rapports ou effectuiez des analyses de données, cette méthode offre une solution simple pour extraire et exploiter le texte surligné.

## FAQ

### Puis-je extraire d’autres types d’annotations en utilisant cette méthode ?  
Oui, vous pouvez extraire d’autres types d’annotations en modifiant le `if` condition à vérifier pour différents types d'annotations, tels que `TextAnnotation`, `StampAnnotation`, etc.

### Est-il possible d'extraire le texte en surbrillance de toutes les pages du PDF ?  
Absolument ! Vous pouvez parcourir chaque page du document PDF et appliquer la même logique d'extraction pour récupérer le texte surligné de chaque page.

### Ai-je besoin d’une licence pour utiliser Aspose.PDF pour .NET ?  
Bien que vous puissiez commencer par un essai gratuit, il est recommandé d'obtenir un [permis temporaire](https://purchase.aspose.com/temporary-license/) ou achetez une licence complète pour un accès illimité à toutes les fonctionnalités.

### Puis-je enregistrer le texte extrait dans un fichier au lieu de l'imprimer sur la console ?  
Oui, vous pouvez facilement modifier le code pour enregistrer le texte extrait dans un fichier texte ou tout autre format souhaité.

### Aspose.PDF prend-il en charge d'autres plates-formes en plus de .NET ?  
Oui, Aspose.PDF prend également en charge Java et d’autres plates-formes, offrant des fonctionnalités similaires dans différents environnements.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}