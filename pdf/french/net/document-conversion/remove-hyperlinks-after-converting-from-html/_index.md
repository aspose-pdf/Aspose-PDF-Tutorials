---
"description": "Découvrez comment supprimer les hyperliens des documents HTML après la conversion au format PDF à l'aide d'Aspose.PDF pour .NET dans ce guide étape par étape."
"linktitle": "Supprimer les hyperliens après la conversion depuis HTML"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Supprimer les hyperliens après la conversion depuis HTML"
"url": "/fr/net/document-conversion/remove-hyperlinks-after-converting-from-html/"
"weight": 250
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer les hyperliens après la conversion depuis HTML

## Introduction

À l'ère du numérique, convertir des documents HTML en PDF est une tâche courante. Cependant, il peut être nécessaire de supprimer des hyperliens du PDF converti pour diverses raisons, comme améliorer la lisibilité ou éviter une navigation indésirable. Dans ce tutoriel, nous découvrirons comment y parvenir avec Aspose.PDF pour .NET. 

## Prérequis

Avant de plonger dans le code, assurez-vous de disposer des prérequis suivants :

1. Visual Studio : Assurez-vous que Visual Studio est installé sur votre machine. Ce sera votre environnement de développement.
2. Aspose.PDF pour .NET : vous devez disposer de la bibliothèque Aspose.PDF. Vous pouvez la télécharger ici. [ici](https://releases.aspose.com/pdf/net/).
3. Connaissances de base de C# : la familiarité avec la programmation C# vous aidera à mieux comprendre le code.

## Importer des packages

Pour commencer, vous devez importer les packages nécessaires dans votre projet C#. Voici comment procéder :

1. Ouvrez votre projet Visual Studio.
2. Cliquez avec le bouton droit sur votre projet dans l'Explorateur de solutions et sélectionnez « Gérer les packages NuGet ».
3. Rechercher `Aspose.PDF` et installez-le.

```csharp
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.IO;
```

Maintenant que tout est configuré, décomposons le processus de suppression des hyperliens d'un fichier HTML après sa conversion en PDF.

## Étape 1 : Configurer le répertoire de documents

Tout d'abord, vous devez spécifier le chemin d'accès à votre répertoire de documents. C'est là que se trouve votre fichier HTML et où le PDF de sortie sera enregistré.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin réel où votre fichier HTML est stocké.

## Étape 2 : Charger le document HTML

Ensuite, vous chargerez le document HTML en utilisant le `Document` Cours d'Aspose.PDF. Ce cours vous permet de travailler facilement avec des documents PDF.

```csharp
Document doc = new Document(dataDir + "SampleHtmlFile.html", new HtmlLoadOptions());
```

Ici, nous chargeons le fichier HTML nommé `SampleHtmlFile.html`Assurez-vous que ce fichier existe dans votre répertoire spécifié.

## Étape 3 : Enregistrer le document dans Memory Stream

Avant de commencer le traitement des annotations, nous devons enregistrer le document dans un flux mémoire. Cette étape est cruciale car elle prépare le document à des manipulations ultérieures.

```csharp
doc.Save(new MemoryStream());
```

Cette ligne enregistre le document en mémoire, nous permettant de travailler avec lui sans l'écrire sur le disque pour le moment.

## Étape 4 : parcourir les annotations

Nous allons maintenant parcourir les annotations du document. Les annotations sont des éléments tels que les liens, les commentaires et les surlignages. Nous nous intéressons plus particulièrement aux annotations de liens.

```csharp
foreach (Annotation a in doc.Pages[1].Annotations)
{
    if (a.AnnotationType == AnnotationType.Link)
    {
        // Traiter l'annotation du lien
    }
}
```

Dans cette boucle, nous vérifions si le type d'annotation est un lien. Si c'est le cas, nous passons aux étapes suivantes.

## Étape 5 : Supprimer l'action de lien hypertexte

Pour chaque annotation de lien, nous devons vérifier si elle possède une action d'hyperlien. Si c'est le cas, nous supprimerons l'hyperlien en définissant son URI sur une chaîne vide.

```csharp
LinkAnnotation la = (LinkAnnotation)a;
if (la.Action is GoToURIAction)
{
    GoToURIAction gta = (GoToURIAction)la.Action;
    gta.URI = "";
```

Cet extrait de code garantit que l’action du lien hypertexte est effectivement supprimée.

## Étape 6 : Absorber les fragments de texte

Nous allons ensuite absorber les fragments de texte associés à l'annotation du lien. Cela nous permettra de manipuler l'apparence du texte.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
tfa.TextSearchOptions = new TextSearchOptions(a.Rect);
doc.Pages[a.PageIndex].Accept(tfa);
```

Ici, nous créons un `TextFragmentAbsorber` et définissez ses options de recherche sur le rectangle de l'annotation. Cela nous aide à trouver le texte lié.

## Étape 7 : Modifier l’apparence du texte

Une fois les fragments de texte récupérés, nous pouvons modifier leur apparence. Dans ce cas, nous supprimerons le soulignement et changerons la couleur du texte en noir.

```csharp
foreach (TextFragment tf in tfa.TextFragments)
{
    tf.TextState.Underline = false;
    tf.TextState.ForegroundColor = Color.Black;
}
```

Cette étape améliore la lisibilité du texte en supprimant le style des hyperliens.

## Étape 8 : Supprimer l’annotation

Après avoir modifié le texte, nous pouvons supprimer en toute sécurité l’annotation du lien du document.

```csharp
doc.Pages[a.PageIndex].Annotations.Delete(a);
}
```

Cette ligne supprime l'hyperlien du PDF, garantissant qu'il n'existe plus dans la sortie finale.

## Étape 9 : Enregistrer le document modifié

Enfin, nous devons enregistrer le document modifié dans un nouveau fichier PDF. C'est la dernière étape de notre processus.

```csharp
doc.Save(dataDir + "RemoveHyperlinksFromText_out.pdf");
```

Cette ligne enregistre le document avec les hyperliens supprimés, créant un nouveau fichier PDF nommé `RemoveHyperlinksFromText_out.pdf`.

## Conclusion

Et voilà ! Vous avez réussi à supprimer les hyperliens d'un document HTML après l'avoir converti en PDF avec Aspose.PDF pour .NET. Ce processus améliore non seulement la lisibilité de votre PDF, mais vous permet également de contrôler le contenu présenté. 

## FAQ

### Puis-je supprimer des hyperliens de n’importe quel document PDF ?
Oui, vous pouvez supprimer les hyperliens de n’importe quel document PDF à l’aide d’Aspose.PDF pour .NET.

### L'utilisation d'Aspose.PDF est-elle gratuite ?
Aspose.PDF propose un essai gratuit, mais pour accéder à toutes les fonctionnalités, vous devez acheter une licence. Consultez la [page d'achat](https://purchase.aspose.com/buy).

### Que faire si je rencontre des problèmes lors de l’utilisation d’Aspose.PDF ?
Vous pouvez demander de l'aide sur le [forum d'assistance](https://forum.aspose.com/c/pdf/10).

### Puis-je convertir d’autres formats de fichiers en PDF à l’aide d’Aspose ?
Oui, Aspose prend en charge différents formats de fichiers pour la conversion en PDF.

### Où puis-je télécharger Aspose.PDF pour .NET ?
Vous pouvez le télécharger à partir du [lien de téléchargement](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}