---
category: general
date: 2026-08-04
description: Jak použít Aspose k extrakci textu ze skenovaného PDF a převodu PDF na
  text pomocí C#. Naučte se číst skenované PDF soubory a získávat spolehlivé výsledky
  OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: cs
lastmod: 2026-08-04
og_description: Jak použít Aspose k načtení naskenovaných PDF souborů, extrakci textu
  z naskenovaného PDF a převodu PDF na text s kompletním, spustitelným příkladem.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Jak používat Aspose – extrahovat text ze skenovaných PDF v C#
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
title: Jak použít Aspose k extrahování textu ze skenovaného PDF – krok za krokem
url: /cs/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat Aspose k extrahování textu ze skenovaného PDF – krok za krokem průvodce

Pokud potřebujete **jak používat Aspose** pro OCR, tento průvodce vám ukáže, jak extrahovat text ze skenovaného PDF v několika řádcích C#. Ať už vytváříte službu pro archivaci dokumentů nebo vyhledávací index pro staré papírové dokumenty, řešení funguje s libovolným skenovaným PDF, které předáte službě Aspose.Pdf.AI.

V tomto tutoriálu:

* Vytvoříte OCR copilot, který načte skenované PDF.
* Asynchronně extrahujete rozpoznaný text.
* Zobrazíte nebo dále zpracujete extrahovaný řetězec.

Jedinou podmínkou je aktivní předplatné Aspose.Pdf.AI a vývojové prostředí .NET 6 (nebo novější).

## Požadavky

| Požadavek | Proč je důležité |
|-------------|----------------|
| .NET 6 SDK nebo novější | Poskytuje `async Main` a moderní jazykové funkce. |
| NuGet balíček Aspose.Pdf.AI (`Aspose.Pdf.AI`) | Obsahuje `AICopilotFactory` a OCR možnosti. |
| Platná instance Aspose.Pdf.AI `client` (API klíč) | Autentizuje vaše požadavky ke cloudové službě. |
| Skenovaný PDF soubor (např. `Scanned.pdf`) | Zdrojový dokument, ze kterého bude text extrahován. |

Nainstalujte balíček pomocí .NET CLI:

```bash
dotnet add package Aspose.Pdf.AI
```

## Krok 1: Nastavte klienta Aspose.Pdf.AI

Než budete moci volat jakýkoli OCR endpoint, musíte vytvořit klienta, který uchovává vaše API přihlašovací údaje. Klient je thread‑safe a může být znovu použit pro více dokumentů.

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

**Proč je tento krok vyžadován** – Služba Aspose ověřuje každý požadavek vůči vašemu předplatnému. Vytvoření klienta jednou zabraňuje opakovaným síťovým handshake a udržuje kód čistý.

## Krok 2: Vytvořte OCR copilot pro skenovaný PDF dokument

`AICopilotFactory` vytváří specializovaného OCR copilota, který umí zpracovat soubor, který specifikujete. Předáte `client` a objekt `OpenAIOcrOptions`, který ukazuje na cestu k PDF.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Vysvětlení** – `CreateOcrCopilot` zapouzdřuje všechny nízko‑úrovňové HTTP volání. Metoda `WithDocument` říká službě, který soubor analyzovat; můžete také předat `Stream`, pokud PDF existuje v paměti.

## Krok 3: Asynchronně extrahujte rozpoznaný text

Volání `GetTextAsync` spustí OCR operaci v cloudu a vrátí výsledek jako prostý text. Protože operace může trvat několik sekund, metoda je asynchronní.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Proč asynchronně?** – Síťová latence a doba zpracování OCR jsou nepředvídatelné. Použití `await` zabraňuje blokování hlavního vlákna aplikace, což je zvláště důležité pro UI nebo web‑service scénáře.

## Krok 4: Použijte extrahovaný text

V tomto okamžiku máte běžný .NET `string`, který obsahuje kompletní transkripci skenovaného PDF. Můžete jej zapsat do konzole, uložit do databáze nebo předat vyhledávači.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Očekávaný výstup

Pokud `Scanned.pdf` obsahuje jednu stránku se větou „Hello, world!“, konzole zobrazí:

```
=== OCR Result ===
Hello, world!
```

U dokumentů s více stránkami výstup spojí text každé stránky a zachová konce řádků.

## Kompletní spustitelný příklad

Níže je kompletní program, který můžete vložit do nového konzolového projektu (`dotnet new console`). Ukazuje **jak používat Aspose** od začátku do konce, včetně ošetření chyb pro běžné úskalí.

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

**Klíčové body v příkladu**

* `await` zajišťuje neblokující provádění.
* Blok `try/catch` odhaluje síťové nebo servisní chyby, což je zásadní při **čtení skenovaných PDF** souborů ve velkém měřítku.
* Nahraďte `YOUR_API_KEY` a `YOUR_DIRECTORY/Scanned.pdf` skutečnými hodnotami před spuštěním.

## Řešení okrajových případů a tipy pro nejlepší praxi

| Situace | Doporučený přístup |
|-----------|----------------------|
| **Velké PDF ( > 50 MB )** | Rozdělte dokument na menší části na straně klienta a zpracujte každou část samostatným copilotem. Tím snížíte zatížení paměti a zvýšíte spolehlivost. |
| **Nízká kvalita skenů** | Upravit kvalitu OCR přidáním `.WithLanguage("eng")` nebo `.WithEnhanceImage(true)` do `OpenAIOcrOptions`. Služba podporuje jazykové nápovědy, které zvyšují přesnost. |
| **Více jazyků** | Poskytněte čárkou oddělený seznam, např. `.WithLanguage("eng,spa")`. OCR engine rozpozná a přepíše oba jazyky. |
| **Obrázkové soubory, které nejsou PDF** | Nejprve převést obrázek na PDF (`Aspose.Pdf` knihovna) nebo použít `OpenAIOcrOptions.WithImage` k přímému odeslání obrázku. |
| **Překročen limit požadavků** | Implementujte exponenciální back‑off a logiku opakování; Aspose API vrací HTTP 429, když překročíte kvótu. |

### Pro tip

Uložte výsledek `ocrText` do cache, pokud jej plánujete později znovu použít. OCR operace je nejdražší částí pracovního postupu a opětovné použití řetězce eliminuje duplicitní API volání a šetří kredity.

## Často kladené otázky

**Q: Funguje to i s PDF chráněnými heslem?**  
A: Ano. Přidejte `.WithPassword("yourPassword")` do builderu možností před vytvořením copilota.

**Q: Můžu extrahovat text ve strukturovaném formátu (např. JSON s čísly stránek)?**  
A: Použijte `GetTextStructureAsync()` místo `GetTextAsync()`. Metoda vrací JSON payload, který obsahuje indexy stránek, ohraničující rámečky a skóre důvěry.

**Q: Co když PDF obsahuje tabulky?**  
A: Extrakce prostého textu převádí tabulky na řádky oddělené konci řádků. Pro bohatší data požádejte o konverzi PDF‑na‑HTML (`GetHtmlAsync`) a parsujte HTML elementy tabulek.

## Závěr

Nyní víte **jak používat Aspose** k načtení skenovaného PDF, extrahování textu ze skenovaného PDF a **převodu PDF na text** pomocí minimálního C# programu. Proces spočívá ve vytvoření OCR copilota, volání `GetTextAsync` a zpracování výsledného řetězce. Dodržením doporučení pro okrajové případy můžete řešení škálovat na velké dávky dokumentů, vícejazyčný obsah i zabezpečená PDF.

Dále můžete zkoumat:

* **Jak extrahovat text** s zachováním rozvržení (`GetHtmlAsync`).
* Použití Aspose.Pdf.AI k **extrakci tabulek** a jejich exportu do CSV.
* Integraci OCR výstupu s Azure Cognitive Search pro prohledávatelné archivní dokumenty.

Šťastné programování a užijte si přesnost, kterou AI‑poháněné OCR od Aspose přináší do vašich pracovních toků se skenovanými PDF!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extrahovat text ze souborů PDF pomocí Aspose.PDF pro .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [Jak extrahovat text z konkrétních oblastí v PDF pomocí Aspose.PDF pro .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [Jak extrahovat zvýrazněný text z PDF pomocí Aspose.PDF pro .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}