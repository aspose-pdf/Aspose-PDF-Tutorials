---
category: general
date: 2026-09-05
description: Vytvořte PDF dokument v C# přidáním prázdné stránky, nakreslením obdélníku
  a uložením PDF souboru. Postupujte podle příkladu Aspose.PDF krok za krokem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: cs
lastmod: 2026-09-05
og_description: Vytvořte PDF dokument v C# přidáním prázdné stránky, nakreslením obdélníku
  a uložením PDF souboru. Postupujte podle tohoto kompletního příkladu s Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Vytvořte PDF dokument s prázdnou stránkou a obdélníkem – průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Jak vytvořit PDF dokument s prázdnou stránkou a obdélníkem
url: /cs/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit PDF dokument s prázdnou stránkou a obdélníkem

Pokud potřebujete **vytvořit PDF dokument** programově, tento průvodce ukazuje kompletní řešení v C#. Naučíte se, jak přidat prázdnou stránku, nakreslit na ní obdélník a nakonec PDF soubor uložit. Příklad používá knihovnu Aspose.PDF, která funguje s .NET 6+ a .NET Framework 4.5+.

Přidání prázdné stránky a kreslení tvarů je běžná potřeba pro faktury, certifikáty nebo vlastní zprávy. Na konci tohoto tutoriálu budete mít spustitelný projekt, který vytvoří PDF obsahující jediný obdélník umístěný na (100, 100) s velikostí 200 × 200 bodů.

## Požadavky

* Visual Studio 2022 (nebo jakékoli C# IDE)
* .NET 6 SDK nebo .NET Framework 4.5+
* Aspose.PDF for .NET NuGet package  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Oprávnění k zápisu do výstupního adresáře

Žádná další konfigurace není vyžadována; kód funguje ihned po spuštění.

## Vytvoření PDF dokumentu – přehled

Celý proces se skládá ze čtyř logických kroků:

1. **Instantiate** objekt `Document` – představuje PDF soubor.
2. **Add a blank page** – stránka poskytuje plátno pro kreslení.
3. **Draw a rectangle** – objekt `Path` definuje tvar.
4. **Save the PDF file** – uloží dokument na disk.

Každý krok je oddělen ve své vlastní sekci, takže jej můžete podle potřeby znovu použít nebo nahradit.

![Diagram PDF s obdélníkem na prázdné stránce](https://example.com/placeholder-image.png){.img-fluid alt="Snímek obrazovky ukazující PDF dokument s nakresleným obdélníkem na prázdné stránce"}

## Přidání prázdné stránky PDF

PDF musí obsahovat alespoň jednu stránku, než lze umístit jakoukoli grafiku. Metoda `Pages.Add()` vytvoří prázdnou stránku s výchozími rozměry (A4). Pokud potřebujete jinou velikost, předávejte argument `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Why this step matters* – Objekt stránky obsahuje kolekce pro text, obrázky a vektorovou grafiku. Bez stránky by jakýkoli pokus o přidání obdélníku vyvolal výjimku.

### Okrajový případ: vlastní velikost stránky

Pokud vaše rozvržení vyžaduje stránku 6 × 9 palců, nahraďte výchozí volání tímto:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Nakreslení obdélníku PDF

Kreslení obdélníku spočívá ve vytvoření geometrie `Rectangle` a jejím zabalení do `Path`. Volání `ValidateBounds()` zajišťuje, že tvar se vejde do okrajů stránky, čímž se zabrání oříznutí.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Why this step matters* – Objekt `Path` je nízkoúrovňová vektorová primitiva používaná v Aspose.PDF. Validací ohraničení se vyhnete chybám za běhu, když obdélník překročí limity stránky.

### Profesionální tip: stylování obdélníku

Můžete změnit barvu obrysu a šířku čáry:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Tím získáte červený obrys o tloušťce 2 body.

## Uložení PDF souboru

Uložení dokumentu dokončuje soubor na disku. Metoda `Save` přijímá cestu k souboru nebo stream. Poskytnutí absolutní cesty činí umístění explicitní, což je užitečné pro automatizační skripty.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Why this step matters* – Ukládání je jediný okamžik, kdy se reprezentace v paměti stane fyzickým souborem. Pokud potřebujete vrátit PDF z webového API, nahraďte cestu k souboru `MemoryStream`.

### Okrajový případ: přepisování existujících souborů

Aspose.PDF ve výchozím nastavení přepíše existující soubor. Pro ochranu předchozích výstupů nejprve zkontrolujte, zda soubor existuje:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Jak přidat obdélník – osvědčené postupy

* **Keep coordinates within the page margins** – použijte `ValidateBounds()` nebo vypočítejte okraje ručně.
* **Reuse `GraphInfo` objects** při kreslení více tvarů; snižuje to alokaci paměti.
* **Dispose of the `Document` object** (jak je ukázáno s `using var`) pro rychlé uvolnění nativních zdrojů.
* **Test with different DPI settings** pokud později vkládáte rastrové obrázky; vektorové tvary jako obdélníky zůstávají ostré při jakémkoli rozlišení.

## Kompletní funkční příklad

Níže je celý program, který můžete zkopírovat do konzolové aplikace. Překompiluje se bez úprav a vytvoří `output.pdf` ve složce projektu.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Očekávaný výstup

Spuštěním programu se vytvoří jednosloučkový PDF. Když otevřete `output.pdf`, uvidíte prázdnou bílou stránku s červeným obdélníkem umístěným 100 bodů od levého a spodního okraje, o rozměrech 200 × 200 bodů.

## Závěr

Nyní víte, jak **vytvořit PDF dokument**, **přidat prázdnou stránku PDF**, **nakreslit obdélník PDF** a **uložit PDF soubor** pomocí Aspose.PDF v C#. Příklad pokrývá základní volání API, vysvětluje, proč je každé volání potřeba, a poskytuje tipy pro běžné varianty, jako jsou vlastní velikosti stránek nebo stylování obdélníku.

Dále prozkoumejte související témata, jako je **přidávání textu**, **vkládání obrázků** nebo **vytváření vícestránkových zpráv**. Stejný vzor – vytvořit `Document`, manipulovat se stránkami, přidat vektorový nebo rastrový obsah a poté `Save` – platí pro všechny tyto scénáře. Klidně experimentujte s různými tvary, barvami a rozvržením stránek, aby vyhovovaly potřebám vašeho projektu.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit PDF dokument C# – Přidat stránku, nakreslit obdélník a uložit](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Vytvořit PDF dokument s Aspose.PDF – Průvodce krok za krokem](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Vytvořit PDF dokument s Aspose – Přidat stránku, textové pole a formulář](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}