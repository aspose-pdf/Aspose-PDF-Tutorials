---
title: Faire pivoter chaque page PDF de 180° avec Aspose.Pdf pour .NET
weight: 260
limit:
description: Guide étape par étape pour faire pivoter toutes les pages d'un PDF de 180 degrés avec Aspose.Pdf pour .NET.
keywords: [rotate pdf pages .net, Aspose.Pdf for .NET, rotate all pages 180 degrees, pdf page rotation, c# pdf manipulation]
url: /net/programming-with-pdf-pages/rotate-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Guide étape par étape pour faire pivoter toutes les pages d'un PDF
    de 180 degrés avec Aspose.Pdf pour .NET.
  headline: Faire pivoter chaque page PDF de 180° avec Aspose.Pdf pour .NET
  type: TechArticle
- description: Guide étape par étape pour faire pivoter toutes les pages d'un PDF
    de 180 degrés avec Aspose.Pdf pour .NET.
  name: Faire pivoter chaque page PDF de 180° avec Aspose.Pdf pour .NET
  steps:
  - name: Déclarez les chemins d'accès du fichier source et du fichier de destination
      pour le PDF.
    text: Déclarez les chemins d'accès du fichier source et du fichier de destination
      pour le PDF.
  - name: Vérifiez que le fichier source existe et interrompez l'exécution avec un
      message d'erreur s'il n'existe pas.
    text: Vérifiez que le fichier source existe et interrompez l'exécution avec un
      message d'erreur s'il n'existe pas.
  - name: Créez un objet Document pour le PDF source à l'intérieur d'un bloc using
      afin de gérer les ressources.
    text: Créez un objet Document pour le PDF source à l'intérieur d'un bloc using
      afin de gérer les ressources.
  - name: Parcourez chaque Page dans pdfDoc.Pages et définissez sa propriété Rotate
      sur Rotation.on180, retournant chaque page à l'envers.
    text: Parcourez chaque Page dans pdfDoc.Pages et définissez sa propriété Rotate
      sur Rotation.on180, retournant chaque page à l'envers.
  - name: Enregistrez le Document modifié dans le fichier de destination, en conservant
      les rotations.
    text: Enregistrez le Document modifié dans le fichier de destination, en conservant
      les rotations.
  - name: Écrivez un message de confirmation dans la console indiquant que l'opération
      est terminée.
    text: Écrivez un message de confirmation dans la console indiquant que l'opération
      est terminée.
  type: HowTo
- questions:
  - answer: Le code vérifie `File.Exists(sourceFile)` et écrit une erreur dans `Console.Error`
      avant de retourner, ainsi aucune exception n'est levée et le programme se termine
      proprement.
    question: Que se passe-t-il si le fichier PDF source n'existe pas ?
  - answer: Oui, remplacez `Rotation.on180` par une autre valeur d'énumération comme
      `Rotation.on90` (dans le sens des aiguilles d'une montre) ou `Rotation.on270`
      (dans le sens inverse) pour appliquer une rotation différente.
    question: Puis-je faire pivoter les pages d'un angle différent, par ex., 90° dans
      le sens des aiguilles d'une montre ?
  - answer: La collection `Pages` d'Aspose.Pdf est indexée à partir de 1, mais l'itérateur
      `foreach` masque cela, parcourant chaque objet `Page` quel que soit l'indice
      sous‑jacent.
    question: La collection de pages est‑elle indexée à partir de zéro ? Comment fonctionne
      la boucle `foreach` ?
  - answer: L'appel à `pdfDoc.Save(destinationFile)` écrasera tout fichier existant
      portant ce nom, donc utilisez un nom de fichier différent ou sauvegardez l'original
      si vous devez le conserver.
    question: Le PDF original sera-t-il écrasé si j'utilise le même nom de fichier
      pour `destinationFile` ?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pages/og-image.png
og_title: Faire pivoter chaque page PDF de 180°
og_description: Apprenez à retourner toutes les pages d'un PDF à l'envers en quelques lignes de code C# seulement.
og_image_alt: Guide montrant comment faire pivoter chaque page d'un PDF de 180 degrés en utilisant Aspose.Pdf pour .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Faire pivoter chaque page PDF de 180° avec Aspose.Pdf pour .NET
Ce tutoriel montre comment faire pivoter chaque page d'un document PDF existant de 180 degrés avec la classe Document d'Aspose.Pdf. En appliquant une rotation sur toute la page, vous pouvez rapidement corriger des numérisations à l'envers ou réorienter des documents sans les recréer. L'exemple est écrit en C# et fonctionne sur la plateforme .NET.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pages" >}}


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

**Q: Que se passe-t-il si le fichier PDF source n'existe pas ?**  
A: Le code vérifie `File.Exists(sourceFile)` et écrit une erreur dans `Console.Error` avant de retourner, ainsi aucune exception n'est levée et le programme se termine proprement.

**Q: Puis-je faire pivoter les pages d'un angle différent, par ex., 90° dans le sens des aiguilles d'une montre ?**  
A: Oui, remplacez `Rotation.on180` par une autre valeur d'énumération comme `Rotation.on90` (dans le sens des aiguilles d'une montre) ou `Rotation.on270` (dans le sens inverse) pour appliquer une rotation différente.

**Q: La collection de pages est‑elle indexée à partir de zéro ? Comment fonctionne la boucle `foreach` ?**  
A: La collection `Pages` d'Aspose.Pdf est indexée à partir de 1, mais l'itérateur `foreach` masque cela, parcourant chaque objet `Page` quel que soit l'indice sous‑jacent.

**Q: Le PDF original sera-t-il écrasé si j'utilise le même nom de fichier pour `destinationFile` ?**  
A: L'appel à `pdfDoc.Save(destinationFile)` écrasera tout fichier existant portant ce nom, donc utilisez un nom de fichier différent ou sauvegardez l'original si vous devez le conserver.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}