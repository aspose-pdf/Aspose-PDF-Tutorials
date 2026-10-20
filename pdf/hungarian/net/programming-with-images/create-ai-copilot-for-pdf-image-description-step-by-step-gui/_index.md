---
category: general
date: 2026-08-04
description: Készíts AI Copilotot, amely képleírást generál PDF-fájlokhoz. Tanulja
  meg, hogyan konfigurálja az OpenAI képi beállításait, és hatékonyan nyerje ki a
  képleírást.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: hu
lastmod: 2026-08-04
og_description: Készíts AI Copilotot, amely képleírást generál PDF-fájlokhoz. Ez az
  útmutató megmutatja, hogyan konfigurálhatod az OpenAI képi beállításait, futtathatod
  a copilotot, és hogyan nyerheted ki a képleírást C#-ban.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: AI Copilot létrehozása PDF képleíráshoz – teljes útmutató
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
title: AI Copilot létrehozása PDF képleíráshoz – lépésről lépésre útmutató
url: /hu/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# AI Copilot létrehozása PDF képleíráshoz – teljes útmutató

Ha **AI Copilot**-ot szeretnél létrehozni, amely automatikusan leírásokat ír a PDF-be beágyazott képekhez, ez az útmutató pontosan megmutatja, hogyan kell ezt megtenni. Megtanulod beállítani az OpenAI képopciókat, futtatni a copilotot, és **képleírást kinyerni** anélkül, hogy elhagynád a C# projektedet.

Szöveges tartalom generálása PDF képekhez gyakori igény a hozzáférhetőség, a tartalom indexelése és az automatizált jelentéskészítés terén. A tutorial végére egy újrahasználható komponenst kapsz, amely **képleírást generál** bármely PDF dokumentumhoz, amelyre rámutatsz.

## Előfeltételek

* .NET 6.0 vagy újabb telepítve  
* Aspose.Pdf.AI licenc (vagy ingyenes próba)  
* OpenAI API kulcs, amelyet az Aspose kliens használhat  
* Visual Studio 2022 (vagy bármely C#-ot támogató IDE)  

A `Aspose.Pdf.AI`-n kívül nincs szükség további NuGet csomagokra.

## 1. lépés: Az Aspose.Pdf.AI kliens beállítása

Az első lépés az AI kliens példányosítása a hitelesítési adataiddal. A kliens a háttérben kezeli a kommunikációt az OpenAI szolgáltatással.

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

**Miért fontos:** A `AiClient` tartalmazza az összes kérés‑szintű beállítást (API kulcs, időkorlát, újrapróbálkozási szabály). Egyszer létrehozni és több copilot példányban újrahasználni csökkenti a terhelést és biztosítja a konzisztens hitelesítést.

## 2. lépés: Képleírás Copilot létrehozása

Most létrehozod a **AI copilot**-ot, amely beolvassa a PDF-et és leírást készít minden egyes képhez. A `CreateImageDescriptionCopilot` gyári metódus elfogadja a klienst és egy opciók halmazt, amely meghatározza, hogyan generálódik a leírás.

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

**Miért fontos:**  
* `OpenAIImageDescriptionOptions` (az **OpenAI képopciók**) lehetővé teszik a nyelvi modell finomhangolását. A hőmérséklet vagy a modell módosítása javíthatja a relevanciát technikai diagramok és természetes fényképek esetén.  
* A dokumentum útvonalának megadása megmondja a copilotnak, melyik PDF-et kell átvizsgálnia. A copilot kinyeri az összes raszter képet, elküldi a modellnek, és egy ember által olvasható leírást ad vissza.

## 3. lépés: A generált leírás aszinkron lekérése

A copilot aszinkron módon működik, mivel előfordulhat, hogy több megabájt képadatot kell feltölteni és a modell válaszára várni. Használd a `await`-et, hogy biztosítsd a hívás befejeződését, mielőtt hozzáférnél az eredményhez.

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

**Miért fontos:** A metódus egy `Dictionary<int, string>`-et ad vissza, amely minden oldalhoz (vagy kép indexhez) a leírást rendeli. Az `AiException` kezelése lehetővé teszi a hálózati vagy kvóta hibák megjelenítését ahelyett, hogy az alkalmazás összeomlana.

## 4. lépés: A leírás megjelenítése vagy tárolása

A leírásokat kiírhatod a konzolra, egy naplófájlba, vagy visszaágyazhatod a PDF-be alt‑szövegként a hozzáférhetőség érdekében. Az alábbi gyors példa a kimenetet egy JSON fájlba írja későbbi felhasználásra.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Miért fontos:** A kimenet JSON formátumban való tárolása megőrzi az egyes oldalak és leírásaik közötti kapcsolatot, így egyszerűvé teszi a downstream folyamatok (kereső indexelés, UI megjelenítés stb.) számára az adatok felhasználását.

## Több kép kezelése oldalanként

Ha egy oldal több képet tartalmaz, a copilot egy összefűzött leírást ad vissza, sorvégekkel elválasztva. A szétválasztáshoz vizsgáld meg a nyers eredményt, és oszd fel a `\n\n` (dupla újsor) alapján. Íme egy segédmetódus:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Ezután végigiterálhatsz az egyes képleírásokon, és szükség esetén külön tárolhatod őket.

## Szélsőséges eset: Nagy PDF-ek és időkorlát kezelése

Egy 100 MB-nál nagyobb PDF feldolgozása meghaladhatja az alapértelmezett HTTP időkorlátokat. Állítsd be a kliens időkorlátát, amikor létrehozod a `AiClient`-et:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Az időkorlát növelése megakadályozza a korai leállást, amíg a szolgáltatás sok nagy felbontású képet dolgoz fel.

## Profi tipp: Az eredmények gyorsítótárazása a költségek csökkentése érdekében

Az OpenAI tokenenként számláz, és a képleírások ismétlődhetnek ugyanazon jelentés különböző verzióiban. Tárold a JSON kimenetet gyorsítótárban, és használd újra, ha a PDF hash-e megegyezik egy korábban feldolgozott fájllal. Ez a gyakorlat pénzt takarít meg és felgyorsítja a későbbi futásokat.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Tárold a hash-t a JSON fájl mellett; ha egy későbbi futásnál a hash egyezik, hagyd ki az AI hívást.

## Teljes futtatható példa

Mindent összevonva, itt egy önálló konzolalkalmazás, amelyet beilleszthetsz egy új .NET projektbe.

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

**Várható kimenet (rövidítve)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

A program beolvassa az `AnnualReport.pdf`-t, létrehoz egy **AI copilot**-ot, és egy JSON fájlt ír, amely minden oldalt a generált leírásához rendeli.

## Gyakori kérdések

* **Működik titkosított PDF-ekkel?**  
  Igen, de a copilot létrehozásakor meg kell adnod a jelszót:  
  `imageOptions.WithPassword("mySecret")`.

* **Korlátozhatom a feldolgozást bizonyos oldalakra?**  
  Használd a `imageOptions.WithPageRange(1, 10)`-t, hogy a copilotot az 1‑10. oldalakra korlátozd.

* **Mi van, ha egy kép szöveget tartalmaz?**  
  A modell megpróbálja leírni a vizuális tartalmat; OCR‑szerű szövegkinyeréshez inkább a `CreateTextExtractionCopilot`-ot kell használnod.

## Következtetés

Most már tudod, hogyan **hozz létre AI Copilot**-ot, amely **képleírást generál** PDF fájlokhoz, hogyan konfiguráld az **OpenAI képopciókat**, és hogyan **nyerj ki képleírást** programozottan C#-ban. A teljes példa bemutatja a legjobb gyakorlatokat, mint az aszinkron kezelés, a hibakezelés és az eredmények gyorsítótárazása.

Ezután érdemes lehet:

* A generált leírások visszaágyazása a PDF-be alt‑szövegként a jobb hozzáférhetőség érdekében (`PdfDocument` → `PdfImage.AlternativeText`).  
* Ugyanazon copilot mintájának használata **képleírás PDF** jelentések generálásához kötegelt feldolgozásban.  
* Kísérletezés különböző OpenAI modellekkel vagy hőmérséklet beállításokkal a leírás stílusának finomhangolásához.

Nyugodtan módosítsd a kódot, kísérletezz nagyobb dokumentumokkal, és integráld a kimenetet az indexelési folyamatodba. Boldog kódolást!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [PDF létrehozása címkézett képpel Java-ban](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [PDF létrehozása címkézett képpel](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Címkézett PDF kép létrehozása .NET-ben](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}