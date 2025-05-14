---
"description": "Découvrez comment créer des fichiers PDF avec Aspose.PDF pour .NET, en définissant l'orientation de la page en fonction des dimensions de l'image dans ce guide étape par étape."
"linktitle": "Orientation de la page selon les dimensions de l'image"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Orientation de la page selon les dimensions de l'image"
"url": "/fr/net/document-conversion/page-orientation-according-image-dimensions/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Orientation de la page selon les dimensions de l'image

## Introduction

Bienvenue dans l'univers d'Aspose.PDF pour .NET ! Si vous souhaitez créer, manipuler ou convertir des documents PDF par programmation, vous êtes au bon endroit. Aspose.PDF est une bibliothèque puissante qui permet aux développeurs de travailler avec des fichiers PDF en toute simplicité. Dans ce guide, nous vous expliquerons comment définir l'orientation des pages en fonction des dimensions des images. Que vous soyez un développeur expérimenté ou débutant, ce tutoriel vous apportera les connaissances nécessaires pour bien démarrer avec Aspose.PDF.

## Prérequis

Avant de plonger dans le code, assurons-nous que vous disposez de tout ce dont vous avez besoin pour suivre :

1. Visual Studio : Assurez-vous d'avoir installé Visual Studio sur votre ordinateur. C'est le meilleur IDE pour le développement .NET.
2. .NET Framework : ce guide suppose que vous utilisez .NET Framework. Assurez-vous d'avoir installé la version appropriée.
3. Aspose.PDF pour .NET : Vous pouvez télécharger la bibliothèque à partir du [Site Web d'Aspose](https://releases.aspose.com/pdf/net/)Si vous souhaitez l'essayer en premier, vous pouvez obtenir un [essai gratuit](https://releases.aspose.com/).
4. Connaissances de base de C# : une familiarité avec la programmation C# vous aidera à mieux comprendre les exemples.

## Importer des packages

Pour commencer, vous devez importer les packages nécessaires. Voici comment procéder :

1. Ouvrez votre projet Visual Studio.
2. Cliquez avec le bouton droit sur votre projet dans l'Explorateur de solutions et sélectionnez « Gérer les packages NuGet ».
3. Rechercher `Aspose.PDF` et installez-le.

Maintenant que nous avons tout configuré, décomposons l’exemple étape par étape.

## Étape 1 : Configurez votre répertoire de documents

Tout d'abord, vous devez spécifier le chemin d'accès au répertoire de vos documents où sont stockées vos images. C'est là qu'Aspose recherchera les fichiers JPG.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin d'accès réel de vos images. Ceci est crucial, car si Aspose ne trouve pas vos images, il ne pourra pas créer le PDF.

## Étape 2 : Créer un nouveau document PDF

Ensuite, vous créerez un nouveau document PDF. C'est là que seront ajoutées toutes vos images.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Cette ligne initialise une nouvelle instance du `Document` classe, qui représente votre fichier PDF.

## Étape 3 : Récupérer les fichiers image

Récupérons maintenant tous les fichiers JPG du répertoire spécifié. Pour cela, utilisez l'outil `Directory.GetFiles` méthode.

```csharp
string[] fileEntries = Directory.GetFiles(dataDir, "*.JPG");
```

Cette ligne vous donnera un tableau de noms de fichiers correspondant au format JPG. Assurez-vous que votre répertoire contient des images JPG pour que cela fonctionne !

## Étape 4 : Parcourir chaque image

Vous devrez parcourir chaque fichier image et l'ajouter au document PDF. Voici comment procéder :

```csharp
int counter;
for (counter = 0; counter < fileEntries.Length - 1; counter++)
{
    // Créer un objet de page
    Aspose.Pdf.Page page = doc.Pages.Add();
```

Dans cette boucle, vous créez une nouvelle page pour chaque image. `doc.Pages.Add()` La méthode ajoute une nouvelle page à votre document PDF.

## Étape 5 : Créer un objet image

Pour chaque image, vous devez créer un `Image` objet qui contiendra les données de l'image.

```csharp
    Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
    image1.File = fileEntries[counter];
```

Ici, vous attribuez le fichier image actuel au `Image` objet. Ceci est essentiel pour ajouter l'image au PDF.

## Étape 6 : Vérifier les dimensions de l’image

Avant d’ajouter l’image au PDF, vous devez vérifier ses dimensions pour déterminer l’orientation de la page.

```csharp
    Bitmap myimage = new Bitmap(fileEntries[counter]);
    if (myimage.Width > page.PageInfo.Width)
        page.PageInfo.IsLandscape = true;
    else
        page.PageInfo.IsLandscape = false;
```

Cet extrait de code vérifie si la largeur de l'image est supérieure à celle de la page. Si c'est le cas, l'orientation de la page est définie sur paysage ; sinon, elle reste en mode portrait.

## Étape 7 : Ajouter l’image au PDF

Maintenant que vous avez défini l’orientation, il est temps d’ajouter l’image au document PDF.

```csharp
    page.Paragraphs.Add(image1);
}
```

Cette ligne ajoute l'image à la collection de paragraphes de la page actuelle. C'est comme placer une image dans un cadre !

## Étape 8 : Enregistrer le document PDF

Enfin, vous devez enregistrer le document PDF dans le répertoire spécifié.

```csharp
doc.Save(dataDir + "SetPageOrientation_out.pdf");
```

Cette ligne enregistre le document sous le nom `SetPageOrientation_out.pdf`Assurez-vous de vérifier votre répertoire de documents pour le PDF nouvellement créé !

## Conclusion

Et voilà ! Vous avez créé un document PDF avec Aspose.PDF pour .NET, en définissant l'orientation de la page en fonction des dimensions des images. Cette puissante bibliothèque ouvre un monde de possibilités pour travailler avec des fichiers PDF dans vos applications. Que vous génériez des rapports, des factures ou tout autre type de document, Aspose.PDF est là pour vous.

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque qui permet aux développeurs de créer, manipuler et convertir des documents PDF par programmation.

### Comment installer Aspose.PDF ?
Vous pouvez installer Aspose.PDF via NuGet Package Manager dans Visual Studio ou le télécharger à partir du [Site Web d'Aspose](https://releases.aspose.com/pdf/net/).

### Puis-je utiliser Aspose.PDF gratuitement ?
Oui, Aspose propose un [essai gratuit](https://releases.aspose.com/) pour que vous puissiez tester la bibliothèque avant de l'acheter.

### Où puis-je trouver de l'aide pour Aspose.PDF ?
Vous pouvez trouver du soutien sur le [Forum Aspose](https://forum.aspose.com/c/pdf/10).

### Quels types de fichiers puis-je convertir en PDF avec Aspose ?
Aspose.PDF prend en charge une large gamme de formats de fichiers, notamment les images, les documents Word, les feuilles de calcul Excel, etc.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}