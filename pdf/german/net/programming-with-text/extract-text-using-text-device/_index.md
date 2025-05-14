---
"description": "Erfahren Sie, wie Sie mit dem Textgerät in Aspose.PDF für .NET Text aus einem PDF-Dokument extrahieren."
"linktitle": "Text mit dem Textgerät extrahieren"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Text mit dem Textgerät extrahieren"
"url": "/de/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Text mit dem Textgerät extrahieren

## Einführung

Das Extrahieren von Text aus einer PDF-Datei kann knifflig sein, insbesondere bei Dokumenten mit verschiedenen Formaten, eingebetteten Schriftarten oder komplexen Layouts. Mit Aspose.PDF für .NET wird dieser Vorgang jedoch zum Kinderspiel! Egal, ob Sie Seiten einer PDF-Datei zur weiteren Analyse in Klartext konvertieren oder einfach nur bestimmte Abschnitte extrahieren möchten – Aspose.PDF bietet Ihnen alles. In diesem Tutorial erklären wir Schritt für Schritt, wie Sie mithilfe der Klasse TextDevice in Aspose.PDF Text aus einer PDF-Datei extrahieren. Wir bieten außerdem klare Erklärungen, damit Sie die gleichen Methoden problemlos auf Ihre eigenen Projekte anwenden können.

## Voraussetzungen

Bevor wir mit dem Code beginnen, stellen Sie sicher, dass Sie alles vorbereitet haben, um mitmachen zu können. Folgendes benötigen Sie:

1. Aspose.PDF für .NET: Laden Sie die neueste Version von der [Aspose.PDF für .NET-Downloadseite](https://releases.aspose.com/pdf/net/).
2. Entwicklungsumgebung: Visual Studio oder eine andere C#-Entwicklungsumgebung.
3. .NET Framework: Stellen Sie sicher, dass Ihr Projekt auf .NET Framework 4.x oder höher abzielt.
4. PDF-Eingabedatei: Eine PDF-Datei, die Sie zur Textextraktion verwenden. Legen Sie diese in einem Verzeichnis auf Ihrem Computer ab (wir nennen es `YOUR DOCUMENT DIRECTORY`).

## Pakete importieren

Oben in Ihrem Code müssen Sie die erforderlichen Namespaces importieren, um mit Aspose.PDF zu arbeiten:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## Schritt 1: Laden Sie Ihr PDF-Dokument

Bevor wir Text extrahieren, müssen wir das PDF-Dokument in den Speicher laden. In diesem Schritt öffnen Sie Ihr PDF mit Aspose.PDFs `Document` Klasse. Dadurch können Sie auf alle Seiten und Inhalte in der Datei zugreifen.

```csharp
// Definieren Sie den Pfad zu Ihrem PDF-Dokument
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Laden Sie das PDF-Dokument
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Hier verwenden wir `Document pdfDocument = new Document(dataDir + "input.pdf");` um das PDF zu laden. Die `dataDir` Die Variable enthält den Verzeichnispfad Ihrer PDF-Datei. Dadurch erhalten wir Zugriff auf das gesamte Dokument und können Seiten durchlaufen und Inhalte extrahieren.

## Schritt 2: Richten Sie einen String Builder für die Textspeicherung ein

Nachdem das Dokument geladen ist, benötigen wir eine Möglichkeit, den extrahierten Text zu speichern. Dazu verwenden wir ein `StringBuilder` was eine effiziente Zeichenkettenverkettung ermöglicht.

```csharp
// StringBuilder zum Speichern des extrahierten Textes
StringBuilder builder = new StringBuilder();
```

Wir initialisieren eine `StringBuilder` Instanz, die den von jeder Seite extrahierten Text sammelt. Dies ist eine effizientere Methode zur Verarbeitung großer Zeichenfolgen als die normale Zeichenfolgenverkettung in einer Schleife.

## Schritt 3: Durch PDF-Seiten blättern

Als nächstes durchlaufen wir jede Seite des PDF-Dokuments, um den Text zu extrahieren. Wir verarbeiten jede Seite einzeln mit dem `TextDevice` Klasse, die für die Konvertierung des PDF-Inhalts in das Textformat verantwortlich ist.

```csharp
// Durchlaufen Sie alle Seiten im PDF
foreach (Page pdfPage in pdfDocument.Pages)
{
    // Verarbeiten Sie jede Seite zur Textextraktion
}
```

Diese Schleife durchläuft jede Seite des PDF (`pdfDocument.Pages`). Für jede Seite extrahieren wir den Text und fügen ihn zu unserem `StringBuilder`.

## Schritt 4: Text von jeder Seite extrahieren

Nun richten wir den Textextraktionsprozess für jede Seite ein. Hier erstellen wir eine `TextDevice` Objekt und verwenden Sie es zur Verarbeitung der PDF-Seiten. Das `TextDevice` extrahiert Rohtext oder formatierten Text basierend auf den von uns festgelegten Extraktionsoptionen.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // Erstellen Sie ein Textgerät zur Textextraktion
    TextDevice textDevice = new TextDevice();
    
    // Stellen Sie die Textextraktionsoptionen auf den Modus „Pure“ ein
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // Extrahieren Sie Text von der aktuellen Seite und speichern Sie ihn im Speicherstream
    textDevice.Process(pdfPage, textStream);

    // Speicherstrom in Text konvertieren
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // Den extrahierten Text an den StringBuilder anhängen
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: Der `TextDevice` Die Klasse wird verwendet, um Text aus der PDF-Datei zu extrahieren.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: Diese Option extrahiert den Rohtext, ohne Formatierungen wie Schriftarten oder Positionen beizubehalten. Sie können auch `TextFormattingMode.Raw` wenn Sie mehr Kontrolle über die Formatierung benötigen.
- `textDevice.Process(pdfPage, textStream);`: Dadurch wird jede Seite des PDFs verarbeitet und der extrahierte Text in einem `MemoryStream`.
- Abschließend konvertieren wir den Text aus dem `MemoryStream` in eine Zeichenfolge und hängen Sie sie an die `StringBuilder`.

## Schritt 5: Extrahierten Text in einer Datei speichern

Nach der Bearbeitung aller Seiten wird der Text im `StringBuilder`Der letzte Schritt besteht darin, den extrahierten Text in einer Datei zu speichern.

```csharp
// Definieren Sie den Ausgabepfad für die Textdatei
dataDir = dataDir + "input_Text_Extracted_out.txt";

// Speichern Sie den extrahierten Text in einer Datei
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`: Dies schreibt den gesamten Inhalt der `StringBuilder` in eine Textdatei.
- Der Pfad für die Ausgabedatei wird durch Anhängen eines Dateinamens (`"input_Text_Extracted_out.txt"`) zum `dataDir` Weg.

## Abschluss

Das Extrahieren von Text aus einer PDF-Datei mit Aspose.PDF für .NET ist ein einfacher und effizienter Prozess. Mit den in dieser Anleitung beschriebenen Schritten können Sie PDF-Dokumente problemlos öffnen, Seiten durchlaufen und Text in eine Textdatei extrahieren. Dies ist besonders nützlich für die Verarbeitung großer PDF-Datenmengen, die Durchführung von Textanalysen oder die Konvertierung von Dokumenten zur weiteren Bearbeitung.

Mit Aspose.PDF sind Sie nicht nur auf die Textextraktion beschränkt – Sie können Anmerkungen verarbeiten, Bilder bearbeiten und PDFs sogar in andere Formate wie HTML oder Word konvertieren. Die Flexibilität und Leistungsfähigkeit dieser Bibliothek machen sie zu einem unverzichtbaren Werkzeug für die PDF-Verwaltung in .NET-Anwendungen.

## Häufig gestellte Fragen

### Kann Aspose.PDF Text aus bildbasierten PDFs extrahieren?
Nein, Aspose.PDF ist für die Textextraktion aus inhaltsbasierten PDFs konzipiert. Für bildbasierte PDFs wird OCR-Technologie benötigt.

### Behält Aspose.PDF die Formatierung beim Extrahieren von Text bei?
Standardmäßig wird der Text ohne Formatierung extrahiert, Sie können die Extraktionsoptionen jedoch anpassen, wenn Sie einen Teil der Formatierung beibehalten möchten.

### Kann ich Text aus einem bestimmten Seitenbereich extrahieren?
Ja, Sie können den Code so ändern, dass er eine Schleife über einen bestimmten Seitenbereich statt über alle Seiten durchführt.

### Welche Textextraktionsmodi gibt es in Aspose.PDF?
Aspose.PDF bietet zwei Modi: Raw und Pure. Der Raw-Modus versucht, das ursprüngliche Layout beizubehalten, während der Pure-Modus nur den Text ohne Formatierung extrahiert.

### Ist Aspose.PDF für .NET mit .NET Core kompatibel?
Ja, Aspose.PDF für .NET ist vollständig kompatibel mit .NET Core und .NET Framework.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}