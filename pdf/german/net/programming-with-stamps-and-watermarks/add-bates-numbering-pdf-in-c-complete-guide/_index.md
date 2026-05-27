---
category: general
date: 2026-05-27
description: Bates-Nummerierung zu PDF mit Aspose.Pdf in C# hinzufügen. Erfahren Sie,
  wie Sie die Bates-Nummerierung schnell einfügen, das Format anpassen und die Kennzeichnung
  juristischer Dokumente automatisieren.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: de
og_description: Bates-Nummerierung zu PDF mit Aspose.Pdf in C# hinzufügen. Diese Anleitung
  zeigt, wie man Bates-Nummerierung hinzufügt, Präfixe konfiguriert und das Ergebnis
  speichert.
og_title: Bates‑Nummerierung zu PDF in C# hinzufügen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Bates-Nummerierung zu PDF in C# hinzufügen – Vollständiger Leitfaden
url: /de/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑Nummerierung zu PDF in C# hinzufügen – Komplett‑Anleitung

Haben Sie sich schon einmal gefragt, **wie man Bates‑Nummern** zu einem PDF hinzufügt, ohne stundenlang mit manuellen Werkzeugen zu hantieren? Sie sind nicht allein – Rechtsabteilungen, Prüfer und E‑Discovery‑Spezialisten benötigen alle eine zuverlässige Methode, um **Bates‑Nummerierung PDF**‑Dateien programmgesteuert hinzuzufügen.  

In diesem Tutorial führen wir Sie durch eine kompakte, durchgängige Lösung mit Aspose.Pdf für .NET, sodass Sie Bates‑Nummern mit nur wenigen Zeilen C#‑Code auf jedes Dokument setzen können.

## Was Sie lernen werden

- Wie man ein bestehendes PDF mit Aspose.Pdf öffnet  
- Wie man ein Bates‑Numbering‑Artifact erstellt und dessen Format feinjustiert  
- Wie man das Artifact jeder Seite (oder nur der ersten) zuweist  
- Wie man die aktualisierte Datei speichert und das Ergebnis prüft  

Vorkenntnisse mit Aspose sind nicht nötig – ein Grundverständnis von C# und .NET reicht. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jedes Projekt kopieren können.

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+)  
- Aspose.Pdf für .NET NuGet‑Paket (`Install-Package Aspose.Pdf`)  
- Eine Quell‑PDF‑Datei, die Sie markieren möchten (legen Sie sie in einem Ordner ab, den Sie referenzieren können)

> **Pro‑Tipp:** Wenn Sie noch keine Lizenz haben, bietet Aspose einen kostenlosen temporären Schlüssel an, der Evaluations‑Wasserzeichen entfernt.

## Schritt 1 – Das Quell‑PDF‑Dokument öffnen  

Zuerst benötigen wir ein `Document`‑Objekt, das die Datei auf der Festplatte repräsentiert. Stellen Sie sich das vor wie das Laden einer leeren Leinwand, auf die wir später die Bates‑Nummern malen.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Warum das wichtig ist:** Das Öffnen des Dokuments innerhalb eines `using`‑Blocks sorgt dafür, dass alle nicht verwalteten Ressourcen sofort freigegeben werden – besonders wichtig bei großen PDFs.

## Schritt 2 – Ein Bates‑Numbering‑Artifact erstellen  

Ein *BatesNumberingArtifact* ist Asposes Art, zu beschreiben, wie die Nummern aussehen sollen. Sie können ein Präfix, die Startnummer, den Inkrementwert und sogar einen benutzerdefinierten Format‑String festlegen.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Warum Sie diese Werte ändern könnten:**  
- **Prefix** ist nützlich für Fall‑IDs („CASE‑“, „DOC‑“).  
- **StartNumber** ermöglicht das Fortsetzen einer vorherigen Serie.  
- **Increment** kann auf 2 gesetzt werden, wenn Sie ungerade/gerade Nummerierung benötigen.  
- **Format** unterstützt jedes .NET‑Composite‑Format; `{0:D5}` garantiert fünf Stellen mit führenden Nullen.

## Schritt 3 – Das Artifact den gewünschten Seiten zuweisen  

Sie können das Artifact einer einzelnen Seite, einem Bereich oder dem gesamten Dokument hinzufügen. Für die meisten juristischen Workflows fügen wir es *jeder* Seite hinzu, das untenstehende Beispiel zeigt jedoch den Minimalfall – das Hinzufügen zur ersten Seite.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Falls Sie alle Seiten abdecken wollen, iterieren Sie über sie:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Warum dieser Schritt entscheidend ist:** Artifacts werden *nach* dem Seiteninhalt gerendert, sodass die Nummern über dem bestehenden Text liegen, ohne das ursprüngliche Layout zu verändern.

## Schritt 4 – Das modifizierte PDF speichern  

Zum Schluss schreiben wir die Änderungen zurück auf die Festplatte. Sie können die Originaldatei überschreiben oder eine neue Datei erzeugen – hier erzeugen wir eine frische Kopie namens `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Wenn Sie `bates.pdf` öffnen, sehen Sie „ABC01000“ (oder das von Ihnen gewählte Format) an der Standardposition – üblicherweise unten rechts.

## Vollständiges funktionierendes Beispiel  

Alles zusammengefügt, hier das komplette Programm, das Sie kompilieren und ausführen können:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Erwartete Ausgabe

Beim Ausführen des Programms gibt die Konsole Folgendes aus:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Das Öffnen von `bates.pdf` zeigt das Präfix „ABC“ gefolgt von einer nullgepolsterten fünfstelligen Sequenz auf jeder Seite – genau das, was der Code bewirken soll.

## Häufige Fragen & Sonderfälle

### Kann ich die Position der Bates‑Nummer ändern?

Ja. Verwenden Sie die `Location`‑Eigenschaft des `BatesNumberingArtifact` (z. B. `Location = new Position(10, 10)`) um die Nummer an benutzerdefinierten X/Y‑Koordinaten zu platzieren. Außerdem können Sie `HorizontalAlignment` und `VerticalAlignment` für mehr Kontrolle setzen.

### Was, wenn mein PDF tausende Seiten hat?

Aspose.Pdf streamt Seiten effizient, dennoch ist es ratsam, in Batches zu verarbeiten, falls Speichergrenzen erreicht werden. Die `Document`‑Klasse unterstützt zudem `PdfConverter` für inkrementelles Speichern.

### Wie ändere ich Schriftart oder Farbe?

Umwickeln Sie das Artifact mit einem `TextState`‑Objekt:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Brauche ich eine Lizenz für den Produktionseinsatz?

Eine lizenzierte Version entfernt Evaluations‑Wasserzeichen und schaltet die volle Performance frei. Die kostenlose Testversion reicht für Tests und Proof‑of‑Concepts aus.

## Verifikation – Schneller visueller Check  

Wenn Sie eine automatisierte Prüfung bevorzugen, kann Aspose den Text einer Seite extrahieren und das Vorhandensein des Präfixes bestätigen:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Wird dies nach dem Speicherschritt ausgeführt, gibt es `Bates number verified.` aus, wenn alles reibungslos verlief.

## Fazit  

Sie wissen jetzt **wie man Bates‑Nummerierung PDF**‑Dateien mit Aspose.Pdf in C# hinzufügt. Vom Öffnen des Dokuments über die Konfiguration des Artifacts, das Anbringen an den Seiten bis zum Speichern – der Prozess ist unkompliziert und vollständig skriptbar.  

Nächste Schritte? Experimentieren Sie mit:

- Unterschiedlichen `Prefix`‑Werten für mehrere Fall‑Batches  
- Benutzerdefinierten `Location`‑ und `TextState`‑Einstellungen für Branding  
- Seiten‑spezifischen Präfixen (z. B. „VOL‑1‑“, „VOL‑2‑“) durch Anpassen von `StartNumber` pro Schleifendurchlauf  

Diese Anpassungen ermöglichen Ihnen, die Lösung an fast jeden juristischen oder archivierenden Workflow anzupassen.  

Haben Sie weitere Fragen zu **wie man Bates‑Nummerierung** für mehrsprachige PDFs oder verschlüsselte Dateien hinzufügt? Hinterlassen Sie einen Kommentar unten, und happy coding!

## Verwandte Tutorials

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Different Headers in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}