---
"description": "V tomto podrobném návodu se naučíte, jak odstranit hypertextové odkazy z HTML dokumentů po převodu do PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Odstranění hypertextových odkazů po převodu z HTML"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Odstranění hypertextových odkazů po převodu z HTML"
"url": "/cs/net/document-conversion/remove-hyperlinks-after-converting-from-html/"
"weight": 250
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Odstranění hypertextových odkazů po převodu z HTML

## Zavedení

V digitálním věku je převod HTML dokumentů do PDF běžným úkolem. Někdy však můžete chtít z převedeného PDF odstranit hypertextové odkazy z různých důvodů, například pro zlepšení čitelnosti nebo zabránění nežádoucí navigaci. V tomto tutoriálu se podíváme na to, jak toho dosáhnout pomocí Aspose.PDF pro .NET. 

## Předpoklady

Než se ponoříte do kódu, ujistěte se, že máte následující předpoklady:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Toto bude vaše vývojové prostředí.
2. Aspose.PDF pro .NET: Potřebujete knihovnu Aspose.PDF. Můžete si ji stáhnout z [zde](https://releases.aspose.com/pdf/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět kódu.

## Importovat balíčky

Chcete-li začít, musíte do svého projektu C# importovat potřebné balíčky. Zde je návod, jak to udělat:

1. Otevřete svůj projekt ve Visual Studiu.
2. V Průzkumníku řešení klikněte pravým tlačítkem myši na svůj projekt a vyberte možnost „Spravovat balíčky NuGet“.
3. Hledat `Aspose.PDF` a nainstalujte ho.

```csharp
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.IO;
```

Nyní, když máte vše nastavené, pojďme si rozebrat proces odstraňování hypertextových odkazů ze souboru HTML po jeho převodu do PDF.

## Krok 1: Nastavení adresáře dokumentů

Nejprve je třeba zadat cestu k adresáři s vašimi dokumenty. Zde se nachází váš HTML soubor a kam se uloží výstupní PDF.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kde je uložen váš HTML soubor.

## Krok 2: Načtení dokumentu HTML

Dále načtete HTML dokument pomocí `Document` třída z Aspose.PDF. Tato třída vám umožňuje snadno pracovat s PDF dokumenty.

```csharp
Document doc = new Document(dataDir + "SampleHtmlFile.html", new HtmlLoadOptions());
```

Zde načítáme HTML soubor s názvem `SampleHtmlFile.html`Ujistěte se, že tento soubor existuje ve vámi zadaném adresáři.

## Krok 3: Uložení dokumentu do paměťového streamu

Než začneme zpracovávat anotace, musíme dokument uložit do paměťového proudu. Tento krok je klíčový, protože připravuje dokument pro další manipulaci.

```csharp
doc.Save(new MemoryStream());
```

Tento řádek ukládá dokument do paměti, což nám umožňuje s ním pracovat, aniž bychom ho zatím zapisovali na disk.

## Krok 4: Iterace anotací

Nyní si projdeme anotace v dokumentu. Anotace jsou prvky jako odkazy, komentáře a zvýraznění. Nás konkrétně zajímají anotace odkazů.

```csharp
foreach (Annotation a in doc.Pages[1].Annotations)
{
    if (a.AnnotationType == AnnotationType.Link)
    {
        // Zpracovat anotaci odkazu
    }
}
```

V této smyčce kontrolujeme, zda je typ anotace odkaz. Pokud ano, pokračujeme k dalším krokům.

## Krok 5: Odebrání akce hypertextového odkazu

každé anotace odkazu musíme zkontrolovat, zda má akci hypertextového odkazu. Pokud ano, hypertextový odkaz odstraníme nastavením jeho URI na prázdný řetězec.

```csharp
LinkAnnotation la = (LinkAnnotation)a;
if (la.Action is GoToURIAction)
{
    GoToURIAction gta = (GoToURIAction)la.Action;
    gta.URI = "";
```

Tento úryvek kódu zajišťuje efektivní odstranění akce hypertextového odkazu.

## Krok 6: Absorbujte textové fragmenty

Dále se budeme zabývat textovými fragmenty spojenými s anotací odkazu. To nám umožní manipulovat se vzhledem textu.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
tfa.TextSearchOptions = new TextSearchOptions(a.Rect);
doc.Pages[a.PageIndex].Accept(tfa);
```

Zde vytváříme `TextFragmentAbsorber` a nastavte jeho možnosti vyhledávání na obdélník anotace. To nám pomůže najít odkazovaný text.

## Krok 7: Úprava vzhledu textu

Jakmile máme fragmenty textu, můžeme upravit jejich vzhled. V tomto případě odstraníme podtržení a změníme barvu textu na černou.

```csharp
foreach (TextFragment tf in tfa.TextFragments)
{
    tf.TextState.Underline = false;
    tf.TextState.ForegroundColor = Color.Black;
}
```

Tento krok zlepšuje čitelnost textu odstraněním stylu hypertextového odkazu.

## Krok 8: Smazání anotace

Po úpravě textu můžeme anotaci odkazu z dokumentu bezpečně odstranit.

```csharp
doc.Pages[a.PageIndex].Annotations.Delete(a);
}
```

Tento řádek odstraní hypertextový odkaz z PDF, čímž zajistí, že se v konečném výstupu již neobjeví.

## Krok 9: Uložení upraveného dokumentu

Nakonec musíme upravený dokument uložit do nového souboru PDF. Toto je poslední krok v našem procesu.

```csharp
doc.Save(dataDir + "RemoveHyperlinksFromText_out.pdf");
```

Tento řádek uloží dokument s odstraněnými hypertextovými odkazy a vytvoří nový soubor PDF s názvem `RemoveHyperlinksFromText_out.pdf`.

## Závěr

A tady to máte! Úspěšně jste odstranili hypertextové odkazy z HTML dokumentu po jeho převodu do PDF pomocí Aspose.PDF pro .NET. Tento proces nejen zlepšuje čitelnost vašeho PDF, ale také vám dává kontrolu nad obsahem, který prezentujete. 

## Často kladené otázky

### Mohu odstranit hypertextové odkazy z libovolného dokumentu PDF?
Ano, hypertextové odkazy můžete odstranit z libovolného PDF dokumentu pomocí Aspose.PDF pro .NET.

### Je Aspose.PDF zdarma k použití?
Aspose.PDF nabízí bezplatnou zkušební verzi, ale pro všechny funkce je nutné zakoupit licenci. Zkontrolujte [koupit stránku](https://purchase.aspose.com/buy).

### Co když narazím na problémy při používání Aspose.PDF?
Pomoc můžete vyhledat na [fórum podpory](https://forum.aspose.com/c/pdf/10).

### Mohu pomocí Aspose převést jiné formáty souborů do PDF?
Ano, Aspose podporuje různé formáty souborů pro převod do PDF.

### Kde si mohu stáhnout Aspose.PDF pro .NET?
Můžete si ho stáhnout z [odkaz ke stažení](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}