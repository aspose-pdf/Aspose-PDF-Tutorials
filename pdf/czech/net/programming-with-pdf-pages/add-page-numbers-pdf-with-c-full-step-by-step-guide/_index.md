---
category: general
date: 2026-01-02
description: Rychle přidejte čísla stránek do PDF pomocí Aspose.Pdf v C#. Naučte se
  přidávat číslování Bates, text zápatí, vlastní vodoznak a procházet stránky PDF
  v jednom skriptu.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: cs
og_description: Okamžitě přidejte číslování stránek do PDF pomocí Aspose.Pdf. Tento
  průvodce také zahrnuje přidání Batesova číslování, textu v zápatí, vlastního vodoznaku
  a procházení stránek PDF.
og_title: Přidání číslování stránek do PDF pomocí C# – Kompletní programovací tutoriál
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Přidání číslování stránek do PDF pomocí C# – Kompletní krok za krokem návod
url: /cs/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání číslování stránek PDF pomocí C# – Kompletní programovací tutoriál

Už jste někdy potřebovali **přidat číslování stránek PDF** souborům, ale nevedeli jste, kde začít? Nejste v tom sami – vývojáři se neustále ptají, jak otisknout čísla, zápatí nebo dokonce identifikátor ve stylu Bates na každou stránku PDF.

V tomto tutoriálu uvidíte připravený příklad v C#, který **prochází stránky PDF**, přidává zápatí s číslem stránky a (pokud chcete) přidává vlastní vodoznak. Ukážeme vám také, jak přepnout otisk na Bates‑číslo, což je jen elegantní způsob, jak „přidat Bates‑číslování“ pro právní nebo forenzní dokumenty. Na konci budete mít jedinou, znovupoužitelnou metodu, která zvládne všechny tyto úkoly bez potíží.

## Přidání číslování stránek PDF – Přehled

Než se ponoříme do kódu, objasníme, co ve světě Aspose.Pdf opravdu znamená „přidat číslování stránek PDF“. Knihovna považuje jakýkoli kus textu umístěný na stránku za **TextStamp**. Vytvořením jednoho otisku s zástupcem stránky (`{page}`) a jeho aplikací na každou stránku získáte automaticky sekvenční číslování. Stejný otisk může nést další text, takže můžete **přidat text zápatí** jako „Confidential“ nebo specifický identifikátor případu.

> **Proč použít otisk místo úpravy PDF streamu?**  
> Otisky jsou vysoce úrovňové objekty, které respektují okraje stránky, otočení a existující grafiku. Navíc jsou mnohem snazší na údržbu – stačí změnit pár vlastností a skript spustit znovu.

## Procházení stránek PDF a aplikace otisků

Prvním praktickým krokem je otevřít zdrojové PDF a iterovat přes jeho stránky. Jedná se o klasický **loop through pdf pages** vzor, který používá většina příkladů Aspose.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Tip:** Pokud je vaše PDF obrovské (stovky stránek), zvažte zpracování po dávkách, aby se snížila spotřeba paměti. Aspose.Pdf načítá stránky líně, takže samotná smyčka je již poměrně efektivní.

## Přidání Bates‑číslování a textu zápatí

Nyní, když můžeme projít každou stránku, vytvoříme **znovupoužitelný TextStamp**, který nese jak číslo stránky, tak volitelný text zápatí. Zástupce `{page}` je automaticky nahrazen aktuálním číslem stránky.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Proč to funguje

* **`Bates-{page}`** – Aspose nahradí `{page}` skutečným číslem stránky a automaticky vytvoří klasické Bates‑číslo.
* **`Confidential`** – Toto je část **add footer text**. Můžete ji nahradit libovolným řetězcem, dokonce načíst data z databáze.
* **Styling** – Použitím `TextState` můžete upravit barvu, průhlednost a dokonce otočení, aniž byste zasahovali do vnitřních PDF streamů.

Pokud potřebujete jen prostá čísla, odstraňte předponu „Bates‑“ a nadbytečný text:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Přidání vlastního vodoznaku (volitelné)

Někdy chcete víc než jen zápatí – potřebujete poloprůhledné logo nebo překrytí „DRAFT“ přes celou stránku. Zde vstupuje **add custom watermark**. Stejnou třídu `TextStamp` můžete přeuspořádat, jen změňte zarovnání a průhlednost.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Poznámka:** Pořadí je důležité. Přidání vodoznaku jako první zajistí, že čísla stránek zůstanou čitelná nad poloprůhledným textem.

## Uložení PDF a ověření výsledků

Po otisku je posledním krokem zapsat změny zpět na disk. Volání `Save`, které jsme umístili dříve, provede těžkou práci, ale přidáme rychlý ověřovací úryvek, který otevře nový soubor a vypíše, kolik stránek bylo zpracováno.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Když spustíte celý program, měli byste vidět PDF, kde každá stránka končí něčím jako **„Bates‑3 – Confidential“** (nebo jen „3“, pokud jste použili jednoduchý otisk) a pokud jste povolili vodoznak, jemné „DRAFT“ uprostřed.

### Očekávaný výstup

| Strana | Zápatí (příklad) |
|--------|-------------------|
| 1      | Bates‑1 – Confidential |
| 2      | Bates‑2 – Confidential |
| …      | … |
| N      | Bates‑N – Confidential |

Pokud soubor otevřete v prohlížeči, čísla budou umístěna 20 pt od levého a spodního okraje, což odpovídá typickým konvencím právních dokumentů.

## Kompletní funkční příklad (připravený ke kopírování)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Uložte tento soubor jako `AddPageNumbers.cs`, obnovte NuGet balíček Aspose.Pdf (`Install-Package Aspose.Pdf`) a spusťte jej. Získáte **přidat číslování stránek PDF** soubor, který zároveň demonstruje **add bates numbering**, **add footer text**, **add custom watermark** a klasický **loop through pdf pages** vzor – vše v jednom úhledném skriptu.

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## Závěr

Probrali jsme vše, co potřebujete k **přidání číslování stránek PDF** souborům pomocí Aspose.Pdf v C#. Od procházení každé stránky, přes otisk Bates‑čísel, přidání vlastního textu zápatí až po vrstvení poloprůhledného vodoznaku, kód je dostatečně kompaktní, aby jej šlo vložit do jakéhokoli existujícího projektu.

Dále můžete zkoumat pokročilejší scénáře – například načítání textu zápatí z databáze, použití různých fontů podle sekce nebo generování samostatného indexového PDF, který vypíše všechna Bates‑čísla. Všechny tyto rozšíření staví na stejných základních myšlenkách, které jsme zde ukázali, takže jste dobře připraveni rozšířit řešení podle rostoucích požadavků.

Vyzkoušejte to, upravte stylování a dejte mi vědět v komentářích, jak to u vás fungovalo. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}