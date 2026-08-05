---
category: general
date: 2026-08-04
description: Přidejte obdélník do PDF pomocí C#. Naučte se, jak v PDF v C# nakreslit
  tvar s Aspose.Pdf v jasném, kompletním příkladu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: cs
lastmod: 2026-08-04
og_description: Přidejte obdélník do PDF pomocí C#. Tento tutoriál ukazuje, jak rychle
  a spolehlivě nakreslit tvar v PDF pomocí C#.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Přidejte obdélník do PDF pomocí C# – kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Přidání obdélníku do PDF pomocí C# – krok za krokem
url: /cs/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání obdélníku do PDF pomocí C# – krok za krokem průvodce

Pokud potřebujete **přidat obdélník do PDF** souborů z aplikace v C#, tento průvodce vám přesně ukáže, jak to provést. Uvidíte kompletní, spustitelný příklad, který kreslí tvar v PDF pomocí C# s knihovnou Aspose.Pdf, a pochopíte, proč je každý řádek kódu důležitý.

Kreslení tvarů v PDF je běžnou požadavkem pro generátory reportů, šablony faktur a vlastní brandování dokumentů. Na konci tohoto tutoriálu budete umět vložit libovolnou obdélníkovou anotaci, změnit její velikost, barvu nebo pozici a uložit upravený dokument bez ztráty existujícího obsahu.

**Co se naučíte**

* Jak načíst existující PDF pomocí Aspose.Pdf.
* Jak definovat hranice obdélníku a vytvořit tvar obdélníku.
* Jak přidat obdélník do kolekce odstavců stránky.
* Jak uložit aktualizované PDF a ověřit výsledek.
* Variace pro více stránek, průhlednost a vlastní styly čar.

**Požadavky**

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+).
* Visual Studio 2022 nebo jakékoli C# IDE.
* Odkaz na NuGet balíček `Aspose.Pdf` (bezplatná zkušební verze nebo licencovaná verze).
* Vstupní PDF soubor pojmenovaný `input.pdf` umístěný ve složce, kterou ovládáte.

---

## Jak kreslit tvar v PDF pomocí C# – nastavení projektu

1. **Vytvořte nový konzolový projekt**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Přidejte balíček Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Umístěte `input.pdf`** do adresáře projektu (nebo do jakékoli složky, na kterou později odkazujete).

Projekt je nyní připraven k překladu kódu, který **přidá obdélník do PDF** souborů.

## Krok 1: Načtení PDF dokumentu

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*`Document` třída parsuje soubor a zpřístupňuje kolekci `Pages`. Načtení je první požadovaná operace před jakýmkoli kreslením.*

## Krok 2: Výběr cílové stránky

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Pokud potřebujete přidat obdélník na jinou stránku, nahraďte index požadovaným číslem stránky. Knihovna vyhodí výjimku, pokud je index mimo rozsah, takže se ujistěte, že PDF obsahuje dostatek stránek.*

## Krok 3: Definování hranic obdélníku

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Souřadnicový systém používá body (1 pt = 1/72 palce). Příklad vytváří obdélník široký 250 pt a vysoký 100 pt poblíž horní části stránky. Upravením čísel přizpůsobte rozvržení.*

## Krok 4: Vytvoření tvaru obdélníku

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*`Rectangle` třída dědí z `GraphicalObject`. Nastavení `FillColor` a `Border` je volitelné, ale ukazuje, jak ovládat vzhled, když **how to draw shape in PDF C#** přesahuje jednoduchý obrys.*

## Krok 5: Přidání obdélníku na stránku

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Odstavce jsou kontejnerem pro jakýkoli kreslitelný objekt. Vložením tvaru do `Paragraphs` Aspose.Pdf jej vykreslí při uložení dokumentu.*

## Krok 6: Uložení upraveného PDF

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Uložení vytvoří nový soubor, takže původní `input.pdf` zůstane nezměněn. Můžete přepsat zdrojový soubor předáním stejné cesty, ale uchování zálohy je osvědčená praxe.*

## Kompletní zdrojový kód (spustitelný)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Očekávaný výstup** – Otevřete `output.pdf` v libovolném prohlížeči PDF. Měli byste vidět modře vyplněný obdélník poblíž pravého horního rohu první stránky, ohraničený tmavě šedým okrajem.

## Jak kreslit tvar v PDF C# na více stránkách

Pokud potřebujete **přidat obdélník do PDF** na každou stránku, projděte kolekci `Pages` pomocí smyčky:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Tento vzor znovu používá stejné hranice na každé stránce. Pokud potřebujete různé pozice, upravte souřadnice pro každou stránku.*

## Časté úskalí a tipy na osvědčené postupy

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| Obdélník se zobrazuje mimo stránku | Souřadnice se měří od levého dolního rohu; použití souřadnicového systému orientovaného nahoru může způsobit záměnu. | Pamatujte, že osa Y roste směrem nahoru. Používejte hodnoty, které se vejdou do velikosti stránky (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Tvar je neviditelný | Průhlednost výplně je nastavena na `0` nebo šířka okraje na `0`. | Zajistěte, aby `FillOpacity` byla větší než `0` a `Border.Width` alespoň `0.5`. |
| Uložení vyvolá `AccessDeniedException` | Výstupní soubor je otevřen v jiném programu. | Zavřete všechny prohlížeče před spuštěním kódu, nebo uložte do jiné cesty. |
| Obdélník překrývá existující obsah | Nebyla nastavena kontrola vrstvení. | Použijte vlastnost `ZIndex` (vyšší hodnoty se vykreslí nahoře), pokud potřebujete řídit vrstvení. |

## Rozšíření obdélníku – gradienty, rotace a průhlednost

Aspose.Pdf podporuje pokročilou grafiku. Pro vytvoření otočeného obdélníku s lineárním gradientem:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Stejný vzor kódu ukazuje **how to draw shape in PDF C#** s bohatšími vizuálními efekty.*

## Ověření výsledku programově

Můžete potvrdit, že byl obdélník přidán, kontrolou počtu odstavců na stránce:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Pokud se počet zvýšil o jednu po vložení, operace byla úspěšná.

## Závěr

Nyní víte, jak **přidat obdélník do PDF** souborů pomocí C#. Tutoriál pokryl načítání dokumentu, definování hranic, vytvoření tvaru obdélníku, vložení do stránky a uložení výsledku. Také jste viděli, jak pracovat s více stránkami, vyhnout se běžným chybám a použít pokročilé stylování.

Dále prozkoumejte související témata, jako je **how to draw shape in PDF C#** pro kruhy, mnohoúhelníky nebo volné cesty, a naučte se kombinovat tvary s textem a obrázky pro tvorbu plně vybavených PDF reportů.

Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak přidat razítka stránek do PDF pomocí Aspose.PDF pro .NET \| Průvodce vodoznaky a pozadí](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [Jak přidat obrázkové razítko do PDF pomocí Aspose.PDF pro .NET: Kompletní průvodce](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Jak přidat otáčející se obrázkový vodoznak do PDF pomocí Aspose.PDF pro .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}