---
category: general
date: 2026-08-04
description: Skapa AI Copilot för att generera bildbeskrivningar för PDF-filer. Lär
  dig hur du konfigurerar OpenAI:s bildalternativ och extraherar bildbeskrivningar
  effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: sv
lastmod: 2026-08-04
og_description: Skapa en AI‑copilot för att generera bildbeskrivningar för PDF‑filer.
  Denna handledning visar hur du konfigurerar OpenAI:s bildalternativ, kör copilot‑programmet
  och extraherar bildbeskrivningar i C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Skapa AI Copilot för PDF-bildbeskrivning – komplett guide
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
title: Skapa AI‑copilot för PDF‑bildbeskrivning – steg‑för‑steg‑guide
url: /sv/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa AI Copilot för PDF‑bildbeskrivning – komplett guide

Om du behöver **create AI Copilot** som automatiskt skriver beskrivningar för bilder som är inbäddade i en PDF, visar den här guiden exakt hur du gör det. Du kommer att lära dig att konfigurera OpenAI image options, köra copilot och **extract image description** utan att lämna ditt C#‑projekt.

Att generera textinnehåll för PDF‑bilder är ett vanligt krav för tillgänglighet, innehållsindexering och automatiserad rapportering. I slutet av den här handledningen kommer du att ha en återanvändbar komponent som **generates image description** för vilket PDF‑dokument du än pekar på.

## Förutsättningar

* .NET 6.0 eller senare installerat  
* En Aspose.Pdf.AI‑licens (eller en gratis provperiod)  
* En OpenAI API‑nyckel som Aspose‑klienten kan använda  
* Visual Studio 2022 (eller någon IDE som stödjer C#)  

Inga ytterligare NuGet‑paket krävs utöver `Aspose.Pdf.AI`.

## Steg 1: Konfigurera Aspose.Pdf.AI‑klienten

Det första steget är att instansiera AI‑klienten med dina autentiseringsuppgifter. Klienten hanterar kommunikationen med OpenAI‑tjänsten i bakgrunden.

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

**Varför detta är viktigt:** `AiClient` kapslar in alla begäransnivåinställningar (API‑nyckel, timeout, återförsökspolicy). Att skapa den en gång och återanvända den över flera copilot‑instanser minskar overhead och säkerställer konsekvent autentisering.

## Steg 2: Skapa en Image Description Copilot

Nu skapar du **AI copilot** som kommer att läsa PDF‑filen och producera en beskrivning för varje bild. Fabriksmetoden `CreateImageDescriptionCopilot` accepterar klienten och en uppsättning alternativ som definierar hur beskrivningen genereras.

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

**Varför detta är viktigt:**  
* `OpenAIImageDescriptionOptions` (de **OpenAI image options**) låter dig finjustera språkmodellen. Justering av temperatur eller modell kan förbättra relevansen för tekniska diagram jämfört med naturliga foton.  
* Att ange dokumentets sökväg talar om för copilot vilken PDF som ska skannas. Copilot extraherar varje rasterbild, skickar den till modellen och returnerar en mänskligt läsbar beskrivning.

## Steg 3: Hämta den genererade beskrivningen asynkront

Copilot arbetar asynkront eftersom den kan behöva ladda upp flera megabyte bilddata och vänta på modellens svar. Använd `await` för att säkerställa att anropet slutförs innan du får åtkomst till resultatet.

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

**Varför detta är viktigt:** Metoden returnerar en `Dictionary<int, string>` som mappar varje sida (eller bildindex) till dess beskrivning. Att hantera `AiException` låter dig visa nätverks‑ eller kvotfel istället för att krascha applikationen.

## Steg 4: Visa eller lagra beskrivningen

Du kan skriva beskrivningarna till konsolen, en loggfil eller bädda in dem tillbaka i PDF‑filen som alt‑text för tillgänglighet. Nedan är ett snabbt exempel som skriver utdata till en JSON‑fil för senare konsumtion.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Varför detta är viktigt:** Att lagra utdata som JSON bevarar kopplingen mellan varje sida och dess beskrivning, vilket gör det enkelt för efterföljande processer (sökindexering, UI‑rendering osv.) att konsumera datan.

## Hantera flera bilder per sida

Om en sida innehåller flera bilder returnerar copilot en sammansatt beskrivning separerad med radbrytningar. För att dela upp dem, inspektera det råa resultatet och dela på `\n\n` (dubbel ny rad). Här är en hjälpfunktion:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Du kan sedan iterera över varje individuell bildbeskrivning och lagra dem separat om så behövs.

## Edge case: Stora PDF‑filer och timeout‑hantering

Att bearbeta en PDF större än 100 MB kan överskrida standard‑HTTP‑timeouts. Justera klientens timeout‑inställning när du skapar `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Att öka timeouten förhindrar för tidig avslutning medan tjänsten bearbetar många högupplösta bilder.

## Proffstips: Cacha resultat för att minska kostnad

OpenAI debiterar per token, och bildbeskrivningar kan vara repetitiva över versioner av samma rapport. Cacha JSON‑utdata och återanvänd den när PDF‑hashen matchar en tidigare bearbetad fil. Denna praxis sparar pengar och snabbar upp efterföljande körningar.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Lagra hashvärdet tillsammans med JSON‑filen; om hashvärdet matchar vid ett senare körning, hoppa över AI‑anropet.

## Fullt körbart exempel

När allt sätts ihop, här är ett fristående konsolprogram som du kan klistra in i ett nytt .NET‑projekt.

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

**Förväntad utdata (trunkerad)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Programmet läser `AnnualReport.pdf`, skapar en **AI copilot** och skriver en JSON‑fil som mappar varje sida till dess genererade beskrivning.

## Vanliga frågor

* **Fungerar detta med krypterade PDF‑filer?**  
  Ja, men du måste ange lösenordet när du skapar copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Kan jag begränsa bearbetning till specifika sidor?**  
  Använd `imageOptions.WithPageRange(1, 10)` för att begränsa copilot till sidor 1‑10.

* **Vad händer om en bild innehåller text?**  
  Modellen försöker beskriva visuellt innehåll; för OCR‑liknande textutvinning bör du istället använda `CreateTextExtractionCopilot`.

## Slutsats

Du vet nu hur du **create AI Copilot** som **generates image description** för PDF‑filer, konfigurerar **OpenAI image options** och **extract image description** programatiskt i C#. Det kompletta exemplet visar bästa praxis såsom asynkron hantering, felhantering och cachning av resultat.

Nästa steg kan vara att utforska:

* Att lägga till de genererade beskrivningarna tillbaka i PDF‑filen som alt‑text för förbättrad tillgänglighet (`PdfDocument` → `PdfImage.AlternativeText`).  
* Att använda samma copilot‑mönster för att **generate image description PDF**‑rapporter för batch‑bearbetning.  
* Att experimentera med olika OpenAI‑modeller eller temperaturinställningar för att finjustera beskrivningsstilen.

Känn dig fri att anpassa koden, experimentera med större dokument och integrera utdata i din indexeringspipeline. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa PDF med taggad bild i Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Skapa PDF med taggad bild](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Skapa taggad PDF‑bild i .NET](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}