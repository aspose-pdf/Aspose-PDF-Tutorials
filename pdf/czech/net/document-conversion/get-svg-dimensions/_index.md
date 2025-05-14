---
"description": "Naučte se, jak pomocí tohoto podrobného návodu používat Aspose.PDF pro .NET k převodu souborů SVG do PDF. Ideální pro vývojáře, kteří chtějí manipulovat s PDF soubory."
"linktitle": "Získat SVG rozměry"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Získat SVG rozměry"
"url": "/cs/net/document-conversion/get-svg-dimensions/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Získat SVG rozměry

## Zavedení

Vítejte ve světě Aspose.PDF pro .NET! Pokud chcete programově manipulovat s PDF soubory, jste na správném místě. Aspose.PDF je výkonná knihovna, která vývojářům umožňuje snadno vytvářet, upravovat a převádět PDF dokumenty. Ať už jste zkušený vývojář, nebo teprve začínáte, tato příručka vás provede základy používání Aspose.PDF pro .NET se zaměřením na to, jak získat SVG rozměry a převést je do formátu PDF.

## Předpoklady

Než se pustíme do samotného kódu, je potřeba mít připraveno několik věcí:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Je to vývojové prostředí (IDE), které budeme v tomto tutoriálu používat.
2. .NET Framework: Ujistěte se, že máte nainstalovaný .NET Framework. Soubor Aspose.PDF podporuje různé verze, proto zkontrolujte [dokumentace](https://reference.aspose.com/pdf/net/) kvůli kompatibilitě.
3. Knihovna Aspose.PDF: Nejnovější verzi souboru Aspose.PDF pro .NET si můžete stáhnout z [odkaz ke stažení](https://releases.aspose.com/pdf/net/)Pokud si to chcete nejdříve vyzkoušet, můžete si také pořídit [bezplatná zkušební verze](https://releases.aspose.com/).
4. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět příkladům.

## Importovat balíčky

Chcete-li začít, musíte importovat potřebné balíčky. Zde je návod, jak to udělat:

1. Otevřete svůj projekt ve Visual Studiu.
2. V Průzkumníku řešení klikněte pravým tlačítkem myši na svůj projekt a vyberte možnost „Spravovat balíčky NuGet“.
3. Vyhledejte „Aspose.PDF“ a nainstalujte balíček.

Jakmile máte balíček nainstalovaný, můžete začít s kódováním!

## Krok 1: Nastavení projektu

### Vytvořit nový projekt

Nejdříve si vytvořme nový projekt v C# ve Visual Studiu.

- Otevřete Visual Studio a vyberte „Vytvořit nový projekt“.
- Vyberte možnost „Konzolová aplikace (.NET Framework)“ a klikněte na tlačítko „Další“.
- Pojmenujte svůj projekt (např. „AsposePDFExample“) a klikněte na „Vytvořit“.

### Přidat pomocí direktiv

Nyní, když je váš projekt nastavený, je třeba přidat potřebné direktivy using na začátek `Program.cs` soubor:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

To vám umožní přístup ke třídám a metodám poskytovaným knihovnou Aspose.PDF.

## Krok 2: Načtení dokumentu SVG

### Definování adresáře dokumentů

Před načtením dokumentu SVG je nutné zadat cestu k adresáři s dokumenty. Nahraďte `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kde se nachází váš SVG soubor.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

### Načíst dokument SVG

Nyní si načtěme SVG dokument pomocí `SvgLoadOptions` třída. Tato třída umožňuje upravit velikost stránky na základě obsahu SVG.

```csharp
var loadopt = new SvgLoadOptions();
loadopt.AdjustPageSize = true;
var svgDoc = new Document(dataDir + "GetSVGDimensions.svg", loadopt);
```

## Krok 3: Úprava okrajů stránky

Aby se obsah SVG dokonale vešel do PDF, je třeba nastavit okraje stránky na nulu. Tento krok je klíčový pro zachování integrity rozměrů SVG.

```csharp
svgDoc.Pages[1].PageInfo.Margin.Top = 0;
svgDoc.Pages[1].PageInfo.Margin.Left = 0;
svgDoc.Pages[1].PageInfo.Margin.Bottom = 0;
svgDoc.Pages[1].PageInfo.Margin.Right = 0;
```

## Krok 4: Uložte dokument jako PDF

Konečně je čas uložit dokument SVG jako PDF. Název výstupního souboru a cestu můžete zadat takto:

```csharp
svgDoc.Save(dataDir + "GetSVGDimensions_out.pdf");
```

to je vše! Úspěšně jste převedli soubor SVG do PDF pomocí Aspose.PDF pro .NET.

## Závěr

Gratulujeme! Právě jste dokončili jednoduchý, ale účinný úkol s Aspose.PDF pro .NET. Dodržováním tohoto návodu jste se naučili, jak načíst dokument SVG, upravit jeho okraje a uložit jej jako PDF. Možnosti s Aspose.PDF jsou nekonečné a toto je jen špička ledovce. Ať už chcete vytvářet složité PDF soubory, manipulovat s existujícími nebo převádět mezi formáty, Aspose.PDF vám s tím pomůže. Tak na co čekáte? Ponořte se hlouběji do... [dokumentace](https://reference.aspose.com/pdf/net/) a prozkoumejte všechny funkce, které tato knihovna nabízí!

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům programově vytvářet, upravovat a převádět PDF dokumenty.

### Jak nainstaluji Aspose.PDF?
Soubor Aspose.PDF si můžete nainstalovat pomocí Správce balíčků NuGet ve Visual Studiu nebo si jej stáhnout z [místo](https://releases.aspose.com/pdf/net/).

### Mohu používat Aspose.PDF zdarma?
Ano, Aspose nabízí [bezplatná zkušební verze](https://releases.aspose.com/) abyste si knihovnu mohli před zakoupením vyzkoušet.

### Kde najdu podporu pro Aspose.PDF?
Podporu můžete získat od [Fórum Aspose](https://forum.aspose.com/c/pdf/10).

### Jak získám dočasnou licenci pro Aspose.PDF?
Můžete požádat o [dočasná licence](https://purchase.aspose.com/temporary-license/) z webových stránek Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}