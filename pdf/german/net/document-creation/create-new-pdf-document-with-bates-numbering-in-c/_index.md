---
category: general
date: 2026-08-04
description: Erstellen Sie ein neues PDF‑Dokument in C# und fügen Sie schnell Bates‑Nummerierung
  mit Aspose.Pdf hinzu – lernen Sie, leere PDF‑Seiten und benutzerdefinierte Seitenzahlen
  hinzuzufügen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: de
lastmod: 2026-08-04
og_description: Erstelle ein neues PDF-Dokument in C# und füge automatisch Bates‑Nummerierung
  für die Rechtsfallverwaltung hinzu – vollständiges Codebeispiel inklusive.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Neues PDF‑Dokument mit Bates‑Nummerierung in C# erstellen
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Neues PDF-Dokument mit Bates‑Nummerierung in C# erstellen
url: /de/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Neues PDF-Dokument mit Bates-Nummerierung in C#

Wenn Sie ein **neues PDF-Dokument erstellen** in C# müssen, zeigt Ihnen diese Anleitung, wie Sie **Bates-Nummerierung zu PDF hinzufügen** mit Aspose.Pdf. Sie lernen, **eine leere Seite zu PDF hinzuzufügen**, **benutzerdefinierte Seitenzahlen zu konfigurieren**, und die endgültige Datei zu speichern.

Das Tutorial deckt jeden Schritt von der Installation der Bibliothek bis zur Erstellung eines PDFs ab, das den Standards für juristische Akten entspricht. Am Ende können Sie ein PDF generieren, eine leere Seite einfügen, Bates-Nummern anwenden und das Nummerierungsformat anpassen – alles mit einem einzigen, ausführbaren Programm.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* .NET 6.0 SDK oder neuer installiert  
* Visual Studio 2022 (oder jede C#‑IDE)  
* Eine aktive Aspose.Pdf für .NET Lizenz oder ein kostenloser Evaluierungsschlüssel  

Sie benötigen keine zusätzlichen NuGet‑Pakete; das Tutorial installiert alles automatisch.

## Schritt 1: Aspose.Pdf über NuGet installieren

Öffnen Sie ein Terminal in Ihrem Projektordner und führen Sie aus:

```bash
dotnet add package Aspose.Pdf
```

Der Befehl fügt die neueste stabile Version von Aspose.Pdf zu Ihrem Projekt hinzu, die die Klassen `Document`, `BatesNumbering` und weitere PDF‑Manipulations‑Klassen bereitstellt, die Sie verwenden werden.

## Schritt 2: Neues PDF-Dokument erstellen – Grundsetup

Das Erstellen der PDF‑Datei ist die Grundlage für alle nachfolgenden Vorgänge. Die Klasse `Document` repräsentiert den gesamten PDF‑Container.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Warum das wichtig ist*: Das Instanziieren von `Document` reserviert die internen Strukturen, die für Seiten, Schriftarten und Grafiken benötigt werden. Die Verwendung von `using var` sorgt dafür, dass die Datei nach dem Speichern ordnungsgemäß freigegeben wird.

## Schritt 3: Leere Seite zu PDF hinzufügen

Ein PDF muss mindestens eine Seite enthalten, bevor Sie Inhalt darauf platzieren können. Das Hinzufügen einer leeren Seite gibt Ihnen eine saubere Leinwand für Bates‑Nummern.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

Die Methode `Pages.Add()` fügt am Ende der Seitensammlung des Dokuments eine neue, leere Seite hinzu. Sie können diesen Aufruf wiederholen, um weitere Seiten hinzuzufügen, falls Sie später **benutzerdefinierte Seitenzahlen** über mehrere Seiten hinweg **add custom page numbers** benötigen.

## Schritt 4: Bates-Nummerierung konfigurieren – wie man Bates hinzufügt

Bates‑Nummerierung ist ein sequenzieller Identifikator, der häufig in juristischen Dokumenten verwendet wird. Sie konfigurieren sie über die Klasse `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Warum das wichtig ist*: `StartNumber` definiert die erste Nummer, `Prefix` fügt ein lesbares Präfix hinzu und `Increment` steuert die Schrittweite. Sie können außerdem `HorizontalAlignment`, `VerticalAlignment`, `FontSize` und `Margins` anpassen, um das Aussehen der Nummer auf jeder Seite zu steuern.

## Schritt 5: Die Bates-Nummerierung auf die Seite anwenden

Jetzt, wo die Nummerierungsoptionen bereitstehen, wenden Sie sie auf die Seite (oder das gesamte Dokument) an.

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Der Aufruf von `Apply` fügt die formatierte Nummer standardmäßig in die Fußzeile der Seite ein. Wenn Sie die Nummer an anderer Stelle benötigen, setzen Sie `bates.Position`, bevor Sie `Apply` aufrufen.

## Schritt 6: PDF mit angewendeter Bates-Nummerierung speichern

Schließlich schreiben Sie das im Speicher befindliche Dokument auf die Festplatte.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Die gespeicherte Datei enthält nun eine einzelne Seite mit der Bates‑Nummer **CaseA-1000**, die am unteren Rand angezeigt wird. Öffnen Sie das PDF in einem beliebigen Viewer, um die Nummerierung zu überprüfen.

## Erwartete Ausgabe

Wenn Sie `BatesNumbered.pdf` öffnen, sollten Sie sehen:

* Eine leere Seite (oder mehr, wenn Sie zusätzliche Seiten hinzugefügt haben)  
* Den Text **CaseA-1000** am unteren Rand der Seite positioniert (Standardposition)  

Wenn Sie weitere Seiten hinzufügen und dieselbe `BatesNumbering`‑Instanz wiederverwenden, werden die Nummern automatisch inkrementiert (CaseA-1001, CaseA-1002, …).

## Profi‑Tipp: Benutzerdefinierte Seitenzahlen zusätzlich zu Bates-Nummern hinzufügen

Manchmal benötigen Sie sowohl Bates‑Nummern als auch traditionelle Seitenzahlen. Sie können beides kombinieren, indem Sie nach dem Anwenden der Bates‑Nummerierung ein `TextFragment` hinzufügen:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Dieses Snippet demonstriert **add custom page numbers**, während das Bates‑Label erhalten bleibt.

## Sonderfall: Bates-Nummerierung auf mehrere Seiten anwenden

Enthält Ihr Dokument mehrere Seiten, können Sie dieselbe `BatesNumbering`‑Instanz in einer Schleife auf jede Seite anwenden:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Die Schleife stellt sicher, dass jede Seite eine sequenzielle Nummer basierend auf dem von Ihnen definierten `StartNumber` und `Increment` erhält.

## Häufige Fallstricke und wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Zahlen erscheinen nicht zentriert | Standardausrichtung passt möglicherweise nicht zu Ihrem Layout | Setzen Sie `bates.HorizontalAlignment` und `bates.VerticalAlignment` explizit |
| Zahlen überlappen bestehenden Inhalt | Es ist kein Rand definiert | Passen Sie `bates.Margin` an oder verwenden Sie `bates.Position`, um die Zahl zu verschieben |
| Lizenzausnahme zur Laufzeit | Evaluierungsversion begrenzt die Ausgabe | Wenden Sie eine gültige Aspose.Pdf-Lizenz an, bevor Sie das Dokument erstellen (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Vollständiges funktionierendes Beispiel

Unten finden Sie ein eigenständiges Programm, das Sie kopieren, einfügen und ausführen können.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Seitenzahlen in PDFs mit Aspose.PDF für .NET hinzufügt und anpasst | Dokumentenmanipulations‑Leitfaden](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET: Seitenzahlen zu PDFs hinzufügen mit FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [PDF-Dokument mit Aspose.PDF erstellen – Seite, Form hinzufügen & speichern](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}