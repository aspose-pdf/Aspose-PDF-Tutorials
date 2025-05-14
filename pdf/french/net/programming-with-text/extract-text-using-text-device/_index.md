---
"description": "Découvrez comment extraire du texte d’un document PDF à l’aide du périphérique texte dans Aspose.PDF pour .NET."
"linktitle": "Extraire du texte à l'aide d'un périphérique texte"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Extraire du texte à l'aide d'un périphérique texte"
"url": "/fr/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à l'aide d'un périphérique texte

## Introduction

Extraire du texte d'un PDF peut s'avérer complexe, surtout lorsqu'il s'agit de documents aux formats variés, aux polices intégrées ou aux mises en page complexes. Mais avec Aspose.PDF pour .NET, ce processus devient un jeu d'enfant ! Que vous souhaitiez convertir des pages d'un PDF en texte brut pour une analyse plus approfondie ou simplement extraire des sections spécifiques, Aspose.PDF est là pour vous. Dans ce tutoriel, nous vous expliquerons étape par étape comment extraire du texte d'un PDF à l'aide de la classe TextDevice d'Aspose.PDF. Nous vous fournirons également des explications claires pour que vous puissiez appliquer facilement les mêmes méthodes à vos propres projets.

## Prérequis

Avant de passer au code, assurez-vous d'avoir tout en place pour suivre. Voici ce dont vous aurez besoin :

1. Aspose.PDF pour .NET : téléchargez la dernière version à partir du [Page de téléchargement d'Aspose.PDF pour .NET](https://releases.aspose.com/pdf/net/).
2. Environnement de développement : Visual Studio ou tout autre environnement de développement C#.
3. .NET Framework : assurez-vous que votre projet cible .NET Framework 4.x ou supérieur.
4. Fichier PDF d'entrée : fichier PDF que vous utiliserez pour l'extraction de texte. Placez-le dans un répertoire de votre machine (nous l'appellerons `YOUR DOCUMENT DIRECTORY`).

## Importer des packages

En haut de votre code, vous devrez importer les espaces de noms nécessaires pour travailler avec Aspose.PDF :

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## Étape 1 : Chargez votre document PDF

Avant d'extraire le texte, nous devons charger le document PDF en mémoire. À cette étape, vous ouvrirez votre PDF avec Aspose.PDF. `Document` classe. Cela vous permettra d'accéder à toutes les pages et à tout le contenu du fichier.

```csharp
// Définissez le chemin d'accès à votre document PDF
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Charger le document PDF
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Ici, nous utilisons `Document pdfDocument = new Document(dataDir + "input.pdf");` pour charger le PDF. Le `dataDir` La variable contient le chemin d'accès au répertoire de votre fichier PDF. Elle nous donne accès à l'intégralité du document, nous permettant de parcourir les pages et d'en extraire le contenu.

## Étape 2 : Configurer un générateur de chaînes pour le stockage de texte

Maintenant que le document est chargé, nous devons trouver un moyen de stocker le texte extrait. Pour cela, nous utiliserons un `StringBuilder` qui permet une concaténation efficace des chaînes.

```csharp
// StringBuilder pour contenir le texte extrait
StringBuilder builder = new StringBuilder();
```

Nous initialisons un `StringBuilder` instance, qui collectera le texte extrait de chaque page. C'est une méthode plus efficace pour gérer les chaînes volumineuses que la concaténation classique de chaînes dans une boucle.

## Étape 3 : Parcourir les pages PDF

Ensuite, nous parcourons chaque page du document PDF pour en extraire le texte. Nous traiterons chaque page individuellement à l'aide de la commande `TextDevice` classe, qui est responsable de la conversion du contenu PDF au format texte.

```csharp
// Parcourez toutes les pages du PDF
foreach (Page pdfPage in pdfDocument.Pages)
{
    // Traiter chaque page pour l'extraction de texte
}
```

Cette boucle parcourt chaque page du PDF (`pdfDocument.Pages`). Pour chaque page, nous extrairons le texte et l'ajouterons à notre `StringBuilder`.

## Étape 4 : Extraire le texte de chaque page

Nous allons maintenant configurer le processus d'extraction de texte pour chaque page. Ici, nous allons créer un `TextDevice` objet et l'utiliser pour traiter les pages PDF. `TextDevice` extrait du texte brut ou formaté en fonction des options d'extraction que nous définissons.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // Créer un périphérique texte pour l'extraction de texte
    TextDevice textDevice = new TextDevice();
    
    // Définir les options d'extraction de texte sur le mode « Pur »
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // Extraire le texte de la page actuelle et l'enregistrer dans le flux de mémoire
    textDevice.Process(pdfPage, textStream);

    // Convertir le flux de mémoire en texte
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // Ajouter le texte extrait au StringBuilder
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: Le `TextDevice` la classe est utilisée pour extraire du texte du PDF.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: Cette option extrait le texte brut sans conserver de formatage, comme les polices ou les positions. Vous pouvez également utiliser `TextFormattingMode.Raw` si vous avez besoin de plus de contrôle sur le formatage.
- `textDevice.Process(pdfPage, textStream);`: Cela traite chaque page du PDF et stocke le texte extrait dans un `MemoryStream`.
- Enfin, nous convertissons le texte du `MemoryStream` à une chaîne et l'ajouter à la `StringBuilder`.

## Étape 5 : Enregistrer le texte extrait dans un fichier

Après avoir traité toutes les pages, le texte est stocké dans le `StringBuilder`La dernière étape consiste à enregistrer ce texte extrait dans un fichier.

```csharp
// Définir le chemin de sortie du fichier texte
dataDir = dataDir + "input_Text_Extracted_out.txt";

// Enregistrer le texte extrait dans un fichier
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`: Ceci écrit tout le contenu du `StringBuilder` dans un fichier texte.
- Le chemin d'accès au fichier de sortie est défini en ajoutant un nom de fichier (`"input_Text_Extracted_out.txt"`) au `dataDir` chemin.

## Conclusion

Extraire du texte d'un PDF avec Aspose.PDF pour .NET est un processus simple et efficace. En suivant les étapes décrites dans ce guide, vous pouvez facilement ouvrir des documents PDF, parcourir les pages et extraire du texte dans un fichier texte. Ceci est particulièrement utile pour traiter de gros volumes de données PDF, effectuer des analyses de texte ou convertir des documents en vue de manipulations ultérieures.

Avec Aspose.PDF, vous ne vous limitez pas à l'extraction de texte : vous pouvez gérer les annotations, manipuler les images et même convertir des PDF dans d'autres formats comme HTML ou Word. La flexibilité et la puissance de cette bibliothèque en font un outil précieux pour la gestion des PDF dans les applications .NET.

## FAQ

### Aspose.PDF peut-il extraire du texte à partir de fichiers PDF basés sur des images ?
Non, Aspose.PDF est conçu pour extraire du texte à partir de PDF contenant du contenu. Pour les PDF contenant des images, la technologie OCR est nécessaire.

### Aspose.PDF conserve-t-il la mise en forme lors de l'extraction de texte ?
Par défaut, le texte est extrait sans mise en forme, mais vous pouvez ajuster les options d'extraction si vous souhaitez conserver une certaine mise en forme.

### Puis-je extraire du texte d’une plage de pages spécifique ?
Oui, vous pouvez modifier le code pour qu'il boucle sur une plage spécifique de pages au lieu de toutes les pages.

### Quels sont les modes d'extraction de texte dans Aspose.PDF ?
Aspose.PDF propose deux modes : Brut et Pur. Le mode Brut tente de conserver la mise en page d'origine, tandis que le mode Pur extrait uniquement le texte sans mise en forme.

### Aspose.PDF pour .NET est-il compatible avec .NET Core ?
Oui, Aspose.PDF pour .NET est entièrement compatible avec .NET Core et .NET Framework.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}