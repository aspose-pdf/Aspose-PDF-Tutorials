---
category: general
date: 2026-06-21
description: Fügen Sie Bates‑Nummerierung zu PDF hinzu und lernen Sie, wie man Bates‑Nummern
  hinzufügt, PDF zu PDF/X‑4 konvertiert, PDF zu PDF/A‑4 konvertiert und PDF in C#
  digital signiert – alles in einem einzigen Leitfaden.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: de
og_description: Bates-Nummerierung zu PDF hinzufügen, erfahren Sie, wie Sie Bates-Nummern
  hinzufügen, PDF in PDF/X‑4 konvertieren, PDF in PDF/A‑4 konvertieren und PDF digital
  mit C# und Aspose.Pdf signieren.
og_title: Bates‑Nummerierung zu PDF hinzufügen – Schritt‑für‑Schritt C#‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Bates-Nummerierung zu PDF hinzufügen – Vollständiger C#‑Leitfaden mit Signierung
  & Konvertierung
url: /de/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering PDF – Komplett‑C#‑Leitfaden mit Signatur & Konvertierung

Haben Sie sich schon einmal gefragt, **add bates numbering pdf** zu verwenden, ohne sich die Haare zu raufen? Sie sind nicht allein. Rechtsteams, Prüfer und alle, die nachvollziehbare Dokumente benötigen, fragen ständig *wie man Bates‑Nummern hinzufügt* zu einem PDF, und dann müssen sie das Dokument außerdem den PDF/X‑4‑ oder PDF/A‑4‑Standards entsprechen und digital signiert sein.  

In diesem Tutorial gehen wir genau darauf ein – mit Aspose.Pdf für .NET **add bates numbering pdf**, zeigen **how to add bates numbers**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4** und schließlich **digitally sign pdf c#**. Am Ende haben Sie ein sofort ausführbares Programm, das drei aufbereitete PDFs erzeugt: eine PDF/X‑4‑Version, eine Bates‑nummerierte Version und eine digital signierte Version.

![add bates numbering pdf example](image-placeholder.png "Screenshot showing add bates numbering pdf in action")

## Was Sie benötigen

- **.NET 6+** (oder .NET Framework 4.6+). Aspose.Pdf unterstützt beides.
- Eine **gültige Aspose.Pdf for .NET‑Lizenz** (oder Sie arbeiten mit der Evaluation, dann erscheinen Wasserzeichen).
- Eine **PKCS#7‑Zertifikatsdatei** (`.pfx`) und das zugehörige Passwort zum Signieren.
- Das **Beispiel‑PDF**, das Sie transformieren möchten (legen Sie es in einem Ordner Ihrer Wahl ab).
- Visual Studio, Rider oder eine beliebige C#‑IDE Ihrer Wahl.

Das war’s – keine zusätzlichen NuGet‑Pakete außer `Aspose.Pdf`. Falls Sie die Bibliothek noch nicht hinzugefügt haben, führen Sie aus:

```bash
dotnet add package Aspose.Pdf
```

Jetzt tauchen wir in den Code ein.

## Schritt 1: Laden des Quell‑PDF‑Dokuments

Zuerst müssen wir die Originaldatei in den Speicher laden. Das ist die Basis für alle nachfolgenden Operationen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Warum das wichtig ist:** Das Laden des PDFs erzeugt ein `Document`‑Objekt, das die gesamte Datei repräsentiert und uns Zugriff auf Konvertierungs‑, Formular‑ und Sicherheits‑APIs gibt.

## Schritt 2: PDF in PDF/X‑4 konvertieren (PDF/A‑4‑Konformität)

Wenn Ihr Workflow Archivqualität erfordert, ist PDF/X‑4 (ein Teilbereich von PDF/A‑4) die richtige Wahl. So **convert pdf to pdf/x-4** Sie mit Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Tipp:** Das Flag `ConvertErrorAction.Delete` entfernt Inhalte, die die Konformität brechen würden, und sorgt für ein sauberes PDF/X‑4‑Ergebnis.

## Schritt 3: PDF/X‑4‑Version speichern

Jetzt, wo das Dokument PDF/X‑4‑konform ist, speichern wir es auf die Festplatte.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Sie besitzen nun eine **convert pdf to pdfa-4**‑kompatible Datei (PDF/X‑4 ist ein Mitglied der PDF/A‑4‑Familie). Öffnen Sie sie gern in Acrobat, um das Konformitäts‑Badge zu prüfen.

## Schritt 4: Bates‑Nummerierung hinzufügen – Der Kern von „Add Bates Numbering PDF“

Bates‑Nummerierung ist ein fortlaufender Identifier, der auf jeder Seite platziert wird. Das ist die exakte Antwort auf *how to add bates numbers* programmatisch.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Warum das funktioniert:** `AddBatesNumbering` durchläuft jede Seite und stempelt die Nummer an der Standardposition (unten rechts). Sie können die Position später über `BatesNumberingOptions` anpassen.

## Schritt 5: Bates‑nummeriertes PDF speichern

Nachdem wir **add bates numbering pdf** durchgeführt haben, benötigen wir eine separate Datei, die die Nummern beibehält.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Öffnen Sie die Datei; Sie sollten „CASE‑5000“, „CASE‑5001“ usw. am unteren Rand jeder Seite sehen.

## Schritt 6: PDF digital signieren – „Digitally Sign PDF C#“ in Aktion

Eine digitale Signatur garantiert Authentizität und Integrität. Im Folgenden **digitally sign pdf c#** wir mit einem SHA‑384‑Hash.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro‑Tipp:** Das `Rectangle` definiert, wo die sichtbare Signatur erscheint. Wenn Sie keinen visuellen Hinweis benötigen, setzen Sie `signatureAppearance` auf `false`.

## Schritt 7: Digital signiertes PDF speichern

Abschließend schreiben wir das signierte Dokument auf die Festplatte.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Sie besitzen nun eine **digitally sign pdf c#**‑Datei, die in jedem PDF‑Reader mit Unterstützung für digitale Signaturen validiert werden kann.

## Vollständiger Quellcode – All‑in‑One‑Lösung

Unten finden Sie das komplette, sofort ausführbare Programm, das alles zusammenführt. Kopieren‑Sie es, passen Sie die Pfade an und drücken Sie **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Erwartete Ausgabe

| Datei | Zweck | Hauptmerkmal |
|------|-------|--------------|
| `sample_pdfx4.pdf` | PDF/X‑4‑Version | Meets PDF/A‑4 compliance |
| `sample_bates.pdf` | Bates‑nummeriertes PDF | **add bates numbering pdf** applied |
| `sample_signed.pdf` | Digital signiertes PDF | **digitally sign pdf c#** with SHA‑384 |

Öffnen Sie eine der drei Dateien in Adobe Acrobat Reader; Sie sehen die Bates‑Nummern in der zweiten Datei und ein Signaturfeld in der dritten.

## Häufig gestellte Fragen (FAQ)

**F: Kann ich die Position der Bates‑Nummern ändern?**  
A: Ja. Verwenden Sie die Eigenschaften von `BatesNumberingOptions` wie `Location` und `FontSize`, um die Platzierung fein abzustimmen.

**F: Was, wenn ich PDF/A‑4 statt PDF/X‑4 benötige?**  
A: Ändern Sie `PdfFormat.PDF_X_4` zu `PdfFormat.PDFA_4` in den Konvertierungsoptionen. Das erfüllt die Anforderung **convert pdf to pdfa-4**.

**F: Mein Zertifikat nutzt einen anderen Hash‑Algorithmus – kann ich SHA‑256 verwenden?**  
A: Absolut. Ersetzen Sie `DigestHashAlgorithm.Sha384` durch `DigestHashAlgorithm.Sha256` (oder einen anderen unterstützten Algorithmus).

**F: Muss ich `document.Save` nach jedem Schritt aufrufen?**  
A: Nicht zwingend. In diesem Ablauf speichern wir nach der Konvertierung und nach der Bates‑Nummerierung, um Ihnen Zwischendateien zu geben. Sie könnten das Speichern bis zum Schluss aufschieben, wenn Sie nur einen Schreibvorgang wünschen.

## Fazit

Wir haben gerade eine praxisnahe, durchgängige Lösung demonstriert, die **add bates numbering pdf**, erklärt **how to add bates numbers**, zeigt **convert pdf to pdf/x-4**, abdeckt


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}