---
"description": "Erfahren Sie mit unserer Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.PDF für .NET mühelos lokale Hyperlinks in PDF-Dateien erstellen."
"linktitle": "Lokalen Hyperlink in PDF-Datei erstellen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Lokalen Hyperlink in PDF-Datei erstellen"
"url": "/de/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lokalen Hyperlink in PDF-Datei erstellen

## Einführung

In dieser Anleitung führen wir Sie durch die Erstellung lokaler Hyperlinks in einer PDF-Datei mit Aspose.PDF für .NET. Wir erklären jeden Schritt klar und deutlich, sodass Sie auch als PDF-Neuling problemlos folgen können.

## Voraussetzungen

Bevor wir uns kopfüber in den Code stürzen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:

1. Visual Studio: Sie benötigen es für die Entwicklung Ihrer .NET-Anwendungen. Laden Sie es herunter von [Webseite](https://visualstudio.microsoft.com/).
2. Aspose.PDF für .NET: Sie können diese Bibliothek über das [Download-Link hier](https://releases.aspose.com/pdf/net/)Es verfügt über zahlreiche Funktionen zur PDF-Bearbeitung.
3. Grundkenntnisse in C#: Ein wenig Vertrautheit mit der C#-Programmierung ist hilfreich, aber keine Sorge, wir gehen den Code Zeile für Zeile durch.
4. .NET Framework: Stellen Sie sicher, dass das .NET Framework auf Ihrem Computer installiert ist. Die Anforderungen finden Sie im Aspose.PDF. [Dokumentation](https://reference.aspose.com/pdf/net/).

Wenn diese Voraussetzungen erfüllt sind, können Sie lernen, wie Sie lokale Hyperlinks in Ihren PDF-Dokumenten erstellen!

## Pakete importieren

Nachdem Sie nun alles vorbereitet haben, importieren Sie die erforderlichen Pakete in Ihr C#-Projekt. Die Bibliothek Aspose.PDF enthält alle benötigten Klassen. So geht's:

### Öffnen Sie Ihr Projekt

Öffnen Sie Ihr vorhandenes .NET-Projekt oder erstellen Sie ein neues in Visual Studio. Wenn Sie neu beginnen, wählen Sie im Startbildschirm „Neues Projekt erstellen“ aus.

### Verweis auf Aspose.PDF hinzufügen

Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf „Abhängigkeiten“. Wählen Sie „NuGet-Pakete verwalten“ und suchen Sie nach `Aspose.PDF`Installieren Sie die neueste verfügbare Version. Damit erhalten Sie alle Tools, die Sie zum Erstellen und Bearbeiten von PDFs benötigen.

### Namespaces importieren

Fügen Sie oben in Ihrer CS-Datei Using-Direktiven für die Aspose.PDF-Bibliothek wie folgt hinzu:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Auf diese Weise können Sie auf die Funktionen der Bibliothek zugreifen.

Wir unterteilen den Prozess der Erstellung lokaler Hyperlinks in einfache Schritte. Jeder Schritt wird ausführlich erklärt, damit Sie die Logik dahinter verstehen.

## Schritt 1: Dokumentinstanz einrichten

In diesem Schritt erstellen Sie eine neue Instanz der Document-Klasse, die die PDF-Datei darstellt, mit der Sie arbeiten werden.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Legen Sie Ihr Dokumentverzeichnis fest
Document doc = new Document(); // Dokumentinstanz erstellen
```
Der `dataDir` Variable ist der Ort, an dem Ihr neu erstelltes PDF gespeichert wird. Sie müssen ersetzen `"YOUR DOCUMENT DIRECTORY"` mit dem tatsächlichen Pfad auf Ihrem System. Die `Document` Die Klasse erstellt ein neues PDF-Dokument, in dem wir Seiten und Links hinzufügen können.

## Schritt 2: Dem Dokument eine Seite hinzufügen

Als Nächstes fügen Sie Ihrem PDF-Dokument eine Seite hinzu. 

```csharp
Page page = doc.Pages.Add(); // Seite zur Seitensammlung hinzufügen
```
Der `Pages.Add()` Die Methode fügt dem Dokument eine neue Seite hinzu. Hier werden alle Ihre Inhalte gespeichert.

## Schritt 3: Erstellen Sie ein Textfragment

Lassen Sie uns nun einen Textabschnitt erstellen, der als anklickbarer Link fungiert.

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
Der `TextFragment` stellt einen Textabschnitt im PDF dar. Hier erstellen wir einen Link, der den Benutzern mitteilt, dass sie zu Seite 7 weitergeleitet werden.

## Schritt 4: Lokalen Hyperlink erstellen

Und hier geschieht die Magie! Sie müssen einen lokalen Hyperlink erstellen, der dem Textfragment mitteilt, wohin es zeigen soll.

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // Lokalen Hyperlink erstellen
link.TargetPageNumber = 7; // Zielseite für Linkinstanz festlegen
text.Hyperlink = link; // TextFragment-Hyperlink festlegen
```
Der `LocalHyperlink` Klasse ermöglicht es uns, auf andere Seiten im selben Dokument zu verweisen. Durch die Einstellung `TargetPageNumber` bis 7: Sie weisen den Hyperlink an, beim Anklicken zu dieser bestimmten Seite zu springen.

## Schritt 5: Fügen Sie das Textfragment zur Seite hinzu

Nachdem wir den Hyperlink eingerichtet haben, ist es an der Zeit, unser Textfragment zu der von uns erstellten Seite hinzuzufügen.

```csharp
page.Paragraphs.Add(text); // Fügen Sie Text zur Absatzsammlung der Seite hinzu
```
Diese Zeile fügt Ihren anklickbaren Text zur Absatzsammlung der Seite hinzu.

## Schritt 6: Erstellen Sie ein weiteres Textfragment (optional)

Fügen wir einen weiteren Hyperlink hinzu, um zurück zu Seite 1 zu navigieren.

```csharp
text = new TextFragment("link page number test to page 1"); // Neues TextFragment erstellen
text.IsInNewPage = true; // Fügen Sie es einer neuen Seite hinzu
```
Erstellen eines neuen `TextFragment` für den zweiten Link setzen wir `IsInNewPage` auf „true“, was bedeutet, dass dieser Text auf einer neuen Seite erscheint.

## Schritt 7: Einrichten des zweiten lokalen Hyperlinks

Wie zuvor erstellen Sie einen weiteren lokalen Hyperlink für Seite 1.

```csharp
link = new LocalHyperlink(); // Erstellen Sie eine weitere lokale Hyperlink-Instanz
link.TargetPageNumber = 1; // Zielseite für zweiten Hyperlink festlegen
text.Hyperlink = link; // Link für zweites TextFragment festlegen
```
Dieser Hyperlink zielt auf Seite 1 und ermöglicht es Benutzern, zurückzuspringen, wenn sie die zweite Seite erreichen.

## Schritt 8: Fügen Sie das zweite Textfragment zur neuen Seite hinzu

Fügen wir diesen Text nun der Seite hinzu.

```csharp
page.Paragraphs.Add(text); // Fügen Sie Text zur Absatzsammlung des Seitenobjekts hinzu
```
Ähnlich wie Schritt 5 fügt diese Zeile den neuen Hyperlinktext zur neu erstellten Seite hinzu.

## Schritt 9: Speichern Sie das Dokument

Endlich ist es Zeit, Ihre harte Arbeit zu speichern! 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // Geben Sie den Namen der Ausgabedatei an
doc.Save(dataDir); // Aktualisiertes Dokument speichern
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
Dies kombiniert Ihren Verzeichnispfad mit dem Dateinamen. Die `Save()` Mit dieser Methode wird Ihr Dokument gespeichert und Sie erhalten eine Bestätigungsnachricht, die Ihnen mitteilt, dass alles reibungslos verlaufen ist!

## Abschluss

Das Erstellen lokaler Hyperlinks in PDF-Dateien mit Aspose.PDF für .NET ist nicht nur ein cooler Trick, sondern eine praktische Funktion, die die Navigation und das Benutzererlebnis verbessert. Sie verfügen nun über das nötige Wissen, um Ihre Leser direkt zu den benötigten Informationen zu führen. Denken Sie nur an unsere anfängliche Analogie: Keine verlorenen Seelen mehr, die sich durch endlose Seiten quälen.

## Häufig gestellte Fragen

### Was ist Aspose.PDF für .NET?
Aspose.PDF für .NET ist eine Bibliothek, die es Entwicklern ermöglicht, PDF-Dokumente mithilfe des .NET-Frameworks programmgesteuert zu erstellen, zu bearbeiten und zu konvertieren.

### Kann ich Hyperlinks zu externen Webseiten erstellen?
Ja, Aspose.PDF unterstützt neben lokalen Hyperlinks innerhalb der PDF auch das Erstellen von Hyperlinks zu externen URLs.

### Gibt es eine kostenlose Testversion für Aspose.PDF?
Absolut! Sie können die kostenlose Testversion über die [Website](https://releases.aspose.com/).

### Welche Programmiersprachen unterstützt Aspose?
Aspose bietet Bibliotheken für verschiedene Programmiersprachen, darunter unter anderem Java, C++ und Python.

### Wie erhalte ich Support für Aspose-Produkte?
Sie können Unterstützung beantragen über das [Aspose Forum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}