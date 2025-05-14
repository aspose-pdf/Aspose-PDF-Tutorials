---
"description": "Podrobný návod pro změnu orientace stránky PDF pomocí Aspose.PDF pro .NET. Snadno sledovatelný a implementovatelný ve vašich projektech."
"linktitle": "Změna orientace"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Změna orientace"
"url": "/cs/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Změna orientace

## Zavedení

Už jste někdy měli potíže se souborem PDF, kde je orientace stránky prostě... špatně nastavená? Možná máte co do činění s dokumentem, který byl naskenován nebo vytvořen nesprávně, a stránky je potřeba otočit, aby dávaly smysl. Naštěstí pro nás Aspose.PDF pro .NET nabízí snadný a výkonný způsob, jak manipulovat se soubory PDF prakticky jakýmkoli představitelným způsobem – včetně změny orientace stránek. Ať už chcete přepnout z orientace na výšku na šířku nebo naopak, tento průvodce vás krok za krokem provede celým procesem.

Takže, pokud jste připraveni se do toho pustit a snadno otáčet stránky PDF, pojďme na to!

## Předpoklady

Než se pustíme do podrobností o změně orientace stránky v PDF, pojďme si stručně probrat, co budete potřebovat:

- Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF pro .NET. Pokud ji nemáte, můžete... [stáhněte si to zde](https://releases.aspose.com/pdf/net/).
- Vývojové prostředí .NET: Pro práci s .NET můžete použít Visual Studio, JetBrains Rider nebo jakékoli preferované IDE.
- Základní znalost jazyka C#: I když je tento průvodce přímočarý, základní znalost jazyka C# vám jeho pochopení ještě usnadní.
- Soubor PDF: V níže uvedeném příkladu se předpokládá, že máte soubor PDF s více stránkami. Pokud žádný nemáte po ruce, vytvořte si nebo si stáhněte ukázkový soubor PDF, se kterým budete pracovat.

Také, pokud s tím teprve začínáte, můžete vyzkoušet Aspose.PDF s [bezplatná dočasná licence](https://purchase.aspose.com/temporary-license/) než se rozhodnete [koupit plnou verzi](https://purchase.aspose.com/buy).

## Importovat jmenné prostory

Než budete moci upravovat orientaci stránek v PDF, budete muset do projektu C# importovat potřebné jmenné prostory. Ujistěte se, že máte následující:

```csharp
using System.IO;
using Aspose.Pdf;
```

Po importu se pojďme přesunout k hlavní části tutoriálu.

## Krok 1: Načtěte dokument PDF

První věc, kterou musíme udělat, je načíst PDF soubor, který chceme upravit. Můžete použít `Document` třídu z oboru názvů Aspose.PDF pro otevření PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Tento řádek načte PDF ze zadaného adresáře. Nezapomeňte nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou k vašemu souboru. `"input.pdf"` je PDF, jehož orientaci chcete změnit.

## Krok 2: Procházení jednotlivých stránek

Nyní, když máme dokument načtený, projdeme si jednotlivé stránky v PDF. Použijeme `foreach` smyčka pro procházení všech stránek, což nám umožňuje aplikovat změnu orientace na všechny z nich.

```csharp
foreach (Page page in doc.Pages)
{
    // Manipulovat s každou stránkou
}
```

Tato smyčka bude iterovat všemi stránkami v dokumentu.

## Krok 3: Získejte MediaBox stránky

Každá stránka v PDF má `MediaBox` která definuje hranice stránky. K tomuto přístupu potřebujeme, abychom určili aktuální orientaci a mohli ji upravit.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

Ten/Ta/To `MediaBox` nám udává rozměry stránky, jako je její šířka, výška a umístění.

## Krok 4: Prohoďte šířku a výšku

Chcete-li změnit orientaci stránky z na výšku na šířku nebo z na šířku na výšku, jednoduše prohodíme hodnoty šířky a výšky. Tímto krokem upravíme rozměry stránky.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

Tento kód prohodí výšku a šířku a změní polohu levého dolního rohu (`LLY`) aby se obsah po otočení úhledně vešel.

## Krok 5: Aktualizace MediaBoxu a CropBoxu

Nyní, když máme novou výšku a šířku, aplikujme změny na stránku. `MediaBox` a `CropBox`Ten/Ta/To `CropBox` je nezbytné, pokud měl původní dokument jednu sadu, aby se zajistilo správné zobrazení celé stránky.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

Tento krok změní velikost stránky na základě nově vypočítaných rozměrů.

## Krok 6: Otočení stránky

Nakonec nastavíme úhel natočení stránky. Aspose.PDF to velmi zjednodušuje. Stránku můžeme otočit o 90 stupňů, abychom ji přesunuli z orientace na výšku do orientace na šířku nebo naopak.

```csharp
page.Rotate = Rotation.on90;
```

Tento kód otočí stránku o 90 stupňů a převrátí ji do požadované orientace.

## Krok 7: Uložení výstupního PDF

Po provedení změn orientace na všechny stránky uložíme upravený dokument do nového souboru. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

Ujistěte se, že jste zadali nový název souboru (v tomto případě `ChangeOrientation_out.pdf`) pro uložení výstupu. Tímto způsobem nepřepíšete původní soubor.

### Závěr

A je to! Změna orientace stránky PDF souboru pomocí Aspose.PDF pro .NET je stejně jednoduchá jako načtení dokumentu, procházení stránek, úprava MediaBoxu a uložení aktualizovaného souboru. Ať už máte co do činění se špatně naskenovaným dokumentem nebo potřebujete otočit stránky podle svých potřeb formátování, tento podrobný návod by vám měl pomoci.

## Často kladené otázky

### Mohu v PDF otočit pouze určité stránky místo všech?  
Ano, smyčku můžete upravit tak, aby cílila na konkrétní stránky pomocí jejich indexu, místo aby procházela všechny stránky.

### Co je `MediaBox`?  
Ten/Ta/To `MediaBox` definuje velikost a tvar stránky v souboru PDF. Je to místo, kam je umístěn obsah stránky.

### Funguje Aspose.PDF pro .NET s jinými formáty souborů?  
Ano, Aspose.PDF dokáže zpracovat různé formáty souborů, jako je HTML, XML, XPS a další.

### Existuje bezplatná verze Aspose.PDF pro .NET?  
Ano, můžete začít s [bezplatná zkušební verze](https://releases.aspose.com/) nebo požádejte o [dočasná licence](https://purchase.aspose.com/temporary-license/).

### Mohu po uložení změny vrátit zpět?  
Jakmile dokument uložíte, změny jsou trvalé. Nezapomeňte pracovat na kopii nebo si ponechat zálohu původního souboru.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}