---
category: general
date: 2026-06-08
description: Ořízněte obrázek v PDF pomocí Aspose.PDF v C#. Naučte se, jak vytvořit
  PDF s obrázkem, uložit PDF s obrázkem a přidat obrázek do PDF během několika řádků.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: cs
og_description: Ořízněte obrázek v PDF pomocí Aspose.PDF v C#. Tento tutoriál ukazuje,
  jak vytvořit PDF s obrázkem, uložit PDF s obrázkem a rychle přidat obrázek do PDF.
og_title: Oříznutí obrázku v PDF pomocí Aspose.PDF – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Oříznutí obrázku v PDF pomocí Aspose.PDF – Kompletní průvodce
url: /cs/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Oříznutí obrázku v PDF pomocí Aspose.PDF – Kompletní průvodce

Už jste se někdy zamysleli, jak **crop image in PDF** bez nutnosti otevírat grafický editor? Nejste v tom sami. V mnoha zprávách, fakturách nebo e‑knihách potřebujete jen kousek obrázku – třeba roh loga nebo fragment grafu – a chcete jej přímo v PDF.  

Tento průvodce vám přesně ukáže, jak: **create PDF with image**, **add image to PDF**, a pak **crop image in PDF** pomocí knihovny Aspose.PDF pro C#. Na konci také budete vědět, jak **save PDF with image**, abyste mohli soubor poslat komukoli.

---

## Co budete potřebovat

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+)  
- Licencovaná nebo zkušební kopie **Aspose.PDF for .NET** (nainstalujte přes NuGet `Install-Package Aspose.PDF`)  
- Soubor s obrázkem (JPEG/PNG) na disku – nazveme jej `image.jpg`  
- Jakékoliv IDE, které chcete (Visual Studio, Rider, VS Code)

To je vše. Žádné další služby, žádné externí nástroje.

## Krok 1: Nastavení projektu a importů

Nejprve vytvořte konzolovou aplikaci a přidejte jmenné prostory, které budeme používat. `using` příkazy udržují kód přehledný a usnadňují čtení následujících kroků.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Tip:** Pokud používáte Visual Studio, klikněte pravým tlačítkem na projekt → *Manage NuGet Packages* → vyhledejte “Aspose.PDF” a nainstalujte. Knihovna interně zpracovává jak umístění obrázku, tak ořezávání, takže nebudete potřebovat žádné knihovny třetích stran.

## Krok 2: Vytvoření PDF s obrázkem

Nyní skutečně **create pdf with image**. Následující úryvek vytvoří nový `Document`, přidá prázdnou stránku a připraví proud obrázku.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Spuštěním tohoto kódu získáte PDF s celým obrázkem nataženým na rozměry, které jste zadali. Je to dobrá kontrola před zahájením ořezávání.

## Krok 3: Jak přidat obrázek do PDF (a připravit pro ořezávání)

Pokud již znáte přesnou oblast, kterou chcete, můžete přeskočit krok s plnou velikostí a přejít rovnou k části **how to add image to pdf**. Metoda `AddImage` přijímá tři parametry:

1. **Image stream** – surové bajty vašeho obrázku.  
2. **Placement rectangle** – kde na stránce se obrázek nachází.  
3. **Crop rectangle** – část obrázku, kterou chcete skutečně vykreslit.

Níže je kompaktní verze, která provádí jak umístění **tak** ořezávání v jednom volání.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Proč to funguje:** Aspose.PDF interně mapuje ořezový obdélník na rozměry pixelů obrázku a poté vykreslí jen ten výsek uvnitř oblasti `placement`. Není potřeba žádné další bitmapové zpracování, což znamená, že velikost PDF zůstane malá.

## Krok 4: Jak oříznout obrázek v PDF – Pokročilé možnosti

Občas není dostatečný ořez na čtvrtinu. Možná potřebujete vlastní obdélník nebo chcete zachovat poměr stran obrázku. Zde je flexibilnější přístup:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Řešení okrajových případů:**  
- **Null streams** – vždy zabalte `FileStream` do bloku `using`, jak je ukázáno, aby nedocházelo k únikům.  
- **Large images** – pokud je zdrojový obrázek obrovský, zvažte zmenšení obdélníku `placement`; Aspose automaticky provede downsampling.  
- **Transparent PNGs** – knihovna respektuje alfa kanály, takže ořezaná oblast zachová průhlednost.

## Krok 5: Uložení PDF s obrázkem (a ověření)

Nakonec **save pdf with image**. Metoda `Save` zapíše dokument na disk. Můžete jej také streamovat zpět webovému klientovi, pokud budujete API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Když otevřete `output.pdf`, měli byste vidět pouze ořezanou část `image.jpg` umístěnou přesně tam, kde jste ji definovali. Pokud se obrázek zdá natažený, upravte šířku/výšku obdélníku `placement`, aby odpovídala poměru stran ořezového obdélníku.

## Časté otázky a úskalí

| Otázka | Odpověď |
|----------|--------|
| **Mohu oříznout více obrázků na stejné stránce?** | Ano. Zavolejte `page.AddImage` pro každý obrázek s jeho vlastním obdélníkem umístění a ořezu. |
| **Co když je můj obrázek v jiném formátu (např. BMP)?** | Aspose.PDF podporuje JPEG, PNG, BMP, GIF a TIFF přímo. Stačí změnit příponu souboru. |
| **Potřebuji licenci pro produkční použití?** | Zkušební verze funguje až pro 5 stránek. Pro reálné nasazení zakupte licenci, která odstraní vodoznak. |
| **Jak otočím oříznutý obrázek?** | Po přidání obrázku získejte objekt `Image` a nastavte jeho vlastnost `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **Existuje způsob, jak ořezávat pomocí procent místo absolutních bodů?** | Ano – vypočítejte rozměry obdélníku na základě `image.Width * 0.25` atd., a poté je převěďte na body, jak je ukázáno v Kroku 4. |

## Kompletní funkční příklad (připravený ke zkopírování)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Spusťte program, otevřete `output.pdf` a uvidíte pouze levý horní čtvrtý díl `image.jpg` vykreslený v levém horním rohu stránky. Změňte hodnoty obdélníku `crop` a experimentujte s různými výřezy.

## Závěr

Prošli jsme celý proces **crop image in pdf** pomocí Aspose.PDF pro C#. Začali jsme s novým dokumentem, **create pdf with image**, ukázali **how to add image to pdf**, aplikovali vlastní obdélník **how to crop image pdf** a nakonec **save pdf with image**.  

Nyní můžete vložit přesně oříznuté obrázky do libovolného PDF, které generujete – ideální pro faktury, marketingové brožury nebo automatizované zprávy. Dále můžete zvážit přidání textových popisků (`TextFragment`) nebo kreslení tvarů kolem oříznutého obrázku pro jeho zvýraznění.  

Máte další scénáře, o které máte zájem? Zanechte komentář a šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak nastavit velikost obrázku v PDF pomocí Aspose.PDF pro .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Jak přidat obrázkový razítko do PDF pomocí Aspose.PDF pro .NET&#58; Kompletní průvodce](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Jak extrahovat informace o obrázcích z PDF pomocí Aspose.PDF pro .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}