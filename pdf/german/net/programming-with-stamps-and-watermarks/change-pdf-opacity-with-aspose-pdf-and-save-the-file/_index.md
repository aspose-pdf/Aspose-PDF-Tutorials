---
category: general
date: 2026-11-12
description: Erfahren Sie, wie Sie die PDF‑Opazität mit Aspose.Pdf ändern, Transparenz
  hinzufügen, den Mischmodus festlegen und das modifizierte PDF in C# speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: de
lastmod: 2026-11-12
og_description: PDF-Deckkraft mit Aspose.Pdf ändern, erfahren Sie, wie Sie Transparenz
  hinzufügen, den Mischmodus festlegen und modifizierte PDF-Dateien in C# speichern.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: PDF-Transparenz mit Aspose.Pdf ändern – Transparenz hinzufügen und speichern
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: PDF-Opazität mit Aspose.Pdf ändern und die Datei speichern
url: /de/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-Transparenz mit Aspose.Pdf ändern und Datei speichern

Wenn Sie die **PDF-Transparenz** in einem Dokument **ändern** müssen, bietet Aspose.Pdf eine unkomplizierte API, um sowohl die Strich‑ als auch die Füll‑Transparenz anzupassen. Dieses Tutorial zeigt genau **wie man Transparenz hinzufügt**, **wie man den Mischmodus festlegt** und **modifizierte PDF**‑Dateien mit nur wenigen Zeilen C#‑Code speichert.

Sie gehen jeden Schritt durch – vom Laden einer bestehenden PDF über das Definieren eines neuen Grafik‑Zustands bis hin zum Persistieren der Änderungen. Am Ende dieser Anleitung können Sie:

* Die Sichtbarkeit von Vektorgrafiken oder Bildern reduzieren.
* Einen benutzerdefinierten Mischmodus wie *Normal* oder *Multiply* anwenden.
* Die aktualisierte Datei exportieren, ohne anderen Inhalt zu verlieren.

Die einzige Voraussetzung ist eine funktionierende .NET‑Entwicklungsumgebung und ein Verweis auf die Aspose.Pdf‑Bibliothek (Version 23.9 oder höher). Es werden keine externen Werkzeuge benötigt.

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| .NET 6.0 SDK or later | Garantiert die Kompatibilität mit den neuesten Aspose.Pdf‑APIs. |
| Aspose.Pdf for .NET NuGet package | Stellt die Klassen `Document`, `CosPdfDictionary` und weitere, die im Code verwendet werden, bereit. |
| A PDF file to edit (e.g., `input.pdf`) | Dient als Quelle für die Transparenz‑Änderungen. |

Install the NuGet package with:

```bash
dotnet add package Aspose.Pdf
```

## PDF-Transparenz mit Aspose.Pdf ändern

### Schritt 1: PDF‑Dokument laden

Beginnen Sie damit, eine `Document`‑Instanz zu erstellen, die auf Ihre Quelldatei verweist. Der Konstruktor liest die gesamte PDF in den Speicher, sodass Sie deren interne Objekte manipulieren können.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Warum dieser Schritt?** Das Laden der Datei erzeugt ein manipulierbares Objektmodell. Alle nachfolgenden Änderungen wirken auf diese In‑Memory‑Repräsentation, wodurch die Originaldatei unverändert bleibt, bis Sie explizit speichern.

### Schritt 2: Auf die Ressourcen der ersten Seite zugreifen

Jede PDF‑Seite speichert ein *Ressourcen‑Dictionary*, das Objekte wie Schriften, Bilder und Grafik‑Zustände enthält. Sie müssen dieses Dictionary bearbeiten, um einen neuen `ExtGState`‑Eintrag einzufügen.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Tipp:** Wenn Ihre PDF mehrere Seiten enthält, die dieselbe Transparenz benötigen, wiederholen Sie diesen Schritt für jede Seite oder teilen Sie ein einzelnes `ExtGState` über mehrere Seiten hinweg.

### Schritt 3: Sicherstellen, dass ein ExtGState‑Dictionary existiert

Das `ExtGState`‑Dictionary enthält benutzerdefinierte Grafik‑Zustände. Falls es nicht existiert, erzeugt der Code automatisch eines.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Warum dieser Schritt?** Ohne einen `ExtGState`‑Container würde jeder Versuch, einen neuen Grafik‑Zustand zu referenzieren, fehlschlagen, was zu einer PDF führt, die Ihre Transparenz‑Einstellungen ignoriert.

### Schritt 4: Einen neuen Grafik‑Zustand definieren (ExtGState)

Ein Grafik‑Zustand definiert, wie Zeichenoperationen sich verhalten. Das folgende Dictionary legt die Strich‑Transparenz (`CA`), die Füll‑Transparenz (`ca`) und den Mischmodus (`BM`) fest.

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Wie man die Füll‑Transparenz einstellt:** Der `ca`‑Eintrag steuert die Transparenz gefüllter Formen (Text, Pfade). Passen Sie den numerischen Wert zwischen `0` (vollständig transparent) und `1` (vollständig undurchsichtig) an Ihre Design‑Anforderungen an.

> **Wie man den Mischmodus einstellt:** Der `BM`‑Eintrag wählt den Kompositions‑Algorithmus. Gängige Werte sind `Normal`, `Multiply`, `Screen` und `Overlay`. Wählen Sie denjenigen, der Ihrer visuellen Absicht entspricht.

### Schritt 5: Den Grafik‑Zustand im Ressourcen‑Dictionary registrieren

Geben Sie dem neuen Zustand einen Namen (z. B. `GS0`) und fügen Sie ihn dem `ExtGState`‑Dictionary hinzu. Dieser Name wird später im Inhalts‑Stream der Seite referenziert.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Pro‑Tipp:** Verwenden Sie eine Namenskonvention wie `GS0`, `GS1`, … wenn Sie mehrere Zustände erstellen. Das verhindert Namenskollisionen und erleichtert das Debugging.

### Schritt 6: Den Grafik‑Zustand auf den Seiteninhalt anwenden

Um den Transparenzeffekt tatsächlich zu sehen, fügen Sie den Operator `/GS0 gs` vor den Zeichenbefehlen ein, die Sie beeinflussen möchten. Das untenstehende Beispiel zeichnet ein halbtransparentes Rechteck.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Warum die Operatoren `q` und `Q`?** Sie schieben den Grafik‑Zustands‑Stack und holen ihn wieder ab, wodurch die Transparenz‑Änderung nur das Rechteck und nicht den Rest der Seite beeinflusst.

### Schritt 7: Das modifizierte PDF speichern

Schließlich schreiben Sie das aktualisierte Dokument auf die Festplatte. Die `Save`‑Methode überschreibt die Zieldatei oder erstellt eine neue, falls sie nicht existiert.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Wie man das modifizierte PDF speichert:** Der Aufruf von `Save` schreibt alle In‑Memory‑Modifikationen, einschließlich des neuen `ExtGState`, in den angegebenen Pfad. Sie können das Ergebnis auch in einen `MemoryStream` für Web‑Antworten streamen.

## Vollständiges funktionierendes Beispiel

Unten finden Sie ein einzelnes, eigenständiges Programm, das jeden oben beschriebenen Schritt integriert. Kopieren Sie es in eine Konsolenanwendung und führen Sie es aus, um die Transparenz‑Änderung zu überprüfen.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man ein modifiziertes PDF mit Aspose.Pdf speichert und Transparenz hinzufügt](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Wie man Transparenz zu PDF mit Aspose.PDF in C# hinzufügt](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Wie man einen Grafik‑Zustand zu PDF hinzufügt und Transparenz mit Aspose.PDF steuert](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}