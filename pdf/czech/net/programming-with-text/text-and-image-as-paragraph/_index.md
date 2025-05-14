---
"description": "Vytvářejte PDF soubory s textem a obrázky pomocí Aspose.PDF pro .NET. Naučte se krok za krokem přidávat text a vložené obrázky."
"linktitle": "Text a obrázek jako odstavec v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Text a obrázek jako odstavec v souboru PDF"
"url": "/cs/net/programming-with-text/text-and-image-as-paragraph/"
"weight": 530
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Text a obrázek jako odstavec v souboru PDF

## Zavedení

dnešním digitálním světě jsou PDF univerzálním formátem dokumentů, se kterým se většina z nás setkává denně. Ať už se jedná o zprávu, elektronickou knihu nebo firemní fakturu, PDF usnadňují sdílení informací napříč různými platformami. Co když si ale chcete PDF programově přizpůsobit? A v tom případě přichází na řadu Aspose.PDF pro .NET. V tomto tutoriálu vás provedeme vkládáním textu a obrázků jako odstavců do PDF souboru pomocí Aspose.PDF pro .NET.

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte vše potřebné k jeho bezproblémovému sledování:

- Knihovna Aspose.PDF pro .NET: Budete muset nainstalovat Aspose.PDF pro .NET. Můžete si ji stáhnout [zde](https://releases.aspose.com/pdf/net/).
- Visual Studio: Jakákoli verze, která podporuje .NET, bude fungovat bez problémů.
- Základní znalost C#: Určitá znalost C# bude užitečná, ale nebojte se – provedu vás každým krokem!
- PDF dokument připraven: Pokud chcete přidat vlastní obrázek, mějte ho připravený.

Můžete si také vyzkoušet knihovnu zdarma [zde](https://releases.aspose.com/), nebo pokud pracujete na rozsáhlém projektu, zvažte jeho koupi [zde](https://purchase.aspose.com/buy)Potřebujete více informací? Prohlédněte si dokumentaci. [zde](https://reference.aspose.com/pdf/net/).

## Importovat balíčky

Abyste mohli začít s Aspose.PDF pro .NET, je třeba importovat požadované jmenné prostory. Tyto jmenné prostory umožňují interakci vašeho kódu v C# s funkcemi Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

Jednoduché, že? A teď se pojďme pustit do té zábavné části – vytvoření vlastního PDF souboru.

## Podrobný návod: Vytvoření PDF s textem a vloženým obrázkem

Rozdělme si to na stravitelné a snadno sledovatelné kroky. Představte si, že skládáte puzzle; každý krok je jako najít a umístit správný dílek.

## Krok 1: Inicializace dokumentu PDF

Prvním krokem je inicializace nového PDF dokumentu pomocí Aspose.PDF. Tento dokument bude sloužit jako základ pro přidávání textu a obrázků.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Vytvoření instance dokumentu
Document doc = new Document();
```

Co se tady děje? Jednoduše vytváříme nový dokument pomocí `Document` třídu a definování adresáře, kam chcete PDF uložit. Je to jako otevřít nové plátno pro vaše mistrovské dílo!

## Krok 2: Přidání stránky do PDF

Dokument bez stránek moc k ničemu není, že? Pojďme do dokumentu přidat prázdnou stránku.

```csharp
// Přidat stránku do kolekce stránek instance Document
Page page = doc.Pages.Add();
```

Tento úryvek kódu přidá novou stránku do kolekce stránek vašeho dokumentu. Představte si to jako otevření prázdné stránky v poznámkovém bloku.

## Krok 3: Přidání textu jako odstavce

Dále přidáme textový odstavec. Sem můžete vložit svou zprávu nebo nadpis.

```csharp
// Vytvořit textový fragment
TextFragment text = new TextFragment("Hello World.. ");
// Přidat fragment textu do kolekce odstavců objektu Page
page.Paragraphs.Add(text);
```

Zde vytváříme `TextFragment` objekt pro uložení textu „Hello World..“, který je poté přidán na stránku jako odstavec. Je to jako napsat první větu ve vašem PDF dokumentu.

## Krok 4: Přidání obrázku jako vloženého odstavce

Teď, když máme text, okořeníme to přidáním obrázku jako vloženého odstavce. Vložený odstavec jednoduše znamená, že se obrázek zobrazí hned za textem, podobně jako se obrázky zobrazují v dokumentech Wordu.

```csharp
// Vytvoření instance obrazu
Aspose.Pdf.Image image = new Aspose.Pdf.Image();
// Nastavit obrázek jako vložený odstavec, aby se zobrazoval hned za 
// Objekt předchozího odstavce (TextFragment)
image.IsInLineParagraph = true;
// Zadejte cestu k souboru s obrázkem 
image.File = dataDir + "aspose-logo.jpg";
```

V tomto úryvku vytvoříme `Image` objekt, řekněte mu, aby se zarovnal s textem, a zadejte cestu k souboru s obrázkem. To je ekvivalent vložení obrázku hned za větu v dokumentu. Soubor „aspose-logo.jpg“ můžete nahradit požadovaným obrázkem.

## Krok 5: Nastavení velikosti obrázku (volitelné)

Chcete změnit velikost obrázku? Žádný problém. Aspose.PDF vám nabízí možnost upravit výšku a šířku obrázku před jeho přidáním do dokumentu.

```csharp
// Nastavení výšky obrázku (volitelné)
image.FixHeight = 30;
// Nastavení šířky obrázku (volitelné)
image.FixWidth = 100;
```

Tato část je volitelná, ale pomáhá vám ovládat, jak velký nebo malý se obrázek v PDF zobrazí. Je to jako změnit velikost fotografie před jejím vytištěním.

## Krok 6: Přidání obrázku do kolekce odstavců

Obrázek máme připravený. Nyní ho vložíme do dokumentu jako vložený odstavec.

```csharp
// Přidat obrázek do kolekce odstavců objektu stránky
page.Paragraphs.Add(image);
```

Tento řádek přidá obrázek hned za text v kolekci odstavců. Je to jako stisknout tlačítko „Vložit obrázek“ v textovém editoru.

## Krok 7: Přidání dalšího odstavce vloženého textu

Co když chcete hned za obrázek přidat další text? Udělejme to vložením dalšího fragmentu textu.

```csharp
// Znovu inicializovat objekt TextFragment s jiným obsahem
text = new TextFragment(" Hello Again..");
// Nastavit TextFragment jako vložený odstavec
text.IsInLineParagraph = true;
// Přidat nově vytvořený TextFragment do kolekce odstavců stránky
page.Paragraphs.Add(text);
```

Znovu používáme `TextFragment` objekt s novým textem („Ahoj znovu..“) a jeho vložením přímo za obrázek. Díky tomu bude váš PDF soubor plynulý a soudržný.

## Krok 8: Uložení dokumentu PDF

Jsme skoro hotovi! Teď uložme dokument do vámi určeného adresáře.

```csharp
dataDir = dataDir + "TextAndImageAsParagraph_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nText and image added successfully as inline paragraphs.\nFile saved at " + dataDir);
```

Tento poslední krok uloží soubor do vašeho adresáře s názvem „TextAndImageAsParagraph_out.pdf“. Gratulujeme – vytvořili jste PDF s textem i vloženými obrázky!

## Závěr

A tady to máte – vytvoření PDF s textem a obrázky jako vloženými odstavci pomocí Aspose.PDF pro .NET je stejně jednoduché jako provedení těchto kroků. S pouhými několika řádky kódu můžete do svých PDF souborů přidat dynamický obsah, čímž je učiníte vizuálně přitažlivějšími a profesionálnějšími. Ať už se jedná o obchodní zprávu nebo elektronickou knihu, mít kontrolu nad rozvržením vašich PDF souborů může mít obrovský význam.

## Často kladené otázky

### Mohu přidat více obrázků jako vložené odstavce?  
Ano, můžete přidat více obrázků vytvořením samostatných `Image` objekty a jejich přidání do kolekce odstavců.

### Mohu ovládat polohu textu a obrázku v PDF?  
Ano, pomocí vlastností, jako jsou okraje, můžete ovládat přesné umístění textu a obrázků.

### Je Aspose.PDF pro .NET zdarma?  
Ne, je to licencovaný produkt, ale můžete si ho pořídit [bezplatná zkušební verze](https://releases.aspose.com/) nebo si koupit licenci [zde](https://purchase.aspose.com/buy).

### Mohu do textu přidat hypertextové odkazy?  
Ano, Aspose.PDF umožňuje přidávat hypertextové odkazy do textových fragmentů. Zaškrtněte [dokumentace](https://reference.aspose.com/pdf/net/) pro více informací.

### Mohu si přizpůsobit písmo a styl textu?  
Rozhodně! Písma, barvy a další stylistické vlastnosti textových fragmentů si můžete snadno přizpůsobit.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}