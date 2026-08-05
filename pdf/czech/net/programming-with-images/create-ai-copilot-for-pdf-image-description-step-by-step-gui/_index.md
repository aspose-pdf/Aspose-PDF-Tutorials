---
category: general
date: 2026-08-04
description: Vytvořte AI Copilot pro generování popisu obrázku v PDF souborech. Naučte
  se, jak nastavit možnosti obrázků OpenAI a efektivně extrahovat popis obrázku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: cs
lastmod: 2026-08-04
og_description: Vytvořte AI Copilot pro generování popisu obrázků v PDF souborech.
  Tento tutoriál vám ukáže, jak nastavit možnosti obrázků OpenAI, spustit copilot
  a extrahovat popis obrázků v C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Vytvořte AI Copilot pro popis obrázků v PDF – kompletní průvodce
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
title: Vytvořte AI copilot pro popis obrázků v PDF – krok za krokem průvodce
url: /cs/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte AI Copilot pro popis obrázků v PDF – kompletní průvodce

Pokud potřebujete **vytvořit AI Copilot**, který automaticky generuje popisy pro obrázky vložené v PDF, tento průvodce vám přesně ukáže, jak na to. Naučíte se nakonfigurovat OpenAI image options, spustit copilot a **extrahovat popis obrázku** aniž byste opustili svůj C# projekt.

Generování textového obsahu pro obrázky v PDF je běžnou potřebou pro přístupnost, indexaci obsahu a automatické reportování. Na konci tohoto tutoriálu budete mít znovupoužitelnou komponentu, která **generuje popis obrázku** pro libovolný PDF dokument, na který ji nasměříte.

## Požadavky

* .NET 6.0 nebo novější nainstalovaný  
* Licence Aspose.Pdf.AI (nebo bezplatná zkušební verze)  
* API klíč OpenAI, který může použít klient Aspose  
* Visual Studio 2022 (nebo jakékoli IDE podporující C#)  

Kromě `Aspose.Pdf.AI` nejsou vyžadovány žádné další NuGet balíčky.

## Krok 1: Nastavte klienta Aspose.Pdf.AI

Prvním krokem je vytvořit instanci AI klienta s vašimi autentizačními údaji. Klient zajišťuje komunikaci se službou OpenAI na pozadí.

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

**Proč je to důležité:** `AiClient` zapouzdřuje všechna nastavení na úrovni požadavku (API klíč, časový limit, politika opakování). Vytvoření jedné instance a její opakované používání napříč více copiloty snižuje režii a zajišťuje konzistentní autentizaci.

## Krok 2: Vytvořte copilot pro popis obrázku

Nyní vytvoříte **AI copilot**, který načte PDF a vygeneruje popis pro každý obrázek. Tovární metoda `CreateImageDescriptionCopilot` přijímá klienta a sadu možností, které definují, jak je popis generován.

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

**Proč je to důležité:**  
* `OpenAIImageDescriptionOptions` (tj. **OpenAI image options**) vám umožňují jemně ladit jazykový model. Úprava teploty nebo modelu může zlepšit relevanci pro technické diagramy oproti přirozeným fotografiím.  
* Zadání cesty k dokumentu říká copilotovi, který PDF má skenovat. Copilot extrahuje každý rastrový obrázek, odešle jej modelu a vrátí čitelný popis.

## Krok 3: Asynchronně načtěte vygenerovaný popis

Copilot pracuje asynchronně, protože může potřebovat nahrát několik megabajtů obrazových dat a čekat na odpověď modelu. Použijte `await`, aby byl volání dokončeno, než přistoupíte k výsledku.

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

**Proč je to důležité:** Metoda vrací `Dictionary<int, string>`, který mapuje každou stránku (nebo index obrázku) na jeho popis. Ošetření `AiException` vám umožní zobrazit chyby sítě nebo kvóty místo zhroucení aplikace.

## Krok 4: Zobrazte nebo uložte popis

Popisy můžete zapsat do konzole, logovacího souboru nebo je vložit zpět do PDF jako alt‑text pro přístupnost. Níže je rychlý příklad, který zapisuje výstup do JSON souboru pro pozdější využití.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Proč je to důležité:** Uložení výstupu jako JSON zachovává vazbu mezi každou stránkou a jejím popisem, což usnadňuje spotřebu dat následnými procesy (indexování vyhledávání, vykreslování UI atd.).

## Zpracování více obrázků na stránce

Pokud stránka obsahuje několik obrázků, copilot vrátí spojený popis oddělený konci řádků. Pro jejich rozdělení prohlédněte surový výsledek a rozdělte jej podle `\n\n` (dvojitý nový řádek). Zde je pomocná metoda:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Poté můžete iterovat přes každý jednotlivý popis obrázku a případně je uložit samostatně.

## Okrajový případ: Velké PDF a správa časových limitů

Zpracování PDF většího než 100 MB může překročit výchozí HTTP časové limity. Upravte nastavení časového limitu klienta při vytváření `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Zvýšení časového limitu zabraňuje předčasnému ukončení, zatímco služba zpracovává mnoho vysoce rozlišených obrázků.

## Profesionální tip: Cache výsledků ke snížení nákladů

OpenAI účtuje za token a popis obrázku může být opakující se napříč verzemi stejné zprávy. Uložte JSON výstup do cache a znovu jej použijte, když hash PDF odpovídá dříve zpracovanému souboru. Tato praxe šetří peníze a urychluje následné běhy.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Uložte hash spolu s JSON souborem; pokud se hash při pozdějším běhu shoduje, přeskočte volání AI.

## Kompletní spustitelný příklad

Spojením všech částí získáte samostatnou konzolovou aplikaci, kterou můžete vložit do nového .NET projektu.

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

**Očekávaný výstup (zkrácený)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Program načte `AnnualReport.pdf`, vytvoří **AI copilot** a zapíše JSON soubor, který mapuje každou stránku na její vygenerovaný popis.

## Často kladené otázky

* **Funguje to s šifrovanými PDF?**  
  Ano, ale musíte při vytváření copilotu zadat heslo:  
  `imageOptions.WithPassword("mySecret")`.

* **Mohu omezit zpracování na konkrétní stránky?**  
  Použijte `imageOptions.WithPageRange(1, 10)` k omezení copilotu na stránky 1‑10.

* **Co když obrázek obsahuje text?**  
  Model se snaží popsat vizuální obsah; pro extrakci textu ve stylu OCR byste měli místo toho použít `CreateTextExtractionCopilot`.

## Závěr

Nyní víte, jak **vytvořit AI Copilot**, který **generuje popis obrázku** pro PDF soubory, nakonfigurovat **OpenAI image options** a **extrahovat popis obrázku** programově v C#. Kompletní příklad ukazuje osvědčené postupy, jako je asynchronní zpracování, správa chyb a cache výsledků.

Dále můžete zkoumat:

* Přidání vygenerovaných popisů zpět do PDF jako alt‑text pro zlepšenou přístupnost (`PdfDocument` → `PdfImage.AlternativeText`).  
* Použití stejného copilot vzoru k **generování PDF zpráv s popisem obrázků** pro dávkové zpracování.  
* Experimentování s různými OpenAI modely nebo nastavením teploty pro jemné ladění stylu popisu.

Neváhejte upravit kód, experimentovat s většími dokumenty a integrovat výstup do vašeho indexovacího pipeline. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}