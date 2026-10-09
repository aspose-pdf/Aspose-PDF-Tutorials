---
category: general
date: 2026-02-12
description: Fügen Sie PDF-Dateien schnell Bates‑Nummern hinzu. Erfahren Sie, wie
  Sie ein Textfeld zu einem PDF, ein Formularfeld zu einem PDF und Seitenzahlen zu
  einem PDF mithilfe von Aspose.PDF hinzufügen.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: de
og_description: Fügen Sie Bates‑Nummern zu PDF‑Dokumenten in C# hinzu. Dieser Leitfaden
  zeigt, wie man Textfeld‑PDF, Formularfeld‑PDF und Seitenzahlen‑PDF mit Aspose.PDF
  hinzufügt.
og_title: Bates-Nummern zu PDFs hinzufügen – Vollständiges C#‑Tutorial
tags:
- PDF
- C#
- Aspose.PDF
title: Bates‑Nummern zu PDFs hinzufügen – Schritt‑für‑Schritt C#‑Leitfaden
url: /de/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑Nummern zu PDFs hinzufügen – Vollständiger C# Leitfaden

Haben Sie jemals **Bates‑Nummern** zu einem Stapel juristischer PDFs hinzufügen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. In vielen Kanzleien und e‑Discovery‑Projekten ist das Stempeln jeder Seite mit einem eindeutigen Kennzeichen eine tägliche Aufgabe, und dies manuell zu erledigen ist ein Albtraum.  

Die gute Nachricht? Mit ein paar Zeilen C# und Aspose.PDF können Sie den gesamten Vorgang automatisieren. In diesem Tutorial zeigen wir Ihnen **wie man Bates‑Nummern** hinzufügt, ein Textfeld auf jeder Seite einfügt und ein sauberes, durchsuchbares PDF speichert – ganz ohne Schweiß.

> **Was Sie erhalten:** ein vollständig ausführbares Code‑Beispiel, Erklärungen, warum jede Zeile wichtig ist, Tipps für Randfälle und eine schnelle Checkliste, um Ihre Ausgabe zu überprüfen.  

Wir gehen auch auf verwandte Aufgaben ein wie **add text field pdf**, **add form field pdf** und **add page numbers pdf**, sodass Sie ein Werkzeugkasten für jede Dokument‑Automatisierungs‑Herausforderung haben.

---

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+)  
- Visual Studio 2022 (oder jede IDE Ihrer Wahl)  
- Eine gültige Aspose.PDF for .NET Lizenz (die kostenlose Testversion funktioniert für Tests)  
- Ein Quell‑PDF mit dem Namen `source.pdf` in einem Ordner, den Sie referenzieren können  

Wenn Ihnen einer dieser Punkte unbekannt ist, pausieren Sie kurz und installieren Sie das fehlende Element, bevor Sie fortfahren. Die nachfolgenden Schritte gehen davon aus, dass Sie das Aspose.PDF NuGet‑Paket bereits hinzugefügt haben:

```bash
dotnet add package Aspose.Pdf
```

---

## Wie man Bates‑Nummern zu einem PDF mit Aspose.PDF hinzufügt

Im Folgenden finden Sie das komplette, copy‑paste‑bereite Programm. Es lädt ein PDF, erstellt ein **text box field** auf jeder Seite, schreibt eine formatierte Bates‑Nummer und speichert schließlich die modifizierte Datei.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Warum das funktioniert

- **`Document`** ist der Einstiegspunkt; er repräsentiert die gesamte PDF‑Datei.  
- **`Rectangle`** definiert, wo das Feld auf der Seite platziert wird. Die Zahlen sind in Punkten angegeben (1 pt ≈ 1/72 in). Passen Sie die Koordinaten an, wenn Sie die Nummer in einer anderen Ecke benötigen.  
- **`TextBoxField`** ist ein *Formularfeld*, das beliebige Zeichenketten aufnehmen kann. Durch Zuweisung von `Value` fügen wir effektiv **add page numbers pdf** mit einem benutzerdefinierten Präfix hinzu.  
- **`pdfDocument.Form.Add`** registriert das Feld im AcroForm des PDFs, sodass es in Betrachtern wie Adobe Acrobat sichtbar wird.  

Falls Sie das Aussehen (Schriftart, Farbe, Größe) ändern müssen, können Sie die Eigenschaften von `TextBoxField` anpassen – siehe die Aspose‑Dokumentation zu `DefaultAppearance` und `Border`.

---

## Hinzufügen eines Textfeldes zu jeder PDF‑Seite (der „add text field pdf“-Schritt)

Manchmal möchte man nur ein sichtbares Etikett, kein interaktives Formularfeld. In diesem Fall können Sie das `TextBoxField` durch ein `TextFragment` ersetzen und es direkt zur `Paragraphs`‑Sammlung der Seite hinzufügen. Hier ein kurzer Alternativansatz:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

Der **add text field pdf**‑Ansatz ist nützlich, wenn das endgültige Dokument schreibgeschützt sein soll, während die **add form field pdf**‑Methode die Nummern später editierbar lässt.

---

## Speichern des PDFs mit Bates‑Nummern (der „add page numbers pdf“-Moment)

Nachdem die Schleife abgeschlossen ist, schreibt `pdfDocument.Save` alles auf die Festplatte. Wenn Sie die Originaldatei erhalten möchten, ändern Sie einfach den Ausgabepfad oder verwenden Sie Überladungen von `pdfDocument.Save`, um das Ergebnis direkt als Stream an eine Antwort in einer Web‑API zu senden.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Das ist der elegante Teil – keine temporären Dateien, keine zusätzlichen Bibliotheken, nur Aspose übernimmt die schwere Arbeit.

---

## Erwartetes Ergebnis & Schnell‑Verifizierung

Öffnen Sie `bates.pdf` in einem beliebigen PDF‑Betrachter. Sie sollten in der linken unteren Ecke jeder Seite ein kleines Kästchen sehen mit dem Text:

```
BATES-00001
BATES-00002
…
```

Wenn Sie die Dokumenteigenschaften untersuchen, werden Sie ein AcroForm mit Feldern namens `Bates_1`, `Bates_2` usw. finden. Das bestätigt, dass der **add form field pdf**‑Schritt erfolgreich war.

---

## Häufige Stolperfallen & Pro‑Tipps

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Zahlen erscheinen nicht zentriert | Rechteck‑Koordinaten sind relativ zur linken unteren Ecke der Seite. | Y‑Wert umkehren (`pageHeight - marginTop`) oder `page.PageInfo.Height` verwenden, um eine Platzierung mit Oberrand zu berechnen. |
| Felder sind in Adobe Reader unsichtbar | Der Standardrahmen ist auf „Keine“ gesetzt. | `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` setzen |
| Große PDFs verursachen Speicherdruck | `using` gibt das Dokument erst nach Abschluss der Schleife frei. | Seiten in Chargen verarbeiten oder `pdfDocument.Save` mit `SaveOptions` verwenden, die Streaming ermöglichen. |
| Lizenz nicht angewendet | Aspose druckt ein Wasserzeichen auf die erste Seite. | Lizenz früh registrieren: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Erweiterung der Lösung

- **Benutzerdefinierte Präfixe:** Ersetzen Sie `"BATES-"` durch jede Zeichenkette (`"DOC-"`, `"CASE-"`, …).  
- **Null‑auffüllende Länge:** Ändern Sie `{pageNumber:D5}` zu `{pageNumber:D3}` für drei Stellen.  
- **Dynamische Platzierung:** Verwenden Sie `pdfDocument.Pages[pageNumber].PageInfo.Width`, um das Feld rechtsbündig zu positionieren.  
- **Bedingte Nummerierung:** Überspringen Sie leere Seiten, indem Sie `pdfDocument.Pages[pageNumber].IsBlank` prüfen.

All diese Varianten behalten das Kernmuster von **add bates numbers**, **add text field pdf** und **add form field pdf** bei.

---

## Vollständiges funktionierendes Beispiel (Alles‑in‑Einem)

Im Folgenden finden Sie das finale, sofort ausführbare Programm, das die oben genannten Tipps integriert. Kopieren Sie es in eine neue Konsolen‑App und drücken Sie F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Führen Sie es aus, öffnen Sie das Ergebnis, und Sie sehen einen professionell aussehenden Kennzeichner auf jeder Seite – genau das, was ein Litigation‑Support‑Spezialist erwartet.

---

## Fazit

Wir haben gerade gezeigt, **wie man Bates‑Nummern** zu jedem PDF mit C# und Aspose.PDF hinzufügt. Durch das Erstellen eines **text box field** auf jeder Seite fügen wir gleichzeitig **add text field pdf**, **add form field pdf** und **add page numbers pdf** in einem Durchlauf hinzu. Der Ansatz ist schnell, skalierbar und lässt sich leicht für benutzerdefinierte Präfixe, unterschiedliche Layouts oder bedingte Logik anpassen.

Bereit für die nächste Herausforderung? Versuchen Sie, einen QR‑Code einzubetten, der auf die Original‑Falldatei verweist, oder erzeugen Sie eine separate Index‑Seite, die alle Bates‑Nummern mit den zugehörigen Seitentiteln auflistet. Die gleiche API ermöglicht das Zusammenführen von PDFs, das Extrahieren von Seiten und sogar das Redigieren sensibler Daten – die Möglichkeiten sind grenzenlos.

Wenn Sie auf ein Problem stoßen, hinterlassen Sie unten einen Kommentar oder schauen Sie in die offizielle Aspose‑Dokumentation für tiefere Einblicke. Viel Spaß beim Coden, und mögen Ihre PDFs immer perfekt nummeriert bleiben!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}