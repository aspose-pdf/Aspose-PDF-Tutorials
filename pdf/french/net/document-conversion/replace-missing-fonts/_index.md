---
"description": "Découvrez comment remplacer les polices manquantes dans les documents PDF à l’aide d’Aspose.PDF pour .NET avec ce guide étape par étape."
"linktitle": "Remplacer les polices manquantes"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Remplacer les polices manquantes"
"url": "/fr/net/document-conversion/replace-missing-fonts/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Remplacer les polices manquantes

## Introduction

Avez-vous déjà ouvert un document PDF et constaté l'absence de certaines polices ? C'est frustrant, n'est-ce pas ? L'absence de polices peut donner un document complètement différent de celui souhaité par son créateur. Heureusement, avec Aspose.PDF pour .NET, vous pouvez facilement remplacer les polices manquantes et garantir que vos documents PDF conservent leur apparence initiale. Dans ce tutoriel, nous vous guiderons pas à pas pour une procédure simple et directe.

## Prérequis

Avant de commencer, vous devez mettre en place quelques éléments :

1. Aspose.PDF pour .NET : Assurez-vous d'avoir installé la bibliothèque Aspose.PDF. Vous pouvez la télécharger depuis [ici](https://releases.aspose.com/pdf/net/).
2. Visual Studio : un environnement de développement dans lequel vous pouvez écrire et tester votre code.
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre les extraits de code.

## Importer des packages

Pour commencer, vous devrez importer les packages nécessaires dans votre projet C#. Voici comment procéder :

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## Étape 1 : Configurez votre répertoire de documents

Tout d'abord, vous devez spécifier le chemin d'accès à votre répertoire de documents. C'est là que se trouve votre fichier PDF d'entrée et où sera enregistré le fichier de sortie.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## Étape 2 : Initialiser la police d’origine

Ensuite, vous devrez essayer de trouver la police d'origine manquante. Dans ce cas, nous recherchons « AgencyFB ».

```csharp
Aspose.Pdf.Text.Font originalFont = null;
try
{
    originalFont = FontRepository.FindFont("AgencyFB");
}
catch (Exception)
{
    // La police est manquante sur la machine de destination
    FontRepository.Substitutions.Add(new SimpleFontSubstitution("AgencyFB", "Arial"));
}
```

Ici, nous essayons de trouver la police. Si elle est introuvable, nous interceptons l'exception et la remplaçons par une police plus courante, « Arial ». Cela garantit que votre document conserve son aspect, même si la police d'origine n'est pas disponible.

## Étape 3 : Charger le document PDF

Chargez maintenant le document PDF à traiter. Vous devrez spécifier le chemin d'accès au fichier d'entrée.

```csharp
var fileNew = new FileInfo(dataDir + "newfile_out.pdf");
var pdf = new Document(dataDir + "input.pdf");
```

Dans cette étape, nous créons un nouveau `FileInfo` objet pour le fichier de sortie et charger le document PDF d'entrée dans un nouveau `Document` objet.

## Étape 4 : Convertir le document PDF

Avant d'enregistrer le document, il est conseillé de le convertir dans un format PDF spécifique. Dans ce cas, nous le convertirons au format PDF/A-1B, norme d'archivage à long terme des documents électroniques.

```csharp
pdf.Convert(dataDir + "log.xml", PdfFormat.PDF_A_1B, ConvertErrorAction.Delete);
```

Cette ligne convertit le PDF et enregistre les erreurs dans un fichier XML spécifié. Tout problème rencontré lors de la conversion sera enregistré dans le fichier « log.xml ».

## Étape 5 : Enregistrez le document PDF mis à jour

Enfin, il est temps d'enregistrer le document PDF mis à jour avec les polices remplacées.

```csharp
pdf.Save(fileNew.FullName);
```

Cette ligne enregistre le PDF modifié dans le chemin de sortie spécifié. Ainsi, vous avez réussi à remplacer les polices manquantes dans votre document PDF !

## Conclusion

Remplacer les polices manquantes dans vos documents PDF n'est pas forcément une tâche ardue. Avec Aspose.PDF pour .NET, vous pouvez facilement gérer les substitutions de polices et garantir l'apparence parfaite de vos documents. En suivant les étapes décrites dans ce tutoriel, vous préserverez l'intégrité de vos fichiers PDF, même lorsque certaines polices sont indisponibles. Ainsi, la prochaine fois que vous rencontrerez un problème de police manquante, vous saurez exactement quoi faire !

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque puissante qui permet aux développeurs de créer, manipuler et convertir des documents PDF par programmation.

### Puis-je utiliser Aspose.PDF gratuitement ?
Oui, Aspose propose une version d'essai gratuite pour évaluer la bibliothèque. Vous pouvez la télécharger. [ici](https://releases.aspose.com/).

### Que dois-je faire si la police dont j’ai besoin n’est pas disponible ?
Vous pouvez remplacer la police manquante par une police plus courante en utilisant la fonction de substitution de police dans Aspose.PDF.

### Est-il possible de convertir des PDF vers d’autres formats ?
Absolument ! Aspose.PDF prend en charge la conversion vers différents formats, notamment PDF/A, DOCX, etc.

### Où puis-je trouver de l'aide pour Aspose.PDF ?
Vous pouvez trouver du soutien et poser des questions sur le forum Aspose [ici](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}