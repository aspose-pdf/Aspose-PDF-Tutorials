---
"description": "Naučte se, jak nastavit datum platnosti v souborech PDF pomocí Aspose.PDF pro .NET. Zvyšte zabezpečení dokumentů pomocí tohoto podrobného návodu."
"linktitle": "Nastavit datum platnosti v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Nastavit datum platnosti v souboru PDF"
"url": "/cs/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavit datum platnosti v souboru PDF

## Zavedení

V dnešní digitální době je správa a zabezpečení dokumentů důležitější než kdy dříve. Představte si, že odesíláte PDF soubor, který se po určitém datu automaticky stane nepřístupným. Zní to jako kouzlo, že? S Aspose.PDF pro .NET můžete snadno nastavit datum vypršení platnosti pro vaše PDF soubory. Tato funkce je obzvláště užitečná pro citlivé dokumenty, které je třeba po určité době omezit. V tomto tutoriálu vás krok za krokem provedeme procesem nastavení data vypršení platnosti v PDF souboru. Takže, vezměte si programátorskou čepici a pojďme se do toho pustit!

## Předpoklady

Než začneme, je potřeba mít připraveno několik věcí:

1. Vývojové prostředí: Ujistěte se, že máte nastavené vývojové prostředí pro .NET. Může se jednat o Visual Studio nebo jakékoli jiné vývojové prostředí (IDE), které podporuje .NET.
2. Aspose.PDF pro .NET: Musíte mít nainstalovanou knihovnu Aspose.PDF. Pokud jste tak ještě neučinili, můžete si ji stáhnout z [zde](https://releases.aspose.com/pdf/net/).
3. Základní znalost C#: Tento tutoriál předpokládá, že máte základní znalosti programování v C#. Pokud s C# začínáte, nebojte se! Snažíme se vše zjednodušit a srozumitelně vysvětlit.

## Importovat balíčky

Abyste mohli začít s Aspose.PDF, musíte do svého projektu v C# importovat potřebné jmenné prostory. Postupujte takto:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Tyto jmenné prostory vám poskytují přístup k základním funkcím potřebným pro práci s PDF dokumenty v Aspose.PDF.

## Krok 1: Nastavení adresáře dokumentů

Nejdříve je třeba zadat cestu k adresáři s vašimi dokumenty. Sem bude uložen váš výstupní PDF. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kam chcete soubor PDF uložit. Je to jako byste programu řekli: „Hej, tady mám své soubory!“

## Krok 2: Vytvoření instance objektu Document

Dále je třeba vytvořit novou instanci `Document` třída. Toto je vaše plátno, na kterém vytvoříte PDF.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Přemýšlejte o `Document` objekt jako prázdný list papíru. Můžete do něj přidávat obsah, jak chcete!

## Krok 3: Přidání stránky do PDF

Nyní, když máte dokument nastavený, je čas do něj přidat stránku. Na ni se bude umisťovat váš obsah.

```csharp
doc.Pages.Add();
```

Právě jste ve svém PDF vytvořili novou stránku. Je to jako byste si do sešitu přidali novou stránku, kam si můžete zapsat své myšlenky.

## Krok 4: Přidání textu na stránku

Udělejme tuto stránku trochu zajímavější přidáním textu. Přidáme jednoduchou zprávu „Ahoj světe“.

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

Tento řádek kódu přidá fragment textu na první stránku vašeho PDF. Je to jako napsat nadpis na začátek stránky!

## Krok 5: Vytvořte JavaScript pro datum vypršení platnosti

teď přichází ta zábavná část! Vytvoříte JavaScriptovou akci, která bude kontrolovat datum vypršení platnosti PDF. Pokud aktuální datum překročí datum vypršení platnosti, zobrazí se uživateli upozornění.

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

Zde se dozvíte, co se děje:
- Definujete rok a měsíc platnosti.
- Dostaneš dnešní datum.
- Porovnáte dnešní datum s datem expirace.
- Pokud je dnešní datum po datu expirace, zobrazí se zpráva!

## Krok 6: Nastavení JavaScriptu jako akce pro otevření PDF

Nyní je třeba nastavit akci JavaScriptu jako akci otevření pro váš PDF dokument. To znamená, že JavaScript se spustí ihned po otevření PDF.

```csharp
doc.OpenAction = javaScript;
```

Tento řádek říká PDF souboru, aby spustil JavaScript, když ho někdo otevře. Je to jako nastavit připomenutí, které se spustí, jakmile si otevřete kalendář!

## Krok 7: Uložení dokumentu PDF

Konečně je čas uložit dokument PDF s funkcí data platnosti. 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

Tento řádek uloží váš PDF soubor do zadaného adresáře s názvem „SetExpiryDate_out.pdf“. Je to jako byste zarámovali hotový obrázek!

## Závěr

A je to! Úspěšně jste vytvořili PDF soubor s datem platnosti pomocí Aspose.PDF pro .NET. Tato funkce nejen zvyšuje zabezpečení, ale také zajišťuje, že citlivé informace jsou pod kontrolou. Ať už odesíláte smlouvy, zprávy nebo jakékoli jiné důležité dokumenty, nastavení data platnosti může být zásadní.

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je výkonná knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět PDF dokumenty v .NET aplikacích.

### Mohu používat Aspose.PDF zdarma?
Ano, můžete použít bezplatnou zkušební verzi souboru Aspose.PDF. Můžete si ji stáhnout. [zde](https://releases.aspose.com/).

### Jak si mohu zakoupit Aspose.PDF?
Soubor Aspose.PDF si můžete zakoupit na adrese [stránka nákupu](https://purchase.aspose.com/buy).

### Co když budu potřebovat podporu?
Pokud máte jakékoli dotazy nebo potřebujete pomoc, můžete navštívit [Fórum podpory Aspose](https://forum.aspose.com/c/pdf/10).

### Mohu získat dočasnou licenci pro Aspose.PDF?
Ano, můžete požádat o dočasnou licenci [zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}