---
"description": "Naučte se, jak převést PDF do formátu TIFF pomocí Bradleyho algoritmu v Aspose.PDF pro .NET. Podrobný návod, předpoklady a nejčastější dotazy pro bezproblémový převod."
"linktitle": "Bradleyho algoritmus"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Bradleyho algoritmus"
"url": "/cs/net/programming-with-images/bradley-algorithm/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bradleyho algoritmus

## Zavedení

Práce se soubory PDF může někdy vyžadovat více než jen jejich čtení nebo úpravu – možná je budete muset převést do obrázků. Jedním z účinných způsobů, jak převést soubory PDF do obrázků TIFF, je použití Bradleyho algoritmu prostřednictvím knihovny Aspose.PDF pro .NET. Tato metoda zajišťuje vysoce kvalitní binární obrazy, ideální pro archivaci dokumentů a další specializované případy použití.

Tento tutoriál vás provede podrobným a snadno srozumitelným postupem pro převod stránky PDF do obrázku TIFF pomocí Bradleyho binarizačního algoritmu. Aspose.PDF pro .NET tento úkol zjednodušuje a poskytuje vám možnost automatizovat a zefektivnit vaše pracovní postupy s dokumenty.

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte vše potřebné k jeho dodržování:

- Aspose.PDF pro .NET: Budete potřebovat knihovnu. Stáhněte si ji z [zde](https://releases.aspose.com/pdf/net/).
- Visual Studio (nebo jakékoli C# IDE).
- Základní znalost C#.
- Platný řidičský průkaz nebo [dočasná licence](https://purchase.aspose.com/temporary-license/) z Aspose.

## Importovat balíčky

V první řadě se ujistěte, že jste do projektu importovali potřebné jmenné prostory. Tyto knihovny vám poskytnou nástroje pro manipulaci s dokumenty PDF, jejich převod do formátu TIFF a použití Bradleyho binarizačního algoritmu.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Rozdělme si proces do jednoduchých kroků, abyste v něm mohli hladce pokračovat. Na konci této příručky budete mít úspěšně převedenu stránku PDF do binárního obrázku TIFF pomocí Bradleyho algoritmu.

## Krok 1: Nastavení adresáře dokumentů

Prvním krokem je zadání cesty k adresáři, kde se nachází váš dokument PDF. Také definujete výstupní cesty pro generované obrázky TIFF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Cesta k vašemu PDF souboru
```

Zde se ukládají zdrojový PDF i převedené soubory TIFF. Ujistěte se, že je adresář správně nastaven, aby kód mohl číst a zapisovat soubory bez chyb.

## Krok 2: Otevřete dokument PDF

Nyní, když je cesta nastavena, je čas otevřít PDF dokument, který chcete převést. Aspose.PDF pro .NET usnadňuje načtení dokumentu pro další zpracování.

```csharp
Document pdfDocument = new Document(dataDir + "PageToTIFF.pdf");
```

Zde, `PageToTIFF.pdf` je vzorový soubor. Můžete jej nahradit libovolným souborem PDF dle vlastního výběru. Objekt dokument nyní obsahuje PDF pro další manipulaci.

## Krok 3: Definování výstupních cest pro obrázky

Dále určíte výstupní cesty pro generované soubory TIFF, a to jak standardní TIFF, tak i binarizované verze.

```csharp
string outputImageFile = dataDir + "resultant_out.tif";
string outputBinImageFile = dataDir + "37116-bin_out.tif";
```

Oddělením těchto cest získáte jeden soubor pro standardní konverzi TIFF a druhý pro binarizovaný obrázek po aplikaci Bradleyho algoritmu.

## Krok 4: Vytvořte objekt rozlišení

Při převodu PDF do formátu TIFF hraje rozlišení významnou roli při určování kvality obrazu. Pro naše účely jej nastavíme na 300 DPI, abychom zajistili vysoce kvalitní výstup.

```csharp
Resolution resolution = new Resolution(300);
```

Vyšší DPI znamená lepší ostrost obrazu, zejména při práci s dokumenty, které budou vytištěny nebo archivovány.

## Krok 5: Konfigurace nastavení TIFF

Dále budete muset nakonfigurovat nastavení pro obrázek TIFF. Zde použijeme kompresi LZW a nastavíme barevnou hloubku na 1 bpp (1 bit na pixel), abychom dosáhli binárního obrazu.

```csharp
TiffSettings tiffSettings = new TiffSettings();
tiffSettings.Compression = CompressionType.LZW;
tiffSettings.Depth = Aspose.Pdf.Devices.ColorDepth.Format1bpp;
```

Nastavením hloubky na 1 bpp připravíme obrázek pro binární výstup. LZW komprese je zvolena pro svou efektivitu při zmenšování velikosti souboru bez ztráty kvality.

## Krok 6: Vytvořte zařízení TIFF

Nyní budete muset vytvořit zařízení TIFF, které bude provádět konverzi. Toto zařízení použije rozlišení a nastavení TIFF definované dříve.

```csharp
TiffDevice tiffDevice = new TiffDevice(resolution, tiffSettings);
```

Jádrem této operace je zařízení TIFF. Vezme dokument PDF a převede každou stránku do obrázku TIFF na základě předdefinovaných nastavení.

## Krok 7: Převod stránky PDF do formátu TIFF

Je čas zpracovat PDF a převést první stránku do obrázku ve formátu TIFF. `Process` Metoda umožňuje převést konkrétní stránky nebo celý dokument. V tomto příkladu převádíme první stránku.

```csharp
tiffDevice.Process(pdfDocument, outputImageFile);
```

Po dokončení metody budete mít obrázek TIFF uložený v dříve definovaném umístění.

## Krok 8: Aplikujte Bradleyho binarizační algoritmus

A teď přichází na řadu kouzlo – Bradleyho algoritmus! Tento algoritmus převádí šedotónový TIFF obrázek na binární obrázek a optimalizuje ho pro systémy rozpoznávání dokumentů.

```csharp
using (FileStream inStream = new FileStream(outputImageFile, FileMode.Open))
{
    using (FileStream outStream = new FileStream(outputBinImageFile, FileMode.Create))
    {
        tiffDevice.BinarizeBradley(inStream, outStream, 0.1);
    }
}
```

Metoda BinarizeBradley přijímá dva souborové streamy (vstupní a výstupní) a také prahovou hodnotu (zde `0.1`), která určuje úroveň binarizace. Po spuštění budete mít dokonale zbinovaný obraz připravený k použití.

## Krok 9: Potvrzení úspěšné konverze

Nakonec je dobrým zvykem informovat uživatele o úspěšném dokončení procesu. To lze provést jednoduchým výstupem do konzole.

```csharp
System.Console.WriteLine("Conversion using Bradley algorithm performed successfully!");
```

Jakmile se to vytiskne, víte, že vaše stránka PDF byla úspěšně převedena na binární obrázek TIFF!

## Závěr

A tady to máte! Právě jste se naučili, jak převést stránku PDF do obrázku TIFF a použít Bradleyho binarizační algoritmus pomocí Aspose.PDF pro .NET. Tento proces je nezbytný pro archivaci dokumentů, optické rozpoznávání znaků (OCR) a další profesionální aplikace. Díky vysokému rozlišení a efektivní kompresi si můžete být jisti, že obrázky vašich dokumentů budou jasné a zároveň zvládnutelné velikosti.

## Často kladené otázky

### Co je Bradleyho algoritmus?
Bradleyho algoritmus je binarizační technika, která převádí obrazy ve stupních šedi na binární (černobílé) obrazy určením adaptivního prahu pro každý pixel na základě jeho okolí.

### Mohu touto metodou převést více stránek PDF do formátu TIFF?
Ano, můžete upravit `Process` metoda pro převod všech stránek smyčkou procházením stránek v dokumentu.

### Jaké je optimální rozlišení pro převod PDF do TIFF?
Pro vysoce kvalitní obrázky se obecně doporučuje 300 DPI. Tuto hodnotu však můžete upravit podle svých potřeb.

### Co znamená 1bpp v barevné hloubce?
1bpp (1 bit na pixel) znamená, že obraz bude černobílý, přičemž každý pixel bude buď zcela černý, nebo zcela bílý.

### Je Bradleyho algoritmus vhodný pro OCR?
Ano, Bradleyho algoritmus se často používá v předzpracování OCR, protože zvyšuje kontrast textu ve skenovaných dokumentech.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}