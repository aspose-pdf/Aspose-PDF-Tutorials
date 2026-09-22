---
category: general
date: 2026-03-03
description: Vytvořte PDF dokument v C# s Batesovým číslováním – naučte se, jak přidat
  Bates, přidat sekvenční čísla stránek a generovat Bates během několika kroků.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: cs
og_description: Vytvořte PDF dokument v C# s Batesovým číslováním. Tento návod ukazuje,
  jak přidat Bates, přidat sekvenční čísla stránek a rychle generovat Bates.
og_title: Vytvořit PDF dokument v C# – Přidat Batesovo číslování
tags:
- C#
- PDF
- Bates numbering
title: Vytvořit PDF dokument v C# – Přidat Batesovo číslování
url: /cs/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF dokumentu C# – Přidání Bates číslování

Už jste někdy potřebovali **create PDF document C#** a poté označit každou stránku jedinečným identifikátorem pro právní nebo archivní účely? Nejste v tom sami—právnické firmy, soudy i velké korporace se neustále ptají: „Jak mohu automaticky přidat Bates čísla do mých PDF?“ Dobrou zprávou je, že s několika řádky kódu můžete vygenerovat PDF, posypat Bates čísla na každou stránku a výsledek uložit, aniž byste kdykoli otevírali editor.

V tomto tutoriálu projdeme praktickým, end‑to‑end příkladem, který ukazuje **how to add Bates**, jak **add sequential page numbers**, a dokonce **generate Bates** s vlastními předponami. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- **.NET 6+** (kód funguje také na .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – komerční knihovna, která nabízí čisté API pro manipulaci s PDF. Bezplatná zkušební verze funguje dobře pro testování.
- Základní znalost C# (pravděpodobně už jste zvyklí na `using` příkazy a objekty).

Kromě `Aspose.Pdf` nejsou vyžadovány žádné další balíčky NuGet. Pokud jste jej ještě nenainstalovali, spusťte:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Udržujte svou verzi Aspose aktuální; poslední verze 23.x přidává vylepšení výkonu pro velké dokumenty.

## Krok 1: Otevřete (nebo vytvořte) zdrojový PDF dokument

Nejprve potřebujeme PDF, se kterým budeme pracovat. V mnoha reálných scénářích již máte vstupní soubor—například naskenovanou smlouvu. Pro potřeby příkladu otevřeme existující soubor nazvaný `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Proč je to důležité:** Otevření dokumentu uvnitř `using` bloku zaručuje, že souborový handle je rychle uvolněn, což zabraňuje problémům se zamčením souboru, když později budete chtít přepsat stejný soubor.

## Krok 2: Definujte možnosti Bates číslování

Bates čísla se skládají z **prefixu** (často identifikátor případu) a **počátečního čísla**. Můžete také řídit počet číslic, umístění na stránce a styl písma. Zde použijeme sekundární klíčové slovo **add bates numbering pdf** nastavením objektu `BatesNumberingOptions`.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **Jak přidat bates:** Úpravou `Prefix` a `Start` řídíte přesný řetězec, který se objeví na každé stránce. Vlastnost `NumberOfDigits` zajišťuje jednotnou šířku, což je užitečné pro právní podání.

## Krok 3: Aplikujte Bates číslování na každou stránku

Nyní přichází hlavní operace—přidání čísel. Metoda `AddBatesNumbering` prochází každou stránku, kreslí text a respektuje nastavené možnosti.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Pod povrchem Aspose vykresluje text jako *content* element, což znamená, že čísla se stanou součástí PDF a nelze je v prohlížeči vypnout. To je přesně to, co potřebujete, když chcete **add sequential page numbers**, které jsou neměnné.

### Okrajové případy a varianty

- **Multiple prefixes:** Pokud potřebujete různé předpony pro jednotlivé sekce, vytvořte samostatné `BatesNumberingOptions` a zavolejte `AddBatesNumbering` na rozsah stránek (`pdfDocument.Pages[1..5]`).
- **Zero‑padding control:** Vynechte `NumberOfDigits` pro číslo proměnné délky, nebo nastavte vyšší hodnotu pro úvodní nuly.
- **Custom positioning:** Použijte `Margin` pro odsazení čísla od okraje, nebo přepněte `HorizontalAlignment` na `Center` pro styl zápatí.

## Krok 4: Uložte upravený PDF

Nakonec zapište aktualizovaný dokument na disk. Můžete přepsat originál nebo vytvořit zcela nový soubor.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

Po spuštění tohoto řádku `output.pdf` obsahuje původní obsah plus viditelný Bates štítek na každé stránce—přesně to, co očekáváte, když **how to generate bates** pro soubor případu.

## Kompletní, spustitelný příklad

Spojením všech částí získáte kompletní úryvek, který můžete zkopírovat a vložit do konzolové aplikace:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Očekávaný výsledek

Otevřete `output.pdf` v libovolném prohlížeči (Adobe Reader, Edge, atd.). Uvidíte, že každá stránka je označena něčím jako **CASE-001000**, **CASE-001001**, … až po poslední stránku. Čísla jsou umístěna pevně v pravém dolním rohu, podle nastavených možností.

## Časté otázky a řešení problémů

- **„Co když je můj PDF chráněn heslem?“**  
  Načtěte jej s heslem: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **„Mohu přidat Bates čísla do nově vytvořeného PDF?“**  
  Rozhodně. Stačí nejprve vytvořit dokument (`var doc = new Document();`) a pak postupovat podle kroků 2‑4 před uložením.

- **„Je písmo vždy vloženo?“**  
  Aspose automaticky vloží písmo, pokud již není v PDF. Pokud potřebujete konkrétní rodinu písma, nastavte `options.Font` podle toho.

- **„Jaký je výkon u souborů s 10 000 stránkami?“**  
  Knihovna streamuje stránky, takže využití paměti zůstává skromné. Přesto můžete zvýšit `PdfSaveOptions.CompressionMode` pro rychlejší I/O.

## Pro tipy pro produkční použití

1. **Batch processing:** Zabalte výše uvedenou logiku do smyčky, která prochází složku s PDF soubory. Použijte `Directory.GetFiles("*.pdf")` a zpracujte každý soubor samostatně.
2. **Logging:** Vypište první a poslední Bates čísla do log souboru—pomáhá auditorům ověřit, že číslování bylo kontinuální.
3. **Error handling:** Oblečte celý blok do `try/catch` a zobrazte jasnou zprávu, pokud chybí nebo je poškozený zdrojový PDF.
4. **Zero‑padding flexibility:** Pokud potřebujete dynamický počet číslic na základě celkového počtu stránek, vypočítejte `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Závěr

Právě jsme ukázali, jak **create PDF document C#** a bez problémů **add Bates numbering**—od počátečního načtení až po finální uložení. Krátký příklad demonstruje **how to add bates**, **add sequential page numbers**, a **how to generate bates** s vlastními předponami a nulovým doplněním. S několika úpravami můžete tento vzor přizpůsobit dávkovým úlohám, různým rozvržením nebo jej dokonce integrovat do webového API, které na vyžádání vrátí čerstvě očíslovaný PDF.

Jste připraveni na další krok? Zkuste kombinovat toto s funkcí **watermark** od Aspose, nebo vygenerujte souhrnný index, který uvádí každé Bates číslo spolu s krátkým popisem obsahu stránky. Možnosti jsou neomezené a kód, který nyní máte, je pevnou základnou pro jakýkoli workflow automatizace dokumentů.

Šťastné programování a ať jsou vaše PDF vždy perfektně očíslované! 

![Snímek obrazovky PDF prohlížeče zobrazující create pdf document c# s aplikovanými Bates čísly](image-placeholder.png "create pdf document c# s Bates čísly")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}