---
category: general
date: 2026-09-18
description: Jak vložit ICC profil při převodu PDF na PDF/X‑1 pomocí Aspose.Pdf. Naučte
  se krok za krokem převod a vkládání ICC profilu v C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed icc
- convert pdf to pdf/x-1
- how to create pdf/x-1
- convert pdf using aspose
language: cs
lastmod: 2026-09-18
og_description: Jak vložit ICC profil při převodu PDF na PDF/X-1 pomocí Aspose.Pdf.
  Sledujte kompletní průvodce v C# pro vytvoření souborů kompatibilních s PDF/X-1.
og_image_alt: Screenshot of Aspose.Pdf conversion to PDF/X-1 with embedded ICC profile
og_title: Jak vložit ICC profil a převést PDF na PDF/X-1 pomocí Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to embed ICC profile while converting PDF to PDF/X-1 using Aspose.Pdf.
    Learn step‑by‑step conversion and ICC embedding in C#.
  headline: How to embed ICC profile and convert PDF to PDF/X-1 with Aspose.Pdf
  type: TechArticle
- description: How to embed ICC profile while converting PDF to PDF/X-1 using Aspose.Pdf.
    Learn step‑by‑step conversion and ICC embedding in C#.
  name: How to embed ICC profile and convert PDF to PDF/X-1 with Aspose.Pdf
  steps:
  - name: '**Load the source PDF** – create a `Document` object.'
    text: '**Load the source PDF** – create a `Document` object.'
  - name: '**Configure conversion options** – tell Aspose which ICC profile to embed
      and set a custom output intent.'
    text: '**Configure conversion options** – tell Aspose which ICC profile to embed
      and set a custom output intent.'
  - name: '**Execute the conversion** – produce a PDF/X‑1‑a file.'
    text: '**Execute the conversion** – produce a PDF/X‑1‑a file.'
  type: HowTo
tags:
- Aspose.Pdf
- ICC profile
- PDF/X-1
- C#
title: Jak vložit ICC profil a převést PDF na PDF/X-1 pomocí Aspose.Pdf
url: /cs/net/document-conversion/how-to-embed-icc-profile-and-convert-pdf-to-pdf-x-1-with-asp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vložit ICC profil a převést PDF na PDF/X-1 pomocí Aspose.Pdf

Pokud potřebujete **how to embed icc** uvnitř PDF a vytvořit soubor splňující normu PDF/X‑1‑a, tento průvodce vám ukáže přesné kroky. Pomocí Aspose.Pdf pro .NET můžete převést běžné PDF na PDF/X‑1 a zároveň vložit vlastní ICC profil, což vyhovuje požadavkům předtiskových workflow s řízením barev.

V tomto tutoriálu se také naučíte **convert pdf to pdf/x-1**, uvidíte **how to create pdf/x-1** dokumenty a objevíte nejlepší postup pro **convert pdf using aspose**. Na konci budete mít připravený PDF/X‑1 soubor připravený k tisku s vloženým ICC profilem.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+)
- Platná licence Aspose.Pdf pro .NET (nebo bezplatná dočasná licence pro testování)
- Vstupní PDF soubor, který chcete převést
- Soubor ICC profilu (např. `FOGRA39.icc`), který odpovídá vašim cílovým tiskovým podmínkám
- Visual Studio 2022 nebo jakýkoli C# editor, který preferujete

> **Tip:** Uchovejte soubor ICC ve stejné složce jako váš zdrojový PDF, aby nedocházelo k chybám souvisejícím s cestou.

## Jak vložit ICC profil a převést PDF na PDF/X-1 pomocí Aspose

Proces konverze se skládá ze tří logických fází:

1. **Načtěte zdrojové PDF** – vytvořte objekt `Document`.
2. **Nastavte možnosti konverze** – sdělte Aspose, který ICC profil vložit, a nastavte vlastní výstupní záměr.
3. **Spusťte konverzi** – vytvořte soubor PDF/X‑1‑a.

Níže je kompletní, spustitelný příklad, který tyto fáze následuje.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

namespace PdfX1Conversion
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the source PDF document
            // -----------------------------------------------------------------
            // Replace "YOUR_DIRECTORY/input.pdf" with the actual path to your PDF.
            var sourcePath = @"YOUR_DIRECTORY/input.pdf";
            var doc = new Document(sourcePath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up conversion options for PDF/X‑1 output
            // -----------------------------------------------------------------
            var conversionOptions = new PdfFormatConversionOptions();

            // 2a️⃣ Embed an external ICC profile (e.g., FOGRA39)
            // The ICC file must be accessible at runtime.
            conversionOptions.IccProfileFileName = @"YOUR_DIRECTORY/FOGRA39.icc";

            // 2b️⃣ Define a custom OutputIntent that describes the ICC profile.
            // This is required by the PDF/X‑1 specification.
            var outputIntent = new OutputIntent
            {
                Info = "Custom ICC Profile – FOGRA39"
            };
            conversionOptions.OutputIntent = outputIntent;

            // -----------------------------------------------------------------
            // 3️⃣ Convert the document to PDF/X‑1 using the configured options
            // -----------------------------------------------------------------
            var outputPath = @"YOUR_DIRECTORY/output_pdfx1.pdf";
            doc.Convert(conversionOptions, PdfFormat.PdfX1);
            doc.Save(outputPath);

            Console.WriteLine($"Conversion complete. PDF/X-1 saved to: {outputPath}");
        }
    }
}
```

### Vysvětlení každého kroku

| Krok | Proč je důležitý |
|------|-------------------|
| **Načtěte zdrojové PDF** | Třída `Document` představuje celý PDF soubor v paměti. Bez načtení souboru nemůžete použít žádné možnosti konverze. |
| **Nastavte `IccProfileFileName`** | Vložení ICC profilu zajišťuje, že následná zařízení (tiskárny, proofingové systémy) interpretují barvy správně. Profil je uložen v výstupním záměru PDF/X‑1. |
| **Vytvořte `OutputIntent`** | PDF/X‑1 vyžaduje slovník *OutputIntent*, který odkazuje na ICC profil. Nastavení `Info` poskytuje lidsky čitelný popis, užitečný pro auditory. |
| **Zavolejte `Convert` s `PdfFormat.PdfX1`** | Tato metoda přepíše strukturu PDF tak, aby odpovídala standardu PDF/X‑1‑a, automaticky zpracovává požadovaná metadata a validaci barevného prostoru. |
| **Uložte výsledek** | Uložení převedeného dokumentu dokončuje workflow. |

## Převod PDF na PDF/X-1 pomocí Aspose.Pdf

Pokud je vaším jediným cílem **convert pdf to pdf/x-1** bez ICC profilu, můžete vynechat vlastnosti související s ICC. Konverze stále ověřuje PDF vůči omezením PDF/X‑1‑a, ale výstupní záměr bude odkazovat na výchozí profil sRGB.

```csharp
var doc = new Document("input.pdf");

// No ICC profile – use default sRGB
var options = new PdfFormatConversionOptions();
doc.Convert(options, PdfFormat.PdfX1);
doc.Save("output_pdfx1_no_icc.pdf");
```

> **Poznámka:** Některé předtiskové služby vyžadují *specifický* ICC profil. Pokud profil vynecháte, soubor může být odmítnut, i když je technicky kompatibilní s PDF/X‑1.

## Jak vytvořit PDF/X-1 kompatibilní dokumenty od nuly

Někdy začínáte s prázdným dokumentem místo existujícího PDF. Stejný konverzní proces se použije – nejprve vytvořte nový `Document`.

```csharp
var doc = new Document();               // Empty PDF
var page = doc.Pages.Add();             // Add a single page

// Add simple text for demonstration
var tf = new TextFragment("Hello PDF/X-1!");
page.Paragraphs.Add(tf);

// Set up conversion options with ICC profile (same as earlier)
var options = new PdfFormatConversionOptions
{
    IccProfileFileName = @"YOUR_DIRECTORY/FOGRA39.icc",
    OutputIntent = new OutputIntent { Info = "FOGRA39 for PDF/X-1" }
};

doc.Convert(options, PdfFormat.PdfX1);
doc.Save("created_pdfx1.pdf");
```

### Okrajové případy a běžné úskalí

| Situace | Na co si dát pozor | Doporučené řešení |
|-----------|-------------------|-----------------|
| **Chybějící ICC soubor** | `FileNotFoundException` za běhu. | Ověřte cestu, použijte `Path.Combine` pro bezpečnost napříč platformami. |
| **Nesprávný barevný prostor** | Aspose může vyhodit `PdfException`, pokud zdrojové PDF obsahuje nepodporované spotové barvy. | Převěďte spotové barvy na procesní barvy před konverzí, nebo použijte `doc.Convert` s `PdfFormat.PdfX1a`, který provádí další konverzi barev. |
| **Velké PDF ( > 200 MB )** | Vysoké využití paměti během konverze. | Použijte `PdfLoadOptions` s `EnableMemoryOptimization = true`. |
| **Licence není aplikována** | Vodoznak „Evaluation Only“ se objeví ve výstupu. | Aplikujte licenci brzy: `License license = new License(); license.SetLicense("Aspose.Pdf.lic");` |

## Ověření konverze a vloženého ICC profilu

Po konverzi můžete programově potvrdit, že ICC profil je přítomen:

```csharp
var resultDoc = new Document("output_pdfx1.pdf");
bool hasIcc = resultDoc.OutputIntents.Count > 0 &&
              resultDoc.OutputIntents[1].IccProfile != null;

Console.WriteLine(hasIcc
    ? "ICC profile successfully embedded."
    : "No ICC profile found.");
```

Alternativně otevřete soubor v Adobe Acrobat **Preflight** nebo nástroji **PDF/X Validation**, abyste viděli zprávu o shodě.

## Závěr

Nyní víte, **how to embed icc** profily při provádění **convert pdf to pdf/x-1** pomocí Aspose.Pdf, a také rozumíte **how to create pdf/x-1** dokumentům od nuly. Kompletní C# příklad zahrnuje načtení PDF, nastavení možností konverze s vlastním ICC profilem, provedení konverze a ověření výsledku.  

Dále můžete prozkoumat:

- **Convert PDF using Aspose** pro jiné rodiny PDF/X (PDF/X‑3, PDF/X‑4)
- Vkládání více výstupních záměrů pro workflow s více profily
- Automatizace hromadných konverzí pomocí `Parallel.ForEach` pro velké tiskové fronty

Neváhejte experimentovat s různými ICC soubory, obsahem stránek a možnostmi konverze PDF/A. Ovládnutí těchto technik zajistí, že vaše PDF splňují přísné požadavky na řízení barev a metadata moderních tiskových řetězců. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vložit a podmnožovat písma v PDF pomocí Aspose.PDF pro .NET – komplexní průvodce](/pdf/english/net/text-operations/embed-subset-fonts-aspose-pdf-net/)
- [Jak převést stránky PDF na obrázky pomocí Aspose.PDF pro .NET (průvodce krok za krokem)](/pdf/english/net/conversion-export/convert-pdf-pages-to-images-aspose-pdf-net/)
- [Jak převést PDF na XML pomocí Aspose.PDF pro .NET: průvodce krok za krokem](/pdf/english/net/conversion-export/pdf-to-xml-conversion-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}