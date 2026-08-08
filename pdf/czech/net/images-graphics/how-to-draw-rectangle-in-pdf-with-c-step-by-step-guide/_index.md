---
category: general
date: 2026-03-27
description: Naučte se, jak kreslit obdélník v PDF pomocí Aspose.Pdf pro C#. Přidejte
  obdélník do PDF, přidejte tvar do PDF a nakreslete tvar v PDF s přehlednými ukázkami
  kódu.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: cs
og_description: Ovládněte, jak nakreslit obdélník v PDF pomocí Aspose.Pdf. Tento tutoriál
  vám krok za krokem ukáže, jak přidat obdélník do PDF, přidat tvar do PDF a nakreslit
  tvar v PDF.
og_title: Jak nakreslit obdélník v PDF pomocí C# – Kompletní průvodce
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Jak nakreslit obdélník v PDF pomocí C# – krok za krokem
url: /cs/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nakreslit obdélník v PDF pomocí C# – krok za krokem

Už jste se někdy zamýšleli **jak nakreslit obdélník** v PDF, aniž byste se museli potýkat s nízkoúrovňovou PDF syntaxí? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují vizualizovat ohraničovací rámeček, zvýrazněnou oblast nebo jednoduchý dekorativní prvek v generovaném dokumentu. Dobrá zpráva? S Aspose.Pdf pro .NET je to hračka.

V tomto tutoriálu projdeme vše, co potřebujete k **přidání obdélníku do PDF**, **přidání tvaru do PDF**, a nakonec **nakreslení obdélníku v PDF** pomocí čistého, idiomatického C#. Na konci budete mít spustitelný program, který vytvoří PDF soubor obsahující ostrý obdélník – bez nutnosti externích nástrojů.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Core a .NET Framework)
- NuGet balíček Aspose.Pdf pro .NET (`Install-Package Aspose.Pdf`)
- Základní vývojové prostředí C# (Visual Studio, VS Code, Rider, atd.)

Žádné další knihovny nejsou potřeba; vše ostatní zajišťuje samotný Aspose.Pdf.

## Krok 1: Nastavení projektu a import jmenných prostorů

Nejprve vytvořte novou konzolovou aplikaci a načtěte jmenný prostor Aspose.Pdf.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Proč je to důležité:** Import `Aspose.Pdf.Drawing` vám poskytne přístup ke třídě tvaru `Rectangle`, kterou použijeme k **nakreslení tvaru v PDF**. Udržení vstupního bodu přehledného usnadní pozdější kroky.

## Krok 2: Vytvoření nového PDF dokumentu a stránky

PDF bez stránek nedává smysl, takže začneme vytvořením objektu dokumentu a přidáním jedné stránky.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Vysvětlení:** Třída `Document` představuje celý soubor, zatímco `Pages.Add()` vrací čerstvý objekt `Page`, do kterého později **přidáme obdélník do PDF**. Výchozí velikost A4 funguje ve většině případů, ale můžete zadat šířku/výšku, pokud potřebujete vlastní plátno.

## Krok 3: Definování tvaru obdélníku

Nyní přichází jádro **jak nakreslit obdélník** – definování jeho pozice a rozměrů.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Proč nastavujeme tyto vlastnosti:**  
- `BorderColor` a `BorderWidth` řídí obrys, čímž dělají obdélník viditelným.  
- `FillColor` mu dává jemné pozadí, užitečné, když chcete zvýraznit oblast.  
- Konstruktor `(x, y, width, height)` vám umožní **nakreslit obdélník v PDF** přesně tam, kde jej potřebujete.

## Krok 4: Přidání obdélníku na stránku

S připraveným tvarem nyní **přidáme tvar do PDF** tím, že jej připojíme ke kolekci `Annotations` stránky. Aspose.Pdf automaticky ověří hranice, takže se nemusíte starat o přetečení.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Co se děje pod kapotou:** Kolekce `Annotations` zachází s obdélníkem jako s vektorovou grafikou. Když se PDF vykreslí, knihovna převede naše souřadnice do PDF content streamu.

## Krok 5: Uložení dokumentu

Nakonec zapíšeme PDF na disk, abyste jej mohli otevřít v libovolném prohlížeči.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Výsledek:** Otevření souboru `RectangleDemo.pdf` zobrazí světle šedý obdélník s černým okrajem umístěný 100 pt od levého okraje a 500 pt od spodního okraje stránky. To je kompletní řešení **jak nakreslit obdélník** v PDF pomocí C#.

## Kompletní funkční příklad

Sestavením všech částí získáte kompletní, připravený program:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Očekávaný výstup:** Soubor pojmenovaný `RectangleDemo.pdf` obsahující jednu stránku se středovým světle šedým obdélníkem ohraničeným černě. Soubor můžete otevřít v Adobe Reader, Chrome nebo jakémkoli PDF prohlížeči.

## Běžné varianty a okrajové případy

### 1. Kreslení více obdélníků

Pokud potřebujete **přidat obdélník do PDF** vícekrát, stačí vytvořit další objekty `Rectangle` a přidat je do `page.Annotations`. Procházení kolekce souřadnic to dělá triviální.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Použití různých jednotek

Aspose.Pdf pracuje v bodech (1 pt = 1/72 palce). Pokud dáváte přednost milimetrům, nejprve je převeďte:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Přidání obdélníku jako formulářového pole

Když potřebujete interaktivní obdélník (např. klikací oblast), použijte `LinkAnnotation` místo prostého `Rectangle`. Kód je podobný, ale přidává URL nebo JavaScript akci.

### 4. Problémy s kompatibilitou

Aspose.Pdf verze 23.9 (vydaná začátkem 2026) plně podporuje výše uvedené API. Starší verze mohou vyžadovat `page.AddAnnotation(rectangleShape)` místo `page.Annotations.Add`. Vždy zkontrolujte poznámky k vydání, pokud narazíte na chyby při kompilaci.

## Profesionální tipy a úskalí

- **Profesionální tip:** Nastavte `FillColor = Color.Transparent`, pokud potřebujete jen obrys. Tím mírně snížíte velikost souboru.  
- **Dejte pozor na:** Používání souřadnic, které přesahují rozměry stránky. Aspose.Pdf tvar tichounce ořízne, což může být při ladění matoucí.  
- **Poznámka o výkonu:** Přidání tisíců obdélníků je v pořádku, ale pokud generujete velké zprávy, zvažte seskupení tvarů do jediného objektu `Graphics`, abyste snížili režii.

## Vizualizační odkaz

Níže je rychlý snímek vygenerovaného PDF (obdélník je zvýrazněn světle šedě). Alt text obsahuje hlavní klíčové slovo pro SEO.

![jak nakreslit obdélník v PDF příklad](https://example.com/images/rectangle-demo.png "jak nakreslit obdélník v PDF příklad")

## Závěr

Probrali jsme **jak nakreslit obdélník** v PDF pomocí Aspose.Pdf pro C#. Vytvořením `Document`, přidáním `Page`, definováním tvaru `Rectangle` a nakonec **přidáním tvaru do PDF** můžete generovat vektorovou grafiku pouhými několika řádky kódu. Ať už potřebujete **přidat obdélník do pdf** pro zvýraznění, ladění rozvržení nebo UI překrytí, tento přístup se dobře škáluje.

Dále můžete zkoumat **kreslení tvarů v pdf** nad rámec obdélníků – například kruhy, polyliny nebo vlastní SVG cesty. Nebo se ponořit do renderování textu, vkládání obrázků a manipulace s PDF formuláři, abyste vytvořili plnohodnotné zprávy. Knihovna Aspose.Pdf nabízí bohaté API a s těmito základy jste připraveni experimentovat.

Šťastné programování a ať vaše PDF vždy vypadají přesně tak, jak si představujete!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}