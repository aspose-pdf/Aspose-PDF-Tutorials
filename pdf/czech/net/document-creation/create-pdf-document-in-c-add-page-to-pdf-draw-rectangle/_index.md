---
category: general
date: 2026-03-24
description: Vytvořte PDF dokument v C# s Aspose.Pdf – naučte se, jak přidat stránku
  do PDF, nakreslit obdélník a uložit PDF do souboru.
draft: false
keywords:
- create pdf document
- add page to pdf
- save pdf to file
- how to create pdf
- how to add rectangle
language: cs
og_description: Vytvořte PDF dokument v C# pomocí Aspose.Pdf. Naučte se, jak přidat
  stránku do PDF, nakreslit obdélník a uložit PDF do souboru během několika jednoduchých
  kroků.
og_title: Vytvořte PDF dokument v C# – Přidejte stránku do PDF a nakreslete obdélník
tags:
- pdf
- csharp
- aspose
title: Vytvořte PDF dokument v C# – Přidejte stránku do PDF a nakreslete obdélník
url: /cs/net/document-creation/create-pdf-document-in-c-add-page-to-pdf-draw-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF dokumentu v C# – Přidání stránky do PDF a vykreslení obdélníku

Už jste někdy potřebovali **vytvořit PDF dokument** v C#, ale nebyli jste si jisti, kde začít? Nejste v tom sami – většina vývojářů narazí na tuto překážku, když poprvé řeší programové generování PDF. Dobrou zprávou je, že s Aspose.Pdf můžete během několika řádků vytvořit PDF, přidat stránku do PDF, umístit na ni obdélník a poté **uložit PDF do souboru**.

V tomto tutoriálu projdeme celý proces, od inicializace dokumentu až po jeho uložení na disk. Na konci budete vědět, **jak vytvořit PDF** soubory za běhu, **jak přidat obdélník** a přesně, kde se soubor na vašem systému nachází.

## Co se naučíte

- Jak **vytvořit PDF dokument** pomocí třídy `Document` z Aspose.Pdf.  
- Správný způsob, jak **přidat stránku do PDF** bez vyvolání chyb rozvržení.  
- Postupné instrukce, jak **přidat obdélník** na stránku.  
- Nejbezpečnější metoda, jak **uložit PDF do souboru** a řešit běžné úskalí.  

Žádné složité předpoklady – jen vývojové prostředí .NET a NuGet balíček Aspose.Pdf pro .NET.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.7+).  
- Visual Studio 2022 nebo jakékoli IDE kompatibilní s C#.  
- Aspose.Pdf pro .NET nainstalovaný (`dotnet add package Aspose.Pdf`).  

Pokud je máte, pojďme na to.

## Vytvoření PDF dokumentu – Přehled

První věc, kterou musíte udělat, je vytvořit instanci objektu `Document`. Představte si ho jako prázdné plátno čekající na stránky, text, obrázky nebo tvary.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document in memory
using var pdfDocument = new Document();
```

Proč použít `using var`? Zaručuje, že podkladové souborové proudy jsou automaticky uvolněny, což později zabraňuje chybám se zamčením souboru, když se pokusíte **uložit PDF do souboru**.

## Přidání stránky do PDF

PDF bez stránek je v podstatě prázdný obal. Přidání stránky je tak jednoduché jako zavolat `Pages.Add()`. Metoda vrací objekt `Page`, se kterým můžete okamžitě začít pracovat.

```csharp
// Step 2: Add a blank page to the document
var pdfPage = pdfDocument.Pages.Add();
```

**Tip:** Výchozí velikost stránky je A4 (595 × 842 bodů). Pokud potřebujete jinou velikost, předávejte `PageSize` enum nebo vlastní rozměry do `Add()`.

```csharp
// Example: Add a Letter‑sized page
var letterPage = pdfDocument.Pages.Add(PageSize.Letter);
```

## Jak přidat obdélník na stránku PDF

Nyní ta zábavná část – kreslení obdélníku. Třída `Rectangle` z Aspose.Pdf očekává souřadnice levého dolního rohu, následované šířkou a výškou. Tyto hodnoty jsou měřeny v bodech (1 pt ≈ 1/72 palce).

```csharp
// Step 3: Insert a rectangle shape onto the page
// Lower‑left corner at (0,0), width 600 pt, height 800 pt
pdfPage.Paragraphs.Add(new Rectangle(0, 0, 600, 800));
```

### Proč jsou tato čísla důležitá

- **(0,0)** umisťuje obdélník do levého dolního rohu stránky.  
- **600 × 800** pohodlně zapadá na stránku A4 (která má rozměry 595 × 842).  
- Pokud obdélník přesáhne hranice stránky, Aspose vyhodí výjimku – proto vždy ověřujte rozměry, zejména při změně velikosti stránky.

### Přizpůsobení obdélníku

Můžete změnit styl čáry, barvu a výplň:

```csharp
var rect = new Rectangle(50, 700, 200, 100)
{
    Border = new BorderInfo(BorderSide.All, .5f, Color.Black),
    FillColor = Color.LightGray
};
pdfPage.Paragraphs.Add(rect);
```

Tento úryvek vykreslí obdélník o rozměrech 200 × 100 pt, posunutý o 50 pt od levého okraje a 700 pt od spodního, s tenkým černým okrajem a světle šedou výplní.

## Uložení PDF do souboru

Jakmile stránka vypadá tak, jak chcete, posledním krokem je uložení souboru. Metoda `Save` přijímá cestu k souboru, `Stream` nebo dokonce `MemoryStream`, pokud chcete PDF poslat po síti.

```csharp
// Step 4: Save the PDF to a file on disk
pdfDocument.Save("C:\\Temp\\output.pdf");
```

**Pamatujte:** Když spouštíte tento kód na Linuxu, používejte lomítka (`/`) nebo `Path.Combine`, abyste se vyhnuli problémům s oddělovači cest.

### Ošetření výjimek

Ukládání může selhat z důvodů, jako jsou nedostatečná oprávnění k zápisu nebo existující soubor jen pro čtení. Zabalte volání do try/catch, aby se zobrazily užitečné diagnostické informace:

```csharp
try
{
    pdfDocument.Save("C:\\Temp\\output.pdf");
}
catch (IOException ex)
{
    Console.WriteLine($"Unable to write file: {ex.Message}");
}
```

## Kompletní funkční příklad

Níže je samostatný program, který můžete zkopírovat a vložit do konzolové aplikace. Ukazuje **jak vytvořit PDF**, **přidat stránku do PDF**, **jak přidat obdélník** a **uložit PDF do souboru** – vše najednou.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing; // For Color struct

class Program
{
    static void Main()
    {
        // 1️⃣ Create the PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Add a new page (default A4)
        var page = pdfDocument.Pages.Add();

        // 3️⃣ Draw a rectangle – fits inside the page
        var rect = new Rectangle(0, 0, 600, 800)
        {
            Border = new BorderInfo(BorderSide.All, 1.0f, Color.Blue),
            FillColor = Color.AliceBlue
        };
        page.Paragraphs.Add(rect);

        // 4️⃣ Persist the PDF to disk
        const string outputPath = "output.pdf";
        try
        {
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF successfully saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error saving PDF: {ex.Message}");
        }
    }
}
```

**Očekávaný výsledek:** Otevřete `output.pdf` a uvidíte jedinou stránku A4 s modrým okrajem, světle modrým obdélníkem umístěným v levém dolním rohu. Text není potřeba; samotný obdélník dokazuje, že tvar byl přidán správně.

## Běžné úskalí a tipy

| Problém | Proč se to děje | Jak to opravit |
|---------|----------------|----------------|
| **Obdélník přesahuje velikost stránky** | Souřadnice nebo rozměry větší než rozměry stránky způsobí `ArgumentException`. | Zkontrolujte velikost stránky (`page.PageInfo.Width`, `.Height`) před kreslením. |
| **Cesta k souboru není zapisovatelná** | Spuštění pod omezeným uživatelským účtem nebo pokus o zápis do chráněné složky. | Použijte adresář zapisovatelný uživatelem, např. `%TEMP%` nebo `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)`. |
| **Zapomenuto uvolnit** | Nepoužití `Dispose` na `Document` může soubor zamknout až do ukončení procesu. | Použijte `using var` nebo explicitně zavolejte `pdfDocument.Dispose()`. |
| **Chybí odkaz na Aspose.Pdf** | NuGet balíček není nainstalován nebo projekt cílí na nekompatibilní framework. | Spusťte `dotnet add package Aspose.Pdf` a ujistěte se, že cílový framework je podporován. |

### Okrajové případy

- **Více stránek:** Zavolejte `pdfDocument.Pages.Add()` pro každou další stránku a poté přidejte tvary do příslušných objektů `Page`.  
- **Dynamické rozměry:** Pokud potřebujete, aby obdélník vyplnil celou stránku, použijte `page.PageInfo.Width` a `page.PageInfo.Height` pro šířku/výšku.  
- **Streamování na webového klienta:** Nahraďte `pdfDocument.Save(filePath)` voláním `pdfDocument.Save(stream, SaveFormat.Pdf)` a pošlete stream v HTTP odpovědi.  

## Další kroky

Nyní, když víte **jak vytvořit PDF**, zvažte rozšíření dokumentu:

- Přidejte text pomocí `TextFragment`.  
- Vložte obrázky pomocí třídy `Image`.  
- Vytvořte tabulky pro faktury nebo zprávy.  

Všechny tyto kroky následují stejný vzor: vytvořte objekt, nakonfigurujte jeho vlastnosti a přidejte jej do `page.Paragraphs`.

Pokud vás zajímá pokročilejší stylování – jako jsou gradienty, rotace nebo šifrování PDF – podívejte se na oficiální dokumentaci Aspose nebo sérii tutoriálů „Advanced PDF Manipulation“.

## Závěr

Probrali jsme vše, co potřebujete k **vytvoření PDF dokumentu** v C# pomocí Aspose.Pdf: inicializaci dokumentu, **přidání stránky do PDF**, kreslení obdélníku pomocí **jak přidat obdélník** a nakonec **uložení PDF do souboru**. Kompletní příklad funguje ihned po spuštění a výše uvedené tipy by vás měly ochránit před nejčastějšími problémy.

Give it

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}