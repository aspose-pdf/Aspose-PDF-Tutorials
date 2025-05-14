---
"description": "Erfahren Sie in diesem ausführlichen Schritt-für-Schritt-Tutorial, wie Sie die Callout-Eigenschaft in einer PDF-Datei mit Aspose.PDF für .NET festlegen."
"linktitle": "Callout-Eigenschaft in PDF-Datei festlegen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Callout-Eigenschaft in PDF-Datei festlegen"
"url": "/de/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Callout-Eigenschaft in PDF-Datei festlegen

## Einführung

Das Erstellen professioneller und optisch ansprechender PDF-Dokumente erfordert oft das Hinzufügen von Anmerkungen, die die Aufmerksamkeit auf bestimmte Inhalte lenken. Eine solche Anmerkung ist der Callout, ähnlich den Sprechblasen aus Comics. Er hilft, Text in Ihrem PDF zu verdeutlichen oder hervorzuheben. Aspose.PDF für .NET macht das Hinzufügen solcher Anmerkungen zu Ihren Dokumenten unglaublich einfach. In diesem Tutorial erfahren Sie, wie Sie die Callout-Eigenschaft in einer PDF-Datei mithilfe dieser leistungsstarken Bibliothek festlegen. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen – am Ende dieses Handbuchs haben Sie ein klares Verständnis für die Arbeit mit Callouts in PDF-Dateien.

## Voraussetzungen

Bevor wir uns in den Code vertiefen, wollen wir die wesentlichen Dinge besprechen, die Sie für den Einstieg benötigen.

1. Aspose.PDF für .NET: Stellen Sie sicher, dass die Aspose.PDF für .NET-Bibliothek installiert ist. Sie können sie hier herunterladen. [Hier](https://releases.aspose.com/pdf/net/).
2. IDE: Eine Entwicklungsumgebung wie Visual Studio.
3. .NET Framework: Stellen Sie sicher, dass .NET auf Ihrem Computer installiert ist.
4. Temporäre Lizenz: Wenn Sie die vollen Funktionen von Aspose.PDF ohne Einschränkungen ausprobieren möchten, erhalten Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).

## Pakete importieren

Bevor Sie mit dem Schreiben des Codes beginnen, müssen Sie die erforderlichen Pakete importieren, die Ihnen die Arbeit mit PDF-Dateien und Anmerkungen ermöglichen.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Diese Importe stellen Ihnen alle erforderlichen Klassen und Methoden zur Verfügung, um PDF-Dokumente zu bearbeiten und Anmerkungen wie Callouts zu erstellen.

## Schritt 1: Initialisieren Sie das PDF-Dokument

Der erste Schritt besteht darin, ein neues PDF-Dokument zu initialisieren, in das wir unsere Callout-Anmerkung einfügen. Stellen Sie sich das wie eine leere Leinwand vor, auf der Sie Elemente hinzufügen können.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Initialisieren eines neuen PDF-Dokuments
Document doc = new Document();
```
Hier schaffen wir ein neues `Document` Objekt, das als PDF-Datei dient. Die `dataDir` Die Variable wird auf das Verzeichnis eingestellt, in dem Sie Ihre PDF-Datei speichern möchten, wenn wir fertig sind.

## Schritt 2: Dem Dokument eine neue Seite hinzufügen

Ein PDF-Dokument kann mehrere Seiten umfassen. In diesem Schritt fügen wir unserem Dokument eine neue Seite hinzu. Auf dieser Seite wird unsere Callout-Anmerkung platziert.

```csharp
// Dem Dokument eine neue Seite hinzufügen
Page page = doc.Pages.Add();
```
Der `Pages.Add()` -Methode wird verwendet, um eine neue Seite zum `doc` Objekt. Die neue Seite wird gespeichert im `page` Variable, die wir später beim Hinzufügen der Anmerkung verwenden werden.

## Schritt 3: Definieren Sie das Standard-Erscheinungsbild

Anmerkungen haben, wie die Legende, ein visuelles Erscheinungsbild, das Sie anpassen können. In diesem Schritt definieren wir, wie der Text in der Legende aussehen soll.

```csharp
// Definieren Sie das Standard-Erscheinungsbild für die Anmerkung
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
Wir schaffen eine `DefaultAppearance` Objekt, das die Textfarbe und Schriftgröße definiert. Hier ist der Text rot und die Schriftgröße auf 10 eingestellt. Dieses Erscheinungsbild wird auf die Callout-Anmerkung angewendet.

## Schritt 4: Erstellen Sie die Freitextanmerkung

Jetzt ist es an der Zeit, die eigentliche Anmerkung zu erstellen. Mit der Freitextanmerkung können wir einen Callout mit spezifischem Text und Stil hinzufügen.

```csharp
// Erstellen Sie eine FreeTextAnnotation mit einem Callout
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
Wir schaffen eine `FreeTextAnnotation` Objekt mit spezifischen Koordinaten, die seine Position auf der Seite definieren. Die `Intent` ist eingestellt auf `FreeTextCallout`, was darauf hinweist, dass es sich um eine Callout-Anmerkung handelt. Die `EndingStyle` ist eingestellt auf `OpenArrow`, was bedeutet, dass die Callout-Linie mit einem offenen Pfeil endet.

## Schritt 5: Definieren Sie die Callout-Linienpunkte

Eine Callout-Annotation weist eine Linie auf den relevanten Bereich. Hier definieren wir die Punkte, aus denen diese Linie besteht.

```csharp
// Definieren Sie die Punkte für die Callout-Linie
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
Der `Callout` Eigenschaft ist ein Array von `Point` Objekte, die jeweils eine Koordinate auf der Seite darstellen. Diese Punkte definieren den Pfad der Callout-Linie und verleihen ihr das klassische Aussehen einer Sprechblase.

## Schritt 6: Fügen Sie der Seite die Anmerkung hinzu

Nachdem wir unsere Anmerkung erstellt und konfiguriert haben, besteht der nächste Schritt darin, sie der Seite hinzuzufügen.

```csharp
// Fügen Sie der Seite die Anmerkung hinzu
page.Annotations.Add(fta);
```
Der `Annotations.Add()` Mit dieser Methode wird die Anmerkung auf der zuvor erstellten Seite platziert. Dieser Schritt „zeichnet“ die Beschriftung auf der PDF-Seite.

## Schritt 7: Rich-Text-Inhalt festlegen

Callout-Anmerkungen können Rich Text enthalten, sodass formatierter Inhalt innerhalb der Sprechblase möglich ist. Fügen wir Beispieltext hinzu.

```csharp
// Legen Sie den Rich Text für die Anmerkung fest
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">Dies ist ein Beispiel</span></p></body>";
```
Der `RichText` Die Eigenschaft wird mit HTML-Inhalt festgelegt. Dies ermöglicht eine detaillierte Formatierung innerhalb des Callouts, z. B. die Angabe von Schriftgröße, Farbe und Stil.

## Schritt 8: Speichern Sie das PDF-Dokument

Nachdem wir alles eingerichtet haben, müssen wir das Dokument abschließend speichern. Dieser Schritt schließt die Erstellung der PDF-Datei mit der Callout-Anmerkung ab.

```csharp
// Speichern des Dokuments
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
Der `Save()` Die Methode speichert das Dokument im angegebenen Verzeichnis unter dem Dateinamen „SetCalloutProperty.pdf“. Damit ist die PDF-Erstellung abgeschlossen.

## Abschluss

Und da haben Sie es! Sie haben gerade ein PDF-Dokument mit einer Callout-Anmerkung mit Aspose.PDF für .NET erstellt. Diese Anmerkung kann unglaublich nützlich sein, um bestimmte Teile Ihres Dokuments hervorzuheben oder zu erklären. Aspose.PDF bietet eine leistungsstarke API, die die PDF-Bearbeitung einfach und flexibel macht. Ob Sie Anmerkungen hinzufügen, Dokumente konvertieren oder komplexe PDF-Aufgaben erledigen – Aspose.PDF unterstützt Sie dabei.

## Häufig gestellte Fragen

### Kann ich das Erscheinungsbild des Callouts weiter anpassen?

Absolut! Sie können verschiedene Aspekte wie Linienfarbe, Linienstärke sowie Schriftart und -stil des Textes anpassen.

### Ist es möglich, mehrere Callouts auf einer Seite hinzuzufügen?

Ja, Sie können so viele Callouts hinzufügen wie nötig, indem Sie die Schritte für jede Anmerkung wiederholen.

### Wie ändere ich die Position des Callouts?

Ändern Sie einfach die Koordinaten in der `Rectangle` Und `Callout` Eigenschaften, um die Anmerkung neu zu positionieren.

### Kann ich mit Aspose.PDF andere Arten von Anmerkungen hinzufügen?

Ja, Aspose.PDF unterstützt verschiedene Anmerkungstypen, darunter Hervorhebungen, Stempel und Dateianhänge.

### Ist der Rich-Text-Inhalt auf HTML beschränkt?

Der `RichText` Die Eigenschaft unterstützt eine Teilmenge von HTML und ermöglicht Ihnen die Einbindung formatierten Textes und grundlegender Formatierungen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}