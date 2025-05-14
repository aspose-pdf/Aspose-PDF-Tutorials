---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET ein Ablaufdatum in PDF-Dateien festlegen. Verbessern Sie die Dokumentensicherheit mit dieser Schritt-für-Schritt-Anleitung."
"linktitle": "Ablaufdatum in PDF-Datei festlegen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Ablaufdatum in PDF-Datei festlegen"
"url": "/de/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ablaufdatum in PDF-Datei festlegen

## Einführung

Im digitalen Zeitalter ist die Verwaltung und Sicherung von Dokumenten wichtiger denn je. Stellen Sie sich vor, Sie versenden eine PDF-Datei, die nach einem bestimmten Datum automatisch nicht mehr zugänglich ist. Klingt nach Zauberei, oder? Mit Aspose.PDF für .NET können Sie ganz einfach ein Ablaufdatum für Ihre PDF-Dateien festlegen. Diese Funktion ist besonders nützlich für vertrauliche Dokumente, deren Zugriff nach einer bestimmten Zeit eingeschränkt werden muss. In diesem Tutorial führen wir Sie Schritt für Schritt durch das Festlegen eines Ablaufdatums in einer PDF-Datei. Also, schnappen Sie sich Ihren Programmierhut und los geht‘s!

## Voraussetzungen

Bevor wir beginnen, müssen Sie einige Dinge vorbereitet haben:

1. Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine .NET-Entwicklungsumgebung eingerichtet haben. Dies kann Visual Studio oder eine andere IDE sein, die .NET unterstützt.
2. Aspose.PDF für .NET: Sie müssen die Aspose.PDF-Bibliothek installiert haben. Falls Sie dies noch nicht getan haben, können Sie sie hier herunterladen: [Hier](https://releases.aspose.com/pdf/net/).
3. Grundkenntnisse in C#: Dieses Tutorial setzt Grundkenntnisse in der C#-Programmierung voraus. Falls Sie neu in C# sind, keine Sorge! Wir halten es einfach und unkompliziert.

## Pakete importieren

Um mit Aspose.PDF zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. So geht's:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Diese Namespaces bieten Ihnen Zugriff auf die Kernfunktionen, die für die Arbeit mit PDF-Dokumenten in Aspose.PDF erforderlich sind.

## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein

Zuerst müssen Sie den Pfad zu Ihrem Dokumentenverzeichnis angeben. Hier wird Ihr Ausgabe-PDF gespeichert. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersetzen `"YOUR DOCUMENT DIRECTORY"` mit dem tatsächlichen Pfad, in dem Sie Ihre PDF-Datei speichern möchten. Das ist, als würden Sie Ihrem Programm sagen: „Hey, hier speichere ich meine Dateien!“

## Schritt 2: Instanziieren des Dokumentobjekts

Als nächstes müssen Sie eine neue Instanz des `Document` Klasse. Dies ist Ihre Leinwand, auf der Sie Ihr PDF erstellen.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Denken Sie an die `Document` Objekt als leeres Blatt Papier. Sie können es beliebig mit Inhalten füllen!

## Schritt 3: Eine Seite zum PDF hinzufügen

Nachdem Sie Ihr Dokument eingerichtet haben, können Sie eine Seite hinzufügen. Hier wird Ihr Inhalt abgelegt.

```csharp
doc.Pages.Add();
```

Sie haben gerade eine neue Seite in Ihrem PDF erstellt. Das ist, als würden Sie Ihrem Notizbuch eine neue Seite hinzufügen, auf der Sie Ihre Gedanken notieren können.

## Schritt 4: Text zur Seite hinzufügen

Gestalten wir diese Seite etwas interessanter, indem wir etwas Text hinzufügen. Wir fügen eine einfache „Hallo Welt“-Nachricht hinzu.

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

Diese Codezeile fügt der ersten Seite Ihrer PDF-Datei ein Textfragment hinzu. Das ist, als würden Sie oben auf Ihrer Seite einen Titel schreiben!

## Schritt 5: JavaScript für Ablaufdatum erstellen

Jetzt kommt der spannende Teil! Sie erstellen eine JavaScript-Aktion, die das Ablaufdatum der PDF-Datei überprüft. Wenn das aktuelle Datum das Ablaufdatum überschreitet, wird der Benutzer durch eine entsprechende Meldung darauf hingewiesen.

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

Folgendes passiert:
- Sie bestimmen Ablaufjahr und -monat.
- Sie erhalten das heutige Datum.
- Sie vergleichen das heutige Datum mit dem Ablaufdatum.
- Wenn das heutige Datum nach dem Ablaufdatum liegt, erscheint eine Meldung!

## Schritt 6: JavaScript als PDF-Öffnen-Aktion festlegen

Nun müssen Sie die JavaScript-Aktion als Öffnungsaktion für Ihr PDF-Dokument festlegen. Das bedeutet, dass das JavaScript ausgeführt wird, sobald das PDF geöffnet wird.

```csharp
doc.OpenAction = javaScript;
```

Diese Zeile weist das PDF an, JavaScript auszuführen, sobald es geöffnet wird. Das ist wie eine Erinnerung, die ausgelöst wird, sobald Sie Ihren Kalender öffnen!

## Schritt 7: Speichern Sie das PDF-Dokument

Schließlich ist es an der Zeit, Ihr PDF-Dokument mit der Ablaufdatumsfunktion zu speichern. 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

Diese Zeile speichert Ihre PDF-Datei im angegebenen Verzeichnis unter dem Namen „SetExpiryDate_out.pdf“. Es ist, als würden Sie Ihr fertiges Kunstwerk in einen Rahmen stecken!

## Abschluss

Und da haben Sie es! Sie haben erfolgreich eine PDF-Datei mit Ablaufdatum mit Aspose.PDF für .NET erstellt. Diese Funktion erhöht nicht nur die Sicherheit, sondern sorgt auch dafür, dass vertrauliche Informationen unter Kontrolle bleiben. Ob Sie Verträge, Berichte oder andere wichtige Dokumente versenden – die Festlegung eines Ablaufdatums kann entscheidend sein.

## Häufig gestellte Fragen

### Was ist Aspose.PDF für .NET?
Aspose.PDF für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler PDF-Dokumente in .NET-Anwendungen erstellen, bearbeiten und konvertieren können.

### Kann ich Aspose.PDF kostenlos nutzen?
Ja, Sie können eine kostenlose Testversion von Aspose.PDF verwenden. Sie können es herunterladen [Hier](https://releases.aspose.com/).

### Wie kaufe ich Aspose.PDF?
Sie können Aspose.PDF kaufen, indem Sie die [Kaufseite](https://purchase.aspose.com/buy).

### Was ist, wenn ich Unterstützung brauche?
Wenn Sie Fragen haben oder Hilfe benötigen, können Sie die [Aspose-Supportforum](https://forum.aspose.com/c/pdf/10).

### Kann ich eine temporäre Lizenz für Aspose.PDF erhalten?
Ja, Sie können eine temporäre Lizenz anfordern [Hier](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}