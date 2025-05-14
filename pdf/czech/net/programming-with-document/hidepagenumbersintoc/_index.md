---
"description": "Naučte se, jak skrýt čísla stránek v obsahu pomocí Aspose.PDF pro .NET. Postupujte podle tohoto podrobného návodu s příklady kódu a vytvářejte profesionální PDF soubory."
"linktitle": "Skrýt čísla stránek v obsahu"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Skrýt čísla stránek v obsahu"
"url": "/cs/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skrýt čísla stránek v obsahu

## Zavedení

Při práci s PDF soubory se někdy může stát, že budete chtít vygenerovat obsah (TOC), ale zároveň zachovat elegantní vzhled skrytím čísel stránek. Možná dokument bez nich lépe vypadá, nebo je to možná estetická volba. Ať už je váš důvod jakýkoli, pokud pracujete s Aspose.PDF pro .NET, tento tutoriál vám ukáže, jak přesně skrýt čísla stránek v obsahu.

## Předpoklady

Než začneme, je tu několik věcí, které budete potřebovat. Zde je stručný kontrolní seznam:

- Nainstalované Visual Studio: Pro psaní kódu budete potřebovat funkční verzi Visual Studia.
- Knihovna Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF pro .NET.
  - Odkaz ke stažení: [Aspose.PDF pro .NET](https://releases.aspose.com/pdf/net/)
- Dočasná licence: Pokud testujete funkce, je užitečné mít dočasnou licenci.
  - Dočasná licence: [Získejte to zde](https://purchase.aspose.com/temporary-license/)

## Importovat balíčky

Než se pustíte do samotného kódu, ujistěte se, že jste do svého projektu v C# importovali následující jmenné prostory. Ty poskytnou potřebné třídy a metody pro práci s dokumenty PDF a vytváření obsahu (TOC).

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Nyní, když je vaše prostředí připravené a balíčky jsou importovány, pojďme si rozebrat jednotlivé kroky procesu. Probereme každou část kódu, abyste mohli snadno sledovat.

## Krok 1: Inicializace dokumentu PDF

První věc, kterou musíme udělat, je vytvořit nový PDF dokument a přidat stránku pro obsah (TOC).


```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir: Toto je adresář, kam bude uložen váš výstupní soubor.
- Dokument(): Inicializuje nový dokument PDF.
- Pages.Add(): Přidá do dokumentu novou prázdnou stránku, která bude později obsahovat váš obsah.

## Krok 2: Nastavení informací o obsahu a názvu

Dále definujeme informace o obsahu, včetně nastavení názvu, který se zobrazí v horní části obsahu.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo: Tento objekt obsahuje veškeré informace o obsahu.
- TextFragment: Představuje text názvu obsahu, zde jej nastavujeme jako „Obsah“.
- Styl písma: Název obsahu upravíme tak, že nastavíme jeho velikost na 20 a zvýrazníme ho tučně.
- tocPage.TocInfo: Informace o obsahu přiřadíme stránce, která bude obsah zobrazovat.

## Krok 3: Skrýt čísla stránek v obsahu

A teď ta zábavná část! Zde nakonfigurujeme obsah tak, aby se v něm skryla čísla stránek.

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers: Toto je magický přepínač, který skryje čísla stránek. Nastavte ho na `false`čísla stránek se v obsahu nezobrazí.
- FormatArrayLength: Nastavíme tuto hodnotu na 4, což znamená, že chceme definovat formátování pro čtyři úrovně nadpisů obsahu.

## Krok 4: Úprava formátování obsahu

Abychom vašemu obsahu dodali více stylu, definujeme nyní formátování pro různé úrovně nadpisů.

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray: Toto pole řídí formátování položek obsahu. Každý index představuje jinou úroveň nadpisu.
- Okraje a styl textu: Pro každou úroveň nadpisů nastavíme okraje a použijeme styly písma, jako je tučné, kurzíva a podtržené.

## Krok 5: Přidání nadpisů do dokumentu

Nakonec přidejme samotné nadpisy, které budou součástí obsahu.

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- Nadpis a textový segment: Tyto nadpisy představují nadpisy, které se objeví v obsahu. Každá úroveň má svůj vlastní nadpis.
- IsAutoSequence: Automaticky očísluje nadpisy.
- IsInList: Zajišťuje, aby se každý nadpis objevil v obsahu.

## Krok 6: Uložte dokument

Jakmile je vše nastaveno, uložte dokument PDF do vámi určeného výstupního souboru.

```csharp
doc.Save(outFile);
```

A to je vše! Úspěšně jste vytvořili PDF s obsahem a čísla stránek jsou skrytá!

## Závěr

Vytvoření obsahu v PDF a skrytí čísel stránek se může zdát složité, ale s Aspose.PDF pro .NET je to hračka. Dodržováním tohoto podrobného návodu jste se naučili, jak přizpůsobit formát obsahu, skrýt čísla stránek a aplikovat různé styly na nadpisy. Nyní můžete vytvářet profesionální PDF soubory přizpůsobené vašim přesným potřebám.

## Často kladené otázky

### Mohu v obsahu zobrazit čísla stránek pro konkrétní nadpisy?
Ne, Aspose.PDF skryje nebo zobrazí čísla stránek pro celý obsah. Nelze je selektivně skrýt pro konkrétní položky.

### Je možné do obsahu přidat další úrovně?
Ano, můžete zvýšit `FormatArrayLength` definovat více úrovní nadpisů obsahu.

### Jak mohu změnit písmo pro všechny položky obsahu?
Písmo můžete změnit úpravou `TextState.Font` nemovitost pro každou úroveň v `FormatArray`.

### Mohu do obsahu vkládat hypertextové odkazy?
Ano, každou položku obsahu můžete propojit s konkrétní sekcí v dokumentu pomocí `Heading.TocPage` vlastnictví.

### Potřebuji licenci pro Aspose.PDF?
Ano, pro produkční použití je vyžadována platná licence. Můžete získat dočasnou licenci. [zde](https://purchase.aspose.com/temporary-license/) otestovat funkce.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}