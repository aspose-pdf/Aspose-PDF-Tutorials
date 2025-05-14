---
"description": "Découvrez comment définir la propriété de légende dans un fichier PDF à l'aide d'Aspose.PDF pour .NET dans ce didacticiel détaillé, étape par étape."
"linktitle": "Définir la propriété de légende dans le fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Définir la propriété de légende dans le fichier PDF"
"url": "/fr/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Définir la propriété de légende dans le fichier PDF

## Introduction

Créer des documents PDF professionnels et attrayants nécessite souvent l'ajout d'annotations pour attirer l'attention sur un contenu spécifique. Parmi ces annotations, on trouve les légendes, semblables à ces bulles de dialogue que l'on voit dans les bandes dessinées. Elles permettent de clarifier ou de mettre en valeur le texte de votre PDF. Aspose.PDF pour .NET simplifie considérablement l'ajout de telles annotations à vos documents. Dans ce tutoriel, nous vous expliquerons comment définir la propriété de légende dans un fichier PDF grâce à cette puissante bibliothèque. Que vous soyez un développeur expérimenté ou débutant, à la fin de ce guide, vous maîtriserez parfaitement l'utilisation des légendes dans les fichiers PDF.

## Prérequis

Avant de plonger dans le code, couvrons les éléments essentiels dont vous avez besoin pour commencer.

1. Aspose.PDF pour .NET : Assurez-vous d'avoir installé la bibliothèque Aspose.PDF pour .NET. Vous pouvez la télécharger depuis [ici](https://releases.aspose.com/pdf/net/).
2. IDE : un environnement de développement tel que Visual Studio.
3. .NET Framework : assurez-vous que .NET est installé sur votre machine.
4. Licence temporaire : si vous souhaitez tester toutes les fonctionnalités d'Aspose.PDF sans limitations, obtenez une [permis temporaire](https://purchase.aspose.com/temporary-license/).

## Importer des packages

Avant de commencer à écrire le code, vous devez importer les packages nécessaires qui vous permettront de travailler avec des fichiers PDF et des annotations.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Ces importations vous fourniront toutes les classes et méthodes nécessaires pour manipuler des documents PDF et créer des annotations comme la légende.

## Étape 1 : Initialiser le document PDF

La première étape consiste à initialiser un nouveau document PDF dans lequel nous ajouterons notre annotation. Considérez cela comme la création d'une zone vierge sur laquelle vous pouvez commencer à ajouter des éléments.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Initialiser un nouveau document PDF
Document doc = new Document();
```
Ici, nous créons un nouveau `Document` objet qui servira de fichier PDF. `dataDir` la variable est définie sur le répertoire dans lequel vous souhaitez enregistrer votre fichier PDF une fois que nous avons terminé.

## Étape 2 : Ajouter une nouvelle page au document

Un document PDF peut comporter plusieurs pages. Dans cette étape, nous allons ajouter une nouvelle page à notre document. C'est sur cette page que sera placée notre annotation.

```csharp
// Ajouter une nouvelle page au document
Page page = doc.Pages.Add();
```
Le `Pages.Add()` méthode est utilisée pour ajouter une nouvelle page à la `doc` objet. La nouvelle page est stockée dans le `page` variable, que nous utiliserons plus tard lors de l'ajout de l'annotation.

## Étape 3 : Définir l’apparence par défaut

Les annotations, comme la légende, ont une apparence visuelle personnalisable. Dans cette étape, nous allons définir l'apparence du texte de la légende.

```csharp
// Définir l'apparence par défaut de l'annotation
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
Nous créons un `DefaultAppearance` Objet définissant la couleur et la taille de police du texte. Ici, le texte est rouge et la taille de police est fixée à 10. Cette apparence sera appliquée à l'annotation de légende.

## Étape 4 : Créer l'annotation de texte libre

Il est maintenant temps de créer l'annotation proprement dite. L'annotation en texte libre nous permet d'ajouter une légende avec un texte et un style spécifiques.

```csharp
// Créer une annotation de texte libre avec une légende
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
Nous créons un `FreeTextAnnotation` objet avec des coordonnées spécifiques, définissant sa position sur la page. `Intent` est réglé sur `FreeTextCallout`, indiquant qu'il s'agit d'une annotation d'appel. `EndingStyle` est réglé sur `OpenArrow`, ce qui signifie que la ligne de légende se terminera par une flèche ouverte.

## Étape 5 : Définir les points de la ligne de légende

Une annotation de légende comporte une ligne pointant vers la zone d'intérêt. Nous allons ici définir les points qui composent cette ligne.

```csharp
// Définir les points pour la ligne de rappel
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
Le `Callout` la propriété est un tableau de `Point` objets, chacun représentant une coordonnée sur la page. Ces points définissent le tracé de la ligne de légende, lui donnant l'aspect classique d'une bulle de dialogue.

## Étape 6 : Ajouter l'annotation à la page

Après avoir créé et configuré notre annotation, l’étape suivante consiste à l’ajouter à la page.

```csharp
// Ajouter l'annotation à la page
page.Annotations.Add(fta);
```
Le `Annotations.Add()` La méthode permet de placer l'annotation sur la page créée précédemment. Cette étape permet de « dessiner » la légende sur la page PDF.

## Étape 7 : Définir le contenu du texte enrichi

Les annotations de légende peuvent inclure du texte enrichi, permettant d'insérer du contenu formaté dans la bulle. Ajoutons un exemple de texte.

```csharp
// Définir le texte enrichi pour l'annotation
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">Ceci est un exemple</span></p></body>";
```
Le `RichText` La propriété est définie avec du contenu HTML. Cela permet un formatage détaillé de la légende, comme la spécification de la taille, de la couleur et du style de police.

## Étape 8 : Enregistrer le document PDF

Enfin, après avoir tout configuré, nous devons enregistrer le document. Cette étape finalise la création du PDF avec l'annotation de légende.

```csharp
// Enregistrer le document
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
Le `Save()` La méthode enregistre le document dans le répertoire spécifié sous le nom « SetCalloutProperty.pdf ». Cette étape conclut notre processus de création de PDF.

## Conclusion

Et voilà ! Vous venez de créer un document PDF avec une annotation de légende avec Aspose.PDF pour .NET. Cette annotation peut s'avérer extrêmement utile pour mettre en évidence ou expliquer des parties spécifiques de votre document. Aspose.PDF propose une API puissante qui simplifie et adapte la manipulation des PDF. Que vous souhaitiez ajouter des annotations, convertir des documents ou gérer des tâches PDF complexes, Aspose.PDF est là pour vous.

## FAQ

### Puis-je personnaliser davantage l’apparence de la légende ?

Absolument ! Vous pouvez personnaliser divers aspects comme la couleur et l'épaisseur des lignes, ainsi que la police et le style du texte.

### Est-il possible d'ajouter plusieurs légendes sur une seule page ?

Oui, vous pouvez ajouter autant de légendes que nécessaire en répétant les étapes pour chaque annotation.

### Comment puis-je modifier la position de la légende ?

Modifiez simplement les coordonnées dans le `Rectangle` et `Callout` propriétés pour repositionner l'annotation.

### Puis-je ajouter d’autres types d’annotations à l’aide d’Aspose.PDF ?

Oui, Aspose.PDF prend en charge différents types d’annotations, notamment les surlignages, les tampons et les pièces jointes.

### Le contenu de texte enrichi est-il limité au HTML ?

Le `RichText` La propriété prend en charge un sous-ensemble de HTML, vous permettant d'inclure du texte stylisé et une mise en forme de base.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}