---
category: general
date: 2026-07-14
description: PDF mentése HTML-ként az Aspose.Pdf segítségével – megtanulhatja, hogyan
  hozzon létre PDF-dokumentumot, adjon hozzá téglalap alakzatot a PDF-hez, és exportálja
  tiszta HTML-be képek nélkül.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: hu
lastmod: 2026-07-14
og_description: Mentse a PDF-et HTML-ként az Aspose.Pdf segítségével. Ismerje meg,
  hogyan hozhat létre PDF-dokumentumot, rajzolhat téglalap alakú PDF-et, és generálhat
  képek nélküli HTML-t percek alatt.
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: PDF mentése HTML-ként – Gyors útmutató PDF létrehozásához és téglalap alakzat
  hozzáadásához
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
title: PDF mentése HTML-ként – PDF létrehozása, téglalap alakzat hozzáadása
url: /hu/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF mentése HTML-ként – PDF létrehozása, téglalap alakzat hozzáadása

Gondolkodtál már azon, hogyan **mentheted a PDF-et HTML-ként**, miközben továbbra is tudsz grafikákat rajzolni az eredeti PDF-re? Nem vagy egyedül. Sok belső eszközben szükségünk van egy tiszta HTML előnézetre egy olyan PDF-ről, amely egyedi alakzatokat tartalmaz, és a szokásos konvertálók vagy nehéz raszteres képeket ágyaznak be, vagy teljesen eltávolítják a vektor adatokat.

Ebben az útmutatóban végigvezetünk a **PDF dokumentum létrehozásának** programozott módon az Aspose.Pdf segítségével, egy **téglalap alakzat PDF** rajzolásán, a Bates-számozás beállításán, és végül a **PDF HTML-ként való mentésén** raszteres képek kihagyásával. A végére egy teljesen futtatható C# konzolalkalmazást kapsz, amely egy HTML fájlt generál, amelyet bármely böngészőben megnyithatsz – további képfájlok nélkül.

> **Pro tipp:** Az Aspose.Pdf működik .NET 6+, .NET Framework 4.6+ és még a .NET Core‑val is, így beillesztheted egy régi Windows szolgáltatásba vagy egy vadonúj mikroszolgáltatásba egyaránt.

---

## Előfeltételek

- **Visual Studio 2022** (Community vagy magasabb) vagy bármely C#‑kompatibilis IDE.  
- **Aspose.Pdf for .NET** NuGet csomag (23.11 vagy újabb). Telepítsd a Package Manager Console‑ból:

```powershell
Install-Package Aspose.Pdf
```

- Alapvető ismeretek a C# szintaxisában; előzetes PDF tapasztalat nem szükséges.

---

## PDF mentése HTML-ként az Aspose.Pdf segítségével

Az alábbiakban a teljes, másolás‑beillesztésre kész kód látható. Pontosan az eredeti részlet lépéseit követi, de megjegyzéseket, hibakezelést és egy kis segédmetódust ad hozzá, hogy a fő folyamat olvasható maradjon.

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

### Mit csinál a kód, lépésről‑lépésre

| Lépés | Miért fontos |
|------|----------------|
| **PDF dokumentum létrehozása** | Ez az alap—`Document` objektum nélkül nem tudsz semmit hozzáadni. |
| **Téglalap alakzat PDF hozzáadása** | Vektoros rajzolást mutat be; a téglalap a legegyszerűbb alakzat, de ugyanaz az API köröket, sokszögeket stb. is támogat. |
| **Bates-számozás beállítása** | Gyakran szükséges peres vagy kötegelt feldolgozási helyzetekben az oldalak egyedi azonosításához. |
| **Címkék struktúrája** | Javítja a hozzáférhetőséget; a képernyőolvasók a címkékre támaszkodnak az olvasási sorrend közvetítéséhez. |
| **Megváltozott aláírások észlelése** | A biztonságra érzékeny alkalmazásoknak tudniuk kell, ha egy digitális aláírást manipuláltak. |
| **PDF mentése HTML-ként** | A végső cél—tiszta HTML előállítása, amely tükrözi a PDF elrendezését nehéz képfájlok nélkül. |

> **Miért `SkipImages = true`?**  
> Amikor egy vektoros grafikákat (például a mi téglalapunkat) tartalmazó PDF-et konvertálsz, általában nincs szükség a raszteres visszaesésre. A `SkipImages` beállítás eltávolítja a `<img>` elemeket, amelyek egyébként base‑64 blobokra hivatkoznának, így az HTML fájl néhány kilobájt alatt marad.

---

## PDF dokumentum létrehozása az Aspose.Pdf segítségével

Ha újonc vagy az Aspose-nál, a könyvtár a PDF-et egy Word dokumentumhoz hasonlóan kezeli: **oldalakat** adsz hozzá, majd **bekezdés**, **alakzat** vagy **annotáció** ezekhez az oldalakhoz. A `Document` osztály a belépési pont, és minden `Page` egy `Paragraphs` nevű gyűjteményt tartalmaz. Bármilyen, a `TextFragmentAbsorber`, `Image`, `Rectangle` stb. osztályból származó elem beilleszthető ebbe a gyűjteménybe.

Az alábbiakban egy minimális kódrészlet látható, amely csak egy üres PDF-et hoz létre – hasznos, ha a semmiből szeretnél kezdeni:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

További oldalakat egyszerű `for` ciklussal láncolhatsz, vagy oldal‑szintű beállításokat (margó, méret) alkalmazhatsz a `PageInfo`‑val. A rugalmasság teszi az Aspose.Pdf‑t kedveltté a szerver‑oldali PDF generálásban.

---

## Téglalap alakzat PDF‑hez – grafika rajzolása

A `Rectangle` osztály a `Aspose.Pdf.Annotations` névtérben található. Négy koordinátát fogad el: **bal‑alsó X**, **bal‑alsó Y**, **jobb‑felső X**, **jobb‑felső Y**. Gondolj a PDF koordináta‑rendszerre úgy, mint

## Mit érdemes még megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészletet tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [PDF dokumentum létrehozása Aspose.PDF‑vel – oldal, alakzat hozzáadása és mentés](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [PDF konvertálása HTML‑re .NET‑ben az Aspose.PDF használatával képek mentése nélkül](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [PDF‑t HTML‑re konvertálás Aspose.PDF .NET&#58; képek mentése külső PNG‑ként](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}