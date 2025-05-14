---
"description": "Erfahren Sie in diesem Tutorial, wie Sie mit Aspose.PDF für .NET markierten Text effizient aus einer PDF-Datei extrahieren. Perfekt für Datenanalyse und Inhaltsprüfung."
"linktitle": "Markierten Text in PDF-Datei extrahieren"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Markierten Text in PDF-Datei extrahieren"
"url": "/de/net/annotations/extracthighlightedtext/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Markierten Text in PDF-Datei extrahieren

## Einführung

Beim Arbeiten mit PDF-Dateien kann das Extrahieren von markiertem Text eine wichtige Aufgabe sein, sei es für die Datenanalyse, die Inhaltsprüfung oder einfach zum Organisieren Ihrer Notizen. Mit Aspose.PDF für .NET ist dieser Vorgang unkompliziert und effizient. In diesem Tutorial zeigen wir Ihnen, wie Sie mit Aspose.PDF für .NET markierten Text aus einem PDF-Dokument extrahieren. Wir behandeln alles von den Voraussetzungen bis zur Schritt-für-Schritt-Anleitung, damit Sie am Ende ein umfassendes Verständnis haben.

## Voraussetzungen

Bevor Sie sich in den Code vertiefen, müssen Sie einige Dinge vorbereitet haben:

- Aspose.PDF für .NET Bibliothek: Stellen Sie sicher, dass die Aspose.PDF Bibliothek installiert ist. Falls nicht, können Sie sie von der [Veröffentlichungsseite](https://releases.aspose.com/pdf/net/).
- Entwicklungsumgebung: Sie sollten eine funktionierende Entwicklungsumgebung wie Visual Studio eingerichtet haben.
- Grundkenntnisse in C#: Kenntnisse der Programmiersprache C# und der objektorientierten Programmierung sind unerlässlich.
- Eine gültige Aspose-Lizenz: Sie können zwar mit einer kostenlosen Testversion beginnen, sollten aber den Erwerb einer [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) oder den Kauf eines von [Hier](https://purchase.aspose.com/buy) zur uneingeschränkten Nutzung.

## Pakete importieren

Zunächst müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Dies ist entscheidend für den Zugriff auf die von Aspose.PDF für .NET bereitgestellten Klassen und Methoden.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Lassen Sie uns nun den Prozess des Extrahierens von markiertem Text aus einer PDF-Datei mit Aspose.PDF für .NET analysieren. Jeder Schritt wird detailliert erklärt, um Ihnen das Verständnis der zugrunde liegenden Konzepte und der Implementierung zu erleichtern.

## Schritt 1: Richten Sie Ihr Projektverzeichnis ein

Zuerst müssen Sie Ihr Projektverzeichnis einrichten, in dem sich Ihre PDF-Datei befindet. Hier geschieht die Magie.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersetzen `"YOUR DOCUMENT DIRECTORY"` mit dem tatsächlichen Pfad zu Ihrem Verzeichnis, in dem sich die PDF-Datei befindet. Aus diesem Verzeichnis ruft die Anwendung die PDF-Datei zur Verarbeitung ab.

## Schritt 2: Laden Sie das PDF-Dokument

Als nächstes müssen Sie das PDF-Dokument laden, aus dem Sie den markierten Text extrahieren möchten. Dies geschieht mit dem `Document` Klasse bereitgestellt von Aspose.PDF.

```csharp
Document doc = new Document(dataDir + "ExtractHighlightedText.pdf");
```

Der `Document` Die Klasse wird mit dem Pfad zur PDF-Datei instanziiert. Hier `"ExtractHighlightedText.pdf"` ist der Name der PDF-Datei, die den markierten Text enthält. Stellen Sie sicher, dass diese Datei im angegebenen Verzeichnis vorhanden ist.

## Schritt 3: Zugriff auf die Annotationssammlung

Sobald das PDF-Dokument geladen ist, können Sie im nächsten Schritt auf die Anmerkungen auf der ersten Seite zugreifen. Anmerkungen dienen in PDF-Dateien dazu, zusätzliche Informationen wie Markierungen, Kommentare und mehr hinzuzufügen.

```csharp
foreach (Annotation annotation in doc.Pages[1].Annotations)
{
```

Der `Annotations` Eigentum der `Page` Das Objekt ermöglicht den Zugriff auf alle Anmerkungen auf einer bestimmten Seite der PDF-Datei. Hier durchlaufen wir jede Anmerkung auf der ersten Seite.

## Schritt 4: Filtern nach hervorgehobenen Textanmerkungen

Da wir nun Zugriff auf alle Anmerkungen haben, müssen wir nur die hervorgehobenen Textanmerkungen herausfiltern. Dies erreichen wir, indem wir den Typ jeder Anmerkung überprüfen.

```csharp
if (annotation is TextMarkupAnnotation)
{
    TextMarkupAnnotation highlightedAnnotation = annotation as TextMarkupAnnotation;
```

Der `TextMarkupAnnotation` Die Klasse wird zur Darstellung von Textmarkierungen, einschließlich Hervorhebungen, verwendet. Die `is` Das Schlüsselwort prüft, ob die Annotation vom Typ ist `TextMarkupAnnotation`, und wenn dies der Fall ist, wird die Anmerkung in `TextMarkupAnnotation`.

## Schritt 5: Extrahieren Sie den markierten Text

Nachdem die hervorgehobene Anmerkung identifiziert wurde, besteht der nächste Schritt darin, den mit der Hervorhebung verknüpften Text zu extrahieren.

```csharp
TextFragmentCollection collection = highlightedAnnotation.GetMarkedTextFragments();
foreach (TextFragment tf in collection)
{
    Console.WriteLine(tf.Text);
}
```

Der `GetMarkedTextFragments()` Methode gibt eine Sammlung von `TextFragment` Objekte, die jeweils einen Teil des hervorgehobenen Textes darstellen. Wir durchlaufen diese Sammlung und geben den Text jedes Fragments auf der Konsole aus.

## Abschluss

Das Extrahieren von markiertem Text aus einer PDF-Datei mit Aspose.PDF für .NET ist eine leistungsstarke Funktion, die Ihren Workflow optimiert, insbesondere bei großen Dokumenten. Mit den in diesem Tutorial beschriebenen Schritten können Sie diese Funktionalität problemlos in Ihre eigenen Projekte integrieren. Ob Sie Ihre Notizen organisieren, Berichte erstellen oder Datenanalysen durchführen – diese Methode bietet eine nahtlose Lösung zum Extrahieren und Nutzen von markiertem Text.

## Häufig gestellte Fragen

### Kann ich mit dieser Methode andere Arten von Anmerkungen extrahieren?  
Ja, Sie können andere Arten von Anmerkungen extrahieren, indem Sie die `if` Bedingung zur Überprüfung auf verschiedene Annotationstypen, wie z. B. `TextAnnotation`, `StampAnnotation`, usw.

### Ist es möglich, markierten Text aus allen Seiten der PDF-Datei zu extrahieren?  
Absolut! Sie können jede Seite des PDF-Dokuments durchlaufen und dieselbe Extraktionslogik anwenden, um markierten Text von jeder Seite zu erfassen.

### Benötige ich eine Lizenz, um Aspose.PDF für .NET zu verwenden?  
Sie können zwar mit einer kostenlosen Testversion beginnen, es wird jedoch empfohlen, eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) oder erwerben Sie eine Volllizenz für uneingeschränkten Zugriff auf alle Funktionen.

### Kann ich den extrahierten Text in einer Datei speichern, anstatt ihn auf der Konsole auszudrucken?  
Ja, Sie können den Code problemlos ändern, um den extrahierten Text in einer Textdatei oder einem anderen gewünschten Format zu speichern.

### Unterstützt Aspose.PDF neben .NET auch andere Plattformen?  
Ja, Aspose.PDF unterstützt auch Java und andere Plattformen und bietet ähnliche Funktionen in verschiedenen Umgebungen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}