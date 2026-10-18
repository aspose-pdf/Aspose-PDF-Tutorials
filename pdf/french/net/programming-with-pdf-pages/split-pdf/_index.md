---
title: Diviser un PDF après la dixième page avec Aspose.Pdf for .NET
weight: 360
limit:
description: Code étape par étape pour diviser un document PDF immédiatement après la dixième page avec Aspose.Pdf for .NET.
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Code étape par étape pour diviser un document PDF immédiatement après
    la dixième page avec Aspose.Pdf for .NET.
  headline: Diviser un PDF après la dixième page avec Aspose.Pdf for .NET
  type: TechArticle
- description: Code étape par étape pour diviser un document PDF immédiatement après
    la dixième page avec Aspose.Pdf for .NET.
  name: Diviser un PDF après la dixième page avec Aspose.Pdf for .NET
  steps:
  - name: Les commentaires d’en-tête expliquent le but de l’exemple, indiquent que
      le code complet a été déplacé et fournissent un lien vers la source à jour.
    text: Les commentaires d’en-tête expliquent le but de l’exemple, indiquent que
      le code complet a été déplacé et fournissent un lien vers la source à jour.
  - name: La ligne factice n’effectue aucune action et n’existe que pour maintenir
      l’URL d’origine fonctionnelle.
    text: La ligne factice n’effectue aucune action et n’existe que pour maintenir
      l’URL d’origine fonctionnelle.
  type: HowTo
- questions:
  - answer: Aspose.Pdf ne lèvera pas d’erreur ; la méthode `Split` renverra simplement
      le document original inchangé car il n’y a aucune page après la dixième pour
      commencer une nouvelle partie.
    question: Que se passe-t-il si le PDF source comporte moins de dix pages ?
  - answer: Vous appelez `PdfDocument.Split(pageNumber)` sur une instance de `PdfDocument`,
      en passant `10` comme `pageNumber` pour créer deux documents séparés.
    question: Quelle classe et quelle méthode sont utilisées pour diviser le PDF à
      la page dix ?
  - answer: Oui, Aspose.Pdf conserve tous les objets au niveau de la page (signets,
      annotations, champs de formulaire, etc.) dans les documents découpés, les maintenant
      attachés aux pages dont ils proviennent.
    question: Les signets, annotations et champs de formulaire restent‑ils sur leurs
      pages d’origine après la division ?
  - answer: Après avoir appelé `Split`, vous obtenez deux objets `PdfDocument`; vous
      devez appeler `Save("FirstPart.pdf")` sur le premier et `Save("SecondPart.pdf")`
      sur le second, en fournissant vous‑même des noms de fichiers distincts.
    question: Comment devrais‑je nommer les fichiers de sortie pour les deux parties
      créées par la division ?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: Diviser le PDF après la page 10
og_description: Tutoriel rapide pour diviser un PDF à la page 10 en utilisant Aspose.Pdf for .NET.
og_image_alt: Guide montrant comment diviser un PDF après la dixième page en utilisant Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diviser un PDF après la dixième page avec Aspose.Pdf
Diviser un PDF en documents séparés peut simplifier la distribution et le traitement. Ce tutoriel vous guide dans l’utilisation d’Aspose.Pdf for .NET pour diviser un PDF immédiatement après la dixième page, créant ainsi deux fichiers distincts. Suivez le code étape par étape pour extraire les dix premières pages et les pages restantes avec seulement quelques lignes de C#.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/split-pdf" >}}


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

**Q: Que se passe-t-il si le PDF source comporte moins de dix pages ?**  
A: Aspose.Pdf ne lèvera pas d’erreur ; la méthode `Split` renverra simplement le document original inchangé car il n’y a aucune page après la dixième pour commencer une nouvelle partie.

**Q: Quelle classe et quelle méthode sont utilisées pour diviser le PDF à la page dix ?**  
A: Vous appelez `PdfDocument.Split(pageNumber)` sur une instance de `PdfDocument`, en passant `10` comme `pageNumber` pour créer deux documents séparés.

**Q: Les signets, annotations et champs de formulaire restent‑ils sur leurs pages d’origine après la division ?**  
A: Oui, Aspose.Pdf conserve tous les objets au niveau de la page (signets, annotations, champs de formulaire, etc.) dans les documents découpés, les maintenant attachés aux pages dont ils proviennent.

**Q: Comment devrais‑je nommer les fichiers de sortie pour les deux parties créées par la division ?**  
A: Après avoir appelé `Split`, vous obtenez deux objets `PdfDocument`; vous devez appeler `Save("FirstPart.pdf")` sur le premier et `Save("SecondPart.pdf")` sur le second, en fournissant vous‑même des noms de fichiers distincts.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}