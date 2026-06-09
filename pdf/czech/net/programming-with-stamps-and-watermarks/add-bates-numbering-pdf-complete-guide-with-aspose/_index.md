---
category: general
date: 2026-06-08
description: Přidejte Batesovo číslování PDF pomocí Aspose.Pdf v C#. Naučte se, jak
  přidat Bates, přidat čísla stránek do PDF, přidat sekvenční čísla do PDF a podívejte
  se na příklad Batesova čísla PDF.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: cs
og_description: Přidání Batesova číslování PDF v C#. Tento tutoriál ukazuje, jak přidat
  Bates, jak přidat čísla stránek do PDF a jak přidat sekvenční čísla do PDF s kompletním
  příkladem Batesova číslování PDF.
og_title: Přidání Batesova číslování do PDF – Kompletní průvodce s Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Přidání Batesova číslování do PDF – Kompletní průvodce s Aspose
url: /cs/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Bates Numbering PDF – Kompletní programovací průvodce

Už jste někdy potřebovali **add bates numbering pdf**, ale nebyli jste si jisti, kde začít? Pokud jste se někdy ptali, *jak přidat bates* do právního dokumentu, jste na správném místě. V tomto tutoriálu vás provedeme praktickým, end‑to‑end příkladem, který nejen přidá Bates čísla, ale také vám ukáže, jak **add page numbers pdf**, **add sequential numbers pdf**, a dokonce poskytne připravený **bates number pdf example**.

Budeme používat knihovnu Aspose.Pdf pro .NET, protože abstrahuje nízkoúrovňové interní struktury PDF a zároveň vám poskytuje jemnou kontrolu. Na konci tohoto průvodce budete mít znovupoužitelný úryvek, který můžete vložit do jakéhokoli C# projektu, a pochopíte, proč je každá řádka důležitá.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód také funguje na .NET Framework 4.6+).  
- **Licence** pro Aspose.Pdf nebo bezplatný dočasný evaluační klíč.  
- Vzorek PDF nazvaný `input.pdf` umístěný ve složce, na kterou můžete odkazovat.  
- Visual Studio, Rider nebo jakýkoli C# editor, který preferujete.

To je vše—žádné další nástroje, žádné gymnastiky v příkazovém řádku. Připravení? Ponořme se.

## Přidání Bates Numbering PDF – Krok za krokem implementace

Níže rozdělujeme proces do šesti logických kroků. Každý krok obsahuje krátký úryvek kódu, vysvětlení *proč* to děláme a tip, který vám může přijít vhod.

### Krok 1: Instalace NuGet balíčku Aspose.Pdf

Nejprve přidejte knihovnu do svého projektu. Otevřete Package Manager Console a spusťte:

```powershell
Install-Package Aspose.Pdf
```

> **Tip:** Pokud používáte .NET Core, můžete také použít `dotnet add package Aspose.Pdf`.

Instalace balíčku vám poskytne přístup ke třídě `Aspose.Pdf.Facades.BatesNumbering`, která je hlavním nástrojem pro **add bates numbering pdf**.

### Krok 2: Otevření zdrojového PDF dokumentu

Nyní načteme PDF, které chceme označit. Příkaz `using` zajišťuje, že soubor bude řádně uzavřen i v případě výjimky.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

Proč použít `Aspose.Pdf.Document`? Reprezentuje celý PDF v paměti, což nám umožňuje manipulovat s stránkami, fonty a metadaty, aniž bychom se dotkli původního souboru na disku.

### Krok 3: Vytvoření Bates Numbering Facade

Vzor *facade* skrývá složitost podkladové struktury PDF. Zde je, jak jej vytvoříme:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

Tento objekt bude později nastaven s předponou, počátečním číslem a možnostmi formátování. Považujte ho za „motor“, který **add page numbers pdf** v souladu s Bates.

### Krok 4: Nastavení počátečního čísla a předpony

Bates čísla často obsahují specifickou předponu případu. Můžete také řídit počet číslic, oddělovač a umístění na stránce.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**Proč tato nastavení?**  
- `StartNumber` vám umožní pokračovat v předchozí sérii.  
- `NumberOfDigits` zajišťuje jednotnou délku, což je klíčové pro právní indexaci.  
- `Location` určuje, kde se objeví **add sequential numbers pdf**; můžete jej přesunout do pravého horního rohu, pokud chcete.

### Krok 5: Aplikace Bates číslování na dokument

Po nastavení facade nyní označíme každou stránku:

```csharp
bates.AddBatesNumbering(doc);
```

Pod povrchem Aspose prochází každou stránku, vykresluje text na zadaném místě a respektuje existující obsah. Tento jediný řádek ve skutečnosti **add bates numbering pdf** do vašeho souboru.

### Krok 6: Uložení upraveného PDF

Nakonec zapíšete výstup na disk:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

Nyní máte PDF, kde každá stránka nese jedinečný Bates identifikátor, připravený pro vyhledávání nebo podání soudu.

#### Kompletní funkční příklad (Bates Number PDF Example)

Spojením všeho dohromady, zde je kompletní, samostatný program, který můžete zkompilovat a spustit:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Očekávaný výstup:** Otevřete `output.pdf` a uvidíte „CASE‑01000“, „CASE‑01001“, … v levém dolním rohu každé stránky.

![Snímek obrazovky PDF stránky s Bates numbers v levém dolním rohu – add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "add bates numbering pdf example")

*(Alt text obrázku: *add bates numbering pdf example* – ukazuje Bates čísla aplikovaná na ukázkový PDF.)*

## Jak přidat Bates – Porozumění Facade

Možná se ptáte, **how to add bates** bez Aspose facade. Alternativou je ručně kreslit text na každou stránku pomocí nízkoúrovňových PDF operátorů, ale tento přístup je náchylný k chybám a vyžaduje hluboké znalosti PDF specifikace. Facade abstrahuje tyto detaily, takže se můžete soustředit na *co* chcete (předpona, počáteční číslo) místo na *jak* to vykreslit.

Pokud někdy potřebujete **add page numbers pdf** v ne‑Bates stylu (např. „Strana 3 z 12“), můžete znovu použít stejnou třídu `BatesNumbering`—stačí změnit `Prefix` na prázdný řetězec a upravit `Location`. Podkladový motor je stejný, což znamená, že získáte konzistentní vykreslování v obou případech.

## Přidání Page Numbers PDF – Přizpůsobení umístění a stylu

Právní týmy často požadují číslo stránky v hlavičce, zatímco podpora soudních procesů jej upřednostňuje v patičce. Zde je rychlá úprava:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

Stejné volání `AddBatesNumbering` nyní **add page numbers pdf** na vrchol každé stránky. Protože facade pracuje s objektem dokumentu, můžete mezi Bates a běžným číslováním stránek přepínat pomocí několika změn vlastností—není potřeba přepisovat smyčku.

## Přidání Sequential Numbers PDF – Pokročilé formátování

Předpokládejme, že potřebujete formát jako `2023-CASE-00123`. Můžete kombinovat datumovou předponu s existujícími nastaveními:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Nyní každá stránka bude obsahovat `2023-CASE-00123`, `2023-CASE-00124` atd. To ukazuje, jak snadno můžete **add sequential numbers pdf**, které splňují složité pojmenovací konvence.

## Okrajové případy a běžné úskalí

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|----------------------|---------------|
| **Velmi velké PDF ( > 500 MB )** | Spotřeba paměti může výrazně vzrůst, protože celý dokument je načten do RAM. | Použijte `Document` s nastavením `MemoryManagement` nebo zpracovávejte soubor po částech pomocí `PdfFileEditor`. |
| **Existující čísla stránek** |  |  |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak přidat a přizpůsobit čísla stránek v PDF pomocí Aspose.PDF pro .NET \| Průvodce manipulací s dokumenty](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Jak přidat razítka s čísly stránek v PDF pomocí Aspose.PDF pro .NET \| Vodoznaky a pozadí](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Přidání čísel stránek do PDF pomocí FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}