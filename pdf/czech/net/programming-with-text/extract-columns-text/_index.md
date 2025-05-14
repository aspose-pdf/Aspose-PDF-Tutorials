---
"description": "Naučte se, jak extrahovat sloupce textu ze souborů PDF pomocí Aspose.PDF pro .NET. Tato příručka rozebírá jednotlivé kroky s příklady kódu a vysvětleními."
"linktitle": "Extrahovat text sloupců v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Extrahovat text sloupců v souboru PDF"
"url": "/cs/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text sloupců v souboru PDF

## Zavedení

Pracujete se soubory PDF a potřebujete extrahovat text v určitém sloupcovém formátu? Ať už zpracováváte faktury, reporty nebo jakékoli strukturované dokumenty, přesná extrakce textu z PDF může být ošemetná. A právě zde přichází na řadu Aspose.PDF pro .NET, který proces zjednoduší. V tomto tutoriálu vás provedeme tím, jak snadno extrahovat sloupce textu ze souboru PDF. 

## Předpoklady

Než se ponoříme do kódu, pojďme si probrat základní věci, které budete potřebovat:

- Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou nejnovější verzi Aspose.PDF pro .NET. Pokud ne, můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/).
- Vývojové prostředí: Pro práci s kódem budete potřebovat Visual Studio nebo jiné vývojové prostředí .NET.
- PDF dokument: Mějte po ruce vzorový PDF dokument, nejlépe takový se sloupci textu, protože z něj budeme text extrahovat.

Pokud ještě nemáte nainstalovaný Aspose.PDF pro .NET, můžete si ho stáhnout [bezplatná zkušební verze](https://releases.aspose.com/) nebo [koupit licenci](https://purchase.aspose.com/buy) pro plnou funkcionalitu. Můžete si také zažádat o [dočasná licence](https://purchase.aspose.com/temporary-license) v případě potřeby.

## Importovat jmenné prostory

Chcete-li ve svém projektu použít Aspose.PDF pro .NET, budete muset importovat následující jmenné prostory:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## Podrobný návod: Extrakce sloupců textu z PDF

Nyní si rozebereme jednotlivé části kódu, abychom lépe pochopili, jak funguje. Sledujte nás krok za krokem a vysvětlujte každý segment procesu.

## Krok 1: Načtěte dokument PDF

První věc, kterou musíte udělat, je načíst soubor PDF do `Document` objekt. Takto Aspose.PDF interaguje s vaším dokumentem.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

V tomto kroku jednoduše definujeme adresář, kde je uložen váš PDF dokument. Nahraďte `"YOUR DOCUMENT DIRECTORY"` s cestou k vašemu lokálnímu souboru PDF. `Document` Objekt načte PDF do paměti a zpřístupní ho tak pro další zpracování.

## Krok 2: Nastavení absorbéru textových fragmentů

Dále použijeme `TextFragmentAbsorber` absorbovat nebo zachytit veškerý text ze souboru PDF. Tato třída absorber je navržena tak, aby extrahovala fragmenty textu z konkrétních oblastí v PDF, což ji činí ideální pro extrakci sloupců textu.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

Zde vytvoříme instanci `TextFragmentAbsorber` a aplikujte jej na všechny stránky PDF pomocí `Accept()`Ten/Ta/To `TextFragmentCollection` ukládá extrahovaný text a z této kolekce můžeme text podle potřeby manipulovat nebo extrahovat.

## Krok 3: Upravte velikost písma extrahovaného textu

Jakmile zachytíte fragmenty textu, můžete chtít zmenšit jejich velikost písma, zejména pokud je původní text příliš velký. V tomto příkladu zmenšujeme velikost písma o 70 %.

```csharp
foreach (TextFragment tf in tfc)
{
    // Zmenšit velikost písma o 70 %
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

Tento kód prochází každým `TextFragment` v kolekci a zmenší velikost písma o 70 %. Úprava velikosti písma může usnadnit správu extrahovaného textu, zejména pokud jej formátujete pro různé účely.

## Krok 4: Uložení dokumentu do paměťového streamu

Po úpravě textu uložíme PDF soubor do `MemoryStream`To nám umožňuje uchovat dokument v paměti pro další zpracování, aniž bychom jej museli zapisovat zpět na disk.

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

Zde uložíme PDF do paměťového proudu a poté dokument znovu načteme. Tato metoda je užitečná, když pracujete s velkými soubory a chcete se vyhnout zbytečným operacím na disku.

## Krok 5: Extrahujte veškerý text pomocí nástroje Text Absorber

Nyní, když jsme připravili PDF, je čas extrahovat text. Použijeme `TextAbsorber` načíst veškerý text z dokumentu.

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

V tomto kroku `TextAbsorber` absorbuje veškerý text z PDF a extrahovaný text se uloží do `extractedText` řetězec. A tady se děje ta zázrak – vaše sloupce textu jsou nyní ve formátu prostého textu!

## Krok 6: Uložení extrahovaného textu do souboru

Nakonec uložíme extrahovaný text do `.txt` soubor pro snadný přístup a další použití.

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

Tento kód zapíše extrahovaný text do nového `.txt` soubor a uloží jej do vámi zadaného adresáře. V konzoli se zobrazí zpráva potvrzující úspěšné dokončení procesu.

## Závěr

A tady to máte! Extrakce sloupců textu ze souboru PDF pomocí Aspose.PDF pro .NET je jednodušší, než si myslíte. S pouhými několika řádky kódu můžete načíst PDF, extrahovat konkrétní text, upravit formátování a uložit výsledky do textového souboru.

Tato technika je neuvěřitelně užitečná pro zpracování strukturovaných dokumentů, jako jsou tabulky, sestavy nebo jakýkoli obsah uspořádaný do sloupců. Ať už potřebujete automatizovat extrakci dat nebo zpracovávat hromadné dokumenty, Aspose.PDF poskytuje nástroje, které vám to umožní efektivně.

## Často kladené otázky

### Mohu extrahovat text z konkrétních stránek PDF souboru?  
Ano! Můžete to upravit `TextFragmentAbsorber` cílit na konkrétní stránky pomocí `pdfDocument.Pages[pageIndex].Accept(tfa);` metoda.

### Je možné extrahovat text pouze z jednoho sloupce ve vícesloupcovém PDF?  
Ano, ale budete muset pracovat se souřadnicemi fragmentů textu pomocí `TextFragment.Rectangle` zaměřit se na konkrétní oblasti dokumentu.

### Jak mohu zlepšit přesnost extrakce textu?  
Pro větší přesnost se ujistěte, že je struktura PDF dobře definovaná, a vyhněte se dokumentům se složitým rozvržením. Můžete také doladit `TextFragmentAbsorber` extrahovat text na základě stylů písma, velikostí nebo oblastí.

### Podporuje Aspose.PDF extrakci textu ze skenovaných dokumentů?  
Ano, ale budete muset použít technologii OCR (optické rozpoznávání znaků). Aspose pro to také poskytuje nástroje.

### Jak zpracuji velké PDF soubory s tisíci stránkami?  
U velkých PDF souborů zpracovávejte dokument po částech extrahováním textu z několika stránek najednou, abyste se vyhnuli vysokému využití paměti.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}