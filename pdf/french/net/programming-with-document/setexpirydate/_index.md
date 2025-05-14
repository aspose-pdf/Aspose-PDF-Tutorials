---
"description": "Apprenez à définir une date d'expiration dans vos fichiers PDF avec Aspose.PDF pour .NET. Améliorez la sécurité de vos documents grâce à ce guide étape par étape."
"linktitle": "Définir la date d'expiration dans le fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Définir la date d'expiration dans le fichier PDF"
"url": "/fr/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Définir la date d'expiration dans le fichier PDF

## Introduction

À l'ère du numérique, gérer et sécuriser les documents est plus crucial que jamais. Imaginez envoyer un PDF qui devient automatiquement inaccessible après une certaine date. Un vrai miracle, non ? Avec Aspose.PDF pour .NET, vous pouvez facilement définir une date d'expiration pour vos fichiers PDF. Cette fonctionnalité est particulièrement utile pour les documents sensibles dont l'accès doit être restreint après une certaine période. Dans ce tutoriel, nous vous expliquerons étape par étape comment définir une date d'expiration dans un fichier PDF. Alors, à vos codes et c'est parti !

## Prérequis

Avant de commencer, il y a quelques éléments que vous devez mettre en place :

1. Environnement de développement : Assurez-vous de disposer d'un environnement de développement .NET. Il peut s'agir de Visual Studio ou de tout autre IDE prenant en charge .NET.
2. Aspose.PDF pour .NET : la bibliothèque Aspose.PDF doit être installée. Si ce n'est pas déjà fait, vous pouvez la télécharger depuis [ici](https://releases.aspose.com/pdf/net/).
3. Connaissances de base en C# : Ce tutoriel suppose que vous avez des connaissances de base en programmation C#. Si vous débutez en C#, pas d'inquiétude ! Nous allons faire simple et direct.

## Importer des packages

Pour démarrer avec Aspose.PDF, vous devez importer les espaces de noms nécessaires dans votre projet C#. Voici comment procéder :

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Ces espaces de noms vous donnent accès aux fonctionnalités principales requises pour travailler avec des documents PDF dans Aspose.PDF.

## Étape 1 : Configurez votre répertoire de documents

Tout d'abord, vous devez spécifier le chemin d'accès à votre répertoire de documents. C'est là que votre PDF de sortie sera enregistré. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin d'accès exact où vous souhaitez enregistrer votre fichier PDF. C'est comme si vous disiez à votre programme : « Hé, c'est ici que je stocke mes fichiers ! »

## Étape 2 : instancier l'objet document

Ensuite, vous devez créer une nouvelle instance du `Document` classe. Ceci est votre toile où vous créerez votre PDF.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Pensez à la `Document` L'objet est une feuille blanche. Vous pouvez y ajouter du contenu à votre guise !

## Étape 3 : Ajouter une page au PDF

Maintenant que votre document est configuré, il est temps d'y ajouter une page. C'est là que votre contenu sera placé.

```csharp
doc.Pages.Add();
```

Vous venez de créer une nouvelle page dans votre PDF. C'est comme ajouter une nouvelle page dans votre carnet pour noter vos pensées.

## Étape 4 : ajouter du texte à la page

Rendons cette page plus intéressante en ajoutant du texte. Nous ajouterons un simple message « Bonjour tout le monde ».

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

Cette ligne de code ajoute un fragment de texte à la première page de votre PDF. C'est comme écrire un titre en haut de la page !

## Étape 5 : Créer un code JavaScript pour la date d'expiration

Passons maintenant à la partie amusante ! Vous allez créer une action JavaScript qui vérifiera la date d'expiration du PDF. Si la date actuelle est supérieure à la date d'expiration, un message avertira l'utilisateur.

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

Voici ce qui se passe :
- Vous définissez l'année et le mois d'expiration.
- Vous obtenez la date d'aujourd'hui.
- Vous comparez la date d’aujourd’hui avec la date d’expiration.
- Si la date d'aujourd'hui est dépassée, un message apparaît !

## Étape 6 : définir JavaScript comme action d'ouverture de PDF

Vous devez maintenant définir l'action JavaScript comme action d'ouverture de votre document PDF. Cela signifie que JavaScript s'exécutera dès l'ouverture du PDF.

```csharp
doc.OpenAction = javaScript;
```

Cette ligne indique au PDF d'exécuter le JavaScript à l'ouverture. C'est comme définir un rappel qui se déclenche dès l'ouverture de votre calendrier !

## Étape 7 : Enregistrer le document PDF

Enfin, il est temps d'enregistrer votre document PDF avec la fonction de date d'expiration. 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

Cette ligne enregistre votre PDF dans le répertoire spécifié sous le nom « SetExpiryDate_out.pdf ». C'est comme encadrer votre œuvre terminée !

## Conclusion

Et voilà ! Vous avez créé avec succès un fichier PDF avec une date d'expiration grâce à Aspose.PDF pour .NET. Cette fonctionnalité renforce non seulement la sécurité, mais garantit également la maîtrise des informations sensibles. Que vous envoyiez des contrats, des rapports ou tout autre document important, définir une date d'expiration peut être une solution révolutionnaire.

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque puissante qui permet aux développeurs de créer, manipuler et convertir des documents PDF dans des applications .NET.

### Puis-je utiliser Aspose.PDF gratuitement ?
Oui, vous pouvez utiliser une version d'essai gratuite d'Aspose.PDF. Vous pouvez la télécharger. [ici](https://releases.aspose.com/).

### Comment acheter Aspose.PDF ?
Vous pouvez acheter Aspose.PDF en visitant le [page d'achat](https://purchase.aspose.com/buy).

### Et si j'ai besoin d'aide ?
Si vous avez des questions ou besoin d'aide, vous pouvez visiter le [Forum d'assistance Aspose](https://forum.aspose.com/c/pdf/10).

### Puis-je obtenir une licence temporaire pour Aspose.PDF ?
Oui, vous pouvez demander une licence temporaire [ici](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}