---
"description": "V tomto komplexním tutoriálu se naučte, jak přizpůsobit čísla stránek při přidávání obsahu do dokumentů PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Přizpůsobení čísel stránek při přidávání obsahu"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přizpůsobení čísel stránek při přidávání obsahu"
"url": "/cs/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přizpůsobení čísel stránek při přidávání obsahu

## Zavedení

Ve světě správy dokumentů kralují PDF soubory. Jsou to formáty, které jsou nejoblíbenější pro sdílení a uchovávání dokumentů napříč různými platformami. Co se ale stane, když chcete své PDF dokumenty vylepšit funkcemi, jako je obsah (TOC)? A právě zde přichází na řadu Aspose.PDF pro .NET! Tato výkonná knihovna umožňuje vývojářům snadno manipulovat s PDF soubory a bez námahy přidávat, upravovat a přizpůsobovat obsah. V tomto tutoriálu se ponoříme do toho, jak přizpůsobit čísla stránek a zároveň přidat obsah do PDF dokumentů pomocí Aspose.PDF pro .NET. Takže, chyťte svou programátorskou čepici a pojďme na to!

## Předpoklady

Než se pustíme do samotného kódu, je potřeba mít připraveno několik věcí:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Toto bude naše vývojové prostředí.
2. Aspose.PDF pro .NET: Je třeba si stáhnout a nainstalovat knihovnu Aspose.PDF. Najdete ji [zde](https://releases.aspose.com/pdf/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.
4. Ukázkový soubor PDF: Mějte připravený ukázkový soubor PDF, se kterým můžeme pracovat. Můžete si vytvořit jednoduchý soubor nebo si stáhnout existující PDF.

## Importovat balíčky

Pro začátek musíme importovat potřebné balíčky. Otevřete projekt Visual Studia a přidejte odkaz na knihovnu Aspose.PDF. Můžete to provést pomocí Správce balíčků NuGet:

1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte možnost „Spravovat balíčky NuGet“.
3. Vyhledejte soubor „Aspose.PDF“ a nainstalujte jej.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Jakmile máte knihovnu nainstalovanou, můžete začít programovat!

## Krok 1: Nastavení adresáře dokumentů

Nejdříve si musíme nastavit adresář s dokumenty. Zde budeme ukládat vstupní a výstupní PDF soubory. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

V tomto úryvku nahraďte `YOUR DOCUMENT DIRECTORY` se skutečnou cestou, kde se nacházejí vaše soubory PDF. To nám pomůže načíst existující PDF a uložit upravenou verzi.

## Krok 2: Načtěte existující soubor PDF

Nyní, když máme nastavený adresář dokumentů, načtěme existující soubor PDF. 

```csharp
Document doc = new Document(inFile);
```

Zde vytváříme nový `Document` objekt předáním cesty ke vstupnímu souboru. To nám umožňuje programově manipulovat s obsahem PDF.

## Krok 3: Vložení nové stránky pro obsah

Dále musíme v našem PDF vytvořit novou stránku, kde bude umístěn obsah.

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

Tento řádek vloží novou stránku na začátek dokumentu. Obsah se zobrazí na této stránce.

## Krok 4: Vytvořte informace o obsahu

Nyní si vytvořme objekt, který bude reprezentovat informace o obsahu.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

V tomto kroku vytvoříme `TocInfo` objekt a nastavíme jeho název na „Obsah“. Také upravíme velikost a styl písma. `PageNumbersPrefix` je nastaveno na „P“, což bude předčíslí stránek v obsahu.

## Krok 5: Přidání nadpisů do obsahu

A teď přichází ta zábavná část! Projdeme si stránky dokumentu a přidáme nadpisy do obsahu.

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

V této smyčce vytvoříme nový `Heading` objekt pro každou stránku. Pro každý nadpis nastavíme cílovou stránku a zadáme text, který se má zobrazit, což je „Stránka X“, kde X je číslo stránky. Nakonec přidáme nadpis na stránku s obsahem.

## Krok 6: Uložte aktualizovaný dokument

Po přidání všech potřebných nadpisů je čas uložit náš aktualizovaný dokument.

```csharp
doc.Save(outFile);
```

Tento řádek uloží upravený PDF soubor včetně obsahu. Nyní můžete otevřít výstupní soubor a zobrazit si svůj přizpůsobený obsah!

## Závěr

A tady to máte! Úspěšně jste si upravili čísla stránek a zároveň přidali obsah do svého PDF dokumentu pomocí Aspose.PDF pro .NET. Tato výkonná knihovna usnadňuje manipulaci s PDF soubory a pomocí několika řádků kódu můžete své dokumenty výrazně vylepšit. Ať už vytváříte zprávy, elektronické knihy nebo jakýkoli jiný typ PDF, obsah může výrazně zlepšit navigaci pro vaše čtenáře. Tak na co čekáte? Ponořte se do Aspose.PDF a začněte vytvářet úžasné PDF soubory ještě dnes!

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům programově vytvářet, manipulovat a převádět PDF dokumenty.

### Mohu používat Aspose.PDF zdarma?
Ano, Aspose nabízí bezplatnou zkušební verzi, kterou můžete použít k prozkoumání funkcí knihovny. Můžete si ji stáhnout. [zde](https://releases.aspose.com/).

### Jak získám podporu pro Aspose.PDF?
Podporu můžete získat na fóru Aspose. [zde](https://forum.aspose.com/c/pdf/10).

### Je k dispozici dočasná licence?
Ano, můžete požádat o dočasnou licenci pro Aspose.PDF [zde](https://purchase.aspose.com/temporary-license/).

### Kde si mohu koupit Aspose.PDF pro .NET?
Můžete si zakoupit Aspose.PDF pro .NET [zde](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}