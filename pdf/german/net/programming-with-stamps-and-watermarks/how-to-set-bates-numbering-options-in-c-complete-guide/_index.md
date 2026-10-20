---
category: general
date: 2026-08-14
description: Wie man Bates‑Nummerierungsoptionen in C# mit GroupDocs festlegt. Folgen
  Sie dieser Schritt‑für‑Schritt‑Anleitung, um benutzerdefinierte Präfixe und Startnummern
  beim Konvertieren von Word zu PDF hinzuzufügen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: de
lastmod: 2026-08-14
og_description: Wie man die Bates-Nummerierungsoptionen in C# schnell einstellt. Dieser
  Leitfaden zeigt, wie man benutzerdefinierte Präfixe und Startnummern beim Konvertieren
  von Word zu PDF hinzufügt.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Wie man Bates‑Nummerierungsoptionen in C# einstellt – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Wie man Bates‑Nummerierungsoptionen in C# einstellt – vollständige Anleitung
url: /de/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Bates‑Nummerierungsoptionen in C# festlegt – vollständige Anleitung

Wenn Sie **wie man Bates‑Nummerierungsoptionen festlegt** in C# benötigen, führt Sie diese Anleitung Schritt für Schritt durch. Sie lernen, wie Sie die Startnummer festlegen, ein Präfix hinzufügen und die Nummerierung beim Konvertieren eines Word‑Dokuments in PDF mit der GroupDocs API anwenden.

Die Dokumentenverarbeitung erfordert häufig eindeutige Kennzeichnungen auf jeder Seite zu rechtlichen oder archivierenden Zwecken. Am Ende dieses Tutorials besitzen Sie ein wiederverwendbares Snippet, das Sie in jedes .NET‑Projekt einbinden können, egal ob Sie ein Litigation‑Support‑Tool oder einen automatisierten Berichtsgenerator bauen. Keine externen Werkzeuge sind nötig – nur die GroupDocs.Conversion‑Bibliothek und ein paar Zeilen C#.

## Was Sie benötigen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* .NET 6.0 SDK oder neuer installiert  
* Visual Studio 2022 (oder jede IDE, die .NET unterstützt)  
* Eine gültige GroupDocs.Conversion‑Lizenz (die kostenlose Testversion reicht für Tests)  
* Ein Beispiel‑Word‑Dokument (`input.docx`), das Sie nummerieren möchten  

Diese Voraussetzungen stellen sicher, dass der Code ohne zusätzliche Konfiguration läuft.

## Wie man Bates‑Nummerierungsoptionen festlegt – Überblick

Der Kern von **wie man Bates‑Nummerierungsoptionen festlegt** liegt in drei Objekten:

1. `Document` – lädt die Quelldatei.  
2. `BatesNumberingOptions` – enthält die Startnummer, das Präfix und weitere Formatierungsdetails.  
3. `AddBatesNumbering` – die Methode, die die Nummerierung in jede Seite einfügt.

Das Verständnis, warum jedes Bauteil existiert, hilft Ihnen, die Lösung an komplexere Szenarien anzupassen, etwa benutzerdefinierte Schriftarten oder mehrsprachige Nummerierung.

## Schritt 1: Installieren Sie das GroupDocs.Conversion‑NuGet‑Paket

Öffnen Sie ein Terminal im Ordner Ihrer Lösung und führen Sie aus:

```bash
dotnet add package GroupDocs.Conversion
```

Die **GroupDocs API** stellt die Klasse `Document` und die Erweiterungsmethode `AddBatesNumbering` bereit, die später im Tutorial verwendet werden.

## Schritt 2: Laden Sie das Quelldokument

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Warum dieser Schritt?*  
Das Laden der Datei erzeugt eine In‑Memory‑Repräsentation, die die Konvertierungs‑Engine manipulieren kann. Ohne eine `Document`‑Instanz können Sie keine Bates‑Nummerierung oder andere Transformationen anwenden.

## Schritt 3: Erstellen Sie die Bates‑Nummerierungsoptionen

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Warum dieser Schritt?*  
`BatesNumberingOptions` fasst alle Einstellungen zusammen, die Sie benötigen, wenn Sie **Bates‑Nummerierungsoptionen festlegen**. Durch Anpassen von `StartNumber` und `Prefix` können Sie die Ausgabe an Ihr Fall‑Management‑System anpassen. Die Eigenschaft `Position` steuert die visuelle Platzierung, was häufig eine Compliance‑Anforderung ist.

## Schritt 4: Wenden Sie die Bates‑Nummerierung auf das Dokument an

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

Die Methode `AddBatesNumbering` durchläuft jede Seite des geladenen `Document` und fügt die konfigurierte Zeichenkette ein. Da die Methode auf der In‑Memory‑Repräsentation arbeitet, können Sie weitere Verarbeitungsschritte (z. B. Wasserzeichen) vor dem Speichern anketten.

## Schritt 5: Konvertieren und speichern Sie das Ergebnis als PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Warum dieser Schritt?*  
Das Speichern als PDF ist ein gängiges Endformat für juristische Dokumente. Das Objekt `PdfConvertOptions` ermöglicht Feineinstellungen der Ausgabe, ist aber für die Grund‑Nummerierung nicht zwingend erforderlich. Der Aufruf `Save` schreibt das vollständig nummerierte PDF auf die Festplatte.

## Vollständiges, ausführbares Beispiel

Alles zusammengeführt, hier eine eigenständige Konsolenanwendung, die Sie kompilieren und ausführen können:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Erwartete Ausgabe**

Beim Ausführen des Programms wird `output.pdf` erzeugt, in dem jede Seite ein Etikett wie `CASE-1000`, `CASE-1001` usw. im rechten Fußbereich anzeigt. Öffnen Sie das PDF in einem beliebigen Viewer, um zu prüfen, dass die Nummern wie gewünscht erscheinen.

## Häufige Stolperfallen und bewährte Praktiken

| Problem | Warum es passiert | Wie man es vermeidet |
|---------|-------------------|----------------------|
| **Relative Pfade verursachen `FileNotFoundException`** | Das Arbeitsverzeichnis einer Konsolen‑App kann vom Visual‑Studio‑Verzeichnis abweichen. | Verwenden Sie absolute Pfade oder `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Nummerierung überlappt vorhandene Fußzeilen** | Befindet das Quell‑Dokument bereits Inhalt im gewählten Fußzeilenbereich, kann die neue Nummer verdeckt werden. | Wählen Sie eine andere `Position` (z. B. `HeaderLeft`) oder passen Sie die Quell‑Vorlage an. |
| **Große Dokumente sind langsam** | Bates‑Nummerierung iteriert über jede Seite; der Speicherverbrauch steigt mit der Dateigröße. | Verarbeiten Sie das Dokument in Teilen mit `Document.Split`, wenn Sie 500 Seiten überschreiten. |
| **Lizenzablauf** | Die kostenlose Testversion von GroupDocs läuft nach 30 Tagen ab und löst eine Ausnahme bei `AddBatesNumbering` aus. | Setzen Sie vor dem Laden des Dokuments einen gültigen Lizenzschlüssel: `License license = new License(); license.SetLicense("license.lic");`. |

**Pro‑Tipp:** Wenn Sie pro Fall ein anderes Zahlenformat benötigen (z. B. `2023-CASE-001`), bauen Sie das Präfix dynamisch, bevor Sie `BatesNumberingOptions` erstellen.

## Erweiterung der Lösung

Der gleiche **Bates‑Numbering‑C#‑Ansatz** funktioniert mit anderen Quellformaten wie `.txt`, `.html` oder sogar Bildern. Ändern Sie einfach die Dateierweiterung beim Erzeugen des `Document`‑Objekts, und die Konvertierungs‑Engine übernimmt den Rest.

Sie können **Document‑Conversion‑C#** auch mit OCR für gescannte PDFs kombinieren:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Fazit

Sie wissen jetzt **wie man Bates‑Nummerierungsoptionen in C#** von Anfang bis Ende festlegt. Durch Erzeugen eines `BatesNumberingOptions`‑Objekts, Anwenden mit `AddBatesNumbering` und Speichern als PDF können Sie die Produktion rechtlich konformer, eindeutig identifizierter Dokumente automatisieren.  

Ab hier können Sie verwandte Themen wie **C# PDF‑Generierung**, **Document‑Conversion‑C#** oder erweiterte **GroupDocs API**‑Funktionen wie Wasserzeichen und digitale Signaturen erkunden. Experimentieren Sie mit verschiedenen Präfixen, Positionen und Zahlenformaten, um sie an Ihren Workflow anzupassen.

Viel Spaß beim Coden!


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Add Bates Numbering PDF in C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step‑By‑Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}