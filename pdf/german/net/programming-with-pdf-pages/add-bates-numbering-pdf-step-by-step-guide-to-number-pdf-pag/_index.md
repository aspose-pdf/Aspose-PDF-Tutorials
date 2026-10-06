---
category: general
date: 2026-03-03
description: Bates‑Nummerierung für PDFs schnell hinzufügen und lernen, wie man PDF‑Seiten
  nummeriert oder sequenzielle PDF‑Nummern mit Aspose.Pdf in C# hinzufügt.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: de
og_description: Bates-Nummerierung zu PDF in C# hinzufügen, um PDF-Seiten zu nummerieren
  und fortlaufende PDF-Nummern hinzuzufügen. Vollständiger Code, Erklärungen und bewährte
  Methoden.
og_title: Bates-Nummerierung zu PDF hinzufügen – Vollständiges C#‑Tutorial
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: Bates‑Nummerierung zu PDF hinzufügen – Schritt‑für‑Schritt‑Anleitung zum Nummerieren
  von PDF‑Seiten
url: /de/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-Nummerierung zu PDF hinzufügen – Komplettes C#‑Tutorial

Haben Sie jemals **Bates-Nummerierung zu PDF**‑Dateien hinzufügen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – Rechtsabteilungen, Prüfer und Archivare kämpfen mit demselben Problem. Die gute Nachricht? Mit ein paar Zeilen C# und der Aspose.Pdf‑Bibliothek können Sie **PDF‑Seiten automatisch nummerieren** und erhalten sogar die Flexibilität, **sequenzielle PDF‑Nummern** mit benutzerdefinierten Präfixen, Suffixen und Platzierungen hinzuzufügen.

In diesem Leitfaden gehen wir ein reales Beispiel durch, erklären, warum jede Einstellung wichtig ist, und zeigen, wie Sie den Code für Sonderfälle wie unterschiedliche Seitengrößen oder benutzerdefinierte Ziffernzahlen anpassen können. Am Ende haben Sie ein sofort ausführbares Snippet, das Bates‑Nummern zu jeder PDF hinzufügt, die Sie ihm geben, und Sie verstehen das „Warum“ hinter jeder Option.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie folgendes haben:

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+).
- Eine gültige Aspose.Pdf für .NET Lizenz (oder ein kostenloser Evaluierungsschlüssel).
- Visual Studio 2022 (oder ein beliebiger C#‑Editor Ihrer Wahl).
- Eine Quell‑PDF‑Datei namens `source.pdf` in einem Ordner, den Sie referenzieren können.

Das war’s – keine zusätzlichen NuGet‑Pakete außer Aspose.Pdf.

## Schritt 1 – Quell‑PDF‑Dokument öffnen

Das Erste, was Sie tun müssen, ist das PDF zu laden, das Sie stempeln möchten. Die Verwendung eines `using`‑Blocks stellt sicher, dass das Dateihandle korrekt freigegeben wird, was spätere Sperrprobleme verhindert.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Warum das wichtig ist:** Das Öffnen des Dokuments innerhalb einer `using`‑Anweisung gewährleistet eine deterministische Entsorgung. Wenn Sie das weglassen, kann die Datei gesperrt bleiben, und nachfolgende Versuche, das PDF zu speichern oder zu löschen, schlagen fehl – etwas, das ich in Produktionspipelines schon als Kopfschmerz erlebt habe.

## Schritt 2 – Bates‑Nummerierungsoptionen konfigurieren

Jetzt teilen wir Aspose mit, wie die Bates‑Nummern aussehen sollen. Jede Eigenschaft entspricht direkt einem visuellen Element auf der Seite.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Schnelle Tipps zu den Optionen

| Property | Was es bewirkt | Wann ändern |
|----------|----------------|-------------|
| **Prefix / Suffix** | Fügt statischen Text vor bzw. nach dem numerischen Teil hinzu. | Verwenden Sie eine Fall‑ID, Projektcode oder „CONF‑“ für vertrauliche Dokumente. |
| **Start** | Die erste Nummer in der Serie. | Wenn Sie ein Nummerierungsschema aus einem vorherigen Batch fortsetzen, setzen Sie diesen Wert entsprechend. |
| **NumberOfDigits** | Steuert die Null‑Auffüllung. | Für juristische Einreichungen benötigen Sie oft exakt 6 Stellen; setzen Sie es auf `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Wählen Sie basierend auf dem Layout Ihres Dokuments; BottomRight ist am häufigsten für Bates‑Nummern. |

> **Pro‑Tipp:** Wenn Sie **PDF‑Seiten** in mehreren Spalten **nummerieren** müssen, können Sie `pdfDocument.AddBatesNumbering` zweimal mit unterschiedlichen `Placement`‑Werten und verschiedenen `Prefix`‑Zeichenketten aufrufen.

## Schritt 3 – Bates‑Nummerierung auf das Dokument anwenden

Mit den vorbereiteten Optionen ist das eigentliche Stempeln ein einzelner Methodenaufruf. Aspose übernimmt intern die Seitennummerierung, Drehung und Randberechnungen.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Warum ein einzelner Aufruf funktioniert:** Intern iteriert Aspose über `pdfDocument.Pages`, erstellt für jede Seite ein `TextFragment` und positioniert es basierend auf dem von Ihnen gewählten `Placement`. Diese Abstraktion erspart Ihnen das Schreiben einer manuellen Schleife und das Handhaben von Koordinatentransformationen.

## Schritt 4 – Aktualisiertes PDF speichern

Schließlich schreiben Sie die modifizierte Datei auf die Festplatte. Sie können das Original überschreiben oder eine neue Datei erstellen; das untenstehende Beispiel erzeugt eine frische Kopie.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

Wenn Sie **sequenzielle PDF‑Nummern** zu einem Stream hinzufügen müssen (z. B. beim Senden der Datei über eine API), ersetzen Sie den Dateipfad durch einen `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier das komplette, sofort ausführbare Programm:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Erwartete Ausgabe

- Eine neue Datei `bates_numbered.pdf` erscheint in `C:\MyDocs`.
- Jede Seite zeigt etwas wie `2025-05000-A`, `2025-05001-A`, … in der rechten unteren Ecke.
- Die Zahlen sind mit führenden Nullen auf fünf Stellen aufgefüllt, entsprechend der Einstellung `NumberOfDigits`.

## Umgang mit gängigen Variationen

### 1. Unterschiedliche Seitengrößen

Wenn Ihr PDF Hoch- und Querformatseiten mischt, kann es vorkommen, dass die Nummer an der breiteren Seite abgeschnitten wird. Aktivieren Sie dazu die `AutoFit`‑Eigenschaft:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Benutzerdefinierte Schriftart oder Farbe

Bates‑Nummern sind standardmäßig schwarz, 12 pt Times New Roman. Ändern Sie das Aussehen, indem Sie auf den `TextState` zugreifen:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Seiten überspringen

Angenommen, Sie möchten **PDF‑Seiten** nummerieren, aber die Titelseite überspringen. Verwenden Sie einen Seitenbereich:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Mehrere Nummerierungsschemata hinzufügen

Rechtsabteilungen benötigen manchmal sowohl eine Bates‑Nummer als auch ein vertrauliches Wasserzeichen. Führen Sie zwei separate `AddBatesNumbering`‑Aufrufe mit unterschiedlichen `Placement`‑Werten aus:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Häufig gestellte Fragen

**Q: Funktioniert das mit PDFs, die bereits vorhandenen Text enthalten?**  
A: Ja. Aspose fügt die Bates‑Nummer als separate Ebene hinzu, sodass vorhandener Inhalt unverändert bleibt. Wenn Sie die Nummern *hinter* bestehendem Text anzeigen lassen müssen (selten), müssten Sie die Inhaltsstreams der Seite manuell manipulieren.

**Q: Was ist, wenn das PDF passwortgeschützt ist?**  
A: Laden Sie es zuerst mit dem Passwort: `new Document(path, new LoadOptions { Password = "secret" })`. Nach dem Stempeln können Sie die Verschlüsselung erneut mit `pdfDocument.Encrypt(...)` anwenden.

**Q: Kann ich das in einer .NET‑Core‑Konsolenanwendung verwenden?**  
A: Absolut. Der gleiche Code funktioniert in .NET Core, .NET 5+ und .NET Framework. Verweisen Sie einfach auf das passende Aspose.Pdf‑NuGet‑Paket.

## Fazit

Wir haben gerade erklärt, wie man **Bates‑Nummerierung zu PDF**‑Dateien hinzufügt, wie man **PDF‑Seiten nummeriert** und wie man **sequenzielle PDF‑Nummern** mit voller Kontrolle über Formatierung, Platzierung und Sonderfall‑Behandlung hinzufügt. Das kurze Snippet oben übernimmt die Hauptarbeit, während die zusätzlichen Optionen es Ihnen ermöglichen, die Lösung an jeden rechtlichen, archivierenden oder Compliance‑Workflow anzupassen.

Bereit für den nächsten Schritt? Versuchen Sie, diesen Ansatz zu kombinieren mit:

- **Batch‑Verarbeitung** – iterieren Sie über einen Ordner mit PDFs und wenden Sie das gleiche Nummerierungsschema an.
- **Dynamische Präfixe** – holen Sie Fall‑IDs aus einer Datenbank und fügen Sie sie pro Dokument ein.
- **PDF/A‑Konformität** – nach der Nummerierung rufen Sie `pdfDocument.Convert(..., PdfFormat.PdfA2b)` auf, um langfristige Archivierung sicherzustellen.

Fühlen Sie sich frei zu experimentieren, Ihre Ergebnisse zu teilen oder Fragen in den Kommentaren zu stellen. Viel Spaß beim Coden, und möge Ihre PDFs immer perfekt indiziert bleiben!

![Screenshot einer PDF‑Seite mit Bates‑Nummern in der rechten unteren Ecke](https://example.com/images/bates-numbered.png "Beispiel für Bates-Nummerierung zu PDF hinzufügen")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}