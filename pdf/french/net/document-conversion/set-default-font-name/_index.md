---
"description": "Découvrez comment définir un nom de police par défaut lors du rendu de PDF en images avec Aspose.PDF pour .NET. Ce guide présente les prérequis, des instructions étape par étape et une FAQ."
"linktitle": "Définir le nom de police par défaut"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Définir le nom de police par défaut"
"url": "/fr/net/document-conversion/set-default-font-name/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Définir le nom de police par défaut

## Introduction

Avez-vous déjà essayé de convertir un document PDF en image, mais les polices ne vous conviennent pas ? Le texte est peut-être déformé, ou la police d'origine n'est pas prise en charge. C'est là que définir une police par défaut peut vous sauver la mise ! Avec Aspose.PDF pour .NET, vous pouvez facilement définir une police par défaut pour le rendu de vos PDF, garantissant ainsi un rendu net et professionnel. Dans ce tutoriel, nous vous expliquerons comment définir le nom de la police par défaut lors du rendu d'un PDF en image. À la fin de ce guide, vous serez en mesure de relever tous les défis de rendu PDF qui se présenteront à vous. Prêt ? C'est parti !

## Prérequis

Avant de passer au code, vous devez mettre en place quelques éléments :

- Aspose.PDF pour .NET : Cette puissante bibliothèque nous permettra de manipuler notre document PDF. Vous pouvez la télécharger depuis le [Site Web d'Aspose](https://releases.aspose.com/pdf/net/).
- Visual Studio : Assurez-vous d'avoir installé Visual Studio sur votre machine. Ce sera notre environnement de développement.
- .NET Framework : assurez-vous d'avoir installé .NET Framework. Aspose.PDF pour .NET est compatible avec plusieurs versions. Consultez la documentation pour savoir comment l'utiliser.
- Un document PDF : vous aurez besoin d'un exemple de document PDF. Si vous n'en avez pas, créez un PDF simple ou téléchargez un exemple en ligne.

Une fois que tout est configuré, nous sommes prêts à commencer à coder !

## Importer des packages

Avant de nous plonger dans le code, il est essentiel d'importer les packages nécessaires. Cela nous permettra d'avoir accès à toutes les classes et méthodes nécessaires à notre projet.

```csharp
using Aspose.Pdf.Devices;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Ces importations sont essentielles car elles apportent les espaces de noms requis pour gérer la manipulation PDF, le rendu d'images et les opérations de flux de fichiers.

## Étape 1 : Configurez votre projet et le chemin du document

Tout d'abord, définissons le chemin d'accès au répertoire où se trouve votre document PDF. Ce sera votre point de départ pour manipuler le fichier PDF.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```
Ici, `dataDir` est le répertoire où se trouve votre document PDF. Assurez-vous de remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin d'accès réel à votre document. Ceci est essentiel car le code doit savoir où récupérer le fichier PDF.

## Étape 2 : Charger le document PDF

Maintenant que nous avons le chemin du document, l’étape suivante consiste à charger le document PDF en mémoire afin que nous puissions commencer à travailler dessus.

```csharp
using (Document pdfDocument = new Document(dataDir + "input.pdf"))
```
Nous utilisons le `Document` Classe de la bibliothèque Aspose.PDF pour charger notre fichier PDF. Cette classe fournit diverses méthodes et propriétés pour travailler avec le document PDF. `"input.pdf"` doit être remplacé par le nom réel du fichier PDF. Ce fichier sera utilisé comme entrée pour le rendu.

## Étape 3 : Créer un flux d’images pour la sortie

Une fois le document chargé, nous devons configurer un flux pour enregistrer l'image rendue. C'est là que l'image de sortie sera stockée.

```csharp
using (FileStream imageStream = new FileStream(dataDir + "SetDefaultFontName.png", FileMode.Create))
```
Le `FileStream` La classe permet de créer un nouveau fichier dans lequel l'image rendue sera enregistrée. Dans cet exemple, nous enregistrons l'image sous le nom `"SetDefaultFontName.png"`. Le `FileMode.Create` garantit qu'un nouveau fichier est créé ou qu'un fichier existant est écrasé.

## Étape 4 : Définir la résolution de l’image

Avant de convertir le PDF en image, il est essentiel de définir la résolution. Cela détermine la qualité et la clarté de l'image de sortie.

```csharp
Resolution resolution = new Resolution(300);
```
Le `Resolution` La classe définit la résolution de l'image de sortie. Nous avons choisi ici une résolution de 300 DPI (points par pouce), standard pour les images de haute qualité. Cela garantit un rendu clair du texte et des graphiques de votre PDF, sans perte de détails.

## Étape 5 : Configurer le périphérique PNG

Ensuite, nous devons configurer le périphérique qui gérera le rendu du PDF en une image PNG.

```csharp
PngDevice pngDevice = new PngDevice(resolution);
```
Le `PngDevice` La classe est responsable du rendu du document PDF en image PNG. En passant la `resolution` pour nous y opposer, nous nous assurons que l'image est créée avec le DPI spécifié.

## Étape 6 : Définir le nom de police par défaut

Voici l'étape cruciale : définir le nom de la police par défaut. Ce sera la police de secours si la police d'origine du PDF n'est pas disponible.

```csharp
RenderingOptions ro = new RenderingOptions();
ro.DefaultFontName = "Arial";
pngDevice.RenderingOptions = ro;
```
Nous créons une instance de `RenderingOptions` et définissez son `DefaultFontName` propriété à `"Arial"`Cela signifie que si la police d'origine du PDF est introuvable, Arial sera utilisée. Cette étape est cruciale pour préserver la lisibilité et l'apparence du texte dans l'image rendue.

## Étape 7 : Convertir la page PDF en image

Enfin, une fois tout configuré, nous pouvons désormais restituer la première page du document PDF en une image et l'enregistrer à l'aide du flux de fichiers que nous avons créé précédemment.

```csharp
pngDevice.Process(pdfDocument.Pages[1], imageStream);
```
Le `Process` méthode de la `PngDevice` La classe permet de convertir la page PDF spécifiée (ici, la première page) en image. Le résultat est ensuite enregistré dans le `imageStream`Cette étape convertit la page PDF en une image PNG avec la résolution spécifiée et la police par défaut.

## Étape 8 : Fermez le flux de fichiers et le document PDF

Après avoir rendu l'image, il est essentiel de fermer le flux de fichiers et le document PDF pour libérer des ressources.

```csharp
imageStream.Close();
pdfDocument.Dispose();
```
Fermeture du `imageStream` garantit que le fichier est correctement enregistré et qu'aucune donnée n'est perdue. L'élimination du `pdfDocument` libère de la mémoire et des ressources, évitant ainsi toute fuite de mémoire potentielle.

## Conclusion

Et voilà ! En quelques lignes de code, vous avez appris à définir un nom de police par défaut lors du rendu d'un PDF en image avec Aspose.PDF pour .NET. Cette compétence est extrêmement pratique, surtout pour les PDF contenant des polices non prises en charge. En définissant une police par défaut, vous garantissez la lisibilité et l'aspect professionnel de vos images rendues.

## FAQ

### Que se passe-t-il si la police par défaut spécifiée n'est pas installée sur le système ?
Si la police par défaut spécifiée dans le `RenderingOptions` n'est pas installé sur le système, Aspose.PDF utilisera une police de secours définie par le système.

### Puis-je utiliser d’autres polices qu’Arial comme police par défaut ?
Absolument ! Vous pouvez définir n'importe quelle police installée sur votre système comme police par défaut.

### Est-il possible de rendre plusieurs pages d'un PDF en images en une seule fois ?
Oui, vous pouvez parcourir les pages de votre PDF et restituer chaque page individuellement en utilisant le même processus.

### La définition d’une résolution élevée affecte-t-elle les performances du rendu PDF ?
Oui, des résolutions plus élevées donneront lieu à des fichiers image plus volumineux et peuvent augmenter le temps de rendu, mais elles produiront également des images plus claires.

### Puis-je rendre le PDF dans d'autres formats d'image en plus du PNG ?
Oui, Aspose.PDF prend en charge le rendu dans divers formats d'image tels que JPEG, BMP et TIFF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}