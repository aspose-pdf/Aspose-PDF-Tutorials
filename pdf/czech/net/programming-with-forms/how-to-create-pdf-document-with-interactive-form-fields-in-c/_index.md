---
category: general
date: 2026-09-27
description: Vytvořte PDF dokument a přidávejte stránky do PDF při vytváření interaktivního
  PDF formuláře. Naučte se, jak přidat textové pole do PDF a vytvořit AcroForm PDF
  pomocí Aspose.Pdf.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add pages to pdf
- create interactive pdf form
- how to add textbox to pdf
- how to create acroform pdf
language: cs
lastmod: 2026-09-27
og_description: Vytvořte PDF dokument a přidejte stránky do PDF při tvorbě interaktivního
  PDF formuláře. Postupujte podle tohoto návodu a naučte se, jak přidat TextBox do
  PDF a vytvořit AcroForm PDF pomocí Aspose.Pdf.
og_image_alt: Screenshot showing a PDF document with a textbox field on two pages
og_title: Vytvořte PDF dokument s interaktivními formulářovými poli – krok za krokem
  průvodce C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  headline: How to create PDF document with interactive form fields in C#
  type: TechArticle
- description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  name: How to create PDF document with interactive form fields in C#
  steps:
  - name: '**Create PDF document** and add the needed pages.'
    text: '**Create PDF document** and add the needed pages.'
  - name: '**Initialize AcroForm** and define a `TextBoxField`.'
    text: '**Initialize AcroForm** and define a `TextBoxField`.'
  - name: '**Add widget annotations** on each page to place the textbox.'
    text: '**Add widget annotations** on each page to place the textbox.'
  - name: '**Save** the document and test the interactive behavior.'
    text: '**Save** the document and test the interactive behavior.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF forms
title: Jak vytvořit PDF dokument s interaktivními formulářovými poli v C#
url: /cs/net/programming-with-forms/how-to-create-pdf-document-with-interactive-form-fields-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit PDF dokument s interaktivními formulářovými poli v C#

Pokud potřebujete **vytvořit PDF dokument**, který obsahuje více stránek a interaktivní formulář, tento průvodce vám přesně ukáže, jak na to. Provedeme vás přidáváním stránek do PDF, vytvořením AcroForm a umístěním pole TextBox na každou stránku pomocí Aspose.Pdf pro .NET.

Na konci budete mít jeden PDF soubor, který umožní uživatelům psát komentáře na obou stránkách. Žádné externí nástroje, jen několik řádků C# a výkonná knihovna Aspose.Pdf.

## Předpoklady

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
* Platná licence Aspose.Pdf pro .NET nebo dočasný evaluační klíč
* Visual Studio 2022 (nebo jakékoli IDE podporující C#)
* Základní znalost syntaxe C# a objektově orientovaných konceptů

> **Tip:** Pokud používáte bezplatnou zkušební verzi, nezapomeňte nastavit objekt `License` brzy ve svém programu, aby se předešlo vodoznakům z hodnocení.

## Krok 1: Nastavení projektu a importování jmenných prostorů

Vytvořte novou konzolovou aplikaci a přidejte NuGet balíček Aspose.Pdf:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
dotnet add package Aspose.Pdf
```

V souboru `Program.cs` importujte požadované jmenné prostory:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Tyto jmenné prostory vám poskytují přístup k základním PDF objektům, typům anotací a třídám formulářových polí potřebných pro tento tutoriál.

## Krok 2: Vytvoření PDF dokumentu a přidání stránek do PDF

Prvním funkčním krokem je **vytvořit PDF dokument** a poté **přidat stránky do PDF**. Každá stránka bude obsahovat stejné pole TextBox.

```csharp
// Initialize a new PDF document
var pdfDocument = new Document();

// Add two blank pages
var firstPage = pdfDocument.Pages.Add();
var secondPage = pdfDocument.Pages.Add();
```

*Proč je to důležité:*  
`Document` představuje celý PDF soubor. Explicitní přidání stránek zajišťuje, že máte plátno pro umístění formulářových widgetů. Můžete přidat libovolný počet stránek; v příkladu jsou použity dvě pro přehlednost.

## Krok 3: Vytvoření interaktivního PDF formuláře (AcroForm)

Interaktivní PDF formulář (**interactive PDF form**) je postaven na objektu AcroForm, který se nachází uvnitř `Document`. Vytvoříme jedno `TextBoxField`, které bude sdíleno na obou stránkách.

```csharp
// Initialize the AcroForm if it doesn't exist
if (!pdfDocument.AcroForm.IsPresent)
{
    pdfDocument.AcroForm = new AcroForm(pdfDocument);
}

// Create a TextBox field named "Comments"
var textBoxField = new TextBoxField(pdfDocument.AcroForm)
{
    Name = "Comments",
    // Optional: set default appearance (font size, color)
    DefaultAppearance = new DefaultAppearance("Helvetica", 12, Color.Black)
};
```

*Proč je to důležité:*  
Kontejner AcroForm obsahuje všechny interaktivní prvky. Vytvořením jednoho `TextBoxField` můžeme znovu použít stejné logické pole na více stránkách, čímž se data synchronizují, když je uživatel vyplní.

## Krok 4: Jak přidat TextBox do PDF – umístění widget anotací

Widget anotace (**widget annotation**) spojuje vizuální obdélník na stránce s logickým formulářovým polem. Přidáme jeden widget na každou stránku.

```csharp
// Widget on the first page (coordinates: lower‑left X,Y – upper‑right X,Y)
var firstPageWidget = new WidgetAnnotation(
    firstPage,
    new Rectangle(50, 700, 200, 750))
{
    Parent = textBoxField,
    // Optional visual properties
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};

// Widget on the second page, positioned slightly lower
var secondPageWidget = new WidgetAnnotation(
    secondPage,
    new Rectangle(50, 600, 200, 650))
{
    Parent = textBoxField,
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};
```

*Proč je to důležité:*  
`WidgetAnnotation` určuje, kde se textbox zobrazí a jak vypadá. Přiřazením stejného `Parent` (`textBoxField`) oba widgety odkazují na stejné podkladové datové pole. Uživatelé, kteří píší do jednoho widgetu, uvidí stejnou hodnotu na druhé stránce.

## Krok 5: Uložení PDF a ověření výsledku

Konečně zapíšete dokument na disk:

```csharp
// Save the PDF to the output folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);

Console.WriteLine($"PDF saved to {outputPath}");
```

Když otevřete `output.pdf` v Adobe Acrobat Readeru:

* Dokument zobrazuje dvě stránky.
* Každá stránka obsahuje textbox označený „Comments“.
* Psaní do textboxu na kterékoliv stránce okamžitě aktualizuje druhý (sdílí stejné jméno pole).

### Očekávaný snímek výstupu

![PDF s textboxem na dvou stránkách](https://example.com/pdf-form-screenshot.png "vytvořit PDF dokument s interaktivními formulářovými poli")

*(Text alt obrázku obsahuje primární klíčové slovo pro přístupnost a SEO.)*

## Běžné varianty a okrajové případy

| Situace | Jak to řešit |
|-----------|------------------|
| **Více než dvě stránky** | Vytvořte další objekty `WidgetAnnotation` pro každou novou stránku a znovu použijte stejný `textBoxField`. |
| **Různá jména polí na stránkách** | Vytvořte samostatné instance `TextBoxField` (např. `CommentsPage1`, `CommentsPage2`) a přiřaďte každému widgetu jeho vlastní rodič. |
| **Víceřádkový textbox** | Nastavte `textBoxField.Multiline = true;` před přidáním widgetů. |
| **Pole jen pro čtení** | Nastavte `textBoxField.ReadOnly = true;` aby se zabránilo úpravám uživatelem. |
| **Vlastní fonty** | Načtěte `TrueTypeFont` a přiřaďte jej pomocí `textBoxField.DefaultAppearance = new DefaultAppearance(font, 12, Color.Black);` |

## Shrnutí krok za krokem (rychlý odkaz)

1. **Vytvořit PDF dokument** a přidat potřebné stránky.  
2. **Inicializovat AcroForm** a definovat `TextBoxField`.  
3. **Přidat widget anotace** na každou stránku pro umístění textboxu.  
4. **Uložit** dokument a otestovat interaktivní chování.

## Další kroky

Nyní, když víte **jak přidat textbox do PDF** a **jak vytvořit AcroForm PDF**, můžete formulář rozšířit:

* Přidejte zaškrtávací políčka, přepínače nebo rozbalovací seznamy pomocí `CheckBoxField`, `RadioButtonField` a `ComboBoxField`.
* Exportujte data formuláře do FDF nebo XFDF pro serverové zpracování.
* Použijte JavaScript akce na pole pro dynamickou validaci.

Prozkoumejte oficiální dokumentaci Aspose.Pdf pro úplný seznam typů formulářových polí a pokročilých možností stylování.

---

*Naučili jste se, jak **vytvořit PDF dokument**, **přidat stránky do PDF**, **vytvořit interaktivní PDF formulář**, **jak přidat textbox do PDF** a **jak vytvořit AcroForm PDF** pomocí stručného, spustitelného příkladu. Klidně experimentujte s dalšími typy polí a úpravami rozvržení, aby vyhovovaly potřebám vaší aplikace.*

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit PDF s Aspose – Přidat formulářové pole a stránky](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Jak přidat Text Box do PDF – Vytvořit PDF formulářové pole a uložit upravený PDF dokument](/pdf/english/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/)
- [Vytvořit PDF dokument s Aspose – Přidat stránku, Text Box a formulář](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}