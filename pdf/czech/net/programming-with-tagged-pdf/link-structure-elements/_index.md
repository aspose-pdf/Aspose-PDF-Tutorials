---
"description": "Naučte se, jak vytvářet prvky struktury odkazů v PDF pomocí Aspose.PDF pro .NET. Podrobný návod pro přidání přístupných odkazů, obrázků a ověření shody."
"linktitle": "Prvky struktury odkazů"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Prvky struktury odkazů"
"url": "/cs/net/programming-with-tagged-pdf/link-structure-elements/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Prvky struktury odkazů

## Zavedení

Vytváření a správa prvků struktury odkazů v PDF může být klíčová pro dokumenty vyžadující přístupnost a plynulou navigaci. V tomto tutoriálu si ukážeme, jak to udělat pomocí Aspose.PDF pro .NET. Pokud s Aspose.PDF nebo manipulací s PDF obecně začínáte, nebojte se. Vysvětlím vám každý krok podrobně, abyste se v něm snadno orientovali!

## Předpoklady  

Než se pustíme do kódování, pojďme si nejprve ujasnit pár věcí. Toto jsou základní požadavky pro zajištění hladkého vývoje.

1. Aspose.PDF pro .NET: Můžete si stáhnout nejnovější verzi [zde](https://releases.aspose.com/pdf/net/).
2. Vývojové prostředí .NET: Ať už se jedná o Visual Studio nebo jakékoli vývojové prostředí kompatibilní s .NET, mějte ho nainstalované a připravené.
3. Licence Aspose: Můžete použít bezplatnou zkušební verzi souboru Aspose.PDF [zde](https://releases.aspose.com/) nebo získat [dočasná licence](https://purchase.aspose.com/temporary-license/).
4. Základní znalost C#: Budeme pracovat s kódem v C#, takže pochopení základů nám to hodně usnadní.

## Importovat balíčky

Před napsáním kódu pro prvky struktury odkazů budete muset importovat několik balíčků. Začněte tím, že ve svém projektu odkážete na potřebné knihovny Aspose.PDF:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tyto importy nám umožňují pracovat s PDF dokumenty, přidávat tagy a spravovat strukturní prvky.

Nyní vytvoříme dokument PDF s různými typy struktur odkazů a každý krok bude rozebrán, abyste procesu důkladně porozuměli.

## Krok 1: Inicializace dokumentu  

Začněme vytvořením nového PDF dokumentu a nastavením označeného obsahu pro usnadnění přístupu.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "LinkStructureElements_Output.pdf";
string logFile = dataDir + "46035_log.xml";
string imgFile = dataDir + "google-icon-512.png";

// Vytvořte nový PDF dokument
Document document = new Document(); 

// Načíst rozhraní TaggedContent
ITaggedContent taggedContent = document.TaggedContent;
```
  
Zde inicializujeme `Document` objekt, který představuje náš PDF soubor. Také načteme `TaggedContent` rozhraní, které nám umožňuje přidávat strukturní prvky, jako jsou odstavce, odkazy a obrázky.

## Krok 2: Nastavení názvu a jazyka  

Každý PDF soubor by měl mít nastavení názvu a jazyka, zejména pokud usilujete o shodu se standardy PDF/UA.

```csharp
// Nastavení názvu a jazyka dokumentu
taggedContent.SetTitle("Link Elements Example");
taggedContent.SetLanguage("en-US");
```
  
Tento krok zajistí, že váš PDF bude mít smysluplný název a nastaví jazyk na angličtinu (`en-US`). To je zásadní pro přístupnost a zajišťuje, že čtečky obrazovky nebo jiné asistenční technologie dokáží váš dokument správně interpretovat.

## Krok 3: Vytvořte a přidejte odstavce  

V tomto kroku přidáme odstavce, které budou obsahovat naše prvky odkazu.

```csharp
// Vytvořte kořenový element
StructureElement rootElement = taggedContent.RootElement;

// Vytvořte odstavec a přidejte ho do kořenového elementu
ParagraphElement p1 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p1);
```
  
Vytvoříme kořenový strukturní prvek, který je v podstatě kontejnerem nejvyšší úrovně pro všechny ostatní prvky. Poté vytvoříme odstavec (`p1`) a přidejte jej ke kořenovému elementu.

## Krok 4: Přidání jednoduchého odkazu  

Nyní přidejme základní hypertextový odkaz, který bude odkazovat na Google.

```csharp
// Vytvořte element odkazu a přidejte ho do odstavce
LinkElement link1 = taggedContent.CreateLinkElement();
p1.AppendChild(link1);

// Nastavení hypertextového odkazu a textu pro odkaz
link1.Hyperlink = new WebHyperlink("http://google.com");
link1.SetText("Google");
link1.AlternateDescriptions = "Link to Google";
```
  
V tomto kroku jsme vytvořili prvek odkazu, nastavili jeho hypertextový odkaz na „http://google.com“ a poskytli text odkazu („Google“). Také jsme přidali alternativní popis pro zajištění přístupnosti.

## Krok 5: Přidání odkazu pomocí rozpětí  

Můžeme také vytvářet odkazy s různě dlouhým textem.

```csharp
// Vytvořte další odstavec
ParagraphElement p2 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p2);

// Vytvoření odkazu s elementem span
LinkElement link2 = taggedContent.CreateLinkElement();
p2.AppendChild(link2);
link2.Hyperlink = new WebHyperlink("http://google.com");

SpanElement span2 = taggedContent.CreateSpanElement();
span2.SetText("Google");
link2.AppendChild(span2);

link2.AlternateDescriptions = "Link to Google";
```
  
Zde jsme použili element span k uzavření části textu v odkazu, což nám umožnilo přizpůsobit, jak se určité části odkazu zobrazují.

## Krok 6: Víceřádkové propojení  

Co když je text odkazu příliš dlouhý? Nebojte se, můžete ho rozdělit na více řádků.

```csharp
ParagraphElement p4 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p4);

LinkElement link4 = taggedContent.CreateLinkElement();
p4.AppendChild(link4);
link4.Hyperlink = new WebHyperlink("http://google.com");
link4.SetText("The multiline link: Google Google Google Google Google...");
link4.AlternateDescriptions = "Link to Google (multiline)";
```
  
V tomto případě jsme vytvořili víceřádkový odkaz pouhým nastavením hodnoty dlouhého textu a text se automaticky zalomí přes více řádků.

## Krok 7: Přidání obrázku k odkazu  

Nakonec můžete do odkazu vložit i obrázky.

```csharp
// Vytvoření nového odstavce a prvku odkazu
ParagraphElement p5 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p5);

LinkElement link5 = taggedContent.CreateLinkElement();
p5.AppendChild(link5);
link5.Hyperlink = new WebHyperlink("http://google.com");

// Přidat obrázek k odkazu
FigureElement figure5 = taggedContent.CreateFigureElement();
figure5.SetImage(imgFile, 1200);
figure5.AlternativeText = "Google icon";
link5.AppendChild(figure5);

link5.AlternateDescriptions = "Link to Google";
```
  
Tento krok ukazuje, jak můžete vylepšit své odkazy obrázkem. V tomto případě jsme do odkazu přidali ikonu Google. Přístupnost jsme také zajistili nastavením alternativního textu k obrázku.

## Krok 8: Ověření shody PDF s předpisy  

Pokud usilujete o shodu s PDF/UA (standard přístupnosti), je dobrým zvykem ověřit váš dokument.

```csharp
// Uložit dokument PDF
document.Save(outFile);

// Ověřte shodu dokumentu s PDF/UA
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```
  
Dokument jsme uložili a ověřili ho podle standardu PDF/UA, což zajišťuje, že PDF splňuje požadavky na přístupnost.

## Závěr  

V tomto tutoriálu jsme se popsali, jak vytvářet strukturované PDF dokumenty pomocí Aspose.PDF pro .NET. Od přidávání základních hypertextových odkazů až po složitější struktury, jako jsou rozteče, víceřádkové odkazy a dokonce i obrázky, tato příručka poskytuje solidní základ pro manipulaci s prvky odkazů ve vašich PDF souborech. Díky výhodě kompatibility s PDF/UA jste nyní vybaveni k vytváření přístupných a snadno ovladatelných PDF souborů.

## Často kladené otázky

### Mohu do odkazů přidat složitější struktury, jako například tabulky?  
Ne, odkazy jsou primárně určeny pro text a obrázky, ale poblíž můžete vkládat i složitější prvky.

### Je ověření PDF/UA povinné?  
Ne vždy, ale pokud máte obavy o přístupnost, důrazně se to doporučuje.

### Co se stane, když je cesta k souboru s obrázkem nesprávná?  
Dokument nezobrazí obrázek a během vykreslování může dojít k chybě.

### Mohu stylizovat text v odkazu?  
Ano, textové styly můžete použít pomocí elementů span.

### Je možné vytvářet interní odkazy na dokumenty?  
Rozhodně! Můžete odkazovat na konkrétní sekce v rámci stejného dokumentu.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}