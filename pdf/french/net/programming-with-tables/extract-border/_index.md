---
"description": "Apprenez à extraire les bordures d'un fichier PDF et à les enregistrer sous forme d'image avec Aspose.PDF pour .NET. Guide étape par étape avec exemples de code et conseils pour réussir."
"linktitle": "Extraire la bordure dans un fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Extraire la bordure dans un fichier PDF"
"url": "/fr/net/programming-with-tables/extract-border/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extraire la bordure dans un fichier PDF

## Introduction

Lorsque vous travaillez avec des PDF, extraire des éléments spécifiques tels que des bordures ou des tracés graphiques peut sembler complexe. Mais avec Aspose.PDF pour .NET, vous pouvez facilement extraire des bordures ou des formes d'un fichier PDF et les enregistrer au format image. Dans ce tutoriel, nous allons explorer le processus d'extraction d'une bordure d'un PDF et de son enregistrement au format PNG. Préparez-vous à maîtriser le contenu graphique de votre PDF !

## Prérequis

Avant de plonger dans le code, assurez-vous que tout est configuré :

1. Aspose.PDF pour .NET : si vous n’avez pas encore installé la bibliothèque Aspose.PDF, vous pouvez [téléchargez-le ici](https://releases.aspose.com/pdf/net/)Vous devrez également appliquer la licence, soit via l'essai gratuit, soit via une licence achetée.
2. Configuration de l'IDE : Configurez un projet C# dans Visual Studio ou tout autre IDE .NET. Assurez-vous d'avoir ajouté les références nécessaires à la bibliothèque Aspose.PDF.
3. Fichier PDF d'entrée : Préparez un fichier PDF dont vous extrairez les bordures. Ce tutoriel fera référence à un fichier nommé `input.pdf`.

## Importation des packages requis

Commençons par importer les espaces de noms requis. Ces packages fournissent les outils nécessaires à la manipulation du contenu PDF.

```csharp
using System.IO;
using System;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;
using System.Collections;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
```

Maintenant que nous avons couvert les bases, passons au guide étape par étape où nous décomposerons chaque partie du code pour l'expliquer en détail.


## Étape 1 : Chargement du document PDF

La première étape consiste à charger le document PDF contenant la bordure à extraire. C'est comme ouvrir un livre avant de commencer sa lecture : vous devez accéder à son contenu !

Nous commencerons par spécifier le répertoire dans lequel votre fichier PDF est stocké et chargerons le document à l'aide de l' `Aspose.Pdf.Document` classe.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Ce code charge le `input.pdf` fichier du répertoire spécifié. Assurez-vous que le chemin d'accès est correct, sinon vous risquez d'obtenir une erreur « Fichier introuvable ».

## Étape 2 : Configuration des graphiques et des bitmaps

Avant de commencer l'extraction, nous devons créer une zone de dessin. Dans .NET, cela implique de configurer des objets Bitmap et Graphics. Le Bitmap représente l'image, tandis que l'objet Graphics nous permet de dessiner des formes, telles que des bordures, extraites du PDF.

```csharp
System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap((int)doc.Pages[1].PageInfo.Width, (int)doc.Pages[1].PageInfo.Height);
System.Drawing.Drawing2D.GraphicsPath graphicsPath = new System.Drawing.Drawing2D.GraphicsPath();
System.Drawing.Drawing2D.Matrix lastCTM = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, 0);
System.Drawing.Drawing2D.Matrix inversionMatrix = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, (float)doc.Pages[1].PageInfo.Height);
System.Drawing.PointF lastPoint = new System.Drawing.PointF(0, 0);
System.Drawing.Color fillColor = System.Drawing.Color.FromArgb(0, 0, 0);
System.Drawing.Color strokeColor = System.Drawing.Color.FromArgb(0, 0, 0);
```

Voici une ventilation :
- Nous créons une image bitmap de la taille de la première page du PDF.
- GraphicsPath est utilisé pour définir des formes (dans ce cas, des bordures).
- La matrice définit comment les graphiques seront transformés ; nous avons besoin d'une matrice d'inversion car PDF et .NET ont des systèmes de coordonnées différents.

## Étape 3 : Traitement du contenu du PDF


Le fichier PDF est une série de commandes de dessin, et nous devons traiter chacune de ces commandes pour identifier et extraire les informations de bordure.

```csharp
foreach (Operator op in doc.Pages[1].Contents)
{
    // Traitement des commandes telles que l'enregistrement/la restauration de l'état, le dessin de lignes, le remplissage de formes, etc.
}
```

Le code parcourt chaque opérateur de dessin du flux de contenu du PDF. Chaque opérateur peut représenter une ligne, un rectangle ou une autre instruction graphique.

## Étape 4 : Gestion des opérateurs PDF

Chaque opérateur du fichier PDF contrôle une action. Pour extraire la bordure, nous devons identifier des commandes telles que « déplacer vers », « ligne vers » et « dessiner un rectangle ». Les opérateurs suivants gèrent ces actions :

- MoveTo : déplace le curseur vers un point de départ.
- LineTo : trace une ligne du point actuel vers un nouveau point.
- Re : Dessine un rectangle (cela pourrait faire partie de la bordure).

```csharp
Aspose.Pdf.Operators.MoveTo opMoveTo = op as Aspose.Pdf.Operators.MoveTo;
Aspose.Pdf.Operators.LineTo opLineTo = op as Aspose.Pdf.Operators.LineTo;
Aspose.Pdf.Operators.Re opRe = op as Aspose.Pdf.Operators.Re;

if (opMoveTo != null)
{
    lastPoint = new System.Drawing.PointF((float)opMoveTo.X, (float)opMoveTo.Y);
}
else if (opLineTo != null)
{
    System.Drawing.PointF linePoint = new System.Drawing.PointF((float)opLineTo.X, (float)opLineTo.Y);
    graphicsPath.AddLine(lastPoint, linePoint);
    lastPoint = linePoint;
}
else if (opRe != null)
{
    System.Drawing.RectangleF re = new System.Drawing.RectangleF((float)opRe.X, (float)opRe.Y, (float)opRe.Width, (float)opRe.Height);
    graphicsPath.AddRectangle(re);
}
```

Dans cette étape :
- Nous capturons les points pour chaque ligne ou forme dessinée.
- Pour les rectangles (`opRe`), nous les ajoutons directement au `graphicsPath`, que nous utiliserons plus tard pour dessiner la bordure.

## Étape 5 : Dessiner la bordure

Une fois les lignes et les rectangles formant la bordure identifiés, il faut les dessiner sur l'objet Bitmap. C'est là qu'intervient l'objet Graphics.

```csharp
using (System.Drawing.Graphics gr = System.Drawing.Graphics.FromImage(bitmap))
{
    gr.SmoothingMode = SmoothingMode.HighQuality;
    gr.DrawPath(new System.Drawing.Pen(strokeColor), graphicsPath);
}
```

- Nous créons un objet graphique basé sur le bitmap.
- SmoothingMode.HighQuality garantit que nous obtenons une belle image lisse.
- Enfin, nous utilisons DrawPath pour dessiner la bordure.

## Étape 6 : enregistrement de la bordure extraite

Maintenant que nous avons extrait la bordure, il est temps de l'enregistrer au format image. La bordure sera alors enregistrée au format PNG.

```csharp
dataDir = dataDir + "ExtractBorder_out.png";
bitmap.Save(dataDir, ImageFormat.Png);
```

- L'image bitmap est enregistrée sous forme d'image PNG.
- Vous pouvez maintenant ouvrir cette image pour visualiser la bordure extraite.

## Conclusion

Extraire les bordures d'un fichier PDF avec Aspose.PDF pour .NET peut paraître complexe au premier abord, mais une fois le processus analysé, cela devient simple. En comprenant les opérateurs de dessin d'un PDF et en utilisant les puissantes bibliothèques .NET, vous pouvez manipuler et extraire efficacement du contenu graphique. Ce guide vous offre une base solide pour débuter dans la manipulation de PDF !

## FAQ

### Comment gérer plusieurs pages dans le PDF ?  
Vous pouvez parcourir chaque page du document en effectuant une itération `doc.Pages` au lieu de coder en dur `doc.Pages[1]`.

### Puis-je extraire d’autres éléments, comme du texte, en utilisant la même approche ?  
Oui, Aspose.PDF fournit des API riches pour extraire du texte, des images et d’autres contenus à partir de fichiers PDF.

### Comment puis-je appliquer une licence pour éviter les limitations ?  
Tu peux [appliquer une licence](https://purchase.aspose.com/temporary-license/) en le chargeant via le `License` cours fourni par Aspose.

### Que faire si mon PDF n’a pas de bordures ?  
Si votre PDF ne contient aucune bordure visible, l'extraction des graphiques risque de ne produire aucun résultat. Assurez-vous que le contenu PDF comporte des bordures dessinables.

### Puis-je enregistrer la sortie dans des formats autres que PNG ?  
Oui, changez simplement le `ImageFormat.Png` vers un autre format pris en charge tel que `ImageFormat.Jpeg`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}