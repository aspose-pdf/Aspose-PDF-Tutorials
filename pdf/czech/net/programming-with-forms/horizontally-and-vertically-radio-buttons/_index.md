---
"description": "Naučte se, jak v PDF pomocí Aspose.PDF pro .NET vytvářet vodorovně a svisle zarovnané přepínače v tomto podrobném návodu."
"linktitle": "Přepínače horizontálně a vertikálně"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přepínače horizontálně a vertikálně"
"url": "/cs/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přepínače horizontálně a vertikálně

## Zavedení

Vytváření interaktivních PDF formulářů může výrazně zlepšit uživatelský zážitek, zejména pokud jde o shromažďování informací. Jedním z nejběžnějších prvků formuláře je přepínač, který uživatelům umožňuje vybrat jednu možnost z nabídky. V tomto tutoriálu se podíváme na to, jak vytvořit vodorovně a svisle zarovnané přepínače pomocí Aspose.PDF pro .NET. Ať už jste zkušený vývojář, nebo teprve začínáte, tento průvodce vás krok za krokem provede celým procesem a zajistí, že budete mít jasnou představu o každé části.

## Předpoklady

Než se ponoříte do kódu, měli byste mít splněno několik předpokladů:

1. Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF. Můžete si ji stáhnout z [místo](https://releases.aspose.com/pdf/net/).
2. Visual Studio: Vývojové prostředí, kde můžete psát a testovat svůj kód.
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.

## Importovat balíčky

Chcete-li začít, musíte do svého projektu C# importovat potřebné balíčky. Zde je návod, jak to udělat:

### Vytvořit nový projekt

Otevřete Visual Studio a vytvořte nový projekt v C#. Pro zjednodušení si můžete vybrat konzolovou aplikaci.

### Přidat odkaz na Aspose.PDF

1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte možnost „Spravovat balíčky NuGet“.
3. Vyhledejte soubor „Aspose.PDF“ a nainstalujte nejnovější verzi.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

Nyní, když máte vše nastavené, pojďme rozebrat kód a vytvořit vodorovně a svisle zarovnané přepínače.

## Krok 1: Nastavení adresáře dokumentů

V tomto kroku definujeme cestu k adresáři, kde budou uloženy vaše PDF dokumenty.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kam chcete soubor PDF uložit. To je klíčové, protože programu říká, kde má hledat vstupní soubory a kam má ukládat výstup.

## Krok 2: Načtěte existující dokument PDF

Dále musíme načíst PDF dokument, se kterým budeme pracovat. To se provádí pomocí `FormEditor` třída.

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

Zde vytvoříme instanci `FormEditor` a svázat jej s existujícím PDF souborem s názvem `input.pdf`Ujistěte se, že tento soubor existuje ve vámi zadaném adresáři.

## Krok 3: Konfigurace vlastností přepínače

Nyní nastavme některé vlastnosti pro naše přepínače. Patří sem mezera mezi tlačítky, jejich orientace a jejich velikost.

```csharp
formEditor.RadioGap = 4; // Vzdálenost mezi možnostmi přepínačů
formEditor.RadioHoriz = true; // Pro vodorovné zarovnání nastavte na hodnotu true.
formEditor.RadioButtonItemSize = 20; // Velikost přepínače
formEditor.Facade.BorderWidth = 1; // Šířka okraje
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // Barva okraje
```

Tyto vlastnosti pomohou definovat, jak se budou přepínací tlačítka zobrazovat v PDF. `RadioGap` vlastnost řídí prostor mezi tlačítky, zatímco `RadioHoriz` určuje jejich rozvržení.

## Krok 4: Přidání horizontálních přepínačů

Nyní přidejme do PDF vodorovné přepínače.

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

V tomto kódu definujeme položky pro přepínače a přidáme je do PDF. `AddField` Metoda přijímá několik parametrů, včetně typu pole, názvu pole a souřadnic pro umístění.

## Krok 5: Přidání vertikálních přepínačů

Dále přidáme vertikální přepínače. Abychom to dokázali, musíme změnit orientaci zpět na vertikální.

```csharp
formEditor.RadioHoriz = false; // Pro svislé zarovnání nastavte na hodnotu false.
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

Stejně jako předtím definujeme položky a přidáváme je do PDF, ale tentokrát budou zarovnány svisle.

## Krok 6: Uložení dokumentu PDF

Nakonec musíme upravený dokument PDF uložit.

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

Tento kód uloží PDF s nově přidanými přepínači. Nezapomeňte zkontrolovat zadaný adresář pro výstupní soubor.

## Závěr

Vytváření přepínačů v PDF pomocí Aspose.PDF pro .NET je jednoduchý proces. Dodržováním kroků popsaných v tomto tutoriálu můžete snadno přidat vodorovně i svisle zarovnané přepínače do formulářů PDF. To nejen vylepší interaktivitu vašich dokumentů, ale také zlepší celkový uživatelský zážitek. Tak do toho a vyzkoušejte to!

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je výkonná knihovna, která umožňuje vývojářům programově vytvářet, manipulovat a převádět PDF dokumenty.

### Mohu používat Aspose.PDF zdarma?
Ano, Aspose nabízí bezplatnou zkušební verzi, kterou můžete použít k otestování knihovny. Můžete si ji stáhnout. [zde](https://releases.aspose.com/).

### Jak získám podporu pro Aspose.PDF?
Podporu můžete získat návštěvou [Fórum Aspose](https://forum.aspose.com/c/pdf/10).

### Je možné pomocí Aspose.PDF vytvářet další prvky formuláře?
Rozhodně! Aspose.PDF podporuje různé prvky formulářů, včetně textových polí, zaškrtávacích políček a rozbalovacích nabídek.

### Kde mohu koupit Aspose.PDF pro .NET?
Soubor Aspose.PDF pro .NET si můžete zakoupit od [stránka nákupu](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}