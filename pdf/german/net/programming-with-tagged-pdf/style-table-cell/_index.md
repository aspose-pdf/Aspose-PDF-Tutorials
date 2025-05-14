---
"description": "Erfahren Sie in diesem ausführlichen Tutorial, wie Sie Tabellenzellen in einer PDF-Datei mit Aspose.PDF für .NET formatieren. Folgen Sie den Anweisungen, um ansprechende PDF-Tabellen zu erstellen und zu formatieren."
"linktitle": "Stiltabellenzelle"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Stiltabellenzelle"
"url": "/de/net/programming-with-tagged-pdf/style-table-cell/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stiltabellenzelle

## Einführung

Das Erstellen professioneller PDF-Tabellen kann knifflig sein, aber mit Aspose.PDF für .NET ist es überraschend einfach! Ob Kopf- und Fußzeilen oder einzelne Tabellenzellen – diese leistungsstarke Bibliothek bietet Ihnen alle Werkzeuge für ansprechend formatierte PDF-Dokumente. In diesem Tutorial zeigen wir Ihnen, wie Sie Tabellenzellen in einem PDF-Dokument mit Aspose.PDF für .NET formatieren. Keine Sorge – wir erklären alles in leicht verständlichen Schritten.

## Voraussetzungen

Bevor Sie sich in den Code vertiefen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

1. Aspose.PDF für .NET: Laden Sie die neueste Version von Aspose.PDF herunter und installieren Sie sie von [Hier](https://releases.aspose.com/pdf/net/).
2. IDE (wie Visual Studio): Richten Sie eine .NET-Entwicklungsumgebung ein.
3. Grundkenntnisse der C#-Programmierung: Ein wenig Vertrautheit mit C# ist erforderlich.
4. Aspose.PDF-Lizenz: Erwerben Sie eine temporäre oder Volllizenz, um alle Funktionen der Bibliothek freizuschalten. Sie können eine kostenlose Testversion erhalten [Hier](https://purchase.aspose.com/temporary-license/).

## Pakete importieren

Stellen Sie vor dem Start sicher, dass Sie die erforderlichen Namespaces importieren. Folgendes benötigen Sie in Ihrem Projekt:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nachdem nun alles eingerichtet ist, können wir mit der Schritt-für-Schritt-Anleitung beginnen!

Wir erstellen eine Tabelle in einem PDF-Dokument und formatieren deren Zellen. Jeder Schritt wird detailliert erläutert.

## Schritt 1: Erstellen Sie ein neues PDF-Dokument

Der erste Schritt besteht darin, ein neues PDF-Dokument zu erstellen. In Aspose.PDF können Sie ein neues `Document` Objekt, das Ihre PDF-Datei darstellt.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Erstellen Sie ein neues PDF-Dokument
Document document = new Document();
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table cell style");
taggedContent.SetLanguage("en-US");
```

Hier initialisieren wir ein PDF-Dokument und legen Titel und Sprache fest. Dadurch erhält Ihr Dokument eine korrekte Struktur, die für die PDF/UA-Konformität unerlässlich ist.

## Schritt 2: Einrichten der Tabellenstruktur

Tabellen in PDFs werden innerhalb von Strukturelementen definiert. Erstellen wir die Tabelle und definieren wir ihre Zeilen und Spalten.

```csharp
// Holen Sie sich das Stammstrukturelement
StructureElement rootElement = taggedContent.RootElement;

// Erstellen eines Tabellenstrukturelements
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

Wir haben nun den Kopf der Tabelle definiert (`TableTHeadElement`), Körper (`TableTBodyElement`) und Fuß (`TableTFootElement`) Abschnitte. Sie können sich diese als das Skelett Ihrer Tabelle vorstellen.

## Schritt 3: Formatieren Sie die Kopfzellen

Durch die Gestaltung der Kopfzellen heben wir sie hervor. Hier wenden wir Hintergrundfarben, Rahmen und Textausrichtung an.

```csharp
int colCount = 4;
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";

for (int colIndex = 0; colIndex < colCount; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
    thElement.BackgroundColor = Color.GreenYellow;
    thElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
    thElement.IsNoBorder = true;
    thElement.Margin = new MarginInfo(16.0, 2.0, 8.0, 2.0);
    thElement.Alignment = HorizontalAlignment.Right;
}
```

In diesem Schritt durchlaufen wir jede Kopfzelle und geben ihr einen grün-gelben Hintergrund, einen grauen Rahmen und einen rechtsbündigen Text. Sie können diese Eigenschaften an Ihr gewünschtes Design anpassen.

## Schritt 4: Füllen und formatieren Sie den Tabellenkörper

Der Tabellenkörper enthält die eigentlichen Daten. So können Sie jede Zelle mit spezifischen Rändern, Rahmen und Texteinstellungen gestalten.

```csharp
int rowCount = 4;

for (int rowIndex = 0; rowIndex < rowCount; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = $"Row {rowIndex}";

    for (int colIndex = 0; colIndex < colCount; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
        tdElement.BackgroundColor = Color.Yellow;
        tdElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
        tdElement.Margin = new MarginInfo(8.0, 2.0, 8.0, 2.0);
        tdElement.Alignment = HorizontalAlignment.Center;
        
        TextState cellTextState = new TextState();
        cellTextState.ForegroundColor = Color.DarkBlue;
        cellTextState.FontSize = 7.5F;
        cellTextState.FontStyle = FontStyles.Bold;
        cellTextState.Font = FontRepository.FindFont("Arial");
        tdElement.DefaultCellTextState = cellTextState;
    }
}
```

In diesem Schritt füllen wir den Tabellenkörper mit vier Zeilen und gestalten jede Zelle mit gelbem Hintergrund und zentriertem, fettem blauem Text. Wir verwenden außerdem die `MarginInfo` Klasse zum Definieren der Polsterung um den Text.

## Schritt 5: Gestalten Sie die Fußzeile

Um der Tabelle eine vollständige Struktur zu geben, fügen wir die Fußzeilenzellen hinzu und formatieren sie, genau wie wir es mit der Kopfzeile getan haben.

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";

for (int colIndex = 0; colIndex < colCount; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText($"Foot {colIndex}");
}
```

Der Fußzeilenabschnitt ist ähnlich wie die Kopfzeile gestaltet, sodass die Leser der Struktur der Tabelle leicht folgen können.

## Schritt 6: Speichern und validieren Sie das PDF-Dokument

Abschließend speichern wir das PDF-Dokument und prüfen, ob es PDF/UA-kompatibel ist.

```csharp
// Speichern Sie das mit Tags versehene PDF-Dokument
document.Save(dataDir + "StyleTableCell.pdf");

// Überprüfung der PDF/UA-Konformität
document = new Document(dataDir + "StyleTableCell.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableCell.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Wir speichern das PDF und verwenden die `Validate` Methode, um sicherzustellen, dass es den Zugänglichkeitsstandards (PDF/UA-Konformität) entspricht.

## Abschluss

Die Formatierung von Tabellen in PDF-Dateien mit Aspose.PDF für .NET ist leistungsstark und flexibel. Mit wenigen Codezeilen erstellen Sie individuelle Tabellendesigns, die Ihre PDF-Dokumente hervorheben. Von der Anpassung von Zellrändern und Hintergründen bis hin zur Sicherstellung der Barrierefreiheit – Aspose.PDF erleichtert die Erstellung ansprechender PDF-Dateien.

## Häufig gestellte Fragen

### Kann ich einzelnen Tabellenzellen unterschiedliche Stile zuweisen?  
Ja, Sie können einzelne Zellen gestalten, indem Sie die `TableTDElement` Eigenschaften.

### Wie kann ich Tabellenzellen zusammenführen?  
Sie können die `ColSpan` Und `RowSpan` Eigenschaften zum Zusammenführen von Zellen in einer Tabelle.

### Ist es möglich, eine PDF/UA-kompatible Tabelle zu erstellen?  
Ja, wie in diesem Handbuch gezeigt, können Sie die PDF/UA-Konformität sicherstellen, indem Sie Ihr Dokument mithilfe des `Validate` Verfahren.

### Kann ich in den Tabellenzellen unterschiedliche Schriftarten verwenden?  
Absolut! Sie können verschiedene Schriftarten angeben, indem Sie `TextState` Objekt für jede Zelle.

### Wie lade ich Aspose.PDF für .NET herunter?  
Sie können es herunterladen von der [Veröffentlichungsseite](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}