---
"description": "Naučte se, jak nastavit vlastní zarážky tabulace v PDF pomocí Aspose.PDF pro .NET. Tento tutoriál obsahuje podrobné pokyny pro profesionální zarovnání textu."
"linktitle": "Vlastní zarážky tabulace v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vlastní zarážky tabulace v souboru PDF"
"url": "/cs/net/programming-with-text/custom-tab-stops/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní zarážky tabulace v souboru PDF

## Zavedení

Už jste někdy museli formátovat text v PDF a přáli si mít přesnou kontrolu nad zarovnáním jednotlivých slov? A právě zde se hodí zarážky tabulátoru! Stejně jako v dokumentech Word můžete použít vlastní zarážky tabulátoru k dokonalému zarovnání textu v určitých bodech PDF. Ať už chcete obsah zarovnat vpravo, na střed nebo vlevo, Aspose.PDF pro .NET to usnadní. V tomto tutoriálu vás provedeme nastavením vlastních zarážek tabulátoru v souboru PDF pomocí Aspose.PDF pro .NET. Na konci budete schopni snadno vytvořit krásně zarovnaný dokument.

## Předpoklady

Než začneme, je třeba dodržovat následující pokyny:

- Aspose.PDF pro .NET: Budete muset mít nainstalovanou knihovnu Aspose.PDF. Můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/).
- Vývojové prostředí .NET: Ujistěte se, že máte nainstalované Visual Studio nebo jiné vývojové prostředí (IDE) pro spouštění aplikací .NET.
- Základní znalost C#: Budeme psát kód v C#, takže se doporučuje určitá znalost tohoto jazyka.
- Dočasná licence: Můžete použít [dočasná licence](https://purchase.aspose.com/temporary-license/) odemknout všechny funkce Aspose.PDF pro .NET.

Jakmile budete mít vše připravené, pojďme k importu potřebných balíčků a nastavení prostředí.

## Importovat balíčky

Chcete-li začít, budete muset importovat jmenné prostory Aspose.PDF. Zde je návod, jak to udělat:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Tyto dva řádky jsou zásadní. `Aspose.Pdf` jmenný prostor poskytuje strukturu dokumentu, zatímco `Aspose.Pdf.Text` nám poskytuje přístup k funkcím specifickým pro text, jako jsou vlastní zarážky tabulátoru.

Pojďme si rozebrat proces nastavení vlastních zarážek tabulátoru v PDF. Projdeme si každý krok podrobně, abyste se ujistili, že přesně rozumíte tomu, co se děje.

## Krok 1: Vytvořte nový dokument PDF

První věc, kterou musíte udělat, je vytvořit nový PDF dokument. Představte si ho jako své plátno. Přidáte stránky a poté na ně umístíte formátovaný text.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document _pdfdocument = new Document();
Page page = _pdfdocument.Pages.Add();
```

V tomto úryvku:
- Tvoříme nový `Document` objekt.
- Do dokumentu přidáme novou stránku pomocí `Pages.Add()`Sem vložíme text s tabulačními zarážkami.

## Krok 2: Nastavení zarážek tabulace

Nyní, když máme prázdný dokument, je čas definovat zarážky tabulátoru. Zarážky tabulátoru ovládají, jak se text zarovnává na různých pozicích na stránce. Můžete například chtít zarovnat část textu doprava a jinou na střed nebo doleva.

```csharp
Aspose.Pdf.Text.TabStops ts = new Aspose.Pdf.Text.TabStops();
Aspose.Pdf.Text.TabStop ts1 = ts.Add(100);
ts1.AlignmentType = TabAlignmentType.Right;
ts1.LeaderType = TabLeaderType.Solid;
```

Zde my:
- Inicializovat `TabStops` objekt, který bude obsahovat naše vlastní zarážky tabulátoru.
- Přidejte zarážku tabulátoru na značce 100 pixelů pomocí `ts.Add(100)`Toto definuje, kde se bude tabulace nacházet.
- Nastavte typ zarovnání na `Right`, což znamená, že text, který se dostane na tuto zarážku tabulátoru, se zarovná doprava.
- Definujte typ odkazové čáry. Odkazové čáry jsou tečky nebo čárky, které vyplňují prostor před zarážkou tabulátoru. V tomto případě používáme plnou čáru.

## Krok 3: Přidání dalších zarážek tabulace

Můžeme přidat libovolný počet zarážek tabulátoru. V tomto příkladu přidáme také tabulátor zarovnaný na střed a tabulátor zarovnaný vlevo.

```csharp
Aspose.Pdf.Text.TabStop ts2 = ts.Add(200);
ts2.AlignmentType = TabAlignmentType.Center;
ts2.LeaderType = TabLeaderType.Dash;

Aspose.Pdf.Text.TabStop ts3 = ts.Add(300);
ts3.AlignmentType = TabAlignmentType.Left;
ts3.LeaderType = TabLeaderType.Dot;
```

- Druhá zarážka tabulátoru je nastavena na 200 pixelů se zarovnáním na střed a čárkovanou vodicí čárou.
- Třetí zarážka tabulátoru je umístěna na 300 pixelech, zarovnána doleva a používá tečkovanou vodicí čáru.

## Krok 4: Vytvořte text pomocí tabulátorů

Nyní, když jsou zarážky tabulátoru nastaveny, je čas vytvořit text, který je používá. Tyto zarážky tabulátoru si můžete představit jako neviditelná vodítka, která pomáhají zarovnat obsah na různých pozicích.

```csharp
TextFragment header = new TextFragment("This is an example of forming a table with TAB stops", ts);
TextFragment text0 = new TextFragment("#$TABHead1 #$TABHead2 #$TABHead3", ts);
TextFragment text1 = new TextFragment("#$TABdata11 #$TABdata12 #$TABdata13", ts);
```

- `TextFragment` představuje kus textu.
- Používáme značky tabulací (`#$TAB`) abyste PDF souboru sdělili, kam má použít zarážky tabulátoru.
- Například v `text0`, `#$TABHead1` zarovná se podle první zarážky tabulátoru, `#$TABHead2` zarovná se s druhou a tak dále.

## Krok 5: Přidání segmentů do textu

Někdy můžete chtít rozdělit text do více segmentů, z nichž každý má vlastní zarážku tabulátoru. Zde je místo, kde `TextSegment` se hodí.

```csharp
TextFragment text2 = new TextFragment("#$TABdata21 ", ts);
text2.Segments.Add(new TextSegment("#$TAB"));
text2.Segments.Add(new TextSegment("data22 "));
text2.Segments.Add(new TextSegment("#$TAB"));
text2.Segments.Add(new TextSegment("data23"));
```

V tomto případě:
- Začínáme s `#$TABdata21`, který se zarovná s první zarážkou tabulátoru.
- Přidáváme další segmenty, jako např. `data22` a `data23`, přičemž každý je zarovnán k jiným zarážkám tabulátoru.

## Krok 6: Přidání textu na stránku PDF

Nyní, když jsme vytvořili všechny naše textové fragmenty, je čas je přidat na stránku.

```csharp
page.Paragraphs.Add(header);
page.Paragraphs.Add(text0);
page.Paragraphs.Add(text1);
page.Paragraphs.Add(text2);
```

Tento kód přidává každý `TextFragment` na stránku PDF a ujistěte se, že je text naformátován podle zarážek tabulátoru.

## Krok 7: Uložení dokumentu PDF

Nakonec musíme dokument uložit do vámi určeného adresáře.

```csharp
dataDir = dataDir + "CustomTabStops_out.pdf";
_pdfdocument.Save(dataDir);
Console.WriteLine("\nCustom tab stops setup successfully.\nFile saved at " + dataDir);
```

- Soubor PDF se uloží s použitými vlastními zarážkami tabulátoru.
- Zobrazí se zpráva potvrzující úspěšné vytvoření souboru.

## Závěr

A tady to máte! Dodržováním tohoto návodu jste se naučili, jak vytvářet vlastní zarážky tabulátoru v dokumentu PDF pomocí Aspose.PDF pro .NET. Zarážky tabulátoru vám umožňují zarovnat text strukturovaným a vizuálně přitažlivým způsobem, čímž vaše PDF soubory vypadají profesionálněji. Ať už zarovnáváte podrobnosti faktur, tabulky nebo jakoukoli jinou formu dat, tato funkce vám dává úplnou kontrolu nad umístěním textu.

## Často kladené otázky

### Mohu použít zarážky tabulátoru na existující PDF soubory?  
Ano, existující soubory PDF můžete upravit přidáním vlastních zarážek tabulátoru pro zarovnání textu.

### Jaké typy vedoucích jsou k dispozici?  
Pro vyplnění prostoru před zarážkou tabulátoru si můžete vybrat z plných, čárkovaných, tečkovaných a dalších typů odkazových značek.

### Mohu do jednoho řádku přidat více typů zarovnání?  
Rozhodně! Jak je znázorněno v příkladu, můžete v jednom řádku kombinovat zarovnání vpravo, vlevo a na střed.

### Existuje nějaký limit pro počet zarážek tabulace, které můžu přidat?  
Ne, můžete přidat tolik zarážek tabulace, kolik potřebujete, aby vyhovovalo vašim požadavkům na design.

### Mohu si přizpůsobit polohu zarážek tabulátoru?  
Ano, můžete definovat přesnou pozici v pixelech pro každou zarážku tabulátoru tak, aby vyhovovala vašemu rozvržení.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}