---
category: general
date: 2026-05-27
description: Přidejte Batesovo číslování do PDF pomocí Aspose.Pdf v C#. Naučte se,
  jak rychle přidat Batesovo číslování, přizpůsobit formát a automatizovat označování
  právních dokumentů.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: cs
og_description: Přidání Bates číslování PDF s Aspose.Pdf v C#. Tento průvodce ukazuje,
  jak přidat Bates číslování, nastavit předpony a uložit výsledek.
og_title: Přidejte Batesovo číslování PDF v C# – krok za krokem tutoriál
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Přidání Batesova číslování do PDF v C# – Kompletní průvodce
url: /cs/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Batesova číslování PDF v C# – Kompletní průvodce

Chtěli jste někdy **jak přidat Batesovo číslování** do PDF, aniž byste strávili hodiny manipulací s ručními nástroji? Nejste sami – právní týmy, auditoři a specialisté na e‑discovery všichni potřebují spolehlivý způsob, jak **programově přidat Batesovo číslování PDF** souborům.

V tomto tutoriálu projdeme stručné, kompletní řešení pomocí Aspose.Pdf pro .NET, takže můžete přidat Batesova čísla do libovolného dokumentu pomocí několika řádků C# kódu.

## Co se naučíte

- Jak otevřít existující PDF pomocí Aspose.Pdf  
- Jak vytvořit artefakt Batesova číslování a doladit jeho formát  
- Jak připojit artefakt ke každé stránce (nebo jen k první)  
- Jak uložit aktualizovaný soubor a ověřit výsledek  

Žádná předchozí zkušenost s Aspose není vyžadována – stačí základní znalost C# a .NET. Na konci budete mít znovupoužitelný úryvek, který můžete zkopírovat a vložit do jakéhokoli projektu.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+)
- NuGet balíček Aspose.Pdf pro .NET (`Install-Package Aspose.Pdf`)
- Zdrojový PDF soubor, který chcete označit (umístěte jej do složky, na kterou můžete odkazovat)

> **Pro tip:** Pokud ještě nemáte licenci, Aspose nabízí zdarma dočasný klíč, který odstraňuje vodotisky z hodnocení.

## Krok 1 – Otevření zdrojového PDF dokumentu  

Nejprve potřebujeme objekt `Document`, který představuje soubor na disku. Představte si to jako načtení prázdného plátna, na které později namalujeme Batesova čísla.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Proč je to důležité:** Otevření dokumentu uvnitř bloku `using` zajišťuje, že všechny neřízené prostředky jsou rychle uvolněny, což je zvláště důležité u velkých PDF.

## Krok 2 – Vytvoření artefaktu Batesova číslování  

*BatesNumberingArtifact* je způsob, jakým Aspose popisuje vzhled čísel. Můžete nastavit předponu, počáteční číslo, přírůstek a dokonce vlastní formátovací řetězec.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Proč byste mohli tyto hodnoty změnit:**  
- **Prefix** je užitečný pro ID případů (“CASE‑”, “DOC‑”).  
- **StartNumber** vám umožní pokračovat v předchozí sérii.  
- **Increment** lze nastavit na 2, pokud potřebujete liché/sudé číslování.  
- **Format** podporuje libovolný .NET kompozitní formát; `{0:D5}` zaručuje pět číslic s úvodními nulami.

## Krok 3 – Připojení artefaktu k požadovaným stránkám  

Můžete přidat artefakt na jednu stránku, rozsah nebo celý dokument. Pro většinu právních pracovních postupů jej připojujeme ke *každé* stránce, ale níže uvedený příklad ukazuje minimální případ – přidání na první stránku.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Pokud potřebujete pokrýt všechny stránky, projděte je v cyklu:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Proč je tento krok zásadní:** Artefakty jsou vykresleny *po* obsahu stránky, takže čísla se zobrazí nad existujícím textem, aniž by se změnil původní rozvržení.

## Krok 4 – Uložení upraveného PDF  

Na závěr zapíšete změny zpět na disk. Můžete přepsat originál nebo vytvořit nový soubor – zde vytvoříme čerstvou kopii s názvem `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Když otevřete `bates.pdf`, uvidíte v defaultní pozici (obvykle v pravém dolním rohu) otisk “ABC01000” (nebo jakýkoli formát, který jste zvolili).

## Kompletní funkční příklad  

Spojením všeho dohromady zde máte kompletní program, který můžete zkompilovat a spustit:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Očekávaný výstup

Když spustíte program, konzole vypíše:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Otevřením `bates.pdf` se zobrazí předpona “ABC” následovaná nulami doplněnou pětimístnou sekvencí na každé stránce – přesně to, co kód požadoval.

## Časté otázky a okrajové případy

### Můžu umístit Batesovo číslo jinde?

Ano. Použijte vlastnost `Location` u `BatesNumberingArtifact` (např. `Location = new Position(10, 10)`) k umístění čísla na vlastní X/Y souřadnice. Můžete také nastavit `HorizontalAlignment` a `VerticalAlignment` pro větší kontrolu.

### Co když má moje PDF tisíce stránek?

Aspose.Pdf efektivně streamuje stránky, ale je stále dobré zpracovávat je po dávkách, pokud narazíte na limity paměti. Třída `Document` také podporuje `PdfConverter` pro inkrementální ukládání.

### Jak změním písmo nebo barvu?

Zabalte artefakt do objektu `TextState`:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Potřebuji licenci pro produkční použití?

Licencovaná verze odstraňuje vodotisky z hodnocení a odemyká plný výkon. Bezplatná zkušební verze funguje dobře pro testování a proof‑of‑concepty.

## Ověření – Rychlá vizuální kontrola  

Pokud dáváte přednost automatizovanému ověření, Aspose může extrahovat text stránky a potvrdit přítomnost předpony:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Spuštěním po kroku uložení se vypíše `Bates number verified.`, pokud vše proběhlo hladce.

## Závěr  

Nyní víte **jak přidat Batesovo číslování PDF** souborům pomocí Aspose.Pdf v C#. Od otevření dokumentu po konfiguraci artefaktu, jeho připojení ke stránkám a uložení výsledku, je proces jednoduchý a plně skriptovatelný.

Další kroky? Zkuste experimentovat s:

- Různými hodnotami `Prefix` pro více případových šarží  
- Vlastním `Location` a `TextState` pro branding  
- Přidáním specifických předpon pro stránky (např. “VOL‑1‑”, “VOL‑2‑”) úpravou `StartNumber` v každé iteraci smyčky  

Tyto úpravy vám umožní přizpůsobit řešení téměř jakémukoli právnímu nebo archivnímu workflowu.

Máte další otázky ohledně **jak přidat Batesovo číslování** pro vícejazyčná PDF nebo šifrované soubory? Zanechte komentář níže a šťastné programování!

## Související tutoriály

- [Jak přidat a přizpůsobit číslování stránek v PDF pomocí Aspose.PDF pro .NET | Průvodce manipulací s dokumenty](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Jak přidat různé záhlaví v PDF pomocí Aspose.PDF pro .NET: krok za krokem](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [Jak přidat textový razítkový zápatí v PDF pomocí Aspose.PDF pro .NET: krok za krokem](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}