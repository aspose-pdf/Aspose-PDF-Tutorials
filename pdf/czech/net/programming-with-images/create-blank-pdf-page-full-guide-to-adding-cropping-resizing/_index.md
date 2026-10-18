---
category: general
date: 2026-03-27
description: Vytvořte prázdnou stránku PDF a naučte se, jak vytvořit PDF z obrázku,
  přidat obrázek do PDF, oříznout obrázek v PDF a změnit velikost obrázku v PDF pomocí
  Aspose.Pdf v C#.
draft: false
keywords:
- create blank pdf page
- create pdf from image
- add image to pdf
- crop image in pdf
- resize image in pdf
language: cs
og_description: Vytvořte prázdnou stránku PDF a okamžitě přidejte, ořízněte a změňte
  velikost obrázků pomocí Aspose.Pdf. Krok‑za‑krokem C# tutoriál pro vývojáře.
og_title: Vytvořte prázdnou stránku PDF – Přidejte, ořízněte a změňte velikost obrázků
  v C#
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Vytvořte prázdnou stránku PDF – Kompletní průvodce přidáváním, ořezáváním a
  změnou velikosti obrázků
url: /cs/net/programming-with-images/create-blank-pdf-page-full-guide-to-adding-cropping-resizing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prázdné PDF stránky – Kompletní tutoriál v C#

Už jste někdy potřebovali **vytvořit prázdnou PDF stránku** a poté na ni přidat obrázek, ale nebyli jste si jisti, kde začít? Nejste v tom sami. V mnoha reálných aplikacích – například fakturách, produktových katalozích nebo rychlých generátorech reportů – budete potřebovat čisté PDF plátno, vložit obrázek, možná jej oříznout a nakonec upravit jeho velikost.

V tomto průvodci projdeme celý proces: **create PDF from image**, **add image to PDF**, **crop image in PDF** a **resize image in PDF** pomocí knihovny Aspose.Pdf. Na konci budete mít připravený kód, který vytvoří profesionálně vypadající PDF s oříznutým a změněným obrázkem.

---

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.6+). API funguje stejně napříč verzemi, ale nejnovější runtime poskytuje lepší výkon.
- **Aspose.Pdf for .NET** – můžete jej získat z NuGet (`Install-Package Aspose.Pdf`) nebo stáhnout bezplatnou zkušební verzi z oficiální stránky.
- Soubor s obrázkem (JPEG, PNG, atd.) umístěný někde na disku; budeme ho nazývat `input.jpg`.
- Editor kódu – Visual Studio, VS Code nebo Rider – cokoliv, co vám vyhovuje.

> Pro tip: Pokud používáte CI/CD pipeline, přidejte balíček Aspose.Pdf NuGet do souboru projektu, aby build nikdy nezapomněl na závislost.

---

## Krok 1: Vytvoření prázdné PDF stránky

Prvním krokem je vytvořit zcela nový PDF dokument a přidat do něj **prázdnou PDF stránku**. Představte si dokument jako zápisník a stránku jako první list, na který budete psát.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // Step 1: Initialize a fresh PDF document (blank canvas)
        using var pdfDocument = new Document();

        // Step 2: Add a blank page – this is where the image will live
        Page pdfPage = pdfDocument.Pages.Add();

        // (More steps follow...)
```

Proč nejprve přidat stránku? API Aspose očekává objekt stránky, když později umisťujete grafiku. Vynechání tohoto kroku by vyvolalo `NullReferenceException`, protože kam by se mělo kreslit.

---

## Krok 2: Vytvoření PDF z obrázku (volitelný rychlý start)

Pokud chcete jednoduše PDF, které obsahuje *pouze* obrázek – žádný další text, žádné další stránky – Aspose nabízí zkratku. Není to nutné pro hlavní postup, ale je dobré to vědět.

```csharp
// Quick way: convert an image directly to a one‑page PDF
// Comment out if you prefer the manual approach below
pdfDocument.Pages.Add(ImageStreamToPdfPage("YOUR_DIRECTORY/input.jpg"));
```

```csharp
static Page ImageStreamToPdfPage(string imagePath)
{
    var stream = File.OpenRead(imagePath);
    var page = new Page(pdfDocument);
    // The image fills the whole page by default
    page.AddImage(stream, new Rectangle(0, 0, pdfDocument.PageInfo.Width, pdfDocument.PageInfo.Height));
    return page;
}
```

Tento úryvek ukazuje zkratku **create pdf from image**, ale budeme pokračovat ruční metodou, abychom mohli přesně **oříznout** a **změnit velikost**.

---

## Krok 3: Načtení proudu zdrojového obrázku

Nyní otevřeme soubor s obrázkem jako stream. Použití streamu udržuje nízkou spotřebu paměti, zejména u velkých obrázků.

```csharp
        // Step 3: Open the source image file as a read‑only stream
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/input.jpg");
```

Pokud soubor není nalezen, bude vyvolána `FileNotFoundException` – proto zkontrolujte cestu. V produkčním kódu byste to mohli obalit do try‑catch a zaznamenat přátelskou zprávu.

---

## Krok 4: Definování zdrojových a cílových obdélníků (ořez a změna velikosti)

Aspose umožňuje zadat dva obdélníky:

1. **Source rectangle** – část původního obrázku, kterou chcete zachovat.
2. **Destination rectangle** – oblast na PDF stránce, kam bude tato část vykreslena, čímž se řídí konečná velikost.

```csharp
        // Step 4: Set up the area of the image to keep (crop) and its size on the PDF page (resize)
        // Source rectangle – top‑left corner (0,0), width 600px, height 800px
        var sourceRectangle = new Rectangle(0, 0, 600, 800);

        // Destination rectangle – where the cropped piece lands on the page
        // Here we shrink it to half the original dimensions (300x400)
        var destinationRectangle = new Rectangle(0, 0, 300, 400);
```

Proč nepoužít celý obrázek? Protože v mnoha reálných scénářích je potřeba oříznout bílé okraje nebo se zaměřit na logo. Přizpůsobte čísla podle rozměrů vašeho obrázku.

---

## Krok 5: Přidání obrázku do PDF, aplikace ořezu a změny velikosti

S připravenými obdélníky zavoláme `AddImage`. Tento jediný volání provede těžkou práci: extrahuje definovanou část zdrojového obrázku a vykreslí ji na stránku v určené velikosti.

```csharp
        // Step 5: Place the cropped & resized image onto the blank page
        pdfPage.AddImage(imageStream, sourceRectangle, destinationRectangle);
```

Pod kapotou Aspose vytvoří XObject, ořízne jej a v jedné operaci jej škáluje – takže nepotřebujete další knihovny pro zpracování obrázků.

---

## Krok 6: Uložení výsledného PDF

Nakonec dokument uložíme na disk. Soubor `CroppedImage.pdf` bude obsahovat **prázdnou PDF stránku**, kterou jsme vytvořili, nyní ozdobenou pěkně oříznutým a změněným obrázkem.

```csharp
        // Step 6: Write the PDF to the output file
        pdfDocument.Save("YOUR_DIRECTORY/CroppedImage.pdf");
    }
}
```

Když otevřete `CroppedImage.pdf` v libovolném prohlížeči, měli byste vidět jedinou stránku, kde obrázek zabírá levý horní roh, přesně 300 × 400 bodů (≈4 × 5 palců při 72 dpi).  

> **Očekávaný výstup:** PDF s jednou stránkou, obrázek oříznutý na obdélník (0,0,600,800) ze zdroje a zobrazený v poloviční velikosti (300 × 400) na stránce.

---

## Často kladené otázky a okrajové případy

### Co když je můj obrázek menší než zdrojový obdélník?

Aspose automaticky roztažením obrázek přizpůsobí zdrojovému obdélníku, což může vypadat rozmazaně. Aby se tomu předešlo, vypočítejte zdrojový obdélník na základě skutečných rozměrů obrázku:

```csharp
using var img = Image.FromStream(imageStream);
var actualWidth = img.Width;
var actualHeight = img.Height;
var sourceRect = new Rectangle(0, 0, actualWidth, actualHeight);
```

### Jak mohu obrázek umístit jinde na stránce?

Stačí změnit hodnoty X a Y v `destinationRectangle`. Například pro vycentrování obrázku:

```csharp
float pageWidth = pdfPage.PageInfo.Width;
float pageHeight = pdfPage.PageInfo.Height;
float destX = (pageWidth - destinationRectangle.Width) / 2;
float destY = (pageHeight - destinationRectangle.Height) / 2;
var centeredRect = new Rectangle(destX, destY, destinationRectangle.Width, destinationRectangle.Height);
pdfPage.AddImage(imageStream, sourceRectangle, centeredRect);
```

### Chcete přidat více obrázků?

Opakujte **Krok 5** s různými zdrojovými/cílovými obdélníky. Každé volání přidá nový XObject na stejnou stránku, nebo můžete vytvořit další stránky pomocí `pdfDocument.Pages.Add()`.

### Potřebujete výstup ve vysokém rozlišení?

Aspose pracuje v bodech (1 pt = 1/72 palce). Pokud potřebujete 300 dpi, vynásobte požadovanou velikost faktorem 4,2 (300/72) před nastavením cílového obdélníku.

---

## Profesionální tipy pro produkční PDF

- **Dispose properly:** `using` příkazy ve vzorku zajišťují uzavření souborových handle, čímž zabraňují zamčeným souborům ve Windows.
- **Compression:** Před uložením zavolejte `pdfDocument.Compress();`, čímž zmenšíte velikost souboru.
- **Security:** Pokud potřebujete PDF chránit, nastavte `pdfDocument.Encrypt` s uživatelským heslem.
- **Performance:** Pro dávkové zpracování znovu použijte jedinou instanci `Document` a přidávejte stránky ve smyčce – tím snížíte režii.

---

## Úplný funkční příklad (připravený ke kopírování a vložení)

```csharp
using System;
using System.Drawing;          // Needed for Image class (System.Drawing.Common NuGet)
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class CreatePdfWithCroppedImage
{
    static void Main()
    {
        // Initialize a new PDF document (blank canvas)
        using var pdfDocument = new Document();

        // Add a blank page – the surface for our image
        Page pdfPage = pdfDocument.Pages.Add();

        // Load the image file
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/input.jpg");

        // Optional: Adjust source rectangle to actual image size
        using var img = Image.FromStream(imageStream);
        var sourceRectangle = new Rectangle(0, 0, img.Width, img.Height);
        imageStream.Position = 0; // Reset stream after reading size

        // Destination rectangle – half the size, placed at (0,0)
        var destinationRectangle = new Rectangle(0, 0, img.Width / 2, img.Height / 2);

        // Place the cropped (full‑image here) and resized picture onto the page
        pdfPage.AddImage(imageStream, sourceRectangle, destinationRectangle);

        // Save the PDF
        pdfDocument.Save("YOUR_DIRECTORY/CroppedImage.pdf");

        Console.WriteLine("PDF created successfully!");
    }
}
```

> **Poznámka:** Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce na vašem počítači. Výše uvedený kód také ukazuje, jak dynamicky **create pdf from image** načtením skutečných rozměrů obrázku.

---

## Závěr

Právě jsme probrali vše, co potřebujete k **vytvoření prázdné PDF stránky**, následnému **přidání obrázku do PDF**, **oříznutí obrázku v PDF** a **změně velikosti obrázku v PDF** pomocí Aspose.Pdf pro .NET. Úryvek je samostatný, funguje ihned a ukazuje, proč je Aspose solidní volbou pro manipulaci s PDF – žádné externí knihovny pro obrázky, žádné komplikované grafické kontexty.

Dále můžete zkoumat přidávání textových anotací, generování tabulek nebo slučování více PDF dohromady. Všechny tyto úkoly následují stejný vzor: začněte s **prázdnou PDF stránkou**, pak postupně vrstvěte obsah.

Máte nápad, který vás zajímá? Zanechte komentář a pojďme pokračovat v diskusi. Šťastné programování!  

![Create blank PDF page with cropped image using C#](https://example.com/placeholder-image.png "Create blank PDF page with cropped image using C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}