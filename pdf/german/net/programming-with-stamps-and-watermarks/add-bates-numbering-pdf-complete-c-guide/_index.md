---
category: general
date: 2026-03-22
description: Fügen Sie PDFs schnell mit Bates‑Nummerierung mithilfe von Aspose.Pdf
  hinzu. Erfahren Sie, wie Sie Bates‑Nummern, fortlaufende Seitenzahlen, benutzerdefinierte
  Fußzeilen und Artefakte zu PDFs in wenigen Minuten hinzufügen.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: de
og_description: Bates-Nummerierung zu PDF hinzufügen mit Aspose.Pdf. Dieser Leitfaden
  zeigt, wie man Bates-Nummern, fortlaufende Seitenzahlen, benutzerdefinierte Fußzeilen
  und Artefakte zu PDFs hinzufügt.
og_title: Bates-Nummerierung zu PDF hinzufügen – Schritt‑für‑Schritt C#‑Tutorial
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Bates-Nummerierung zu PDF hinzufügen – Vollständiger C#‑Leitfaden
url: /de/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-Nummerierung zu PDF hinzufügen – Vollständiger C# Leitfaden

Haben Sie jemals **add bates numbering pdf** zu einem Stapel juristischer Dokumente hinzufügen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht der Erste – viele Entwickler stoßen bei der Erstellung von Fall‑Management‑Tools auf dieses Problem. Die gute Nachricht? Mit Aspose.Pdf können Sie **add bates**, **add sequential page numbers** und sogar **add custom footer pdf** Elemente in nur wenigen Codezeilen hinzufügen.  

In diesem Tutorial gehen wir den gesamten Prozess durch, von der Installation der Bibliothek bis zum Speichern der finalen Datei, und wir geben Tipps, wie man **add artifact to pdf** Dateien hinzufügt, ohne bestehenden Inhalt zu beschädigen. Am Ende haben Sie ein einsatzbereites Snippet, das Sie in jedes .NET‑Projekt einbinden können.

## Was Sie benötigen

- .NET 6+ (der Code funktioniert sowohl auf .NET Core als auch auf .NET Framework)  
- Eine gültige Aspose.Pdf für .NET Lizenz (Sie können mit einer kostenlosen Evaluation beginnen)  
- Eine Eingabe‑PDF (`input.pdf`), die in einem Ordner liegt, den Sie referenzieren können  
- Visual Studio, Rider oder ein beliebiger C#‑Editor Ihrer Wahl  

Das war's – keine zusätzlichen NuGet‑Pakete außer Aspose.Pdf.

## Schritt 1: Aspose.Pdf über NuGet installieren

Zuerst das Wichtigste – holen wir die Bibliothek auf Ihren Rechner. Öffnen Sie ein Terminal in Ihrem Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.Pdf
```

Oder, wenn Sie die Package Manager Console von Visual Studio verwenden:

```powershell
Install-Package Aspose.Pdf
```

*Pro‑Tipp:* Nach der Installation prüfen Sie, dass der Ordner `Aspose.Pdf` unter `Dependencies → Packages` im Solution Explorer erscheint.

## Schritt 2: Das Quell-PDF-Dokument laden

Jetzt erstellen wir ein `Document`‑Objekt, das das PDF repräsentiert, das wir versehen wollen. Die Verwendung der `using`‑Anweisung stellt sicher, dass der Dateihandle automatisch freigegeben wird.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Warum `using var` verwenden? Es garantiert die Entsorgung selbst bei einer Ausnahme, wodurch spätere Datei‑Lock‑Probleme beim Überschreiben derselben Datei vermieden werden.

## Schritt 3: Ein Bates-Nummerierungs-Artifact erstellen und konfigurieren

Eine Bates-Nummer ist im Wesentlichen ein Text-Artifact, das in der logischen Struktur des PDFs lebt. Sie können es wie einen **custom footer pdf** behandeln, da es auf jeder Seite erscheint, ohne Teil des Inhalts‑Streams der Seite zu sein.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Warum diese Einstellungen wichtig sind

- **Prefix**: Nützlich, um Dokumenttypen zu unterscheiden (z. B. „INV‑“ für Rechnungen).  
- **Start**: Legt die erste Nummer fest; Sie können diesen Wert aus einer Datenbank beziehen, wenn Sie Kontinuität über Dateien hinweg benötigen.  
- **Format**: `"0000"` erzwingt eine vierstellige Anzeige und sorgt für Ausrichtung, wenn die Zahlen wachsen.  
- **X/Y**: Koordinaten werden vom unteren linken Eckpunkt gemessen, sodass `Y = 20` den Text knapp über dem Seitenrand platziert. Passen Sie `X` an, wenn Sie die Nummer linksbündig oder zentriert haben möchten.

Wenn Sie **add sequential page numbers** anstelle von Bates-Nummern benötigen, lassen Sie einfach `Prefix` weg und passen `Format` zu `"###"` oder einem beliebigen Muster Ihrer Wahl an.

## Schritt 4: Das Artifact auf alle Seiten anwenden

Aspose.Pdf ermöglicht es, ein Artifact in einem einzigen Aufruf an das gesamte Dokument anzuhängen. Dies ist der effizienteste Weg, **add artifact to pdf** hinzuzufügen, ohne jede Seite manuell zu durchlaufen.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Im Hintergrund fügt Aspose das Artifact dem Seiten‑Dictionary jeder Seite hinzu, wodurch die Nummerierung Teil der logischen Struktur des PDFs wird – ideal für spätere Extraktion oder Suche.

## Schritt 5: Das aktualisierte PDF speichern

Zum Schluss schreiben Sie die Änderungen zurück auf die Festplatte. Sie können die Originaldatei überschreiben oder in eine neue Datei speichern; Letzteres ist während der Entwicklung sicherer.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Wenn Sie `output.pdf` in einem Viewer öffnen, sehen Sie „INV‑1000“, „INV‑1001“, … unten rechts auf jeder Seite.

### Ergebnis überprüfen

Öffnen Sie das PDF in Adobe Acrobat oder einem beliebigen Viewer und suchen Sie nach den Zahlen. Wenn Sie programmgesteuert bestätigen möchten, können Sie das Artifact erneut auslesen:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Dieses Snippet gibt das Bates-Label jeder Seite aus – praktisch für automatisierte Tests.

## Sonderfälle & häufige Fragen

### Was ist, wenn mein PDF bereits eine Fußzeile hat?

Das Hinzufügen eines Artifacts überschreibt vorhandene Fußzeilen nicht, da Artifacts in einer separaten Ebene liegen. Wenn jedoch die visuelle Überlappung ein Problem darstellt, passen Sie die `Y`‑Koordinate an oder erhöhen Sie den `X`‑Versatz, um die Bates-Nummer aus dem Weg zu räumen.

### Kann ich eine andere Schriftart oder Farbe verwenden?

Absolut. Der `BatesNumberingArtifact` erbt von `Artifact`, sodass Sie `Font`, `FontColor` und sogar `Opacity` setzen können. Beispiel:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Wie setze ich den Zähler für ein neues Dokument zurück?

Ändern Sie einfach `Start` bevor Sie `AddArtifact` aufrufen. Wenn Sie viele PDFs in einer Schleife erzeugen, behalten Sie einen laufenden Zähler in Ihrer Anwendungslogik.

### Ist dieser Ansatz mit verschlüsselten PDFs kompatibel?

Aspose.Pdf kann verschlüsselte PDFs öffnen, wenn Sie das Passwort angeben:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Nach der Entschlüsselung funktionieren die gleichen Schritte zum Hinzufügen des Artifacts einwandfrei.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, einsatzbereite Programm. Fügen Sie es in eine Konsolen‑App ein, passen Sie die Pfade an und drücken Sie **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Erwartete Ausgabe:** Die Konsole gibt „Bates numbering added successfully!“ aus und `output.pdf` enthält sequenzielle Labels wie `INV‑1000`, `INV‑1001` usw., positioniert unten rechts auf jeder Seite.

## Kurze Zusammenfassung

- **Hauptziel:** **add bates numbering pdf** mit Aspose.Pdf.  
- Wir haben behandelt, **how to add bates**, **add sequential page numbers** und **add custom footer pdf** Elemente über ein einzelnes Artifact.  
- Das Tutorial zeigte, wie man **add artifact to pdf** hinzufügt, Sonderfälle behandelt und das Ergebnis überprüft.  

## Was kommt als Nächstes?

- **Dynamische Präfixe:** Werte aus einer Datenbank ziehen, um „CASE‑2023‑001“, „CASE‑2023‑002“ … zu erzeugen.  
- **Bedingte Platzierung:** Seiten­größen‑Erkennung (`page.MediaBox`) verwenden, um Zahlen auf Querformatseiten zu zentrieren.  
- **Mit Wasserzeichen kombinieren:** Ein halbtransparentes Logo neben der Bates‑Nummer für Branding hinzufügen.  

Fühlen Sie sich frei zu experimentieren – vielleicht entdecken Sie einen clevereren Weg, Tausende von Dateien stapelweise zu verarbeiten. Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar oder schauen Sie in die offiziellen Aspose‑Docs (sie sind überraschend klar). Viel Spaß beim Coden!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}