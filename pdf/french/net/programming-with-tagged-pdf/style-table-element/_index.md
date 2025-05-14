---
"description": "Découvrez comment créer et styliser un élément de tableau dans Aspose.PDF pour .NET avec des instructions étape par étape, un style personnalisé et la conformité PDF/UA."
"linktitle": "Élément de tableau de style"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Élément de tableau de style"
"url": "/fr/net/programming-with-tagged-pdf/style-table-element/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Élément de tableau de style

## Introduction

Dans cet article, nous allons découvrir comment créer et styliser un élément de tableau avec Aspose.PDF pour .NET. Vous apprendrez à structurer un tableau, à appliquer des styles personnalisés et à valider la conformité PDF/UA de votre document. À la fin de ce tutoriel, vous serez capable de créer facilement des tableaux de qualité professionnelle dans vos PDF !

## Prérequis

Avant de commencer le didacticiel, vous devez vous assurer que vous disposez des éléments suivants :

1. Visual Studio ou un IDE similaire installé sur votre machine.
2. .NET Framework ou .NET Core SDK pour exécuter l'application.
3. Bibliothèque Aspose.PDF pour .NET téléchargée et référencée dans votre projet. Vous pouvez obtenir la dernière version sur [ici](https://releases.aspose.com/pdf/net/).
4. Une licence Aspose valide ou un [permis temporaire](https://purchase.aspose.com/temporary-license/) pour déverrouiller toutes les fonctionnalités de la bibliothèque.

## Importer des packages

Pour commencer, importez les espaces de noms nécessaires dans votre projet :

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ces espaces de noms couvrent les opérations PDF de base, le contenu balisé, les tableaux et la mise en forme du texte.

Décomposons maintenant le processus de création et de mise en forme d'un tableau dans Aspose.PDF. Nous détaillerons chaque section pour que vous puissiez suivre le processus.

## Étape 1 : Créer un nouveau document PDF et configurer le contenu balisé

Dans cette première étape, nous allons créer un document PDF vierge et configurer son contenu balisé.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Créer un nouveau document PDF
Document document = new Document();

// Configurer le contenu balisé
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table style");
taggedContent.SetLanguage("en-US");
```

Nous commençons par créer un nouveau `Document` objet, représentant notre PDF. Le `TaggedContent` L'objet permet de gérer la structure du document, garantissant ainsi sa conformité aux normes d'accessibilité. Nous définissons le titre et la langue du document pour un balisage approprié.

## Étape 2 : Définir l’élément racine

Ensuite, nous allons créer l’élément de structure racine, qui agit comme conteneur pour tout le contenu de notre PDF.

```csharp
// Obtenir l'élément de structure racine
StructureElement rootElement = taggedContent.RootElement;
```

Le `RootElement` Il sert de conteneur de base pour tous les éléments structurés, y compris notre tableau. Il contribue à maintenir la hiérarchie structurelle du document, essentielle à l'organisation et à l'accessibilité.

## Étape 3 : Créer et styliser l’élément de tableau

Maintenant que l'élément racine est configuré, nous allons créer un `TableElement` et appliquez des styles tels que la couleur d'arrière-plan, les bordures et l'alignement.

```csharp
// Créer un élément de structure de table
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// Styliser la table
tableElement.BackgroundColor = Color.Beige;
tableElement.Border = new BorderInfo(BorderSide.All, 0.80F, Color.Gray);
tableElement.Alignment = HorizontalAlignment.Center;
tableElement.Broken = TableBroken.Vertical;
tableElement.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```

Nous créons un `TableElement`, qui définit la structure de notre table. `BackgroundColor`, `Border`, et `Alignment` Les propriétés nous permettent de personnaliser l'apparence du tableau. `Broken` La propriété garantit que si le tableau est divisé en plusieurs pages, il est divisé verticalement.

## Étape 4 : Définir les dimensions du tableau et les styles de cellule

Dans cette étape, nous allons définir le nombre de colonnes, le remplissage des cellules et d’autres propriétés importantes du tableau.

```csharp
tableElement.ColumnWidths = "80 80 80 80 80";
tableElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.DarkBlue);
tableElement.DefaultCellPadding = new MarginInfo(16.0, 2.0, 8.0, 2.0);
tableElement.DefaultCellTextState.ForegroundColor = Color.DarkCyan;
tableElement.DefaultCellTextState.FontSize = 8F;
```

Nous spécifions les largeurs de colonne pour garantir que chaque colonne du tableau est uniformément espacée. `DefaultCellBorder`, `DefaultCellPadding`, et `DefaultCellTextState` définir les styles par défaut des cellules, y compris les bordures, le remplissage, la couleur du texte et la taille de la police.

## Étape 5 : Ajouter des lignes répétitives et des styles personnalisés

Nous pouvons également définir des styles pour les lignes répétitives et d'autres éléments de tableau spécifiques comme les en-têtes et les pieds de page.

```csharp
tableElement.RepeatingRowsCount = 3;
TextState rowStyle = new TextState();
rowStyle.BackgroundColor = Color.LightCoral;
tableElement.RepeatingRowsStyle = rowStyle;
```

Le `RepeatingRowsCount` garantit que les trois premières lignes se répètent si le tableau s'étend sur plusieurs pages. Nous définissons `RepeatingRowsStyle` pour appliquer une couleur d'arrière-plan personnalisée à ces lignes.

## Étape 6 : Ajouter les éléments d'en-tête, de corps et de pied du tableau

Maintenant, créons les sections d’en-tête, de corps et de pied de page du tableau et remplissons-les de contenu.

```csharp
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// Créer une ligne d'en-tête
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 5; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
}

// Remplir le corps du tableau
for (int rowIndex = 0; rowIndex < 10; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    for (int colIndex = 0; colIndex < 5; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
    }
}
```

Le tableau est divisé en trois parties : l'en-tête, le corps et le pied de page. Nous créons d'abord la ligne d'en-tête avec `TableTHElement` et ajoutons des en-têtes de colonnes. Ensuite, nous remplissons le corps du tableau avec `TableTDElement`, en remplissant chaque cellule avec une étiquette qui inclut sa position.

## Étape 7 : Enregistrer le document

Enfin, nous enregistrons le document PDF dans le répertoire spécifié.

```csharp
// Enregistrer le document PDF balisé
document.Save(dataDir + "StyleTableElement.pdf");
```

Cette étape finalise le processus de création du document en enregistrant le fichier PDF avec le tableau stylisé.

## Étape 8 : Valider la conformité PDF/UA

Après avoir enregistré le document, il est essentiel de s'assurer qu'il est conforme aux normes PDF/UA (Universal Accessibility).

```csharp
// Vérifier la conformité PDF/UA
document = new Document(dataDir + "StyleTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableElement.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Ici, nous rechargeons le document et le validons selon les normes PDF/UA. Cette conformité garantit que votre PDF répond aux exigences d'accessibilité, le rendant ainsi adapté à un large éventail d'utilisateurs.

## Conclusion

Avec Aspose.PDF pour .NET, créer et styliser des tableaux dans vos documents PDF est simple et intuitif. En suivant les étapes décrites dans ce tutoriel, vous pouvez créer des tableaux avec des styles personnalisés et garantir que vos PDF respectent les normes d'accessibilité. Que vous génériez des rapports ou créiez des documents structurés, les tableaux sont un outil puissant pour présenter clairement les données.

## FAQ

### Puis-je ajouter des images à l’intérieur des cellules d’un tableau ?
Oui, vous pouvez insérer des images dans les cellules d'un tableau à l'aide de la `Image` élément.

### Comment ajuster la largeur des colonnes de manière dynamique ?
Vous pouvez définir le `ColumnAdjustment` propriété à `AutoFitToWindow` pour ajuster automatiquement la largeur des colonnes en fonction du contenu.

### La conformité PDF/UA est-elle obligatoire pour tous les documents ?
Bien que non obligatoire, il est recommandé pour les documents qui nécessitent des normes d’accessibilité élevées.

### Puis-je appliquer différents styles à des lignes spécifiques ?
Oui, vous pouvez personnaliser des lignes ou des cellules individuelles en ajustant leur `TextState` ou `BackgroundColor`.

### Quel est l’avantage d’utiliser du contenu balisé ?
Le contenu balisé améliore l'accessibilité des documents et contribue à garantir la conformité avec des normes telles que PDF/UA.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}