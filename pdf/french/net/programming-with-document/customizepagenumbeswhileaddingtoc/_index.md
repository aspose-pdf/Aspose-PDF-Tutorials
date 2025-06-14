---
"description": "Découvrez comment personnaliser les numéros de page tout en ajoutant une table des matières à vos documents PDF à l'aide d'Aspose.PDF pour .NET dans ce didacticiel complet."
"linktitle": "Personnaliser les numéros de page lors de l'ajout de la table des matières"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Personnaliser les numéros de page lors de l'ajout de la table des matières"
"url": "/fr/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Personnaliser les numéros de page lors de l'ajout de la table des matières

## Introduction

Dans le monde de la gestion documentaire, le PDF est roi. C'est le format de référence pour le partage et la conservation de documents sur différentes plateformes. Mais que faire lorsque vous souhaitez enrichir vos documents PDF avec des fonctionnalités comme une table des matières (TDM) ? C'est là qu'Aspose.PDF pour .NET entre en jeu ! Cette puissante bibliothèque permet aux développeurs de manipuler facilement les fichiers PDF, leur permettant d'ajouter, de modifier et de personnaliser du contenu sans effort. Dans ce tutoriel, nous allons découvrir comment personnaliser les numéros de page tout en ajoutant une TDM à vos documents PDF avec Aspose.PDF pour .NET. Alors, à vos codes et c'est parti !

## Prérequis

Avant de passer au code, vous devez mettre en place quelques éléments :

1. Visual Studio : Assurez-vous d'avoir installé Visual Studio sur votre machine. Ce sera notre environnement de développement.
2. Aspose.PDF pour .NET : vous devez télécharger et installer la bibliothèque Aspose.PDF. Vous pouvez la trouver. [ici](https://releases.aspose.com/pdf/net/).
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.
4. Exemple de fichier PDF : Préparez un exemple de fichier PDF que nous pourrons exploiter. Vous pouvez en créer un simple ou télécharger un PDF existant.

## Importer des packages

Pour commencer, nous devons importer les packages nécessaires. Ouvrez votre projet Visual Studio et ajoutez une référence à la bibliothèque Aspose.PDF. Pour ce faire, utilisez le gestionnaire de packages NuGet :

1. Cliquez avec le bouton droit sur votre projet dans l’Explorateur de solutions.
2. Sélectionnez « Gérer les packages NuGet ».
3. Recherchez « Aspose.PDF » et installez-le.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Une fois la bibliothèque installée, vous pouvez commencer à coder !

## Étape 1 : Configurez votre répertoire de documents

Tout d'abord, nous devons configurer notre répertoire de documents. C'est là que nous stockerons nos fichiers PDF d'entrée et de sortie. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

Dans cet extrait, remplacez `YOUR DOCUMENT DIRECTORY` avec le chemin d'accès réel de vos fichiers PDF. Cela nous permettra de charger le PDF existant et d'enregistrer la version modifiée.

## Étape 2 : Charger le fichier PDF existant

Maintenant que notre répertoire de documents est configuré, chargeons le fichier PDF existant. 

```csharp
Document doc = new Document(inFile);
```

Ici, nous créons un nouveau `Document` en transmettant le chemin du fichier d'entrée. Cela nous permet de manipuler le contenu PDF par programmation.

## Étape 3 : Insérer une nouvelle page pour la table des matières

Ensuite, nous devons créer une nouvelle page dans notre PDF où résidera la table des matières.

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

Cette ligne insère une nouvelle page au début du document. La table des matières sera affichée sur cette page.

## Étape 4 : Créer des informations de table des matières

Maintenant, créons un objet pour représenter les informations de la table des matières.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

Dans cette étape, nous créons un `TocInfo` et définissez son titre sur « Table des matières ». Nous personnalisons également la taille et le style de police. `PageNumbersPrefix` est défini sur « P », ce qui préfixera les numéros de page dans la table des matières.

## Étape 5 : Ajouter des titres à la table des matières

Voici la partie amusante ! Nous allons parcourir les pages du document et ajouter des titres à notre table des matières.

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

Dans cette boucle, nous créons un nouveau `Heading` Objet pour chaque page. Nous définissons la page de destination de chaque titre et spécifions le texte à afficher : « Page X », où X est le numéro de page. Enfin, nous ajoutons le titre à la table des matières.

## Étape 6 : Enregistrer le document mis à jour

Après avoir ajouté tous les titres nécessaires, il est temps d'enregistrer notre document mis à jour.

```csharp
doc.Save(outFile);
```

Cette ligne enregistre le PDF modifié avec la table des matières. Vous pouvez maintenant ouvrir le fichier de sortie et consulter votre table des matières personnalisée !

## Conclusion

Et voilà ! Vous avez réussi à personnaliser les numéros de page tout en ajoutant une table des matières à votre document PDF avec Aspose.PDF pour .NET. Cette puissante bibliothèque simplifie la manipulation des fichiers PDF et, en quelques lignes de code seulement, vous pouvez améliorer considérablement vos documents. Que vous créiez des rapports, des livres numériques ou tout autre type de PDF, une table des matières peut grandement améliorer la navigation pour vos lecteurs. Alors, qu'attendez-vous ? Lancez-vous dans Aspose.PDF et commencez à créer des PDF exceptionnels dès aujourd'hui !

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque qui permet aux développeurs de créer, manipuler et convertir des documents PDF par programmation.

### Puis-je utiliser Aspose.PDF gratuitement ?
Oui, Aspose propose une version d'essai gratuite pour explorer les fonctionnalités de la bibliothèque. Vous pouvez la télécharger. [ici](https://releases.aspose.com/).

### Comment obtenir de l'aide pour Aspose.PDF ?
Vous pouvez obtenir de l'aide en visitant le forum Aspose [ici](https://forum.aspose.com/c/pdf/10).

### Existe-t-il une licence temporaire disponible ?
Oui, vous pouvez demander une licence temporaire pour Aspose.PDF [ici](https://purchase.aspose.com/temporary-license/).

### Où puis-je acheter Aspose.PDF pour .NET ?
Vous pouvez acheter Aspose.PDF pour .NET [ici](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}