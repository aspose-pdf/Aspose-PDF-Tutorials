---
"description": "Apprenez à ajouter des infobulles au texte de vos fichiers PDF avec Aspose.PDF pour .NET. Améliorez vos PDF avec des textes informatifs au survol, sans effort."
"linktitle": "Ajouter une info-bulle au texte d'un fichier PDF"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Ajouter une info-bulle au texte d'un fichier PDF"
"url": "/fr/net/programming-with-text/add-tooltip-to-text/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter une info-bulle au texte d'un fichier PDF

## Introduction

Pour créer des PDF attrayants et interactifs, les infobulles peuvent s'avérer précieuses. Vous connaissez ces petites fenêtres contextuelles qui affichent des informations supplémentaires au survol ? Elles peuvent fournir du contexte, des descriptions, voire des conseils, sans encombrer votre document. Dans ce tutoriel, nous vous expliquerons comment ajouter des infobulles au texte d'un fichier PDF à l'aide de la bibliothèque Aspose.PDF pour .NET. Que vous soyez un développeur expérimenté ou que vous débutiez dans le monde des PDF, vous êtes au bon endroit ! Alors, c'est parti !

## Prérequis

Avant de passer à la partie codage, assurons-nous que vous disposez de tout ce dont vous avez besoin pour suivre en douceur.

### Visual Studio installé
Il est essentiel que Visual Studio soit installé sur votre machine, car il constituera votre environnement de développement principal pour les applications .NET.

### Bibliothèque Aspose.PDF pour .NET
Vous aurez également besoin de la bibliothèque Aspose.PDF. Vous pouvez [téléchargez-le ici](https://releases.aspose.com/pdf/net/)Assurez-vous de l'inclure dans vos références de projet.

### Connaissances de base de C#
Une connaissance de C# sera très utile, car nous coderons dans ce langage. Mais pas d'inquiétude, je vous guiderai pas à pas !

### Un document PDF avec lequel travailler
Vous pouvez commencer avec un document PDF vierge, comme nous le faisons dans cet exemple, ou utiliser un document existant si vous préférez.

Passons maintenant à la partie codage !

## Importer des packages 

La première étape de notre aventure de codage consiste à importer les packages nécessaires. Ouvrez votre projet Visual Studio et ajoutez ce qui suit en haut de votre fichier C#. `using` directives:

```csharp
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
```

Ces packages vous donnent accès à toutes les classes et fonctionnalités dont vous avez besoin pour créer et manipuler des documents PDF.

## Étape 1 : Configurez votre répertoire de documents

Tout d'abord, nous devons définir le chemin d'accès où vous enregistrerez vos documents. Imaginez que vous cherchiez un emplacement pratique dans votre système de fichiers pour y stocker toutes vos créations.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outputFile = dataDir + "Tooltip_out.pdf";
```

Assurez-vous de remplacer `YOUR DOCUMENT DIRECTORY` avec le chemin réel sur votre machine.

## Étape 2 : Créer un exemple de document PDF

Ensuite, il est temps de créer un PDF simple avec du texte. C'est ici que commence notre processus créatif !

```csharp
// Créer un exemple de document avec du texte
Document doc = new Document();
doc.Pages.Add().Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a tooltip"));
doc.Pages[1].Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a very long tooltip"));
doc.Save(outputFile);
```

Dans cette étape, nous créons un document, ajoutons deux fragments de texte et l’enregistrons dans notre chemin précédemment spécifié.

## Étape 3 : Ouvrir le document pour traitement

Maintenant que notre document est créé, ouvrons-le pour pouvoir travailler sur ces info-bulles !

```csharp
// Ouvrir un document avec du texte
Document document = new Document(outputFile);
```

Ici, nous chargeons simplement le document que nous venons de créer.

## Étape 4 : Créer un absorbeur de texte pour rechercher des fragments de texte

Nous devons trouver les fragments de texte où nous souhaitons ajouter les infobulles. C'est comme utiliser une loupe pour mettre en évidence une partie spécifique d'une grande carte ! 

```csharp
// Créez un objet TextAbsorber pour trouver toutes les phrases correspondant à l'expression régulière
TextFragmentAbsorber absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a tooltip");
document.Pages.Accept(absorber);
```

## Étape 5 : Extraire des fragments de texte

Ensuite, nous extrayons les fragments de texte que nous avons trouvés lors de notre étape précédente.

```csharp
// Obtenir les fragments de texte extraits
TextFragmentCollection textFragments = absorber.TextFragments;
```

Cet extrait nous permet de conserver les références des fragments de texte qui nous intéressent.

## Étape 6 : Parcourez les fragments et ajoutez des info-bulles

Et maintenant, place au fun ! Nous allons parcourir chaque fragment de texte et ajouter une infobulle à chacun. Imaginez que vous enveloppiez des petits cadeaux (infobulles) autour d'éléments spécifiques (fragments de texte).

```csharp
// Boucle à travers les fragments
foreach (TextFragment fragment in textFragments)
{
	// Créer un bouton invisible sur la position du fragment de texte
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// La valeur AlternateName sera affichée sous forme d'info-bulle par une application de visualisation
	field.AlternateName = "Tooltip for text.";
	// Ajouter un champ de bouton au document
	document.Form.Add(field);
}
```

À chaque itération, nous créons un champ de bouton qui correspond à la position du fragment de texte et lui attribuons le texte de l'info-bulle.

## Étape 7 : Répétez l'opération pour les infobulles longues

Tout comme nous avons ajouté une simple info-bulle, nous pouvons faire de même pour un texte plus long. Laissons libre cours à notre créativité !

```csharp
// Ensuite, nous verrons un exemple d'info-bulle très longue
absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a very long tooltip");
document.Pages.Accept(absorber);
textFragments = absorber.TextFragments;
foreach (TextFragment fragment in textFragments)
{
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// Définir un texte très long
	field.AlternateName = "Lorem ipsum dolor sit amet, consectetur adipiscing elit," +
							" sed do eiusmod tempor incididunt ut labore et dolore magna" +
							" aliqua. Ut enim ad minim veniam, quis nostrud exercitation" +
							" ullamco laboris nisi ut aliquip ex ea commodo consequat." +
							" Duis aute irure dolor in reprehenderit in voluptate velit" +
							" esse cillum dolore eu fugiat nulla pariatur. Excepteur sint" +
							" occaecat cupidatat non proident, sunt in culpa qui officia" +
							" deserunt mollit anim id est laborum.";
	document.Form.Add(field);
}
```

Ici, nous faisons le même genre de travail que précédemment, mais avec une info-bulle beaucoup plus étendue.

## Étape 8 : Enregistrez votre document

La dernière étape consiste à enregistrer votre document avec toutes ces nouvelles info-bulles brillantes. 

```csharp
// Enregistrer le document
document.Save(outputFile);
```

Et voilà, c'est fait ! Vous avez ajouté des infobulles à votre PDF, le rendant plus convivial et interactif.

## Conclusion

Et voilà, un guide facile à suivre pour ajouter des infobulles au texte de vos fichiers PDF avec Aspose.PDF pour .NET. Cette technique peut considérablement améliorer l'expérience utilisateur, rendant vos documents plus informatifs sans submerger le lecteur sous un texte trop long d'un coup. 

En survolant simplement un mot ou une expression, le lecteur obtient des informations pertinentes et enrichissantes, sans encombrement. Alors, retroussez vos manches et essayez ! En un rien de temps, vous pourriez créer toutes sortes de documents attrayants et remarquables.

## FAQ

### Qu'est-ce qu'Aspose.PDF pour .NET ?
Aspose.PDF pour .NET est une bibliothèque qui permet aux développeurs de créer, manipuler et convertir des documents PDF dans des applications .NET.

### Puis-je utiliser Aspose.PDF gratuitement ?
Oui, Aspose propose un essai gratuit pour explorer ses fonctionnalités ! Vous pouvez le trouver. [ici](https://releases.aspose.com/).

### Existe-t-il des options de licence disponibles pour Aspose.PDF ?
Oui, vous pouvez acheter une licence ou obtenir une licence temporaire. Découvrez les options. [ici](https://purchase.aspose.com/).

### Puis-je ajouter des éléments interactifs autres que des info-bulles à l'aide d'Aspose.PDF ?
Absolument ! Aspose.PDF permet d'ajouter divers éléments interactifs comme des hyperliens, des boutons et des formulaires.

### Où puis-je trouver plus de documentation sur Aspose.PDF ?
Vous pouvez consulter la documentation [ici](https://reference.aspose.com/pdf/net/) pour des conseils plus approfondis.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}