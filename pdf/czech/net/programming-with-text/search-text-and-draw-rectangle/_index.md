---
"description": "Naučte se vyhledávat text v PDF a zvýrazňovat ho pomocí obdélníků pomocí Aspose.PDF pro .NET! Snadný podrobný návod pro vylepšení dovedností manipulace s PDF."
"linktitle": "Vyhledat text a nakreslit obdélník"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vyhledat text a nakreslit obdélník"
"url": "/cs/net/programming-with-text/search-text-and-draw-rectangle/"
"weight": 460
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vyhledat text a nakreslit obdélník

## Zavedení

Chcete si vylepšit dovednosti v práci s PDF? Chcete se naučit, jak vyhledávat konkrétní text v PDF souborech a zvýrazňovat ho obdélníkem? Narazili jste na perfektního průvodce! Dnes vás provedu tím, jak používat Aspose.PDF pro .NET k vyhledávání textu v PDF dokumentu a kreslení obdélníků kolem něj. Tento článek poskytne podrobný návod, který je navržen s ohledem na srozumitelnost a užitečnost, a zajistí, že budete moci tyto techniky sledovat a aplikovat je ve svých projektech. 

## Předpoklady

Než se pustíme do tutoriálu, připravme si, co budete potřebovat pro hladký průběh práce:

1. Základní znalost .NET: Pro efektivní pochopení tohoto tutoriálu byste měli být obeznámeni s programováním v jazyce C# a frameworkem .NET.
   
2. Nainstalované Visual Studio: Pro psaní a testování kódu budete potřebovat integrované vývojové prostředí (IDE). Visual Studio Community je skvělou volbou a je zdarma.
   
3. Aspose.PDF pro .NET: V projektu musíte mít nainstalovanou knihovnu Aspose.PDF. Můžete si ji stáhnout [zde](https://releases.aspose.com/pdf/net/) nebo zvažte [dočasná licence](https://purchase.aspose.com/temporary-license/) pro rozšířené funkce.
   
4. Ukázkový PDF dokument: Pro tento tutoriál budete potřebovat ukázkový PDF soubor s názvem `SearchAndGetTextFromAll.pdf` uloženy v adresáři vašeho projektu. 

## Importovat balíčky

Nejprve budete muset importovat potřebné balíčky do svého projektu .NET. Postupujte takto:

### Otevřít Visual Studio

Spusťte Visual Studio a vytvořte novou konzolovou aplikaci nebo použijte existující, kam chcete implementovat funkce PDF.

### Přidejte Aspose.PDF do svého projektu

1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte možnost „Spravovat balíčky NuGet“.
3. Hledat `Aspose.PDF` a nainstalujte nejnovější verzi.

Tímto způsobem si připravíte základy pro všechny úžasné manipulace s PDF, které se chystáte provést.

## Importovat jmenné prostory

horní části souboru programu budete chtít importovat příslušné jmenné prostory z knihovny Aspose:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Facades;
```

Díky tomu je pro vaše úkoly snazší přístup ke třídám a metodám v knihovně Aspose.PDF.


Nyní, když máte vše nastavené, si rozdělme proces vyhledávání textu v PDF a nakreslení obdélníku kolem něj na zvládnutelné kroky.

## Krok 1: Nastavení cesty k dokumentu

Nejprve nastavte cestu k souboru PDF. Nezapomeňte nahradit `YOUR DOCUMENT DIRECTORY` se skutečnou cestou, kde se nachází vaše `SearchAndGetTextFromAll.pdf` je uloženo.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## Krok 2: Otevřete dokument PDF

Dále vytvořte instanci `Document` třída pro načtení PDF:

```csharp
Document document = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

Tento řádek kódu otevře vámi zadaný soubor PDF a umožní vám s ním dále manipulovat.

## Krok 3: Vytvořte absorbér textu

Nyní budete potřebovat způsob, jak v daném dokumentu vyhledávat text. K tomu použijeme `TextFragmentAbsorber`:

```csharp
TextFragmentAbsorber textAbsorber = new TextFragmentAbsorber(@"[\S]+");
```

Regulární výraz `@"[\S]+"` je navržen tak, aby odpovídal jakémukoli řetězci v PDF bez mezer. 

## Krok 4: Konfigurace možností textového vyhledávání

Dále byste měli nastavit možnosti textového vyhledávání:

```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textAbsorber.TextSearchOptions = textSearchOptions;
```

Zde, `true` Parametr znamená, že vyhledávání bude rozlišovat velká a malá písmena. Můžete jej nastavit na `false` pokud chcete vyhledávání bez rozlišování velkých a malých písmen.

## Krok 5: Přijměte absorbér textu v dokumentu

S vaším `TextFragmentAbsorber` a možnosti vyhledávání jsou připraveny, je čas vstřebat text z dokumentu:

```csharp
document.Pages.Accept(textAbsorber);
```

Tato metoda prozkoumá každou stránku ve vašem PDF souboru a vyhledá fragmenty textu, které odpovídají zadanému vzoru.

## Krok 6: Vytvořte editor obsahu PDF

Pro kreslení tvarů v dokumentu budete potřebovat `PdfContentEditor`:

```csharp
var editor = new PdfContentEditor(document);
```

Tento editor umožňuje snadnou manipulaci a úpravu obsahu PDF.

## Krok 7: Procházení nalezených fragmentů textu

Nyní budete chtít procházet nalezené fragmenty textu a nakreslit kolem nich obdélníky:

```csharp
foreach (TextFragment textFragment in textAbsorber.TextFragments)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        DrawBox(editor, textFragment.Page.Number, textSegment, System.Drawing.Color.Red);
    }
}
```

Tato smyčka iteruje přes každý fragment textu a jeho segmenty a volá `DrawBox` metoda kreslení obdélníku.

## Krok 8: Definování metody DrawBox

Musíte definovat `DrawBox` metoda, která bude zpracovávat logiku vykreslování obdélníku. Zde je jednoduchá implementace:

```csharp
private static void DrawBox(PdfContentEditor editor, int pageNumber, TextSegment textSegment, System.Drawing.Color color)
{
    // Vypočítejte rozměry obdélníku na základě textového segmentu
    float x = textSegment.Rectangle.LLX;
    float y = textSegment.Rectangle.LLY;
    float width = textSegment.Rectangle.Width;
    float height = textSegment.Rectangle.Height;

    // Nakreslete obdélník pomocí vypočítaných hodnot
    editor.DrawRectangle(pageNumber, x, y, width, height, color, 1);
}
```

Tato metoda určuje polohu a velikost obdélníku na základě ohraničujícího obdélníku segmentu a pomocí editoru jej vykreslí.

## Krok 9: Uložení upraveného dokumentu

Po nakreslení obdélníků kolem nalezeného textu můžete upravený dokument uložit:

```csharp
dataDir = dataDir + "SearchTextAndDrawRectangle_out.pdf";
document.Save(dataDir);
```

Ujistěte se, že je nový soubor uložen s odlišným názvem, abyste zabránili přepsání původního dokumentu.

## Krok 10: Potvrzovací zpráva

Nakonec vypište do konzole potvrzovací zprávu, která vás informuje o úspěšném provedení operace:

```csharp
Console.WriteLine("\nRectangle drawn successfully on searched text.\nFile saved at " + dataDir);
```

A tady to máte! Úspěšně jste vytvořili skript pro vyhledávání textu v PDF a jeho zvýraznění obdélníky.

## Závěr

Gratulujeme! Právě jste odemkli mocnou dovednost, která vám může výrazně vylepšit schopnosti manipulace s PDF pomocí Aspose.PDF pro .NET. Stačí jen pár jednoduchých kroků a můžete v dokumentu vyhledat jakýkoli text a vizuálně ho zvýraznit, čímž se vaše PDF dokumenty stanou interaktivnějšími a lépe spravovatelnými. Neváhejte experimentovat s různými vzory regulárních výrazů a barevnými možnostmi, abyste si tento nástroj skutečně přizpůsobili!

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která poskytuje komplexní způsob, jak programově vytvářet, manipulovat a převádět dokumenty PDF.

### Mohu používat Aspose.PDF zdarma?
Ano, Aspose nabízí bezplatnou zkušební verzi, kterou můžete využít k otestování funkcí knihovny. Vyzkoušejte ji. [zde](https://releases.aspose.com/).

### Jaký programovací jazyk musím použít s Aspose.PDF pro .NET?
Aspose.PDF pro .NET je navržen pro použití s C# a dalšími jazyky .NET.

### Jak získám pomoc s Aspose.PDF?
Fórum podpory Aspose vám může pomoci s jakýmkoli problémem nebo dotazem. Najděte podporu. [zde](https://forum.aspose.com/c/pdf/10).

### Kde si stáhnu Aspose.PDF pro .NET?
Knihovnu si můžete stáhnout z webových stránek Aspose, [zde](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}