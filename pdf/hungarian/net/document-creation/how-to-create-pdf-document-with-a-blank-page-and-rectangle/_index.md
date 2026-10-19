---
category: general
date: 2026-09-05
description: PDF-dokumentum létrehozása C#-ban egy üres oldal hozzáadásával, egy téglalap
  rajzolásával, és a PDF-fájl mentésével. Kövesse az Aspose.PDF lépésről‑lépésre példáját.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: hu
lastmod: 2026-09-05
og_description: PDF dokumentum létrehozása C#-ban egy üres oldal hozzáadásával, egy
  téglalap rajzolásával, majd a PDF fájl mentésével. Kövesse ezt a teljes példát az
  Aspose.PDF használatával.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: PDF-dokumentum létrehozása üres oldallal és téglalappal – C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Hogyan készítsünk PDF dokumentumot üres oldallal és téglalappal
url: /hu/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF dokumentum létrehozása üres oldallal és téglalappal

Ha programozott módon **PDF dokumentumot** kell létrehoznod, ez az útmutató egy teljes megoldást mutat be C#-ban. Megtanulod, hogyan adj hozzá egy üres oldalt, hogyan rajzolj egy téglalapot az oldalra, és végül hogyan mentsd el a PDF fájlt. A példa az Aspose.PDF könyvtárat használja, amely a .NET 6+ és a .NET Framework 4.5+ verziókkal működik.

Az üres oldal hozzáadása és alakzatok rajzolása gyakori követelmény számlák, bizonyítványok vagy egyedi jelentések esetén. A tutorial végére egy futtatható projekted lesz, amely egy PDF-et hoz létre, amely egyetlen téglalapot tartalmaz, a (100, 100) koordinátán elhelyezve, 200 × 200 pont mérettel.

## Előfeltételek

* Visual Studio 2022 (vagy bármely C# IDE)
* .NET 6 SDK vagy .NET Framework 4.5+
* Aspose.PDF for .NET NuGet csomag  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Írási jogosultság a kimeneti könyvtárban

Nem szükséges további konfiguráció; a kód azonnal futtatható.

## PDF dokumentum létrehozása – áttekintés

A teljes folyamat négy logikai lépésből áll:

1. **Instantiate** egy `Document` objektumot – ez képviseli a PDF fájlt.
2. **Add a blank page** – az oldal egy vásznat biztosít a rajzoláshoz.
3. **Draw a rectangle** – egy `Path` objektum határozza meg az alakzatot.
4. **Save the PDF file** – a dokumentumot lemezre menti.

Minden lépés saját szekcióban van elkülönítve, így szükség szerint újra felhasználhatod vagy cserélheted a részeket.

![Diagram egy PDF-ről, amelyen egy téglalap van egy üres oldalon](https://example.com/placeholder-image.png){.img-fluid alt="Képernyőkép, amely egy PDF dokumentumot mutat, rajzolt téglalappal egy üres oldalon"}

## Üres oldal hozzáadása PDF-hez

Egy PDF-nek legalább egy oldalt kell tartalmaznia, mielőtt bármilyen grafikát elhelyezhetnénk. A `Pages.Add()` metódus egy üres oldalt hoz létre alapértelmezett méretekkel (A4). Ha más méretre van szükséged, adj meg egy `PageSize` argumentumot.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Why this step matters* – A page objektum tartalmazza a szöveg, képek és vektoros grafikák gyűjteményeit. Oldal nélkül bármilyen kísérlet a téglalap hozzáadására kivételt eredményez.

### Szélhelyzet: egyedi oldalméret

Ha az elrendezésed 6 × 9 hüvelykes oldalt igényel, cseréld le az alapértelmezett hívást a következőre:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Téglalap rajzolása PDF-ben

Téglalap rajzolása annyit jelent, hogy létrehozunk egy `Rectangle` geometriát, és egy `Path`-ba ágyazzuk. A `ValidateBounds()` hívás biztosítja, hogy az alakzat a oldal margóin belül maradjon, elkerülve a levágást.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Why this step matters* – A `Path` objektum az alacsony szintű vektoros primitív, amelyet az Aspose.PDF használ. A határok validálásával elkerülheted a futásidejű hibákat, ha a téglalap meghaladja az oldal határait.

### Profi tipp: a téglalap stílusának beállítása

Megváltoztathatod a körvonal színét és a vonalvastagságot:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Ez egy piros körvonalat eredményez 2‑pontos vastagsággal.

## PDF fájl mentése

A dokumentum mentése befejezi a fájl lemezen való létrehozását. A `Save` metódus elfogad egy fájl útvonalat vagy egy stream-et. Abszolút útvonal megadása egyértelművé teszi a helyet, ami hasznos automatizálási szkriptekhez.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Why this step matters* – A mentés az egyetlen pont, ahol a memóriában lévő reprezentáció fizikai fájllá válik. Ha a PDF-et egy web API-ból kell visszaadni, cseréld le a fájl útvonalat egy `MemoryStream`-re.

### Szélhelyzet: meglévő fájlok felülírása

Az Aspose.PDF alapértelmezés szerint felülír egy meglévő fájlt. A korábbi kimenetek védelme érdekében először ellenőrizd, hogy a fájl létezik-e:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Hogyan adjunk hozzá téglalapot – legjobb gyakorlatok

* **Keep coordinates within the page margins** – használd a `ValidateBounds()`-t vagy számold ki a margókat manuálisan.
* **Reuse `GraphInfo` objects** több alakzat rajzolásakor; ez csökkenti a memóriafoglalást.
* **Dispose of the `Document` object** (ahogy a `using var` mutatja) a natív erőforrások gyors felszabadításához.
* **Test with different DPI settings** ha később raszteres képeket ágyazol be; a vektoros alakzatok, például a téglalapok, bármilyen felbontáson élesek maradnak.

## Teljes működő példa

Az alábbiakban a teljes program látható, amelyet egy konzolalkalmazásba másolhatsz. Módosítás nélkül lefordul, és a projekt mappájában `output.pdf`-t hoz létre.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Várt kimenet

A program futtatása egy egyoldalas PDF-et hoz létre. Amikor megnyitod a `output.pdf`-t, egy üres fehér oldalt látsz, amelyen egy piros téglalap található, 100 pont távolságra a bal és az alsó élétől, mérete 200 × 200 pont.

## Összegzés

Most már tudod, hogyan **hozz létre PDF dokumentumot**, **adj hozzá üres oldalt PDF-hez**, **rajzolj téglalapot PDF-ben**, és **mentsd el a PDF fájlt** az Aspose.PDF használatával C#-ban. A példa lefedi a lényeges API hívásokat, elmagyarázza, miért szükséges minden hívás, és tippeket ad a gyakori variációkhoz, például egyedi oldalméretekhez vagy a téglalap stílusához.

Ezután fedezd fel a kapcsolódó témákat, mint a **szöveg hozzáadása**, **képek beágyazása**, vagy **többoldalas jelentések létrehozása**. Ugyanaz a minta – egy `Document` példányosítása, oldalak manipulálása, vektor vagy raszter tartalom hozzáadása, majd `Save` – minden esetben alkalmazható. Nyugodtan kísérletezz különböző alakzatokkal, színekkel és oldalelrendezésekkel, hogy megfeleljenek a projekted igényeinek.

## Mit érdemes következőként megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [PDF dokumentum létrehozása C# – Oldal hozzáadása, téglalap rajzolása és mentés](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [PDF dokumentum létrehozása Aspose.PDF‑vel – Lépésről‑lépésre útmutató](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [PDF dokumentum létrehozása Aspose‑val – Oldal hozzáadása, szövegdoboz és űrlap](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}