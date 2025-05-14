---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET wiederkehrende Spalten zu PDF-Dokumenten hinzufügen. Schritt-für-Schritt-Anleitung mit Beispielen und Code. Perfekt für Entwickler."
"linktitle": "Wiederholende Spalte im PDF-Dokument hinzufügen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Wiederholende Spalte im PDF-Dokument hinzufügen"
"url": "/de/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wiederholende Spalte im PDF-Dokument hinzufügen

## Einführung

Wenn Sie mit PDF-Dokumenten arbeiten und wiederkehrende Spalten hinzufügen müssen, sind Sie hier genau richtig! Mit Aspose.PDF für .NET können Sie Tabellen und Inhalte in PDF-Dokumenten einfach verwalten. Ob Sie dynamische Berichte, Rechnungen oder andere strukturierte Dokumente erstellen – wiederkehrende Spalten können die Datenorganisation entscheidend verändern. Wir zeigen Ihnen Schritt für Schritt, wie Sie wiederkehrende Spalten zu einem PDF-Dokument hinzufügen.

## Voraussetzungen

Bevor wir uns in den Code stürzen, stellen wir sicher, dass Sie alles eingerichtet haben:

- Aspose.PDF für .NET: Sie müssen die Bibliothek Aspose.PDF für .NET in Ihrem Projekt installiert haben.
- [Laden Sie Aspose.PDF für .NET herunter](https://releases.aspose.com/pdf/net/)
- [Kostenlose Testversion](https://releases.aspose.com/)
- Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine .NET-kompatible IDE wie Visual Studio installiert haben.
- Grundlegende Kenntnisse in C#: Wir werden zwar alles aufschlüsseln, aber grundlegende Kenntnisse in C# helfen Ihnen dabei, problemlos zu folgen.
  
Wenn Sie Aspose.PDF für .NET noch nicht haben, können Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) um mit der Erkundung seiner Funktionen zu beginnen.

## Pakete importieren

Zunächst müssen Sie die erforderlichen Namespaces aus Aspose.PDF für .NET importieren. So geht's:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Diese Pakete bieten die wesentlichen Klassen und Methoden, die zum Arbeiten mit PDF-Dokumenten und Bearbeiten von Tabellen erforderlich sind.

Lassen Sie uns nun den Vorgang in mehrere Schritte unterteilen, um einem PDF-Dokument wiederkehrende Spalten hinzuzufügen. Folgen Sie uns!

## Schritt 1: Legen Sie den Pfad zu Ihrem Dokumentverzeichnis fest

Bevor wir Dateien erstellen oder bearbeiten, müssen wir den Pfad definieren, unter dem die generierte PDF-Datei gespeichert wird. Legen Sie in Ihrem C#-Projekt den Verzeichnispfad fest, in dem Ihre Dateien gespeichert werden:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

Dieser Pfad verweist auf das Verzeichnis, in dem die Ausgabe-PDF gespeichert wird. Ersetzen Sie `"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad auf Ihrem Computer.

## Schritt 2: Erstellen Sie ein neues PDF-Dokument

Um zu beginnen, instanziieren Sie ein neues `Document` Objekt. Dies dient als Container für alle Seiten und Inhalte innerhalb der PDF-Datei.

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

Hier haben wir ein neues PDF-Dokument erstellt und eine leere Seite hinzugefügt. Die `doc.Pages.Add()` Methode fügt eine neue Seite in das Dokument ein.

## Schritt 3: Instanziieren der äußeren Tabelle

Als Nächstes erstellen wir eine äußere Tabelle. Diese Tabelle erstreckt sich über die gesamte Seitenbreite und dient als Container für andere Tabellen, einschließlich der Tabelle mit den sich wiederholenden Spalten.

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

Wir haben die `ColumnWidths` -Eigenschaft auf „100 %“, was bedeutet, dass sich die Tabelle über die gesamte Seitenbreite erstreckt.

## Schritt 4: Erstellen Sie die innere Tabelle

Erstellen wir nun die innere Tabelle mit wiederkehrenden Spalten. Die wichtigsten Eigenschaften sind `Broken`, wodurch die Tabelle auf derselben Seite fortgesetzt werden kann, und `ColumnAdjustment`, wodurch die Spaltenbreiten automatisch an den Inhalt angepasst werden.

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

Diese innere Tabelle wird in der äußeren Tabelle verschachtelt.

## Schritt 5: Tabellen zur Seite hinzufügen

Nachdem wir nun sowohl die äußeren als auch die inneren Tabellen vorbereitet haben, fügen wir sie der Seite hinzu. Dieser Schritt stellt sicher, dass die Tabellen in die Dokumentstruktur integriert werden.

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

Hier haben wir hinzugefügt: `outerTable` auf die Seite, und dann innerhalb der äußeren Tabelle, verschachtelten wir die `mytable`. Zusätzlich setzen wir `RepeatingColumnsCount` bis 5 und gibt an, wie viele Spalten beim Hinzufügen von Daten wiederholt werden sollen.

## Schritt 6: Kopfzeile hinzufügen

Jetzt ist es an der Zeit, der Tabelle die Überschriften hinzuzufügen. Die Überschriftenzeile gibt den Daten Kontext und hilft bei der Strukturierung der Spalten. 

```csharp
Aspose.Pdf.Row row = mytable.Rows.Add();
row.Cells.Add("header 1");
row.Cells.Add("header 2");
row.Cells.Add("header 3");
row.Cells.Add("header 4");
row.Cells.Add("header 5");
row.Cells.Add("header 6");
row.Cells.Add("header 7");
row.Cells.Add("header 11");
row.Cells.Add("header 12");
row.Cells.Add("header 13");
row.Cells.Add("header 14");
row.Cells.Add("header 15");
row.Cells.Add("header 16");
row.Cells.Add("header 17");
```

Dieser Codeausschnitt fügt die erste Zeile hinzu (die wir als Überschriften verwenden) und füllt sie mit Zellen, die Text wie „Überschrift 1“, „Überschrift 2“ usw. enthalten.

## Schritt 7: Datenzeilen hinzufügen

Abschließend können wir der Tabelle Daten hinzufügen. Diese Schleife erstellt dynamisch Zeilen und füllt die Zellen mit Inhalt:

```csharp
for (int RowCounter = 0; RowCounter <= 5; RowCounter++)
{
    Aspose.Pdf.Row row1 = mytable.Rows.Add();
    row1.Cells.Add("col " + RowCounter.ToString() + ", 1");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 2");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 3");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 4");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 5");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 6");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 7");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 11");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 12");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 13");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 14");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 15");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 16");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 17");
}
```

Die Schleife wird sechsmal durchlaufen, wobei Zeilen hinzugefügt und jede Zelle mit den entsprechenden Spaltendaten gefüllt wird (z. B. „Spalte 1, 1“, „Spalte 2, 2“ usw.).

## Schritt 8: Speichern Sie das Dokument

Nachdem alle Zeilen und Spalten hinzugefügt wurden, besteht der letzte Schritt darin, das Dokument im angegebenen Dateipfad zu speichern.

```csharp
doc.Save(outFile);
```

Ihr Dokument wird jetzt mit sich wiederholenden Spalten gespeichert!

## Abschluss

Fertig! Mit diesen einfachen Schritten erstellen Sie mit Aspose.PDF für .NET ein PDF-Dokument mit sich wiederholenden Spalten. Durch die Flexibilität verschachtelter Tabellen können Sie komplexe Layouts erstellen, die Ihren PDFs ein professionelles und übersichtliches Aussehen verleihen. Probieren Sie es für Ihr nächstes Projekt aus und entdecken Sie das volle Potenzial von Aspose.PDF für Ihre PDF-Generierungsanforderungen.

## Häufig gestellte Fragen

### Was ist Aspose.PDF für .NET?
Aspose.PDF für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler PDF-Dokumente programmgesteuert erstellen, bearbeiten und verwalten können.

### Kann ich die Anzahl der sich wiederholenden Spalten dynamisch anpassen?
Ja, Sie können die Anzahl der sich wiederholenden Spalten ändern, indem Sie die `RepeatingColumnsCount` Eigentum.

### Wie kann ich eine Lizenz für Aspose.PDF für .NET anwenden?
Sie können eine Lizenz aus einer Datei oder einem Stream anwenden, indem Sie den [Dokumentation](https://reference.aspose.com/pdf/net/).

### Ist es möglich, den Tabellenzellen Bilder hinzuzufügen?
Ja, Aspose.PDF für .NET unterstützt das Hinzufügen verschiedener Inhaltstypen, einschließlich Bildern, zu Tabellenzellen.

### Kann ich das Tabellenlayout weiter anpassen?
Absolut! Aspose.PDF bietet umfangreiche Funktionen zum Anpassen von Tabellenstilen, einschließlich Rahmen, Polsterung, Ausrichtung und mehr.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}