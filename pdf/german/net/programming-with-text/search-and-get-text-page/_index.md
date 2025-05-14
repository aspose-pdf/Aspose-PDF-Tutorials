---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET nach Text auf einer bestimmten Seite in einer PDF-Datei suchen und diesen abrufen."
"linktitle": "Suchen und Abrufen einer Textseite in einer PDF-Datei"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Suchen und Abrufen einer Textseite in einer PDF-Datei"
"url": "/de/net/programming-with-text/search-and-get-text-page/"
"weight": 430
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Suchen und Abrufen einer Textseite in einer PDF-Datei

## Einführung

Mussten Sie schon einmal in einem PDF-Dokument nach bestimmtem Text suchen und ihn zur weiteren Verwendung extrahieren? Vielleicht entwickeln Sie eine App, die Dokumente verarbeitet und eine präzise Datenextraktion erfordert, oder Sie müssen PDFs einfach nur effizient analysieren. Was auch immer Ihr Fall sein mag, hier sind Sie richtig! In diesem Tutorial erfahren Sie, wie Sie mit Aspose.PDF für .NET Text aus einer Seite in einer PDF-Datei suchen und abrufen. Egal, ob Sie Anfänger oder erfahrener Entwickler sind, diese Anleitung führt Sie Schritt für Schritt und verständlich durch jeden Schritt. Bereit? Los geht's!

## Voraussetzungen

Bevor wir mit dem Programmieren beginnen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:

1. Aspose.PDF für .NET-Bibliothek: Sie können es herunterladen von [Hier](https://releases.aspose.com/pdf/net/) oder erhalten Sie eine kostenlose Testversion über den gleichen Link. Zum Kauf gehen Sie auf die [Aspose-Laden](https://purchase.aspose.com/buy).
2. .NET Framework: Sie benötigen eine funktionierende .NET-Entwicklungsumgebung wie Visual Studio.
3. Eine PDF-Datei: Sie benötigen eine Beispiel-PDF-Datei, in der wir den Text suchen und extrahieren können. Für dieses Tutorial nehmen wir an, die Datei heißt `SearchAndGetTextPage.pdf`.

## Pakete importieren

Zunächst müssen wir die erforderlichen Namespaces für die Arbeit mit Aspose.PDF für .NET importieren. Stellen Sie sicher, dass diese oben in Ihrem Code enthalten sind.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System
```

Nachdem wir die Voraussetzungen geklärt haben, analysieren wir den Code Schritt für Schritt. Jeder Schritt ist klar beschrieben, damit er leicht nachvollziehbar ist.

## Schritt 1: Legen Sie den Pfad zu Ihrem Dokumentverzeichnis fest

Bevor Sie mit Ihrem PDF-Dokument interagieren, müssen Sie den Pfad zum Speicherort Ihres PDF-Dokuments definieren. Dadurch wird sichergestellt, dass das Programm auf die Datei zugreifen kann.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- dataDir: Dies ist der Pfad zum Ordner, in dem Ihre PDF-Dateien gespeichert sind. Ersetzen Sie `"YOUR DOCUMENT DIRECTORY"` mit dem tatsächlichen Pfad, in dem sich das PDF befindet.

## Schritt 2: Laden Sie das PDF-Dokument

Im nächsten Schritt laden Sie das PDF-Dokument in den Speicher, damit Sie damit arbeiten können. So geht's:

```csharp
Document pdfDocument = new Document(dataDir + "SearchAndGetTextPage.pdf");
```

- Dokument: Dies ist die Aspose.PDF-Klasse, die die PDF-Datei lädt.
- pdfDocument: Die Variable, in der Ihre PDF-Datei nach dem Laden gespeichert wird.

## Schritt 3: Erstellen Sie ein Text Absorber-Objekt

Der `TextFragmentAbsorber` Mit dieser Klasse können Sie nach bestimmtem Text in der PDF-Datei suchen. Erstellen wir eine Instanz dieser Klasse, um alle Vorkommen eines bestimmten Suchbegriffs zu finden.

```csharp
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Figure");
```

- TextFragmentAbsorber: Diese Klasse ist für das Suchen und Extrahieren von Text aus der PDF-Datei verantwortlich.
- „Abbildung“: Ersetzen Sie dies durch einen beliebigen Text, nach dem Sie im PDF suchen möchten.

## Schritt 4: Den Text Absorber auf die gesamte PDF-Datei anwenden

Sobald der Textabsorber eingerichtet ist, müssen Sie dem Programm sagen, dass es alle Seiten der PDF-Datei durchsuchen soll.

```csharp
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Accept(): Diese Methode wendet den Textabsorber auf das PDF an und durchsucht jede Seite nach dem von Ihnen angegebenen Text.

## Schritt 5: Abrufen und Durchlaufen des extrahierten Textes

Nachdem wir die PDF-Datei gescannt haben, ist es an der Zeit, die Ergebnisse abzurufen und anzuzeigen. Wir durchlaufen die extrahierten Textfragmente in einer Schleife.

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- TextFragmentCollection: Diese Sammlung enthält alle Instanzen der vom Textabsorber gefundenen Textfragmente.

## Schritt 6: Durchlaufen Sie jedes Fragment und extrahieren Sie Daten

Wir durchlaufen nun die `textFragmentCollection` und extrahieren Sie verschiedene Eigenschaften jedes Textsegments, wie beispielsweise seine Position, Schriftartdetails und Farbe.

```csharp
foreach (TextFragment textFragment in textFragmentCollection)
{
	foreach (TextSegment textSegment in textFragment.Segments)
	{
		Console.WriteLine("Text : {0} ", textSegment.Text);
		Console.WriteLine("Position : {0} ", textSegment.Position);
		Console.WriteLine("XIndent : {0} ", textSegment.Position.XIndent);
		Console.WriteLine("YIndent : {0} ", textSegment.Position.YIndent);
		Console.WriteLine("Font - Name : {0}", textSegment.TextState.Font.FontName);
		Console.WriteLine("Font - IsAccessible : {0} ", textSegment.TextState.Font.IsAccessible);
		Console.WriteLine("Font - IsEmbedded : {0} ", textSegment.TextState.Font.IsEmbedded);
		Console.WriteLine("Font - IsSubset : {0} ", textSegment.TextState.Font.IsSubset);
		Console.WriteLine("Font Size : {0} ", textSegment.TextState.FontSize);
		Console.WriteLine("Foreground Color : {0} ", textSegment.TextState.ForegroundColor);
	}
}
```

- TextFragment: Jedes Fragment enthält Teile des gefundenen Textes.
- Textsegment: Jedes Fragment kann mehrere Segmente haben, die unterschiedliche Teile des Textes darstellen.
- TextState: Bietet detaillierte Informationen zu Schriftart, Größe und Farbe des Textes.

In dieser Schleife drucken wir Details wie den eigentlichen Text, seine Position (X- und Y-Koordinaten), die Schriftart, ob die Schriftart in das PDF eingebettet ist und die Vordergrundfarbe des Textes aus.

## Abschluss

Und da haben Sie es! Sie haben nun erfolgreich mit Aspose.PDF für .NET nach Text in einer PDF-Datei gesucht und diesen extrahiert. Die Flexibilität dieser Bibliothek ist unglaublich. Ob Sie in einem großen Dokument nach bestimmtem Text suchen, ihn extrahieren oder seine Eigenschaften analysieren müssen – Aspose.PDF macht es zum Kinderspiel. Mit dem von uns vorgestellten Code sind Sie zudem bestens gerüstet, ihn an Ihre Bedürfnisse anzupassen. 

## Häufig gestellte Fragen

### Kann ich nach mehreren Phrasen gleichzeitig suchen?  
Ja, Sie können den Code ändern, um nach mehreren Phrasen zu suchen, indem Sie mehrere `TextFragmentAbsorber` Objekte.

### Wie kann ich Text von einer bestimmten Seite extrahieren?  
Sie können eine bestimmte Seite ansprechen, indem Sie die `TextFragmentAbsorber` auf eine einzelne Seite statt auf das gesamte Dokument. Beispiel: `pdfDocument.Pages[1].Accept(textFragmentAbsorber);`.

### Ist Aspose.PDF für .NET kostenlos?  
Aspose.PDF ist ein kommerzielles Produkt, aber Sie können es mit einem [kostenlose Testversion](https://releases.aspose.com/).

### Kann ich mit Aspose.PDF Bilder aus dem PDF extrahieren?  
Ja, Aspose.PDF ermöglicht es Ihnen, neben Text auch Bilder zu extrahieren. Überprüfen Sie die [Dokumentation](https://reference.aspose.com/pdf/net/) für weitere Details.

### Was ist, wenn ich weitere Hilfe oder Unterstützung benötige?  
Hilfe erhalten Sie jederzeit von der [Aspose Support Forum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}