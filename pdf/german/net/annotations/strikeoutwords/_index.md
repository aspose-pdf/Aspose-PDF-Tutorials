---
"description": "Erfahren Sie in dieser umfassenden Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.PDF für .NET Wörter in einer PDF-Datei durchstreichen. Verbessern Sie Ihre Fähigkeiten zur Dokumentbearbeitung."
"linktitle": "Wörter durchstreichen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Wörter durchstreichen"
"url": "/de/net/annotations/strikeoutwords/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wörter durchstreichen

## Einführung

Mussten Sie schon einmal bestimmten Text in einer PDF-Datei durchstreichen? Ob beim Überprüfen von Dokumenten, beim Markieren von Text oder einfach beim Hervorheben bestimmter Abschnitte – das Durchstreichen von Wörtern kann ein wertvolles Werkzeug sein. In diesem Tutorial erfahren Sie, wie Sie genau das mit Aspose.PDF für .NET erreichen. Diese umfassende Anleitung führt Sie Schritt für Schritt durch die einzelnen Schritte und stellt sicher, dass Sie alle Informationen haben, die Sie für die effektive Implementierung dieser Funktion in Ihren .NET-Anwendungen benötigen. 

## Voraussetzungen

Bevor wir uns in den Code stürzen, müssen Sie einige Voraussetzungen erfüllen, um diesem Tutorial folgen zu können:

1. Aspose.PDF für .NET Bibliothek: Stellen Sie sicher, dass Sie die Aspose.PDF für .NET Bibliothek installiert haben. Sie können [Laden Sie es hier herunter](https://releases.aspose.com/pdf/net/).

2. .NET Framework: Stellen Sie sicher, dass .NET Framework auf Ihrem Computer installiert ist. Dieses Tutorial ist für .NET-Anwendungen konzipiert.

3. Entwicklungsumgebung: Sie benötigen eine IDE wie Visual Studio, um Ihren Code zu schreiben und auszuführen.

4. PDF-Dokument: Halten Sie eine Beispiel-PDF-Datei bereit, mit der Sie arbeiten möchten. In diesem Dokument streichen wir den Text.

5. Grundlegende C#-Kenntnisse: Um die Schritte in diesem Tutorial zu verstehen und umzusetzen, sind Kenntnisse in der C#-Programmierung erforderlich.

## Pakete importieren

Bevor wir mit dem Programmieren beginnen können, müssen wir die erforderlichen Namespaces in unser .NET-Projekt importieren. Dadurch erhalten wir Zugriff auf die Klassen und Methoden, die zur Bearbeitung von PDF-Dateien mit Aspose.PDF erforderlich sind.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Diese Namespaces sind für die Arbeit mit PDF-Dokumenten, die Textverarbeitung und das Hinzufügen von Anmerkungen wie Durchstreichungen von entscheidender Bedeutung.

In diesem Abschnitt wird das Durchstreichen von Wörtern in einem PDF-Dokument in einfache, übersichtliche Schritte unterteilt. Jeder Schritt wird von einer ausführlichen Erklärung begleitet, damit Sie alles verstehen.

## Schritt 1: Laden Sie das PDF-Dokument

Laden Sie zunächst das PDF-Dokument, das Sie bearbeiten möchten. In diesem Dokument streichen Sie bestimmte Wörter oder Ausdrücke.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Öffnen Sie das PDF-Dokument
Document document = new Document(dataDir + "input.pdf");
```

- `dataDir`: Diese Variable enthält den Pfad zu Ihrem Dokumentverzeichnis. Ersetzen Sie `"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad, in dem sich Ihre PDF-Datei befindet.
- `Document`: Der `Document` Die Klasse stellt ein PDF-Dokument dar. Indem wir den Dateipfad an den Konstruktor übergeben, öffnen wir die PDF-Datei zur Verarbeitung.

## Schritt 2: Erstellen Sie einen TextFragment-Absorber, um bestimmten Text zu finden

Als nächstes erstellen wir eine Instanz von `TextFragmentAbsorber` um im PDF-Dokument nach einem bestimmten Textfragment zu suchen. So können wir den Text finden, den wir streichen möchten.

```csharp
// Erstellen Sie eine TextFragment Absorber-Instanz, um nach einem bestimmten Textfragment zu suchen
Aspose.Pdf.Text.TextFragmentAbsorber textFragmentAbsorber = new Aspose.Pdf.Text.TextFragmentAbsorber("Estoque");
```

- `TextFragmentAbsorber`Diese Klasse dient zum Suchen und Bearbeiten bestimmter Textfragmente im PDF-Dokument. In diesem Beispiel suchen wir nach dem Wort „Estoque“. Ersetzen Sie „Estoque“ durch das gesuchte Wort oder die gesuchte Phrase in Ihrem Dokument.

## Schritt 3: Durch die Seiten des PDF-Dokuments iterieren

Jetzt, da wir unsere `TextFragmentAbsorber`müssen wir jede Seite des PDF-Dokuments durchlaufen, um den angegebenen Text zu finden.

```csharp
// Durch die Seiten des PDF-Dokuments iterieren
for (int i = 1; i <= document.Pages.Count; i++)
{
    // Aktuelle Seite des PDF-Dokuments abrufen
    Page page = document.Pages[i];
    page.Accept(textFragmentAbsorber);
}
```

- `for (int i = 1; i <= document.Pages.Count; i++)`: Diese Schleife durchläuft jede Seite des PDF-Dokuments.
- `document.Pages[i]`: Ruft die aktuell verarbeitete Seite ab.
- `page.Accept(textFragmentAbsorber)`: Diese Methode wendet die `TextFragmentAbsorber` zur aktuellen Seite und sucht nach dem angegebenen Text.

## Schritt 4: Sammeln und Verarbeiten der Textfragmente

Nach der Iteration durch die Seiten sammeln wir die gefundenen Textfragmente und bereiten sie für die weitere Verarbeitung vor.

```csharp
// Erstellen Sie eine Sammlung aufgenommener Textfragmente
Aspose.Pdf.Text.TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`Diese Sammlung speichert alle im Dokument gefundenen Textfragmente. Wir verwenden diese Sammlung im nächsten Schritt, um den Text zu streichen.

## Schritt 5: Durchlaufen Sie die Textfragmente und streichen Sie sie durch

In diesem Schritt durchlaufen wir jedes Textfragment in unserer Sammlung und wenden eine Durchstreichungsanmerkung darauf an.

```csharp
// Iterieren Sie über die Sammlung von Textfragmenten
for (int j = 1; j <= textFragmentCollection.Count; j++)
{
	Aspose.Pdf.Text.TextFragment textFragment = textFragmentCollection[j];

    // Holen Sie sich die rechteckigen Abmessungen des TextFragment-Objekts
    Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(
        (float)textFragment.Position.XIndent,
        (float)textFragment.Position.YIndent,
        (float)textFragment.Position.XIndent + (float)textFragment.Rectangle.Width,
        (float)textFragment.Position.YIndent + (float)textFragment.Rectangle.Height);

    // Instanziieren einer StrikeOut-Annotation
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.Page, rect);

    // Eigenschaften der Durchstreichungsanmerkung festlegen
    strikeOut.Opacity = .80f;
    strikeOut.Border = new Border(strikeOut);
    strikeOut.Color = Aspose.Pdf.Color.Red;

    // Fügen Sie die Anmerkung zur Anmerkungssammlung der Seite des Textfragments hinzu
    textFragment.Page.Annotations.Add(strikeOut);
}
```

- `TextFragment textFragment = textFragmentCollection[j]`: Diese Zeile ruft das aktuelle Textfragment ab.
- `Aspose.Pdf.Rectangle`: Wir berechnen die rechteckigen Abmessungen des Textfragments, um zu bestimmen, wo die Durchstreichung angewendet werden soll.
- `StrikeOutAnnotation`: Diese Klasse stellt die Durchstreichungsannotation dar. Wir instanziieren sie mit dem berechneten Rechteck und der aktuellen Seite.
- `strikeOut.Opacity`: Diese Eigenschaft legt die Deckkraft des Durchgestrichenen fest und macht ihn zu 80 % sichtbar.
- `strikeOut.Color`Wir haben die Farbe des Durchstrichs auf Rot gesetzt. Sie können dies in jede beliebige Farbe ändern.
- `textFragment.Page.Annotations.Add(strikeOut)`: Dadurch wird der Seite die Durchstreichungsanmerkung hinzugefügt.

## Schritt 6: Speichern Sie das geänderte PDF-Dokument

Der letzte Schritt besteht darin, das geänderte PDF-Dokument mit den angewendeten Durchstreichungen zu speichern.

```csharp
// Speichern Sie das aktualisierte PDF-Dokument
dataDir = dataDir + "StrikeOutWords_out.pdf";
document.Save(dataDir);
```

- `dataDir + "StrikeOutWords_out.pdf"`: Dadurch wird ein neuer Dateiname für das geänderte Dokument erstellt. Die Originaldatei bleibt unverändert.
- `document.Save(dataDir)`: Speichert das PDF-Dokument mit den Durchstreichungen am angegebenen Speicherort.

## Abschluss

Herzlichen Glückwunsch! Sie haben mit Aspose.PDF für .NET erfolgreich bestimmte Wörter in einem PDF-Dokument durchgestrichen. Mit dieser Schritt-für-Schritt-Anleitung können Sie PDF-Dokumente nun individuell anpassen, indem Sie Text markieren oder durchstreichen. So gestalten Sie sie dynamischer und individueller. Ob Sie juristische Dokumente kommentieren, Berichte erstellen oder einfach nur Text zur Überprüfung markieren – dieses Tutorial vermittelt Ihnen die nötigen Fähigkeiten, um dies effizient zu erledigen.

## Häufig gestellte Fragen

### Kann ich die Farbe des Durchgestrichenen ändern?

Ja, Sie können die Farbe ändern, indem Sie die `strikeOut.Color` Eigenschaft. Sie können sie beispielsweise auf `Aspose.Pdf.Color.Blue` für einen blauen Strikeout.

### Ist es möglich, mehrere Wörter gleichzeitig durchzustreichen?

Absolut! Die `TextFragmentAbsorber` kann verwendet werden, um nach einem beliebigen Wort oder einer beliebigen Phrase im Dokument zu suchen. Sie können die Durchstreichung auf mehrere Instanzen anwenden, indem Sie die `TextFragmentCollection`.

### Was ist, wenn ich Text nur auf bestimmten Seiten streichen möchte?

Sie können die Schleife, die die Seiten durchläuft, so ändern, dass nur die Seiten berücksichtigt werden, die Sie ändern möchten. Beispiel: `for (int i = 1; i <= 3; i++)` würde die Durchstreichung nur auf die ersten drei Seiten anwenden.

### Wie kann ich die Dicke der Durchstreichlinie anpassen?

Sie können die Dicke der durchgestrichenen Linie anpassen, indem Sie die `Border` Eigentum der `StrikeOutAnnotation`. Dadurch kann das Erscheinungsbild der Durchstreichungen angepasst werden.

### Gibt es eine Möglichkeit, die Durchstreichung nach dem Speichern des Dokuments rückgängig zu machen?

Sobald das Dokument gespeichert ist, ist die Durchstreichung dauerhaft. Wenn Sie den Originaltext ohne Durchstreichung beibehalten möchten, sollten Sie vor dem Anwenden von Änderungen eine Sicherungskopie des Originaldokuments erstellen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}