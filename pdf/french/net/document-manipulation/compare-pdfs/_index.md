---
title: Comparer des PDF et générer un document de différence mis en évidence à l'aide d'Aspose.PDF for .NET
weight: 101
limit:
description: Apprenez à comparer deux PDF et à créer un PDF de différence mis en évidence avec Aspose.PDF for .NET.
keywords: [pdf comparison, Aspose.PDF for .NET, compare pdf files, generate diff pdf, pdf diff highlighting, pdf document comparison]
url: /net/document-manipulation/compare-pdfs/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Apprenez à comparer deux PDF et à créer un PDF de différence mis en
    évidence avec Aspose.PDF for .NET.
  headline: Comparer des PDF et générer un document de différence mis en évidence
    à l'aide d'Aspose.PDF for .NET
  type: TechArticle
- description: Apprenez à comparer deux PDF et à créer un PDF de différence mis en
    évidence avec Aspose.PDF for .NET.
  name: Comparer des PDF et générer un document de différence mis en évidence à l'aide
    d'Aspose.PDF for .NET
  steps:
  - name: Déclarez les chemins d'accès des fichiers PDF originaux, modifiés et de
      sortie du diff.
    text: Déclarez les chemins d'accès des fichiers PDF originaux, modifiés et de
      sortie du diff.
  - name: Vérifiez que les deux PDF d'entrée existent et interrompez l'exécution avec
      un message d'erreur si l'un d'eux est manquant.
    text: Vérifiez que les deux PDF d'entrée existent et interrompez l'exécution avec
      un message d'erreur si l'un d'eux est manquant.
  - name: Chargez les PDF originaux et modifiés dans des objets `Document` à l'intérieur
      d'un bloc `using`.
    text: Chargez les PDF originaux et modifiés dans des objets `Document` à l'intérieur
      d'un bloc `using`.
  - name: Créez une instance de `ComparisonOptions` avec les paramètres par défaut
      pour la comparaison.
    text: Créez une instance de `ComparisonOptions` avec les paramètres par défaut
      pour la comparaison.
  - name: Exécutez la comparaison, en générant un PDF de différence à `outputPath`
      qui met en évidence les différences entre les deux documents.
    text: Exécutez la comparaison, en générant un PDF de différence à `outputPath`
      qui met en évidence les différences entre les deux documents.
  - name: Affichez un message de confirmation indiquant que le PDF de différence a
      été créé.
    text: Affichez un message de confirmation indiquant que le PDF de différence a
      été créé.
  - name: Fermez le bloc `using`, en libérant les objets `Document` source et cible.
    text: Fermez le bloc `using`, en libérant les objets `Document` source et cible.
  type: HowTo
- questions:
  - answer: Le code vérifie `File.Exists` pour `originalDocument.pdf` et `modifiedDocument.pdf` ;
      si l'un d'eux est manquant, il écrit une erreur dans `Console.Error` et quitte
      sans créer de PDF de différence.
    question: Que se passe-t-il si l'un des fichiers PDF d'entrée n'existe pas ?
  - answer: Non, la version actuelle d'Aspose.Pdf.Comparison ne possède pas de drapeau
      `TextComparisonOptions` pour une comparaison insensible à la casse, ainsi les
      changements de casse apparaîtront comme des différences dans le PDF de différence
      généré.
    question: Puis-je faire en sorte que la comparaison ignore les différences de
      casse dans le texte ?
  - answer: '`TextPdfComparer.CompareFlatDocuments(sourceDoc, targetDoc, compareOpts,
      outputPath)` exécute la comparaison en utilisant les `ComparisonOptions` fournis
      et écrit les différences mises en évidence dans `diffOutput.pdf`.'
    question: Quelle méthode effectue réellement la comparaison de PDF et crée le
      fichier de différence ?
  - answer: Les instructions `using` appellent automatiquement `Dispose` sur `sourceDoc`
      et `targetDoc` à la fin du bloc, aucune disposition supplémentaire n'est donc
      requise.
    question: Dois‑je disposer manuellement des objets `Document` ?
  type: FAQPage
images:
- /net/document-manipulation/compare-pdfs/og-image.png
og_title: Générer un PDF de différence en comparant deux PDF
og_description: Créez un PDF de différence mis en évidence pour voir les modifications entre deux documents à l'aide d'Aspose.PDF for .NET.
og_image_alt: Guide montrant comment comparer deux PDF et produire un PDF de différence qui met en évidence les changements en utilisant Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Comparer des PDF et générer un document de différence mis en évidence à l'aide d'Aspose.PDF
Ce tutoriel montre comment utiliser Aspose.Pdf.Comparison pour comparer deux fichiers PDF et produire un PDF de différence qui met clairement en évidence les écarts. Vous apprendrez à charger les documents original et modifié, à exécuter la comparaison et à enregistrer le fichier de différence résultant. Le code étape par étape montre le processus exact de génération d'un rapport de comparaison visuel.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/compare-pdfs" >}}


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

**Q: Que se passe-t-il si l'un des fichiers PDF d'entrée n'existe pas ?**  
A: Le code vérifie `File.Exists` pour `originalDocument.pdf` et `modifiedDocument.pdf` ; si l'un d'eux est manquant, il écrit une erreur dans `Console.Error` et quitte sans créer de PDF de différence.

**Q: Puis-je faire en sorte que la comparaison ignore les différences de casse dans le texte ?**  
A: Non, la version actuelle d'Aspose.Pdf.Comparison ne possède pas de drapeau `TextComparisonOptions` pour une comparaison insensible à la casse, ainsi les changements de casse apparaîtront comme des différences dans le PDF de différence généré.

**Q: Quelle méthode effectue réellement la comparaison de PDF et crée le fichier de différence ?**  
A: `TextPdfComparer.CompareFlatDocuments(sourceDoc, targetDoc, compareOpts, outputPath)` exécute la comparaison en utilisant les `ComparisonOptions` fournis et écrit les différences mises en évidence dans `diffOutput.pdf`.

**Q: Dois‑je disposer manuellement des objets `Document` ?**  
A: Les instructions `using` appellent automatiquement `Dispose` sur `sourceDoc` et `targetDoc` à la fin du bloc, aucune disposition supplémentaire n'est donc requise.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}