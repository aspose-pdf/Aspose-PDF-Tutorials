---
category: general
date: 2026-02-10
description: Vytvořte PDF dokument v C# pomocí Aspose.Pdf. Naučte se, jak přidat stránku
  do PDF a jak bezpečně přidat obdélník do PDF pomocí kontroly hranic.
draft: false
keywords:
- create pdf document
- add page to pdf
- how to add rectangle pdf
language: cs
og_description: Vytvořte PDF dokument v C# pomocí Aspose.Pdf. Tento návod ukazuje,
  jak přidat stránku do PDF a jak přidat obdélník do PDF při kontrole hranic.
og_title: Vytvořte PDF dokument v C# – Přidejte stránku do PDF a obdélník
tags:
- pdf
- csharp
- aspose
title: Vytvořit PDF dokument v C# – Přidat stránku do PDF a obdélník
url: /cs/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF dokumentu v C# – Přidání stránky do PDF a obdélníku

Už jste někdy potřebovali **create pdf document** v C# a nebyli jste si jisti, kde začít? Nejste sami — většina vývojářů narazí na stejnou překážku, když poprvé zkouší knihovny pro generování PDF. Dobrou zprávou je, že s Aspose.Pdf můžete rychle vytvořit PDF, přidat stránku do PDF a dokonce kreslit tvary jako obdélník bez potíží.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který nejen **creates a PDF document**, ale také ukazuje **how to add rectangle PDF** objekty bezpečně zapnutím globální kontroly hranic. Na konci budete mít pevné pochopení API, budete vědět, proč je každý krok důležitý, a uvidíte přesný výstup, který byste měli očekávat.

## Co budete potřebovat

- .NET 6+ (nebo .NET Framework 4.6+). Kód funguje stejně na obou.
- NuGet balíček Aspose.Pdf pro .NET (`Aspose.Pdf`) — nainstalujte jej pomocí `dotnet add package Aspose.Pdf`.
- Jakýkoli editor C# (Visual Studio, VS Code, Rider… podle vás).

Žádná další konfigurace není vyžadována; knihovna obsahuje vše, co potřebujete k okamžitému generování PDF.

## Krok 1: Vytvoření PDF dokumentu a povolení kontroly hranic

Prvním krokem je vytvořit objekt `Document`. Považujte jej za prázdné plátno pro vaše dobrodružství s **create pdf document**. Hned poté povolíme globální nastavení, které nutí knihovnu ověřovat, že každý grafický objekt zůstává uvnitř oblasti stránky. To je klíčové, když později budete kreslit tvary, které by mohly přesahovat okraje.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Initialise a new PDF document
using var document = new Document();

// Step 1b: Turn on boundary checking for all graphics objects
document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;
```

*Proč povolit kontrolu hranic?*  
Pokud omylem umístíte obdélník mimo stránku, Aspose vyhodí `PdfException`. Zachycení této výjimky včas vás ochrání před poškozenými PDF, které některé prohlížeče jednoduše odmítnou otevřít.

## Krok 2: Přidání stránky do PDF

PDF bez stránek je jako kniha bez listů — naprosto k ničemu. Přidání stránky je tak jednoduché jako zavolat `Pages.Add()`. Metoda vrátí objekt `Page`, který použijete k umístění obsahu.

```csharp
// Step 2: Add a new page (this is the “add page to pdf” part)
Page page = document.Pages.Add();
```

> **Tip:** Výchozí velikost stránky v Aspose je 595 × 842 bodů (A4). Pokud potřebujete jinou velikost, můžete nastavit `page.PageInfo.Width` a `page.PageInfo.Height` před přidáním obsahu.

## Krok 3: Definování obdélníku, který bude mimo hranice

Nyní přicházíme k jádru **how to add rectangle pdf** objektů. Úmyslně vytvoříme obdélník, který překračuje rozměry stránky, abychom viděli výjimku v akci. Konstruktor `Rectangle` přijímá čtyři argumenty: *dolní‑levý X, dolní‑levý Y, horní‑pravý X, horní‑pravý Y*.

```csharp
// Step 3: Create a rectangle that goes beyond the page edges
// Page size: 595x842, so X=800 and Y=900 are out of bounds
var outOfBoundsRect = new Rectangle(400, 750, 800, 900);
```

Pokud spustíte kód s vypnutou kontrolou hranic, obdélník bude jednoduše oříznut. S kontrolou zapnutou Aspose vyvolá chybu, což je přesně to, co chceme pro robustní pipeline generování PDF.

## Krok 4: Vytvoření tvaru a přidání viditelného okraje

Obdélník sám o sobě je neviditelný, pokud nepřidáte okraj nebo výplň. Zde zabalíme `Rectangle` do objektu tvaru `Rectangle` (ano, název třídy je trochu matoucí) a přiřadíme tenký černý okraj.

```csharp
// Step 4: Turn the rectangle into a shape and add a border
var rectangleShape = new Rectangle(outOfBoundsRect)
{
    Border = new BorderInfo(BorderSide.All, 1f)   // 1‑point black border
};
```

*Proč okraj?*  
Bez okraje byste na stránce nic neviděli, což ztěžuje ladění. Tenčí okraj také jasně ukazuje, když je tvar mimo hranice.

## Krok 5: Přidání tvaru na stránku – Očekávejte výjimku

Nyní skutečně umístíme tvar na stránku. Protože obdélník překračuje limity stránky a zapnuli jsme kontrolu hranic, Aspose vyhodí `PdfException`. Volání zabalíme do bloku `try/catch`, abychom ukázali elegantní zpracování chyb.

```csharp
// Step 5: Attempt to add the shape – this will raise an exception
try
{
    page.Paragraphs.Add(rectangleShape);
}
catch (PdfException ex)
{
    Console.WriteLine("Caught PdfException: " + ex.Message);
    // Handle the error – maybe adjust the rectangle or log the issue
}
```

Pokud zakomentujete řádek `CheckGraphicsObjectBoundaries` v Kroku 1, kód uspěje a obdélník bude oříznut na okraje stránky. Toto chování je užitečné pro rychlé prototypy, ale v produkci obvykle chcete mít bezpečnostní síť.

## Krok 6: Uložení PDF

Nakonec dokument uložíme na disk. Soubor bude vytvořen ve složce, kterou určíte; ujistěte se, že cesta existuje, nebo použijte `Path.Combine` s `Environment.CurrentDirectory`.

```csharp
// Step 6: Save the resulting PDF
string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
document.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Když otevřete `checked_shapes.pdf`, uvidíte prázdnou stránku (protože obdélník byl odmítnut). Pokud byste odstranili kontrolu hranic, viděli byste částečně vykreslený obdélník oříznutý na pravém a horním okraji.

---

![Příklad vytvoření PDF dokumentu ukazující kontrolu hranic obdélníku](https://example.com/images/checked_shapes.png "Příklad vytvoření PDF dokumentu s kontrolou hranic obdélníku")

*Náhled výše ukazuje PDF po spuštění tutoriálu s vypnutou kontrolou hranic (obdélník je oříznut). S kontrolou zapnutou je tvar vynechán a je zaznamenána výjimka.*

## Shrnutí: Kompletní funkční příklad

Spojením všech částí dohromady získáte kompletní, připravený k spuštění program:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise document and enable boundary checking
        using var document = new Document();
        document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;

        // 2️⃣ Add a page (add page to pdf)
        Page page = document.Pages.Add();

        // 3️⃣ Define an out‑of‑bounds rectangle (how to add rectangle pdf)
        var outOfBoundsRect = new Rectangle(400, 750, 800, 900);

        // 4️⃣ Create shape with a visible border
        var rectangleShape = new Rectangle(outOfBoundsRect)
        {
            Border = new BorderInfo(BorderSide.All, 1f)
        };

        // 5️⃣ Try to add the shape – expect an exception
        try
        {
            page.Paragraphs.Add(rectangleShape);
        }
        catch (PdfException ex)
        {
            Console.WriteLine("Caught PdfException: " + ex.Message);
        }

        // 6️⃣ Save the PDF
        string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
        document.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

Spusťte program a uvidíte výstup v konzoli, který potvrdí, zda byla výjimka zachycena. Otevřete vygenerované PDF a ověřte výsledek.

## Časté otázky a okrajové případy

- **Co když potřebuji jinou velikost stránky?**  
  Nastavte `page.PageInfo.Width` a `page.PageInfo.Height` před přidáním tvarů. Kontrola hranic automaticky použije nové rozměry.

- **Mohu vypnout kontrolu hranic pro jeden konkrétní tvar?**  
  Ne přímo. Nastavení je globální, ale můžete ji dočasně vypnout, přidat tvar a pak ji znovu zapnout — mějte na vědomí, že pro tuto operaci přijdete o bezpečnostní síť.

- **Je zpráva výjimky užitečná?**  
  Ano, Aspose zahrnuje problematické souřadnice, takže můžete programově upravit obdélník nebo zaznamenat podrobné diagnostické informace.

- **Bude to fungovat na .NET Core na Linuxu?**  
  Rozhodně. Aspose.Pdf je platformově nezávislý; jen se ujistěte, že soubory fontů, na které odkazujete, jsou dostupné na cílovém OS.

## Další kroky

Nyní, když znáte **how to add rectangle pdf** objekty a jak **add page to pdf**, můžete chtít prozkoumat:

- Přidání dalších typů grafiky (elipsy, čáry) se stejnými kontrolami hranic.
- Vkládání textu, obrázků nebo tabulek — Aspose nabízí bohaté API pro každou možnost.
- Použití přetížení `Document.Save` pro výstup přímo do `MemoryStream` pro webová API.

Neváhejte experimentovat s různými souřadnicemi obdélníku, okraji a barvami výplně. Čím více si budete hrát, tím lépe pochopíte, jak Aspose.P

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}