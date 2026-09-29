---
category: general
date: 2026-04-12
description: Füge schnell eine Abbildung in Word mit C# hinzu. Erfahre, wie du die
  Abbildung in Word positionierst, sie in eine docx‑Datei einfügst und benutzerdefiniertes
  XML für ein erweitertes Layout hinzufügst.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: de
og_description: Füge schnell eine Abbildung in Word mit C# ein. Lerne, wie du eine
  Abbildung in Word positionierst, in eine docx einfügst und benutzerdefiniertes XML
  für ein erweitertes Layout hinzufügst.
og_title: Abbildung zu Word hinzufügen – Vollständiger C#‑Programmierleitfaden
tags:
- C#
- Word Automation
- Document Generation
title: Abbildung zu Word hinzufügen – Vollständiger C#‑Programmierleitfaden
url: /de/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Abbildung zu Word hinzufügen – Vollständiger C# Programmierleitfaden

Haben Sie jemals **Abbildung zu Word hinzufügen** gebraucht, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. In vielen Office‑Automatisierungsprojekten fehlt das schön platzierte Bild oder Diagramm, das in einem benutzerdefinierten XML‑Teil lebt. Dieser Leitfaden zeigt Ihnen genau, wie Sie **Abbildung in Word positionieren**, die Abbildung in eine *.docx*-Datei einfügen und sogar das zugrunde liegende benutzerdefinierte XML anpassen, damit die Form sich wie jedes native Word‑Objekt verhält.

Wir gehen ein praxisnahes Beispiel mit der GemBox.Document‑Bibliothek (kostenlos für kleine Dateien, kommerziell für größere Workloads) durch. Am Ende haben Sie ein eigenständiges, ausführbares Programm, das eine Abbildung bei den Koordinaten X = 50, Y = 200 innerhalb eines Tagged‑Content‑Containers platziert. Keine vagen „siehe Dokumentation“-Abkürzungen – nur klarer Code, warum er funktioniert, und Tipps, die Sie direkt in Ihr eigenes Projekt übernehmen können.

## Voraussetzungen

- .NET 6.0 oder höher (der Code kompiliert auch mit .NET Core 3.1)
- **GemBox.Document** NuGet‑Paket (`Install-Package GemBox.Document`)
- Eine Ausgangs‑Word‑Datei (`input.docx`), die bereits ein benutzerdefiniertes XML‑Tag enthält, an dem die Abbildung erscheinen soll
- Grundlegende C#‑Kenntnisse (Sie werden sehen, warum jede Zeile wichtig ist)

> **Pro‑Tipp:** Wenn Sie kein vorab getaggtes Dokument haben, können Sie eines in Word erstellen, indem Sie ein *Content Control* → *XML Mapping Pane* → ein benutzerdefiniertes XML‑Teil zuordnen. Die Bibliothek behandelt dieses Steuerelement als `TaggedContent`.

## Schritt 1 – Quell‑Dokument laden

Das erste, was wir tun, ist die vorhandene *.docx*-Datei zu öffnen. `Document` ist der Einstiegspunkt für alle GemBox‑Operationen.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Warum?* Das Laden der Datei gibt uns Zugriff auf ihre internen Teile, einschließlich aller benutzerdefinierten XML‑Container. Ohne das könnten wir den `TaggedContent`‑Knoten, der unsere Abbildung halten soll, nicht finden.

## Schritt 2 – Zugriff auf den Tagged Content (Custom XML‑Container)

Benutzerdefiniertes XML wird in Word in einem *content control* gespeichert. GemBox stellt es als `TaggedContent` bereit.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Falls das Dokument mehrere markierte Abschnitte hat, gibt `TaggedContent` den **ersten** zurück. Sie können auch `doc.TaggedContents` enumerieren, um ein bestimmtes Tag nach Namen auszuwählen.

## Schritt 3 – Figure‑Element erstellen

Ein `FigureElement` repräsentiert ein Bild, Diagramm oder jedes visuelle Objekt, das Word als *shape* behandelt. Wir erstellen es innerhalb des getaggten Containers.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Warum hier ein Figure‑Element erstellen?* Durch die Anbindung an den benutzerdefinierten XML‑Knoten weiß Word, dass die Abbildung zu diesem logischen Abschnitt gehört – das ist entscheidend für spätere Bearbeitungen oder Workflows, die auf Content‑Controls basieren.

## Schritt 4 – Figure präzise positionieren

Word verwendet Punkte (1 pt ≈ 1/72 in) für die Positionierung. Die `PointF`‑Struktur ermöglicht es uns, X/Y‑Koordinaten einfach zu setzen.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** Die `Position`‑Eigenschaft akzeptiert ein `PointF`, wobei der erste Wert den horizontalen Versatz (links) und der zweite den vertikalen Versatz (oben) relativ zum Seitenrand angibt. Passen Sie diese Zahlen an, um die Platzierung feinzujustieren.

## Schritt 5 – Figure in den Tagged‑Content‑Baum einfügen

Jetzt hängen wir die Abbildung an das Wurzelelement des benutzerdefinierten XML‑Baums an. Das fügt die Form physisch in das Word‑Dokument ein.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

An diesem Punkt befindet sich die Abbildung im Dokument, hat aber noch keine Bildquelle. Lassen Sie uns ein einfaches PNG von der Festplatte hinzufügen.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Schritt 6 – Modifiziertes Dokument speichern

Abschließend schreiben wir die Änderungen in eine neue *.docx*-Datei zurück.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Wenn Sie `output.docx` in Word öffnen, sehen Sie das Bild exakt bei (50, 200) innerhalb des benutzerdefinierten XML‑Blocks, den Sie anvisiert haben.

### Vollständiges funktionierendes Beispiel

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Erwartetes Ergebnis:** Beim Öffnen von `output.docx` wird das PNG genau dort platziert, wo Sie es angegeben haben, eingebettet im benutzerdefinierten XML‑Teil. Wenn Sie das XML des Dokuments inspizieren (`.docx` → unzip → `word/document.xml`), sehen Sie ein `<w:pict>`‑Element mit den korrekten `<v:shape>`‑Koordinaten.

## Häufige Fragen & Sonderfälle

### Was ist, wenn das Dokument mehrere Tagged‑Abschnitte hat?

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Wie fügt man der Figure eine Beschriftung hinzu?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Funktioniert das mit Word 2010 und neuer?

Ja. GemBox.Document richtet sich nach dem Open‑XML‑Standard, der mit Word 2007 + (einschließlich 2010, 2013, 2016, 2019 und Microsoft 365) kompatibel ist.

### Was ist, wenn ich die Form drehen muss?

```csharp
figure.Rotation = 45; // degrees
```

### Wie fügt man eine Vektorgrafik anstelle eines Rasterbildes hinzu?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro‑Tipps & Fallstricke

- **File paths:** Verwenden Sie `Path.Combine`, um hartkodierte Trennzeichen zu vermeiden, besonders auf Nicht‑Windows‑Plattformen.
- **License limits:** Die kostenlose GemBox‑Lizenz begrenzt die Dokumentgröße auf 20 KB. Für größere Dateien erwerben Sie einen kommerziellen Schlüssel.
- **Performance:** Die Wiederverwendung einer einzelnen `Document`‑Instanz für Batch‑Verarbeitung reduziert den Speicherverbrauch erheblich.
- **Shape overflow:** Wenn die Abmessungen der Figure die Seitenränder überschreiten, schneidet Word sie ab. Passen Sie `figure.Width` und `figure.Height` entsprechend an.

## Fazit

Sie wissen jetzt, **wie man Abbildung zu Word hinzufügen** kann, **Abbildung in Word präzise positionieren** und das zugrunde liegende benutzerdefinierte XML manipulieren, damit die Form sich wie jedes native Element verhält. Das vollständige, ausführbare Beispiel demonstriert jeden Schritt – vom Laden des Dokuments, Erstellen eines `FigureElement`, Setzen der Koordinaten, Anhängen eines Bildes bis zum finalen Speichern der aktualisierten *.docx*.

Als Nächstes experimentieren Sie mit **insert figure into docx**, indem Sie mehrere Figuren hinzufügen, Schleifen verwenden oder Diagramme on‑the‑fly generieren. Vielleicht erkunden Sie auch **how to add custom xml** für reichhaltigere Content‑Controls oder lernen **how to position shape word** in Tabellen und Kopf‑/Fußzeilen. Die Möglichkeiten sind endlos, und mit den hier behandelten Grundlagen können Sie Word‑Dokumente wie ein Profi automatisieren.

Viel Spaß beim Coden, und hinterlassen Sie gern einen Kommentar, falls Sie auf Probleme stoßen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}