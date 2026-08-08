---
category: general
date: 2026-08-08
description: Bates-Nummerierung zu PDF hinzufügen mit Aspose.Pdf in C#. Dieses Tutorial
  zeigt auch, wie man eine leere PDF‑Seite hinzufügt und PDF programmgesteuert erzeugt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: de
lastmod: 2026-08-08
og_description: Bates‑Nummerierung zu PDF mit Aspose.Pdf in C# hinzufügen. Lernen
  Sie, leere PDF‑Seiten hinzuzufügen, PDFs programmgesteuert zu erzeugen und das endgültige
  Dokument in wenigen Minuten zu speichern.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Bates-Nummerierung zu PDF mit Aspose hinzufügen – vollständiger C#‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Bates-Nummerierung zu PDF mit Aspose hinzufügen – Schritt‑für‑Schritt‑Anleitung
url: /de/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-Nummerierung zu PDF hinzufügen mit Aspose – Schritt‑für‑Schritt‑Anleitung

Bates-Nummerierung zu PDF hinzufügen mit Aspose.Pdf ist einfach, sobald Sie die grundlegenden Schritte verstehen. Wenn Sie zusätzlich ein leeres PDF hinzufügen oder PDF programmgesteuert erzeugen möchten, deckt dieser Leitfaden alles ab, was Sie benötigen.

In diesem Tutorial lernen Sie:

* Ein neues PDF‑Dokument von Grund auf erstellen.  
* Ein leeres PDF hinzufügen, das die Bates‑Nummern aufnehmen wird.  
* Das Bates‑Nummerierungs‑Artifact mit einem benutzerdefinierten Präfix konfigurieren.  
* Das PDF speichern, sodass die Nummern im erzeugten Dokument erscheinen.  

Am Ende verfügen Sie über eine voll funktionsfähige C#‑Konsolenanwendung, die ein PDF mit Bates‑Nummern wie **CASE‑1000**, **CASE‑1001**, … erzeugt – ein gängiges Erfordernis für juristische und e‑Discovery‑Workflows.

## Voraussetzungen

* .NET 6.0 SDK oder neuer (der Code funktioniert auch mit .NET Framework 4.8).  
* Visual Studio 2022 oder eine beliebige C#‑kompatible IDE.  
* Eine gültige Aspose.Pdf‑für‑.NET‑Lizenz (oder ein kostenloser Evaluierungsschlüssel).  
* Grundlegende Kenntnisse der C#‑Syntax.

> **Pro‑Tipp:** Wenn Sie den Code ohne Lizenz ausführen, fügt Aspose dem Ausgabepdf ein kleines Wasserzeichen hinzu.

## Schritt 1: Projekt einrichten und Aspose.Pdf importieren

Ein neues Konsolenprojekt erstellen und das Aspose.Pdf‑NuGet‑Paket hinzufügen:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Die für das Beispiel benötigten `using`‑Direktiven sind:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Diese Namespaces geben Ihnen Zugriff auf die Klassen `Document`, `Page` und `BatesNumberingArtifact`, die später verwendet werden.

## Schritt 2: Ein leeres PDF hinzufügen

Eine Bates‑Nummer muss einer Seite zugeordnet sein, daher erstellen wir zuerst eine leere Seite, die das Nummerierungs‑Artifact erhalten wird.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

Die Klasse `Document` repräsentiert die gesamte PDF‑Datei, während `Pages.Add()` eine neue, leere Seite am Ende der Seitensammlung des Dokuments einfügt. Da das Dokument zu Beginn leer ist, erzeugt dieser Aufruf gleichzeitig die erste Seite.

## Schritt 3: Das Bates‑Nummerierungs‑Artifact konfigurieren

Jetzt definieren wir, wie die Bates‑Nummern aussehen sollen. Mit `BatesNumberingArtifact` können Sie Startnummer, Präfix, Suffix und Formatierungsoptionen festlegen.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Warum das wichtig ist:**  
Die Einstellung `StartNumber` auf **1000** entspricht den üblichen Konventionen für juristische Akten. Das `Prefix` sorgt dafür, dass jede Nummer als **CASE‑1000**, **CASE‑1001**, … erscheint, was die Suche und Sortierung erleichtert.

## Schritt 4: Das Artifact der Seite hinzufügen

Das Artifact muss der `Artifacts`‑Sammlung der Seite hinzugefügt werden, damit Aspose es beim Speichern auf jeder Seite rendert.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Beim Speichern des Dokuments wiederholt Aspose das Artifact automatisch auf allen Seiten und erhöht die Nummer für jede nachfolgende Seite.

## Schritt 5: (Optional) Weitere Seiten hinzufügen

Falls Sie mehr Seiten benötigen, wiederholen Sie einfach `pdfDocument.Pages.Add()`. Das Bates‑Nummerierungs‑Artifact, das Sie im vorherigen Schritt angehängt haben, erscheint automatisch auf jeder neuen Seite.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Schritt 6: PDF speichern – PDF programmgesteuert erzeugen

Zum Schluss das Dokument auf die Festplatte schreiben. An diesem Punkt werden die Bates‑Nummern auf die Seiten gerendert.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Erwartetes Ergebnis:**  
Öffnen Sie *BatesNumberedDocument.pdf* und Sie sehen ein dreiseitiges PDF. Jede Seite zeigt eine Bates‑Nummer in der unteren rechten Ecke:

* Seite 1 → **CASE‑1000**  
* Seite 2 → **CASE‑1001**  
* Seite 3 → **CASE‑1002**

Die Nummern werden automatisch inkrementiert, weil das Artifact an die Seitensammlung angehängt ist.

## Vollständiges, ausführbares Beispiel

Alles zusammengeführt, hier ein komplettes Konsolenprogramm, das Sie kopieren, einfügen und ausführen können:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Programm mit `dotnet run` starten. Nach der Ausführung finden Sie die Datei auf Ihrem Desktop und können die Bates‑Nummern überprüfen.

![Beispiel für Bates‑Nummerierung zu PDF](/images/bates-numbering.png "Beispiel für Bates‑Nummerierung zu PDF")

## Häufige Fragen und Sonderfälle

### Was tun, wenn ich eine andere Schriftart oder Position benötige?

`BatesNumberingArtifact` stellt Eigenschaften wie `FontSize`, `FontColor`, `HorizontalAlignment` und `VerticalAlignment` bereit. Zum Beispiel:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Wie schließe ich eine bestimmte Seite von der Nummerierung aus?

Erstellen Sie ein separates `BatesNumberingArtifact` für die Seiten, die Sie nummerieren möchten, und fügen Sie es nur diesen Seiten hinzu. Seiten ohne angehängtes Artifact bleiben unnummeriert.

### Funktioniert das mit bereits vorhandenen PDFs?

Ja. Statt `new Document()` laden Sie eine bestehende Datei:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Anschließend das Artifact zu den gewünschten Seiten hinzufügen und speichern.

## Fazit

Sie wissen jetzt, wie Sie **Bates‑Nummerierung zu PDF** mit Aspose.Pdf **hinzufügen**, wie Sie **ein leeres PDF hinzufügen** und wie Sie **PDF programmgesteuert erzeugen** in einer sauberen, wiederverwendbaren C#‑Lösung. Der Ansatz funktioniert mit beliebig vielen Seiten, benutzerdefinierten Präfixen und Stiloptionen und gibt Ihnen volle Kontrolle über das Enddokument.

Nächste Schritte, die Sie erkunden könnten:

* **create pdf as


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Seitenzahlen in PDFs mit Aspose.PDF für .NET hinzufügt und anpasst | Dokumenten‑Manipulations‑Leitfaden](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Wie man am Ende eines PDFs eine leere Seite mit Aspose.PDF für .NET hinzufügt | Schritt‑für‑Schritt‑Leitfaden](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [PDF‑Dokument mit Aspose.PDF erstellen – Seite, Form hinzufügen & speichern](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}