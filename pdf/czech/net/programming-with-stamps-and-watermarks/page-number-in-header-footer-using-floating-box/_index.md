---
"description": "V tomto podrobném tutoriálu snadno přidáte čísla stránek do záhlaví a zápatí PDF pomocí plovoucího rámečku s Aspose.PDF pro .NET."
"linktitle": "Číslo stránky v záhlaví a zápatí pomocí plovoucího rámečku"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Číslo stránky v záhlaví a zápatí pomocí plovoucího rámečku"
"url": "/cs/net/programming-with-stamps-and-watermarks/page-number-in-header-footer-using-floating-box/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Číslo stránky v záhlaví a zápatí pomocí plovoucího rámečku

## Zavedení

Pokud jde o programovou správu PDF dokumentů, Aspose.PDF pro .NET vyniká jako výjimečný nástroj. Zjednodušuje způsob, jakým vytváříme, upravujeme a manipulujeme s PDF soubory v .NET aplikacích. Ať už generujete faktury, reporty nebo jakýkoli typ dokumentu, elegantní přidání čísel stránek může zlepšit profesionalitu a organizaci vašich PDF souborů. V tomto tutoriálu se ponoříme do toho, jak přidat čísla stránek do záhlaví a zápatí PDF pomocí plovoucího rámečku. Jste připraveni začít? Pojďme na to!

## Předpoklady

Než se pustíme do této vzrušující cesty do světa manipulace s PDF, je třeba mít několik věcí:

### Nastavení prostředí .NET
Ujistěte se, že máte vývojové prostředí .NET. Můžete použít Visual Studio, které je mezi vývojáři oblíbenou volbou pro aplikace .NET.

### Knihovna Aspose.PDF
Nainstalujte si knihovnu Aspose.PDF. Můžete si ji snadno stáhnout z webových stránek:

- [Stáhnout Aspose.PDF pro .NET](https://releases.aspose.com/pdf/net/)

### Základní znalost programování v C#
Základní znalost jazyka C# vám pomůže pochopit koncepty a úryvky kódu prezentované v tomto tutoriálu.

### Přístup k dokumentaci
Vždy je výhodné mít [Dokumentace Aspose.PDF](https://reference.aspose.com/pdf/net/) praktické pro referenci a hlubší prozkoumání případných dalších funkcí.

## Importovat balíčky

Pro zahájení budete muset do projektu importovat potřebné balíčky. Tím zajistíte, že sestava Aspose.PDF bude dostupná pro použití ve vašem kódu. Zde je návod, jak to udělat:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nyní si rozebereme proces přidávání čísel stránek pomocí plovoucího rámečku do snadno zvládnutelných kroků. Sledujte nás, jak jimi procházíme.

## Krok 1: Nastavení prostředí dokumentů

Začněme určením adresáře, kam bude váš PDF dokument uložen. To je klíčové, protože určuje, kam bude váš výstupní soubor uložen.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Nahradit `YOUR DOCUMENT DIRECTORY` s cestou dle vašeho výběru, kam chcete uložit výstupní soubor PDF.

## Krok 2: Vytvoření instance dokumentu

Dalším krokem je vytvoření nového PDF dokumentu. To zahrnuje použití `Document` třída z knihovny Aspose.PDF.

```csharp
// Vytvoření instance dokumentu
Aspose.Pdf.Document pdf = new Aspose.Pdf.Document();
```
Zde vytvoříme novou instanci třídy `Document` třída, která nám slouží jako plátno pro manipulaci.

## Krok 3: Přidání nové stránky

A teď přidejme stránku do našeho PDF dokumentu. Každý PDF soubor potřebuje alespoň jednu stránku, že?

```csharp
// Přidání stránky do dokumentu PDF
Aspose.Pdf.Page page = pdf.Pages.Add();
```
Tento úryvek kódu přidá do našeho dokumentu novou stránku, která ho připraví k přijímání obsahu, včetně plovoucího rámečku s čísly stránek.

## Krok 4: Vytvořte plovoucí rámeček

Dále je čas vytvořit plovoucí rámeček, který bude obsahovat číslo stránky. `FloatingBox` Třída nám umožňuje volně umisťovat obsah na stránku.

```csharp
// Inicializuje novou instanci třídy FloatingBox.
Aspose.Pdf.FloatingBox box1 = new Aspose.Pdf.FloatingBox(140, 80);
```
Zde jsou parametry `(140, 80)` Zadejte šířku a výšku plovoucího rámečku. Tyto hodnoty můžete upravit podle svých preferencí rozvržení.

## Krok 5: Umístění plovoucího rámečku

Umístění je klíčové! Chcete určit, kde se číslo stránky na stránce zobrazí. Budete pracovat s `Left` a `Top` vlastnosti pro určení pozice.

```csharp
// Hodnota s plovoucí čárkou, která označuje levou pozici odstavce
box1.Left = 2;
// Číslo s plovoucí čárkou, které označuje horní pozici odstavce
box1.Top = 10;
```
Tyto hodnoty určují umístění plovoucího rámečku na stránce. Nebojte se s nimi experimentovat a zjistěte, co pro váš dokument vypadá nejlépe.

## Krok 6: Přidání textu pomocí makra Číslo stránky

Nyní přidáme řetězec, který dynamicky zobrazuje číslo stránky. A tady se začne dít ta pravá magie!

```csharp
// Přidejte makra do kolekce odstavců FloatingBoxu
box1.Paragraphs.Add(new Aspose.Pdf.Text.TextFragment("Page: ($p/ $P )"));
```
V tomto případě, `($p/ $P)` je makro, které zobrazí aktuální číslo stránky (`$p`) a celkový počet stránek (`$P`). V důsledku toho formátuje text tak, aby zněl například „Strana: 1/5“.

## Krok 7: Přidání plovoucího rámečku na stránku

Je čas přidat plovoucí rámeček spolu s textem čísla stránky na naši nově vytvořenou stránku.

```csharp
// Přidejte na stránku plovoucí pole (floatingBox).
page.Paragraphs.Add(box1);
```
Tento řádek v podstatě vloží váš plovoucí rámeček do stránky, čímž se stane součástí rozvržení dokumentu. 

## Krok 8: Uložte dokument

Nakonec nezapomeňte uložit svou práci! Posledním krokem je uložení PDF dokumentu se správným názvem souboru.

```csharp
// Uložit dokument
pdf.Save(dataDir + "PageNumberinHeaderFooterUsingFloatingBox_out.pdf");
```
Ujistěte se, že zadaná cesta obsahuje požadovaný název souboru. Nyní je váš úžasný PDF s čísly stránek vytvořen! 

## Závěr

tady to máte, lidi! Přidání čísel stránek do záhlaví a zápatí vašeho PDF souboru pomocí Aspose.PDF pro .NET je tak jednoduché. S pouhými několika řádky kódu jste se vydali na cestu k zvládnutí zpracování dokumentů ve vašich aplikacích. Neváhejte experimentovat s různými rozvrženími a formátováním – koneckonců, kreativita nezná mezí! Jste připraveni vytvořit profesionální dokument? Popadněte programátorskou čepici a začněte experimentovat.

## Často kladené otázky

### Mohu si přizpůsobit vzhled textu čísla stránky?  
Ano, vlastnosti textu, jako je velikost písma, barva a styl, můžete přizpůsobit úpravou `TextFragment` vlastnosti.

### Je Aspose.PDF zdarma k použití?  
Ačkoliv Aspose.PDF nabízí bezplatnou zkušební verzi, jedná se o placený produkt pro produkční použití. Můžete [kupte si to zde](https://purchase.aspose.com/buy).

### Kde najdu podrobnější dokumentaci?  
Komplexní dokumentaci naleznete na [Dokumentační stránka Aspose.PDF](https://reference.aspose.com/pdf/net/).

### Jak mohu použít záhlaví a zápatí na více stránek?  
Můžete procházet všechny stránky v dokumentu a na každou z nich podobným způsobem aplikovat plovoucí rámeček.

### Co když potřebuji podporu pro další funkce?  
V případě dalších dotazů nebo potřeby podpory můžete navštívit [Fórum Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}