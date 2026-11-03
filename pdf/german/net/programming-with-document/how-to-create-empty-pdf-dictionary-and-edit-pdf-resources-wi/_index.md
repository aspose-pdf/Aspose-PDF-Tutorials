---
category: general
date: 2026-10-26
description: Erfahren Sie, wie Sie ein leeres PDF‑Verzeichnis erstellen und PDF‑Ressourcen
  mit Aspose.PDF für C# bearbeiten. Schritt‑für‑Schritt‑Anleitung mit vollständigem
  Codebeispiel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: de
lastmod: 2026-10-26
og_description: Erstellen Sie ein leeres PDF‑Wörterbuch und bearbeiten Sie PDF‑Ressourcen
  mit Aspose.PDF für C#. Folgen Sie diesem vollständigen Tutorial, um Grafikzustände
  in PDFs zu ändern.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Leeres PDF-Wörterbuch erstellen & PDF-Ressourcen in C# bearbeiten – Aspose.PDF‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Wie man ein leeres PDF‑Wörterbuch erstellt und PDF‑Ressourcen mit Aspose.PDF
  in C# bearbeitet
url: /de/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein leeres PDF‑Wörterbuch erstellt und PDF‑Ressourcen mit Aspose.PDF in C# bearbeitet

Wenn Sie **create empty PDF dictionary** und dann **edit PDF resources** in einer C#‑Anwendung benötigen, zeigt Ihnen dieser Leitfaden die genauen Schritte. Sie sehen ein vollständiges, ausführbares Beispiel, das einen benutzerdefinierten graphics state zur ersten Seite einer bestehenden PDF hinzufügt.

Die Arbeit mit Low‑Level‑PDF‑Objekten kann einschüchternd wirken, aber Aspose.PDF bietet eine klare API für die Manipulation von Wörterbüchern. Am Ende dieses Tutorials verstehen Sie, warum jede Operation wichtig ist und wie Sie den Code für andere Ressourcentypen anpassen können.

## Voraussetzungen

* .NET 6.0 (oder höher) installiert.
* Eine lizenzierte Kopie von **Aspose.PDF for .NET** – die kostenlose Testversion funktioniert zum Testen.
* Eine IDE wie Visual Studio 2022.
* Eine PDF‑Datei mit dem Namen `input.pdf`, die in einem Ordner liegt, den Sie im Code referenzieren können.

Keine zusätzlichen NuGet‑Pakete sind über `Aspose.Pdf` hinaus erforderlich.

## Schritt 1: Projekt einrichten und Namespaces importieren

Erstellen Sie ein neues Konsolenprojekt und fügen Sie das Aspose.PDF‑Paket hinzu:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

Importieren Sie in `Program.cs` die Namespaces, die Sie verwenden werden:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Diese Importe stellen die Klassen `Document`, `DictionaryEditor` und COS (Canonical Object Structure) bereit, mit denen Sie **create empty PDF dictionary**‑Objekte erstellen und vorhandene Ressourcen‑Wörterbücher ändern können.

## Schritt 2: Ordner festlegen, der die PDF‑Dateien enthält

Geben Sie das Verzeichnis an, das `input.pdf` enthält. Die Verwendung eines absoluten Pfads vermeidet Mehrdeutigkeiten, wenn das Programm aus einem anderen Arbeitsverzeichnis ausgeführt wird.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Ersetzen Sie `C:\PdfDemo\` durch den Pfad auf Ihrem Rechner. Das Speichern des Pfads in einer Variablen erleichtert die Wiederverwendung für Eingabe‑ und Ausgabedateien.

## Schritt 3: Quell‑PDF‑Dokument öffnen

Laden Sie die zu modifizierende PDF innerhalb eines `using`‑Blocks, damit das Dateihandle automatisch freigegeben wird.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

Das Öffnen des Dokuments gibt Ihnen Zugriff auf die Seitensammlung, Ressourcen‑Wörterbücher und Low‑Level‑COS‑Objekte.

## Schritt 4: Erste Seite und ihr Ressourcen‑Wörterbuch zugreifen

Die erste Seite ist mit `1` indiziert (PDF‑Seiten sind 1‑basiert). Rufen Sie das `Resources`‑Wörterbuch der Seite ab und wickeln Sie es in einen `DictionaryEditor` ein, um sicheres Bearbeiten zu ermöglichen.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` abstrahiert die zugrunde liegende COS‑Struktur und ermöglicht das Lesen oder Erstellen von Einträgen, ohne das PDF zu beschädigen.

## Schritt 5: **Create empty PDF dictionary** für einen neuen graphics state

Ein graphics state steuert Transparenz, Blend‑Modus und andere Zeichenparameter. Um einen benutzerdefinierten Zustand hinzuzufügen, benötigen Sie zunächst ein leeres Wörterbuch und füllen es anschließend mit den erforderlichen Einträgen.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

Der Aufruf von `CreateEmptyDictionary` ist das Kernstück beim **create empty PDF dictionary**. Er gibt ein COS‑Wörterbuch zurück, das zum selben Dokument gehört und die Integrität der Kreuzreferenzen sicherstellt.

### Grafik‑State‑Einträge befüllen

Fügen Sie die Standard‑Schlüssel hinzu:

* `CA` – Strokings‑Alpha‑Konstante (Bereich 0 – 1).
* `ca` – Non‑Strokings‑Alpha‑Konstante.
* `BM` – Blend‑Mode‑Name.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Jeder Eintrag wird zu dem von Ihnen gerade erstellten leeren Wörterbuch hinzugefügt. Durch die Trennung von Definition und Einfügeschleife bleibt der Code lesbar und lässt sich später leicht um weitere Schlüssel erweitern.

### Neuen graphics state im Ressourcen‑Wörterbuch registrieren

Geben Sie dem Zustand einen Namen (`GS0`) und fügen Sie ihn dem `ExtGState`‑Wörterbuch hinzu, das in den Seiten‑Ressourcen enthalten ist.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Jetzt enthält das Ressourcen‑Wörterbuch der Seite eine Referenz auf den benutzerdefinierten graphics state, den Sie später auf Inhaltsströme anwenden können.

## Schritt 6: Aktualisiertes PDF speichern

Schreiben Sie schließlich das geänderte Dokument in eine neue Datei. Das Original unverändert zu lassen, erleichtert die Überprüfung der Änderungen.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

Wenn Sie `output.pdf` in einem Viewer öffnen, der die Inspektion von graphics states unterstützt (z. B. Adobe Acrobat Pro), sehen Sie, dass das `ExtGState`‑Wörterbuch einen Eintrag mit dem Namen `GS0` und den von Ihnen definierten Werten enthält.

## Vollständiger Quellcode

Wenn man alle Teile zusammenfügt, entsteht ein eigenständiges Programm:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Erwartete Ausgabe

Beim Ausführen des Programms wird ausgegeben:

```
PDF updated successfully.
```

und erstellt `output.pdf` im selben Ordner. Das Öffnen der Datei zeigt einen neuen Eintrag unter **Resources → ExtGState → GS0** mit den von Ihnen festgelegten Parametern.

## Häufige Variationen und Sonderfälle

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Multiple pages** benötigen denselben graphics state | Erstellen Sie das Wörterbuch einmal und fügen Sie dann dieselbe `GS0`‑Referenz zu jedem `ExtGState`‑Wörterbuch der Seite hinzu. |
| **Different blend mode** (z. B. `Multiply`) | Ändern Sie den Wert `CosPdfName("Normal")` zu `CosPdfName("Multiply")`. |
| **No existing ExtGState dictionary** | Bevor Sie auf `resourcesEditor["ExtGState"]` zugreifen, prüfen Sie `resourcesEditor.ContainsKey("ExtGState")`. Falls nicht vorhanden, erstellen Sie ein neues leeres Wörterbuch und fügen es zu `firstPage.Resources` hinzu. |
| **Large PDFs** verursachen Speicherbelastung | Verwenden Sie die Überladung `PdfDocument.Load`, die Seiten streamt, oder verarbeiten Sie Seiten einzeln innerhalb des `using`‑Blocks. |
| **Need to edit other resources** (fonts, XObjects) | Ersetzen Sie `"ExtGState"` durch `"Font"` oder `"XObject"` in der `resourcesEditor`‑Suche und folgen Sie dann dem gleichen Muster, ein leeres Wörterbuch zu erstellen und zu befüllen. |

Diese Variationen zeigen, wie das gleiche **create empty PDF dictionary**‑Muster auf jeden Ressourcentyp angewendet werden kann, den Sie **edit PDF resources** möchten.

## Profi‑Tipps

* **Validate the result** – nach dem Speichern öffnen Sie die PDF in einem Tool, das das rohe Ressourcen‑Wörterbuch anzeigen kann (z. B. PDF‑Box’s `PDFDebugger`), um sicherzustellen, dass der Eintrag existiert.
* **Reuse dictionaries** – wenn Sie denselben graphics state zu vielen Seiten hinzufügen, speichern Sie das Wörterbuch in einer Variablen und referenzieren es, anstatt es jedes Mal neu zu erstellen.
* **Version compatibility** – der Code funktioniert mit Aspose.PDF 23.12 und später. Ältere Versionen benötigen möglicherweise `CosDictionary` anstelle von `CosPdfDictionary`.

## Fazit

Sie wissen jetzt, wie man **create empty PDF dictionary**‑Objekte und **edit PDF resources** mit Aspose.PDF für C# verwendet. Das Tutorial behandelte das Öffnen eines Dokuments, den Zugriff auf das Ressourcen‑Wörterbuch der Seite, das Erstellen eines benutzerdefinierten graphics state, dessen Registrierung und das Speichern des Ergebnisses. Von hier aus können Sie mit anderen Ressourcentypen experimentieren, mehrere graphics states kombinieren oder die Technik in eine größere PDF‑Verarbeitungspipeline integrieren.

---

*Bereit, mehr zu erkunden? Versuchen Sie, ein benutzerdefiniertes **ExtGState** zu einem Inhaltsstrom hinzuzufügen, oder manipulieren Sie das **Font**‑Wörterbuch, um neue Schriften einzubetten. Beide folgen dem gleichen Muster, ein leeres Wörterbuch zu erstellen und PDF‑Ressourcen zu bearbeiten.*

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [PDF‑Ressourcen‑Wörterbuch mit Aspose.PDF bearbeiten – C#‑Leitfaden](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Benutzerdefinierten graphics state in PDF mit Aspose.Pdf erstellen](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Wie man einen leeren graphics state in einer PDF mit C# erstellt](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}