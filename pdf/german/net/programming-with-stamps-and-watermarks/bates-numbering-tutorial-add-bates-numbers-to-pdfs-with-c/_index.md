---
category: general
date: 2026-02-25
description: Bates‑Nummerierungstutorial – lernen Sie, wie Sie PDF‑Seitenzahlen hinzufügen
  und benutzerdefinierte Bates‑Nummerierung mit Aspose.Pdf in C# anwenden. Schritt‑für‑Schritt‑Anleitung
  mit vollständigem Code.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: de
og_description: Das Bates‑Nummerierungs‑Tutorial zeigt, wie man Seitenzahlen zu PDFs
  hinzufügt und benutzerdefinierte Bates‑Nummerierung in C# implementiert. Vollständiger
  Code, Erklärungen und Tipps.
og_title: Bates-Nummerierungstutorial – Bates-Nummern zu PDFs mit C# hinzufügen
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Bates-Nummerierungstutorial: Bates-Nummern zu PDFs mit C# hinzufügen'
url: /de/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑Nummerierungstutorial – Hinzufügen von Bates‑Nummern zu PDFs in C#

Haben Sie sich jemals gefragt, wie man Seitenzahlen zu PDFs hinzufügt und gleichzeitig eine rechtlich formatierte Bates‑Nummer einbettet? Sie sind nicht allein. In diesem **bates numbering tutorial** führen wir Sie durch alles, was Sie wissen müssen, um jede Seite eines PDFs mit einem benutzerdefinierten Präfix, führenden Nullen und präziser Positionierung zu versehen – mit Aspose.Pdf für .NET.

Die gute Nachricht? Es ist ziemlich einfach, sobald Sie die Kernkonzepte verstanden haben. Am Ende dieses Leitfadens haben Sie ein ausführbares Programm, das *input.pdf* nimmt und *bates_out.pdf* mit einem sauberen „ABC‑01000“-Label auf jeder Seite erzeugt. Tauchen wir ein.

## Was Sie benötigen

- **Aspose.Pdf for .NET** (Version 23.10 oder neuer). Die Bibliothek ist kommerziell, aber eine kostenlose Testversion reicht zum Lernen völlig aus.
- .NET 6+ SDK (jede aktuelle Version ist ausreichend).
- Eine grundlegende C#‑Entwicklungsumgebung – Visual Studio, VS Code oder Rider.
- Ein Eingabe‑PDF zum Experimentieren (jedes mehrseitige Dokument veranschaulicht den Effekt).

Keine zusätzlichen NuGet‑Pakete über Aspose.Pdf hinaus sind erforderlich, und der Code läuft unter Windows, Linux oder macOS ohne Änderungen.

## Schritt 1: Laden des Quell‑PDF‑Dokuments (bates numbering tutorial – Initialisierung)

Zuerst erstellen wir ein `Document`‑Objekt, das das PDF repräsentiert, das wir ändern möchten. Betrachten Sie es als das Laden einer leeren Leinwand, auf die Sie zeichnen können.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Warum das wichtig ist:** Ohne das Laden der Datei gibt es nichts zu annotieren. Die Plausibilitätsprüfung verhindert ein stilles Versagen später, wenn Sie versuchen, Artefakte zu einer nicht existierenden Seitensammlung hinzuzufügen.

## Schritt 2: Definieren des Bates‑Nummerierungsartefakts (how to add bates)

Ein *BatesNumberingArtifact* teilt Aspose mit, wo und wie der Bezeichner gezeichnet werden soll. Sie können das Präfix, die Startnummer, die Nullauffüllung, die Schriftgröße und die genauen X/Y‑Koordinaten steuern.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Warum das wichtig ist:** Die Eigenschaft `LeadingZeros` stellt sicher, dass jedes Label die gleiche Länge hat, was für Rechtsdokumente, bei denen die Ausrichtung wichtig ist, entscheidend ist. Passen Sie `X` und `Y` an, um den Stempel nach oben rechts, unten links oder an jede gewünschte Position zu verschieben.

## Schritt 3: Anbringen des Artefakts an jeder Seite (add page numbers pdf)

Jetzt iterieren wir über jede Seite und hängen dasselbe Artefakt an. Hier wird die Anforderung *add page numbers pdf* erfüllt – jede Seite erhält automatisch ihr eigenes sequenzielles Label.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Warum das wichtig ist:** Durch das Hinzufügen des Artefakts zur `Artifacts`‑Sammlung anstatt Text manuell zu zeichnen, lässt man Aspose die Nummerierungslogik, führende Nullen und das Rendern verwalten. Das reduziert Fehler und hält den Code kompakt.

## Schritt 4: Speichern des modifizierten PDFs (add bates numbering)

Abschließend speichern wir die Änderungen in einer neuen Datei. Es ist eine gute Gewohnheit, in einen anderen Dateinamen zu schreiben, damit das Original unverändert bleibt.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Warum das wichtig ist:** Die Methode `Save` schreibt das gesamte PDF und bettet die Artefakte als Teil des Seiten‑Content‑Streams ein. Die resultierende Datei kann in jedem PDF‑Betrachter geöffnet werden und zeigt die Bates‑Nummern exakt wie angegeben.

## Vollständiges funktionierendes Beispiel (Alle Schritte kombiniert)

Unten finden Sie das komplette, sofort ausführbare Programm. Kopieren Sie es in ein Konsolen‑App‑Projekt, ersetzen Sie die Platzhalter‑Pfade und drücken Sie **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Erwartetes Ergebnis

Öffnen Sie *bates_out.pdf* in Adobe Reader, Foxit oder einem beliebigen Viewer. Sie sollten ein Label wie **ABC‑01000** auf der ersten Seite, **ABC‑01001** auf der zweiten usw. sehen, positioniert 50 pt vom linken Rand und 30 pt vom unteren Rand. Die Zahlen sind wegen der führenden Nullen rechtsbündig, was dem Dokument ein sauberes, professionelles Aussehen verleiht.

## Häufige Variationen & Sonderfälle

| Szenario | Wie anpassen |
|----------|---------------|
| **Anderes Präfix** | Ändern Sie `Prefix = "XYZ"` in der Artefaktdefinition. |
| **Bei einer benutzerdefinierten Nummer starten** | Setzen Sie `Start = 5000` (oder eine beliebige ganze Zahl). |
| **Platzieren Sie die Nummer in der oberen rechten Ecke** | Verwenden Sie `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Schriftgröße für größere Dokumente ändern** | Ändern Sie `FontSize = 12` (oder eine beliebige Größe). |
| **Ein Hintergrundrechteck hinzufügen** | Erstellen Sie ein `RectangleArtifact` und fügen Sie es vor dem `BatesNumberingArtifact` hinzu. |
| **Bestimmte Seiten überspringen** | Fügen Sie innerhalb der `foreach`‑Schleife ein `if (page.Number % 2 == 0) continue;` hinzu, um gerade Seiten zu überspringen. |

**Pro‑Tipp:** Testen Sie immer zuerst mit einem kurzen PDF. Es ist schneller, die Positionierung zu überprüfen, bevor Sie das Skript auf einer 200‑seitigen Aktenmappe ausführen.

## Häufig gestellte Fragen

- **Funktioniert das mit verschlüsselten PDFs?**  
  Aspose.Pdf kann passwortgeschützte Dateien öffnen, wenn Sie das Passwort über `Document(string, string)` übergeben. Das Bates‑Artefakt wird nach der Entschlüsselung weiterhin angewendet.

- **Kann ich sowohl Bates‑Nummern als auch reguläre Seitenzahlen hinzufügen?**  
  Ja. Fügen Sie ein `PageNumberArtifact` neben dem `BatesNumberingArtifact` hinzu. Jedes Artefakt verwaltet seinen eigenen Zähler.

- **Was ist, wenn mein PDF unterschiedliche Seitengrößen hat?**  
  Die Werte von `Position` sind absolute Punkte. Für Dokumente mit gemischten Größen berechnen Sie die Position pro Seite innerhalb der Schleife mit `page.PageInfo.Width` und `page.PageInfo.Height`.

## Nächste Schritte & verwandte Themen

Jetzt, da Sie das **bates numbering tutorial** gemeistert haben, möchten Sie vielleicht Folgendes erkunden:

- **Wasserzeichen hinzufügen** – ähnlicher Artefakt‑Ansatz mit `TextArtifact`.
- **Mehrere PDFs zusammenführen** – verwenden Sie `Document.AppendDocument`.
- **Text für die Suchindizierung extrahieren** – `TextAbsorber`‑Klasse.
- **Batch‑Verarbeitung automatisieren** – über einen Ordner mit PDFs iterieren und dasselbe Artefakt anwenden.

All diese Themen bauen auf denselben Konzepten auf, die Sie gerade gelernt haben, sodass Sie gut positioniert sind, um Ihr PDF‑Automatisierungs‑Toolkit zu erweitern.

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen oder Ideen für weitere Anpassungen haben, hinterlassen Sie gerne einen Kommentar unten. Die Welt der PDF‑Manipulation ist groß, aber mit einem soliden **bates numbering tutorial** im Gepäck sind Sie bereits einen Schritt voraus.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}