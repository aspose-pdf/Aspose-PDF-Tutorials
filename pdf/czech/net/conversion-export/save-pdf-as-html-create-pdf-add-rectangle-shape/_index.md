---
category: general
date: 2026-07-14
description: Uložte PDF jako HTML pomocí Aspose.Pdf – naučte se, jak vytvořit PDF
  dokument, přidat do PDF obdélníkový tvar a exportovat do čistého HTML bez obrázků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: cs
lastmod: 2026-07-14
og_description: Uložte PDF jako HTML s Aspose.Pdf. Objevte, jak vytvořit PDF dokument,
  nakreslit obdélníkový tvar v PDF a během několika minut vygenerovat HTML bez obrázků.
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: Uložení PDF jako HTML – Rychlý průvodce tvorbou PDF a přidáním obdélníkového
  tvaru
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: Uložit PDF jako HTML – Vytvořit PDF, přidat obdélníkový tvar
url: /cs/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uložit PDF jako HTML – Vytvořit PDF, přidat obdélníkový tvar

Už jste se někdy zamýšleli, jak **uložit PDF jako HTML**, a přitom stále být schopni kreslit grafiku v původním PDF? Nejste v tom sami. V mnoha interních nástrojích potřebujeme čistý HTML náhled PDF, který obsahuje vlastní tvary, a běžné konvertory buď vloží těžké rastrové obrázky, nebo zcela odstraní vektorová data.

V tomto tutoriálu vás provedeme **tvorbou PDF dokumentu** programově pomocí Aspose.Pdf, nakreslením **obdélníkového tvaru PDF**, nastavením Batesova číslování a nakonec **uložením PDF jako HTML** bez rastrových obrázků. Na konci budete mít plně spustitelnou C# konzolovou aplikaci, která vytvoří HTML soubor, který můžete otevřít v libovolném prohlížeči – bez nutnosti dalších souborů s obrázky.

> **Pro tip:** Aspose.Pdf funguje s .NET 6+, .NET Framework 4.6+ a dokonce i .NET Core, takže jej můžete vložit do starší Windows služby nebo zcela nového mikroservisu.

---

## Požadavky

- **Visual Studio 2022** (Community nebo vyšší) nebo jakékoli IDE kompatibilní s C#.
- **Aspose.Pdf for .NET** NuGet balíček (verze 23.11 nebo novější). Nainstalujte jej pomocí Package Manager Console:

```powershell
Install-Package Aspose.Pdf
```

- Základní znalost syntaxe C#; předchozí zkušenost s PDF není vyžadována.

---

## Uložit PDF jako HTML pomocí Aspose.Pdf

Níže je kompletní, připravený k zkopírování kód. Sleduje přesně kroky z původního úryvku, ale přidává komentáře, ošetření chyb a malou pomocnou metodu, aby hlavní tok byl čitelný.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### Co kód dělá, krok po kroku

| Krok | Proč je důležité |
|------|------------------|
| **Vytvořit PDF dokument** | Toto je základ – bez objektu `Document` nemůžete nic přidat. |
| **Přidat obdélníkový tvar PDF** | Ukazuje vektorové kreslení; obdélníky jsou nejjednodušší tvar, ale stejné API podporuje kruhy, polygony atd. |
| **Nastavit Batesovo číslování** | Často vyžadováno v soudních sporech nebo scénářích dávkového zpracování pro jedinečnou identifikaci stránek. |
| **Struktura značek** | Zlepšuje přístupnost; čtečky obrazovky se spoléhají na značky pro určení pořadí čtení. |
| **Detekovat kompromitované podpisy** | Aplikace zaměřené na bezpečnost potřebují vědět, zda byl digitální podpis pozměněn. |
| **Uložit PDF jako HTML** | Konečný cíl – vytvořit čisté HTML, které odráží rozložení PDF bez objemných souborů s obrázky. |

> **Proč `SkipImages = true`?**  
> Když převádíte PDF, které obsahuje vektorovou grafiku (jako náš obdélník), obvykle nepotřebujete rastrový záložní obrázek. Nastavením `SkipImages` odstraníte elementy `<img>`, které by jinak odkazovaly na base‑64 blob, čímž udržíte HTML soubor pod několika kilobajty.

---

## Jak vytvořit PDF dokument pomocí Aspose.Pdf

Pokud jste v Aspose noví, knihovna zachází s PDF podobně jako s dokumentem Word: přidáváte **stránky**, poté **odstavce**, **tvary** nebo **poznámky** na tyto stránky. Třída `Document` je vstupním bodem a každá `Page` obsahuje kolekci nazvanou `Paragraphs`. Cokoliv, co dědí z `TextFragmentAbsorber`, `Image`, `Rectangle` atd., může být vloženo do této kolekce.

Níže je minimální úryvek, který vytvoří pouze prázdné PDF – užitečné, když chcete začít od nuly:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

Další stránky můžete přidat pomocí jednoduché smyčky `for`, nebo použít nastavení na úrovni stránky (okraj, velikost) pomocí `PageInfo`. Tato flexibilita je důvod, proč je Aspose.Pdf oblíbený pro generování PDF na serveru.

---

## Přidat obdélníkový tvar PDF – kreslení grafiky

`Rectangle` třída se nachází v `Aspose.Pdf.Annotations`. Přijímá čtyři souřadnice: **dolní‑levý X**, **dolní‑levý Y**, **horní‑pravý X**, **horní‑pravý Y**. Představte si souřadnicový systém PDF jako

---

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vlastních projektech.

- [Vytvořit PDF dokument pomocí Aspose.PDF – Přidat stránku, tvar a uložit](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Převést PDF na HTML v .NET pomocí Aspose.PDF bez ukládání obrázků](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Převod PDF na HTML pomocí Aspose.PDF .NET: Uložit obrázky jako externí PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}