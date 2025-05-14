---
"description": "Apprenez à créer des hyperliens locaux dans des fichiers PDF à l'aide d'Aspose.PDF pour .NET sans effort grâce à notre guide étape par étape."
"linktitle": "Créer un lien hypertexte local dans un fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Créer un lien hypertexte local dans un fichier PDF"
"url": "/fr/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Créer un lien hypertexte local dans un fichier PDF

## Introduction

Dans ce guide, nous vous expliquerons comment créer des hyperliens locaux dans un fichier PDF avec Aspose.PDF pour .NET. Chaque étape sera détaillée clairement, afin que même si vous débutez dans la manipulation de PDF, vous puissiez suivre le processus sans effort.

## Prérequis

Avant de plonger tête baissée dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin :

1. Visual Studio : vous en aurez besoin pour développer vos applications .NET. Téléchargez-le depuis le [site web](https://visualstudio.microsoft.com/).
2. Aspose.PDF pour .NET : Vous pouvez télécharger cette bibliothèque via le [lien de téléchargement ici](https://releases.aspose.com/pdf/net/)Il est livré avec un riche ensemble de fonctionnalités pour la manipulation de PDF.
3. Connaissances de base de C# : une petite familiarité avec la programmation C# vous aidera, mais ne vous inquiétez pas ; nous allons parcourir le code ligne par ligne.
4. .NET Framework : Assurez-vous que .NET Framework est installé sur votre ordinateur. Vous pouvez consulter la configuration requise sur le fichier Aspose.PDF. [documentation](https://reference.aspose.com/pdf/net/).

Une fois ces prérequis définis, vous êtes prêt à apprendre à créer des hyperliens locaux dans vos documents PDF !

## Importer des packages

Maintenant que tout est prêt, il est temps d'importer les packages nécessaires dans votre projet C#. La bibliothèque Aspose.PDF contient toutes les classes nécessaires. Voici comment procéder :

### Ouvrez votre projet

Ouvrez votre projet .NET existant ou créez-en un nouveau dans Visual Studio. Si vous démarrez de zéro, sélectionnez « Créer un nouveau projet » dans l'écran de démarrage.

### Ajouter une référence à Aspose.PDF

Faites un clic droit sur « Dépendances » dans le dossier de votre projet dans l'Explorateur de solutions. Sélectionnez « Gérer les packages NuGet », puis recherchez `Aspose.PDF`Installez la dernière version disponible. Vous disposerez ainsi de tous les outils nécessaires à la création et à la manipulation de PDF.

### Importer des espaces de noms

En haut de votre fichier .cs, ajoutez des directives using pour la bibliothèque Aspose.PDF comme ceci :

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

De cette façon, vous pourrez accéder aux fonctionnalités de la bibliothèque.

Décomposons le processus de création de liens hypertextes locaux en étapes simples. Chaque étape sera expliquée en détail pour vous aider à comprendre la logique qui la sous-tend.

## Étape 1 : Configurer l'instance de document

Dans cette étape, vous allez créer une nouvelle instance de la classe Document, qui représente le fichier PDF avec lequel vous allez travailler.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Définissez votre répertoire de documents
Document doc = new Document(); // Créer une instance de document
```
Le `dataDir` La variable est l'emplacement où se trouvera votre PDF nouvellement créé. Vous devrez remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin réel sur votre système. Le `Document` la classe crée un nouveau document PDF dans lequel nous pouvons ajouter des pages et des liens.

## Étape 2 : ajouter une page au document

Ensuite, vous allez ajouter une page à votre document PDF. 

```csharp
Page page = doc.Pages.Add(); // Ajouter une page à la collection de pages
```
Le `Pages.Add()` La méthode ajoute une nouvelle page au document. C'est là que résidera tout votre contenu.

## Étape 3 : Créer un fragment de texte

Maintenant, créons un morceau de texte qui fera office de lien cliquable.

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
Le `TextFragment` Représente un segment de texte du PDF. Ici, nous créons un lien indiquant aux utilisateurs qu'il les mènera à la page 7.

## Étape 4 : Créer un lien hypertexte local

C'est là que la magie opère ! Vous devez créer un lien hypertexte local qui indiquera au fragment de texte où pointer.

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // Créer un lien hypertexte local
link.TargetPageNumber = 7; // Définir la page cible pour l'instance de lien
text.Hyperlink = link; // Définir le lien hypertexte TextFragment
```
Le `LocalHyperlink` La classe permet de pointer vers d'autres pages du même document. En définissant `TargetPageNumber` jusqu'à 7, vous indiquez au lien hypertexte de sauter vers cette page spécifique lorsque vous cliquez dessus.

## Étape 5 : ajouter le fragment de texte à la page

Après avoir configuré l'hyperlien, il est temps d'ajouter notre fragment de texte à la page que nous avons créée.

```csharp
page.Paragraphs.Add(text); // Ajouter du texte à la collection de paragraphes de la page
```
Cette ligne ajoute votre texte cliquable à la collection de paragraphes de la page.

## Étape 6 : Créer un autre fragment de texte (facultatif)

Ajoutons un autre lien hypertexte pour revenir à la page 1.

```csharp
text = new TextFragment("link page number test to page 1"); // Créer un nouveau fragment de texte
text.IsInNewPage = true; // Ajoutez-le à une nouvelle page
```
Créer un nouveau `TextFragment` pour le deuxième lien, nous avons défini `IsInNewPage` à vrai, indiquant que ce texte sera placé sur une nouvelle page.

## Étape 7 : Configurer le deuxième lien hypertexte local

Tout comme précédemment, vous créerez un autre lien hypertexte local pour la page 1.

```csharp
link = new LocalHyperlink(); // Créer une autre instance d'hyperlien local
link.TargetPageNumber = 1; // Définir la page cible pour le deuxième lien hypertexte
text.Hyperlink = link; // Définir le lien pour le deuxième TextFragment
```
Ce lien hypertexte cible la page 1, permettant aux utilisateurs de revenir en arrière lorsqu'ils atteignent la deuxième page.

## Étape 8 : Ajouter le deuxième fragment de texte à la nouvelle page

Maintenant, ajoutons ce texte à sa page.

```csharp
page.Paragraphs.Add(text); // Ajouter du texte à la collection de paragraphes de l'objet de page
```
Similaire à l’étape 5, cette ligne ajoute le nouveau texte d’hyperlien à la page nouvellement créée.

## Étape 9 : Enregistrer le document

Enfin, il est temps de sauvegarder votre travail acharné ! 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // Spécifier le nom du fichier de sortie
doc.Save(dataDir); // Enregistrer le document mis à jour
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
Ceci combine votre chemin de répertoire avec le nom du fichier. `Save()` La méthode enregistre votre document et un message de confirmation vous permet de savoir que tout s'est bien passé !

## Conclusion

Créer des hyperliens locaux dans des fichiers PDF avec Aspose.PDF pour .NET n'est pas seulement une astuce pratique ; c'est une fonctionnalité pratique qui améliore la navigation et l'expérience utilisateur. Vous disposez désormais des connaissances nécessaires pour orienter vos lecteurs directement vers l'information dont ils ont besoin. Repensez à notre analogie initiale : fini les âmes perdues errant dans des pages interminables.

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque qui permet aux développeurs de créer, manipuler et convertir des documents PDF par programmation à l'aide du framework .NET.

### Puis-je créer des hyperliens vers des pages Web externes ?
Oui, Aspose.PDF prend également en charge la création d'hyperliens vers des URL externes en plus des hyperliens locaux dans le PDF.

### Existe-t-il un essai gratuit pour Aspose.PDF ?
Absolument ! Vous pouvez accéder à l'essai gratuit depuis le [site](https://releases.aspose.com/).

### Quels langages de programmation Aspose prend-il en charge ?
Aspose propose des bibliothèques pour divers langages de programmation, notamment Java, C++ et Python, entre autres.

### Comment obtenir de l'assistance pour les produits Aspose ?
Vous pouvez demander de l'aide via le [Forum Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}