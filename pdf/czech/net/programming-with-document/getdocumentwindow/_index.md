---
"description": "Naučte se, jak používat funkci GetDocumentWindow v Aspose.PDF pro .NET k načtení informací o vlastnostech okna dokumentu PDF."
"linktitle": "Okno Získat dokument"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Okno Získat dokument"
"url": "/cs/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Okno Získat dokument

# Zavedení

Pracujete s PDF soubory a chcete mít větší kontrolu nad tím, jak se zobrazují po otevření? Ať už jde o skrytí panelu nabídek nebo změnu velikosti okna tak, aby se vešlo na první stránku, Aspose.PDF pro .NET vám poskytuje všechny nástroje, které potřebujete k přizpůsobení chování PDF souboru při otevření v prohlížeči. V tomto tutoriálu si ukážeme, jak v Aspose.PDF pro .NET načíst a manipulovat s nastavením okna dokumentu.


# Předpoklady

Než se pustíte do tutoriálu, ujistěte se, že máte splněny následující předpoklady:

- Aspose.PDF pro .NET nainstalovaný ve vašem vývojovém prostředí.
  - [Stáhnout Aspose.PDF pro .NET](https://releases.aspose.com/pdf/net/)
- Platná licence pro Aspose.PDF, nebo si můžete pořídit [bezplatná zkušební verze](https://releases.aspose.com/) nebo [dočasná licence](https://purchase.aspose.com/temporary-license/).
- Základní znalost .NET a C#.
- Visual Studio nebo jiné vhodné IDE.

# Importovat balíčky

Než začnete psát jakýkoli kód, budete muset importovat potřebné balíčky. Otevřete projekt a na začátek souboru C# přidejte následující jmenný prostor:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Tím získáte přístup ke všem třídám a metodám potřebným pro manipulaci s PDF dokumenty pomocí Aspose.PDF pro .NET.

Nyní si rozebereme proces načítání různých nastavení okna dokumentu. V tomto příkladu použijeme vzorový soubor PDF s názvem `GetDocumentWindow.pdf`.

## Krok 1: Nastavení cesty k adresáři dokumentů

Nejdříve musíme definovat cestu k našemu PDF souboru. Je nezbytné, abyste měli správnou cestu k souboru, abyste se vyhnuli chybám během provádění.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Zde nahraďte `"YOUR DOCUMENT DIRECTORY"` se skutečným adresářem, kde se nachází váš soubor PDF. Toto je váš pracovní adresář, odkud budete načítat dokument PDF.

## Krok 2: Otevřete dokument PDF

Nyní, když je cesta k souboru nastavena, je dalším krokem otevření dokumentu PDF pomocí Aspose.PDF. Tím se dokument načte do paměti a vy si můžete zobrazit jeho vlastnosti.

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

S tímto jednoduchým řádkem kódu jste úspěšně načetli soubor PDF do `pdfDocument` objekt, který vám nyní umožní přístup ke všem jeho vlastnostem.

## Krok 3: Zjištění stavu centrování okna

Dále zkontrolujme, zda má být okno dokumentu po otevření vycentrováno. Výchozí hodnota je `false`.

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

Pokud je výstup `true`, okno dokumentu se otevře uprostřed obrazovky. Jinak se otevře na výchozí pozici.

## Krok 4: Zkontrolujte směr textu

Dalším klíčovým aspektem vzhledu PDF je směr textu, který určuje, zda se text čte zleva doprava (L2R) nebo zprava doleva (R2L). Tuto informaci můžete získat pomocí následujícího kódu:

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

Výstup bude `L2R` pro text zleva doprava a `R2L` pro text zprava doleva. Toto nastavení je obzvláště užitečné pro dokumenty v jazycích, jako je arabština nebo hebrejština.

## Krok 5: Zobrazení názvu dokumentu v okně

Další vlastnost umožňuje určit, zda se v záhlaví okna má zobrazovat název dokumentu nebo název souboru. Ve výchozím nastavení je tato hodnota nastavena na `false`, což znamená, že se zobrazí název souboru.

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

Pokud chcete, aby se místo názvu souboru zobrazoval název dokumentu, musí být toto nastavení povoleno.

## Krok 6: Změna velikosti okna na první stránku

Někdy můžete chtít, aby se okno dokumentu po otevření automaticky změnilo na první stránku PDF. Zde je návod, jak zkontrolovat, zda je tato funkce povolena:

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

Ve výchozím nastavení je toto nastaveno na `false`, což znamená, že velikost okna zůstane zachována bez ohledu na velikost první stránky.

## Krok 7: Skrytí panelu nabídek

Pro lepší čtení můžete skrýt panel nabídek prohlížeče. Toto nastavení můžete zobrazit pomocí následujícího řádku:

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

To se vrátí `true` pokud je panel nabídek skrytý a `false` jinak.

## Krok 8: Skrýt panel nástrojů

Podobně můžete také chtít skrýt panel nástrojů v prohlížeči PDF pro přehlednější uživatelské rozhraní. Toto nastavení lze získat takto:

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

Pokud je toto nastavení povoleno, panel nástrojů se při otevření PDF skryje.

## Krok 9: Skrytí posuvníků a prvků uživatelského rozhraní

Pokud chcete zobrazit pouze obsah stránky bez dalších prvků uživatelského rozhraní, jako jsou posuvníky, toto nastavení řídí toto chování:

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

Při nastavení na `true`, prohlížeč PDF skryje posuvníky a další prvky uživatelského rozhraní a ponechá pouze obsah dokumentu.

## Krok 10: Nastavení režimu stránky bez zobrazení na celou obrazovku

Zobrazení dokumentu po ukončení režimu celé obrazovky můžete ovládat pomocí `NonFullScreenPageMode` vlastnost. Toto nastavení je užitečné pro definování, jak má uživatel interagovat s dokumentem v režimu, který není na celou obrazovku.

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

Výstup lze nastavit do různých režimů, jako jsou miniatury, obrysy nebo panel příloh.

## Krok 11: Definování rozvržení stránky

Toto nastavení umožňuje ovládat rozvržení stránek dokumentu. Můžete si například zvolit zobrazení jedné stránky nebo zobrazení spojitých sloupců:

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

To uživatelům dává flexibilitu v tom, jak čtou nebo zobrazují obsah dokumentu.

## Krok 12: Určete režim stránky

Konečně, `PageMode` Vlastnost definuje, jak se má dokument zobrazit po otevření. Mezi možnosti patří zobrazení miniatur, přechod do režimu celé obrazovky nebo zobrazení panelu příloh.

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

V závislosti na vašich potřebách můžete nastavit libovolný režim, který vyhovuje účelu vašeho PDF.

## Závěr

Jak vidíte, Aspose.PDF pro .NET poskytuje komplexní nástroje pro manipulaci se zobrazováním PDF dokumentů v různých prohlížečích PDF. Ať už chcete skrýt panel nástrojů, vycentrovat okno nebo ovládat směr textu, Aspose.PDF nabízí flexibilitu pro vylepšení uživatelského zážitku ze sledování.

# Často kladené otázky

### Mohu si přizpůsobit počáteční úroveň přiblížení PDF?
Ano, Aspose.PDF umožňuje nastavit úroveň přiblížení při otevření dokumentu.

### Jak mohu uzamknout velikost okna PDF?
Můžete nastavit `FitWindow` vlastnost, která zabraňuje změně velikosti okna.

### Podporuje Aspose.PDF různé režimy čtení?
Ano, podporuje různé režimy, jako je celá obrazovka, miniatury a přílohy.

### Je možné skrýt posuvníky v prohlížeči PDF?
Posuvníky můžete samozřejmě skrýt nastavením `HideWindowUI` majetek `true`.

### Mohu po otevření vycentrovat okno dokumentu?
Ano, můžete to ovládat nastavením `CenterWindow` vlastnictví.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}