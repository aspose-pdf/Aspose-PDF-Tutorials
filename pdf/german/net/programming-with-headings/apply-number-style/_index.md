---
"description": "Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.PDF für .NET verschiedene Zahlenstile (römische Ziffern, alphabetisch) auf Überschriften in einer PDF-Datei anwenden."
"linktitle": "Zahlenstil in PDF-Datei anwenden"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Zahlenstil in PDF-Datei anwenden"
"url": "/de/net/programming-with-headings/apply-number-style/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zahlenstil in PDF-Datei anwenden

## Einführung

Mussten Sie Ihren PDF-Dokumenten schon einmal ansprechend nummerierte Listen hinzufügen? Ob Sie juristische Dokumente, Berichte oder Präsentationen formatieren – korrekte Nummerierungsstile sind für die Organisation von Informationen unerlässlich. Mit Aspose.PDF für .NET können Sie verschiedene Nummerierungsstile auf die Überschriften Ihrer PDF-Datei anwenden und so gut strukturierte und professionelle Dokumente erstellen. 

## Voraussetzungen

Bevor wir uns in die Programmierung stürzen, schauen wir uns an, was Sie brauchen:

1. Aspose.PDF für .NET: Laden Sie die neueste Version von Aspose.PDF herunter von [Hier](https://releases.aspose.com/pdf/net/).
2. Entwicklungsumgebung: Stellen Sie sicher, dass Sie über Visual Studio oder eine andere .NET-kompatible IDE verfügen.
3. .NET Framework: Stellen Sie sicher, dass Sie .NET Framework 4.0 oder höher installiert haben.
4. Lizenz: Sie können eine temporäre Lizenz von [Hier](https://purchase.aspose.com/temporary-license/) oder erkunden Sie die [kostenlose Testversion](https://releases.aspose.com/) Optionen.

## Pakete importieren

Stellen Sie zunächst sicher, dass Sie die folgenden Namespaces in Ihr Projekt importiert haben:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## Schritt 1: Einrichten des Dokuments

Beginnen wir mit der Erstellung eines neuen PDF-Dokuments und der Konfiguration seiner Seiteneinstellungen. Wir legen die Seitengröße und die Ränder fest, um das Layout unseres Inhalts zu steuern.

Erklärung: In diesem Schritt richten wir die Grundstruktur des PDFs ein, einschließlich der Definition der Seitengröße, Höhe und Ränder für eine einheitliche Formatierung.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDoc = new Document();

// Festlegen von Seitenabmessungen und Rändern
pdfDoc.PageInfo.Width = 612.0;
pdfDoc.PageInfo.Height = 792.0;
pdfDoc.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfDoc.PageInfo.Margin.Left = 72;
pdfDoc.PageInfo.Margin.Right = 72;
pdfDoc.PageInfo.Margin.Top = 72;
pdfDoc.PageInfo.Margin.Bottom = 72;
```

Dadurch erhält Ihr Dokument eine Standardseitengröße, die einer Seite im Format 8,5 x 11 Zoll entspricht, und einen Rand von 72 Punkten (oder 1 Zoll) auf allen Seiten.

## Schritt 2: Hinzufügen einer Seite zum PDF

Als nächstes fügen wir dem PDF-Dokument eine neue Seite hinzu, auf der wir später die Nummerierungsstile anwenden.

Erklärung: Jedes PDF benötigt Seiten! Dieser Schritt fügt dem PDF eine leere Seite hinzu und legt die Ränder entsprechend den Einstellungen auf Dokumentebene fest.

```csharp
// Dem PDF-Dokument eine neue Seite hinzufügen
Aspose.Pdf.Page pdfPage = pdfDoc.Pages.Add();
pdfPage.PageInfo.Width = 612.0;
pdfPage.PageInfo.Height = 792.0;
pdfPage.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfPage.PageInfo.Margin.Left = 72;
pdfPage.PageInfo.Margin.Right = 72;
pdfPage.PageInfo.Margin.Top = 72;
pdfPage.PageInfo.Margin.Bottom = 72;
```

## Schritt 3: Erstellen Sie eine schwebende Box

Mit einer FloatingBox können Sie Inhalte (wie Text oder Überschriften) in einem Feld platzieren, das sich unabhängig vom Seitenfluss verhält. Dies ist nützlich, wenn Sie die vollständige Kontrolle über das Layout Ihrer Inhalte haben möchten.

Erklärung: Hier richten wir eine FloatingBox ein, die die Überschriften enthält, auf die Zahlenstile angewendet werden.

```csharp
// Erstellen Sie eine FloatingBox für strukturierte Inhalte
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox();
floatBox.Margin = pdfPage.PageInfo.Margin;
pdfPage.Paragraphs.Add(floatBox);
```

## Schritt 4: Fügen Sie die erste Überschrift mit römischen Ziffern hinzu

Jetzt kommt der spannende Teil! Fügen wir die erste Überschrift mit römischen Kleinbuchstaben hinzu.

Erklärung: Wir wenden den Stil NumberingStyle.NumeralsRomanLowercase auf die Überschrift an, wodurch die Nummerierung in römischen Ziffern (i, ii, iii usw.) angezeigt wird.

```csharp
// Erstellen Sie die erste Überschrift mit römischen Ziffern
Aspose.Pdf.Heading heading = new Aspose.Pdf.Heading(1);
heading.IsInList = true;
heading.StartNumber = 1;
heading.Text = "List 1";
heading.Style = NumberingStyle.NumeralsRomanLowercase;
heading.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading);
```

## Schritt 5: Fügen Sie eine zweite römische Ziffernüberschrift hinzu

Zu Demonstrationszwecken fügen wir eine zweite Überschrift mit römischen Zahlen hinzu, aber dieses Mal beginnen wir bei 13.

Erklärung: Mit der Eigenschaft „StartNumber“ können Sie die Nummerierung mit einer benutzerdefinierten Zahl beginnen – in diesem Fall beginnen wir bei 13.

```csharp
// Erstellen Sie eine zweite Überschrift, beginnend bei der römischen Zahl 13
Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
heading2.IsInList = true;
heading2.StartNumber = 13;
heading2.Text = "List 2";
heading2.Style = NumberingStyle.NumeralsRomanLowercase;
heading2.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading2);
```

## Schritt 6: Fügen Sie eine Überschrift mit alphabetischer Nummerierung hinzu

Zur Abwechslung fügen wir eine dritte Überschrift hinzu, dieses Mal verwenden wir jedoch eine alphabetische Nummerierung in Kleinbuchstaben (a, b, c usw.).

Erklärung: Durch Ändern des Nummerierungsstils in „LettersLowercase“ können wir unseren Überschriften eine alphabetische Nummerierung zuweisen.

```csharp
// Erstellen Sie eine Überschrift mit alphabetischer Nummerierung
Aspose.Pdf.Heading heading3 = new Aspose.Pdf.Heading(2);
heading3.IsInList = true;
heading3.StartNumber = 1;
heading3.Text = "the value, as of the effective date of the plan, of property to be distributed under the plan on account of each allowed";
heading3.Style = NumberingStyle.LettersLowercase;
heading3.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading3);
```

## Schritt 7: Speichern der PDF

Nachdem Sie alle Überschriften- und Nummerierungsstile angewendet haben, speichern wir die PDF-Datei im gewünschten Verzeichnis.

Erklärung: Dieser Schritt speichert die PDF-Datei mit allen formatierten Überschriften und den angewendeten Nummerierungsstilen.

```csharp
// Speichern Sie das PDF-Dokument
dataDir = dataDir + "ApplyNumberStyle_out.pdf";
pdfDoc.Save(dataDir);
Console.WriteLine("\nNumber style applied successfully in headings.\nFile saved at " + dataDir);
```

## Abschluss

Und fertig! Sie haben mit Aspose.PDF für .NET erfolgreich Nummerierungsstile – römische Ziffern und alphabetische Zahlen – auf Überschriften in einer PDF-Datei angewendet. Die Flexibilität von Aspose.PDF bei der Steuerung von Seitenlayout, Nummerierungsstilen und Inhaltspositionierung bietet Ihnen ein leistungsstarkes Toolset für die Erstellung übersichtlicher, professioneller PDF-Dokumente.

## Häufig gestellte Fragen

### Kann ich auf dasselbe PDF-Dokument unterschiedliche Nummerierungsstile anwenden?  
Ja, mit Aspose.PDF für .NET können Sie verschiedene Nummerierungsstile wie römische Ziffern, arabische Ziffern und alphabetische Nummerierungen im selben Dokument mischen.

### Wie kann ich die Startnummer für Überschriften anpassen?  
Sie können die Startnummer für jede Überschrift mit dem `StartNumber` Eigentum.

### Gibt es eine Möglichkeit, die Nummerierungsreihenfolge zurückzusetzen?  
Ja, Sie können die Nummerierung zurücksetzen, indem Sie die `StartNumber` Eigenschaft für jede Überschrift.

### Kann ich Überschriften zusätzlich zur Nummerierung auch fett oder kursiv formatieren?  
Absolut! Sie können Überschriftenstile anpassen, indem Sie Eigenschaften wie Schriftart, Größe, Fettdruck und Kursivschrift mithilfe der `TextState` Objekt.

### Wie erhalte ich eine temporäre Lizenz für Aspose.PDF?  
Eine vorläufige Lizenz erhalten Sie bei [Hier](https://purchase.aspose.com/temporary-license/) um Aspose.PDF ohne Einschränkungen zu testen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}