---
category: general
date: 2026-09-18
description: Lernen Sie, ein leeres PDF‑Wörterbuch in C# mit Aspose.PDF zu erstellen.
  Diese Schritt‑für‑Schritt‑Anleitung behandelt ExtGState, den Grafikstatus und die
  Manipulation von CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: de
lastmod: 2026-09-18
og_description: Erstellen Sie ein leeres PDF‑Wörterbuch in C# mit Aspose.PDF. Folgen
  Sie diesem umfassenden Tutorial, um ExtGState‑ und Grafikzustandswörterbücher zu
  bearbeiten.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Leeres PDF‑Wörterbuch in C# erstellen – vollständige Aspose.PDF‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Wie man ein leeres PDF‑Wörterbuch mit Aspose.PDF in C# erstellt
url: /de/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein leeres PDF-Wörterbuch mit Aspose.PDF in C# erstellt

Wenn Sie ein **create empty PDF dictionary** beim Verarbeiten einer PDF-Datei benötigen, zeigt Ihnen dieser Leitfaden genau, wie Sie dies mit Aspose.PDF für .NET tun. Egal, ob Sie Transparenz, Mischmodi oder einen benutzerdefinierten Grafik‑Status anpassen, die nachstehenden Schritte ermöglichen Ihnen, das `ExtGState`‑Wörterbuch sicher und effizient zu bearbeiten.

In diesem Tutorial lernen Sie:

* Laden Sie ein PDF-Dokument mit Aspose.PDF.
* Greifen Sie auf die Ressourcen der ersten Seite und das vorhandene `ExtGState`‑Wörterbuch zu.
* Erstellen Sie ein neues leeres `CosPdfDictionary` und füllen Sie es mit Grafik‑Status‑Einträgen.
* Speichern Sie das modifizierte PDF, ohne den ursprünglichen Inhalt zu verlieren.

Die Lösung funktioniert mit jeder PDF, die mindestens eine Seite enthält, und erfordert nur die Aspose.PDF-Bibliothek (Version 23.10 oder neuer).

## Voraussetzungen

* .NET 6.0 oder höher (der Code läuft auch unter .NET Framework 4.8).
* Ein Verweis auf das **Aspose.PDF** NuGet-Paket.
* Eine Eingabe‑PDF‑Datei unter `YOUR_DIRECTORY/input.pdf`.
* Grundlegende Kenntnisse in C# und PDF-Konzepten wie Ressourcen und Grafikstatus.

> **Profi‑Tipp:** Beim Arbeiten mit großen PDFs sollten Sie das `Document`‑Objekt in einen `using`‑Block einbetten, um sicherzustellen, dass alle Dateihandles sofort freigegeben werden.

## Schritt 1: PDF-Dokument laden

Der erste Vorgang öffnet die Quelldatei. Aspose.PDF liest das gesamte Dokument in den Speicher, sodass Sie interne Objekte bearbeiten können.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Warum das wichtig ist*: Das Laden des Dokuments erstellt ein veränderbares Objektmodell. Ohne diesen Schritt können Sie nicht auf die Seitenressourcen zugreifen, die für die Wörterbuchmanipulation benötigt werden.

## Schritt 2: Ressourcen der ersten Seite abrufen

Jede Seite speichert ein `Resources`‑Wörterbuch, das Schriftarten, Bilder und Grafik‑Status enthält. Der Zugriff darauf liefert Ihnen einen `DictionaryEditor`, der Lese‑/Schreib‑Operationen vereinfacht.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Warum das wichtig ist*: Das `ExtGState`‑Wörterbuch befindet sich innerhalb der Seitenressourcen. Das Bearbeiten des falschen Wörterbuchs hätte keine Auswirkung auf das Rendering.

## Schritt 3: Vorhandenes ExtGState‑Wörterbuch finden

Der `ExtGState`‑Eintrag kann bereits Grafik‑Status‑Objekte enthalten. Wir holen ihn als `CosPdfDictionary`, damit wir neue Einträge hinzufügen können.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Falls der `ExtGState`‑Eintrag nicht existiert, erstellt Aspose.PDF automatisch ein leeres Wörterbuch, wenn Sie später ein neues zuweisen.

## Schritt 4: **Create empty PDF dictionary** für einen neuen Grafik‑Status

Hier erstellen wir ein brandneues `CosPdfDictionary` — den Kern der **create empty PDF dictionary**‑Operation. Anschließend füllen wir es mit Standard‑Grafik‑Status‑Schlüsseln:

* `CA` — Strich‑Deckkraft.
* `ca` — Füll‑Deckkraft.
* `BM` — Mischmodus.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Warum das wichtig ist*: Durch die explizite Definition jedes Eintrags steuern Sie, wie Objekte auf der Seite mischen und gerendert werden. Das Wörterbuch ist **leer**, bis Sie diese Schlüssel hinzufügen, was die Anforderung erfüllt, **create empty PDF dictionary** zu **erstellen**, bevor es befüllt wird.

## Schritt 5: Neuen Grafik‑Status zum ExtGState‑Wörterbuch hinzufügen

Jeder Grafik‑Status muss einen eindeutigen Namen besitzen (z. B. `GS0`). Wir fügen das frisch erstellte Wörterbuch unter diesem Namen ein.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Falls Sie mehrere Zustände benötigen, fügen Sie weitere Einträge wie `GS1`, `GS2` usw. hinzu und stellen Sie sicher, dass jeder Name innerhalb des `ExtGState`‑Wörterbuchs eindeutig ist.

## Schritt 6: Aktualisiertes PDF-Dokument speichern

Abschließend schreiben Sie die Änderungen zurück auf die Festplatte. Die Originaldatei bleibt unverändert, da wir in einen neuen Pfad speichern.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

Das resultierende `output.pdf` enthält nun einen zusätzlichen Grafik‑Status (`GS0`), den Sie aus jedem Seiten‑Content‑Stream mit dem Operator `/GS0` referenzieren können.

## Vollständiges funktionierendes Beispiel

Wenn Sie alle Schritte zusammenführen, erhalten Sie ein eigenständiges Programm, das Sie sofort ausführen können.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Erwartete Ausgabe**: Nach dem Ausführen des Programms enthält `output.pdf` denselben visuellen Inhalt wie `input.pdf`. Die Inspektion des PDFs mit einem Tool wie Adobe Acrobat oder PDF‑Tron zeigt einen neuen Eintrag `GS0` im `ExtGState`‑Wörterbuch der ersten Seite.

## Häufige Variationen und Sonderfälle

| Situation | Was anzupassen ist |
|-----------|--------------------|
| **No existing ExtGState entry** | Ersetzen Sie `resourcesEditor["ExtGState"]` durch `new CosPdfDictionary(pdfDocument)` und weisen Sie es wieder `firstPage.Resources["ExtGState"]` zu. |
| **Multiple pages need the same state** | Fügen Sie denselben `GS0`‑Eintrag zu jedem Seiten‑`ExtGState`‑Wörterbuch hinzu oder referenzieren Sie das Wörterbuch aus einem gemeinsam genutzten Ressourcen‑Objekt. |
| **Different blend mode** | Ändern Sie den `CosPdfName`‑Wert von `"Normal"` zu `"Multiply"`, `"Screen"` usw., je nach gewünschtem Effekt. |
| **Higher opacity values** | Verwenden Sie `new CosPdfNumber(0.8)` für `ca` oder `CA`, um die Füll‑ bzw. Strich‑Deckkraft zu erhöhen. |
| **Using a stream operator** | Schreiben Sie im Content‑Stream `"/GS0 gs"` vor den Zeichenoperationen, um den neuen Grafik‑Status anzuwenden. |

## Leistungsüberlegungen

* **Speichernutzung** – Das Laden einer sehr großen PDF verbraucht Speicher proportional zur Seitenzahl. Wenn Sie nur die erste Seite bearbeiten müssen, überlegen Sie, nach der Verarbeitung `pdfDocument.Pages.Delete(pageNumber)` zu verwenden, um Ressourcen freizugeben.
* **Thread‑Sicherheit** – Aspose.PDF‑Objekte sind nicht thread‑sicher. Führen Sie Wörterbuch‑Änderungen in einem einzelnen Thread aus oder erstellen Sie separate `Document`‑Instanzen pro Thread.

## Fazit

Sie wissen jetzt, wie Sie mit Aspose.PDF **create empty PDF dictionary**‑Objekte erstellen, sie mit Grafik‑Status‑Einträgen befüllen und an das `ExtGState`‑Wörterbuch einer Seite anhängen. Diese Technik ermöglicht eine feinkörnige Steuerung von Deckkraft, Mischmodus und anderen Rendering‑Parametern direkt aus C#.

Als Nächstes erkunden Sie verwandte Themen wie **PDF manipulation C#**, das Hinzufügen benutzerdefinierter **ExtGState dictionary**‑Einträge für erweiterte Transparenzeffekte oder die Verwendung von **CosPdfDictionary**, um andere Ressourcentypen wie Schriftarten oder XObjects zu ändern. Experimentieren Sie mit mehreren Grafik‑Status, um anspruchsvolle visuelle Effekte in Ihren PDFs zu erzeugen.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}