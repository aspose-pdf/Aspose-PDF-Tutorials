---
category: general
date: 2026-06-30
description: Jak přidat razítko do PDF pomocí Aspose.PDF a automaticky přizpůsobit
  text v PDF. Krok za krokem tutoriál s kompletním kódem, vysvětleními a tipy.
draft: false
keywords:
- how to add stamp pdf
- adjust font size to fit
- auto‑fit text in pdf
language: cs
og_description: Jak snadno přidat razítko do PDF. Naučte se upravit velikost písma
  tak, aby se vešlo, a automaticky přizpůsobit text v PDF pomocí Aspose.PDF během
  několika minut.
og_title: Jak přidat razítko PDF – Návod na automatické přizpůsobení textu
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to add stamp pdf using Aspose.PDF and auto‑fit text in pdf. Step‑by‑step
    tutorial with full code, explanations, and tips.
  headline: How to add stamp pdf – Complete guide with auto‑fit text
  type: TechArticle
- description: How to add stamp pdf using Aspose.PDF and auto‑fit text in pdf. Step‑by‑step
    tutorial with full code, explanations, and tips.
  name: How to add stamp pdf – Complete guide with auto‑fit text
  steps:
  - name: Expected Output
    text: Open `autoFontStamp.pdf` in any PDF viewer. You should see a rectangular
      label on the first page, **exactly 300 × 100 points**, containing the phrase
      “Long text that must fit”. If the original string is longer than the rectangle
      can accommodate at the default font size, you’ll notice the text has sh
  - name: 1. Multiple Stamps on One Page
    text: If you need several annotations, simply repeat the `AddStamp` call with
      different `TextStamp` instances. Remember to adjust `XIndent` and `YIndent`
      to position each stamp.
  - name: 2. Changing Font Family or Color
    text: 'You can customize the appearance via the `TextState` property:'
  - name: 3. Using Images Instead of Text
    text: Aspose also supports `ImageStamp`. The same auto‑fit logic doesn’t apply,
      but you can manually size the image to the stamp rectangle.
  type: HowTo
tags:
- pdf
- aspnet
- stamp
- font-size
title: Jak přidat razítko do PDF – Kompletní průvodce s automatickým přizpůsobením
  textu
url: /cs/net/programming-with-stamps-and-watermarks/how-to-add-stamp-pdf-complete-guide-with-auto-fit-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat razítko PDF – Kompletní průvodce s Auto‑Fit Text

Jak přidat razítko PDF je častá otázka, kdykoli potřebujete anotovat dokument bez otevření GUI editoru. Už jste někdy zkusili umístit dlouhý popisek na stránku PDF a sledovali, jak přesahuje okraje? V tomto tutoriálu tento problém vyřešíme pomocí **Aspose.PDF for .NET** a ukážeme vám, jak **automaticky upravit velikost písma tak, aby se vešla**.

Projdeme každý řádek kódu, vysvětlíme, proč je každé nastavení důležité, a skončíme plně funkčním PDF, které dokazuje, že razítko se skutečně zmenší (nebo zvětší), aby zůstalo uvnitř svého obdélníku. Žádné vágní odkazy – jen konkrétní řešení copy‑and‑paste, které můžete spustit ještě dnes.

## Co budete potřebovat

* **.NET 6.0** nebo novější (kód také funguje na .NET Framework 4.7+).  
* Balíček **Aspose.Pdf** NuGet (`Install-Package Aspose.Pdf`).  
* PDF soubor pojmenovaný `input.pdf` umístěný ve složce, na kterou můžete odkazovat (nazveme ji `YOUR_DIRECTORY`).  
* Jakékoliv IDE, které chcete – Visual Studio, Rider nebo i VS Code bude stačit.

A to je vše. Žádné externí služby, žádné licenční triky (Aspose nabízí bezplatný zkušební klíč, který můžete vložit pro testování). Připravení? Pojďme na to.

## Jak přidat razítko PDF – Krok 1: Načtení zdrojového dokumentu

Prvním krokem je otevřít PDF, které chcete upravit. Aspose.PDF zachází se souborem jako s objektem `Document`, který vám poskytuje přístup ke stránkám, anotacím a samozřejmě k razítkům.

```csharp
using Aspose.Pdf;

// Step 1: Open the source PDF document
using (var document = new Document(@"YOUR_DIRECTORY\input.pdf"))
{
    // The using‑statement ensures the file is closed properly.
```

> **Proč je to důležité:**  
> Otevření dokumentu uvnitř bloku `using` zaručuje uvolnění všech souborových handle, což zabraňuje chybám „soubor uzamčen“, když se později pokusíte PDF uložit nebo smazat.

## Přizpůsobení velikosti písma – Konfigurace TextStamp

Nyní vytvoříme objekt `TextStamp`. Toto je část, která se skutečně objeví na stránce. Magie nastane, když povolíme **AutoAdjustFontSizeToFitStampRectangle** a nastavíme hodnotu přesnosti.

```csharp
    // Step 2: Create a text stamp and enable automatic font size adjustment
    var stamp = new TextStamp("Long text that must fit")
    {
        // Shrink or expand text to fit the stamp area automatically
        AutoAdjustFontSizeToFitStampRectangle = true,

        // Precision for the size calculation (0.01 = 1% tolerance)
        AutoAdjustFontSizePrecision = 0.01f,

        // Define the rectangle that the stamp must stay inside
        Width = 300,   // points (approx 4.2 inches)
        Height = 100,  // points (approx 1.4 inches)

        // Keep the original text scaling; we only want font size to change
        Scale = false
    };
```

> **Tip:** Pokud pracujete s vícejazyčným textem, také nastavte `stamp.TextState.Font = FontRepository.FindFont("Arial Unicode MS");`, abyste se vyhnuli problémům s chybějícími glyfy.

> **Proč to funguje:**  
> `AutoAdjustFontSizeToFitStampRectangle` říká Aspose, aby vypočítal největší možnou velikost písma, která stále zapadne do obdélníku definovaného pomocí `Width` a `Height`. `AutoAdjustFontSizePrecision` určuje, jak podrobný je tento výpočet – menší čísla znamenají těsnější přizpůsobení, ale mírně delší dobu zpracování.

## Auto‑fit text in pdf – Přidání razítka na stránku

Po nakonfigurování razítka je dalším krokem umístit jej na konkrétní stránku. V tomto příkladu použijeme první stránku, ale můžete cílit na libovolný index (`document.Pages[3]` pro třetí stránku, například).

```csharp
    // Step 3: Add the stamp to the first page of the PDF
    document.Pages[1].AddStamp(stamp);
```

> **Častá otázka:** *Co když PDF nemá žádné stránky?*  
> Aspose vyhodí `ArgumentOutOfRangeException`. Rychlá kontrola (`if (document.Pages.Count == 0) throw new InvalidOperationException("PDF is empty.");`) učiní kód odolným.

## Uložení PDF – Ověření výsledku

Nakonec zapíšeme změny zpět na disk. Název výstupního souboru jasně ukazuje, že velikost písma razítka byla automaticky upravena.

```csharp
    // Step 4: Save the modified PDF with the auto‑adjusted stamp
    document.Save(@"YOUR_DIRECTORY\autoFontStamp.pdf");
} // End of using block – document is disposed here
```

### Očekávaný výstup

Otevřete `autoFontStamp.pdf` v libovolném prohlížeči PDF. Měli byste vidět obdélníkový popisek na první stránce, **přesně 300 × 100 bodů**, obsahující frázi „Long text that must fit“. Pokud je původní řetězec delší, než obdélník může při výchozí velikosti písma pojmout, všimnete si, že text se zmenšil právě natolik, aby zůstal uvnitř – žádné ořezání, žádný přetečení.

![Screenshot of PDF with auto‑fit stamp](https://example.com/auto-fit-stamp.png "auto‑fit text in pdf example")  
*Alt text: Screenshot of PDF with auto‑fit stamp showing adjusted font size.*

## Okrajové případy a varianty

### 1. Více razítek na jedné stránce

Pokud potřebujete několik anotací, jednoduše opakujte volání `AddStamp` s různými instancemi `TextStamp`. Nezapomeňte upravit `XIndent` a `YIndent` pro umístění každého razítka.

```csharp
stamp.XIndent = 50;   // horizontal offset from the left edge
stamp.YIndent = 150;  // vertical offset from the bottom edge
document.Pages[1].AddStamp(stamp);
```

### 2. Změna rodiny písma nebo barvy

Můžete přizpůsobit vzhled pomocí vlastnosti `TextState`:

```csharp
stamp.TextState.Font = FontRepository.FindFont("Times New Roman");
stamp.TextState.FontSize = 12; // base size; auto‑adjust will override if needed
stamp.TextState.ForegroundColor = Color.FromRgb(255, 0, 0); // red text
```

### 3. Použití obrázků místo textu

Aspose také podporuje `ImageStamp`. Stejná logika automatického přizpůsobení se nepoužije, ale můžete ručně nastavit velikost obrázku na obdélník razítka.

```csharp
var imgStamp = new ImageStamp(@"YOUR_DIRECTORY\logo.png")
{
    Width = 200,
    Height = 80,
    XIndent = 20,
    YIndent = 20
};
document.Pages[1].AddStamp(imgStamp);
```

## Praktické tipy z praxe

* **Nezakódovávejte cesty** – použijte `Path.Combine(Environment.CurrentDirectory, "input.pdf")` pro přenositelnost.  
* **Dávkové zpracování** – obalte celý postup do smyčky `foreach (var file in Directory.GetFiles(...))`, abyste automaticky razítkovali desítky PDF.  
* **Výkon** – pokud zpracováváte velké PDF, zvažte vypnutí `AutoAdjustFontSizePrecision` (nastavte na `0.05f`), aby se urychlil výpočet s neznatelným vizuálním rozdílem.  
* **Testování** – vždy otevřete výsledné PDF po prvním spuštění, abyste potvrdili, že rozměry obdélníku jsou takové, jaké očekáváte. Rychlá vizuální kontrola ušetří hodiny ladění později.

## Závěr

Nyní máte kompletní řešení copy‑and‑paste pro **jak přidat razítko PDF**, které automaticky **upravit velikost písma tak, aby se vešla** a dosáhnout **auto‑fit text in pdf** pomocí Aspose.PDF. Načtením dokumentu, konfigurací `TextStamp` s povoleným automatickým přizpůsobením, umístěním na požadovanou stránku a uložením souboru můžete programově anotovat PDF bez obav o přetečení textu.

Co dál? Zkuste kombinovat tuto techniku s datově řízenými workflow – načtěte jména zákazníků z databáze a razítkujte každou fakturu ve smyčce. Nebo experimentujte s různými velikostmi obdélníku a podívejte se, jak se algoritmus automatického přizpůsobení chová u velmi krátkých versus extrémně dlouhých řetězců.

Máte nápad, který chcete sdílet? Zanechte komentář, nebo spusťte nový projekt a nechte magii automatického přizpůsobení pracovat. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak přidat textové razítko do PDF pomocí Aspose.PDF for .NET](/pdf/english/net/document-manipulation/add-text-stamp-pdf-aspose-dotnet/)
- [Jak přidat a zarovnat textová razítka v PDF pomocí Aspose.PDF for .NET | Vodoznaky a pozadí](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [Jak přidat obrázkové razítko do PDF pomocí Aspose.PDF for .NET: Kompletní průvodce](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}