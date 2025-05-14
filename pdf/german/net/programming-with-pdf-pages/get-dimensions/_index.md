---
"description": "In diesem Tutorial erklären wir, wie Sie PDF-Seitenabmessungen ermitteln und mit Aspose.PDF für .NET bearbeiten. Detaillierte Schritte führen Sie durch den Prozess."
"linktitle": "PDF-Seitenabmessungen abrufen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "PDF-Seitenabmessungen abrufen"
"url": "/de/net/programming-with-pdf-pages/get-dimensions/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF-Seitenabmessungen abrufen

## Einführung

Mussten Sie schon einmal die Seitenmaße eines PDF-Dokuments anpassen? Vielleicht wollten Sie die Größe einer Seite ändern oder sie drehen, um sie Ihren Bedürfnissen anzupassen? Dann sind Sie hier richtig! In diesem Tutorial führen wir Sie durch das Abrufen und Ändern der PDF-Seitenmaße mit Aspose.PDF für .NET. Egal, ob Sie Anfänger oder erfahrener Entwickler sind, diese Anleitung ist einfach und leicht verständlich.

Aspose.PDF für .NET ist eine leistungsstarke Bibliothek, mit der Sie PDF-Dateien mühelos erstellen, bearbeiten und transformieren können. Es ist wie ein Schweizer Taschenmesser für PDFs – Sie können jedes Detail genau an Ihre Anforderungen anpassen. Lassen Sie uns gleich loslegen und lernen, wie Sie mit diesem fantastischen Tool PDF-Seitenabmessungen abrufen und aktualisieren!

## Voraussetzungen

Bevor Sie beginnen, müssen Sie einige Dinge vorbereitet haben, damit Sie diesem Tutorial problemlos folgen können:

1. Aspose.PDF für .NET: Sie können [Laden Sie hier die neueste Version herunter](https://releases.aspose.com/pdf/net/). Wenn Sie keine Lizenz haben, keine Sorge! Sie können eine anfordern [kostenlose Testversion](https://releases.aspose.com/)oder entscheiden Sie sich für eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
2. Visual Studio: Die Entwicklungsumgebung, die Sie zum Schreiben und Ausführen des Codes verwenden.
3. Grundkenntnisse in C#: Wir halten die Dinge zwar einfach, aber eine gewisse Vertrautheit mit C# wird den Prozess reibungsloser gestalten.
4. Zum Arbeiten geeignete PDF-Datei: Greifen Sie auf eine beliebige Beispiel-PDF-Datei zu oder erstellen Sie zum Testen eine neue.

## Pakete importieren

Um mit Aspose.PDF für .NET arbeiten zu können, müssen Sie einige wichtige Namespaces importieren. Dies schafft die Grundlage für die Interaktion mit PDF-Dokumenten. So geht's:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Diese Importe stellen sicher, dass Sie Zugriff auf die Kernklassen haben, die zum Bearbeiten von PDF-Dateien erforderlich sind, insbesondere zum Verwalten von Seiten und Abrufen ihrer Abmessungen.

Nachdem wir nun alles vorbereitet haben, unterteilen wir den Prozess in leicht verständliche Schritte.

## Schritt 1: Dateipfad festlegen und Dokument laden

Der erste Schritt besteht darin, den Pfad zu Ihrem PDF-Dokument anzugeben und es mit Aspose.PDF zu laden. Dadurch können Sie mit den Seiten in der PDF-Datei interagieren.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Dokument öffnen
Document pdfDocument = new Document(dataDir + "UpdateDimensions.pdf");
```

In diesem Schritt öffnen Sie im Wesentlichen die PDF-Datei, die Sie bearbeiten möchten. Wenn Sie schon einmal eine bestimmte Seite eines Buches aufgeschlagen haben, ist dies ganz ähnlich – nur dass Sie stattdessen ein PDF-Dokument öffnen, um auf dessen Seiten zuzugreifen.

## Schritt 2: Fügen Sie eine leere Seite hinzu, wenn keine Seiten vorhanden sind

Was ist, wenn Ihr Dokument keine Seiten enthält? Keine Sorge! Wir können dem Dokument eine leere Seite hinzufügen und damit arbeiten. So prüfen Sie, ob eine Seite vorhanden ist, und fügen bei Bedarf eine neue hinzu:

```csharp
// Fügt dem PDF-Dokument eine leere Seite hinzu
Page page = pdfDocument.Pages.Count > 0 ? pdfDocument.Pages[1] : pdfDocument.Pages.Add();
```

Diese Codezeile prüft, ob das Dokument bereits eine Seite enthält. Wenn ja, wird die erste Seite ausgewählt (`Pages[1]`). Andernfalls wird eine leere Seite erstellt und der PDF-Datei hinzugefügt.

Stellen Sie sich vor, Sie öffnen ein leeres Notizbuch und schreiben auf die erste Seite, obwohl dort nichts steht – einfach, oder?

## Schritt 3: Informationen zur Seitenhöhe und -breite abrufen

Nachdem wir nun eine Seite erstellt haben, mit der wir arbeiten können, ermitteln wir die Abmessungen der Seite. Wir verwenden die `GetPageRect()` Methode, um die Höhe und Breite zu erhalten.

```csharp
// Informationen zur Seitenhöhe und -breite abrufen
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

Hier, `GetPageRect(true)` Gibt ein Rechteck zurück, das die Höhe und Breite der Seite umfasst. Es ist vergleichbar mit dem Messen eines Blattes Papier mit einem Lineal. Die Ausgabe wird in der Konsole angezeigt und gibt die aktuellen Seitenabmessungen an.

## Schritt 4: Drehen Sie die Seite um 90 Grad

Möchten Sie die Seite drehen? Kein Problem! Mit einer einfachen Eigenschaft können Sie die Seite um 90 Grad drehen.

```csharp
// Seite um 90 Grad drehen
page.Rotate = Rotation.on90;
```

Dieser Schritt dreht die Seite im Uhrzeigersinn um 90 Grad. Stellen Sie sich vor, Sie drehen ein gedrucktes Blatt auf Ihrem Schreibtisch um – jetzt ist es im Querformat!

## Schritt 5: Überprüfen Sie die Seitenabmessungen nach der Drehung erneut

Nach dem Drehen der Seite empfiehlt es sich, die Abmessungen noch einmal zu überprüfen. Warum? Weil die Drehung Ihre Interpretation von Höhe und Breite beeinflussen kann.

```csharp
// Informationen zur Seitenhöhe und -breite abrufen
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

Die Seitenmaße werden nun entsprechend der neuen Ausrichtung aktualisiert. Es ist, als würde man ein Foto auf dem Handy drehen – plötzlich wird die Breite zur Höhe und umgekehrt.


## Abschluss

Herzlichen Glückwunsch! Sie haben erfolgreich gelernt, wie Sie die Abmessungen einer PDF-Seite mit Aspose.PDF für .NET abrufen und ändern. Jetzt sollten Sie in der Lage sein, eine PDF-Datei zu laden, ihre Seitenabmessungen zu überprüfen und die Seite bei Bedarf sogar zu drehen.

Die Bearbeitung von PDFs muss nicht kompliziert sein. Mit Aspose.PDF ist es ganz einfach: Befolgen Sie einfach ein paar Schritte und nutzen Sie intuitive Methoden. Wenn Sie das nächste Mal PDF-Seitenmaße bearbeiten müssen, wissen Sie genau, was zu tun ist!

## Häufig gestellte Fragen

### Kann ich die Seite um andere Winkel als 90 Grad drehen?
Ja, Aspose.PDF ermöglicht Ihnen das Drehen von Seiten um 0, 90, 180 oder 270 Grad mit dem `Rotation` Eigentum.

### Was passiert, wenn mein PDF keine Seiten hat?
Wenn Ihr PDF keine Seiten hat, können Sie eine leere Seite hinzufügen, indem Sie `Pages.Add()` Methode, wie in diesem Tutorial gezeigt.

### Kann ich mehrere Seiten gleichzeitig bearbeiten?
Ja, Sie können mehrere Seiten durchlaufen und auf alle Transformationen anwenden, z. B. die Größe ändern oder drehen.

### Haben die Seitenabmessungen Auswirkungen auf den Inhalt der PDF-Datei?
Seitenabmessungen ändern nur die Größe der Arbeitsfläche, nicht den Inhalt. Eine Größenänderung kann jedoch die Darstellung des Inhalts auf der Seite verändern.

### Wo finde ich weitere Informationen zu Aspose.PDF für .NET?
Besuchen Sie die [Dokumentation hier](https://reference.aspose.com/pdf/net/) für ausführlichere Informationen und erweiterte Anwendungsfälle.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}