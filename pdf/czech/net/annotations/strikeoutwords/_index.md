---
"description": "Naučte se, jak pomocí Aspose.PDF pro .NET přeškrtávat slova v PDF s tímto komplexním podrobným návodem. Zlepšete si své dovednosti v úpravě dokumentů."
"linktitle": "Přeškrtnutá slova"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přeškrtnutá slova"
"url": "/cs/net/annotations/strikeoutwords/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přeškrtnutá slova

## Zavedení

Už jste někdy zjistili, že potřebujete zdůraznit určitý text v PDF jeho přeškrtnutím? Ať už kontrolujete dokumenty, označujete text nebo jednoduše potřebujete zvýraznit určité části, přeškrtávání slov může být cenným nástrojem. V tomto tutoriálu se podíváme na to, jak toho dosáhnout pomocí Aspose.PDF pro .NET. Tato komplexní příručka vás provede jednotlivými kroky a zajistí, že budete mít všechny informace potřebné k efektivní implementaci této funkce ve vašich .NET aplikacích. 

## Předpoklady

Než se pustíme do kódu, je třeba splnit několik předpokladů, abyste mohli tento tutoriál dodržovat:

1. Knihovna Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF pro .NET. Můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/).

2. .NET Framework: Ujistěte se, že máte na svém počítači nainstalovaný .NET Framework. Tento tutoriál je určen pro aplikace .NET.

3. Vývojové prostředí: Pro psaní a spuštění kódu budete potřebovat IDE, jako je Visual Studio.

4. PDF dokument: Mějte připravený vzorový PDF soubor, se kterým chcete pracovat. Toto bude dokument, ve kterém budeme text škrtat.

5. Základní znalost C#: Znalost programování v C# je nezbytná pro pochopení a implementaci kroků v tomto tutoriálu.

## Importovat balíčky

Než začneme s kódováním, musíme do našeho projektu .NET importovat potřebné jmenné prostory. To nám umožní přístup ke třídám a metodám potřebným pro manipulaci s PDF soubory pomocí Aspose.PDF.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Tyto jmenné prostory jsou nezbytné pro práci s dokumenty PDF, manipulaci s textem a přidávání anotací, jako jsou přeškrtnuté texty.

V této části si rozdělíme proces škrtání slov v dokumentu PDF do jednoduchých a snadno zvládnutelných kroků. Každý krok bude doprovázen podrobným vysvětlením, abyste pochopili, jak vše funguje.

## Krok 1: Načtěte dokument PDF

Prvním krokem je načtení PDF dokumentu, který chcete upravit. V tomto dokumentu budete škrtat konkrétní slova nebo fráze.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Otevřete PDF dokument
Document document = new Document(dataDir + "input.pdf");
```

- `dataDir`Tato proměnná obsahuje cestu k adresáři s dokumenty. Nahraďte `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kde se nachází váš PDF soubor.
- `Document`: Ten `Document` Třída představuje PDF dokument. Předáním cesty k souboru jejímu konstruktoru otevřeme PDF soubor ke zpracování.

## Krok 2: Vytvořte absorbér TextFragment pro nalezení konkrétního textu

Dále vytvoříme instanci `TextFragmentAbsorber` vyhledat konkrétní fragment textu v dokumentu PDF. To nám umožní najít text, který chceme vyškrtnout.

```csharp
// Vytvořte instanci třídy TextFragment Absorber pro vyhledávání konkrétního fragmentu textu.
Aspose.Pdf.Text.TextFragmentAbsorber textFragmentAbsorber = new Aspose.Pdf.Text.TextFragmentAbsorber("Estoque");
```

- `TextFragmentAbsorber`Tato třída se používá k vyhledávání a práci s konkrétními textovými fragmenty v dokumentu PDF. V tomto příkladu hledáme slovo „Estoque“. Nahraďte „Estoque“ slovem nebo frází, kterou chcete v dokumentu najít.

## Krok 3: Procházení stránek dokumentu PDF

Teď, když máme naše `TextFragmentAbsorber`, musíme iterovat každou stránku PDF dokumentu, abychom našli zadaný text.

```csharp
// Procházení stránek PDF dokumentu
for (int i = 1; i <= document.Pages.Count; i++)
{
    // Získání aktuální stránky dokumentu PDF
    Page page = document.Pages[i];
    page.Accept(textFragmentAbsorber);
}
```

- `for (int i = 1; i <= document.Pages.Count; i++)`Tato smyčka iteruje každou stránkou dokumentu PDF.
- `document.Pages[i]`: Načte aktuálně zpracovávanou stránku.
- `page.Accept(textFragmentAbsorber)`Tato metoda aplikuje `TextFragmentAbsorber` na aktuální stránku a hledání zadaného textu.

## Krok 4: Shromáždění a zpracování textových fragmentů

Po iteraci stránkami shromáždíme nalezené textové fragmenty a připravíme je k dalšímu zpracování.

```csharp
// Vytvořte kolekci absorbovaných textových fragmentů
Aspose.Pdf.Text.TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`Tato kolekce uchovává všechny fragmenty textu, které byly v dokumentu nalezeny. Tuto kolekci použijeme v dalším kroku k přeškrtnutí textu.

## Krok 5: Projděte si textové fragmenty a vyškrtněte je

V tomto kroku projdeme každý textový fragment v naší kolekci a aplikujeme na něj anotaci přeškrtnutí.

```csharp
// Iterovat nad kolekcí textových fragmentů
for (int j = 1; j <= textFragmentCollection.Count; j++)
{
	Aspose.Pdf.Text.TextFragment textFragment = textFragmentCollection[j];

    // Získání obdélníkových rozměrů objektu TextFragment
    Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(
        (float)textFragment.Position.XIndent,
        (float)textFragment.Position.YIndent,
        (float)textFragment.Position.XIndent + (float)textFragment.Rectangle.Width,
        (float)textFragment.Position.YIndent + (float)textFragment.Rectangle.Height);

    // Vytvoření instance anotace přeškrtnutím
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.Page, rect);

    // Nastavení vlastností přeškrtnuté anotace
    strikeOut.Opacity = .80f;
    strikeOut.Border = new Border(strikeOut);
    strikeOut.Color = Aspose.Pdf.Color.Red;

    // Přidejte anotaci do kolekce anotací stránky s textovým fragmentem
    textFragment.Page.Annotations.Add(strikeOut);
}
```

- `TextFragment textFragment = textFragmentCollection[j]`Tento řádek načte aktuální fragment textu.
- `Aspose.Pdf.Rectangle`Vypočítáme obdélníkové rozměry textového fragmentu, abychom určili, kam použít přeškrtnutí.
- `StrikeOutAnnotation`Tato třída představuje anotaci přeškrtnutí. Vytvoříme její instanci s vypočítaným obdélníkem a aktuální stránkou.
- `strikeOut.Opacity`Tato vlastnost nastavuje neprůhlednost přeškrtnutého textu, takže bude viditelný na 80 %.
- `strikeOut.Color`Barvu přeškrtnutí jsme nastavili na červenou. Tuto barvu můžete změnit na libovolnou.
- `textFragment.Page.Annotations.Add(strikeOut)`: Tím se na stránku přidá anotace přeškrtnutí.

## Krok 6: Uložení upraveného dokumentu PDF

Posledním krokem je uložení upraveného dokumentu PDF s použitými přeškrtnutími.

```csharp
// Uložit aktualizovaný dokument PDF
dataDir = dataDir + "StrikeOutWords_out.pdf";
document.Save(dataDir);
```

- `dataDir + "StrikeOutWords_out.pdf"`: Tím se pro upravený dokument vytvoří nový název souboru. Původní soubor zůstane nezměněn.
- `document.Save(dataDir)`: Uloží dokument PDF s přeškrtnutými řádky do zadaného umístění.

## Závěr

Gratulujeme! Úspěšně jste vyškrtli konkrétní slova v dokumentu PDF pomocí Aspose.PDF pro .NET. Dodržováním tohoto podrobného návodu si nyní můžete dokumenty PDF přizpůsobit zvýrazněním nebo vyškrtnutím textu, čímž je učiníte dynamičtějšími a přizpůsobenými vašim potřebám. Ať už anotujete právní dokumenty, připravujete zprávy nebo jen označujete text k recenzování, tento tutoriál vás vybavil dovednostmi, které vám pomohou to dělat efektivně.

## Často kladené otázky

### Mohu změnit barvu přeškrtnutého kousku?

Ano, barvu můžete změnit úpravou `strikeOut.Color` vlastnost. Můžete ji například nastavit na `Aspose.Pdf.Color.Blue` pro modrý strikeout.

### Je možné vyškrtnout více slov najednou?

Rozhodně! `TextFragmentAbsorber` lze použít k vyhledání libovolného slova nebo fráze v dokumentu. Přeškrtnutí můžete použít na více instancí iterací v rámci `TextFragmentCollection`.

### Co když chci přeškrtnout text pouze na konkrétních stránkách?

Smyčku, která iteruje stránkami, můžete upravit tak, aby zahrnovala pouze stránky, které chcete upravit. Například `for (int i = 1; i <= 3; i++)` by se přeškrtnutí vztahovalo pouze na první tři stránky.

### Jak mohu upravit tloušťku přeškrtnuté čáry?

Tloušťku přeškrtnuté čáry můžete upravit úpravou `Border` majetek `StrikeOutAnnotation`To umožňuje přizpůsobení vzhledu přeškrtnutí.

### Existuje způsob, jak vrátit zpět přeškrtnutí po uložení dokumentu?

Jakmile je dokument uložen, je přeškrtnutí trvalé. Pokud potřebujete zachovat původní text bez přeškrtnutí, zvažte před provedením jakýchkoli úprav uložení zálohy původního dokumentu.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}