---
"description": "Naučte se, jak vytvořit vyplněný obdélník v PDF pomocí Aspose.PDF pro .NET v tomto podrobném návodu. Ideální pro vývojáře všech úrovní."
"linktitle": "Vytvořit vyplněný obdélník"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vytvořit vyplněný obdélník"
"url": "/cs/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit vyplněný obdélník

## Zavedení

Chtěli jste někdy programově vytvářet vizuálně atraktivní PDF soubory? Pokud ano, jste na správném místě! V tomto tutoriálu se ponoříme do světa Aspose.PDF pro .NET, výkonné knihovny, která vám umožní snadno manipulovat s PDF dokumenty. Dnes se zaměříme na vytvoření vyplněného obdélníku v PDF souboru. Ať už jste zkušený vývojář, nebo teprve začínáte, tento průvodce vás provede každým krokem přátelským a poutavým způsobem. Takže, vezměte si programátorskou čepici a pojďme na to!

## Předpoklady

Než se pustíme do samotného kódu, je potřeba mít připraveno několik věcí:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Je to fantastické IDE pro vývoj v .NET.
2. Aspose.PDF pro .NET: Budete si muset stáhnout a nainstalovat knihovnu Aspose.PDF. Najdete ji [zde](https://releases.aspose.com/pdf/net/).
3. Základní znalost C#: Trocha znalosti programování v C# vám pomůže lépe porozumět úryvkům kódu.

## Importovat balíčky

Chcete-li začít, musíte do svého projektu C# importovat potřebné balíčky. Zde je návod, jak to udělat:

### Vytvořit nový projekt

Otevřete Visual Studio a vytvořte nový projekt v C#. Pro zjednodušení si můžete vybrat konzolovou aplikaci.

### Přidat odkaz na Aspose.PDF

1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte možnost „Spravovat balíčky NuGet“.
3. Vyhledejte soubor „Aspose.PDF“ a nainstalujte nejnovější verzi.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Teď, když máme vše nastavené, pojďme se ponořit do kódu!

## Krok 1: Nastavení adresáře dokumentů

Nejdříve je třeba zadat cestu, kam bude váš PDF soubor uložen. To je klíčové, protože to programu říká, kde má soubor vytvořit.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou na vašem počítači, kam chcete PDF uložit.

## Krok 2: Vytvoření instance dokumentu

Dále vytvoříme instanci `Document` třída. Tato třída představuje dokument PDF, se kterým budete pracovat.

```csharp
// Vytvořit instanci dokumentu
Document doc = new Document();
```

Tento řádek inicializuje nový PDF dokument, se kterým můžeme manipulovat.

## Krok 3: Přidání stránky do dokumentu

A teď přidejme do našeho dokumentu stránku. Každý PDF soubor potřebuje alespoň jednu stránku, že?

```csharp
// Přidat stránku do kolekce stránek souboru PDF
Page page = doc.Pages.Add();
```

Tento kód přidá do dokumentu novou stránku, která nám umožní na ni kreslit tvary.

## Krok 4: Vytvoření instance grafu

Abychom mohli kreslit tvary, musíme vytvořit `Graph` například. Představte si graf jako plátno, na kterém můžete kreslit různé tvary.

```csharp
// Vytvořit instanci grafu
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

Zde vytváříme graf o šířce 100 a výšce 400.

## Krok 5: Přidání grafu na stránku

Nyní, když máme graf, přidejme ho na stránku, kterou jsme vytvořili dříve.

```csharp
// Přidat objekt grafu do kolekce odstavců instance stránky
page.Paragraphs.Add(graph);
```

Tato čára připojí graf ke stránce a připraví ho tak k vykreslení.

## Krok 6: Vytvořte instanci obdélníku

Dále vytvoříme obdélník, který chceme vyplnit barvou.

```csharp
// Vytvořit instanci obdélníku
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

V tomto kódu definujeme polohu a velikost obdélníku. Parametry představují souřadnice x a y, šířku a výšku.

## Krok 7: Určete barvu výplně

Nyní si vybereme barvu pro náš obdélník. V tomto příkladu ho vyplníme červenou barvou.

```csharp
// Zadejte barvu výplně pro objekt Graf
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

Tato čára nastaví barvu výplně obdélníku na červenou. Můžete si vybrat libovolnou barvu!

## Krok 8: Přidání obdélníku do grafu

Když máme obdélník připravený, je čas ho přidat do grafu.

```csharp
// Přidat objekt obdélník do kolekce tvarů objektu Graph
graph.Shapes.Add(rect);
```

Tento kód přidá obdélník do grafu, čímž se stane součástí našeho výkresu.

## Krok 9: Uložení dokumentu PDF

Nakonec musíme uložit náš dokument do zadaného adresáře.

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// Uložit soubor PDF
doc.Save(dataDir);
```

Tento kód uloží PDF soubor s názvem `CreateFilledRectangle_out.pdf` v adresáři, který jste dříve zadali.

## Krok 10: Potvrzovací zpráva

Abychom věděli, že vše proběhlo hladce, můžeme vytisknout potvrzovací zprávu.

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

Tento řádek vypíše v konzoli zprávu potvrzující, že vyplněný obdélník byl úspěšně vytvořen.

## Závěr

A tady to máte! Úspěšně jste vytvořili vyplněný obdélník v dokumentu PDF pomocí Aspose.PDF pro .NET. Tato výkonná knihovna otevírá svět možností pro manipulaci s PDF a umožňuje vám programově vytvářet úžasné dokumenty. Ať už generujete zprávy, faktury nebo jakýkoli jiný typ PDF, Aspose.PDF vám s tím pomůže.

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům programově vytvářet, manipulovat a převádět PDF dokumenty.

### Mohu používat Aspose.PDF zdarma?
Ano, Aspose nabízí bezplatnou zkušební verzi, kterou můžete použít k prozkoumání funkcí knihovny. Můžete si ji stáhnout. [zde](https://releases.aspose.com/).

### Existuje způsob, jak získat podporu pro Aspose.PDF?
Rozhodně! Podporu můžete získat prostřednictvím fóra Aspose. [zde](https://forum.aspose.com/c/pdf/10).

### Jak si mohu zakoupit Aspose.PDF?
Soubor Aspose.PDF si můžete zakoupit na stránce nákupu. [zde](https://purchase.aspose.com/buy).

### Jaké typy tvarů mohu vytvářet pomocí Aspose.PDF?
Pomocí knihovny Aspose.PDF můžete vytvářet různé tvary, včetně obdélníků, kruhů, čar a dalších.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}