---
"description": "Fügen Sie in diesem Schritt-für-Schritt-Tutorial mithilfe einer Floating Box mit Aspose.PDF für .NET ganz einfach Seitenzahlen in Ihre PDF-Kopf- und Fußzeile ein."
"linktitle": "Seitenzahl in Kopf- und Fußzeile mithilfe einer schwebenden Box"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Seitenzahl in Kopf- und Fußzeile mithilfe einer schwebenden Box"
"url": "/de/net/programming-with-stamps-and-watermarks/page-number-in-header-footer-using-floating-box/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Seitenzahl in Kopf- und Fußzeile mithilfe einer schwebenden Box

## Einführung

Wenn es um die programmatische Verwaltung von PDF-Dokumenten geht, ist Aspose.PDF für .NET ein herausragendes Tool. Es vereinfacht die Erstellung, Bearbeitung und Manipulation von PDF-Dateien in .NET-Anwendungen. Egal, ob Sie Rechnungen, Berichte oder andere Dokumenttypen erstellen – das elegante Hinzufügen von Seitenzahlen verbessert die Professionalität und Organisation Ihrer PDFs. In diesem Tutorial erfahren Sie, wie Sie mithilfe einer Floating Box Seitenzahlen in Kopf- und Fußzeile Ihrer PDF-Datei einfügen. Bereit zum Start? Los geht’s!

## Voraussetzungen

Bevor wir diese spannende Reise in das Reich der PDF-Bearbeitung beginnen, benötigen Sie einige Dinge:

### Einrichten der .NET-Umgebung
Stellen Sie sicher, dass Sie über eine .NET-Entwicklungsumgebung verfügen. Sie können Visual Studio verwenden, das bei Entwicklern für .NET-Anwendungen beliebt ist.

### Aspose.PDF-Bibliothek
Installieren Sie die Aspose.PDF-Bibliothek. Sie können sie einfach von der Website herunterladen:

- [Laden Sie Aspose.PDF für .NET herunter](https://releases.aspose.com/pdf/net/)

### Grundkenntnisse der C#-Programmierung
Grundlegende Kenntnisse in C# helfen Ihnen, die in diesem Tutorial vorgestellten Konzepte und Codeausschnitte zu begreifen.

### Zugriff auf die Dokumentation
Es ist immer von Vorteil, die [Aspose.PDF Dokumentation](https://reference.aspose.com/pdf/net/) praktisch zum Nachschlagen und zur eingehenderen Erkundung zusätzlicher Funktionen.

## Pakete importieren

Zunächst müssen Sie die erforderlichen Pakete in Ihr Projekt importieren. Dadurch wird sichergestellt, dass die Aspose.PDF-Assembly in Ihrem Code verfügbar ist. So geht's:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Lassen Sie uns nun den Vorgang des Hinzufügens von Seitenzahlen mithilfe einer schwebenden Box in überschaubare Schritte unterteilen. Folgen Sie uns, während wir durch die Schritte gehen.

## Schritt 1: Richten Sie Ihre Dokumentumgebung ein

Geben Sie zunächst das Verzeichnis an, in dem Ihr PDF-Dokument gespeichert wird. Dies ist wichtig, da es bestimmt, wo Ihre Ausgabedatei gespeichert wird.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersetzen `YOUR DOCUMENT DIRECTORY` mit dem Pfad Ihrer Wahl, in dem Sie die PDF-Ausgabedatei speichern möchten.

## Schritt 2: Instanziieren des Dokuments

Im nächsten Schritt wird ein neues PDF-Dokument erstellt. Dazu wird das `Document` Klasse aus der Aspose.PDF-Bibliothek.

```csharp
// Dokumentinstanz instanziieren
Aspose.Pdf.Document pdf = new Aspose.Pdf.Document();
```
Hier erstellen wir eine neue Instanz des `Document` Klasse, die uns als Leinwand für die Manipulation dient.

## Schritt 3: Eine neue Seite hinzufügen

Fügen wir nun unserem PDF-Dokument eine Seite hinzu. Jedes PDF benötigt mindestens eine Seite, oder?

```csharp
// Fügen Sie dem PDF-Dokument eine Seite hinzu
Aspose.Pdf.Page page = pdf.Pages.Add();
```
Dieser Codeausschnitt fügt unserem Dokument eine neue Seite hinzu und bereitet es für den Empfang von Inhalten vor, einschließlich unserer schwebenden Box mit Seitenzahlen.

## Schritt 4: Erstellen Sie eine schwebende Box

Als nächstes erstellen wir unsere Floating Box, die die Seitenzahl enthält. Die `FloatingBox` Klasse ermöglicht es uns, Inhalte frei auf der Seite zu positionieren.

```csharp
// Initialisiert eine neue Instanz der FloatingBox-Klasse
Aspose.Pdf.FloatingBox box1 = new Aspose.Pdf.FloatingBox(140, 80);
```
Hier sind die Parameter `(140, 80)` Geben Sie die Breite und Höhe der Floating Box an. Sie können diese Werte je nach Ihren Layout-Präferenzen anpassen.

## Schritt 5: Positionierung der Floating Box

Die Positionierung ist entscheidend! Sie möchten bestimmen, wo die Seitenzahl auf der Seite erscheinen soll. Sie arbeiten mit dem `Left` Und `Top` Eigenschaften, um die Position anzugeben.

```csharp
// Float-Wert, der die linke Position des Absatzes angibt
box1.Left = 2;
// Float-Wert, der die obere Position des Absatzes angibt
box1.Top = 10;
```
Diese Werte bestimmen die Platzierung der Floating Box auf der Seite. Experimentieren Sie ruhig damit, um herauszufinden, was für Ihr Dokument am besten aussieht.

## Schritt 6: Text mit dem Seitenzahlen-Makro hinzufügen

Jetzt fügen wir eine Zeichenfolge hinzu, die die Seitenzahl dynamisch anzeigt. Hier geschieht die Magie!

```csharp
// Fügen Sie die Makros zur Absatzsammlung der FloatingBox hinzu
box1.Paragraphs.Add(new Aspose.Pdf.Text.TextFragment("Page: ($p/ $P )"));
```
In diesem Fall, `($p/ $P)` ist ein Makro, das die aktuelle Seitenzahl anzeigt (`$p`) und die Gesamtseitenzahl (`$P`). Der Text wird dann so formatiert, dass er etwa „Seite: 1/5“ lautet.

## Schritt 7: Fügen Sie die schwebende Box zur Seite hinzu

Es ist Zeit, die Floating Box zusammen mit dem Seitenzahlentext zu unserer neu erstellten Seite hinzuzufügen.

```csharp
// Fügen Sie der Seite eine FloatingBox hinzu
page.Paragraphs.Add(box1);
```
Diese Zeile bettet Ihre Floating Box im Wesentlichen in die Seite ein und macht sie zu einem Teil des Dokumentlayouts. 

## Schritt 8: Speichern Sie Ihr Dokument

Vergessen Sie nicht, Ihre Arbeit zu speichern! Der letzte Schritt besteht darin, Ihr PDF-Dokument unter einem geeigneten Dateinamen zu speichern.

```csharp
// Speichern des Dokuments
pdf.Save(dataDir + "PageNumberinHeaderFooterUsingFloatingBox_out.pdf");
```
Stellen Sie sicher, dass der angegebene Pfad den gewünschten Dateinamen enthält. Jetzt ist Ihr beeindruckendes PDF mit Seitenzahlen erstellt! 

## Abschluss

Und da haben Sie es! Mit Aspose.PDF für .NET ist es ganz einfach, Seitenzahlen in Kopf- und Fußzeile Ihres PDFs einzufügen. Mit nur wenigen Codezeilen meistern Sie die Dokumentenverarbeitung in Ihren Anwendungen. Experimentieren Sie ruhig mit verschiedenen Layouts und Formatierungen – der Kreativität sind schließlich keine Grenzen gesetzt! Bereit für die Erstellung eines professionellen Dokuments? Dann schnappen Sie sich Ihren Programmierhut und fangen Sie an zu experimentieren.

## Häufig gestellte Fragen

### Kann ich das Erscheinungsbild des Seitenzahlentextes anpassen?  
Ja, Sie können Texteigenschaften wie Schriftgröße, Farbe und Stil anpassen, indem Sie die `TextFragment` Eigenschaften.

### Ist die Nutzung von Aspose.PDF kostenlos?  
Aspose.PDF bietet zwar eine kostenlose Testversion an, ist aber für den produktiven Einsatz kostenpflichtig. Sie können [Kaufen Sie es hier](https://purchase.aspose.com/buy).

### Wo finde ich ausführlichere Dokumentation?  
Eine umfassende Dokumentation finden Sie auf der [Aspose.PDF-Dokumentationsseite](https://reference.aspose.com/pdf/net/).

### Wie wende ich Kopf- und Fußzeilen auf mehreren Seiten an?  
Sie können alle Seiten in Ihrem Dokument durchlaufen und die Floating Box auf jede Seite in gleicher Weise anwenden.

### Was ist, wenn ich Unterstützung für zusätzliche Funktionen benötige?  
Für weitere Fragen oder Unterstützung besuchen Sie bitte die [Aspose Forum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}