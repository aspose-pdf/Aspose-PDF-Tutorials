---
"description": "Erfahren Sie in dieser vollständigen Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.PDF für .NET Bilder in der XImage-Sammlung speichern."
"linktitle": "Bild in XImage-Sammlung speichern"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Bild in XImage-Sammlung speichern"
"url": "/de/net/programming-with-images/store-image-in-ximage-collection/"
"weight": 290
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bild in XImage-Sammlung speichern

## Einführung

Im heutigen digitalen Zeitalter ist die programmgesteuerte Bearbeitung von Dokumenten für viele Anwendungen unerlässlich. Aspose.PDF für .NET ermöglicht Entwicklern die mühelose Arbeit mit PDF-Dateien, verbessert Arbeitsabläufe und ermöglicht die Erstellung dynamischer Inhalte. In diesem Leitfaden erläutern wir die Speicherung eines Bildes in der XImage-Sammlung, einer wichtigen Funktion, mit der Sie visuelle Elemente direkt in Ihre PDFs einbetten können. Bereit für die Erstellung beeindruckender Inhalte?

## Voraussetzungen

Bevor wir uns in den Code und die Prozesse vertiefen, müssen Sie sicherstellen, dass einige Dinge vorhanden sind:

- .NET-Umgebung: Das .NET Framework sollte auf Ihrem Computer installiert sein. Wählen Sie die passende Version entsprechend Ihren Projektanforderungen.
- Aspose.PDF für .NET: Stellen Sie sicher, dass Sie die Aspose.PDF-Bibliothek haben. Sie können sie herunterladen von [Hier](https://releases.aspose.com/pdf/net/) oder starten Sie mit einer kostenlosen Testversion [Hier](https://releases.aspose.com/).
- Bilddatei: Sie benötigen außerdem eine Bilddatei (z. B. JPG oder PNG), die Sie im PDF speichern möchten. Für dieses Beispiel verwenden wir die Datei „aspose-logo.jpg“.
- Grundlegende Kenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie problemlos weitermachen.

## Pakete importieren

Um Aspose.PDF für .NET nutzen zu können, müssen Sie die erforderlichen Namespaces importieren. Dieser Schritt legt den Grundstein für die Nutzung aller Funktionen der Bibliothek.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Operators;
```

Durch das Importieren dieser Namespaces aktivieren Sie verschiedene Funktionen in Aspose.PDF, darunter Dokumenterstellung, Bildverarbeitung und mehr.

Lassen Sie uns dies in überschaubare Schritte unterteilen, damit Sie es leichter nachvollziehen können.

## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein

Was müssen Sie als Erstes tun? Definieren Sie, wo Ihre Dokumente gespeichert werden sollen. Richten Sie eine Variable ein, die den Pfad zu Ihrem Dokumentverzeichnis enthält. Dort wird Ihre PDF-Datei gespeichert.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Ersetzen Sie es durch Ihr tatsächliches Dokumentverzeichnis.
```

## Schritt 2: Initialisieren des Dokuments

Jetzt ist es an der Zeit, ein neues PDF-Dokument zu erstellen. In diesem Schritt wird Ihr PDF zum Leben erweckt. 

```csharp
Aspose.Pdf.Document document = new Document();
```

Hier instanziieren wir ein neues Dokumentobjekt, das als Leinwand dient.

## Schritt 3: Eine neue Seite hinzufügen

Jedes Meisterwerk braucht eine Leinwand, oder? In unserem Fall benötigen wir eine Seite, auf der wir innerhalb des Dokuments arbeiten können.

```csharp
document.Pages.Add();
Page page = document.Pages[1]; // Holen Sie sich die erste Seite.
```

Wir fügen unserem Dokument eine neue Seite hinzu. Nun bearbeiten wir diese Seite.

## Schritt 4: Laden Sie die Bilddatei

Als Nächstes müssen Sie das Bild in Ihr Programm laden. Dieser Schritt ähnelt dem Öffnen eines Buches zum Lesen: Sie müssen auf den Inhalt zugreifen, bevor Sie ihn verwenden können.

```csharp
using (FileStream imageStream = new FileStream(dataDir + "aspose-logo.jpg", FileMode.Open))
{
```

Diese Zeile öffnet die Bilddatei als Stream, sodass wir sie bearbeiten und in das PDF einbetten können.

## Schritt 5: Fügen Sie das Bild zu den Seitenressourcen hinzu

Jetzt, da das Bild einsatzbereit ist, ist es an der Zeit, es zu den Seitenressourcen hinzuzufügen und dem PDF im Wesentlichen zu sagen: „Hey, ich habe ein cooles Bild, an das du dich erinnern sollst!“

```csharp
page.Resources.Images.Add(imageStream, ImageFilterType.Flate);
XImage ximage = page.Resources.Images[page.Resources.Images.Count];
```

Dieser Code übernimmt die schwere Arbeit, das Bild zum PDF hinzuzufügen und es einem `XImage` Variable, auf die wir später verweisen können.

## Schritt 6: Bereiten Sie sich auf das Zeichnen des Bildes vor

Jetzt kommt der spannende Teil: die Positionierung des Bildes auf der Seite. Legen Sie die Koordinaten fest, damit das Bild genau dort platziert wird, wo Sie es haben möchten.

```csharp
page.Contents.Add(new GSave());
```

Diese Zeile speichert den Grafikzustand für eine spätere Wiederherstellung. Es ist, als würden wir einen Schnappschuss davon machen, wie alles eingerichtet ist, bevor wir etwas ändern.

## Schritt 7: Bildposition und -größe festlegen

Legen Sie nun fest, wie groß und wo Sie Ihr Bild platzieren möchten:

```csharp
int lowerLeftX = 0;
int lowerLeftY = 0;
int upperRightX = 600;
int upperRightY = 600;
Aspose.Pdf.Rectangle rectangle = new Aspose.Pdf.Rectangle(lowerLeftX, lowerLeftY, upperRightX, upperRightY);
```

Dieser Codeblock legt die Abmessungen des Rechtecks fest, in das Ihr Bild passt, und gibt ihm damit im Wesentlichen einen Platz auf Ihrer Seite.

## Schritt 8: Erstellen einer Transformationsmatrix 

Um die Platzierung des Bildes zu steuern, definieren wir eine Transformationsmatrix. Diese bestimmt, wie das Bild an den Zielkoordinaten angezeigt wird.

```csharp
Matrix matrix = new Matrix(new double[] { rectangle.URX - rectangle.LLX, 0, 0, rectangle.URY - rectangle.LLY, rectangle.LLX, rectangle.LLY });
```

Stellen Sie sich das so vor, als würden Sie vor Ihrer Reise eine Karte zeichnen. So können Sie bestimmen, wie das Bild auf der Seite angezeigt wird.

## Schritt 9: Platzieren Sie das Bild auf der Seite

Jetzt ist es an der Zeit, dem PDF mitzuteilen, wo das Bild abgelegt werden soll.

```csharp
page.Contents.Add(new ConcatenateMatrix(matrix));
page.Contents.Add(new Do(ximage.Name));
page.Contents.Add(new GRestore());
```

Hier fügen wir dem Inhaltsstrom des PDFs Befehle hinzu, die das Bild tatsächlich entsprechend der Matrix zeichnen, die wir gerade erstellt haben.

## Schritt 10: Speichern Sie das Dokument

Endlich können wir unser Meisterwerk speichern! Dies ist der Moment, in dem all Ihre harte Arbeit zu einem greifbaren Ergebnis zusammenfließt.

```csharp
document.Save(dataDir + "FlateDecodeCompression.pdf");
```

Sie haben Aspose.PDF angewiesen, das Dokument unter dem angegebenen Dateinamen zu speichern. Wenn Sie diesen Code ausführen, finden Sie Ihre neu erstellte PDF-Datei mit dem eingebetteten Bild im angegebenen Verzeichnis.

## Abschluss

Und da haben Sie es! Sie haben gelernt, wie Sie mit Aspose.PDF für .NET ein Bild Punkt für Punkt in der XImage-Sammlung speichern. Ist es nicht schön zu sehen, wie Ihr Code Gestalt annimmt und etwas Nützliches generiert? Egal, ob Sie Anwendungen erstellen oder Berichte automatisieren möchten, dieser Leitfaden bietet Ihnen eine hervorragende Grundlage. Denken Sie daran: Die Leistungsfähigkeit von Aspose.PDF kann Sie bei einer Vielzahl von Aufgaben unterstützen, die über diese hinausgehen. Entdecken Sie es also weiter!

## Häufig gestellte Fragen

### Welche Dateiformate werden für Bilder in Aspose.PDF unterstützt?
Aspose.PDF unterstützt verschiedene Bildformate, darunter JPG, PNG, BMP und GIF.

### Kann ich die Größe des Bildes beim Hinzufügen zum PDF ändern?
Ja, durch Anpassen der im Rechteck definierten Koordinaten können Sie die Größe des im PDF angezeigten Bildes ändern.

### Benötige ich eine Lizenz, um Aspose.PDF zu verwenden?
Aspose bietet eine kostenlose Testversion und verschiedene Kaufoptionen. Sie finden sie [Hier](https://purchase.aspose.com/buy).

### Wie erhalte ich Unterstützung, wenn Probleme auftreten?
Sie können Hilfe von der Aspose-Community suchen [Hier](https://forum.aspose.com/c/pdf/10).

### Gibt es eine Möglichkeit, die dem PDF hinzugefügten Bilder zu komprimieren?
Ja, wenn Sie Bilder zum PDF hinzufügen, können Sie den Bildfiltertyp angeben, um Komprimierungsmethoden wie Flate zu verwenden.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}