---
"description": "Naučte se, jak nastavit výchozí název písma při vykreslování PDF do obrázků pomocí Aspose.PDF pro .NET. Tato příručka zahrnuje předpoklady, podrobné pokyny a nejčastější dotazy."
"linktitle": "Nastavit výchozí název písma"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Nastavit výchozí název písma"
"url": "/cs/net/document-conversion/set-default-font-name/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavit výchozí název písma

## Zavedení

Už jste někdy zkusili vykreslit PDF dokument do obrázku, ale zjistili jste, že písma prostě nevypadají správně? Možná je text zkreslený, nebo původní písmo není podporováno. A tady může nastavení výchozího písma zachránit situaci! Pomocí Aspose.PDF pro .NET můžete snadno nastavit výchozí písmo pro vykreslování PDF a zajistit tak, aby váš dokument vypadal ostře a profesionálně. V tomto tutoriálu vás provedeme tím, jak nastavit výchozí název písma při vykreslování PDF do obrázku. Na konci tohoto průvodce budete mít dovednosti, které vám pomohou s vykreslováním PDF, které se vám postaví do cesty. Připraveni? Pojďme se do toho pustit!

## Předpoklady

Než se pustíme do kódu, je třeba mít připraveno několik věcí:

- Aspose.PDF pro .NET: Tuto výkonnou knihovnu budeme používat k manipulaci s naším PDF dokumentem. Můžete si ji stáhnout z [Webové stránky Aspose](https://releases.aspose.com/pdf/net/).
- Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Toto bude naše vývojové prostředí.
- .NET Framework: Ujistěte se, že máte nainstalovaný .NET Framework. Soubor Aspose.PDF pro .NET podporuje různé verze, proto si ověřte dokumentaci, která odpovídá vašim potřebám.
- Dokument PDF: Budete potřebovat vzorový dokument PDF. Pokud žádný nemáte, vytvořte si jednoduchý PDF nebo si vzorek stáhněte online.

Jakmile máte vše nastavené, můžeme začít s kódováním!

## Importovat balíčky

Než se ponoříme do kódu, je nezbytné importovat potřebné balíčky. Tím zajistíme přístup ke všem třídám a metodám, které pro náš projekt potřebujeme.

```csharp
using Aspose.Pdf.Devices;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Tyto importy jsou zásadní, protože přinášejí potřebné jmenné prostory pro zpracování manipulace s PDF, vykreslování obrázků a operací se streamováním souborů.

## Krok 1: Nastavení cesty k projektu a dokumentu

Nejprve si nastavme cestu k adresáři, kde se nachází váš PDF dokument. To bude váš výchozí bod pro manipulaci s PDF souborem.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```
Zde, `dataDir` je adresář, kde se nachází váš dokument PDF. Nezapomeňte nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou k vašemu dokumentu. To je nezbytné, protože kód potřebuje vědět, odkud má soubor PDF načíst.

## Krok 2: Načtěte dokument PDF

Nyní, když máme cestu k dokumentu, je dalším krokem načtení PDF dokumentu do paměti, abychom s ním mohli začít pracovat.

```csharp
using (Document pdfDocument = new Document(dataDir + "input.pdf"))
```
Používáme `Document` třída z knihovny Aspose.PDF pro načtení našeho PDF souboru. Tato třída poskytuje různé metody a vlastnosti pro práci s PDF dokumentem. `"input.pdf"` by měl být nahrazen skutečným názvem souboru PDF. Tento soubor bude použit jako vstup pro vykreslení.

## Krok 3: Vytvořte obrazový stream pro výstup

Jakmile je dokument načten, musíme nastavit stream pro uložení vykresleného obrázku. Zde bude uložen výstupní obrázek.

```csharp
using (FileStream imageStream = new FileStream(dataDir + "SetDefaultFontName.png", FileMode.Create))
```
Ten/Ta/To `FileStream` Třída se používá k vytvoření nového souboru, kam bude uložen vykreslený obrázek. V tomto příkladu ukládáme obrázek jako `"SetDefaultFontName.png"`Ten/Ta/To `FileMode.Create` zajišťuje vytvoření nového souboru nebo přepsání existujícího souboru.

## Krok 4: Nastavení rozlišení obrázku

Před vykreslením PDF do obrázku je důležité nastavit rozlišení. To určuje kvalitu a jasnost výstupního obrazu.

```csharp
Resolution resolution = new Resolution(300);
```
Ten/Ta/To `Resolution` Třída nastavuje rozlišení výstupního obrazu. Zde jsme zvolili rozlišení 300 DPI (bodů na palec), což je standard pro vysoce kvalitní obrázky. To zajišťuje, že text a grafika ve vašem PDF se vykreslí jasně bez ztráty detailů.

## Krok 5: Konfigurace zařízení PNG

Dále musíme nakonfigurovat zařízení, které bude zpracovávat vykreslování PDF do obrázku PNG.

```csharp
PngDevice pngDevice = new PngDevice(resolution);
```
Ten/Ta/To `PngDevice` Třída je zodpovědná za vykreslení PDF dokumentu do obrázku PNG. Předáním metody `resolution` Pokud proti tomu vzneseme námitku, zajistíme, aby byl obrázek vytvořen se zadaným DPI.

## Krok 6: Nastavení výchozího názvu písma

Zde je klíčová část – nastavení výchozího názvu písma. Toto bude záložní písmo pro případ, že původní písmo v PDF není k dispozici.

```csharp
RenderingOptions ro = new RenderingOptions();
ro.DefaultFontName = "Arial";
pngDevice.RenderingOptions = ro;
```
Vytvoříme instanci `RenderingOptions` a nastavit jeho `DefaultFontName` majetek `"Arial"`To znamená, že pokud nelze v PDF najít původní písmo, použije se místo něj písmo Arial. Tento krok je klíčový pro zachování čitelnosti a vzhledu textu ve vykresleném obrázku.

## Krok 7: Vykreslení stránky PDF do obrázku

Konečně, když je vše nastaveno, můžeme nyní vykreslit první stránku PDF dokumentu do obrázku a uložit ji pomocí datového proudu souborů, který jsme vytvořili dříve.

```csharp
pngDevice.Process(pdfDocument.Pages[1], imageStream);
```
Ten/Ta/To `Process` metoda `PngDevice` Třída se používá k vykreslení zadané stránky PDF (v tomto případě první stránky) do obrázku. Výstup se poté uloží do třídy `imageStream`Tento krok převede stránku PDF do obrázku PNG se zadaným rozlišením a výchozím písmem.

## Krok 8: Zavřete souborový stream a dokument PDF

Po vykreslení obrázku je nezbytné zavřít souborový stream a PDF dokument, aby se uvolnily prostředky.

```csharp
imageStream.Close();
pdfDocument.Dispose();
```
Zavření `imageStream` zajišťuje, že soubor bude správně uložen a nedojde ke ztrátě dat. Likvidace `pdfDocument` uvolňuje paměť a zdroje a zabraňuje potenciálním únikům paměti.

## Závěr

A tady to máte! S pouhými několika řádky kódu jste se naučili, jak nastavit výchozí název písma při vykreslování PDF do obrázku pomocí Aspose.PDF pro .NET. Tato dovednost je neuvěřitelně užitečná, zejména při práci s PDF soubory, které mohou obsahovat nepodporovaná písma. Nastavením výchozího písma zajistíte, že si vykreslené obrázky zachovají čitelnost a profesionální vzhled.

## Často kladené otázky

### Co se stane, když zadané výchozí písmo není v systému nainstalováno?
Pokud je výchozí písmo zadané v `RenderingOptions` Pokud není v systému nainstalován, Aspose.PDF použije systémem definované záložní písmo.

### Mohu jako výchozí písmo použít jiná písma než Arial?
Rozhodně! Jako výchozí písmo můžete nastavit libovolné písmo, které je nainstalováno ve vašem systému.

### Je možné vykreslit více stránek PDF najednou do obrázků?
Ano, můžete procházet stránkami PDF a vykreslit každou stránku jednotlivě pomocí stejného postupu.

### Ovlivňuje nastavení vysokého rozlišení výkon vykreslování PDF?
Ano, vyšší rozlišení povedou k větším obrazovým souborům a mohou prodloužit dobu vykreslování, ale také vytvoří jasnější obrázky.

### Mohu PDF vykreslit do jiných obrazových formátů než PNG?
Ano, Aspose.PDF podporuje vykreslování do různých obrazových formátů, jako jsou JPEG, BMP a TIFF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}