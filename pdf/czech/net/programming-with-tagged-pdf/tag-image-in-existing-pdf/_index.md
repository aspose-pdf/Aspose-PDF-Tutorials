---
"description": "Naučte se, jak označovat obrázky v existujících PDF souborech pomocí Aspose.PDF pro .NET. Podrobný návod pro zlepšení přístupnosti s dodržováním standardu PDF/UA."
"linktitle": "Označit obrázek v existujícím PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Označit obrázek v existujícím PDF"
"url": "/cs/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Označit obrázek v existujícím PDF

## Zavedení

V tomto tutoriálu si ukážeme, jak označit obrázek v existujícím PDF souboru pomocí Aspose.PDF pro .NET. Na konci tohoto průvodce budete schopni nastavit alternativní text pro obrázky, upravit atributy rozvržení a zajistit, aby váš PDF soubor splňoval standardy přístupnosti.

## Předpoklady

Než se do toho pustíme, pojďme si projít, co budete k začátku potřebovat:

- Aspose.PDF pro .NET: Ujistěte se, že jste si stáhli a nainstalovali nejnovější verzi souboru Aspose.PDF pro .NET. [Stáhnout zde](https://releases.aspose.com/pdf/net/).
- .NET Framework: Ujistěte se, že máte nainstalované vývojové prostředí .NET, jako je Visual Studio.
- Základní znalost struktury PDF: Znalost prvků struktury PDF, jako jsou odstavce, rozpětí, tabulky a obrázky.
- Platná licence: Licenci si můžete zakoupit [zde](https://purchase.aspose.com/buy) nebo použijte dočasný [zde](https://purchase.aspose.com/temporary-license/).

## Importovat balíčky

Abyste mohli začít s kódováním, je potřeba importovat základní jmenné prostory z Aspose.PDF pro .NET. Ty vám umožní přístup k potřebným třídám a metodám pro manipulaci s dokumentem PDF.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nyní, když jsme si připravili půdu, pojďme si rozdělit proces označování obrázku do několika kroků.

## Krok 1: Načtěte existující dokument PDF

Prvním krokem je načtení PDF souboru, se kterým chcete pracovat. Může se jednat o jakýkoli PDF soubor s obrázkem, který chcete označit tagy.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// Otevřete dokument
Document document = new Document(inFile);
```

- Nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou k vašemu souboru.
- Ten/Ta/To `Document` Třída umožňuje načíst existující PDF. Upravíte tento PDF soubor tak, aby byl obrázek označen tagy.

## Krok 2: Přístup k označenému obsahu a prvku kořenové struktury

Jakmile otevřete PDF, dalším krokem je přístup k označenému obsahu a identifikace prvku kořenové struktury. To je klíčové, protože vám to umožňuje procházet prvky v PDF a provádět úpravy.

```csharp
// Získat označený obsah a prvek kořenové struktury
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` poskytuje přístup ke strukturovaným prvkům v PDF.
- Ten/Ta/To `RootElement` je nejvyšším strukturním prvkem, od kterého můžete přecházet dolů k dalším prvkům, jako jsou odstavce, tabulky a obrázky.

## Krok 3: Nastavení názvu pro tagovaný dokument PDF

Přidáním názvu k tagovanému dokumentu PDF zajistíte, že bude dokument správně označen, což je užitečné pro přístupnost a shodu s PDF/UA.

```csharp
// Nastavení názvu pro tagovaný dokument PDF
taggedContent.SetTitle("Document with images");
```

- Nastavení názvu pro tagovaný PDF dokument zlepšuje přístupnost a srozumitelnost dokumentu pro čtečky obrazovky a asistenční technologie.

## Krok 4: Najděte a označte obrázek

Nyní si najděme obrazový prvek (označovaný jako `FigureElement` v souboru Aspose.PDF), nastavte pro něj alternativní text a nakonfigurujte jeho atributy rozvržení.

```csharp
// Procházet všechny prvky Figure (obrázky) a nastavit alternativní text a atributy rozvržení
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // Nastavení alternativního textu pro obrázek
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // Vytvoření a nastavení atributu BBox (ohraničující rámeček)
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // Nastavení atributů rozvržení pro obrázek
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- Tento kód prochází všemi `FigureElement` objekty v kořenové struktuře, které reprezentují obrázky.
- Nastavuje alternativní text pro přístupnost (čtečky obrazovky jej použijí k popisu obrázku).
- Ohraničující rámeček (`BBox`) určuje souřadnice pro rozvržení obrázku a zajišťuje jeho správné zobrazení v dokumentu.

## Krok 5: Úprava prvků rozsahu v tabulce

některých případech může být nutné upravit prvky typu span v tabulce. Zde si ukážeme, jak najít `SpanElement` a přesuňte to do odstavce.

```csharp
// Nalezení prvků table, span a paragraph
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// Přesunout element span do odstavce
spanElement.ChangeParentElement(paragraph);
```

- Zde nacházíme `TableElement`, `SpanElement`a `ParagraphElement` v rámci PDF.
- Použití `ChangeParentElement` metodou přesuneme rozpětí do odstavce, abychom zajistili správné tagování a strukturu.

## Krok 6: Uložte dokument a ověřte shodu s PDF/UA

Jakmile jsou provedeny všechny změny, posledním krokem je uložení aktualizovaného PDF a kontrola, zda splňuje standardy PDF/UA.

```csharp
// Uložit aktualizovaný dokument PDF
document.Save(outFile);

// Ověření shody s PDF/UA
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- Ten/Ta/To `Validate` Metoda kontroluje PDF dokument podle standardů PDF/UA a zaznamenává výsledky.
- Zajištění souladu s předpisy pomáhá zlepšit přístupnost a splnit regulační požadavky na publikování dokumentů.

## Závěr

tomto tutoriálu jsme vám ukázali, jak označit obrázky v existujícím PDF pomocí Aspose.PDF pro .NET. Nastavením alternativního textu, úpravou atributů rozvržení a ověřením dokumentu pro shodu s PDF/UA můžete zajistit, aby vaše PDF soubory byly přístupné a splňovaly moderní standardy. Aspose.PDF usnadňuje práci se strukturovanými prvky a dává vám kontrolu nad rozvržením a přístupností dokumentu.

## Často kladené otázky

### K čemu se používá Aspose.PDF pro .NET?
Aspose.PDF pro .NET je výkonná knihovna používaná pro programovou tvorbu, úpravu a manipulaci s PDF dokumenty v prostředí .NET.

### Jak zajistím soulad s PDF/UA?
Můžete použít soubory Aspose.PDF `Validate` metoda pro kontrolu shody s PDF/UA po provedení úprav dokumentu.

### Co je alternativní text v PDF souborech?
Alternativní text je popis přidaný k obrázkům v PDF souborech za účelem zlepšení přístupnosti, zejména pro uživatele, kteří používají čtečky obrazovky.

### Mohu pomocí Aspose.PDF manipulovat s tabulkami a rozsahy v PDF?
Ano, Aspose.PDF umožňuje manipulovat s tabulkami, rozsahy a dalšími strukturovanými prvky v dokumentu PDF.

### Kde si mohu stáhnout Aspose.PDF pro .NET?
Nejnovější verzi souboru Aspose.PDF pro .NET si můžete stáhnout. [zde](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}