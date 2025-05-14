---
"description": "V tomto podrobném návodu se naučte, jak přidat obrázek a čísla stránek do záhlaví a zápatí PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Obrázek a číslo stránky v sekci záhlaví a zápatí"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Obrázek a číslo stránky v sekci záhlaví a zápatí"
"url": "/cs/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Obrázek a číslo stránky v sekci záhlaví a zápatí

## Zavedení

Pokud jde o vytváření profesionálních PDF dokumentů, je nezbytné mít kontrolu nad drobnými detaily, jako jsou záhlaví a zápatí. Chcete, aby vaše dokumenty vypadaly uhlazeně a dobře organizovaně, že? S Aspose.PDF pro .NET můžete bez problémů přidávat obrázky a čísla stránek do záhlaví a zápatí dokumentu. V tomto tutoriálu vás provedeme každým krokem, abyste si ho snadno osvojili.

## Předpoklady

Než se ponoříte do detailů tohoto tutoriálu, ujistěte se, že máte vyřešeno následující:

1. .NET Framework: V počítači musíte mít nainstalovanou libovolnou verzi .NET Frameworku. Pokud ji nemáte, můžete si ji snadno stáhnout z webových stránek společnosti Microsoft.
2. Aspose.PDF pro .NET: Protože budeme používat Aspose.PDF, ujistěte se, že jej máte ve svém projektu nainstalovaný. Můžete si stáhnout zkušební verzi. [zde](https://releases.aspose.com/pdf/net/).
3. Základní znalost C#: Znalost základů programování v C# vám jistě pomůže porozumět kódu bez větších potíží.
4. Soubor s obrázkem: Budete potřebovat obrázek, který chcete vložit do záhlaví dokumentu PDF, například logo. Uložte ho do přístupného adresáře. 
5. IDE: Pro práci s vaším projektem .NET použijte integrované vývojové prostředí (IDE) dle vlastního výběru, například Visual Studio.

Jakmile budete mít připravené předpoklady, budete moci vytvořit skvělý PDF soubor!

## Importovat balíčky

Chcete-li začít používat Aspose.PDF pro .NET, je třeba importovat potřebné jmenné prostory. Na začátek souboru C# byste přidali:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Image;
```

Tyto jmenné prostory vám poskytnou přístup ke třídám potřebným pro manipulaci se soubory PDF.

A teď se pustíme do samotného díla! Postupujte podle těchto kroků a vytvořte si PDF dokument, do záhlaví vložte obrázek a do zápatí čísla stránek.

## Krok 1: Nastavení adresáře dokumentů

Každý dobrý projekt začíná organizací. Definujte adresář dokumentů, kam budete ukládat soubory a obrázky. Zde je návod, jak to udělat:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Nezapomeňte vyměnit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kam chcete PDF uložit a kde se nachází váš obrázek.

## Krok 2: Vytvořte nový dokument PDF

Dále vytvoříme nový PDF dokument, kde se bude dít všechna ta magie:

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

V tomto okamžiku jste vytvořili prázdný dokument PDF. Vzrušující, že?

## Krok 3: Přidání stránky do dokumentu

PDF je o stránkách. Přidejme do dokumentu novou stránku pomocí:

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

Nyní máte plátno, na kterém můžete začít navrhovat!

## Krok 4: Vytvořte záhlaví

Vaše záhlaví bude obsahovat obrázek (například logo), který chcete zobrazit. Vytvořte sekci záhlaví pomocí následujícího kódu:

```csharp
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
page.Header = header;
```

Nyní máte hlavičku, kterou si můžete přizpůsobit!

## Krok 5: Přidání obrázku do záhlaví

teď se dostáváme k té zábavné části! Obrázek musíte přidat do záhlaví. Nejprve vytvořte objekt obrázku:

```csharp
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
```

Nastavte cestu k souboru s vaším obrázkem:

```csharp
image1.File = dataDir + "aspose-logo.jpg";
```

Nakonec přidejte obrázek do záhlaví:

```csharp
header.Paragraphs.Add(image1);
```

Gratulujeme! Právě jste přidali obrázek do záhlaví PDF souboru.

## Krok 6: Vytvořte zápatí

Nyní se pojďme věnovat zápatí. Podobně jako u záhlaví vytvořte objekt zápatí:

```csharp
Aspose.Pdf.HeaderFooter footer = new Aspose.Pdf.HeaderFooter();
page.Footer = footer;
```

Sem umístíte číslo stránky. 

## Krok 7: Přidání textu do zápatí

Vytvořte fragment textu, který bude obsahovat číslo stránky:

```csharp
Aspose.Pdf.Text.TextFragment txt = new Aspose.Pdf.Text.TextFragment("Page: ($p of $P ) ");
```

Pak do zápatí přidejte tento textový fragment:

```csharp
footer.Paragraphs.Add(txt);
```

Vidíte, jak snadné to bylo? Číslo stránky jste si nastavili dynamicky!

## Krok 8: Uložení dokumentu PDF

Posledním krokem v našem dobrodružství je uložení dokumentu. Pomocí tohoto příkazu uložte nově vytvořený PDF soubor:

```csharp
doc.Save(dataDir + "ImageAndPageNumberInHeaderFooter_out.pdf");
```

A tak je váš PDF soubor připravený a načtený s obrázkem záhlaví a čísly stránek v zápatí!

## Závěr

tady to máte! Právě jste vytvořili PDF s obrázkem v záhlaví a dynamickými čísly stránek v zápatí pomocí Aspose.PDF pro .NET. Je neuvěřitelné, jak jen pár řádků kódu dokáže vytvořit tak propracovaný výstup. Ať už se jedná o firemní zprávu nebo personalizovaný dokument, přidání těchto prvků změní tón a profesionalitu vašeho PDF.

## Často kladené otázky

### Mohu použít Aspose.PDF na jakékoli platformě .NET?
Ano, Aspose.PDF pro .NET podporuje více platforem .NET včetně .NET Framework, .NET Core a dalších.

### Je k dispozici bezplatná zkušební verze pro Aspose.PDF?
Rozhodně! Můžete si stáhnout bezplatnou zkušební verzi [zde](https://releases.aspose.com/).

### Jaké formáty obrázků jsou podporovány pro záhlaví?
Aspose.PDF podporuje pro záhlaví a zápatí nejběžnější obrazové formáty, jako jsou JPG, PNG a BMP.

### Mohu si přizpůsobit formát čísla stránky?
Ano, text a formát zápatí si můžete snadno přizpůsobit podle svých potřeb.

### Je k dispozici technická podpora?
Ano, Aspose poskytuje specializovanou podporu prostřednictvím svého fóra. Můžete se na ně obrátit s žádostí o pomoc. [zde](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}