---
category: general
date: 2026-02-25
description: Tutoriál Bates číslování – naučte se, jak přidat čísla stránek do PDF
  a použít vlastní Bates číslování pomocí Aspose.Pdf v C#. Krok za krokem průvodce
  s kompletním kódem.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: cs
og_description: Tutoriál Bates číslování vám ukáže, jak přidat číslování stránek do
  PDF a vlastní Bates číslování v C#. Kompletní kód, vysvětlení a tipy.
og_title: Tutoriál Bates číslování – Přidejte Batesova čísla do PDF pomocí C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Návod na Batesovo číslování: Přidejte Batesova čísla do PDF pomocí C#'
url: /cs/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Návod na Bates číslování – Přidání Batesových čísel do PDF v C#

Už jste se někdy zamýšleli, jak přidat čísla stránek do PDF a zároveň vložit právně stylizované Batesovo číslo? Nejste v tom sami. V tomto **bates numbering tutorial** projdeme vše, co potřebujete vědět, abyste každou stránku PDF označili vlastním prefixem, nulovým doplněním a přesným umístěním — pomocí Aspose.Pdf pro .NET.  
Dobrá zpráva? Je to poměrně jednoduché, jakmile pochopíte základní koncepty. Na konci tohoto průvodce budete mít spustitelný program, který vezme *input.pdf* a vytvoří *bates_out.pdf* s úhledným štítkem ve stylu “ABC‑01000” na každé stránce. Pojďme na to.

## Co budete potřebovat

- **Aspose.Pdf for .NET** (verze 23.10 nebo novější). Knihovna je komerční, ale bezplatná zkušební verze stačí pro učení.  
- .NET 6+ SDK (libovolná recentní verze bude stačit).  
- Základní vývojové prostředí C# — Visual Studio, VS Code nebo Rider.  
- Vstupní PDF pro experimentování (libovolný více‑stránkový dokument ukáže efekt).  

Žádné další NuGet balíčky kromě Aspose.Pdf nejsou potřeba a kód běží na Windows, Linuxu nebo macOS bez úprav.

## Krok 1: Načtení zdrojového PDF dokumentu (bates numbering tutorial – inicializace)

Nejprve vytvoříme objekt `Document`, který představuje PDF, které chceme upravit. Představte si to jako načtení prázdného plátna, na které můžete kreslit.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Proč je to důležité:** Bez načtení souboru není co anotovat. Kontrola sanity zabraňuje tichému selhání později, když se pokusíte přidat artefakty do neexistující kolekce stránek.

## Krok 2: Definování artefaktu Bates číslování (jak přidat bates)

Objekt *BatesNumberingArtifact* říká Aspose, kde a jak vykreslit identifikátor. Můžete nastavit prefix, počáteční číslo, doplnění nul, velikost písma a přesné souřadnice X/Y.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Proč je to důležité:** Vlastnost `LeadingZeros` zajišťuje, že každý štítek má stejnou délku, což je v právních dokumentech klíčové, kde záleží na zarovnání. Upravením `X` a `Y` přesunete razítko do pravého horního, levého dolního rohu nebo kamkoli váš pracovní postup vyžaduje.

## Krok 3: Připojení artefaktu ke každé stránce (add page numbers pdf)

Nyní procházíme každou stránku a připojujeme stejný artefakt. Zde se splňuje požadavek *add page numbers pdf* — každá stránka automaticky získá vlastní sekvenční štítek.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Proč je to důležité:** Přidáním artefaktu do kolekce `Artifacts` místo ručního kreslení textu necháme Aspose spravovat logiku číslování, doplňování nul a vykreslování. Tím se sníží počet chyb a kód zůstane stručný.

## Krok 4: Uložení upraveného PDF (add bates numbering)

Nakonec změny uložíme do nového souboru. Je dobrý zvyk zapisovat do jiného názvu souboru, aby originál zůstal nedotčený.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Proč je to důležité:** Metoda `Save` zapíše celé PDF a vloží artefakty jako součást proudu obsahu stránky. Výsledný soubor lze otevřít v libovolném PDF prohlížeči a zobrazí Batesova čísla přesně tak, jak byla zadána.

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní, připravený k spuštění program. Zkopírujte jej do projektu konzolové aplikace, nahraďte zástupné cesty a stiskněte **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Očekávaný výsledek

Otevřete *bates_out.pdf* v Adobe Reader, Foxit nebo jakémkoli prohlížeči. Na první stránce byste měli vidět štítek jako **ABC‑01000**, na druhé **ABC‑01001** a tak dále, umístěný 50 pt od levého okraje a 30 pt od spodního okraje. Čísla jsou zarovnána vpravo díky doplnění nul, což dává dokumentu čistý, profesionální vzhled.

## Běžné varianty a okrajové případy

| Scénář | Jak upravit |
|----------|---------------|
| **Různý prefix** | Change `Prefix = "XYZ"` in the artifact definition. |
| **Začít od vlastního čísla** | Set `Start = 5000` (or any integer). |
| **Umístit číslo do pravého horního rohu** | Use `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Změnit velikost písma pro větší dokumenty** | Modify `FontSize = 12` (or any size). |
| **Přidat pozadí ve tvaru obdélníku** | Create a `RectangleArtifact` and add it before the `BatesNumberingArtifact`. |
| **Přeskočit určité stránky** | Inside the `foreach` loop, add an `if (page.Number % 2 == 0) continue;` to skip even pages. |

**Pro tip:** Vždy nejprve testujte s krátkým PDF. Je rychlejší ověřit umístění, než spustíte skript na 200‑stránkový soubor.

## Často kladené otázky

- **Funguje to s šifrovanými PDF?**  
  Aspose.Pdf může otevřít soubory chráněné heslem, pokud heslo předáte pomocí `Document(string, string)`. Batesův artefakt bude i po dešifrování aplikován.

- **Mohu přidat jak Batesová čísla, tak běžná čísla stránek?**  
  Ano. Přidejte `PageNumberArtifact` vedle `BatesNumberingArtifact`. Každý artefakt má svůj vlastní čítač.

- **Co když má mé PDF různé velikosti stránek?**  
  Hodnoty `Position` jsou v absolutních bodech. Pro dokumenty s různými velikostmi stránek vypočítejte pozici pro každou stránku uvnitř smyčky pomocí `page.PageInfo.Width` a `page.PageInfo.Height`.

## Další kroky a související témata

Nyní, když jste zvládli **bates numbering tutorial**, můžete chtít prozkoumat:

- **Adding watermarks** – podobný přístup s artefaktem pomocí `TextArtifact`.  
- **Merging multiple PDFs** – použijte `Document.AppendDocument`.  
- **Extracting text for search indexing** – třída `TextAbsorber`.  
- **Automating batch processing** – procházejte složku s PDF a aplikujte stejný artefakt.  

Všechny tyto témata staví na stejných konceptech, které jste se právě naučili, takže jste dobře připraveni rozšířit svůj nástroj pro automatizaci PDF.

*Šťastné programování! Pokud narazíte na potíže nebo máte nápady na další úpravy, neváhejte zanechat komentář níže. Svět manipulace s PDF je rozsáhlý, ale s pevně zvládnutým **bates numbering tutorial** už jste o krok napřed.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}