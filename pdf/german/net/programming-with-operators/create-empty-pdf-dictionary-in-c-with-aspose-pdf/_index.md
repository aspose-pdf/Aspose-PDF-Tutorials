---
category: general
date: 2026-08-14
description: Erstellen Sie ein leeres PDF-Wörterbuch in C# mit Aspose.Pdf – erfahren
  Sie, wie Sie einen Grafikzustand zur ExtGState‑Sammlung hinzufügen und PDFs programmgesteuert
  ändern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: de
lastmod: 2026-08-14
og_description: Erstellen Sie ein leeres PDF‑Wörterbuch in C# mit Aspose.Pdf. Folgen
  Sie dieser vollständigen Anleitung, um einen benutzerdefinierten Grafikzustand zur
  ExtGState‑Sammlung eines PDFs hinzuzufügen.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Leeres PDF‑Wörterbuch in C# erstellen – Aspose.Pdf Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Leeres PDF‑Wörterbuch in C# mit Aspose.Pdf erstellen
url: /de/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Leeres PDF‑Wörterbuch in C# mit Aspose.Pdf erstellen

Wenn Sie **leere PDF‑Wörterbuch**‑Objekte benötigen, während Sie mit PDF‑Dateien arbeiten, zeigt Ihnen diese Anleitung genau, wie Sie das in C# mit der Aspose.Pdf‑Bibliothek tun. Egal, ob Sie einen benutzerdefinierten Grafik‑Zustand erstellen, eine neue Ressource hinzufügen oder eine Vorlage für die spätere Verwendung vorbereiten – die nachfolgenden Schritte liefern eine vollständige, ausführbare Lösung.

Sie lernen, wie Sie ein PDF laden, das Ressourcen‑Wörterbuch der ersten Seite öffnen, ein brandneues `CosPdfDictionary` erstellen und es in die `ExtGState`‑Sammlung einfügen. Am Ende des Tutorials haben Sie ein funktionierendes `output.pdf`, das das neu erstellte Wörterbuch enthält.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+)
- Visual Studio 2022 oder eine andere C#‑IDE Ihrer Wahl
- Eine Aspose.Pdf‑für‑.NET‑Lizenz (oder einen temporären Evaluierungsschlüssel)
- Eine Beispiel‑PDF‑Datei namens **input.pdf**, die in einem von Ihnen kontrollierten Ordner liegt (der Ordnerpfad wird als `dataDir` verwendet)

Keine zusätzlichen NuGet‑Pakete sind über `Aspose.Pdf` hinaus erforderlich.

## Schritt 1: Projekt einrichten und Aspose.Pdf referenzieren

1. Erstellen Sie ein neues **Console App**‑Projekt in Visual Studio.  
2. Öffnen Sie den **NuGet Package Manager** und installieren Sie `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Fügen Sie die folgenden `using`‑Direktiven am Anfang von `Program.cs` hinzu:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Warum diese Namespaces?* `Aspose.Pdf` enthält die Kernklasse `Document`, während `Aspose.Pdf.Operators.Gfx` `CosPdfDictionary`, `CosPdfNumber` und verwandte Low‑Level‑PDF‑Objekte bereitstellt, die zum **Erstellen leerer PDF‑Wörterbuch**‑Strukturen nötig sind.

## Schritt 2: Quell‑PDF laden

Der erste Vorgang besteht darin, die vorhandene PDF‑Datei in eine `Document`‑Instanz zu laden. Dadurch erhalten Sie Zugriff auf alle Seiten, Ressourcen und Low‑Level‑Wörterbücher.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Erklärung*: `Document` liest die Datei in den Speicher und bereitet interne Strukturen vor. Die `using`‑Anweisung sorgt dafür, dass das Dateihandle nach Abschluss der Verarbeitung freigegeben wird.

## Schritt 3: Ressourcen‑Wörterbuch der ersten Seite öffnen

Jede PDF‑Seite besitzt ein **Resources**‑Wörterbuch, das Schriften, Bilder, ExtGState‑Objekte und andere gemeinsam genutzte Ressourcen gruppiert. Um einen neuen Grafik‑Zustand einzufügen, müssen wir dieses Wörterbuch bearbeiten.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` ist eine Hilfsklasse, die es Ihnen ermöglicht, ein PDF‑Wörterbuch wie ein C#‑`Dictionary<string, object>` zu behandeln.

## Schritt 4: ExtGState‑Sammlung abrufen (oder erstellen)

`ExtGState` enthält Grafik‑Zustandsobjekte wie Opazität, Mischmodus und Linienstärke. Wenn das Quell‑PDF bereits einen `ExtGState`‑Eintrag enthält, verwenden wir ihn; andernfalls erstellen wir ein neues leeres Wörterbuch.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Warum diese Prüfung?* Einige PDFs lassen den `ExtGState`‑Eintrag komplett weg. Durch die Behandlung beider Fälle bleibt das Tutorial für jede Eingabedatei robust.

## Schritt 5: **Leeres PDF‑Wörterbuch** für einen neuen Grafik‑Zustand erstellen

Jetzt erstellen wir tatsächlich **leere PDF‑Wörterbuch**‑Objekte, die die Grafik‑Zustandsparameter definieren. Das Wörterbuch startet leer, und wir fügen die erforderlichen Schlüssel hinzu:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Was jeder Eintrag bewirkt

| Schlüssel | Typ | Bedeutung |
|-----------|-----|------------|
| **CA** | `CosPdfNumber` | Strich‑Opazität (Wertbereich 0‑1). |
| **ca** | `CosPdfNumber` | Füll‑Opazität (Wertbereich 0‑1). |
| **BM** | `CosPdfName`   | Mischmodus; `"Normal"` ist am gebräuchlichsten. |

Da wir mit einem **leeren PDF‑Wörterbuch** begonnen haben, haben wir die volle Kontrolle darüber, welche Einträge hinzugefügt werden. Sie können dieses Wörterbuch jederzeit um weitere Grafik‑Zustandsparameter wie `LW` (Linienstärke) oder `LC` (Linien‑Ende) erweitern.

## Schritt 6: Neuen Grafik‑Zustand in ExtGState einfügen

Das `ExtGState`‑Wörterbuch funktioniert wie eine Map, bei der jeder Eintrag durch einen Namen (z. B. `GS0`, `GS1`) identifiziert wird. Wir fügen unser frisch gebautes Wörterbuch unter einem eindeutigen Schlüssel hinzu.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Wenn Sie mehrere Zustände hinzufügen möchten, erhöhen Sie das Suffix (`GS1`, `GS2`, …), um Namenskollisionen zu vermeiden.

## Schritt 7: Modifiziertes PDF speichern

Abschließend schreiben wir die Änderungen zurück auf die Festplatte. Die `Save`‑Methode serialisiert die aktualisierten Wörterbücher automatisch.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Öffnen Sie `output.pdf` in einem beliebigen PDF‑Betrachter und prüfen Sie den Eintrag **Resources → ExtGState** (die meisten Betrachter verbergen diesen, aber Werkzeuge wie Adobe Acrobat Preflight oder PDF‑Tron können ihn anzeigen). Sie sollten einen `GS0`‑Eintrag sehen, der die von Ihnen definierten Opazitäts‑ und Mischmodus‑Werte enthält.

## Vollständiges funktionierendes Beispiel

Alle Teile zusammengefügt, hier das komplette Programm, das Sie in `Program.cs` einfügen und ausführen können:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Erwartete Ausgabe** – Die Konsole gibt eine Bestätigungszeile aus, und `output.pdf` enthält den neuen `GS0`‑Eintrag unter `ExtGState`. Wenn Sie eine Seite rendern, die `GS0` (z. B. über den Inhalts‑Stream‑Operator `gs`) referenziert, sind Striche vollständig undurchsichtig, während Füllungen zu 50 % transparent sind.

## Häufige Fragen und Sonderfall‑Behandlung

| Frage | Antwort |
|-------|----------|
| *Was, wenn das PDF mehrere Seiten hat?* | Das Beispiel richtet sich an die erste Seite (`Pages[1]`). Um alle Seiten zu beeinflussen, iterieren Sie über `pdfDocument.Pages` und wiederholen die Schritte 3‑5 für jede Seiten‑Ressource. |
| *Kann ich das Wörterbuch zu einer Seite hinzufügen, die bereits einen ExtGState‑Eintrag namens „GS0“ hat?* | Ja, Sie müssen jedoch einen anderen Schlüssel (`GS1`, `GS2`, …) verwenden, um das bestehende Element nicht zu überschreiben. |
| *Ist es sicher, das Wörterbuch nach dem Speichern weiter zu ändern?* | Sobald Sie `Save` aufrufen, ist die In‑Memory‑Repräsentation von der Datei getrennt. Sie können das `Document`‑Objekt weiter bearbeiten und bei Bedarf erneut `Save` aufrufen. |
| *Benötige ich eine Lizenz für Aspose.Pdf, um ` |  |

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [How to Create Multi-Layer PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}