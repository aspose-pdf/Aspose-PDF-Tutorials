---
category: general
date: 2026-07-20
description: 'PDF-Dokument in C# mit Aspose.Pdf erstellen: Text im PDF positionieren
  und strukturellen Baum für Barrierefreiheit hinzufügen. Befolgen Sie diese Schritt‑für‑Schritt‑Anleitung.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: de
lastmod: 2026-07-20
og_description: Erstellen Sie sofort ein PDF-Dokument mit C#. Erfahren Sie, wie Sie
  Text im PDF positionieren und einen Strukturbaum hinzufügen, um die PDF/A‑2b‑Konformität
  mit Aspose.Pdf zu erreichen.
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: PDF-Dokument mit C# erstellen – Vollständiger Leitfaden zur Positionierung
  von Text und Tag‑Struktur
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: PDF-Dokument erstellen in C# – Text positionieren und Strukturbaum hinzufügen
url: /de/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-Dokument erstellen C# – Text positionieren und Strukturbaum hinzufügen

Haben Sie jemals **PDF-Dokument erstellen C#** benötigt, das nicht nur Text genau dort platziert, wo Sie ihn haben möchten, sondern auch einen korrekten Strukturbaum für Barrierefreiheit einbettet? Sie sind nicht allein – Entwickler, die Rechnungen, Berichte oder E‑Books erstellen, stoßen ständig auf dieses Bedürfnis. In diesem Tutorial führen wir Sie durch ein komplettes, sofort ausführbares Beispiel, das genau das tut, und zwar mit der leistungsstarken Aspose.Pdf-Bibliothek.

Wir zeigen, wie man **Text im PDF positioniert**, ein semantisches Tag über den Schritt **Strukturbaum hinzufügen** anfügt und schließlich die Datei als PDF/A‑2b‑konformes Dokument speichert. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jedes .NET‑Projekt einbinden können.

---

## Was Sie benötigen

- **.NET 6.0** oder höher (der Code funktioniert auch mit .NET Framework 4.6+)  
- **Aspose.Pdf for .NET** NuGet‑Paket (`Install-Package Aspose.Pdf`)  
- Eine grundlegende C#‑Entwicklungsumgebung (Visual Studio, Rider oder VS Code)  

Keine zusätzlichen Drittanbieter‑Tools sind erforderlich; die Bibliothek übernimmt alles von der Seitenlayout‑ bis zur PDF/A‑Konformität.

---

## Schritt 1: PDF-Dokument initialisieren (PDF-Dokument erstellen C#)

Das erste, was wir tun, ist ein frisches `Document`‑Objekt zu erzeugen. Denken Sie daran wie an eine leere Leinwand – noch nichts darauf, aber bereit, Seiten, Text und strukturelle Metadaten aufzunehmen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **Warum das wichtig ist:** Die `Document`‑Klasse ist der Einstiegspunkt für alle Aspose.Pdf‑Operationen. Das frühe Hinzufügen einer Seite gibt uns eine Oberfläche, an die wir sowohl visuelle Inhalte als auch später den Strukturbaum anhängen können.

---

## Schritt 2: Absatz definieren und positionieren (Text im PDF positionieren)

Jetzt erstellen wir ein `Paragraph`‑Objekt und teilen Aspose mit, wo genau auf der Seite es erscheinen soll. PDF‑Koordinaten werden in Punkten gemessen (1 Zoll = 72 pt), daher verwenden wir `Position(72, 720)`, um den Absatz 1 Zoll vom linken Rand und 10 Zoll vom unteren Rand zu platzieren.

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **Pro‑Tipp:** Wenn Sie mehrere Zeilen positionieren müssen, passen Sie die `Y`‑Koordinate für jeden nachfolgenden Absatz an oder verwenden Sie einen `TextBuilder` für feinere Kontrolle.

---

## Schritt 3: Strukturelles Element erstellen (Strukturbaum hinzufügen)

Barrierefreie PDFs basieren auf einem *Strukturbaum*, der die logische Reihenfolge des Inhalts beschreibt. Hier erstellen wir ein `StructureElement` mit dem Tag `"P"` (Paragraph) und hängen unseren positionierten Absatz als Kind an.

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **Warum wir einen Strukturbaum hinzufügen:** Screen‑Reader und andere Hilfstechnologien nutzen diese Tags, um durch das Dokument zu navigieren. Ohne sie ist Ihr PDF zwar visuell perfekt, aber nicht zugänglich.

---

## Schritt 4: Strukturelles Element an die Seite anhängen

Jede Seite verwaltet ihre eigene Sammlung von Strukturelementen. Indem wir unser `structElement` zu `pdfPage.StructElements` hinzufügen, integrieren wir die logische Hierarchie in das visuelle Layout.

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **Häufiges Stolper‑Problem:** Wenn dieser Schritt vergessen wird, existiert das Tag nur im Speicher, ist aber keiner Seite zugeordnet, sodass die Barrierefreiheits‑Informationen für Leser unsichtbar bleiben.

---

## Schritt 5: Als PDF/A‑2b speichern (Langzeitarchivierung sicherstellen)

PDF/A‑2b ist ein Unterset­z von PDF, das für die Archivierung entwickelt wurde. Aspose.Pdf kann dieses Format mit einem einzigen Aufruf erzeugen. Ersetzen Sie `"YOUR_DIRECTORY"` durch einen tatsächlichen Pfad auf Ihrem Rechner.

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **Ergebnis:** Sie erhalten ein PDF, bei dem der Text exakt dort sitzt, wo Sie ihn platziert haben, und das Dokument enthält einen korrekten Strukturbaum für Barrierefreiheits‑Tools.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette Programm, das Sie in eine Konsolen‑App kopieren‑und‑einfügen können. Es kompiliert und läuft sofort (nachdem Sie den Aspose.Pdf‑NuGet‑Verweis hinzugefügt haben).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**Erwartete Ausgabe:** Nach dem Ausführen öffnen Sie `TaggedWithPosition.pdf`. Sie sehen den Satz „Tagged paragraph at a specific location.“ nahe der unteren rechten Ecke der ersten Seite. Wenn Sie die PDF‑Tags (z. B. mit dem „Tags“-Paneel von Adobe Acrobat) inspizieren, finden Sie ein `<P>`‑Element, das mit diesem Absatz verknüpft ist.

---

![Screenshot of positioned text in a PDF generated with Aspose.Pdf](/images/pdf-positioned.png){: .align-center }

*Bildbeschreibung:* **create pdf document c#** – Screenshot, der positionierten Text in einem mit Aspose.Pdf erzeugten PDF zeigt.

---

## Häufige Fragen & Sonderfälle

### Kann ich andere Einheiten (mm, cm) für die Positionierung verwenden?

Aspose.Pdf arbeitet nativ mit Punkten. Wenn Sie Millimeter bevorzugen, konvertieren Sie mit `1 mm ≈ 2.83465 pt`. Zum Beispiel platziert `Position(25.4, 254)` den Absatz 1 cm vom linken Rand und 9 cm vom unteren Rand.

### Was ist, wenn ich mehrere Tags hinzufügen muss (Überschriften, Tabellen)?

Erstellen Sie einfach weitere `StructureElement`‑Objekte mit Tags wie `"H1"` für Überschriften oder `"Table"` für Tabellen und fügen Sie den entsprechenden Inhalt als Kinder hinzu. Das Verschachteln funktioniert gleich – Kinder erben die logische Reihenfolge des Eltern‑Elements.

### Funktioniert dieser Ansatz für PDF/A‑1b oder PDF/A‑3b?

Ja. Ersetzen Sie `SaveFormat.PdfA2b` durch `SaveFormat.PdfA1b` oder `SaveFormat.PdfA3b`. Beachten Sie, dass jede PDF/A‑Version ihre eigenen Metadaten‑Anforderungen hat; Aspose.Pdf wird Sie warnen, falls etwas fehlt.

---

## Zusammenfassung

Wir haben ein **PDF-Dokument erstellen C#**‑Szenario durchlaufen, das:

1. Ein neues PDF mit Aspose.Pdf instanziiert.  
2. **Text im PDF positioniert**, indem genaue Koordinaten gesetzt werden.  
3. **Strukturbaum**‑Elemente für Barrierefreiheit hinzufügt.  
4. Das Ergebnis als standard‑konformes PDF/A‑2b‑Dokument speichert.

Alle Schritte sind vollständig eigenständig und Sie können das Snippet für komplexere Layouts, mehrere Seiten oder verschiedene Tag‑Typen anpassen.

---

## Was kommt als Nächstes?

- **Text formatieren** – erkunden Sie `TextState`, um Schriftarten, Farben und Größen zu ändern.  
- **Bilder einbetten** – verwenden Sie `ImageFragment` und positionieren Sie es neben dem Absatz.  
- **Tabellen erzeugen** – erstellen Sie `Table`‑Objekte und taggen Sie sie mit `"Table"` für reichere Semantik.  
- **Automatisierungspipelines** – integrieren Sie diesen Code in einen Hintergrund‑Service, der nachts Rechnungen generiert.

Probieren Sie es aus und teilen Sie uns mit, welche Varianten Sie am nützlichsten finden. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Erstellen von getaggten PDFs mit Aspose.PDF für .NET: Ein vollständiger Leitfaden zur Verbesserung von Barrierefreiheit und Dokumentenstruktur](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [PDF-Dokument mit Aspose.PDF erstellen – Schritt‑für‑Schritt‑Anleitung](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Text in PDFs erstellen & drehen mit Aspose.PDF .NET: Ein umfassender Leitfaden für Entwickler](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}