---
category: general
date: 2026-06-08
description: Vytvořte PDF obrázek v C# převodem HEIC na PDF. Naučte se, jak přidat
  obrázek do PDF a vygenerovat PDF z obrázku pomocí krok za krokem kódu.
draft: false
keywords:
- create pdf image
- convert heic to pdf
- add image to pdf
- generate pdf from image
- how to read heic
language: cs
og_description: Vytvořte PDF obrázek v C# převodem HEIC na PDF. Postupujte podle tohoto
  návodu, jak přidat obrázek do PDF a rychle vygenerovat PDF z obrázku.
og_title: Vytvořte PDF obrázek z HEIC – Kompletní C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  headline: Create PDF Image from HEIC – Complete C# Guide
  type: TechArticle
- description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  name: Create PDF Image from HEIC – Complete C# Guide
  steps:
  - name: What if the HEIC file is corrupted?
    text: The `HeicImage.Load` method throws a `HeicException`. Wrap the call in a
      try/catch (as shown) and log the error. In production you might fall back to
      a default placeholder image.
  - name: Can I batch‑process multiple HEIC files?
    text: Absolutely. Just move the core logic into a method like `ConvertHeicToPdf(string
      input, string output)` and iterate over a directory with `Directory.GetFiles("*.heic")`.
  - name: Does this approach preserve EXIF metadata?
    text: No, Aspose.Pdf does not automatically copy EXIF data into the PDF. If you
      need metadata, extract it with `HeicImage.Metadata` and add it to the PDF using
      `Document.Info` properties.
  - name: What about memory usage for huge images?
    text: For images larger than 10 MP, consider down‑sampling before creating `BitmapInfo`.
      You can use `HeicImage.Resize` (if supported) or a third‑party bitmap library
      to reduce dimensions.
  type: HowTo
tags:
- C#
- Aspose.Pdf
- HEIC
- ImageConversion
title: Vytvořte PDF obrázek z HEIC – Kompletní průvodce C#
url: /cs/net/document-creation/create-pdf-image-from-heic-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF obrázku z HEIC – Kompletní průvodce v C#

Už jste se někdy zamysleli, jak **vytvořit PDF obrázek** z HEIC souboru, aniž byste si trhali vlasy? Nejste v tom sami. V mnoha mobilně‑první aplikacích fotoaparát vytváří HEIC, ale starší systémy stále potřebují dobrý starý PDF. Tento tutoriál vám přesně ukáže, jak **převést HEIC na PDF**, přidat obrázek na novou PDF stránku a nakonec **vygenerovat PDF z obrázku** pomocí Aspose.Pdf.

Projdeme každý řádek kódu, vysvětlíme, proč je každá část důležitá, a poskytneme vám připravený příklad ke spuštění. Na konci budete schopni vložit HEIC do složky a získat z něj ostrý PDF – bez potřeby externích nástrojů.

## Co se naučíte

* Jak **číst HEIC** soubory v C# pomocí dekodéru `FileFormat.Heic`.
* Přesné kroky k **převodu HEIC na PDF** s Aspose.Pdf.
* Způsoby, jak **přidat obrázek do PDF** a řídit formát pixelů.
* Tipy pro práci s velkými obrázky a běžné úskalí.
* Kompletní, připravený ke kompilaci program, který můžete zkopírovat a vložit.

*Požadavky*: .NET 6+ (nebo .NET Framework 4.6+), Aspose.Pdf pro .NET a balíček NuGet `FileFormat.Heic`. Pokud jste tyto knihovny ještě nepoužili, nebojte se – instalace je popsána v prvním kroku.

---

## Krok 0: Instalace požadovaných balíčků

Než se ponoříme do kódu, ujistěte se, že jsou v projektu odkázány oba knihovny:

```powershell
dotnet add package Aspose.Pdf
dotnet add package FileFormat.Heic
```

Oba balíčky jsou zdarma pro vývoj a podporují .NET Standard, takže fungují v konzolových aplikacích, ASP.NET nebo dokonce v Unity.

---

## Krok 1: Jak číst HEIC – Načtení souboru jako stream

Čtení HEIC souboru je podobné otevření libovolného binárního souboru, ale potřebujete dekodér, který rozumí kontejneru HEIC. Knihovna `FileFormat.Heic` poskytuje pohodlnou statickou metodu `Load`.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using FileFormat.Heic.Decoder;

// ...

// Open the HEIC file safely with a using block
using (FileStream heicStream = new FileStream(
           @"C:\Images\input.heic", FileMode.Open, FileAccess.Read))
{
    // Decode the HEIC image into a HeicImage object
    HeicImage heicImage = HeicImage.Load(heicStream);
```

**Proč stream?**  
Stream umožňuje dekodéru číst soubor líně, což snižuje zatížení paměti u obrovských obrázků. Příkaz `using` také zaručuje uvolnění souborového handle, čímž předchází chybám zamčení souboru později.

---

## Krok 2: Převod HEIC na PDF – Extrakce pixelových dat

Aspose.Pdf očekává surová bitmapová data, ne objekt HEIC. Proto vytáhneme bajty pixelů ve formátu, který rozumí – `Rgb24` funguje pro většinu případů.

```csharp
    // Grab the raw RGB24 pixel array from the HEIC image
    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);

    // Capture image dimensions for later use
    int width  = (int)heicImage.Width;
    int height = (int)heicImage.Height;
```

**Poznámka k okrajovým případům:** Pokud váš zdrojový HEIC obsahuje alfa kanál, `Rgb24` jej zahodí. Pro průhlednost byste přešli na `Rgba32` a odpovídajícím způsobem upravili `BitmapInfo`.

---

## Krok 3: Přidání obrázku do PDF – Vytvoření objektu Aspose Image

Nyní zabalíme surové bajty do `Aspose.Pdf.Image`. Konstruktor `BitmapInfo` sděluje Aspose stride, velikost a formát pixelů.

```csharp
    // Create an Aspose PDF Image using the pixel buffer
    Image pdfImage = new Image
    {
        BitmapInfo = new BitmapInfo(
            pixelData,
            width,
            height,
            BitmapInfo.PixelFormat.Rgb24)
    };
```

**Profesionální tip:** Pokud plánujete vložit mnoho obrázků do stejného dokumentu, znovu použijte jedinou instanci `Document` a na každé stránce vytvářejte jen nové objekty `Image`. Tím ušetříte režii při vytváření objektů.

---

## Krok 4: Generování PDF z obrázku – Sestavení dokumentu

S připraveným obrázkem vytvoříme nový PDF dokument, přidáme stránku a umístíme na ni obrázek. Kolekce `Paragraphs` od Aspose to dělá triviální.

```csharp
    // Initialize a new PDF document
    Document pdfDoc = new Document();

    // Add a blank page to the document
    Page page = pdfDoc.Pages.Add();

    // Insert the image into the page's paragraph collection
    page.Paragraphs.Add(pdfImage);
```

Pokud potřebujete obrázek umístit (na střed, změnit měřítko atd.), můžete jej zabalit do `ImageStamp` nebo upravit `pdfImage.Margin`. Pro většinu jednorázových konverzí funguje výchozí umístění dobře.

---

## Krok 5: Uložení výsledku – Zapsání PDF na disk

Poslední krok je jednoduše uložit PDF soubor. Aspose podporuje mnoho formátů; zde zůstáváme u klasického `.pdf`.

```csharp
    // Define the output path and save the PDF
    string outputPath = @"C:\Images\output.pdf";
    pdfDoc.Save(outputPath);
}
```

**Očekávaný výstup:** Otevření `output.pdf` v libovolném prohlížeči zobrazí původní HEIC obrázek vykreslený v jeho nativním rozlišení. Žádná ztráta kvality nad rámec původní HEIC komprese.

---

## Kompletní funkční příklad

Níže je kompletní program, který můžete zkopírovat do konzolové aplikace. Obsahuje všechny using direktivy a ošetření chyb pro pocit připravený na produkci.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using FileFormat.Heic.Decoder;

namespace HeicToPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath  = @"C:\Images\input.heic";
            string outputPath = @"C:\Images\output.pdf";

            try
            {
                // 1️⃣ Open the HEIC file as a stream
                using (FileStream heicStream = new FileStream(
                           inputPath, FileMode.Open, FileAccess.Read))
                {
                    // 2️⃣ Load the HEIC image from the stream
                    HeicImage heicImage = HeicImage.Load(heicStream);

                    // 3️⃣ Extract pixel data in RGB24 format
                    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);
                    int width  = (int)heicImage.Width;
                    int height = (int)heicImage.Height;

                    // 4️⃣ Create an Aspose.Pdf.Image using the pixel data
                    Image pdfImage = new Image
                    {
                        BitmapInfo = new BitmapInfo(
                            pixelData,
                            width,
                            height,
                            BitmapInfo.PixelFormat.Rgb24)
                    };

                    // 5️⃣ Add the image to a new PDF page
                    Document pdfDoc = new Document();
                    Page page = pdfDoc.Pages.Add();
                    page.Paragraphs.Add(pdfImage);

                    // 6️⃣ Save the resulting PDF
                    pdfDoc.Save(outputPath);
                }

                Console.WriteLine($"✅ Success! PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Error: {ex.Message}");
            }
        }
    }
}
```

Spusťte program a uvidíte zprávu v konzoli potvrzující vytvoření PDF. Otevřete soubor a obrázek by měl vypadat identicky jako původní HEIC.

---

## Časté otázky a úskalí

### Co když je HEIC soubor poškozený?
Metoda `HeicImage.Load` vyhodí `HeicException`. Zabalte volání do try/catch (jak je ukázáno) a zaznamenejte chybu. V produkci můžete přejít na výchozí zástupný obrázek.

### Můžu hromadně zpracovávat více HEIC souborů?
Určitě. Stačí přesunout hlavní logiku do metody jako `ConvertHeicToPdf(string input, string output)` a iterovat přes adresář pomocí `Directory.GetFiles("*.heic")`.

### Zachovává tento přístup EXIF metadata?
Ne, Aspose.Pdf automaticky nekopíruje EXIF data do PDF. Pokud potřebujete metadata, extrahujte je pomocí `HeicImage.Metadata` a přidejte je do PDF pomocí vlastností `Document.Info`.

### Co s využitím paměti u obrovských obrázků?
U obrázků větších než 10 MP zvažte down‑sampling před vytvořením `BitmapInfo`. Můžete použít `HeicImage.Resize` (pokud je podporováno) nebo knihovnu třetí strany pro bitmapy ke snížení rozměrů.

---

## Závěr

Nyní víte, jak **vytvořit PDF obrázek** ze zdroje HEIC, efektivně **převést HEIC na PDF** a **přidat obrázek do PDF** pomocí Aspose.Pdf v C#. Kroky – čtení HEIC, extrakce pixelových dat, zabalení do PDF obrázku a uložení – jsou jednoduché, ale dostatečně výkonné pro produkční pipeline.

Dále zkuste rozšířit skript: generovat více‑stránkový PDF, kde každá stránka obsahuje jiný HEIC, nebo vložit OCR textové vrstvy pro prohledávatelné PDF. Můžete také prozkoumat další formáty obrázků (`jpeg`, `png`) stejným vzorem, čímž posílíte dovednost **generovat PDF z obrázku**.

Neváhejte experimentovat, sdílet své poznatky nebo klást otázky v komentářích. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak přidat obrázkovou hlavičku do PDF pomocí Aspose.PDF pro .NET&#58; Průvodce krok za krokem](/pdf/english/net/images-graphics/add-image-header-pdf-aspose-dotnet/)
- [Jak přidat obrázkové razítko do PDF pomocí Aspose.PDF pro .NET&#58; Průvodce krok za krokem](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Přidat obrázkové razítko do paty PDF pomocí Aspose.PDF .NET&#58; Průvodce krok za krokem](/pdf/english/net/document-manipulation/add-image-stamp-pdf-footer-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}