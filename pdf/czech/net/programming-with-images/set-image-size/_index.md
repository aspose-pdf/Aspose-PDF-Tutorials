---
"description": "Naučte se, jak nastavit velikost obrázku v PDF pomocí Aspose.PDF pro .NET. Tento podrobný návod vám pomůže změnit velikost obrázků, upravit vlastnosti stránky a uložit PDF soubory."
"linktitle": "Nastavení velikosti obrázku v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Nastavení velikosti obrázku v souboru PDF"
"url": "/cs/net/programming-with-images/set-image-size/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení velikosti obrázku v souboru PDF

## Zavedení

Práce s PDF soubory je běžným požadavkem pro mnoho aplikací a schopnost manipulovat s prvky v PDF souboru může být klíčová. Ať už vytváříte generátor sestav nebo přidáváte dynamický obsah do PDF souboru, ovládání velikosti obrázků v dokumentu je nezbytnou funkcí. V tomto tutoriálu si ukážeme, jak nastavit velikost obrázku v PDF souboru pomocí Aspose.PDF pro .NET. Tato výkonná knihovna nabízí rozsáhlou kontrolu nad obsahem PDF a my si ji krok za krokem rozebereme, abychom vám ukázali, jak snadné to může být. Na konci budete s jistotou měnit velikost obrázků a pochopíte, jak tato funkce může vylepšit vaše pracovní postupy s PDF.


## Předpoklady

Než se pustíme do kódu, je třeba mít připraveno několik věcí, které budete v tomto tutoriálu dodržovat.

1. Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou nejnovější verzi knihovny Aspose.PDF. Můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/).
2. .NET Framework nebo .NET Core: Ujistěte se, že máte pracovní prostředí s nainstalovaným .NET Frameworkem nebo .NET Core.
3. Základní znalost C#: Budeme používat C# jako programovací jazyk, takže znalost tohoto jazyka je nezbytná.
4. Ukázkový obrázek: Budete potřebovat ukázkový obrázek, který vložíte do PDF. Můžete použít libovolný obrázek, ale ujistěte se, že je dostupný v adresáři vašeho projektu.

## Importovat balíčky

Chcete-li používat Aspose.PDF pro .NET, musíte nejprve importovat potřebné jmenné prostory. Zde je jednoduché nastavení:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nyní, když máme základy probrané, pojďme k vytváření a úpravě dokumentu PDF.

## Krok 1: Inicializace dokumentu PDF

První věc, kterou musíme udělat, je vytvořit nový PDF dokument. Použijeme `Document` třída z Aspose.PDF, aby toho bylo dosaženo.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Vytvoření instance objektu Document
Document doc = new Document();
```
 
Zde vytváříme instanci `Document` objekt, který bude reprezentovat náš PDF soubor. Také určíme adresář, kde se naše soubory nacházejí, pomocí `dataDir` proměnná. Toto je výchozí bod pro vytváření libovolného PDF souboru pomocí Aspose.PDF.

## Krok 2: Přidání nové stránky do PDF

Jakmile máme dokument připravený, musíme do něj přidat stránku. Každý PDF soubor musí mít alespoň jednu stránku, takže si jednu přidejme.

```csharp
// Přidat stránku do kolekce stránek souboru PDF
Aspose.Pdf.Page page = doc.Pages.Add();
```
 
Novou stránku do dokumentu přidáme pomocí `Pages.Add()` metoda. Tato stránka bude sloužit jako plátno, na které umístíme náš obrázek. Každá stránka v PDF je v podstatě prázdná tabulka, kam můžete přidat text, obrázky nebo jiný obsah.

## Krok 3: Vytvoření instance obrazu

Nyní je čas připravit obrázek, který chceme vložit do PDF. Aspose.PDF poskytuje `Image` třída pro práci s obrázky.

```csharp
// Vytvoření instance obrazu
Aspose.Pdf.Image img = new Aspose.Pdf.Image();
```
 
Vytvoříme novou instanci `Image` třída. Tento objekt bude obsahovat vlastnosti obrázku, který chceme přidat do PDF. Velikost a typ obrázku nakonfigurujeme v dalších krocích.

## Krok 4: Nastavení velikosti obrázku (šířka a výška)

Zde se dostáváme k jádru našeho tutoriálu: nastavení velikosti obrázku. Aspose.PDF umožňuje zadat šířku a výšku obrázku v bodech.

```csharp
// Nastavení šířky a výšky obrázku v bodech
img.FixWidth = 100;
img.FixHeight = 100;
```
 
Ten/Ta/To `FixWidth` a `FixHeight` Vlastnosti umožňují nastavit přesné rozměry obrázku v bodech. V tomto příkladu měníme velikost obrázku na 100x100 bodů. Tyto hodnoty můžete upravit podle svých potřeb.

## Krok 5: Zadejte typ obrázku

V závislosti na formátu obrázku, se kterým pracujete, může být nutné nastavit typ obrázku. Aspose.PDF podporuje různé formáty obrázků a zde definujeme typ souboru.

```csharp
// Nastavit typ obrázku jako SVG
img.FileType = Aspose.Pdf.ImageFileType.Unknown;
```
 
V tomto případě ponecháváme typ souboru jako `Unknown`což umožňuje knihovně automaticky detekovat typ obrázku. Pokud znáte konkrétní typ souboru, můžete jej nastavit (např. `ImageFileType.Jpeg` (pro obrázky JPEG). Tento krok zajišťuje, že Aspose ví, jak s obrázkem správně zacházet.

## Krok 6: Nastavte cestu k souboru s obrázkem

Nyní musíme Aspose sdělit, kde má najít soubor s obrázkem. Ujistěte se, že je váš obrázek v zadaném adresáři dostupný.

```csharp
// Cesta ke zdrojovému souboru
img.File = dataDir + "aspose-logo.jpg";
```
 
Zde nastavíme cestu k souboru s obrázkem. Obrázek se v tomto případě nachází v `dataDir` složka a je pojmenována `aspose-logo.jpg`Ujistěte se, že jste toto místo nahradili skutečným názvem a umístěním souboru s obrázkem.

## Krok 7: Přidání obrázku na stránku

Po nakonfigurování obrázku a nastavení cesty k souboru jej nyní můžeme přidat na naši stránku.

```csharp
// Přidejte obrázek do kolekce odstavců
page.Paragraphs.Add(img);
```
 
Ten/Ta/To `Paragraphs.Add()` metoda nám umožňuje přidat obrázek na stránku. Zamyslete se nad `Paragraphs` kolekce jako seznam položek, které se budou vykreslovat na stránce PDF. Do této kolekce můžeme přidat více prvků, například obrázky, text a tvary.

## Krok 8: Úprava vlastností stránky

Aby se nám obrázek dobře vešel, upravíme velikost stránky. Tím zajistíme, že rozměry stránky budou odpovídat obsahu, který přidáváme.

```csharp
// Nastavení vlastností stránky
page.PageInfo.Width = 800;
page.PageInfo.Height = 800;
```
 
Zde nastavujeme šířku a výšku stránky na 800 bodů. Tento krok je volitelný, ale zajišťuje, že se na stránku vejde upravený obrázek. Tyto hodnoty můžete upravit podle svých specifických požadavků.

## Krok 9: Uložte PDF

Nakonec, po konfiguraci vlastností obrázku a stránky, můžeme PDF uložit.

```csharp
// Uložte výsledný soubor PDF
dataDir = dataDir + "SetImageSize_out.pdf";
doc.Save(dataDir);
```
 
Upravený dokument uložíme jako `SetImageSize_out.pdf` ve stejném adresáři. Tento soubor bude nyní obsahovat změněnou velikost obrázku, který jste přidali.

## Závěr

tomto tutoriálu jsme se popsali, jak nastavit velikost obrázku v PDF pomocí Aspose.PDF pro .NET. Prošli jsme si vytvořením dokumentu, přidáním stránky, konfigurací obrázku a uložením výsledku. Tento podrobný návod je jen začátkem toho, co můžete s Aspose.PDF pro .NET dělat. Nyní, když jste se naučili měnit velikost obrázků, můžete se podívat na další funkce, jako je formátování textu, vytváření tabulek a dokonce i přidávání anotací do PDF.

## Často kladené otázky

### Mohu s Aspose.PDF pro .NET používat různé obrazové formáty?  
Ano, Aspose.PDF podporuje různé obrazové formáty, jako například JPEG, PNG, BMP a SVG.

### Jak zachovám poměr stran obrazu?  
Poměr stran můžete zachovat nastavením buď `FixWidth` nebo `FixHeight` zatímco druhá dimenze zůstává nenastavená.

### Mohu na jednu stránku PDF přidat více obrázků?  
Rozhodně! Stačí zopakovat proces přidávání instancí obrázku a každou z nich přidat do `Paragraphs` sbírka.

### Je možné nastavit velikost obrázku v jiných jednotkách než v bodech?  
Aspose.PDF pracuje primárně s body, ale můžete převést i jiné jednotky, jako jsou palce nebo milimetry, na body (1 palec = 72 bodů).

### Jak umístím obrázek na určité místo na stránce?  
Můžete nastavit `Image.LowerLeftX` a `Image.LowerLeftY` vlastnosti pro umístění obrázku na stránce.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}