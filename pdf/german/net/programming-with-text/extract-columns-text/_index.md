---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET Textspalten aus PDF-Dateien extrahieren. Diese Anleitung erläutert jeden Schritt anhand von Codebeispielen und Erklärungen."
"linktitle": "Spaltentext in PDF-Datei extrahieren"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Spaltentext in PDF-Datei extrahieren"
"url": "/de/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Spaltentext in PDF-Datei extrahieren

## Einführung

Arbeiten Sie mit PDF-Dateien und müssen Text in einem bestimmten Spaltenformat extrahieren? Ob Sie Rechnungen, Berichte oder strukturierte Dokumente verarbeiten – das präzise Extrahieren von Text aus einer PDF-Datei kann eine knifflige Angelegenheit sein. Hier kommt Aspose.PDF für .NET ins Spiel und vereinfacht den Prozess. In diesem Tutorial zeigen wir Ihnen, wie Sie mühelos Textspalten aus einer PDF-Datei extrahieren. 

## Voraussetzungen

Bevor wir uns in den Code vertiefen, wollen wir die wesentlichen Dinge besprechen, die Sie benötigen:

- Aspose.PDF für .NET: Stellen Sie sicher, dass Sie die neueste Version von Aspose.PDF für .NET installiert haben. Falls nicht, können Sie [Laden Sie es hier herunter](https://releases.aspose.com/pdf/net/).
- Entwicklungsumgebung: Sie benötigen Visual Studio oder eine andere .NET-Entwicklungsumgebung, um mit dem Code zu arbeiten.
- PDF-Dokument: Halten Sie ein Beispiel-PDF-Dokument bereit, vorzugsweise eines mit Textspalten, da wir Text daraus extrahieren werden.

Wenn Sie Aspose.PDF für .NET noch nicht installiert haben, können Sie sich eine [kostenlose Testversion](https://releases.aspose.com/) oder [eine Lizenz kaufen](https://purchase.aspose.com/buy) für alle Funktionen. Sie können auch eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license) falls erforderlich.

## Namespaces importieren

Um Aspose.PDF für .NET in Ihrem Projekt zu verwenden, müssen Sie die folgenden Namespaces importieren:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## Schritt-für-Schritt-Anleitung: Textspalten aus einer PDF-Datei extrahieren

Lassen Sie uns nun jeden Teil des Codes analysieren, um die Funktionsweise besser zu verstehen. Folgen Sie uns Schritt für Schritt, während wir jeden Abschnitt des Prozesses erklären.

## Schritt 1: Laden Sie das PDF-Dokument

Als erstes müssen Sie Ihre PDF-Datei in das `Document` Objekt. So interagiert Aspose.PDF mit Ihrem Dokument.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

In diesem Schritt definieren wir lediglich das Verzeichnis, in dem Ihr PDF-Dokument gespeichert ist. Ersetzen Sie `"YOUR DOCUMENT DIRECTORY"` mit dem Pfad zu Ihrer lokalen PDF-Datei. Die `Document` Objekt lädt das PDF in den Speicher und macht es für die weitere Verarbeitung zugänglich.

## Schritt 2: Richten Sie den Textfragmentabsorber ein

Als nächstes verwenden wir ein `TextFragmentAbsorber` um den gesamten Text aus der PDF-Datei zu absorbieren oder zu erfassen. Diese Absorberklasse dient zum Extrahieren von Textfragmenten aus bestimmten Bereichen Ihrer PDF-Datei und eignet sich daher ideal zum Extrahieren von Textspalten.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

Hier erstellen wir eine Instanz von `TextFragmentAbsorber` und wenden Sie es auf alle Seiten des PDFs an, indem Sie `Accept()`. Der `TextFragmentCollection` speichert den extrahierten Text und aus dieser Sammlung können wir Text nach Bedarf bearbeiten oder extrahieren.

## Schritt 3: Passen Sie die Schriftgröße des extrahierten Textes an

Nachdem Sie die Textfragmente erfasst haben, möchten Sie möglicherweise deren Schriftgröße reduzieren, insbesondere wenn der Originaltext zu groß ist. In diesem Beispiel reduzieren wir die Schriftgröße um 70 %.

```csharp
foreach (TextFragment tf in tfc)
{
    // Reduzieren Sie die Schriftgröße um 70 %
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

Dieser Code durchläuft jede `TextFragment` in der Sammlung und reduziert die Schriftgröße um 70 %. Durch Anpassen der Schriftgröße lässt sich der extrahierte Text leichter verwalten, insbesondere wenn Sie ihn für verschiedene Zwecke formatieren.

## Schritt 4: Speichern Sie das Dokument in einem Memory Stream

Nach der Textbearbeitung speichern wir das PDF in einem `MemoryStream`Dadurch können wir das Dokument zur weiteren Verarbeitung im Speicher behalten, ohne es wieder auf die Festplatte schreiben zu müssen.

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

Hier speichern wir die PDF-Datei in einem Speicherstream und laden sie anschließend neu. Diese Methode ist nützlich, wenn Sie mit großen Dateien arbeiten und unnötige Festplattenoperationen vermeiden möchten.

## Schritt 5: Extrahieren Sie den gesamten Text mit Text Absorber

Nachdem wir das PDF vorbereitet haben, ist es Zeit, den Text zu extrahieren. Wir verwenden `TextAbsorber` um den gesamten Text aus dem Dokument zu erfassen.

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

In diesem Schritt wird `TextAbsorber` absorbiert den gesamten Text aus dem PDF und der extrahierte Text wird im `extractedText` Zeichenfolge. Hier geschieht die Magie – Ihre Textspalten liegen jetzt im Nur-Text-Format vor!

## Schritt 6: Speichern Sie den extrahierten Text in einer Datei

Abschließend speichern wir den extrahierten Text in einem `.txt` Datei für einfachen Zugriff und weitere Verwendung.

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

Dieser Code schreibt den extrahierten Text in eine neue `.txt` Datei und speichert sie im angegebenen Verzeichnis. In der Konsole wird eine Meldung angezeigt, die bestätigt, dass der Vorgang erfolgreich war.

## Abschluss

So, fertig! Das Extrahieren von Textspalten aus einer PDF-Datei mit Aspose.PDF für .NET ist einfacher als gedacht. Mit nur wenigen Codezeilen können Sie eine PDF-Datei laden, Text extrahieren, die Formatierung anpassen und die Ergebnisse in einer Textdatei speichern.

Diese Technik ist äußerst nützlich für die Verarbeitung strukturierter Dokumente wie Tabellen, Berichte oder anderer in Spalten organisierter Inhalte. Ob Sie die Datenextraktion automatisieren oder Massendokumente verarbeiten müssen – Aspose.PDF bietet die Tools für eine effiziente Umsetzung.

## Häufig gestellte Fragen

### Kann ich Text aus bestimmten Seiten einer PDF-Datei extrahieren?  
Ja! Sie können die `TextFragmentAbsorber` um bestimmte Seiten mit dem `pdfDocument.Pages[pageIndex].Accept(tfa);` Verfahren.

### Ist es möglich, Text aus nur einer Spalte in einem mehrspaltigen PDF zu extrahieren?  
Ja, aber Sie müssen mit den Koordinaten der Textfragmente arbeiten, indem Sie `TextFragment.Rectangle` um bestimmte Bereiche des Dokuments anzusprechen.

### Wie kann ich die Genauigkeit der Textextraktion verbessern?  
Für eine höhere Genauigkeit achten Sie auf eine klar definierte PDF-Struktur und vermeiden Sie Dokumente mit komplexen Layouts. Sie können auch die `TextFragmentAbsorber` um Text basierend auf Schriftarten, -größen oder -regionen zu extrahieren.

### Unterstützt Aspose.PDF die Textextraktion aus gescannten Dokumenten?  
Ja, aber Sie benötigen OCR-Technologie (Optical Character Recognition). Aspose bietet hierfür ebenfalls Tools an.

### Wie gehe ich mit großen PDF-Dateien mit Tausenden von Seiten um?  
Verarbeiten Sie große PDF-Dokumente in Abschnitten, indem Sie den Text jeweils von einigen Seiten extrahieren, um einen hohen Speicherverbrauch zu vermeiden.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}