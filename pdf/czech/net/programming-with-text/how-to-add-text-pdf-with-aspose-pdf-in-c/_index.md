---
category: general
date: 2026-09-27
description: Jak přidat text do PDF pomocí Aspose.PDF a umístit text na stránky PDF.
  Postupujte podle tohoto krok‑za‑krokem průvodce, abyste efektivně vložili text na
  stránku PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add text pdf
- position text in pdf
- insert text pdf page
- aspose pdf add text
- access specific pdf page
language: cs
lastmod: 2026-09-27
og_description: Jak přidat text do PDF pomocí Aspose.PDF. Naučte se umístit text v
  PDF, vložit text na stránku PDF a přistupovat ke konkrétní stránce PDF s jasnými
  ukázkami kódu.
og_image_alt: Screenshot showing how to add text PDF with Aspose.PDF in C#
og_title: Jak přidat text do PDF pomocí Aspose.PDF – kompletní průvodce v C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to add text PDF using Aspose.PDF and position text in PDF pages.
    Follow this step‑by‑step guide to insert text PDF page efficiently.
  headline: How to add text PDF with Aspose.PDF in C#
  type: TechArticle
- description: How to add text PDF using Aspose.PDF and position text in PDF pages.
    Follow this step‑by‑step guide to insert text PDF page efficiently.
  name: How to add text PDF with Aspose.PDF in C#
  steps:
  - name: Load the PDF document
    text: '```csharp // Step 1: Load the PDF document var document = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf");
      ```'
  - name: Access the specific PDF page
    text: '```csharp // Step 2: Access the second page (index starts at 1) var page
      = document.Pages[1]; ```'
  - name: Position text in PDF
    text: '```csharp // Step 3: Create a tagged content element positioned at (100,
      200) on the page var taggedContent = new Aspose.Pdf.TaggedContent(page) { X
      = 100, Y = 200 }; ```'
  - name: Insert text PDF page
    text: '```csharp // Step 4: Add a text fragment to the tagged content taggedContent.Add(new
      Aspose.Pdf.Text.TextFragment("Important")); ```'
  - name: Save the modified PDF
    text: '```csharp // Step 5: Save the modified PDF document.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Expected output
    text: 'When you open `output.pdf`:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Jak přidat text do PDF pomocí Aspose.PDF v C#
url: /cs/net/programming-with-text/how-to-add-text-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat text do PDF pomocí Aspose.PDF v C#

Pokud potřebujete **jak přidat text do PDF** programově, tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.PDF pro .NET. Naučíte se umístit text v PDF, vložit text na stránku PDF a přistupovat ke konkrétní stránce PDF, aniž byste opustili své IDE.

Tutoriál pokrývá vše od instalace knihovny až po uložení finálního dokumentu, takže můžete kód zkopírovat a spustit okamžitě. Nejsou potřeba žádné externí odkazy – stačí kroky níže.

## Prerequisites

Než začnete, ujistěte se, že máte:

* .NET 6.0 (nebo novější) nainstalováno.
* Visual Studio 2022 nebo jakékoli IDE kompatibilní s C#.
* NuGet balíček Aspose.PDF pro .NET (`Aspose.Pdf`) přidaný do vašeho projektu.
* Zdrojový PDF soubor (`input.pdf`) umístěný v známém adresáři.

Tyto požadavky zajišťují, že kód se zkompiluje a manipulace s PDF funguje podle očekávání.

## Jak přidat text do PDF pomocí Aspose.PDF

Následující sekce rozdělují proces na jednotlivé, snadno sledovatelné kroky. Každý krok vysvětluje **proč** je důležitý, nejen **co** napsat.

### Krok 1: Načtení PDF dokumentu

```csharp
// Step 1: Load the PDF document
var document = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf");
```

**Proč je to důležité:** Načtení dokumentu vytvoří v‑paměti reprezentaci, kterou může Aspose.PDF upravovat. Bez tohoto objektu nemůžete přistupovat ke stránkám ani přidávat obsah.

### Krok 2: Přístup ke konkrétní stránce PDF

```csharp
// Step 2: Access the second page (index starts at 1)
var page = document.Pages[1];
```

**Proč je to důležité:** Stránky PDF jsou v Aspose.PDF číslovány od 1, takže `Pages[1]` vrací druhou stránku. Použití správného indexu je zásadní, když potřebujete **přistupovat ke konkrétní stránce PDF** pro úpravy.

### Krok 3: Umístění textu v PDF

```csharp
// Step 3: Create a tagged content element positioned at (100, 200) on the page
var taggedContent = new Aspose.Pdf.TaggedContent(page) { X = 100, Y = 200 };
```

**Proč je to důležité:** Vlastnosti `X` a `Y` definují levý dolní roh textu v bodech (1 pt ≈ 1/72 in). Úpravou těchto hodnot můžete **umístit text v PDF** přesně tam, kde chcete.

### Krok 4: Vložení textu na stránku PDF

```csharp
// Step 4: Add a text fragment to the tagged content
taggedContent.Add(new Aspose.Pdf.Text.TextFragment("Important"));
```

**Proč je to důležité:** `TextFragment` představuje řetězec znaků. Přidáním do elementu `TaggedContent` skutečně **vloží text na stránku PDF** na souřadnice nastavené v předchozím kroku.

### Krok 5: Uložení upraveného PDF

```csharp
// Step 5: Save the modified PDF
document.Save("YOUR_DIRECTORY/output.pdf");
```

**Proč je to důležité:** Uložení změn zapíše nový PDF soubor na disk. Výstupní soubor nyní obsahuje slovo „Important“ na druhé stránce na přesně určeném místě.

## Kompletní, spustitelný příklad

Níže je celý program, který můžete zkopírovat a vložit do konzolové aplikace. Obsahuje všechny potřebné `using` direktivy a komentáře pro přehlednost.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace PdfTextAdder
{
    class Program
    {
        static void Main()
        {
            // Load the existing PDF
            var document = new Document("YOUR_DIRECTORY/input.pdf");

            // Access the second page (index starts at 1)
            var page = document.Pages[1];

            // Create a tagged content element at (100, 200)
            var taggedContent = new TaggedContent(page) { X = 100, Y = 200 };

            // Add the text fragment "Important"
            taggedContent.Add(new TextFragment("Important"));

            // Save the result
            document.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("Text added successfully. Check output.pdf.");
        }
    }
}
```

### Očekávaný výstup

Po otevření `output.pdf`:

* Druhá stránka obsahuje slovo **Important** umístěné 100 pt od levého okraje a 200 pt od spodního okraje.
* Všechny ostatní stránky zůstávají beze změny.

Pokud souřadnice umístí text mimo okraje stránky, text bude oříznut. Upravit `X` a `Y` podle potřeby.

## Běžné varianty a okrajové případy

| Situace | Jak řešit |
|-----------|---------------|
| **Různé číslo stránky** | Změňte `document.Pages[1]` na požadovaný index číslovaný od 1. |
| **Více textových fragmentů** | Zavolejte `taggedContent.Add(new TextFragment("First"));` a následně další volání `Add`. |
| **Změna stylu písma** | Vytvořte `TextFragment`, nastavte jeho `TextState.Font` a `TextState.FontSize`, poté jej přidejte do `taggedContent`. |
| **Otočený text** | Nastavte `taggedContent.Rotation = 90;` před přidáním fragmentu. |
| **Velké PDF soubory** | Načtěte dokument s `Document.LoadOptions`, abyste umožnili paměťově efektivní streamování. |

Tyto varianty vám umožní rozšířit základní **aspose pdf add text** vzor tak, aby vyhovoval složitějším požadavkům.

## Profesionální tipy

* **Soustava souřadnic:** PDF používá počátek v levém dolním rohu. Pokud jste zvyklí na souřadnice v levém horním rohu (např. v HTML), odečtěte hodnotu Y od výšky stránky.
* **Výkon:** Při zpracování mnoha stránek znovu použijte jedinou instanci `Document`, abyste se vyhnuli opakovanému I/O souborů.
* **Bezpečnost:** Vždy pracujte s kopií původního PDF, abyste zachovali zdrojový soubor.

## Závěr

Nyní víte **jak přidat text do PDF** pomocí Aspose.PDF, **jak umístit text v PDF**, **jak vložit text na stránku PDF** a **jak přistupovat ke konkrétní stránce PDF**. Dodržením výše uvedených kroků můžete programově vložit libovolný řetězec na libovolné místo v PDF dokumentu.

Jste připraveni objevovat dál? Zkuste přidat obrázky, kreslit tvary nebo vytvářet tabulky s Aspose.PDF. Každé z těchto témat staví na stejných principech, které jste právě zvládli.

---

![jak přidat text PDF příklad](image.png)


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak přidat textový razítko do PDF pomocí Aspose.PDF .NET: komplexní průvodce](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Jak otočit text v PDF pomocí Aspose.PDF pro .NET: krok za krokem průvodce](/pdf/english/net/text-operations/rotate-text-aspose-pdf-net-guide/)
- [Přidávat, upravovat a extrahovat text pomocí Aspose.PDF pro .NET](/pdf/english/net/programming-with-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}