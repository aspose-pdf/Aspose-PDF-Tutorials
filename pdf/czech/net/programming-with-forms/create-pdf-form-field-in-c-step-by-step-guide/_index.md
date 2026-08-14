---
category: general
date: 2026-08-14
description: Rychle vytvořte pole formuláře PDF pomocí C#. Naučte se, jak přidat textové
  pole do PDF a upravit PDF tak, aby obsahovalo textové pole pomocí Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf form field
- add text box to pdf
- modify pdf to include text box
- Aspose.PDF form field
- C# PDF manipulation
language: cs
lastmod: 2026-08-14
og_description: Vytvořte pole formuláře PDF pomocí C#. Tento tutoriál ukazuje, jak
  přidat textové pole do PDF a upravit PDF tak, aby obsahovalo textové pole pomocí
  Aspose.PDF.
og_image_alt: Screenshot of a PDF page showing a newly added text box form field
og_title: Vytvořte PDF formulářové pole v C# – kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  headline: Create pdf form field in C# – step‑by‑step guide
  type: TechArticle
- description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  name: Create pdf form field in C# – step‑by‑step guide
  steps:
  - name: Load the existing PDF document.
    text: Load the existing PDF document.
  - name: Instantiate a `TextBoxField` and configure its name and appearance.
    text: Instantiate a `TextBoxField` and configure its name and appearance.
  - name: Add a widget annotation that defines the visual rectangle on the target
      page.
    text: Add a widget annotation that defines the visual rectangle on the target
      page.
  - name: Insert the field into the document’s form collection.
    text: Insert the field into the document’s form collection.
  - name: Save the modified PDF.
    text: Save the modified PDF.
  - name: Open `output.pdf` in Adobe Acrobat Reader.
    text: Open `output.pdf` in Adobe Acrobat Reader.
  - name: Click inside the “Comments” box; the cursor should appear.
    text: Click inside the “Comments” box; the cursor should appear.
  - name: Type any text and press **Tab** or click elsewhere.
    text: Type any text and press **Tab** or click elsewhere.
  - name: Choose **File → Save As** to persist the entered value.
    text: Choose **File → Save As** to persist the entered value.
  - name: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
    text: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
  type: HowTo
tags:
- pdf
- csharp
- form-fields
title: Vytvořte PDF formulářové pole v C# – krok za krokem
url: /cs/net/programming-with-forms/create-pdf-form-field-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření pole formuláře PDF v C# – krok za krokem

Pokud potřebujete **vytvořit pole formuláře PDF** v dokumentu, tento průvodce vás provede celým procesem. Uvidíte přesně, jak **přidat textové pole do PDF** stránek a jak **upravit PDF tak, aby obsahovalo textové pole** pomocí knihovny Aspose.PDF pro .NET.

Práce s PDF formuláři je běžnou požadavkou pro fakturační systémy, průzkumy nebo jakýkoli workflow, který sbírá vstup od uživatele. Na konci tohoto tutoriálu budete mít znovupoužitelný úryvek kódu, který vytvoří plně funkční textové pole, umístí jej tam, kde chcete, a uloží aktualizované PDF – vše bez opuštění vašeho C# projektu.

## Požadavky

Než začnete, ujistěte se, že máte:

* .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.7+)
* Visual Studio 2022 nebo jakékoli IDE podporující C#
* Aktivní licenci Aspose.PDF pro .NET (bezplatná zkušební verze stačí pro vývoj)
* PDF soubor pojmenovaný `input.pdf` umístěný v známém adresáři (v tutoriálu je jako zástupce použito `YOUR_DIRECTORY`)

> **Tip:** Pokud ještě nemáte licenci, můžete si požádat o dočasný klíč na webu Aspose; knihovna funguje v evaluačním režimu bez úprav kódu.

## Jak vytvořit pole formuláře PDF v C# (přehled)

1. Načtěte existující PDF dokument.  
2. Vytvořte instanci `TextBoxField` a nastavte její název a vzhled.  
3. Přidejte widget anotaci, která určuje vizuální obdélník na cílové stránce.  
4. Vložte pole do kolekce formulářů dokumentu.  
5. Uložte upravené PDF.

Každý krok je podrobně vysvětlen níže, včetně kompletních ukázek kódu a odůvodnění volání API.

## Krok 1: Načtení PDF dokumentu

Prvním úkolem je načíst zdrojové PDF. Aspose.PDF představuje PDF soubor třídou `Document`. Načtení dokumentu vám poskytne přístup k jeho stránkám, kolekci formulářů a dalším strukturám.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

// Adjust the path to match your environment
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

// Load the PDF you want to modify
Document pdfDocument = new Document(inputPath);
```

**Proč je to důležité:**  
Načtení souboru vytvoří v‑paměťový model PDF, který vám umožní přidávat, odebírat nebo upravovat objekty, aniž byste poškodili původní soubor. Objekt `Document` také vystavuje vlastnost `Form`, kde později **přidáte textové pole do PDF**.

## Krok 2: Vytvoření textového pole

Textové pole je typ formulářového pole, který uživatelům umožňuje zadávat volný text. V Aspose.PDF jej vytvoříte instancí `TextBoxField`, přičemž předáte cílovou stránku a obdélník definující počáteční velikost widgetu.

```csharp
// Choose the page index (0‑based). Here we use page 2 (index 1).
Page targetPage = pdfDocument.Pages[1];

// Define the rectangle for the field’s *initial* size.
// Rectangle(left, bottom, right, top) – values are in points (1/72 inch).
Rectangle fieldRect = new Rectangle(100, 500, 200, 530);

// Create the TextBoxField with a partial name that will be used in form data.
TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
{
    PartialName = "Comments", // This identifier appears in the PDF form data.
    // Optional: set default appearance (font, size, color)
    DefaultAppearance = new DefaultAppearance(FontRepository.FindFont("Helvetica"), 12, Color.Black)
};
```

**Proč je to důležité:**  
* `PartialName` je klíč, který nástroje pro zpracování formulářů (např. Adobe Acrobat, server‑side parsers) používají k získání zadané hodnoty.  
* Obdélník, který zde předáte, určuje pouze *počáteční* velikost widgetu; jeho vizuální umístění můžete později upravit pomocí widget anotace (další krok).  
* Nastavení `DefaultAppearance` zajišťuje, že text uvnitř pole bude konzistentně vykreslen ve všech prohlížečích.

## Krok 3: Definování vizuální widget anotace

Formulářové pole může mít jednu nebo více **widget anotací**, které určují, kde se pole zobrazí na každé stránce. Přidáním widgetu můžete umístit stejné logické pole na jiné místo nebo dokonce na více stránek.

```csharp
// Define where the field will actually be displayed on the page.
// This rectangle can differ from the one used in the constructor.
Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
textBox.AddWidgetAnnotation(widgetRect);
```

**Proč je to důležité:**  
Widget obdélník určuje souřadnice na obrazovce, které uživatelé vidí. Pokud tento krok přeskočíte, pole může existovat ve struktuře PDF, ale nebude viditelné pro koncového uživatele. Přidání widgetu je krok, který skutečně **přidá textové pole do PDF**.

## Krok 4: Přidání nakonfigurovaného pole do formuláře dokumentu

Nyní, když je `TextBoxField` plně nastavený, musíte jej zaregistrovat v kolekci formulářů PDF. Tím se pole stane součástí interaktivního formuláře a zajistí se jeho uložení.

```csharp
pdfDocument.Form.Add(textBox);
```

**Proč je to důležité:**  
Bez přidání pole do `pdfDocument.Form` by PDF prohlížeč ignoroval widget anotaci a data pole by nikdy nebyla odeslána. Tento řádek finalizuje operaci **upravit PDF tak, aby obsahovalo textové pole**.

## Krok 5: Uložení aktualizovaného PDF

Nakonec zapíšete změny zpět na disk. Můžete přepsat původní soubor nebo vytvořit nový; v příkladu se ukládá do `output.pdf`.

```csharp
string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");

// Save the document with the new form field
pdfDocument.Save(outputPath);
```

Když otevřete `output.pdf` v Adobe Acrobat Reader, uvidíte obdélníkové textové pole označené „Comments“ na stránce 2. Uživatelé mohou kliknout dovnitř, psát a zadaný text bude součástí dat PDF formuláře.

## Kompletní funkční příklad

Když spojíme všechny části, získáme kompletní, připravený program. Zkopírujte jej do nového konzolového projektu, nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce a spusťte.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Drawing; // For Color

namespace PdfFormFieldDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the existing PDF
            string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
            Document pdfDocument = new Document(inputPath);

            // 2️⃣ Create a TextBoxField on page 2 (index 1)
            Page targetPage = pdfDocument.Pages[1];
            Rectangle fieldRect = new Rectangle(100, 500, 200, 530);
            TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
            {
                PartialName = "Comments",
                DefaultAppearance = new DefaultAppearance(
                    FontRepository.FindFont("Helvetica"), 12, Color.Black)
            };

            // 3️⃣ Add a widget annotation to control visual placement
            Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
            textBox.AddWidgetAnnotation(widgetRect);

            // 4️⃣ Register the field with the document's form collection
            pdfDocument.Form.Add(textBox);

            // 5️⃣ Save the modified PDF
            string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
            pdfDocument.Save(outputPath);

            Console.WriteLine("PDF form field created successfully.");
            Console.WriteLine($"Output saved to: {outputPath}");
        }
    }
}
```

**Očekávaný výstup:**  
Spuštění programu vypíše dva potvrzovací řádky do konzole. Otevření `output.pdf` zobrazí textové pole na stránce 2, kde uživatel může zadat komentáře. Když je formulář odeslán (např. pomocí tlačítka „Submit“ v Adobe Acrobat), název pole `Comments` se objeví v exportovaných datech FDF nebo XFDF.

## Běžné varianty a okrajové případy

| Situace | Jak upravit kód |
|-----------|-----------------------|
| **Přidat pole na jinou stránku** | Změňte `pdfDocument.Pages[1]` na požadovaný index stránky (číslování od 0). |
| **Vytvořit víceřádkové textové pole** | Nastavte `textBox.Multiline = true;` před přidáním widgetu. |
| **Nastavit výchozí hodnotu** | Přiřaďte `textBox.Value = "Enter your comments here";`. |
| **Označit pole jako povinné** | Nastavte `textBox.Required = true;`. |
| **Umístit pole na více stránek** | Zavolejte `textBox.AddWidgetAnnotation` pro každý další obdélník na cílových stránkách. |
| **Použít vlastní font** | Načtěte font pomocí `FontRepository.AddFont("path/to/font.ttf")` a odkažte na něj v `DefaultAppearance`. |

**Tip:** Vždy ověřujte souřadnice obdélníku vůči velikosti stránky (`pdfDocument.Pages[1].Rect`). Pokud widget leží mimo okraje stránky, prohlížeče jej mohou oříznout nebo skrýt.

## Testování pole formuláře

1. Otevřete `output.pdf` v Adobe Acrobat Reader.  
2. Klikněte do pole „Comments“; kurzor by se měl objevit.  
3. Zadejte libovolný text a stiskněte **Tab** nebo klikněte mimo pole.  
4. Zvolte **File → Save As** pro uložení zadané hodnoty.  
5. (Volitelné) Použijte API `Form` z Aspose.PDF k programovému získání hodnoty:

```csharp
string commentValue = pdfDocument.Form["Comments"].Value;
Console.WriteLine($"Submitted comment: {commentValue}");
```

Tento úryvek ukazuje, že pole není jen viditelné, ale také lze získat pomocí kódu – což je nezbytné pro server‑side zpracování.

## Závěr

Nyní víte, jak **vytvořit pole formuláře PDF** v C# od začátku až do konce. Tutoriál pokrýval načtení PDF, konfiguraci `TextBoxField`, přidání widget anotace, registraci pole a uložení výsledku. S těmito stavebními kameny můžete **přidat textové pole do PDF** dokumentů, **upravit PDF tak, aby obsahovalo textové pole** a rozšířit přístup i na další typy polí, jako jsou zaškrtávací políčka, přepínače nebo rozbalovací seznamy.

Dále prozkoumejte související témata jako **extrakce dat z formuláře**, **zploštění PDF formulářů** nebo **stylování polí pomocí okrajů a barev**. Každý z těchto konceptů staví na stejném jádru API, které jste právě zvládli, a umožní vám vytvářet sofistikované interaktivní PDF kompletně v C#.

Šťastné kódování a nebojte se experimentovat s různými obdélníky, fonty a validačními pravidly, aby vyhovovaly potřebám vaší aplikace!

## Co se naučíte dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}