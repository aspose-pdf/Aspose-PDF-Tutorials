---
category: general
date: 2026-09-05
description: Erstellen Sie ein PDF‑Dokument in C#, indem Sie eine leere Seite hinzufügen,
  ein Rechteck zeichnen und die PDF‑Datei speichern. Folgen Sie einem Schritt‑für‑Schritt‑Beispiel
  von Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: de
lastmod: 2026-09-05
og_description: Erstellen Sie ein PDF‑Dokument in C#, indem Sie eine leere Seite hinzufügen,
  ein Rechteck zeichnen und die PDF‑Datei speichern. Folgen Sie diesem vollständigen
  Beispiel mit Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: PDF-Dokument mit leerer Seite und Rechteck erstellen – C#‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Wie man ein PDF‑Dokument mit einer leeren Seite und einem Rechteck erstellt
url: /de/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-Dokument mit einer leeren Seite und Rechteck erstellen

Wenn Sie **PDF-Dokument** programmgesteuert erstellen müssen, zeigt Ihnen dieses Handbuch eine vollständige Lösung in C#. Sie lernen, wie Sie eine leere Seite hinzufügen, ein Rechteck auf dieser Seite zeichnen und schließlich die PDF‑Datei speichern. Das Beispiel verwendet die Aspose.PDF‑Bibliothek, die mit .NET 6+ und .NET Framework 4.5+ funktioniert.

Das Hinzufügen einer leeren Seite und das Zeichnen von Formen ist ein häufiges Bedürfnis für Rechnungen, Zertifikate oder benutzerdefinierte Berichte. Am Ende dieses Tutorials besitzen Sie ein ausführbares Projekt, das ein PDF erzeugt, das ein einzelnes Rechteck bei (100, 100) mit einer Größe von 200 × 200 Points enthält.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* Visual Studio 2022 (oder jede C#‑IDE)
* .NET 6 SDK oder .NET Framework 4.5+
* Aspose.PDF for .NET NuGet‑Paket  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Schreibrechte für das Ausgabeverzeichnis

Keine zusätzliche Konfiguration ist erforderlich; der Code läuft sofort einsatzbereit.

## PDF-Dokument erstellen – Übersicht

Der gesamte Prozess besteht aus vier logischen Schritten:

1. **Instantiate** ein `Document`‑Objekt – das repräsentiert die PDF‑Datei.
2. **Add a blank page** – die Seite liefert die Zeichenfläche.
3. **Draw a rectangle** – ein `Path`‑Objekt definiert die Form.
4. **Save the PDF file** – speichert das Dokument auf dem Datenträger.

Jeder Schritt ist in einem eigenen Abschnitt isoliert, sodass Sie Teile bei Bedarf wiederverwenden oder ersetzen können.

![Diagramm eines PDFs mit einem Rechteck auf einer leeren Seite](https://example.com/placeholder-image.png){.img-fluid alt="Screenshot, der ein PDF‑Dokument mit einem gezeichneten Rechteck auf einer leeren Seite zeigt"}

## Leere Seite hinzufügen (pdf)

Ein PDF muss mindestens eine Seite enthalten, bevor Grafiken platziert werden können. Die Methode `Pages.Add()` erzeugt eine leere Seite mit Standardmaßen (A4). Wenn Sie eine andere Größe benötigen, übergeben Sie ein `PageSize`‑Argument.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Warum dieser Schritt wichtig ist* – Das Seitenobjekt enthält Sammlungen für Text, Bilder und Vektorgrafiken. Ohne Seite würde jeder Versuch, ein Rechteck hinzuzufügen, eine Ausnahme auslösen.

### Sonderfall: benutzerdefinierte Seitengröße

Wenn Ihr Layout eine 6 × 9‑Zoll‑Seite erfordert, ersetzen Sie den Standardaufruf durch:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Rechteck zeichnen (pdf)

Ein Rechteck zu zeichnen besteht darin, eine `Rectangle`‑Geometrie zu erstellen und sie in einen `Path` zu verpacken. Der Aufruf `ValidateBounds()` stellt sicher, dass die Form innerhalb der Seitenränder liegt und ein Abschneiden verhindert.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Warum dieser Schritt wichtig ist* – Das `Path`‑Objekt ist das Low‑Level‑Vektor‑Primitive, das von Aspose.PDF verwendet wird. Durch die Validierung der Grenzen vermeiden Sie Laufzeitfehler, wenn das Rechteck die Seitenlimits überschreitet.

### Profi‑Tipp: Rechteck formatieren

Sie können die Strichfarbe und die Linienbreite ändern:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Damit entsteht ein roter Umriss mit einer Dicke von 2 Points.

## PDF‑Datei speichern

Das Persistieren des Dokuments finalisiert die Datei auf dem Datenträger. Die `Save`‑Methode akzeptiert einen Dateipfad oder einen Stream. Die Angabe eines absoluten Pfads macht den Speicherort eindeutig, was für Automatisierungsskripte nützlich ist.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Warum dieser Schritt wichtig ist* – Das Speichern ist der einzige Moment, in dem die In‑Memory‑Repräsentation zu einer physischen Datei wird. Wenn Sie das PDF aus einer Web‑API zurückgeben wollen, ersetzen Sie den Dateipfad durch einen `MemoryStream`.

### Sonderfall: Überschreiben vorhandener Dateien

Aspose.PDF überschreibt standardmäßig eine bestehende Datei. Um frühere Ausgaben zu schützen, prüfen Sie zuerst, ob die Datei existiert:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Wie man ein Rechteck hinzufügt – bewährte Vorgehensweisen

* **Koordinaten innerhalb der Seitenränder halten** – verwenden Sie `ValidateBounds()` oder berechnen Sie die Ränder manuell.
* **`GraphInfo`‑Objekte wiederverwenden**, wenn Sie mehrere Formen zeichnen; das reduziert Speicherzuweisungen.
* **Das `Document`‑Objekt freigeben** (wie mit `using var` gezeigt), um native Ressourcen sofort zu entsorgen.
* **Mit verschiedenen DPI‑Einstellungen testen**, falls Sie später Rasterbilder einbetten; Vektorformen wie Rechtecke bleiben bei jeder Auflösung scharf.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette Programm, das Sie in eine Konsolenanwendung kopieren können. Es kompiliert ohne Änderungen und erzeugt `output.pdf` im Projektordner.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Erwartete Ausgabe

Das Ausführen des Programms erzeugt ein einseitiges PDF. Wenn Sie `output.pdf` öffnen, sehen Sie eine leere weiße Seite mit einem roten Rechteck, das 100 Points vom linken und unteren Rand entfernt ist und 200 × 200 Points misst.

## Fazit

Sie wissen jetzt, wie Sie **PDF-Dokument** erstellen, **leere Seite pdf** hinzufügen, **Rechteck pdf** zeichnen und **pdf‑Datei** speichern können – alles mit Aspose.PDF in C#. Das Beispiel deckt die wesentlichen API‑Aufrufe ab, erklärt, warum jeder Aufruf nötig ist, und gibt Tipps für gängige Variationen wie benutzerdefinierte Seitengrößen oder Rechteck‑Styling.

Als Nächstes können Sie verwandte Themen wie **Text hinzufügen**, **Bilder einbetten** oder **Mehrseitige Berichte erstellen** erkunden. Das gleiche Muster – `Document` instanziieren, Seiten manipulieren, Vektor‑ oder Raster‑Inhalte hinzufügen und dann `Save` – gilt für all diese Szenarien. Experimentieren Sie gern mit verschiedenen Formen, Farben und Seitenlayouts, um die Anforderungen Ihres Projekts zu erfüllen.


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [PDF-Dokument in C# erstellen – Seite hinzufügen, Rechteck zeichnen & speichern](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [PDF-Dokument mit Aspose.PDF erstellen – Schritt‑für‑Schritt‑Anleitung](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [PDF-Dokument mit Aspose erstellen – Seite, Textfeld und Formular hinzufügen](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}