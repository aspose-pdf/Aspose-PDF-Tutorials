---
"description": "Découvrez comment ajouter une date et une heure à vos fichiers PDF avec Aspose.PDF pour .NET grâce à ce guide étape par étape. Idéal pour renforcer l'authenticité de vos documents."
"linktitle": "Ajouter un horodatage dans un fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Ajouter un horodatage dans un fichier PDF"
"url": "/fr/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un horodatage dans un fichier PDF

## Introduction

Pour la gestion de documents, notamment PDF, l'ajout d'un horodatage peut être une véritable révolution. Que vous travailliez sur des documents juridiques, des rapports de projet ou des factures, un horodatage renforce non seulement l'authenticité du document, mais fournit également une trace claire de sa création ou de sa modification. Dans ce guide, nous vous expliquerons comment ajouter un horodatage à un fichier PDF à l'aide de la bibliothèque Aspose.PDF pour .NET. 

Cet article est conçu pour être simple et facile à suivre. Ainsi, même si vous débutez en programmation ou avec la bibliothèque Aspose.PDF, vous pourrez implémenter cette fonctionnalité en toute confiance. C'est parti !

## Prérequis

Avant de commencer, vous devez mettre en place quelques prérequis :

1. Visual Studio : Assurez-vous que Visual Studio est installé sur votre ordinateur. C'est ici que vous écrirez et exécuterez votre code.
2. Aspose.PDF pour .NET : vous devez télécharger et installer la bibliothèque Aspose.PDF. Vous trouverez la dernière version. [ici](https://releases.aspose.com/pdf/net/).
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les exemples, mais ne vous inquiétez pas si vous débutez ; nous vous expliquerons tout étape par étape.
4. Un fichier PDF : Préparez un exemple de fichier PDF. Pour notre exemple, nous utiliserons un fichier nommé `AddTextStamp.pdf`.

Une fois ces prérequis remplis, vous êtes prêt à commencer à ajouter des horodatages à vos fichiers PDF !

## Importer des packages

Pour commencer, vous devez importer les espaces de noms nécessaires dans votre projet C#. Voici comment procéder :

### Créer un nouveau projet

1. Ouvrez Visual Studio : lancez votre application Visual Studio.
2. Créer un nouveau projet : sélectionnez « Créer un nouveau projet » sur l’écran de démarrage.
3. Choisir l’application console : sélectionnez « Application console (.NET Framework) » dans la liste des modèles de projet.
4. Nommez votre projet : Donnez un nom à votre projet, par exemple, `PDFDateTimeStamp`.

### Ajouter une référence Aspose.PDF

1. Cliquez avec le bouton droit sur Références : Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le dossier « Références » de votre projet.
2. Sélectionnez « Ajouter une référence » : Choisissez « Ajouter une référence » dans le menu contextuel.
3. Rechercher Aspose.PDF : Accédez à l'emplacement où vous avez téléchargé Aspose.PDF et sélectionnez-le. Cliquez sur « OK » pour l'ajouter à votre projet.

### Importer les espaces de noms requis

Au sommet de votre `Program.cs` fichier, vous devez importer les espaces de noms suivants :

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

Maintenant que tout est configuré, décomposons le processus d'ajout d'un horodatage à un fichier PDF en étapes claires et gérables.

## Étape 1 : Définir le répertoire du document

Tout d'abord, vous devez spécifier le répertoire où se trouve votre fichier PDF. C'est crucial, car le code recherchera le PDF dans ce répertoire.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Remplacez par votre chemin réel
```

Assurez-vous de remplacer `YOUR DOCUMENT DIRECTORY` avec le chemin réel vers votre fichier PDF.

## Étape 2 : ouvrez le document PDF

Ensuite, vous ouvrirez le document PDF dans lequel vous souhaitez ajouter l’horodatage. 

```csharp
// Ouvrir le document
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

Cette ligne de code initialise le `Document` classe et charge votre fichier PDF dans le `pdfDocument` objet.

## Étape 3 : Créer l'horodatage

Il est maintenant temps de générer l'horodatage. Vous le formaterez pour un affichage spécifique. 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

Ici, `DateTime.Now` obtient la date et l'heure actuelles, et `ToString` le formate au format souhaité.

## Étape 4 : Créer un tampon de texte

Une fois la chaîne de date et d'heure prête, vous pouvez maintenant créer un tampon de texte qui sera ajouté à votre PDF.

```csharp
// Créer un tampon de texte
TextStamp textStamp = new TextStamp(annotationText);
```

Cette ligne crée une nouvelle instance de `TextStamp` en utilisant la chaîne de date et d'heure formatée.

## Étape 5 : Définir les propriétés du tampon

Vous pouvez personnaliser l'apparence et la position du tampon. Voici comment définir ses propriétés :

```csharp
// Définir les propriétés du tampon
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

Dans cette étape, nous définissons les marges et alignons le tampon sur le coin inférieur droit de la page PDF.

## Étape 6 : Ajouter le tampon au PDF

Il est maintenant temps d'ajouter le tampon de texte à votre document PDF. 

```csharp
// Ajout d'un timbre sur une collection de timbres
pdfDocument.Pages[1].AddStamp(textStamp);
```

Cette ligne ajoute le tampon à la première page du PDF. Vous pouvez modifier le numéro de page si vous souhaitez le placer sur une autre page.

## Étape 7 : Créer une annotation de texte libre (facultatif)

Si vous souhaitez ajouter une annotation au tampon, vous pouvez créer un `FreeTextAnnotation` comme suit:

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

Cette étape facultative crée une annotation de texte libre qui peut fournir un contexte ou des informations supplémentaires sur le tampon.

## Étape 8 : Configurer la bordure d’annotation

Si vous souhaitez personnaliser la bordure de votre annotation, vous pouvez également le faire :

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

Cet extrait de code définit la largeur de la bordure sur 0, la rendant invisible, et ajoute l'annotation au PDF.

## Étape 9 : Enregistrer le document PDF

Enfin, vous devez enregistrer le document PDF modifié. 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // Spécifiez le nom du fichier de sortie
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

Cette ligne enregistre le PDF avec l'horodatage ajouté dans un nouveau fichier. Vous pouvez consulter le répertoire spécifié pour voir le résultat.

## Conclusion

Félicitations ! Vous avez ajouté avec succès un horodatage à un fichier PDF grâce à Aspose.PDF pour .NET. Cette fonctionnalité simple et efficace peut améliorer vos documents, les rendre plus professionnels et fournir un enregistrement clair de leur date de création ou de modification. 

## FAQ

### Puis-je personnaliser le format de date dans l'horodatage ?
Oui, vous pouvez modifier le `ToString` méthode pour modifier le format de date selon vos préférences.

### L'utilisation d'Aspose.PDF est-elle gratuite ?
Aspose.PDF propose un essai gratuit, mais pour accéder à toutes les fonctionnalités, vous devez acheter une licence. Vous pouvez obtenir une licence temporaire. [ici](https://purchase.aspose.com/temporary-license/).

### Puis-je ajouter plusieurs horodatages à un PDF ?
Absolument ! Vous pouvez créer plusieurs `TextStamp` instances et les ajouter à différentes pages ou positions dans le PDF.

### Que faire si je n’ai pas Visual Studio ?
Vous pouvez utiliser n’importe quel IDE C# ou éditeur de texte, mais pour exécuter et déboguer votre projet, Visual Studio est recommandé.

### Où puis-je trouver plus d'exemples d'utilisation d'Aspose.PDF ?
Vous pouvez explorer plus d'exemples et de tutoriels dans le [Documentation Aspose.PDF](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}