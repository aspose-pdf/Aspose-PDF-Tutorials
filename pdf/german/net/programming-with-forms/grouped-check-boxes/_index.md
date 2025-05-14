---
"description": "Erfahren Sie in diesem Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.PDF für .NET gruppierte Kontrollkästchen (Optionsfelder) in einem PDF-Dokument erstellen."
"linktitle": "Gruppierte Kontrollkästchen im PDF-Dokument"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Gruppierte Kontrollkästchen im PDF-Dokument"
"url": "/de/net/programming-with-forms/grouped-check-boxes/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gruppierte Kontrollkästchen im PDF-Dokument

## Einführung

Das Erstellen interaktiver PDFs ist gar nicht so schwierig, wie es klingt, insbesondere mit leistungsstarken Tools wie Aspose.PDF für .NET. Eines der interaktiven Elemente, die Sie Ihren PDF-Dokumenten hinzufügen können, sind gruppierte Kontrollkästchen, genauer gesagt Optionsfelder, mit denen Benutzer eine Option aus einer Gruppe auswählen können. Dieses Tutorial führt Sie durch das Hinzufügen gruppierter Kontrollkästchen (Optionsfelder) zu einem PDF-Dokument mit Aspose.PDF für .NET. Egal, ob Sie Anfänger oder erfahrener Entwickler sind, diese Anleitung ist ansprechend, detailliert und leicht verständlich.

## Voraussetzungen

Bevor wir in die Schritt-für-Schritt-Anleitung eintauchen, wollen wir einige wesentliche Voraussetzungen klären:

1. Aspose.PDF für .NET: Stellen Sie sicher, dass die Aspose.PDF-Bibliothek installiert ist. Falls nicht, können Sie [Laden Sie es hier herunter](https://releases.aspose.com/pdf/net/).
2. IDE: Sie sollten eine Entwicklungsumgebung wie Visual Studio eingerichtet haben.
3. .NET Framework: Das Projekt sollte auf eine Version des .NET Frameworks abzielen, die mit Aspose.PDF kompatibel ist.
4. Grundlegende C#-Kenntnisse: Um reibungslos mitmachen zu können, sind Kenntnisse in C# und der PDF-Bearbeitung erforderlich.
5. Lizenz: Aspose.PDF benötigt eine Lizenz für die volle Funktionalität. Sie können [eine vorübergehende Lizenz erhalten](https://purchase.aspose.com/temporary-license/) falls erforderlich.

## Pakete importieren

Stellen Sie vor dem Start sicher, dass Sie die erforderlichen Namespaces in Ihr Projekt importiert haben:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Diese Pakete geben Ihnen Zugriff auf alle Klassen und Methoden, die zum Bearbeiten von PDF-Dokumenten erforderlich sind, einschließlich der Erstellung von Optionsfeldern und der Definition ihrer Eigenschaften.

In diesem Abschnitt unterteilen wir den Vorgang zum Erstellen gruppierter Kontrollkästchen (Optionsfelder) in klare, leicht verständliche Schritte.

## Schritt 1: Erstellen Sie ein neues PDF-Dokument

Der erste Schritt besteht darin, eine Instanz des `Document` Objekt, das Ihre PDF-Datei darstellt. Fügen Sie dann Ihrem Dokument eine leere Seite hinzu, auf der Sie Ihre gruppierten Kontrollkästchen platzieren.

```csharp
// Instanziieren des Dokumentobjekts
Document pdfDocument = new Document();

// Fügen Sie der PDF-Datei eine Seite hinzu
Page page = pdfDocument.Pages.Add();
```

Damit wird die Grundlage für das Hinzufügen beliebiger Elemente, beispielsweise Optionsfelder, zur PDF-Datei geschaffen.

## Schritt 2: Radiobutton-Feld initialisieren

Als nächstes müssen wir eine `RadioButtonField` Objekt, das die gruppierten Kontrollkästchen (Optionsfelder) enthält. Dieses Feld wird der jeweiligen Seite hinzugefügt, auf der die Kontrollkästchen angezeigt werden.

```csharp
// Instanziieren Sie das RadioButtonField-Objekt und weisen Sie es der ersten Seite zu
RadioButtonField radio = new RadioButtonField(pdfDocument.Pages[1]);
```

Stellen Sie sich dies als den Container vor, der die einzelnen Optionsfeldoptionen zusammenfasst.

## Schritt 3: Optionsfeldoptionen hinzufügen

Fügen wir nun die einzelnen Optionsfelder zum Feld hinzu. In diesem Beispiel fügen wir zwei Optionsfelder hinzu und legen ihre Positionen mit dem `Rectangle` Objekt.

```csharp
// Fügen Sie die erste Optionsschaltfläche hinzu und geben Sie ihre Position mit Rechteck an
RadioButtonOptionField opt1 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(0, 0, 20, 20));
RadioButtonOptionField opt2 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(100, 0, 120, 20));

// Legen Sie Optionsnamen zur Identifizierung fest
opt1.OptionName = "Option1";
opt2.OptionName = "Option2";
```

Hier, die `Rectangle` Das Objekt definiert die Koordinaten und die Größe jedes Optionsfelds auf der Seite.

## Schritt 4: Passen Sie den Stil der Optionsfelder an

Sie können das Erscheinungsbild der Optionsfelder anpassen, indem Sie deren `Style` Eigenschaft. Beispielsweise möchten Sie möglicherweise quadratische oder kreuzförmige Kontrollkästchen.

```csharp
// Legen Sie den Stil der Optionsfelder fest
opt1.Style = BoxStyle.Square;
opt2.Style = BoxStyle.Cross;
```

Auf diese Weise können Sie das Erscheinungsbild der Kontrollkästchen steuern und sie benutzerfreundlicher und optisch ansprechender gestalten.

## Schritt 5: Rahmeneigenschaften konfigurieren

Rahmen spielen eine wichtige Rolle bei der einfachen Erkennbarkeit der Kontrollkästchen. Hier fügen wir jedem Optionsfeld einen durchgehenden Rahmen hinzu und definieren dessen Breite und Farbe.

```csharp
// Konfigurieren Sie den Rahmen des ersten Optionsfelds
opt1.Border = new Border(opt1);
opt1.Border.Style = BorderStyle.Solid;
opt1.Border.Width = 1;
opt1.Characteristics.Border = Color.Black;

// Konfigurieren Sie den Rahmen des zweiten Optionsfelds
opt2.Border = new Border(opt2);
opt2.Border.Style = BorderStyle.Solid;
opt2.Border.Width = 1;
opt2.Characteristics.Border = Color.Black;
```

Dieser Schritt stellt sicher, dass jedes Optionsfeld einen klar definierten Rahmen hat, was die Lesbarkeit des Dokuments verbessert.

## Schritt 6: Hinzufügen von Optionsfeldern zum Formular

Nun fügen wir die Optionsfelder zum Formular des Dokuments hinzu. Dies ist der letzte Schritt zur Gruppierung der Kontrollkästchen in einem einzigen Feld.

```csharp
// Fügen Sie dem Formularobjekt des Dokuments ein Optionsfeld hinzu
pdfDocument.Form.Add(radio);
```

Das Formularobjekt fungiert als Container für alle interaktiven Elemente, einschließlich unserer gruppierten Kontrollkästchen.

## Schritt 7: Speichern Sie das PDF-Dokument

Wenn alles eingerichtet ist, können Sie das PDF-Dokument am gewünschten Speicherort speichern.

```csharp
// Definieren Sie den Ausgabedateipfad
string dataDir = "YOUR DOCUMENT DIRECTORY" + "GroupedCheckBoxes_out.pdf";

// Speichern Sie das PDF-Dokument
pdfDocument.Save(dataDir);

// Erfolgreiche Erstellung bestätigen
Console.WriteLine("Grouped checkboxes added successfully. File saved at " + dataDir);
```

Und das war's! Sie haben erfolgreich ein PDF mit gruppierten Kontrollkästchen mit Aspose.PDF für .NET erstellt.

## Abschluss

Das Hinzufügen interaktiver Elemente wie gruppierter Kontrollkästchen zu PDF-Dokumenten mag zunächst schwierig erscheinen, doch mit Aspose.PDF für .NET wird es zum Kinderspiel. In dieser Schritt-für-Schritt-Anleitung lernen Sie, wie Sie ein einfaches PDF-Dokument erstellen, gruppierte Optionsfelder hinzufügen, deren Darstellung anpassen und das Endergebnis speichern. Egal, ob Sie Formulare, Umfragen oder andere interaktive PDF-Dateien erstellen – diese Anleitung bietet Ihnen eine solide Grundlage für den Einstieg.

## Häufig gestellte Fragen

### Kann ich einer Gruppe mehr als zwei Optionsfelder hinzufügen?
Absolut! Instanziieren Sie einfach zusätzliche `RadioButtonOptionField` Objekte und fügen Sie sie dem `RadioButtonField` wie im Tutorial gezeigt.

### Wie gehe ich mit mehreren Gruppen von Kontrollkästchen in einem Dokument um?
Um mehrere Gruppen zu erstellen, instanziieren Sie separate `RadioButtonField` Objekte für jede Gruppe.

### Gibt es eine Begrenzung für die Anzahl der Kontrollkästchen, die ich hinzufügen kann?
Nein, Aspose.PDF für .NET setzt keine Beschränkungen hinsichtlich der Anzahl der Kontrollkästchen, die Sie einem PDF hinzufügen können.

### Kann ich das Erscheinungsbild von Kontrollkästchen ändern, nachdem sie hinzugefügt wurden?
Ja, Sie können die Eigenschaften wie Rahmenstil, Breite und Farbe ändern, nachdem die Kontrollkästchen hinzugefügt wurden.

### Ist es möglich, Bilder als Optionsfelder zu verwenden?
Ja, Aspose.PDF ermöglicht Ihnen die Verwendung von benutzerdefinierten Bildern als Optionsfelder, indem Sie die `Appearance` Eigenschaft jeder Optionsfeldoption.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}