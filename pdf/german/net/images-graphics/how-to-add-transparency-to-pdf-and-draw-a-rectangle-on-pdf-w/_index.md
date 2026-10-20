---
category: general
date: 2026-09-12
description: Erfahren Sie, wie Sie Transparenz zu PDF hinzufügen, ein Rechteck auf
  PDF zeichnen und PDF mit Transparenz mithilfe von Aspose.PDF in C# speichern – Schritt‑für‑Schritt‑Anleitung.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: de
lastmod: 2026-09-12
og_description: Fügen Sie einem PDF Transparenz hinzu, zeichnen Sie ein Rechteck auf
  das PDF und speichern Sie das PDF mit Transparenz mithilfe von Aspose.PDF in C#.
  Folgen Sie diesem vollständigen Tutorial.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Transparenz zu PDF hinzufügen und ein Rechteck im PDF zeichnen – vollständige
  C#‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Wie man Transparenz zu PDF hinzufügt und ein Rechteck auf PDF mit Aspose.PDF
  zeichnet
url: /de/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Transparenz zu PDF hinzufügt und ein Rechteck in PDF mit Aspose.PDF zeichnet

Wenn Sie **Transparenz zu PDF** hinzufügen müssen, zeigt Ihnen dieser Leitfaden genau, wie Sie dies in C# tun. Sie lernen außerdem, wie Sie **ein Rechteck in PDF zeichnen** und schließlich **PDF mit Transparenz speichern**, sodass das Ergebnis in Berichten, Rechnungen oder jedem Dokument‑Automatisierungs‑Workflow wiederverwendet werden kann.

In diesem Tutorial werden Sie:

* Ein vorhandenes PDF-Dokument laden.
* Einen benutzerdefinierten Grafikzustand erstellen, der Strich‑ und Füll‑Opazität definiert.
* Diesen Grafikzustand auf die Zeichenfläche anwenden und ein Rechteck zeichnen.
* Die modifizierte Datei speichern und dabei die Transparenzeinstellungen beibehalten.

Keine externen Werkzeuge sind über die Aspose.PDF für .NET-Bibliothek hinaus erforderlich, und jede Codezeile wird erklärt, damit Sie verstehen, *warum* jeder Schritt wichtig ist.

## Voraussetzungen

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+).
* Eine lizenzierte oder Evaluierungskopie von **Aspose.PDF for .NET**. Installieren Sie sie über NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Eine Eingabe‑PDF (`input.pdf`), die in einem Ordner liegt, den Sie aus Ihrem Projekt referenzieren können.

## Schritt 1: PDF-Dokument laden

Der erste Vorgang besteht darin, die Quelldatei zu öffnen. Die Verwendung der `using`‑Anweisung stellt sicher, dass das Dokument ordnungsgemäß freigegeben wird, was später beim Speichern Datei‑Locking‑Probleme verhindert.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Warum das wichtig ist*: Das Laden des Dokuments gibt Ihnen Zugriff auf die Seitensammlung, Ressourcendictionaries und Canvas‑Objekte, die zum Zeichnen benötigt werden.

## Schritt 2: Auf das Ressourcen‑Dictionary der ersten Seite zugreifen

Jede PDF‑Seite besitzt ein **Ressourcen‑Dictionary**, das Objekte wie Schriften, Bilder und Grafikzustände speichert. Um eine neue Transparenzeinstellung einzuführen, müssen wir den `ExtGState`‑Eintrag bearbeiten.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Warum das wichtig ist*: Der `DictionaryEditor` ermöglicht es uns, Low‑Level‑PDF‑Objekte zu lesen und zu ändern, ohne die Dokumentenstruktur zu beschädigen.

## Schritt 3: Einen benutzerdefinierten Grafikzustand mit Transparenzwerten erstellen

Ein Grafikzustand (`ExtGState`) steuert, wie Zeichenoperationen gerendert werden. Wir definieren zwei Opazitäts‑Parameter:

* **CA** – Strich‑Opazität (die Kontur von Formen).
* **ca** – Füll‑Opazität (das Innere von Formen).

Wir setzen außerdem den Mischmodus (`BM`) auf „Normal“, was die gebräuchlichste Komposit‑Operation ist.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Warum das wichtig ist*: Durch das Hinzufügen von `GS0` zum `ExtGState`‑Dictionary erstellen wir eine wiederverwendbare Referenz, die das Canvas vor dem Zeichnen aktivieren kann. Die Füll‑Opazität von `0.5` macht das Rechteck halbtransparent und erreicht das Ziel **Transparenz zu PDF hinzufügen**.

## Schritt 4: Grafikzustand anwenden und ein Rechteck zeichnen

Jetzt weisen wir das Canvas der Seite an, den gerade erstellten Grafikzustand zu verwenden, und zeichnen anschließend ein Rechteck. Die Koordinaten folgen dem PDF‑Koordinatensystem (Ursprung in der linken unteren Ecke).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Warum das wichtig ist*: `SetGraphicsState("GS0")` schaltet den Zeichenkontext zu den zuvor definierten Transparenzeinstellungen um. Die Methode `Rectangle` definiert die Form, und `Stroke` rendert die Kontur mit der angegebenen Opazität. Wenn Sie auch ein gefülltes Rechteck möchten, ersetzen Sie `Stroke()` durch `FillAndStroke()`.

## Schritt 5: Modifiziertes PDF speichern und Transparenz beibehalten

Abschließend schreiben wir das Dokument zurück auf die Festplatte. Die Ausgabedatei enthält den neuen Grafikzustand, das gezeichnete Rechteck und die Transparenzinformationen.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Warum das wichtig ist*: Das Speichern des Dokuments finalisiert alle Änderungen. Die resultierende Datei kann in jedem PDF‑Betrachter geöffnet werden, und das Rechteck wird mit 50 % Füll‑Opazität angezeigt.

### Erwartetes Ergebnis

Wenn Sie `output_with_extgstate.pdf` öffnen, sollten Sie ein Rechteck sehen, dessen Rand vollständig undurchsichtig ist und dessen Innenbereich halbtransparent, sodass darunterliegende Seiteninhalte durchscheinen.

## Sonderfälle und praktische Tipps

| Situation | Empfohlene Anpassung |
|-----------|------------------------|
| **Mehrere Seiten** | Durchlaufen Sie `pdfDocument.Pages` und wiederholen Sie die Schritte 2‑4 für jede Zielseite. |
| **Unterschiedliche Opazitätswerte** | Ändern Sie die `CosPdfNumber`‑Werte für `CA` (Strich) und `ca` (Füllung) zu einer beliebigen Zahl zwischen `0` (vollständig transparent) und `1` (vollständig undurchsichtig). |
| **Benutzerdefinierte Mischmodi** | Ersetzen Sie `"Normal"` durch `"Multiply"`, `"Screen"` oder einen anderen PDF‑Standard‑Mischmodus, der von Ihrem Betrachter unterstützt wird. |
| **Gefülltes Rechteck** | Rufen Sie `canvas.FillAndStroke()` anstelle von `canvas.Stroke()` auf, um sowohl Füllung als auch Kontur anzuwenden. |
| **Wiederverwenden desselben Grafikzustands** | Sie können `canvas.SetGraphicsState("GS0")` aufrufen, bevor Sie beliebig viele Formen auf derselben Seite zeichnen. |

**Profi‑Tipp:** Überprüfen Sie immer das Ressourcen‑Dictionary, nachdem Sie ein neues `ExtGState` hinzugefügt haben. Wenn das Dictionary nicht existiert, erstellen Sie es zuerst:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Vollständiges, ausführbares Beispiel

Unten finden Sie ein eigenständiges Programm, das Sie in eine Konsolenanwendung kopieren und sofort ausführen können (ersetzen Sie `YOUR_DIRECTORY` durch einen tatsächlichen Pfad).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Das Ausführen des Programms erzeugt `output_with_extgstate.pdf`, das **Transparenz zu PDF hinzufügen**, **Rechteck in PDF zeichnen** und **PDF mit Transparenz speichern** in einem einzigen Ablauf demonstriert.

## Fazit

Sie wissen jetzt, wie Sie mit Aspose.PDF für .NET **Transparenz zu PDF**‑Dateien **hinzufügen**, **ein Rechteck in PDF zeichnen** und **PDF mit Transparenz speichern**. Der Prozess dreht sich um das Erstellen eines benutzerdefinierten `ExtGState`, das Anwenden auf das Canvas und das Persistieren der Änderungen. Mit diesen Bausteinen können Sie die Technik auf andere Formen, mehrere Seiten oder dynamische Opazitätswerte ausweiten.

**Nächste Schritte**

* Erkunden Sie weitere Zeichenprimitive wie `canvas.Ellipse`, `canvas.Path` oder `canvas.TextFragment`, während Sie denselben Grafikzustand wiederverwenden.
* Kombinieren Sie Transparenz mit Bildüberlagerungen, um Wasserzeichen zu erstellen (`canvas.Image` + benutzerdefiniertes `ExtGState`).
* Lesen Sie die Aspose.PDF‑Dokumentation zu **Grafikzustands‑Parametern** für erweiterte Komposit‑Effekte.

Viel Spaß beim Programmieren und genießen Sie die visuelle Flexibilität, die Transparenz Ihren PDF‑Workflows verleiht!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man PDF in C# erstellt – Seite hinzufügen, Rechteck zeichnen & speichern](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Wie man ein Linienobjekt in PDF mit Aspose.PDF für .NET hinzufügt: Eine Schritt‑für‑Schritt‑Anleitung](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Wie man Bildstempel zu PDFs mit Aspose.PDF für .NET hinzufügt: Eine Schritt‑für‑Schritt‑Anleitung](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}