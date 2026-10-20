---
category: general
date: 2026-08-14
description: Zeichnen Sie schnell ein Rechteck in ein PDF mit C#. Erfahren Sie, wie
  Sie Rechtecksmaße definieren und Formen zu einer PDF‑Seite in nur wenigen Zeilen
  hinzufügen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: de
lastmod: 2026-08-14
og_description: Rechteck in PDF mit C# in Sekunden zeichnen. Dieser Leitfaden zeigt,
  wie man Rechteckabmessungen definiert, eine Form hinzufügt und Seitenränder überprüft,
  um zuverlässige PDF‑Grafiken zu erstellen.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: Rechteck auf PDF zeichnen – vollständiges C#‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Rechteck in PDF zeichnen – Schritt‑für‑Schritt C#‑Leitfaden
url: /de/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rechteck auf PDF zeichnen – vollständiges C#‑Tutorial

Wenn Sie **ein Rechteck auf PDF** mit C# zeichnen möchten, zeigt Ihnen dieser Leitfaden eine kompakte, produktionsreife Lösung. Sie sehen genau **wie man Rechteck‑Abmessungen definiert**, prüft, ob die Form passt, und fügt sie mit einem einzigen Methodenaufruf einer Seite hinzu.

Das Tutorial deckt alles ab, vom Erstellen eines PDF‑Dokuments bis zum Rendern des Rechtecks, sodass Sie den Code einfach in Ihr Projekt kopieren und sofort Ergebnisse sehen können. Keine externe Dokumentation nötig – nur die nachfolgenden Schritte.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+)
* Das **Aspose.PDF for .NET** NuGet‑Paket (`Install-Package Aspose.PDF`)
* Grundlegende Kenntnisse der C#‑Syntax
* Eine IDE wie Visual Studio oder VS Code

> **Pro‑Tipp:** Nutzen Sie die kostenlose Evaluierungslizenz von Aspose.PDF für schnelle Experimente; sie fügt ein kleines Wasserzeichen hinzu, lässt Sie aber alle Funktionen testen.

## Wie man ein Rechteck auf PDF mit C# zeichnet

Der Kern der Aufgabe besteht darin, ein `RectangleShape` zu erstellen, seine Größe und Kontur zu setzen und es an eine `Page` anzuhängen. Die folgende H2‑Überschrift enthält das Haupt‑Keyword und erfüllt damit die SEO‑Anforderungen.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Erklärung jedes Schrittes

| Schritt | Warum das wichtig ist |
|------|----------------|
| **1️⃣ Neues PDF‑Dokument erstellen** | Initialisiert den Container, der Seiten und Grafiken hält. |
| **2️⃣ Leere Seite hinzufügen** | Sie benötigen ein `Page`‑Objekt, weil Formen an eine Seite, nicht direkt an das Dokument, angehängt werden. |
| **3️⃣ Rechteckgrenzen definieren** | Hier erfahren Sie **wie man Rechteck‑Abmessungen definiert**. Der `Rectangle`‑Konstruktor nimmt `x`, `y`, `width` und `height` in Punkten (1 pt = 1/72 in). |
| **4️⃣ Rechteckform erstellen** | `RectangleShape` ist die Aspose‑Klasse, die ein Rechteck rendert. Das Setzen von `StrokeColor` definiert die Kontur; Sie können auch `FillColor` für eine Füllung setzen. |
| **5️⃣ Seitenränder prüfen** | `CheckShapeBoundary` wirft eine Ausnahme, wenn das Rechteck die Seitengröße überschreitet, und verhindert fehlerhafte PDFs. |
| **6️⃣ Form zur Seite hinzufügen** | Die Form wird Teil des Inhaltsstroms der Seite. |
| **7️⃣ PDF speichern** | Persistiert das Dokument in einer Datei, die Sie mit jedem PDF‑Betrachter öffnen können. |

Das resultierende `RectangleDemo.pdf` enthält ein schwarzes Rechteck, das in der oberen linken Ecke der Seite positioniert ist und exakt 500 pt breit sowie 700 pt hoch ist.

![draw rectangle on pdf example](https://example.com/rectangle-demo.png "draw rectangle on pdf example")

*Bild‑Alt‑Text: draw rectangle on pdf example zeigt ein schwarzes Rechteck in der oberen linken Ecke einer PDF‑Seite.*

## Wie man Rechteck‑Abmessungen für verschiedene Seitengrößen definiert

Das obige Snippet verwendet feste Werte (`500 x 700`). In realen Anwendungen muss das Rechteck häufig an die Breite und Höhe der Seite angepasst werden.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Wichtige Punkte:**

* Verwenden Sie `page.PageInfo.Width` und `Height`, um die tatsächliche Seitengröße zu lesen.
* Durch Multiplikation mit einem Faktor (z. B. `0.8f`) können Sie Abmessungen als Prozentsatz der Seite ausdrücken.
* Das Zentrieren erfolgt, indem Sie die Rechteckgröße von der Seitengröße subtrahieren und den Rest halbieren.

## Häufige Stolperfallen und wie man sie vermeidet

| Stolperfalle | Warum sie auftritt | Lösung |
|---------|----------------|-----|
| Rechteck reicht über die Seite hinaus | Fest codierte Abmessungen, die größer sind als die Seitengröße. | Rufen Sie `page.CheckShapeBoundary` **vor** dem Hinzufügen der Form auf; passen Sie die Abmessungen an, wenn eine Ausnahme geworfen wird. |
| Kontur nicht sichtbar | `StrokeColor` bleibt beim Standard (`Color.Empty`). | Setzen Sie `StrokeColor` explizit (z. B. `Color.Black`). |
| Rechteck erscheint außerhalb des Bildschirms | Koordinaten beginnen im PDF‑Raum unten links; die Verwendung von Bildschirm‑Koordinaten (oben links) führt zu einer Umkehr. | Denken Sie daran, dass der Ursprung `(0,0)` die linke untere Ecke ist. Passen Sie `y` entsprechend an oder verwenden Sie `pageHeight - desiredY`. |
| Unerwartete Linienstärke | Die Standard‑Linienbreite kann für den Druck zu dünn sein. | Setzen Sie `rectangleShape.LineWidth = 2;`, um die Stärke zu erhöhen. |

## Erweiterung des Beispiels

Sobald Sie **ein Rechteck auf PDF** zeichnen können, lassen sich leicht weitere Formen hinzufügen:

* **EllipseShape** – für Kreise oder Ovale.
* **PolygonShape** – für benutzerdefinierte Polygone.
* **TextFragment** – um Ihre Rechtecke zu beschriften.

Alle Formen folgen demselben Ablauf: Grenzen definieren, Aussehen konfigurieren, Grenzen prüfen und dann zur Seite hinzufügen.

## Komplettes, ausführbares Programm

Unten finden Sie das vollständige Programm, das das einfache Rechteck‑Beispiel und das dynamische Größen‑Beispiel kombiniert. Kopieren Sie es in ein neues Konsolen‑Projekt, stellen Sie das `Aspose.PDF`‑NuGet‑Paket wieder her und führen Sie es aus.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Erwartete Ausgabe:**  
Öffnen Sie `CombinedRectangles.pdf`. Sie sehen ein schwarzes Rechteck, das an der unteren linken Ecke verankert ist, sowie ein zentriertes dunkelblaues Rechteck mit einer hellgelben Füllung. Beide Rechtecke respektieren die Seitenränder.

## Fazit

Sie wissen jetzt, wie man **ein Rechteck auf PDF** mit C# zeichnet und genau **wie man Rechteck‑Abmessungen** für feste und responsive Layouts definiert. Der Ansatz nutzt Aspose.PDFs `RectangleShape`, die Grenzprüfung und einfache Mathematik, um sich an jede Seitengröße anzupassen.

Als Nächstes könnten Sie folgendes erkunden:

* Hinzufügen von **Füllfarben** und **Linienstilen** (gestrichelt, gepunktet) – sekundäres Keyword: how to define rectangle dimensions with style.
* Kombinieren mehrerer Formen zu einer einzigen `Page`, um Diagramme oder Formulare zu erstellen.
* Exportieren des PDFs in einen Stream für Web‑APIs anstatt in eine Datei zu speichern.

Experimentieren Sie mit verschiedenen Größen, Farben und Positionen, um PDF‑Grafiken in Ihren .NET‑Anwendungen zu meistern. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu beherrschen und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}