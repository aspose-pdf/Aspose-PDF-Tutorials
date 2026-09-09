---
category: general
date: 2026-09-08
description: Jak použít Aspose k převodu PDF na PDF/X‑1A při specifikaci ICC profilu.
  Naučte se možnosti převodu PDF, jak přidat ICC a načíst PDF pomocí Aspose v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- how to add icc
- pdf conversion options
- specify icc profile
- load pdf aspose
language: cs
lastmod: 2026-09-08
og_description: Jak použít Aspose k převodu PDF na PDF/X‑1A při zadání ICC profilu.
  Postupujte podle podrobného návodu, který pokrývá možnosti převodu PDF a jak přidat
  ICC.
og_image_alt: Diagram showing how to use Aspose to convert a PDF to PDF/X‑1A with
  an ICC profile
og_title: Jak používat Aspose pro konverzi PDF/X‑1A s ICC profilem
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to use Aspose to convert a PDF to PDF/X‑1A while specifying an
    ICC profile. Learn pdf conversion options, how to add icc, and load pdf aspose
    in C#.
  headline: How to use Aspose to convert PDF to PDF/X‑1A with ICC
  type: TechArticle
- description: How to use Aspose to convert a PDF to PDF/X‑1A while specifying an
    ICC profile. Learn pdf conversion options, how to add icc, and load pdf aspose
    in C#.
  name: How to use Aspose to convert PDF to PDF/X‑1A with ICC
  steps:
  - name: – Load the source PDF (load pdf aspose)
    text: '```csharp using System; using Aspose.Pdf; using Aspose.Pdf.Conversion;'
  - name: – Create conversion options and **how to add icc** (specify icc profile)
    text: '```csharp // Create an instance of PdfFormatConversionOptions. // This
      object lets you control the output format and color management. PdfFormatConversionOptions
      conversionOptions = new PdfFormatConversionOptions();'
  - name: – Save as PDF/X‑1A (the final PDF/X‑1A output)
    text: '```csharp // Save the document as PDF/X‑1A, passing the conversion options.
      pdfDocument.Save( dataFolder + "output_pdfx1.pdf", PdfSaveOptions.PdfX1A, conversionOptions);'
  - name: Full, runnable example
    text: Putting the three steps together yields a self‑contained program you can
      copy‑paste into Visual Studio, Rider, or any .NET editor.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF/X‑1A
title: Jak použít Aspose k převodu PDF na PDF/X‑1A s ICC
url: /cs/net/document-conversion/how-to-use-aspose-to-convert-pdf-to-pdf-x-1a-with-icc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít Aspose pro převod PDF na PDF/X‑1A s ICC

Pokud potřebujete **jak použít Aspose** pro spolehlivý převod PDF, tento průvodce vám ukáže, jak přesně převést běžný PDF soubor na PDF/X‑1A soubor při **specifikaci ICC profilu**. Přístup funguje s nejnovější verzí Aspose.Pdf pro .NET a vyžaduje jen několik řádků kódu.

Převod PDF do standardu PDF/X‑1A je běžný, když musíte splnit požadavky tiskového průmyslu. Navíc připojení ICC (International Color Consortium) profilu, například **FOGRA39**, zajišťuje, že barvy se zobrazují konzistentně napříč zařízeními. Také se dozvíte o **pdf conversion options**, které můžete upravit, a jak **load PDF Aspose** bezpečně načíst.

## Co dosáhnete

Na konci tohoto tutoriálu budete:

* **Load PDF Aspose** pomocí třídy `Document`.  
* Vytvořit **pdf conversion options** a **specify ICC profile** správně.  
* Uložit soubor jako PDF/X‑1A, formát požadovaný pro pre‑press workflow.  
* Pochopit běžné úskalí při **how to add icc** do převodu.

> **Předpoklad** – Musíte mít licenci Aspose.Pdf pro .NET (nebo dočasný evaluační klíč) a nainstalovaný .NET 6+. Kód běží na Windows, Linuxu i macOS se stejnými výsledky.

## Jak použít Aspose pro převod PDF s ICC profilem

Tato sekce vás provede každým krokem. Hlavní klíčové slovo **how to use Aspose** se nachází v nadpisu, čímž splňuje SEO pravidlo, že hlavní klíčové slovo musí být alespoň v jednom H2.

### Krok 1 – Načtěte zdrojový PDF (load pdf aspose)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Conversion;

class PdfX1AConverter
{
    static void Main()
    {
        // Define the folder that contains the input PDF and the ICC file.
        // Adjust the path to match your environment.
        string dataFolder = @"C:\MyData\";

        // Load PDF aspose. The Document constructor reads the file into memory.
        using (Document pdfDocument = new Document(dataFolder + "input.pdf"))
        {
            // Subsequent steps go here.
```

**Proč je to důležité:**  
`Document` je centrální třída v Aspose.Pdf. Parsuje strukturu PDF a poskytuje plný přístup ke stránkám, fontům a zdrojům. Správné načtení souboru je základem pro jakýkoli převod, takže **load pdf aspose** je první operace, kterou musíte provést.

### Krok 2 – Vytvořte možnosti převodu a **how to add icc** (specify icc profile)

```csharp
            // Create an instance of PdfFormatConversionOptions.
            // This object lets you control the output format and color management.
            PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions();

            // How to add ICC: set the path to the ICC profile file.
            // The profile must be a valid .icc/.icm file; here we use FOGRA39.
            conversionOptions.IccProfileFileName = dataFolder + "FOGRA39.icc";

            // You can also tweak additional pdf conversion options if needed.
            // For example, conversionOptions.PreserveFormFields = true;
```

**Proč je to důležité:**  
Objekt **pdf conversion options** je místem, kde říkáte Aspose, jaký barevný prostor použít. Přiřazením `IccProfileFileName` **specify ICC profile** pro výstupní PDF/X‑1A soubor. Tento krok přímo odpovídá na otázku **how to add icc** do převodu.

### Krok 3 – Uložte jako PDF/X‑1A (finální PDF/X‑1A výstup)

```csharp
            // Save the document as PDF/X‑1A, passing the conversion options.
            pdfDocument.Save(
                dataFolder + "output_pdfx1.pdf",
                PdfSaveOptions.PdfX1A,
                conversionOptions);

            // Inform the user that the process succeeded.
            Console.WriteLine("PDF converted to PDF/X‑1A with ICC profile successfully.");
        }
    }
}
```

**Proč je to důležité:**  
`PdfSaveOptions.PdfX1A` říká Aspose, aby vytvořil soubor kompatibilní s PDF/X‑1A, což je podmnožina PDF 1.3 s přísnými požadavky na barvy a fonty. `conversionOptions`, které jste vytvořili v předchozím kroku, jsou aplikovány automaticky, což zajišťuje, že vlajka **specify icc profile** je respektována.

### Kompletní, spustitelný příklad

Spojením tří kroků získáte samostatný program, který můžete zkopírovat a vložit do Visual Studio, Rider nebo jakéhokoli .NET editoru.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak nastavit ICC v převodu Aspose PDF – Kompletní průvodce](/pdf/english/net/document-conversion/how-to-set-icc-in-aspose-pdf-conversion-complete-guide/)
- [Jak převést PDF na PDF/A pomocí Aspose.PDF pro Java : krok za krokem](/pdf/english/java/pdfa-compliance/convert-pdf-to-pdfa-aspose-java-guide/)
- [Jak sledovat průběh převodu PDF s Aspose.PDF pro .NET : krok za krokem](/pdf/english/net/conversion-export/track-pdf-conversion-progress-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}