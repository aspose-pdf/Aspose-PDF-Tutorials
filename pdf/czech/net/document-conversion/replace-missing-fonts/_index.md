---
"description": "Naučte se, jak nahradit chybějící písma v dokumentech PDF pomocí Aspose.PDF pro .NET s tímto podrobným návodem."
"linktitle": "Nahradit chybějící písma"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Nahradit chybějící písma"
"url": "/cs/net/document-conversion/replace-missing-fonts/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nahradit chybějící písma

## Zavedení

Už se vám někdy stalo, že jste po otevření PDF dokumentu zjistili, že v něm chybí některá písma? Může to být frustrující, že? Chybějící písma mohou vést k tomu, že dokument vypadá úplně jinak, než zamýšlel tvůrce. Naštěstí s Aspose.PDF pro .NET můžete chybějící písma snadno nahradit a zajistit, aby si vaše PDF dokumenty zachovaly zamýšlený vzhled. V tomto tutoriálu vás krok za krokem provedeme celým procesem, který bude jednoduchý a přímočarý.

## Předpoklady

Než začneme, je třeba mít připraveno několik věcí:

1. Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF. Můžete si ji stáhnout z [zde](https://releases.aspose.com/pdf/net/).
2. Visual Studio: Vývojové prostředí, kde můžete psát a testovat svůj kód.
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.

## Importovat balíčky

Pro začátek budete muset importovat potřebné balíčky do vašeho projektu C#. Zde je návod, jak to udělat:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## Krok 1: Nastavení adresáře dokumentů

Nejprve je třeba zadat cestu k adresáři s vašimi dokumenty. Zde se nachází váš vstupní PDF soubor a kam bude uložen výstupní soubor.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## Krok 2: Inicializace původního písma

Dále se budete chtít pokusit najít původní písmo, které případně chybí. V tomto případě hledáme „AgencyFB“.

```csharp
Aspose.Pdf.Text.Font originalFont = null;
try
{
    originalFont = FontRepository.FindFont("AgencyFB");
}
catch (Exception)
{
    // Na cílovém počítači chybí písmo.
    FontRepository.Substitutions.Add(new SimpleFontSubstitution("AgencyFB", "Arial"));
}
```

Zde se pokusíme najít písmo. Pokud se nenajde, zachytíme výjimku a nahradíme ho běžnějším písmem, „Arial“. Tím zajistíme, že váš dokument bude stále vypadat dobře, i když původní písmo není k dispozici.

## Krok 3: Načtěte dokument PDF

Nyní načtěme PDF dokument, který chcete zpracovat. Budete muset zadat cestu ke vstupnímu souboru.

```csharp
var fileNew = new FileInfo(dataDir + "newfile_out.pdf");
var pdf = new Document(dataDir + "input.pdf");
```

V tomto kroku vytvoříme nový `FileInfo` objekt pro výstupní soubor a načíst vstupní PDF dokument do nového `Document` objekt.

## Krok 4: Převod dokumentu PDF

Před uložením dokumentu je vhodné jej převést do konkrétního formátu PDF. V tomto případě jej převedeme do formátu PDF/A-1B, což je standard pro dlouhodobou archivaci elektronických dokumentů.

```csharp
pdf.Convert(dataDir + "log.xml", PdfFormat.PDF_A_1B, ConvertErrorAction.Delete);
```

Tento řádek převede PDF a zaznamená všechny chyby do zadaného souboru XML. Pokud se během převodu vyskytnou nějaké problémy, budou zaznamenány do souboru „log.xml“.

## Krok 5: Uložení aktualizovaného dokumentu PDF

Konečně je čas uložit aktualizovaný PDF dokument s nahrazenými fonty.

```csharp
pdf.Save(fileNew.FullName);
```

Tento řádek uloží upravený PDF soubor do zadané cesty k výstupnímu souboru. A tímto způsobem jste úspěšně nahradili chybějící písma ve vašem PDF dokumentu!

## Závěr

Nahrazení chybějících písem v dokumentech PDF nemusí být náročný úkol. S Aspose.PDF pro .NET můžete snadno spravovat nahrazování písem a zajistit, aby vaše dokumenty vypadaly přesně tak, jak mají. Dodržováním kroků uvedených v tomto tutoriálu můžete zachovat integritu svých souborů PDF, i když některá písma nejsou k dispozici. Takže až příště narazíte na problém s chybějícím písmem, budete přesně vědět, co dělat!

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je výkonná knihovna, která umožňuje vývojářům programově vytvářet, manipulovat a převádět PDF dokumenty.

### Mohu používat Aspose.PDF zdarma?
Ano, Aspose nabízí bezplatnou zkušební verzi, kterou můžete použít k otestování knihovny. Můžete si ji stáhnout. [zde](https://releases.aspose.com/).

### Co mám dělat, když potřebné písmo není k dispozici?
Chybějící písmo můžete nahradit běžnějším písmem pomocí funkce nahrazování písem v souboru Aspose.PDF.

### Je možné převést PDF soubory do jiných formátů?
Rozhodně! Aspose.PDF podporuje konverzi do různých formátů, včetně PDF/A, DOCX a dalších.

### Kde najdu podporu pro Aspose.PDF?
Podporu a dotazy můžete najít na fóru Aspose. [zde](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}