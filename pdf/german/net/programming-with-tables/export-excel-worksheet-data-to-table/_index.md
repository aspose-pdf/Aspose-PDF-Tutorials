---
"description": "Erfahren Sie, wie Sie Excel-Arbeitsblattdaten mit Aspose.PDF für .NET in eine PDF-Tabelle exportieren. Schritt-für-Schritt-Anleitung mit Codebeispielen, Voraussetzungen und hilfreichen Tipps."
"linktitle": "Excel-Arbeitsblattdaten in Tabelle exportieren"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Excel-Arbeitsblattdaten in Tabelle exportieren"
"url": "/de/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsblattdaten in Tabelle exportieren

## Einführung

Mussten Sie schon einmal Daten aus einem Excel-Arbeitsblatt in eine PDF-Datei exportieren und diese übersichtlich in einem Tabellenformat präsentieren? Stellen Sie sich vor, Sie haben viele Daten in Excel, möchten diese aber als professionelles PDF teilen. Klingt kompliziert, oder? Mit Aspose.PDF für .NET wird diese Aufgabe zum Kinderspiel. In diesem Tutorial führen wir Sie durch den Prozess des Exports von Excel-Arbeitsblattdaten in eine Tabelle innerhalb eines PDF-Dokuments mit Aspose.PDF für .NET. Wir führen Sie Schritt für Schritt durch die einzelnen Schritte, sodass Sie sich am Ende wie ein Profi fühlen, auch wenn Sie neu dabei sind.

## Voraussetzungen

Bevor wir uns in die Codierung stürzen, lassen Sie uns ein paar Dinge einrichten:

1. Aspose.PDF für .NET Bibliothek – Stellen Sie sicher, dass Sie die neueste Version installiert haben. Sie können [Laden Sie es hier herunter](https://releases.aspose.com/pdf/net/).
2. Aspose.Cells für .NET-Bibliothek – Sie benötigen diese Bibliothek für Excel-Operationen. Laden Sie sie herunter von [Hier](https://releases.aspose.com/cells/net/).
3. .NET-Entwicklungsumgebung – Ein Tool wie Visual Studio eignet sich perfekt zum Codieren.
4. Excel-Datei – Halten Sie eine Excel-Datei mit den Daten bereit, die Sie exportieren möchten.

Wenn Sie die Bibliotheken Aspose.PDF und Aspose.Cells nicht haben, können Sie mit einem [kostenlose Testversion](https://releases.aspose.com/).

## Pakete importieren

Stellen Sie zunächst sicher, dass Sie sowohl die Bibliotheken Aspose.PDF als auch Aspose.Cells in Ihrem Projekt installiert haben. Sie können sie mit dem NuGet-Paket-Manager in Visual Studio installieren.

So importieren Sie die erforderlichen Pakete in Ihren C#-Code:

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

Nachdem die Voraussetzungen nun erfüllt sind, gehen wir den Prozess des Datenexports aus einem Excel-Blatt in eine Tabelle in einem PDF-Dokument durch.

## Schritt 1: Laden Sie die Excel-Arbeitsmappe

Zunächst müssen Sie Ihre Excel-Arbeitsmappe in das Programm laden. In diesem Schritt verwenden wir Aspose.Cells, um die Excel-Datei zu öffnen.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Laden Sie die Excel-Arbeitsmappe
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

Erklärung: Hier geben wir den Verzeichnispfad an, in dem sich unsere Excel-Datei befindet und laden die Arbeitsmappe mit `Aspose.Cells.Workbook`. Stellen Sie sicher, dass `"YOUR DOCUMENT DIRECTORY"` um auf den Speicherort Ihrer Datei zu verweisen.

## Schritt 2: Zugriff auf das erste Arbeitsblatt

Nach dem Laden der Arbeitsmappe müssen wir auf das erste Arbeitsblatt zugreifen, in dem unsere Daten gespeichert sind.

```csharp
// Zugriff auf das erste Arbeitsblatt in der Excel-Datei
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

Erklärung: Dieser Schritt ist unkompliziert – wir nehmen das erste Arbeitsblatt aus der Arbeitsmappe, das die zu exportierenden Daten enthält.

## Schritt 3: Daten in DataTable exportieren

Exportieren wir nun die Daten aus dem Excel-Blatt in ein DataTable-Objekt, das als Vermittler für die Übertragung der Daten in das PDF fungiert.

```csharp
// Exportieren des Inhalts von 7 Zeilen und 2 Spalten ab der 1. Zelle in DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

Erklärung: Die `ExportDataTable` Die Methode extrahiert die Daten ab der ersten Zelle des Arbeitsblatts und erstreckt sich über alle Zeilen und Spalten. Diese Daten werden dann in einem `DataTable` zur weiteren Verwendung.

## Schritt 4: Erstellen Sie ein neues PDF-Dokument

Als Nächstes müssen wir mit Aspose.PDF ein neues PDF-Dokument erstellen.

```csharp
// Instanziieren einer Dokumentinstanz
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// Erstellen einer Seite in der Dokumentinstanz
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

Erklärung: Hier initialisieren wir ein neues `Aspose.Pdf.Document` und fügen Sie eine Seite hinzu. Diese Seite enthält später die Tabelle, die wir aus den Excel-Daten erstellen.

## Schritt 5: Erstellen Sie ein Tabellenobjekt in PDF

Fahren wir mit der Erstellung einer Tabelle im PDF-Dokument fort.

```csharp
// Erstellen eines Tabellenobjekts
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// Fügen Sie das Tabellenobjekt zur Absatzsammlung der Seite hinzu
page.Paragraphs.Add(table);
```

Erklärung: Wir erstellen eine `Aspose.Pdf.Table` Objekt und fügen Sie es der Absatzsammlung der Seite hinzu, wodurch sichergestellt wird, dass die Tabelle auf der Seite angezeigt wird.

## Schritt 6: Spaltenbreiten und Ränder festlegen

Tabellen in PDFs benötigen definierte Spaltenbreiten. Wir fügen außerdem Rahmen hinzu, um die Lesbarkeit der Tabelle zu verbessern.

```csharp
// Spaltenbreiten der Tabelle festlegen
table.ColumnWidths = "40 100 100";

// Standardzellenrahmen festlegen
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

Erklärung: Wir legen die Breiten der drei Spalten fest und geben allen Zellen einen Standardrahmen mit einer Dicke von `0.1F`.

## Schritt 7: Daten aus DataTable in PDF-Tabelle importieren

Jetzt ist es an der Zeit, die Daten aus der DataTable in unsere PDF-Tabelle zu importieren.

```csharp
// Importieren Sie Daten aus der DataTable in das Table-Objekt
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

Erklärung: Die `ImportDataTable` Methode überträgt alle Daten aus dem `DataTable` in die PDF-Tabelle. Dadurch wird die Tabelle mit den Daten aus Ihrem Excel-Blatt gefüllt.

## Schritt 8: Gestalten Sie die Kopfzeile

Gestalten wir die Kopfzeile der Tabelle, indem wir die Hintergrundfarbe, Schriftart und Ausrichtung ändern.

```csharp
// Holen Sie sich die erste Zeile aus der Tabelle
Aspose.Pdf.Row headerRow = table.Rows[0];

// Stil für die Kopfzeile festlegen
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

Erklärung: Wir durchlaufen alle Zellen in der ersten Zeile (Kopfzeile) und setzen ihre Hintergrundfarbe auf Blau, ihre Textfarbe auf Gelb und richten den Text zentriert aus.

## Schritt 9: Gestalten Sie die restlichen Zeilen

Um zwischen der Kopfzeile und den restlichen Zeilen zu unterscheiden, fügen wir für die restlichen Zeilen einen anderen Stil hinzu.

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

Erklärung: Für alle Zeilen außer der Kopfzeile legen wir einen grauen Hintergrund und eine weiße Textfarbe fest.

## Schritt 10: Speichern Sie das PDF-Dokument

Speichern Sie abschließend das PDF-Dokument mit der Tabelle.

```csharp
// Speichern Sie die PDF-Datei
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

Erklärung: Wir speichern die PDF-Datei im angegebenen Verzeichnis. Voilà! Ihre Excel-Daten befinden sich nun in einer schön formatierten PDF-Tabelle.

## Abschluss

Und da haben Sie es! In nur wenigen Schritten haben Sie Daten aus einem Excel-Arbeitsblatt mit Aspose.PDF für .NET in eine Tabelle in einem PDF exportiert. Indem Sie den Prozess aufschlüsseln und dabei formatieren, können Sie Ihre Ausgabe anpassen und sicherstellen, dass Ihre Daten sauber und professionell aussehen. Wenn Ihnen also das nächste Mal jemand eine Excel-Datei überreicht und nach einem PDF-Bericht fragt, wissen Sie genau, was zu tun ist.

## Häufig gestellte Fragen

### Kann ich die Tabelle noch weiter anpassen?
Absolut! Sie können Farben, Schriftarten und Ausrichtung ändern und sogar Rahmen zu bestimmten Zellen hinzufügen.

### Ist Aspose.PDF für .NET kostenlos?
Es gibt eine kostenlose Testversion, für die erweiterte Nutzung benötigen Sie jedoch eine Lizenz. Sie können [Kaufen Sie es hier](https://purchase.aspose.com/buy).

### Kann ich nur bestimmte Zeilen und Spalten exportieren?
Ja, Sie können die Parameter im `ExportDataTable` Methode zum Exportieren bestimmter Bereiche.

### Funktioniert dies mit großen Excel-Dateien?
Ja, Aspose.Cells ist für die effiziente Verarbeitung großer Excel-Dateien konzipiert.

### Wie kann ich dem PDF weitere Seiten hinzufügen?
Sie können `pdfDocument.Pages.Add()` um so viele Seiten hinzuzufügen, wie Sie benötigen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}