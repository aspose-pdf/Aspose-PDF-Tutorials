---
"description": "Apprenez à baliser des images dans des PDF existants avec Aspose.PDF pour .NET. Guide étape par étape pour améliorer l'accessibilité grâce à la conformité PDF/UA."
"linktitle": "Image de balise dans un PDF existant"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Image de balise dans un PDF existant"
"url": "/fr/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Image de balise dans un PDF existant

## Introduction

Dans ce tutoriel, nous vous expliquerons comment baliser une image dans un PDF existant avec Aspose.PDF pour .NET. À la fin de ce guide, vous serez capable de définir un texte alternatif pour les images, d'ajuster les attributs de mise en page et de garantir la conformité de votre PDF aux normes d'accessibilité.

## Prérequis

Avant de commencer, passons en revue ce dont vous aurez besoin pour commencer :

- Aspose.PDF pour .NET : assurez-vous d’avoir téléchargé et installé la dernière version d’Aspose.PDF pour .NET. [Télécharger ici](https://releases.aspose.com/pdf/net/).
- .NET Framework : assurez-vous d’avoir configuré un environnement de développement .NET tel que Visual Studio.
- Compréhension de base de la structure PDF : Familiarité avec les éléments de structure PDF tels que les paragraphes, les étendues, les tableaux et les images.
- Une licence valide : Vous pouvez soit acheter une licence [ici](https://purchase.aspose.com/buy) ou utilisez-en un temporaire [ici](https://purchase.aspose.com/temporary-license/).

## Importer des packages

Pour commencer à coder, vous devez importer les espaces de noms essentiels depuis Aspose.PDF pour .NET. Ceux-ci vous donneront accès aux classes et méthodes nécessaires pour manipuler le document PDF.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Maintenant que nous avons préparé le terrain, décomposons le processus de marquage d’une image en plusieurs étapes.

## Étape 1 : Charger le document PDF existant

La première étape consiste à charger le fichier PDF que vous souhaitez utiliser. Il peut s'agir de n'importe quel fichier PDF contenant une image à baliser.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// Ouvrir le document
Document document = new Document(inFile);
```

- Remplacer `"YOUR DOCUMENT DIRECTORY"` avec le chemin réel vers votre fichier.
- Le `Document` La classe vous permet de charger un PDF existant. Vous modifierez ce PDF pour baliser l'image.

## Étape 2 : Accéder au contenu balisé et à l'élément de structure racine

Une fois le PDF ouvert, l'étape suivante consiste à accéder au contenu balisé et à identifier l'élément de structure racine. Cette étape est cruciale, car elle vous permet de parcourir les éléments du PDF et d'y apporter des modifications.

```csharp
// Obtenir le contenu balisé et l'élément de structure racine
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` donne accès aux éléments structurés du PDF.
- Le `RootElement` est l'élément de structure le plus élevé, à partir duquel vous pouvez accéder à d'autres éléments tels que des paragraphes, des tableaux et des images.

## Étape 3 : Définir le titre du document PDF balisé

L'ajout d'un titre au document PDF balisé garantit que votre document est correctement étiqueté, ce qui est utile pour l'accessibilité et la conformité PDF/UA.

```csharp
// Définir le titre du document PDF balisé
taggedContent.SetTitle("Document with images");
```

- La définition d’un titre pour votre PDF balisé améliore l’accessibilité et la clarté du document pour les lecteurs d’écran et les technologies d’assistance.

## Étape 4 : Rechercher et étiqueter l’image

Maintenant, trouvons l'élément d'image (appelé `FigureElement` dans Aspose.PDF), définissez un texte alternatif et configurez ses attributs de mise en page.

```csharp
// Parcourez tous les éléments de la figure (images) et définissez des attributs de texte et de mise en page alternatifs.
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // Définir un texte alternatif pour la figure
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // Créer et définir l'attribut BBox (boîte englobante)
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // Définir les attributs de mise en page pour la figure
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- Ce code parcourt tous les `FigureElement` objets dans la structure racine, qui représentent des images.
- Il définit le texte alternatif pour l'accessibilité (les lecteurs d'écran l'utiliseront pour décrire l'image).
- Le cadre de délimitation (`BBox`) spécifie les coordonnées de la mise en page de l'image, garantissant qu'elle est correctement affichée dans le document.

## Étape 5 : Modifier les éléments Span dans le tableau

Dans certains cas, vous devrez peut-être modifier des éléments span dans un tableau. Nous allons ici vous montrer comment trouver un `SpanElement` et le déplacer dans un paragraphe.

```csharp
// Rechercher les éléments de tableau, d'étendue et de paragraphe
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// Déplacer l'élément span dans le paragraphe
spanElement.ChangeParentElement(paragraph);
```

- Ici, nous localisons le `TableElement`, `SpanElement`, et `ParagraphElement` dans le PDF.
- En utilisant le `ChangeParentElement` méthode, nous déplaçons l'étendue dans le paragraphe pour assurer un balisage et une structure appropriés.

## Étape 6 : Enregistrez le document et validez la conformité PDF/UA

Une fois toutes les modifications effectuées, l’étape finale consiste à enregistrer le PDF mis à jour et à vérifier s’il est conforme aux normes PDF/UA.

```csharp
// Enregistrer le document PDF mis à jour
document.Save(outFile);

// Valider la conformité PDF/UA
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- Le `Validate` La méthode vérifie le document PDF par rapport aux normes PDF/UA et enregistre les résultats.
- Assurer la conformité permet d’améliorer l’accessibilité et de répondre aux exigences réglementaires en matière de publication de documents.

## Conclusion

Dans ce tutoriel, nous vous avons montré comment baliser des images dans un PDF existant avec Aspose.PDF pour .NET. En définissant un texte alternatif, en ajustant les attributs de mise en page et en validant la conformité PDF/UA du document, vous garantissez l'accessibilité et la conformité de vos PDF aux normes actuelles. Aspose.PDF simplifie l'utilisation d'éléments structurés et vous permet de contrôler la mise en page et l'accessibilité de votre document.

## FAQ

### À quoi sert Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque puissante utilisée pour créer, éditer et manipuler des documents PDF par programmation dans un environnement .NET.

### Comment garantir la conformité PDF/UA ?
Vous pouvez utiliser Aspose.PDF `Validate` méthode pour vérifier la conformité PDF/UA après avoir apporté des modifications au document.

### Qu'est-ce qu'un texte alternatif dans les PDF ?
Le texte alternatif est une description ajoutée aux images dans les fichiers PDF pour améliorer l'accessibilité, en particulier pour les utilisateurs qui utilisent des lecteurs d'écran.

### Puis-je manipuler des tableaux et des étendues dans un PDF avec Aspose.PDF ?
Oui, Aspose.PDF vous permet de manipuler des tableaux, des étendues et d’autres éléments structurés dans un document PDF.

### Où puis-je télécharger Aspose.PDF pour .NET ?
Vous pouvez télécharger la dernière version d'Aspose.PDF pour .NET [ici](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}