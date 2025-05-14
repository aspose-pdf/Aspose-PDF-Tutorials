---
"description": "Naučte se, jak vyhledávat a získávat text ze všech stránek dokumentu PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Vyhledat a získat text vše"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vyhledat a získat text vše"
"url": "/cs/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vyhledat a získat text vše

## Zavedení

Potřebovali jste někdy extrahovat konkrétní text z PDF, ale shledali jste to složitým? PDF soubory se někdy mohou jevit jako uzamčené kontejnery, což ztěžuje získání potřebných informací. Ale tady je dobrá zpráva: s Aspose.PDF pro .NET můžete snadno vyhledávat a načítat text z jakéhokoli PDF. Tato výkonná knihovna poskytuje vše, co potřebujete pro práci s PDF soubory ve vašich .NET aplikacích, takže extrakce textu je hračka. V tomto tutoriálu vás provedeme procesem vyhledávání a extrakce textu ze souboru PDF pomocí Aspose.PDF pro .NET. Ať už vytváříte nástroj pro analýzu textu, nebo jen potřebujete automatizovat extrakci dat z PDF sestav, jste na správném místě!

## Předpoklady

Než se pustíme do kódu, ujistěme se, že máte vše nastavené:

1. Aspose.PDF pro .NET: Budete si muset stáhnout a nainstalovat Aspose.PDF pro .NET. Můžete si ho stáhnout ze stránky pro stahování. [zde](https://releases.aspose.com/pdf/net/).
2. Prostředí .NET: Ujistěte se, že máte na vývojovém počítači nainstalováno rozhraní .NET Framework nebo .NET Core.
3. Základní znalost C##: Doporučuje se určitá znalost C# a práce s .NET projekty.
4. PDF dokument: Ukázkový PDF soubor, ze kterého budeme extrahovat text. V tomto příkladu použijeme `SearchAndGetTextFromAll.pdf`.

## Importovat balíčky

Než začnete psát jakýkoli kód, musíte do projektu importovat potřebné jmenné prostory, abyste mohli pracovat s Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Tyto jmenné prostory poskytují přístup k objektovému modelu dokumentu PDF a umožňují nám manipulovat s textem v souboru.

Rozdělme si celý proces na jednoduché kroky, abyste je mohli snadno sledovat.

## Krok 1: Nastavení adresáře dokumentů

Nejprve je třeba zadat cestu k adresáři, kde se nachází váš PDF soubor. To pomůže aplikaci najít soubor, ze kterého chcete text extrahovat.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- Ten/Ta/To `dataDir` proměnná by měla ukazovat na adresář, kde se nachází vaše `SearchAndGetTextFromAll.pdf` soubor je uložen.
- Nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou na vašem počítači.

## Krok 2: Otevřete dokument PDF

Dále otevřeme PDF dokument pomocí Aspose.PDF. `Document` objekt.

```csharp
// Otevřít dokument
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- Vytvoříme novou instanci `Document` třídu předáním úplné cesty k souboru PDF.
- Tím se PDF soubor načte do paměti a připraví ho ke zpracování.

## Krok 3: Vytvořte absorbér textu

Ten/Ta/To `TextFragmentAbsorber` Objekt se používá k vyhledávání konkrétního textu v PDF. V tomto případě budeme hledat slovo „text“.

```csharp
// Vytvořte objekt TextAbsorber pro nalezení všech výskytů vstupní hledané fráze.
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- Ten/Ta/To `TextFragmentAbsorber` je inicializován řetězcem `"text"`To znamená, že bude hledat všechny výskyty slova „text“ v dokumentu PDF.

## Krok 4: Přijměte absorbér pro všechny stránky

Nyní dáme PDF dokumentu pokyn, aby přijal absorbér a prohledal text na všech jeho stránkách.

```csharp
// Přijměte absorbér pro všechny stránky
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Ten/Ta/To `Accept` Metoda se použije na stránky dokumentu. Tato metoda prohledá všechny stránky a vyhledá zadaný text.

## Krok 5: Extrahování fragmentů textu

Jakmile absorbér naskenuje dokument, můžeme načíst extrahované textové fragmenty.

```csharp
// Získejte extrahované fragmenty textu
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- Ten/Ta/To `TextFragments` majetek `TextFragmentAbsorber` vrací kolekci všech fragmentů textu, které odpovídají hledanému výrazu.

## Krok 6: Procházení textových fragmentů

Nyní, když máme kolekci textových fragmentů, projdeme je smyčkou a extrahujeme z nich podrobnosti.

```csharp
// Procházejte fragmenty
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- Ten/Ta/To `foreach` smyčka iteruje skrz každý `TextFragment` ve sbírce.
- Vypíšeme různé vlastnosti každého fragmentu, jako je skutečný text, jeho pozice na stránce, podrobnosti o písmu a velikost písma.
- Ten/Ta/To `XIndent` a `YIndent` vlastnosti udávají přesné souřadnice textového fragmentu v PDF.

## Závěr

tady to máte! S pouhými několika řádky kódu jsme úspěšně vyhledali a extrahovali text z PDF pomocí Aspose.PDF pro .NET. Flexibilita Aspose.PDF umožňuje manipulovat s PDF soubory mnoha způsoby, což z něj činí vynikající volbu pro vývojáře, kteří potřebují robustní řešení pro PDF v prostředí .NET. Tento příklad můžete snadno rozšířit tak, aby vyhledával další slova, extrahoval další podrobnosti nebo dokonce manipuloval s obsahem PDF na základě vašich potřeb. Doufejme, že vám tento průvodce poskytl jasný a přímočarý přístup k práci s PDF soubory. Vyzkoušejte to s vlastními PDF soubory!

## Často kladené otázky

### Mohu vyhledávat více slov najednou?  
Ano, můžete upravit `TextFragmentAbsorber` vyhledávat více frází úpravou vyhledávacího řetězce odpovídajícím způsobem.

### Co když text zabírá více řádků?  
Aspose.PDF rozpozná a extrahuje text, i když přesahuje více řádků. S těmito fragmenty můžete pracovat jednotlivě.

### Jak uložím extrahovaný text do souboru?  
Extrahovaný text můžete zapsat do souboru pomocí standardních operací C# se soubory, jako například `StreamWriter`.

### Podporuje Aspose.PDF extrakci textu ze skenovaných PDF souborů?  
Aspose.PDF nepodporuje OCR. Pro naskenované PDF soubory byste k rozpoznání textu potřebovali nástroj OCR.

### Jak mám zpracovat šifrované PDF soubory?  
Pokud je váš PDF soubor chráněn heslem, můžete jej odemknout pomocí Aspose.PDF zadáním hesla při načítání dokumentu.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}