---
"description": "Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie PDF mit Aspose.PDF für .NET in XPS konvertieren. Perfekt für Entwickler und Dokumentenverarbeitungs-Enthusiasten."
"linktitle": "PDF zu XPS"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "PDF zu XPS"
"url": "/de/net/document-conversion/pdf-to-xps/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF zu XPS

## Einführung

In der heutigen digitalen Welt ist die Konvertierung von Dokumenten von einem Format in ein anderes häufiger denn je. Ob Entwickler, der die Dokumentenverarbeitung in seine Anwendung integrieren möchte, oder Geschäftsleute, die Dateien in einem allgemein akzeptierten Format teilen müssen – das Wissen, wie man PDF-Dateien in XPS (XML Paper Specification) konvertiert, kann äußerst hilfreich sein. In diesem Tutorial vertiefen wir uns in den Prozess der Konvertierung von PDF in XPS mithilfe der leistungsstarken Aspose.PDF-Bibliothek für .NET.

## Voraussetzungen

Bevor wir beginnen, müssen einige Voraussetzungen erfüllt sein:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Hier schreiben und führen Sie Ihren .NET-Code aus.
2. .NET Framework: Kenntnisse des .NET Frameworks sind unerlässlich, da wir für unsere Beispiele C# verwenden werden.
3. Aspose.PDF Bibliothek: Sie müssen die Aspose.PDF Bibliothek installiert haben. Sie können sie von der [Aspose PDF für .NET-Releases-Seite](https://releases.aspose.com/pdf/net/).
4. Grundlegende C#-Kenntnisse: Ein grundlegendes Verständnis der C#-Programmierung wird Ihnen helfen, den Beispielen zu folgen.

## Pakete importieren

Um mit Aspose.PDF zu beginnen, müssen Sie die erforderlichen Pakete in Ihr Projekt importieren. So geht's:

1. Öffnen Sie Visual Studio: Starten Sie Visual Studio und erstellen Sie ein neues Projekt.
2. Referenz hinzufügen: Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt, wählen Sie „NuGet-Pakete verwalten“ und suchen Sie nach „Aspose.PDF“. Installieren Sie das Paket in Ihrem Projekt.
3. Using-Direktiven: Fügen Sie oben in Ihrer C#-Datei die folgende Using-Direktive ein:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
```

Nachdem wir nun alles eingerichtet haben, unterteilen wir den Konvertierungsprozess in überschaubare Schritte.

## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein

Bevor Sie eine PDF-Datei in XPS konvertieren können, müssen Sie das Verzeichnis angeben, in dem sich Ihre PDF-Datei befindet. Dies ist wichtig, da das Programm wissen muss, wo sich die Eingabedatei befindet.

In diesem Schritt definieren Sie eine Zeichenfolgenvariable, die den Pfad zu Ihrem Dokumentenverzeichnis enthält. Dieser Pfad sollte auf den Speicherort Ihrer PDF-Datei verweisen.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersetzen `"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad auf Ihrem Computer, wo die PDF-Datei gespeichert ist.

## Schritt 2: Laden Sie das PDF-Dokument

Nachdem Sie Ihr Dokumentverzeichnis eingerichtet haben, besteht der nächste Schritt darin, das PDF-Dokument zu laden, das Sie konvertieren möchten.

Sie erstellen eine Instanz des `Document` Klasse aus der Aspose.PDF-Bibliothek und übergeben Sie den Pfad Ihrer PDF-Datei an ihren Konstruktor. Dadurch wird das PDF-Dokument in den Speicher geladen.

```csharp
// PDF-Dokument laden
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Stellen Sie sicher, dass Sie `"input.pdf"` durch den Namen Ihrer tatsächlichen PDF-Datei.

## Schritt 3: XPS-Speicheroptionen instanziieren

Bevor Sie das Dokument im XPS-Format speichern, müssen Sie eine Instanz des `XpsSaveOptions` Klasse. Mit dieser Klasse können Sie verschiedene Optionen zum Speichern des Dokuments angeben.

Durch Instanziieren `XpsSaveOptions`können Sie die Konvertierung von PDF-Dateien in XPS anpassen. Für diese grundlegende Konvertierung können Sie die Standardeinstellungen verwenden.

```csharp
// XPS-Speicheroptionen instanziieren
Aspose.Pdf.XpsSaveOptions saveOptions = new Aspose.Pdf.XpsSaveOptions();
```

## Schritt 4: Speichern Sie das Dokument als XPS

Abschließend speichern Sie das geladene PDF-Dokument als XPS-Datei. Hier geschieht die Magie!

Sie rufen die `Save` Methode auf der `pdfDocument` Objekt, wobei der gewünschte Ausgabedateiname und die `saveOptions` Sie haben zuvor erstellt.

```csharp
// Speichern des XPS-Dokuments
pdfDocument.Save("PDFToXPS_out.xps", saveOptions);
```

Diese Codezeile erstellt eine XPS-Datei mit dem Namen `PDFToXPS_out.xps` in Ihrem Projektverzeichnis.

## Abschluss

Herzlichen Glückwunsch! Sie haben ein PDF-Dokument mit Aspose.PDF für .NET erfolgreich in das XPS-Format konvertiert. Diese einfache, aber leistungsstarke Bibliothek ermöglicht Ihnen die einfache Bewältigung verschiedener Dokumentverarbeitungsaufgaben. Egal, ob Sie Dateien für bessere Kompatibilität konvertieren oder Dokumente einfach in einem anderen Format archivieren möchten – Aspose.PDF bietet Ihnen alles.

## Häufig gestellte Fragen

### Was ist das XPS-Format?
XPS (XML Paper Specification) ist ein von Microsoft entwickeltes Dokumentformat, das das Layout und Erscheinungsbild von Dokumenten beibehält.

### Kann ich mehrere PDF-Dateien gleichzeitig in XPS konvertieren?
Ja, Sie können mehrere PDF-Dateien in einem Verzeichnis durchlaufen und jede mit derselben Methode in XPS konvertieren.

### Ist die Nutzung von Aspose.PDF kostenlos?
Aspose.PDF bietet eine kostenlose Testversion an, für den vollen Funktionsumfang ist jedoch eine Lizenz erforderlich. Weitere Informationen finden Sie auf der [Kaufseite](https://purchase.aspose.com/buy).

### Was ist, wenn während der Konvertierung Probleme auftreten?
Sie können Hilfe von der Aspose-Community auf deren [Support-Forum](https://forum.aspose.com/c/pdf/10).

### Kann ich eine temporäre Lizenz für Aspose.PDF erhalten?
Ja, Sie können eine temporäre Lizenz zu Testzwecken anfordern bei der [Seite mit temporärer Lizenz](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}