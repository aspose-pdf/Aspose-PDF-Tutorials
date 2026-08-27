---
category: general
date: 2026-02-14
description: Jednoduše přidejte Batesovo číslování PDF do svých dokumentů. Naučte
  se, jak přidat čísla stránek do zápatí a sekvenční čísla do PDF pomocí Aspose.Pdf
  během několika minut.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: cs
og_description: Rychle přidejte Batesovo číslování PDF. Tento průvodce ukazuje, jak
  pomocí Aspose.Pdf přidat čísla stránek do zápatí a sekvenční čísla do PDF, s kompletním
  kódem a tipy.
og_title: Přidání Batesova číslování PDF – krok za krokem C# tutoriál
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Přidání Batesova číslování do PDF – Kompletní C# průvodce
url: /cs/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

text. Ensure we keep code block placeholders unchanged.

Let's produce the translated content.

Check for any URLs inside text? Not present. There's no markdown links. So fine.

We need to translate headings, bullet points, paragraphs.

Also note "RTL formatting if needed" not needed.

Let's produce.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Bates číslování do PDF – Kompletní průvodce v C#

Už jste někdy potřebovali **přidat Bates číslování do PDF** souborů, ale nevedeli jste, kde začít? Nejste v tom sami. Právnické týmy, auditoři i všichni, kdo pracují s velkými sadami dokumentů, se neustále ptají: „Jak přidat Bates čísla, aniž by se rozbil layout?“ Dobrou zprávou je, že s Aspose.Pdf pro .NET můžete tato čísla vložit jako jednoduchý zápatí – žádná ruční úprava není potřeba.

V tomto tutoriálu projdeme praktickým, end‑to‑end řešením, které nejen **přidá čísla stránek do zápatí**, ale také vám umožní **přidat sekvenční čísla do PDF** souborů s vlastním prefixem, velikostí písma a zarovnáním. Na konci budete mít připravený spustitelný C# program, jasné pochopení, proč každé nastavení má význam, a několik tipů, jak se vyhnout nejčastějším úskalím.

## Co se naučíte

- Jak načíst existující PDF a připravit jej pro Bates číslování.  
- Které vlastnosti **BatesNumberingOptions** řídí vzhled a umístění.  
- Jak aplikovat číslování na každou stránku jedním voláním.  
- Jak přizpůsobit prefix, počáteční číslo a okraje pro různé právní formáty.  
- Řešení okrajových případů – co dělat s šifrovanými PDF nebo dokumenty, které již obsahují zápatí.

**Požadavky**: .NET 6+ (nebo .NET Framework 4.7+), aktuální verze Aspose.Pdf (v příkladu je použita 23.10) a vstupní PDF, ke kterému máte právo upravovat. Žádné další knihovny třetích stran nejsou potřeba.

---

## Krok 1 – Načtení PDF, které chcete očíslovat

Prvním krokem je vytvořit instanci `Document`, která ukazuje na zdrojový soubor. Použití vzoru `using var` zajistí automatické uvolnění souborového handle.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Proč je to důležité:** Aspose.Pdf načte celou strukturu PDF do paměti, což nám umožní manipulovat se stránkami, anotacemi i metadaty, aniž bychom se dotkli původního souboru na disku. Pokud je PDF chráněno heslem, můžete heslo předat konstruktoru – viz poznámka „Šifrovaná PDF“ na konci.

---

## Krok 2 – Definování možností Bates číslování

Bates čísla jsou v podstatě zápatí stránek s konfigurovatelným prefixem a sekvenčním čítačem. Třída `BatesNumberingOptions` vám umožní doladit každý vizuální aspekt.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Rychlý tip

- **Prefix**: Použijte krátký, jedinečný identifikátor (např. číslo případu), aby bylo zápatí čitelné.  
- **StartNumber**: Právnické firmy často začínají od `1` nebo od vlastního offsetu; zvolte to, co odpovídá vašemu systému archivace.  
- **Margins**: Spodní okraj `20` bodů udržuje text mimo poznámky pod čarou nebo podpisy, které mohou být již blízko okraje stránky.

---

## Krok 3 – Aplikace číslování na všechny stránky

Po nastavení možností je samotná injekce jedním řádkem. Aspose.Pdf se postará o stránkování, aktualizuje existující obsahové proudy a automaticky respektuje otočení stránky.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **Co se děje pod kapotou?** Knihovna iteruje přes každý objekt `Page`, vytvoří `TextFragment`, který obsahuje prefix a aktuální čítač, a vykreslí jej pomocí souřadnicového systému stránky. Protože jsme nastavili `HorizontalAlignment.Right` a `VerticalAlignment.Bottom`, text se přichytí do pravého dolního rohu bez ohledu na velikost stránky.

---

## Krok 4 – Uložení upraveného PDF

Nakonec výsledek zapíšeme do nového souboru. Přepsání originálu je možné, ale uchování kopie pomáhá při správě verzí.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Pokud potřebujete zachovat původní metadata (autor, datum vytvoření), Aspose.Pdf je standardně kopíruje. Můžete také zadat objekt `SaveOptions` pro soulad s PDF/A nebo kompresi.

---

## Kompletní funkční příklad

Níže je kompletní, připravený k spuštění program. Vložte jej do projektu konzolové aplikace, upravte cesty k souborům a stiskněte **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Očekávaný výsledek:** Každá stránka souboru `output.pdf` nyní zobrazuje zápatí jako `ABC-1000`, `ABC-1001`, … umístěné v pravém dolním rohu. Otevřete soubor v libovolném PDF prohlížeči a ověřte.

---

## Řešení běžných variant

### Přidání pouze čísel stránek do zápatí

Pokud potřebujete jen jednoduchá čísla stránek bez prefixu, nastavte `Prefix = ""` a případně upravte okraj, aby nedošlo ke kolizi s existujícími zápatími.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Použití jiného zarovnání

Právnické dokumenty někdy vyžadují číslo uprostřed dole. Změňte zarovnání:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Práce se šifrovanými PDF

Když je zdrojové PDF chráněno heslem, předávejte heslo takto:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

Zbytek pracovního postupu zůstává stejný.

### Přeskočení existujících zápatí

Pokud dokument již obsahuje zápatí, které nechcete přepsat, můžete předřadit vlastní řetězec, aby nové číslo bylo odlišné, nebo můžete iterovat stránky ručně a přidat `TextFragment` jen tam, kde zápatí chybí. Třída `Page` poskytuje kolekce `Annotations` a `Contents` pro detailní kontrolu.

---

## Pro tipy a úskalí

- **Vyhněte se oříznutí**: Velmi malé spodní okraje mohou způsobit, že se text ořízne při tisku. Otestujte na fyzickém výtisku, pokud budete distribuovat papírové kopie.  
- **Výkon**: Přidání Bates číslování do 500‑stránkového PDF trvá pod sekundu na moderním notebooku, ale velké dávky těží z paralelního zpracování – pamatujte, že `Document` není thread‑safe, takže každé vlákno potřebuje vlastní instanci.  
- **Kompatibilita verzí**: Kód funguje s Aspose.Pdf 23.10 a novějšími. Ve starších verzích jsou názvy vlastností stejné, ale konstruktor `MarginInfo` může vyžadovat argumenty typu `float`.  
- **Právní shoda**: Některé jurisdikce vyžadují umístění Bates čísla na konkrétní místo (např. dole vlevo). Upravit `HorizontalAlignment` podle potřeby.

---

## Závěr

Ukázali jsme, jak **přidat Bates číslování do PDF** souborů pomocí Aspose.Pdf pro .NET, od načtení dokumentu až po uložení finální verze s čistým zápatím. Úpravou několika vlastností můžete také **přidat čísla stránek do zápatí**, **přidat sekvenční čísla do PDF** nebo přizpůsobit vzhled tak, aby vyhovoval jakémukoli právnímu standardu.

Jste připraveni na další krok? Zkuste zkombinovat tuto techniku s OCR extrakcí textu a vložit vyhledávatelná klíčová slova vedle vašich Bates čísel, nebo automatizujte proces pro celé složky pomocí `Directory.GetFiles`. Možnosti jsou neomezené a základ, který nyní máte, usnadní všechny další rozšíření.

Šťastné programování a ať jsou vaše PDF vždy perfektně očíslovaná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}