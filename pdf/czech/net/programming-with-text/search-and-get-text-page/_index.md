---
"description": "Naučte se, jak vyhledávat a získávat text z konkrétní stránky v souboru PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Vyhledávání a získávání textové stránky v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vyhledávání a získávání textové stránky v souboru PDF"
"url": "/cs/net/programming-with-text/search-and-get-text-page/"
"weight": 430
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vyhledávání a získávání textové stránky v souboru PDF

## Zavedení

Už jste někdy zjistili, že potřebujete vyhledat konkrétní text v PDF dokumentu a extrahovat ho pro další použití? Možná vytváříte aplikaci, která zpracovává dokumenty a vyžaduje přesnou extrakci dat, nebo možná jen potřebujete efektivně analyzovat PDF soubory. Ať už je váš případ jakýkoli, jste na správném místě! V tomto tutoriálu se ponoříme do toho, jak vyhledávat a získávat text ze stránky v PDF souboru pomocí Aspose.PDF pro .NET. Ať už jste začátečník nebo zkušený vývojář, tento průvodce vás provede každým krokem konverzačním a poutavým způsobem. Jste připraveni? Pojďme na to!

## Předpoklady

Než se pustíme do kódování, ujistěte se, že máte vše, co potřebujete:

1. Aspose.PDF pro knihovnu .NET: Můžete si ji stáhnout z [zde](https://releases.aspose.com/pdf/net/) nebo si stáhněte bezplatnou zkušební verzi ze stejného odkazu. Pro zakoupení přejděte na [Obchod Aspose](https://purchase.aspose.com/buy).
2. .NET Framework: Budete potřebovat funkční vývojové prostředí .NET, například Visual Studio.
3. Soubor PDF: Budete potřebovat vzorový soubor PDF, ve kterém můžeme prohledat a extrahovat text. V tomto tutoriálu předpokládejme, že soubor má název `SearchAndGetTextPage.pdf`.

## Importovat balíčky

Nejdříve musíme importovat potřebné jmenné prostory pro práci s Aspose.PDF pro .NET. Ujistěte se, že jsou zahrnuty v horní části kódu.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System
```

Nyní, když jsme si probrali předpoklady, pojďme si kód krok za krokem rozebrat. Každý krok je jasně popsán, aby se snadno sledoval.

## Krok 1: Nastavení cesty k adresáři dokumentů

Než budete moci pracovat s PDF dokumentem, budete muset definovat cestu k jeho uložení. Tím zajistíte, že program bude mít k souboru přístup.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- dataDir: Toto je cesta ke složce, kde jsou uloženy vaše soubory PDF. Nahraďte `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kde se PDF nachází.

## Krok 2: Načtěte dokument PDF

Dalším krokem je načtení PDF dokumentu do paměti, abyste s ním mohli pracovat. Postupujte takto:

```csharp
Document pdfDocument = new Document(dataDir + "SearchAndGetTextPage.pdf");
```

- Dokument: Toto je třída Aspose.PDF, která načítá soubor PDF.
- pdfDocument: Proměnná, kam se ukládá váš PDF soubor po načtení.

## Krok 3: Vytvořte objekt absorbéru textu

Ten/Ta/To `TextFragmentAbsorber` Třída umožňuje vyhledávat konkrétní text v PDF. Vytvořme instanci této třídy, která vyhledá všechny výskyty zadané hledané fráze.

```csharp
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Figure");
```

- TextFragmentAbsorber: Tato třída je zodpovědná za vyhledávání a extrakci textu z PDF.
- „Obrázek“: Nahraďte jej libovolným textem, který chcete v PDF vyhledat.

## Krok 4: Použití absorbéru textu na celý PDF

Jakmile je absorbér textu nastaven, musíte programu sdělit, aby prohledal všechny stránky PDF.

```csharp
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Accept(): Tato metoda aplikuje absorbér textu na PDF a prohledává každou stránku a hledá zadaný text.

## Krok 5: Načtení a iterování extrahovaného textu

Nyní, když jsme naskenovali PDF, je čas načíst výsledky a zobrazit je. Projdeme si extrahované textové fragmenty.

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- TextFragmentCollection: Tato kolekce obsahuje všechny instance textových fragmentů nalezených absorbérem textu.

## Krok 6: Procházení každého fragmentu a extrakce dat

Nyní projdeme `textFragmentCollection` a extrahovat různé vlastnosti každého textového segmentu, jako je jeho poloha, podrobnosti o písmu a barva.

```csharp
foreach (TextFragment textFragment in textFragmentCollection)
{
	foreach (TextSegment textSegment in textFragment.Segments)
	{
		Console.WriteLine("Text : {0} ", textSegment.Text);
		Console.WriteLine("Position : {0} ", textSegment.Position);
		Console.WriteLine("XIndent : {0} ", textSegment.Position.XIndent);
		Console.WriteLine("YIndent : {0} ", textSegment.Position.YIndent);
		Console.WriteLine("Font - Name : {0}", textSegment.TextState.Font.FontName);
		Console.WriteLine("Font - IsAccessible : {0} ", textSegment.TextState.Font.IsAccessible);
		Console.WriteLine("Font - IsEmbedded : {0} ", textSegment.TextState.Font.IsEmbedded);
		Console.WriteLine("Font - IsSubset : {0} ", textSegment.TextState.Font.IsSubset);
		Console.WriteLine("Font Size : {0} ", textSegment.TextState.FontSize);
		Console.WriteLine("Foreground Color : {0} ", textSegment.TextState.ForegroundColor);
	}
}
```

- TextFragment: Každý fragment obsahuje části nalezeného textu.
- TextSegment: Každý fragment může mít více segmentů, které představují různé části textu.
- TextState: Toto poskytuje podrobné informace o písmu, velikosti a barvě textu.

V této smyčce vytiskneme podrobnosti, jako je skutečný text, jeho poloha (souřadnice X a Y), písmo, zda je písmo vloženo do PDF a barva popředí textu.

## Závěr

tady to máte! Nyní jste úspěšně vyhledali a extrahovali text ze souboru PDF pomocí Aspose.PDF pro .NET. Je neuvěřitelné, kolik flexibility tato knihovna nabízí. Ať už potřebujete vyhledat konkrétní text ve velkém dokumentu, extrahovat ho nebo analyzovat jeho vlastnosti, Aspose.PDF to udělá hračkou. Navíc s kódem, který jsme probrali, jste dobře vybaveni k tomu, abyste si jej přizpůsobili svým potřebám. 

## Často kladené otázky

### Mohu vyhledávat více frází najednou?  
Ano, kód můžete upravit tak, aby vyhledával více frází, a to vytvořením více `TextFragmentAbsorber` objekty.

### Jak mohu extrahovat text z konkrétní stránky?  
Můžete cílit na konkrétní stránku použitím `TextFragmentAbsorber` na jednu stránku místo celého dokumentu. Například: `pdfDocument.Pages[1].Accept(textFragmentAbsorber);`.

### Je Aspose.PDF pro .NET zdarma?  
Aspose.PDF je komerční produkt, ale můžete ho používat s [bezplatná zkušební verze](https://releases.aspose.com/).

### Mohu extrahovat obrázky z PDF pomocí Aspose.PDF?  
Ano, Aspose.PDF umožňuje extrahovat obrázky kromě textu. Zaškrtněte [dokumentace](https://reference.aspose.com/pdf/net/) pro více informací.

### Co když budu potřebovat další pomoc nebo podporu?  
Vždycky můžete získat pomoc od [Fórum podpory Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}