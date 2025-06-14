---
"description": "Découvrez comment définir des légendes de boutons radio dans vos PDF avec Aspose.PDF pour .NET. Ce guide étape par étape vous guide pas à pas pour charger, modifier et enregistrer vos formulaires PDF."
"linktitle": "Définir la légende du bouton radio"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Définir la légende du bouton radio"
"url": "/fr/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Définir la légende du bouton radio

## Introduction

Si vous vous lancez dans la manipulation de PDF avec Aspose.PDF pour .NET, vous allez être comblé ! Aujourd'hui, nous nous intéressons à une fonctionnalité pratique : la définition des légendes des boutons radio dans vos formulaires PDF. Les boutons radio sont essentiels pour les formulaires utilisateur nécessitant un choix parmi plusieurs options. Imaginez-les comme des questions à choix multiples avec une seule réponse autorisée. Ce tutoriel vous guidera dans la mise à jour des légendes des boutons radio dans un formulaire PDF, pour des documents à la fois interactifs et conviviaux. 

## Prérequis

Avant de plonger dans le code, vous devez vous assurer de disposer de quelques éléments :

1. Aspose.PDF pour .NET : Assurez-vous d'avoir installé la bibliothèque Aspose.PDF. Cette bibliothèque vous permettra de manipuler les fichiers PDF par programmation.
2. Environnement de développement : vous devez disposer d’un environnement de développement .NET configuré, tel que Visual Studio.
3. Exemple de formulaire PDF : Pour ce tutoriel, vous aurez besoin d'un exemple de formulaire PDF avec boutons radio. Vous pouvez utiliser n'importe quel formulaire PDF existant ou en créer un nouveau avec des boutons radio.
4. Connaissances de base de C# : ce guide suppose que vous avez une compréhension de base des concepts de programmation C# et .NET.

Si vous n'avez pas encore installé Aspose.PDF pour .NET ou si vous avez besoin d'une licence temporaire, vous pouvez [téléchargez-le ici](https://releases.aspose.com/pdf/net/) ou [obtenir un permis temporaire](https://purchase.aspose.com/temporary-license/).

## Importer des packages

Pour commencer, vous devez importer les packages nécessaires dans votre projet C#. Voici comment inclure la bibliothèque Aspose.PDF :

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

Assurez-vous d’avoir ajouté ces packages à votre projet via NuGet ou votre méthode préférée.

## Étape 1 : Charger le formulaire PDF

Tout d'abord, vous devez charger le formulaire PDF qui contient les boutons radio. `Aspose.Pdf.Facades.Form` La classe est utilisée à cet effet. Voici comment procéder :

```csharp
// Définissez le chemin d'accès à votre répertoire de documents
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Charger le formulaire PDF source
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

Dans cet extrait de code :
- `dataDir` spécifie le chemin où se trouve votre PDF.
- `Form` la classe est utilisée pour interagir avec les champs de formulaire dans le PDF.
- `Document` la classe donne accès aux pages du document PDF.

## Étape 2 : parcourir les champs des boutons radio

Ensuite, vous devrez parcourir les champs de votre formulaire pour identifier et manipuler les champs des boutons radio :

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

Dans cette boucle :
- `FieldNames` fournit une liste de tous les noms de champs dans le PDF.
- `GetButtonOptionValues(item)` récupère les options disponibles pour chaque bouton radio.

## Étape 3 : Modifier les options des boutons radio

Une fois les champs des boutons radio identifiés, vous pouvez modifier leurs options. Pour cela, vous devez convertir le champ en `RadioButtonField` et mettre à jour ses options :

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

Ici:
- Nous vérifions si le nom du champ contient « radio1 » pour identifier le champ de bouton radio spécifique que nous souhaitons modifier.
- `RadioButtonField` est lancé à partir des champs de formulaire pour apporter des modifications spécifiques.

## Étape 4 : Définir la légende du bouton radio

Pour définir ou mettre à jour la légende du bouton radio, vous devrez créer un `TextFragment` et utiliser `TextBuilder` pour le placer à l'endroit souhaité :

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // Créer un objet TextParagraph
        TextParagraph par = new TextParagraph();
        // Définir la position du paragraphe
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // Spécifier le mode de retour à la ligne
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // Ajouter un nouveau TextFragment au paragraphe
        par.AppendLine(updatedFragment);
        // Ajouter le TextParagraph à l'aide de TextBuilder
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

Dans cette partie :
- `TextFragment` est utilisé pour définir le texte et son apparence.
- `TextParagraph` aide à positionner et à formater le texte.
- `TextBuilder` ajoute le texte à la page spécifiée du PDF.

## Étape 5 : Enregistrer le PDF mis à jour

Enfin, enregistrez le PDF mis à jour dans un nouveau fichier :

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

Cela garantira que :
- Les modifications sont appliquées au PDF.
- L'option de bouton radio d'origine est supprimée comme spécifié.

## Conclusion

Modifier les légendes des boutons radio dans un formulaire PDF avec Aspose.PDF pour .NET peut grandement améliorer l'interactivité et la convivialité de vos documents. Grâce aux étapes décrites dans ce tutoriel, vous pouvez facilement charger un PDF, mettre à jour les options des boutons radio et enregistrer vos modifications. Cette approche est pratique pour la gestion des formulaires et garantit que vos PDF répondent parfaitement aux besoins de vos utilisateurs. Découvrez Aspose.PDF et ses possibilités de manipulation de PDF !

## FAQ

### Puis-je mettre à jour plusieurs champs de boutons radio à la fois ?
Oui, vous pouvez parcourir tous les champs des boutons radio et appliquer les modifications selon vos besoins.

### Ai-je besoin d'une licence pour utiliser Aspose.PDF ?
Vous pouvez commencer avec un essai gratuit, mais une licence est requise pour une utilisation prolongée. [Obtenez une licence ici](https://purchase.aspose.com/buy).

### Comment puis-je tester les modifications avant d'enregistrer le PDF ?
Vous pouvez prévisualiser le PDF dans votre environnement de développement ou utiliser une visionneuse PDF pour vérifier les modifications.

### Aspose.PDF est-il compatible avec toutes les versions de .NET ?
Aspose.PDF prend en charge différentes versions de .NET. Assurez-vous de vérifier la compatibilité avec votre version de .NET.

### Puis-je manipuler d’autres champs de formulaire de la même manière ?
Oui, des techniques similaires peuvent être appliquées à d’autres types de champs de formulaire dans les documents PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}