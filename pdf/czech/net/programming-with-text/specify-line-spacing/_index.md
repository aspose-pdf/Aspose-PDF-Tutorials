---
"description": "Naučte se, jak v PDF pomocí Aspose.PDF pro .NET zadat řádkování v souboru. Ideální pro vývojáře, kteří hledají přesné formátování textu."
"linktitle": "Zadání řádkování v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Zadání řádkování v souboru PDF"
"url": "/cs/net/programming-with-text/specify-line-spacing/"
"weight": 510
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zadání řádkování v souboru PDF

## Zavedení

Měli jste někdy potíže s ovládáním řádkování v souboru PDF? Možná jste měli text, který vypadal příliš natěsnaný nebo prostě nevypadal tak uhlazeně, jak byste si představovali. V tomto tutoriálu si ukážeme, jak snadno nastavit řádkování v PDF pomocí Aspose.PDF pro .NET. Použijeme jednoduchý podrobný návod, který vás provede od prázdného PDF k PDF s vlastním řádkováním. To je ideální, pokud potřebujete přesné rozvržení textu v dokumentech, jako jsou zprávy, faktury nebo certifikáty.

## Předpoklady

Než se pustíme do kódu, ujistěme se, že máte vše potřebné:

1. Nainstalován soubor Aspose.PDF pro .NET. Pokud jej nemáte, stáhněte si jej z [Stránka ke stažení Aspose.PDF](https://releases.aspose.com/pdf/net/).
2. Vývojové prostředí .NET (jako je Visual Studio).
3. Soubor písma TrueType (`.ttf`), které použijeme v příkladu. Můžete použít libovolné písmo, ale v této příručce použijeme `HPSimplified.TTF` písmo.
4. Základní znalost C# a práce s PDF.

Pokud jste připraveni, pojďme k importu potřebných balíčků.

## Importovat balíčky

Ve vašem projektu v C# budete muset importovat jmenné prostory Aspose.PDF, abyste mohli pracovat s funkcemi PDF. Zde je návod, jak to udělat:

```csharp
using Aspose.Pdf.Text;
using System.IO;
```

Tyto jmenné prostory umožňují vytvářet a manipulovat s dokumenty PDF a také pracovat s formátováním textu a možnostmi písma.

Rozdělíme to na několik kroků, abyste se v tom snadno orientovali. Každý krok se zaměří na klíčovou část procesu, od nastavení PDF až po určení řádkování.

## Krok 1: Nastavení projektu a definování adresáře dokumentů

První věc, kterou musíme udělat, je definovat, kde se naše soubory nacházejí. To pomůže programu vědět, kde najít písmo a kam uložit výsledný PDF soubor.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string fontFile = dataDir + "HPSimplified.TTF";
```

V tomto kroku nahradíte `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou k uložení souborů. Sem umístíte soubor s písmem (`HPSimplified.TTF`) a kam bude PDF soubor uložen.

## Krok 2: Načtení dokumentu PDF

Nyní musíme vytvořit nový dokument PDF. V tomto návodu začneme s prázdným dokumentem, ale v případě potřeby můžete načíst i existující PDF.

```csharp
Document doc = new Document();
```

Tím se vytvoří nový, prázdný PDF dokument. Snadné, že?

## Krok 3: Nastavení možností formátování textu

A tady se začne dít ta pravá magie. Určíme režim řádkování textu, který chceme do PDF přidat. Aspose.PDF nám nabízí několik možností, ale v této příručce použijeme `LineSpacingMode.FullSize`, což zajišťuje plné dodržení řádkování.

```csharp
TextFormattingOptions formattingOptions = new TextFormattingOptions();
formattingOptions.LineSpacing = TextFormattingOptions.LineSpacingMode.FullSize;
```

Tento kód nastaví režim řádkování na `FullSize`čímž se zajistí, že text bude zobrazen se správným rozestupem. Existují i další možnosti, jako například `Proportional` Pokud chcete různé způsoby rozestupů, ale prozatím se držme `FullSize`.

## Krok 4: Vytvořte textový fragment

Nyní vytvoříme samotný text, který bude umístěn do PDF. Tento text bude respektovat řádkování, které jsme definovali.

```csharp
TextFragment textFragment = new TextFragment("Hello world");
```

Vytvořili jsme textový fragment s řetězcem `"Hello world"`Tento text si samozřejmě můžete upravit podle libosti.

## Krok 5: Načtení a použití vlastního písma

Aby text vynikl, načteme ze souboru vlastní písmo TrueType. Tento krok je volitelný, ale může vašim PDF souborům dodat profesionální nádech.

```csharp
if (fontFile != "")
{
    using (FileStream fontStream = System.IO.File.OpenRead(fontFile))
    {
        textFragment.TextState.Font = FontRepository.OpenFont(fontStream, FontTypes.TTF);
```

Zde načteme soubor s písmem a aplikujeme ho na fragment textu. Pokud je cesta k souboru platná, použije se písmo. V opačném případě se použije výchozí písmo.

## Krok 6: Nastavení pozice a formátování textu

Dále musíme umístit text v PDF. Použijeme také možnosti formátování, které jsme vytvořili dříve.

```csharp
textFragment.Position = new Position(100, 600);
textFragment.TextState.FormattingOptions = formattingOptions;
```

Ten/Ta/To `Position` Metoda nastavuje souřadnice, kde se text na stránce zobrazí (v tomto případě 100 jednotek od levého okraje a 600 jednotek od spodního okraje). Zde se použijí možnosti formátování, včetně režimu řádkování.

## Krok 7: Přidání textu na stránku PDF

Nyní, když je náš text naformátován a umístěn, je čas ho přidat do dokumentu PDF.

```csharp
var page = doc.Pages.Add();
page.Paragraphs.Add(textFragment);
```

Tento kód vytvoří v dokumentu PDF novou stránku a přidá na ni fragment textu.

## Krok 8: Uložte PDF

Dosáhli jsme posledního kroku! Nyní, když je vše nastaveno, uložme PDF.

```csharp
dataDir = dataDir + "SpecifyLineSpacing_out.pdf";
doc.Save(dataDir);
```

Tím se PDF uloží se zadaným řádkováním a váš soubor je připraven!

## Závěr

A to je vše! Právě jste vytvořili PDF dokument s vlastním řádkováním pomocí Aspose.PDF pro .NET. Je to výkonný nástroj, který vám umožňuje ovládat každý aspekt vašich PDF souborů, a toto je jen jeden příklad toho, čeho můžete dosáhnout. Od umístění textu až po formátování, možnosti jsou nekonečné.

Pokud se chcete hlouběji ponořit do manipulace s PDF, Aspose.PDF nabízí nepřeberné množství funkcí k prozkoumání. Neváhejte experimentovat a posouvat hranice toho, co s vašimi dokumenty můžete dělat!

## Často kladené otázky

### Mohu upravit řádkování pro jiné režimy?  
Ano, můžete použít i jiné režimy, jako například `Propnebotional` or `Fixed` v závislosti na vašich potřebách.

### Je možné načíst fonty ze systému místo ze souboru?  
Ano, písma nainstalovaná systémem můžete načíst pomocí `FontRepository`.

### Mohu použít Aspose.PDF pro .NET s jinými formáty souborů?  
Rozhodně! Aspose.PDF pro .NET podporuje řadu formátů, jako je XML, HTML a další.

### Potřebuji licenci k používání Aspose.PDF pro .NET?  
Ano, pro plnou funkčnost budete potřebovat licenci, kterou si můžete zakoupit [zde](https://purchase.aspose.com/buy).

### Jak nastavím řádkování pro více odstavců?  
Můžete se přihlásit `TextFormattingOptions` každému `TextFragment` nebo `TextParagraph` pro ovládání mezer mezi více řádky nebo odstavci.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}