---
category: general
date: 2026-04-12
description: Ajoutez rapidement une figure à Word avec C#. Apprenez à positionner
  la figure dans Word, à insérer la figure dans un fichier docx et à ajouter du XML
  personnalisé pour une mise en page avancée.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: fr
og_description: Ajoutez rapidement une figure à Word avec C#. Apprenez à positionner
  la figure dans Word, à l’insérer dans un fichier docx et à ajouter du XML personnalisé
  pour une mise en page avancée.
og_title: Ajouter une figure à Word – Guide complet de programmation C#
tags:
- C#
- Word Automation
- Document Generation
title: Ajouter une figure à Word – Guide complet de programmation C#
url: /fr/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une figure à Word – Guide complet de programmation C#

Vous avez déjà eu besoin d'**ajouter une figure à Word** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul. Dans de nombreux projets d'automatisation de bureau, l'élément manquant est une image ou un diagramme bien placé qui vit à l'intérieur d'une partie XML personnalisée. Ce guide vous montre exactement comment **positionner une figure dans Word**, insérer la figure dans un fichier *.docx*, et même ajuster le XML personnalisé sous‑jacent afin que la forme se comporte comme n'importe quel objet natif de Word.

Nous allons parcourir un exemple réel en utilisant la bibliothèque GemBox.Document (gratuite pour les petits fichiers, commerciale pour les charges de travail plus importantes). À la fin, vous disposerez d'un programme autonome et exécutable qui place une figure aux coordonnées X = 50, Y = 200 à l'intérieur d'un conteneur de contenu balisé. Pas de raccourcis vagues du type « voir la documentation » — seulement du code clair, les raisons de son fonctionnement, et des astuces que vous pouvez copier directement dans votre propre projet.

## Prérequis

- .NET 6.0 ou version ultérieure (le code se compile également avec .NET Core 3.1)
- Package NuGet **GemBox.Document** (`Install-Package GemBox.Document`)
- Un fichier Word de départ (`input.docx`) qui contient déjà une balise XML personnalisée à l'endroit où vous souhaitez que la figure apparaisse
- Connaissances de base en C# (vous verrez pourquoi chaque ligne est importante)

> **Astuce pro :** Si vous n'avez pas de document pré‑balisé, vous pouvez en créer un dans Word en insérant un *Contrôle de contenu* → *Volet de mappage XML* → mapper une partie XML personnalisée. La bibliothèque traitera ce contrôle comme `TaggedContent`.

## Étape 1 – Charger le document source

La première chose que nous faisons est d'ouvrir le fichier *.docx* existant. `Document` est le point d'entrée pour toutes les opérations GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Pourquoi ?* Charger le fichier nous donne accès à ses parties internes, y compris aux conteneurs XML personnalisés. Sans cela, nous ne pourrions pas localiser le nœud `TaggedContent` qui contiendra notre figure.

## Étape 2 – Accéder au contenu balisé (conteneur XML personnalisé)

Le XML personnalisé est stocké à l'intérieur d'un *contrôle de contenu* dans Word. GemBox l'expose sous le nom `TaggedContent`.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Si le document possède plusieurs sections balisées, `TaggedContent` renvoie la **première**. Vous pouvez également énumérer `doc.TaggedContents` pour choisir une balise spécifique par son nom.

## Étape 3 – Créer l'élément Figure

`FigureElement` représente une image, un graphique ou tout objet visuel que Word considère comme une *forme*. Nous le créerons à l'intérieur du conteneur balisé.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Pourquoi créer une figure ici ?* En l'attachant au nœud XML personnalisé, Word sait que la figure appartient à cette section logique, ce qui est crucial pour les modifications ultérieures ou les flux de travail basés sur les contrôles de contenu.

## Étape 4 – Positionner la figure avec précision

Word utilise des points (1 pt ≈ 1/72 in) pour le positionnement. La structure `PointF` nous permet de définir facilement les coordonnées X/Y.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Comment positionner une forme dans Word :** La propriété `Position` accepte un `PointF` où la première valeur est le décalage horizontal (gauche) et la seconde le décalage vertical (haut) par rapport à la marge de la page. Ajustez ces nombres pour affiner le placement.

## Étape 5 – Insérer la figure dans l'arbre de contenu balisé

Nous attachons maintenant la figure à l'élément racine de l'arbre XML personnalisé. Cela ajoute physiquement la forme au document Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

À ce stade, la figure se trouve dans le document, mais elle n'a pas encore de source d'image. Ajoutons un PNG simple depuis le disque.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Étape 6 – Enregistrer le document modifié

Enfin, nous écrivons les modifications dans un nouveau fichier *.docx*.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Lorsque vous ouvrez `output.docx` dans Word, vous verrez l'image positionnée exactement à (50, 200) à l'intérieur du bloc XML personnalisé que vous avez ciblé.

### Exemple complet fonctionnel

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Résultat attendu :** L'ouverture de `output.docx` montre le PNG placé exactement où vous l'avez spécifié, imbriqué dans la partie XML personnalisée. Si vous inspectez le XML du document (`.docx` → dézipper → `word/document.xml`), vous verrez un élément `<w:pict>` avec les coordonnées correctes du `<v:shape>`.

## Questions fréquentes & cas particuliers

### Et si le document possède plusieurs sections balisées ?

Utilisez `doc.TaggedContents` pour énumérer et sélectionner par nom de balise :

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Comment ajouter une légende à la figure ?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Cela fonctionne-t-il avec Word 2010 et versions ultérieures ?

Oui. GemBox.Document cible la norme Open XML, qui est compatible avec Word 2007 + (y compris 2010, 2013, 2016, 2019 et Microsoft 365).

### Et si je dois faire pivoter la forme ?

```csharp
figure.Rotation = 45; // degrees
```

### Comment ajouter un graphique vectoriel au lieu d'une image raster ?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Astuces pro & pièges

- **Chemins de fichiers :** Utilisez `Path.Combine` pour éviter les séparateurs codés en dur, surtout sur les plateformes non Windows.
- **Limites de licence :** La licence gratuite de GemBox limite la taille du document à 20 KB. Pour des fichiers plus volumineux, achetez une clé commerciale.
- **Performance :** Réutiliser une seule instance `Document` pour le traitement par lots réduit considérablement la consommation de mémoire.
- **Débordement de forme :** Si les dimensions de la figure dépassent les marges de la page, Word la découpera. Ajustez `figure.Width` et `figure.Height` en conséquence.

## Conclusion

Vous savez maintenant **comment ajouter une figure à Word**, **positionner précisément une figure dans Word**, et manipuler le XML personnalisé sous‑jacent pour que la forme se comporte comme n'importe quel élément natif. L'exemple complet et exécutable montre chaque étape — du chargement du document, à la création d'un `FigureElement`, en passant par la définition de ses coordonnées, l'attachement d'une image, et enfin l'enregistrement du *.docx* mis à jour.

Ensuite, essayez d'expérimenter avec **insert figure into docx** en ajoutant plusieurs figures, en utilisant des boucles, ou en générant des graphiques à la volée. Vous pouvez également explorer **how to add custom xml** pour des contrôles de contenu plus riches ou apprendre **how to position shape word** dans les tableaux et les en-têtes. Les possibilités sont infinies, et avec les bases couvertes ici, vous êtes prêt à automatiser les documents Word comme un pro.

Bon codage, et n'hésitez pas à laisser un commentaire si vous rencontrez le moindre problème !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}