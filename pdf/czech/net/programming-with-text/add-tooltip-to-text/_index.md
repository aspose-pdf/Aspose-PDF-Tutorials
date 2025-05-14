---
"description": "Naučte se, jak přidávat popisky k textu v PDF souborech pomocí Aspose.PDF pro .NET. Vylepšete své PDF soubory informativním textem při najetí myší."
"linktitle": "Přidat popisek k textu v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přidat popisek k textu v souboru PDF"
"url": "/cs/net/programming-with-text/add-tooltip-to-text/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat popisek k textu v souboru PDF

## Zavedení

Pokud jde o vytváření poutavých a interaktivních PDF souborů, mohou být popisky neocenitelné. Znáte ty malé vyskakovací okna, která vám po najetí myší na něco poskytnou další informace? Mohou poskytnout kontext, popisy nebo dokonce i rady, aniž by zahltily váš dokument. V tomto tutoriálu si ukážeme, jak přidat popisky k textu v PDF souboru pomocí knihovny Aspose.PDF pro .NET. Ať už jste zkušený vývojář, nebo se ve světě PDF teprve seznamujete, jste na správném místě! Tak se do toho pustíme!

## Předpoklady

Než se pustíme do kódování, ujistěte se, že máte vše potřebné k hladkému průběhu.

### Nainstalováno Visual Studio
Je nezbytné mít na svém počítači nainstalované Visual Studio, protože to bude vaše primární vývojové prostředí pro .NET aplikace.

### Aspose.PDF pro knihovnu .NET
Budete také potřebovat k dispozici knihovnu Aspose.PDF. Můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/)Nezapomeňte to uvést v referencích projektu.

### Základní znalost C#
Znalost C# nám hodně pomůže, protože v tomto jazyce budeme programovat. Ale nebojte se – provedu vás každým krokem!

### PDF dokument pro práci
Můžete začít s prázdným dokumentem PDF, jako v tomto příkladu, nebo použít existující, pokud chcete.

A teď se pojďme pustit do kódování!

## Importovat balíčky 

Prvním krokem v našem kódovacím dobrodružství je import potřebných balíčků. Otevřete si projekt Visual Studia a na začátek souboru C# budete chtít přidat následující `using` směrnice:

```csharp
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
```

Tyto balíčky vám poskytují přístup ke všem třídám a funkcím, které potřebujete pro vytváření a manipulaci s dokumenty PDF.

## Krok 1: Nastavení adresáře dokumentů

Nejdříve musíme nastavit cestu, kam budeme ukládat své dokumenty. Představte si to jako nalezení útulného místa ve vašem souborovém systému, kde budou uloženy všechny vaše výtvory.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outputFile = dataDir + "Tooltip_out.pdf";
```

Nezapomeňte vyměnit `YOUR DOCUMENT DIRECTORY` se skutečnou cestou na vašem počítači.

## Krok 2: Vytvořte vzorový dokument PDF

Dále je čas vytvořit jednoduchý PDF soubor s nějakým textem. Zde zahájíme náš tvůrčí proces!

```csharp
// Vytvořit vzorový dokument s textem
Document doc = new Document();
doc.Pages.Add().Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a tooltip"));
doc.Pages[1].Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a very long tooltip"));
doc.Save(outputFile);
```

V tomto kroku vytvoříme dokument, přidáme dva textové fragmenty a uložíme ho do dříve zadané cesty.

## Krok 3: Otevření dokumentu pro zpracování

Teď, když máme dokument vytvořený, otevřeme ho, abychom mohli pracovat na popiscích!

```csharp
// Otevřít dokument s textem
Document document = new Document(outputFile);
```

Zde jednoduše načteme dokument, který jsme právě vytvořili.

## Krok 4: Vytvořte absorbér textu pro vyhledávání fragmentů textu

Potřebujeme najít fragmenty textu, kam chceme přidat popisky. Je to jako použití lupy k zvýraznění určité části velké mapy! 

```csharp
// Vytvořte objekt TextAbsorber pro nalezení všech frází odpovídajících regulárnímu výrazu.
TextFragmentAbsorber absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a tooltip");
document.Pages.Accept(absorber);
```

## Krok 5: Extrahování fragmentů textu

Dále extrahujeme fragmenty textu, které jsme našli v předchozím kroku.

```csharp
// Získejte extrahované fragmenty textu
TextFragmentCollection textFragments = absorber.TextFragments;
```

Tento úryvek nám umožňuje uchovávat reference pro textové fragmenty, které nás zajímají.

## Krok 6: Procházení fragmentů a přidání popisků

A teď přichází ta zábavná část! Projdeme si každý textový fragment a ke každému z nich přidáme popisek. Představte si, že kolem konkrétních položek (textových fragmentů) balíte malé dárky (popisky).

```csharp
// Procházejte fragmenty
foreach (TextFragment fragment in textFragments)
{
	// Vytvořit neviditelné tlačítko na pozici fragmentu textu
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// Hodnota AlternateName se zobrazí jako popisek v prohlížeči.
	field.AlternateName = "Tooltip for text.";
	// Přidat do dokumentu pole tlačítka
	document.Form.Add(field);
}
```

V každé iteraci vytvoříme pole tlačítka, které odpovídá pozici fragmentu textu, a přiřadíme mu text popisku.

## Krok 7: Opakujte pro dlouhé popisky

Stejně jako jsme přidali jednoduchý popisek, můžeme totéž udělat pro delší text. Pojďme rozšířit naši kreativitu!

```csharp
// Dále bude ukázka velmi dlouhého tooltipu
absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a very long tooltip");
document.Pages.Accept(absorber);
textFragments = absorber.TextFragments;
foreach (TextFragment fragment in textFragments)
{
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// Nastavit velmi dlouhý text
	field.AlternateName = "Lorem ipsum dolor sit amet, consectetur adipiscing elit," +
							" sed do eiusmod tempor incididunt ut labore et dolore magna" +
							" aliqua. Ut enim ad minim veniam, quis nostrud exercitation" +
							" ullamco laboris nisi ut aliquip ex ea commodo consequat." +
							" Duis aute irure dolor in reprehenderit in voluptate velit" +
							" esse cillum dolore eu fugiat nulla pariatur. Excepteur sint" +
							" occaecat cupidatat non proident, sunt in culpa qui officia" +
							" deserunt mollit anim id est laborum.";
	document.Form.Add(field);
}
```

Zde děláme stejnou práci jako předtím, ale s mnohem rozšířenějším popiskem.

## Krok 8: Uložte dokument

Posledním krokem je uložení dokumentu se všemi těmi novými a lesklými popisky. 

```csharp
// Uložit dokument
document.Save(outputFile);
```

A je to! Přidali jste do PDF popisky, díky nimž je uživatelsky přívětivější a interaktivnější.

## Závěr

Tak tady to máte – snadno srozumitelný návod, jak přidat popisky k textu v PDF souborech pomocí Aspose.PDF pro .NET. Tato technika může výrazně vylepšit uživatelský zážitek a učinit vaše dokumenty informativnějšími, aniž by čtenáře zahltila příliš velkým množstvím textu najednou. 

Pouhým najetím myší na slovo nebo frázi čtenář získá relevantní informace, které mu přidají hodnotu, a to bez zbytečných detailů. Vyhrňte si tedy rukávy a zkuste to! Než se nadějete, můžete vytvářet nejrůznější poutavé dokumenty, které vyčnívají.

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět PDF dokumenty v .NET aplikacích.

### Mohu používat Aspose.PDF zdarma?
Ano, Aspose nabízí bezplatnou zkušební verzi, abyste si mohli prohlédnout jeho funkce! Najdete ji [zde](https://releases.aspose.com/).

### Existují nějaké možnosti licencování pro Aspose.PDF?
Ano, můžete si zakoupit licenci nebo získat dočasnou licenci. Podívejte se na možnosti. [zde](https://purchase.aspose.com/).

### Mohu pomocí Aspose.PDF přidat interaktivní prvky jiné než popisky?
Rozhodně! Aspose.PDF umožňuje přidávat různé interaktivní prvky, jako jsou hypertextové odkazy, tlačítka a formuláře.

### Kde najdu další dokumentaci k Aspose.PDF?
Můžete si prohlédnout dokumentaci [zde](https://reference.aspose.com/pdf/net/) pro podrobnější pokyny.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}