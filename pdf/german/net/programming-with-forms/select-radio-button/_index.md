---
"description": "Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.PDF für .NET Optionsfelder in PDF-Dokumenten auswählen. Automatisieren Sie Formularinteraktionen ganz einfach."
"linktitle": "Optionsfeld im PDF-Dokument auswählen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Optionsfeld im PDF-Dokument auswählen"
"url": "/de/net/programming-with-forms/select-radio-button/"
"weight": 250
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Optionsfeld im PDF-Dokument auswählen

## Einführung

Die programmgesteuerte Auswahl von Optionsfeldern in einem PDF-Dokument kann Ihnen viel Zeit sparen, insbesondere bei großen Formularen oder der Automatisierung von Prozessen. Aspose.PDF für .NET ist eine leistungsstarke Bibliothek, die die Interaktion mit PDF-Dateien auf vielfältige Weise erleichtert. In dieser Anleitung führen wir Sie Schritt für Schritt durch die Auswahl eines Optionsfelds in einem PDF-Dokument mit Aspose.PDF für .NET. 

## Voraussetzungen

Bevor Sie sich in den Code vertiefen, stellen Sie sicher, dass Sie Folgendes eingerichtet haben:

1. Aspose.PDF für .NET: Laden Sie die neueste Version von herunter und installieren Sie sie [Aspose.PDF für .NET](https://releases.aspose.com/pdf/net/).
2. IDE: Eine integrierte Entwicklungsumgebung (IDE) wie Visual Studio zum Schreiben und Ausführen Ihres C#-Codes.
3. .NET Framework: Stellen Sie sicher, dass .NET Framework auf Ihrem System installiert ist.
4. PDF-Dokument mit Optionsfeldern: Sie benötigen eine PDF-Datei, die Optionsfelder enthält (z. B. `RadioButton.pdf`).
5. Aspose.PDF Lizenz: Sie können eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) oder nutzen Sie eine kostenlose Testversion von Aspose.

## Namespaces importieren

Um mit Aspose.PDF für .NET zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren:

```csharp
using System;
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
```

Lassen Sie uns nun in das Schritt-für-Schritt-Tutorial zur Auswahl eines Optionsfelds in einem PDF-Formular eintauchen.

## Schritt 1: Öffnen Sie das PDF-Dokument

Der erste Schritt besteht darin, das PDF-Dokument mit den Optionsfeldern zu laden. Dies können Sie mit dem `Document` Klasse aus der Aspose.PDF-Bibliothek. So geht's:

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Öffnen Sie das Dokument
Document pdfDocument = new Document(dataDir + "RadioButton.pdf");
```

In diesem Beispiel laden wir eine PDF-Datei mit dem Namen `RadioButton.pdf`. Ersetzen `"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad zur Datei.

## Schritt 2: Zugriff auf das Optionsfeld

Nachdem das Dokument geladen ist, besteht der nächste Schritt darin, auf die Formularfelder zuzugreifen. Konkret möchten wir mit einer Optionsfeldgruppe interagieren. Der Zugriff auf das Optionsfeld erfolgt über `Form` Eigentum der `pdfDocument` Objekt.

Hier ist der Code für den Zugriff auf ein Optionsfeld namens `radio`:

```csharp
// Holen Sie sich ein Feld
RadioButtonField radioField = pdfDocument.Form["radio"] as RadioButtonField;
```

In diesem Beispiel gehen wir davon aus, dass das Optionsfeld im PDF-Formular den Namen `radio`Sollte das Feld in Ihrem Dokument einen anderen Namen haben, müssen Sie diesen entsprechend anpassen.

## Schritt 3: Wählen Sie ein Optionsfeld aus der Gruppe

Optionsfelder in Formularen sind in der Regel Teil einer Gruppe, aus der Sie eine Option auswählen können. Um ein Optionsfeld programmgesteuert auszuwählen, müssen Sie seinen Index innerhalb der Gruppe angeben. 

So legen Sie die Auswahl auf die zweite Option in der Gruppe fest:

```csharp
// Geben Sie den Index des Optionsfelds aus der Gruppe an
radioField.Selected = 2;
```

Der Index beginnt bei `0`, daher ist in diesem Fall die zweite Schaltfläche in der Gruppe ausgewählt.

## Schritt 4: Speichern Sie die aktualisierte PDF-Datei

Nach Auswahl des Optionsfelds müssen die Änderungen in einer neuen PDF-Datei gespeichert werden. Sie können das aktualisierte Dokument in einer neuen Datei speichern, indem Sie einen anderen Ausgabepfad angeben:

```csharp
dataDir = dataDir + "SelectRadioButton_out.pdf";

// Speichern Sie die PDF-Datei
pdfDocument.Save(dataDir);

Console.WriteLine("\nRadioButton from group selected successfully.\nFile saved at " + dataDir);
```

Dieser Code speichert das geänderte PDF als `SelectRadioButton_out.pdf` im selben Verzeichnis, in dem sich das Originaldokument befindet.

## Abschluss

Und da haben Sie es! In dieser Schritt-für-Schritt-Anleitung haben Sie gelernt, wie Sie mit Aspose.PDF für .NET programmgesteuert ein Optionsfeld in einem PDF-Dokument auswählen. Dieser Vorgang kann äußerst nützlich sein, wenn Sie Formularinteraktionen in großen Dokumenten automatisieren oder Skripts zum automatischen Ausfüllen von Formularen erstellen.

## Häufig gestellte Fragen

### Kann ich mit dieser Methode auch Kontrollkästchen auswählen?  
Ja, Aspose.PDF für .NET unterstützt die Interaktion mit verschiedenen Formularfeldern, einschließlich Kontrollkästchen, Textfeldern und mehr. Sie können ähnliche Methoden verwenden, um Kontrollkästchen zu bearbeiten.

### Was passiert, wenn das PDF das angegebene Optionsfeld nicht enthält?  
Wenn das angegebene Optionsfeld nicht vorhanden ist, erhalten Sie einen Fehler, den Sie mit einem Try-Catch-Block abfangen können, um die Ausnahme ordnungsgemäß zu verarbeiten.

### Kann ich mehrere Optionsfelder gleichzeitig auswählen?  
Nein, Optionsfelder erlauben nur eine Auswahl pro Gruppe. Wenn Sie mehrere Auswahlmöglichkeiten benötigen, sollten Sie stattdessen Kontrollkästchen verwenden.

### Ist es möglich, das aktuell ausgewählte Optionsfeld zu lesen?  
Ja, Sie können überprüfen, welches Optionsfeld aktuell ausgewählt ist, indem Sie die `Selected` Eigentum der `RadioButtonField` Objekt.

### Benötige ich eine Lizenz, um Aspose.PDF für .NET zu verwenden?  
Ja, Aspose.PDF benötigt eine Lizenz für die volle Funktionalität. Sie erhalten eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) oder verwenden Sie eine [kostenlose Testversion](https://releases.aspose.com/) um loszulegen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}