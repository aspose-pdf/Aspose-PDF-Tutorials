---
"description": "Apprenez à exporter les données d'une feuille de calcul Excel vers un tableau PDF avec Aspose.PDF pour .NET. Tutoriel étape par étape avec des exemples de code, des prérequis et des conseils utiles."
"linktitle": "Exporter les données d'une feuille de calcul Excel vers un tableau"
"second_title": "Référence de l'API Aspose.PDF pour .NET"
"title": "Exporter les données d'une feuille de calcul Excel vers un tableau"
"url": "/fr/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exporter les données d'une feuille de calcul Excel vers un tableau

## Introduction

Avez-vous déjà eu besoin d'exporter des données d'une feuille de calcul Excel vers un fichier PDF, soigneusement organisées sous forme de tableau ? Imaginez : vous avez beaucoup de données dans Excel et vous devez les partager au format PDF professionnel. Cela peut paraître compliqué, n'est-ce pas ? Mais avec Aspose.PDF pour .NET, cette tâche devient un jeu d'enfant. Dans ce tutoriel, nous vous expliquerons comment exporter des données d'une feuille de calcul Excel vers un tableau au sein d'un document PDF avec Aspose.PDF pour .NET. Nous vous guiderons étape par étape, en détaillant chaque étape, pour que, même novice, vous vous sentiez comme un pro à la fin.

## Prérequis

Avant de plonger dans le codage, mettons en place quelques éléments :

1. Bibliothèque Aspose.PDF pour .NET – Assurez-vous d'avoir installé la dernière version. Vous pouvez [téléchargez-le ici](https://releases.aspose.com/pdf/net/).
2. Bibliothèque Aspose.Cells pour .NET – Vous en aurez besoin pour gérer les opérations Excel. Téléchargez-la depuis [ici](https://releases.aspose.com/cells/net/).
3. Environnement de développement .NET – Un outil comme Visual Studio fonctionnera parfaitement pour le codage.
4. Fichier Excel – Préparez un fichier Excel contenant les données que vous souhaitez exporter.

Si vous ne disposez pas des bibliothèques Aspose.PDF et Aspose.Cells, vous pouvez commencer avec un [essai gratuit](https://releases.aspose.com/).

## Importer des packages

Pour commencer, assurez-vous d'avoir installé les bibliothèques Aspose.PDF et Aspose.Cells dans votre projet. Vous pouvez les installer via le gestionnaire de packages NuGet dans Visual Studio.

Voici comment importer les packages nécessaires dans votre code C# :

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

Maintenant que les conditions préalables sont définies, passons en revue le processus d'exportation de données d'une feuille Excel vers un tableau dans un document PDF.

## Étape 1 : Charger le classeur Excel

Pour commencer, vous devez charger votre classeur Excel dans le programme. Dans cette étape, nous utiliserons Aspose.Cells pour ouvrir le fichier Excel.

```csharp
// Le chemin vers le répertoire des documents.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Charger le classeur Excel
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

Explication : Ici, nous spécifions le chemin du répertoire où se trouve notre fichier Excel et chargeons le classeur à l'aide de `Aspose.Cells.Workbook`Assurez-vous d'ajuster `"YOUR DOCUMENT DIRECTORY"` pour pointer vers l'emplacement de votre fichier.

## Étape 2 : Accéder à la première feuille de travail

Après avoir chargé le classeur, nous devons accéder à la première feuille de calcul où nos données sont stockées.

```csharp
// Accéder à la première feuille de calcul du fichier Excel
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

Explication : Cette étape est simple : nous récupérons la première feuille de calcul du classeur, qui contient les données à exporter.

## Étape 3 : Exporter les données vers DataTable

Maintenant, exportons les données de la feuille Excel dans un objet DataTable, qui servira d'intermédiaire pour transférer les données vers le PDF.

```csharp
// Exporter le contenu de 7 lignes et 2 colonnes à partir de la 1ère cellule vers DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

Explication : Le `ExportDataTable` La méthode extrait les données à partir de la première cellule de la feuille de calcul et couvre toutes les lignes et colonnes. Ces données sont ensuite stockées dans un `DataTable` pour une utilisation ultérieure.

## Étape 4 : Créer un nouveau document PDF

Ensuite, nous devons créer un nouveau document PDF à l’aide d’Aspose.PDF.

```csharp
// Instancier une instance de document
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// Créer une page dans l'instance du document
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

Explication : Ici, nous initialisons un nouveau `Aspose.Pdf.Document` et y ajouter une page. Cette page contiendra ensuite le tableau que nous allons créer à partir des données Excel.

## Étape 5 : Créer un objet tableau dans un PDF

Passons maintenant à la création d’un tableau à l’intérieur du document PDF.

```csharp
// Créer un objet Table
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// Ajoutez l'objet Table à la collection de paragraphes de la page
page.Paragraphs.Add(table);
```

Explication : Nous créons un `Aspose.Pdf.Table` objet et l'ajouter à la collection de paragraphes de la page, ce qui garantit que le tableau s'affiche sur la page.

## Étape 6 : Définir la largeur et les bordures des colonnes

Les tableaux PDF nécessitent des largeurs de colonnes définies. Nous ajouterons également des bordures pour améliorer la lisibilité du tableau.

```csharp
// Définir la largeur des colonnes du tableau
table.ColumnWidths = "40 100 100";

// Définir la bordure de cellule par défaut
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

Explication : Nous définissons les largeurs des trois colonnes et donnons à toutes les cellules une bordure par défaut d'une épaisseur de `0.1F`.

## Étape 7 : Importer les données de DataTable dans un tableau PDF

Il est maintenant temps d’importer les données du DataTable dans notre tableau PDF.

```csharp
// Importer des données dans l'objet Table à partir du DataTable
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

Explication : Le `ImportDataTable` méthode transfère toutes les données du `DataTable` au tableau PDF. Cela remplit le tableau avec les données de votre feuille Excel.

## Étape 8 : Styliser la ligne d'en-tête

Modifions le style de la ligne d’en-tête du tableau en modifiant la couleur d’arrière-plan, la police et l’alignement.

```csharp
// Obtenir la première ligne du tableau
Aspose.Pdf.Row headerRow = table.Rows[0];

// Définir le style de la ligne d'en-tête
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

Explication : Nous parcourons toutes les cellules de la première ligne (en-tête) et définissons leur couleur d'arrière-plan sur bleu, la couleur du texte sur jaune et alignons le texte au centre.

## Étape 9 : styliser les rangées restantes

Pour différencier l'en-tête du reste des lignes, ajoutons un style différent pour les lignes restantes.

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

Explication : Pour toutes les lignes sauf l’en-tête, nous définissons un arrière-plan gris et une couleur de texte blanche.

## Étape 10 : Enregistrer le document PDF

Enfin, enregistrez le document PDF avec le tableau.

```csharp
// Enregistrer le PDF
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

Explication : Nous enregistrons le PDF dans le répertoire spécifié. Et voilà ! Vos données Excel sont désormais intégrées dans un tableau PDF parfaitement formaté.

## Conclusion

Et voilà ! En quelques étapes seulement, vous avez exporté les données d'une feuille de calcul Excel vers un tableau au format PDF grâce à Aspose.PDF pour .NET. En décomposant le processus et en le stylisant au fur et à mesure, vous pouvez personnaliser votre résultat et garantir un rendu clair et professionnel. Ainsi, la prochaine fois que quelqu'un vous remettra un fichier Excel et vous demandera un rapport PDF, vous saurez exactement quoi faire.

## FAQ

### Puis-je personnaliser davantage la table ?
Absolument ! Vous pouvez modifier les couleurs, les polices, l'alignement et même ajouter des bordures à des cellules spécifiques.

### Aspose.PDF pour .NET est-il gratuit ?
Il propose un essai gratuit, mais pour une utilisation prolongée, vous aurez besoin d'une licence. Vous pouvez [achetez-le ici](https://purchase.aspose.com/buy).

### Puis-je exporter uniquement des lignes et des colonnes spécifiques ?
Oui, vous pouvez modifier les paramètres dans le `ExportDataTable` méthode pour exporter des plages spécifiques.

### Cela fonctionne-t-il avec des fichiers Excel volumineux ?
Oui, Aspose.Cells est conçu pour gérer efficacement les fichiers Excel volumineux.

### Comment puis-je ajouter plus de pages au PDF ?
Vous pouvez utiliser `pdfDocument.Pages.Add()` pour ajouter autant de pages que vous le souhaitez.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}