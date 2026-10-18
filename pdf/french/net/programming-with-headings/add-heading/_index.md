---
title: Ajouter un en-tête, une langue et un titre à un PDF avec Aspose.PDF for .NET
weight: 110
limit:
description: Créez un PDF, définissez sa langue et son titre, et ajoutez un en-tête de niveau 1 avec Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Créez un PDF, définissez sa langue et son titre, et ajoutez un en-tête
    de niveau 1 avec Aspose.PDF for .NET.
  headline: Ajouter un en-tête, une langue et un titre à un PDF avec Aspose.PDF for
    .NET
  type: TechArticle
- description: Créez un PDF, définissez sa langue et son titre, et ajoutez un en-tête
    de niveau 1 avec Aspose.PDF for .NET.
  name: Ajouter un en-tête, une langue et un titre à un PDF avec Aspose.PDF for .NET
  steps:
  - name: Définissez le nom du fichier de sortie pour le PDF généré.
    text: Définissez le nom du fichier de sortie pour le PDF généré.
  - name: Créez une nouvelle instance de document PDF vide (`pdfDoc`) à l'intérieur
      d'un bloc `using`.
    text: Créez une nouvelle instance de document PDF vide (`pdfDoc`) à l'intérieur
      d'un bloc `using`.
  - name: Obtenez l'interface `ITaggedContent` pour travailler avec les structures
      PDF balisées.
    text: Obtenez l'interface `ITaggedContent` pour travailler avec les structures
      PDF balisées.
  - name: Définissez la langue par défaut du document sur l'anglais (États‑Unis) et
      attribuez un métadonnée de titre.
    text: Définissez la langue par défaut du document sur l'anglais (États‑Unis) et
      attribuez un métadonnée de titre.
  - name: Récupérez l'élément racine de l'arbre de structure logique.
    text: Récupérez l'élément racine de l'arbre de structure logique.
  - name: Construisez un élément d'en-tête de niveau 1, définissez son texte affiché
      et spécifiez sa langue.
    text: Construisez un élément d'en-tête de niveau 1, définissez son texte affiché
      et spécifiez sa langue.
  - name: Ajoutez l'élément d'en-tête à la racine, ce qui fait apparaître le titre
      dans le PDF.
    text: Ajoutez l'élément d'en-tête à la racine, ce qui fait apparaître le titre
      dans le PDF.
  - name: Enregistrez le PDF dans le fichier spécifié et fermez la portée du document.
    text: Enregistrez le PDF dans le fichier spécifié et fermez la portée du document.
  - name: Affichez un message de confirmation dans la console.
    text: Affichez un message de confirmation dans la console.
  type: HowTo
- questions:
  - answer: '`SetLanguage` définit la langue par défaut pour l''ensemble de la structure
      logique du document ; tout élément qui n''a pas de langue propre héritera de
      "en-US".'
    question: Quel est l'effet de l'appel à `tagContent.SetLanguage("en-US")` sur
      le PDF ?
  - answer: Définir `header.Language` est optionnel ; le titre héritera de la langue
      par défaut du document à moins que vous n'attribuiez une valeur différente,
      comme le montre l'exemple.
    question: Do I need to set `header.Language` if I already called `SetLanguage`
      on the document?
  - answer: Utilisez `tagContent.CreateHeaderElement(2)` pour créer un en-tête de
      niveau 2 ; l'argument numérique indique le niveau d'en-tête qui sera reflété
      dans l'arbre de structure du PDF.
    question: Comment créer un en-tête de niveau 2 au lieu d'un en-tête de niveau 1 ?
  - answer: '`SetTitle` écrit la chaîne fournie dans le champ de métadonnées titre
      du document PDF, qui peut être consulté dans les lecteurs PDF et utilisé pour
      la recherche ou l''indexation.'
    question: Que fait `tagContent.SetTitle("PDF Example with Header")` ?
  - answer: L'élément d'en-tête ne sera pas ajouté à l'arbre de structure logique,
      il n'apparaîtra donc pas dans le PDF généré et ne sera pas reconnu comme un
      titre par les outils d'accessibilité.
    question: Que se passe-t-il si j'omets `rootElement.AppendChild(header)` ?
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: Insérer un en-tête et définir la langue dans un PDF
og_description: Apprenez à créer un PDF, définir sa langue et son titre, puis ajouter un en-tête de niveau 1 avec quelques lignes de code .NET.
og_image_alt: Guide montrant comment ajouter un en-tête, définir la langue et le titre dans un PDF avec Aspose.PDF for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un en-tête, une langue et un titre à un PDF avec Aspose.PDF
Ce tutoriel vous guide dans la création d'un nouveau document PDF avec Aspose.PDF for .NET, l'attribution d'une langue par défaut et d'un titre de document, ainsi que l'insertion d'un en-tête de niveau 1. Vous verrez comment travailler avec les classes Document, ITaggedContent, StructureElement et HeaderElement pour produire un PDF correctement balisé, adapté aux outils d'accessibilité.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Quel est l'effet de l'appel à `tagContent.SetLanguage("en-US")` sur le PDF ?**  
A: `SetLanguage` définit la langue par défaut pour l'ensemble de la structure logique du document ; tout élément qui n'a pas de langue propre héritera de "en-US".

**Q: Do I need to set `header.Language` if I already called `SetLanguage` on the document?**  
A: Définir `header.Language` est optionnel ; le titre héritera de la langue par défaut du document à moins que vous n'attribuiez une valeur différente, comme le montre l'exemple.

**Q: Comment créer un en-tête de niveau 2 au lieu d'un en-tête de niveau 1 ?**  
A: Utilisez `tagContent.CreateHeaderElement(2)` pour créer un en-tête de niveau 2 ; l'argument numérique indique le niveau d'en-tête qui sera reflété dans l'arbre de structure du PDF.

**Q: Que fait `tagContent.SetTitle("PDF Example with Header")` ?**  
A: `SetTitle` écrit la chaîne fournie dans le champ de métadonnées titre du document PDF, qui peut être consulté dans les lecteurs PDF et utilisé pour la recherche ou l'indexation.

**Q: Que se passe-t-il si j'omets `rootElement.AppendChild(header)` ?**  
A: L'élément d'en-tête ne sera pas ajouté à l'arbre de structure logique, il n'apparaîtra donc pas dans le PDF généré et ne sera pas reconnu comme un titre par les outils d'accessibilité.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}