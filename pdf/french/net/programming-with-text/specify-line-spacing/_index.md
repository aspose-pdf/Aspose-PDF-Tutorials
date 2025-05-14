---
"description": "Apprenez à définir l'interligne dans un PDF avec Aspose.PDF pour .NET grâce à ce guide étape par étape. Idéal pour les développeurs recherchant une mise en forme de texte précise."
"linktitle": "Spécifier l'espacement des lignes dans le fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Spécifier l'espacement des lignes dans le fichier PDF"
"url": "/fr/net/programming-with-text/specify-line-spacing/"
"weight": 510
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Spécifier l'espacement des lignes dans le fichier PDF

## Introduction

Avez-vous déjà eu du mal à contrôler l'interligne dans un fichier PDF ? Peut-être avez-vous eu du texte trop chargé ou pas aussi soigné que vous le souhaitiez. Dans ce tutoriel, nous allons vous montrer comment définir facilement l'interligne dans un PDF avec Aspose.PDF pour .NET. Nous utiliserons un guide simple et étape par étape pour vous accompagner d'un PDF vierge à un PDF avec interligne personnalisé. C'est idéal si vous avez besoin de précision dans la mise en page de votre texte pour des documents tels que des rapports, des factures ou des certificats.

## Prérequis

Avant de passer au code, assurons-nous que vous avez tout ce dont vous avez besoin :

1. Aspose.PDF pour .NET est installé. Si vous ne l'avez pas, téléchargez-le depuis le [Page de téléchargement d'Aspose.PDF](https://releases.aspose.com/pdf/net/).
2. Un environnement de développement .NET (comme Visual Studio).
3. Un fichier de police TrueType (`.ttf`) que nous utiliserons dans l'exemple. Vous pouvez utiliser n'importe quelle police, mais pour ce guide, nous utiliserons la police `HPSimplified.TTF` fonte.
4. Connaissances de base en C# et manipulation PDF.

Si vous êtes prêt, passons à l’importation des packages nécessaires.

## Importer des packages

Dans votre projet C#, vous devrez importer les espaces de noms Aspose.PDF pour utiliser les fonctionnalités PDF. Voici comment procéder :

```csharp
using Aspose.Pdf.Text;
using System.IO;
```

Ces espaces de noms vous permettent de créer et de manipuler des documents PDF, ainsi que de travailler avec des options de formatage de texte et de police.

Nous allons décomposer ce processus en étapes simples pour que vous puissiez le suivre facilement. Chaque étape se concentrera sur une étape clé du processus, de la configuration de votre PDF à la définition de l'interligne.

## Étape 1 : Configurez votre projet et définissez le répertoire des documents

La première chose à faire est de définir l'emplacement de nos fichiers. Cela permet au programme de savoir où trouver la police et où enregistrer le PDF obtenu.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string fontFile = dataDir + "HPSimplified.TTF";
```

Dans cette étape, vous remplacerez `"YOUR DOCUMENT DIRECTORY"` avec le chemin d'accès réel vers lequel vous stockez vos fichiers. C'est là que vous placerez votre fichier de police (`HPSimplified.TTF`) et où le PDF sera enregistré.

## Étape 2 : Charger un document PDF

Nous devons maintenant créer un nouveau document PDF. Pour ce guide, nous partirons d'un document vierge, mais vous pouvez également charger un PDF existant si nécessaire.

```csharp
Document doc = new Document();
```

Cela crée un nouveau document PDF vide. Facile, non ?

## Étape 3 : Définir les options de formatage du texte

C'est là que la magie opère. Nous allons spécifier l'interligne du texte à ajouter au PDF. Aspose.PDF propose plusieurs options, mais dans ce guide, nous utiliserons `LineSpacingMode.FullSize`, ce qui garantit que l'interligne est entièrement respecté.

```csharp
TextFormattingOptions formattingOptions = new TextFormattingOptions();
formattingOptions.LineSpacing = TextFormattingOptions.LineSpacingMode.FullSize;
```

Ce code définit le mode d'espacement des lignes sur `FullSize`garantissant que le texte sera affiché avec un espacement approprié. Il existe d'autres options, comme `Proportional` si vous voulez des comportements d'espacement différents, mais pour l'instant, restons-en à `FullSize`.

## Étape 4 : Créer un fragment de texte

Nous allons maintenant créer le texte qui sera inséré dans le PDF. Ce texte respectera l'interligne défini.

```csharp
TextFragment textFragment = new TextFragment("Hello world");
```

Nous avons créé un fragment de texte avec la chaîne `"Hello world"`Vous pouvez bien sûr personnaliser ce texte comme vous le souhaitez.

## Étape 5 : Charger et appliquer une police personnalisée

Pour mettre en valeur le texte, nous allons charger une police TrueType personnalisée à partir d'un fichier. Cette étape est facultative, mais elle peut apporter une touche professionnelle à vos PDF.

```csharp
if (fontFile != "")
{
    using (FileStream fontStream = System.IO.File.OpenRead(fontFile))
    {
        textFragment.TextState.Font = FontRepository.OpenFont(fontStream, FontTypes.TTF);
```

Ici, nous chargeons le fichier de police et l'appliquons au fragment de texte. Si le chemin d'accès est valide, la police est utilisée. Sinon, la police par défaut est appliquée.

## Étape 6 : Définir la position et le formatage du texte

Ensuite, nous devons positionner le texte sur le PDF. Nous appliquerons également les options de mise en forme créées précédemment.

```csharp
textFragment.Position = new Position(100, 600);
textFragment.TextState.FormattingOptions = formattingOptions;
```

Le `Position` La méthode définit les coordonnées où le texte apparaîtra sur la page (ici, 100 unités à partir de la gauche et 600 unités à partir du bas). Les options de formatage, y compris l'interligne, sont appliquées ici.

## Étape 7 : ajouter du texte à la page PDF

Maintenant que notre texte est formaté et positionné, il est temps de l'ajouter au document PDF.

```csharp
var page = doc.Pages.Add();
page.Paragraphs.Add(textFragment);
```

Ce code crée une nouvelle page dans le document PDF et y ajoute le fragment de texte.

## Étape 8 : Enregistrer le PDF

Nous sommes arrivés à l'étape finale ! Maintenant que tout est configuré, enregistrons le PDF.

```csharp
dataDir = dataDir + "SpecifyLineSpacing_out.pdf";
doc.Save(dataDir);
```

Cela enregistre le PDF avec l’espacement de ligne spécifié et votre fichier est prêt !

## Conclusion

Et voilà ! Vous venez de créer un document PDF avec interligne personnalisé avec Aspose.PDF pour .NET. Cet outil puissant vous permet de contrôler tous les aspects de vos fichiers PDF, et ce n'est qu'un exemple de ce que vous pouvez réaliser. Du placement du texte à la mise en forme, les possibilités sont infinies.

Si vous souhaitez approfondir la manipulation des PDF, Aspose.PDF offre une multitude de fonctionnalités à explorer. N'hésitez pas à expérimenter et à repousser les limites de vos possibilités avec vos documents !

## FAQ

### Puis-je ajuster l'espacement des lignes à d'autres modes ?  
Oui, vous pouvez utiliser d'autres modes comme `Propoutional` or `Fixed` selon vos besoins.

### Est-il possible de charger des polices depuis le système au lieu d'un fichier ?  
Oui, vous pouvez charger les polices installées par le système à l'aide de l' `FontRepository`.

### Puis-je utiliser Aspose.PDF pour .NET avec d'autres formats de fichiers ?  
Absolument ! Aspose.PDF pour .NET prend en charge divers formats tels que XML, HTML, etc.

### Ai-je besoin d’une licence pour utiliser Aspose.PDF pour .NET ?  
Oui, pour bénéficier de toutes les fonctionnalités, vous aurez besoin d'une licence, que vous pouvez obtenir [ici](https://purchase.aspose.com/buy).

### Comment définir l'interligne pour plusieurs paragraphes ?  
Vous pouvez postuler `TextFormattingOptions` à chacun `TextFragment` ou `TextParagraph` pour contrôler l'espacement de plusieurs lignes ou paragraphes.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}