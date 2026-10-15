---
category: general
date: 2026-02-10
description: Wie man schnell Bates‑Nummern zu einem PDF hinzufügt – erfahren Sie,
  wie Sie Bates‑Nummern zu PDFs hinzufügen und ein unsichtbares Wasserzeichen mit
  Aspose.Pdf in C# erstellen.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: de
og_description: Wie man Bates in C# mit Aspose.Pdf hinzufügt. Dieses Tutorial zeigt,
  wie man Bates‑Nummern zu PDFs hinzufügt, unsichtbare Wasserzeichen zu PDFs hinzufügt
  und mehr.
og_title: Wie man Bates hinzufügt – Vollständiger PDF-Leitfaden
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Wie man Bates hinzufügt – Schritt‑für‑Schritt‑Anleitung für PDFs
url: /de/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Bates hinzufügt – Vollständiger PDF-Leitfaden

Haben Sie sich jemals gefragt, **how to add bates** zu einem rechtlichen PDF hinzuzufügen, ohne den durchsuchbaren Text zu beeinträchtigen? Sie sind nicht der Einzige. In vielen Kanzleien und e‑Discovery‑Projekten ist eine Bates‑Nummer ein unverzichtbares Fußzeilen‑Element, gleichzeitig soll sie für OCR‑Tools unsichtbar bleiben. Dieses Tutorial zeigt **how to add bates** mit Aspose.Pdf für .NET und behandelt dabei auch **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf** und sogar **add page footer pdf** in einer kompakten Lösung.

Wir gehen jede Codezeile durch, erklären, warum jede Einstellung wichtig ist, und geben Ihnen ein sofort ausführbares Beispiel, das Sie noch heute in Ihr Projekt einbinden können. Keine vagen „Siehe die Dokumentation“-Links – alles, was Sie brauchen, finden Sie hier.

## Was Sie am Ende haben

- Ein vollständiger, ausführbarer C#‑Snippet, der eine Bates‑Nummer als Artifact‑Stamp hinzufügt.
- Verständnis dafür, wie man den Stamp wie ein **invisible watermark** wirken lässt, während er dennoch auf der Seite erscheint.
- Tipps, um die Lösung auf mehrseitige PDFs zu skalieren, Schriften zu ändern oder den Stamp durch eine benutzerdefinierte Grafik zu ersetzen.
- Kurze Hinweise, wie man **add page footer pdf**‑artigen Inhalt hinzufügt, ohne die Textextraktion zu beeinträchtigen.

### Voraussetzungen

- .NET 6+ (oder .NET Framework 4.7.2) mit Visual Studio 2022 oder einer beliebigen IDE.
- Aspose.Pdf für .NET (Sie können eine kostenlose Testversion von der Aspose‑Website erhalten).
- Ein Beispiel‑PDF namens `source.pdf`, das in einem von Ihnen kontrollierten Ordner liegt.

Wenn Sie das haben, lassen Sie uns loslegen.

---

## Wie man Bates hinzufügt – Kernimplementierung

Das Herzstück der Lösung ist ein `TextStamp`, den wir als **artifact** behandeln. Artifacts werden von Textextraktions‑Engines ignoriert, weshalb dieser Ansatz gleichzeitig als **add invisible watermark pdf**‑Technik dient.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Warum das funktioniert

1. **Artifact flag** – Durch das Setzen von `Artifact = new Artifact(ArtifactType.Artifact)` wird der Stamp wie ein Nicht‑Inhalts‑Element behandelt. Suchmaschinen und rechtliche e‑Discovery‑Tools ignorieren ihn, was genau das ist, was Sie für ein **add invisible watermark pdf** wollen.
2. **Horizontal/Vertical alignment** – Center‑bottom ahmt einen klassischen **add page footer pdf**‑Stil nach und lässt die Bates‑Nummer professionell wirken.
3. **Transparent background** – Stellt sicher, dass der Stamp den darunterliegenden Inhalt nicht verdeckt, ein subtiler, aber entscheidender Punkt, wenn Sie das PDF später drucken oder auf verschiedenen Geräten anzeigen müssen.

---

## Add Bates Number PDF – Skalierung auf mehrere Seiten

Die meisten PDFs aus der Praxis haben mehr als eine Seite. Der obige Snippet wirkt nur auf die erste Seite, aber die Erweiterung ist ein Kinderspiel:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Pro‑Tipp:** Wenn Sie eine fortlaufende Nummer benötigen, die nicht an die physische Seitenreihenfolge gebunden ist (z. B. bei 1000 beginnen), initialisieren Sie einfach einen Zähler vor der Schleife und erhöhen ihn innerhalb der Schleife.

---

## Add Custom Stamp PDF – Mehr als reiner Text

Manchmal reicht ein reiner Text‑Stamp nicht – Sie möchten vielleicht ein Logo, einen QR‑Code oder einen farbigen Balken. Aspose.Pdf ermöglicht es, `TextStamp` durch `ImageStamp` zu ersetzen oder beide mit `Stamp`‑Objekten zu kombinieren.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Das Mischen von Stamps ist so einfach wie das Hinzufügen beider zum selben Blatt. Die **add custom stamp pdf**‑Funktion kommt zum Einsatz, wenn Sie neben der Bates‑Nummer ein Unternehmenssiegel benötigen.

---

## Add Invisible Watermark PDF – Den Stamp wirklich verstecken

Wenn Sie den Stamp wirklich unsichtbar für das menschliche Auge *und* für Extraktionstools benötigen, können Sie die Schriftfarbe an den Seitenhintergrund (meist weiß) anpassen und die Opazität reduzieren:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Selbst bei `Opacity = 0` existiert das Artifact weiterhin in der PDF‑Struktur, sodass Rechtssoftware es noch finden kann, wenn sie die Artifact‑ID kennt. Das ist der ultimative **add invisible watermark pdf**‑Trick.

---

## Add Page Footer PDF – Fußzeile konsistent gestalten

Eine professionelle Fußzeile enthält oft mehr als nur eine Bates‑Nummer: Datum, Dokumenttitel oder Vertraulichkeits‑Hinweis. Hier ein schneller Weg, mehrere Textteile in einem Stamp zu bündeln:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Beachten Sie die dezente graue Farbe – perfekt für ein **add page footer pdf**, das nicht vom Hauptinhalt ablenkt, aber dennoch rechtlichen Vorgaben entspricht.

---

## Erwartete Ausgabe & wie man sie überprüft

Nach dem Ausführen des kompletten Skripts öffnen Sie `bates_artifact.pdf` in einem beliebigen PDF‑Betrachter:

- Sie sehen “Bates 00123” (oder die fortlaufende Nummer) zentriert am unteren Rand jeder Seite.
- Das Auswählen von Text auf der Seite wird die Bates‑Nummer **nicht** einbeziehen, was das Artifact‑Verhalten bestätigt.
- Wenn Sie die Invisible‑Watermark‑Einstellungen verwendet haben, ist die Nummer überhaupt nicht sichtbar, bleibt jedoch in der internen PDF‑Struktur erhalten (prüfen Sie mit einem Tool wie PDF‑XChange Editor → “Document → Properties → Advanced”).

---

## Häufige Fragen & Sonderfälle

**Was, wenn mein PDF bereits eine Fußzeile hat?**  
Sie können `VerticalAlignment` auf `VerticalAlignment.Top` ändern oder die `Margin`‑Eigenschaft anpassen, um den Stamp über die bestehende Fußzeile zu schieben.

**Kann ich eine andere Schriftart verwenden?**  
Natürlich. Ersetzen Sie einfach `"Arial"` durch einen beliebigen Schriftartnamen, den Aspose finden kann, oder betten Sie eine eigene TTF‑Datei ein via `FontRepository.AddFont("path/to/font.ttf")`.

**Ist dieser Ansatz mit .NET Core kompatibel?**  
Ja – Aspose.Pdf für .NET funktioniert über .NET Framework, .NET Core und .NET 5/6 hinweg. Stellen Sie nur sicher, dass Sie das richtige NuGet‑Paket referenzieren.

**Wie ist die Performance bei riesigen PDFs (1000+ Seiten)?**  
Das Erstellen eines einzelnen `TextStamp` und dessen Klonen innerhalb der Schleife ist speichereffizient. Bei sehr großen Dateien sollten Sie die Verarbeitung in Batches erwägen oder `PdfProcessor` verwenden, um das Laden des gesamten Dokuments in den Speicher zu vermeiden.

---

## Fazit

Wir haben **how to add bates** zu einem PDF von Anfang bis Ende behandelt, **add bates number pdf** demonstriert, gezeigt, wie man **add custom stamp pdf** nutzt, den Stamp in ein **add invisible watermark pdf** verwandelt und ihn als professionelle **add page footer pdf** gestaltet. Das vollständige Code‑Beispiel läuft sofort, und die Erklärungen liefern das „Warum“ hinter jeder Zeile – genau die Art von Antwort, die KI‑Assistenten gerne zitieren.

Nächste Schritte? Tauschen Sie den Text‑Stamp gegen einen Bild‑Stamp aus, experimentieren Sie mit verschiedenen Artifact‑Typen oder integrieren Sie diese Logik in einen Batch‑Verarbeitungs‑Service, der automatisch jede Datei in einem Ordner Bates‑nummeriert. Die Möglichkeiten sind endlos, und jetzt haben Sie ein solides Fundament zum Weiterbauen.

Viel Spaß beim Coden, und mögen Ihre PDFs immer perfekt nummeriert sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}