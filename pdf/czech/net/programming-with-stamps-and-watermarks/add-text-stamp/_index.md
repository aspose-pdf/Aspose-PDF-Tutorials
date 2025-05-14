---
"description": "Naučte se, jak přidat textové razítko do PDF souboru pomocí Aspose.PDF pro .NET s naším podrobným návodem a vylepšete své prezentace dokumentů."
"linktitle": "Přidat textové razítko do PDF souboru"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přidat textové razítko do PDF souboru"
"url": "/cs/net/programming-with-stamps-and-watermarks/add-text-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat textové razítko do PDF souboru

## Zavedení

dnešní digitální době jsou PDF soubory běžným formátem pro sdílení a distribuci dokumentů. Ať už jste vývojář, tvůrce obsahu nebo jen někdo, kdo chce vylepšit své PDF soubory, znalost programově manipulace s PDF soubory může být zásadní. Jednou z užitečných funkcí, kterou byste mohli chtít využít, je možnost přidávat do PDF souborů textová razítka. Přidání textového razítka může dodat vašim dokumentům profesionální vzhled nebo sdělit důležité informace, jako například „Ukázka“, „Důvěrné“ nebo dokonce vodoznak.

## Předpoklady

Než se pustíme do kódu, je třeba splnit několik předpokladů, abyste se ujistili, že máte vše správně nastavené. Zde je to, co budete potřebovat:

1. Aspose.PDF pro .NET: Ujistěte se, že máte ve svém projektu nainstalovanou knihovnu Aspose.PDF. Pokud jste tak ještě neučinili, můžete si ji stáhnout z [Webové stránky Aspose](https://releases.aspose.com/pdf/net/).
2. Visual Studio nebo kompatibilní IDE: Pro psaní a spouštění kódu .NET budete potřebovat vývojové prostředí. Visual Studio je mezi vývojáři nejčastější volbou.
3. Základní znalost jazyka C#: Znalost jazyka C# a principů objektově orientovaného programování vám pomůže lépe porozumět příkladům.
4. Ukázkový soubor PDF: Měli byste mít připravený soubor PDF, se kterým můžete pracovat. Můžete vytvořit základní PDF nebo použít libovolný existující PDF k otestování funkčnosti.

Jakmile si splníte tyto předpoklady, můžeme se pustit do kódování!

## Importovat balíčky

Nyní importujme potřebné balíčky. Tento krok je klíčový, protože zpřístupňuje třídy a metody z knihovny Aspose ve vašem projektu.

### Importovat sestavu Aspose.PDF

Chcete-li začít, musíte importovat jmenný prostor Aspose.PDF. Na začátek souboru C# přidejte následující direktivu using:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

To vám umožní přístup ke třídám, které jsou nezbytné pro vytváření a manipulaci s dokumenty PDF.

teď se pojďme pustit do jádra tutoriálu. Rozdělíme si proces do jasných a stručných kroků. Každý krok vás provede kódem pro přidání textového razítka do PDF souboru.

## Krok 1: Nastavení adresáře dokumentů

Nejprve je třeba nastavit adresář, kde je uložen váš PDF dokument. To znamená, že váš kód musí vědět, kde najít PDF soubor, který chcete upravit.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Vysvětlení: Nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kam se váš PDF soubor (`AddTextStamp.pdf`) je uložen. Tato cesta se později použije k otevření a uložení upraveného PDF.

## Krok 2: Otevřete dokument PDF

Dále otevřeme PDF dokument pomocí `Document` třída z oboru názvů Aspose.PDF.

```csharp
// Otevřít dokument
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

Vysvětlení: Zde vytváříme instanci `Document` třídu a předáním cesty k našemu PDF souboru. Tím se PDF načte, abychom s ním mohli manipulovat.

## Krok 3: Vytvořte textové razítko

Nyní vytvoříme textové razítko, které později použijeme v našem PDF dokumentu.

```csharp
// Vytvořit textové razítko
TextStamp textStamp = new TextStamp("Sample Stamp");
```

Vysvětlení: `TextStamp` Objekt je vytvořen s textem, který chcete zobrazit. V tomto případě používáme jako text pro naše razítko „Ukázkové razítko“.

## Krok 4: Nastavení vlastností razítka

Pro přizpůsobení razítka můžeme nastavit různé vlastnosti, jako je barva pozadí, poloha a rotace. Pojďme to udělat nyní:

```csharp
// Nastavit, zda je razítko pozadím
textStamp.Background = true;

// Nastavit původ
textStamp.XIndent = 100;
textStamp.YIndent = 100;

// Otočit razítko
textStamp.Rotate = Rotation.on90;
```

Vysvětlení:
- Pozadí: Nastavení na `true` znamená, že se razítko zobrazí za obsahem PDF.
- XIndent a YIndent: Tyto vlastnosti určují polohu razítka na stránce. V tomto příkladu bude razítko umístěno 100 jednotek od levého a horního okraje stránky.
- Otočit: Tím se razítko otočí o 90 stupňů. Můžete si vybrat různé možnosti otočení na základě požadavků na design.

## Krok 5: Úprava vlastností textu

Dále se pojďme podívat na kreativitu a přizpůsobíme si vzhled textu v našem razítku:

```csharp
// Nastavení vlastností textu
textStamp.TextState.Font = FontRepository.FindFont("Arial");
textStamp.TextState.FontSize = 14.0F;
textStamp.TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
textStamp.TextState.ForegroundColor = Aspose.Pdf.Color.FromRgb(Color.Aqua);
```

Vysvětlení:
- Písmo: Používáme písmo Arial, které je tučné a kurzívou.
- Velikost písma: Je nastavena na 14 bodů.
- Barva popředí: Použití RGB k nastavení barvy textu na akvamarínovou. Nebojte se změnit barvu podle svých potřeb v oblasti brandingu nebo designu!

## Krok 6: Přidání razítka na stránku PDF

Nyní je čas přidat razítko na konkrétní stránku dokumentu PDF.

```csharp
// Přidat razítko na konkrétní stránku
pdfDocument.Pages[1].AddStamp(textStamp);
```

Vysvětlení: V tomto příkladu je razítko přidáno na první stránku PDF (stránky jsou indexovány od 1). Upravte číslo stránky podle potřeby pro váš dokument.

## Krok 7: Uložení upraveného PDF

Nakonec uložme dokument s nově přidaným textovým razítkem.

```csharp
dataDir = dataDir + "AddTextStamp_out.pdf";

// Uložit výstupní dokument
pdfDocument.Save(dataDir);
Console.WriteLine("\nText stamp added successfully.\nFile saved at " + dataDir);
```

Vysvětlení: Definujeme novou cestu k výstupnímu souboru a poté upravený dokument uložíme. Po uložení se cesta vypíše do konzole, což potvrzuje úspěšnou operaci.

## Závěr

Gratulujeme! Úspěšně jste přidali textové razítko do PDF souboru pomocí Aspose.PDF pro .NET. Tato metoda vám umožňuje efektivně anotovat dokumenty, čímž zvyšuje jejich profesionalitu i použitelnost. Ať už přidáváte vodoznaky, podpisy nebo jednoduché poznámky, knihovna Aspose poskytuje výkonné nástroje pro snadnou manipulaci s PDF soubory.

## Často kladené otázky

### Co je textové razítko v PDF?
Textové razítko je grafická vrstva obsahující text, kterou lze umístit do dokumentu PDF a často se používá pro anotace nebo vodoznaky.

### Mohu si razítko upravit pomocí obrázků?
Ano, Aspose.PDF také podporuje přidávání obrazových razítek, což poskytuje větší flexibilitu návrhu.

### Jaké programovací jazyky mohu použít s Aspose.PDF?
Aspose.PDF je primárně zaměřen na .NET, ale existují verze i pro další jazyky, jako je Java a Python.

### Jak získám dočasnou licenci pro Aspose.PDF?
O dočasnou licenci můžete požádat na adrese [odkaz na nákup](https://purchase.aspose.com/temporary-license/) na jejich webových stránkách.

### Kde najdu podporu pro Aspose.PDF?
Podpora pro Aspose.PDF je k dispozici na jejich [fórum podpory](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}