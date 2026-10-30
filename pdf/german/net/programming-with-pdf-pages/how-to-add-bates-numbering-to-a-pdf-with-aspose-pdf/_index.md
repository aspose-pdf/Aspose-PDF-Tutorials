---
category: general
date: 2026-10-07
description: Erfahren Sie, wie Sie einer PDF mit C# Bates‑Nummerierung hinzufügen.
  Diese Schritt‑für‑Schritt‑Anleitung behandelt außerdem die Seitennummerierung von
  PDFs und weitere Nummerierungs‑Tricks.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: de
lastmod: 2026-10-07
og_description: Fügen Sie PDFs schnell Bates-Nummerierung hinzu. Folgen Sie diesem
  Tutorial, um die PDF‑Seitenzahlierung zu meistern, PDF‑Seiten zu nummerieren und
  die Dokumentenverfolgung zu automatisieren.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Bates-Nummerierung zu PDFs in C# hinzufügen – vollständige Aspose-Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Wie man einer PDF mit Aspose.Pdf Bates‑Nummerierung hinzufügt
url: /de/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Bates-Nummerierung zu einem PDF mit Aspose.Pdf hinzufügt

Wenn Sie **Bates-Nummerierung** zu einem PDF hinzufügen müssen, zeigt Ihnen diese Anleitung genau, wie Sie dies in C# tun. Egal, ob Sie juristische Dossiers zusammenstellen, Akten verwalten oder einfach zuverlässige **PDF-Seitenzahlen** benötigen, die nachfolgenden Schritte bieten Ihnen eine vollständige, ausführbare Lösung.

In diesem Tutorial lernen Sie, wie man:

* Eine vorhandene PDF-Datei lädt.
* Bates-Nummerierungsoptionen wie Präfix, Startnummer, Stellenauffüllung, Trennzeichen und Suffix konfiguriert.
* Die Nummerierung auf jeder Seite anwendet.
* Das aktualisierte Dokument speichert.

Es werden keine externen Werkzeuge benötigt, außer der Aspose.Pdf für .NET-Bibliothek, und der Code funktioniert mit .NET 6+ sowie .NET Framework 4.7.2+.

---

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| **Aspose.Pdf for .NET** (NuGet-Paket `Aspose.Pdf`) | Stellt die im Code verwendeten Klassen `Document` und `BatesNumberingOptions` bereit. |
| **.NET SDK** (6.0 oder höher empfohlen) | Ermöglicht das Kompilieren und Ausführen der C#-Konsolenanwendung. |
| **Eine Quell-PDF** die Sie nummerieren möchten | Das Tutorial verwendet `source.pdf` als Beispiel; ersetzen Sie den Pfad durch Ihre eigene Datei. |
| **Schreibberechtigung** für den Ausgabordner | Der `Save`-Aufruf muss die neue Datei schreiben. |

Sie können die Bibliothek mit dem folgenden CLI-Befehl installieren:

```bash
dotnet add package Aspose.Pdf
```

---

## Schritt 1: Neues Konsolenprojekt erstellen

Öffnen Sie ein Terminal und führen Sie aus:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Dies erstellt ein minimales C#‑Projekt, das wir mit dem Code füllen, der zum **Hinzufügen von Bates-Nummerierung** benötigt wird.

---

## Schritt 2: Die erforderlichen `using`‑Direktiven hinzufügen

Öffnen Sie `Program.cs` und fügen Sie die Namespaces am Anfang der Datei hinzu:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` gibt Ihnen Zugriff auf die Klasse `Document` zum Laden und Speichern von PDFs.  
* `Aspose.Pdf.Text` enthält `BatesNumberingOptions`, das Objekt, das definiert, wie die Nummern erscheinen.

---

## Schritt 3: Die Quell‑PDF laden

Die erste ausführbare Zeile lädt das PDF, das Sie nummerieren möchten. Ersetzen Sie `"YOUR_DIRECTORY/source.pdf"` durch den tatsächlichen Pfad zu Ihrer Datei.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Falls die Datei nicht gefunden wird, wirft Aspose eine `FileNotFoundException`. Um dies zu vermeiden, sollten Sie den Pfad vorher prüfen:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Schritt 4: Bates-Nummerierungsoptionen definieren

`BatesNumberingOptions` ermöglicht Ihnen die Kontrolle jedes visuellen Elements der Nummerierung. Das untenstehende Beispiel zeigt eine typische Konfiguration für juristische Akten:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Warum jede Eigenschaft wichtig ist**

| Eigenschaft | Zweck |
|-------------|-------|
| `Prefix` | Ermöglicht das Gruppieren von Dokumenten nach Projekt, Kunde oder Fall. |
| `StartNumber` | Setzt den Anfangszähler; nützlich, wenn bereits nummerierte Dateien existieren. |
| `Digits` | Garantiert eine einheitliche Breite, was das Sortieren erleichtert. |
| `Separator` | Verbessert die Lesbarkeit, besonders beim Kombinieren von Präfix und Suffix. |
| `Suffix` | Ermöglicht das Hinzufügen eines Jahres, einer Version oder eines beliebigen nachgestellten Identifikators. |

Sie können auch die Platzierung (oben, unten, links, rechts) und den Schriftstil steuern, indem Sie auf `batesOptions.Position` und `batesOptions.Font` zugreifen. Für die meisten Szenarien funktionieren die Vorgaben (unten‑rechts, 12‑pt Times New Roman) gut.

---

## Schritt 5: Die Nummerierung auf jede Seite anwenden

Der Aufruf von `pdf.BatesNumbering.Add` fügt die Nummern auf jeder Seite in der Reihenfolge ihres Auftretens ein.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Wenn Sie **PDF-Seiten** nur für einen Teilbereich nummerieren müssen (z. B. die Titelseite überspringen), können Sie stattdessen eine `PageCollection` übergeben:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Schritt 6: Das aktualisierte PDF speichern

Schließlich schreiben Sie das modifizierte Dokument auf die Festplatte. Der Dateiname spiegelt in der Regel wider, dass das PDF nun Bates-Nummern enthält.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Falls der Ausgabordner nicht existiert, erstellt Aspose ihn automatisch. Sie sollten jedoch sicherstellen, dass Sie Schreibrechte haben, um eine `UnauthorizedAccessException` zu vermeiden.

---

## Vollständiges, ausführbares Beispiel

Wenn Sie alle Teile zusammenfügen, erhalten Sie ein vollständiges Programm, das Sie kopieren, einfügen und ausführen können:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Erwartete Ausgabe** (Konsole):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Öffnen Sie `bates_numbered.pdf` und Sie werden jede Seite mit einer Beschriftung wie `CASE-001000-2025`, `CASE-001001-2025` usw. sehen, positioniert in der standardmäßigen unteren rechten Ecke.

---

## Häufig gestellte Fragen (FAQ)

### 1. Kann ich den Ort der Nummern ändern?
Ja. Setzen Sie `batesOptions.Position = new Position(10, 10, 10, 10);`, wobei die vier Werte die Abstände vom oberen, unteren, linken und rechten Rand darstellen. Aspose stellt außerdem vordefinierte Enums wie `BatesNumberingPosition.BottomCenter` bereit.

### 2. Was, wenn mein PDF bereits Seitenzahlen enthält?
Das Hinzufügen von Bates-Nummern wird **über** den vorhandenen Zahlen liegen. Um visuelle Unordnung zu vermeiden, können Sie entweder die ursprünglichen Zahlen ausblenden (wenn sie Teil einer Textebene sind) oder die Schriftgröße und Position von `batesOptions` anpassen.

### 3. Funktioniert das mit verschlüsselten PDFs?
Aspose kann passwortgeschützte PDFs öffnen, wenn Sie das Passwort angeben:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Die Bates-Nummerierung wird dann auf dieselbe Weise angewendet.

### 4. Wie nummeriere ich **PDF-Seiten** mit einem einfachen fortlaufenden Zähler (ohne Präfix/Suffix)?
Setzen Sie einfach `Prefix = string.Empty` und `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Kann ich diesen Ansatz in ASP.NET Core verwenden, um PDFs on‑the‑fly zu liefern?
Absolut. Laden Sie das Dokument, wenden Sie die Nummerierung an und schreiben Sie dann den Stream in die HTTP‑Antwort:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Randfälle und bewährte Vorgehensweisen

| Situation | Empfohlener Ansatz |
|-----------|--------------------|
| **Große PDFs (Hunderte von Seiten)** | Rufen Sie `pdf.BatesNumbering.Add` **nach** allen seitenbezogenen Transformationen auf, um zu vermeiden, dass dieselben Seiten mehrfach verarbeitet werden. |
| **Benutzerdefinierte Schriften** | Setzen Sie `batesOptions.Font = FontRepository.FindFont("Arial")` und passen Sie `batesOptions.FontSize` für bessere Lesbarkeit bei gescannten Dokumenten an. |
| **Leistungs‑kritische Batch‑Jobs** | Verwenden Sie eine einzelne `Document`‑Instanz, wenn Sie viele Dateien in einer Schleife verarbeiten; geben Sie sie nach jeder Iteration frei, um Speicher zu sparen. |
| **Internationale Zeichen** | Verwenden Sie Unicode‑kompatible Schriften (z. B. `Times New Roman Unicode`), um sicherzustellen, dass Präfix oder Suffix korrekt angezeigt werden. |
| **Versionskompatibilität** | Der Code funktioniert mit Aspose.Pdf 23.10 und neuer. Wenn Sie eine ältere Version anvisieren, prüfen Sie die API‑Referenz auf mögliche Änderungen von Eigenschaftsnamen. |

---

## Fazit

Sie wissen jetzt, wie Sie **Bates-Nummerierung** zu einem PDF mit Aspose.Pdf für .NET hinzufügen. Das Tutorial behandelte das Laden eines PDFs, das Konfigurieren von `BatesNumberingOptions`, das Anwenden der Nummern auf jede Seite und das Speichern des Ergebnisses. Mit diesen Bausteinen können Sie auch generische **PDF-Seitenzahlen**, **PDF-Seiten nummerieren** mit benutzerdefinierten Formaten implementieren und den Prozess in größere Automatisierungspipelines integrieren.

**Nächste Schritte**

* Erkunden Sie die **bates numbering pdf** API weiter, um Schriftart, Farbe und Platzierung anzupassen.  
* Kombinieren Sie diese Technik mit **digitalen Signaturen**, um manipulationssichere juristische Dossiers zu erstellen.  
* Untersuchen Sie Asposes **PDF-Merging**‑Funktionen, falls Sie mehrere Akten vor der Nummerierung zusammenführen müssen.

Probieren Sie gern verschiedene Präfixe, Suffixe und Stellenlängen aus, um den Ablagevorgaben Ihrer Organisation zu entsprechen. Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}