---
title: Comparer des PDF tout en ignorant des zones spécifiques avec Aspose.Pdf for .NET
weight: 201
limit:
description: Apprenez à comparer des PDF côte à côte et à ignorer des régions sélectionnées avec Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Apprenez à comparer des PDF côte à côte et à ignorer des régions sélectionnées
    avec Aspose.Pdf for .NET.
  headline: Comparer des PDF tout en ignorant des zones spécifiques avec Aspose.Pdf
    for .NET
  type: TechArticle
- description: Apprenez à comparer des PDF côte à côte et à ignorer des régions sélectionnées
    avec Aspose.Pdf for .NET.
  name: Comparer des PDF tout en ignorant des zones spécifiques avec Aspose.Pdf for
    .NET
  steps:
  - name: Définissez les chemins d’accès des deux PDF source et du PDF de différences
      en sortie.
    text: Définissez les chemins d’accès des deux PDF source et du PDF de différences
      en sortie.
  - name: Vérifiez que les deux fichiers PDF source existent et arrêtez l’exécution
      avec un message d’erreur si l’un d’eux est manquant.
    text: Vérifiez que les deux fichiers PDF source existent et arrêtez l’exécution
      avec un message d’erreur si l’un d’eux est manquant.
  - name: Créez un tableau contenant la zone rectangulaire à ignorer dans le premier
      PDF.
    text: Créez un tableau contenant la zone rectangulaire à ignorer dans le premier
      PDF.
  - name: Créez un tableau contenant la zone rectangulaire à ignorer dans le deuxième
      PDF.
    text: Créez un tableau contenant la zone rectangulaire à ignorer dans le deuxième
      PDF.
  - name: Configurez la comparaison côte à côte en assignant les tableaux de zones
      à ignorer aux propriétés appropriées.
    text: Configurez la comparaison côte à côte en assignant les tableaux de zones
      à ignorer aux propriétés appropriées.
  - name: Chargez les deux PDF et lancez la comparaison côte à côte, en générant le
      fichier de différences au chemin spécifié.
    text: Chargez les deux PDF et lancez la comparaison côte à côte, en générant le
      fichier de différences au chemin spécifié.
  - name: Affichez un message de confirmation indiquant que la comparaison est terminée
      et où le PDF de différences a été enregistré.
    text: Affichez un message de confirmation indiquant que la comparaison est terminée
      et où le PDF de différences a été enregistré.
  type: HowTo
- questions:
  - answer: Les coordonnées sont exprimées en points (1/72 pouce) avec l’origine au
      coin inférieur gauche de la page, ainsi les deux premiers nombres représentent
      les X/Y du coin inférieur gauche et les deux derniers les X/Y du coin supérieur
      droit.
    question: Quel système de coordonnées les valeurs de `Rectangle` utilisent‑elles
      lors de la définition des zones à ignorer ?
  - answer: Oui – fournissez plusieurs objets `Aspose.Pdf.Rectangle` dans le tableau
      `ExcludeAreas1` (ou `ExcludeAreas2`) ; chaque rectangle sera exclu indépendamment
      lors de la comparaison.
    question: Puis‑je ignorer plusieurs zones rectangulaires dans le même document ?
  - answer: Non. `ExcludeAreas1` s’applique au premier PDF et `ExcludeAreas2` au second,
      vous pouvez donc spécifier des coordonnées différentes pour chaque document.
    question: Les rectangles à ignorer doivent-ils être identiques dans les deux PDF ?
  - answer: Aspose.Pdf ignore silencieusement les rectangles qui se trouvent entièrement
      en dehors de la page ; ils n’ont aucun effet sur le résultat de la comparaison.
    question: Que se passe‑t‑il si un rectangle est défini en dehors des limites de
      la page ?
  - answer: Les tableaux `ExcludeAreas` s’appliquent par page, il faut donc ajouter
      le même `Rectangle` à la collection de chaque page (par ex., parcourir `pdf.Pages`
      et assigner le tableau) avant d’appeler `SideBySidePdfComparer.Compare`.
    question: Comment puis‑je exclure la même région sur chaque page d’un PDF ?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Ignorer des régions lors de la comparaison de PDF
og_description: Découvrez comment ignorer des zones sélectionnées dans une comparaison PDF côte à côte et obtenir un PDF de différences propre.
og_image_alt: Guide montrant la comparaison PDF côte à côte avec des régions rectangulaires exclues en utilisant Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Comparer des PDF tout en ignorant des zones spécifiques avec Aspose.Pdf
Ce tutoriel montre comment comparer deux documents PDF côte à côte avec Aspose.Pdf for .NET tout en excluant des régions rectangulaires désignées de l’analyse. En définissant des zones d’exclusion dans chaque fichier, le PDF de différences généré met en évidence uniquement les changements qui comptent, facilitant ainsi la concentration sur les différences pertinentes.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Quel système de coordonnées les valeurs de `Rectangle` utilisent‑elles lors de la définition des zones à ignorer ?**  
A: Les coordonnées sont exprimées en points (1/72 pouce) avec l’origine au coin inférieur gauche de la page, ainsi les deux premiers nombres représentent les X/Y du coin inférieur gauche et les deux derniers les X/Y du coin supérieur droit.

**Q: Puis‑je ignorer plusieurs zones rectangulaires dans le même document ?**  
A: Oui – fournissez plusieurs objets `Aspose.Pdf.Rectangle` dans le tableau `ExcludeAreas1` (ou `ExcludeAreas2`) ; chaque rectangle sera exclu indépendamment lors de la comparaison.

**Q: Les rectangles à ignorer doivent-ils être identiques dans les deux PDF ?**  
A: Non. `ExcludeAreas1` s’applique au premier PDF et `ExcludeAreas2` au second, vous pouvez donc spécifier des coordonnées différentes pour chaque document.

**Q: Que se passe‑t‑il si un rectangle est défini en dehors des limites de la page ?**  
A: Aspose.Pdf ignore silencieusement les rectangles qui se trouvent entièrement en dehors de la page ; ils n’ont aucun effet sur le résultat de la comparaison.

**Q: Comment puis‑je exclure la même région sur chaque page d’un PDF ?**  
A: Les tableaux `ExcludeAreas` s’appliquent par page, il faut donc ajouter le même `Rectangle` à la collection de chaque page (par ex., parcourir `pdf.Pages` et assigner le tableau) avant d’appeler `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}