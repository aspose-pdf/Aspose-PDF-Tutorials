---
"description": "Erfahren Sie in dieser Schritt-für-Schritt-Anleitung voller praktischer Beispiele, wie Sie mit Aspose.PDF für .NET mühelos Strichtext in PDF-Dateien einfügen."
"linktitle": "Strichtext in PDF-Datei füllen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Strichtext in PDF-Datei füllen"
"url": "/de/net/programming-with-stamps-and-watermarks/fill-stroke-text/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Strichtext in PDF-Datei füllen

## Einführung

Wollten Sie schon immer eine PDF-Datei anpassen, um sie hervorzuheben? Vielleicht möchten Sie ein auffälliges Wasserzeichen oder einen auffälligen Stempel hinzufügen, der ein wichtiges Dokument unverwechselbar macht. Mit Aspose.PDF für .NET können Sie Strichtext in einer PDF-Datei ganz einfach füllen und so einen künstlerischen Akzent setzen, der ins Auge fällt. Im heutigen Tutorial zeigen wir Ihnen, wie Sie Strichtext in einer PDF-Datei mit C# füllen. Am Ende haben Sie ein solides Verständnis dafür, wie Sie PDF-Dateien wie ein Profi bearbeiten.

## Voraussetzungen

Bevor wir uns in die Codierung stürzen, müssen Sie einige Dinge vorbereitet haben, damit dieses Tutorial ein Kinderspiel wird:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist, da wir C#-Code schreiben werden.
2. Aspose.PDF Bibliothek: Stellen Sie sicher, dass Sie die Aspose.PDF für .NET Bibliothek heruntergeladen haben. Sie können es greifen [Hier](https://releases.aspose.com/pdf/net/).
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie das Tutorial leichter verstehen.
4. Beispiel-PDF-Datei: Sie benötigen eine Beispiel-PDF-Datei (`input.pdf`) zu Testzwecken. Sie können eine einfache Datei erstellen oder eine vorhandene PDF-Datei verwenden.

Nachdem wir nun alles vorbereitet haben, können wir uns an die Einzelheiten des Ausfüllens des Strichtexts in Ihrer PDF-Datei machen.

## Pakete importieren

Zunächst müssen wir die notwendigen Pakete importieren. Hier ist eine kurze Übersicht über die wichtigsten Importe für unser Projekt:

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Diese Pakete ermöglichen uns die Nutzung der robusten Funktionen der Aspose.PDF-Bibliothek.

Lassen Sie uns die Hauptaufgabe in klare Schritte unterteilen. Wenn Sie diese Schritte befolgen, können Sie Ihre PDF-Dateien ganz einfach mit Strichtext füllen. 

## Schritt 1: Richten Sie Ihre Umgebung ein

Stellen Sie zunächst sicher, dass in Ihrem Visual Studio-Projekt alles korrekt eingerichtet ist. Erstellen Sie ein neues Projekt oder wählen Sie ein vorhandenes aus. Wenn Sie Hilfe benötigen, gehen Sie wie folgt vor:

1. Öffnen Sie Visual Studio.
2. Erstellen Sie ein neues C#-Projekt (z. B. eine Konsolenanwendung).
3. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt und wählen Sie „NuGet-Pakete verwalten“ aus.
4. Suchen nach `Aspose.PDF` und installieren Sie es.

## Schritt 2: Definieren Sie Ihr Dokumentverzeichnis

Jede Reise braucht einen Ausgangspunkt, und in unserem Fall ist dies das Dokumentenverzeichnis, in dem die Eingabe- und Ausgabedateien gespeichert werden. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersetzen `"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad, in dem sich Ihre Eingabe-PDF-Datei befindet. 

## Schritt 3: Erstellen Sie das TextState-Objekt

In diesem Schritt beginnen Sie mit der Definition der Eigenschaften des Textes, den Sie hinzufügen möchten. 

```csharp
TextState ts = new TextState();
```

Der `TextState` Das Objekt enthält die Stiloptionen für Ihren Strichtext.

## Schritt 4: Legen Sie die Farbe für den Strich fest

Als Nächstes möchten Sie die Strichfarbe für Ihren Text definieren. 

```csharp
ts.StrokingColor = Color.Gray;
```

In diesem Code verwenden wir Grau für den Strich. Sie können die Farbe gerne Ihren Wünschen entsprechend ändern!

## Schritt 5: Rendering-Modus konfigurieren

Um sicherzustellen, dass Ihr Text wie gewünscht angezeigt wird, legen Sie den Rendering-Modus fest:

```csharp
ts.RenderingMode = TextRenderingMode.StrokeText;
```

Dies weist die Aspose-Bibliothek an, dass wir mit Strichtext arbeiten.

## Schritt 6: Laden Sie Ihr Eingabe-PDF-Dokument

Jetzt ist es an der Zeit, die PDF-Datei zu laden, die Sie ändern möchten. 

```csharp
Facades.PdfFileStamp fileStamp = new Facades.PdfFileStamp(new Aspose.Pdf.Document(dataDir + "input.pdf"));
```

Stellen Sie sicher, dass Ihr Eingabe-PDF (`input.pdf`) befindet sich im in den vorherigen Schritten definierten Dokumentenverzeichnis.

## Schritt 7: Erstellen Sie ein Stempelobjekt

Erstellen Sie als Nächstes einen Stempel, der Ihren Strichtext enthält. 

```csharp
Aspose.Pdf.Facades.Stamp stamp = new Aspose.Pdf.Facades.Stamp();
```

Dieser Stempel wird verwendet, um Ihren Text auf das PDF zu legen.

## Schritt 8: Definieren Sie den zu stempelnden Text

Sie müssen angeben, welchen Text Sie der PDF-Datei hinzufügen möchten:

```csharp
stamp.BindLogo(new Facades.FormattedText("PAID IN FULL", System.Drawing.Color.Gray, "Arial", Facades.EncodingType.Winansi, true, 78));
```

Hier fügen wir den Text „VOLLSTÄNDIG BEZAHLT“ zusammen mit den entsprechenden Stilattributen hinzu. Passen Sie ihn Ihren Anforderungen entsprechend an!

## Schritt 9: Binden Sie den Textstatus

Binden Sie nun die `TextState` Sie haben zuvor den Stempel definiert. 

```csharp
stamp.BindTextState(ts);
```

In diesem Schritt werden alle Stile wie Farbe und Rendering-Modus auf Ihren Text angewendet.

## Schritt 10: Position des Stempels festlegen

Bestimmen Sie, wo Ihr Stempel in der PDF-Datei erscheinen soll:

```csharp
stamp.SetOrigin(100, 100);
```

Die Argumente `(100, 100)` Geben Sie die X- und Y-Koordinaten (in Punkten) für den Ursprung des Textes an. Passen Sie diese Werte an, um Ihren Text optimal zu positionieren!

## Schritt 11: Opazität und Rotation konfigurieren

Hier können Sie mit der Darstellung Ihres Textes experimentieren:

```csharp
stamp.Opacity = 5;
stamp.BlendingSpace = Facades.BlendingColorSpace.DeviceRGB;
stamp.Rotation = 45.0F;
```

In diesem Fall verleihen ein Deckkraftwert und ein Drehwinkel von 45 Grad Ihrem Text eine einzigartige Note. Sie können diese Einstellungen gerne für verschiedene Effekte anpassen.

## Schritt 12: Stempel zum PDF hinzufügen

Dies ist der entscheidende Schritt, in dem wir schließlich unseren Stempel, der den Strichtext enthält, zum PDF hinzufügen:

```csharp
fileStamp.AddStamp(stamp);
```

Und schon ist Ihr Text bereit, eine Aussage zu machen!

## Schritt 13: Speichern und Schließen des Dokuments

Speichern Sie abschließend Ihre Änderungen und stellen Sie sicher, dass alles ordnungsgemäß bereinigt wurde. 

```csharp
fileStamp.Save(dataDir + "output_out.pdf");
fileStamp.Close();
```

Ihre neu geänderte PDF-Datei mit dem Strichtext wird gespeichert als `output_out.pdf` in Ihrem Dokumentverzeichnis. 

## Abschluss

Und da haben Sie es! Mit diesen einfachen Schritten können Sie mit Aspose.PDF für .NET ganz einfach Strichtext in eine PDF-Datei einfügen. Ob für Geschäftsdokumente oder private Projekte – mit dieser Technik verleihen Sie Ihren PDFs eine einzigartige Note und lassen sie in jedem Papierstapel hervorstechen.

## Häufig gestellte Fragen

### Was ist Aspose.PDF für .NET?
Aspose.PDF für .NET ist eine Bibliothek, die es Entwicklern ermöglicht, PDF-Dateien programmgesteuert zu erstellen, zu bearbeiten und zu konvertieren.

### Kann ich Aspose.PDF kostenlos nutzen?
Ja, Aspose bietet eine kostenlose Testversion an. Sie können es bekommen [Hier](https://releases.aspose.com/).

### Muss ich für eine Lizenz bezahlen?
Während die Bibliothek eine kostenlose Testversion anbietet, kann eine temporäre Lizenz auch erworben werden bei [dieser Link](https://purchase.aspose.com/temporary-license/).

### Wo finde ich die Dokumentation?
Sie können auf die vollständige Dokumentation zugreifen [Hier](https://reference.aspose.com/pdf/net/).

### Gibt es Support, wenn ich auf Probleme stoße?
Absolut! Support erhalten Sie im Aspose-Forum [Hier](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}