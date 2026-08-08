---
category: general
date: 2026-08-04
description: Wie man Aspose verwendet, um Text aus gescannten PDFs zu extrahieren
  und PDFs mit C# in Text zu konvertieren. Lernen Sie, gescannte PDF‑Dateien zu lesen
  und zuverlässige OCR‑Ergebnisse zu erhalten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: de
lastmod: 2026-08-04
og_description: Wie man Aspose verwendet, um gescannte PDF‑Dateien zu lesen, den Text
  aus gescannten PDFs zu extrahieren und PDF in Text zu konvertieren, mit einem vollständigen,
  ausführbaren Beispiel.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Wie man Aspose verwendet – Text aus gescannten PDFs in C# extrahieren
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Wie man Aspose verwendet, um Text aus einem gescannten PDF zu extrahieren –
  Schritt‑für‑Schritt‑Anleitung
url: /de/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Aspose verwendet, um Text aus einem gescannten PDF zu extrahieren – Schritt‑für‑Schritt‑Anleitung

Wenn Sie **wie man Aspose verwendet** für OCR benötigen, zeigt Ihnen diese Anleitung, wie Sie Text aus einem gescannten PDF in wenigen Zeilen C# extrahieren können. Egal, ob Sie einen Dokumenten‑Archivierungsservice oder einen Suchindex für alte Unterlagen erstellen, die Lösung funktioniert mit jedem gescannten PDF, das Sie an den Aspose.Pdf.AI‑Dienst übergeben.

In diesem Tutorial werden Sie:

* Einen OCR‑Copiloten erstellen, der ein gescanntes PDF liest.
* Den erkannten Text asynchron extrahieren.
* Den extrahierten String anzeigen oder weiterverarbeiten.

Die einzige Voraussetzung ist ein aktives Aspose.Pdf.AI‑Abonnement und eine .NET 6 (oder neuere) Entwicklungsumgebung.

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| .NET 6 SDK oder neuer | Stellt `async Main` und moderne Sprachfeatures bereit. |
| Aspose.Pdf.AI NuGet-Paket (`Aspose.Pdf.AI`) | Enthält die `AICopilotFactory` und OCR‑Optionen. |
| Eine gültige Aspose.Pdf.AI `client`‑Instanz (API‑Schlüssel) | Authentifiziert Ihre Anfragen beim Cloud‑Dienst. |
| Eine gescannte PDF‑Datei (z. B. `Scanned.pdf`) | Das Quelldokument, aus dem der Text extrahiert wird. |

Installieren Sie das Paket mit der .NET‑CLI:

```bash
dotnet add package Aspose.Pdf.AI
```

## Schritt 1: Einrichten des Aspose.Pdf.AI‑Clients

Bevor Sie irgendeinen OCR‑Endpunkt aufrufen können, müssen Sie einen Client erstellen, der Ihre API‑Anmeldedaten enthält. Der Client ist thread‑safe und kann für mehrere Dokumente wiederverwendet werden.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**Warum dieser Schritt erforderlich ist** – Der Aspose‑Dienst prüft jede Anfrage anhand Ihres Abonnements. Das einmalige Erstellen des Clients vermeidet wiederholte Netzwerk‑Handshakes und hält den Code sauber.

## Schritt 2: Erstellen eines OCR‑Copiloten für das gescannte PDF‑Dokument

Die `AICopilotFactory` baut einen spezialisierten OCR‑Copiloten, der weiß, wie die von Ihnen angegebene Datei zu verarbeiten ist. Sie übergeben den `client` und ein `OpenAIOcrOptions`‑Objekt, das auf den PDF‑Pfad zeigt.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Erklärung** – `CreateOcrCopilot` kapselt alle Low‑Level‑HTTP‑Aufrufe. Die Methode `WithDocument` teilt dem Dienst mit, welche Datei analysiert werden soll; Sie können auch einen `Stream` übergeben, wenn das PDF im Speicher liegt.

## Schritt 3: Asynchrones Extrahieren des erkannten Textes

Der Aufruf von `GetTextAsync` führt die OCR‑Operation in der Cloud aus und gibt das Klartext‑Ergebnis zurück. Da die Operation einige Sekunden dauern kann, ist die Methode asynchron.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Warum asynchron?** – Netzwerk‑Latenz und OCR‑Verarbeitungszeit sind unvorhersehbar. Durch `await` wird verhindert, dass Ihre Anwendung den Haupt‑Thread blockiert, was besonders in UI‑ oder Web‑Service‑Szenarien wichtig ist.

## Schritt 4: Verwenden des extrahierten Textes

An diesem Punkt haben Sie einen regulären .NET `string`, der die vollständige Transkription des gescannten PDFs enthält. Sie können ihn in die Konsole schreiben, in einer Datenbank speichern oder an eine Suchmaschine weitergeben.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Erwartete Ausgabe

Wenn `Scanned.pdf` eine einzelne Seite mit dem Satz „Hello, world!“ enthält, zeigt die Konsole:

```
=== OCR Result ===
Hello, world!
```

Bei mehrseitigen Dokumenten wird der Text jeder Seite aneinandergehängt, wobei Zeilenumbrüche erhalten bleiben.

## Vollständiges, ausführbares Beispiel

Unten finden Sie ein komplettes Programm, das Sie in ein neues Konsolenprojekt (`dotnet new console`) einfügen können. Es demonstriert **wie man Aspose verwendet** von Anfang bis Ende, inklusive Fehlerbehandlung für gängige Stolperfallen.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**Wichtige Punkte im Beispiel**

* `await` sorgt für nicht‑blockierende Ausführung.
* Der `try/catch`‑Block gibt Netzwerk‑ oder Service‑Fehler aus, was essenziell ist, wenn **gescannte PDF**‑Dateien in großem Umfang gelesen werden.
* Ersetzen Sie `YOUR_API_KEY` und `YOUR_DIRECTORY/Scanned.pdf` durch reale Werte, bevor Sie das Programm ausführen.

## Umgang mit Randfällen und Best‑Practice‑Tipps

| Situation | Empfohlener Ansatz |
|-----------|--------------------|
| **Große PDFs ( > 50 MB )** | Teilen Sie das Dokument clientseitig in kleinere Stücke und verarbeiten Sie jedes Stück mit einem separaten Copiloten. Das reduziert den Speicherverbrauch und erhöht die Zuverlässigkeit. |
| **Scans von schlechter Qualität** | Passen Sie die OCR‑Qualität an, indem Sie `.WithLanguage("eng")` oder `.WithEnhanceImage(true)` zu `OpenAIOcrOptions` hinzufügen. Der Service unterstützt Sprach‑Hinweise, die die Genauigkeit verbessern. |
| **Mehrere Sprachen** | Geben Sie eine kommagetrennte Liste an, z. B. `.WithLanguage("eng,spa")`. Die OCR‑Engine erkennt und transkribiert beide Sprachen. |
| **Nicht‑PDF‑Bilddateien** | Konvertieren Sie das Bild zuerst in ein PDF (`Aspose.Pdf`‑Bibliothek) oder verwenden Sie `OpenAIOcrOptions.WithImage`, um das Bild direkt zu senden. |
| **Rate‑Limit überschritten** | Implementieren Sie exponentielles Back‑off‑ und Wiederholungs‑Logik; die Aspose‑API gibt HTTP 429 zurück, wenn Sie das Kontingent überschreiten. |

### Profi‑Tipp

Cache Sie das Ergebnis `ocrText`, wenn Sie es später erneut verwenden möchten. Die OCR‑Operation ist der kostenintensivste Teil des Workflows, und das Wiederverwenden des Strings vermeidet doppelte API‑Aufrufe und spart Credits.

## Häufig gestellte Fragen

**Q: Funktioniert das mit passwortgeschützten PDFs?**  
A: Ja. Fügen Sie `.WithPassword("yourPassword")` zum Options‑Builder hinzu, bevor Sie den Copiloten erstellen.

**Q: Kann ich den Text in einem strukturierten Format (z. B. JSON mit Seitenzahlen) extrahieren?**  
A: Verwenden Sie `GetTextStructureAsync()` anstelle von `GetTextAsync()`. Die Methode liefert ein JSON‑Payload, das Seitenindizes, Begrenzungsrahmen und Vertrauenswerte enthält.

**Q: Was, wenn das PDF Tabellen enthält?**  
A: Die Klartext‑Extraktion flacht Tabellen zu zeilenumbruchsgetrennten Reihen ab. Für reichhaltigere Daten fordern Sie die PDF‑zu‑HTML‑Konvertierung (`GetHtmlAsync`) an und parsen die HTML‑Tabellenelemente.

## Fazit

Sie wissen jetzt **wie man Aspose verwendet**, um ein gescanntes PDF zu lesen, gescannten PDF‑Text zu extrahieren und **PDF zu Text zu konvertieren** mit einem minimalen C#‑Programm. Der Prozess besteht aus dem Erstellen eines OCR‑Copiloten, dem Aufruf von `GetTextAsync` und der Verarbeitung des resultierenden Strings. Durch Befolgen der Randfall‑Empfehlungen können Sie die Lösung auf große Dokumenten‑Batches, mehrsprachige Inhalte und gesicherte PDFs skalieren.

Als Nächstes könnten Sie erkunden:

* **Wie man Text** mit Layout‑Erhaltung extrahiert (`GetHtmlAsync`).
* Verwendung von Aspose.Pdf.AI zum **Extrahieren von Tabellen** und Exportieren in CSV.
* Integration der OCR‑Ausgabe mit Azure Cognitive Search für durchsuchbare Dokumentenarchive.

Viel Spaß beim Coden und genießen Sie die Genauigkeit, die Asposes KI‑gestützte OCR Ihren gescannten PDF‑Workflows verleiht!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Extract Text from PDF Files Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [How to Extract Text from Specific Regions in PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [How to Extract Highlighted Text from PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}