---
"description": "V tomto podrobném návodu krok za krokem se naučíte, jak nastavit vlastnost callout v souboru PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Nastavení vlastnosti popisku v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Nastavení vlastnosti popisku v souboru PDF"
"url": "/cs/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení vlastnosti popisku v souboru PDF

## Zavedení

Vytváření profesionálních a vizuálně přitažlivých dokumentů PDF často vyžaduje přidání anotací, které upozorňují na konkrétní obsah. Jednou z takových anotací je popisek, který je podobný těm bublinám v komiksech. Pomáhá objasnit nebo zdůraznit text ve vašem PDF. Aspose.PDF pro .NET neuvěřitelně usnadňuje přidávání takových anotací do vašich dokumentů a v tomto tutoriálu si ukážeme, jak nastavit vlastnost popisek v souboru PDF pomocí této výkonné knihovny. Ať už jste zkušený vývojář, nebo teprve začínáte, po přečtení této příručky budete mít jasnou představu o tom, jak s popisky v souborech PDF pracovat.

## Předpoklady

Než se ponoříme do kódu, pojďme si probrat základy, které potřebujete k zahájení.

1. Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF pro .NET. Můžete si ji stáhnout z [zde](https://releases.aspose.com/pdf/net/).
2. IDE: Vývojové prostředí, jako například Visual Studio.
3. .NET Framework: Ujistěte se, že máte na svém počítači nainstalované rozhraní .NET.
4. Dočasná licence: Pokud chcete vyzkoušet všechny funkce Aspose.PDF bez omezení, pořiďte si [dočasná licence](https://purchase.aspose.com/temporary-license/).

## Importovat balíčky

Než začnete psát kód, je potřeba importovat potřebné balíčky, které vám umožní pracovat s PDF soubory a anotacemi.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Tyto importy vám poskytnou všechny potřebné třídy a metody pro manipulaci s PDF dokumenty a vytváření anotací, jako je například popisek.

## Krok 1: Inicializace dokumentu PDF

Prvním krokem na naší cestě je inicializace nového PDF dokumentu, kam přidáme naši anotaci s popiskem. Představte si to jako nastavení prázdného plátna, kam můžete začít přidávat prvky.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Inicializace nového PDF dokumentu
Document doc = new Document();
```
Zde vytváříme nový `Document` objekt, který bude sloužit jako náš PDF soubor. `dataDir` Proměnná je nastavena na adresář, kam chcete po dokončení uložit soubor PDF.

## Krok 2: Přidání nové stránky do dokumentu

Dokument PDF může mít více stránek a v tomto kroku do dokumentu přidáme novou stránku. Na tuto stránku umístíme naši popisnou anotaci.

```csharp
// Přidat do dokumentu novou stránku
Page page = doc.Pages.Add();
```
Ten/Ta/To `Pages.Add()` Metoda se používá k přidání nové stránky do `doc` objekt. Nová stránka je uložena v `page` proměnnou, kterou později použijeme při přidávání anotace.

## Krok 3: Definování výchozího vzhledu

Anotace, stejně jako popisek, mají vizuální vzhled, který si můžete přizpůsobit. V tomto kroku definujeme, jak by měl text v popisku vypadat.

```csharp
// Definujte výchozí vzhled anotace
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
Vytvoříme `DefaultAppearance` objekt, který definuje barvu textu a velikost písma. Zde bude text červený a velikost písma je nastavena na 10. Tento vzhled bude použit na popisek.

## Krok 4: Vytvořte anotaci s volným textem

Nyní je čas vytvořit samotnou anotaci. Anotace s volným textem nám umožňuje přidat popisek s konkrétním textem a stylem.

```csharp
// Vytvořte anotaci FreeText s popiskem
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
Vytvoříme `FreeTextAnnotation` objekt se specifickými souřadnicemi, které definují jeho polohu na stránce. `Intent` je nastaveno na `FreeTextCallout`, což značí, že se jedná o anotaci s popiskem. `EndingStyle` je nastaveno na `OpenArrow`, což znamená, že řádek popisu bude končit otevřenou šipkou.

## Krok 5: Definování bodů čáry popisu

Popisek má čáru, která ukazuje na oblast zájmu. Zde definujeme body, které tuto čáru tvoří.

```csharp
// Definujte body pro čáru popisu
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
Ten/Ta/To `Callout` vlastnost je pole `Point` objekty, z nichž každý představuje souřadnici na stránce. Tyto body definují cestu čáry popisu a dodávají jí klasický vzhled řečové bubliny.

## Krok 6: Přidání anotace na stránku

Po vytvoření a konfiguraci naší anotace je dalším krokem její přidání na stránku.

```csharp
// Přidejte anotaci na stránku
page.Annotations.Add(fta);
```
Ten/Ta/To `Annotations.Add()` Metoda se používá k umístění anotace na stránku, kterou jsme vytvořili dříve. Tento krok efektivně „nakreslí“ popisek na stránku PDF.

## Krok 7: Nastavení obsahu formátovaného textu

Popisky mohou obsahovat formátovaný text, což umožňuje vložit formátovaný obsah do bubliny. Přidejme ukázkový text.

```csharp
// Nastavení formátovaného textu pro anotaci
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">Toto je ukázka</span></p></body>";
```
Ten/Ta/To `RichText` Vlastnost je nastavena s HTML obsahem. To umožňuje detailní formátování v rámci popisku, například určení velikosti písma, barvy a stylu.

## Krok 8: Uložení dokumentu PDF

Nakonec, po nastavení všech parametrů, je třeba dokument uložit. Tímto krokem se dokončí vytvoření PDF souboru s popisem anotace.

```csharp
// Uložit dokument
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
Ten/Ta/To `Save()` Metoda uloží dokument do zadaného adresáře s názvem souboru „SetCalloutProperty.pdf“. Tímto krokem dokončíme proces vytváření PDF.

## Závěr

A tady to máte! Právě jste vytvořili PDF dokument s popisnou anotací pomocí Aspose.PDF pro .NET. Tato anotace může být neuvěřitelně užitečná pro zvýraznění nebo vysvětlení konkrétních částí dokumentu. Aspose.PDF nabízí výkonné API, které usnadňuje a zjednodušuje manipulaci s PDF. Ať už přidáváte anotace, převádíte dokumenty nebo zpracováváte složité úlohy s PDF, Aspose.PDF vám s tím pomůže.

## Často kladené otázky

### Mohu si vzhled popisku dále přizpůsobit?

Rozhodně! Můžete si přizpůsobit různé aspekty, jako je barva a tloušťka čáry a rodina a styl písma textu.

### Je možné přidat více popisků na jednu stránku?

Ano, můžete přidat libovolný počet popisků opakováním kroků pro každou anotaci.

### Jak změním polohu popisku?

Jednoduše upravte souřadnice v `Rectangle` a `Callout` vlastnosti pro změnu polohy anotace.

### Mohu pomocí Aspose.PDF přidat další typy anotací?

Ano, Aspose.PDF podporuje různé typy anotací, včetně zvýraznění, razítek a příloh souborů.

### Je obsah formátovaného textu omezen na HTML?

Ten/Ta/To `RichText` Vlastnost podporuje podmnožinu HTML, což umožňuje zahrnout stylizovaný text a základní formátování.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}