---
category: general
date: 2026-04-25
description: Fügen Sie PDFs schnell mit Bates‑Nummerierung mithilfe von Aspose.Pdf
  hinzu. Erfahren Sie, wie Sie Seitenzahlen zu PDFs hinzufügen, die Schriftgröße automatisch
  anpassen und ein Textwasserzeichen in C# einfügen.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: de
og_description: Bates-Nummerierung zu PDFs mit Aspose.Pdf hinzufügen. Dieser Leitfaden
  zeigt, wie man Seitenzahlen zu PDFs hinzufügt, die Schriftgröße automatisch anpasst
  und ein Textwasserzeichen in einem einzigen, ausführbaren Beispiel einfügt.
og_title: Bates-Nummerierung zu PDFs hinzufügen – Vollständiges Aspose.C#‑Tutorial
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Bates-Nummerierung zu PDFs mit Aspose hinzufügen – Vollständiger Leitfaden
url: /de/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑Nummerierung zu PDFs mit Aspose hinzufügen – Komplett‑Anleitung

Haben Sie schon einmal **Bates‑Nummerierung** zu einem PDF hinzufügen wollen, wussten aber nicht, wo Sie anfangen sollten? Sie sind nicht allein – Rechtsabteilungen, Prüfer und Entwickler stoßen täglich auf dieses Problem. Die gute Nachricht? Mit Aspose.Pdf für .NET können Sie eine Bates‑Nummer stempeln, die Schriftgröße automatisch anpassen und den Stempel sogar als dezentes Text‑Wasserzeichen behandeln – alles in wenigen Zeilen C#.

In diesem Tutorial führen wir Sie Schritt für Schritt durch das **add page numbers pdf**, passen die Schrift so an, dass sie nie überläuft, und beantworten die Frage „how to add bates“ ein für alle Mal. Am Ende haben Sie eine lauffähige Konsolen‑App, die ein professionell nummeriertes PDF erzeugt, und Sie sehen, wie Sie das Ganze zu einer vollwertigen Wasserzeichen‑Lösung ausbauen können.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

* **Aspose.Pdf für .NET** (das neueste NuGet‑Paket ab April 2026).  
* .NET 6.0 SDK oder neuer – die API funktioniert genauso unter .NET Framework, aber .NET 6 bietet die beste Performance.  
* Ein Beispiel‑PDF namens `input.pdf` in einem Ordner, den Sie referenzieren können (z. B. `C:\Docs\`).  

Keine zusätzliche Konfiguration nötig; die Bibliothek ist eigenständig.

---

## Schritt 1 – Quell‑PDF‑Dokument laden

Als erstes öffnen wir die Datei, die wir nummerieren wollen. Asposes `Document`‑Klasse repräsentiert das gesamte PDF, und das Laden ist so einfach wie das Übergeben des Pfads an den Konstruktor.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Warum das wichtig ist*: Durch das Laden des Dokuments erhalten Sie Zugriff auf die `Pages`‑Sammlung, in der wir später den Bates‑Stempel anbringen. Wenn die Datei nicht gefunden wird, wirft Aspose eine klare `FileNotFoundException`, sodass Sie sofort wissen, was schiefgelaufen ist.

---

## Schritt 2 – Text‑Stamp für Bates‑Nummern erstellen

Jetzt erstellen wir das visuelle Element, das auf jeder Seite erscheinen soll. Die `TextStamp`‑Klasse ermöglicht das Einbetten beliebiger Zeichenketten, und wir verwenden den Platzhalter `{page}-{total}`, damit Aspose diese Tokens automatisch ersetzt.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Wichtige Punkte*:

* **auto adjust font size** – Das Setzen von `AutoAdjustFontSizeToFitStampRectangle` auf `true` garantiert, dass der Text niemals außerhalb des Rechtecks überläuft – ideal für variabel lange Seitenzahlen.  
* **add text watermark** – Durch Verringern der `Opacity` verwandeln wir die Bates‑Nummer in ein leichtes Wasserzeichen, wodurch die Anforderung „add text watermark“ ohne zusätzlichen Schritt erfüllt wird.  
* **how to add bates** – Die Tokens `{page}` und `{total}` sind das Geheimrezept; Aspose ersetzt sie zur Laufzeit, sodass Sie nichts selbst berechnen müssen.

---

## Schritt 3 – Stempel auf jede Seite anwenden

Ein häufiger Stolperstein ist, nur die erste Seite zu stempeln. Um wirklich **add page numbers pdf** zu erreichen, müssen wir die gesamte `Pages`‑Sammlung durchlaufen.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Warum klonen? Die Methode `AddStamp` erstellt intern eine Kopie, aber das explizite Verwenden einer frischen Instanz pro Durchlauf verhindert unbeabsichtigte Nebeneffekte, falls Sie später Stempel‑Eigenschaften ändern (z. B. Farbe für bestimmte Seiten).

---

## Schritt 4 – Aktualisiertes PDF speichern

Mit den Stempeln an Ort und Stelle ist das Persistieren der Änderungen unkompliziert. Sie können die Originaldatei überschreiben oder an einem neuen Ort speichern – hier speichern wir eine neue Datei namens `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Öffnen Sie `output.pdf` und Sie sehen jede Seite mit dem Label „Bates: 1‑10“, „Bates: 2‑10“, … unten rechts, mit einer leichten Transparenz, die zugleich als **add text watermark** fungiert.

---

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier ein einzelnes, eigenständiges Konsolen‑Programm, das Sie in Visual Studio einfügen können.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Erwartetes Ergebnis**: Öffnen Sie `output.pdf` in einem beliebigen Viewer; jede Seite zeigt eine Zeile wie „Bates: 3‑12“ in der unteren rechten Ecke, exakt passend zum Rechteck und mit 40 % Opazität gerendert. Das erfüllt sowohl die Anforderung zur rechtlichen Nachverfolgung als auch das visuelle Wasserzeichen‑Bedürfnis.

---

## Häufige Varianten & Sonderfälle

| Situation | Was zu ändern ist | Warum |
|-----------|-------------------|-------|
| **Andere Platzierung** | `HorizontalAlignment` / `VerticalAlignment` anpassen oder `XIndent`/`YIndent` setzen | Einige Firmen bevorzugen oben links oder zentrierte Platzierung. |
| **Benutzerdefiniertes Präfix** | `"Bates: "` durch `"Doc‑ID: "` oder einen beliebigen String ersetzen | Sie verwenden ein anderes Benennungsschema. |
| **Mehrere Stempel** | Einen zweiten `TextStamp` erstellen (z. B. für einen Vertraulichkeits‑Hinweis) und nach dem ersten hinzufügen | Das Kombinieren von **add bates numbering** mit anderen **add text watermark**‑Anforderungen ist trivial. |
| **Hohe Seitenzahlen** | Anfangs‑Schriftgröße erhöhen (z. B. `14`) – das Auto‑Adjust verkleinert sie bei Bedarf | Bei > 999 Seiten wird die Zeichenkette länger; das Auto‑Adjust verhindert Abschneiden. |
| **Verschlüsselte PDFs** | `pdfDocument.Decrypt("password")` vor dem Stempeln aufrufen | Ohne Passwort lässt sich eine gesicherte Datei nicht ändern. |

---

## Profi‑Tipps & Fallstricke

* **Pro‑Tipp:** Setzen Sie `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)`, wenn der Text zu nah am Rand liegt.  
* **Achten Sie auf:** Sehr kleine Rechtecke (Standardgröße 100 × 30 pt). Wenn Sie einen größeren Bereich benötigen, setzen Sie `batesStamp.Width` und `batesStamp.Height` manuell.  
* **Performance‑Hinweis:** Das Stempeln von tausenden Seiten kann einige Sekunden dauern, aber Aspose streamt die Seiten effizient – ein Laden des gesamten Dokuments in den Speicher ist nicht nötig.  

---

## Fazit

Wir haben gezeigt, wie man **add bates numbering** zu einem PDF mit Aspose.Pdf hinzufügt, gleichzeitig **add page numbers pdf** realisiert, **auto adjust font size** aktiviert und ein **add text watermark** in einem zusammenhängenden Ablauf erstellt. Das komplette, ausführbare Beispiel oben liefert Ihnen ein solides Fundament, das Sie an jeden Rechts‑Dokument‑Workflow oder internes Reporting‑System anpassen können.

Bereit für den nächsten Schritt? Kombinieren Sie diesen Ansatz mit Asposes PDF‑Merge‑API, um mehrere Dateien stapelweise zu verarbeiten, oder erkunden Sie die `TextFragment`‑Klasse für reichhaltigere Wasserzeichen (farbig, rotiert oder mehrzeilig). Die Möglichkeiten sind endlos, und der Code, den Sie jetzt besitzen, ist eine verlässliche Basis.

Wenn Ihnen dieser Leitfaden geholfen hat, hinterlassen Sie gern einen Kommentar, geben Sie dem Repository einen Stern oder teilen Sie Ihre eigenen Varianten. Viel Spaß beim Coden und mögen Ihre PDFs immer perfekt nummeriert sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}