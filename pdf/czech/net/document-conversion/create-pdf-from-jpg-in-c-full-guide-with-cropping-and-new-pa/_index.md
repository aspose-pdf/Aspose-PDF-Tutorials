---
category: general
date: 2026-04-06
description: Vytvořte PDF z JPG rychle a naučte se, jak oříznout obrázek v PDF, přidat
  novou stránku PDF a převést JPG na PDF s oříznutím pomocí C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: cs
og_description: Vytvořte PDF z JPG a ořízněte obrázek v PDF pomocí C#. Naučte se,
  jak přidat novou stránku PDF a převést JPG na PDF s oříznutím.
og_title: Vytvořte PDF z JPG v C# – krok za krokem průvodce
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Vytvořte PDF z JPG v C# – Kompletní průvodce s ořezáváním a novými stránkami
url: /cs/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF z JPG v C# – Kompletní průvodce ořezáváním a novými stránkami

Už jste někdy potřebovali **create PDF from JPG**, ale nebyli jste si jisti, jak zachovat jen tu část, kterou skutečně chcete? Nejste v tom sami. V mnoha aplikacích – například fakturách, účtenkách nebo foto‑knihách – vývojáři musí převést obrázek na PDF a zároveň odstranit nežádoucí okraje.  

V tomto tutoriálu projdeme kompletní, připravené řešení, které **creates PDF from JPG**, ukáže vám, jak **crop image in PDF**, a demonstruje **how to add new pdf page**, když potřebujete více než jeden obrázek. Na konci také budete vědět, jak **convert JPG to PDF with crop** a **insert image into PDF C#** pomocí knihovny Aspose.Pdf.

## Co se naučíte

- Nastavit Aspose.Pdf v .NET projektu (není potřeba složitá konfigurace).  
- Načíst JPEG, definovat oblast, kterou chcete zachovat, a oříznout ji při vkládání na stránku PDF.  
- Přidat další stránky do stejného dokumentu, což vám umožní vytvářet multi‑page PDF z mnoha obrázků.  
- Uložit finální soubor a ověřit výstup.  

**Požadavky:** .NET 6+ (nebo .NET Framework 4.6+), Visual Studio 2022 nebo jakýkoli editor, který máte rádi, a odkaz na NuGet balíček `Aspose.Pdf`. Žádné další externí služby nejsou potřeba.

![Create PDF from JPG example](image.jpg){: .align-center alt="Příklad vytvoření PDF z JPG ukazující oříznutý obrázek umístěný na stránce PDF"}

---

## Krok 1: Instalace Aspose.Pdf a příprava projektu

Nejprve přidejte balíček Aspose.Pdf. Otevřete terminál ve složce řešení a spusťte:

```bash
dotnet add package Aspose.Pdf
```

Tento jediný řádek stáhne vše, co potřebujete: třídy `Document`, `Rectangle` a `Page`, které později použijeme. Podle mé zkušenosti je cesta přes NuGet nejčistší způsob, jak zůstat aktuální, aniž byste museli manipulovat s DLL soubory.

> **Tip:** Pokud cílíte na .NET Framework, použijte místo toho balíček `Aspose.Pdf.NET`; rozhraní API je identické.

---

## Krok 2: Načtení JPEG a definování velikosti stránky

Potřebujeme plátno, které odpovídá rozměrům, jež chceme pro finální stránku PDF. Níže uvedený kód vytvoří nový `Document` a otevře zdrojový obrázek jako stream.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Proč obdélník? V Aspose.Pdf představuje `Rectangle` jak rozměry stránky, tak oblast obrázku, kterou chcete zobrazit. Oddělením *stránky* od *ořezové oblasti* získáte detailní kontrolu nad tím, co se objeví v PDF.

---

## Krok 3: Výběr ořezové oblasti (levý horní čtvrt)

Předpokládejme, že potřebujete jen levý horní čtvrt fotografie. Vypočítáme tuto oblast relativně k velikosti stránky:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

`Rectangle` konstruktor přijímá hodnoty **lower‑left X/Y** a **upper‑right X/Y**. Přidáním poloviny výšky k `LLY` posuneme spodní část ořezu nahoru, čímž efektivně odstraníme spodní polovinu obrázku. Pokud potřebujete jinou část, upravte tyto výpočty.

> **Proč ořezávat před přidáním?**  
> Ořezávání na straně PDF zabraňuje vytváření dočasného bitmapového souboru na disku, čímž šetří I/O i paměť. Aspose provede výpočty za vás a výsledek je čisté, vektorové PDF.

---

## Krok 4: Přidání nové stránky a vložení oříznutého obrázku

Nyní skutečně umístíme obrázek na stránku PDF. Zde se ukáže síla klíčového slova **how to add new pdf page**.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` přijímá tři argumenty:

1. **Stream** – zdrojový JPEG.  
2. **Page rectangle** – určuje velikost stránky (náš `pageBounds`).  
3. **Crop rectangle** – říká Aspose, kterou část obrázku vykreslit.

Pokud potřebujete více stránek, jednoduše opakujte vzor `Add` + `AddImage` s novým `imageStream` pokaždé. Tím splníte požadavek **how to add new pdf page** a zároveň udržíte kód přehledný.

---

## Krok 5: Uložení PDF a ověření výsledku

Poslední krok je jednorázový řádek, ale nepodceňujte ho – uložení na správnou cestu zajišťuje, že soubor může otevřít jakýkoli PDF prohlížeč.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

Když otevřete `cropped_image.pdf`, měli byste vidět jedinou stránku, která obsahuje jen levý horní čtvrt původního JPEG, perfektně vycentrovaný na stránce 600 × 800.

---

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Překládá se tak, jak je, za předpokladu, že jste nainstalovali Aspose.Pdf a umístili JPEG na uvedené místo.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Očekávaný výstup

- **Soubor:** `cropped_image.pdf` (≈ 30 KB).  
- **Obsah:** Jedna stránka, 600 × 800 bodů, zobrazující levý horní čtvrt `photo.jpg`.  
- **Chování:** Žádné zkreslení; obrázek si zachovává původní rozlišení v oříznutých mezích.

---

## Často kladené otázky a okrajové případy

### Co když potřebuji zachovat celý obrázek, ne jen čtvrtinu?

Jednoduše nastavte `cropArea` na hodnotu `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Mohu použít jinou velikost stránky (např. A4)?

Určitě. Nahraďte hodnoty `pageBounds` rozměry stránky A4 v bodech (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

Ořezový obdélník může zůstat stejný nebo být přepočítán tak, aby odpovídal novému poměru stran.

### Jak přidám více obrázků, každý na vlastní stránku?

Procházejte kolekci cest k souborům:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### Co transparentnost nebo PNG obrázky?

Aspose.Pdf zachází s PNG stejně jako s JPEG. Pokud má zdroj alfa kanál, PDF jej zachová, pokud verze PDF podporuje transparentnost (výchozí nastavení je v pořádku).

### Funguje to na .NET Core na Linuxu?

Ano. Aspose.Pdf je multiplatformní; stačí zajistit, aby `imageStream` ukazoval na platnou cestu k souboru na cílovém OS. Nepoužívá se žádné Windows‑specifické API.

---

## Tipy a osvědčené postupy

- **Správa paměti:** Vždy obalte streamy do `using` bloků (jak je ukázáno), aby nedocházelo k zamykání souborů.  
- **Výkon:** Pokud zpracováváte desítky obrázků, zvažte opakované použití jedné instance `Document` a volání `pdfDocument.Pages.Add()` pro každý obrázek.  
- **Zpracování chyb:** Celý postup zabalte do `try/catch` bloku a logujte `PdfException` pro ladění.  
- **Kontrola kvality:** Aspose.Pdf umožňuje nastavit rozlišení obrázku pomocí `ImageFragment`. Pro skeny s vysokým DPI nastavte `ImageFragment.Resolution = 300;`.  
- **Bezpečnost:** Pokud bude PDF sdíleno externě, můžete přidat šifrování pomocí `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

## Závěr

Právě jsme probrali, jak **create PDF from JPG** v C#, **crop image in PDF** a **add new PDF page** pro tvorbu vícestránkových dokumentů. Stejný vzor vám umožní **convert JPG to PDF with crop** a **insert image into PDF C#** pro jakýkoli scénář – od jednoduchých účtenek po složité foto‑knihy.  

Vyzkoušejte to: změňte logiku ořezu, experimentujte s A4 stránkami nebo spojte několik obrázků dohromady. Knihovna Aspose.Pdf tyto úkoly učiní bezbolestnými a výše uvedený kód je solidní, citovatelný odkaz, který můžete vložit do libovolného projektu.

### Co dál?

- **Přidat textové anotace** do PDF (např. popisky pod každým obrázkem).  
- **Vytvořit automatický obsah** pro vícestránkové PDF.  
- **Sloučit více PDF** pomocí `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Každé z těchto témat staví na základech, které jste právě zvládli, takže jste dobře připraveni je prozkoumat.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}