---
category: general
date: 2026-03-03
description: PDF-Dokument in C# mit Bates‑Nummerierung erstellen – erfahren Sie, wie
  Sie Bates hinzufügen, fortlaufende Seitenzahlen einfügen und Bates in nur wenigen
  Schritten generieren.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: de
og_description: PDF-Dokument in C# mit Bates‑Nummerierung erstellen. Dieser Leitfaden
  zeigt, wie man Bates hinzufügt, fortlaufende Seitenzahlen einfügt und Bates schnell
  generiert.
og_title: PDF-Dokument in C# erstellen – Bates‑Nummerierung hinzufügen
tags:
- C#
- PDF
- Bates numbering
title: PDF-Dokument in C# erstellen – Bates‑Nummerierung hinzufügen
url: /de/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF‑Dokument in C# erstellen – Bates‑Nummerierung hinzufügen

Haben Sie schon einmal **create PDF document C#** benötigt und anschließend jede Seite mit einem eindeutigen Kennzeichen für rechtliche oder archivierte Zwecke versehen wollen? Sie sind nicht allein – Anwaltskanzleien, Gerichte und sogar große Unternehmen fragen ständig: „Wie füge ich automatisch Bates‑Nummern zu meinen PDFs hinzu?“ Die gute Nachricht: Mit nur wenigen Code‑Zeilen können Sie ein PDF erzeugen, Bates‑Nummern auf jeder Seite verteilen und das Ergebnis speichern, ohne einen Editor zu öffnen.

In diesem Tutorial führen wir Sie durch ein praktisches End‑zu‑End‑Beispiel, das zeigt, **how to add bates**, **add sequential page numbers** und sogar **how to generate bates** mit benutzerdefinierten Präfixen. Am Ende besitzen Sie ein wiederverwendbares Snippet, das Sie in jedes .NET‑Projekt einbinden können.

## Was Sie benötigen

- **.NET 6+** (der Code funktioniert auch mit .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – eine kommerzielle Bibliothek, die eine saubere API für die PDF‑Manipulation bietet. Eine kostenlose Evaluation reicht für Tests aus.
- Grundlegende Kenntnisse in C# (Sie sind wahrscheinlich bereits mit `using`‑Anweisungen und Objekten vertraut).

Es werden keine zusätzlichen NuGet‑Pakete über `Aspose.Pdf` hinaus benötigt. Wenn Sie es noch nicht installiert haben, führen Sie aus:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Halten Sie Ihre Aspose‑Version aktuell; das neueste 23.x‑Release enthält Performance‑Optimierungen für große Dokumente.

## Schritt 1: Öffnen (oder Erstellen) des Quell‑PDF‑Dokuments

Zuerst benötigen wir ein PDF, mit dem wir arbeiten können. In vielen realen Szenarien haben Sie bereits eine Eingabedatei – zum Beispiel einen gescannten Vertrag. Für das Beispiel öffnen wir eine vorhandene Datei namens `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Why this matters:** Das Öffnen des Dokuments innerhalb eines `using`‑Blocks stellt sicher, dass der Dateihandle sofort freigegeben wird, wodurch Dateisperren vermieden werden, wenn Sie später dieselbe Datei überschreiben wollen.

## Schritt 2: Definieren Ihrer Bates‑Nummerierungsoptionen

Bates‑Nummern bestehen aus einem **prefix** (oft ein Fall‑Identifier) und einer **starting number**. Sie können zudem die Anzahl der Stellen, die Platzierung auf der Seite und den Schriftstil steuern. Hier verwenden wir das sekundäre Stichwort **add bates numbering pdf**, indem wir ein `BatesNumberingOptions`‑Objekt konfigurieren.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **How to add bates:** Durch Anpassen von `Prefix` und `Start` bestimmen Sie exakt den String, der auf jeder Seite erscheint. Die Eigenschaft `NumberOfDigits` sorgt für eine einheitliche Breite, was bei juristischen Einreichungen praktisch ist.

## Schritt 3: Bates‑Nummerierung auf jede Seite anwenden

Jetzt kommt die Kernoperation – das Hinzufügen der Nummern. Die Methode `AddBatesNumbering` durchläuft jede Seite, zeichnet den Text und beachtet die zuvor definierten Optionen.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Unter der Haube rendert Aspose den Text als *content*‑Element, sodass die Nummern Teil des PDFs werden und in einem Viewer nicht ausgeschaltet werden können. Genau das benötigen Sie, wenn Sie **add sequential page numbers** unveränderlich einfügen wollen.

### Edge Cases & Variations

- **Multiple prefixes:** Wenn Sie unterschiedliche Präfixe pro Abschnitt benötigen, erstellen Sie separate `BatesNumberingOptions` und rufen `AddBatesNumbering` für einen Seitenbereich (`pdfDocument.Pages[1..5]`) auf.
- **Zero‑padding control:** Lassen Sie `NumberOfDigits` weg für eine variable Länge, oder setzen Sie es auf einen höheren Wert für führende Nullen.
- **Custom positioning:** Verwenden Sie `Margin`, um die Nummer vom Rand zu versetzen, oder wechseln Sie `HorizontalAlignment` zu `Center` für eine Fußzeilen‑Darstellung.

## Schritt 4: Das modifizierte PDF speichern

Zum Schluss schreiben wir das aktualisierte Dokument auf die Festplatte. Sie können die Originaldatei überschreiben oder eine brandneue Datei erstellen.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

Nachdem diese Zeile ausgeführt wurde, enthält `output.pdf` den ursprünglichen Inhalt plus ein sichtbares Bates‑Tag auf jeder Seite – genau das, was Sie erwarten, wenn Sie **how to generate bates** für eine Falldatei benötigen.

## Vollständiges, ausführbares Beispiel

Alles zusammengefügt, hier das komplette Snippet, das Sie in eine Konsolen‑App kopieren‑und‑einfügen können:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Erwartetes Ergebnis

Öffnen Sie `output.pdf` in einem beliebigen Viewer (Adobe Reader, Edge usw.). Jede Seite ist mit etwas wie **CASE-001000**, **CASE-001001**, … bis zur letzten Seite versehen. Die Nummern sitzen bündig unten rechts und entsprechen den von uns gesetzten Optionen.

## Häufige Fragen & Fehlersuche

- **„Was, wenn mein PDF passwortgeschützt ist?“**  
  Laden Sie es mit dem Passwort: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **„Kann ich Bates‑Nummern zu einem neu erstellten PDF hinzufügen?“**  
  Absolut. Erstellen Sie das Dokument zuerst (`var doc = new Document();`) und führen Sie dann die Schritte 2‑4 vor dem Speichern aus.

- **„Ist die Schriftart immer eingebettet?“**  
  Aspose bettet die Schriftart automatisch ein, falls sie noch nicht im PDF vorhanden ist. Wenn Sie eine bestimmte Schriftfamilie benötigen, setzen Sie `options.Font` entsprechend.

- **„Wie ist die Performance bei 10.000‑Seiten‑Dateien?“**  
  Die Bibliothek streamt die Seiten, sodass der Speicherverbrauch gering bleibt. Dennoch könnten Sie `PdfSaveOptions.CompressionMode` erhöhen, um die I/O‑Geschwindigkeit zu steigern.

## Pro‑Tipps für den Produktionseinsatz

1. **Batch processing:** Verpacken Sie die obige Logik in eine Schleife, die einen Ordner mit PDFs durchläuft. Verwenden Sie `Directory.GetFiles("*.pdf")` und verarbeiten Sie jede Datei einzeln.
2. **Logging:** Schreiben Sie die erste und letzte Bates‑Nummer in eine Log‑Datei – das hilft Prüfern, die Kontinuität der Nummerierung zu verifizieren.
3. **Error handling:** Umschließen Sie den gesamten Block mit einem `try/catch` und geben Sie eine klare Meldung aus, wenn das Quell‑PDF fehlt oder beschädigt ist.
4. **Zero‑padding flexibility:** Wenn Sie die Stellenzahl dynamisch anhand der Gesamtseitenzahl bestimmen wollen, berechnen Sie `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Fazit

Wir haben gerade gezeigt, wie man **create PDF document C#** und nahtlos **add Bates numbering** durchführt – von der ersten Ladung bis zum finalen Speichern. Das kurze Beispiel demonstriert **how to add bates**, **add sequential page numbers** und **how to generate bates** mit benutzerdefinierten Präfixen und Null‑Auffüllung. Mit ein paar Anpassungen lässt sich dieses Muster für Batch‑Jobs, unterschiedliche Layouts oder sogar die Integration in eine Web‑API nutzen, die bei Bedarf ein frisch nummeriertes PDF zurückgibt.

Bereit für den nächsten Schritt? Kombinieren Sie dies mit Aspose’s **watermark**‑Funktion oder erzeugen Sie ein Inhalts‑Index, das jede Bates‑Nummer zusammen mit einer kurzen Beschreibung des Seiteninhalts auflistet. Die Möglichkeiten sind endlos, und der Code, den Sie jetzt besitzen, bildet ein solides Fundament für jede Dokument‑Automatisierungs‑Workflow.

Viel Spaß beim Coden und mögen Ihre PDFs stets perfekt nummeriert sein!

![Screenshot eines PDF‑Viewers, der das erstellte PDF‑Dokument C# mit angewendeten Bates‑Nummern zeigt](image-placeholder.png "PDF‑Dokument C# mit Bates‑Nummern")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}