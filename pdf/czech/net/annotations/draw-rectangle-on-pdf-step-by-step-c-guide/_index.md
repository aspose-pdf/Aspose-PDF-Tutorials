---
category: general
date: 2026-08-14
description: Nakreslete obdélník do PDF rychle pomocí C#. Naučte se, jak definovat
  rozměry obdélníku a přidávat tvary na stránku PDF během několika řádků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: cs
lastmod: 2026-08-14
og_description: Nakreslete obdélník do PDF pomocí C# během několika sekund. Tento
  průvodce ukazuje, jak definovat rozměry obdélníku, přidat tvar a ověřit hranice
  stránky pro spolehlivou grafiku PDF.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: Nakreslete obdélník do PDF – kompletní C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Nakreslete obdélník v PDF – krok za krokem C# průvodce
url: /cs/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nakreslit obdélník do pdf – kompletní C# tutoriál

Pokud potřebujete **draw rectangle on pdf** pomocí C#, tento průvodce vám ukáže stručné, připravené pro produkci řešení. Uvidíte přesně **how to define rectangle dimensions**, ověříte, že tvar pasuje, a přidáte jej na stránku jedním voláním metody.

Tutoriál pokrývá vše od vytvoření PDF dokumentu až po vykreslení obdélníku, takže můžete kód zkopírovat‑vložit do svého projektu a okamžitě vidět výsledek. Žádná externí dokumentace není potřeba – stačí kroky níže.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
* NuGet balíček **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* Základní znalost syntaxe C#
* IDE, např. Visual Studio nebo VS Code

> **Pro tip:** Použijte bezplatnou evaluační licenci Aspose.PDF pro rychlé experimenty; přidá malou vodoznak, ale umožní vám otestovat všechny funkce.

## Jak nakreslit obdélník do PDF pomocí C#

Jádrem úkolu je vytvořit `RectangleShape`, nastavit jeho velikost a tah a připojit jej k `Page`. Následující nadpis H2 obsahuje primární klíčové slovo, čímž splňuje SEO požadavky.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Vysvětlení jednotlivých kroků

| Krok | Proč je důležitý |
|------|-------------------|
| **1️⃣ Create a new PDF document** | Inicializuje kontejner, který bude obsahovat stránky a grafiku. |
| **2️⃣ Add a blank page** | Potřebujete objekt `Page`, protože tvary se připojují k stránce, ne přímo k dokumentu. |
| **3️⃣ Define the rectangle bounds** | Zde se ukazuje **how to define rectangle dimensions**. Konstruktor `Rectangle` přijímá `x`, `y`, `width` a `height` v bodech (1 pt = 1/72 in). |
| **4️⃣ Create the rectangle shape** | `RectangleShape` je třída Aspose, která vykresluje obdélník. Nastavení `StrokeColor` určuje obrys; můžete také nastavit `FillColor` pro plnou výplň. |
| **5️⃣ Verify page boundaries** | `CheckShapeBoundary` vyvolá výjimku, pokud obdélník přesahuje velikost stránky, čímž zabrání poškozeným PDF. |
| **6️⃣ Add the shape to the page** | Tvar se stane součástí content streamu stránky. |
| **7️⃣ Save the PDF** | Uloží dokument do souboru, který můžete otevřít v libovolném PDF prohlížeči. |

Výsledný `RectangleDemo.pdf` obsahuje černý obdélník umístěný v levém horním rohu stránky, přesně 500 pt široký a 700 pt vysoký.

![nakreslit obdélník do pdf příklad](https://example.com/rectangle-demo.png "nakreslit obdélník do pdf příklad")

*Text alternativy obrázku: nakreslit obdélník do pdf příklad ukazující černý obdélník v levém horním rohu PDF stránky.*

## Jak definovat rozměry obdélníku pro různé velikosti stránek

Ukázka výše používá pevné hodnoty (`500 x 700`). Ve skutečných aplikacích často potřebujete, aby se obdélník přizpůsobil šířce a výšce stránky.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Klíčové body:**

* Použijte `page.PageInfo.Width` a `Height` pro načtení skutečné velikosti stránky.
* Násobení faktorem (např. `0.8f`) vám umožní vyjádřit rozměry jako procento stránky.
* Centrovaní se dosáhne odečtením velikosti obdélníku od velikosti stránky a vydělením zbytku dvěma.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč k tomu dochází | Řešení |
|---------|----------------------|--------|
| Obdélník přesahuje stránku | Pevně zakódované rozměry jsou větší než velikost stránky. | Zavolejte `page.CheckShapeBoundary` **před** přidáním tvaru; upravte rozměry, pokud je vyhozena výjimka. |
| Obrys není viditelný | `StrokeColor` zůstala na výchozí (`Color.Empty`). | Explicitně nastavte `StrokeColor` (např. `Color.Black`). |
| Obdélník se zobrazuje mimo obrazovku | Souřadnice v PDF začínají v levém dolním rohu; použití souřadnic typu „horní‑levý“ způsobí převrácení. | Pamatujte, že počátek `(0,0)` je levý dolní roh. Upravit `y` podle toho nebo použít `pageHeight - desiredY`. |
| Neočekávaná tloušťka čáry | Výchozí šířka čáry může být pro tisk příliš tenká. | Nastavte `rectangleShape.LineWidth = 2;` pro zvýšení tloušťky. |

## Rozšíření příkladu

Jakmile umíte **draw rectangle on pdf**, můžete snadno přidat i další tvary:

* **EllipseShape** – pro kruhy nebo elipsy.
* **PolygonShape** – pro vlastní mnohoúhelníky.
* **TextFragment** – pro popisky vašich obdélníků.

Všechny tvary používají stejný postup: definovat hranice, nakonfigurovat vzhled, ověřit hranice a poté přidat na stránku.

## Kompletní, spustitelný program

Níže je celý program, který kombinuje základní obdélník a příklad dynamického velikostního nastavení. Zkopírujte jej do nového konzolového projektu, obnovte NuGet balíček `Aspose.PDF` a spusťte.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Očekávaný výstup:**  
Otevřete `CombinedRectangles.pdf`. Uvidíte černý obdélník ukotvený v levém dolním rohu a centrovaný tmavě modrý obdélník s světle žlutou výplní. Oba obdélníky respektují okraje stránky.

## Závěr

Nyní víte, jak **draw rectangle on pdf** pomocí C# a přesně **how to define rectangle dimensions** pro pevné i responzivní rozvržení. Přístup využívá `RectangleShape` z Aspose.PDF, kontrolu hranic a jednoduchou aritmetiku pro přizpůsobení jakékoli velikosti stránky.

Dále můžete zkoumat:

* Přidání **výplňových barev** a **stylů čar** (čárkovaná, tečkovaná) – sekundární klíčové slovo: how to define rectangle dimensions with style.
* Kombinování více tvarů do jedné `Page` pro tvorbu grafů nebo formulářů.
* Export PDF do streamu pro webová API místo ukládání na disk.

Experimentujte s různými velikostmi, barvami a pozicemi, abyste zvládli PDF grafiku ve svých .NET aplikacích. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak přizpůsobit PDF pomocí Aspose.PDF pro .NET: nastavit okraje stránky a kreslit čáry](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Jak přidat razítka stránek do PDF pomocí Aspose.PDF pro .NET: kompletní průvodce](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Jak přidat číslování stránek do PDF pomocí Aspose.PDF pro .NET | Vodoznaky a pozadí](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}