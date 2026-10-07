---
category: general
date: 2026-10-07
description: Naučte se, jak přidat Batesovo číslování do PDF pomocí C#. Tento krok‑za‑krokem
  průvodce také pokrývá číslování stránek PDF a další triky s číslováním.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: cs
lastmod: 2026-10-07
og_description: Rychle přidejte Batesovo číslování do PDF. Sledujte tento tutoriál,
  abyste zvládli číslování stránek PDF, číslovali stránky PDF a automatizovali sledování
  dokumentů.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Přidejte Batesovo číslování do PDF v C# – kompletní průvodce Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Jak přidat Batesovo číslování do PDF pomocí Aspose.Pdf
url: /cs/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat Batesovo číslování do PDF pomocí Aspose.Pdf

Pokud potřebujete **přidat Batesovo číslování** do PDF, tento návod vám přesně ukáže, jak to provést v C#. Ať už připravujete právní svazky, spravujete spisové složky, nebo jen chcete spolehlivé **pdf číslování stránek**, níže uvedené kroky vám poskytnou kompletní, spustitelný řešení.

V tomto tutoriálu se naučíte:

* Načíst existující PDF soubor.
* Nakonfigurovat možnosti Batesova číslování jako předpona, počáteční číslo, doplnění číslic, oddělovač a přípona.
* Aplikovat číslování na každou stránku.
* Uložit aktualizovaný dokument.

Nejsou vyžadovány žádné externí nástroje kromě knihovny Aspose.Pdf pro .NET a kód funguje s .NET 6+ i s .NET Framework 4.7.2+.  

---

## Předpoklady

Než začnete, ujistěte se, že máte:

| Požadavek | Proč je důležité |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet balíček `Aspose.Pdf`) | Poskytuje třídy `Document` a `BatesNumberingOptions` používané v kódu. |
| **.NET SDK** (doporučeno 6.0 nebo novější) | Umožňuje kompilovat a spouštět C# konzolovou aplikaci. |
| **Zdrojové PDF**, které chcete očíslovat | V tutoriálu je použito `source.pdf` jako příklad; nahraďte cestu vlastním souborem. |
| **Oprávnění k zápisu** do výstupní složky | Volání `Save` potřebuje zapsat nový soubor. |

Knihovnu můžete nainstalovat pomocí následujícího CLI příkazu:

```bash
dotnet add package Aspose.Pdf
```

---

## Krok 1: Vytvořte nový konzolový projekt

Otevřete terminál a spusťte:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Tím vytvoříte minimální C# projekt, který naplníme kódem potřebným k **přidání Batesova číslování**.

---

## Krok 2: Přidejte požadované `using` direktivy

Otevřete `Program.cs` a přidejte jmenné prostory na začátek souboru:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` vám poskytuje přístup ke třídě `Document` pro načítání a ukládání PDF.  
* `Aspose.Pdf.Text` obsahuje `BatesNumberingOptions`, objekt definující vzhled čísel.

---

## Krok 3: Načtěte zdrojové PDF

První akční řádek načte PDF, které chcete očíslovat. Nahraďte `"YOUR_DIRECTORY/source.pdf"` skutečnou cestou k vašemu souboru.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Pokud soubor nelze najít, Aspose vyhodí `FileNotFoundException`. Abyste tomu předešli, můžete předem ověřit cestu:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Krok 4: Definujte možnosti Batesova číslování

`BatesNumberingOptions` vám umožňuje řídit každý vizuální prvek číslování. Níže uvedený příklad ukazuje typickou konfiguraci pro právní spisové soubory:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Proč je každá vlastnost důležitá**

| Vlastnost | Účel |
|----------|------|
| `Prefix` | Pomáhá seskupovat dokumenty podle projektu, klienta nebo případu. |
| `StartNumber` | Nastavuje počáteční čítač; užitečné, když již máte existující očíslované soubory. |
| `Digits` | Zajišťuje jednotnou šířku, usnadňuje řazení. |
| `Separator` | Zlepšuje čitelnost, zejména při kombinaci předpony a přípony. |
| `Suffix` | Umožňuje přidat rok, verzi nebo jakýkoli koncový identifikátor. |

Můžete také ovládat umístění (nahoře, dole, vlevo, vpravo) a styl písma pomocí `batesOptions.Position` a `batesOptions.Font`. Pro většinu scénářů fungují výchozí hodnoty (dolní‑pravý roh, 12‑pt Times New Roman) dobře.

---

## Krok 5: Aplikujte číslování na každou stránku

Volání `pdf.BatesNumbering.Add` vloží čísla na každou stránku v pořadí, v jakém se objevují.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Pokud potřebujete **číslovat pdf stránky** jen na podmnožině (např. přeskočit titulní stránku), můžete místo toho předat `PageCollection`:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Krok 6: Uložte aktualizované PDF

Nakonec zapište upravený dokument na disk. Název souboru obvykle odráží, že PDF nyní obsahuje Batesova čísla.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Pokud výstupní složka neexistuje, Aspose ji vytvoří automaticky. Přesto byste měli zajistit, že máte oprávnění k zápisu, aby nedošlo k `UnauthorizedAccessException`.

---

## Kompletní, spustitelný příklad

Sestavením všech částí získáte kompletní program, který můžete zkopírovat, vložit a spustit:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Očekávaný výstup** (konzole):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Otevřete `bates_numbered.pdf` a uvidíte, že každá stránka je označena například `CASE-001000-2025`, `CASE-001001-2025` atd., umístěno ve výchozím dolním‑pravém rohu.

---

## Často kladené otázky (FAQ)

### 1. Mohu změnit umístění čísel?
Ano. Nastavte `batesOptions.Position = new Position(10, 10, 10, 10);`, kde čtyři hodnoty představují okraje od horního, dolního, levého a pravého okraje. Aspose také poskytuje předdefinované výčty jako `BatesNumberingPosition.BottomCenter`.

### 2. Co když moje PDF již obsahuje číslování stránek?
Přidání Batesových čísel **překryje** existující čísla. Aby nedošlo k vizuálnímu nepořádku, buď skryjte původní čísla (pokud jsou součástí textové vrstvy), nebo upravte velikost písma a umístění v `batesOptions`.

### 3. Funguje to s šifrovanými PDF?
Aspose může otevřít PDF chráněné heslem, pokud heslo předáte:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Batesové číslování se pak použije stejným způsobem.

### 4. Jak **číslovat pdf stránky** jednoduchým sekvenčním čítačem (bez předpony/přípony)?
Stačí nastavit `Prefix = string.Empty` a `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Můžu tento přístup použít v ASP.NET Core k podávání PDF za běhu?
Rozhodně. Načtěte dokument, aplikujte číslování a poté zapište proud do HTTP odpovědi:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Okrajové případy a tipy pro nejlepší praxi

| Situace | Doporučený přístup |
|-----------|----------------------|
| **Velká PDF (stovky stránek)** | Zavolejte `pdf.BatesNumbering.Add` **po** provedení jakýchkoli úprav na úrovni stránek, aby nedošlo k opakovanému zpracování stejných stránek. |
| **Vlastní písma** | Nastavte `batesOptions.Font = FontRepository.FindFont("Arial")` a upravte `batesOptions.FontSize` pro lepší čitelnost naskenovaných dokumentů. |
| **Výkonnostně kritické dávkové úlohy** | Znovu použijte jedinou instanci `Document` při zpracování mnoha souborů ve smyčce; po každé iteraci ji uvolněte, aby se uvolnila paměť. |
| **Mezinárodní znaky** | Používejte Unicode‑kompatibilní písma (např. `Times New Roman Unicode`), aby se správně zobrazila předpona nebo přípona. |
| **Kompatibilita verzí** | Kód funguje s Aspose.Pdf 23.10 a novějšími. Pokud cílíte na starší verzi, zkontrolujte referenční dokumentaci API pro případné změny názvů vlastností. |

---

## Závěr

Nyní víte, jak **přidat Batesovo číslování** do PDF pomocí Aspose.Pdf pro .NET. Tutoriál pokryl načtení PDF, konfiguraci `BatesNumberingOptions`, aplikaci čísel na každou stránku a uložení výsledku. S těmito stavebními kameny můžete také implementovat obecné **pdf číslování stránek**, **číslování pdf stránek** s vlastním formátem a integrovat proces do větších automatizačních pipeline.

**Další kroky**

* Prozkoumejte API **bates numbering pdf** dále a přizpůsobte písmo, barvu a umístění.  
* Kombinujte tuto techniku s **digitálními podpisy** pro vytvoření právně nezměnitelných svazků.  
* Podívejte se na možnosti **PDF slučování** od Aspose, pokud potřebujete před číslováním spojit více spisových souborů.

Neváhejte experimentovat s různými předponami, příponami a délkami číslic, aby vyhovovaly standardům vaší organizace. Šťastné programování!


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}