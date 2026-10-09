---
category: general
date: 2026-06-21
description: Fügen Sie schnell Bates‑Nummerierung in Word ein. Erfahren Sie, wie Sie
  Bates hinzufügen, Bates‑Nummerierung für juristische Dokumente anwenden und die
  Nummerierung mit C# automatisieren.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: de
og_description: Fügen Sie Bates‑Nummerierung in Word mit C# hinzu. Dieser Leitfaden
  zeigt, wie man Bates hinzufügt, die Bates‑Nummerierung für Rechtsdokumente anwendet
  und den Vorgang automatisiert.
og_title: Bates-Nummerierung in Word hinzufügen – vollständiger Programmierleitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Bates‑Nummerierung in Word hinzufügen – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-Nummerierung in Word hinzufügen – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie sich schon einmal gefragt, wie man Bates‑Nummerierung zu einer Word‑Datei hinzufügt, ohne jede Nummer manuell einzugeben? Sie sind nicht allein. Viele Anwälte, Paralegals und E‑Discovery‑Spezialisten benötigen eine zuverlässige Methode, um **Bates‑Nummerierung** zu Hunderten von Seiten hinzuzufügen, und das per Hand ist ein Albtraum.

In diesem Tutorial führen wir Sie durch eine saubere C#‑Lösung, die **Bates‑Nummerierung** auf eine `.docx`‑Datei **anwenden** kann, erklären, warum jede Zeile wichtig ist, und zeigen Ihnen, wie Sie den Code für rechtsspezifische Anforderungen anpassen. Am Ende können Sie in Sekunden ein perfekt nummeriertes Dokument erzeugen – ohne zusätzliche Plugins.

## Was Sie lernen werden

- Den genauen Code, der **Bates‑Nummerierung** zu einem Word‑Dokument hinzufügt.  
- Wie die Klasse `BatesNumberingOptions` funktioniert und warum Sie das Präfix oder den Startwert anpassen möchten.  
- Tipps zur Verwendung dieses Ansatzes bei großen Akten, einschließlich speicherbezogener Überlegungen.  
- Einen kurzen Überblick über die Voraussetzungen, damit Sie die Lösung noch heute kopieren, einfügen und ausführen können.

**Voraussetzungen**  
- .NET 6+ (oder .NET Framework 4.7.2+, wenn Sie die ältere Laufzeit bevorzugen).  
- Ein Verweis auf die Aspose.Words for .NET‑Bibliothek (oder eine ähnliche API, die `AddBatesNumbering` bereitstellt).  
- Grundlegende Kenntnisse in C# und Visual Studio (oder Ihrer bevorzugten IDE).

Wenn Sie damit vertraut sind, legen wir los.

## Schritt 1: Projekt einrichten und Bibliothek importieren

Erstellen Sie zunächst eine neue Konsolen‑App (oder integrieren Sie den Code in einen bestehenden Service). Fügen Sie dann das Aspose.Words‑NuGet‑Paket hinzu:

```bash
dotnet add package Aspose.Words
```

> **Pro‑Tipp:** Verwenden Sie die kostenlose Evaluierungslizenz zum Testen; sie fügt ein kleines Wasserzeichen hinzu, funktioniert aber ansonsten exakt wie die Vollversion.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Diese `using`‑Anweisungen bringen die Klassen `Document` und `BatesNumberingOptions` in den Gültigkeitsbereich, die für den späteren Schritt **Bates‑Nummerierung anwenden** unerlässlich sind.

## Schritt 2: Quell‑Dokument laden

Sie benötigen eine Word‑Datei, an der Sie arbeiten können. Der Code unten lädt `input.docx` aus einem von Ihnen angegebenen Ordner. Ersetzen Sie `"YOUR_DIRECTORY"` durch den tatsächlichen Pfad auf Ihrem Rechner.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Warum das Dokument zuerst laden? Das `Document`‑Objekt parsed das gesamte Word‑Paket in den Speicher, sodass wir Header, Footer und Seitenlayout manipulieren können, bevor wir speichern. Wenn die Datei riesig ist (denken Sie an 10 000 Seiten), sollten Sie `LoadOptions` mit `LoadFormat.Docx` verwenden, um Abschnitte zu streamen, anstatt alles auf einmal zu laden.

## Schritt 3: Optionen für die Bates‑Nummerierung konfigurieren

Hier passiert die Magie. Sie teilen der Bibliothek mit, welches Präfix verwendet werden soll (`"ABC-"` im Beispiel) und bei welchem Wert die Zählung beginnen soll (`1000`). Beide Werte sind vollständig anpassbar.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Warum ein Präfix?** In der juristischen Praxis identifizieren Präfixe häufig den Fall oder die erzeugende Partei (`"ABC-"` könnte für *Acme Bank Corp.* stehen). Der Start bei `1000` ist üblich, weil viele Kanzleien die ersten 999 Nummern für interne Entwürfe reservieren.

Wenn Sie **Bates‑Nummerierung für juristische** Dokumente benötigen, können Sie zusätzlich `batesOptions.Position` auf `Header` oder `Footer` setzen und die Ausrichtung an die Gerichtsregeln anpassen. Die Bibliothek unterstützt diese Anpassungen von Haus aus.

## Schritt 4: Bates‑Nummerierung auf das gesamte Dokument anwenden

Jetzt fügen wir die Nummern tatsächlich ein. Die Methode `AddBatesNumbering` durchläuft jede Seite, fügt die formatierte Zeichenkette ein und aktualisiert die interne Seitenzahl des Dokuments.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Im Hintergrund erstellt Aspose.Words ein verstecktes Feld auf jeder Seite, das als `ABC-1000`, `ABC-1001` usw. gerendert wird. Da es ein Feld ist, können Sie später das Präfix oder die Startnummer ändern, ohne die gesamte Datei neu zu generieren – praktisch für **wie man Bates‑Nummerierung hinzufügt**, wenn sich ein Discovery‑Request ändert.

## Schritt 5: Das modifizierte Dokument speichern

Abschließend schreiben Sie die Ausgabe in eine neue Datei. Das Original unverändert zu lassen, ist eine bewährte Praxis, besonders wenn es um Beweismaterial geht, das unverändert bleiben muss.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Sie haben nun `output.docx` mit fortlaufenden Bates‑Nummern auf jeder Seite. Öffnen Sie die Datei in Word, und Sie sehen die Nummern genau dort, wo Sie sie angegeben haben (standardmäßig im Footer). Die Dateigröße kann leicht zunehmen wegen der zusätzlichen Felder, ist aber im Vergleich zu den Vorteilen vernachlässigbar.

### Erwartete Ausgabe

| Seite | Bates‑Nummer |
|------|--------------|
| 1    | ABC-1000     |
| 2    | ABC-1001     |
| …    | …            |
| N    | ABC‑(1000 + N‑1) |

Wenn Sie die „Feld‑Codes“-Ansicht in Word öffnen (`Alt+F9`), sehen Sie etwas wie `{ BATES \* MERGEFORMAT ABC-1000 }` auf jeder Seite.

## Sonderfälle & häufige Fragen

### Was, wenn das Dokument bereits Seitenzahlen enthält?

Die Methode `AddBatesNumbering` **überschreibt** keine bestehenden Seitenzahl‑Felder; sie fügt einfach ein neues Feld hinzu. Wenn Sie die bestehenden Nummern ersetzen wollen, entfernen Sie diese zuerst oder setzen Sie `batesOptions.Position` an dieselbe Position wie die aktuellen Seitenzahlen.

### Kann ich Seiten überspringen (z. B. ein Deckblatt ausschließen)?

Ja. Verwenden Sie die Überladung, die einen `PageRange` akzeptiert:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Das ist nützlich, wenn Sie **Bates‑Nummerierung für juristische** Schriftsätze benötigen, die erst nach einer Titelseite beginnen.

### Wie ändere ich das Nummerierungsformat (römische Zahlen, Buchstaben)?

Die Klasse `BatesNumberingOptions` unterstützt die Eigenschaft `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Setzen Sie sie, bevor Sie `AddBatesNumbering` aufrufen. Diese Flexibilität hilft, wenn ein Gericht einen bestimmten Stil vorschreibt.

### Wie sieht es mit der Performance bei riesigen Dateien aus?

Das Laden einer 2‑GB‑Word‑Datei kann viel RAM verbrauchen. Um dem entgegenzuwirken, verarbeiten Sie das Dokument in Teilen mit dem `DocumentSplitter`‑Utility, wenden Sie die Bates‑Nummerierung auf jeden Teil an und fügen Sie die Abschnitte anschließend wieder zusammen. Dieses Muster hält den Speicherverbrauch im Griff, während Sie **Bates‑Nummerierung effizient anwenden** können.

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier ein sofort ausführbares Konsolen‑Programm:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Programm starten, `output.docx` öffnen – Sie sehen eine saubere Zahlenreihe, bereit für Einreichungen, Discovery oder Gerichtseinreichungen.

## Fazit

Sie wissen jetzt genau **wie man Bates‑Nummerierung** zu einem Word‑Dokument mit C# hinzufügt. Die Schritte – Laden, konfigurieren, anwenden und speichern – sind einfach, aber flexibel genug, um **Bates‑Nummerierung für juristische** Workflows, benutzerdefinierte Präfixe und sogar groß angelegte Batch‑Verarbeitungen zu unterstützen.

Wenn Sie weitergehen wollen, überlegen Sie:

- Den Code in eine Web‑API zu integrieren, sodass Kolleg*innen Dateien hochladen und sofort nummerierte PDFs erhalten.  
- Fehlerbehandlung für fehlende Dateien oder Berechtigungsprobleme hinzuzufügen (ein kurzer `try/catch` um `Document.Load`).  
- Weitere Aspose.Words‑Funktionen wie Wasserzeichen oder Redaktion zu erkunden, um ein komplettes E‑Discovery‑Toolkit zu erhalten.

Experimentieren Sie gern mit verschiedenen Präfixen, Startnummern oder sogar mehreren Nummerierungsschemata im selben Dokument. Die Welt der **Bates‑Nummerierung anwenden** ist überraschend vielseitig, sobald Sie die Kernlogik beherrschen.

Fragen oder ein kniffliges Szenario? Hinterlassen Sie einen Kommentar unten, und wir lösen das gemeinsam. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Features meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [Nummerierungsstil in PDF‑Überschrift mit Java anwenden](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Nummerierungsstil in PDF‑Überschrift mit Java anwenden (Deutsch)](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Nummerierungsstil in PDF‑Überschrift mit Java anwenden (Französisch)](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}