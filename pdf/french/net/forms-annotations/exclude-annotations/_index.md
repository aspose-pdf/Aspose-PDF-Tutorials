---
title: Comparaison PDF côte à côte excluant les annotations avec Aspose.Pdf for .NET
weight: 101
limit:
description: Guide étape par étape pour comparer des PDF et exclure les zones d'annotation à l'aide d'Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Guide étape par étape pour comparer des PDF et exclure les zones d'annotation
    à l'aide d'Aspose.Pdf for .NET.
  headline: Comparaison PDF côte à côte excluant les annotations avec Aspose.Pdf for
    .NET
  type: TechArticle
- description: Guide étape par étape pour comparer des PDF et exclure les zones d'annotation
    à l'aide d'Aspose.Pdf for .NET.
  name: Comparaison PDF côte à côte excluant les annotations avec Aspose.Pdf for .NET
  steps:
  - name: Définissez les chemins de fichiers pour le PDF principal, le PDF secondaire
      et le PDF de différences en sortie.
    text: Définissez les chemins de fichiers pour le PDF principal, le PDF secondaire
      et le PDF de différences en sortie.
  - name: Vérifiez que les deux fichiers PDF d'entrée existent et arrêtez l'exécution
      avec un message d'erreur si l'un d'eux est manquant.
    text: Vérifiez que les deux fichiers PDF d'entrée existent et arrêtez l'exécution
      avec un message d'erreur si l'un d'eux est manquant.
  - name: Ouvrez les deux fichiers PDF en tant qu'objets Document (pdfA et pdfB) dans
      un bloc using afin qu'ils soient libérés automatiquement.
    text: Ouvrez les deux fichiers PDF en tant qu'objets Document (pdfA et pdfB) dans
      un bloc using afin qu'ils soient libérés automatiquement.
  - name: Collectez les rectangles englobants de chaque annotation dans pdfA et stockez‑les
      dans ignoredRectsA.
    text: Collectez les rectangles englobants de chaque annotation dans pdfA et stockez‑les
      dans ignoredRectsA.
  - name: Collectez les rectangles englobants de chaque annotation dans pdfB et stockez‑les
      dans ignoredRectsB.
    text: Collectez les rectangles englobants de chaque annotation dans pdfB et stockez‑les
      dans ignoredRectsB.
  - name: Créez un objet SideBySideComparisonOptions et affectez les rectangles d'annotation
      précédemment collectés à ExcludeAreas1 et ExcludeAreas2 afin que ces régions
      soient ignorées lors de la comparaison.
    text: Créez un objet SideBySideComparisonOptions et affectez les rectangles d'annotation
      précédemment collectés à ExcludeAreas1 et ExcludeAreas2 afin que ces régions
      soient ignorées lors de la comparaison.
  - name: Exécutez la comparaison PDF côte à côte en utilisant les deux objets Document
      et les options configurées, en écrivant le résultat dans outputPdf.
    text: Exécutez la comparaison PDF côte à côte en utilisant les deux objets Document
      et les options configurées, en écrivant le résultat dans outputPdf.
  - name: Libérez les objets Document et quittez le bloc using.
    text: Libérez les objets Document et quittez le bloc using.
  - name: Affichez un message de confirmation indiquant que la comparaison est terminée
      et où le PDF de différences a été enregistré.
    text: Affichez un message de confirmation indiquant que la comparaison est terminée
      et où le PDF de différences a été enregistré.
  type: HowTo
- questions:
  - answer: Oui. Le code n'ajoute simplement aucun rectangle à la liste `ignoredRects`
      correspondante, de sorte que `ExcludeAreas1`/`ExcludeAreas2` reçoivent un tableau
      vide et le comparateur traite la page entière.
    question: Que se passe-t-il si une page PDF ne contient aucune annotation – la
      comparaison fonctionnera-t-elle toujours ?
  - answer: Définissez `ExcludeAreas1` (ou `ExcludeAreas2`) sur les rectangles collectés
      et laissez l'autre propriété comme un tableau vide ; le comparateur ignorera
      les régions uniquement dans le document spécifié.
    question: Puis‑je exclure uniquement les annotations d'un document tout en conservant
      les annotations de l'autre dans le diff ?
  - answer: Les rectangles qui se chevauchent sont fusionnés en interne par le comparateur,
      de sorte que les limites d'annotation qui se chevauchent sont exclues en toute
      sécurité sans double comptage.
    question: Les rectangles d'annotation qui se chevauchent posent-ils des problèmes
      avec `ExcludeAreas` ?
  - answer: Oui, définissez `compareOpts.ExcludeTables = true;` – ce drapeau fonctionne
      en parallèle avec `ExcludeAreas1`/`ExcludeAreas2` pour ignorer également les
      régions de tableau.
    question: Existe-t-il un moyen d'exclure les tableaux en plus des annotations
      en utilisant le même objet d'options ?
  - answer: Le code vérifie `if (a != null && a.Rect != null)` avant d'ajouter à la
      liste, de sorte que les rectangles nuls sont simplement ignorés et aucune exception
      n'est levée.
    question: Que se passe-t-il si la propriété `Rect` d’une annotation est nulle
      – le code lèvera‑t‑il une exception ?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Comparer des PDF sans annotations
og_description: Exécutez une comparaison PDF côte à côte qui ignore toutes les marques d'annotation.
og_image_alt: Guide montrant une comparaison PDF côte à côte qui exclut les régions d'annotation à l'aide d'Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Comparaison PDF côte à côte excluant les annotations avec Aspose.Pdf
Ce tutoriel montre comment comparer deux fichiers PDF avec Aspose.Pdf for .NET tout en ignorant tout le contenu des annotations. Il extrait les boîtes englobantes de toutes les annotations de chaque document, les transmet à SideBySideComparisonOptions, puis exécute une comparaison côte à côte. Le résultat est un PDF de différences qui met en évidence uniquement les modifications non liées aux annotations.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Que se passe-t-il si une page PDF ne contient aucune annotation – la comparaison fonctionnera-t-elle toujours ?**  
A: Oui. Le code n'ajoute simplement aucun rectangle à la liste `ignoredRects` correspondante, de sorte que `ExcludeAreas1`/`ExcludeAreas2` reçoivent un tableau vide et le comparateur traite la page entière.

**Q: Puis‑je exclure uniquement les annotations d'un document tout en conservant les annotations de l'autre dans le diff ?**  
A: Définissez `ExcludeAreas1` (ou `ExcludeAreas2`) sur les rectangles collectés et laissez l'autre propriété comme un tableau vide ; le comparateur ignorera les régions uniquement dans le document spécifié.

**Q: Les rectangles d'annotation qui se chevauchent posent-ils des problèmes avec `ExcludeAreas` ?**  
A: Les rectangles qui se chevauchent sont fusionnés en interne par le comparateur, de sorte que les limites d'annotation qui se chevauchent sont exclues en toute sécurité sans double comptage.

**Q: Existe-t-il un moyen d'exclure les tableaux en plus des annotations en utilisant le même objet d'options ?**  
A: Oui, définissez `compareOpts.ExcludeTables = true;` – ce drapeau fonctionne en parallèle avec `ExcludeAreas1`/`ExcludeAreas2` pour ignorer également les régions de tableau.

**Q: Que se passe-t-il si la propriété `Rect` d’une annotation est nulle – le code lèvera‑t‑il une exception ?**  
A: Le code vérifie `if (a != null && a.Rect != null)` avant d'ajouter à la liste, de sorte que les rectangles nuls sont simplement ignorés et aucune exception n'est levée.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}