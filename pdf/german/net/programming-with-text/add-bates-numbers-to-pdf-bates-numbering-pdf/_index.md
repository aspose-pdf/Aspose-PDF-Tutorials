---
category: general
date: 2026-01-15
description: Fügen Sie Ihrem PDF schnell Bates‑Nummern mit Aspose.Pdf hinzu. Erfahren
  Sie, wie Sie eine Fußzeile zum PDF hinzufügen, Seitenzahlen zum PDF hinzufügen und
  benutzerdefinierte Seitennummerierung einfügen.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: de
og_description: Fügen Sie Ihrem PDF schnell Bates-Nummern mit Aspose.Pdf hinzu. Erfahren
  Sie, wie Sie eine Fußzeile zum PDF hinzufügen, Seitenzahlen einfügen und benutzerdefinierte
  Seitennummerierung erstellen.
og_title: Bates-Nummern zum PDF hinzufügen – Bates-Nummerierung PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Bates-Nummern zum PDF hinzufügen – Bates-Nummerierung PDF
url: /de/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-Nummern zu PDF hinzufügen – Komplettanleitung

Haben Sie jemals **Bates-Nummern** zu einem PDF hinzufügen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – Rechtsteams, Prüfer und alle, die mit riesigen Dokumentensammlungen arbeiten, stoßen täglich auf dieses Problem. Die gute Nachricht? Mit Aspose.Pdf für .NET können Sie diese Nummern mit nur wenigen Zeilen auf jede Seite streuen.

In diesem Tutorial führen wir Sie durch den gesamten Prozess: vom Einbinden der Aspose.Pdf-Bibliothek, Laden Ihrer Quelldatei, Konfigurieren eines *BatesNumberingArtifact*, Anfügen als Fußzeile und schließlich dem Speichern des Ergebnisses. Am Ende wissen Sie außerdem, wie man **add footer to pdf**, **add page numbers pdf** und sogar **add custom page numbering** für knifflige Sonderfälle **add footer to pdf**.

## Was Sie benötigen

- .NET 6+ (oder .NET Framework 4.8, falls Sie noch den klassischen Stack verwenden)  
- Einen Verweis auf das **Aspose.Pdf** NuGet‑Paket (`Install-Package Aspose.Pdf`)  
- Eine PDF‑Datei, die Sie versehen möchten (wir nennen sie `source.pdf`)  

Das war's – keine zusätzlichen Werkzeuge, keine schweren PDF‑Editoren. Lassen Sie uns eintauchen.

![Beispiel für das Hinzufügen von Bates-Nummern](https://example.com/images/add-bates-numbers.png "Beispiel für das Hinzufügen von Bates-Nummern")

## Schritt 1: Bates-Nummern hinzufügen – PDF-Dokument laden

Zuerst benötigen wir ein `Document`‑Objekt, das das PDF repräsentiert, das wir gleich ändern wollen. Denken Sie daran wie beim Öffnen eines Word‑Dokuments, bevor Sie mit dem Schreiben beginnen.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Warum das wichtig ist:** Das Laden der Datei gibt Ihnen Zugriff auf die `Pages`‑Sammlung, in der wir später das Bates‑Nummerierungs‑Artifact anfügen werden. Wenn die Datei nicht gefunden wird, wirft Aspose eine klare `FileNotFoundException`, also überprüfen Sie den Pfad erneut.

## Schritt 2: Einstellungen für die Bates-Nummerierung konfigurieren

Jetzt definieren wir *wie* die Nummern aussehen sollen. Das `BatesNumberingArtifact` ermöglicht das Festlegen eines Präfixes, einer Startnummer, einer Stellenauffüllung, eines Suffixes und der Position. Das ist das Kernstück von **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Profi‑Tipp:** Wenn die Nummern stattdessen in der Kopfzeile erscheinen sollen, ersetzen Sie `BottomCenter` durch `TopCenter`. Das Placement‑Enum unterstützt außerdem `BottomLeft`, `BottomRight` usw., was Ihnen Flexibilität für verschiedene **add footer to pdf**‑Stile gibt.

## Schritt 3: Seitenzahlen hinzufügen – Artifact zu jeder Seite hinzufügen

Mit dem vorbereiteten Artifact durchlaufen wir jede Seite und fügen es der `Artifacts`‑Sammlung hinzu. Das ist der Schritt, der tatsächlich **adds page numbers pdf** ausführt.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Was passiert im Hintergrund?** Die `Artifacts`‑Sammlung wird nach dem Hauptinhalt der Seite gerendert, wodurch die Bates‑Nummer über jeglichem vorhandenen Text, aber unter Anmerkungen liegt. Wenn die Nummer hinter dem Inhalt liegen soll (selten), würden Sie `page.Artifacts.Insert(0, batesArtifact)` verwenden.

## Schritt 4: Benutzerdefinierte Seitennummerierung hinzufügen – Aktualisiertes PDF speichern

Abschließend schreiben wir das modifizierte Dokument auf die Festplatte. Die Ausgabedatei enthält die Bates‑Nummern als festen Bestandteil jeder Seite.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Verifizierungstipp:** Öffnen Sie `bates_out.pdf` in einem beliebigen Viewer. Sie sollten etwas wie `CASE-01000-A` zentriert am unteren Rand jeder Seite sehen. Wenn die Nummern fehlen, überprüfen Sie erneut, ob die `Placement`‑Eigenschaft Ihrem gewünschten Ort entspricht.

## Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier das komplette, sofort ausführbare Programm:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Erwartetes Ergebnis

- **Datei:** `bates_out.pdf` im selben Ordner wie `source.pdf`
- **Visuell:** Text `CASE-01000-A`, `CASE-01001-A`, … zentriert unten auf jeder nachfolgenden Seite
- **Verhalten:** Die Nummern sind dauerhaft eingebettet; sie überstehen das Drucken, das Flattening und weitere Bearbeitungen.

## Häufige Variationen & Sonderfälle

| Situation | Wie anzupassen |
|-----------|---------------|
| **Anders startende Nummer** | Ändern Sie `StartNumber` zu einer beliebigen Ganzzahl (z. B. `StartNumber = 500`). |
| **Buchstaben‑Suffixe pro Band** | Verwenden Sie eine Schleife, um `Suffix` pro Seite zu ändern, oder erstellen Sie mehrere Artifacts mit unterschiedlichen Suffixen. |
| **Rechtsbündige Nummerierung** | Setzen Sie `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Große Dokumente (10 k+ Seiten)** | Erwägen Sie das Stapeln von Seiten oder erhöhen Sie `NumberDigits`, um Überläufe zu vermeiden. |
| **Nummern auf bestimmten Seiten ausblenden** | Überspringen Sie diese Seiten in der `foreach`‑Schleife (z. B. `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Achten Sie auf:** Die Verwendung eines `Prefix` oder `Suffix`, das illegale Dateinamen‑Zeichen enthält (z. B. `*` oder `?`). Aspose bettet sie trotzdem ein, aber sie können später beim Extrahieren des Textes Probleme verursachen.

## Profi-Tipps für den Produktionseinsatz

- **Cache das Artifact**, wenn Sie viele PDFs hintereinander verarbeiten; das einmalige Erstellen spart einige Millisekunden pro Datei.  
- **Thread‑Sicherheit:** Die `BatesNumberingArtifact`‑Instanz ist nicht thread‑sicher, geben Sie also jedem Thread eine eigene Kopie.  
- **Performance:** Für massive Stapel deaktivieren Sie die PDF‑Kompression (`pdfDocument.Compress = false`) vor dem Speichern und aktivieren sie bei Bedarf wieder.  
- **Testing:** Führen Sie immer eine schnelle visuelle Prüfung des zuerst erzeugten PDFs durch, um sicherzustellen, dass die Platzierung den Standards Ihres Rechtsteams entspricht.

## Fazit

Sie haben nun ein solides, durchgängiges Rezept, wie Sie **add bates numbers** zu jedem PDF mit Aspose.Pdf hinzufügen, inklusive Optionen zum **add footer to pdf**, **add page numbers pdf** und **add custom page numbering**. Der Code ist vollständig eigenständig, funktioniert mit .NET 6 und höher und lässt sich in jede bestehende Automatisierungspipeline einbinden.

Was kommt als Nächstes? Versuchen Sie, die `BottomCenter`‑Platzierung durch einen Header‑Stil zu ersetzen, experimentieren Sie mit dynamischen Präfixen (z. B. Fall‑IDs aus einer Datenbank) oder kombinieren Sie dies mit Asposes Text‑Extraktions‑Funktionen, um einen durchsuchbaren Index Ihrer neu nummerierten Dokumente zu erstellen. Der Himmel ist die Grenze, und Sie haben gerade ein leistungsstarkes Werkzeug für die Dokumentenverwaltung erhalten.

Viel Spaß beim Programmieren, und mögen Ihre PDFs stets perfekt nummeriert bleiben!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}