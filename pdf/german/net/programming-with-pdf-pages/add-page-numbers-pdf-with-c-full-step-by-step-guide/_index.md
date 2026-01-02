---
category: general
date: 2026-01-02
description: Fügen Sie PDF-Seitenzahlen schnell mit Aspose.Pdf in C# hinzu. Erfahren
  Sie, wie Sie Bates-Nummerierung, Fußzeilentext, benutzerdefiniertes Wasserzeichen
  hinzufügen und in einem einzigen Skript durch PDF-Seiten iterieren.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: de
og_description: Fügen Sie PDF‑Seitenzahlen sofort mit Aspose.Pdf hinzu. Dieser Leitfaden
  behandelt auch das Hinzufügen von Bates‑Nummerierung, Fußzeilentext, benutzerdefiniertem
  Wasserzeichen und das Durchlaufen von PDF‑Seiten.
og_title: PDF‑Seitenzahlen mit C# hinzufügen – Komplettes Programmier‑Tutorial
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: PDF‑Seitenzahlen hinzufügen mit C# – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add page numbers pdf with C# – Complete Programming Tutorial

Haben Sie schon einmal **add page numbers pdf**‑Dateien hinzufügen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – Entwickler fragen ständig, wie man Nummern, Fußzeilen oder sogar einen Bates‑ähnlichen Identifier auf jeder Seite eines PDFs anbringt.  

In diesem Tutorial sehen Sie ein sofort ausführbares C#‑Beispiel, das **pdf‑Seiten durchläuft**, eine Seitenzahl‑Fußzeile stempelt und (falls gewünscht) ein benutzerdefiniertes Wasserzeichen hinzufügt. Wir zeigen Ihnen außerdem, wie Sie den Stempel zu einer Bates‑Nummer ändern, also im Grunde „Bates‑Nummerierung hinzufügen“ für juristische oder forensische Dokumente. Am Ende haben Sie eine einzelne, wiederverwendbare Methode, die all diese Aufgaben ohne großen Aufwand erledigt.

## Add page numbers pdf – Overview

Bevor wir in den Code eintauchen, klären wir, was „add page numbers pdf“ in der Aspose.Pdf‑Welt wirklich bedeutet. Die Bibliothek behandelt jedes Textstück, das Sie auf einer Seite platzieren, als **TextStamp**. Indem Sie einen Stempel mit einem Seiten‑Platzhalter (`{page}`) erstellen und ihn auf jede Seite anwenden, erhalten Sie automatisch eine fortlaufende Nummerierung. Derselbe Stempel kann zusätzlichen Text enthalten, sodass Sie **add footer text** wie „Confidential“ oder einen fall‑spezifischen Identifier hinzufügen können.

> **Why use a stamp instead of editing the PDF content stream?**  
> Stamps are high‑level objects that respect page margins, rotation, and existing graphics. They’re also far easier to maintain—just change a few properties and re‑run the script.

## Loop through PDF pages to apply stamps

Der erste praktische Schritt ist, das Quell‑PDF zu öffnen und über seine Seiten zu iterieren. Das ist das klassische **loop through pdf pages**‑Muster, das die meisten Aspose‑Beispiele verwenden.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Pro tip:** If your PDF is huge (hundreds of pages), consider processing it in batches to keep memory usage low. Aspose.Pdf streams pages lazily, so the loop itself is already pretty efficient.

## Add bates numbering and footer text

Jetzt, wo wir jede Seite durchlaufen können, erstellen wir einen **reusable TextStamp**, der sowohl die Seitenzahl als auch optionalen Fußzeilentext enthält. Der Platzhalter `{page}` wird automatisch durch die aktuelle Seitenzahl ersetzt.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Why this works

* **`Bates-{page}`** – Aspose substitutes `{page}` with the actual page number, giving you a classic Bates number automatically.
* **`Confidential`** – This is the **add footer text** part. You can replace it with any string, even pull data from a database.
* **Styling** – Using `TextState` lets you tweak color, opacity, and even rotation without touching the PDF's inner content streams.

If you only need plain numbers, drop the “Bates‑” prefix and the extra text:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Add a custom watermark (optional)

Manchmal wollen Sie mehr als nur eine Fußzeile – Sie benötigen ein halbtransparentes Logo oder ein „DRAFT“‑Overlay über die gesamte Seite. Hier kommt **add custom watermark** ins Spiel. Die gleiche `TextStamp`‑Klasse kann wiederverwendet werden, ändern Sie einfach ihre Ausrichtung und Transparenz.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Note:** Order matters. Adding the watermark first ensures the page numbers stay readable on top of the semi‑transparent text.

## Save the PDF and verify results

Nach dem Stempeln ist der letzte Schritt, die Änderungen wieder auf die Festplatte zu schreiben. Der `Save`‑Aufruf, den wir vorher platziert haben, erledigt die schwere Arbeit, aber wir fügen noch ein kurzes Verifizierungs‑Snippet hinzu, das die neue Datei öffnet und ausgibt, wie viele Seiten verarbeitet wurden.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Wenn Sie das komplette Programm ausführen, sollten Sie ein PDF sehen, bei dem jede Seite mit etwas wie **„Bates‑3 – Confidential“** endet (oder nur „3“, wenn Sie den einfachen Stempel verwendet haben) und, falls Sie das Wasserzeichen aktiviert haben, ein schwaches „DRAFT“ über die Mitte gelegt ist.

### Expected output

| Seite | Fußzeile (Beispiel) |
|------|----------------------|
| 1    | Bates‑1 – Vertraulich |
| 2    | Bates‑2 – Vertraulich |
| …    | … |
| N    | Bates‑N – Vertraulich |

Wenn Sie die Datei in einem Viewer öffnen, stehen die Zahlen 20 pts vom linken und unteren Rand entfernt, was den üblichen Konventionen für juristische Dokumente entspricht.

## Full working example (copy‑paste ready)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Speichern Sie dies als `AddPageNumbers.cs`, stellen Sie das Aspose.Pdf‑NuGet‑Paket wieder her (`Install-Package Aspose.Pdf`) und führen Sie es aus. Sie erhalten eine **add page numbers pdf**‑Datei, die zudem **add bates numbering**, **add footer text**, **add custom watermark** und das klassische **loop through pdf pages**‑Muster demonstriert – alles in einem übersichtlichen Skript.

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot, der nummerierte PDF‑Seiten mit Fußzeile und Wasserzeichen zeigt")

## Conclusion

Wir haben alles behandelt, was Sie benötigen, um **add page numbers pdf**‑Dateien mit Aspose.Pdf in C# zu erstellen. Vom Durchlaufen jeder Seite über das Stempeln von Bates‑Nummern, das Anhängen benutzerdefinierter Fußzeilentexte bis hin zum Einfügen eines halbtransparenten Wasserzeichens – der Code ist kompakt genug, um ihn in jedes bestehende Projekt zu übernehmen.  

Als nächstes könnten Sie fortgeschrittene Szenarien erkunden – etwa das Laden des Fußzeilentextes aus einer Datenbank, das Anwenden verschiedener Schriftarten pro Abschnitt oder das Erzeugen eines separaten Index‑PDFs, das alle Bates‑Nummern auflistet. All diese Erweiterungen bauen auf den hier gezeigten Kernideen auf, sodass Sie gut gerüstet sind, die Lösung an wachsende Anforderungen anzupassen.  

Probieren Sie es aus, passen Sie das Styling an und teilen Sie mir in den Kommentaren mit, wie es bei Ihnen funktioniert hat. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}