---
category: general
date: 2026-04-12
description: Přidejte obrázek do Wordu rychle pomocí C#. Naučte se, jak umístit obrázek
  ve Wordu, vložit obrázek do souboru docx a přidat vlastní XML pro pokročilé rozvržení.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: cs
og_description: Rychle přidejte obrázek do Wordu pomocí C#. Naučte se, jak umístit
  obrázek ve Wordu, vložit obrázek do souboru docx a přidat vlastní XML pro pokročilé
  rozvržení.
og_title: Přidat obrázek do Wordu – Kompletní průvodce programováním v C#
tags:
- C#
- Word Automation
- Document Generation
title: Přidat obrázek do Wordu – Kompletní průvodce programováním v C#
url: /cs/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání obrázku do Wordu – Kompletní průvodce programováním v C#

Už jste někdy potřebovali **add figure to Word**, ale nebyli jste si jisti, kde začít? Nejste v tom sami. V mnoha projektech kancelářské automatizace chybí správně umístěný obrázek nebo diagram, který žije uvnitř vlastního XML dílu. Tento průvodce vám ukáže přesně, jak **position figure in Word**, vložit obrázek do souboru *.docx* a dokonce upravit podkladové vlastní XML, aby se tvar choval jako jakýkoli nativní objekt Wordu.

Provedeme vás reálným příkladem pomocí knihovny GemBox.Document (zdarma pro malé soubory, komerční pro větší zátěže). Na konci budete mít samostatný spustitelný program, který vloží obrázek na souřadnice X = 50, Y = 200 uvnitř kontejneru s označeným obsahem. Žádné vágní zkratky typu „viz dokumentaci“ – jen čistý kód, proč funguje, a tipy, které můžete přímo zkopírovat do svého projektu.

## Požadavky

- .NET 6.0 nebo novější (kód se také kompiluje s .NET Core 3.1)
- **GemBox.Document** NuGet balíček (`Install-Package GemBox.Document`)
- Výchozí soubor Word (`input.docx`), který již obsahuje vlastní XML značku, kam chcete obrázek vložit
- Základní znalost C# (uvidíte, proč je každý řádek důležitý)

> **Pro tip:** Pokud nemáte předem označený dokument, můžete jej vytvořit ve Wordu vložením *Content Control* → *XML Mapping Pane* → mapování vlastního XML dílu. Knihovna bude tento ovládací prvek zacházet jako `TaggedContent`.

## Krok 1 – Načtení zdrojového dokumentu

Prvním krokem je otevření existujícího souboru *.docx*. `Document` je vstupní bod pro všechny operace GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Proč?* Načtení souboru nám poskytuje přístup k jeho vnitřním částem, včetně všech vlastních XML kontejnerů. Bez toho bychom nemohli najít uzel `TaggedContent`, který bude obsahovat náš obrázek.

## Krok 2 – Přístup k označenému obsahu (vlastní XML kontejner)

Vlastní XML je uloženo uvnitř *content control* ve Wordu. GemBox jej zpřístupňuje jako `TaggedContent`. 

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Pokud má dokument více označených sekcí, `TaggedContent` vrací **první**. Můžete také enumerovat `doc.TaggedContents` a vybrat konkrétní značku podle názvu.

## Krok 3 – Vytvoření elementu obrázku

`FigureElement` představuje obrázek, graf nebo jakýkoli vizuální objekt, který Word považuje za *shape*. Vytvoříme jej uvnitř označeného kontejneru.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Proč zde vytvořit obrázek?* Připojením k uzlu vlastního XML Word ví, že obrázek patří do této logické sekce, což je klíčové pro pozdější úpravy nebo workflow založené na content‑control.

## Krok 4 – Přesné umístění obrázku

Word používá pro umístění body (1 pt ≈ 1/72 in). Struktura `PointF` nám umožňuje snadno nastavit souřadnice X/Y.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Jak umístit shape ve Wordu:** Vlastnost `Position` přijímá `PointF`, kde první hodnota je horizontální posun (vlevo) a druhá je vertikální posun (nahoře) relativně k okraji stránky. Upravením těchto čísel můžete jemně doladit umístění.

## Krok 5 – Vložení obrázku do stromu označeného obsahu

Nyní připojíme obrázek k kořenovému elementu stromu vlastního XML. Tím se fyzicky přidá shape do dokumentu Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

V tomto okamžiku obrázek existuje v dokumentu, ale ještě nemá zdroj obrázku. Přidáme jednoduchý PNG ze souboru.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Krok 6 – Uložení upraveného dokumentu

Nakonec zapíšeme změny zpět do nového souboru *.docx*.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Když otevřete `output.docx` ve Wordu, uvidíte obrázek umístěný přesně na (50, 200) uvnitř vlastního XML bloku, který jste cílili.

### Kompletní funkční příklad

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Očekávaný výsledek:** Otevření `output.docx` ukazuje PNG umístěný přesně tam, kde jste zadali, vnořený do vlastního XML dílu. Pokud prozkoumáte XML dokumentu (`.docx` → unzip → `word/document.xml`), uvidíte element `<w:pict>` se správnými souřadnicemi `<v:shape>`.

## Časté otázky a okrajové případy

### Co když má dokument více označených sekcí?

Použijte `doc.TaggedContents` k enumeraci a výběru podle názvu značky:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Jak přidat popisek k obrázku?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Funguje to s Word 2010 a novějšími?

Ano. GemBox.Document cílí na standard Open XML, který je kompatibilní s Word 2007 + (včetně 2010, 2013, 2016, 2019 a Microsoft 365).

### Co když potřebuji otočit shape?

```csharp
figure.Rotation = 45; // degrees
```

### Jak přidat vektorovou grafiku místo rastrového obrázku?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro tipy a úskalí

- **File paths:** Používejte `Path.Combine` k vyhnutí se pevně zakódovaným oddělovačům, zejména na ne‑Windows platformách.
- **License limits:** Bezplatná licence GemBox omezuje velikost dokumentu na 20 KB. Pro větší soubory zakupte komerční klíč.
- **Performance:** Opakované používání jedné instance `Document` pro dávkové zpracování dramaticky snižuje paměťovou zátěž.
- **Shape overflow:** Pokud rozměry obrázku přesahují okraje stránky, Word jej ořízne. Podle toho upravte `figure.Width` a `figure.Height`.

## Závěr

Nyní víte **how to add figure to Word**, přesně **position figure in Word** a jak manipulovat s podkladovým vlastním XML, aby se shape choval jako jakýkoli nativní prvek. Kompletní spustitelný příklad demonstruje každý krok – od načtení dokumentu, vytvoření `FigureElement`, nastavení jeho souřadnic, připojení obrázku a nakonec uložení aktualizovaného *.docx*.

Dále zkuste experimentovat s **insert figure into docx** přidáním více obrázků, použitím smyček nebo generováním grafů za běhu. Můžete také prozkoumat **how to add custom xml** pro bohatší content control nebo se naučit **how to position shape word** v tabulkách a záhlavích. Možnosti jsou neomezené a s těmito základy jste připraveni automatizovat dokumenty Word jako profesionál.

Šťastné kódování a neváhejte zanechat komentář, pokud narazíte na nějaké potíže!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}