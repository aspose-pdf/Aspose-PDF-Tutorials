---
category: general
date: 2026-03-06
description: Erstelle ein PDF‑Dokument in C# und füge einfach Bates‑Nummern hinzu.
  Lerne, wie du eine leere Seite zum PDF hinzufügst, einen Stempel auf einer Seite
  platzierst und die Bates‑Nummerierung implementierst.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: de
og_description: PDF-Dokument in C# erstellen und Bates-Nummer hinzufügen. Dieser Leitfaden
  zeigt, wie man eine leere PDF-Seite hinzufügt, einen Stempel auf der Seite platziert
  und Bates-Nummerierung anwendet.
og_title: PDF-Dokument mit Bates-Nummerierung erstellen – C#‑Tutorial
tags:
- Aspose.Pdf
- C#
- PDF automation
title: PDF-Dokument mit Bates-Nummerierung in C# erstellen – Vollständige Anleitung
url: /de/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-Dokument mit Bates-Nummerierung in C# erstellen

Haben Sie jemals **ein PDF-Dokument** in C# erstellen müssen und sich gefragt, wie man eine Bates-Nummer hinzufügt, ohne sich die Haare zu raufen? Sie sind nicht allein – Anwaltskanzleien, Gerichte und sogar einige Unternehmens‑Compliance‑Teams stehen täglich vor genau diesem Problem. Die gute Nachricht? Mit ein paar Zeilen Aspose.Pdf‑Code können Sie ein brandneues PDF erzeugen, eine leere Seite hinzufügen und eine korrekte Bates‑Nummer in einem reibungslosen Ablauf stempeln.

In diesem Tutorial führen wir Sie durch den gesamten Prozess: vom Einrichten des Projekts über das Hinzufügen einer leeren PDF‑Seite bis hin zum Ermitteln, **wie man Bates‑Nummerierung hinzufügt**, und schließlich zum **Platzieren des Stempels auf der Seite** und dem Speichern des Ergebnisses. Am Ende haben Sie ein einsatzbereites Snippet, das Sie in jede .NET‑App einbinden können. Keine vagen Verweise, sondern ein vollständiges, ausführbares Beispiel.

## Was Sie benötigen

- **.NET 6+** (oder .NET Framework 4.6+ – Aspose.Pdf funktioniert mit beiden)
- **Aspose.Pdf for .NET** NuGet‑Paket (`Install-Package Aspose.Pdf`)
- Eine brauchbare IDE (Visual Studio, Rider oder VS Code mit C#‑Erweiterung)

Das war's. Keine zusätzlichen DLLs, keine externen Dienste. Lassen Sie uns eintauchen.

## Schritt 1: PDF-Dokument erstellen – Erste Einrichtung

Zuerst benötigen wir ein frisches `Document`‑Objekt. Betrachten Sie es als die leere Leinwand, auf der alles andere platziert wird.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Warum das wichtig ist:** Die `Document`‑Klasse ist der Einstiegspunkt für jede Aspose‑Operation. Durch die Instanziierung erhalten Sie Zugriff auf die `Pages`‑Sammlung, Metadaten und Sicherheitseinstellungen – alles Bausteine für ein professionelles PDF.

## Schritt 2: Leere Seite zum PDF hinzufügen

Ein PDF ohne Seiten ist wie ein Buch ohne Seiten – ziemlich nutzlos. Das Hinzufügen einer leeren Seite ist einfach und liefert uns eine Oberfläche, auf die wir die Bates‑Nummer stempeln können.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Profi‑Tipp:** Wenn Sie mehrere Seiten benötigen, rufen Sie einfach `pdfDocument.Pages.Add()` in einer Schleife auf. Jeder Aufruf liefert ein neues `Page`‑Objekt, das Sie unabhängig anpassen können.

## Schritt 3: Wie man Bates‑Nummerierung hinzufügt – Erstellen des TextStamp

Jetzt kommt das Kernstück: die **Bates‑Nummer**. In Aspose.Pdf ist sie einfach ein `TextStamp` mit einem speziellen Artifact‑Flag.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Warum wir `Artifact` setzen:** Einige PDF‑Reader zeigen Bates‑Nummern als durchsuchbare Metadaten an. Das Markieren des Stempels als `BatesNumbering`‑Artifact stellt sicher, dass nachgelagerte Werkzeuge ihn automatisch erkennen können.

## Schritt 4: Stempel auf Seite platzieren

Mit dem fertigen Stempel **platzieren wir den Stempel auf der Seite**. Dies ist der Schritt, in dem die sichtbare Nummer tatsächlich im PDF erscheint.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Randfall:** Wenn die Nummer auf jeder Seite inkrementiert werden muss, würden Sie über `pdfDocument.Pages` iterieren und `batesStamp.Value` vor dem Aufruf von `AddStamp` aktualisieren. Das Beispiel hier hält es einfach mit einer statischen „Bates‑001“.

## Schritt 5: Ergebnis speichern und überprüfen

Abschließend speichern wir das PDF auf dem Datenträger. Wählen Sie einen Ordner, für den Sie Schreibrechte haben; andernfalls erhalten Sie eine `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Wenn Sie `BatesStamped.pdf` in einem beliebigen Viewer öffnen, sollten Sie ein kleines „Bates‑001“ sauber in der rechten unteren Ecke der leeren Seite sehen.

> **Erwartete Ausgabe:**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *Alt-Text: PDF mit Bates‑Nummer‑Stempel in der rechten unteren Ecke.*

Wenn die Nummer nicht angezeigt wird, überprüfen Sie die Randwerte und stellen Sie sicher, dass die Seitengröße nicht zu klein ist (Standard‑A4 funktioniert gut). Vergewissern Sie sich außerdem, dass das `Artifact`‑Flag nicht von nachgelagerten Verarbeitungstools entfernt wird.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, sofort kopier‑fertige Programm. Es enthält alle `using`‑Direktiven und Kommentare, damit Sie den Überblick behalten.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Führen Sie das Programm aus, öffnen Sie das PDF, und Sie sehen die Bates‑Nummer genau dort, wo wir sie platziert haben. 🎉

## Häufige Varianten & Stolperfallen

| Scenario | What to Change | Why |
|----------|----------------|-----|
| **Mehrere Seiten, inkrementierende Nummern** | Schleife über `pdfDocument.Pages`, setze `batesStamp.Value = $"Bates-{i:D3}"` vor `AddStamp` | Gibt jeder Seite einen eindeutigen Bezeichner, typisch für juristische Dossiers |
| **Andere Platzierung (oben‑links)** | Ändere `HorizontalAlignment = HorizontalAlignment.Left` und `VerticalAlignment = VerticalAlignment.Top` | Einige Organisationen bevorzugen die Nummer in der Kopfzeile statt in der Fußzeile |
| **Benutzerdefinierte Schriftart oder Farbe** | Setze `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Verbessert die Lesbarkeit oder erfüllt Markenrichtlinien |
| **Ein vorhandenes PDF als Hintergrund hinzufügen** | Lade das Quell‑PDF mit `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Nützlich, wenn Sie über ein vorab generiertes Formular stempeln müssen |

## Fazit

Wir haben gerade gezeigt, wie man mit Aspose.Pdf für .NET **ein PDF‑Dokument erstellt**, **eine leere PDF‑Seite hinzufügt** und **eine Bates‑Nummer** einfügt, dann **den Stempel auf der Seite platziert** und die Datei speichert. Der Code ist bewusst kompakt, damit Sie ihn an größere Workflows anpassen können – egal, ob Sie Dutzende von Dateien stapeln oder in einen Web‑Service integrieren.

- Die Inkrement‑Logik für große Akten automatisieren.  
- Die PDF‑Erstellung in eine ASP.NET Core‑API einbetten.  
- Sicherheit hinzufügen (Passwortschutz) mit `pdfDocument.Encrypt(...)`.

Fühlen Sie sich frei zu experimentieren, Dinge zu zerlegen und Fragen in den Kommentaren zu stellen. Viel Spaß beim Coden und möge Ihre PDFs immer perfekt gestempelt sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}