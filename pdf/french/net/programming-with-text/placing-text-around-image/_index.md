---
"description": "Apprenez à placer du texte autour des images dans vos PDF avec Aspose.PDF pour .NET. Suivez notre guide étape par étape pour créer des PDF professionnels avec images et texte côte à côte."
"linktitle": "Placer du texte autour de l'image dans un fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Placer du texte autour de l'image dans un fichier PDF"
"url": "/fr/net/programming-with-text/placing-text-around-image/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Placer du texte autour de l'image dans un fichier PDF

## Introduction

Avez-vous déjà essayé d'insérer du texte autour d'une image dans un fichier PDF, mais vous avez trouvé cela difficile ? Si oui, vous êtes au bon endroit ! Aspose.PDF pour .NET simplifie ce processus en vous permettant d'insérer du texte à côté d'images en quelques lignes de code seulement. Que vous créiez des rapports, des documents ou des présentations, cette fonctionnalité est un excellent moyen d'améliorer la mise en page de votre contenu et de le rendre plus attrayant visuellement. Aujourd'hui, nous allons vous expliquer comment utiliser Aspose.PDF pour .NET pour insérer du texte autour d'images dans un document PDF.

## Prérequis

Avant de passer au code, vérifions que tout est configuré. Voici ce dont vous aurez besoin :

- Aspose.PDF pour .NET : vous pouvez le télécharger à partir de [ici](https://releases.aspose.com/pdf/net/).
- Visual Studio : assurez-vous d’avoir installé la dernière version pour suivre l’opération en douceur.
- .NET Framework : cet exemple utilise .NET, assurez-vous donc que votre environnement est configuré pour le développement .NET.
- Une licence temporaire : Vous pouvez demander une licence temporaire [ici](https://purchase.aspose.com/temporary-license/) si vous évaluez le produit.

Si vous n'avez pas encore configuré Aspose.PDF pour .NET, suivez les instructions d'installation dans le [documentation](https://reference.aspose.com/pdf/net/).

## Importer des espaces de noms

Avant de commencer à coder, nous devons importer les espaces de noms nécessaires. Voici l'extrait de code pour cela :

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ces espaces de noms sont essentiels car ils donnent accès à des classes telles que `Document`, `Page`, `Image`, et `HtmlFragment`, que nous utiliserons pour créer et manipuler le PDF.

Maintenant que nous avons posé le décor, voyons comment placer du texte autour d'une image dans votre fichier PDF avec Aspose.PDF pour .NET. Nous vous guiderons pas à pas.

## Étape 1 : instancier l'objet document

Tout d'abord, vous devez créer un document PDF. Dans Aspose.PDF, cela se fait en instanciant un `Document` objet. Cet objet servira de base à tout le contenu que nous ajouterons.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Ici, nous avons créé un document PDF vide. Il ne contient pas encore de pages, mais ne vous inquiétez pas, nous en ajouterons une à l'étape suivante.

## Étape 2 : ajouter une page au document

Maintenant que nous avons notre document, il est temps d'ajouter une page. Imaginez que vous créez une feuille blanche sur laquelle vous ajouterez votre contenu.

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

Ce code ajoute une nouvelle page au document. Par défaut, la page est vierge, mais nous allons modifier cela.

## Étape 3 : Créer un tableau pour organiser le contenu

Pour aligner correctement l'image et le texte, nous utiliserons un tableau. Les tableaux dans les PDF peuvent aider à structurer votre mise en page, tout comme dans les documents Word ou HTML.

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
page.Paragraphs.Add(table1);
```

Cet extrait crée un tableau et l'ajoute à la page. Considérez le tableau comme le cadre permettant d'aligner votre image et votre texte.

## Étape 4 : Définir la largeur des colonnes du tableau

Maintenant que nous avons ajouté un tableau, nous devons définir la largeur des colonnes. Cela garantit que l'image et le texte sont correctement dimensionnés sur la page.

```csharp
table1.ColumnWidths = "120 270";
```

Cette ligne définit la largeur de deux colonnes : une pour l'image et une pour le texte. Ajustez ces valeurs si votre image ou votre texte nécessite plus ou moins d'espace.

## Étape 5 : Définir les marges et le remplissage

Pour nous assurer que tout semble bien rangé, ajoutons des marges et du remplissage au tableau.

```csharp
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;
table1.DefaultCellPadding = margin;
```

Ces paramètres garantissent que votre tableau dispose d'un espacement cohérent, ce qui rend le contenu visuellement attrayant.

## Étape 6 : Insérer une image dans le tableau

Passons maintenant à la partie amusante : ajouter une image. Dans ce cas, nous ajouterons le logo Aspose, mais n'hésitez pas à utiliser l'image de votre choix.

```csharp
Aspose.Pdf.Row row1 = table1.Rows.Add();
Aspose.Pdf.Image logo = new Aspose.Pdf.Image();
logo.File = dataDir + "aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;
row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```

Voici ce qui se passe :
- Nous chargeons l'image à partir de votre répertoire spécifié.
- Nous définissons la hauteur et la largeur de l'image.
- Enfin, nous ajoutons l’image à la première cellule du tableau.

## Étape 7 : Ajouter du texte à côté de l’image

Maintenant que l'image est en place, ajoutons du texte à côté. Dans cet exemple, nous utiliserons du texte au format HTML pour styliser le contenu.

```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component that enables .NET applications to <b>create PDF documents from scratch</b> without utilizing Adobe Acrobat.</font>";

Aspose.Pdf.HtmlFragment TitleText = new Aspose.Pdf.HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);
```

Ce bloc ajoute un titre et une description stylisés dans la cellule à côté de l'image. Vous pouvez formater le texte à l'aide de balises HTML pour une personnalisation plus poussée.

## Étape 8 : Ajuster l’alignement vertical

Par défaut, le contenu des cellules d'un tableau peut ne pas être aligné comme souhaité. Dans ce cas, nous souhaitons nous assurer que le texte est aligné en haut de la cellule.

```csharp
row1.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
```

Cela garantit que le texte se trouve en haut de la cellule, gardant ainsi la mise en page propre et professionnelle.

## Étape 9 : Ajoutez plus de texte sous l’image et la description

Vous pourriez vouloir ajouter du contenu sous l'image et le texte. Ajoutons une ligne supplémentaire au tableau à cet effet.

```csharp
Aspose.Pdf.Row SecondRow = table1.Rows.Add();
SecondRow.Cells.Add();
SecondRow.Cells[0].ColSpan = 2;
SecondRow.Cells[0].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;

string SecondRowString = "<font face=\"Arial\" size=2>Aspose.Pdf for .NET supports the creation of PDF files through API and XML or XSL-FO templates.</font>";
Aspose.Pdf.HtmlFragment SecondRowText = new Aspose.Pdf.HtmlFragment(SecondRowString);
SecondRow.Cells[0].Paragraphs.Add(SecondRowText);
```

Ici, nous avons ajouté une autre ligne avec du texte supplémentaire, couvrant les deux colonnes pour maintenir l'équilibre dans la mise en page.

## Étape 10 : Enregistrer le document PDF

Enfin, nous devons enregistrer le document afin que vous puissiez visualiser les modifications.

```csharp
doc.Save(dataDir + "PlacingTextAroundImage_out.pdf");
```

Cela enregistre le PDF avec l'image et le texte formatés exactement comme nous le souhaitons.

## Conclusion

Placer du texte autour des images dans un PDF peut sembler complexe, mais Aspose.PDF pour .NET simplifie le processus. En exploitant les tableaux, les images et le texte stylisé, vous pouvez créer des PDF de qualité professionnelle en un minimum d'effort. En quelques lignes de code, vous pouvez positionner le contenu exactement où vous le souhaitez, donnant à vos documents un aspect soigné et bien organisé.

## FAQ

### Puis-je utiliser cette méthode pour placer plusieurs images avec du texte ?
Oui, ajoutez simplement plus de lignes et de cellules à votre tableau pour inclure des images et du texte supplémentaires.

### Puis-je modifier l'alignement de l'image ?
Absolument ! Vous pouvez modifier l'alignement de l'image en ajustant les propriétés d'alignement de la cellule.

### Comment puis-je styliser davantage le texte ?
Vous pouvez utiliser des balises HTML dans le `HtmlFragment` objet permettant d'appliquer différents styles comme le gras, l'italique ou des polices différentes.

### Puis-je contrôler l’espacement entre le texte et l’image ?
Oui, en utilisant le `MarginInfo` L'objet vous permet de contrôler le remplissage et les marges entre les éléments.

### Est-il possible d'ajouter des liens au texte ?
Absolument ! Vous pouvez intégrer des hyperliens dans le texte au format HTML en utilisant l' `<a>` étiqueter.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}