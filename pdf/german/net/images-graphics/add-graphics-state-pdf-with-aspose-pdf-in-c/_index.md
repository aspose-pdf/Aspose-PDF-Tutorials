---
category: general
date: 2026-10-07
description: Grafikzustand PDF mit Aspose.Pdf in C# hinzufügen, um die PDF‑Transparenz
  zu ändern. Folgen Sie dieser Schritt‑für‑Schritt‑Anleitung, um benutzerdefinierte
  Grafikzustände einzubetten und die Opazität zu steuern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: de
lastmod: 2026-10-07
og_description: Grafikzustand PDF mit Aspose.Pdf in C# hinzufügen. Erfahren Sie, wie
  Sie die PDF‑Transparenz ändern, indem Sie ein benutzerdefiniertes Grafikzustands‑Wörterbuch
  erstellen.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Grafikzustand zum PDF hinzufügen mit Aspose.Pdf – PDF‑Transparenz steuern
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Grafikzustand zu PDF mit Aspose.Pdf in C# hinzufügen
url: /de/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafiks‑Zustand‑PDF mit Aspose.Pdf in C# hinzufügen

Wenn Sie einem Dokument **Grafiks‑Zustand‑PDF** hinzufügen müssen, zeigt Ihnen dieses Tutorial genau, wie Sie das mit Aspose.Pdf für .NET erledigen. Am Ende der Anleitung wissen Sie außerdem, wie Sie **PDF‑Transparenz ändern** können, sodass Sie benutzerdefinierte Opazitätswerte für jede Zeichenoperation festlegen können.

Die Arbeit mit PDF‑Grafikzuständen ermöglicht Ihnen die Steuerung von Parametern wie Linienbreite, Mischmodus und – am wichtigsten für diesen Artikel – der Transparenz von Inhalten. Die nachfolgenden Schritte sind für Entwickler geschrieben, die mit C# vertraut sind und eine sofort einsatzbereite Lösung ohne langes Durchforsten der offiziellen SDK‑Dokumentation suchen.

## Was Sie lernen werden

* Wie Sie ein neues Grafikzustands‑Dictionary erstellen und es mit den Einträgen `CA`, `ca` und `BM` füllen.  
* Wie Sie dieses Dictionary in die `ExtGState`‑Ressource der Seite einfügen, sodass das PDF es erkennt.  
* Wie die Werte `ca` (Strich) und `CA` (Füllung) **PDF‑Transparenz ändern** für nachfolgende Zeichenbefehle beeinflussen.  
* Häufige Stolperfallen wie Namenskollisionen und Versionskompatibilität sowie Profi‑Tipps zum späteren Erweitern des Grafikzustands.

**Voraussetzungen**

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+).  
* Eine gültige Aspose.Pdf‑für‑.NET‑Lizenz (die kostenlose Evaluierung reicht für Tests).  
* Visual Studio 2022 oder eine beliebige C#‑IDE Ihrer Wahl.  

---

## Schritt 1: Aspose.Pdf für .NET installieren

Fügen Sie das NuGet‑Paket zu Ihrem Projekt hinzu:

```bash
dotnet add package Aspose.Pdf
```

Das Paket enthält den Namespace `Aspose.Pdf`, der die Klassen `Document`, `DictionaryEditor` und `CosPdfDictionary` bereitstellt, die später verwendet werden.

> **Pro‑Tipp:** Wenn Sie viele PDFs stapelweise verarbeiten wollen, aktivieren Sie die **License** frühzeitig in `Program.cs`, um das Evaluierungs‑Wasserzeichen zu vermeiden.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Schritt 2: Eingabe‑ und Ausgabepfade definieren

Sie müssen das SDK auf ein vorhandenes PDF (`input.pdf`) zeigen und angeben, wo die modifizierte Datei gespeichert werden soll (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Warum das wichtig ist:** Durch die Verwendung absoluter Pfade wird verhindert, dass das SDK im falschen Arbeitsverzeichnis nach der Datei sucht – ein häufiger Grund für `FileNotFoundException`.

## Schritt 3: PDF öffnen und Ressourcen der ersten Seite finden

Das `ExtGState`‑Dictionary befindet sich im Ressourcen‑Dictionary jeder Seite. Wir bearbeiten aus Gründen der Einfachheit die erste Seite, aber das gleiche Vorgehen funktioniert für jede Seiten‑Index‑Nummer.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Randfall:** Wenn die Seite keinen `ExtGState`‑Eintrag besitzt, müssen Sie ihn erstellen:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Schritt 4: Neues Grafikzustands‑Dictionary erstellen

Ein Grafikzustand ist eine Sammlung von Schlüssel‑/Wert‑Paaren, die beschreiben, wie Zeichenoperationen sich verhalten. Für Transparenz benötigen wir drei Schlüssel:

| Schlüssel | Bedeutung | Typischer Wert |
|-----------|-----------|----------------|
| `CA`      | Füll‑Opazität (0 = transparent, 1 = undurchsichtig) | `1` (vollständig undurchsichtig) |
| `ca`      | Strich‑Opazität (gleiche Skala) | `0.5` (50 % transparent) |
| `BM`      | Mischmodus (z. B. `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Warum diese Werte?**  
`ca = 0.5` lässt jede gestrichelte Pfad‑Zeichnung (Linien, Rahmen) mit 50 % Opazität erscheinen, während `CA = 1` gefüllte Formen vollständig undurchsichtig lässt. Passen Sie beide Zahlen an, um den gewünschten **PDF‑Transparenz‑Effekt** zu erzielen.

## Schritt 5: Grafikzustand in das ExtGState‑Dictionary einfügen

Sie müssen dem neuen Zustand einen eindeutigen Namen geben (z. B. `GS0`). Existiert der Name bereits, überschreibt Aspose.Pdf den vorhandenen Eintrag, was andere Inhalte, die darauf angewiesen sind, beschädigen könnte.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Jetzt kennen die Ressourcen der Seite `GS0`. Um ihn tatsächlich zu verwenden, würden Sie den Grafikzustand in einem Inhaltsstrom über den Operator `gs` referenzieren (z. B. `GS0 gs`). Aspose.Pdf ermöglicht das Einfügen roher PDF‑Operatoren, falls Sie eigene Formen zeichnen müssen.

## Schritt 6: Modifiziertes PDF speichern

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

Das resultierende `output.pdf` enthält denselben visuellen Inhalt wie das Original, aber alle nachfolgenden Zeichenbefehle, die `GS0` auswählen, respektieren die von Ihnen definierten Transparenzeinstellungen.

### Erwartetes Ergebnis

Öffnen Sie `output.pdf` in Adobe Acrobat oder einem beliebigen PDF‑Betrachter. Wenn Sie eine neue gestrichelte Linie mit dem Grafikzustand `GS0` hinzufügen (z. B. über `pdfDocument.Pages[1].Contents.Add(...)`), erscheint die Linie halbtransparent, während Füllungen undurchsichtig bleiben. Das zeigt, dass Sie erfolgreich **Grafiks‑Zustand‑PDF** hinzugefügt und **PDF‑Transparenz geändert** haben.

---

## Vollständiges ausführbares Beispiel

Unten finden Sie das komplette Programm, das Sie in eine Konsolenanwendung kopieren‑und‑einfügen können. Es beinhaltet das Laden der Lizenz, Fehlerbehandlung und Kommentare, die jeden nicht‑offensichtlichen Schritt erklären.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## Was Sie als Nächstes lernen sollten


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Transparenz zu PDF mit Aspose PDF in C# hinzufügen – Schritt‑für‑Schritt‑Anleitung](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Transparenz zu PDF mit Aspose hinzufügen – Vollständige C#‑Anleitung](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Wie man einen Bildstempel zu einem PDF mit Aspose.PDF für .NET hinzufügt: Ein umfassender Leitfaden](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}