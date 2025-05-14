---
"description": "Erfahren Sie, wie Sie mit dem Bradley-Algorithmus in Aspose.PDF für .NET PDF in TIFF konvertieren. Schritt-für-Schritt-Anleitung, Voraussetzungen und FAQs für eine reibungslose Konvertierung."
"linktitle": "Bradley-Algorithmus"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Bradley-Algorithmus"
"url": "/de/net/programming-with-images/bradley-algorithm/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bradley-Algorithmus

## Einführung

Die Arbeit mit PDF-Dateien erfordert manchmal mehr als nur das Lesen und Bearbeiten – Sie müssen sie möglicherweise in Bilder konvertieren. Eine leistungsstarke Möglichkeit, PDFs in TIFF-Bilder zu konvertieren, ist die Verwendung des Bradley-Algorithmus über die Aspose.PDF für .NET-Bibliothek. Diese Methode gewährleistet hochwertige Binärbilder, ideal für die Dokumentenarchivierung und andere spezielle Anwendungsfälle.

Dieses Tutorial führt Sie durch einen detaillierten, leicht verständlichen Prozess zur Konvertierung einer PDF-Seite in ein TIFF-Bild mit dem Bradley-Binarisierungsalgorithmus. Aspose.PDF für .NET vereinfacht diese Aufgabe und ermöglicht Ihnen die Automatisierung und Optimierung Ihrer Dokumenten-Workflows.

## Voraussetzungen

Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie zum Mitmachen brauchen:

- Aspose.PDF für .NET: Sie benötigen die Bibliothek. Laden Sie sie herunter von [Hier](https://releases.aspose.com/pdf/net/).
- Visual Studio (oder eine beliebige C#-IDE).
- Grundkenntnisse in C#.
- Eine gültige Lizenz oder ein [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) von Aspose.

## Pakete importieren

Stellen Sie zunächst sicher, dass Sie die erforderlichen Namespaces in Ihr Projekt importieren. Diese Bibliotheken bieten Ihnen die Werkzeuge, um PDF-Dokumente zu bearbeiten, ins TIFF-Format zu konvertieren und den Bradley-Binarisierungsalgorithmus anzuwenden.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Wir unterteilen den Vorgang in einfache Schritte, damit Sie ihn problemlos nachvollziehen können. Am Ende dieser Anleitung haben Sie mithilfe des Bradley-Algorithmus erfolgreich eine PDF-Seite in ein binäres TIFF-Bild konvertiert.

## Schritt 1: Dokumentverzeichnis festlegen

Im ersten Schritt geben Sie den Pfad zum Verzeichnis Ihres PDF-Dokuments an. Außerdem definieren Sie die Ausgabepfade für die zu generierenden TIFF-Bilder.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Pfad zu Ihrer PDF-Datei
```

Hier speichern Sie sowohl die PDF-Quelldatei als auch die konvertierten TIFF-Dateien. Stellen Sie sicher, dass das Verzeichnis korrekt eingestellt ist, damit der Code Dateien fehlerfrei lesen und schreiben kann.

## Schritt 2: Öffnen Sie das PDF-Dokument

Nachdem der Pfad festgelegt ist, öffnen Sie das zu konvertierende PDF-Dokument. Aspose.PDF für .NET erleichtert das Laden eines Dokuments zur weiteren Verarbeitung.

```csharp
Document pdfDocument = new Document(dataDir + "PageToTIFF.pdf");
```

Hier, `PageToTIFF.pdf` ist die Beispieldatei. Sie können sie durch eine beliebige PDF-Datei ersetzen. Das Dokumentobjekt enthält nun die PDF-Datei zur weiteren Bearbeitung.

## Schritt 3: Ausgabepfade für Bilder definieren

Als Nächstes geben Sie die Ausgabepfade für die generierten TIFF-Dateien an, einschließlich des Standard-TIFF und der binären Version.

```csharp
string outputImageFile = dataDir + "resultant_out.tif";
string outputBinImageFile = dataDir + "37116-bin_out.tif";
```

Durch die Trennung dieser Pfade erhalten Sie eine Datei für die Standard-TIFF-Konvertierung und eine andere für das binärisierte Bild nach Anwendung des Bradley-Algorithmus.

## Schritt 4: Erstellen eines Auflösungsobjekts

Bei der Konvertierung von PDFs in TIFF spielt die Auflösung eine entscheidende Rolle für die Bildqualität. Für unsere Zwecke stellen wir sie auf 300 DPI ein, um eine hochwertige Ausgabe zu gewährleisten.

```csharp
Resolution resolution = new Resolution(300);
```

Ein höherer DPI-Wert bedeutet eine bessere Bildschärfe, insbesondere bei Dokumenten, die gedruckt oder archiviert werden.

## Schritt 5: TIFF-Einstellungen konfigurieren

Als Nächstes müssen Sie die Einstellungen für das TIFF-Bild konfigurieren. Hier verwenden wir die LZW-Komprimierung und stellen die Farbtiefe auf 1 bpp (1 Bit pro Pixel) ein, um ein Binärbild zu erhalten.

```csharp
TiffSettings tiffSettings = new TiffSettings();
tiffSettings.Compression = CompressionType.LZW;
tiffSettings.Depth = Aspose.Pdf.Devices.ColorDepth.Format1bpp;
```

Indem wir die Tiefe auf 1 bpp einstellen, bereiten wir das Bild für die binäre Ausgabe vor. Die LZW-Komprimierung wurde gewählt, da sie die Dateigröße effizient reduziert, ohne Qualitätsverlust zu verursachen.

## Schritt 6: Erstellen Sie das TIFF-Gerät

Nun müssen Sie ein TIFF-Gerät erstellen, das die Konvertierung durchführt. Dieses Gerät verwendet die zuvor definierte Auflösung und TIFF-Einstellungen.

```csharp
TiffDevice tiffDevice = new TiffDevice(resolution, tiffSettings);
```

Das TIFF-Gerät ist das Herzstück dieser Operation. Es nimmt das PDF-Dokument entgegen und konvertiert jede Seite basierend auf Ihren vordefinierten Einstellungen in ein TIFF-Bild.

## Schritt 7: Konvertieren Sie die PDF-Seite in TIFF

Es ist Zeit, das PDF zu verarbeiten und die erste Seite in ein TIFF-Bild zu konvertieren. Die `Process` Mit dieser Methode können Sie einzelne Seiten oder das gesamte Dokument konvertieren. In diesem Beispiel konvertieren wir die erste Seite.

```csharp
tiffDevice.Process(pdfDocument, outputImageFile);
```

Sobald die Methode abgeschlossen ist, wird ein TIFF-Bild am zuvor definierten Speicherort gespeichert.

## Schritt 8: Wenden Sie den Bradley-Binarisierungsalgorithmus an

Jetzt kommt die Magie – der Bradley-Algorithmus! Dieser Algorithmus konvertiert das Graustufen-TIFF-Bild in ein Binärbild und optimiert es für Dokumentenerkennungssysteme.

```csharp
using (FileStream inStream = new FileStream(outputImageFile, FileMode.Open))
{
    using (FileStream outStream = new FileStream(outputBinImageFile, FileMode.Create))
    {
        tiffDevice.BinarizeBradley(inStream, outStream, 0.1);
    }
}
```

Die Methode BinarizeBradley verwendet zwei Dateiströme (Eingabe und Ausgabe) sowie einen Schwellenwert (hier `0.1`), der den Binärisierungsgrad bestimmt. Nach der Ausführung steht Ihnen ein perfekt binärisiertes Bild zur Verfügung.

## Schritt 9: Erfolgreiche Konvertierung bestätigen

Abschließend empfiehlt es sich, den Benutzer über den erfolgreichen Abschluss des Vorgangs zu informieren. Dies kann über eine einfache Konsolenausgabe erfolgen.

```csharp
System.Console.WriteLine("Conversion using Bradley algorithm performed successfully!");
```

Sobald dies gedruckt ist, wissen Sie, dass Ihre PDF-Seite erfolgreich in ein binäres TIFF-Bild konvertiert wurde!

## Abschluss

Fertig! Sie haben gelernt, wie Sie eine PDF-Seite in ein TIFF-Bild konvertieren und den Bradley-Binarisierungsalgorithmus mit Aspose.PDF für .NET anwenden. Dieser Prozess ist unerlässlich für die Dokumentenarchivierung, die optische Zeichenerkennung (OCR) und andere professionelle Anwendungen. Dank hoher Auflösung und effizienter Komprimierung stellen Sie sicher, dass Ihre Dokumentbilder klar und handlich sind.

## Häufig gestellte Fragen

### Was ist der Bradley-Algorithmus?
Der Bradley-Algorithmus ist eine Binärisierungstechnik, die Graustufenbilder in Binärbilder (Schwarzweiß) umwandelt, indem für jedes Pixel basierend auf seiner Umgebung ein adaptiver Schwellenwert bestimmt wird.

### Kann ich mit dieser Methode mehrere PDF-Seiten in TIFF konvertieren?
Ja, Sie können die `Process` Methode zum Konvertieren aller Seiten durch Durchlaufen der Seiten im Dokument.

### Was ist die optimale Auflösung für die Konvertierung von PDFs in TIFF?
Für qualitativ hochwertige Bilder werden im Allgemeinen 300 DPI empfohlen. Sie können diesen Wert jedoch Ihren Anforderungen entsprechend anpassen.

### Was bedeutet 1bpp in der Farbtiefe?
1bpp (1 Bit pro Pixel) bedeutet, dass das Bild schwarzweiß ist und jedes Pixel entweder vollständig schwarz oder vollständig weiß ist.

### Ist der Bradley-Algorithmus für OCR geeignet?
Ja, der Bradley-Algorithmus wird häufig bei der OCR-Vorverarbeitung verwendet, da er den Textkontrast in gescannten Dokumenten verbessert.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}