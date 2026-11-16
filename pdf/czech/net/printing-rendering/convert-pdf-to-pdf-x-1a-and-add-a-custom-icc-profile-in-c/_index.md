---
category: general
date: 2026-11-16
description: Převést PDF na PDF/X‑1A a přidat vlastní ICC profil v C# pomocí Aspose.PDF.
  Postupujte podle tohoto krok‑za‑krokem průvodce pro spolehlivý tiskový výstup.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert pdf to pdf/x-1a
- add icc profile
- set custom icc profile
language: cs
lastmod: 2026-11-16
og_description: Převod PDF na PDF/X‑1A a vložení vlastního ICC profilu v C#. Tento
  průvodce ukazuje kompletní kód Aspose.PDF a tipy na osvědčené postupy.
og_image_alt: Screenshot of C# code that converts a PDF to PDF/X‑1A while attaching
  an ICC profile
og_title: Převést PDF na PDF/X‑1A a vložit vlastní ICC profil v C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Convert PDF to PDF/X‑1A and add a custom ICC profile in C# using Aspose.PDF.
    Follow this step‑by‑step guide for reliable printing output.
  headline: Convert PDF to PDF/X‑1A and add a custom ICC profile in C#
  type: TechArticle
- description: Convert PDF to PDF/X‑1A and add a custom ICC profile in C# using Aspose.PDF.
    Follow this step‑by‑step guide for reliable printing output.
  name: Convert PDF to PDF/X‑1A and add a custom ICC profile in C#
  steps:
  - name: '**Set PDF/X‑1A conformance** – required for print‑ready files.'
    text: '**Set PDF/X‑1A conformance** – required for print‑ready files.'
  - name: '**Attach the custom ICC profile** – guarantees color fidelity.'
    text: '**Attach the custom ICC profile** – guarantees color fidelity.'
  - name: '**Choose how to reference the profile** – either by file name or via an
      `OutputIntent`.'
    text: '**Choose how to reference the profile** – either by file name or via an
      `OutputIntent`.'
  type: HowTo
tags:
- PDF conversion
- C#
- Aspose.PDF
title: Převést PDF na PDF/X‑1A a přidat vlastní ICC profil v C#
url: /cs/net/printing-rendering/convert-pdf-to-pdf-x-1a-and-add-a-custom-icc-profile-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod PDF na PDF/X‑1A a přidání vlastního ICC profilu v C#

Pokud potřebujete **převést PDF na PDF/X‑1A**, tento návod vám ukáže, jak současně vložit vlastní ICC profil. Tiskařské domy často vyžadují shodu s PDF/X‑1A, protože to zaručuje, že všechny barvy jsou definovány ICC profilem, čímž se eliminují nepříjemná překvapení při tisku. Naučíte se přesný kód pro **přidání ICC profilu** a **nastavení vlastního ICC profilu** pomocí Aspose.PDF pro .NET, plus tipy, jak se vyhnout běžným úskalím.

Návod pokrývá vše od instalace knihovny po validaci výstupního PDF. Nepotřebujete žádnou externí dokumentaci – stačí zkopírovat finální program, upravit cesty k souborům a spustit jej.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
* Visual Studio 2022 (nebo jakékoli C# IDE)
* Licence Aspose.PDF pro .NET nebo dočasný evaluační klíč
* Zdrojové PDF, které chcete převést
* Soubor ICC profilu (např. `FOGRA39.icc`), který odpovídá vašemu tiskovému workflow

You can install Aspose.PDF via NuGet:

```bash
dotnet add package Aspose.Pdf
```

## Krok 1: Instalace Aspose.PDF pro .NET

Balíček NuGet poskytuje jmenný prostor `Aspose.Pdf` a třídu `PdfFormatConversionOptions`, kterou použijeme k **převodu PDF na PDF/X‑1A**. Po dokončení příkazu se balíček objeví v odkazech vašeho projektu.

> **Tip:** Pokud používáte zkušební licenci, zavolejte `License license = new License(); license.SetLicense("Aspose.Pdf.lic");` na začátku `Main`, abyste se vyhnuli vodoznakům z hodnocení.

## Krok 2: Načtení zdrojového PDF

Načtěte PDF, které chcete převést. Třída `Document` načte soubor do paměti, připravený pro konverzi.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class PdfX1AConverter
{
    static void Main()
    {
        // Path to the original PDF
        string sourcePdfPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

        // Load the PDF document
        Document pdfDocument = new Document(sourcePdfPath);
```

Objekt `Document` představuje celé PDF, včetně jeho stránek, fontů a zdrojů. Udržení dokumentu v paměti zajišťuje rychlý průběh konverze.

## Krok 3: Konfigurace možností konverze pro převod PDF na PDF/X‑1A a přidání ICC profilu

Tento krok provádí tři věci:

1. **Nastavit shodu s PDF/X‑1A** – vyžadováno pro soubory připravené k tisku.
2. **Připojit vlastní ICC profil** – zaručuje věrnost barev.
3. **Zvolit způsob odkazování na profil** – buď podle názvu souboru, nebo přes `OutputIntent`.

```csharp
        // -----------------------------------------------------------------
        // 3.1 Create conversion options and request PDF/X‑1A conformance
        // -----------------------------------------------------------------
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions
        {
            // Enforce PDF/X‑1A:2001 compliance
            PdfXConformance = PdfXConformance.PdfX1A2001
        };

        // -----------------------------------------------------------------
        // 3.2 Path to the ICC profile you want to embed
        // -----------------------------------------------------------------
        string iccProfilePath = Path.Combine("YOUR_DIRECTORY", "FOGRA39.icc");

        // -----------------------------------------------------------------
        // 3.3 Option A – set the profile file name directly (simplest)
        // -----------------------------------------------------------------
        conversionOptions.IccProfileFileName = iccProfilePath;

        // -----------------------------------------------------------------
        // 3.4 Option B – set the profile via an OutputIntent (more control)
        // -----------------------------------------------------------------
        OutputIntent outputIntent = new OutputIntent
        {
            DestinationOutputProfile = new FileStreamSource(iccProfilePath)
        };
        conversionOptions.OutputIntents = new[] { outputIntent };

        // You can use either Option A or Option B. Both effectively
        // **set custom ICC profile** for the PDF/X‑1A output.
```

**Proč nastavujeme ICC profil:** PDF/X‑1A vyžaduje jediný výstupní záměr, který definuje barevný prostor. Připojením `FOGRA39.icc` řeknete následným zařízením přesně, jak interpretovat barvy.

**Volba mezi možností A a B:**  
*Možnost A* je stručná a funguje ve většině scénářů.  
*Možnost B* vám poskytuje přístup k celému objektu `OutputIntent`, což umožňuje přidat další metadata (např. slovník `Info`), pokud je potřeba.

## Krok 4: Provedení konverze a ověření výsledku

Now run the conversion and write the PDF/X‑1A file to disk.

```csharp
        // -----------------------------------------------------------------
        // 4.1 Destination path for the PDF/X‑1A file
        // -----------------------------------------------------------------
        string outputPdfPath = Path.Combine("YOUR_DIRECTORY", "output_pdfx1.pdf");

        // -----------------------------------------------------------------
        // 4.2 Convert and save
        // -----------------------------------------------------------------
        pdfDocument.Convert(conversionOptions, outputPdfPath);

        Console.WriteLine($"PDF/X‑1A file saved to: {outputPdfPath}");
    }
}
```

Po dokončení `Convert` soubor `output_pdfx1.pdf` splňuje standard PDF/X‑1A:2001 a obsahuje vložený ICC profil. Shodu můžete ověřit pomocí nástrojů jako **veraPDF** nebo **Adobe Acrobat Preflight**.

> **Tip:** Spusťte `veraPDF` z příkazové řádky po konverzi:  
> `verapdf --format text output_pdfx1.pdf` – vypíše případná porušení shody.

## Časté úskalí a osvědčené postupy

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| **Chybějící ICC soubor** | `FileNotFoundException`, když je cesta špatná | Použijte `Path.Combine` a před přiřazením zkontrolujte `File.Exists` |
| **Špatný barevný prostor** | Zdrojové PDF používá CMYK, ale ICC profil je RGB | Vyberte ICC profil, který odpovídá zdrojovému barevnému prostoru, nebo před vložením převádějte barvy |
| **Neshoda verze PDF** | PDF/X‑1A vyžaduje PDF 1.3; novější PDF mohou obsahovat nepodporované funkce | Aspose.PDF automaticky downgraduje, ale můžete nastavit `PdfVersion` v `PdfFormatConversionOptions`, pokud je to potřeba |
| **Licence nebyla použita** | Ve výstupu se objeví evaluační vodoznaky | Načtěte soubor licence na začátku `Main` |

### Okrajový případ: Převod PDF, které již obsahuje ICC profil

Pokud má zdrojové PDF již výstupní záměr, Aspose.PDF jej nahradí tím, který poskytnete. To je obvykle žádoucí pro tiskovou produkci, ale pokud potřebujete zachovat původní záměr, nejprve načtěte existující kolekci `Document.OutputIntents` a podle potřeby ji sloučte.

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete vložit do nového konzolového projektu. Nahraďte `YOUR_DIRECTORY` skutečnou složkou, která obsahuje `input.pdf` a `FOGRA39.icc`.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Sources;

class PdfX1AConverter
{
    static void Main()
    {
        // Load license (optional for evaluation)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        // 1. Load the source PDF
        string sourcePdfPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
        Document pdfDocument = new Document(sourcePdfPath);

        // 2. Prepare conversion options for PDF/X‑


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Embed ICC profile and convert PDF to PDF/X-1 using Aspose.Pdf](/pdf/english/net/document-conversion/how-to-embed-icc-profile-and-convert-pdf-to-pdf-x-1-with-asp/)
- [Set ICC Profile in PDF/X‑1A Conversion – Complete C# Guide](/pdf/english/net/document-conversion/set-icc-profile-in-pdf-x-1a-conversion-complete-c-guide/)
- [add icc profile and convert PDF to PDF/X‑4 – C# guide](/pdf/english/net/document-conversion/add-icc-profile-and-convert-pdf-to-pdf-x-4-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}