---
title: Faire pivoter une seule page PDF de 180 degrés avec Aspose.PDF for .NET
weight: 260
limit:
description: Apprenez à faire pivoter la troisième page d'un PDF de 180° en utilisant Aspose.PDF for .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Apprenez à faire pivoter la troisième page d'un PDF de 180° en utilisant
    Aspose.PDF for .NET.
  headline: Faire pivoter une seule page PDF de 180 degrés avec Aspose.PDF for .NET
  type: TechArticle
- description: Apprenez à faire pivoter la troisième page d'un PDF de 180° en utilisant
    Aspose.PDF for .NET.
  name: Faire pivoter une seule page PDF de 180 degrés avec Aspose.PDF for .NET
  steps:
  - name: Le fichier ne contient que des commentaires explicatifs et aucun code exécutable,
      servant de substitut à l'exemple original.
    text: Le fichier ne contient que des commentaires explicatifs et aucun code exécutable,
      servant de substitut à l'exemple original.
  type: HowTo
- questions:
  - answer: Utilisez la collection de pages du SDK avec un indexage à base zéro, par
      ex. `pdfDocument.Pages[2]`, car l'index 2 correspond à la troisième page.
    question: Comment cibler la troisième page du PDF pour la rotation ?
  - answer: La propriété de rotation n'accepte que les quatre valeurs standard 0,
      90, 180 et 270 degrés ; toute autre valeur est arrondie à l'angle autorisé le
      plus proche.
    question: Puis-je faire pivoter une page d'un angle différent de 180 degrés ?
  - answer: La rotation n'est appliquée qu'au `PdfDocument` en mémoire ; vous devez
      appeler `pdfDocument.Save(\"output.pdf\")` (ou une méthode d'enregistrement
      similaire) pour écrire les modifications dans un nouveau fichier, en laissant
      la source inchangée.
    question: La rotation de la page modifie-t-elle automatiquement le fichier original ?
  - answer: Le SDK recalcule automatiquement les positions des annotations et des
      champs de formulaire afin qu'ils restent correctement alignés avec la nouvelle
      orientation.
    question: Que se passe-t-il avec les annotations ou les champs de formulaire après
      la rotation de la page ?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Faire pivoter une page PDF de 180° avec Aspose.PDF
og_description: Retournez rapidement la troisième page de votre PDF à l'envers avec quelques lignes de code Aspose.PDF for .NET.
og_image_alt: Guide montrant le code qui fait pivoter la troisième page d'un PDF de 180 degrés en utilisant Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Faire pivoter une seule page PDF de 180 degrés avec Aspose.PDF
Dans ce tutoriel, vous apprendrez comment faire pivoter la troisième page d'un document PDF de 180 degrés en utilisant Aspose.PDF for .NET. L'exemple montre comment charger un PDF, sélectionner la page 3, appliquer la rotation et enregistrer le fichier mis à jour. Cette approche vous permet de retourner une page spécifique sans modifier l'orientation des autres pages.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: Comment cibler la troisième page du PDF pour la rotation ?**  
A: Utilisez la collection de pages du SDK avec un indexage à base zéro, par ex. `pdfDocument.Pages[2]`, car l'index 2 correspond à la troisième page.

**Q: Puis-je faire pivoter une page d'un angle différent de 180 degrés ?**  
A: La propriété de rotation n'accepte que les quatre valeurs standard 0, 90, 180 et 270 degrés ; toute autre valeur est arrondie à l'angle autorisé le plus proche.

**Q: La rotation de la page modifie-t-elle automatiquement le fichier original ?**  
A: La rotation n'est appliquée qu'au `PdfDocument` en mémoire ; vous devez appeler `pdfDocument.Save(\"output.pdf\")` (ou une méthode d'enregistrement similaire) pour écrire les modifications dans un nouveau fichier, en laissant la source inchangée.

**Q: Que se passe-t-il avec les annotations ou les champs de formulaire après la rotation de la page ?**  
A: Le SDK recalcule automatiquement les positions des annotations et des champs de formulaire afin qu'ils restent correctement alignés avec la nouvelle orientation.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}