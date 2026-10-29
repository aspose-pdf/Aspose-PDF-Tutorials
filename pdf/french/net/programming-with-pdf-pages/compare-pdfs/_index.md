---
title: Comparer des PDF avec des tailles de page différentes en utilisant Aspose.PDF for .NET
weight: 460
limit:
description: Apprenez à synchroniser les tailles de page et à comparer des PDF, en produisant un PDF de différences qui met en évidence les changements, avec Aspose.PDF for .NET.
keywords: [compare pdfs, different page sizes pdf, Aspose.PDF for .NET, GraphicalPdfComparer, pdf difference highlighting, pdf page size synchronization]
url: /net/programming-with-pdf-pages/compare-pdfs/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Apprenez à synchroniser les tailles de page et à comparer des PDF,
    en produisant un PDF de différences qui met en évidence les changements, avec
    Aspose.PDF for .NET.
  headline: Comparer des PDF avec des tailles de page différentes en utilisant Aspose.PDF
    for .NET
  type: TechArticle
- description: Apprenez à synchroniser les tailles de page et à comparer des PDF,
    en produisant un PDF de différences qui met en évidence les changements, avec
    Aspose.PDF for .NET.
  name: Comparer des PDF avec des tailles de page différentes en utilisant Aspose.PDF
    for .NET
  steps:
  - name: Définissez les chemins de fichiers pour les deux PDF source et le PDF résultat.
    text: Définissez les chemins de fichiers pour les deux PDF source et le PDF résultat.
  - name: Vérifiez que les deux fichiers PDF source existent et annulez l'opération
      si l'un d'eux est manquant.
    text: Vérifiez que les deux fichiers PDF source existent et annulez l'opération
      si l'un d'eux est manquant.
  - name: Commencez un bloc try pour intercepter les erreurs pendant le traitement.
    text: Commencez un bloc try pour intercepter les erreurs pendant le traitement.
  - name: Chargez les deux PDF dans des objets Document `docA` et `docB` à l'intérieur
      d'instructions using.
    text: Chargez les deux PDF dans des objets Document `docA` et `docB` à l'intérieur
      d'instructions using.
  - name: Assurez-vous que chaque PDF contient au moins une page avant de continuer.
    text: Assurez-vous que chaque PDF contient au moins une page avant de continuer.
  - name: Récupérez la première page de chaque document pour la comparaison.
    text: Récupérez la première page de chaque document pour la comparaison.
  - name: Copiez les informations MediaBox de `firstPage` vers `secondPage` afin que
      les pages partagent les mêmes dimensions.
    text: Copiez les informations MediaBox de `firstPage` vers `secondPage` afin que
      les pages partagent les mêmes dimensions.
  - name: Créez et configurez un `GraphicalPdfComparer` avec une mise en surbrillance
      rouge, une haute résolution et un seuil de différence de 1 %.
    text: Créez et configurez un `GraphicalPdfComparer` avec une mise en surbrillance
      rouge, une haute résolution et un seuil de différence de 1 %.
  - name: Exécutez la comparaison, générez un PDF de différences à `outputPdfPath`,
      écrivez un message de fin, puis fermez les blocs using et try.
    text: Exécutez la comparaison, générez un PDF de différences à `outputPdfPath`,
      écrivez un message de fin, puis fermez les blocs using et try.
  - name: Gérez l'ArgumentException qui peut survenir si l'alignement des tailles
      de page reste insuffisant.
    text: Gérez l'ArgumentException qui peut survenir si l'alignement des tailles
      de page reste insuffisant.
  - name: Capturez toute autre exception inattendue et signalez‑la.
    text: Capturez toute autre exception inattendue et signalez‑la.
  type: HowTo
- questions:
  - answer: Non, `GraphicalPdfComparer.ComparePagesToPdf` est appelé uniquement avec
      `firstPage` et `secondPage`, donc seules ces deux pages sont comparées ; pour
      les documents multi‑pages, vous devez parcourir les indices de pages et appeler
      le comparateur pour chaque paire.
    question: Le tutoriel ne synchronise que les premières pages des deux PDF – la
      comparaison fonctionnera-t-elle pour des documents comportant plusieurs pages ?
  - answer: '`Threshold` est le pourcentage minimum de différence de pixels qui doit
      être dépassé avant qu''un changement ne soit mis en évidence ; une valeur de
      1 signifie que les différences inférieures à 1 % de la page sont ignorées, tandis
      qu''une valeur de 0 marquerait tout changement de pixel.'
    question: Que fait réellement le paramètre `Threshold = 1` ?
  - answer: La copie de `PageInfo` transfère le MediaBox, le CropBox et la rotation,
      de sorte que les pages auront des dimensions et une orientation correspondantes ;
      cependant, si vous devez conserver la rotation originale du deuxième document,
      vous devez définir explicitement `secondPage.Rotation` après l'affectation.
    question: Si les deux PDF ont des rotations de page différentes, la copie de `PageInfo`
      suffira-t-elle à éviter une `ArgumentException` ?
  - answer: Oui, vous pouvez définir une `Resolution` plus élevée (par ex., `new Resolution(300)`)
      sur le `GraphicalPdfComparer ; cela permet une comparaison de pixels plus fine
      au prix d'un traitement plus lent et d'une utilisation mémoire plus importante.
    question: Puis-je augmenter la précision de détection au‑delà de la résolution
      par défaut de 200 dpi ?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/compare-pdfs/og-image.png
og_title: Synchroniser les tailles de page & comparer les PDF
og_description: Guide étape par étape pour aligner les tailles de page et mettre en évidence les différences entre les PDF.
og_image_alt: Guide montrant comment synchroniser les tailles de page et comparer deux PDF avec Aspose.PDF for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Comparer des PDF avec des tailles de page différentes en utilisant Aspose.PDF
Dans ce tutoriel, vous apprendrez comment comparer deux documents PDF dont les dimensions de page ne correspondent pas. Nous synchroniserons d'abord la taille des premières pages, puis configurerons un GraphicalPdfComparer pour détecter les changements, et enfin générerons un PDF qui met visuellement en évidence les différences. Cette approche vous permet de repérer avec précision les variations de contenu même lorsque les fichiers source n'ont pas la même taille.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/compare-pdfs" >}}


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

**Q: Le tutoriel ne synchronise que les premières pages des deux PDF – la comparaison fonctionnera-t-elle pour des documents comportant plusieurs pages ?**  
A: Non, `GraphicalPdfComparer.ComparePagesToPdf` est appelé uniquement avec `firstPage` et `secondPage`, donc seules ces deux pages sont comparées ; pour les documents multi‑pages, vous devez parcourir les indices de pages et appeler le comparateur pour chaque paire.

**Q: Que fait réellement le paramètre `Threshold = 1` ?**  
A: `Threshold` est le pourcentage minimum de différence de pixels qui doit être dépassé avant qu'un changement ne soit mis en évidence ; une valeur de 1 signifie que les différences inférieures à 1 % de la page sont ignorées, tandis qu'une valeur de 0 marquerait tout changement de pixel.

**Q: Si les deux PDF ont des rotations de page différentes, la copie de `PageInfo` suffira-t-elle à éviter une `ArgumentException` ?**  
A: La copie de `PageInfo` transfère le MediaBox, le CropBox et la rotation, de sorte que les pages auront des dimensions et une orientation correspondantes ; cependant, si vous devez conserver la rotation originale du deuxième document, vous devez définir explicitement `secondPage.Rotation` après l'affectation.

**Q: Puis-je augmenter la précision de détection au‑delà de la résolution par défaut de 200 dpi ?**  
A: Oui, vous pouvez définir une `Resolution` plus élevée (par ex., `new Resolution(300)`) sur le `GraphicalPdfComparer ; cela permet une comparaison de pixels plus fine au prix d'un traitement plus lent et d'une utilisation mémoire plus importante.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}