---
"description": "Erfahren Sie in diesem umfassenden Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.PDF für .NET Barrierefreiheitsstrukturelemente in PDFs einfügen."
"linktitle": "Strukturelement zu Element hinzufügen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Strukturelement zu Element hinzufügen"
"url": "/de/net/programming-with-tagged-pdf/add-structure-element-into-element/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Strukturelement zu Element hinzufügen

## Einführung

In der heutigen digitalen Welt ist Barrierefreiheit entscheidend. Jeder sollte gleichberechtigten Zugang zu Informationen haben, und die Bereitstellung in einem für alle leicht verständlichen Format ist entscheidend. In diesem Tutorial erfahren Sie, wie Sie die Barrierefreiheit von PDFs durch das Hinzufügen von Strukturelementen mit Aspose.PDF für .NET verbessern können. Diese leistungsstarke Bibliothek ermöglicht Entwicklern die nahtlose Arbeit mit PDF-Dokumenten und die Erstellung getaggter PDFs, die den Barrierefreiheitsstandards entsprechen.

## Voraussetzungen

Bevor wir unsere Reise in die Welt der PDF-Strukturelemente beginnen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:

1. Visual Studio: Dies ist Ihre IDE, in der Sie Ihren C#-Code schreiben und ausführen. Sie können es herunterladen von [Visual Studio](https://visualstudio.microsoft.com/) falls Sie das nicht bereits getan haben.
2. Aspose.PDF für .NET Bibliothek: Sie benötigen die Bibliothek zur Bearbeitung von PDFs. Laden Sie die neueste Version von der [Aspose-Website](https://releases.aspose.com/pdf/net/). Diese Bibliothek ist für unser Projekt von zentraler Bedeutung.
3. Grundkenntnisse in C#: Kenntnisse der C#-Syntax und der objektorientierten Programmierung sind von Vorteil. Wenn Sie problemlos ein paar Zeilen C# schreiben können, sind Sie startklar!
4. Ein PDF-Dokumentenverzeichnis: Erstellen Sie auf Ihrem System ein Verzeichnis, in dem Sie die Eingabe- und Ausgabe-PDF-Dateien für dieses Tutorial speichern.

Nachdem wir nun unsere Werkzeuge und Kenntnisse zusammengestellt haben, können wir mit den erforderlichen Paketen beginnen!

## Pakete importieren

Zunächst importieren wir die erforderlichen Namespaces. Stellen Sie sicher, dass sich am Anfang Ihrer C#-Datei Folgendes befindet:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
```

Diese Namespaces ermöglichen Ihnen den Zugriff auf die Klassen und Methoden, die Sie für die Arbeit mit Ihren PDF-Dokumenten und die Erstellung getaggter Inhalte benötigen. Kommen wir nun zum Kern der Sache und beginnen Sie mit dem Programmieren!

## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein

Bevor wir mit der Programmierung beginnen, müssen wir festlegen, wo wir unsere Dateien speichern. Dies ist entscheidend für den reibungslosen Ablauf unseres Skripts.

```csharp
// Definieren Sie den Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY"; 
```

Ersetzen `"YOUR DOCUMENT DIRECTORY"` mit dem tatsächlichen Pfad, in dem Sie Ihre PDF-Dateien speichern möchten. Dies könnte so etwas sein wie `C:\\PDFs\\`.

## Schritt 2: Erstellen Sie ein neues PDF-Dokument

Nachdem wir nun unser Verzeichnis festgelegt haben, erstellen wir ein PDF-Dokument, in das wir unsere Strukturelemente einfügen.

```csharp
Document document = new Document();
```

Diese Zeile initialisiert eine neue Instanz des `Document` Klasse, sodass wir mit der Arbeit an unseren PDF-Inhalten beginnen können.

## Schritt 3: Zugriff auf markierte Inhalte und Einrichten

Sobald Ihr Dokument fertig ist, ist es an der Zeit, getaggte Inhalte einzurichten, die für die Zugänglichkeit unerlässlich sind.

### Markierten Inhalt initialisieren

```csharp
ITaggedContent taggedContent = document.TaggedContent;
```

Über diese Zeile erhalten Sie Zugriff auf den getaggten Inhalt Ihrer PDF-Datei. Dieser ist für Screenreader erforderlich, damit Ihr Dokument korrekt interpretiert werden kann.

### Dokumentmetadaten festlegen

Sie möchten Ihrem Dokument einen passenden Titel geben und die Sprache definieren.

```csharp
taggedContent.SetTitle("Text Elements Example");
taggedContent.SetLanguage("en-US");
```

Dadurch werden die Metadaten des Dokuments erweitert und seine Zugänglichkeit verbessert.

## Schritt 4: Strukturelemente erstellen und anhängen

Fügen wir etwas Struktur hinzu! Dazu gehört das Erstellen von Absätzen und Span-Elementen, um ein ordnungsgemäß formatiertes und getaggtes Dokument zu erstellen.

### Stammstrukturelement erstellen

```csharp
StructureElement rootElement = taggedContent.RootElement;
```

Jetzt erstellen wir unseren ersten Satz von Absätzen und Spannelementen.

### Erstes Absatzelement erstellen

```csharp
ParagraphElement p1 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p1);
```

Hier initialisieren wir ein neues Absatzelement und hängen es an das Stammstrukturelement an. Dies ist der Ausgangspunkt Ihres Inhalts!

### Hinzufügen von Span-Elementen zum Absatz

```csharp
SpanElement span11 = taggedContent.CreateSpanElement();
span11.SetText("Span_11");
SpanElement span12 = taggedContent.CreateSpanElement();
span12.SetText(" and Span_12.");
```

Der `span` Elemente sind wie Miniabsätze innerhalb unseres größeren Absatzes. Sie ermöglichen eine feinere Kontrolle über die Textformatierung.

### Kombinieren Sie alles

Lassen Sie uns nun den vollständigen Absatz mit allen Elementen zusammen konstruieren:

```csharp
p1.SetText("Paragraph with ");
p1.AppendChild(span11);
p1.AppendChild(span12);
```

### Wiederholen Sie dies für weitere Absätze.

Sie wiederholen diesen Vorgang für weitere Absätze:

```csharp
ParagraphElement p2 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p2);
SpanElement span21 = taggedContent.CreateSpanElement();
span21.SetText("Span_21");
SpanElement span22 = taggedContent.CreateSpanElement();
span22.SetText("Span_22.");
p2.AppendChild(span21);
p2.SetText(" and ");
p2.AppendChild(span22);
```

Einfach weiter kreieren `ParagraphElement`s und `SpanElement`s, und hängen Sie sie an die `rootElement` auf die gleiche Weise wie oben gezeigt für `p1`.

## Schritt 5: Speichern Sie Ihr Dokument

Wenn alle Strukturelemente vorhanden sind, ist es Zeit, Ihr PDF-Dokument zu speichern.

### Geben Sie den Ausgabedateipfad an

```csharp
string outFile = dataDir + "AddStructureElementIntoElement_Output.pdf";
```

### Speichern des Dokuments

```csharp
document.Save(outFile);
```

Hier geschieht die Magie! Ihr Dokument wird im angegebenen Ausgabedateipfad gespeichert.

## Schritt 6: PDF/UA-Konformität validieren

Im letzten Schritt prüfen Sie, ob Ihr Dokument den PDF/UA-Standards für Barrierefreiheit entspricht.

Um die Konformität zu überprüfen, verwenden Sie den folgenden Code:

```csharp
document = new Document(outFile);
string logFile = dataDir + "46144_log.xml";
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

Dadurch wird ausgegeben, ob Ihr Dokument den PDF/UA-Standards entspricht, was für die Barrierefreiheit von entscheidender Bedeutung ist.

## Abschluss

Und da haben Sie es! Sie haben gerade gelernt, wie Sie mit Aspose.PDF für .NET Strukturelemente in ein PDF-Dokument einfügen. Mit diesen Schritten können Sie jedes PDF in ein barrierefreies, standardkonformes Format umwandeln und so allen den gleichen Zugang zu Informationen ermöglichen. 

## Häufig gestellte Fragen

### Was ist Aspose.PDF für .NET?
Aspose.PDF für .NET ist eine Bibliothek, die es Entwicklern ermöglicht, PDF-Dokumente programmgesteuert zu erstellen, zu bearbeiten und zu konvertieren.

### Wie überprüfe ich, ob mein PDF barrierefrei ist?
Sie können Ihre PDF-Datei mithilfe der Aspose.PDF-Bibliothek anhand von PDF/UA-Standards validieren, um sicherzustellen, dass sie den Richtlinien zur Barrierefreiheit entspricht.

### Kann ich Aspose.PDF kostenlos nutzen?
Ja, Aspose bietet eine kostenlose Testversion an, mit der Sie die Funktionen kostenlos testen können. Sie können sie herunterladen [Hier](https://releases.aspose.com/).

### Wo finde ich die Dokumentation für Aspose.PDF?
Eine umfassende Dokumentation zu Aspose.PDF finden Sie hier [Hier](https://reference.aspose.com/pdf/net/).

### Wie erwerbe ich eine Lizenz für Aspose.PDF?
Sie können eine Lizenz direkt von der Aspose-Website kaufen [Hier](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}