---
"description": "Naučte se, jak snadno a podrobně vytvářet lokální hypertextové odkazy v souborech PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Vytvořit lokální hypertextový odkaz v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vytvořit lokální hypertextový odkaz v souboru PDF"
"url": "/cs/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit lokální hypertextový odkaz v souboru PDF

## Zavedení

V této příručce vás provedeme procesem vytváření lokálních hypertextových odkazů v souboru PDF pomocí Aspose.PDF pro .NET. Každý krok si jasně rozebereme, abyste i když jste ve světě manipulace s PDF nováčkem, mohli bez námahy sledovat postup.

## Předpoklady

Než se po hlavě pustíme do kódu, ujistěte se, že máte vše potřebné:

1. Visual Studio: Budete ho potřebovat k vývoji aplikací .NET. Stáhněte si ho z [webové stránky](https://visualstudio.microsoft.com/).
2. Aspose.PDF pro .NET: Tuto knihovnu si můžete stáhnout prostřednictvím [odkaz ke stažení zde](https://releases.aspose.com/pdf/net/)Dodává se s bohatou sadou funkcí pro manipulaci s PDF.
3. Základní znalost C#: Trocha znalosti programování v C# vám pomůže, ale nebojte se, projdeme si kód řádek po řádku.
4. .NET Framework: Ujistěte se, že máte na svém počítači nainstalovaný .NET Framework. Požadavky si můžete ověřit v souboru Aspose.PDF. [dokumentace](https://reference.aspose.com/pdf/net/).

Po nastavení těchto předpokladů jste připraveni naučit se, jak vytvářet lokální hypertextové odkazy ve vašich dokumentech PDF!

## Importovat balíčky

Nyní, když jste vše připraveni, je čas importovat potřebné balíčky do vašeho projektu v C#. Knihovna Aspose.PDF obsahuje všechny potřebné třídy. Zde je návod, jak to udělat:

### Otevřete svůj projekt

Otevřete stávající projekt .NET nebo vytvořte nový ve Visual Studiu. Pokud začínáte znovu, vyberte na úvodní obrazovce možnost „Vytvořit nový projekt“.

### Přidat odkaz na Aspose.PDF

V Průzkumníku řešení klikněte pravým tlačítkem myši na „Závislosti“ ve složce projektu. Vyberte „Spravovat balíčky NuGet“ a poté vyhledejte `Aspose.PDF`Nainstalujte si nejnovější dostupnou verzi. Ta vám přinese všechny nástroje, které potřebujete pro vytváření a manipulaci s PDF soubory.

### Importovat jmenné prostory

Na začátek souboru .cs přidejte direktivy using pro knihovnu Aspose.PDF takto:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Tímto způsobem budete mít přístup k funkcím knihovny.

Rozeberme si proces vytváření lokálních hypertextových odkazů do jednoduchých kroků. Každý krok bude podrobně vysvětlen, abyste lépe pochopili logiku, která se za ním skrývá.

## Krok 1: Nastavení instance dokumentu

V tomto kroku vytvoříte novou instanci třídy Document, která představuje soubor PDF, se kterým budete pracovat.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Nastavení adresáře dokumentů
Document doc = new Document(); // Vytvořit instanci dokumentu
```
Ten/Ta/To `dataDir` proměnná je místo, kde bude uložen nově vytvořený PDF. Budete muset nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou ve vašem systému. `Document` Třída vytvoří nový PDF dokument, do kterého můžeme přidat stránky a odkazy.

## Krok 2: Přidání stránky do dokumentu

Dále přidáte do dokumentu PDF stránku. 

```csharp
Page page = doc.Pages.Add(); // Přidat stránku do kolekce stránek
```
Ten/Ta/To `Pages.Add()` Metoda přidá do dokumentu novou stránku. Na ní bude umístěn veškerý váš obsah.

## Krok 3: Vytvořte textový fragment

Nyní si vytvořme text, který bude fungovat jako klikatelný odkaz.

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
Ten/Ta/To `TextFragment` představuje segment textu v PDF. Zde vytváříme odkaz, který uživatelům sdělí, že je přesměruje na stránku 7.

## Krok 4: Vytvořte lokální hypertextový odkaz

A tady se začne dít ta pravá magie! Musíte vytvořit lokální hypertextový odkaz, který bude textovému fragmentu sdělovat, kam má ukazovat.

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // Vytvořit lokální hypertextový odkaz
link.TargetPageNumber = 7; // Nastavit cílovou stránku pro instanci odkazu
text.Hyperlink = link; // Nastavení hypertextového odkazu TextFragment
```
Ten/Ta/To `LocalHyperlink` třída nám umožňuje odkazovat na další stránky ve stejném dokumentu. Nastavením `TargetPageNumber` V bodě 7 sdělíte hypertextovému odkazu, aby po kliknutí přeskočil na danou stránku.

## Krok 5: Přidání fragmentu textu na stránku

Po nastavení hypertextového odkazu je čas přidat náš textový fragment na stránku, kterou jsme vytvořili.

```csharp
page.Paragraphs.Add(text); // Přidat text do kolekce odstavců na stránce
```
Tento řádek přidá váš klikatelný text do kolekce odstavců na stránce.

## Krok 6: Vytvořte další textový fragment (volitelné)

Přidejme další hypertextový odkaz pro navigaci zpět na stránku 1.

```csharp
text = new TextFragment("link page number test to page 1"); // Vytvořit nový TextFragment
text.IsInNewPage = true; // Přidat na novou stránku
```
Vytvoření nového `TextFragment` pro druhý odkaz nastavíme `IsInNewPage` na hodnotu true, což znamená, že tento text bude umístěn na nové stránce.

## Krok 7: Nastavení druhého lokálního hypertextového odkazu

Stejně jako předtím vytvoříte další lokální hypertextový odkaz pro stránku 1.

```csharp
link = new LocalHyperlink(); // Vytvořit další instanci lokálního hypertextového odkazu
link.TargetPageNumber = 1; // Nastavit cílovou stránku pro druhý hypertextový odkaz
text.Hyperlink = link; // Nastavit odkaz pro druhý TextFragment
```
Tento hypertextový odkaz cílí na stránku 1 a umožňuje uživatelům vrátit se zpět, když dosáhnou druhé stránky.

## Krok 8: Přidání druhého textového fragmentu na novou stránku

Nyní přidejme tento text na jeho stránku.

```csharp
page.Paragraphs.Add(text); // Přidat text do kolekce odstavců objektu stránky
```
Podobně jako v kroku 5 tento řádek přidá nový text hypertextového odkazu na nově vytvořenou stránku.

## Krok 9: Uložte dokument

Konečně je čas ušetřit si vaši tvrdou práci! 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // Zadejte název výstupního souboru
doc.Save(dataDir); // Uložit aktualizovaný dokument
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
Toto zkombinuje cestu k adresáři s názvem souboru. `Save()` Metoda uloží váš dokument a potvrzovací zpráva vám dá vědět, že vše proběhlo hladce!

## Závěr

Vytváření lokálních hypertextových odkazů v souborech PDF pomocí Aspose.PDF pro .NET není jen skvělý trik; je to praktická funkce, která vylepšuje navigaci a uživatelský zážitek. Nyní máte znalosti, které pomohou vašim čtenářům nasměrovat přímo k informacím, které potřebují. Stačí si vzpomenout na naši původní analogii – už žádné ztracené duše bloudící nekonečnými stránkami.

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům programově vytvářet, manipulovat a převádět PDF dokumenty pomocí frameworku .NET.

### Mohu vytvářet hypertextové odkazy na externí webové stránky?
Ano, Aspose.PDF také podporuje vytváření hypertextových odkazů na externí URL adresy kromě lokálních hypertextových odkazů v PDF.

### Existuje bezplatná zkušební verze pro Aspose.PDF?
Rozhodně! Bezplatnou zkušební verzi si můžete vyzkoudat zde [místo](https://releases.aspose.com/).

### Jaké programovací jazyky Aspose podporuje?
Aspose nabízí knihovny pro různé programovací jazyky, včetně Javy, C++ a Pythonu, mimo jiné.

### Jak získám podporu pro produkty Aspose?
Podporu můžete vyhledat prostřednictvím [Fórum Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}