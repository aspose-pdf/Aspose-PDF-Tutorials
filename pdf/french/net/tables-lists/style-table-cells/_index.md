---
title: Personnalisez l'arrière‑plan, les bordures et le remplissage des cellules de tableau dans les PDF avec Aspose.Pdf for .NET
weight: 101
limit:
description: Apprenez à créer un PDF avec un tableau à deux colonnes et à appliquer des couleurs d'arrière‑plan, des bordures et du remplissage personnalisés à chaque cellule en utilisant Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Apprenez à créer un PDF avec un tableau à deux colonnes et à appliquer
    des couleurs d'arrière‑plan, des bordures et du remplissage personnalisés à chaque
    cellule en utilisant Aspose.Pdf for .NET.
  headline: Personnalisez l'arrière‑plan, les bordures et le remplissage des cellules
    de tableau dans les PDF avec Aspose.Pdf for .NET
  type: TechArticle
- description: Apprenez à créer un PDF avec un tableau à deux colonnes et à appliquer
    des couleurs d'arrière‑plan, des bordures et du remplissage personnalisés à chaque
    cellule en utilisant Aspose.Pdf for .NET.
  name: Personnalisez l'arrière‑plan, les bordures et le remplissage des cellules
    de tableau dans les PDF avec Aspose.Pdf for .NET
  steps:
  - name: Créez un nouveau document PDF vide à l'intérieur d'un bloc using.
    text: Créez un nouveau document PDF vide à l'intérieur d'un bloc using.
  - name: Ajoutez une page vierge au document PDF.
    text: Ajoutez une page vierge au document PDF.
  - name: Instanciez un objet Table avec deux colonnes de 200 points, une fine bordure
      extérieure noire et un remplissage de cellule par défaut de 5 points.
    text: Instanciez un objet Table avec deux colonnes de 200 points, une fine bordure
      extérieure noire et un remplissage de cellule par défaut de 5 points.
  - name: Ajoutez la première ligne au tableau.
    text: Ajoutez la première ligne au tableau.
  - name: Créez la première cellule, insérez le texte "First cell", définissez un
      arrière‑plan jaune clair, une bordure rouge de 2 points et une marge de 4 points.
    text: Créez la première cellule, insérez le texte "First cell", définissez un
      arrière‑plan jaune clair, une bordure rouge de 2 points et une marge de 4 points.
  - name: Créez la deuxième cellule, ajoutez le texte "Second cell", donnez‑lui un
      arrière‑plan vert clair, une bordure bleue de 2 points et une marge de 4 points.
    text: Créez la deuxième cellule, ajoutez le texte "Second cell", donnez‑lui un
      arrière‑plan vert clair, une bordure bleue de 2 points et une marge de 4 points.
  - name: Ajoutez la deuxième ligne au tableau.
    text: Ajoutez la deuxième ligne au tableau.
  - name: Créez la troisième cellule, insérez "Third cell", définissez un arrière‑plan
      cyan clair, une bordure gris foncé de 2 points et une marge de 4 points.
    text: Créez la troisième cellule, insérez "Third cell", définissez un arrière‑plan
      cyan clair, une bordure gris foncé de 2 points et une marge de 4 points.
  - name: Créez la quatrième cellule, ajoutez "Fourth cell", donnez‑lui un arrière‑plan
      rose clair, une bordure violette de 2 points et une marge de 4 points.
    text: Créez la quatrième cellule, ajoutez "Fourth cell", donnez‑lui un arrière‑plan
      rose clair, une bordure violette de 2 points et une marge de 4 points.
  - name: Ajoutez le tableau entièrement stylisé à la page afin qu'il devienne visible
      dans le PDF.
    text: Ajoutez le tableau entièrement stylisé à la page afin qu'il devienne visible
      dans le PDF.
  - name: Enregistrez le document PDF dans un fichier et fermez le bloc using.
    text: Enregistrez le document PDF dans un fichier et fermez le bloc using.
  - name: Affichez un message de confirmation dans la console.
    text: Affichez un message de confirmation dans la console.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` fournit un remplissage de base pour chaque cellule,
      mais si vous attribuez une `Margin` (par ex., `cellA1.Margin = new MarginInfo(...)`)
      les valeurs de marge remplacent le remplissage par défaut pour cette cellule
      spécifique.'
    question: Le `DefaultCellPadding` défini sur le `Table` affecte-t-il les cellules
      qui ont également une `Margin` définie ?
  - answer: Sans `Table.Border`, le rectangle extérieur entourant l'ensemble du tableau
      est omis ; seules les bordures individuelles des cellules que vous avez définies
      (par ex., `cellA2.Border`) seront visibles.
    question: À quoi ressemblera le PDF si je supprime la propriété `Border` de l'objet
      `Table` ?
  - answer: Oui, créez un `BorderInfo` avec un `BorderSide` spécifique (par ex., `new
      BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) et affectez‑le à la
      propriété `Border` de la cellule.
    question: Puis-je donner à une cellule une largeur de bordure différente sur chaque
      côté ?
  - answer: Instanciez une nouvelle `Row` avec `Row newRow = dataTable.Rows.Add();`
      puis ajoutez des cellules à `newRow.Cells` de la même manière que pour les lignes
      précédentes.
    question: Comment ajouter une troisième ligne au tableau après le code présenté ?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Styliser les cellules de tableau PDF – Arrière‑plan, bordure, remplissage
og_description: Formatez rapidement les cellules d'un tableau dans un PDF avec des couleurs, des bordures et des espacements personnalisés en utilisant Aspose.Pdf for .NET.
og_image_alt: Guide montrant comment styliser la couleur d'arrière‑plan, la bordure et le remplissage des cellules de tableau dans un PDF en utilisant Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Personnalisez l'arrière‑plan, les bordures et le remplissage des cellules de tableau dans les PDF avec Aspose.Pdf
Dans ce tutoriel, vous verrez comment générer un document PDF, ajouter un tableau à deux colonnes et contrôler précisément l'apparence de chaque cellule. En définissant les couleurs d'arrière‑plan, les bordures et en ajustant le remplissage, vous pouvez faire ressortir les données du tableau et leur donner un aspect soigné. L'exemple utilise les classes Aspose.Pdf Document et Table pour illustrer chaque option de style.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: Le `DefaultCellPadding` défini sur le `Table` affecte-t-il les cellules qui ont également une `Margin` définie ?**  
A: `DefaultCellPadding` fournit un remplissage de base pour chaque cellule, mais si vous attribuez une `Margin` (par ex., `cellA1.Margin = new MarginInfo(...)`) les valeurs de marge remplacent le remplissage par défaut pour cette cellule spécifique.

**Q: À quoi ressemblera le PDF si je supprime la propriété `Border` de l'objet `Table` ?**  
A: Sans `Table.Border`, le rectangle extérieur entourant l'ensemble du tableau est omis ; seules les bordures individuelles des cellules que vous avez définies (par ex., `cellA2.Border`) seront visibles.

**Q: Puis-je donner à une cellule une largeur de bordure différente sur chaque côté ?**  
A: Oui, créez un `BorderInfo` avec un `BorderSide` spécifique (par ex., `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) et affectez‑le à la propriété `Border` de la cellule.

**Q: Comment ajouter une troisième ligne au tableau après le code présenté ?**  
A: Instanciez une nouvelle `Row` avec `Row newRow = dataTable.Rows.Add();` puis ajoutez des cellules à `newRow.Cells` de la même manière que pour les lignes précédentes.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}