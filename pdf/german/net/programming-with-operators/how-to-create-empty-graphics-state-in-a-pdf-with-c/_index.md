---
category: general
date: 2026-08-17
description: Erstellen Sie einen leeren Grafikzustand in einem PDF mit C# und Aspose.Pdf.
  Befolgen Sie diese Schritt‑für‑Schritt‑Anleitung, um ExtGState‑Ressourcen sicher
  zu bearbeiten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: de
lastmod: 2026-08-17
og_description: Erstellen Sie einen leeren Grafikzustand in einem PDF mit C#. Dieses
  Tutorial zeigt, wie man ExtGState‑Ressourcen mit Aspose.Pdf bearbeitet, um zuverlässige
  PDF‑Modifikationen vorzunehmen.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Leeren Grafikzustand in PDF mit C# erstellen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Wie man einen leeren Grafikzustand in einem PDF mit C# erstellt
url: /de/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man einen leeren Grafikzustand in einem PDF mit C# erstellt

Wenn Sie einen **leeren Grafikzustand** in einem PDF **erstellen** müssen, zeigt Ihnen dieser Leitfaden genau, wie Sie dies mit C# und Aspose.Pdf tun. Sie sehen ein vollständiges, ausführbares Beispiel, das einen neuen Eintrag zum ExtGState‑Wörterbuch der Seite hinzufügt, ohne vorhandenen Inhalt zu beeinflussen.

Die Arbeit mit PDF‑Grafikzuständen ist eine häufige Anforderung, wenn Sie Transparenz, Mischmodi oder andere Render‑Parameter auf Objektbasis steuern möchten. Der untenstehende Code demonstriert den empfohlenen Ansatz, erklärt, warum jeder Schritt wichtig ist, und behandelt typische Variationen, denen Sie begegnen könnten.

## Voraussetzungen

* .NET 6.0 oder höher (das Beispiel lässt sich auch mit .NET Core kompilieren).
* Eine Aspose.Pdf for .NET Lizenz (oder ein temporärer Evaluierungsschlüssel).
* Ein Ordner, der eine `input.pdf`‑Datei enthält, die Sie ändern möchten.
* Grundlegende Kenntnisse der C#‑Syntax und von PDF‑Konzepten wie Ressourcen‑Wörterbüchern.

## Schritt 1: Projekt einrichten und Namespaces importieren

Erstellen Sie eine neue Konsolenanwendung oder integrieren Sie den Code in ein bestehendes Projekt. Fügen Sie das Aspose.Pdf‑NuGet‑Paket hinzu:

```bash
dotnet add package Aspose.Pdf
```

Anschließend importieren Sie die erforderlichen Namespaces:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Diese Importe geben Ihnen Zugriff auf die Klassen `Document`, `DictionaryEditor` und PDF‑Primitive, die zum **Erstellen leerer Grafikzustände** erforderlich sind.

## Schritt 2: Ordner festlegen, der die PDF‑Dateien enthält

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Ersetzen Sie den Pfad durch den Speicherort Ihrer eigenen PDF‑Dateien. Das Halten des Verzeichnisses in einer Variablen macht den Code wiederverwendbar und einfacher zu testen.

## Schritt 3: Quell‑PDF‑Dokument laden

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Das Öffnen des Dokuments innerhalb einer `using`‑Anweisung stellt sicher, dass der Dateihandle nach dem Speichern der Änderungen automatisch freigegeben wird.

## Schritt 4: Erste Seite und ihr Ressourcen‑Wörterbuch zugreifen

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` ruft die erste Seite ab (PDF‑Seitenzahlen beginnen bei 1).
* `DictionaryEditor` bietet eine bequeme Möglichkeit, PDF‑Wörterbücher zu lesen und zu ändern.
* Der Eintrag `ExtGState` enthält alle Grafik‑Zustandsobjekte für die Seite. Wenn der Schlüssel nicht existiert, erstellt Aspose.Pdf automatisch ein leeres Wörterbuch.

## Schritt 5: Neues leeres Grafik‑Zustands‑Wörterbuch erstellen

Der Grafikzustand, den Sie hinzufügen, kann leer sein oder bereits mit Parametern wie Opazität (`CA`, `ca`) oder Mischmodus (`BM`) vorbefüllt sein. In diesem Tutorial erstellen wir einen **leeren Grafikzustand** und setzen anschließend einige typische Werte, um zu zeigen, wie das Wörterbuch funktioniert.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` erstellt einen leeren Container, den Sie mit beliebigen Grafik‑Zustands‑Schlüsseln füllen können.
* Das Hinzufügen von `CA`, `ca` und `BM` ist optional; Sie können sie weglassen, wenn Sie wirklich einen leeren Zustand benötigen. Der Code zeigt, wie Einträge hinzugefügt werden, wenn Sie später das Rendering steuern möchten.

## Schritt 6: Neuen Grafikzustand in das ExtGState‑Wörterbuch einfügen

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Die Benennung des Eintrags `"GS0"` folgt der üblichen Konvention, Grafik‑Zustands‑Namen mit „GS“ zu prefixed. Sie können jeden gültigen PDF‑Namen wählen, der nicht mit bestehenden Schlüsseln kollidiert.

## Schritt 7: Modifiziertes PDF‑Dokument speichern

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

Der Aufruf `Save` schreibt die aktualisierte Datei nach `output.pdf`. Das Öffnen dieser Datei in einem PDF‑Betrachter bestätigt, dass der neue Grafikzustand existiert; Sie können später mit dem `gs`‑Operator in Inhaltsstreams darauf verweisen.

### Vollständige Quellcode‑Auflistung

Wenn das Programm ausgeführt wird, gibt es eine Bestätigungszeile aus und erzeugt `output.pdf` mit dem neu hinzugefügten Grafikzustand.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

## Warum dieser Ansatz am besten funktioniert

* **Direktes Wörterbuch‑Editing** – Die Verwendung von `DictionaryEditor` vermeidet das Parsen des gesamten Inhaltsstreams. Sie ändern nur die Ressourcen, die Sie interessieren.
* **Typisierte PDF‑Primitive** – `CosPdfNumber`, `CosPdfName` und `CosPdfDictionary` garantieren, dass das erzeugte PDF der PDF 1.7‑Spezifikation entspricht.
* **Sicherheit** – Der `using`‑Block gibt das `Document`‑Objekt frei und verhindert Dateisperren, die nachfolgende Builds beschädigen könnten.
* **Erweiterbarkeit** – Sobald der leere Grafikzustand existiert, können Sie ihn von jedem Inhaltsoperator (`gs`) aus referenzieren, um Opazität, Mischmodus oder andere Parameter für ausgewählte Zeichenbefehle zu ändern.

## Häufige Variationen und Sonderfälle

| Situation | Empfohlene Anpassung |
|-----------|----------------------|
| **Mehrere Seiten** | Durchlaufen Sie `pdfDocument.Pages` und wiederholen Sie das Einfügen des Wörterbuchs für jede Seite, die Sie ändern müssen. |
| **Kein vorhandener ExtGState‑Eintrag** | `resourcesEditor["ExtGState"]` erstellt automatisch ein leeres Wörterbuch, wenn es nicht existiert. Kein zusätzlicher Code ist erforderlich. |
| **Anderer Grafik‑Zustands‑Name** | Ersetzen Sie `"GS0"` durch einen Namen, der Ihrer Namenskonvention entspricht, z. B. `"MyTransparentState"`. |
| **Nur einen leeren Zustand hinzufügen** | Lassen Sie das `parameters`‑Array und die `foreach`‑Schleife weg; das Wörterbuch bleibt leer. |
| **Arbeiten mit verschlüsselten PDFs** | Geben Sie das Passwort beim Erzeugen von `new Document(path, password)` an, bevor Sie Ressourcen bearbeiten. |

## Ergebnis verifizieren

Sie können überprüfen, dass der Grafikzustand hinzugefügt wurde, indem Sie das PDF mit einem Low‑Level‑Viewer wie **PDF‑Tron** oder **iText Sharp** inspizieren. Suchen Sie nach einem Eintrag ähnlich wie:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Wenn der Eintrag erscheint, war die **Erstellung eines leeren Grafikzustands** erfolgreich.

## Fazit

Sie wissen jetzt, wie Sie mit C# und Aspose.Pdf einen **leeren Grafikzustand** in einem PDF **erstellen**. Das Tutorial behandelte jeden Schritt – vom Laden des Dokuments über das Bearbeiten des `ExtGState`‑Wörterbuchs bis zum Speichern des Ergebnisses – und erklärte die Begründung hinter jeder Aktion.

Ab hier können Sie:

* Den neuen Grafikzustand in Inhaltsstreams verwenden (`gs /GS0`).
* Mit zusätzlichen Schlüsseln wie `/SM` (Strichanpassung) oder `/OPM` (Überdruckmodus) experimentieren.
* Die gleiche Technik auf andere Ressourcentypen wie `/XObject` oder `/ColorSpace` anwenden.

Viel Spaß beim PDF‑Hacken und fühlen Sie sich frei, weitere **Aspose PDF Grafikzustands**‑Szenarien zu erkunden, wie dynamische Opazitätsänderungen oder benutzerdefinierte Mischmodi!

## Was sollten Sie als Nächstes lernen?

- [Wie man gestrichelte Linien in PDFs mit Aspose.PDF für .NET erstellt: Eine Schritt‑für‑Schritt‑Anleitung](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Wie man Grafiken aus PDFs mit Aspose.PDF .NET entfernt: Ein vollständiger Leitfaden](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Rechtecke in PDFs erstellen & füllen mit Aspose.PDF für .NET: Eine Schritt‑für‑Schritt‑Anleitung](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}