---
"description": "Naučte se, jak přidat obrázek a číslo stránky přímo do záhlaví PDF souboru pomocí Aspose.PDF pro .NET v tomto podrobném návodu."
"linktitle": "Obrázek a číslo stránky v sekci záhlaví a zápatí v textu"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Obrázek a číslo stránky v sekci záhlaví a zápatí v textu"
"url": "/cs/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section-inline/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Obrázek a číslo stránky v sekci záhlaví a zápatí v textu

## Zavedení

Aspose.PDF pro .NET je výkonný nástroj, který nabízí rozsáhlé možnosti pro manipulaci s PDF soubory a jejich generování. Ať už potřebujete přidat obrázky, upravit záhlaví a zápatí nebo spravovat text, Aspose.PDF vám s tím pomůže. V tomto tutoriálu se podíváme na to, jak přidat obrázek a číslo stránky přímo do záhlaví nebo zápatí PDF dokumentu. Pojďme se do toho pustit a rozebrat si celý proces krok za krokem.

## Předpoklady

Než se pustíme do samotného kódu, ujistěte se, že máte vše potřebné k jeho načtení:

- Aspose.PDF pro .NET: Stáhněte si nejnovější verzi z [Stránka pro stažení PDF od Aspose](https://releases.aspose.com/pdf/net/).
- Vývojové prostředí: Budete potřebovat C# IDE, například Visual Studio.
- Licence: Pokud ještě nemáte licenci, můžete si ji pořídit [dočasná licence zde](https://purchase.aspose.com/temporary-license/) nebo si kupte celý od [Obchod Aspose](https://purchase.aspose.com/buy).

Nyní, když máte připravené předpoklady, pojďme začít.

## Importovat balíčky

Než začnete s kódováním, nezapomeňte importovat potřebné jmenné prostory:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tyto balíčky umožňují práci se soubory PDF a manipulaci s textem.

## Krok 1: Nastavení adresáře dokumentů

První věc, kterou musíme udělat, je definovat cestu k adresáři, kam bude uložen náš PDF soubor. Tuto cestu lze přizpůsobit složce vašeho projektu nebo libovolnému umístění na vašem počítači.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Tato proměnná obsahuje umístění, kam bude váš dokument uložen. Nahraďte `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou.

## Krok 2: Vytvoření instance dokumentu PDF

V tomto kroku vytvoříme novou instanci `Aspose.Pdf.Document` objekt. Tento objekt bude sloužit jako páteř vašeho PDF souboru.

```csharp
// Vytvořte instanci objektu Document voláním jeho prázdného konstruktoru
Aspose.Pdf.Document pdf1 = new Aspose.Pdf.Document();
```

Zde vytváříme prázdný PDF soubor, který můžeme později naplnit obsahem.

## Krok 3: Přidání stránky do PDF

Váš PDF soubor potřebuje alespoň jednu stránku, na kterou můžete přidat záhlaví, zápatí a obsah. Přidejme do našeho dokumentu prázdnou stránku.

```csharp
// Vytvořte stránku v objektu PDF
Aspose.Pdf.Page page = pdf1.Pages.Add();
```

Zavoláním `pdf1.Pages.Add()`, do dokumentu se přidá nová stránka připravená k úpravě záhlaví a zápatí.

## Krok 4: Vytvořte a nastavte záhlaví

Nyní je čas vytvořit záhlaví dokumentu. Zde přidáme text, obrázek a číslo stránky.

```csharp
// Vytvořte záhlaví dokumentu
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
// Nastavení záhlaví souboru PDF
page.Header = header;
```

Vytvoříme `HeaderFooter` objektu a přiřadit ho k `Header` vlastnost stránky, která zajišťuje, že vše, co přidáme do záhlaví, se zobrazí v horní části stránky.

## Krok 5: Přidání vloženého textu do záhlaví

Přidání textu je stejně jednoduché jako vytvoření `TextFragment` a specifikaci jeho vlastností. Přidejme do záhlaví barevný text.

```csharp
// Vytvoření textového objektu
Aspose.Pdf.Text.TextFragment txt1 = new Aspose.Pdf.Text.TextFragment("Aspose.Pdf is a Robust component by");
// Zadejte barvu
txt1.TextState.ForegroundColor = Color.Blue;
txt1.IsInLineParagraph = true;
```

V tomto kroku vytvoříme `TextFragment` s obsahem „Aspose.Pdf je robustní komponenta od“ a nastavte její barvu na modrou. `IsInLineParagraph` Vlastnost zajišťuje, že text bude vložený, což znamená, že se zobrazí na stejném řádku jako ostatní prvky (jako obrázek a další text).

## Krok 6: Vložení vloženého obrázku do záhlaví

Aby byla vaše záhlaví vizuálně atraktivní, můžete do textu přidat obrázek. Může to být logo vaší společnosti nebo jakýkoli jiný grafický prvek.

```csharp
// Vytvořte v sekci objekt obrázku
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
// Nastavte cestu k souboru s obrázkem
image1.File = dataDir + "aspose-logo.jpg";
// Nastavení šířky obrázku Informace
image1.FixWidth = 50;
image1.FixHeight = 20;
// Označuje, že InlineParagraph v segmentu seg1 je obrázek.
image1.IsInLineParagraph = true;
```

Zde přidáme obrázek do záhlaví vytvořením `Image` objektu, nastavení jeho cesty a úprava šířky a výšky. `IsInLineParagraph` zajišťuje, že obrázek je zarovnaný s textem.

## Krok 7: Přidání dalšího vloženého textu pro dokončení záhlaví

Přidejme další text pro dokončení vložené hlavičky.

```csharp
Aspose.Pdf.Text.TextFragment txt2 = new Aspose.Pdf.Text.TextFragment(" Pty Ltd.");
txt2.IsInLineParagraph = true;
txt2.TextState.ForegroundColor = Color.Maroon;
header.Paragraphs.Add(txt1);
header.Paragraphs.Add(image1);
header.Paragraphs.Add(txt2);
```

V této části vytvoříme další `TextFragment` s obsahem „Pty Ltd.“ a nastavte jeho barvu na kaštanově hnědou. Do záhlaví se přidají jak textové fragmenty, tak i obrázek.

## Krok 8: Uložte PDF

Jakmile nastavíte záhlaví, je čas uložit PDF.

```csharp
// Uložit PDF
pdf1.Save(dataDir + "ImageAndPageNumberInHeaderFooter_UsingInlineParagraph_out.pdf");
```

Ten/Ta/To `Save` Metoda zapíše finální PDF soubor do zadaného umístění.

## Závěr

Gratulujeme! Úspěšně jste přidali obrázek a text do záhlaví PDF dokumentu pomocí Aspose.PDF pro .NET. Tento tutoriál vás provedl základními kroky, včetně vytvoření dokumentu, přidávání stránek, vkládání záhlaví a umisťování vloženého obsahu, jako je text a obrázky. Aspose.PDF vám poskytuje neuvěřitelnou flexibilitu při správě PDF souborů, ať už se jedná o manipulaci se záhlavími, zápatími nebo složitým obsahem. 

## Často kladené otázky

### Mohu do záhlaví také přidat číslo stránky?
Ano! Číslo stránky můžete snadno přidat pomocí `TextFragment` třídu a naformátujte ji dle potřeby. Stačí ji vložit do sekce záhlaví jako vložený obsah.

### Jak nastavím obrázek na pozadí v záhlaví?
Můžete použít `BackgroundImage` majetek `HeaderFooter` třída pro nastavení obrázku na pozadí. Nejedná se však o vložený obsah a pokryje celou oblast záhlaví.

### Je možné použít i jiné formáty obrázků než JPEG?
Rozhodně! Aspose.PDF podporuje různé obrazové formáty, jako například PNG, BMP a GIF.

### Mohu si přizpůsobit písmo textu v záhlaví?
Ano, můžete použít `TextState` objekt pro změnu písma, velikosti a stylu textu.

### Potřebuji licenci k používání Aspose.PDF pro .NET?
Ano, Aspose.PDF vyžaduje licenci pro produkční použití, ale můžete začít s [bezplatná zkušební verze zde](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}