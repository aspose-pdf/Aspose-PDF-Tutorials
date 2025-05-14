---
"description": "Naučte se přidávat a vyhledávat skrytý text v PDF dokumentech pomocí Aspose.PDF pro .NET. Podrobný návod s příklady kódu."
"linktitle": "Přidat a vyhledat skrytý text v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přidat a vyhledat skrytý text v souboru PDF"
"url": "/cs/net/programming-with-text/add-and-search-hidden-text/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat a vyhledat skrytý text v souboru PDF

## Zavedení

tomto tutoriálu vás provedeme podrobným návodem, jak přidat a vyhledat skrytý text v souboru PDF pomocí Aspose.PDF pro .NET. Ať už jste zkušený vývojář nebo nováček, který si chce zlepšit své programátorské dovednosti, tento článek vám poskytne informace, které potřebujete k začlenění funkce skrytého textu do svých aplikací.

## Předpoklady

Než se ponoříme do kódování, je třeba splnit několik předpokladů:

### Kontrolní seznam požadavků
- Visual Studio: Ujistěte se, že máte nainstalované Visual Studio. V tomto tutoriálu se předpokládá, že používáte .NET Framework.
- Aspose.PDF pro .NET: Potřebujete knihovnu Aspose.PDF pro .NET. Můžete si ji stáhnout [zde](https://releases.aspose.com/pdf/net/).
- Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět úryvkům kódu.

## Importovat balíčky

Než začnete s kódem, musíte se ujistit, že jste importovali potřebné jmenné prostory Aspose.PDF. Postupujte takto:

### Nastavení projektu
1. Otevřete Visual Studio a vytvořte nový projekt v C# nebo použijte existující.
2. Nainstalujte soubor Aspose.PDF přidáním balíčku NuGet. To provedete tak, že přejdete do Správce balíčků NuGet a vyhledáte `Aspose.PDF`. 
3. Případně si můžete knihovnu stáhnout přímo z [zde](https://releases.aspose.com/pdf/net/) a přidejte jej jako referenci do svého projektu.

### Importovat požadované jmenné prostory
V horní části souboru C# importujte následující jmenné prostory:

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tento krok je klíčový, protože tyto jmenné prostory obsahují třídy a metody potřebné k manipulaci s dokumenty PDF.

## Vytvoření PDF dokumentu se skrytým textem

Nyní, když máte vše nastavené, si projdeme kroky k vytvoření dokumentu PDF, který obsahuje viditelný i neviditelný text.

### Krok 1: Definování adresáře dokumentů
Nejprve budete chtít nastavit cestu, kam bude PDF soubor uložen. Tady začíná kouzlo!

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Změňte toto na váš adresář
```

Tento řádek definuje, kam bude uložen vygenerovaný PDF soubor. Nezapomeňte nahradit `YOUR DOCUMENT DIRECTORY` s vaší skutečnou cestou.

### Krok 2: Vytvořte dokument PDF
Dále vytvořme nový dokument PDF a přidáme do něj stránky.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
Page page = doc.Pages.Add();
```

Zde inicializujeme nový dokument a přidáváme stránku, kam umístíme naše textové fragmenty.

### Krok 3: Přidání viditelného a skrytého textu
Nyní do našeho PDF přidáme viditelný i neviditelný text.

```csharp
TextFragment frag1 = new TextFragment("This is common text.");
TextFragment frag2 = new TextFragment("This is invisible text.");
```

V tomto úryvku, `frag1` bude viditelné, zatímco `frag2` bude dále nastaveno na neviditelné.

### Krok 4: Nastavte text na neviditelný
Aby se text `frag2` neviditelný, stačí ho jen upravit `TextState`.

```csharp
frag2.TextState.Invisible = true;
```

Nastavením této vlastnosti bude jakýkoli text spojený s `frag2` se při prohlížení PDF nezobrazí.

### Krok 5: Přidání fragmentů textu na stránku
Nakonec tyto textové fragmenty přidáme na stránku a uložíme PDF.

```csharp
page.Paragraphs.Add(frag1);
page.Paragraphs.Add(frag2);
doc.Save(dataDir + "39400_out.pdf");
doc.Dispose();
```

Tato část kódu přidá na stránku naše textové fragmenty. Poté dokument řádně uložíme a zlikvidujeme.

## Hledání skrytého textu v PDF

Nyní, když jsme vytvořili PDF s viditelným i skrytým textem, jak tento skrytý text vyhledáme? Pojďme si to rozebrat.

### Krok 1: Načtěte dokument PDF
Abychom mohli v PDF vyhledávat text, musíme nejprve načíst dokument, který jsme právě vytvořili.

```csharp
doc = new Aspose.Pdf.Document(dataDir + "39400_out.pdf");
```

### Krok 2: Vytvořte absorbér textových fragmentů
Použijeme `TextFragmentAbsorber` zachytit všechny textové fragmenty v PDF.

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber();
absorber.Visit(doc.Pages[1]);
```

Zde určíme, že chceme absorbovat všechny textové fragmenty z první stránky.

### Krok 3: Iterace fragmentů
Nyní můžeme iterovat shromážděnými textovými fragmenty, abychom zjistili, které z nich jsou viditelné a které skryté.

```csharp
foreach (TextFragment fragment in absorber.TextFragments)
{
    Console.WriteLine("Text '{0}' on pos {1} invisibility: {2}",
        fragment.Text, fragment.Position.ToString(), fragment.TextState.Invisible);
}
```

Tato smyčka kontroluje každý textový fragment a vypisuje jeho obsah spolu s jeho pozicí a stavem viditelnosti. Pokud `fragment.TextState.Invisible` je nastaveno na hodnotu true, znamená to, že text je skrytý!

### Krok 4: Zlikvidujte dokument
Nakonec nezapomeňte dokument po dokončení znovu zlikvidovat.

```csharp
doc.Dispose();
```

## Závěr

tomto tutoriálu jsme si prošli vzrušujícím procesem přidávání a vyhledávání skrytého textu v souborech PDF pomocí Aspose.PDF pro .NET. Naučili jsme se, jak vytvořit dokument PDF s viditelným i skrytým textem a také jak programově vyhledávat tento skrytý text. Tato funkce může být neuvěřitelně užitečná v různých aplikacích, ať už potřebujete ukládat důvěrné informace nebo poskytovat jedinečný uživatelský zážitek ve svých dokumentech.

Jak se budete lépe seznamovat s ASPose.PDF, vaše možnosti se stanou nekonečnými. Neustále experimentujte a posouvejte hranice toho, čeho můžete se svými PDF dokumenty dosáhnout!

## Často kladené otázky

### Může Aspose.PDF zpracovat šifrované PDF soubory?  
Ano, Aspose.PDF podporuje šifrování a dešifrování PDF dokumentů. Své PDF soubory můžete snadno zabezpečit hesly.

### Je k dispozici zkušební verze pro Aspose.PDF?  
Rozhodně! Bezplatnou zkušební verzi si můžete stáhnout z [zde](https://releases.aspose.com/).

### Jaké programovací jazyky podporuje Aspose.PDF?  
Aspose.PDF poskytuje podporu pro více jazyků, včetně C#, Javy a Pythonu.

### Kde najdu dokumentaci k souboru Aspose.PDF?  
Dokumentaci si můžete prohlédnout [zde](https://reference.aspose.com/pdf/net/).

### Jak mohu získat podporu, pokud narazím na problémy?  
Pro podporu můžete navštívit fóra Aspose [zde](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}