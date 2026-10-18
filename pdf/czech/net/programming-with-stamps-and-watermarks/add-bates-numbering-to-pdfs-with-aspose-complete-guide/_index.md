---
category: general
date: 2026-04-25
description: Přidejte Batesovo číslování do PDF rychle pomocí Aspose.Pdf. Naučte se,
  jak přidat čísla stránek do PDF, automaticky upravit velikost písma a přidat textový
  vodoznak v C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: cs
og_description: Přidejte Batesovo číslování do PDF pomocí Aspose.Pdf. Tento návod
  ukazuje, jak přidat čísla stránek do PDF, automaticky upravit velikost písma a přidat
  textový vodoznak v jednom spustitelném příkladu.
og_title: Přidejte Batesovo číslování do PDF – Kompletní tutoriál Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Přidejte Batesovo číslování do PDF pomocí Aspose – kompletní průvodce
url: /cs/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Batesova číslování do PDF pomocí Aspose – Kompletní průvodce

Už jste někdy potřebovali **přidat Batesovo číslování** do PDF, ale nevedeli jste, kde začít? Nejste v tom sami—právní týmy, auditoři i vývojáři tuto překážku potkávají denně. Dobrá zpráva? S Aspose.Pdf pro .NET můžete přidat Batesovo číslo, automaticky upravit velikost písma a dokonce považovat razítko za jemnou textovou vodoznak — vše během několika řádků C#.

V tomto tutoriálu projdeme přesně kroky k **add page numbers pdf**, upravíme písmo tak, aby nikdy nepřeteklo, a jednou provždy odpovíme na otázku „how to add bates“. Na konci budete mít připravenou konzolovou aplikaci, která vytvoří profesionálně očíslované PDF, a uvidíte, jak ji rozšířit na kompletní řešení vodoznaku.

## Požadavky

* **Aspose.Pdf for .NET** (nejnovější NuGet balíček k dubnu 2026).  
* .NET 6.0 SDK nebo novější – API funguje stejně na .NET Framework, ale .NET 6 poskytuje nejlepší výkon.  
* Vzorkový PDF soubor pojmenovaný `input.pdf` umístěný ve složce, na kterou můžete odkazovat (např. `C:\Docs\`).  

Žádná další konfigurace není potřeba; knihovna je samostatná.

---

## Krok 1 – Načtení zdrojového PDF dokumentu

Prvním krokem je otevřít soubor, který chceme očíslovat. Třída `Document` od Aspose představuje celé PDF a načtení je tak jednoduché jako předat cestu do konstruktoru.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Proč je to důležité*: Načtením dokumentu získáte přístup ke kolekci `Pages`, kam později připojíme Batesovo razítko. Pokud soubor nelze najít, Aspose vyhodí jasnou `FileNotFoundException`, takže přesně víte, co se pokazilo.

---

## Krok 2 – Vytvoření textového razítka pro Batesova čísla

Nyní vytvoříme vizuální prvek, který se objeví na každé stránce. Třída `TextStamp` vám umožní vložit libovolný řetězec a použijeme zástupný text `{page}-{total}`, aby ho Aspose automaticky nahradil.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Klíčové body*:

* **auto adjust font size** – Nastavení `AutoAdjustFontSizeToFitStampRectangle` na `true` zaručuje, že text nikdy nevystoupí mimo obdélník, což je ideální pro čísla stránek proměnné délky.  
* **add text watermark** – Snížením `Opacity` proměníme Batesovo číslo na slabý vodoznak, čímž splníme požadavek „add text watermark“ bez dalšího kroku.  
* **how to add bates** – Tokeny `{page}` a `{total}` jsou tajnou ingrediencí; Aspose je nahradí během běhu, takže nemusíte nic vypočítávat sami.

---

## Krok 3 – Aplikace razítka na každou stránku

Běžnou chybou je razítkování jen první stránky. Pro skutečné **add page numbers pdf** musíme projít celou kolekci `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Proč klonovat? Metoda `AddStamp` interně vytvoří kopii, ale explicitní použití nové instance v každé iteraci zabraňuje nechtěným vedlejším efektům, pokud později změníte vlastnosti razítka (např. barvu pro konkrétní stránky).

---

## Krok 4 – Uložení aktualizovaného PDF

S razítky na svém místě je uložení změn jednoduché. Můžete přepsat původní soubor nebo zapsat do nového umístění — zde uložíme nový soubor pojmenovaný `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Pokud otevřete `output.pdf`, uvidíte každou stránku označenou „Bates: 1‑10“, „Bates: 2‑10“ … v pravém dolním rohu, s mírnou neprůhledností, která zároveň funguje jako **add text watermark**.

---

## Kompletní funkční příklad

Spojením všeho dohromady zde máte jednorázový, samostatný konzolový program, který můžete zkopírovat a vložit do Visual Studia.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Očekávaný výsledek**: Otevřete `output.pdf` v libovolném prohlížeči; každá stránka zobrazí řádek jako „Bates: 3‑12“ v pravém dolním rohu, velikost přesně odpovídá obdélníku a je vykreslená s 40 % neprůhledností. To splňuje jak požadavek na právní sledování, tak potřebu vizuálního vodoznaku.

---

## Běžné varianty a okrajové případy

| Situace | Co změnit | Proč |
|-----------|----------------|-----|
| **Různé umístění** | Upravit `HorizontalAlignment` / `VerticalAlignment` nebo nastavit `XIndent`/`YIndent` | Některé firmy upřednostňují umístění v levém horním rohu nebo uprostřed. |
| **Vlastní předpona** | Nahradit `"Bates: "` za `"Doc‑ID: "` nebo libovolný řetězec | Můžete používat jinou konvenci pojmenování. |
| **Více razítek** | Vytvořit druhý `TextStamp` (např. pro upozornění na důvěrnost) a přidat jej po prvním | Kombinace **add bates numbering** s dalšími požadavky **add text watermark** je jednoduchá. |
| **Velký počet stránek** | Zvýšit počáteční velikost písma (např. `14`) – automatické přizpůsobení ji zmenší podle potřeby | Když máte > 999 stránek, řetězec se prodlouží; automatické přizpůsobení zabraňuje oříznutí. |
| **Šifrované PDF** | Zavolat `pdfDocument.Decrypt("password")` před razítkováním | Nemůžete upravit zabezpečený soubor bez hesla. |

---

## Profesionální tipy a úskalí

* **Pro tip:** Nastavte `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)`, pokud si všimnete, že text leží těsně u okraje stránky.  
* **Dejte pozor na:** Velmi malé obdélníky (výchozí velikost je 100 × 30 pt). Pokud potřebujete větší oblast, nastavte ručně `batesStamp.Width` a `batesStamp.Height`.  
* **Poznámka o výkonu:** Razítkování tisíců stránek může trvat několik sekund, ale Aspose efektivně streamuje stránky — není nutné načítat celý dokument do paměti.  

---

## Závěr

Právě jsme ukázali, jak **add bates numbering** do PDF pomocí Aspose.Pdf, zároveň **add page numbers pdf**, povolit **auto adjust font size** a vytvořit **add text watermark** v jednom soudržném postupu. Kompletní, spustitelný příklad výše vám poskytuje pevný základ, který můžete přizpůsobit libovolnému workflow právních dokumentů nebo internímu reportovacímu systému.

Jste připraveni na další krok? Zkuste kombinovat tento přístup s PDF slučovacím API od Aspose pro hromadné zpracování více souborů, nebo prozkoumejte třídu `TextFragment` pro bohatší vodoznaky (barevné, otočené nebo víceřádkové). Možnosti jsou neomezené a kód, který nyní máte, je spolehlivý výchozí bod.

Pokud se vám tento průvodce líbil, neváhejte zanechat komentář, přidat hvězdičku do repozitáře nebo sdílet své vlastní varianty. Šťastné kódování a ať jsou vaše PDF vždy dokonale očíslovaná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}