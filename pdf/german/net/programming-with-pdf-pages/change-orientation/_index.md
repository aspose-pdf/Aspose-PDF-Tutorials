---
"description": "Schritt-für-Schritt-Anleitung zum Ändern der Seitenausrichtung einer PDF-Datei mit Aspose.PDF für .NET. Einfach zu befolgen und in Ihren Projekten zu implementieren."
"linktitle": "Orientierung ändern"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Orientierung ändern"
"url": "/de/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Orientierung ändern

## Einführung

Haben Sie schon einmal mit einer PDF-Datei gekämpft, deren Seitenausrichtung einfach nicht stimmt? Vielleicht haben Sie es mit einem falsch gescannten oder erstellten Dokument zu tun, dessen Seiten gedreht werden müssen, um Sinn zu ergeben. Zum Glück bietet Aspose.PDF für .NET eine einfache und leistungsstarke Möglichkeit, PDF-Dateien auf nahezu jede erdenkliche Weise zu bearbeiten – einschließlich der Änderung der Seitenausrichtung. Egal, ob Sie von Hoch- auf Querformat oder umgekehrt wechseln möchten, diese Anleitung führt Sie Schritt für Schritt durch den Vorgang.

Wenn Sie also bereit sind, loszulegen und diese PDF-Seiten mühelos zu drehen, dann legen wir los!

## Voraussetzungen

Bevor wir uns mit den Details zum Ändern der Seitenausrichtung in Ihrem PDF befassen, wollen wir kurz besprechen, was Sie dafür benötigen:

- Aspose.PDF für .NET: Stellen Sie sicher, dass Sie die Aspose.PDF-Bibliothek für .NET installiert haben. Falls nicht, können Sie [Laden Sie es hier herunter](https://releases.aspose.com/pdf/net/).
- Eine .NET-Entwicklungsumgebung: Sie können Visual Studio, JetBrains Rider oder jede bevorzugte IDE für die Arbeit mit .NET verwenden.
- Grundkenntnisse in C#: Diese Anleitung ist zwar unkompliziert, aber mit einigen Grundkenntnissen in C# ist sie noch einfacher zu befolgen.
- Eine PDF-Datei: Das folgende Beispiel geht von einer mehrseitigen PDF-Datei aus. Falls Sie keine zur Hand haben, erstellen oder laden Sie eine Beispiel-PDF herunter.

Wenn Sie gerade erst anfangen, können Sie Aspose.PDF auch mit einem [kostenlose temporäre Lizenz](https://purchase.aspose.com/temporary-license/) bevor Sie sich entscheiden, [Kaufen Sie die Vollversion](https://purchase.aspose.com/buy).

## Namespaces importieren

Bevor Sie die Seitenausrichtung in Ihrer PDF-Datei ändern können, müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Stellen Sie sicher, dass Folgendes vorhanden ist:

```csharp
using System.IO;
using Aspose.Pdf;
```

Nachdem dies importiert wurde, können wir mit dem Hauptteil des Tutorials beginnen.

## Schritt 1: Laden Sie das PDF-Dokument

Als erstes müssen wir die PDF-Datei laden, die Sie ändern möchten. Sie können die `Document` Klasse aus dem Aspose.PDF-Namespace, um Ihr PDF zu öffnen.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Diese Zeile lädt das PDF aus dem angegebenen Verzeichnis. Ersetzen Sie `"YOUR DOCUMENT DIRECTORY"` mit dem tatsächlichen Pfad zu Ihrer Datei. Die `"input.pdf"` ist die PDF-Datei, deren Ausrichtung Sie ändern möchten.

## Schritt 2: Jede Seite durchlaufen

Nachdem wir das Dokument geladen haben, gehen wir nun jede Seite im PDF durch. Wir verwenden eine `foreach` Schleife, um jede Seite zu durchlaufen, sodass wir die Ausrichtungsänderung auf alle anwenden können.

```csharp
foreach (Page page in doc.Pages)
{
    // Bearbeiten Sie jede Seite
}
```

Diese Schleife durchläuft alle Seiten im Dokument.

## Schritt 3: Holen Sie sich die MediaBox der Seite

Jede Seite in einer PDF-Datei hat eine `MediaBox` , das die Seitenränder definiert. Wir müssen darauf zugreifen, um die aktuelle Ausrichtung zu bestimmen und zu ändern.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

Der `MediaBox` gibt uns die Abmessungen der Seite, wie etwa ihre Breite, Höhe und Positionierung.

## Schritt 4: Breite und Höhe vertauschen

Um die Seitenausrichtung von Hochformat auf Querformat oder von Querformat auf Hochformat zu ändern, vertauschen wir einfach die Werte für Breite und Höhe. Dadurch werden die Abmessungen der Seite angepasst.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

Dieser Code vertauscht Höhe und Breite und positioniert die untere linke Ecke neu (`LLY`), damit der Inhalt nach der Drehung ordentlich passt.

## Schritt 5: Aktualisieren Sie die MediaBox und CropBox

Nachdem wir nun die neue Höhe und Breite haben, wenden wir die Änderungen auf die Seite an. `MediaBox` Und `CropBox`. Der `CropBox` ist wichtig, wenn das Originaldokument einen Satz hatte, um sicherzustellen, dass die gesamte Seite korrekt angezeigt wird.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

Dieser Schritt ändert die Größe der Seite basierend auf den neuen Abmessungen, die wir gerade berechnet haben.

## Schritt 6: Drehen Sie die Seite

Abschließend legen wir den Drehwinkel der Seite fest. Aspose.PDF macht dies kinderleicht. Wir können die Seite um 90 Grad drehen, um vom Hoch- ins Querformat oder umgekehrt zu wechseln.

```csharp
page.Rotate = Rotation.on90;
```

Dieser Code dreht die Seite um 90 Grad und bringt sie in die gewünschte Ausrichtung.

## Schritt 7: Speichern Sie die Ausgabe-PDF

Nachdem wir die Ausrichtungsänderungen auf alle Seiten angewendet haben, speichern wir das geänderte Dokument in einer neuen Datei. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

Stellen Sie sicher, dass Sie einen neuen Dateinamen angeben (in diesem Fall `ChangeOrientation_out.pdf`), um die Ausgabe zu speichern. Auf diese Weise überschreiben Sie Ihre Originaldatei nicht.

### Abschluss

Und fertig! Das Ändern der Seitenausrichtung einer PDF-Datei mit Aspose.PDF für .NET ist ganz einfach: Laden Sie das Dokument, durchlaufen Sie die Seiten, passen Sie die MediaBox an und speichern Sie die aktualisierte Datei. Egal, ob Sie ein schlecht gescanntes Dokument haben oder Seiten drehen müssen, um Ihren Formatierungsanforderungen gerecht zu werden – diese Schritt-für-Schritt-Anleitung hilft Ihnen dabei.

## Häufig gestellte Fragen

### Kann ich bestimmte Seiten statt aller Seiten im PDF drehen?  
Ja, Sie können die Schleife so ändern, dass sie bestimmte Seiten anhand ihres Indexes anspricht, anstatt alle Seiten zu durchlaufen.

### Was ist der `MediaBox`?  
Der `MediaBox` Definiert die Größe und Form der Seite in einer PDF-Datei. Hier wird der Inhalt der Seite platziert.

### Funktioniert Aspose.PDF für .NET mit anderen Dateiformaten?  
Ja, Aspose.PDF kann eine Vielzahl von Dateiformaten wie HTML, XML, XPS und mehr verarbeiten.

### Gibt es eine kostenlose Version von Aspose.PDF für .NET?  
Ja, Sie können beginnen mit einem [kostenlose Testversion](https://releases.aspose.com/) oder fordern Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).

### Kann ich die Änderungen nach dem Speichern rückgängig machen?  
Sobald Sie das Dokument speichern, sind die Änderungen dauerhaft. Arbeiten Sie unbedingt mit einer Kopie oder bewahren Sie eine Sicherungskopie der Originaldatei auf.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}