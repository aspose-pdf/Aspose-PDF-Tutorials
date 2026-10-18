---
category: general
date: 2026-06-21
description: Créez un champ de zone de texte PDF avec C# et apprenez comment dupliquer
  un champ de formulaire PDF ou ajouter une zone de texte à un formulaire PDF en quelques
  lignes de code.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: fr
og_description: Créez rapidement un champ de zone de texte PDF. Ce guide montre comment
  dupliquer un champ de formulaire PDF et ajouter une zone de texte à un formulaire
  PDF en utilisant une bibliothèque PDF moderne en C#.
og_title: Créer un champ de texte PDF – Tutoriel complet C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Créer un champ de zone de texte PDF – Guide étape par étape
url: /fr/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un champ de zone de texte PDF – Tutoriel complet C#

Vous avez déjà eu besoin de **créer un champ de zone de texte PDF** sans savoir quelles appels d’API utiliser ? Vous n'êtes pas seul. Que vous construisiez un portail de signature de contrats ou une simple feuille de capture de données, ajouter des zones de texte interactives à un PDF est une compétence de base pour tout développeur d’automatisation de formulaires.  

Dans ce guide, nous parcourrons un exemple pratique qui non seulement **ajoute une zone de texte à un formulaire PDF**, mais montre aussi comment **dupliquer un champ de formulaire PDF** afin que la même saisie apparaisse sur plusieurs pages. À la fin, vous disposerez d’un programme exécutable que vous pourrez intégrer à n’importe quel projet .NET.

## Ce dont vous avez besoin

- .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Core)  
- Une bibliothèque PDF moderne pour C# – l’extrait ci‑dessous utilise **PDFTron SDK**, mais les concepts s’appliquent à iText 7, PdfSharp ou d’autres bibliothèques.  
- Visual Studio 2022 (ou tout autre IDE de votre choix)  

C’est tout – aucun service supplémentaire, aucune dépendance obscure. Si vous avez déjà un PDF à enrichir, pointez simplement le code dessus.

---

## Étape 1 : Créer le projet et importer le SDK

Tout d’abord, créez une application console :

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Ajoutez le package NuGet PDFTron :

```bash
dotnet add package PDFTron.NET
```

Ouvrez maintenant `Program.cs` et importez les espaces de noms dont nous aurons besoin :

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Astuce :** Si vous utilisez une autre bibliothèque, remplacez les instructions `using` par leurs équivalents (par ex., `iText.Kernel.Pdf` pour iText 7).

## Étape 2 : Initialiser le document PDF et le formulaire

Nous commencerons avec un PDF vierge contenant deux pages – la page source pour la zone de texte originale et une page cible pour la duplication.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

L’objet `Form` est l’endroit où résident tous les champs interactifs. Si le document ne possède pas encore de formulaire, `GetForm()` en crée un pour nous.

## Étape 3 : **Créer un champ de zone de texte PDF** sur la première page

Voici le cœur de notre tutoriel – créer un champ de zone de texte. Les coordonnées du rectangle sont exprimées en points (1 pouce = 72 points). L’exemple place la boîte près du haut‑centre de la première page.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Pourquoi définissons‑nous `Value` immédiatement ? Pré‑remplir le champ donne à l’utilisateur un indice sur la saisie attendue, et cela montre également que le champ fonctionne pleinement.

## Étape 4 : Ajouter le champ au formulaire – **Ajouter une zone de texte au formulaire PDF**

Ensuite, nous enregistrons le champ auprès du formulaire en utilisant un nom logique. Ce nom est celui que vous référencerez plus tard pour lire ou modifier les données du champ par programme.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Choisir un nom clair (comme `"multiBox"`) rend le code ultérieur plus lisible, surtout lorsque vous avez des dizaines de champs.

## Étape 5 : **Dupliquer un champ de formulaire PDF** sur une autre page

Une exigence courante consiste à afficher le même champ sur plusieurs pages – pensez à une boîte « Nom du client » qui apparaît sur chaque page de facture. PDFTron nous permet de cloner l’annotation widget, qui est la représentation visuelle du champ.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Le widget cloné partage les mêmes données sous‑jacentes que la zone de texte d’origine. Lorsqu’un utilisateur saisit du texte dans une instance, l’autre se met à jour automatiquement – c’est la magie du **duplicate PDF form field**.

## Étape 6 : Enregistrer le document et nettoyer

Enfin, écrivez le PDF sur le disque et arrêtez le runtime PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

L’exécution du programme produit un PDF de deux pages (`output.pdf`). Ouvrez‑le dans Adobe Acrobat Reader, cliquez sur la zone de texte de la page 1, saisissez quelque chose, puis passez à la page 2 – le même texte apparaît instantanément. Voilà un exemple complet de **create pdf textbox field** avec un champ dupliqué.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Résultat attendu :** Un fichier nommé `output.pdf` contenant deux pages. Les deux pages affichent la même zone de texte éditable intitulée « Sample ». Modifier l’une met à jour l’autre immédiatement.

---

## Questions fréquentes & cas particuliers

### Et si j’ai besoin du champ sur *plus* de deux pages ?

Répétez simplement les étapes de clonage‑et‑ajout pour chaque page supplémentaire. L’objet de données sous‑jacent reste le même, donc tous les widgets restent synchronisés.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Comment changer l’apparence (police, bordure, arrière‑plan) ?

Chaque `Widget` possède les méthodes `SetBorderColor`, `SetBorderWidth` et `SetBackgroundColor`. Vous pouvez également assigner une chaîne d’apparence par défaut (`DA`) pour contrôler la police et la taille.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Puis‑je rendre le champ en lecture‑seule après que l’utilisateur l’ait rempli ?

Oui. Activez le drapeau `ReadOnly` sur le champ après avoir collecté les données, ou basculez‑le selon votre flux de travail.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Et les PDF qui contiennent déjà un formulaire ?

Si le document possède déjà un AcroForm, `doc.GetForm()` le renvoie simplement. Vous pouvez alors ajouter de nouveaux champs sans perturber ceux existants. Veillez simplement à choisir des noms de champ uniques.

---

## Conseils pour les projets réels

- **Convention de nommage :** Préfixez les noms de champ avec la page ou la section (par ex., `invoice_customer_name`) pour éviter les collisions.  
- **Validation :** Utilisez des actions JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) si vous avez besoin d’une validation côté client.  
- **Performance :** Lors du traitement de gros PDF, appelez `doc.Lock()` avant les opérations en masse pour réduire la surcharge d’E/S.  
- **Accessibilité :** Définissez la propriété `AlternateName` afin que les lecteurs d’écran puissent décrire le champ.

---

## Conclusion

Nous venons de **créer un champ de zone de texte PDF**, montré comment **dupliquer un champ de formulaire PDF** sur plusieurs pages, et démontré la façon la plus simple d’**ajouter une zone de texte à un formulaire PDF** en C#. Le code complet et exécutable se trouve ci‑dessus, et vous pouvez l’étendre avec du style, de la validation ou des pages supplémentaires selon vos besoins.

Prêt pour l’étape suivante ? Essayez d’intégrer une liste déroulante (`ChoiceField`) ou un widget de signature, ou explorez comment aplatir le formulaire après la saisie des données pour l’archivage. Le SDK PDFTron (ou toute bibliothèque comparable) vous fournit les blocs de construction — votre imagination décide de la forme finale.

Si vous rencontrez un problème, laissez un commentaire ci‑dessous ou consultez la documentation officielle de la bibliothèque ; elle regorge d’exemples qui complètent ce que nous avons couvert ici. Bon codage, et que vos formulaires restent toujours synchronisés !


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}