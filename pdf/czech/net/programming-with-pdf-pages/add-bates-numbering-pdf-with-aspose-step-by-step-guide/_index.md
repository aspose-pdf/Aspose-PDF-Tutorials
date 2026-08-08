---
category: general
date: 2026-08-08
description: Přidat Batesovo číslování PDF pomocí Aspose.Pdf v C#. Tento tutoriál
  také ukazuje, jak přidat prázdnou stránku do PDF a generovat PDF programově.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: cs
lastmod: 2026-08-08
og_description: Přidejte Batesovo číslování PDF pomocí Aspose.Pdf v C#. Naučte se
  přidávat prázdnou stránku do PDF, generovat PDF programově a uložit finální dokument
  během několika minut.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Přidání Batesova číslování do PDF pomocí Aspose – kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Přidání Batesova číslování PDF pomocí Aspose – krok za krokem
url: /cs/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Batesova číslování PDF pomocí Aspose – krok za krokem

Přidání Batesova číslování PDF pomocí Aspose.Pdf je jednoduché, jakmile pochopíte základní kroky. Pokud také potřebujete přidat prázdnou stránku PDF nebo generovat PDF programově, tento průvodce pokrývá vše, co potřebujete.

V tomto tutoriálu budete:

* Vytvořit nový PDF dokument od nuly.  
* Přidat prázdnou stránku PDF, která bude hostit Batesova čísla.  
* Nakonfigurovat artefakt Batesova číslování s vlastním prefixem.  
* Uložit PDF, aby se čísla objevila v vygenerovaném souboru.  

Na konci budete mít plně funkční C# konzolovou aplikaci, která vytváří PDF obsahující Batesova čísla jako **CASE‑1000**, **CASE‑1001**, … – běžný požadavek pro právní a e‑discovery workflowy.

## Požadavky

* .NET 6.0 SDK nebo novější (kód také funguje s .NET Framework 4.8).  
* Visual Studio 2022 nebo jakékoli C#‑kompatibilní IDE.  
* Platná licence Aspose.Pdf pro .NET (nebo bezplatný evaluační klíč).  
* Základní znalost syntaxe C#.

> **Tip:** Pokud spustíte kód bez licence, Aspose přidá malý vodoznak do výstupního PDF.

## Krok 1: Nastavení projektu a import Aspose.Pdf

Vytvořte nový konzolový projekt a přidejte NuGet balíček Aspose.Pdf:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Direktivy `using` potřebné pro příklad jsou:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Tyto jmenné prostory vám poskytují přístup ke třídám `Document`, `Page` a `BatesNumberingArtifact`, které budou použity později.

## Krok 2: Přidání prázdné stránky PDF

Batesovo číslo musí být připojeno ke stránce, takže nejprve vytvoříme prázdnou stránku, která přijme artefakt číslování.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

Třída `Document` představuje celý PDF soubor, zatímco `Pages.Add()` vloží novou, prázdnou stránku na konec kolekce stránek dokumentu. Protože dokument začíná prázdný, tento volání také vytvoří první stránku.

## Krok 3: Konfigurace artefaktu Batesova číslování

Nyní definujeme, jak by Batesova čísla měla vypadat. `BatesNumberingArtifact` vám umožňuje nastavit počáteční číslo, prefix, suffix a možnosti formátování.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Proč je to důležité:**  
Nastavení `StartNumber` na **1000** odpovídá typickým konvencím právních spisů. `Prefix` zajistí, že každé číslo bude vypadat jako **CASE‑1000**, **CASE‑1001**, … což usnadňuje vyhledávání a řazení.

## Krok 4: Připojení artefaktu k stránce

Artefakt musí být přidán do kolekce `Artifacts` stránky, aby ho Aspose vykreslil na každé stránce během ukládání.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Když je dokument uložen, Aspose automaticky opakuje artefakt na všech stránkách a zvyšuje číslo pro každou následující stránku.

## Krok 5: (Volitelné) Přidání dalších stránek

Pokud potřebujete více stránek, jednoduše opakujte `pdfDocument.Pages.Add()`. Artefakt Batesova číslování, který jste připojili v předchozím kroku, se automaticky objeví na každé nové stránce.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Krok 6: Uložení PDF – generování PDF programově

Nakonec dokument uložíme na disk. V tomto okamžiku jsou Batesova čísla vykreslena na stránkách.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Očekávaný výsledek:**  
Otevřete *BatesNumberedDocument.pdf* a uvidíte třístránkové PDF. Každá stránka zobrazuje Batesovo číslo v pravém dolním rohu:

* Stránka 1 → **CASE‑1000**  
* Stránka 2 → **CASE‑1001**  
* Stránka 3 → **CASE‑1002**

Čísla jsou automaticky inkrementována, protože artefakt je připojen ke kolekci stránek.

## Kompletní, spustitelný příklad

Spojením všeho dohromady získáte kompletní konzolový program, který můžete zkopírovat, vložit a spustit:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Spusťte program pomocí `dotnet run`. Po dokončení najděte soubor na ploše a ověřte Batesova čísla.

![Příklad přidání Batesova číslování PDF](/images/bates-numbering.png "Příklad přidání Batesova číslování PDF")

## Časté otázky a okrajové případy

### Co když potřebuji jiné písmo nebo pozici?

`BatesNumberingArtifact` vystavuje vlastnosti jako `FontSize`, `FontColor`, `HorizontalAlignment` a `VerticalAlignment`. Například:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Jak vyloučit konkrétní stránku z číslování?

Vytvořte samostatný `BatesNumberingArtifact` pro stránky, které chcete číslovat, a přidejte jej jen těmto stránkám. Stránky bez připojeného artefaktu zůstanou nečíslované.

### Funguje to s existujícími PDF?

Ano. Místo `new Document()` načtěte existující soubor:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Pak připojte artefakt k požadovaným stránkám a uložte.

## Závěr

Nyní víte, jak **přidat Batesovo číslování PDF** pomocí Aspose.Pdf, jak **přidat prázdnou stránku PDF** a jak **generovat PDF programově** v čistém, znovupoužitelném C# řešení. Přístup funguje s libovolným počtem stránek, vlastními prefixy a možnostmi stylování, což vám dává plnou kontrolu nad konečným dokumentem.

Další kroky, které můžete prozkoumat:

* Use **create pdf as

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak přidat a přizpůsobit čísla stránek v PDF pomocí Aspose.PDF pro .NET \| Průvodce manipulací s dokumenty](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Jak přidat prázdnou stránku na konec PDF pomocí Aspose.PDF pro .NET \| Krok za krokem průvodce](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Vytvořit PDF dokument pomocí Aspose.PDF – Přidat stránku, tvar a uložit](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}