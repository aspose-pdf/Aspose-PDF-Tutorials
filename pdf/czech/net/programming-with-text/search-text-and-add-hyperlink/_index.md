---
"description": "Naučte se, jak vyhledávat text a přidávat hypertextové odkazy v PDF pomocí Aspose.PDF pro .NET s naším podrobným návodem."
"linktitle": "Vyhledat text a přidat hypertextový odkaz"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vyhledat text a přidat hypertextový odkaz"
"url": "/cs/net/programming-with-text/search-text-and-add-hyperlink/"
"weight": 450
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vyhledat text a přidat hypertextový odkaz

## Zavedení

Hledáte způsob, jak nejen manipulovat s PDF soubory, ale také je vylepšovat vkládáním hypertextových odkazů? Jste na správném místě! Díky výkonné knihovně Aspose.PDF pro .NET můžete ve svých PDF dokumentech vyhledávat textové vzory a bezproblémově přidávat hypertextové odkazy. Představte si, že máte dokument, který nejen sděluje informace, ale také propojuje čtenáře s relevantními zdroji pouhým kliknutím na odkaz. Zní to skvěle, že? V tomto tutoriálu vás krok za krokem provedeme vyhledáváním textu pomocí regulárních výrazů a přidáváním hypertextových odkazů do vašich PDF souborů. Ať už jste zkušený vývojář, nebo teprve začínáte, shledáte tento proces jednoduchým a obohacujícím.

## Předpoklady

Než se ponoříme do detailů, ujistěme se, že máte vše potřebné k dodržování pokynů. Zde je praktický kontrolní seznam:

- .NET Framework: Měli byste mít na svém počítači nainstalovaný .NET Framework (verze 4.0 nebo vyšší).
- Knihovna Aspose.PDF pro .NET: Nezapomeňte si stáhnout a přidat odkaz na knihovnu Aspose.PDF ve vašem projektu. Najdete ji [zde](https://releases.aspose.com/pdf/net/).
- IDE: K napsání a spuštění kódu budete potřebovat integrované vývojové prostředí (IDE), jako je Visual Studio.
- Ukázkový soubor PDF: Vezměte si ukázkový soubor PDF, na kterém můžete kód otestovat. Můžete vytvořit jednoduchý PDF nebo použít jeden ze stávajících dokumentů.

Jakmile odškrtnete vše na tomto seznamu, můžeme se pustit do toho!

## Importovat balíčky

Prvním krokem na naší cestě je import potřebných balíčků. Zde sdělíme našemu projektu, jaké nástroje budeme používat. Zde je návod, jak to udělat:

V souboru C# začněte zahrnutím následujících jmenných prostorů na začátek:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

Importem těchto jmenných prostorů poskytnete svému programu přístup ke všem skvělým funkcím, které Aspose.PDF nabízí.

Teď, když máme vše připravené, je čas pustit se do akce. Projdeme si to v několika krocích, takže pozorně sledujte!

### Krok 1: Nastavení adresáře dokumentů

Nejprve budete muset určit, kam jsou vaše soubory PDF uloženy. Upravte `dataDir` proměnnou, která bude odkazovat na adresář vašeho dokumentu. Zde je návod, jak to udělat:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Nezapomeňte vyměnit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou k vašim dokumentům.

### Krok 2: Vytvořte absorbér textového fragmentu

Dále potřebujeme nástroj pro nalezení textu, na který chceme vytvořit odkaz. Zadejte `TextFragmentAbsorber`Tento malý pomocník nám pomůže vyhledat konkrétní textový vzor v našem PDF.

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber("\\d{4}-\\d{4}");
```

Zde hledáme specifický vzorec: čtyři číslice, pomlčka a následované dalšími čtyřmi číslicemi (například telefonní číslo nebo rok).

### Krok 3: Povolení vyhledávání pomocí regulárních výrazů

Již používáme regulární výraz k nalezení textového vzoru, ale musíme se ujistit, že náš `absorber` ví, že je to povoleno. To je pro správné vyhledávání zásadní.

```csharp
absorber.TextSearchOptions = new TextSearchOptions(true);
```

### Krok 4: Inicializace PdfContentEditoru

Nyní, když máme absorbér připravený, potřebujeme `PdfContentEditor` pro práci s naším PDF souborem. Tato třída nám umožňuje navázat vazby na náš PDF soubor a manipulovat s ním.

```csharp
PdfContentEditor editor = new PdfContentEditor();
```

### Krok 5: Svázání zdrojového PDF souboru

S připraveným editorem obsahu je čas ho propojit se skutečným PDF souborem, se kterým chceme pracovat.

```csharp
editor.BindPdf(dataDir + "SearchRegularExpressionPage.pdf");
```

Nezapomeňte vyměnit `"SearchRegularExpressionPage.pdf"` s názvem vašeho PDF souboru.

### Krok 6: Přijměte absorbér pro stránku

Musíme dát editorovi vědět, že chceme vyhledávat na konkrétní stránce dokumentu. V tomto případě zvolme stránku 1.

```csharp
editor.Document.Pages[1].Accept(absorber);
```

### Krok 7: Příprava na procházení textových fragmentů

Nyní jsme připraveni projít všechny textové fragmenty nalezené naším absorbérem. Upravíme jejich vzhled a nastavíme hypertextový odkaz.

```csharp
int[] dashArray = { };
String[] LEArray = { };
Color blue = Color.Blue;
```

Zde nastavujeme některé parametry, například barvu našeho hypertextového odkazu.

### Krok 8: Procházení každého textového fragmentu

Pro každý textový fragment, který odpovídá našemu vyhledávání, změníme jeho barvu a vytvoříme hypertextový odkaz. Vypadá to takto:

```csharp
foreach (TextFragment textFragment in absorber.TextFragments)
{
    textFragment.TextState.ForegroundColor = Aspose.Pdf.Color.Blue;
    Rectangle rect = new Rectangle((int)textFragment.Rectangle.LLX,
        (int)Math.Round(textFragment.Rectangle.LLY), (int)Math.Round(textFragment.Rectangle.Width + 2),
        (int)Math.Round(textFragment.Rectangle.Height + 1));
    Enum[] actionName = new Enum[2] { Aspose.Pdf.Annotations.PredefinedAction.Document_AttachFile, Aspose.Pdf.Annotations.PredefinedAction.Document_ExtractPages };
    
    editor.CreateWebLink(rect, "http://www.aspose.com", 1, modrá, název akce);
    editor.CreateLine(rect, "", (float)textFragment.Rectangle.LLX + 1, (float)textFragment.Rectangle.LLY - 1,
        (float)textFragment.Rectangle.URX, (float)textFragment.Rectangle.LLY - 1, 1, 1, blue, "S", dashArray, LEArray);
}
```

### Krok 9: Uložte upravený PDF

Jsme skoro hotovi! Teď je čas uložit změny do nového PDF souboru.

```csharp
dataDir = dataDir + "SearchTextAndAddHyperlink_out.pdf";
editor.Save(dataDir);
```

### Krok 10: Zavřete editor

Nakonec nezapomeňte dokument zavřít, abyste uvolnili zdroje!

```csharp
editor.Close();
Console.WriteLine("\nText replaced and hyperlink added successfully based on a regular expression.\nFile saved at " + dataDir);
```

Právě jste vytvořili PDF s hypertextovým odkazem, který byl dynamicky generován na základě výsledků vyhledávání. To je skvělé?

## Závěr

A tady to máte! Dodržováním těchto kroků jste se naučili, jak prohledávat PDF a přidávat hypertextové odkazy pomocí knihovny Aspose.PDF pro .NET. To vám může otevřít spoustu možností, zejména pokud pracujete s dokumenty, které vyžadují interaktivitu. Představte si, že přidáváte odkazy na související zdroje, referenční webové stránky nebo dokonce interní stránky – to vše jen s několika řádky kódu!
## Často kladené otázky

### Co je Aspose.PDF pro .NET?  
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům vytvářet, manipulovat a spravovat PDF dokumenty v .NET aplikacích.

### Jak si mohu stáhnout soubor Aspose.PDF pro .NET?  
Knihovnu si můžete stáhnout [zde](https://releases.aspose.com/pdf/net/).

### Mohu si Aspose.PDF vyzkoušet zdarma?  
Rozhodně! Můžete získat bezplatnou zkušební verzi [zde](https://releases.aspose.com/).

### Je k dispozici podpora pro produkty Aspose?  
Ano, můžete najít podporu a diskuze v komunitě [zde](https://forum.aspose.com/c/pdf/10).

### Jak mohu získat dočasnou licenci pro Aspose.PDF?  
Můžete požádat o dočasnou licenci [zde](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}