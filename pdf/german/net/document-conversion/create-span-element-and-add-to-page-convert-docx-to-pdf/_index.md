---
category: general
date: 2026-03-27
description: Erstellen Sie ein Span‑Element in C# und lernen Sie, wie Sie ein Span
  zu einer Seite hinzufügen, während Sie DOCX in PDF konvertieren und als PDF speichern.
  Schritt‑für‑Schritt‑Anleitung für Entwickler.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: de
og_description: Erstellen Sie ein Span-Element in C# und lernen Sie, wie Sie ein Span
  zu einer Seite hinzufügen, während Sie DOCX in PDF konvertieren, und dann als PDF
  speichern. Vollständiges Codebeispiel enthalten.
og_title: Span-Element erstellen und zur Seite hinzufügen – DOCX in PDF konvertieren
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Span-Element erstellen und zur Seite hinzufügen – DOCX in PDF konvertieren
url: /de/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Span-Element erstellen und zur Seite hinzufügen – DOCX in PDF konvertieren

Ein **Span-Element** in einer DOCX-Datei zu erstellen ist eine gängige Aufgabe, wenn Sie eine präzise Layout‑Kontrolle benötigen. In diesem Tutorial zeigen wir Ihnen **wie man ein Span** zu einer Seite hinzufügt, **DOCX in PDF konvertiert** und **als PDF speichert** – alles in wenigen übersichtlichen Schritten.  

Wenn Sie jemals auf ein Word‑Dokument gestarrt haben und gedacht haben: „Ich wünschte, ich könnte ein winziges Textfeld an einer genauen Koordinate platzieren“, dann sind Sie hier genau richtig. Wir führen Sie durch den gesamten Workflow, vom Laden der Quelldatei bis zum fertigen PDF‑Ergebnis.

## Was Sie erreichen werden

* Laden Sie eine `.docx`‑Datei mit der `Document`‑Klasse der Dokumentbibliothek.  
* **Span-Element erstellen** mit der `TaggedContent`‑API.  
* Positionieren Sie dieses Span an genauen X/Y‑Koordinaten auf einer gewählten Seite.  
* **Element zur Seite hinzufügen** zuverlässig, selbst wenn die Seite nicht die erste ist.  
* **DOCX in PDF konvertieren** und **als PDF speichern** mit einem einzigen `Save`‑Aufruf.

Keine externen Werkzeuge, keine mysteriösen Einstellungen – nur reiner C#‑Code, den Sie in Ihr Projekt kopieren‑und‑einfügen können.

## Voraussetzungen

* .NET 6+ (oder jede aktuelle .NET‑Runtime, die Ihre Bibliothek unterstützt).  
* Das Dokumenten‑Verarbeitungs‑SDK, das `Document`, `TaggedContent`, `Position` usw. bereitstellt.  
* Grundlegende Kenntnisse der C#‑Syntax – wenn Sie ein `Console.WriteLine` schreiben können, sind Sie bereit.

> **Profi‑Tipp:** Halten Sie Ihre SDK‑Version aktuell; die neueste Version (v3.2 ab März 2026) enthält Leistungsverbesserungen für Vorgänge auf Seitenebene.

---

![Diagram illustrating how to create span element and place it on a PDF page](https://example.com/images/create-span-element.png "Create span element placement diagram")

## Span-Element erstellen – Positionieren und zur Seite hinzufügen

Im Folgenden finden Sie den vollständigen, ausführbaren Code, der alles von dem Laden der Quell‑DOCX bis zum Schreiben des finalen PDFs erledigt. Sie können ihn einfach in eine Konsolen‑App einfügen, die Pfade anpassen und ausführen.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Schritt‑für‑Schritt‑Erklärung

#### Schritt 1 – DOCX-Dokument laden  
Wir instanziieren ein `Document`‑Objekt, das auf `input.docx` zeigt. Dieses Objekt repräsentiert die gesamte Word‑Datei im Speicher und gibt uns Zugriff auf Seiten, Inhalte und Metadaten.  

#### Schritt 2 – Span-Element erstellen  
Der Aufruf `TaggedContent.CreateSpanElement()` liefert einen leichten Inline‑Container. Stellen Sie sich das als ein winziges, unsichtbares Kästchen vor, das Text, Bilder oder andere Inline‑Elemente aufnehmen kann. Das Hinzufügen von Text (`span.Text`) ist optional, aber für Debug‑Zwecke nützlich.  

#### Schritt 3 – Span positionieren  
`new Position(50, 750)` setzt die obere linke Ecke des Spans 50 pts vom linken Rand und 750 pts vom oberen Rand der Seite. Diese Werte sind absolut, sodass Sie das Span überall platzieren können – ideal für präzise Layouts.  

#### Schritt 4 – Span zur Zielseite hinzufügen  
`doc.Pages[1].Add(span)` fügt das Span in die zweite Seite ein. Die API verwendet nullbasierte Indizierung, sodass Seite 0 die erste Seite ist. Wenn Sie es auf die erste Seite setzen wollen, verwenden Sie einfach `doc.Pages[0]`.  

#### Schritt 5 – DOCX in PDF konvertieren und als PDF speichern  
Der Aufruf `doc.Save("output.pdf")` erledigt zwei Dinge: Er schreibt das modifizierte Dokument auf die Festplatte **und** konvertiert den Inhalt dank der `.pdf`‑Erweiterung in PDF. Kein zusätzlicher Konvertierungsschritt ist nötig – das ist der einfachste Weg, **als PDF zu speichern**.  

---

## Wie man ein Span auf einer anderen Seite hinzufügt (fortgeschritten)

Manchmal kennen Sie den Seitenindex im Voraus nicht. Sie können eine Seite anhand ihrer Nummer (menschenfreundlich) oder durch Suchen nach einem bestimmten Schlüsselwort finden.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Warum das wichtig ist:** In Berichten, bei denen die Seitenzahl variiert, kann das harte Kodieren von `Pages[1]` das Layout zerstören. Dieses Snippet zeigt ein robustes Muster, um **wie man ein Span** dynamisch hinzufügt.

---

## Häufige Fallstricke und wie man sie vermeidet

| Problem | Was passiert | Lösung |
|---------|--------------|--------|
| **Span nicht sichtbar** | Koordinaten liegen außerhalb der Seite oder das Span hat Breite/Höhe 0. | Überprüfen Sie die `Position`‑Werte; verwenden Sie ein Lineal in Ihrem PDF‑Betrachter. |
| **Falscher Seitenindex** | Sie fügen zu Seite 0 hinzu, erwarten es aber auf Seite 2. | Denken Sie daran, dass die API nullbasiert ist; addieren Sie 1 zur menschlichen Seitennummer. |
| **Speichern überschreibt Quelle** | `doc.Save("input.docx")` ersetzt die Originaldatei. | Speichern Sie immer in einen neuen Pfad (`output.pdf`) beim Konvertieren. |
| **Fehlende SDK‑Referenz** | Kompilierungsfehler bei der `Document`‑Klasse. | Installieren Sie das NuGet‑Paket: `dotnet add package DocumentProcessing.SDK`. |

---

## Ergebnis überprüfen

Nach dem Ausführen des Programms öffnen Sie `output.pdf` in einem beliebigen PDF‑Betrachter. Sie sollten den Text „Hello, world!“ exakt bei (50, 750) auf der zweiten Seite sehen. Wenn der Text an anderer Stelle erscheint, passen Sie die `Position`‑Werte an und führen Sie das Programm erneut aus.  

Für automatisierte Tests können Sie einen PDF‑Parser (z. B. iTextSharp) verwenden, um die Koordinaten des Textes programmgesteuert zu prüfen.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Nächste Schritte

* **Span formatieren** – erkunden Sie `span.Font`, `span.Color` und weitere Stil‑Eigenschaften.  
* **Bilder hinzufügen** – verwenden Sie `CreateImageElement()` anstelle eines Span für Grafiken.  
* **Batch‑Verarbeitung** – iterieren Sie über einen Ordner mit DOCX‑Dateien  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}