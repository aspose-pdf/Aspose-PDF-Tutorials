---
category: general
date: 2026-10-10
description: Naučte se, jak přidat obdélník do PDF, nakreslit tvar v PDF a uložit
  upravené PDF pomocí Aspose.PDF. Zahrnuje krok‑za‑krokem průvodce pro přístup ke
  konkrétní stránce PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: cs
lastmod: 2026-10-10
og_description: Přidejte obdélník do PDF pomocí Aspose.PDF v C#. Tento tutoriál ukazuje,
  jak nakreslit tvar do PDF, přistupovat ke konkrétní stránce PDF a uložit upravený
  PDF.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Přidejte obdélník do PDF pomocí Aspose.PDF – kompletní průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Jak přidat obdélník do PDF pomocí Aspose.PDF v C#
url: /cs/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat obdélník do PDF pomocí Aspose.PDF v C#

Pokud potřebujete **přidat obdélník do PDF** souborů programově, tento návod vám přesně ukáže, jak na to. Naučíte se **kreslit tvar v PDF**, zaměřit se na konkrétní stránku a **uložit upravené PDF** bez chyb.

Práce s PDF dokumenty je běžná potřeba pro reportování, fakturaci nebo anotaci dokumentů. Na konci tohoto tutoriálu budete sebejistě **přidávat tvar do PDF** souborů, zvládat chyby mimo rozsah a integrovat řešení do jakéhokoli .NET projektu.

## Požadavky

* .NET 6.0 SDK nebo novější nainstalovaný  
* Visual Studio 2022 (nebo jakékoli C# IDE)  
* Licence Aspose.PDF pro .NET nebo bezplatný evaluační klíč – API funguje stejným způsobem v obou režimech  
* PDF soubor pojmenovaný `input.pdf` umístěný ve složce, na kterou můžete odkazovat z kódu  

Tyto položky jsou jedinými externími závislostmi pro příklad.

## Krok 1: Instalace NuGet balíčku Aspose.PDF

Knihovna Aspose.PDF poskytuje třídy `Document`, `Rectangle` a další kreslicí třídy, které potřebujete.

```bash
dotnet add package Aspose.PDF
```

Spuštěním tohoto příkazu přidáte nejnovější stabilní verzi Aspose.PDF do svého projektu, čímž zpřístupníte třídy PDF pro kompilaci.

## Krok 2: Načtení PDF dokumentu

Prvním krokem je načíst zdrojový soubor. Tím se vytvoří paměťová reprezentace, kterou můžete upravovat.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Proč je to důležité*: Načtení dokumentu vám poskytuje přístup k jeho kolekci stránek, což je později potřeba pro **přístup ke konkrétní PDF stránce**.

## Krok 3: Přístup ke druhé stránce (index od nuly)

Stránky PDF jsou indexovány od `0`. Pro umístění obdélníku na druhou stránku načtěte stránku s indexem `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Pokud má dokument méně než dvě stránky, bude vyhozena výjimka `ArgumentOutOfRangeException`, která vás upozorní na potřebu kontrolního výrazu v produkčním kódu.

## Krok 4: Vytvoření tvaru obdélníku

Definujte pozici a velikost obdélníku pomocí struktury `Rectangle` a poté jej zabalte do kreslicího objektu Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Proč je to důležité*: Vlastnosti `BorderInfo` a `FillColor` vám umožňují **kreslit tvar v PDF** s viditelným obrysem a volitelným výplní, což způsobí, že obdélník bude pro čtenáře výrazný.

## Krok 5: Přidání obdélníku do kolekce odstavců stránky

Aspose.PDF zachází s kreslicími objekty jako s prvky odstavců. Přidáním obdélníku do kolekce `Paragraphs` stránky jej vykreslí na stránce.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

V tomto okamžiku PDF dokument v paměti obsahuje nový tvar, ale soubor na disku zůstane nezměněn, dokud jej neuložíte.

## Krok 6: Uložení upraveného PDF a ošetření chyb mimo rozsah

Voláním `Save` zapíšete aktualizovaný dokument do nového souboru. Pokud obdélník přesáhne rozměry stránky, Aspose vyhodí `PdfException`. Zachycením této výjimky můžete problém čistě nahlásit.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Proč je to důležité*: Blok `try/catch` zajišťuje, že vaše aplikace **uloží upravené PDF** bezpečně, a chybová zpráva vám pomůže upravit souřadnice obdélníku, pokud bude potřeba.

## Kompletní funkční příklad

Spojením všech kroků dohromady získáte kompletní, připravený k spuštění program:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Očekávaný výstup

Spuštěním programu se vypíše:

```
PDF saved successfully with rectangle added.
```

a vytvoří `output.pdf`, který zobrazuje původní obsah plus modrý obdélník na zadaných souřadnicích na druhé stránce.

Pokud by byl obdélník větší než stránka, uvidíte:

```
Shape out of bounds: The shape exceeds page margins.
```

## Časté otázky a okrajové případy

### Co když má PDF jen jednu stránku?

Pokus o přístup k `pdfDocument.Pages[1]` vyvolá `ArgumentOutOfRangeException`. Ochráníte se tím, že před indexací zkontrolujete `pdfDocument.Pages.Count`.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Jak přidat více obdélníků na různé stránky?

Opakujte kroky 2‑4 pro každou cílovou stránku a podle potřeby upravte souřadnice obdélníku. Logiku můžete umístit do smyčky, která iteruje přes `pdfDocument.Pages`.

### Mohu použít jiné tvary, jako jsou kruhy nebo mnohoúhelníky?

Ano. Aspose.PDF poskytuje třídy `Ellipse`, `Polygon` a `Polyline`, které fungují podle stejného vzoru jako `Rectangle`. Nahraďte volání `new Aspose.Pdf.Drawing.Rectangle` požadovanou třídou tvaru.

### Podporuje knihovna PDF s otočenými stránkami?

Aspose.PDF automaticky respektuje otočení stránky při vykreslování tvarů. Souřadnice obdélníku jsou interpretovány v nativním souřadnicovém systému stránky, takže není potřeba žádná další transformace.

## Úvahy o výkonu

* **Spotřeba paměti** – Načtení velkého PDF (stovky megabajtů) spotřebuje úměrnou paměť. Pokud potřebujete upravit jen jednu stránku, zvažte použití `PdfFileInfo` k extrakci této stránky, úpravě a následnému sloučení zpět.  
* **Dávkové zpracování** – Při přidávání tvarů do mnoha dokumentů znovu použijte jedinou instanci `License`, abyste se vyhnuli opakovanému zatížení validací licence.

## Další kroky

Nyní, když můžete **přidat obdélník do PDF**, prozkoumejte tato související témata:

* **draw shape on PDF** – naučte se překrývat text, obrázky a vodoznaky  
* **add shape to PDF** – kombinujte více tvarů do jedné vrstvy anotací  
* **save modified PDF** – použijte streamy (`MemoryStream`) k přímému vracení PDF z webových API  
* **access specific PDF page** – implementujte extrakci rozsahu stránek pro vlastní reporty  

Experimentujte s různými barvami, styly čar a úrovněmi průhlednosti, aby odpovídaly vašim brandovým směrnicím.

---

*Šťastné kódování! Pokud vám tento tutoriál pomohl **přidat obdélník do PDF**, zvažte jeho sdílení s kolegy nebo přispění vylepšení zpět do komunity.*

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak přidat tvar do PDF s Aspose.PDF v C# – krok za krokem](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Jak přidat čáru do PDF pomocí Aspose.PDF pro .NET: krok za krokem](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Jak vytvořit PDF v C# – přidat stránku, nakreslit obdélník a uložit](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}