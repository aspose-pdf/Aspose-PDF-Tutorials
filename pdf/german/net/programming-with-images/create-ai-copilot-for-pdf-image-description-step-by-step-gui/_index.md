---
category: general
date: 2026-08-04
description: Erstelle einen KI‑Copilot, um Bildbeschreibungen für PDF‑Dateien zu generieren.
  Erfahre, wie du OpenAI‑Bildoptionen konfigurierst und Bildbeschreibungen effizient
  extrahierst.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: de
lastmod: 2026-08-04
og_description: Erstelle einen KI‑Copilot, um Bildbeschreibungen für PDF‑Dateien zu
  generieren. Dieses Tutorial zeigt, wie man OpenAI‑Bildoptionen konfiguriert, den
  Copilot ausführt und Bildbeschreibungen in C# extrahiert.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: KI-Copilot für PDF-Bildbeschreibung erstellen – vollständige Anleitung
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: KI-Copilot für PDF‑Bildbeschreibung erstellen – Schritt‑für‑Schritt‑Anleitung
url: /de/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# KI‑Copilot für PDF‑Bildbeschreibungen erstellen – vollständige Anleitung

Wenn Sie **einen KI‑Copilot erstellen** möchten, der automatisch Beschreibungen für in einem PDF eingebettete Bilder schreibt, zeigt Ihnen diese Anleitung genau, wie das geht. Sie lernen, die OpenAI‑Bildoptionen zu konfigurieren, den Copilot auszuführen und **Bildbeschreibungen zu extrahieren**, ohne Ihr C#‑Projekt zu verlassen.

Die Generierung von Textinhalten für PDF‑Bilder ist ein häufiges Anliegen für Barrierefreiheit, Inhaltsindizierung und automatisierte Berichterstellung. Am Ende dieses Tutorials besitzen Sie eine wiederverwendbare Komponente, die **Bildbeschreibungen generiert** für jedes PDF‑Dokument, das Sie ihr übergeben.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 oder neuer installiert  
* Eine Aspose.Pdf.AI‑Lizenz (oder eine kostenlose Testversion)  
* Einen OpenAI‑API‑Schlüssel, den der Aspose‑Client verwenden kann  
* Visual Studio 2022 (oder eine beliebige IDE, die C# unterstützt)  

Keine zusätzlichen NuGet‑Pakete sind über `Aspose.Pdf.AI` hinaus erforderlich.

## Schritt 1: Aspose.Pdf.AI‑Client einrichten

Der erste Schritt besteht darin, den KI‑Client mit Ihren Authentifizierungsdaten zu instanziieren. Der Client übernimmt die Kommunikation mit dem OpenAI‑Dienst im Hintergrund.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Warum das wichtig ist:** Der `AiClient` kapselt alle anfragebezogenen Einstellungen (API‑Schlüssel, Timeout, Retry‑Policy). Durch einmaliges Erstellen und Wiederverwenden in mehreren Copilot‑Instanzen reduzieren Sie den Overhead und gewährleisten eine konsistente Authentifizierung.

## Schritt 2: Einen Bildbeschreibungs‑Copilot erstellen

Jetzt erstellen Sie den **KI‑Copilot**, der das PDF liest und für jedes Bild eine Beschreibung erzeugt. Die Fabrik‑Methode `CreateImageDescriptionCopilot` akzeptiert den Client und eine Reihe von Optionen, die festlegen, wie die Beschreibung generiert wird.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Warum das wichtig ist:**  
* `OpenAIImageDescriptionOptions` (die **OpenAI‑Bildoptionen**) ermöglichen das Feintuning des Sprachmodells. Das Anpassen von Temperatur oder Modell kann die Relevanz für technische Diagramme gegenüber natürlichen Fotos verbessern.  
* Die Angabe des Dokumentpfads teilt dem Copilot mit, welches PDF gescannt werden soll. Der Copilot extrahiert jedes Raster‑Bild, sendet es an das Modell und gibt eine menschenlesbare Beschreibung zurück.

## Schritt 3: Die erzeugte Beschreibung asynchron abrufen

Der Copilot arbeitet asynchron, weil er möglicherweise mehrere Megabyte Bilddaten hochladen und auf die Modellantwort warten muss. Verwenden Sie `await`, um sicherzustellen, dass der Aufruf abgeschlossen ist, bevor Sie das Ergebnis verwenden.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Warum das wichtig ist:** Die Methode liefert ein `Dictionary<int, string>`, das jede Seite (oder Bild‑Index) ihrer Beschreibung zuordnet. Das Abfangen von `AiException` ermöglicht es Ihnen, Netzwerk‑ oder Kontingent‑Fehler anzuzeigen, anstatt die Anwendung abstürzen zu lassen.

## Schritt 4: Die Beschreibung anzeigen oder speichern

Sie können die Beschreibungen in die Konsole, in eine Log‑Datei schreiben oder sie wieder in das PDF als Alt‑Text für Barrierefreiheit einbetten. Nachfolgend ein kurzes Beispiel, das die Ausgabe in eine JSON‑Datei für die spätere Verwendung schreibt.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Warum das wichtig ist:** Das Speichern der Ausgabe als JSON bewahrt die Zuordnung zwischen jeder Seite und ihrer Beschreibung, sodass nachgelagerte Prozesse (Suchindizierung, UI‑Rendering usw.) die Daten leicht konsumieren können.

## Mehrere Bilder pro Seite verarbeiten

Enthält eine Seite mehrere Bilder, liefert der Copilot eine zusammengefügte Beschreibung, getrennt durch Zeilenumbrüche. Um sie zu splitten, prüfen Sie das Roh‑Ergebnis und teilen Sie bei `\n\n` (doppelter Zeilenumbruch). Hier eine Hilfsmethode:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Anschließend können Sie über jede einzelne Bildbeschreibung iterieren und sie bei Bedarf separat speichern.

## Sonderfall: Große PDFs und Timeout‑Verwaltung

Die Verarbeitung eines PDFs, das größer als 100 MB ist, kann die Standard‑HTTP‑Timeouts überschreiten. Passen Sie die Timeout‑Einstellung des Clients an, wenn Sie den `AiClient` erstellen:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Ein erhöhter Timeout verhindert ein vorzeitiges Abbrechen, während der Dienst viele hochauflösende Bilder verarbeitet.

## Profi‑Tipp: Ergebnisse cachen, um Kosten zu senken

OpenAI berechnet pro Token, und Bildbeschreibungen können bei mehreren Versionen desselben Berichts wiederholt auftreten. Cachen Sie die JSON‑Ausgabe und verwenden Sie sie erneut, wenn der PDF‑Hash mit einer bereits verarbeiteten Datei übereinstimmt. Diese Praxis spart Geld und beschleunigt nachfolgende Durchläufe.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Speichern Sie den Hash zusammen mit der JSON‑Datei; stimmt der Hash bei einem späteren Lauf, überspringen Sie den KI‑Aufruf.

## Vollständiges, ausführbares Beispiel

Alles zusammengeführt, hier eine eigenständige Konsolenanwendung, die Sie in ein neues .NET‑Projekt einfügen können.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Erwartete Ausgabe (gekürzt)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Das Programm liest `AnnualReport.pdf`, erstellt einen **KI‑Copilot** und schreibt eine JSON‑Datei, die jede Seite ihrer erzeugten Beschreibung zuordnet.

## Häufige Fragen

* **Funktioniert das mit verschlüsselten PDFs?**  
  Ja, Sie müssen das Passwort beim Erstellen des Copilots angeben:  
  `imageOptions.WithPassword("mySecret")`.

* **Kann ich die Verarbeitung auf bestimmte Seiten beschränken?**  
  Verwenden Sie `imageOptions.WithPageRange(1, 10)`, um den Copilot auf die Seiten 1‑10 zu begrenzen.

* **Was, wenn ein Bild Text enthält?**  
  Das Modell versucht, visuellen Inhalt zu beschreiben; für OCR‑artige Textextraktion sollten Sie stattdessen `CreateTextExtractionCopilot` verwenden.

## Fazit

Sie wissen jetzt, wie Sie **einen KI‑Copilot erstellen**, der **Bildbeschreibungen generiert** für PDF‑Dateien, **OpenAI‑Bildoptionen konfigurieren** und **Bildbeschreibungen** programmgesteuert in C# **extrahieren**. Das vollständige Beispiel demonstriert Best Practices wie asynchrone Verarbeitung, Fehlermanagement und Ergebnis‑Caching.

Als Nächstes könnten Sie:

* Die generierten Beschreibungen wieder in das PDF als Alt‑Text einbetten, um die Barrierefreiheit zu verbessern (`PdfDocument` → `PdfImage.AlternativeText`).  
* Das gleiche Copilot‑Muster nutzen, um **Bildbeschreibungs‑PDF‑Berichte** für die Batch‑Verarbeitung zu **generieren**.  
* Mit verschiedenen OpenAI‑Modellen oder Temperatureinstellungen experimentieren, um den Beschreibungsstil fein abzustimmen.

Passen Sie den Code gern an, testen Sie größere Dokumente und integrieren Sie die Ausgabe in Ihre Indexierungs‑Pipeline. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}