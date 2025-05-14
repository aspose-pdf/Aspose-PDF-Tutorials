---
"description": "Naučte se, jak extrahovat text z PDF dokumentu pomocí textového zařízení v Aspose.PDF pro .NET."
"linktitle": "Extrakce textu pomocí textového zařízení"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Extrakce textu pomocí textového zařízení"
"url": "/cs/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrakce textu pomocí textového zařízení

## Zavedení

Extrakce textu z PDF může být složitá, zejména při práci s dokumenty, které mají různé formáty, vložená písma nebo složité rozvržení. Ale s Aspose.PDF pro .NET se tento proces stává hračkou! Ať už chcete převést stránky PDF do prostého textu pro další analýzu, nebo potřebujete jednoduše extrahovat určité části, Aspose.PDF vám s tím pomůže. V tomto tutoriálu si krok za krokem ukážeme, jak extrahovat text z PDF pomocí třídy TextDevice v Aspose.PDF. Poskytneme také jasná vysvětlení, abyste mohli stejné metody snadno aplikovat na své vlastní projekty.

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte vše potřebné k jeho napsání. Zde je to, co budete potřebovat:

1. Aspose.PDF pro .NET: Stáhněte si nejnovější verzi z [Stránka ke stažení souboru Aspose.PDF pro .NET](https://releases.aspose.com/pdf/net/).
2. Vývojové prostředí: Visual Studio nebo jakékoli jiné vývojové prostředí C#.
3. .NET Framework: Ujistěte se, že váš projekt cílí na .NET Framework 4.x nebo vyšší.
4. Vstupní PDF soubor: PDF soubor, který použijete pro extrakci textu. Umístěte jej do adresáře na vašem počítači (budeme jej označovat jako `YOUR DOCUMENT DIRECTORY`).

## Importovat balíčky

V horní části kódu budete muset importovat potřebné jmenné prostory pro práci s Aspose.PDF:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## Krok 1: Načtěte dokument PDF

Před extrakcí textu musíme načíst PDF dokument do paměti. V tomto kroku otevřete PDF pomocí Aspose.PDF. `Document` třída. To vám umožní přístup ke všem stránkám a obsahu v souboru.

```csharp
// Definujte cestu k dokumentu PDF
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Načíst PDF dokument
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Zde používáme `Document pdfDocument = new Document(dataDir + "input.pdf");` načíst PDF. `dataDir` Proměnná obsahuje cestu k adresáři vašeho PDF souboru. To nám umožní přístup k celému dokumentu, což nám umožní procházet stránkami a extrahovat obsah.

## Krok 2: Nastavení nástroje pro tvorbu řetězců pro ukládání textu

Nyní, když je dokument načten, potřebujeme způsob, jak uložit extrahovaný text. K tomu použijeme `StringBuilder` což umožňuje efektivní zřetězení řetězců.

```csharp
// StringBuilder pro uchování extrahovaného textu
StringBuilder builder = new StringBuilder();
```

Inicializujeme `StringBuilder` instance, která bude shromažďovat text extrahovaný z každé stránky. Je to efektivnější způsob, jak zpracovat velké řetězce ve srovnání s běžným zřetězením řetězců ve smyčce.

## Krok 3: Procházení stránek PDF

Dále projdeme každou stránku PDF dokumentu, abychom extrahovali text. Každou stránku zpracujeme jednotlivě pomocí `TextDevice` třída, která je zodpovědná za převod obsahu PDF do textového formátu.

```csharp
// Procházet všechny stránky v PDF
foreach (Page pdfPage in pdfDocument.Pages)
{
    // Zpracovat každou stránku pro extrakci textu
}
```

Tato smyčka prochází každou stránkou PDF (`pdfDocument.Pages`). Pro každou stránku extrahujeme text a přidáme ho do našeho `StringBuilder`.

## Krok 4: Extrahujte text z každé stránky

Nyní nastavíme proces extrakce textu pro každou stránku. Zde vytvoříme `TextDevice` objekt a použít ho ke zpracování stránek PDF. `TextDevice` extrahuje nezpracovaný nebo formátovaný text na základě nastavených možností extrakce.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // Vytvořte textové zařízení pro extrakci textu
    TextDevice textDevice = new TextDevice();
    
    // Nastavte možnosti extrakce textu na režim „Čistý“
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // Extrahovat text z aktuální stránky a uložit jej do paměťového proudu
    textDevice.Process(pdfPage, textStream);

    // Převod paměťového proudu na text
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // Přidejte extrahovaný text do StringBuilderu
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: Ten `TextDevice` Třída se používá k extrakci textu z PDF.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: Tato možnost extrahuje nezpracovaný text bez zachování formátování, jako jsou písma nebo pozice. Můžete také použít `TextFormattingMode.Raw` pokud potřebujete větší kontrolu nad formátováním.
- `textDevice.Process(pdfPage, textStream);`: Zpracuje každou stránku PDF a uloží extrahovaný text do `MemoryStream`.
- Nakonec převedeme text z `MemoryStream` do řetězce a přidat ho k `StringBuilder`.

## Krok 5: Uložení extrahovaného textu do souboru

Po zpracování všech stránek je text uložen do `StringBuilder`Posledním krokem je uložení extrahovaného textu do souboru.

```csharp
// Definujte výstupní cestu pro textový soubor
dataDir = dataDir + "input_Text_Extracted_out.txt";

// Uložit extrahovaný text do souboru
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`: Tím se zapíše celý obsah `StringBuilder` do textového souboru.
- Cesta k výstupnímu souboru se nastaví přidáním názvu souboru (`"input_Text_Extracted_out.txt"`) k `dataDir` cesta.

## Závěr

Extrakce textu z PDF pomocí Aspose.PDF pro .NET je jednoduchý a efektivní proces. Dodržováním kroků uvedených v této příručce můžete snadno otevírat dokumenty PDF, procházet stránky a extrahovat text do textového souboru. To je obzvláště užitečné pro zpracování velkých objemů dat PDF, provádění analýzy textu nebo převod dokumentů pro další manipulaci.

S Aspose.PDF se neomezujete pouze na extrakci textu – můžete pracovat s anotacemi, manipulovat s obrázky nebo dokonce převádět PDF soubory do jiných formátů, jako je HTML nebo Word. Flexibilita a výkon této knihovny z ní činí neocenitelný nástroj pro správu PDF v aplikacích .NET.

## Často kladené otázky

### Může Aspose.PDF extrahovat text z PDF souborů založených na obrázcích?
Ne, Aspose.PDF je navržen tak, aby extrahoval text z PDF souborů založených na obsahu. Pro PDF soubory založené na obrázcích je potřeba technologie OCR.

### Zachovává Aspose.PDF formátování při extrakci textu?
Ve výchozím nastavení se text extrahuje bez formátování, ale pokud chcete zachovat formátování, můžete upravit možnosti extrakce.

### Mohu extrahovat text z určitého rozsahu stránek?
Ano, kód můžete upravit tak, aby se smyčka procházela přes určitý rozsah stránek místo všech stránek.

### Jaké jsou režimy extrakce textu v Aspose.PDF?
Aspose.PDF nabízí dva režimy: Raw a Pure. Režim Raw se snaží zachovat původní rozvržení, zatímco režim Pure extrahuje pouze text bez formátování.

### Je Aspose.PDF pro .NET kompatibilní s .NET Core?
Ano, Aspose.PDF pro .NET je plně kompatibilní s .NET Core a .NET Framework.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}