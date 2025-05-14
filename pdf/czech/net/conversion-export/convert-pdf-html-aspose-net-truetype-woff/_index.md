---
"date": "2025-04-10"
"description": "Naučte se, jak převádět PDF soubory do HTML pomocí Aspose.PDF pro .NET se zachováním písem v TrueType (TTF) a Web Open Font Format (WOFF). Podrobný návod s příklady kódu."
"title": "Převod PDF do HTML pomocí Aspose.PDF pro .NET a zachování fontů ve formátech TTF a WOFF"
"url": "/cs/net/conversion-export/convert-pdf-html-aspose-net-truetype-woff/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Převod PDF do HTML pomocí Aspose.PDF pro .NET: Zachování písem ve formátech TTF a WOFF

## Zavedení
Máte potíže se zachováním původního rozvržení a integrity písma vašich PDF dokumentů při jejich převodu do HTML? Převod PDF se zachováním jejich písem může být náročný, ale nemusí být. S **Aspose.PDF pro .NET**můžete snadno převést soubory PDF do formátu HTML a zároveň zajistit, aby písma byla zachována ve formátu TrueType (TTF) nebo Web Open Font Format (WOFF). Tato příručka vás krok za krokem provede celým procesem.

V tomto tutoriálu se budeme zabývat:
- Jak ukládat fonty jako TTF při převodu PDF do HTML
- Konfigurace převodu pro ukládání písem jako WOFF
- Ukládání písem ve všech formátech během převodu

Do konce tohoto článku budete mít komplexní znalosti o efektivním používání Aspose.PDF pro .NET k správě konverzí písem. Než začneme, pojďme se ponořit do potřebných předpokladů.

## Předpoklady
Než se pustíte do převodu PDF do HTML pomocí Aspose.PDF, ujistěte se, že splňujete tyto požadavky:

### Požadované knihovny a závislosti
- **Aspose.PDF pro .NET**Tato knihovna je nezbytná pro zpracování PDF souborů v aplikacích .NET.
- **.NET Framework nebo .NET Core/5+**Ujistěte se, že vaše vývojové prostředí tyto frameworky podporuje.

### Požadavky na nastavení prostředí
Ujistěte se, že vaše vývojové prostředí (např. Visual Studio) je nastaveno pro práci s knihovnou Aspose.PDF. Budete potřebovat:
- Projekt vytvořený v .NET Frameworku nebo .NET Core/5+
- Přístup k NuGet Package Manageru pro instalaci knihoven

### Předpoklady znalostí
Základní znalost jazyka C# a znalost práce se soubory v .NET bude výhodou.

## Nastavení Aspose.PDF pro .NET
Pro začátek je potřeba nainstalovat knihovnu Aspose.PDF. Můžete to provést pomocí různých správců balíčků:

**Rozhraní příkazového řádku .NET:**
```bash
dotnet add package Aspose.PDF
```

**Konzola Správce balíčků:**
```powershell
Install-Package Aspose.PDF
```

**Uživatelské rozhraní Správce balíčků NuGet:**
Vyhledejte soubor „Aspose.PDF“ a nainstalujte nejnovější verzi.

### Získání licence
Můžete si pořídit dočasnou licenci nebo si od Aspose zakoupit plnou licenci. Bezplatná zkušební verze vám umožní prozkoumat všechny funkce bez omezení, což je ideální pro počáteční testování. Zde je návod, jak nastavit prostředí s licencí:
1. Žádost o [dočasná licence](https://purchase.aspose.com/temporary-license/).
2. Před provedením jakýchkoli operací použijte licenci ve své aplikaci pomocí následujícího úryvku kódu:

```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to your License File");
```

## Průvodce implementací
Rozdělme si implementaci do tří klíčových funkcí: ukládání písem ve formátu TTF, WOFF a všech ostatních formátech.

### Uložit písma jako TTF
**Přehled**
Tato funkce umožňuje ukládat písma z dokumentu PDF ve formátu TrueType (TTF) během jeho převodu do HTML. Tím je zajištěno, že během převodu bude zachována vizuální integrita vašich písem.

#### Postupná implementace
1. **Inicializace dokumentu a možností:**
   Začněte načtením PDF dokumentu pomocí Aspose.PDF `Document` třída a nastavení `HtmlSaveOptions`.

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   string outFile = Path.GetFullPath(dataDir + "/36192_out.html");
   Document doc = new Document(dataDir + "/input.pdf");

   HtmlSaveOptions saveOptions = new HtmlSaveOptions();
   ```

2. **Konfigurace možností ukládání:**
   Nastavte potřebné možnosti pro zachování rozvržení a určete režim ukládání písma.

   ```csharp
   saveOptions.FixedLayout = true; // Zachovat původní rozvržení PDF
   saveOptions.SplitIntoPages = false; // Nerozdělovat do více HTML souborů
   saveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsTTF;
   ```

3. **Příprava výstupního adresáře:**
   Ujistěte se, že výstupní adresář je připraven pro uložení propojených souborů písem.

   ```csharp
   string linkedFilesFolder = Path.GetDirectoryName(outFile) + "/36192_files";
   if (Directory.Exists(linkedFilesFolder))
   {
       Directory.Delete(linkedFilesFolder, true); // Vymazat existující soubory
   }
   ```

4. **Uložit dokument:**
   Nakonec uložte dokument s požadovanými možnostmi.

   ```csharp
doc.Uložit(outSoubor, MožnostiUložení);
```

### Save Fonts as WOFF
**Overview**
Configuring Aspose.PDF to save fonts in Web Open Font Format (WOFF) is beneficial for web optimization, reducing font file sizes while maintaining quality.

#### Step-by-Step Implementation
1. **Configure Save Options:**
   Initialize `HtmlSaveOptions` and set the font saving mode to WOFF.

   ```csharp
   HtmlSaveOptions woffSaveOptions = new HtmlSaveOptions();
   woffSaveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsWOFF;
   ```

2. **Použít možnosti uložení:**
   Tyto možnosti použijte při ukládání dokumentu, podobně jako u metody TTF.

### Ukládání písem ve všech formátech
**Přehled**
Pro zajištění maximální kompatibility a flexibility můžete během převodu uložit písma ve všech dostupných formátech.

#### Postupná implementace
1. **Inicializace dokumentu a možností:**
   Načtěte dokument PDF a nakonfigurujte jej `HtmlSaveOptions`.

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document doc = new Document(dataDir + "/input.pdf");
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
   ```

2. **Konfigurace možností ukládání:**
   Nastavte možnosti pro uložení všech formátů písem a zachování rozvržení.

   ```csharp
   htmlOptions.FixedLayout = true;
   htmlOptions.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsExternalPngFilesReferencedViaSvg;
   htmlOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.SaveInAllFormats;
   ```

3. **Uložit dokument:**
   Uložte dokument s tímto nastavením.

   ```csharp
doc.Uložit(datovýAdresář + "/ThreeSetFonts_out.html", htmlMožnosti);
```

## Practical Applications
Converting PDFs to HTML with font preservation has numerous real-world applications:
1. **Web Publishing**: Ensure that documents retain their original styling when published online.
2. **Content Portability**: Easily move content between desktop and web environments without loss of formatting.
3. **Document Archiving**: Maintain document integrity during long-term storage or migration.

Integration possibilities include embedding these conversions into CMS systems, automated reporting tools, or digital libraries for seamless font management across platforms.

## Performance Considerations
When using Aspose.PDF for .NET, consider the following tips to optimize performance:
- **Memory Management**: Dispose of objects properly and utilize `using` statements where applicable.
- **Batch Processing**: Process documents in batches if dealing with large volumes to prevent memory overflow.
- **Resource Optimization**: Configure options like image compression and font subsetting to reduce file sizes.

## Conclusion
We've explored how to convert PDFs to HTML while preserving fonts using Aspose.PDF for .NET. Whether saving fonts as TTF, WOFF, or all formats, these techniques ensure your documents maintain their original design and readability in web environments. 

For further exploration, consider diving into Aspose's extensive documentation or experimenting with additional conversion features offered by the library.

## FAQ Section
1. **What are the benefits of converting PDFs to HTML using Aspose.PDF?**
   - Maintains document layout and font integrity.
   - Facilitates web publishing and content portability.
2. **Can I convert large PDF files efficiently with Aspose.PDF?**
   - Yes, by optimizing memory usage and processing in batches.
3. **How do I handle licensing for Aspose.PDF?**
   - Obtain a temporary or full license from the [Aspose website](https://purchase.aspose.com/buy).
4. **Is it possible to customize font settings during conversion?**
   - Yes, through various `HtmlSaveOptions`.
5. **What are some common issues when converting PDFs and how can I address them?**
   - Common issues include missing fonts or layout discrepancies. Adjusting save options and ensuring proper licensing can help mitigate these problems.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}